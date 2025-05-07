##  💻 Implementació del *Clúster* Proxmox

### Instal·lació dels nodes Proxmox VE

#### 🧱 Instal·lació del primer node de Proxmox

**Passos per a la instal·lació:**

1. Baixem la imatge *ISO* de Proxmox des de la [web oficial](https://proxmox.com/en/downloads), triant l’última versió disponible.
2. Una vegada descarregada, la col·loquem en el dispositiu des d'on farem la instal·lació en l’equip.

---

🔸 El primer pas, després de col·locar la *ISO*, és la càrrega del menú *GRUB*, on hem de seleccionar el procés d’instal·lació desitjat. En este cas, triarem l'opció amb interfície gràfica.

![GRUB](../../../img/image.png)

🔸 A continuació, acceptem la **llicència d’ús** del programari.

![Llicència](../../../img/image-1.png)

🔸 En el següent pas, seleccionem en quin disc volem instal·lar Proxmox. En este exemple només tenim un disc disponible, així que el seleccionem. També podem configurar el sistema de fitxers. Triem **ext4**.

![Disc](../../../img/image-2.png)

🔸 Assignem la totalitat de l’espai disponible al disc, ja que només n'hi ha un.

![Espai disc](../../../img/image-3.png)

🔸 Configurem la **zona horària**.

![Zona Horariá](../../../img/image-4.png)
🔸 Introduïm la **contrasenya d’administració** i un **correu electrònic** per a notificacions del sistema.

![Contrasenya i correu](../../../img/image-5.png)

🔸 Assignem el **nom del *host***, la **IP**, el **gateway** i els **DNS**.

![Configuració de xarxa](../../../img/image-6.png)

🔸 Finalment, es mostra un **resum de la configuració** triada. Confirmem i iniciem la instal·lació.

![Resum](../../../img/image-7.png)

🔸 Un cop finalitzada la instal·lació, a la consola apareixerà un missatge indicant que podem accedir a la interfície web de Proxmox via:

```
https://10.10.10.60:8006
```

![Accés web](../../../img/image-10.png)

🔸 Així accedim a la **interfície web de Proxmox VE**:

![Web Proxmox](../../../img/image-11.png)

---

### 🖥️ Instal·lació del Node 2

El procés d’instal·lació del **segon node** és **idèntic** al del primer, excepte pels valors del **nom del host** i la **IP**, que han de ser únics per a cada node.

![Configuració node 2](../../../img/image-8.png)

Com es pot comprovar en el resum, l’única diferència és la IP i el nom del host.

![Resum node 2](../../../img/image-9.png)

Després de completar la instal·lació, tornem a tindre accés a la interfície web per la nova IP configurada:

```
https://10.10.10.61:8006
```

![Accés node 2](../../../img/image-12.png)

I amb això, accedim de nou a la interfície de gestió de Proxmox:

![Web node 2](../../../img/image-13.png)

---

### 🖥️ Instal·lació del Node 3

El procés d’instal·lació del **segon node** és **idèntic** al del primer, excepte pels valors del **nom del host** i la **IP**, que han de ser únics per a cada node.

![Configuració node 3](../../../img/image-29.png)

Com es pot comprovar en el resum, l’única diferència és la IP i el nom del host.

![Resum node 3](../../../img/image-30.png)

Després de completar la instal·lació, tornem a tindre accés a la interfície web per la nova IP configurada:

```
https://10.10.10.58:8006
```

![Accés node 3](../../../img/image-31.png)

I amb això, accedim de nou a la interfície de gestió de Proxmox:

![Web node 3](../../../img/image-32.png)
