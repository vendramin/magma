---
title: 'Groups of order 12 as semidirect products'
date: 2025-11-27
author: Leandro Vendramin
categories:
  - exercises
tags:
  - group
  - semidirect product
  - homomorphism
  - automorphism group
  - conjugation
---
The idea is to construct all groups of order 12 that are 
semidirect products.

```
> C2 := CyclicGroup(2);
> C2xC2 := DirectProduct(C2,C2);
> C3 := CyclicGroup(3);
> aut_C2xC2 := AutomorphismGroup(C2xC2);
> f := aut_C2xC2.3;
> g := aut_C2xC2.4;
> Order(f);
2
> Order(g);
2
> Order(f*g);
3
> sigma := hom<C3->aut_C2xC2|<C3.1,f*g>>;
> G := SemidirectProduct(C2xC2, C3, sigma);
> GroupName(G);
A4
```
