<a name="top"></a>
> Jordi Corbí Micó
> IES JAUME II EL JUST (Tavernes de la Valldiga) - Curs 2023/2025  
> Cicle: Administració de Sistemes Informatics en Xarxa

# Projecte Final de Cicle Superior d'ASIR: Gestió Avançada de Proxmox

## 📌 Descripció

Aquest projecte es basa en la **implementació d’una infraestructura virtualitzada** mitjançant la plataforma **Proxmox Virtual Environment (Proxmox VE)**. L’objectiu principal és **desplegar un clúster d’alta disponibilitat** que permeta **centralitzar la gestió de màquines virtuals (VMs) i contenidors (LXC)**, garantint alhora escalabilitat, eficiència de recursos i tolerància a fallades.

Per aconseguir-ho, s’ha configurat un entorn complet que inclou:

* Un **clúster de Proxmox VE** amb diversos nodes interconnectats.
* Un sistema d’**emmagatzematge distribuït** mitjançant **Ceph**, per assegurar la replicació de dades i la disponibilitat contínua.
* La integració de **Proxmox Backup Server (PBS)** com a sistema de còpia de seguretat centralitzada i amb retenció intel·ligent.
* La configuració d’**Alta Disponibilitat (HA)** per a la continuïtat del servei en cas de caiguda de nodes.
* La monitorització amb **Netdata Cloud**, per obtindre visibilitat en temps real del rendiment i estat del sistema.
* La implementació de **mecanismes de seguretat**, com tallafocs, actualitzacions automatitzades i control d’accés delegat.

Aquest entorn permet simular escenaris reals d’administració de sistemes, facilitant la gestió dels recursos, la protecció de dades i l’automatització de tasques, tot dins d’un marc tècnic robust i preparat per a la producció o entorns educatius avançats.

## 🧱 Estructura del projecte

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

## 📄 Contingut

