# 3. 🖥️ Implementació del Clúster Proxmox

A continuació et detallem pas a pas com crear un clúster en Proxmox i unir-hi altres nodes.

---

## 🛠️ 1. Crear el Clúster

1. Accedeix a un dels nodes de Proxmox.
2. Ves a **Datacenter → Cluster** des del menú lateral esquerre.
3. Fes clic a **Crear Clúster** (`Create Cluster`).

![Pantalla inicial del cluster](image.png)



4. Ompli les dades del clúster:

   * **Nom del Clúster**
   * **Interfície de xarxa**
   * Altres paràmetres segons la teua configuració

<p align="center">
  <img src="image-1.png" alt="Crear cluster pas 1" />
</p>

<p align="center">
  <img src="image-2.png" alt="Crear cluster pas 2" />
</p>

5. Un cop creat, veuràs el node com a part del clúster.

![Cluster creat](image-3.png)

---

## 🔗 2. Unir Nodes al Clúster

Per afegir un altre node al clúster:

1. Accedeix al segon node i ves a **Datacenter → Cluster**.
2. Fes clic a **Unir-se al clúster** (`Join Cluster`).

![Unir-se al cluster](image-4.png)

3. A continuació, hauràs d’introduir la **informació del clúster**.

<p align="center">
  <img src="image-5.png" alt="Formulari unir-se" />
</p>

4. Per obtindre aquesta informació, torna al node principal del clúster i fes clic a **Join Information**.

![Informació per unir-se](image-6.png)

5. Copia aquesta informació i torna al node secundari. Enganxa-la al formulari per unir-se.

<p align="center">
  <img src="image-7.png" alt="Enganxar informació" />
</p>

6. Fes clic a **Unir-se**. Si tot és correcte, el node s’afegirà automàticament al clúster.

![Node afegit](image-8.png)

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

![Comprovació](image-9.png)

Perfecte! Comencem pel punt **4.1 Introducció a Ceph i integració amb Proxmox**. Et deixe a continuació una proposta redactada en valencià formal, clara i adequada per al teu projecte:

---

### 🧠 4 Introducció a **Ceph** i Integració amb **Proxmox VE**

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

Perfecte! Ací tens el punt **4.2 Instal·lació i configuració de Ceph al clúster**, redactat en valencià formal i pensat per a un projecte tècnic:

---

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

![alt text](image-10.png)

![alt text](image-11.png)

3. **Crear els monitors (MON)**

   * Un mínim de **tres monitors** és recomanat per garantir el quorum
   * Des de l’apartat `Monitor`, fes clic a **Create Monitor**

![alt text](image-12.png)

![alt text](image-13.png)

4. **Afegir el gestor (MGR)**

   * Necessari per a la interfície gràfica i gestió avançada
   * Crea’l des de la mateixa pestanya amb el botó **Create Manager**

![alt text](image-14.png)

5. **Afegir els OSDs (Object Storage Daemons)**

   * Els OSDs són els processos que gestionen els discos durs del clúster
   * Ves a `OSD → Create OSD`, selecciona el disc físic i crea’l
   * Repeteix el procés per a cada node i disc dedicat

![alt text](image-15.png)


<p align="center">
  <img src="image-16.png" alt="Enganxar informació" />
</p>

* Com tenim 2 discos per cada node (menos en el node 3 que sols hi ha 1)de proxmox haurem de repetir el proccess dos voltes

**Node 1:**

![alt text](image-17.png)

**Node 2**

![alt text](image-18.png)

**Node 3**

![alt text](image-19.png)

6. **(Opcional) Crear un MDS (Metadata Server)**

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

![alt text](image-20.png)

4. Emplena els camps següents:



   * **Nom del pool:** (ex. `vm_data`, `cephfs_data`, `backups`)
   * **Nombre de rèpliques (Size):** recomanat mínim **3** per a alta disponibilitat
   * **Min. rèpliques (Min. Size):** mínim **2** per a mantenir el servei actiu amb una fallada
   * **Crush Rule:** regla de distribució entre els dispositius de disc

<p align="center">
  <img src="image-21.png" alt="Creació de pool en Proxmox" />
</p>

1. Fes clic a **Create** i espera a que el pool aparega a la llista

![alt text](image-22.png)

Al pas d'un temps podem veure com en els nodes apareix l'almacenament del ceph.

![alt text](image-23.png)

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
  <img src="image-24.png" alt="Creació de pool en Proxmox" />
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

![Observar Ceph](image-25.png)

3. Torna a engegar l’OSD i comprova la **reestructuració automàtica**:

   ```bash
   systemctl start ceph-osd@X
   ```

![Restauració](image-26.png)

---
Perfecte! A continuació et redacte el punt **4.5 Gestió i monitoratge de Ceph**, amb to tècnic, formal i en valencià, adaptat per al teu projecte de forma clara i estructurada:

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
  <img src="image-27.png" alt="Gestor HA" />
</p>

---

### 🧩 5.2 Definició de Grups HA

Els **grups HA** permeten organitzar i assignar màquines virtuals o contenidors per a gestionar millor les polítiques de tolerància a fallades.

#### Creació d’un grup HA:

1. Ves a `Datacenter → HA → Groups`

![alt text](image-28.png)

1. Fes clic a **Create**
2. Assigna:

<p align="center">
  <img src="image-29.png" alt="Gestor HA" />
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
  <img src="image-30.png" alt="Gestor HA" />
</p>

2. Para o apaga un node manualment

![alt text](image-31.png)

3. Observa com la VM és **migrada automàticament** a un altre node disponible
4. Verifica que el servei continua operatiu sense intervenció manual

🔍 Es pot monitorar aquest procés des de `Datacenter → HA → Status`.

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

Vols que continue amb la secció **6. Proxmox Backup Server (PBS)** o vols que t’ajude a fer una portada o resum del projecte?
