---
title: Template für Laufzettel
description: 
published: true
date: 2022-10-18T09:38:51.484Z
tags: 
editor: markdown
dateCreated: 2022-10-18T08:23:48.185Z
---

# Hintergrund
Bisher gibt es einen Druck Button, der eine Seite mit nur wenigen Informationen ausdruckt. Um weitere Informationen auf die Seite zu bringen müssen diese in der Programmierung hinzugefügt werden. Dies ist immer mit etwas Aufwand verbunden und meistens nicht zeitnah bzw. flexibel umsetzbar.
Daher wurde eine Vorlage entwickelt die dann automatisch von der Webapplikation ausgefüllt wird.
Diese Vorlage kann jederzeit mit einem gängigen Office Programm geändert werden.
So können auch Admins ohne programmierkenntnisse den Ausdruck leicht ändern.

# Format der Vorlage
Im original liegt die Vorlage z.B. als Word oder Libre Office Datei vor.
In der Datei befindet sich oben eine Kopfzeile die aus einer fest gelegten Grafik besteht. Im weiteren Verlauf werden Bezeichnungen und Felder in einem beliebigen Layout angeordnet. 

**Wichtig:**
Innerhalb eines Feldes muss ein passendes Schlüsselwort angegeben werden. Eine Auflistung aller Schlüsselwörter ist in der nachfolgenden Tabelle dargestellt.

Für die Webapplikation muss die original Datei als HTML Dokument gespeichert werden.

# Schlüsselwörter
Die Schlüsselwörter entsprechen den Feldnamen im Entity-Model.

|Schlüsselwort |Bedeutung |
|:--- |:--- |
|**cus_first_name** |Vorname des Besitzers |
|**cus_last_name** |Nachname des Besitzers |
|**cus_phone_no** |Telefonnummer des Besitzers |
|**cus_email** |Emailadresse des Besitzers |
|**tsk_creation_date** |Datum an dem der Datensatz erstellt wurde. |
|**last_log_dat** |Datum der letzten Aktion (z.B. neuer Kommentar oder Status Änderung) |
|**tsk_id** |Fortlaufende Nummer die jedem Gerät zugeordnet ist. |
|**dev_name** |Bezeichnung des Gerätes |
|**dev_mnf_name** |Hersteller |
|**dev_model** |Modellbezeichnung des Gerätes |
|**tsk_fault_description** |Fehlerbeschreibung |
|**log_string** |Alle Aktionen wie z.B. Status Änderungen und Kommentare einfach untereinander geschrieben. |
