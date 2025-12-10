---
title: 'Given a polynomial $f$, does `f(1)` work instead of Evaluate(f, 1)?
date: 2025-11-27
author: Andrew Darlington
categories:
  - questions
tags:
  - polynomials
---
Given a polynomial `f`, does `f(1)` work instead of `Evaluate(f, 1)?`
No. Example:
```
> Q<x> := PolynomialAlgebra(Rationals());
> f := x^2+x+1;
> f(1);

>> f(1);
    ^
Runtime error in '@': Bad argument types
Argument types given: RngIntElt, RngUPolElt[FldRat]
``` 

