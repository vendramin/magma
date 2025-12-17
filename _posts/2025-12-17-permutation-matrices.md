---
title: 'Permutation matrices'
date: 2025-12-17
author: VUB
categories:
  - questions
tags:
  - linear algebra
  - permutation
  - permutation matrix
---
How we deal with permutation matrices? 

In Magma, vectors are row vectors and permutation matrices act on the right.
For a permutation $\sigma$, 
the corresponding permutation matrix constructed 
with `PermutationMatrix` 
permutes the coordinates according to $\sigma$. Here is an example 
corresponding to the permutation $\sigma=(1234)\in\mathbb{S}_5$: 

```
> m := PermutationMatrix(Integers(), [2,3,4,1,5]);
> v := Vector(Integers(), [0,0,0,0,1]);
> v*m;
(0 0 0 0 1)
> w := Vector(Integers(), [1,0,0,0,0]);
> w*m;
(0 1 0 0 0)
```

Here is another example:
```
> s := Sym(3)!(1,2);
> m := PermutationMatrix(Integers(), [ x^s : x in [1,2,3] ]);
> m;
[0 1 0]
[1 0 0]
[0 0 1]
> Vector(Integers(), [0,1,0])*m;
(1 0 0)
> Vector(Integers(), [0,0,1])*m;
(0 0 1)
```

