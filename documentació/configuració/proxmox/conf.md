---
title: "Configuració Proxmox"
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

\section*{7. \emoji{busts-in-silhouette} Gestió d’Usuaris i Pools de Recursos}
\begin{itemize}
  \item 7.1 Creació de rols personalitzats i permisos  
  \item 7.2 Definició de pools de recursos  
  \item 7.3 Gestió delegada i multiusuari  
\end{itemize}

\newpage

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