---
title: Webserver
description: Apache und Pakete wie z.B. PHP installieren und einrichten.
published: true
date: 2021-10-31T15:49:17.782Z
tags: 
editor: markdown
dateCreated: 2021-10-31T15:45:39.523Z
---

# Webserver installieren

Als Webserver eignen sich Apache und Nginx.
Hier wird die Installation von Apache beschrieben.

## Apache installieren
In der Konsole geben wir folgendes ein um den Apache Webserver zu installieren:
```bash
sudo apt-get install apache2
```
Nach der Installation wird Apache automatisch im Hintergrund gestartet.
Ruft man jetzt die IP des Servers auf so erhält man bereits eine Testseite.

## PHP7 installieren
Wordpress benötigt PHP, daher installieren wir mit folgendem Befehl alle nötigen Pakete:
```bash
sudo apt-get install php7.2
```

Zusätzlich müssen noch weitere Pakete installiert werden:
```bash
sudo apt-get install
```

## Zusätzliche Pakete installieren
Zum Betrieb von Joomla! sind noch weitere Pakete notwendig.
Diese installieren wir mit folgendem Befehl:
```bash
sudo apt-get install php-mysql php-xml
````