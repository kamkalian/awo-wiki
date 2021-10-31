---
title: Sicherheit
description: Bestimmte Logins sperren und Firewall installieren
published: true
date: 2021-10-31T13:49:38.027Z
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