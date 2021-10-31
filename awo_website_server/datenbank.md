---
title: Datenbank
description: MySQL Datenbank installieren und einen User / eine Datenbank für Wordpress einrichten.
published: true
date: 2021-10-31T16:07:22.541Z
tags: 
editor: markdown
dateCreated: 2021-10-31T16:07:22.541Z
---

# MySQL installieren
Als Datenbank verwenden wir MySQL. Folgender Befehl installiert alle notwendigen Pakete:
```bash
sudo apt-get install mysql-server
```

## Datenbank und User für Wordpress anlegen =====
Wordpress braucht zum Betrieb zwingend eine Datenbank. \\

Nun erstellen wir eine Datenbank und legen einen User an, für den wir dann noch die Berechtigung auf die Datenbank erteilen müssen.

### Mit Datenbank verbinden
```bash
sudo -u root -p
```

### Datenbank erstellen
```
create database db_wordpress;
```

### User anlegen
```
create user 'USERNAME'@'localhost' identified by 'PASSWORD';
```

### Berechtigung erteilen
```
grant all privileges on db_joomla.* to 'USERNAME'@'localhost';
```