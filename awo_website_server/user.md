---
title: User
description: Anlegen eines User und Vergabe von Berechtigungen
published: true
date: 2021-01-20T18:00:09.545Z
tags: 
editor: markdown
dateCreated: 2021-01-20T17:33:51.179Z
---

# Neuen User anlegen
Auf dem Server sollten wir nicht mit root arbeiten, sondern einen eigenen User anlegen.
- Gib dazu folgenden Befehl ein, der den User mit USERNAME erstellt:
	```bash
	adduser --gecos "" USERNAME
	```
  - `--gecos` mit dieser Einstellung werden keine Daten zum User abgefragt.
- Den Benutzer kannst du mit `su` wechseln:
  ```bash
  su USERNAME
  ```


> Der neue User hat ein eigenes Homeverzeichnis (meistens unter /home/USERNAME). In diesem Verzeichnis sollte auch ein `.ssh` Verzeichnis angelegt werden, in dem dann auch in der Datei `authorized_keys` die SSH Keys hinterlegt werden. Somit kann man sich dann direkt mit dem neuen User per SSH verbinden und kann später den Login per root sperren. 
{.is-info}



  
# Sudo Privileg für User vergeben