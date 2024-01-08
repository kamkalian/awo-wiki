---
title: Subdomain Weiterleitung
description: Wie kann man mehrere Subdomains, auf einem Server, auf unterschiedliche Seiten/Dienste weiterleiten?
published: 1
date: 2024-01-08T16:19:07.524Z
tags: apache, subdomain, webserver, weiterleitung
editor: markdown
dateCreated: 2023-12-19T16:11:17.859Z
---

# Subdomain Weiterleitung
Auf einem Server können mehrer Dienste laufen, die jeweils eine Webseite oder Weboberfläche auf Port 80 bzw. Port 443 anbieten.

Über mehrere Subdomains, die z.B. bei Strato erstellt werden, lässt sich eine Weiterleitung auf die IP Adresse des Servers einrichten.
Der Server weiß aber jetzt noch nicht an welchen Dienst er die weitergeleiteten Anfragen senden soll.

Wir können nun unseren Apache Webserver so einrichten, dass er die Anfragen von außen an den richtigen Dienst weiterleitet. 
Apache unterscheidet dann die Anfragen anhand des Servernamens(Subdomain).

Zum einrichten der Weiterleitung benutzen wir für jede Subdomain eine config Datei, die im Verzeichnis `/etc/apache2/sites-enabled` liegen.

```bash
ls /etc/apache2/sites-enabled
default-ssl.conf
nextcloud.conf
```

Für unsere Subdomain cloud.awo-oberlar.de haben wir folgende Konfiguration in der Datei `nextcloud.conf` eingerichtet:

```
<VirtualHost *:80>
        ServerName http://cloud.awo-oberlar.de
        Redirect permanent / https://cloud.awo-oberlar.de/
</VirtualHost>


<VirtualHost *:443>
        ServerName https://cloud.awo-oberlar.de
        DocumentRoot /var/www/html/nextcloud/

        ErrorLog ${APACHE_LOG_DIR}/cloud_error.log
        CustomLog ${APACHE_LOG_DIR}/cloud_access.log combined

        SSLEngine on
        SSLCertificateFile /etc/letsencrypt/live/cloud.awo-oberlar.de/fullchain.pem
        SSLCertificateKeyFile /etc/letsencrypt/live/cloud.awo-oberlar.de/privkey.pem
</VirtualHost>
```
- `<VirtualHost *:80>`
Erstellt einen virtuellen Host der alles auf Port 80 verarbeitet.
- `ServerName` 
Mit ServerName wird die Subdomain angegeben, damit der virtuelle Host nur auf Anfragen von dieser Subdomain schaut.
- `DocumentRoot` 
Dies ist das Verzeichnis wo der Dienst liegt, bzw. hin installiert wurde.
- `ErrorLog` und `CustomLog`
Damit werden die Verzeichnisse und Dateinamen zu den Logs angegeben.
- `SSLEngine on`
Aktiviert Verschlüsselung, Domain bekommt https.
- `SSLCertificateFile` und `SSLCertificateKeyFile`
Gibt die Verzeichnisse und Dateinamen zu dem über letsencrypt durch certbot erstellten Zertifikat bzw. Schlüssel an. 

Wir haben zwei virtuelle Hosts eingerichtet, einer verarbeitet Anfragen von Port 80 und einer von Port 443. 

Die Anfragen von Port 80 die über die mit `ServerName` angegebene Subdomain rein kommen, werden mit `Redirect` direkt an die https (Port 443) Seite weitergeleitet. 

Der zweite virtuelle Host nimmt die Anfragen von Port 443 und leitet sie an unsere Nextcloud im angegeben Verzeichnis weiter.
Zusätlich wird mit `SSLEnginge on` die Verschlüsselung eingeschaltet.

Der Besucher einer Seite wird so immer auf der verschlüsselten https Seite landen. Und mit `ServerName` können wir eine Weiterleitung für bestimmte Subdomains einrichten. In mehreren config Dateien lässt sich so für weitere Subdomains eine Weiterleitung einrichten. 


