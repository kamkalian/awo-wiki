---
title: Commit eines leeren Ordners
description: 
published: 1
date: 2024-01-08T16:22:44.447Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:11:10.382Z
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