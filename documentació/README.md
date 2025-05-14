# 📘 Índex del Projecte: Infraestructura Virtualitzada amb **Proxmox VE**  
### Amb Alta Disponibilitat i Còpia de Seguretat Centralitzada

## 1. 🧭 Introducció
- 1.1 Objectius del projecte  
- 1.2 Justificació de l’elecció de Proxmox VE  
- 1.3 Abast del projecte  
- 1.4 Requisits previs i coneixements necessaris  

## 2. 🧱 Anàlisi i Disseny de la Infraestructura
- 2.1 Requisits funcionals i no funcionals  
- 2.2 Topologia de xarxa proposada  
- 2.3 Maquinari utilitzat  
- 2.4 Disseny lògic del clúster Proxmox  
- 2.5 Consideracions d’alta disponibilitat i tolerància a fallades  

## 3. 🖥️ Implementació del Clúster Proxmox
- 3.1 Instal·lació dels nodes Proxmox VE  
- 3.2 Configuració del clúster (`pvecm`)  

## 4. 🧩 Configuració de **Ceph** com a Emmagatzematge Distribuït
- 4.1 Introducció a Ceph i integració amb Proxmox  
- 4.2 Instal·lació i configuració de Ceph al clúster  
- 4.3 Creació de pools d’emmagatzematge  
- 4.4 Proves de rendiment i replicació  
- 4.5 Gestió i monitoratge de Ceph  

## 5. 🛡️ Alta Disponibilitat (**HA**)
- 5.1 Activació del gestor HA en Proxmox  
- 5.2 Definició de grups HA  
- 5.3 Proves de tolerància a fallades (failover de màquines virtuals)  
- 5.4 Casos d’ús i recuperació davant caigudes de nodes  

## 6. 💾 Proxmox Backup Server (**PBS**)
- 6.1 Instal·lació de PBS  
- 6.2 Creació del Datastore
- 6.3 Integració amb Proxmox VE  
- 6.4 Programació de còpies de seguretat  
- 6.5 Restauració de màquines virtuals  
- 6.6 Estratègia de retenció i rotació de backups  

## 7. 👥 Gestió d’Usuaris i Pools de Recursos
- 7.1 Creació de rols personalitzats i permisos  
- 7.2 Definició de pools de recursos  
- 7.3 Gestió delegada i multiusuari  

## 8. 🔐 Seguretat i Bones Pràctiques
- 8.1 Actualitzacions i pegats de seguretat  
- 8.2 Configuració del tallafoc en Proxmox  
- 8.3 Còpies de seguretat de la configuració  
- 8.4 Bones pràctiques d’administració del clúster  
- 8.5 Monitorització del sistema amb **Netdata**

## 9. 📊 Monitoratge Centralitzat amb Zabbix
- 9.1 Què és Zabbix i funcionalitats principals
- 9.2 Justificació de l’elecció de Zabbix front altres solucions (Nagios, Prometheus, Netdata...)
- 9.3 Integració amb la infraestructura virtualitzada de Proxmox VE
- 9.4 Desplegament en Alta Disponibilitat (HA) per garantir la continuïtat del servei
- 9.5 Procés d’instal·lació del servidor Zabbix
- 9.6 Afegeix un host al monitoratge Zabbix

## 10. 📈 Conclusions i Valoració Personal
- 10.1 Objectius assolits  
- 10.2 Dificultats trobades i solucions adoptades  
- 10.3 Possibles millores futures  
- 10.4 Valoració tècnica i personal del projecte  

## 11. 📎 Annexos
- 11.1 Enllaços d’interés i bibliografia  
