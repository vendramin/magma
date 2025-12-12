---
title: 'Evaluating polynomials' 
date: 2025-11-27
author: Silvia Properzi
categories:
  - questions
tags:
  - polynomial
---
Given a polynomial `f`, does `f(1)` work as an alternative to `Evaluate(f, 1)?`
No. For example: 
```
Q<x> := PolynomialAlgebra(Rationals());
f := x^2+x+1;
```
The command `f(1)` results in an error. In addition, note that the expression 
```
f where x is 1; 
```
does not evaluate `f` at `1`, but `y^2+y+1 where y is 1;` does. 
