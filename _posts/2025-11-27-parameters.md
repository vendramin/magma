---
title: 'Can we use matrices with parameters?'
date: 2025-11-27
categories:
  - questions
tags:
  - matrices
---
I believe the matrix has to be defined over a polynomial ring. For example:
```
> R<x> := PolynomialRing(Integers());
```
followed by, say
```
> M := Matrix(R,2,2,[[x,2],[3,x-1]]);
```
gives the matrix
```
x 2
3 x−1.
```
You can compute with this thing too. For example,
```
> Determinant(M);
```
gives
```
x^2−x−6.
```
If you then wanted to change the base ring to, say $Q[x]$, then define
```
> S<x>:=PolynomialRing(Rationals());
```
and writing
```
> N:=ChangeRing(M,S);
```
does the trick.
