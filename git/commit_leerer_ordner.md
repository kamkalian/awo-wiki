---
title: Commit eines leeren Ordners
description: 
published: true
date: 2021-05-30T18:20:10.313Z
tags: 
editor: markdown
dateCreated: 2021-05-30T18:20:10.313Z
---

# Workaround
In Git ist es nicht möglich ein leeres Verzeichnis (z.B. images), durch einen Commit ins Repo einzubinden.
Es gibt aber einen Workaround, der es möglich macht:
- Erstelle in dem Verzeichnis eine leere Datei, z.B. .gitkeep
- Setze das Verzeichnis auf die .gitignore Liste
	```
	images/*
  ```
- Setze für die leere .gitkeep Datei folgenden Eintrag:
  ```
  !images/.gitkeep
  ```
  Mit dem vorangestellten Ausrufezeichen wird explizit angegben, dasd die Datei erhalten bleiben soll.