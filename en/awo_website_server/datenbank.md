---
title: Datenbank
description: MySQL Datenbank installieren und einen User / eine Datenbank für Wordpress einrichten.
published: 1
date: 2024-01-08T16:33:08.077Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:10:43.676Z
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