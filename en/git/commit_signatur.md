---
title: Git Commits mit Signaturen
description: 
published: 1
date: 2024-01-08T16:22:02.044Z
tags: 
editor: markdown
dateCreated: 2023-12-19T16:11:12.261Z
---

# Git Commits immer mit Signatur
Es macht sinn, alle Commits automatisch signieren zu lassen. Denn dadurch lässt sich schneller ekennen, wenn schadhafter Code von dritten implementiert wurde.

Mit folgendem Befehl kann man angeben, welcher GPG Schlüssel  standardmäßigen verwendet werden soll:
```bash
git config user.signingkey 806563016317C3949AFC8E5
```
Innerhalb eines Git Repos, kann dies durch folgende Einstellung erzwungen werden:
```bash
git config commit.gpgsign true
```

