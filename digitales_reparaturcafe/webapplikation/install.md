---
title: Webapplikation und notwendige Pakete installieren
description: 
published: true
date: 2021-05-27T09:36:13.771Z
tags: 
editor: markdown
dateCreated: 2021-05-27T07:36:34.340Z
---

# Webapplikation und notwendige Pakete installieren
Zum Betrieb der Webbapplikation müssen einige Pakete installiert werden.
In dieser Anleitung werden diese Pakete Schritt für Schritt installiert und eingerichtet. Es wird vorrausgestzt das ein Linux Server, z.B. eine virtuelle Maschine oder ein PC, Notebook, Raspbeery Pi, etc., mit installiertem Linux vorhanden ist.
Die Installation und Einrichtung erfolgt weitestgehend auf der Konsole. Eine Grafische Oberfläche ist auf dem Server nicht erforderlich.

## Node.js installieren
Node.js ist eine JavaScript Laufzeitumgebung, welche wir für zum Bau des UI's, unserer Webapplikation, benötigen.

Im ersten Schritt installieren wir uns NVM über ein Script. NVM ist ein Node Version Manager, der uns später Node.js installiert.
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
Das Script lädt NVM aus dem Github Repo [https://github.com/nvm-sh/nvm] und fügt ein paar Pfade zu deinem Bash-Profil(~/.bash_profile, ~/.zshrc, ~/.profile, oder ~/.bashrc) hinzu.

Starte jetzt deine Shell neu:
```bash
source ~/.bashrc
```

Folgender Befehl zeigt dir an, ob schon Node.js Versionen vorhanden sind:
```bash
nvm ls
```
![terminal_nvm_ls.png](/terminal_nvm_ls.png)

Die letzte Node.js Version installieren:
```bash
nvm install --lts
```
![terminal_nvm_install_nodejs.png](/terminal_nvm_install_nodejs.png)



