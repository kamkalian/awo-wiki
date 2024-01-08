---
title: Installierte Pakete anzeigen
description: So kannst du nachschauen ob ein Paket schon installiert ist.
published: 1
date: 2024-01-08T16:32:20.343Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:10:45.559Z
---

Manchmal möchte man noch einmal nachschauen welche Pakete installiert sind.
Dazu können wir folgenden Befehl eingeben:
```bash
apt list --installed
```
Dies zeigt uns ein Liste mit allen installierten Paketen:
![apt_paketliste.png](/apt_paketliste.png)
Wenn wir z.B. sehen möchten ob Apache installiert ist, dann können wir das mit folgendem Befehl tun:
```bash
apt list --installed | grep apache
```
![apt_liste_apache.png](/apt_liste_apache.png)
