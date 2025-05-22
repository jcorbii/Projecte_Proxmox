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

\section*{\emoji{blue-book} Índex del Projecte: Infraestructura Virtualitzada amb \textbf{Proxmox VE}}  
\subsection*{Amb Alta Disponibilitat i Còpia de Seguretat Centralitzada}

\section*{1. \emoji{compass} Introducció}
\begin{itemize}
  \item 1.1 Objectius del projecte  
  \item 1.2 Justificació de l’elecció de Proxmox VE  
  \item 1.3 Abast del projecte  
  \item 1.4 Requisits previs i coneixements necessaris  
\end{itemize}

\section*{2. \emoji{bricks} Anàlisi i Disseny de la Infraestructura}
\begin{itemize}
  \item 2.1 Requisits funcionals i no funcionals  
  \item 2.2 Topologia de xarxa proposada  
  \item 2.3 Maquinari utilitzat  
  \item 2.4 Disseny lògic del clúster Proxmox  
  \item 2.5 Consideracions d’alta disponibilitat i tolerància a fallades  
\end{itemize}

\section*{3. \emoji{desktop-computer} Implementació del Clúster Proxmox}
\begin{itemize}
  \item 3.1 Instal·lació dels nodes Proxmox VE  
  \item 3.2 Configuració del clúster (\texttt{pvecm})  
\end{itemize}

\section*{4. \emoji{jigsaw} Configuració de \textbf{Ceph} com a Emmagatzematge Distribuït}
\begin{itemize}
  \item 4.1 Introducció a Ceph i integració amb Proxmox  
  \item 4.2 Instal·lació i configuració de Ceph al clúster  
  \item 4.3 Creació de pools d’emmagatzematge  
  \item 4.4 Proves de rendiment i replicació  
  \item 4.5 Gestió i monitoratge de Ceph  
\end{itemize}

\section*{5. \emoji{shield} Alta Disponibilitat (\textbf{HA})}
\begin{itemize}
  \item 5.1 Activació del gestor HA en Proxmox  
  \item 5.2 Definició de grups HA  
  \item 5.3 Proves de tolerància a fallades (failover de màquines virtuals)  
  \item 5.4 Casos d’ús i recuperació davant caigudes de nodes  
\end{itemize}

\section*{6. \emoji{floppy-disk} Proxmox Backup Server (\textbf{PBS})}
\begin{itemize}
  \item 6.1 Instal·lació de PBS  
  \item 6.2 Creació del Datastore
  \item 6.3 Integració amb Proxmox VE  
  \item 6.4 Programació de còpies de seguretat  
  \item 6.5 Restauració de màquines virtuals  
  \item 6.6 Estratègia de retenció i rotació de backups  
\end{itemize}

\section*{7. \emoji{busts-in-silhouette} Gestió d’Usuaris i Pools de Recursos}
\begin{itemize}
  \item 7.1 Creació de rols personalitzats i permisos  
  \item 7.2 Definició de pools de recursos  
  \item 7.3 Gestió delegada i multiusuari  
\end{itemize}

\section*{8. \emoji{locked-with-key} Seguretat i Bones Pràctiques}
\begin{itemize}
  \item 8.1 Actualitzacions i pegats de seguretat  
  \item 8.2 Configuració del tallafoc en Proxmox  
  \item 8.3 Còpies de seguretat de la configuració  
  \item 8.4 Bones pràctiques d’administració del clúster  
  \item 8.5 Monitorització del sistema amb \textbf{Netdata}  
\end{itemize}

\section*{9. \emoji{bar-chart} Monitoratge Centralitzat amb Zabbix}
\begin{itemize}
  \item 9.1 Què és Zabbix i funcionalitats principals  
  \item 9.2 Justificació de l’elecció de Zabbix front altres solucions (Nagios, Prometheus, Netdata...)  
  \item 9.3 Integració amb la infraestructura virtualitzada de Proxmox VE  
  \item 9.4 Desplegament en Alta Disponibilitat (HA) per garantir la continuïtat del servei  
  \item 9.5 Procés d’instal·lació del servidor Zabbix  
  \item 9.6 Afegeix un host al monitoratge Zabbix  
