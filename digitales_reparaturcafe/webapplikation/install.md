---
title: Webapplikation und notwendige Pakete installieren
description: 
published: true
date: 2021-05-30T06:39:12.190Z
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

## MySQL/MariaDB installieren
Die Webapplikation speichert fast alle Daten in eine MySQL Datenbank. 
Daher müssen wir den Datanbankserver MySQL oder MariaDB installieren. Bei MariaDB handelt es sich um einen Fork von MySQL, der seit einigen Jahren parallel weiterentwickelt wird.
Auf vielen Linux System ist MariaDB bereits installiert.
Gebe folgenden Befehl ein, um zu sehen ob und welche Version von MySQL oder MariaDB installiert ist:
```bash
sudo mysql --version
```
![terminal_mysql_version.png](/terminal_mysql_version.png)

Sollte noch kein MySQL oder MariaDB installiert sein, so kannst du eines der beiden über die Paketverwaltung installieren:
```bash
sudo apt install mariadb-server
```

## Datenbank und User anlegen
Egal ob ihr MySQL oder MariaDB verwendet, die Befehle sind bei beiden identisch.
Nach der Installation, von z.B. MariaDB, sollte der Datenbank-Server laufen.
Das Anlegen von Datenbanken und User machen wir über die mysql Konsole.
Dazu rufen wir mysql auf:
```bash
sudo mysql
```
Wir landen nun in der Konsole und können hier weitere mysql Befehle absetzen.
Als erstes erstellen wir die Datenbank "reparaturcafe2":
```
CREATE DATABASE reparaturcafe2;
```
Anschließend erstellen wir einen User mit Namen "oskar2":
```
CREATE USER 'oskar2'@'localhost' IDENTIFIED BY 'PASSWORD';
```
- Als 'PASSWORD' setzt ihr euer Passwort ein.

Mit diesem User wird später die Webapplikation auf die Datenbank zugreifen.
Als nächstes geben wir dem User ein paar Berechtigungen:
```
GRANT ALL PRIVILEGES ON reparaturcafe2.* TO 'oskar2'@'localhost';
```
Damit sind wir hier erstmal fertig. Die Datenbanktabellen werden später über Flask-Migrate erstellt, dazu gibt es schon vorbereitet Scripts die nur noch ausgeführt werden müssen. 

## Webapplikation runterladen
Der Source Code liegt auf GitHub. Mit folgendem Befehl laden wir das Repo herunter. Dabei wird in dem aktuellen Verzeichnis ein neuer Ordner angelegt.
```bash
git clone https://github.com/kamkalian/reparaturcafe2.git
```

## Python und benötigte Module in einer Venv installieren
Ein Teil der Webapplikation funktioniert mit Python und dafür werden einige zusätzliche Module benötigt. Diese Module werden üblicherweise in einer eigenen Python Umgebung installiert.
Wechsle in das api Verzeichnis, welches sich im reparaturcafe2 Verzeichnis befindet:
```bash
cd reparaturcafe2/api
```
Erstelle nun die Venv:
```bash
python3 -m venv venv
```
Sollte python3 noch nicht installiert sein, kannst du es mit `sudo apt-get install python3` installieren.
