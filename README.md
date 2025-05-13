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
│       │    ├── proxmox/
│       │    │   ├──  README.md
│       │    │   └──  install.pdf
│       │    └── proxmox_backup/
│       │        ├──  README.md
│       │        └──  install.pdf
│       │
│       └── configuració/
│           ├── proxmox/
│           │   ├──  README.md
│           │   └──  conf.pdf
│           └── proxmox backup server/
│              ├──  README.md
│              └──  conf.pdf
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

Aquest projecte es basa en la **implementació d’una infraestructura virtualitzada** mitjançant la plataforma **Proxmox Virtual Environment (Proxmox VE)**. L’objectiu principal és **desplegar un clúster d’alta disponibilitat** que permeta **centralitzar la gestió de màquines virtuals (VMs) i contenidors (LXC)**, garantint alhora escalabilitat, eficiència de recursos i tolerància a fallades.

Per aconseguir-ho, s’ha configurat un entorn complet que inclou:

* Un **clúster de Proxmox VE** amb diversos nodes interconnectats.
* Un sistema d’**emmagatzematge distribuït** mitjançant **Ceph**, per assegurar la replicació de dades i la disponibilitat contínua.
* La integració de **Proxmox Backup Server (PBS)** com a sistema de còpia de seguretat centralitzada i amb retenció intel·ligent.
* La configuració d’**Alta Disponibilitat (HA)** per a la continuïtat del servei en cas de caiguda de nodes.
* La monitorització amb **Netdata Cloud**, per obtindre visibilitat en temps real del rendiment i estat del sistema.
* La implementació de **mecanismes de seguretat**, com tallafocs, actualitzacions automatitzades i control d’accés delegat.

Aquest entorn permet simular escenaris reals d’administració de sistemes, facilitant la gestió dels recursos, la protecció de dades i l’automatització de tasques, tot dins d’un marc tècnic robust i preparat per a la producció o entorns educatius avançats.

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

* **CPU:** 16 x Intel(R) Xeon(R) CPU E5-2696 v4 @ 2.20GHz 
* **RAM:** 32 GB DDR4
* **Disc SSD:** 1x 150 GB per a sistema
* **Discos HDD:** 2x 100 TB per a Ceph (OSD)

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

  * Les màquines virtuals considerades crítiques es configuraran amb **HA groups**, de manera que, en cas de fallada d’un node, aquestes es reinicien automàticament en un altre node disponible sense intervenció manual.
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

Aquest projecte m’ha permés consolidar coneixements adquirits durant el cicle formatiu, especialment en àrees com la virtualització, l’alta disponibilitat i la gestió d’infraestructures TI. A través de la implementació pràctica amb **Proxmox VE**, he pogut entendre millor el funcionament dels clústers, l’emmagatzematge distribuït amb **Ceph** i la importància de les còpies de seguretat amb **PBS**.

A nivell acadèmic, ha sigut una experiència molt completa, ja que m’ha ajudat a connectar la teoria amb la pràctica, millorant la meua capacitat d’anàlisi, resolució de problemes i documentació tècnica. Considere que ha sigut un projecte molt útil per a preparar-me de cara a entorns reals i futurs reptes professionals en el sector de les tecnologies de la informació.

---

## 📎 11. Annexos

## 11.1 Bibliografia

A continuació es detallen les fonts utilitzades per al desenvolupament del projecte:

1. Proxmox. *Documentació oficial de Proxmox VE*. Accés 29 d’abril de 2025. [ Proxmox ](https://pve.proxmox.com/wiki/Main_Page).
2. Debian Project. *Debian Wiki*. Accés 25 d’abril de 2025. [Debian](https://wiki.debian.org/).
3. GitHub. *Repo*. Accés de seguit.[ Projecte Proxmox ](https://github.com/jcorbii/Projecte_Proxmox/)
4. Netdata  *Instalació Netdata*. Accés 12 de maig de 2025. [Netdata](https://www.netdata.cloud/)