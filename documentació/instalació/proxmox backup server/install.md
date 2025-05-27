---
title: "Projecte Final de Cicle Superior d'ASIX: Gestió Avançada de Proxmox"
titlepage: true
subtitle: "Jordi Corbí Micó"
lang: es
documentclass: scrartcl
toc-own-page: true
toc-title: Índex
numbersections: false
titlepage-rule-height: 0
titlepage-text-color: "7714C6"
titlepage-background: "../../backgrounds/background5.pdf"
footer-left: IES Jaume II el Just - Projecte ASIX
footer-right: \thepage/\pageref{LastPage}
header-includes:
    - \usepackage{graphicx}
    - \usepackage{lastpage}
    - \usepackage{xltxtra}
    - \usepackage{listings}
    - \usepackage{pdflscape}
    - \usepackage{xcolor,tikz,tcolorbox}
    - \usepackage{emoji}
    - \setemojifont{Twemoji Mozilla}
    - \tcbuselibrary{raster}
    - \definecolor{lightblue}{rgb}{0.68, 0.85, 0.9}
    - \definecolor{ballblue}{rgb}{0.13, 0.67, 0.8}
    - \definecolor{cerulean}{rgb}{0.0, 0.48, 0.65}
    - \definecolor{almond}{rgb}{0.94, 0.87, 0.8}
    - \definecolor{apricot}{rgb}{0.98, 0.81, 0.69}
    - \definecolor{cream}{rgb}{1.0, 0.99, 0.82}
    - \definecolor{coralred}{rgb}{1.0, 0.25, 0.25}
    - \definecolor{byzantium}{rgb}{0.44, 0.16, 0.39}
    - \definecolor{thistle}{rgb}{0.85, 0.75, 0.85}
---

\section*{6. \emoji{floppy-disk} Proxmox Backup Server (\textbf{PBS})}
\begin{itemize}
  \item 6.1 Instal·lació de PBS  
  \item 6.2 Creació del Datastore
  \item 6.3 Integració amb Proxmox VE  
  \item 6.4 Programació de còpies de seguretat  
  \item 6.5 Restauració de màquines virtuals  
  \item 6.6 Estratègia de retenció i rotació de backups  
\end{itemize}

\newpage

## \emoji{desktop-computer} 6 Proxmox Backup Server (PBS)

### 6.1 Instalación de PBS

**Passos per a la instal·lació:**

1. Baixem la imatge *ISO* de Proxmox Backup Server des de la [web oficial](https://proxmox.com/en/downloads), triant l’última versió disponible.
2. Una vegada descarregada, la col·loquem en el dispositiu des d'on farem la instal·lació en l’equip.

\emoji{small-orange-diamond} El primer pas, després de col·locar la *ISO*, és la càrrega del menú *GRUB*, on hem de seleccionar el procés d’instal·lació desitjat. En este cas, triarem l'opció amb interfície gràfica.


\emoji{small-orange-diamond} A continuació, acceptem la **llicència d’ús** del programari.

\emoji{small-orange-diamond} En el següent pas, seleccionem en quin disc volem instal·lar Proxmox. En este exemple només tenim un disc disponible, així que el seleccionem. També podem configurar el sistema de fitxers. Triem **ext4**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-16.png}
\end{center}

\emoji{small-orange-diamond} Introduïm la **contrasenya d’administració** i un **correu electrònic** per a notificacions del sistema.

\emoji{small-orange-diamond} Assignem el **nom del *host***, la **IP**, el **gateway** i els **DNS**.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-18.png}
\end{center}

\emoji{small-orange-diamond} Finalment, es mostra un **resum de la configuració** triada. Confirmem i iniciem la instal·lació.

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-19.png}
\end{center}

\emoji{small-orange-diamond} Un cop finalitzada la instal·lació, a la consola apareixerà un missatge indicant que podem accedir a la interfície web de Proxmox via:

```
https://10.10.10.123:8006
```

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-20.png}
\end{center}

\emoji{small-orange-diamond} Així accedim a la **interfície web de Proxmox VE**:

\begin{center}
    \includegraphics[width=0.6\textwidth]{../../../img/image-21.png}
\end{center}