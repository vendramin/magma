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
> #aut_C2xC2;
6
> f := aut_C2xC2.3;
> g := aut_C2xC2.4;
> Order(f);
2
> Order(g);
2
> Order(f*g);
3
```
In fact, here we see that the automorphism group
of $C_2\times C_2$ is the symmetric group $\mathbb{S}_3$. to construct 
semidirect pdocuts One of 
the homomorphisms $C_3\to Aut(C_2\times C_2)$ is the one
sending the generator of $C_3$ to an automorphism of order three, for example
the product `f*g` we found before. 
```
> sigma := hom< C3->aut_C2xC2 | <C3.1, f*g> >;
> G := SemidirectProduct(C2xC2, C3, sigma);
> GroupName(G);
A4
```
There are other homomorphisms to check, but will give
either the cyclic group of order twelve or
a group isomorphic to $\mathbb{A}_4$. Check it!

What about semidirect products of the form $C_4\rtimes C_3$? In this case
we will only get the cyclic group of order twelve: 
```
> C4 := CyclicGroup(4);
> C3 := CyclicGroup(3);
> aut_C4 := AutomorphismGroup(C4);
> #aut_C4;
2
> id := aut_C4.1;
> IsIdentity(id);
true
> rho := aut_C4.2;
> IsIdentity(rho);
false
> trivial := hom< C3->aut_C4 | <C3.1, id>>;
> G1 := SemidirectProduct(C4, C3, trivial);
> GroupName(G1);
C12
> sigma := hom< C3->aut_C4 | <C3.1, rho> >;
> G2 := SemidirectProduct(C4, C3, sigma);
> GroupName(G2);
C12
```

