---
title: 'Copying from worksheets'
date: 2025-12-13
author: VUB
categories:
  - tips
tags:
  - prompt 
---
If you have Magma code where every line begins with `>` 
(the Magma REPL prompt), then pasting it directly 
into a script or another Magma session will cause errors.
To tell Magma to ignore the prompt symbol automatically, use 
the command 
```
> SetIgnorePrompt(true); 
```
After this, Magma will accept lines beginning with `>` 
exactly as if the symbol were not there.
