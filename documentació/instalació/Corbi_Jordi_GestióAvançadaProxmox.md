# 📄 Documentación del Proyecto: Gestió Avanzada en Proxmox

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

---

## 1. 📘 Introducción

### 1.1. Objetivos del proyecto

# Documentación del Proyecto: Gestió Avanzada en Proxmox

## Índice

1. [Introducción](#1-introducción)
2. [Análisis y Diseño de la Infraestructura](#2-análisis-y-diseño-de-la-infraestructura)
3. [Implementación del Clúster Proxmox](#3-implementación-del-clúster-proxmox)
4. [Configuración de Ceph como Almacenamiento Distribuido](#4-configuración-de-ceph-como-almacenamiento-distribuido)
5. [Alta Disponibilidad (HA)](#5-alta-disponibilidad-ha)
6. [Proxmox Backup Server (PBS)](#6-proxmox-backup-server-pbs)
7. [Gestión de Usuarios y Pools de Recursos](#7-gestión-de-usuarios-y-pools-de-recursos)
8. [Seguridad y Buenas Prácticas](#8-seguridad-y-buenas-prácticas)
9. [Documentación Técnica y Manual de Usuario](#9-documentación-técnica-y-manual-de-usuario)
10. [Conclusiones y Valoración Personal](#10-conclusiones-y-valoración-personal)
11. [Anexos](#11-anexos)

---

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

## 2. 🛠️ Análisis y Diseño de la Infraestructura

### 2.1. Requisitos funcionales y no funcionales
**Requisitos funcionales:**
- El sistema debe permitir la creación y gestión de máquinas virtuales de forma centralizada.
- Debe proporcionar alta disponibilidad para las cargas críticas.
- Debe contar con un sistema de almacenamiento redundante y escalable (Ceph).
- Debe incluir una solución de backup automatizada y fiable.

**Requisitos no funcionales:**
- Uso de tecnologías open-source y sin costes de licencia.
- Escalabilidad horizontal para añadir nuevos nodos al clúster.
- Alta tolerancia a fallos con recuperación automatizada.
- Facilidad de gestión y administración desde interfaz web.

### 2.2. Topología de red propuesta
La topología contempla una red principal de gestión, una red de almacenamiento para Ceph y otra red opcional para tráfico de backup. Esto separa el tráfico crítico y mejora el rendimiento:

- **🌐 Red de gestión:** Para acceder a la interfaz web, consola y servicios SSH.
- **📡 Red de almacenamiento:** Para la comunicación entre nodos Ceph (alta velocidad recomendada, mínimo 10GbE).
- **🗄️ Red de backup:** Para evitar congestión en la red principal durante los respaldos.

### 2.3. Hardware utilizado
Cada nodo del clúster incluye:
- 🧠 Procesador Intel Xeon o AMD EPYC.
- 💾 Mínimo 32 GB de RAM.
- 📀 Múltiples discos SSD para almacenamiento local y Ceph (mínimo 3 por nodo).
- 🌐 Tarjetas de red de 10 Gbps.
- 🖥️ Un servidor adicional para PBS con almacenamiento dedicado (preferentemente con discos de alta capacidad y rendimiento).

### 2.4. Diseño lógico del clúster Proxmox
El clúster se compone de dos nodos interconectados con Ceph. Se utilizan monitores (MON) y OSDs distribuidos para replicación y tolerancia a fallos. Proxmox Backup Server se conecta al clúster para gestionar backups automáticos.

### 2.5. Consideraciones de alta disponibilidad y tolerancia a fallos
- ⚙️ Configuración de recursos HA con monitorización automática.
- 🧩 Servicios críticos distribuidos para minimizar el impacto ante fallos de hardware.
- 🕒 Sincronización de tiempo mediante NTP para evitar inconsistencias en Ceph y PBS.
- 🧭 Uso de quorum de clúster para evitar el “split-brain”.

## 3. 💻 Implementación del Clúster Proxmox

### 3.1. Instalación de nodos Proxmox VE

1. Instalación del Primer Nodo de Proxmox.

Passos de la Istalación:
   1. 

![alt text](image.png)


![alt text](image-1.png)


![alt text](image-2.png)


![alt text](image-3.png)


![alt text](image-4.png)


![alt text](image-5.png)


![alt text](image-6.png)


![alt text](image-7.png)


![alt text](image-10.png)


![alt text](image-11.png)


# Node 2

![alt text](image-8.png)


![alt text](image-9.png)


![alt text](image-12.png)


![alt text](image-13.png)

### 3.2. Configuración del clúster (pvecm)

### 3.3. Sincronización de tiempo (NTP)

## 4. Configuración de Ceph como Almacenamiento Distribuido

### 4.1. Introducción a Ceph y su integración con Proxmox

### 4.2. Instalación y configuración de Ceph en el clúster

### 4.3. Creación de pools de almacenamiento

### 4.4. Pruebas de rendimiento y replicación

### 4.5. Gestión y monitorización de Ceph

## 5. Alta Disponibilidad (HA)

### 5.1. Activación del gestor HA en Proxmox

### 5.2. Definición de grupos de HA

### 5.3. Pruebas de tolerancia a fallos (failover de VMs)

### 5.4. Casos de uso y recuperación ante caídas de nodos

## 6. Proxmox Backup Server (PBS)

### 6.1. Instalación de PBS

![alt text](image-14.png)


![alt text](image-15.png)


![alt text](image-16.png)


![alt text](image-17.png)


![alt text](image-18.png)


![alt text](image-19.png)


![alt text](image-20.png)


![alt text](image-21.png)


### 6.2. Integración con Proxmox VE

### 6.3. Programación de copias de seguridad

### 6.4. Restauración de máquinas virtuales

### 6.5. Estrategia de retención y rotación de backups

## 7. Gestión de Usuarios y Pools de Recursos

### 7.1. Creación de roles personalizados y permisos

### 7.2. Integración con LDAP (opcional)

### 7.3. Definición de pools de recursos

### 7.4. Gestión delegada y multiusuario

## 8. Seguridad y Buenas Prácticas

### 8.1. Actualización y parches de seguridad

### 8.2. Configuración de firewall en Proxmox

### 8.3. Copias de seguridad de la configuración

### 8.4. Buenas prácticas de administración del clúster

## 9. Documentación Técnica y Manual de Usuario

### 9.1. Manual de instalación paso a paso

### 9.2. Guía de administración del clúster

### 9.3. Procedimientos ante fallos comunes

### 9.4. Manual de uso para usuarios delegados

## 10. Conclusiones y Valoración Personal

### 10.1. Logros alcanzados

### 10.2. Dificultades encontradas y soluciones

### 10.3. Posibles mejoras futuras

### 10.4. Valoración técnica y personal del proyecto

## 11. Anexos

### A. Capturas de pantalla

### B. Scripts y comandos utilizados

### C. Fichas técnicas del hardware

### D. Enlaces de interés y bibliografía







