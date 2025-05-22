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

Aquest projecte es basa en la **implementació d’una infraestructura virtualitzada** mitjançant la plataforma **Proxmox Virtual Environment (Proxmox VE)**. L’objectiu principal és **desplegar un clúster d’alta disponibilitat** que permeta **centralitzar la gestió de màquines virtuals (VMs) i contenidors (LXC)**, garantint alhora escalabilitat, eficiència de recursos i tolerància a fallades.

Per aconseguir-ho, s’ha configurat un entorn complet que inclou:

* Un **clúster de Proxmox VE** amb diversos nodes interconnectats.
* Un sistema d’**emmagatzematge distribuït** mitjançant **Ceph**, per assegurar la replicació de dades i la disponibilitat contínua.
* La integració de **Proxmox Backup Server (PBS)** com a sistema de còpia de seguretat centralitzada i amb retenció intel·ligent.
* La configuració d’**Alta Disponibilitat (HA)** per a la continuïtat del servei en cas de caiguda de nodes.
* La monitorització amb **Netdata Cloud**, per obtindre visibilitat en temps real del rendiment i estat del sistema.
* La implementació de **mecanismes de seguretat**, com tallafocs, actualitzacions automatitzades i control d’accés delegat.

Aquest entorn permet simular escenaris reals d’administració de sistemes, facilitant la gestió dels recursos, la protecció de dades i l’automatització de tasques, tot dins d’un marc tècnic robust i preparat per a la producció o entorns educatius avançats.

## \emoji{bricks} Estructura del projecte

```
Projecte_Proxmox/
└── README.md
│   └── documentació/
│       │ 
│       ├── instalació/
│       │   ├── proxmox/
│       │   │   ├──  README.md
│       │   │   └──  install.pdf
│       │   ├── proxmox_backup/
│       │   │   ├──  README.md
│       │   │   └──  install.pdf
│       │   └── zabbix/
│       │       ├──  README.md
│       │       └──  install.pdf
│       │
│       │
│       └── configuració/
│           ├── proxmox/
│           │   ├──  README.md
│           │   └──  conf.pdf
│           ├── proxmox backup server/
│           │   ├──  README.md
│           │   └──  conf.pdf
│           └── zabbix/
│               ├──  README.md
│               └──  conf.pdf
│
│
├── img/
└──  README.md
```

## \emoji{page-facing-up} Contingut

