<a name="top"></a>
> Jordi Corbí Micó
> IES JAUME II EL JUST (Tavernes de la Valldiga) - Curso 2023/2025  
> Ciclo: CFGS Administració de Sistemes Informatics en Xarxa 

# Projecte Final de Cicle Superior d'ASIR: Virtualització amb Proxmox

## 📌 Descripció

Aquest projecte consisteix en la implementació d'una infraestructura virtualitzada utilitzant Proxmox VE. L'objectiu principal és optimitzar la gestió de recursos i facilitar la implementació de serveis en un entorn controlat i escalable.

## 🧱 Estructura del projecte

```
Projecte_Proxmox/
├── documentació/
│   ├── README.md
│   │ 
│   └── instalació
│       ├──  proxmox
│       └── proxmox backup
│     
│
│
├── configuració/
│   ├── proxmox/
│   └── proxmox backup server/
├── captures/
├── README.md
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


### 🔧 Possibles millores futures

Una millora plantejada per a futures iteracions del projecte seria la substitució (o complementarietat) dels contenidors Linux basats en LXC per contenidors gestionats mitjançant Docker. Tot i que LXC és una solució eficient i ben integrada dins de Proxmox VE, l'ús de Docker permet aprofitar un ecosistema molt més ampli d’imatges preconfigurades, facilita l'automatització de desplegaments mitjançant Docker Compose o Kubernetes i ofereix una major portabilitat de serveis entre entorns.

Aquesta millora implicaria:

- Instal·lació i configuració de Docker dins de màquines virtuals o contenidors amb suport per a systemd.
- Avaluació de l’ús de Proxmox en combinació amb eines de gestió d’orquestració com *Portainer* o *Rancher* per simplificar l’administració dels contenidors Docker.
- Creació de plantilles de màquines virtuals o contenidors base amb Docker preinstal·lat, per accelerar la posada en marxa de nous serveis.
- Definició de polítiques de seguretat específiques per a l'ús de Docker, especialment en entorns multiusuari.

L’adopció de Docker dins de la infraestructura no substitueix completament els contenidors LXC, però sí que pot aportar més versatilitat, especialment per a aplicacions modernes que es distribueixen com a imatges Docker. A més, obri la porta a una possible futura integració amb entorns de microserveis i tecnologies cloud-native.


### Valoració personal del projecte


---

## 📎 Annexos

## Bibliografia

A continuació es detallen les fonts utilitzades per al desenvolupament del projecte:

1. **Documentació oficial de Proxmox VE**  
   https://pve.proxmox.com/wiki/Main_Page  
   Documentació oficial del sistema de virtualització utilitzat en el projecte.

2. **Debian Wiki**  
   https://wiki.debian.org/  
   Guia oficial del sistema operatiu base emprat per a la configuració dels servidors.

3. **Manual d’OpenSSH**  
   https://man.openbsd.org/ssh  
   Referència per a la configuració segura d’accés remot a través d’SSH.

4. **Stack Overflow**  
   https://stackoverflow.com/  
   Comunitat de suport tècnic per a la resolució de problemes puntuals durant el desenvolupament.

5. **Tutorials de DigitalOcean**  
   https://www.digitalocean.com/community/tutorials  
   Tutorials pràctics per a la configuració de serveis en entorns Linux.
