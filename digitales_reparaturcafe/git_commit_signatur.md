---
title: Git Comics mit Signaturen
description: 
published: true
date: 2021-05-25T19:22:34.491Z
tags: 
editor: markdown
dateCreated: 2021-05-25T18:33:43.560Z
---

# Git Commits mit Signaturen
Git Commits lassen sich signieren. Dadurch lässt sich schneller ekennen, wenn schadhafter Code von dritten implementiert wurde.
Daher sollten immer alle Commits signiert werden. 
Innerhalb eines Git Repos, kann dies durch folgende Einstellung erzwungen werden:
```bash
git config commit.gpgsign true
```
Vorraussetzung ist, dass es einen GPG Schlüssel gibt. Diesen kann man sich selber generieren -> [GPG generieren](/digitales_reparaturcafe/gpg_generieren)
