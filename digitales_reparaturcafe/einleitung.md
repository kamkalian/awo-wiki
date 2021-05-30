---
title: Einleitung
description: 
published: true
date: 2021-05-30T17:05:50.387Z
tags: 
editor: markdown
dateCreated: 2021-05-30T17:00:22.187Z
---


# Was steckt hinter der Webapplikation?
Die Webapplikation ist eine mit React.js und Python geschriebene Anwendung.
Grundlegend teilt sich die Anwendung in UI(User Interface) und API auf. 
Das UI wurde mit React.js und Material-ui gebaut. Es schickt für die verschiedensten Aktionen, in der Anwendung, einen POST Request an die API.
Die API ist in Python mit Hilfe des FLASK Frameworks geschrieben und nimmt den Request an, verarbeitet ihn und schickt entsprechende Daten aus der Datenbank dem UI zurück.



# MySQL/MariaDB Datenbank
Die Webapplikation speichert fast alle Daten in eine MySQL Datenbank. 
Bei MariaDB handelt es sich um einen Fork von MySQL, der seit einigen Jahren parallel weiterentwickelt wird.
## Entity Modell
![entity_modell_reparaturcafe.png](/entity_modell_reparaturcafe.png)
[reparaturcafe.pdf](/reparaturcafe.pdf)

## MySQL Server auf dem Mac starten
```bash
mysql.server start
```