- **Documentació/**: Conté la memòria del projecte i els annexos amb informació detallada sobre la implementació i configuració.
- **README.md**: Aquest fitxer, que proporciona una visió general del projecte.

## \emoji{gear} Requisits

- Proxmox VE 8.x
- Proxmox Backup Server 
- Maquinari compatible amb virtualització (Intel VT-x o AMD-V)
- Connexió a Internet per a la descàrrega de paquets i actualitzacions

## \emoji{blue-book} 1. Introducció

### \emoji{wrench} **Què és Proxmox VE?**

**Proxmox VE (Virtual Environment)** és una **plataforma de virtualització d'entorns oberts** basada en Debian GNU/Linux, orientada a la creació i gestió de **màquines virtuals (VMs)** i **contenidors (LXCs)** en entorns de producció.

Proxmox VE integra dues tecnologies principals de virtualització:

* **KVM (Kernel-based Virtual Machine):** per a la virtualització completa de sistemes operatius.
* **LXC (Linux Containers):** per a la virtualització lleugera a nivell de sistema operatiu.

A més, incorpora eines avançades com:

* **Gestió de clústers:** permet agrupar múltiples nodes en una sola interfície centralitzada.
* **Alta Disponibilitat (HA):** per a la migració automàtica de VMs/LXCs entre nodes en cas de fallada.
* **Ceph Storage:** sistema d’emmagatzematge distribuït integrat, tolerant a fallades i altament escalable.
* **Proxmox Backup Server (PBS):** per a còpies de seguretat eficients i amb deduplicació.
* **Gestió de xarxes virtuals:** amb VLANs, ponts i interfícies virtuals.
* **Interfície web intuïtiva i potent:** per gestionar tot el sistema des del navegador.

Proxmox VE és una solució de virtualització completa pensada tant per a entorns empresarials com acadèmics, oferint una alternativa robusta, gratuïta i de codi obert a altres plataformes com VMware vSphere o Microsoft Hyper-V.

### 1.1 Objectius del projecte

L’objectiu principal d’aquest projecte és dissenyar, desplegar i documentar una infraestructura virtualitzada d’alta disponibilitat basada en **Proxmox VE**, enfocada tant a la resiliència com a la gestió eficient de recursos. El sistema es construeix sobre un clúster format per **tres nodes físics** que ofereixen serveis de virtualització mitjançant **KVM/QEMU**, amb funcionalitats avançades de gestió centralitzada.

Per garantir la disponibilitat i continuïtat del servei davant possibles fallades, s’integra un sistema d’**emmagatzematge distribuït amb Ceph**, proporcionant replicació automàtica, escalabilitat i tolerància a falles. Aquesta arquitectura permet que les màquines virtuals es puguin migrar dinàmicament entre nodes i continuïn funcionant fins i tot en cas de caiguda parcial de la infraestructura.

Com a part essencial del projecte, es desplega també un **Proxmox Backup Server (PBS)** per gestionar de manera centralitzada les còpies de seguretat, amb una estratègia definida de programació, retenció i restauració eficient de màquines virtuals. Això assegura la recuperació ràpida davant d'incidències, i millora la integritat i seguretat de les dades.

L’objectiu final és demostrar la viabilitat i robustesa d’una solució de virtualització empresarial utilitzant tecnologies de codi obert, tot documentant-ne la planificació, implementació, proves de rendiment i mesures de seguretat, amb una orientació clara a l’escalabilitat, la facilitat de manteniment i l’alt rendiment operatiu.

### \emoji{puzzle-piece} 1.2 Justificació de l’elecció de Proxmox VE

S’ha triat **Proxmox VE (Virtual Environment)** com a plataforma base del projecte per la seua naturalesa de codi obert, la seua gran comunitat, i la capacitat d’oferir una **solució integral de virtualització** sense requerir llicències comercials costoses. Proxmox combina potents tecnologies com **KVM (Kernel-based Virtual Machine)** per a la virtualització completa i **LXC (Linux Containers)** per a la virtualització lleugera, permetent adaptar-se a diversos escenaris d’ús amb eficiència de recursos.

Una de les característiques clau que ha motivat la seua elecció és la **integració nativa amb Ceph**, un sistema d’emmagatzematge distribuït i tolerant a fallades, així com amb **Proxmox Backup Server (PBS)** per gestionar còpies de seguretat de manera centralitzada, incremental i deduplicada. A més, Proxmox ofereix funcionalitats d’**alta disponibilitat (HA)** amb gestió automàtica del reinici de màquines virtuals en cas de caiguda de nodes, així com **clustering** completament integrat mitjançant `pvecm`.

Comparat amb altres plataformes de virtualització, Proxmox destaca per:

* **VMware vSphere**: Tot i ser una de les solucions més madures i utilitzades en entorns corporatius, implica **alts costos de llicenciament**, especialment si es desitja alta disponibilitat, emmagatzematge compartit o automatització amb vCenter. Proxmox, en canvi, ofereix funcionalitats similars sense cost de llicència i amb un model d’assistència opcional.

* **Microsoft Hyper-V**: Encara que està integrat en sistemes Windows Server, la seua gestió resulta **menys flexible en entorns mixtos Linux/Windows** i sovint requereix eines addicionals com System Center per oferir funcionalitats comparables a les de Proxmox. La integració amb Ceph o tecnologies de codi obert és limitada.

* **Red Hat Virtualization (RHV)**: Basat també en KVM, RHV és una plataforma potent, però **requereix subscripcions comercials** i presenta una corba d’aprenentatge més elevada. Proxmox redueix la complexitat i facilita la posada en marxa mitjançant una **interfície web intuïtiva i unificada**, apta fins i tot per a perfils tècnics intermedis.

Finalment, la disponibilitat de **documentació extensa**, suport de la comunitat i la **rapidesa en desplegament** fan de Proxmox VE una opció ideal per a entorns educatius, laboratoris i pimes, sense renunciar a prestacions pròpies d’entorns empresarials. Aquesta versatilitat i autonomia en la gestió de la infraestructura virtual han estat factors decisius per escollir-lo com a tecnologia base del projecte.

### \emoji{compass} 1.3 Abast del Projecte

Aquest projecte abasta de manera integral totes les fases necessàries per al desplegament d’una **infraestructura virtualitzada d’alta disponibilitat**, utilitzant tecnologies de codi obert amb un enfocament pràctic i escalable. La planificació, implementació i documentació cobreixen tant la part física com la lògica del sistema, assegurant un entorn robust, segur i fàcilment administrable.

Les accions principals que formen part de l’abast del projecte són:

* **Disseny i desplegament de tres nodes físics** amb **Proxmox VE**, configurats en mode **clúster** per oferir gestió centralitzada, suport a l’alta disponibilitat i funcionalitats avançades com la migració en viu de màquines virtuals.

* **Integració completa amb Ceph** com a sistema d’**emmagatzematge distribuït**, aprofitant la seua capacitat de replicació, resiliència i escalabilitat per garantir la persistència de les dades i la disponibilitat del servei davant falles de maquinari.

* **Instal·lació i configuració de Proxmox Backup Server (PBS)** per implementar una **estratègia automatitzada de còpies de seguretat**, amb suport per backups incrementals, deduplicació i restauració eficient de màquines virtuals.

* **Definició i aplicació d’una arquitectura d’alta disponibilitat (HA)**, incloent mecanismes de failover automatitzat, agrupació de recursos i comprovacions de tolerància a fallades a nivell de node i emmagatzematge.

* **Configuració de rols, usuaris i polítiques de seguretat**, incloent la gestió d’accés, permisos granulars i monitorització d’activitats, tot garantint la seguretat i el control de l’entorn virtualitzat.

* **Elaboració de documentació tècnica detallada**, incloent manuals d’instal·lació pas a pas, guies d’administració del clúster, procediments de recuperació davant incidències i instruccions d’ús per a usuaris delegats.

Aquest abast garanteix no només la posada en marxa del sistema, sinó també la seua operativitat i manteniment a llarg termini, assegurant la continuïtat del servei i la capacitat de resposta davant imprevistos. A més, s’ha tingut en compte la possibilitat d’escalabilitat futura per afegir nous nodes o serveis al clúster.

### \emoji{compass} 1.4 Requisits Previs i Coneixements Necessaris

Per tal de dur a terme amb èxit aquest projecte d’infraestructura virtualitzada amb alta disponibilitat, és imprescindible disposar d’uns **coneixements previs sòlids** en diverses àrees tècniques relacionades amb sistemes, virtualització i administració de xarxes. Aquests coneixements permeten no només la correcta implementació de les tecnologies involucrades, sinó també la resolució eficient de problemes i l’optimització de l’entorn.

Els requisits tècnics principals inclouen:

* **Administració de sistemes Linux**, especialment en entorns basats en **Debian** (sistema base de Proxmox VE). Es requereix fluïdesa en tasques com gestió de serveis, permisos, xarxes, i l’ús d’eines habituals d’administració.

* **Coneixements de virtualització**, tant en entorns de màquines virtuals amb **KVM/QEMU**, com en **contenidors LXC**, ja que Proxmox VE permet desplegar i gestionar ambdós tipus d’instàncies.

* **Conceptes fonamentals d’emmagatzematge distribuït**, amb especial èmfasi en **Ceph**: arquitectura, tipus de nodes (monitor, OSD, MDS), principis de replicació, pools i gestió de recursos. Tot i que el projecte no requereix una profunditat màxima, sí que és necessari entendre el seu funcionament bàsic per implementar-lo correctament dins d’un clúster.

* **Gestió d’usuaris, rols i permisos**, així com l’aplicació de **polítiques de seguretat**, incloent l’ús de tallafocs (com el propi sistema de Proxmox), accés SSH, autenticació i segregació d’usuaris amb permisos diferenciats.

* **Habilitat amb la línia d’ordres (CLI) en Linux**, especialment per a la configuració directa d’elements com `pvecm`, `ceph`, configuració de xarxes i edició d’arxius com `/etc/network/interfaces`, `/etc/pve/` o fitxers de servei. El projecte combina tant interfície gràfica com administració per consola.

A més, es valora tenir coneixements generals en:

* Xarxes IP (subxarxes, VLANs, ponts de xarxa)
* Monitoratge de sistemes
* Còpies de seguretat i estratègies de retenció

Aquest conjunt de coneixements assegura que l’usuari o equip executor puga afrontar amb autonomia la planificació, el desplegament i la gestió operativa d’una infraestructura virtualitzada basada en Proxmox VE.

## \emoji{bricks} 2. Anàlisi i Disseny de la Infraestructura

L’objectiu d’aquesta secció és definir amb detall els **requisits funcionals i tècnics**, la **topologia de xarxa** i el **disseny lògic** de la infraestructura necessària per desplegar un **clúster Proxmox VE amb alta disponibilitat**, integrant tant un **sistema d’emmagatzematge distribuït Ceph** com una **solució de còpia de seguretat centralitzada amb Proxmox Backup Server (PBS)**.

Aquest apartat proporciona una visió global dels components essencials, establint les bases per a una implementació robusta, escalable i tolerable a fallades. L’arquitectura proposada respon a criteris d’eficiència, resiliència i seguretat, assegurant la continuïtat del servei fins i tot davant de falles parcials del sistema.

Els punts que es desenvolupen en aquesta secció són:

* **2.1 Requisits funcionals i no funcionals**
  Identificació dels objectius tècnics (funcionals) com la creació del clúster, l’alta disponibilitat i la integració de Ceph, així com requisits no funcionals com el rendiment, la seguretat i la facilitat de manteniment del sistema.

* **2.2 Topologia de xarxa proposada**
  Disseny detallat de la infraestructura de xarxa, incloent VLANs si escau, interfícies dedicades per a gestió, sincronització del clúster i tràfic Ceph, garantint una segmentació òptima del tràfic i minimitzant colls d’ampolla.

* **2.3 Maquinari utilitzat**
  Descripció dels nodes físics (CPU, RAM, discs, interfícies de xarxa), així com del maquinari emprat per a la infraestructura de suport (switches, servidor de backups, etc.).

* **2.4 Disseny lògic del clúster Proxmox**
  Explicació de com es configura el clúster a nivell lògic: estructura del *cluster quorum*, configuració dels nodes, agrupació de recursos i distribució de càrregues.

* **2.5 Consideracions d’alta disponibilitat i tolerància a fallades**
  Anàlisi de l’estratègia HA implementada, com la definició de grups HA, la gestió automàtica de reinicis de màquines virtuals i la tolerància davant la pèrdua d’un node o del sistema d’emmagatzematge.

Aquest capítol és fonamental per garantir que el desplegament posterior es realitze sobre una base ben definida, coherent i alineada amb les necessitats del projecte. Un disseny acurat minimitza riscos, facilita la gestió a llarg termini i assegura una millor resposta davant incidències.

### \emoji{check-mark-button} 2.1 Requisits Funcionals i No Funcionals

#### **Requisits funcionals**

* El sistema ha de permetre la creació i gestió de màquines virtuals i contenidors (VM i LXC).
* Ha d’incloure un sistema d’emmagatzematge distribuït (Ceph).
* S’ha de poder realitzar còpies de seguretat automàtiques mitjançant Proxmox Backup Server.
* El clúster ha de suportar alta disponibilitat per a serveis crítics.
* S’ha de poder gestionar usuaris amb permisos delegats.

#### **Requisits no funcionals**

* La infraestructura ha de ser escalable per a afegir nous nodes o recursos.
* Ha de tindre tolerància a fallades sense pèrdua de dades.
* Ha d’oferir un rendiment acceptable amb maquinari limitat.
* El sistema ha de ser administrable mitjançant una interfície gràfica web intuïtiva.

### \emoji{globe-with-meridians} 2.2 Topologia de Xarxa Proposada

> En aquest entorn de pràctiques s’ha desplegat un únic servidor físic amb **Proxmox VE** com a hipervisor principal. Dins d’aquest servidor, s’han creat diverses màquines virtuals que simulen els diferents **nodes d’un clúster**, així com un servidor addicional amb **Proxmox Backup Server (PBS)**.
>
> Aquesta arquitectura permet **reproduir un escenari realista** amb alta disponibilitat, emmagatzematge distribuït (Ceph) i còpies de seguretat centralitzades, però en un entorn virtualitzat controlat i sense necessitat de diversos equips físics.

### \emoji{desktop-computer} Diagrama:

```plaintext
             ┌───────────────────────────────────────────────────────────────────────┐
             │         Servidor físic amb Proxmox VE                                 │
             │                                                                       │
             │   ┌────────────┐   ┌────────────┐   ┌────────────┐   ┌────────────┐   │
             │   │  Node 1 VM │ ←→│  Node 2 VM │ ←→│  Node 3 VM │   │   PBS VM   │   │
             │   └────────────┘   └────────────┘   └────────────┘   └────────────┘   │
             │                                                                       │
             └───────────────────────────────────────────────────────────────────────┘
```

\emoji{wrench} *Tots els nodes i el PBS són màquines virtuals creades dins del mateix host Proxmox VE.*

### \emoji{desktop-computer} 2.3 Maquinari Utilitzat

#### **Nodes del clúster (x2):**

* **CPU:** 16 x Intel(R) Xeon(R) CPU E5-2696 v4 @ 2.20GHz img
* **RAM:** 32 GB DDR4
* **Disc SSD:** 1x 150 GB per a sistema
* **Discos HDD:** 2x 100 GB per a Ceph (OSD)

#### **Nodes del clúster 3:**

* **CPU:** 12 x Intel(R) Xeon(R) CPU E5-2696 v4 @ 2.20GHz 
* **RAM:** 24 GB DDR4
* **Disc SSD:** 1 x 150 GB per a sistema
* **Discos HDD:** 1 x 100 GB per a Ceph (OSD)

#### **Proxmox Backup Server:**

* **CPU:** 16 x Intel(R) Xeon(R) CPU E5-2696 v4 @ 2.20GHz 
* **RAM:** 32 GB
* **Disc SSD:** 1 x 150 GB per al sistema
* **HDD:** 3 x 100 GB RAID1 (datastore de còpies)

### \emoji{money-bag} Pressupost Estimat d’Infraestructura per a Clúster Proxmox amb HA, Ceph i PBS

#### \emoji{desktop-computer} **Nodes del Clúster (x3)**

*Servidors físics amb suport per a virtualització, alta disponibilitat i Ceph*

| Component                                                           | Quantitat | Preu unitari aprox. | Subtotal    |
| ------------------------------------------------------------------- | --------- | ------------------- | ----------- |
| Servidor Proxmox VE (CPU 16 cores, 32-64 GB RAM, SSD + 2x HDD 4 TB) | 3         | 1.200 €             | 3.600 €     |
| Targetes de xarxa addicionals (1/10 Gb) + cablejat                  | 3         | 100 €               | 300 €       |
| **Subtotal nodes del clúster**                                      |           |                     | **3.900 €** |

#### \emoji{floppy-disk} **Servidor de Proxmox Backup Server (PBS)**

*Servidor dedicat per a còpies de seguretat amb alta capacitat i fiabilitat*

| Component                                                       | Quantitat | Preu unitari aprox. | Subtotal    |
| --------------------------------------------------------------- | --------- | ------------------- | ----------- |
| Servidor PBS (CPU 16 cores, 32 GB RAM, SSD + 3x HDD 4 TB RAID)  | 1         | 1.100 €             | 1.100 €     |
| Unitat externa d'emmagatzematge (opcional per backups off-site) | 1         | 300 €               | 300 €       |
| **Subtotal PBS**                                                |           |                     | **1.400 €** |

#### \emoji{globe-with-meridians} **Infraestructura de Xarxa i Accessoris**

| Component                                  | Quantitat | Preu unitari aprox. | Subtotal  |
| ------------------------------------------ | --------- | ------------------- | --------- |
| Switch gestionable gigabit/10Gb            | 1         | 400 €               | 400 €     |
| SAI (Sistema d’alimentació ininterrompuda) | 1         | 300 €               | 300 €     |
| Bastidor (rack) i accessoris               | 1         | 250 €               | 250 €     |
| **Subtotal xarxa/accessoris**              |           |                     | **950 €** |

### \emoji{page-facing-up} **Total Pressupost Estimat**

| Part                            | Cost aproximat |
| ------------------------------- | -------------- |
| Nodes del clúster (x3)          | 3.900 €        |
| Proxmox Backup Server (PBS)     | 1.400 €        |
| Infraestructura de xarxa i rack | 950 €          |
| **TOTAL GENERAL**               | **\~6.250 €**  |

### \emoji{receipt} Notes finals:

* Els preus inclouen maquinari amb capacitat real per executar entorns Ceph i HA amb garantia de rendiment.
* Es poden reduir costos amb equips refurbished o d’ocasió, però aquest pressupost reflecteix una configuració professional i realista.
* No s’han inclòs llicències comercials opcionals de Proxmox (el programari és lliure, però el suport és de pagament si es desitja).

### \emoji{puzzle-piece} 2.4 Disseny Lògic del Clúster Proxmox

El disseny lògic del clúster està orientat a garantir **alta disponibilitat, rendiment i escalabilitat**, aprofitant les funcionalitats natives de **Proxmox VE** i la seua integració directa amb **Ceph** com a plataforma d’emmagatzematge distribuït.

El clúster estarà compost per **tres nodes físics** amb Proxmox VE, cadascun dels quals assumeix rols crítics dins de la infraestructura:

* **Rols assignats per node:**

  * Cada node actuarà simultàniament com a **MON (Monitor)** per al manteniment del consens i del mapa del clúster Ceph.
  * Tindran també el rol de **MGR (Manager)** per facilitar el monitoratge i la interfície d’administració del Ceph.
  * A més, exerciran com a **OSD (Object Storage Daemon)**, aprofitant discos dedicats per oferir emmagatzematge distribuït i replicat entre nodes.

Aquest model distribuït assegura que el clúster siga funcional i operatiu fins i tot si un dels nodes queda fora de servei, mantenint el **quòrum** necessari tant per a Ceph com per al propi clúster de Proxmox.

* **Pool d’emmagatzematge:**

  * Es crearà un **pool de tipus Ceph RBD (RADOS Block Device)**, destinat específicament a allotjar màquines virtuals i contenidors. Aquest pool garanteix redundància mitjançant rèpliques i ofereix accés ràpid i distribuït a les dades.

* **Alta disponibilitat (HA):**

  * Les màquines virtuals considerades crítiques es configuraran amb **HA**, de manera que, en cas de fallada d’un node, aquestes es reinicien automàticament en un altre node disponible sense intervenció manual.
  * Es definiran regles de preferència i prioritat per optimitzar la distribució de càrrega i garantir la resposta immediata davant d’incidències.

* **Gestió centralitzada:**

  * L’administració del clúster es durà a terme mitjançant la **interfície web integrada de Proxmox VE**, que permet la gestió completa de nodes, màquines virtuals, recursos, backups i emmagatzematge, tot des d’un únic punt d’accés.
  * A més, es mantindrà accés per línia d’ordres (`pvecm`, `ceph`, `qm`, etc.) per a tasques avançades o scripts d’automatització.

Aquest disseny garanteix un **entorn equilibrat, resilient i fàcil de gestionar**, optimitzat per a oferir serveis ininterromputs, adaptable a l’escalat futur i alineat amb les millors pràctiques de virtualització en entorns empresarials.

### \emoji{shield} 2.5 Consideracions d’Alta Disponibilitat i Tolerància a Fallades

L’arquitectura proposada ha estat dissenyada per oferir **alta disponibilitat (HA)** i **tolerància a fallades**, garantint així la continuïtat dels serveis virtualitzats davant de caigudes parcials del sistema. La combinació de tecnologies com **Proxmox VE, Ceph i Proxmox Backup Server (PBS)** permet una resposta automàtica, eficient i segura davant incidències crítiques.

Els principals mecanismes de disponibilitat són:

* **Corosync per a comunicació i manteniment del quòrum:**
  El sistema utilitza **Corosync** per sincronitzar l’estat dels nodes i mantenir el **quòrum** del clúster. Aquest protocol de missatgeria distribuïda detecta falles de nodes i pren decisions de gestió segons la disponibilitat dels membres del clúster.

* **Ceph com a emmagatzematge replicat i tolerant a fallades:**
  Ceph replica automàticament les dades entre múltiples **OSDs** distribuïts als tres nodes. Aquesta replicació (amb un mínim de 3 còpies per objecte) assegura que, en cas de fallada d’un disc o node, no es perd informació i es manté la integritat del sistema.

* **Mòdul HA integrat en Proxmox VE:**
  El subsistema HA permet definir **grups d’alta disponibilitat** per a màquines virtuals i contenidors crítics. Si un node falla, el mòdul HA **migra o reinicia automàticament** les màquines afectades en un altre node actiu del clúster, minimitzant el temps d’inactivitat.

* **Estructura amb 3 nodes per mantenir el clúster operatiu amb fallada d’un node:**
  El disseny amb **tres nodes físics** assegura que es mantinga el **quòrum majoritari (2 de 3)** fins i tot si un node deixa de funcionar. Això permet continuar operant amb normalitat i evitar situacions de *split-brain* o inconsistències.

* **Servidor de còpies de seguretat fora del clúster:**
  El **Proxmox Backup Server** s’instal·la en un host separat del clúster per garantir una **còpia externa segura** de totes les màquines virtuals i configuracions. En cas de fallada catastròfica del clúster, aquest servidor permet recuperar ràpidament l’estat del sistema sense dependre de la infraestructura fallida.

Aquesta estratègia global d’alta disponibilitat i resiliència proporciona un entorn fiable i apte per a entorns de producció, minimitzant tant els riscos de pèrdua de dades com els temps d’interrupció dels serveis.

# 4. \emoji{puzzle-piece} Configuració de Ceph com a Emmagatzematge Distribuït

### \emoji{brain} 4.1 Introducció a **Ceph** i Integració amb **Proxmox VE**

**Ceph** és una plataforma d’emmagatzematge distribuït de codi obert dissenyada per oferir alta disponibilitat, escalabilitat i rendiment, sense punts únics de fallada. El seu funcionament es basa en tres components principals:

* **OSD (Object Storage Daemon):** Gestiona el disc dur on s’emmagatzema la informació.
* **MON (Monitor):** Controla l’estat del clúster, manté el mapa del clúster i garanteix el consens entre nodes.
* **MGR (Manager):** Proporciona funcionalitats addicionals de monitoratge i interfície web.

Ceph permet oferir emmagatzematge per a:

* Màquines virtuals (amb RBD – Rados Block Device)
* Sistemes d’arxius (CephFS)
* Objectes (compatible amb S3)

Els **pools d’emmagatzematge** són una part fonamental en l’arquitectura de **Ceph**, ja que representen els espais lògics on es distribueixen les dades entre els diferents OSDs del clúster. A cada pool se li pot assignar una funció específica, com ara allotjar màquines virtuals, contenidors o fitxers de CephFS.

### \emoji{magnifying-glass-tilted-left} Què és un Pool?

Un **pool** és una agrupació lògica d’objectes dins del clúster Ceph. Cada objecte dins d’un pool es reparteix entre els OSDs segons una política de distribució definida, garantint així la replicació i la tolerància a fallades.

#### \emoji{link} Integració amb Proxmox VE

**Proxmox VE** incorpora suport nadiu per a Ceph, cosa que facilita la seua instal·lació, gestió i integració des de la mateixa interfície web o via línia de comandes.

Gràcies a aquesta integració:

* Es pot configurar Ceph directament des de la interfície de **Datacenter → Ceph**
* Els discos Ceph (RBD) poden ser utilitzats com a **emmagatzematge de màquines virtuals** i **contenidors (LXC)**
* El sistema garanteix **alta disponibilitat**, ja que les dades estan replicades en diversos nodes
* Permet una **escala horitzontal** fàcil, afegint més discos o nodes al clúster Ceph

\emoji{light-bulb} **Per què utilitzar Ceph en Proxmox?**

* Elimina la dependència de sistemes d’emmagatzematge extern (NFS, iSCSI, etc.)
* Millora la tolerància a fallades i la continuïtat del servei
* Ofereix una gestió centralitzada i unificada del clúster i l’emmagatzematge

# 5. \emoji{shield} Alta Disponibilitat (HA)

L’**Alta Disponibilitat (HA)** és un conjunt de tecnologies i configuracions dissenyades per garantir que els serveis crítics d’un sistema **romanguen operatius de manera contínua**, fins i tot davant fallades de maquinari, programari o xarxa. En entorns virtualitzats com **Proxmox VE**, la funcionalitat HA és essencial per assegurar la **mínima interrupció dels serveis** que allotgen màquines virtuals i contenidors.

#### Finalitat de la HA:

L'objectiu principal de la HA és **reduir al màxim el temps d’inactivitat (downtime)**. Quan un servidor físic (node) del clúster deixa de funcionar —ja siga per avaria, reinici o manteniment imprevist—, el sistema HA detecta automàticament la fallada i **reinicia les màquines virtuals afectades en un altre node actiu** del clúster, sense intervenció manual.

#### \emoji{gear} Funcionament dins de Proxmox VE:

Proxmox VE incorpora un subsistema HA que treballa estretament amb **Corosync**, el qual s’encarrega de supervisar la salut dels nodes i mantenir el quòrum del clúster. Les màquines virtuals que es volen protegir es configuren dins de **grups HA**, i el gestor HA pren decisions automàtiques segons l’estat dels nodes.

El sistema HA inclou:

* **Monitoratge constant** dels nodes i serveis.
* **Migració o reinici automàtic** de màquines virtuals en cas de fallida.
* **Policies de gestió de recursos**, com assignació preferida de nodes o prioritats.
* **Integració amb l’emmagatzematge compartit (ex. Ceph)** per garantir que les dades estiguen disponibles des de qualsevol node.

#### \emoji{puzzle-piece} Avantatges clau:

* **Continuïtat del servei** sense intervencions manuals.
* **Millora de la tolerància a fallades** en entorns crítics.
* **Reducció de riscos de pèrdua de dades** gràcies a la integració amb sistemes com Ceph i PBS.
* **Augment de la confiança operativa**, especialment en serveis que han d’estar actius 24/7.

En resum, la **Alta Disponibilitat** és un component fonamental en infraestructures professionals, ja que **automatitza la resposta davant incidències**, manté els serveis actius i contribueix a una experiència d’usuari contínua i fiable, fins i tot en condicions adverses.

# 6. \emoji{floppy-disk} Proxmox Backup Server (PBS)

**Proxmox Backup Server (PBS)** és una solució de còpia de seguretat **específicament dissenyada per a entorns virtualitzats amb Proxmox VE**. Proporciona una plataforma eficient, ràpida i segura per realitzar **backups i restauracions** de màquines virtuals (VMs), contenidors (CTs) i fins i tot discos individuals, garantint la **protecció i recuperació de dades** davant de fallades o pèrdua d’informació.

#### Finalitat de PBS:

PBS s’encarrega de centralitzar totes les còpies de seguretat dels recursos virtuals del clúster, amb funcionalitats com:

* **Backups incrementals**: només es guarden els blocs que han canviat, reduint dràsticament el temps i espai necessari.
* **Compressió i deduplicació**: optimitza l’espai d’emmagatzematge evitant duplicació de dades entre snapshots.
* **Xifratge (opcional)**: garanteix la confidencialitat de les dades tant en repòs com en trànsit.
* **Verificació de consistència**: comprova automàticament la integritat dels backups emmagatzemats.

#### \emoji{gear} Integració amb Proxmox VE:

PBS s’integra directament amb **Proxmox VE**, permetent configurar des de la pròpia interfície de Proxmox:

* **Jobs de backup programats**, amb horaris i freqüències personalitzades.
* **Estratègies de retenció** per controlar quants snapshots es conserven.
* **Restauracions selectives**, incloent fitxers individuals dins de contenidors o VMs.

Les comunicacions entre Proxmox VE i PBS es realitzen a través del protocol **Proxmox Backup Protocol**, altament optimitzat per rendiment i seguretat.

#### \emoji{locked} Seguretat i Recuperació:

PBS pot situar-se **fora del clúster principal** (recomanat), la qual cosa el converteix en una **última línia de defensa** en cas de fallida total del clúster o corrupció de dades. Aquesta separació física i lògica assegura que, fins i tot si els nodes de Proxmox fallen completament, les còpies de seguretat puguen ser recuperades des d’un sistema aïllat.

#### \emoji{puzzle-piece} Beneficis principals:

* **Automatització completa de backups i restauracions**.
* **Reducció de l’impacte en el rendiment del clúster** gràcies al backup incremental.
* **Escalabilitat**: un únic PBS pot gestionar còpies de seguretat de múltiples clústers.
* **Integració perfecta** amb la interfície de Proxmox VE i amb suport de CLI i API per a automatitzacions.

En definitiva, **Proxmox Backup Server** és una eina essencial per garantir la **resiliència i recuperació** del sistema virtualitzat, protegint-lo de pèrdues accidentals, errors humans o fallades greus de maquinari.

# \emoji{busts-in-silhouette} 7. Gestió d’Usuaris i Pools de Recursos 

La **gestió d’usuaris** dins d’un entorn virtualitzat com **Proxmox VE** és essencial per controlar **qui pot accedir**, **què pot fer** i **sobre quins recursos pot actuar**. Aquesta gestió garanteix la **seguretat, organització i eficiència** en la utilització del sistema, especialment en entorns compartits, corporatius o amb administració delegada.

#### Finalitat de la gestió d’usuaris:

L’objectiu principal és **definir rols i permisos específics per a cada usuari o grup d’usuaris**, segons les seues responsabilitats o necessitats. Això evita l’accés indegut a recursos crítics i redueix el risc d’errors humans que podrien afectar el funcionament del clúster o les màquines virtuals.

#### \emoji{gear} Funcionalitats clau a Proxmox VE:

* **Creació d’usuaris locals o via integració externa (LDAP/AD):**
  Permet administrar tant usuaris interns com externs mitjançant sistemes d’autenticació centralitzada.

* **Assignació de rols i permisos granulars:**
  Proxmox VE ofereix un sistema flexible de permisos basat en rols (`roles`) que determina quines accions pot realitzar un usuari (crear, modificar, esborrar màquines, accedir a la consola, gestionar backups, etc.).

* **Delegació d’administració:**
  És possible delegar l’administració parcial del sistema a tècnics o usuaris avançats sense donar-los accés complet, millorant la seguretat i separació de funcions (*principi de privilegi mínim*).

* **Definició de Pools de Recursos:**
  Els *pools* permeten agrupar màquines virtuals, contenidors i recursos assignats a usuaris o equips, facilitant-ne la gestió i limitant el seu accés només a la seua àrea de treball.

#### \emoji{locked-with-key} Avantatges de gestionar correctament els usuaris:

* **Millora la seguretat del sistema** evitant accessos no autoritzats o accions destructives.
* **Facilita la traçabilitat** (log dels usuaris i accions realitzades).
* **Permet una administració delegada controlada** en entorns amb múltiples tècnics o departaments.
* **Optimitza l’organització dels recursos**, assignant responsabilitats clares.

En resum, la gestió d’usuaris a Proxmox VE no sols millora la seguretat, sinó que és fonamental per estructurar un entorn **multiusuari estable, escalable i eficient**, tant per a entorns educatius, com empresarials o laboratoris de proves.

# 8. \emoji{locked-with-key} Seguretat i Bones Pràctiques

### 8.5 Monitorització del sistema amb Netdata

**Netdata** és una eina de monitorització en temps real dissenyada per oferir una visió molt detallada del rendiment de sistemes, aplicacions, contenidors i dispositius IoT. És coneguda per la seva **interfície gràfica intuïtiva** i pel seu enfocament en la **visualització immediata** de dades de rendiment, amb una latència molt baixa.

### \emoji{magnifying-glass-tilted-left} **Què fa Netdata?**

* Recull metadades del sistema (CPU, RAM, disc, xarxa, processos, etc.)
* Monitoritza serveis i aplicacions (MySQL, nginx, docker, etc.)
* Mostra les dades en **temps real (per segon o menys)**
* Pot funcionar com a eina independent o integrat en una arquitectura de monitorització més gran.

## \emoji{repeat} Comparativa amb altres solucions similars

A continuació tens una comparació amb tres eines populars de monitorització:

| Característica               | **Netdata**              | **Prometheus + Grafana**          | **Zabbix**                       | **Nagios**                  |
| ---------------------------- | ------------------------ | --------------------------------- | -------------------------------- | --------------------------- |
| **Temps real**               | \emoji{heavy-check-mark} (mil·lisegons)         | \emoji{cross-mark} (intervals mínims de 10-15s)    | \emoji{cross-mark} (intervals configurables)      | \emoji{cross-mark} (intervals configurables) |
| **Interfície gràfica**       | \emoji{heavy-check-mark} Moderna i interactiva  | \emoji{heavy-check-mark} (Grafana)                       | \emoji{heavy-check-mark} Però més complexa              | \emoji{cross-mark} (més bàsic o plugins)     |
| **Facilitat d’instal·lació** | \emoji{heavy-check-mark} Molt fàcil (una línia) | \emoji{cross-mark} Requereix configurar components | \emoji{cross-mark} Requereix bastant configuració | \emoji{cross-mark} Pot ser complexa          |
| **Alertes**                  | \emoji{heavy-check-mark} Bàsiques integrades    | \emoji{heavy-check-mark} Amb Alertmanager                | \emoji{heavy-check-mark} Molt completes                 | \emoji{heavy-check-mark} Molt completes            |
| **Escalabilitat**            | \emoji{heavy-check-mark} Amb Netdata Cloud      | \emoji{heavy-check-mark} Alta amb Thanos/Cortex          | \emoji{heavy-check-mark} Alta                           | \emoji{heavy-check-mark} Mitjana                   |
| **Consum de recursos**       | \emoji{heavy-check-mark} Molt lleuger           | \emoji{cross-mark} Pot ser alt depenent del cas    | \emoji{cross-mark} Pot consumir bastant           | \emoji{heavy-check-mark} Lleuger                   |
| **Extensibilitat**           | \emoji{cross-mark} Limitada               | \emoji{heavy-check-mark} Molt alt                        | \emoji{heavy-check-mark} Alt                            | \emoji{heavy-check-mark} Alt                       |

## \emoji{check-mark-button} **Avantatges de Netdata**

1. **Instal·lació molt senzilla:** una sola línia de comandes.
2. **Monitorització en temps real real:** actualitzacions per segon o menys.
3. **Poc consum de recursos:** ideal per a sistemes petits o embeguts.
4. **Dades molt detallades:** milers de mètriques disponibles per defecte.
5. **Interfície web interactiva:** gràfics clars i navegació fàcil.
6. **Suport per a contenidors i microserveis.**

## \emoji{cross-mark} **Inconvenients de Netdata**

1. **No està pensat per a emmagatzematge a llarg termini:** reté dades en memòria per defecte (encara que es pot integrar amb bases de dades de sèries temporals).
2. **Alertes bàsiques:** menys potent que Zabbix o Prometheus+Alertmanager.
3. **Menys integracions corporatives avançades.**
4. **Escalabilitat limitada si no s’utilitza Netdata Cloud.**

### \emoji{puzzle-piece} En resum:

* **Vols veure dades en temps real de manera fàcil i ràpida?** \emoji{backhand-index-pointing-right} *Netdata és ideal.*
* **Necessites anàlisi a llarg termini, alertes complexes i integració amb sistemes grans?** \emoji{backhand-index-pointing-right} *Millor Prometheus + Grafana o Zabbix.*
* **Tens un entorn molt crític amb necessitat d’alertes robustes i historial llarg?** \emoji{backhand-index-pointing-right} *Zabbix o Nagios són més adequats.*

Doncs en el cas dels servidors és millor NetData i per eixe cas m'he quedat en NetData.

## 9. \emoji{bar-chart} Monitoratge Centralitzat amb Zabbix

### \emoji{magnifying-glass-tilted-left} 9.1 Què és Zabbix i funcionalitats principals

Zabbix és una plataforma de monitoratge open source que permet supervisar en temps real el rendiment i l'estat de sistemes, servidors, màquines virtuals, serveis de xarxa i aplicacions. Proporciona alertes configurables, gràfiques avançades, dashboards personalitzats i recollida d’estadístiques a llarg termini, tot des d’una interfície web centralitzada.

### \emoji{check-mark-button} 9.2 Justificació de l’elecció de Zabbix front altres solucions

Tot i que existeixen altres plataformes com **Nagios**, **Prometheus** o **Netdata**, s’ha escollit Zabbix per les següents raons tècniques:

* **Monitoratge integral** (nivell de xarxa, sistema, servei i aplicació) en un únic entorn.
* **Compatibilitat nativa amb Proxmox VE**, gràcies a plantilles ja desenvolupades per a la monitorització de nodes, màquines virtuals i serveis Ceph.
* Suport per a **alertes proactives i automatització de respostes** davant esdeveniments.
* Interfície gràfica potent amb panells i visualitzacions configurables per a administradors i usuaris.

A diferència de **Prometheus**, que requereix diversos components externs per una solució completa, o de **Nagios**, que té un enfocament més bàsic i menys visual, **Zabbix ofereix una solució tot-en-u** que s’adapta millor a les necessitats del projecte.

### \emoji{link} 9.3 Integració amb la infraestructura virtualitzada de Proxmox VE

Zabbix es desplegarà com a màquina virtual dins del clúster Proxmox, i mitjançant l’ús d’agents Zabbix i connexions SNMP, es recollirà informació detallada de l’estat de cada node, VM, recursos de Ceph i altres serveis crìtics. S’utilitzaran **templates oficials i personalitzades** per adaptar la monitorització als requisits de l’entorn.

### \emoji{shield} 9.4 Desplegament en Alta Disponibilitat (HA)

Per garantir la **continuitat del monitoratge fins i tot en cas de fallada d’un node del clúster**, el servidor Zabbix estarà definit com a **recurs d’alta disponibilitat (HA)** dins de Proxmox. Això implica:

* Assignació a un **grup HA**.
* Configuració del servei Zabbix com a recurs gestionat per `ha-manager`.
* En cas de caiguda del node actiu, **el servei es migrarà automàticament** a un altre node disponible, assegurant una supervisió contínua.


## \emoji{brain}10. Conclusions i Valoració Personal

### 10.1 Objectius Aconseguits

Al llarg del desenvolupament d’aquest projecte, s’han assolit amb èxit els objectius plantejats inicialment, tant a nivell tècnic com formatiu.

S’ha aconseguit desplegar una infraestructura virtualitzada completa mitjançant **Proxmox VE**, incloent-hi:

* La creació i configuració d’un **clúster funcional** amb diversos nodes virtuals.
* La implementació d’un sistema d’**emmagatzematge distribuït amb Ceph**, garantint alta disponibilitat de les dades.
* La integració i ús de **Proxmox Backup Server (PBS)** com a sistema de còpies de seguretat centralitzades.
* La configuració del sistema de **Alta Disponibilitat (HA)**, amb gestió automàtica de fallades i migració de màquines.
* L’aplicació de mesures de **seguretat, monitoratge (amb Netdata Cloud)** i bones pràctiques d’administració.
* La definició de **rols d’usuari i pools de recursos** per a una gestió multiusuari eficient.

A més, s’ha documentat detalladament cada fase del projecte, facilitant

### 10.2 Dificultats trobades i solucions

\emoji{warning} Problema amb els repositoris de **Proxmox Backup Server**
Una de les principals dificultats trobades ha sigut l’actualització dels paquets del sistema, ja que per defecte, Proxmox Backup Server ve configurat amb els repositoris enterprise, els quals requereixen una subscripció de pagament.

\emoji{check-mark-button} ***Solució tècnica:*** utilitzar repositoris públics
Per tal de poder actualitzar i instal·lar paquets sense necessitat de subscripció, es pot configurar el sistema per a fer ús dels repositoris públics (no enterprise) de **Proxmox.**

#### \emoji{warning} Problema amb el almacenament del Ceph:

Durant el procés de configuració i ús del sistema **Ceph** com a emmagatzematge distribuït dins del clúster Proxmox VE, es va presentar una **incidència crítica relacionada amb la pèrdua de redundància de les dades**.

Concretament, després d’un període de funcionament estable, es va detectar que l’estat general del clúster Ceph passava a **WARNING**. L’anàlisi dels logs i l’ús del comandament `ceph status` van indicar que **alguns objectes havien perdut la seua redundància**, mostrant missatges com *“Degraded data redundancy”* o *“Some PGs are undersized”*. La causa principal va ser que el **nivell d’ocupació dels discos OSD havia superat el llindar crític**, impedint a Ceph replicar adequadament els objectes entre nodes.

Aquest comportament és esperable en entorns Ceph, ja que per garantir la replicació i integritat de les dades, el sistema necessita un marge suficient de capacitat lliure. Un cop aquest marge desapareix, el sistema prioritza la protecció de les dades existents però ja **no pot garantir la redundància completa**, fet que suposa un risc en cas de fallada addicional d’un OSD o node.

#### \emoji{check-mark-button} Solució adoptada:

Per resoldre aquest problema, es va procedir a:

1. **Avaluar l’ocupació real de cada OSD** mitjançant `ceph osd df` per identificar els més saturats.
2. **Alliberar espai en el pool Ceph RBD**, eliminant snapshots innecessaris i còpies de màquines virtuals que no requerien retenció prolongada.
3. **Ampliar la capacitat del clúster**, afegint un nou OSD amb un disc addicional per restablir el balanç de dades i la capacitat de replicació.
4. Un cop recuperada la capacitat suficient, Ceph va **recomençar automàticament el reequilibri (rebalancing)** i va restaurar la redundància completa dels objectes afectats.

Aquesta experiència va posar en relleu la **importància de monitorar proactivament l’espai lliure** dins d’un entorn Ceph i definir alertes abans d’arribar a llindars crítics, així com planificar amb antelació l’escalabilitat del sistema d’emmagatzematge.

### \emoji{rocket} 10.3 Possibles millores futures

#### **1. Docker com a Complement a LXC**  
\emoji{pushpin} *Millora la flexibilitat i portabilitat dels contenidors*  
- **Objectiu**: Integrar Docker dins de VMs/containers per aprofitar:  
  - \emoji{whale} Ecosistema més ampli d'imatges preconfigurades  
  - \emoji{repeat} Compatibilitat amb Kubernetes i eines CI/CD  
  - \emoji{hammer-and-wrench} Plantilles predefinides amb Docker + Portainer  
- **Reptes**:  
  - Configurar *systemd* en LXC existents  
  - Establir polítiques de seguretat específiques  

#### **2. Seguretat Avançada**  
\emoji{locked-with-key} *Hardening del cluster i xifrat de dades* 
- **Certificats TLS personalitzats**:  
  
  ```bash  
  pvecm updatecerts -force  # Actualitza certificats autofirmats  
  ```  

- **Xifrat de discs amb LUKS** (per a PBS/Ceph):  
  
  ```bash  
  cryptsetup luksFormat /dev/sdX  # Xifrat en repòs  
  ```  

- **Integració amb LDAP/AD** per a gestió centralitzada d’usuaris.

#### **3. Xarxa i Aïllament**  
\emoji{globe-with-meridians} *Segmentació per a major seguretat*  
- **VLANs dedicades**:  
  ```  
  auto vmbr0.100  
  iface vmbr0.100 inet static  
      address 192.168.100.2/24  
      vlan-raw-device vmbr0  
  ```  
  - Separar trànsit de gestió, Ceph i VMs.  

### **\emoji{clipboard} Resum de Prioritats**  
| **Àrea**          | **Acció Clau**                          | **Benefici Principal**                |  
|--------------------|----------------------------------------|---------------------------------------|  
| **Contenidors**    | Integració Docker + Portainer          | Portabilitat i ecosistema ampliat     |  
| **Seguretat**      | Hardening + LUKS + LDAP                | Protecció de dades i accés controlat  |  
| **Xarxa**          | VLANs Dedicades                        | Segmentació per a major seguretat     |  

### 10.4 Valoració tècnica i personal del projecte

Aquestes millores convertiran el nostre entorn en un sistema **més robust, segur i fàcil de gestionar**, adaptant-se tant a entorns educatius com empresarials.  

### Valoració personal del projecte

Aquest projecte m’ha permés consolidar coneixements adquirits durant el cicle formatiu, especialment en àrees com la **virtualització**, l’**alta disponibilitat** i la **gestió d’infraestructures TI**. A través de la implementació pràctica amb **Proxmox VE**, he pogut entendre millor el funcionament dels **clústers**, l’**emmagatzematge distribuït amb Ceph** i la importància de les **còpies de seguretat mitjançant PBS**.

A més, la incorporació de **Zabbix com a sistema de monitoratge** ha sigut fonamental per adquirir competències en la supervisió d’entorns TI. La configuració d’agents en sistemes **Windows i Linux**, així com la creació i gestió de *hosts* des de la interfície web de Zabbix, m’ha ajudat a entendre com controlar el rendiment, detectar anomalies i mantenir la salut de la infraestructura en temps real.

A nivell acadèmic, ha sigut una experiència molt completa, ja que m’ha ajudat a connectar la teoria amb la pràctica, millorant la meua **capacitat d’anàlisi, resolució de problemes i documentació tècnica**. Considere que ha sigut un projecte molt útil per a preparar-me de cara a **entorns reals i futurs reptes professionals** en el sector de les tecnologies de la informació.

## \emoji{paperclip} 11. Annexos

### \emoji{paperclip} 11.1 Bibliografia

A continuació es detallen les fonts utilitzades per al desenvolupament del projecte:

1. Proxmox. *Documentació oficial de Proxmox VE*. Accés 29 d’abril de 2025. [ Proxmox ](https://pve.proxmox.com/wiki/Main_Page).
2. Debian Project. *Debian Wiki*. Accés 25 d’abril de 2025. [Debian](https://wiki.debian.org/).
3. GitHub. *Repo*. Accés de seguit.[ Projecte Proxmox ](https://github.com/jcorbii/Projecte_Proxmox/)
4. Netdata  *Instal·lació Netdata*. Accés 12 de maig de 2025. [Netdata](https://www.netdata.cloud/)
5. Zabbix  *Docuemntació Zabbix*. Accés 14 de maig de 2025. [Zabbix](https://www.zabbix.com/)

# Instal·lació

## Proxmox

## \emoji{laptop} 3.  Implementació del *Clúster* Proxmox

### 3.1  Instal·lació dels nodes Proxmox VE

#### \emoji{bricks} Instal·lació del primer node de Proxmox

**Passos per a la instal·lació:**

1. Baixem la imatge *ISO* de Proxmox des de la [web oficial](https://proxmox.com/en/downloads), triant l’última versió disponible.
2. Una vegada descarregada, la col·loquem en el dispositiu des d'on farem la instal·lació en l’equip.

\emoji{small-orange-diamond} El primer pas, després de col·locar la *ISO*, és la càrrega del menú *GRUB*, on hem de seleccionar el procés d’instal·lació desitjat. En este cas, triarem l'opció amb interfície gràfica.

\emoji{small-orange-diamond} A continuació, acceptem la **llicència d’ús** del programari.

\emoji{small-orange-diamond} En el següent pas, seleccionem en quin disc volem instal·lar Proxmox. En este exemple només tenim un disc disponible, així que el seleccionem. També podem configurar el sistema de fitxers. Triem **ext4**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-2.png}
\end{center}

\emoji{small-orange-diamond} Assignem la totalitat de l’espai disponible al disc, ja que només n'hi ha un.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-3.png}
\end{center}

\emoji{small-orange-diamond} Configurem la **zona horària**.

\emoji{small-orange-diamond} Introduïm la **contrasenya d’administració** i un **correu electrònic** per a notificacions del sistema.

\emoji{small-orange-diamond} Assignem el **nom del *host***, la **IP**, el **gateway** i els **DNS**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-6.png}
\end{center}
\emoji{small-orange-diamond} Finalment, es mostra un **resum de la configuració** triada. Confirmem i iniciem la instal·lació.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-7.png}
\end{center}

\emoji{small-orange-diamond} Un cop finalitzada la instal·lació, a la consola apareixerà un missatge indicant que podem accedir a la interfície web de Proxmox via:

```
https://10.10.10.60:8006
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-8.png}
\end{center}

\emoji{small-orange-diamond} Així accedim a la **interfície web de Proxmox VE**:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-11.png}
\end{center}

### \emoji{desktop-computer} Instal·lació del Node 2

El procés d’instal·lació del **segon node** és **idèntic** al del primer, excepte pels valors del **nom del host** i la **IP**, que han de ser únics per a cada node.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-8.png}
\end{center}

Com es pot comprovar en el resum, l’única diferència és la IP i el nom del host.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-9.png}
\end{center}

Després de completar la instal·lació, tornem a tindre accés a la interfície web per la nova IP configurada:

```
https://10.10.10.61:8006
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-12.png}
\end{center}

I amb això, accedim de nou a la interfície de gestió de Proxmox:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-13.png}
\end{center}

### \emoji{desktop-computer} Instal·lació del Node 3

El procés d’instal·lació del **segon node** és **idèntic** al del primer, excepte pels valors del **nom del host** i la **IP**, que han de ser únics per a cada node.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-29.png}
\end{center}

Com es pot comprovar en el resum, l’única diferència és la IP i el nom del host.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-30.png}
\end{center}

Després de completar la instal·lació, tornem a tindre accés a la interfície web per la nova IP configurada:

```
https://10.10.10.58:8006
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-31.png}
\end{center}

I amb això, accedim de nou a la interfície de gestió de Proxmox:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-32.png}
\end{center}

## Proxmox Backup Server

## \emoji{desktop-computer} 6 Proxmox Backup Server (PBS)

### 6.1 Instalación de PBS

**Passos per a la instal·lació:**

1. Baixem la imatge *ISO* de Proxmox Backup Server des de la [web oficial](https://proxmox.com/en/downloads), triant l’última versió disponible.
2. Una vegada descarregada, la col·loquem en el dispositiu des d'on farem la instal·lació en l’equip.

\emoji{small-orange-diamond} El primer pas, després de col·locar la *ISO*, és la càrrega del menú *GRUB*, on hem de seleccionar el procés d’instal·lació desitjat. En este cas, triarem l'opció amb interfície gràfica.


\emoji{small-orange-diamond} A continuació, acceptem la **llicència d’ús** del programari.

\emoji{small-orange-diamond} En el següent pas, seleccionem en quin disc volem instal·lar Proxmox. En este exemple només tenim un disc disponible, així que el seleccionem. També podem configurar el sistema de fitxers. Triem **ext4**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-16.png}
\end{center}

\emoji{small-orange-diamond} Introduïm la **contrasenya d’administració** i un **correu electrònic** per a notificacions del sistema.

\emoji{small-orange-diamond} Assignem el **nom del *host***, la **IP**, el **gateway** i els **DNS**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-18.png}
\end{center}

\emoji{small-orange-diamond} Finalment, es mostra un **resum de la configuració** triada. Confirmem i iniciem la instal·lació.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-19.png}
\end{center}

\emoji{small-orange-diamond} Un cop finalitzada la instal·lació, a la consola apareixerà un missatge indicant que podem accedir a la interfície web de Proxmox via:

```
https://10.10.10.123:8006
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-20.png}
\end{center}

\emoji{small-orange-diamond} Així accedim a la **interfície web de Proxmox VE**:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-21.png}
\end{center}

## Zabbix

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

# Configuració 

# Proxmox

# 3. \emoji{desktop-computer} Implementació del Clúster Proxmox

A continuació et detallem pas a pas com crear un clúster en Proxmox i unir-hi altres nodes.

## \emoji{hammer-and-wrench} 3.2 Configuració del clúster (pvecm)

1. Accedeix a un dels nodes de Proxmox.
2. Ves a **Datacenter → Cluster** des del menú lateral esquerre.
3. Fes clic a **Crear Clúster** (`Create Cluster`).

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-56.png}
\end{center}

1. Ompli les dades del clúster:

   * **Nom del Clúster**
   * **Interfície de xarxa**
   * Altres paràmetres segons la teua configuració

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-57.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-58.png}
\end{center}

1. Un cop creat, veuràs el node com a part del clúster.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-59.png}
\end{center}

## \emoji{link} 2. Unir Nodes al Clúster

Per afegir un altre node al clúster:

1. Accedeix al segon node i ves a **Datacenter → Cluster**.
2. Fes clic a **Unir-se al clúster** (`Join Cluster`).

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-60.png}
\end{center}

1. A continuació, hauràs d’introduir la **informació del clúster**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-61.png}
\end{center}

1. Per obtindre aquesta informació, torna al node principal del clúster i fes clic a **Join Information**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-62.png}
\end{center}

1. Copia aquesta informació i torna al node secundari. Enganxa-la al formulari per unir-se.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-63.png}
\end{center}

1. Fes clic a **Unir-se**. Si tot és correcte, el node s’afegirà automàticament al clúster.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-64.png}
\end{center}

## \emoji{heavy-plus-sign} 3. Afegir més nodes

Per afegir més nodes, repeteix exactament el mateix procés:

* Accedeix al node
* Ves a **Datacenter → Cluster**
* Fes clic a **Unir-se al clúster**
* Copia la informació del node principal
* Enganxa-la i uneix el node

\emoji{end} I amb això ja tindràs un clúster Proxmox funcional amb diversos nodes!

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-64.png}
\end{center}

### \emoji{package} Descàrrega de plantilles per a Contenidors (CT)

Per a poder crear un contenidor, és necessari **disposar d’un *template*** (plantilla) corresponent al sistema operatiu desitjat.

1. Ves a la secció de **Storage** (almacenament)
2. Selecciona l’opció **Templates**
3. Tens diverses maneres d’obtindre una plantilla:

   * \emoji{outbox-tray} **Pujar-la manualment** (upload)
   * \emoji{link} **Descarregar-la des d’una URL externa**
   * \emoji{inbox-tray} **Utilitzar les plantilles predefinides** que ofereix Proxmox

\emoji{pushpin} En el nostre cas, utilitzarem la tercera opció: **plantilles predefinides**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-37.png}
\end{center}

Per a aquest projecte, descarregarem i utilitzarem plantilles de:

* **Debian**
* **Fedora**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-38.png}
\end{center}

### \emoji{file-folder} Preparació per a crear una Màquina Virtual (VM)

Per a crear una màquina virtual, és necessari **pujar una ISO** del sistema operatiu al nostre *storage*. Aquesta ISO s’ubica dins de la categoria de **"ISO Images"**.

1. Ves a `Datacenter → Storage`
2. Selecciona el teu emmagatzematge
3. Fes clic a **Upload**
4. Pujar la imatge ISO corresponent (ex. Debian, Ubuntu, Windows...)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-39.png}
\end{center}

## \emoji{bricks} Creació d’un Contenidor (CT)

Un cop tenim el *template* descarregat, podem crear un contenidor amb els passos següents:

### \emoji{compass} Pas 1: Inici de la creació

1. Fes clic a **Create CT** (Crear CT)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-40.png}
\end{center}

### \emoji{memo} Pas 2: Informació bàsica

Introdueix les dades del contenidor:

* **Node:** on es desplegarà
* **CT ID:** identificador únic
* **Hostname:** nom del sistema
* **Resource Pool:** (opcional) agrupació de recursos
* **Password:** per a l’accés del root

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-41.png}
\end{center}

### \emoji{package} Pas 3: Selecció del *Template*

Selecciona la plantilla que has descarregat anteriorment.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-42.png}
\end{center}

### \emoji{computer-disk} Pas 4: Emmagatzematge

Indica quin **storage** utilitzarà el contenidor.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-43.png}
\end{center}

### \emoji{abacus} Pas 5: Configuració de recursos

* **CPU:** nombre de nuclis assignats
* 
\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-44.png}
\end{center}

* **RAM:** memòria en MB
* 
\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-45.png}
\end{center}

### \emoji{globe-with-meridians} Pas 6: Xarxa

Defineix la configuració de xarxa (bridge, IP, VLAN, etc.)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-46.png}
\end{center}

### Finalització

Un cop completats tots els passos, el contenidor serà creat i apareixerà a la llista de recursos del node.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-47.png}
\end{center}

## \emoji{desktop-computer} Creació d’una Màquina Virtual (VM)

Els passos per crear una màquina virtual són **molt similars** als del contenidor, amb l’única diferència que:

* Es selecciona una **ISO** en lloc d’un *template*
* Es configura un **disc virtual** (en format qcow2, raw o ZFS)
* Es defineixen opcions d’instal·lació del sistema operatiu (com si fos una màquina física)

\emoji{repeat-button} Un cop creats els contenidors i les màquines virtuals, ja es poden **programar còpies de seguretat regulars** mitjançant **Proxmox Backup Server (PBS)** o les eines integrades en Proxmox VE.

### \emoji{brain} 4 Introducció a **Ceph** i Integració amb **Proxmox VE**

### 4.2 \emoji{gear} Instal·lació i Configuració de **Ceph** al Clúster

La instal·lació de Ceph en un entorn **Proxmox VE** es pot fer de manera centralitzada i senzilla gràcies a la seua integració nativa. A continuació es detallen els passos principals per a desplegar Ceph en un clúster de Proxmox:

#### \emoji{puzzle-piece} Requisits previs

Abans de començar amb la instal·lació, cal assegurar:

* Tots els nodes tenen l’hora sincronitzada via **NTP**
* Una xarxa específica o VLAN dedicada per al trànsit de Ceph (preferiblement amb baixa latència i alta amplada de banda)
* Discos dedicats per a Ceph (no utilitzar el mateix disc que el sistema operatiu)
* Una configuració bàsica del clúster de Proxmox ja establida

#### \emoji{hammer-and-wrench} Passos d’instal·lació

1. **Accedir a la interfície web de Proxmox**

   * Ves a `Datacenter → Ceph`

2. **Instal·lar Ceph als nodes**

   * Selecciona cada node on vols desplegar Ceph
   * A l’apartat `Ceph`, fes clic a **Install Ceph**
   * El sistema instal·larà automàticament els paquets necessaris (`ceph`, `ceph-common`, etc.)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-66.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-67.png}
\end{center}

1. **Crear els monitors (MON)**

   * Un mínim de **tres monitors** és recomanat per garantir el quorum
   * Des de l’apartat `Monitor`, fes clic a **Create Monitor**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-68.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-69.png}
\end{center}

1. **Afegir el gestor (MGR)**

   * Necessari per a la interfície gràfica i gestió avançada
   * Crea’l des de la mateixa pestanya amb el botó **Create Manager**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-70.png}
\end{center}

1. **Afegir els OSDs (Object Storage Daemons)**

   * Els OSDs són els processos que gestionen els discos durs del clúster
   * Ves a `OSD → Create OSD`, selecciona el disc físic i crea’l
   * Repeteix el procés per a cada node i disc dedicat

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-71.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-72.png}
\end{center}

* Com tenim 2 discos per cada node (menos en el node 3 que sols hi ha 1)de proxmox haurem de repetir el proccess dos voltes

**Node 1:**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-73.png}
\end{center}

**Node 2**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-74.png}
\end{center}

**Node 3**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-75.png}
\end{center}

1. **(Opcional) Crear un MDS (Metadata Server)**

   * Només si vols utilitzar **CephFS** com a sistema de fitxers compartit

    ##### **\emoji{open-file-folder} Què són els metadades?**
    Els metadades són informació sobre els fitxers, com ara:

    Noms de fitxers i directoris

    Jerarquia de carpetes

    Permisos d’accés

    Propietaris

    Dates de creació o modificació

    ##### \emoji{brain} Què fa exactament el MDS?
    
    Quan utilitzes CephFS (el sistema de fitxers distribuït de Ceph), el Metadata Server:

    - Controla l’estructura i organització del sistema de fitxers

    - Processa operacions com ls, mkdir, rm, mv, etc.

    - Fa que les consultes de fitxers siguen ràpides i escalables

    - Allibera als OSDs d’aquesta tasca perquè es centren només en llegir i escriure dades

### 4.3 \emoji{building-construction} Creació de Pools d’Emmagatzematge en Ceph

### \emoji{hammer-and-wrench} Creació d’un Pool pas a pas en Proxmox VE

1. Accedeix a la interfície web de **Proxmox VE**
2. Ves a `Datacenter → Ceph → Pools`
3. Fes clic a **Create**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-76.png}
\end{center}

1. Emplena els camps següents:

   * **Nom del pool:** (ex. `vm_data`, `cephfs_data`, `backups`)
   * **Nombre de rèpliques (Size):** recomanat mínim **3** per a alta disponibilitat
   * **Min. rèpliques (Min. Size):** mínim **2** per a mantenir el servei actiu amb una fallada
   * **Crush Rule:** regla de distribució entre els dispositius de disc

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-77.png}
\end{center}

1. Fes clic a **Create** i espera a que el pool aparega a la llista

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-78.png}
\end{center}

Al pas d'un temps podem veure com en els nodes apareix l'almacenament del ceph.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-79.png}
\end{center}

### \emoji{brain} Consideracions importants

* Els pools amb més rèpliques consumeixen més espai però ofereixen més redundància.
* És possible crear **pools separats** per a diferents usos (ex: un per a VM i un altre per a CephFS).
* Es poden utilitzar **regles CRUSH** per controlar com es distribueixen les dades per racks, discos o ubicacions físiques.

### \emoji{check-mark-button} Resultat

Amb el pool creat, ja pots:

* Assignar-lo com a **emmagatzematge de màquines virtuals (RBD)**
* Utilitzar-lo per a **CephFS**
* Monitorar el seu estat i ús des de la pestanya de **Ceph → Pools**

### 4.4 \emoji{rocket} Proves de Rendiment i Replicació en Ceph

Una vegada el clúster Ceph està desplegat i operatiu, és fonamental realitzar proves de **rendiment** i **replicació** per a verificar el correcte funcionament de l’emmagatzematge distribuït, així com garantir la **fiabilitat** i **eficiència** del sistema.

### \emoji{bar-chart} Proves de rendiment

Les proves de rendiment ens permeten mesurar la **velocitat de lectura i escriptura** dels dispositius Ceph, així com la **latència** i **capacitat de resposta** del clúster.

#### \emoji{test-tube} Eines recomanades:

* `rados bench` → eina pròpia de Ceph per mesurar el rendiment de lectura/escriptura
* `fio` → eina externa per fer proves personalitzades d’I/O

#### Exemple amb `rados bench`:

```bash
# Prova d'escriptura durant 60 segons
rados bench -p vm-data 60 write --no-cleanup

# Prova de lectura seqüencial
rados bench -p vm-data 60 seq

# Prova de lectura aleatòria
rados bench -p vm-data 60 rand
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-80.png}
\end{center}

### \emoji{check-mark-button} Resultat esperat

* Les proves d’escriptura i lectura han de mostrar valors de rendiment estables i adequats segons el teu hardware.
* La replicació ha de funcionar de manera automàtica, garantint la integritat i disponibilitat de les dades davant qualsevol fallada.

#### \emoji{pushpin} Exemple de comandes via CLI

Alternativament, es pot fer la instal·lació via línia de comandes:

```bash
# Instal·lar Ceph
pveceph install

# Crear un monitor
pveceph mon create

# Crear un OSD
pveceph osd create /dev/sdX
```

### \emoji{check-mark-button} Resultat

Una vegada configurats els **MON**, **MGR** i **OSD**, el clúster Ceph estarà operatiu. Ja pots procedir a:

* Crear **pools d’emmagatzematge**
* Assignar-los com a backend per a màquines virtuals
* Monitorar l’estat del clúster des de la interfície de Proxmox

### \emoji{recycling-symbol} Proves de replicació

Ceph replica les dades entre OSDs segons la configuració de rèpliques (per defecte 3). És important verificar que:

1. **Les dades es repliquen correctament** a múltiples discos.
2. **Quan cau un OSD o node**, Ceph automàticament redistribueix les rèpliques.

#### \emoji{repeat} Prova de fallada simulada:

1. Apaga un OSD manualment:

   ```bash
   systemctl stop ceph-osd@X
   ```

   (on `X` és el número de l’OSD)


2. Observa com Ceph reporta l’estat *degraded* i com reubica les dades.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-81.png}
\end{center}

1. Torna a engegar l’OSD i comprova la **reestructuració automàtica**:

   ```bash
   systemctl start ceph-osd@X
   ```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-82.png}
\end{center}

### \emoji{chart-increasing} 4.5 Gestió i Monitoratge de **Ceph**

Una vegada desplegat el clúster **Ceph**, és fonamental realitzar una gestió i monitoratge continuat per garantir l’estabilitat, el rendiment i la disponibilitat de les dades. Proxmox VE ofereix una **integració nativa amb Ceph**, que facilita tant el control operatiu com la detecció anticipada de possibles incidències.

### \emoji{hammer-and-wrench} Eines de gestió disponibles

Proxmox proporciona diversos mètodes per gestionar Ceph:

#### \emoji{pushpin} Interfície web de Proxmox VE

Des de la GUI es pot accedir a:

* **Estat del clúster**: `Datacenter → Ceph → Status`
* **Gestió d’OSDs**: afegir, eliminar o veure l’estat dels Object Storage Daemons
* **Monitors (MONs)** i **Managers (MGRs)**: estat, creació i falles
* **Creació i eliminació de pools**
* **Configuració i gestió de CephFS**

#### \emoji{wrench} Línia de comandes (CLI)

Per a gestió avançada i automatitzacions:

```bash
ceph status             # Estat general del clúster
ceph osd tree           # Visualització jeràrquica dels OSDs
ceph df                 # Ús d’espai en pools
ceph health detail      # Informació detallada de salut
ceph osd out/in <id>    # Marcar un OSD com a fora o dins del clúster
```

### \emoji{bar-chart} Monitoratge actiu del clúster

Els principals paràmetres a controlar de forma contínua són:

* **Salut del clúster (HEALTH\_OK / WARN / ERR)**
* **Nombre d’OSDs actius i en línia**
* **Estat dels MON i MGR**
* **Ús de l’espai per pool i per OSD**
* **Latències de lectura i escriptura**
* **Rebalanceig de dades en cas de fallada o afegit de nous discos**

### \emoji{satellite-antenna} Integració amb eines externes

Encara que Proxmox proporciona visualització bàsica, pots integrar Ceph amb eines de monitoratge més potents com:

* **Prometheus + Grafana** (via Ceph MGR modules)
* **Zabbix** o **Nagios**, mitjançant plugins
* Alertes per correu electrònic o sistemes de notificació

### \emoji{light-bulb} Recomanacions de manteniment

* \emoji{repeat-button} **Revisar l’estat del clúster regularment**
* \emoji{test-tube} **Simular fallades controlades** per validar la replicació i recuperació
* \emoji{package} **No sobrecarregar els OSDs**; mantindre un marge de capacitat lliure
* \emoji{stop-sign} **Evitar la pèrdua simultània de múltiples discos** amb rèpliques mínimes

### \emoji{check-mark-button} Resultat

Amb una correcta gestió i monitoratge, es garanteix que el clúster Ceph oferisca un rendiment estable, altament disponible i resistent a fallades, adaptat a les necessitats de l’entorn virtualitzat en Proxmox VE.

## \emoji{shield} 5. Alta Disponibilitat (**HA**) en Proxmox VE

La **Alta Disponibilitat (High Availability)** és una funcionalitat clau en entorns crítics, ja que permet garantir la **continuïtat del servei** davant la caiguda d’un node. Amb Proxmox VE, aquesta característica s’integra de manera nativa quan es treballa amb un **clúster**.

### \emoji{gear} 5.1 Activació del Gestor HA en Proxmox

Per a fer ús de la funcionalitat HA, cal que:

1. El clúster estiga format per almenys **3 nodes** (per mantenir el **quorum**)
2. Els nodes tinguen **Corosync** i **pve-ha-crm** actius
3. Els recursos (VM o CT) estiguen ubicats en **storage compartit** o Ceph

#### \emoji{repeat} Procediment:

* Ves a `Datacenter → HA`
* Assegura’t que el **HA Manager** està actiu
* Cada node mostrarà el seu estat (online, standby, etc.)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-83.png}
\end{center}

### \emoji{puzzle-piece} 5.2 Definició de Grups HA

Els **grups HA** permeten organitzar i assignar màquines virtuals o contenidors per a gestionar millor les polítiques de tolerància a fallades.

#### Creació d’un grup HA:

1. Ves a `Datacenter → HA → Groups`

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-84.png}
\end{center}

1. Fes clic a **Create**
2. Assigna:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-85.png}
\end{center}

   * **Nom del grup**
   * **Nodes preferits** per executar el servei
   * **Prioritats** (per decidir on s’hauria de migrar en cas de fallada)

Després, quan crees o edites una VM/CT, pots assignar-la a un grup HA.

### \emoji{repeat-button} 5.3 Proves de Tolerància a Fallades (Failover de Màquines Virtuals)

Per assegurar el correcte funcionament de la configuració HA, és recomanable fer proves de **failover controlades**:

#### Escenari de prova:

1. Assigna una VM a un grup HA

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-86.png}
\end{center}

1. Para o apaga un node manualment

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-87.png}
\end{center}

1. Observa com la VM és **migrada automàticament** a un altre node disponible
2. Verifica que el servei continua operatiu sense intervenció manual

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-89.png}
\end{center}

\emoji{magnifying-glass-tilted-left} Es pot monitorar aquest procés des de `Datacenter → HA → Status`.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-90.png}
\end{center}

Per descomptat! Ací tens el fragment redactat de manera formal i clara, ideal per afegir com a continuació dins del punt 5.4 o com un subapartat pràctic de **recuperació post-fallada**:

### \emoji{light-bulb} 5.4 Casos d’Ús i Recuperació davant Caigudes de Nodes

Els entorns amb HA actiu poden recuperar-se de forma automàtica en diferents situacions:

* \emoji{electric-plug} **Fallada de hardware o energia** en un node
* \emoji{fire-extinguisher} **Actualitzacions crítiques** que requereixen reinici
* \emoji{gear} **Errors de sistema** o problemes de rendiment greu

En cada cas:

* El sistema HA detecta la fallada
* Migració automàtica a nodes disponibles
* Restauració del servei amb **temps mínim d’interrupció**

#### Exemple pràctic:

Una màquina virtual crítica (servidor web, base de dades, etc.) està configurada amb HA. Si el node cau inesperadament, aquesta VM es reinicia en un altre node en qüestió de segons, garantint la continuïtat del servei.

### \emoji{check-mark-button} Resultat

Amb la configuració HA en Proxmox VE, es millora significativament la **resiliència de la infraestructura virtualitzada**, assegurant que els serveis essencials estiguen disponibles **24/7**, fins i tot davant fallades greus.

### \emoji{repeat-button} Recuperació manual de màquines HA al seu node original

Després d’una **caiguda temporal d’un node** del clúster, el sistema **HA de Proxmox** trasllada automàticament les màquines virtuals o contenidors afectats a un altre node disponible per garantir la continuïtat del servei.

Un cop el node original torna a estar **en línia i estable**, és **recomanable migrar manualment** les màquines al seu node d'origen per:

* Recuperar l’equilibri de càrrega del clúster
* Retornar els recursos als seus entorns habituals
* Preparar el sistema per a futures fallades

### \emoji{gear} Procediment per a migrar una màquina HA al node original

1. Accedeix a la interfície web de Proxmox
2. Ves al node on actualment està executant-se la màquina
3. Selecciona la màquina virtual o contenidor
4. Fes clic a **"Migrate"**
5. Tria com a destinació el **node original** (ex: `node3`)
6. Confirma l’operació

\emoji{pushpin} *Nota:* La migració es pot fer en calent (**live migration**) si la màquina suporta aquesta funcionalitat (generalment les VMs amb discs en Ceph o ZFS compartit).

### \emoji{check-mark-button} Resultat

Amb aquest procés, la màquina recupera la seua ubicació inicial, mantenint-se dins del grup HA i **preparada per a futures gestions automàtiques** de tolerància a fallades.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-91.png}
\end{center}

## \emoji{busts-in-silhouette} 7. Gestió d’Usuaris i Pools de Recursos

En entorns virtualitzats compartits, com un clúster de **Proxmox VE**, és fonamental establir una **gestió d’usuaris estructurada**, amb **permisos diferenciats** i assignació clara de **recursos**, per garantir la **seguretat, control i eficiència operativa**.

### \emoji{locked-with-key} 7.1 Creació de Rols Personalitzats i Permisos

**Proxmox VE** ofereix un sistema de permisos basat en rols, que permet definir què pot fer cada usuari dins del sistema. Aquest model RBAC (Role-Based Access Control) es basa en tres elements:

* **Usuaris** (local, LDAP o via PAM)
* **Rols** (conjunts de permisos)
* **Objectes** (nodes, VM, storage, etc.)

#### \emoji{wrench} Creació d’un rol personalitzat:

1. Ves a `Datacenter → Permissions → Roles`
2. Fes clic a **Add**
3. Assigna un nom (ex. `gestor_vm`)
4. Selecciona els permisos específics:

   * `VM.Allocate`
   * `VM.Config.Disk`
   * `VM.Console`
   * `Sys.Console`

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-92.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-93.png}
\end{center}

#### \emoji{plus} Assignació del rol:

1. Ves a `Permissions → Add → Users`
2. Selecciona:

   * **Path:** àrea de control (`/`, `/vms`, `/pool/nom`, etc.)
   * **User:** usuari o grup
   * **Role:** el rol que has creat

Això permet donar accés restringit a determinats recursos dins del clúster.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-94.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-95.png}
\end{center}

En este cas he creat un usuari de prova per a assignar el rol creat.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-96.png}
\end{center}

### \emoji{card-index-dividers} 7.2 Definició de Pools de Recursos

Els **pools** són agrupacions lògiques de recursos (VMs, CTs, discos, etc.) que permeten facilitar la gestió, especialment en entorns multiusuari o amb departaments diferenciats.

#### \emoji{hammer-and-wrench} Creació d’un pool:

1. Ves a `Datacenter → Permissions → Pools`
2. Fes clic a **Create**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-97.png}
\end{center}

1. Emplena:

   * **Nom del pool:** ex. `departament_it`, `desenvolupament`
   * **Descripció** (opcional)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-98.png}
\end{center}

1. Afegeix les VMs o CTs desitjades al pool

En este cas anem a fer que el usuari proba puga vore la vm 108(Windows10)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-99.png}
\end{center}

Assignacio del pool al usuari proba amb el rol  que hem creat.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-100.png}
\end{center}

Els pools són útils per:

* Aplicar permisos a grups d’usuari de forma més eficient
* Organitzar recursos segons projectes o àrees de treball
* Limitar l’accés només a les màquines assignades

### \emoji{bust-in-silhouette} 7.3 Gestió Delegada i Multiusuari

Amb els **rols** i **pools**, es pot habilitar un entorn **multiusuari segur**, on cada usuari o equip tinga accés només als recursos que li pertoquen.

#### Exemple de gestió delegada:

* **Usuari:** `anna@pve`
* **Pool assignat:** `marketing_vms`
* **Rol aplicat:** `PVEVMUser` (amb permisos per iniciar/parar/migrar màquines)
* Resultat: Anna només pot gestionar les VMs del pool `marketing_vms`, sense accedir a cap altre recurs del sistema

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-101.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-102.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-103.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-104.png}
\end{center}

### \emoji{check-mark-button} Beneficis

* \emoji{locked} Major seguretat mitjançant la separació de privilegis
* \emoji{family} Facilitat per delegar la gestió a equips tècnics o usuaris finals
* \emoji{puzzle-piece} Escalabilitat per a entorns educatius, empresarials o d'hosting

## \emoji{test-tube} Casos Pràctics de Gestió Delegada i Multiusuari en Proxmox VE

### \emoji{graduation-cap} **Cas 1: Entorn educatiu amb alumnes de pràctiques**

#### Escenari:

L’institut ha desplegat un clúster de Proxmox per a alumnes del cicle de sistemes. Cada alumne ha de gestionar una VM pròpia, però sense accés al sistema complet.

#### Configuració:

* **Usuari:** `alumne01@pve`
* **Pool:** `alumnes`
* **VM assignada:** `vm104` (alumne01-ubuntu24)
* **Rol:** `PVEVMUser`

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-105.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-106.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-107.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-108.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-109.png}
\end{center}

#### Resultat:

L’alumne pot:

* Engegar/parar la seua VM
* Accedir per consola
* No pot crear ni esborrar màquines
* No pot veure cap altra VM

### \emoji{office-building} **Cas 2: Departament de Desenvolupament en una empresa**

#### Escenari:

L’equip de desenvolupament necessita accedir a diverses màquines de testing, però no ha de poder modificar la infraestructura general.

#### Configuració:

* **Usuaris:** `david@pve`, `jordi@pve`
* **Pool:** `dev_pool`
* **Rols:** `gestor_vm_custom` (creat amb permisos limitats com `VM.Console`, `VM.Start`, `VM.Shutdown`)

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-110.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-111.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-112.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-113.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-114.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-115.png}
\end{center}

#### Resultat:

Els usuaris poden:

* Utilitzar i gestionar les seues VMs
* No poden crear VMs noves ni modificar configuracions globals

### \emoji{hammer-and-wrench} **Cas 3: Tècnic amb accés complet a un node concret**

#### Escenari:

Un tècnic extern col·labora en la gestió de sistemes, però només se li vol donar accés al node `node3`.

#### Configuració:

* **Usuari:** `tecnic@pve`
* **Àrea assignada:** `/nodes/node3`
* **Rol:** `PVEAdmin`

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-116.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-117.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-118.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-119.png}
\end{center}

#### Resultat:

Té accés complet només a les màquines i configuració d’eixe node, però no pot accedir a altres nodes ni al datacenter.

### \emoji{jigsaw} **Cas 4: Hosting amb gestió delegada per client**

#### Escenari:

Una empresa ofereix màquines virtuals com a servei. Cada client gestiona la seua pròpia màquina.

#### Configuració:

* **Client:** `client_a@pve`
* **Pool:** `client_a_pool`
* **VM assignada:** `vm104`
* **Rol:** `PVEVMUser`

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-122.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-123.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-124.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-125.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-126.png}
\end{center}


#### Resultat:

Cada client pot administrar la seua pròpia màquina, sense cap visibilitat sobre altres clients o parts del sistema.

### Conclusions dels casos pràctics

Aquests escenaris mostren com Proxmox permet adaptar-se fàcilment a entorns **multiusuari**, amb control granular de permisos i una gestió segura i delegada, mantenint la **seguretat**, **eficiència** i **flexibilitat** del sistema.

### **8.1. Actualitzacions i Pegats de Seguretat**

\emoji{check-mark-button} **Accions recomanades:**

* **Actualitzar regularment**:

  ```bash
  apt update && apt dist-upgrade
  ```
* Habilitar les **actualitzacions automàtiques de seguretat**:

  ```bash
  apt install unattended-upgrades
  dpkg-reconfigure unattended-upgrades
  ```
* Verificar pegats disponibles en Proxmox:

  ```bash
  pveam update
  ```

### **8.2. Configuració del Tallafoc en Proxmox**

\emoji{check-mark-button} **Accions recomanades:**

* Activar el **tallafoc integrat** en Proxmox (GUI: `Datacenter > Firewall`).
* Reglas bàsiques:

  * Permetre només SSH (port 22), accés web de Proxmox (8006) i Ceph (si s’utilitza) des d’IPs de confiança.
  * Bloquejar accessos externs a APIs no necessàries.
* Exemple per permetre accés web només des d’una IP específica:

  ```bash
  pve-firewall localnet add -enable 1 -policy in -action ACCEPT -dport 8006 -source 192.168.1.100
  ```

### **8.3. Còpies de Seguretat de la Configuració**

\emoji{check-mark-button} **Accions recomanades:**

* **Fer còpia de seguretat de la configuració del clúster**:

  ```bash
  tar -czvf /backup/proxmox_config_$(date +%Y-%m-%d).tar.gz /etc/pve/
  ```
* **Automatitzar les còpies** amb PBS:

  * Programar còpies diàries/setmanals de VMs/LXCs (GUI: `PBS > Datastore > Backup Jobs`).
  * Utilitzar **retenció incremental** (exemple: 7 còpies diàries + 4 setmanals).

### **8.4. Bones Pràctiques d’Administració**

\emoji{check-mark-button} **Accions recomanades:**

* **Activar l’autenticació en dos passos (2FA)** per a la GUI de Proxmox (GUI: `Datacenter > Permissions > Users`).
* **Restringir l'accés per SSH**:

  ```bash
  nano /etc/ssh/sshd_config
  ```

  * Afegir: `PermitRootLogin no`, `PasswordAuthentication no` (usar claus SSH).
* **Monitoratge**:

  * Configurar alertes per correu electrònic (GUI: `Datacenter > Notifications`).
  * Utilitzar `ceph health` i `pveperf` per supervisar el rendiment.

### **8.5. Monitoratge Centralitzat amb Netdata Cloud**

**Netdata** és una eina de monitoratge en temps real, lleugera i de codi obert, que permet visualitzar de forma detallada l’ús de CPU, memòria, disc, xarxa, processos i molts altres paràmetres del sistema.

En aquest projecte s’ha optat per utilitzar **Netdata en mode núvol** (*Netdata Cloud*) per garantir:

* \emoji{globe-with-meridians} **Accessibilitat des de qualsevol lloc** amb connexió a Internet
* \emoji{cloud} **Alta disponibilitat** sense necessitat de desplegar servidors de monitoratge propis
* \emoji{chart-increasing} Visualització centralitzada de tots els nodes Proxmox i del PBS en un únic panell

#### \emoji{hammer-and-wrench} Instal·lació i connexió al núvol:

1. Crear un compte gratuït a [https://app.netdata.cloud](https://app.netdata.cloud)
2. En cada node Proxmox:

   * Instal·lar l’agent:

     ```bash
     bash <(curl -Ss https://my-netdata.io/kickstart.sh)
     ```
   * Enllaçar-lo al teu compte Netdata amb la comanda proporcionada pel portal (normalment amb `netdata-claim.sh`)

Després d’això, es podrà visualitzar cada node en temps real des del tauler de **Netdata Cloud**, amb alertes, gràfics detallats i control unificat del rendiment del clúster.

### 8.5 Monitorització del sistema amb **Netdata**

#### \emoji{brain} Què és Netdata?

**Netdata** és una plataforma de monitorització en temps real que permet supervisar el rendiment i l’estat de sistemes i serveis de manera molt detallada. És una eina **lleugera**, de **codi obert** i fàcil d’integrar en entorns Linux, incloent **Proxmox VE**.

Proporciona dades sobre:

* Ús de CPU, RAM i disc
* Tràfic i estat de la xarxa
* Estadístiques de processos
* Temperatura, serveis actius, ports, etc.

### \emoji{cloud} Utilització de **Netdata Cloud** al projecte

En lloc de desplegar una instància de monitorització local o en cada node, en aquest projecte s’utilitzarà la **plataforma centralitzada de Netdata Cloud**.

Aquesta estratègia es basa en instal·lar únicament l’**agent de Netdata** a cada node que es vulga monitoritzar, i connectar-lo al panell de control global de Netdata Cloud.

#### \emoji{check-mark-button} Avantatges de fer servir el núvol:

* \emoji{locked} **Alta disponibilitat:** La plataforma està disponible 24/7 des de qualsevol lloc
* \emoji{globe-with-meridians} **Accessibilitat centralitzada:** Tots els nodes es poden supervisar des d’un únic panell
* \emoji{chart-increasing} **Visualització interactiva:** Gràfics en temps real i alertes integrades
* \emoji{puzzle-piece} **Zero manteniment de servidors de monitoratge locals**
* \emoji{bell} Possibilitat de configurar notificacions (Slack, correu, Discord...)

### \emoji{hammer-and-wrench} Procediment bàsic

1. Crear un compte gratuït en [https://app.netdata.cloud](https://app.netdata.cloud)
2. En cada node que es vulga monitoritzar:

   * Instal·lar l’agent amb:

     ```bash
      wget -O /tmp/netdata-kickstart.sh https://get.netdata.cloud/kickstart.sh && sh /tmp/netdata-kickstart.sh --nightly-channel --claim-token 2j7CJC_yS3oDQ9DD4eVlLNMV5ecx0WeqwfvNvfOthCcBCkXRLoysr-TKkc5GLM9BzHmlE9Bb36sQghRHfbOsn4rhSEDnd4TmTaabd__6loq4Vceb_o5BitgLI_1gfT4D5pCzx4o --claim-rooms 6ff6ecc7-275c-4404-a4a0-5fac76e79776 --claim-url https://app.netdata.cloud
     ```

      \begin{center}
          \includegraphics[width=0.6\textwidth]{../../../img/image-120.png}
      \end{center}

   * Connectar l’agent al compte de Netdata Cloud amb la comanda que proporciona el portal (normalment `netdata-claim.sh`)
3. Accedir al panell de **Netdata Cloud** i visualitzar tots els nodes en temps real

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-121.png}
\end{center}

###  Resultat

Amb aquest sistema, es garanteix una **monitorització eficaç i des de qualsevol lloc**, sense haver de desplegar ni mantindre servidors propis per a l’anàlisi. Netdata Cloud facilita una supervisió **proactiva i àgil** del clúster Proxmox i del Proxmox Backup Server (PBS).

# Proxmox Backup Server

# 6. \emoji{floppy-disk} Proxmox Backup Server (PBS)

## \emoji{open-file-folder} 6.2 Creació del Datastore en Proxmox Backup Server

### \emoji{stop-sign} **Requisits previs**

> \emoji{warning} Tots els discos seran esborrats. Assegura’t que **no continguen dades importants** abans de continuar.

### \emoji{wrench} 1. Verificar instal·lació de ZFS

\emoji{wrench}  Instalar ZFS (si encara no está instalat)

```bash
apt update
apt install zfsutils-linux -y
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-22.png}
\end{center}

Això confirma que el sistema està preparat per a treballar amb pools ZFS.

### \emoji{card-index-dividers} 2. Creació del ZFS pool

Existien tres opcions principals per a crear el pool ZFS, depenent del nombre de discos disponibles i les necessitats d’emmagatzematge i redundància:

* **Opció A**: `striped` – màxim espai però sense cap tolerància a fallades.
* **Opció B**: `mirror` – redundància completa però requereix un nombre parell de discos.
* **Opció C**: `raidz` – una combinació equilibrada entre espai disponible i tolerància a falles (similar a RAID 5).

\emoji{backhand-index-pointing-right} **Atés que en aquesta màquina només disposem de tres discos** (`/dev/vda`, `/dev/vdb` i `/dev/vdc`), la millor opció des del punt de vista tècnic és **RAIDZ**, ja que ens ofereix una bona capacitat d’emmagatzematge i alhora permet resistir la fallada d’un disc sense perdre les dades.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-23.png}
\end{center}

Per crear el pool:

```bash
zpool create backup-pool raidz /dev/vda /dev/vdb /dev/vdc
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-24.png}
\end{center}

### 3. Verificar l’estat del pool

Després de la creació, podem comprovar que el pool funciona correctament:

```bash
zpool status
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-25.png}
\end{center}

Hauries de veure un estat **ONLINE** i el pool anomenat `backup-pool`.

### \emoji{card-file-box} 4. Crear el datastore en PBS

A través de la interfície web de PBS:

1. Anar a **Datastore > Create**
2. Omplir els camps:

   * **ID**: `zfs-backup`
   * **Path**: `/backup-pool` (punt de muntatge automàtic creat per ZFS)

3. Fer clic a **Create**

- Creació del **Datastore**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-26.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-27.png}
\end{center}

### \emoji{counterclockwise-arrows-button} 5. Comprovació i muntatge automàtic

ZFS gestiona automàticament el muntatge del pool. Per comprovar-ho:

```bash
zfs list
```

Resultat esperat:

```
NAME           USED  AVAIL  REFER  MOUNTPOINT
backup-pool    96K   900G    96K   /backup-pool
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-28.png}
\end{center}

A partir d’aquest moment, el sistema ja pot utilitzar el datastore per a còpies de seguretat, amb les garanties que ofereix ZFS quant a integritat de dades i rendiment.

## \emoji{floppy-disk} 6.3 Integració amb Proxmox VE

Per integrar el **Proxmox Backup Server (PBS)** com a sistema d’emmagatzematge dins del clúster de **Proxmox VE**, cal seguir els passos següents:

### \emoji{locked-with-key} 1. Copiar l’**Empremta digital (Fingerprint)** del PBS

Accedeix al **Proxmox Backup Server** i ves a:

\emoji{round-pushpin} `Dashboard → Show Fingerprint`

Esta empremta és necessària per establir una connexió segura entre els nodes de Proxmox VE i el servidor PBS.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-33.png}
\end{center}

### \emoji{heavy-plus-sign} 2. Afegir l’Almacenament al Clúster de Proxmox

Una vegada copiada l’empremta, accedim a qualsevol node del clúster de **Proxmox VE** i seguim els passos següents:

1. Ves a **Datacenter → Storage**
2. Fes clic a **Add** i selecciona l’opció **Proxmox Backup Server**

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-34.png}
\end{center}

### \emoji{memo} 3. Omplir les Dades de Connexió

Ara introduïm la informació requerida del servidor PBS:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-36.png}
\end{center}

* **ID:** Nom identificador per a l’almacenament
* **Server:** IP o domini del servidor PBS
* **Username:** Nom d’usuari per connectar-se
* **Password:** Contrasenya corresponent
* **Nodes:** Nodes del clúster que tindran accés a l’almacenament
* **Datastore:** Nom del repositori, per exemple `zfs-backups`
* **Namespace:** Espai de noms (opcional, si s’utilitzen subespais dins el datastore)

### 4. Confirmar i Finalitzar

Una vegada configurat, el sistema validarà les dades i l’almacenament PBS apareixerà com a disponible per a fer còpies de seguretat o restauracions.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-35.png}
\end{center}

\emoji{end-arrow} **Amb aquests passos, ja tens el teu Proxmox Backup Server integrat dins del clúster de Proxmox VE.** Això et permet gestionar còpies de seguretat de forma centralitzada, eficient i segura.

## \emoji{light-bulb} 6.4 Programació de Còpies de Seguretat i Creació de Màquines Virtuals i Contenidors

En aquest entorn, treballarem tant amb **contenidors (LXC)** com amb **màquines virtuals (KVM)**. Per a gestionar correctament les còpies de seguretat i automatitzar-les, primer hem de tindre clar com es creen els recursos que es volen protegir.

### \emoji{counterclockwise-arrows-button}  Programació de Còpies de Seguretat

Una correcta **estratègia de programació de còpies de seguretat** és essencial per a garantir la disponibilitat i recuperació de dades en entorns de producció. Amb **Proxmox VE** i la integració amb **Proxmox Backup Server (PBS)**, es pot automatitzar aquest procés de forma eficient.

### \emoji{spiral-calendar} Planificació de les còpies

La planificació ha de tindre en compte:

* **Freqüència de còpia:** diària, setmanal o mensual segons la criticitat del sistema
* **Hora d’execució:** preferentment fora de l’horari productiu per minimitzar impacte
* **Recursos inclosos:** contenidors, màquines virtuals o pools de recursos
* **Duració esperada:** basada en la mida i nombre de sistemes a protegir

### \emoji{brain} Bones pràctiques de planificació

* \emoji{jigsaw} **Dividir per grups de càrrega:** programar còpies per pools o per tipus de màquines
* \emoji{one-oclock} **Evitar solapaments:** distribuint les tasques durant la nit o cap de setmana
* \emoji{test-tube} **Fer proves de restauració regulars** per validar les còpies

### \emoji{locked-with-key} Integració amb polítiques de retenció

La programació de còpies de seguretat ha d’anar acompanyada d’una política de **retenció** que mantinga un nombre raonable de còpies antigues per evitar saturació de l’emmagatzematge:

* **Retenció curta:** 7 còpies diàries
* **Retenció mitjana:** 4 setmanals
* **Retenció llarga:** 6 còpies mensuals

Aquesta política es pot aplicar automàticament des de la configuració del **storage** PBS a `Datacenter → Storage → pbs → Backup Retention `.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-53.png}
\end{center}

### \emoji{gear} Automatització des de Proxmox VE

Les tasques de còpia es poden programar fàcilment:

1. `Datacenter → Backup → Add`
2. Selecciona:

   * **Storage (PBS)**
   * **Calendari (cron):** ex. `0 21 * * *` per fer-la a les 21:00h cada dia
   * **Mode:** snapshot, suspend o stop
   * **Recursos:** tots, per pool o per ID

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-52.png}
\end{center}

### Resultat

Amb una programació adequada i una estratègia de retenció ben definida, s'assegura la **protecció contínua de les dades** i es redueix el risc de pèrdua d'informació crítica, mantenint a la vegada l'emmagatzematge net i eficient.

### \emoji{recycling-symbol} 6.5 Restauració de Màquines Virtuals i Contenidors

Una de les funcionalitats més potents del **Proxmox Backup Server (PBS)** és la possibilitat de restaurar còpies de seguretat de manera ràpida i fiable, tant de **màquines virtuals (KVM)** com de **contenidors (LXC)**.

### \emoji{repeat-button} Tipus de restauració

Proxmox permet dues modalitats principals de restauració:

* **Restauració completa:** es crea una nova instància basada en la còpia de seguretat
* **Restauració in situ:** reemplaça una màquina existent per una còpia anterior (amb precaució)

### \emoji{hammer-and-wrench} Procediment de restauració

#### 1. Accedir al la backup

* Entra a la interfície web del **Proxmox **
* Ves a `Datacenter → Storage → pbs`
* Selecciona la còpia de seguretat desitjada

![](../../../img/image-48.png){ width=60% }

#### 2. Llençar la restauració

* Fes clic a **Restore**
* Defineix els paràmetres següents:

  * **Target Node:** node de Proxmox on es restaurarà la màquina
  * **VM ID nou:** (opcional) si vols crear una nova màquina amb un altre ID
  * **Mode de restauració:**

    * **Live restore (per a VMs):** restauració mentre la màquina torna a estar en funcionament (recomanat per a entorns amb poca tolerància a caigudes)
  * **Storage:** tria l’emmagatzematge de destí

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-50.png}
\end{center}

#### 3. Confirmar i monitorar

* Fes clic a **Restore**
* Segueix el procés mitjançant el registre de tasques
* Quan acabe, comprova que la màquina funciona correctament

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-51.png}
\end{center}

### \emoji{light-bulb} Consells pràctics

*  Fes proves de restauració periòdiques per assegurar que les còpies són vàlides
*  Assigna nous ID o noms per evitar conflictes amb màquines existents
* \emoji{warning} Evita restaurar sobre una màquina activa si no és estrictament necessari

### Resultat

Amb aquest procediment, pots restaurar màquines virtuals i contenidors des del **PBS** amb alta flexibilitat i mínima interrupció del servei, millorant així la continuïtat i seguretat de la infraestructura virtualitzada.

Perfecte! Ací tens el punt **6.6 Estratègia de retenció i rotació de backups**, redactat de manera formal, tècnica i en valencià, seguint la línia del teu projecte:

### \emoji{recycling-symbol} 6.6 Estratègia de Retenció i Rotació de Backups

Una gestió adequada de la **retenció i rotació de còpies de seguretat** és fonamental per a garantir un ús eficient de l’emmagatzematge, així com per assegurar la disponibilitat de punts de restauració recents i rellevants.

###  Objectius de la retenció

* Mantindre còpies suficients per cobrir escenaris de recuperació (errors recents, corrupció, ciberatacs...)
* Evitar la saturació del sistema d’emmagatzematge
* Automatitzar l’eliminació de còpies antigues innecessàries

### \emoji{hammer-and-wrench} Configuració de la política de retenció

En **Proxmox Backup Server (PBS)** es poden definir regles específiques per a cada tasca de backup, o de manera global per a cada **datastore**.

#### \emoji{round-pushpin} Localització:

* `Datacenter → Storage → pbs → Backup Retention

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-55.png}
\end{center}

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-54.png}
\end{center}

#### \emoji{memo} Paràmetres comuns:

| Paràmetre      | Descripció                                 | Exemple |
| -------------- | ------------------------------------------ | ------- |
| `keep-last`    | Nombre d'últimes còpies que es conservaran | 3       |
| `keep-daily`   | Nombre de còpies diàries                   | 7       |
| `keep-weekly`  | Còpies setmanals a mantindre               | 4       |
| `keep-monthly` | Còpies mensuals                            | 6       |
| `keep-yearly`  | Còpies anuals (opcional)                   | 1       |

Aquestes polítiques poden combinar-se per cobrir tant recuperacions recents com arxius històrics.

### \emoji{counterclockwise-arrows-button} Procés de rotació

1. Quan s'executa una nova còpia de seguretat, **PBS comprova si s'excedeixen els límits configurats**
2. Si és així, **pruna (elimina)** les còpies més antigues segons la política definida
3. Aquest procés és **automàtic** i es registra en els **logs** del sistema

### \emoji{light-bulb} Recomanacions

* \emoji{abacus} Defineix polítiques diferents segons la criticitat de cada màquina o servei
* \emoji{spiral-calendar} Combina còpies **diàries** amb còpies **mensuals de llarg termini**
* \emoji{test-tube} Revisa periòdicament l’estat dels datastores i els **logs de prunes**

### Resultat

Amb una estratègia de retenció ben definida, el sistema manté un equilibri entre **disponibilitat de dades** i **optimització de recursos**, evitant tant la pèrdua d’informació com la sobrecàrrega del sistema d’emmagatzematge.

# Zabbix

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