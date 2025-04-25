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
│   ├── instalació
│       ├──proxmox
│         ├── proxmox backup
│   │       
│   │
│   │
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



## 📘 Introducción

###  🎯 Objetivos del proyecto

El objetivo principal de este proyecto es diseñar, implementar y documentar una infraestructura virtualizada de alta disponibilidad utilizando Proxmox VE. El entorno incluye almacenamiento distribuido mediante Ceph y una solución centralizada de copias de seguridad con Proxmox Backup Server (PBS). Todo ello se realiza sobre un clúster compuesto por dos nodos físicos que ofrecen servicios de virtualización, replicación y resiliencia ante fallos.

###  🧩 Justificación de la elección de Proxmox VE

Proxmox VE ha sido elegido por ser una plataforma de virtualización de código abierto que ofrece una solución completa y robusta para la gestión de máquinas virtuales y contenedores. Permite la creación de clústeres, integra almacenamiento distribuido con Ceph, ofrece gestión de backups mediante PBS, y soporta alta disponibilidad de manera nativa. Además, su interfaz web intuitiva facilita enormemente las tareas administrativas y de monitoreo, incluso para usuarios con conocimientos medios.

###  🗺️ Alcance del proyecto

Este proyecto abarca desde el diseño inicial hasta la implementación y documentación de toda la infraestructura. Incluye:

- Instalación de dos nodos con Proxmox VE y configuración en clúster.
- Configuración e integración de Ceph como sistema de almacenamiento distribuido.
- Implementación de Proxmox Backup Server para copias de seguridad automatizadas.
- Definición de estrategias de alta disponibilidad y recuperación ante fallos.
- Gestión de usuarios y políticas de seguridad.
- Redacción de guías técnicas para administración y uso del entorno.

###  🧠 Requisitos previos y conocimientos necesarios

Para llevar a cabo este proyecto, se requieren conocimientos en:

- Sistemas operativos Linux (preferiblemente Debian o derivados).


- Virtualización (KVM, contenedores LXC).
- Conceptos básicos de almacenamiento distribuido y Ceph.
- Gestión de usuarios y políticas de seguridad.
- Uso de línea de comandos y edición de archivos de configuración en Linux.


##  🧠 Conclusiones y Valoración Personal

###  Logros alcanzados

###  Dificultades encontradas y soluciones

###  Posibles mejoras futuras

###  Valoración técnica y personal del proyecto

##  📎 Anexos

## Bibliografia

A continuació es detallen les fonts utilitzades per al desenvolupament del projecte:

1. **Proxmox VE Official Documentation**  
   https://pve.proxmox.com/wiki/Main_Page  
   Documentació oficial del sistema de virtualització utilitzat en el projecte.

2. **Debian Wiki**  
   https://wiki.debian.org/  
   Guia oficial del sistema operatiu base emprat per a la configuració dels servidors.

3. **OpenSSH Manual**  
   https://man.openbsd.org/ssh  
   Referència per a la configuració segura d'accés remot a través d’SSH.

4. **Stack Overflow**  
   https://stackoverflow.com/  
   Comunitat de suport tècnic per a la resolució de problemes puntuals durant el desenvolupament.

5. **DigitalOcean Tutorials**  
   https://www.digitalocean.com/community/tutorials  
   Tutorials pràctics per a la configuració de serveis en entorns Linux.





