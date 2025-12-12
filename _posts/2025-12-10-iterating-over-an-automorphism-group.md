---
title: 'Iterating over an automorphism group'
date: 2025-12-10
author: VUB
categories:
  - questions
tags:
  - group
  - automorphism group
  - iteration
---
How can we iterate over the elements of an automorphism group? 

Let us assume we need to iterate over the six automorphisms
of the Klein group. 
```
> G := AbelianGroup([2,2]);
> A := AutomorphismGroup(G);
```
The naive idea doesn't work. Typing 
```
> { a : a in A };
```
produces an error message, saying: _Iteration is not possible over this object_. 
Thus one cannot directly iterate over automorphism groups. We first need to convert
the automorphism group into a structure suitable for iteration.
`PermutationGroup` and `FPGroup` do not work, and something strange happens
with `PCGroup`. So what we should do? Here is the trick: 
```
> p, P := PermutationRepresentation(A);
```
Here, `p` is a (bijective) map from `A` onto the permutation group `P`. 
We can iterate over `P`, and we need to use the inverse of the 
map `p` to identity our elements inside `A`. 
```
> { x @@ p : x in P };
{
    Automorphism of Abelian Group isomorphic to Z/2 + Z/2
    Defined on 2 generators
    Relations:
        2*G.1 = 0
        2*G.2 = 0 of order 1 which maps:
        G.1 |--> G.1
        G.2 |--> G.2,
    Automorphism of Abelian Group isomorphic to Z/2 + Z/2
    Defined on 2 generators
    Relations:
        2*G.1 = 0
        2*G.2 = 0 which maps:
        G.1 |--> G.1
        G.2 |--> G.1 + G.2,
    Automorphism of Abelian Group isomorphic to Z/2 + Z/2
    Defined on 2 generators
    Relations:
        2*G.1 = 0
        2*G.2 = 0 which maps:
        G.1 |--> G.2
        G.2 |--> G.1,
    Automorphism of Abelian Group isomorphic to Z/2 + Z/2
    Defined on 2 generators
    Relations:
        2*G.1 = 0
        2*G.2 = 0 which maps:
        G.1 |--> G.1 + G.2
        G.2 |--> G.2,
    Automorphism of Abelian Group isomorphic to Z/2 + Z/2
    Defined on 2 generators
    Relations:
        2*G.1 = 0
        2*G.2 = 0 which maps:
        G.1 |--> G.2
        G.2 |--> G.1 + G.2,
    Automorphism of Abelian Group isomorphic to Z/2 + Z/2
    Defined on 2 generators
    Relations:
        2*G.1 = 0
        2*G.2 = 0 which maps:
        G.1 |--> G.1 + G.2
        G.2 |--> G.1
}
```