\end{itemize}

\section*{10. \emoji{chart-increasing} Conclusions i Valoració Personal}
\begin{itemize}
  \item 10.1 Objectius assolits  
  \item 10.2 Dificultats trobades i solucions adoptades  
  \item 10.3 Possibles millores futures  
  \item 10.4 Valoració tècnica i personal del projecte  
\end{itemize}

\section*{11. \emoji{paperclip} Annexos}
\begin{itemize}
  \item 11.1 Enllaços d’interés i bibliografia  
\end{itemize}

\newpage

## \emoji{pushpin} Descripció

Aquest projecte implementa una **infraestructura virtualitzada** amb **Proxmox VE** per crear un **clúster d’alta disponibilitat** que centralitza la gestió de **màquines virtuals (VMs)** i **contenidors (LXC)**, assegurant escalabilitat, eficiència i tolerància a fallades. Inclou:

- **Clúster Proxmox VE** amb nodes interconnectats.
- **Ceph** per a emmagatzematge distribuït amb replicació de dades.
- **Proxmox Backup Server (PBS)** per a còpies de seguretat centralitzades.
- Configuració d’**Alta Disponibilitat (HA)** per a continuïtat del servei.
- Monitorització amb **Netdata Cloud** per a visibilitat en temps real.
- **Seguretat** amb tallafocs, actualitzacions automàtiques i control d’accés.

Aquest entorn simula escenaris reals, facilitant gestió, protecció de dades i automatització en entorns de producció o educatius.

## \emoji{bricks} Estructura del projecte

```
Projecte_Proxmox/
├── README.md
├── documentació/
│   ├── instalació/
│   │   ├── proxmox/README.md, install.pdf
│   │   ├── proxmox_backup/README.md, install.pdf
│   │   └── zabbix/README.md, install.pdf
│   └── configuració/
│       ├── proxmox/README.md, conf.pdf
│       ├── proxmox_backup/README.md, conf.pdf
│       └── zabbix/README.md, conf.pdf
└── img/
```

## \emoji{page-facing-up} Contingut

