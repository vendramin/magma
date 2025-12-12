---
title: 'Direct products'
date: 2025-12-05
author: VUB
categories:
  - questions
tags:
  - group
  - direct product
---
To compute the direct product of two or more groups, Magma provides the
function `DirectProduct`. This function returns a group that is isomorphic to
the direct product of the given groups, along with two lists of homomorphisms.
The first list contains the embeddings of the original groups into the direct
product, and the second list contains the projections from the direct product
onto the original groups.
```
C2 := CyclicGroup(2);;
C4 := CyclicGroup(4);;
G, a, b := DirectProduct(C2,C4);
```
The group `G` is `C2*C4`, and 
the variable `a` is the following list: 
```
[
    Mapping from: GrpPerm: C2 to GrpPerm: G,
    Mapping from: GrpPerm: C4 to GrpPerm: G
]
> b;
[
    Mapping from: GrpPerm: G to GrpPerm: C2,
    Mapping from: GrpPerm: G to GrpPerm: C4
]
```
We can also send a list of groups
to the function `DirectProduct`. Here is an example: 
```
G := DirectProduct([C2,C4,C2,C2]);
```

