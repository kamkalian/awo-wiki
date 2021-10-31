---
title: Joomla!
description: Joomla! installieren und einrichten
published: true
date: 2021-10-31T20:13:36.757Z
tags: 
editor: markdown
dateCreated: 2021-10-31T20:13:36.757Z
---

# Joomla! installieren

## Download
Zu erst laden wir uns die aktuellste Joomla! Version, als .bz2 Archive, direkt von der joomla.org Downloadseite herunter:
https://downloads.joomla.org/de/cms|https://downloads.joomla.org/de/cms

## Archive auf den Server kopieren
Das Archive wird nun mit folgendem Befehl auf den Server kopiert:
```bash
scp -r JOOMLA_ARCHIVE USERNAME@SERVER_IP:/var/www/html/joomla
```
  * JOOMLA_ARCHIVE: das ist der Pfad und Dateiname zu dem runtergeladenen Joomla! .bz2 Archive.
  * USERNAME: tragt hier den Username ein, den wir zuvor festgelegt haben.
  * SERVER_IP: ist die IP Adresse des Servers.

## Archive entpacken
Das .bz2 Archive wird nun mit folgendem Befehl entpackt:
```bash
tar xfvj JOOMLA_ARCHIVE
```
  * x: steht für entpacken.
  * f: gibt an das eine Datei entpackt wird.
  * v: Verbose Modus
  * j: gibt an das das Archive ein .bz2 ist.
  * JOOMLA_ARCHIVE: Der Pfad und Dateiname zum runtergeladenen Joomla! Archive.