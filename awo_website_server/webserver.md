---
title: Webserver
description: Apache und Pakete wie z.B. PHP installieren und einrichten.
published: 1
date: 2024-01-08T16:27:43.919Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:10:58.818Z
---

# Webserver installieren

Als Webserver eignen sich Apache und Nginx.
Hier wird die Installation von Apache beschrieben.

## Apache installieren
In der Konsole geben wir folgendes ein um den Apache Webserver zu installieren:
```bash
sudo apt-get install apache2
```
Nach der Installation wird Apache automatisch im Hintergrund gestartet.
Ruft man jetzt die IP des Servers auf so erhält man bereits eine Testseite.

## PHP7 installieren
Wordpress benötigt PHP, daher installieren wir mit folgendem Befehl alle nötigen Pakete:
```bash
sudo apt-get install php7.2
```

Zusätzlich müssen noch weitere Pakete installiert werden:
```bash
sudo apt-get install
```

## Zusätzliche Pakete installieren
Zum Betrieb von Wordpress sind noch weitere Pakete notwendig.
Diese installieren wir mit folgendem Befehl:
```bash
sudo apt-get install php-mysql php-xml
````

## Apache für mehrere Webseiten einrichten

Wir wollen zum Testen auf dem Server mehrere Webseiten parallel laufen lassen.
Dabei wird eine Seite mit Joomla! und eine Setie mit Wordpress eingerichtet.

### Verzeichnisse für Webseiten anlegen
Es macht Sinn für beide Webseiten einen Verzeichnis anzulegen.
Da Apache standardmäßig das Verzeichnis /var/www/html verwendet, erstellen wir darunter die Verzeichnisse für die Webseiten:
```bash
cd /var/www/html
mkdir joomla
mkdir wordpress
```
Damit die gerade angelegten Verzeichnisse auch vom Webserver(z.B. Apache) verwendet werden können, ändern wir den Eigentümer der Verzeichnisse:
```bash
chown www-data joomla
chown www-data wordpress
```

### Konfigurationsdateien erstellen
Damit der Webserver weiss das es zwei Webseiten gibt müssen wir für ihn zwei Konfigurationsdateien anlegen. (Man könnte auch alles in eine Konfigurationsdatei packen, aber mit 2 Konfigurationen hat man die Möglichkeit später gezielt die Webseiten einzeln zu steuern.)

Zum Anlegen der Dateien kopieren wir im Verzeichnis ''/etc/apache2/sites-available'' die Datei ''000-default.conf''
```bash
cd /etc/apache2/sites-available
cp 000-default.conf joomla.conf
cp 000-default.conf wordpress.conf
```
Sollte die default conf nicht existieren, so erstellt man sich erstmal eine leere Datei. 

Nun müssen diese beiden Dateien angepasst werden. 
(Wir wollen Joomla auf Port 80 und Wordpress auf Port 8080 laufen lassen.)
Dazu öffnen wir die Dateien mit dem Editor und ändern die Default Konfiguration wie folgt ab:
**Wichtig: Über der Zeile VirtualHost muss noch ein ''Listen 80'' bzw. ''Listen 8080'' eingefügt werden.**
#### joomla.conf
```
Listen 80
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/joomla

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/joomla_error.log
        CustomLog ${APACHE_LOG_DIR}/joomla_access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>
```

#### wordpress.conf
```
Listen 8080
<VirtualHost *:8080>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html/wordpress

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/wordpress_error.log
        CustomLog ${APACHE_LOG_DIR}/wordpress_access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>
```

### Konfigurationen aktivieren/deaktivieren
Damit unsere angelegten Konfigurationen aktiv werden müssen wir die Default Konfiguration deaktivieren und die joomla.coonf und wordpress.conf aktivieren.

### Default Konfiguration deaktivieren
```bash
a2dissite 000-default.conf
```

### joomla.coonf und wordpress.conf aktivieren
```bash
a2ensite joomla.conf
a2ensite wordpress.conf
```

### Webserver neu starten
Nachdem die Konfigurationen aktiviert wurden, muss der Webserver neu gestartet werden:
```bash
systemctl reload apache2
```
