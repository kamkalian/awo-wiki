---
title: Virtuelle Maschine
description: Virtuelle Maschine mit SSH Key buchen.
published: 1
date: 2024-01-08T16:28:15.115Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:10:56.845Z
---

# Virtuelle Maschine
Eine Wordpress Installation braucht einen Server. Dies kann ein Maschine zu Hause oder in einem Rechenzentrum sein. Bei einigen Anbietern kann man sich Server mit gewünschter Hardware anmieten. Die meisten Anbieter bieten auch virtuelle Maschienen an, die zusammen mit anderen virtuellen Maschinen auf der selben Hardware laufen und meist für wenige Euros im Monat zu bekommen sind.

# Server von hetzner.com
Für die Webseite der AWO Oberlar haben wir für ca. 3€ im Monat den kleinesten virtuellen Server gebucht. Dieser ist für den Anfang zum betreiben einer Wordpress Seite ausreichend.
Auf dem Server ist ein Ubuntu 18.04 ohne Grafische Oberfläche vorinstalliert.
Wenn man schon einen SSH Key besitzt, kann man diesen beim Buchen hinterlegen. Nach dem Start des Servers kann man sich per SSH verbinden.


# SSH Key erstellen
- Gebe in der Konsole zum erstellen eines SSH Keys folgenden Befehl ein:
	```bash
	ssh-keygen
	```
- Du wirst nun nach einem **Speicherort** und einer **Passphrase** gefragt.
	- Der **Speicherort** ist standardmäßig das Verzeichnis `.ssh` in deinem Homeverzeichnis.

	- Die **Passphrase** kannst du leer lassen, oder du gibst hier ein sicheres Passwort ein, um deinen erstellten SSH Key zu schützen.

- Wechsle in das Verzeichnis `.ssh` in deinem Homeverzeichnis und schau dir mit `ls` eine Liste mit enthaltenen Dateien an:
	```bash
	cd ~/.ssh
	ls
	id_rsa
	id_rsa.pub
	```
- Die Datei `id_rsa` ist der private Schlüssel und sollte gut geschützt nur auf dem eigenen Computer liegen. 
Die Berechtigung kann man sich wie folgt anschauen:
	```bash
	ls -ag
	-rw-------  1 akurm 1843 Jun 30  2019 id_rsa
	-rw-r--r--  1 akurm  409 Jun 30  2019 id_rsa.pub
	```
  - Die Berechtigungen stehen am Anfang.  
      * Das erste Zeichen zeigt uns ein "d" wenn es sich um ein Verzeichnis handelt.
      * Danach folgen drei "rwx" Blöcke.
      * Der erste Block steht für den Eigentümer, danach folgt die Gruppe und anschließend alle Anderen.
      * Ein "r" steht für Lesen, ein "w" für Schreiben und ein "x" für Ausführen.
      * **Der private SSH Key sollte nur ein "rw" im ersten Block enthalten.**
      Sollte die Berechtigung anders aussehen kann man sie mit folgendem Befehl setzen: 
      ```bash
      chmod 600 id_rsa
      ```
- Die Datei `id_rsa.pub` ist der öffentliche Schlüssel. Dieser wird später im Server hinterlegt.

# Server buchen
Beim Buchen des Servers kann man bei Hetzner direkt einen SSH Key hinterlegen. Dies ist praktisch und macht weniger arbeit. 
Alternativ könnt ihr auch später den SSH Key manuell einrichten. In diesem Fall wird euch eine Email mit dem Root Passwort zugeschickt.


![hetzen_server_buchen.png](/hetzen_server_buchen.png =600x)


## SSH Key beim Buchen hinzufügen
- Klickt einfach auf "SSH-Key HINZUFÜGEN" und fügt dann in das Fenster den öffentlichen Schlüssel ein.

	![ssh_key_hinzufuegen.png](/ssh_key_hinzufuegen.png =300x)


 > Öffnet am besten euren öffentlichen Schlüssel mit einem Texteditor und kopiert dann den kompletten Inhalt. 
 {.is-info}


# Verbinden über SSH mit Passwort
Nachdem der Server hochgefahren ist, können wir uns über eine Konsole mit dem Server verbinden.
- Öffne eine Konsole und gebe folgenden Befehl ein:
	```bash
	ssh root@SERVER_IP
	```
  - **ssh** ist der Befehl, der einesichere Verbindung (Secure Shell) zum Server aufbaut
  - **root** ist der Benutzer, mit dem wir uns einloggen.
  - **SERVER_IP** ist die IP Adresse des Servers.
- Du wirst jetzt nach dem root Passwort gefragt, welches du von Hetzner per Email zugeschickt bekommen hast. Gebe es ein, anschließend wird die Verbindung aufgebaut und du siehst die Konsole des Servers.
  
# SSH Key manuell einrichten
Der SSH-Key kann auch manuell auf dem Server hinterlegt werden.
Dazu muss auf dem Server im .ssh Verzeichnis des Users die Datei `authorized_keys` vorhanden sein.

In der Datei `authorized_keys` werden die öffentlichen Schlüssel hinterlegt.
- Öffne die Datei mit einem Editor und füge den öffentlichen Schlüssel ein:
![authorized_keys.png](/authorized_keys.png)
> Wichtig: Pro Zeile darf nur ein Schlüssel hinterlegt werden.
{.is-info}

# Verbinden über SSH mit Key
Ist ein SSH Key auf dem Server hinterlegt und der Server hochgefahren können wir in der Konsole eine Verbindung aufbauen.
- Öffne eine Konsole und gebe folgenden Befehl ein:
	```bash
		ssh root@SERVER_IP
	```
  (Erklärung des Befehls siehe unter "Verbinden über SSH mit Passwort")
- Habt ihr eine Pasephrase bei euerem Key hinterlegt, so werdet ihr danach gefragt und müsst diese jetzt eingeben.
- Anschließend landet ihr in der Konsole des Servers.


# Probleme beim Verbinden mit SSH
Es kann vorkommen das der Login nicht sofort funktioniert, dies kann dann mehrere Ursachen haben:

## Key wurde nicht erkannt
Dies kann passieren wenn man in seinem .ssh Verzeichnis mehrere Key drinnen hat. 
- In diesem Fall muss man dem Befehl die Option -i verwenden und so den Pfad und Namen des Keys mitgeben, also z.B. so:
	```bash
	ssh root@SERVER_IP -i /home/akurm/.ssh/KEY_NAME
	```

## User stimmt nicht
Der User wird mit dem ssh Befehl angegeben und steht vor dem '@'-Zeichen. Hier z.B. 'root':
```bash
ssh root@SERVER_IP
```
Wenn man den User nicht angibt wird automatisch der eigene User verwendet.
Wichtig ist, dass der angegebene User auch auf dem Server vorhanden sein muss.