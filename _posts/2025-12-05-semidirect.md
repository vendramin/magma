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
**Exercise.** Construct all all groups of order 12 that are 
semidirect products.

**Solution.** We first start with the group $(C_2\times C_2)\rtimes C_3$.  

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
