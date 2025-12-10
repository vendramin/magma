---
title: 'Iterating over an automorphism group'
date: 2025-11-27
author: VUB algebra research group 
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
> GroupName(A);
S3
```
The naive idea doesn't work. Typing 
```
{ a : a in A };
```
produces an error message: 
```
>> { a : a in A };
         ^
Runtime error in for: Iteration is not possible over this object
```
One cannot directly iterate over automorphism groups. We first need to convert
the automorphism group into a structure suitable for iteration.
`PermutationGroup` and `FPGroup` do not work, and something strange happens
with `PCGroup`. So what we should do? Here is the trick: 
```
> p, P := PermutationRepresentation(A);
> p;
Mapping from: GrpAuto: A to GrpPerm: P
> P;
Permutation group P acting on a set of cardinality 3
Order = 6 = 2 * 3
    (1, 2)
    (1, 3)
```
We can iterate over `P` and use the inverse of the 
map `p` to identity our elements inside `A`: 
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

