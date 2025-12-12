---
title: 'Remove variable binding'
date: 2025-12-13
author: VUB
categories:
  - tips
tags:
  - variable 
---
Suppose you define a variable `x`, e.g.
```
> x := 5;
> x;
5
> assigned x;
true
```
What if we now want to _kill_ the variable `x`?
This can be done with the command `delete`: 
```
> delete x;
> assigned x;
false
```
