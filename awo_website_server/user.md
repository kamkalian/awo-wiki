---
title: User
description: Anlegen eines User und Vergabe von Berechtigungen
published: 1
date: 2024-01-08T16:28:41.569Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:10:54.970Z
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

Da wir uns später nur noch mit dem neu angelegten User auf dem Server einloggen, ist es praktisch wenn dieser User bestimmte Befehle mit ''sudo'' ausführen kann.

Dazu geben wir im Terminal auf dem Server folgenden Befehl ein:
```bash
usermod -aG sudo USERNAME
```