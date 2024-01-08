---
title: Sendmail
description: Sendmail installieren und einrichten
published: 1
date: 2024-01-08T16:29:54.577Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:10:51.197Z
---

# Sendmail installieren

Die Wordpress Seite nutzt die ''mail()'' Funktion von PHP.
Dazu muss auf dem Server das Programm "sendmail" installiert sein.
Ansonsten kann Wordpress keine Emails an die User senden. Somit ist es dann auch nicht möglich sein Passwort über die "Passwort vergessen" Funktion zu erneuern.
In der Konsole auf dem Server installieren wir ''sendmail'' mit folgendem Befehl:
```bash
sudo apt-get install sendmail
```
Führe anschließend zur Konfiguration folgenden Befehl aus (Dabei können alle Fragen mit Ja beantwortet werden.):
```bash
sudo sendmailconfig
```
Zum Schluß sollte der Apache Webserver einmal neu gestartet werden:
```bash
sudo service apache2 restart
```
**Wichtig**: Der Hostname vom Server sollte eine Domain sein, damit eine Email korrekt verschickt wird. Der Hostname kann mit folgendem Befehl geändert werden:
```bash
sudo hostnamectl set-hostname awo-oberlar.de
```