- **Documentació/**: Memòria i annexos detallant implementació i configuració.
- **README.md**: Visió general del projecte.

## \emoji{gear} Requisits

- Proxmox VE 8.x
- Proxmox Backup Server
- Maquinari amb suport de virtualització (Intel VT-x o AMD-V)
- Connexió a Internet per a paquets i actualitzacions

## \emoji{blue-book} 1. Introducció

### \emoji{wrench} Què és Proxmox VE?

**Proxmox VE** és una plataforma de virtualització de codi obert basada en Debian, per a gestionar **VMs (KVM)** i **contenidors (LXC)**. Inclou:

- Gestió de clústers i **HA**.
- **Ceph** per a emmagatzematge distribuït.
- **PBS** per a backups eficients.
- Interfície web per a gestió centralitzada.

És una alternativa robusta a VMware vSphere o Microsoft Hyper-V, ideal per a entorns empresarials i acadèmics.

### 1.1 Objectius del projecte

Desplegar un **clúster Proxmox VE** amb tres nodes, integrant **Ceph** per a emmagatzematge distribuït i **PBS** per a còpies de seguretat, assegurant **HA**, escalabilitat i seguretat. Documentar tot el procés per a entorns de producció o educatius.

### \emoji{puzzle-piece} 1.2 Justificació de Proxmox VE

S’ha escollit **Proxmox VE** per ser de codi obert, amb integració nativa de **Ceph** i **PBS**, i per la seva comunitat activa. Comparat amb:

- **VMware vSphere**: Menor cost i més flexibilitat.
- **Microsoft Hyper-V**: Millor en entorns mixtos Linux/Windows.
- **Red Hat Virtualization**: Més senzill i sense subscripcions obligatòries.

### \emoji{compass} 1.3 Abast del projecte

- Desplegament d’un **clúster de 3 nodes** amb Proxmox VE.
- Configuració de **Ceph** per a emmagatzematge distribuït.
- Implementació de **PBS** per a backups automàtics.
- Configuració d’**HA** per a tolerància a fallades.
- Gestió de **seguretat** i permisos.
- Documentació detallada.

### \emoji{compass} 1.4 Requisits previs

- Coneixements en **Linux (Debian)**, **KVM/QEMU**, **LXC** i **Ceph**.
- Habilitats en **CLI**, xarxes (VLANs, ponts) i seguretat (tallafocs, permisos).

## \emoji{bricks} 2. Anàlisi i Disseny

### \emoji{check-mark-button} 2.1 Requisits

**Funcionals**:
- Gestió de VMs i LXC.
- Emmagatzematge distribuït amb Ceph.
- Backups automàtics amb PBS.
- HA per a serveis crítics.

**No funcionals**:
- Escalabilitat, tolerància a fallades, rendiment i interfície web intuïtiva.

### \emoji{globe-with-meridians} 2.2 Topologia de xarxa

Un **servidor físic amb Proxmox VE** allotja VMs que simulen un clúster amb tres nodes i un PBS.

```plaintext
┌─────────────────────────────────────────────────┐
│ Servidor físic Proxmox VE                       │
│ ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────┐ │
│ │ Node 1 VM│↔│ Node 2 VM│↔│ Node 3 VM│ │PBS VM│ │
│ └──────────┘ └──────────┘ └──────────┘ └──────┘ │
└─────────────────────────────────────────────────┘
```

### \emoji{desktop-computer} 2.3 Maquinari

**Nodes 1 i 2**:
- CPU: 16 x Intel Xeon E5-2696 v4 @ 2.20GHz
- RAM: 32 GB DDR4
- Discs: 1x SSD 150 GB (sistema), 2x HDD 100 GB (Ceph)

**Node 3**:
- CPU: 12 x Intel Xeon E5-2696 v4
- RAM: 24 GB DDR4
- Discs: 1x SSD 150 GB, 1x HDD 100 GB (Ceph)

**PBS**:
- CPU: 16 x Intel Xeon E5-2696 v4
- RAM: 32 GB
- Discs: 1x SSD 150 GB, 3x HDD 100 GB (RAID1)

### \emoji{money-bag} 2.3.1 Pressupost estimat

| Component                     | Quantitat | Preu unitari | Subtotal   |
|------------------------------|-----------|--------------|------------|
| Servidors Proxmox (3 nodes)  | 3         | 1.200 €      | 3.600 €    |
| Targetes xarxa + cablejat    | 3         | 100 €        | 300 €      |
| Servidor PBS                 | 1         | 1.100 €      | 1.100 €    |
| Unitat externa (opcional)    | 1         | 300 €        | 300 €      |
| Switch gigabit/10Gb          | 1         | 400 €        | 400 €      |
| SAI                          | 1         | 300 €        | 300 €      |
| Bastidor i accessoris        | 1         | 250 €        | 250 €      |
| **Total**                    |           |              | **6.250 €**|

### \emoji{puzzle-piece} 2.4 Disseny lògic

- **Rols**: Cada node actua com **MON**, **MGR** i **OSD** per a Ceph.
- **Pool RBD**: Emmagatzematge per a VMs i LXC amb replicació.
- **HA**: Migració automàtica de VMs en cas de fallada.
- **Gestió**: Interfície web i CLI (`pvecm`, `ceph`).

### \emoji{shield} 2.5 Alta disponibilitat

- **Corosync**: Sincronització i quòrum del clúster.
- **Ceph**: Replicació de dades (3 còpies).
- **HA**: Reinici automàtic de VMs en nodes actius.
- **PBS**: Backups externs per a recuperació.

## \emoji{puzzle-piece} 4. Configuració de Ceph

**Ceph** ofereix emmagatzematge distribuït amb:

- **OSD**: Emmagatzema dades.
- **MON**: Gestiona l’estat del clúster.
- **MGR**: Monitorització i interfície.

**Integració amb Proxmox**:
- Configuració via **Datacenter → Ceph**.
- Ús de **RBD** per a VMs i LXC.
- Replicació per alta disponibilitat.

## \emoji{shield} 5. Alta Disponibilitat (HA)

**HA** assegura la continuïtat dels serveis mitjançant:
- **Corosync** per a quòrum.
- **Migració automàtica** de VMs.
- Integració amb **Ceph** i **PBS** per a resiliència.

## \emoji{floppy-disk} 6. Proxmox Backup Server (PBS)

**PBS** ofereix:
- Backups **incrementals** i **deduplicats**.
- **Xifratge** opcional.
- Restauracions selectives.
- Integració amb Proxmox VE via protocol optimitzat.

## \emoji{busts-in-silhouette} 7. Gestió d’Usuaris

- **Rols i permisos**: Control granular d’accés.
- **Pools de recursos**: Agrupació de VMs i LXC per a usuaris.
- **Seguretat**: Autenticació LDAP/AD i principis de privilegi mínim.

## \emoji{locked-with-key} 8. Seguretat i Bones Pràctiques

- **Tallafocs** i **actualitzacions automàtiques**.
- **Netdata**: Monitorització en temps real, lleugera i amb gràfics interactius.

| Eina          | Temps real                   | Interfície | Instal·lació | Consum |
|---------------|------------------------------|------------|--------------|--------|
| **Netdata**   | \emoji{heavy-check-mark}     | Moderna    | Fàcil        | Lleuger|
| **Prometheus**| \emoji{cross-mark}           | Grafana    | Complexa     | Alt    |
| **Zabbix**    | \emoji{cross-mark}           | Completa   | Complexa     | Alt    |
| **Nagios**    | \emoji{cross-mark}           | Bàsica     | Complexa     | Lleuger|

**Per què Netdata?** Fàcil, lleuger i en temps real.

## \emoji{bar-chart} 9. Monitoratge amb Zabbix

### 9.1 Què és Zabbix?

Plataforma de monitoratge open source per a sistemes, xarxes i aplicacions, amb alertes i dashboards.

### 9.2 Justificació

- **Integració amb Proxmox**: Plantilles per a nodes i Ceph.
- **Alertes proactives** i visualitzacions potents.
- Més completa que Nagios o Prometheus per a aquest entorn.

### 9.3 Integració

Zabbix, desplegat com a VM amb **HA**, monitoritza nodes i recursos amb agents i SNMP.

## \emoji{brain} 10. Conclusions

### 10.1 Objectius assolits

- Clúster funcional amb **Proxmox VE**, **Ceph** i **PBS**.
- Configuració d’**HA** i seguretat.
- Monitorització amb **Netdata** i **Zabbix**.

### 10.2 Dificultats

- **Repositoris PBS**: Resolt amb repositoris públics.
- **Ceph (redundància)**: Resolt alliberant espai i afegint un OSD.

### 10.3 Millores futures

- **Docker**: Per a més flexibilitat.
- **Seguretat**: TLS, LUKS, LDAP.
- **Xarxa**: VLANs dedicades.

### 10.4 Valoració personal

Projecte complet que ha consolidat coneixements en **virtualització**, **Ceph**, **HA** i **monitoratge**, preparant-me per a reptes professionals.

## \emoji{paperclip} 11. Annexos

### 11.1 Bibliografia

1. [Proxmox VE](https://pve.proxmox.com/wiki/Main_Page)
2. [Debian Wiki](https://wiki.debian.org/)
3. [Projecte GitHub](https://github.com/jcorbii/Projecte_Proxmox/)
4. [Netdata](https://www.netdata.cloud/)
5. [Zabbix](https://www.zabbix.com/)