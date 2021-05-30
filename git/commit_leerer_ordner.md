---
title: Commit eines leeren Ordners
description: 
published: true
date: 2021-05-30T18:22:58.757Z
tags: 
editor: markdown
dateCreated: 2021-05-30T18:20:10.313Z
---

In Git ist es nicht möglich ein leeres Verzeichnis (z.B. images), durch einen Commit ins Repo einzubinden.
Es gibt aber einen Workaround, bei dem einfach eine leere Datei in das Verzeichnis gelegt wird:
- Erstelle in dem Verzeichnis eine leere Datei, z.B. `.gitkeep`
- Setze das Verzeichnis auf die `.gitignore` Liste
	```
	images/*
  ```
- Setze für die leere `.gitkeep` Datei zusätzlich folgenden Eintrag in `.gitignore`:
  ```
  !images/.gitkeep
  ```
  Mit dem vorangestellten Ausrufezeichen wird explizit angegeben, dass die Datei erhalten bleiben soll.