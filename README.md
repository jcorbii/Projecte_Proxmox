<a name="top"></a>
> Jordi Corbí Micó
> IES JAUME II EL JUST (Tavernes de la Valldiga) - Curs 2023/2025  
> Ciclo: CFGS Administració de Sistemes Informatics en Xarxa

# Projecte Final de Cicle Superior d'ASIR: Gestió Avançada de Proxmox

## 📌 Descripció

Aquest projecte consisteix en la implementació d'una infraestructura virtualitzada utilitzant Proxmox VE. L'objectiu principal és optimitzar la gestió de recursos i facilitar la implementació de serveis en un entorn controlat i escalable.

## 🧱 Estructura del projecte

```
Projecte_Proxmox/
└── README.md
│   └── documentació/
│       │ 
│       ├── instalació/
│       │    ├── proxmox/
│       │    │   ├──  install.md
│       │    │   └──  install.pdf
│       │    └── proxmox_backup/
│       │        ├──  install.md
│       │        └──  install.pdf
│       │
│       └── configuració/
│           ├── proxmox/
│           │   ├──  conf.md
│           │   └──  conf.pdf
│           └── proxmox backup server/
│              ├──  conf.md
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

## 📘 Introducció

### 🎯 Objectius del projecte

L’objectiu principal d’aquest projecte és dissenyar, implementar i documentar una infraestructura virtualitzada d’alta disponibilitat utilitzant Proxmox VE. L’entorn inclou emmagatzematge distribuït mitjançant Ceph i una solució centralitzada de còpies de seguretat amb Proxmox Backup Server (PBS). Tot això es realitza sobre un clúster compost per dos nodes físics que ofereixen serveis de virtualització, replicació i resiliència davant fallades.

### 🧩 Justificació de l’elecció de Proxmox VE

S’ha triat Proxmox VE per ser una plataforma de virtualització de codi obert que ofereix una solució completa i robusta per a la gestió de màquines virtuals i contenidors. Permet la creació de clústers, integra emmagatzematge distribuït amb Ceph, ofereix gestió de backups mitjançant PBS i dona suport a l’alta disponibilitat de manera nativa. A més, la seua interfície web intuïtiva facilita enormement les tasques administratives i de monitoratge, fins i tot per a usuaris amb coneixements mitjans.

### 🗺️ Abast del projecte

Aquest projecte abasta des del disseny inicial fins a la implementació i documentació de tota la infraestructura. Inclou:

- Instal·lació de dos nodes amb Proxmox VE i configuració en clúster.
- Configuració i integració de Ceph com a sistema d’emmagatzematge distribuït.
- Implementació de Proxmox Backup Server per a còpies de seguretat automatitzades.
- Definició d’estratègies d’alta disponibilitat i recuperació davant fallades.
- Gestió d’usuaris i polítiques de seguretat.
- Redacció de guies tècniques per a l’administració i ús de l’entorn.

### 🧠 Requisits previs i coneixements necessaris

Per a dur a terme aquest projecte, es requereixen coneixements en:

- Sistemes operatius Linux (preferiblement Debian o derivats).
- Virtualització (KVM, contenidors LXC).
- Conceptes bàsics d’emmagatzematge distribuït i Ceph.
- Gestió d’usuaris i polítiques de seguretat.
- Ús de línia d’ordres i edició d’arxius de configuració en Linux.

---

## 🧠 Conclusions i Valoració Personal

### Objectius aconseguits

### Dificultats trobades i solucions

⚠️ Problema amb els repositoris de **Proxmox Backup Server**
Una de les principals dificultats trobades ha sigut l’actualització dels paquets del sistema, ja que per defecte, Proxmox Backup Server ve configurat amb els repositoris enterprise, els quals requereixen una subscripció de pagament.

✅ ***Solució tècnica:*** utilitzar repositoris públics
Per tal de poder actualitzar i instal·lar paquets sense necessitat de subscripció, es pot configurar el sistema per a fer ús dels repositoris públics (no enterprise) de **Proxmox.**

---

### 🚀 **Possibles Millores Futures per al Nostre Entorn Proxmox**

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

---

#### **3. Monitorització i Alertes**  
📊 *Sistema proactiu de gestió d’incidents*  
- **Grafana + Prometheus**: Visualització de mètriques en temps real.  
- **Alertes automàtiques** (Telegram/Slack) per:  
  - Caigudes de nodes HA  
  - Espai d’emmagatzematge crític  
- **Auditoria contínua**:  
  ```bash  
  lynis audit system  # Escaneig de vulnerabilitats  
  ```  

---

#### **4. Backup i Recuperació de Desastres**  
💾 *Replicació geogràfica i documentació*  
- **PBS secundari** en altra ubicació:  
  ```bash  
  proxmox-backup-client sync --remote backup2.example.com  
  ```  
- **Playbook de recuperació**: Passos detallats per a:  
  - Restauració de nodes  
  - Recuperació de dades després de fallades greus  

---

#### **5. Xarxa i Aïllament**  
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
| **Monitorització** | Grafana + Alertes automàtiques         | Resposta ràpida a incidents           |  
| **Backup**         | PBS secundari + Playbook               | Resiliencia davant desastres          |  

---

### **🎯 Valoració**  
Aquestes millores convertiran el nostre entorn en un sistema **més robust, segur i fàcil de gestionar**, adaptant-se tant a entorns educatius com empresarials.  

### Valoració personal del projecte


---

## 📎 Annexos

## Bibliografia

A continuació es detallen les fonts utilitzades per al desenvolupament del projecte:

1. Proxmox. *Documentació oficial de Proxmox VE*. Accés 25 d’abril de 2025. https://pve.proxmox.com/wiki/Main_Page.

2. Debian Project. *Debian Wiki*. Accés 25 d’abril de 2025. https://wiki.debian.org/.

3. OpenBSD. *Manual d’OpenSSH*. Accés 25 d’abril de 2025. https://man.openbsd.org/ssh.

4. Stack Overflow. *Stack Overflow*. Accés 25 d’abril de 2025. https://stackoverflow.com/.

5. DigitalOcean. *Tutorials de DigitalOcean*. Accés 25 d’abril de 2025. https://www.digitalocean.com/community/tutorials.

