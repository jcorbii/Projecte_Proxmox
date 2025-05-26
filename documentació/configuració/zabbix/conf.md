---
title: "Configuració Zabbix"
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

# 9.6 Incorporació d’un *host* al sistema de monitoratge amb Zabbix

## \emoji{desktop-computer} 1. Afegir un host Windows

Per integrar un sistema Windows al monitoratge mitjançant **Zabbix**, cal seguir els següents passos:

1. Accedir a la pàgina oficial de Zabbix i descarregar el **paquet de l’agent Zabbix** corresponent al sistema operatiu:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-138.png}
\end{center}

1. Seleccionar:

   * Sistema operatiu (*Windows*)
   * Versió del servidor Zabbix
   * Tipus de xifrat (si és necessari)
   * Format del paquet

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-139.png}
\end{center}

1. Un cop descarregat l’instal·lador, executar-lo i seguir l’assistent d’instal·lació:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-140.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-141.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-142.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-143.png}
\end{center}

1. Verificar que el **servei de l’agent Zabbix** s’ha iniciat correctament:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-144.png}
\end{center}

1. Finalment, accedir a la interfície web de Zabbix i crear el nou host:

   * Menú: **Monitoring → Hosts → Create Host**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-145.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-146.png}
\end{center}

## \emoji{penguin} 2. Afegir un host Linux

Per monitoritzar un sistema Linux, cal seguir aquests passos:

1. Accedir a la web de Zabbix i seleccionar l’agent corresponent al sistema (en aquest cas, per a **SUSE Linux Enterprise Server - SLES**).

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-147.png}
\end{center}

1. Seguir les instruccions per instal·lar l’agent:

### a. Afegir el repositori oficial de Zabbix:

```bash
rpm -Uvh --nosignature https://repo.zabbix.com/zabbix/7.2/release/sles/15/noarch/zabbix-release-latest-7.2.sles15.noarch.rpm
zypper --gpg-auto-import-keys refresh 'Zabbix Official Repository'
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-148.png}
\end{center}

### b. Instal·lar el paquet de l’agent:

```bash
zypper in zabbix-agent
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-149.png}
\end{center}

### c. Configurar el fitxer de configuració de l’agent:

Modificar el fitxer `/etc/zabbix/zabbix_agentd.conf` per definir:

* `Server=` IP del servidor Zabbix
* `Hostname=` nom del dispositiu

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-150.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-151.png}
\end{center}

### d. Iniciar i habilitar el servei de l’agent:

```bash
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-152.png}
\end{center}

1. Afegir el nou host des de la interfície web del servidor Zabbix:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-153.png}
\end{center}

Un cop afegits els sistemes, apareixeran llistats a l’apartat de *Hosts*:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-154.png}
\end{center}

\emoji{magnifying-glass-tilted-left} Amb aquest procés, tant equips Windows com Linux poden ser incorporats al sistema de monitoratge, permetent la supervisió de mètriques com consum de CPU, ús de memòria, estat dels serveis i molt més, tot centralitzat des del panell de control de Zabbix.