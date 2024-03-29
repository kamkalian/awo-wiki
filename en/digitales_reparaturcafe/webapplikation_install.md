---
title: Webapplikation und notwendige Pakete installieren
description: 
published: 1
date: 2024-01-08T16:23:29.308Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:11:08.341Z
---

# Webapplikation und notwendige Pakete installieren
Zum Betrieb der Webbapplikation müssen einige Pakete installiert werden.
In dieser Anleitung werden diese Pakete Schritt für Schritt installiert und eingerichtet. Es wird vorrausgestzt das ein Linux Server, z.B. eine virtuelle Maschine oder ein PC, Notebook, Raspbeery Pi, etc., mit installiertem Linux vorhanden ist.
Die Installation und Einrichtung erfolgt auf der Konsole. Eine Grafische Oberfläche ist auf dem Server nicht erforderlich.


## MySQL/MariaDB installieren
Auf vielen Linux System ist MariaDB bereits installiert.
Gebe folgenden Befehl ein, um zu sehen ob und welche Version von MySQL oder MariaDB installiert ist:
```bash
 mysql --version
```
![terminal_mysql_version.png](/terminal_mysql_version.png)

Sollte noch kein MySQL oder MariaDB installiert sein, so kannst du eines der beiden über die Paketverwaltung installieren:
```bash
 apt install mariadb-server
```


## Datenbank und User anlegen
Egal ob ihr MySQL oder MariaDB verwendet, die Befehle sind bei beiden identisch.
Nach der Installation, von z.B. MariaDB, sollte der Datenbank-Server laufen.
Das Anlegen von Datenbanken und User machen wir über die mysql Konsole.
Dazu rufen wir mysql auf:
```bash
 mysql
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
Der Source Code liegt auf GitHub. Am einfachsten ist es wenn du das Repo direkt in das standard Verzeichnis des Webservers legst. Wechsle also in das Verzeichnis `/var/www` und lade das Repo herunter. 
```bash
cd /var/www/
 git clone https://github.com/kamkalian/reparaturcafe2.git
```
Ein neues Verzeichnis "reparaturcafe2" wurde angelegt und das Repo dort rein geladen:
![terminal_ls_var_www.png](/terminal_ls_var_www.png)
Damit unser standard User und der Webserver auf dieses Verzeichnis zugreifen können, ändern wir den Eigentümer und die Gruppe des Verzeichnisses:
```bash
 chown www-data:www-data /var/www/reparaturcafe2
