---
title: 'Given a polynomial with integer coefficients, how can I consider it as a polynomial with coefficients in other fields? 
date: 2025-11-27
author: Andrew Darlington
categories:
  - questions
tags:
  - fields
  - polynomials
---
For example, let `f` be an integer polynomial. Can we obtain the factorization
of `f` in other fields (e.g. finite fields)?'

Let `f` be an integer polynomial. 
```
> f := x^2-3*x+5;
> g := Q!f;
> Z<x>:=PolynomialRing(Integers());
> f := x^2-3*x+5;
> f;
x^2 - 3*x + 5
> F<x>:=PolynomialRing(FiniteField(3));
> g := F!f;
> g;
x^2 + 2
```
If it makes sense to consider `f` with coefficients in another ring, 
then `g` will be the resulting polynomial. 

For the other question: 
```
> Factorisation(f);
[
    <x^2 - 3*x + 5, 1>
]
> Factorisation(g);
[
    <x + 1, 1>,
    <x + 2, 1>
]
```
This means that the polynomial `f` is irreducible over the integers, and `g`
factors into `(x + 1)(x + 2)` over the field of three elements. 