- **Documentació/**: Conté la memòria del projecte i els annexos amb informació detallada sobre la implementació i configuració.
- **README.md**: Aquest fitxer, que proporciona una visió general del projecte.

## ⚙️ Requisits

- Proxmox VE 8.x
- Proxmox Backup Server 
- Maquinari compatible amb virtualització (Intel VT-x o AMD-V)
- Connexió a Internet per a la descàrrega de paquets i actualitzacions

---

## 📘 1. Introducció

### 🔧 **Què és Proxmox VE?**

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

---

### 🎯 1.1 Objectius del projecte

L’objectiu principal d’aquest projecte és dissenyar, desplegar i documentar una infraestructura virtualitzada d’alta disponibilitat basada en **Proxmox VE**, enfocada tant a la resiliència com a la gestió eficient de recursos. El sistema es construeix sobre un clúster format per **tres nodes físics** que ofereixen serveis de virtualització mitjançant **KVM/QEMU**, amb funcionalitats avançades de gestió centralitzada.

Per garantir la disponibilitat i continuïtat del servei davant possibles fallades, s’integra un sistema d’**emmagatzematge distribuït amb Ceph**, proporcionant replicació automàtica, escalabilitat i tolerància a falles. Aquesta arquitectura permet que les màquines virtuals es puguin migrar dinàmicament entre nodes i continuïn funcionant fins i tot en cas de caiguda parcial de la infraestructura.

Com a part essencial del projecte, es desplega també un **Proxmox Backup Server (PBS)** per gestionar de manera centralitzada les còpies de seguretat, amb una estratègia definida de programació, retenció i restauració eficient de màquines virtuals. Això assegura la recuperació ràpida davant d'incidències, i millora la integritat i seguretat de les dades.

L’objectiu final és demostrar la viabilitat i robustesa d’una solució de virtualització empresarial utilitzant tecnologies de codi obert, tot documentant-ne la planificació, implementació, proves de rendiment i mesures de seguretat, amb una orientació clara a l’escalabilitat, la facilitat de manteniment i l’alt rendiment operatiu.

---

### 🧩 1.2 Justificació de l’elecció de Proxmox VE

S’ha triat **Proxmox VE (Virtual Environment)** com a plataforma base del projecte per la seua naturalesa de codi obert, la seua gran comunitat, i la capacitat d’oferir una **solució integral de virtualització** sense requerir llicències comercials costoses. Proxmox combina potents tecnologies com **KVM (Kernel-based Virtual Machine)** per a la virtualització completa i **LXC (Linux Containers)** per a la virtualització lleugera, permetent adaptar-se a diversos escenaris d’ús amb eficiència de recursos.

Una de les característiques clau que ha motivat la seua elecció és la **integració nativa amb Ceph**, un sistema d’emmagatzematge distribuït i tolerant a fallades, així com amb **Proxmox Backup Server (PBS)** per gestionar còpies de seguretat de manera centralitzada, incremental i deduplicada. A més, Proxmox ofereix funcionalitats d’**alta disponibilitat (HA)** amb gestió automàtica del reinici de màquines virtuals en cas de caiguda de nodes, així com **clustering** completament integrat mitjançant `pvecm`.

Comparat amb altres plataformes de virtualització, Proxmox destaca per:

* **VMware vSphere**: Tot i ser una de les solucions més madures i utilitzades en entorns corporatius, implica **alts costos de llicenciament**, especialment si es desitja alta disponibilitat, emmagatzematge compartit o automatització amb vCenter. Proxmox, en canvi, ofereix funcionalitats similars sense cost de llicència i amb un model d’assistència opcional.

* **Microsoft Hyper-V**: Encara que està integrat en sistemes Windows Server, la seua gestió resulta **menys flexible en entorns mixtos Linux/Windows** i sovint requereix eines addicionals com System Center per oferir funcionalitats comparables a les de Proxmox. La integració amb Ceph o tecnologies de codi obert és limitada.

* **Red Hat Virtualization (RHV)**: Basat també en KVM, RHV és una plataforma potent, però **requereix subscripcions comercials** i presenta una corba d’aprenentatge més elevada. Proxmox redueix la complexitat i facilita la posada en marxa mitjançant una **interfície web intuïtiva i unificada**, apta fins i tot per a perfils tècnics intermedis.

Finalment, la disponibilitat de **documentació extensa**, suport de la comunitat i la **rapidesa en desplegament** fan de Proxmox VE una opció ideal per a entorns educatius, laboratoris i pimes, sense renunciar a prestacions pròpies d’entorns empresarials. Aquesta versatilitat i autonomia en la gestió de la infraestructura virtual han estat factors decisius per escollir-lo com a tecnologia base del projecte.

---

### 🧭 1.3 Abast del Projecte

Aquest projecte abasta de manera integral totes les fases necessàries per al desplegament d’una **infraestructura virtualitzada d’alta disponibilitat**, utilitzant tecnologies de codi obert amb un enfocament pràctic i escalable. La planificació, implementació i documentació cobreixen tant la part física com la lògica del sistema, assegurant un entorn robust, segur i fàcilment administrable.

Les accions principals que formen part de l’abast del projecte són:

* **Disseny i desplegament de tres nodes físics** amb **Proxmox VE**, configurats en mode **clúster** per oferir gestió centralitzada, suport a l’alta disponibilitat i funcionalitats avançades com la migració en viu de màquines virtuals.

* **Integració completa amb Ceph** com a sistema d’**emmagatzematge distribuït**, aprofitant la seua capacitat de replicació, resiliència i escalabilitat per garantir la persistència de les dades i la disponibilitat del servei davant falles de maquinari.

* **Instal·lació i configuració de Proxmox Backup Server (PBS)** per implementar una **estratègia automatitzada de còpies de seguretat**, amb suport per backups incrementals, deduplicació i restauració eficient de màquines virtuals.

* **Definició i aplicació d’una arquitectura d’alta disponibilitat (HA)**, incloent mecanismes de failover automatitzat, agrupació de recursos i comprovacions de tolerància a fallades a nivell de node i emmagatzematge.

* **Configuració de rols, usuaris i polítiques de seguretat**, incloent la gestió d’accés, permisos granulars i monitorització d’activitats, tot garantint la seguretat i el control de l’entorn virtualitzat.

* **Elaboració de documentació tècnica detallada**, incloent manuals d’instal·lació pas a pas, guies d’administració del clúster, procediments de recuperació davant incidències i instruccions d’ús per a usuaris delegats.

Aquest abast garanteix no només la posada en marxa del sistema, sinó també la seua operativitat i manteniment a llarg termini, assegurant la continuïtat del servei i la capacitat de resposta davant imprevistos. A més, s’ha tingut en compte la possibilitat d’escalabilitat futura per afegir nous nodes o serveis al clúster.

---

### 🧭 1.4 Requisits Previs i Coneixements Necessaris

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

---

## 🧱 2. Anàlisi i Disseny de la Infraestructura

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

---

### ✅ 2.1 Requisits Funcionals i No Funcionals

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

---

### 🌐 2.2 Topologia de Xarxa Proposada

> En aquest entorn de pràctiques s’ha desplegat un únic servidor físic amb **Proxmox VE** com a hipervisor principal. Dins d’aquest servidor, s’han creat diverses màquines virtuals que simulen els diferents **nodes d’un clúster**, així com un servidor addicional amb **Proxmox Backup Server (PBS)**.
>
> Aquesta arquitectura permet **reproduir un escenari realista** amb alta disponibilitat, emmagatzematge distribuït (Ceph) i còpies de seguretat centralitzades, però en un entorn virtualitzat controlat i sense necessitat de diversos equips físics.

---

### 🖥️ Diagrama:

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

🔧 *Tots els nodes i el PBS són màquines virtuals creades dins del mateix host Proxmox VE.*

---

### 🖥️ 2.3 Maquinari Utilitzat

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

---

### 💰 Pressupost Estimat d’Infraestructura per a Clúster Proxmox amb HA, Ceph i PBS

#### 🖥️ **Nodes del Clúster (x3)**

*Servidors físics amb suport per a virtualització, alta disponibilitat i Ceph*

| Component                                                           | Quantitat | Preu unitari aprox. | Subtotal    |
| ------------------------------------------------------------------- | --------- | ------------------- | ----------- |
| Servidor Proxmox VE (CPU 16 cores, 32-64 GB RAM, SSD + 2x HDD 4 TB) | 3         | 1.200 €             | 3.600 €     |
| Targetes de xarxa addicionals (1/10 Gb) + cablejat                  | 3         | 100 €               | 300 €       |
| **Subtotal nodes del clúster**                                      |           |                     | **3.900 €** |

---

#### 💾 **Servidor de Proxmox Backup Server (PBS)**

*Servidor dedicat per a còpies de seguretat amb alta capacitat i fiabilitat*

| Component                                                       | Quantitat | Preu unitari aprox. | Subtotal    |
| --------------------------------------------------------------- | --------- | ------------------- | ----------- |
| Servidor PBS (CPU 16 cores, 32 GB RAM, SSD + 3x HDD 4 TB RAID)  | 1         | 1.100 €             | 1.100 €     |
| Unitat externa d'emmagatzematge (opcional per backups off-site) | 1         | 300 €               | 300 €       |
| **Subtotal PBS**                                                |           |                     | **1.400 €** |

---

#### 🌐 **Infraestructura de Xarxa i Accessoris**

| Component                                  | Quantitat | Preu unitari aprox. | Subtotal  |
| ------------------------------------------ | --------- | ------------------- | --------- |
| Switch gestionable gigabit/10Gb            | 1         | 400 €               | 400 €     |
| SAI (Sistema d’alimentació ininterrompuda) | 1         | 300 €               | 300 €     |
| Bastidor (rack) i accessoris               | 1         | 250 €               | 250 €     |
| **Subtotal xarxa/accessoris**              |           |                     | **950 €** |

---

### 📄 **Total Pressupost Estimat**

| Part                            | Cost aproximat |
| ------------------------------- | -------------- |
| Nodes del clúster (x3)          | 3.900 €        |
| Proxmox Backup Server (PBS)     | 1.400 €        |
| Infraestructura de xarxa i rack | 950 €          |
| **TOTAL GENERAL**               | **\~6.250 €**  |

---

### 🧾 Notes finals:

* Els preus inclouen maquinari amb capacitat real per executar entorns Ceph i HA amb garantia de rendiment.
* Es poden reduir costos amb equips refurbished o d’ocasió, però aquest pressupost reflecteix una configuració professional i realista.
* No s’han inclòs llicències comercials opcionals de Proxmox (el programari és lliure, però el suport és de pagament si es desitja).

---

### 🧩 2.4 Disseny Lògic del Clúster Proxmox

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

---

### 🛡️ 2.5 Consideracions d’Alta Disponibilitat i Tolerància a Fallades

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

---

# 4. 🧩 Configuració de Ceph com a Emmagatzematge Distribuït

### 🧠 4.1 Introducció a **Ceph** i Integració amb **Proxmox VE**

**Ceph** és una plataforma d’emmagatzematge distribuït de codi obert dissenyada per oferir alta disponibilitat, escalabilitat i rendiment, sense punts únics de fallada. El seu funcionament es basa en tres components principals:

* **OSD (Object Storage Daemon):** Gestiona el disc dur on s’emmagatzema la informació.
* **MON (Monitor):** Controla l’estat del clúster, manté el mapa del clúster i garanteix el consens entre nodes.
* **MGR (Manager):** Proporciona funcionalitats addicionals de monitoratge i interfície web.

Ceph permet oferir emmagatzematge per a:

* Màquines virtuals (amb RBD – Rados Block Device)
* Sistemes d’arxius (CephFS)
* Objectes (compatible amb S3)

---

#### 🔗 Integració amb Proxmox VE

**Proxmox VE** incorpora suport nadiu per a Ceph, cosa que facilita la seua instal·lació, gestió i integració des de la mateixa interfície web o via línia de comandes.

Gràcies a aquesta integració:

* Es pot configurar Ceph directament des de la interfície de **Datacenter → Ceph**
* Els discos Ceph (RBD) poden ser utilitzats com a **emmagatzematge de màquines virtuals** i **contenidors (LXC)**
* El sistema garanteix **alta disponibilitat**, ja que les dades estan replicades en diversos nodes
* Permet una **escala horitzontal** fàcil, afegint més discos o nodes al clúster Ceph

---

💡 **Per què utilitzar Ceph en Proxmox?**

* Elimina la dependència de sistemes d’emmagatzematge extern (NFS, iSCSI, etc.)
* Millora la tolerància a fallades i la continuïtat del servei
* Ofereix una gestió centralitzada i unificada del clúster i l’emmagatzematge

# 5. 🛡️ Alta Disponibilitat (HA)

L’**Alta Disponibilitat (HA)** és un conjunt de tecnologies i configuracions dissenyades per garantir que els serveis crítics d’un sistema **romanguen operatius de manera contínua**, fins i tot davant fallades de maquinari, programari o xarxa. En entorns virtualitzats com **Proxmox VE**, la funcionalitat HA és essencial per assegurar la **mínima interrupció dels serveis** que allotgen màquines virtuals i contenidors.

#### 🎯 Finalitat de la HA:

L'objectiu principal de la HA és **reduir al màxim el temps d’inactivitat (downtime)**. Quan un servidor físic (node) del clúster deixa de funcionar —ja siga per avaria, reinici o manteniment imprevist—, el sistema HA detecta automàticament la fallada i **reinicia les màquines virtuals afectades en un altre node actiu** del clúster, sense intervenció manual.

#### ⚙️ Funcionament dins de Proxmox VE:

Proxmox VE incorpora un subsistema HA que treballa estretament amb **Corosync**, el qual s’encarrega de supervisar la salut dels nodes i mantenir el quòrum del clúster. Les màquines virtuals que es volen protegir es configuren dins de **grups HA**, i el gestor HA pren decisions automàtiques segons l’estat dels nodes.

El sistema HA inclou:

* **Monitoratge constant** dels nodes i serveis.
* **Migració o reinici automàtic** de màquines virtuals en cas de fallida.
* **Policies de gestió de recursos**, com assignació preferida de nodes o prioritats.
* **Integració amb l’emmagatzematge compartit (ex. Ceph)** per garantir que les dades estiguen disponibles des de qualsevol node.

#### 🧩 Avantatges clau:

* **Continuïtat del servei** sense intervencions manuals.
* **Millora de la tolerància a fallades** en entorns crítics.
* **Reducció de riscos de pèrdua de dades** gràcies a la integració amb sistemes com Ceph i PBS.
* **Augment de la confiança operativa**, especialment en serveis que han d’estar actius 24/7.

En resum, la **Alta Disponibilitat** és un component fonamental en infraestructures professionals, ja que **automatitza la resposta davant incidències**, manté els serveis actius i contribueix a una experiència d’usuari contínua i fiable, fins i tot en condicions adverses.

---

# 6. 💾 Proxmox Backup Server (PBS)

**Proxmox Backup Server (PBS)** és una solució de còpia de seguretat **específicament dissenyada per a entorns virtualitzats amb Proxmox VE**. Proporciona una plataforma eficient, ràpida i segura per realitzar **backups i restauracions** de màquines virtuals (VMs), contenidors (CTs) i fins i tot discos individuals, garantint la **protecció i recuperació de dades** davant de fallades o pèrdua d’informació.

#### 🎯 Finalitat de PBS:

PBS s’encarrega de centralitzar totes les còpies de seguretat dels recursos virtuals del clúster, amb funcionalitats com:

* **Backups incrementals**: només es guarden els blocs que han canviat, reduint dràsticament el temps i espai necessari.
* **Compressió i deduplicació**: optimitza l’espai d’emmagatzematge evitant duplicació de dades entre snapshots.
* **Xifratge (opcional)**: garanteix la confidencialitat de les dades tant en repòs com en trànsit.
* **Verificació de consistència**: comprova automàticament la integritat dels backups emmagatzemats.

#### ⚙️ Integració amb Proxmox VE:

PBS s’integra directament amb **Proxmox VE**, permetent configurar des de la pròpia interfície de Proxmox:

* **Jobs de backup programats**, amb horaris i freqüències personalitzades.
* **Estratègies de retenció** per controlar quants snapshots es conserven.
* **Restauracions selectives**, incloent fitxers individuals dins de contenidors o VMs.

Les comunicacions entre Proxmox VE i PBS es realitzen a través del protocol **Proxmox Backup Protocol**, altament optimitzat per rendiment i seguretat.

#### 🔒 Seguretat i Recuperació:

PBS pot situar-se **fora del clúster principal** (recomanat), la qual cosa el converteix en una **última línia de defensa** en cas de fallida total del clúster o corrupció de dades. Aquesta separació física i lògica assegura que, fins i tot si els nodes de Proxmox fallen completament, les còpies de seguretat puguen ser recuperades des d’un sistema aïllat.

#### 🧩 Beneficis principals:

* **Automatització completa de backups i restauracions**.
* **Reducció de l’impacte en el rendiment del clúster** gràcies al backup incremental.
* **Escalabilitat**: un únic PBS pot gestionar còpies de seguretat de múltiples clústers.
* **Integració perfecta** amb la interfície de Proxmox VE i amb suport de CLI i API per a automatitzacions.

En definitiva, **Proxmox Backup Server** és una eina essencial per garantir la **resiliència i recuperació** del sistema virtualitzat, protegint-lo de pèrdues accidentals, errors humans o fallades greus de maquinari.

---

# 👥 7. Gestió d’Usuaris i Pools de Recursos 

La **gestió d’usuaris** dins d’un entorn virtualitzat com **Proxmox VE** és essencial per controlar **qui pot accedir**, **què pot fer** i **sobre quins recursos pot actuar**. Aquesta gestió garanteix la **seguretat, organització i eficiència** en la utilització del sistema, especialment en entorns compartits, corporatius o amb administració delegada.

---

#### 🎯 Finalitat de la gestió d’usuaris:

L’objectiu principal és **definir rols i permisos específics per a cada usuari o grup d’usuaris**, segons les seues responsabilitats o necessitats. Això evita l’accés indegut a recursos crítics i redueix el risc d’errors humans que podrien afectar el funcionament del clúster o les màquines virtuals.

#### ⚙️ Funcionalitats clau a Proxmox VE:

* **Creació d’usuaris locals o via integració externa (LDAP/AD):**
  Permet administrar tant usuaris interns com externs mitjançant sistemes d’autenticació centralitzada.

* **Assignació de rols i permisos granulars:**
  Proxmox VE ofereix un sistema flexible de permisos basat en rols (`roles`) que determina quines accions pot realitzar un usuari (crear, modificar, esborrar màquines, accedir a la consola, gestionar backups, etc.).

* **Delegació d’administració:**
  És possible delegar l’administració parcial del sistema a tècnics o usuaris avançats sense donar-los accés complet, millorant la seguretat i separació de funcions (*principi de privilegi mínim*).

* **Definició de Pools de Recursos:**
  Els *pools* permeten agrupar màquines virtuals, contenidors i recursos assignats a usuaris o equips, facilitant-ne la gestió i limitant el seu accés només a la seua àrea de treball.

#### 🔐 Avantatges de gestionar correctament els usuaris:

* **Millora la seguretat del sistema** evitant accessos no autoritzats o accions destructives.
* **Facilita la traçabilitat** (log dels usuaris i accions realitzades).
* **Permet una administració delegada controlada** en entorns amb múltiples tècnics o departaments.
* **Optimitza l’organització dels recursos**, assignant responsabilitats clares.

En resum, la gestió d’usuaris a Proxmox VE no sols millora la seguretat, sinó que és fonamental per estructurar un entorn **multiusuari estable, escalable i eficient**, tant per a entorns educatius, com empresarials o laboratoris de proves.

---

# 8. 🔐 Seguretat i Bones Pràctiques

### 8.5 Monitorització del sistema amb Netdata

**Netdata** és una eina de monitorització en temps real dissenyada per oferir una visió molt detallada del rendiment de sistemes, aplicacions, contenidors i dispositius IoT. És coneguda per la seva **interfície gràfica intuïtiva** i pel seu enfocament en la **visualització immediata** de dades de rendiment, amb una latència molt baixa.

---

### 🔍 **Què fa Netdata?**

* Recull metadades del sistema (CPU, RAM, disc, xarxa, processos, etc.)
* Monitoritza serveis i aplicacions (MySQL, nginx, docker, etc.)
* Mostra les dades en **temps real (per segon o menys)**
* Pot funcionar com a eina independent o integrat en una arquitectura de monitorització més gran.

---

## 🔄 Comparativa amb altres solucions similars

A continuació tens una comparació amb tres eines populars de monitorització:

| Característica               | **Netdata**              | **Prometheus + Grafana**          | **Zabbix**                       | **Nagios**                  |
| ---------------------------- | ------------------------ | --------------------------------- | -------------------------------- | --------------------------- |
| **Temps real**               | ✔ (mil·lisegons)         | ✘ (intervals mínims de 10-15s)    | ✘ (intervals configurables)      | ✘ (intervals configurables) |
| **Interfície gràfica**       | ✔ Moderna i interactiva  | ✔ (Grafana)                       | ✔ Però més complexa              | ✘ (més bàsic o plugins)     |
| **Facilitat d’instal·lació** | ✔ Molt fàcil (una línia) | ✘ Requereix configurar components | ✘ Requereix bastant configuració | ✘ Pot ser complexa          |
| **Alertes**                  | ✔ Bàsiques integrades    | ✔ Amb Alertmanager                | ✔ Molt completes                 | ✔ Molt completes            |
| **Escalabilitat**            | ✔ Amb Netdata Cloud      | ✔ Alta amb Thanos/Cortex          | ✔ Alta                           | ✔ Mitjana                   |
| **Consum de recursos**       | ✔ Molt lleuger           | ✘ Pot ser alt depenent del cas    | ✘ Pot consumir bastant           | ✔ Lleuger                   |
| **Extensibilitat**           | ✘ Limitada               | ✔ Molt alt                        | ✔ Alt                            | ✔ Alt                       |

---

## ✅ **Avantatges de Netdata**

1. **Instal·lació molt senzilla:** una sola línia de comandes.
2. **Monitorització en temps real real:** actualitzacions per segon o menys.
3. **Poc consum de recursos:** ideal per a sistemes petits o embeguts.
4. **Dades molt detallades:** milers de mètriques disponibles per defecte.
5. **Interfície web interactiva:** gràfics clars i navegació fàcil.
6. **Suport per a contenidors i microserveis.**

---

## ❌ **Inconvenients de Netdata**

1. **No està pensat per a emmagatzematge a llarg termini:** reté dades en memòria per defecte (encara que es pot integrar amb bases de dades de sèries temporals).
2. **Alertes bàsiques:** menys potent que Zabbix o Prometheus+Alertmanager.
3. **Menys integracions corporatives avançades.**
4. **Escalabilitat limitada si no s’utilitza Netdata Cloud.**

---

### 🧩 En resum:

* **Vols veure dades en temps real de manera fàcil i ràpida?** 👉 *Netdata és ideal.*
* **Necessites anàlisi a llarg termini, alertes complexes i integració amb sistemes grans?** 👉 *Millor Prometheus + Grafana o Zabbix.*
* **Tens un entorn molt crític amb necessitat d’alertes robustes i historial llarg?** 👉 *Zabbix o Nagios són més adequats.*

Doncs en el cas dels servidors és millor NetData i per eixe cas m'he quedat en NetData.

---
## 9. 📊 Monitoratge Centralitzat amb Zabbix

### 🔍 9.1 Què és Zabbix i funcionalitats principals

Zabbix és una plataforma de monitoratge open source que permet supervisar en temps real el rendiment i l'estat de sistemes, servidors, màquines virtuals, serveis de xarxa i aplicacions. Proporciona alertes configurables, gràfiques avançades, dashboards personalitzats i recollida d’estadístiques a llarg termini, tot des d’una interfície web centralitzada.

### ✅ 9.2 Justificació de l’elecció de Zabbix front altres solucions

Tot i que existeixen altres plataformes com **Nagios**, **Prometheus** o **Netdata**, s’ha escollit Zabbix per les següents raons tècniques:

* **Monitoratge integral** (nivell de xarxa, sistema, servei i aplicació) en un únic entorn.
* **Compatibilitat nativa amb Proxmox VE**, gràcies a plantilles ja desenvolupades per a la monitorització de nodes, màquines virtuals i serveis Ceph.
* Suport per a **alertes proactives i automatització de respostes** davant esdeveniments.
* Interfície gràfica potent amb panells i visualitzacions configurables per a administradors i usuaris.

A diferència de **Prometheus**, que requereix diversos components externs per una solució completa, o de **Nagios**, que té un enfocament més bàsic i menys visual, **Zabbix ofereix una solució tot-en-u** que s’adapta millor a les necessitats del projecte.

### 🔗 9.3 Integració amb la infraestructura virtualitzada de Proxmox VE

Zabbix es desplegarà com a màquina virtual dins del clúster Proxmox, i mitjançant l’ús d’agents Zabbix i connexions SNMP, es recollirà informació detallada de l’estat de cada node, VM, recursos de Ceph i altres serveis crìtics. S’utilitzaran **templates oficials i personalitzades** per adaptar la monitorització als requisits de l’entorn.

### 🛡️ 9.4 Desplegament en Alta Disponibilitat (HA)

Per garantir la **continuitat del monitoratge fins i tot en cas de fallada d’un node del clúster**, el servidor Zabbix estarà definit com a **recurs d’alta disponibilitat (HA)** dins de Proxmox. Això implica:

* Assignació a un **grup HA**.
* Configuració del servei Zabbix com a recurs gestionat per `ha-manager`.
* En cas de caiguda del node actiu, **el servei es migrarà automàticament** a un altre node disponible, assegurant una supervisió contínua.

---

## 🧠 10. Conclusions i Valoració Personal

### 🎯 10.1 Objectius Aconseguits

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

⚠️ Problema amb els repositoris de **Proxmox Backup Server**
Una de les principals dificultats trobades ha sigut l’actualització dels paquets del sistema, ja que per defecte, Proxmox Backup Server ve configurat amb els repositoris enterprise, els quals requereixen una subscripció de pagament.

✅ ***Solució tècnica:*** utilitzar repositoris públics
Per tal de poder actualitzar i instal·lar paquets sense necessitat de subscripció, es pot configurar el sistema per a fer ús dels repositoris públics (no enterprise) de **Proxmox.**

---

#### ⚠️ Problema amb el almacenament del Ceph:

Durant el procés de configuració i ús del sistema **Ceph** com a emmagatzematge distribuït dins del clúster Proxmox VE, es va presentar una **incidència crítica relacionada amb la pèrdua de redundància de les dades**.

Concretament, després d’un període de funcionament estable, es va detectar que l’estat general del clúster Ceph passava a **WARNING**. L’anàlisi dels logs i l’ús del comandament `ceph status` van indicar que **alguns objectes havien perdut la seua redundància**, mostrant missatges com *“Degraded data redundancy”* o *“Some PGs are undersized”*. La causa principal va ser que el **nivell d’ocupació dels discos OSD havia superat el llindar crític**, impedint a Ceph replicar adequadament els objectes entre nodes.

Aquest comportament és esperable en entorns Ceph, ja que per garantir la replicació i integritat de les dades, el sistema necessita un marge suficient de capacitat lliure. Un cop aquest marge desapareix, el sistema prioritza la protecció de les dades existents però ja **no pot garantir la redundància completa**, fet que suposa un risc en cas de fallada addicional d’un OSD o node.

#### ✅ Solució adoptada:

Per resoldre aquest problema, es va procedir a:

1. **Avaluar l’ocupació real de cada OSD** mitjançant `ceph osd df` per identificar els més saturats.
2. **Alliberar espai en el pool Ceph RBD**, eliminant snapshots innecessaris i còpies de màquines virtuals que no requerien retenció prolongada.
3. **Ampliar la capacitat del clúster**, afegint un nou OSD amb un disc addicional per restablir el balanç de dades i la capacitat de replicació.
4. Un cop recuperada la capacitat suficient, Ceph va **recomençar automàticament el reequilibri (rebalancing)** i va restaurar la redundància completa dels objectes afectats.

Aquesta experiència va posar en relleu la **importància de monitorar proactivament l’espai lliure** dins d’un entorn Ceph i definir alertes abans d’arribar a llindars crítics, així com planificar amb antelació l’escalabilitat del sistema d’emmagatzematge.

---

### 🚀 10.3 Possibles millores futures

#### **1. Docker com a Complement a LXC**  
📌 *Millora la flexibilitat i portabilitat dels contenidors*  
- **Objectiu**: Integrar Docker dins de VMs/containers per aprofitar:  
  - 🐋 Ecosistema més ampli d'imatges preconfigurades  
  - 🔄 Compatibilitat amb Kubernetes i eines CI/CD  
  - 🛠️ Plantilles predefinides amb Docker + Portainer  
- **Reptes**:  
  - Configurar *systemd* en LXC existents  
  - Establir polítiques de seguretat específiques  

---

#### **2. Seguretat Avançada**  
🔐 *Hardening del cluster i xifrat de dades*  
- **Certificats TLS personalitzats**:  
  ```bash  
  pvecm updatecerts -force  # Actualitza certificats autofirmats  
  ```  
- **Xifrat de discs amb LUKS** (per a PBS/Ceph):  
  ```bash  
  cryptsetup luksFormat /dev/sdX  # Xifrat en repòs  
  ```  
- **Integració amb LDAP/AD** per a gestió centralitzada d’usuaris.  
- 
---

#### **3. Xarxa i Aïllament**  
🌐 *Segmentació per a major seguretat*  
- **VLANs dedicades**:  
  ```  
  auto vmbr0.100  
  iface vmbr0.100 inet static  
      address 192.168.100.2/24  
      vlan-raw-device vmbr0  
  ```  
  - Separar trànsit de gestió, Ceph i VMs.  

---

### **📋 Resum de Prioritats**  
| **Àrea**          | **Acció Clau**                          | **Benefici Principal**                |  
|--------------------|----------------------------------------|---------------------------------------|  
| **Contenidors**    | Integració Docker + Portainer          | Portabilitat i ecosistema ampliat     |  
| **Seguretat**      | Hardening + LUKS + LDAP                | Protecció de dades i accés controlat  |  
| **Xarxa**          | VLANs Dedicades                        | Segmentació per a major seguretat     |  

---

### 🎯 10.4 Valoració tècnica i personal del projecte

Aquestes millores convertiran el nostre entorn en un sistema **més robust, segur i fàcil de gestionar**, adaptant-se tant a entorns educatius com empresarials.  

### Valoració personal del projecte

Aquest projecte m’ha permés consolidar coneixements adquirits durant el cicle formatiu, especialment en àrees com la **virtualització**, l’**alta disponibilitat** i la **gestió d’infraestructures TI**. A través de la implementació pràctica amb **Proxmox VE**, he pogut entendre millor el funcionament dels **clústers**, l’**emmagatzematge distribuït amb Ceph** i la importància de les **còpies de seguretat mitjançant PBS**.

A més, la incorporació de **Zabbix com a sistema de monitoratge** ha sigut fonamental per adquirir competències en la supervisió d’entorns TI. La configuració d’agents en sistemes **Windows i Linux**, així com la creació i gestió de *hosts* des de la interfície web de Zabbix, m’ha ajudat a entendre com controlar el rendiment, detectar anomalies i mantenir la salut de la infraestructura en temps real.

A nivell acadèmic, ha sigut una experiència molt completa, ja que m’ha ajudat a connectar la teoria amb la pràctica, millorant la meua **capacitat d’anàlisi, resolució de problemes i documentació tècnica**. Considere que ha sigut un projecte molt útil per a preparar-me de cara a **entorns reals i futurs reptes professionals** en el sector de les tecnologies de la informació.

---

## 📎 11. Annexos

### 11.1 Bibliografia

A continuació es detallen les fonts utilitzades per al desenvolupament del projecte:

1. Proxmox. *Documentació oficial de Proxmox VE*. Accés 29 d’abril de 2025. [ Proxmox ](https://pve.proxmox.com/wiki/Main_Page).
2. Debian Project. *Debian Wiki*. Accés 25 d’abril de 2025. [Debian](https://wiki.debian.org/).
3. GitHub. *Repo*. Accés de seguit.[ Projecte Proxmox ](https://github.com/jcorbii/Projecte_Proxmox/)
4. Netdata  *Instalació Netdata*. Accés 12 de maig de 2025. [Netdata](https://www.netdata.cloud/)
5. Zabbix  *Docuemntació Zabbix*. Accés 14 de maig de 2025. [Zabbix](https://www.zabbix.com/)


# Instalacio

## Proxmox

## 💻 3.  Implementació del *Clúster* Proxmox

### 3.1  Instal·lació dels nodes Proxmox VE

#### 🧱 Instal·lació del primer node de Proxmox

**Passos per a la instal·lació:**

1. Baixem la imatge *ISO* de Proxmox des de la [web oficial](https://proxmox.com/en/downloads), triant l’última versió disponible.
2. Una vegada descarregada, la col·loquem en el dispositiu des d'on farem la instal·lació en l’equip.

---

🔸 El primer pas, després de col·locar la *ISO*, és la càrrega del menú *GRUB*, on hem de seleccionar el procés d’instal·lació desitjat. En este cas, triarem l'opció amb interfície gràfica.


🔸 A continuació, acceptem la **llicència d’ús** del programari.

🔸 En el següent pas, seleccionem en quin disc volem instal·lar Proxmox. En este exemple només tenim un disc disponible, així que el seleccionem. També podem configurar el sistema de fitxers. Triem **ext4**.

<img src="../../../img/image-2.png" alt="GRUB" width="60%">

🔸 Assignem la totalitat de l’espai disponible al disc, ja que només n'hi ha un.

<img src="../../../img/image-3.png" alt="GRUB" width="60%">

🔸 Configurem la **zona horària**.


🔸 Introduïm la **contrasenya d’administració** i un **correu electrònic** per a notificacions del sistema.

🔸 Assignem el **nom del *host***, la **IP**, el **gateway** i els **DNS**.

<img src="../../../img/image-6.png" alt="GRUB" width="60%">

🔸 Finalment, es mostra un **resum de la configuració** triada. Confirmem i iniciem la instal·lació.

<img src="../../../img/image-7.png" alt="GRUB" width="60%">

🔸 Un cop finalitzada la instal·lació, a la consola apareixerà un missatge indicant que podem accedir a la interfície web de Proxmox via:

```
https://10.10.10.60:8006
```

<img src="../../../img/image-8.png" alt="GRUB" width="60%">

🔸 Així accedim a la **interfície web de Proxmox VE**:

<img src="../../../img/image-11.png" alt="GRUB" width="60%">

---

### 🖥️ Instal·lació del Node 2

El procés d’instal·lació del **segon node** és **idèntic** al del primer, excepte pels valors del **nom del host** i la **IP**, que han de ser únics per a cada node.

<img src="../../../img/image-8.png" alt="GRUB" width="60%">

Com es pot comprovar en el resum, l’única diferència és la IP i el nom del host.

<img src="../../../img/image-9.png" alt="GRUB" width="60%">

Després de completar la instal·lació, tornem a tindre accés a la interfície web per la nova IP configurada:

```
https://10.10.10.61:8006
```

<img src="../../../img/image-12.png" alt="GRUB" width="60%">

I amb això, accedim de nou a la interfície de gestió de Proxmox:

<img src="../../../img/image-13.png" alt="GRUB" width="60%">

---

### 🖥️ Instal·lació del Node 3

El procés d’instal·lació del **segon node** és **idèntic** al del primer, excepte pels valors del **nom del host** i la **IP**, que han de ser únics per a cada node.

<img src="../../../img/image-29.png" alt="GRUB" width="60%">

Com es pot comprovar en el resum, l’única diferència és la IP i el nom del host.

<img src="../../../img/image-30.png" alt="GRUB" width="60%">

Després de completar la instal·lació, tornem a tindre accés a la interfície web per la nova IP configurada:

```
https://10.10.10.58:8006
```

<img src="../../../img/image-31.png" alt="GRUB" width="60%">

I amb això, accedim de nou a la interfície de gestió de Proxmox:

<img src="../../../img/image-32.png" alt="GRUB" width="60%">

## Proxmox Backup Server

## 💻 6 Proxmox Backup Server (PBS)

### 6.1 Instalación de PBS

**Passos per a la instal·lació:**

1. Baixem la imatge *ISO* de Proxmox Backup Server des de la [web oficial](https://proxmox.com/en/downloads), triant l’última versió disponible.
2. Una vegada descarregada, la col·loquem en el dispositiu des d'on farem la instal·lació en l’equip.

---

🔸 El primer pas, després de col·locar la *ISO*, és la càrrega del menú *GRUB*, on hem de seleccionar el procés d’instal·lació desitjat. En este cas, triarem l'opció amb interfície gràfica.


🔸 A continuació, acceptem la **llicència d’ús** del programari.


🔸 En el següent pas, seleccionem en quin disc volem instal·lar Proxmox. En este exemple només tenim un disc disponible, així que el seleccionem. També podem configurar el sistema de fitxers. Triem **ext4**.

<img src="../../../img/image-16.png" alt="GRUB" width="60%">

🔸 Introduïm la **contrasenya d’administració** i un **correu electrònic** per a notificacions del sistema.


🔸 Assignem el **nom del *host***, la **IP**, el **gateway** i els **DNS**.

<img src="../../../img/image-18.png" alt="GRUB" width="60%">

🔸 Finalment, es mostra un **resum de la configuració** triada. Confirmem i iniciem la instal·lació.

<img src="../../../img/image-19.png" alt="GRUB" width="60%">

🔸 Un cop finalitzada la instal·lació, a la consola apareixerà un missatge indicant que podem accedir a la interfície web de Proxmox via:

```
https://10.10.10.123:8006
```

<img src="../../../img/image-20.png" alt="GRUB" width="60%">

🔸 Així accedim a la **interfície web de Proxmox VE**:

<img src="../../../img/image-21.png" alt="GRUB" width="60%">

## Zabbix

## 9. 📊 Monitoratge Centralitzat amb **Zabbix**

### 1. Descàrrega de Zabbix

Per començar, accedim a la web oficial de Zabbix: [https://www.zabbix.com](https://www.zabbix.com)

Una vegada dins, cal anar a l’apartat **Download Zabbix**, on seleccionarem:

* La **versió** desitjada (en aquest cas, la 7.2)
* El **sistema operatiu** (Debian 12)
* Els **components** (servidor, frontend, agent)
* El tipus de **base de dades** (MySQL/MariaDB)
* El servidor web (Apache)

<img src="../../../img/image-127.png" alt="GRUB" width="60%">

---

### 2. Instal·lació i configuració del servidor Zabbix

#### a. Instal·lació del repositori oficial

```bash
wget https://repo.zabbix.com/zabbix/7.2/release/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.2+debian12_all.deb
dpkg -i zabbix-release_latest_7.2+debian12_all.deb
apt update
```

<img src="../../../img/image-128.png" alt="GRUB" width="60%">

---

#### b. Instal·lació dels paquets principals

Instal·lem el servidor Zabbix, el frontend web amb Apache, els scripts SQL i l’agent:

```bash
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
```

<img src="../../../img/image-129.png" alt="GRUB" width="60%">

---

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

<img src="../../../img/image-130.png" alt="GRUB" width="60%">

---

#### d. Importació de l’esquema de dades

Des del servidor Zabbix, importem l’esquema i les dades inicials:

```bash
zcat /usr/share/zabbix/sql-scripts/mysql/server.sql.gz | mysql --default-character-set=utf8mb4 -uzabbix -p zabbix
```

<img src="../../../img/image-131.png" alt="GRUB" width="60%">

Després, restaurem el valor per defecte de la directiva `log_bin_trust_function_creators`:

```bash
mysql -uroot -p
```

```sql
SET GLOBAL log_bin_trust_function_creators = 0;
QUIT;
```

<img src="../../../img/image-132.png" alt="GRUB" width="60%">

---

#### e. Configuració del servidor Zabbix

Editem el fitxer de configuració del servidor `/etc/zabbix/zabbix_server.conf` i establim la contrasenya de la base de dades:

```bash
DBPassword=password
```

<img src="../../../img/image-133.png" alt="GRUB" width="60%">

---

#### f. Inici dels serveis

Reiniciem els serveis necessaris i els activem perquè s’inicien automàticament amb el sistema:

```bash
systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
```

<img src="../../../img/image-134.png" alt="GRUB" width="60%">

---

#### g. Accés a la interfície web

Una vegada tot estiga operatiu, podem accedir a la interfície web de Zabbix des del navegador:

```
http://IP_DEL_SERVIDOR/zabbix
```

Des d’ací podrem finalitzar la configuració via web GUI.

<img src="../../../img/image-135.png" alt="GRUB" width="60%">

---

Amb això, el servidor Zabbix queda instal·lat i llest per a ser utilitzat per a la monitorització centralitzada de la infraestructura.

<img src="../../../img/image-137.png" alt="GRUB" width="60%">


# Configuració 

# Proxmox

# 3. 🖥️ Implementació del Clúster Proxmox

A continuació et detallem pas a pas com crear un clúster en Proxmox i unir-hi altres nodes.

---

## 🛠️ 3.2 Configuració del clúster (pvecm)

1. Accedeix a un dels nodes de Proxmox.
2. Ves a **Datacenter → Cluster** des del menú lateral esquerre.
3. Fes clic a **Crear Clúster** (`Create Cluster`).

<img src="../../../img/image-56.png" alt="GRUB" width="60%">

4. Ompli les dades del clúster:

   * **Nom del Clúster**
   * **Interfície de xarxa**
   * Altres paràmetres segons la teua configuració


<img src="../../../img/image-57.png" alt="GRUB" width="60%">


<img src="../../../img/image-58.png" alt="GRUB" width="60%">


1. Un cop creat, veuràs el node com a part del clúster.

<img src="../../../img/image-59.png" alt="GRUB" width="60%">

---

## 🔗 2. Unir Nodes al Clúster

Per afegir un altre node al clúster:

1. Accedeix al segon node i ves a **Datacenter → Cluster**.
2. Fes clic a **Unir-se al clúster** (`Join Cluster`).

<img src="../../../img/image-60.png" alt="GRUB" width="60%">

3. A continuació, hauràs d’introduir la **informació del clúster**.

<img src="../../../img/image-61.png" alt="GRUB" width="60%">


4. Per obtindre aquesta informació, torna al node principal del clúster i fes clic a **Join Information**.

<img src="../../../img/image-62.png" alt="GRUB" width="60%">

5. Copia aquesta informació i torna al node secundari. Enganxa-la al formulari per unir-se.

<img src="../../../img/image-63.png" alt="GRUB" width="60%">


1. Fes clic a **Unir-se**. Si tot és correcte, el node s’afegirà automàticament al clúster.

<img src="../../../img/image-64.png" alt="GRUB" width="60%">

---

## ➕ 3. Afegir més nodes

Per afegir més nodes, repeteix exactament el mateix procés:

* Accedeix al node
* Ves a **Datacenter → Cluster**
* Fes clic a **Unir-se al clúster**
* Copia la informació del node principal
* Enganxa-la i uneix el node

---

🔚 I amb això ja tindràs un clúster Proxmox funcional amb diversos nodes!

<img src="../../../img/image-64.png" alt="GRUB" width="60%">

Perfecte! Comencem pel punt **4.1 Introducció a Ceph i integració amb Proxmox**. Et deixe a continuació una proposta redactada en valencià formal, clara i adequada per al teu projecte:

---

### 🧠 4 Introducció a **Ceph** i Integració amb **Proxmox VE**

### 4.2 ⚙️ Instal·lació i Configuració de **Ceph** al Clúster

La instal·lació de Ceph en un entorn **Proxmox VE** es pot fer de manera centralitzada i senzilla gràcies a la seua integració nativa. A continuació es detallen els passos principals per a desplegar Ceph en un clúster de Proxmox:

---

#### 🧩 Requisits previs

Abans de començar amb la instal·lació, cal assegurar:

* Tots els nodes tenen l’hora sincronitzada via **NTP**
* Una xarxa específica o VLAN dedicada per al trànsit de Ceph (preferiblement amb baixa latència i alta amplada de banda)
* Discos dedicats per a Ceph (no utilitzar el mateix disc que el sistema operatiu)
* Una configuració bàsica del clúster de Proxmox ja establida

---

#### 🛠️ Passos d’instal·lació

1. **Accedir a la interfície web de Proxmox**

   * Ves a `Datacenter → Ceph`

2. **Instal·lar Ceph als nodes**

   * Selecciona cada node on vols desplegar Ceph
   * A l’apartat `Ceph`, fes clic a **Install Ceph**
   * El sistema instal·larà automàticament els paquets necessaris (`ceph`, `ceph-common`, etc.)

<img src="../../../img/image-66.png" alt="GRUB" width="60%">

<img src="../../../img/image-67.png" alt="GRUB" width="60%">

3. **Crear els monitors (MON)**

   * Un mínim de **tres monitors** és recomanat per garantir el quorum
   * Des de l’apartat `Monitor`, fes clic a **Create Monitor**

<img src="../../../img/image-68.png" alt="GRUB" width="60%">

<img src="../../../img/image-69.png" alt="GRUB" width="60%">

4. **Afegir el gestor (MGR)**

   * Necessari per a la interfície gràfica i gestió avançada
   * Crea’l des de la mateixa pestanya amb el botó **Create Manager**

<img src="../../../img/image-70.png" alt="GRUB" width="60%">

5. **Afegir els OSDs (Object Storage Daemons)**

   * Els OSDs són els processos que gestionen els discos durs del clúster
   * Ves a `OSD → Create OSD`, selecciona el disc físic i crea’l
   * Repeteix el procés per a cada node i disc dedicat

<img src="../../../img/image-71.png" alt="GRUB" width="60%">


<p align="center">
<img src="../../../img/image-72.png" alt="GRUB" width="60%">
</p>

* Com tenim 2 discos per cada node (menos en el node 3 que sols hi ha 1)de proxmox haurem de repetir el proccess dos voltes

**Node 1:**

<img src="../../../img/image-73.png" alt="GRUB" width="60%">

**Node 2**

<img src="../../../img/image-74.png" alt="GRUB" width="60%">

**Node 3**

<img src="../../../img/image-75.png" alt="GRUB" width="60%">

1. **(Opcional) Crear un MDS (Metadata Server)**

   * Només si vols utilitzar **CephFS** com a sistema de fitxers compartit

    ##### **📂 Què són els metadades?**
    Els metadades són informació sobre els fitxers, com ara:

    Noms de fitxers i directoris

    Jerarquia de carpetes

    Permisos d’accés

    Propietaris

    Dates de creació o modificació

    
    ##### 🧠 Què fa exactament el MDS?
    
    Quan utilitzes CephFS (el sistema de fitxers distribuït de Ceph), el Metadata Server:

    Controla l’estructura i organització del sistema de fitxers

    Processa operacions com ls, mkdir, rm, mv, etc.

    Fa que les consultes de fitxers siguen ràpides i escalables

    Allibera als OSDs d’aquesta tasca perquè es centren només en llegir i escriure dades

Perfecte! Ací tens el punt **4.3 Creació de pools d’emmagatzematge** redactat de manera formal i clara en valencià, seguint l’estil dels punts anteriors:

---

### 4.3 🏗️ Creació de Pools d’Emmagatzematge en Ceph

Els **pools d’emmagatzematge** són una part fonamental en l’arquitectura de **Ceph**, ja que representen els espais lògics on es distribueixen les dades entre els diferents OSDs del clúster. A cada pool se li pot assignar una funció específica, com ara allotjar màquines virtuals, contenidors o fitxers de CephFS.

---

### 🔍 Què és un Pool?

Un **pool** és una agrupació lògica d’objectes dins del clúster Ceph. Cada objecte dins d’un pool es reparteix entre els OSDs segons una política de distribució definida, garantint així la replicació i la tolerància a fallades.

---

### 🛠️ Creació d’un Pool pas a pas en Proxmox VE

1. Accedeix a la interfície web de **Proxmox VE**
2. Ves a `Datacenter → Ceph → Pools`
3. Fes clic a **Create**

<img src="../../../img/image-76.png" alt="GRUB" width="60%">

4. Emplena els camps següents:



   * **Nom del pool:** (ex. `vm_data`, `cephfs_data`, `backups`)
   * **Nombre de rèpliques (Size):** recomanat mínim **3** per a alta disponibilitat
   * **Min. rèpliques (Min. Size):** mínim **2** per a mantenir el servei actiu amb una fallada
   * **Crush Rule:** regla de distribució entre els dispositius de disc

<p align="center">
<img src="../../../img/image-77.png" alt="GRUB" width="60%">
</p>

1. Fes clic a **Create** i espera a que el pool aparega a la llista

<img src="../../../img/image-78.png" alt="GRUB" width="60%">

Al pas d'un temps podem veure com en els nodes apareix l'almacenament del ceph.

<img src="../../../img/image-79.png" alt="GRUB" width="60%">

---

### 🧠 Consideracions importants

* Els pools amb més rèpliques consumeixen més espai però ofereixen més redundància.
* És possible crear **pools separats** per a diferents usos (ex: un per a VM i un altre per a CephFS).
* Es poden utilitzar **regles CRUSH** per controlar com es distribueixen les dades per racks, discos o ubicacions físiques.

---

### ✅ Resultat

Amb el pool creat, ja pots:

* Assignar-lo com a **emmagatzematge de màquines virtuals (RBD)**
* Utilitzar-lo per a **CephFS**
* Monitorar el seu estat i ús des de la pestanya de **Ceph → Pools**

Perfecte! A continuació et presente el punt **4.4 Proves de rendiment i replicació** redactat de manera formal i clara, mantenint l’estil del teu projecte en valencià:

---

### 4.4 🚀 Proves de Rendiment i Replicació en Ceph

Una vegada el clúster Ceph està desplegat i operatiu, és fonamental realitzar proves de **rendiment** i **replicació** per a verificar el correcte funcionament de l’emmagatzematge distribuït, així com garantir la **fiabilitat** i **eficiència** del sistema.

---

### 📊 Proves de rendiment

Les proves de rendiment ens permeten mesurar la **velocitat de lectura i escriptura** dels dispositius Ceph, així com la **latència** i **capacitat de resposta** del clúster.

#### 🧪 Eines recomanades:

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

<p align="center">
<img src="../../../img/image-80.png" alt="GRUB" width="60%">
</p>

### ✅ Resultat esperat

* Les proves d’escriptura i lectura han de mostrar valors de rendiment estables i adequats segons el teu hardware.
* La replicació ha de funcionar de manera automàtica, garantint la integritat i disponibilitat de les dades davant qualsevol fallada.

#### 📌 Exemple de comandes via CLI

Alternativament, es pot fer la instal·lació via línia de comandes:

```bash
# Instal·lar Ceph
pveceph install

# Crear un monitor
pveceph mon create

# Crear un OSD
pveceph osd create /dev/sdX
```

---

### ✅ Resultat

Una vegada configurats els **MON**, **MGR** i **OSD**, el clúster Ceph estarà operatiu. Ja pots procedir a:

* Crear **pools d’emmagatzematge**
* Assignar-los com a backend per a màquines virtuals
* Monitorar l’estat del clúster des de la interfície de Proxmox

---

### ♻️ Proves de replicació

Ceph replica les dades entre OSDs segons la configuració de rèpliques (per defecte 3). És important verificar que:

1. **Les dades es repliquen correctament** a múltiples discos.
2. **Quan cau un OSD o node**, Ceph automàticament redistribueix les rèpliques.

#### 🔄 Prova de fallada simulada:

1. Apaga un OSD manualment:

   ```bash
   systemctl stop ceph-osd@X
   ```

   (on `X` és el número de l’OSD)


2. Observa com Ceph reporta l’estat *degraded* i com reubica les dades.

<img src="../../../img/image-81.png" alt="GRUB" width="60%">

3. Torna a engegar l’OSD i comprova la **reestructuració automàtica**:

   ```bash
   systemctl start ceph-osd@X
   ```

<img src="../../../img/image-82.png" alt="GRUB" width="60%">

---

### 📈 4.5 Gestió i Monitoratge de **Ceph**

Una vegada desplegat el clúster **Ceph**, és fonamental realitzar una gestió i monitoratge continuat per garantir l’estabilitat, el rendiment i la disponibilitat de les dades. Proxmox VE ofereix una **integració nativa amb Ceph**, que facilita tant el control operatiu com la detecció anticipada de possibles incidències.

---

### 🛠️ Eines de gestió disponibles

Proxmox proporciona diversos mètodes per gestionar Ceph:

#### 📌 Interfície web de Proxmox VE

Des de la GUI es pot accedir a:

* **Estat del clúster**: `Datacenter → Ceph → Status`
* **Gestió d’OSDs**: afegir, eliminar o veure l’estat dels Object Storage Daemons
* **Monitors (MONs)** i **Managers (MGRs)**: estat, creació i falles
* **Creació i eliminació de pools**
* **Configuració i gestió de CephFS**

#### 🔧 Línia de comandes (CLI)

Per a gestió avançada i automatitzacions:

```bash
ceph status             # Estat general del clúster
ceph osd tree           # Visualització jeràrquica dels OSDs
ceph df                 # Ús d’espai en pools
ceph health detail      # Informació detallada de salut
ceph osd out/in <id>    # Marcar un OSD com a fora o dins del clúster
```

---

### 📊 Monitoratge actiu del clúster

Els principals paràmetres a controlar de forma contínua són:

* **Salut del clúster (HEALTH\_OK / WARN / ERR)**
* **Nombre d’OSDs actius i en línia**
* **Estat dels MON i MGR**
* **Ús de l’espai per pool i per OSD**
* **Latències de lectura i escriptura**
* **Rebalanceig de dades en cas de fallada o afegit de nous discos**

---

### 📡 Integració amb eines externes

Encara que Proxmox proporciona visualització bàsica, pots integrar Ceph amb eines de monitoratge més potents com:

* **Prometheus + Grafana** (via Ceph MGR modules)
* **Zabbix** o **Nagios**, mitjançant plugins
* Alertes per correu electrònic o sistemes de notificació

---

### 💡 Recomanacions de manteniment

* 🔁 **Revisar l’estat del clúster regularment**
* 🧪 **Simular fallades controlades** per validar la replicació i recuperació
* 📦 **No sobrecarregar els OSDs**; mantindre un marge de capacitat lliure
* 🛑 **Evitar la pèrdua simultània de múltiples discos** amb rèpliques mínimes

---

### ✅ Resultat

Amb una correcta gestió i monitoratge, es garanteix que el clúster Ceph oferisca un rendiment estable, altament disponible i resistent a fallades, adaptat a les necessitats de l’entorn virtualitzat en Proxmox VE.


Perfecte! Ací tens el punt **5. Alta Disponibilitat (HA)** completament redactat en valencià formal i tècnic, amb icones i una estructura clara per a incloure’l al teu projecte:

---

## 🛡️ 5. Alta Disponibilitat (**HA**) en Proxmox VE

La **Alta Disponibilitat (High Availability)** és una funcionalitat clau en entorns crítics, ja que permet garantir la **continuïtat del servei** davant la caiguda d’un node. Amb Proxmox VE, aquesta característica s’integra de manera nativa quan es treballa amb un **clúster**.

---

### ⚙️ 5.1 Activació del Gestor HA en Proxmox

Per a fer ús de la funcionalitat HA, cal que:

1. El clúster estiga format per almenys **3 nodes** (per mantenir el **quorum**)
2. Els nodes tinguen **Corosync** i **pve-ha-crm** actius
3. Els recursos (VM o CT) estiguen ubicats en **storage compartit** o Ceph

#### 🔄 Procediment:

* Ves a `Datacenter → HA`
* Assegura’t que el **HA Manager** està actiu
* Cada node mostrarà el seu estat (online, standby, etc.)

<p align="center">
<img src="../../../img/image-83.png" alt="GRUB" width="60%">
</p>

---

### 🧩 5.2 Definició de Grups HA

Els **grups HA** permeten organitzar i assignar màquines virtuals o contenidors per a gestionar millor les polítiques de tolerància a fallades.

#### Creació d’un grup HA:

1. Ves a `Datacenter → HA → Groups`

<img src="../../../img/image-84.png" alt="GRUB" width="60%">

1. Fes clic a **Create**
2. Assigna:

<p align="center">
<img src="../../../img/image-85.png" alt="GRUB" width="60%">
</p>

   * **Nom del grup**
   * **Nodes preferits** per executar el servei
   * **Prioritats** (per decidir on s’hauria de migrar en cas de fallada)

Després, quan crees o edites una VM/CT, pots assignar-la a un grup HA.

---

### 🔁 5.3 Proves de Tolerància a Fallades (Failover de Màquines Virtuals)

Per assegurar el correcte funcionament de la configuració HA, és recomanable fer proves de **failover controlades**:

#### Escenari de prova:

1. Assigna una VM a un grup HA

<p align="center">
<img src="../../../img/image-86.png" alt="GRUB" width="60%">
</p>

2. Para o apaga un node manualment

<img src="../../../img/image-87.png" alt="GRUB" width="60%">

3. Observa com la VM és **migrada automàticament** a un altre node disponible
4. Verifica que el servei continua operatiu sense intervenció manual

<img src="../../../img/image-89.png" alt="GRUB" width="60%">

🔍 Es pot monitorar aquest procés des de `Datacenter → HA → Status`.

<img src="../../../img/image-90.png" alt="GRUB" width="60%">

Per descomptat! Ací tens el fragment redactat de manera formal i clara, ideal per afegir com a continuació dins del punt 5.4 o com un subapartat pràctic de **recuperació post-fallada**:

---

### 💡 5.4 Casos d’Ús i Recuperació davant Caigudes de Nodes

Els entorns amb HA actiu poden recuperar-se de forma automàtica en diferents situacions:

* 🔌 **Fallada de hardware o energia** en un node
* 🧯 **Actualitzacions crítiques** que requereixen reinici
* ⚙️ **Errors de sistema** o problemes de rendiment greu

En cada cas:

* El sistema HA detecta la fallada
* Migració automàtica a nodes disponibles
* Restauració del servei amb **temps mínim d’interrupció**

#### Exemple pràctic:

Una màquina virtual crítica (servidor web, base de dades, etc.) està configurada amb HA. Si el node cau inesperadament, aquesta VM es reinicia en un altre node en qüestió de segons, garantint la continuïtat del servei.

---

### ✅ Resultat

Amb la configuració HA en Proxmox VE, es millora significativament la **resiliència de la infraestructura virtualitzada**, assegurant que els serveis essencials estiguen disponibles **24/7**, fins i tot davant fallades greus.

---


### 🔁 Recuperació manual de màquines HA al seu node original

Després d’una **caiguda temporal d’un node** del clúster, el sistema **HA de Proxmox** trasllada automàticament les màquines virtuals o contenidors afectats a un altre node disponible per garantir la continuïtat del servei.

Un cop el node original torna a estar **en línia i estable**, és **recomanable migrar manualment** les màquines al seu node d'origen per:

* Recuperar l’equilibri de càrrega del clúster
* Retornar els recursos als seus entorns habituals
* Preparar el sistema per a futures fallades

---

### ⚙️ Procediment per a migrar una màquina HA al node original

1. Accedeix a la interfície web de Proxmox
2. Ves al node on actualment està executant-se la màquina
3. Selecciona la màquina virtual o contenidor
4. Fes clic a **"Migrate"**
5. Tria com a destinació el **node original** (ex: `node3`)
6. Confirma l’operació

📌 *Nota:* La migració es pot fer en calent (**live migration**) si la màquina suporta aquesta funcionalitat (generalment les VMs amb discs en Ceph o ZFS compartit).

---

### ✅ Resultat

Amb aquest procés, la màquina recupera la seua ubicació inicial, mantenint-se dins del grup HA i **preparada per a futures gestions automàtiques** de tolerància a fallades.

<img src="../../../img/image-91.png" alt="GRUB" width="60%">

---

## 👥 7. Gestió d’Usuaris i Pools de Recursos

En entorns virtualitzats compartits, com un clúster de **Proxmox VE**, és fonamental establir una **gestió d’usuaris estructurada**, amb **permisos diferenciats** i assignació clara de **recursos**, per garantir la **seguretat, control i eficiència operativa**.

---

### 🔐 7.1 Creació de Rols Personalitzats i Permisos

**Proxmox VE** ofereix un sistema de permisos basat en rols, que permet definir què pot fer cada usuari dins del sistema. Aquest model RBAC (Role-Based Access Control) es basa en tres elements:

* **Usuaris** (local, LDAP o via PAM)
* **Rols** (conjunts de permisos)
* **Objectes** (nodes, VM, storage, etc.)

#### 🔧 Creació d’un rol personalitzat:

1. Ves a `Datacenter → Permissions → Roles`
2. Fes clic a **Add**
3. Assigna un nom (ex. `gestor_vm`)
4. Selecciona els permisos específics:

   * `VM.Allocate`
   * `VM.Config.Disk`
   * `VM.Console`
   * `Sys.Console`

<img src="../../../img/image-92.png" alt="GRUB" width="60%">

<img src="../../../img/image-93.png" alt="GRUB" width="60%">

#### ➕ Assignació del rol:

1. Ves a `Permissions → Add → Users`
2. Selecciona:

   * **Path:** àrea de control (`/`, `/vms`, `/pool/nom`, etc.)
   * **User:** usuari o grup
   * **Role:** el rol que has creat

Això permet donar accés restringit a determinats recursos dins del clúster.

<img src="../../../img/image-94.png" alt="GRUB" width="60%">

<img src="../../../img/image-95.png" alt="GRUB" width="60%">

En este cas he creat un usuari de prova per a assignar el rol creat.

<img src="../../../img/image-96.png" alt="GRUB" width="60%">

---

### 🗂️ 7.2 Definició de Pools de Recursos

Els **pools** són agrupacions lògiques de recursos (VMs, CTs, discos, etc.) que permeten facilitar la gestió, especialment en entorns multiusuari o amb departaments diferenciats.

#### 🛠️ Creació d’un pool:

1. Ves a `Datacenter → Permissions → Pools`
2. Fes clic a **Create**

<img src="../../../img/image-97.png" alt="GRUB" width="60%">

1. Emplena:

   * **Nom del pool:** ex. `departament_it`, `desenvolupament`
   * **Descripció** (opcional)

<img src="../../../img/image-98.png" alt="GRUB" width="60%">

1. Afegeix les VMs o CTs desitjades al pool

En este cas anem a fer que el usuari proba puga vore la vm 108(Windows10)

<img src="../../../img/image-99.png" alt="GRUB" width="60%">

Assignacio del pool al usuari proba amb el rol  que hem creat.

<img src="../../../img/image-100.png" alt="GRUB" width="60%">

Els pools són útils per:

* Aplicar permisos a grups d’usuari de forma més eficient
* Organitzar recursos segons projectes o àrees de treball
* Limitar l’accés només a les màquines assignades

---

### 👤 7.3 Gestió Delegada i Multiusuari

Amb els **rols** i **pools**, es pot habilitar un entorn **multiusuari segur**, on cada usuari o equip tinga accés només als recursos que li pertoquen.

#### Exemple de gestió delegada:

* **Usuari:** `anna@pve`
* **Pool assignat:** `marketing_vms`
* **Rol aplicat:** `PVEVMUser` (amb permisos per iniciar/parar/migrar màquines)
* Resultat: Anna només pot gestionar les VMs del pool `marketing_vms`, sense accedir a cap altre recurs del sistema

<img src="../../../img/image-101.png" alt="GRUB" width="60%">

<img src="../../../img/image-102.png" alt="GRUB" width="60%">

<img src="../../../img/image-103.png" alt="GRUB" width="60%">

<img src="../../../img/image-104.png" alt="GRUB" width="60%">

---

### ✅ Beneficis

* 🔒 Major seguretat mitjançant la separació de privilegis
* 👨‍👩‍👧‍👦 Facilitat per delegar la gestió a equips tècnics o usuaris finals
* 🧩 Escalabilitat per a entorns educatius, empresarials o d'hosting

---

### **8.1. Actualitzacions i Pegats de Seguretat**

✅ **Accions recomanades:**

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

---

### **8.2. Configuració del Tallafoc en Proxmox**

✅ **Accions recomanades:**

* Activar el **tallafoc integrat** en Proxmox (GUI: `Datacenter > Firewall`).
* Reglas bàsiques:

  * Permetre només SSH (port 22), accés web de Proxmox (8006) i Ceph (si s’utilitza) des d’IPs de confiança.
  * Bloquejar accessos externs a APIs no necessàries.
* Exemple per permetre accés web només des d’una IP específica:

  ```bash
  pve-firewall localnet add -enable 1 -policy in -action ACCEPT -dport 8006 -source 192.168.1.100
  ```

---

### **8.3. Còpies de Seguretat de la Configuració**

✅ **Accions recomanades:**

* **Fer còpia de seguretat de la configuració del clúster**:

  ```bash
  tar -czvf /backup/proxmox_config_$(date +%Y-%m-%d).tar.gz /etc/pve/
  ```
* **Automatitzar les còpies** amb PBS:

  * Programar còpies diàries/setmanals de VMs/LXCs (GUI: `PBS > Datastore > Backup Jobs`).
  * Utilitzar **retenció incremental** (exemple: 7 còpies diàries + 4 setmanals).

---

### **8.4. Bones Pràctiques d’Administració**

✅ **Accions recomanades:**

* **Activar l’autenticació en dos passos (2FA)** per a la GUI de Proxmox (GUI: `Datacenter > Permissions > Users`).
* **Restringir l'accés per SSH**:

  ```bash
  nano /etc/ssh/sshd_config
  ```

  * Afegir: `PermitRootLogin no`, `PasswordAuthentication no` (usar claus SSH).
* **Monitoratge**:

  * Configurar alertes per correu electrònic (GUI: `Datacenter > Notifications`).
  * Utilitzar `ceph health` i `pveperf` per supervisar el rendiment.

---

### **8.5. Monitoratge Centralitzat amb Netdata Cloud**

**Netdata** és una eina de monitoratge en temps real, lleugera i de codi obert, que permet visualitzar de forma detallada l’ús de CPU, memòria, disc, xarxa, processos i molts altres paràmetres del sistema.

En aquest projecte s’ha optat per utilitzar **Netdata en mode núvol** (*Netdata Cloud*) per garantir:

* 🌐 **Accessibilitat des de qualsevol lloc** amb connexió a Internet
* ☁️ **Alta disponibilitat** sense necessitat de desplegar servidors de monitoratge propis
* 📈 Visualització centralitzada de tots els nodes Proxmox i del PBS en un únic panell

#### 🛠️ Instal·lació i connexió al núvol:

1. Crear un compte gratuït a [https://app.netdata.cloud](https://app.netdata.cloud)
2. En cada node Proxmox:

   * Instal·lar l’agent:

     ```bash
     bash <(curl -Ss https://my-netdata.io/kickstart.sh)
     ```
   * Enllaçar-lo al teu compte Netdata amb la comanda proporcionada pel portal (normalment amb `netdata-claim.sh`)

Després d’això, es podrà visualitzar cada node en temps real des del tauler de **Netdata Cloud**, amb alertes, gràfics detallats i control unificat del rendiment del clúster.

---

### 8.5 Monitorització del sistema amb **Netdata**

#### 🧠 Què és Netdata?

**Netdata** és una plataforma de monitorització en temps real que permet supervisar el rendiment i l’estat de sistemes i serveis de manera molt detallada. És una eina **lleugera**, de **codi obert** i fàcil d’integrar en entorns Linux, incloent **Proxmox VE**.

Proporciona dades sobre:

* Ús de CPU, RAM i disc
* Tràfic i estat de la xarxa
* Estadístiques de processos
* Temperatura, serveis actius, ports, etc.

---

### ☁️ Utilització de **Netdata Cloud** al projecte

En lloc de desplegar una instància de monitorització local o en cada node, en aquest projecte s’utilitzarà la **plataforma centralitzada de Netdata Cloud**.

Aquesta estratègia es basa en instal·lar únicament l’**agent de Netdata** a cada node que es vulga monitoritzar, i connectar-lo al panell de control global de Netdata Cloud.

#### ✅ Avantatges de fer servir el núvol:

* 🔒 **Alta disponibilitat:** La plataforma està disponible 24/7 des de qualsevol lloc
* 🌐 **Accessibilitat centralitzada:** Tots els nodes es poden supervisar des d’un únic panell
* 📈 **Visualització interactiva:** Gràfics en temps real i alertes integrades
* 🧩 **Zero manteniment de servidors de monitoratge locals**
* 🔔 Possibilitat de configurar notificacions (Slack, correu, Discord...)

---

### 🛠️ Procediment bàsic

1. Crear un compte gratuït en [https://app.netdata.cloud](https://app.netdata.cloud)
2. En cada node que es vulga monitoritzar:

   * Instal·lar l’agent amb:

     ```bash
      wget -O /tmp/netdata-kickstart.sh https://get.netdata.cloud/kickstart.sh && sh /tmp/netdata-kickstart.sh --nightly-channel --claim-token 2j7CJC_yS3oDQ9DD4eVlLNMV5ecx0WeqwfvNvfOthCcBCkXRLoysr-TKkc5GLM9BzHmlE9Bb36sQghRHfbOsn4rhSEDnd4TmTaabd__6loq4Vceb_o5BitgLI_1gfT4D5pCzx4o --claim-rooms 6ff6ecc7-275c-4404-a4a0-5fac76e79776 --claim-url https://app.netdata.cloud
     ```

      <img src="../../../img/image-120.png" alt="GRUB" width="60%">

   * Connectar l’agent al compte de Netdata Cloud amb la comanda que proporciona el portal (normalment `netdata-claim.sh`)
3. Accedir al panell de **Netdata Cloud** i visualitzar tots els nodes en temps real

<img src="../../../img/image-121.png" alt="GRUB" width="60%">

---

### ✅ Resultat

Amb aquest sistema, es garanteix una **monitorització eficaç i des de qualsevol lloc**, sense haver de desplegar ni mantindre servidors propis per a l’anàlisi. Netdata Cloud facilita una supervisió **proactiva i àgil** del clúster Proxmox i del Proxmox Backup Server (PBS).

## 🧪 Casos Pràctics de Gestió Delegada i Multiusuari en Proxmox VE

### 🎓 **Cas 1: Entorn educatiu amb alumnes de pràctiques**

#### Escenari:

L’institut ha desplegat un clúster de Proxmox per a alumnes del cicle de sistemes. Cada alumne ha de gestionar una VM pròpia, però sense accés al sistema complet.

#### Configuració:

* **Usuari:** `alumne01@pve`
* **Pool:** `alumnes`
* **VM assignada:** `vm104` (alumne01-ubuntu24)
* **Rol:** `PVEVMUser`

<img src="../../../img/image-105.png" alt="GRUB" width="60%">

<img src="../../../img/image-106.png" alt="GRUB" width="60%">

<img src="../../../img/image-107.png" alt="GRUB" width="60%">

<img src="../../../img/image-108.png" alt="GRUB" width="60%">

<img src="../../../img/image-109.png" alt="GRUB" width="60%">

#### Resultat:

L’alumne pot:

* Engegar/parar la seua VM
* Accedir per consola
* No pot crear ni esborrar màquines
* No pot veure cap altra VM

---

### 🏢 **Cas 2: Departament de Desenvolupament en una empresa**

#### Escenari:

L’equip de desenvolupament necessita accedir a diverses màquines de testing, però no ha de poder modificar la infraestructura general.

#### Configuració:

* **Usuaris:** `david@pve`, `jordi@pve`
* **Pool:** `dev_pool`
* **Rols:** `gestor_vm_custom` (creat amb permisos limitats com `VM.Console`, `VM.Start`, `VM.Shutdown`)

<img src="../../../img/image-110.png" alt="GRUB" width="60%">

<img src="../../../img/image-111.png" alt="GRUB" width="60%">

<img src="../../../img/image-112.png" alt="GRUB" width="60%">

<img src="../../../img/image-113.png" alt="GRUB" width="60%">

<img src="../../../img/image-114.png" alt="GRUB" width="60%">

<img src="../../../img/image-115.png" alt="GRUB" width="60%">

#### Resultat:

Els usuaris poden:

* Utilitzar i gestionar les seues VMs
* No poden crear VMs noves ni modificar configuracions globals

---

### 🛠️ **Cas 3: Tècnic amb accés complet a un node concret**

#### Escenari:

Un tècnic extern col·labora en la gestió de sistemes, però només se li vol donar accés al node `node3`.

#### Configuració:

* **Usuari:** `tecnic@pve`
* **Àrea assignada:** `/nodes/node3`
* **Rol:** `PVEAdmin`

<img src="../../../img/image-116.png" alt="GRUB" width="60%">

<img src="../../../img/image-117.png" alt="GRUB" width="60%">

<img src="../../../img/image-118.png" alt="GRUB" width="60%">

<img src="../../../img/image-119.png" alt="GRUB" width="60%">

#### Resultat:

Té accés complet només a les màquines i configuració d’eixe node, però no pot accedir a altres nodes ni al datacenter.

---

### 🧩 **Cas 4: Hosting amb gestió delegada per client**

#### Escenari:

Una empresa ofereix màquines virtuals com a servei. Cada client gestiona la seua pròpia màquina.

#### Configuració:

* **Client:** `client_a@pve`
* **Pool:** `client_a_pool`
* **VM assignada:** `vm104`
* **Rol:** `PVEVMUser`

<img src="../../../img/image-122.png" alt="GRUB" width="60%">

<img src="../../../img/image-123.png" alt="GRUB" width="60%">

<img src="../../../img/image-124.png" alt="GRUB" width="60%">

<img src="../../../img/image-125.png" alt="GRUB" width="60%">

<img src="../../../img/image-126.png" alt="GRUB" width="60%">

#### Resultat:

Cada client pot administrar la seua pròpia màquina, sense cap visibilitat sobre altres clients o parts del sistema.

---

### ✅ Conclusions dels casos pràctics

Aquests escenaris mostren com Proxmox permet adaptar-se fàcilment a entorns **multiusuari**, amb control granular de permisos i una gestió segura i delegada, mantenint la **seguretat**, **eficiència** i **flexibilitat** del sistema.

---

# Proxmox Backup Server

# 6. 💾 Proxmox Backup Server (PBS)

## 📂 6.2 Creació del Datastore en Proxmox Backup Server

### 🛑 **Requisits previs**

> ⚠️ Tots els discos seran esborrats. Assegura’t que **no continguen dades importants** abans de continuar.

---

### 🔧 1. Verificar instal·lació de ZFS

🔧  Instalar ZFS (si encara no está instalat)

```bash
apt update
apt install zfsutils-linux -y
```

<img src="../../../img/image-22.png" alt="GRUB" width="60%">

Això confirma que el sistema està preparat per a treballar amb pools ZFS.

---

### 🗂️ 2. Creació del ZFS pool

Existien tres opcions principals per a crear el pool ZFS, depenent del nombre de discos disponibles i les necessitats d’emmagatzematge i redundància:

* **Opció A**: `striped` – màxim espai però sense cap tolerància a fallades.
* **Opció B**: `mirror` – redundància completa però requereix un nombre parell de discos.
* **Opció C**: `raidz` – una combinació equilibrada entre espai disponible i tolerància a falles (similar a RAID 5).

👉 **Atés que en aquesta màquina només disposem de tres discos** (`/dev/vda`, `/dev/vdb` i `/dev/vdc`), la millor opció des del punt de vista tècnic és **RAIDZ**, ja que ens ofereix una bona capacitat d’emmagatzematge i alhora permet resistir la fallada d’un disc sense perdre les dades.

<img src="../../../img/image-23.png" alt="GRUB" width="60%">

Per crear el pool:

```bash
zpool create backup-pool raidz /dev/vda /dev/vdb /dev/vdc
```

<img src="../../../img/image-24.png" alt="GRUB" width="60%">

---

### ✅ 3. Verificar l’estat del pool

Després de la creació, podem comprovar que el pool funciona correctament:

```bash
zpool status
```

<img src="../../../img/image-25.png" alt="GRUB" width="60%">

Hauries de veure un estat **ONLINE** i el pool anomenat `backup-pool`.

---

### 🗃️ 4. Crear el datastore en PBS

A través de la interfície web de PBS:

1. Anar a **Datastore > Create**
2. Omplir els camps:

   * **ID**: `zfs-backup`
   * **Path**: `/backup-pool` (punt de muntatge automàtic creat per ZFS)
3. Fer clic a **Create**

- Creació del **Datastore**

<img src="../../../img/image-26.png" alt="GRUB" width="60%">

<img src="../../../img/image-27.png" alt="GRUB" width="60%">

---

### 🔄 5. Comprovació i muntatge automàtic

ZFS gestiona automàticament el muntatge del pool. Per comprovar-ho:

```bash
zfs list
```

Resultat esperat:

```
NAME           USED  AVAIL  REFER  MOUNTPOINT
backup-pool    96K   900G    96K   /backup-pool
```

<img src="../../../img/image-28.png" alt="GRUB" width="60%">

A partir d’aquest moment, el sistema ja pot utilitzar el datastore per a còpies de seguretat, amb les garanties que ofereix ZFS quant a integritat de dades i rendiment.

Perfecte! Ací tens la redacció millorada en **valencià formal**, amb **iconografia** i amb les **faltes corregides**, mantenint el format Markdown:

---

## 💾 6.3 Integració amb Proxmox VE

Per integrar el **Proxmox Backup Server (PBS)** com a sistema d’emmagatzematge dins del clúster de **Proxmox VE**, cal seguir els passos següents:

---

### 🔐 1. Copiar l’**Empremta digital (Fingerprint)** del PBS

Accedeix al **Proxmox Backup Server** i ves a:

📍 `Dashboard → Show Fingerprint`

Esta empremta és necessària per establir una connexió segura entre els nodes de Proxmox VE i el servidor PBS.

<img src="../../../img/image-33.png" alt="GRUB" width="60%">

---

### ➕ 2. Afegir l’Almacenament al Clúster de Proxmox

Una vegada copiada l’empremta, accedim a qualsevol node del clúster de **Proxmox VE** i seguim els passos següents:

1. Ves a **Datacenter → Storage**
2. Fes clic a **Add** i selecciona l’opció **Proxmox Backup Server**

<img src="../../../img/image-34.png" alt="GRUB" width="60%">

---

### 📝 3. Omplir les Dades de Connexió

Ara introduïm la informació requerida del servidor PBS:

<p align="center">
<img src="../../../img/image-36.png" alt="GRUB" width="60%">
</p>

* **ID:** Nom identificador per a l’almacenament
* **Server:** IP o domini del servidor PBS
* **Username:** Nom d’usuari per connectar-se
* **Password:** Contrasenya corresponent
* **Nodes:** Nodes del clúster que tindran accés a l’almacenament
* **Datastore:** Nom del repositori, per exemple `zfs-backups`
* **Namespace:** Espai de noms (opcional, si s’utilitzen subespais dins el datastore)

---

### ✅ 4. Confirmar i Finalitzar

Una vegada configurat, el sistema validarà les dades i l’almacenament PBS apareixerà com a disponible per a fer còpies de seguretat o restauracions.

<img src="../../../img/image-35.png" alt="GRUB" width="60%">

---

🔚 **Amb aquests passos, ja tens el teu Proxmox Backup Server integrat dins del clúster de Proxmox VE.** Això et permet gestionar còpies de seguretat de forma centralitzada, eficient i segura.

Clar! Ací tens la redacció **revisada, tècnica i formal** en valencià, amb correccions gramaticals i millor estructuració del contingut. Mantinc les imatges i el format Markdown:

---

## 💡 6.4 Programació de Còpies de Seguretat i Creació de Màquines Virtuals i Contenidors

En aquest entorn, treballarem tant amb **contenidors (LXC)** com amb **màquines virtuals (KVM)**. Per a gestionar correctament les còpies de seguretat i automatitzar-les, primer hem de tindre clar com es creen els recursos que es volen protegir.

---

### 📦 Descàrrega de plantilles per a Contenidors (CT)

Per a poder crear un contenidor, és necessari **disposar d’un *template*** (plantilla) corresponent al sistema operatiu desitjat.

1. Ves a la secció de **Storage** (almacenament)
2. Selecciona l’opció **Templates**
3. Tens diverses maneres d’obtindre una plantilla:

   * 📤 **Pujar-la manualment** (upload)
   * 🔗 **Descarregar-la des d’una URL externa**
   * 📥 **Utilitzar les plantilles predefinides** que ofereix Proxmox

📌 En el nostre cas, utilitzarem la tercera opció: **plantilles predefinides**

<img src="../../../img/image-37.png" alt="GRUB" width="60%">

Per a aquest projecte, descarregarem i utilitzarem plantilles de:

* **Debian**
* **Fedora**

<img src="../../../img/image-38.png" alt="GRUB" width="60%">

---

### 📁 Preparació per a crear una Màquina Virtual (VM)

Per a crear una màquina virtual, és necessari **pujar una ISO** del sistema operatiu al nostre *storage*. Aquesta ISO s’ubica dins de la categoria de **"ISO Images"**.

1. Ves a `Datacenter → Storage`
2. Selecciona el teu emmagatzematge
3. Fes clic a **Upload**
4. Pujar la imatge ISO corresponent (ex. Debian, Ubuntu, Windows...)

<img src="../../../img/image-39.png" alt="GRUB" width="60%">

---

## 🧱 Creació d’un Contenidor (CT)

Un cop tenim el *template* descarregat, podem crear un contenidor amb els passos següents:

### 🧭 Pas 1: Inici de la creació

1. Fes clic a **Create CT** (Crear CT)

<img src="../../../img/image-40.png" alt="GRUB" width="60%">

---

### 📝 Pas 2: Informació bàsica

Introdueix les dades del contenidor:

* **Node:** on es desplegarà
* **CT ID:** identificador únic
* **Hostname:** nom del sistema
* **Resource Pool:** (opcional) agrupació de recursos
* **Password:** per a l’accés del root

<img src="../../../img/image-41.png" alt="GRUB" width="60%">

---

### 📦 Pas 3: Selecció del *Template*

Selecciona la plantilla que has descarregat anteriorment.

<img src="../../../img/image-42.png" alt="GRUB" width="60%">

---

### 💽 Pas 4: Emmagatzematge

Indica quin **storage** utilitzarà el contenidor.

<img src="../../../img/image-43.png" alt="GRUB" width="60%">

---

### 🧮 Pas 5: Configuració de recursos

* **CPU:** nombre de nuclis assignats
<img src="../../../img/image-44.png" alt="GRUB" width="60%">

* **RAM:** memòria en MB
<img src="../../../img/image-45.png" alt="GRUB" width="60%">

---

### 🌐 Pas 6: Xarxa

Defineix la configuració de xarxa (bridge, IP, VLAN, etc.)

<img src="../../../img/image-46.png" alt="GRUB" width="60%">

---

### ✅ Finalització

Un cop completats tots els passos, el contenidor serà creat i apareixerà a la llista de recursos del node.

<img src="../../../img/image-47.png" alt="GRUB" width="60%">

---

## 🖥️ Creació d’una Màquina Virtual (VM)

Els passos per crear una màquina virtual són **molt similars** als del contenidor, amb l’única diferència que:

* Es selecciona una **ISO** en lloc d’un *template*
* Es configura un **disc virtual** (en format qcow2, raw o ZFS)
* Es defineixen opcions d’instal·lació del sistema operatiu (com si fos una màquina física)

---

🔁 Un cop creats els contenidors i les màquines virtuals, ja es poden **programar còpies de seguretat regulars** mitjançant **Proxmox Backup Server (PBS)** o les eines integrades en Proxmox VE.

Perfecte! A continuació tens el punt **6.4 Restauració de màquines virtuals i contenidors** redactat en valencià formal i tècnic, mantenint la coherència amb l’estructura del teu projecte:

Clar! Ací tens el punt **6.4 Programació de Còpies de Seguretat** (nota: l’has tornat a enumerar com 6.4, però com que ja s’ha usat aquest número, aquest seria realment el **6.5**, a menys que vulgues reorganitzar). Et deixe el contingut redactat tècnicament i en valencià formal:

---

### 🔄  Programació de Còpies de Seguretat

Una correcta **estratègia de programació de còpies de seguretat** és essencial per a garantir la disponibilitat i recuperació de dades en entorns de producció. Amb **Proxmox VE** i la integració amb **Proxmox Backup Server (PBS)**, es pot automatitzar aquest procés de forma eficient.

---

### 🗓️ Planificació de les còpies

La planificació ha de tindre en compte:

* **Freqüència de còpia:** diària, setmanal o mensual segons la criticitat del sistema
* **Hora d’execució:** preferentment fora de l’horari productiu per minimitzar impacte
* **Recursos inclosos:** contenidors, màquines virtuals o pools de recursos
* **Duració esperada:** basada en la mida i nombre de sistemes a protegir

---

### 🧠 Bones pràctiques de planificació

* 🧩 **Dividir per grups de càrrega:** programar còpies per pools o per tipus de màquines
* 🕐 **Evitar solapaments:** distribuint les tasques durant la nit o cap de setmana
* 🧪 **Fer proves de restauració regulars** per validar les còpies

---

### 🔐 Integració amb polítiques de retenció

La programació de còpies de seguretat ha d’anar acompanyada d’una política de **retenció** que mantinga un nombre raonable de còpies antigues per evitar saturació de l’emmagatzematge:

* **Retenció curta:** 7 còpies diàries
* **Retenció mitjana:** 4 setmanals
* **Retenció llarga:** 6 còpies mensuals

Aquesta política es pot aplicar automàticament des de la configuració del **storage** PBS a `Datacenter → Storage → pbs → Backup Retention `.

<p align="center">
  <img src="../../../img/image-53.png" alt="GRUB" width="60%">
</p>

---

### ⚙️ Automatització des de Proxmox VE

Les tasques de còpia es poden programar fàcilment:

1. `Datacenter → Backup → Add`
2. Selecciona:

   * **Storage (PBS)**
   * **Calendari (cron):** ex. `0 21 * * *` per fer-la a les 21:00h cada dia
   * **Mode:** snapshot, suspend o stop
   * **Recursos:** tots, per pool o per ID

<p align="center">
  <img src="../../../img/image-52.png" alt="GRUB" width="60%">
</p>

---

### ✅ Resultat

Amb una programació adequada i una estratègia de retenció ben definida, s'assegura la **protecció contínua de les dades** i es redueix el risc de pèrdua d'informació crítica, mantenint a la vegada l'emmagatzematge net i eficient.

---

### ♻️ 6.5 Restauració de Màquines Virtuals i Contenidors

Una de les funcionalitats més potents del **Proxmox Backup Server (PBS)** és la possibilitat de restaurar còpies de seguretat de manera ràpida i fiable, tant de **màquines virtuals (KVM)** com de **contenidors (LXC)**.

---

### 🔁 Tipus de restauració

Proxmox permet dues modalitats principals de restauració:

* **Restauració completa:** es crea una nova instància basada en la còpia de seguretat
* **Restauració in situ:** reemplaça una màquina existent per una còpia anterior (amb precaució)

---

### 🛠️ Procediment de restauració

#### 1. Accedir al la backup

* Entra a la interfície web del **Proxmox **
* Ves a `Datacenter → Storage → pbs`
* Selecciona la còpia de seguretat desitjada

  <img src="../../../img/image-48.png" alt="GRUB" width="60%">

#### 2. Llençar la restauració

* Fes clic a **Restore**
* Defineix els paràmetres següents:

  * **Target Node:** node de Proxmox on es restaurarà la màquina
  * **VM ID nou:** (opcional) si vols crear una nova màquina amb un altre ID
  * **Mode de restauració:**

    * **Live restore (per a VMs):** restauració mentre la màquina torna a estar en funcionament (recomanat per a entorns amb poca tolerància a caigudes)
  * **Storage:** tria l’emmagatzematge de destí

<p align="center">
  <img src="../../../img/image-50.png" alt="GRUB" width="60%">
</p>

#### 3. Confirmar i monitorar

* Fes clic a **Restore**
* Segueix el procés mitjançant el registre de tasques
* Quan acabe, comprova que la màquina funciona correctament

  <img src="../../../img/image-51.png" alt="GRUB" width="60%">

---

### 💡 Consells pràctics

* ✅ Fes proves de restauració periòdiques per assegurar que les còpies són vàlides
* ✅ Assigna nous ID o noms per evitar conflictes amb màquines existents
* ⚠️ Evita restaurar sobre una màquina activa si no és estrictament necessari

---

### ✅ Resultat

Amb aquest procediment, pots restaurar màquines virtuals i contenidors des del **PBS** amb alta flexibilitat i mínima interrupció del servei, millorant així la continuïtat i seguretat de la infraestructura virtualitzada.

Perfecte! Ací tens el punt **6.6 Estratègia de retenció i rotació de backups**, redactat de manera formal, tècnica i en valencià, seguint la línia del teu projecte:

---

### ♻️ 6.6 Estratègia de Retenció i Rotació de Backups

Una gestió adequada de la **retenció i rotació de còpies de seguretat** és fonamental per a garantir un ús eficient de l’emmagatzematge, així com per assegurar la disponibilitat de punts de restauració recents i rellevants.

---

### 🎯 Objectius de la retenció

* Mantindre còpies suficients per cobrir escenaris de recuperació (errors recents, corrupció, ciberatacs...)
* Evitar la saturació del sistema d’emmagatzematge
* Automatitzar l’eliminació de còpies antigues innecessàries

---

### 🛠️ Configuració de la política de retenció

En **Proxmox Backup Server (PBS)** es poden definir regles específiques per a cada tasca de backup, o de manera global per a cada **datastore**.

#### 📍 Localització:

* `Datacenter → Storage → pbs → Backup Retention

  <img src="../../../img/image-55.png" alt="GRUB" width="60%">

<p align="center">
  <img src="../../../img/image-54.png" alt="GRUB" width="60%">
</p>

#### 📝 Paràmetres comuns:

| Paràmetre      | Descripció                                 | Exemple |
| -------------- | ------------------------------------------ | ------- |
| `keep-last`    | Nombre d'últimes còpies que es conservaran | 3       |
| `keep-daily`   | Nombre de còpies diàries                   | 7       |
| `keep-weekly`  | Còpies setmanals a mantindre               | 4       |
| `keep-monthly` | Còpies mensuals                            | 6       |
| `keep-yearly`  | Còpies anuals (opcional)                   | 1       |

Aquestes polítiques poden combinar-se per cobrir tant recuperacions recents com arxius històrics.

---

### 🔄 Procés de rotació

1. Quan s'executa una nova còpia de seguretat, **PBS comprova si s'excedeixen els límits configurats**
2. Si és així, **pruna (elimina)** les còpies més antigues segons la política definida
3. Aquest procés és **automàtic** i es registra en els **logs** del sistema

---

### 💡 Recomanacions

* 🧮 Defineix polítiques diferents segons la criticitat de cada màquina o servei
* 🗓️ Combina còpies **diàries** amb còpies **mensuals de llarg termini**
* 🧪 Revisa periòdicament l’estat dels datastores i els **logs de prunes**

---

### ✅ Resultat

Amb una estratègia de retenció ben definida, el sistema manté un equilibri entre **disponibilitat de dades** i **optimització de recursos**, evitant tant la pèrdua d’informació com la sobrecàrrega del sistema d’emmagatzematge.

# Zabbix

# 9.6 Incorporació d’un *host* al sistema de monitoratge amb Zabbix

## 🖥️ 1. Afegir un host Windows

Per integrar un sistema Windows al monitoratge mitjançant **Zabbix**, cal seguir els següents passos:

1. Accedir a la pàgina oficial de Zabbix i descarregar el **paquet de l’agent Zabbix** corresponent al sistema operatiu:

<img src="../../../img/image-138.png" alt="GRUB" width="60%">

2. Seleccionar:

   * Sistema operatiu (*Windows*)
   * Versió del servidor Zabbix
   * Tipus de xifrat (si és necessari)
   * Format del paquet

<img src="../../../img/image-139.png" alt="GRUB" width="60%">

3. Un cop descarregat l’instal·lador, executar-lo i seguir l’assistent d’instal·lació:

<img src="../../../img/image-140.png" alt="GRUB" width="60%">
<img src="../../../img/image-141.png" alt="GRUB" width="60%">
<img src="../../../img/image-142.png" alt="GRUB" width="60%">
<img src="../../../img/image-143.png" alt="GRUB" width="60%">

4. Verificar que el **servei de l’agent Zabbix** s’ha iniciat correctament:

<img src="../../../img/image-144.png" alt="GRUB" width="60%">

5. Finalment, accedir a la interfície web de Zabbix i crear el nou host:

   * Menú: **Monitoring → Hosts → Create Host**

<img src="../../../img/image-145.png" alt="GRUB" width="60%">
<img src="../../../img/image-146.png" alt="GRUB" width="60%">

---

## 🐧 2. Afegir un host Linux

Per monitoritzar un sistema Linux, cal seguir aquests passos:

1. Accedir a la web de Zabbix i seleccionar l’agent corresponent al sistema (en aquest cas, per a **SUSE Linux Enterprise Server - SLES**).

<img src="../../../img/image-147.png" alt="GRUB" width="60%">

2. Seguir les instruccions per instal·lar l’agent:

### a. Afegir el repositori oficial de Zabbix:

```bash
rpm -Uvh --nosignature https://repo.zabbix.com/zabbix/7.2/release/sles/15/noarch/zabbix-release-latest-7.2.sles15.noarch.rpm
zypper --gpg-auto-import-keys refresh 'Zabbix Official Repository'
```

<img src="../../../img/image-148.png" alt="GRUB" width="60%">

### b. Instal·lar el paquet de l’agent:

```bash
zypper in zabbix-agent
```

<img src="../../../img/image-149.png" alt="GRUB" width="60%">

### c. Configurar el fitxer de configuració de l’agent:

Modificar el fitxer `/etc/zabbix/zabbix_agentd.conf` per definir:

* `Server=` IP del servidor Zabbix
* `Hostname=` nom del dispositiu

<img src="../../../img/image-150.png" alt="GRUB" width="60%">
<img src="../../../img/image-151.png" alt="GRUB" width="60%">

### d. Iniciar i habilitar el servei de l’agent:

```bash
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

<img src="../../../img/image-152.png" alt="GRUB" width="60%">

3. Afegir el nou host des de la interfície web del servidor Zabbix:

<img src="../../../img/image-153.png" alt="GRUB" width="60%">

Un cop afegits els sistemes, apareixeran llistats a l’apartat de *Hosts*:

<img src="../../../img/image-154.png" alt="GRUB" width="60%">

---

🔍 Amb aquest procés, tant equips Windows com Linux poden ser incorporats al sistema de monitoratge, permetent la supervisió de mètriques com consum de CPU, ús de memòria, estat dels serveis i molt més, tot centralitzat des del panell de control de Zabbix.