```


## Node.js installieren
Node.js ist eine JavaScript Laufzeitumgebung, welche wir für zum Bau des UI's, unserer Webapplikation, benötigen.

Im ersten Schritt installieren wir uns NVM über ein Script. NVM ist ein Node Version Manager, der uns Node.js installiert.
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
```
Das Script lädt NVM aus dem Github Repo [https://github.com/nvm-sh/nvm] und fügt ein paar Pfade zu deinem Bash-Profil(~/.bash_profile, ~/.zshrc, ~/.profile, oder ~/.bashrc) hinzu.

logge dich jetzt neu ein:
```bash
logout
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

Nachdem node.js installiert ist lassen wir alle benötigten Pakete, die in der package.json aufgelistet sind, automatisch installieren.
Gebe dazu folgenden Befehl ein:
```bash
npm install
```
Nun lassen wir über npm das UI der Webapplikation zusammen bauen:
```bash
npm run build
```


## Python und benötigte Module in einer Venv installieren
Ein Teil der Webapplikation funktioniert mit Python und dafür werden einige zusätzliche Module benötigt. Diese Module werden üblicherweise in einer eigenen Python Umgebung installiert.
Wechsle in das api Verzeichnis, welches sich im reparaturcafe2 Verzeichnis befindet:
```bash
cd api
```
Erstelle nun die Venv:
```bash
python3 -m venv venv
```
Sollte python3 noch nicht installiert sein, kannst du es mit ` apt-get install python3` installieren.
Aktiviere nun die neue Venv:
```bash
source venv/bin/activate
```
![terminal_activate_venv.png](/terminal_activate_venv.png)
Alle benötigten Module sind in der requirements.txt aufgelistet. Mit dem Tool "pip" werden diese Module installiert. Zum installieren übergeben wir dem `pip install` Befehl die Datei requirements.txt:
```bash
pip install -r requirements.txt
```
Nach kurzer Zeit sind alle benötigten Module installiert.


## Webserver Apache2 installieren
Der Webserver verarbeitet die Anfragen und schickt sie weiter an unser UI oder unsere API.
In diesem Beispiel verwenden wir Apache2 als Webserver.

Installiere Apache2:
```bash
 apt-get install apache2
```

## SSL Zertifikate mit Certbot erstellen
Damit die Webseite über HTTPS verschlüsselt wird, brauchen wir ein Zertifikat.
Dieses Zertifikat erstellen wir uns über den Certbot.
Dazu gibt es unter folgender Adresse eine gute Anleitung:
[https://certbot.eff.org/lets-encrypt/ubuntufocal-apache](https://certbot.eff.org/lets-encrypt/ubuntufocal-apache)

## Apache2 Konfiguration erstellen
Erstelle in dem Verzeichnis `/etc/apache2/sites-available` eine neue Konfiguration (z.B. reparaturcafe-ssl.conf), mit folgendem Inhalt.
```
<VirtualHost _default_:443>
        ServerName [DEINE DOMAIN]
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/reparaturcafe2/build
        
        <Directory /var/www/reparaturcafe2/build/>
                AllowOverride All
        </Directory>
        
        <Location /api>
                ProxyPass http://localhost:5000/api
                Allow from all
        </Location>

        SSLProxyEngine on
        SSLProxyVerify none
        SSLProxyCheckPeerCN off
        SSLProxyCheckPeerName off
        SSLProxyCheckPeerExpire off

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        SSLEngine on
        SSLCertificateFile      [PFAD ZUM ZERTIFIKAT]
        SSLCertificateKeyFile 	[PFAD ZUM KEY]
</VirtualHost>
```
- [DEINE DOMAIN]: Trage hier deine Web Adresse ein. (z.B. reparaturcafe.awo-oberlar.de)
- [PFAD ZUM ZERTIFIKAT], [PFAD ZUM KEY]: Gebe hier die Pfade zum Zertifikat und Key an, welche du mit Certbot erstellt hast. 
(z.B. /etc/letsencrypt/live/reparaturcafe.awo-oberlar.de/fullchain.pem,
/etc/letsencrypt/live/reparaturcafe.awo-oberlar.de/privkey.pem)

## Apache2 Konfiguration aktivieren
Nachdem die Konfiguration erstellt wurde, muss sie noch aktiviert werden:

```bash
sudo a2ensite reparaturcafe-ssl.conf
```
Anschließend starten wir den Apache einmal neu:
```bash
systemctl reload apache2
```
Jetzt sollte bereits unser UI laufen und wir können die Webapplikation aufrufen.

## API einrichten
### Zugangsdaten über .env
### Datenbank Modell laden
### API über Gunicorn und Supervisor laufen lassen
Die in Python geschrieben API benötigt zum Betrieb einen kleinen WSGI Server. Hierzu installieren wir uns in der Venv das Tool `gunicorn`.
```bash
pip install gunicorn
```
Damit wir gunicorn nicht immer manuell starten müssen, verwenden wir Supervisor.
Zur Installation geben wir folgendes ein:
```bash
 apt-get install supervisor
```
Unter `/etc/supervisor/conf.d/` erstellen wir die Datei `reparaturcafe.conf` mit folgendem Inhalt:
```
[program:reparaturcafe2]
command=/var/www/reparaturcafe2/api/venv/bin/gunicorn -b localhost:5000 "api:create_app()"
directory=/var/www/reparaturcafe2
user=www-data
autostart=true
autorestart=true
stopasgroup=true
killasgroup=true
stderr_logfile=/var/log/supervisor/reparaturcafe2.err.log
stdout_logfile=/var/log/supervisor/reparaturcafe2.out.log
```
Anschließend wird Supervisor neu gestartet:
```bash
 supervisorctl reload
```
Mit folgendem Befehl können wir schauen ob alles läuft:
```bash
 supervisorctl status
```
![terminal_supervisor_running.png](/terminal_supervisor_running.png)

Sollte dort nicht RUNNING stehen so kann man in dem Logfile: `/var/log/supervisor/reparaturcafe2.err.log` nachschauen, was das Problem ist.