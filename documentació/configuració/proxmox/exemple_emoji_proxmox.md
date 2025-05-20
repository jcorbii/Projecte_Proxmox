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

# \emoji{grinning-face-with-big-eyes} Introducció

Aquest document mostra l'ús de LaTeX i Pandoc amb emojis en un entorn de documentació tècnica.

# Configuració del sistema 

El sistema es basa en Proxmox VE amb diverses màquines virtuals optimitzades.

# Estat del projecte 

Tot està operatiu i validat amb les pràctiques corresponents.