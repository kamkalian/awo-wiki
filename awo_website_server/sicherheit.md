---
title: Sicherheit
description: Bestimmte Logins sperren und Firewall installieren
published: true
date: 2021-10-31T13:55:53.559Z
tags: 
editor: markdown
dateCreated: 2021-10-31T13:49:38.027Z
---

# Login via Passwort sperren

Sobald der SSH Zugang per Key eingerichtet ist, können wir den Login per Passwort sperren. 
Vorher sollten wir sicher sein das wir uns mit dem eingerichteten Key per SSH verbinden können.

Um den Login per Passwort zu sperren müssen wir die Optionen **''PasswordAuthentication''**
in der Datei **''/etc/ssh/sshd_config''** auf **"no"** setzen.

Anschließend wird der SSH Server neu gestartet, damit die Änderungen wirksam werden:
```bash
sudo service ssh restart
```

# Root login sperren

Sobald ein User angelegt wurde, können wir den Login für root sperren. 

Dazu setzen wir die Option **''PermitRootLogin''**
in der Datei **''/etc/ssh/sshd_config''** auf **"no"** setzen.

Anschließend wird der SSH Server neu gestartet, damit die Änderungen wirksam werden:
```bash
sudo service ssh restart
```

# Firewall installieren und einrichten

Mit einer Firewall richten wir auf dem Server eine Sperre ein und erlauben den Zugriff nur für bestimmte Dienste.\\
Als Firewall verwenden wir das Tool UFW (UncomplicatedFirewall). 


## Firewall UFW installieren
Folgender Befehl installiert das Paket ufw:
```bash
sudo apt-get install ufw
```

## Zugriff auf Dienste erlauben
Würden wir jetzt die Firewall aktivieren, so würden standardmäßig alle Anfragen zum Server blockiert und wir könnten uns nicht mehr mit dem Server verbinden. Daher sollten wir vorher ein paar Dienste erlauben.
### SSH und http/https erlauben
Mit dem Befehl ''sudo ufw allow DIENST'' können wir bestimmte Dienste erlauben.
Folgende Dienste sollten auf unserem Server erlaubt werden:
```bash>
sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow 443/tcp
```

## Firewall aktivieren
Damit diese Einstellungen aktiviert werden, geben wir folgendes ein:
```bash
sudo ufw --force enable
```
Nun ist die Firewall aktiv und lässt nur Anfragen über SSH und http bzw. https durch.
## Status der Firewall anzeigen
Mit folgendem Befehl können wir uns jeder Zeit den Status anschauen:
```bash
sudo ufw status
```