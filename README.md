<a name="top"></a>
> Jordi Corbí Micó
> IES JAUME II EL JUST (Tavernes de la Valldiga) - Curso 2023/2025  
> Ciclo: CFGS Administració de Sistemes Informatics en Xarxa 

#  Gestió Avanzada en Proxmox

## 📚 Índice

1. [📘 Introducción](#1-introducción)  
2. [🛠️ Análisis y Diseño de la Infraestructura](#2-análisis-y-diseño-de-la-infraestructura)  
3. [💻 Implementación del Clúster Proxmox](#3-implementación-del-clúster-proxmox)  
4. [🗃️ Configuración de Ceph como Almacenamiento Distribuido](#4-configuración-de-ceph-como-almacenamiento-distribuido)  
5. [⚙️ Alta Disponibilidad (HA)](#5-alta-disponibilidad-ha)  
6. [🧰 Proxmox Backup Server (PBS)](#6-proxmox-backup-server-pbs)  
7. [👥 Gestión de Usuarios y Pools de Recursos](#7-gestión-de-usuarios-y-pools-de-recursos)  
8. [🔐 Seguridad y Buenas Prácticas](#8-seguridad-y-buenas-prácticas)  
9. [📄 Documentación Técnica y Manual de Usuario](#9-documentación-técnica-y-manual-de-usuario)  
10. [🧠 Conclusiones y Valoración Personal](#10-conclusiones-y-valoración-personal)  
11. [📎 Anexos](#11-anexos)


## 1. 📘 Introducción

### 1.1. 🎯 Objetivos del proyecto

El objetivo principal de este proyecto es diseñar, implementar y documentar una infraestructura virtualizada de alta disponibilidad utilizando Proxmox VE. El entorno incluye almacenamiento distribuido mediante Ceph y una solución centralizada de copias de seguridad con Proxmox Backup Server (PBS). Todo ello se realiza sobre un clúster compuesto por dos nodos físicos que ofrecen servicios de virtualización, replicación y resiliencia ante fallos.

### 1.2. 🧩 Justificación de la elección de Proxmox VE

Proxmox VE ha sido elegido por ser una plataforma de virtualización de código abierto que ofrece una solución completa y robusta para la gestión de máquinas virtuales y contenedores. Permite la creación de clústeres, integra almacenamiento distribuido con Ceph, ofrece gestión de backups mediante PBS, y soporta alta disponibilidad de manera nativa. Además, su interfaz web intuitiva facilita enormemente las tareas administrativas y de monitoreo, incluso para usuarios con conocimientos medios.

### 1.3. 🗺️ Alcance del proyecto

Este proyecto abarca desde el diseño inicial hasta la implementación y documentación de toda la infraestructura. Incluye:

- Instalación de dos nodos con Proxmox VE y configuración en clúster.
- Configuración e integración de Ceph como sistema de almacenamiento distribuido.
- Implementación de Proxmox Backup Server para copias de seguridad automatizadas.
- Definición de estrategias de alta disponibilidad y recuperación ante fallos.
- Gestión de usuarios y políticas de seguridad.
- Redacción de guías técnicas para administración y uso del entorno.

### 1.4. 🧠 Requisitos previos y conocimientos necesarios

Para llevar a cabo este proyecto, se requieren conocimientos en:

- Sistemas operativos Linux (preferiblemente Debian o derivados).


- Virtualización (KVM, contenedores LXC).
- Conceptos básicos de almacenamiento distribuido y Ceph.
- Gestión de usuarios y políticas de seguridad.
- Uso de línea de comandos y edición de archivos de configuración en Linux.

Además, es recomendable experiencia previa con plataformas de virtualización o administración de servidores en entornos empresariales.