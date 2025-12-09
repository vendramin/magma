---
title: 'Matrices with parameters'
date: 2025-11-27
categories:
  - questions
tags:
  - matrices
---
##### Can we use parameters when doing computations with matrices? And matrices with parameters?

I believe the matrix has to be defined over a polynomial ring. For example:
```
R<x>:=PolynomialRing(Integers());
```
followed by, say
```
M:=Matrix(R,2,2,[[x,2],[3,x-1]]);
```
gives the matrix
```
x 2
3 x−1.
```
You can compute with this thing too. For example,
```
Determinant(M);
```
gives
```
x^2−x−6.
```
If you then wanted to change the base ring to, say $Q[x]$, then define
```
S<x>:=PolynomialRing(Rationals());
```
and writing
```
N:=ChangeRing(M,S);
```
does the trick.
