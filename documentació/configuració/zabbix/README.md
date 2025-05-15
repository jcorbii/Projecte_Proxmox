# 9.6 Incorporació d’un *host* al sistema de monitoratge amb Zabbix

## 🖥️ 1. Afegir un host Windows

Per integrar un sistema Windows al monitoratge mitjançant **Zabbix**, cal seguir els següents passos:

1. Accedir a la pàgina oficial de Zabbix i descarregar el **paquet de l’agent Zabbix** corresponent al sistema operatiu:

[alt text](../../../img/image-138.png)

2. Seleccionar:

   * Sistema operatiu (*Windows*)
   * Versió del servidor Zabbix
   * Tipus de xifrat (si és necessari)
   * Format del paquet

[alt text](../../../img/image-139.png)

3. Un cop descarregat l’instal·lador, executar-lo i seguir l’assistent d’instal·lació:

[alt text](../../../img/image-140.png)
[alt text](../../../img/image-141.png)
[alt text](../../../img/image-142.png)
[alt text](../../../img/image-143.png)

4. Verificar que el **servei de l’agent Zabbix** s’ha iniciat correctament:

[alt text](../../../img/image-144.png)

5. Finalment, accedir a la interfície web de Zabbix i crear el nou host:

   * Menú: **Monitoring → Hosts → Create Host**

[alt text](../../../img/image-145.png)
[alt text](../../../img/image-146.png)

---

## 🐧 2. Afegir un host Linux

Per monitoritzar un sistema Linux, cal seguir aquests passos:

1. Accedir a la web de Zabbix i seleccionar l’agent corresponent al sistema (en aquest cas, per a **SUSE Linux Enterprise Server - SLES**).

[alt text](../../../img/image-147.png)

2. Seguir les instruccions per instal·lar l’agent:

### a. Afegir el repositori oficial de Zabbix:

```bash
rpm -Uvh --nosignature https://repo.zabbix.com/zabbix/7.2/release/sles/15/noarch/zabbix-release-latest-7.2.sles15.noarch.rpm
zypper --gpg-auto-import-keys refresh 'Zabbix Official Repository'
```

[alt text](../../../img/image-148.png)

### b. Instal·lar el paquet de l’agent:

```bash
zypper in zabbix-agent
```

[alt text](../../../img/image-149.png)

### c. Configurar el fitxer de configuració de l’agent:

Modificar el fitxer `/etc/zabbix/zabbix_agentd.conf` per definir:

* `Server=` IP del servidor Zabbix
* `Hostname=` nom del dispositiu

[alt text](../../../img/image-150.png)
[alt text](../../../img/image-151.png)

### d. Iniciar i habilitar el servei de l’agent:

```bash
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

[alt text](../../../img/image-152.png)

3. Afegir el nou host des de la interfície web del servidor Zabbix:

[alt text](../../../img/image-153.png)

Un cop afegits els sistemes, apareixeran llistats a l’apartat de *Hosts*:

[alt text](../../../img/image-154.png)

---

🔍 Amb aquest procés, tant equips Windows com Linux poden ser incorporats al sistema de monitoratge, permetent la supervisió de mètriques com consum de CPU, ús de memòria, estat dels serveis i molt més, tot centralitzat des del panell de control de Zabbix.
