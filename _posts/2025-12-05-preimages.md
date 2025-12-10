---
title: 'Join and meet'
date: 2025-11-27
author: VUB
categories:
  - questions
tags:
  - homomorphism
  - group
  - quotient
  - normal subgroup
---
Let $G=SL_2(5)$ and $p\colon G\to G/Z(G)$ be the canonical 
map. Typically, Magma will represent $G/Z(G)$
as a permutation group:
```
G := SL(2,5);
Z := Center(G);
Q, p := quo< G|Z >;
```
The group `Q` is a permutation group isomorphic to `A5`.
```
> Q;
Permutation group Q acting on a set of cardinality 6
Order = 60 = 2^2 * 3 * 5
    (1, 2)(3, 4)
    (1, 3, 2)(4, 5, 6)
> GroupName(Q);
A5
```
Let us compute some preimages:
```
> y := Random(Q);
> y;
(1, 3, 5, 4, 2)
> x := y @@ p;
x;
[1 0]
[4 1]
```
How do I get _all_ the preimages of an element $y$? It seems I need the (right)
coset $(\ker p)x$, where $x$ is such that $p(x)=y$. For this, I need to convert
my matrix group into a permutation group: 
```
> f, P := PermutationRepresentation(G);
f;
Homomorphism of SL(2, GF(5)) into GrpPerm: P, Degree 30, Order 2^3 * 3 * 5
induced by
    [2 0]
    [0 3] |--> (2, 4)(5, 6)(7, 8, 9, 10)(11, 19, 13, 21)(12, 20, 14, 22)(15, 18,
        17, 16)(23, 27, 25, 29)(24, 28, 26, 30)
    [4 1]
    [4 0] |--> (1, 2, 3)(4, 5, 6)(7, 11, 15)(8, 12, 16)(9, 13, 17)(10, 14,
        18)(19, 23, 27)(20, 24, 28)(21, 25, 29)(22, 26, 30)
```
The map `f` we get is a bijective group homomorphism $SL_2(5)\to P$, where $P$ is
a permutation group. The preimage of our $y$ has size two, and it is 
the right coset $\{ kx:k\in\ker p\}$. Let us compute this: 
```
> N := f(K);
> K := Kernel(p);
> { Inverse(f)(n*f(x)) : n in N };
{
    [1 0]
    [4 1],

    [4 0]
    [1 4]
}
```
