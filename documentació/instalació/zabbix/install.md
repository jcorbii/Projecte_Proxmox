---
title: "Projecte Final de Cicle Superior d'ASIX: Gestió Avançada de Proxmox"
titlepage: true
subtitle: "Jordi Corbí Micó"
lang: es
documentclass: scrartcl
toc-own-page: true
toc-title: Índex
numbersections: false
titlepage-rule-height: 0
titlepage-text-color: "7714C6"
titlepage-background: "../../backgrounds/background5.pdf"
footer-left: IES Jaume II el Just - Projecte ASIX
footer-right: \thepage/\pageref{LastPage}
header-includes:
    - \usepackage{graphicx}
    - \usepackage{lastpage}
    - \usepackage{xltxtra}
    - \usepackage{listings}
    - \usepackage{pdflscape}
    - \usepackage{xcolor,tikz,tcolorbox}
    - \usepackage{emoji}
    - \setemojifont{Twemoji Mozilla}
    - \tcbuselibrary{raster}
    - \definecolor{lightblue}{rgb}{0.68, 0.85, 0.9}
    - \definecolor{ballblue}{rgb}{0.13, 0.67, 0.8}
    - \definecolor{cerulean}{rgb}{0.0, 0.48, 0.65}
    - \definecolor{almond}{rgb}{0.94, 0.87, 0.8}
    - \definecolor{apricot}{rgb}{0.98, 0.81, 0.69}
    - \definecolor{cream}{rgb}{1.0, 0.99, 0.82}
    - \definecolor{coralred}{rgb}{1.0, 0.25, 0.25}
    - \definecolor{byzantium}{rgb}{0.44, 0.16, 0.39}
    - \definecolor{thistle}{rgb}{0.85, 0.75, 0.85}
---

\section*{9. \emoji{bar-chart} Monitoratge Centralitzat amb Zabbix}
\begin{itemize}
  \item 9.1 Què és Zabbix i funcionalitats principals  
  \item 9.2 Justificació de l’elecció de Zabbix front altres solucions (Nagios, Prometheus, Netdata...)  
  \item 9.3 Integració amb la infraestructura virtualitzada de Proxmox VE  
  \item 9.4 Desplegament en Alta Disponibilitat (HA) per garantir la continuïtat del servei  
  \item 9.5 Procés d’instal·lació del servidor Zabbix  
  \item 9.6 Afegeix un host al monitoratge Zabbix  
\end{itemize}

\newpage

## 9. \emoji{bar-chart} Monitoratge Centralitzat amb **Zabbix**

### 1. Descàrrega de Zabbix

Per començar, accedim a la web oficial de Zabbix: [https://www.zabbix.com](https://www.zabbix.com)

Una vegada dins, cal anar a l’apartat **Download Zabbix**, on seleccionarem:

* La **versió** desitjada (en aquest cas, la 7.2)
* El **sistema operatiu** (Debian 12)
* Els **components** (servidor, frontend, agent)
* El tipus de **base de dades** (MySQL/MariaDB)
* El servidor web (Apache)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-127.png}
\end{center}

### 2. Instal·lació i configuració del servidor Zabbix

#### a. Instal·lació del repositori oficial

```bash
wget https://repo.zabbix.com/zabbix/7.2/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.2+debian12_all.deb
dpkg -i zabbix-release_latest_7.2+debian12_all.deb
apt update
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-128.png}
\end{center}

#### b. Instal·lació dels paquets principals

Instal·lem el servidor Zabbix, el frontend web amb Apache, els scripts SQL i l’agent:

```bash
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-129.png}
\end{center}

#### c. Creació de la base de dades

Assegura’t que el servidor de bases de dades (MariaDB o MySQL) està operatiu.

Accedim al client de MySQL per crear la base de dades i l’usuari:

```bash
mysql -uroot -p
```

```sql
CREATE DATABASE zabbix CHARACTER SET utf8mb4 COLLATE utf8mb4_bin;
CREATE USER zabbix@localhost IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON zabbix.* TO zabbix@localhost;
SET GLOBAL log_bin_trust_function_creators = 1;
QUIT;
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-130.png}
\end{center}

#### d. Importació de l’esquema de dades

Des del servidor Zabbix, importem l’esquema i les dades inicials:

```bash
zcat /usr/share/zabbix/sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-131.png}
\end{center}

Després, restaurem el valor per defecte de la directiva `log_bin_trust_function_creators`:

```bash
mysql -uroot -p
```

```sql
SET GLOBAL log_bin_trust_function_creators = 0;
QUIT;
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-132.png}
\end{center}

#### e. Configuració del servidor Zabbix

Editem el fitxer de configuració del servidor `/etc/zabbix/zabbix_server.conf` i establim la contrasenya de la base de dades:

```bash
DBPassword=password
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-133.png}
\end{center}

#### f. Inici dels serveis

Reiniciem els serveis necessaris i els activem perquè s’inicien automàticament amb el sistema:

```bash
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-134.png}
\end{center}

#### g. Accés a la interfície web

Una vegada tot estiga operatiu, podem accedir a la interfície web de Zabbix des del navegador:

```
http://IP_DEL_SERVIDOR/zabbix
```

Des d’ací podrem finalitzar la configuració via web GUI.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-135.png}
\end{center}

Amb això, el servidor Zabbix queda instal·lat i llest per a ser utilitzat per a la monitorització centralitzada de la infraestructura.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-136.png}
\end{center}