---
title: Problem mit Permalinks in Wordpress
description: Kurze Erklärung, wenn Seiten nicht mehr abgespeichert werden können
published: 1
date: 2024-01-08T16:31:11.410Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:10:49.322Z
---

**Problem**: Seiten können nicht mehr abgespeichert werden.
Es erscheint folgende Fehlermeldung:
![fehlermeldung_wordpress.png](/fehlermeldung_wordpress.png)

Dies kann passieren wenn in den Einstellungen -> Permalinks auf "Beitragsname" umgestellt wurde.
Dann können die Seiten nur mit index.php davor aufgerufen werden:
![permalink_einstellung.png](/permalink_einstellung.png)
Dies sieht aber unschön aus und macht die URL nur unötig lang.

**Lösung**:
In der Datei:
/etc/apache2/apache2.conf
den Parameter "AllowOverride" auf "All" setzen.