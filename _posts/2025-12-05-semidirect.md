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
**Exercise.** Construct all groups of order 12 that are semidirect products.

**Solution.** An exercise in elementary group theory states that every group of
order 12 is a semidirect product of a group of order three and a group of order
four. The groups of order three are isomorphic to $C_3$, and the groups of
order four are isomorphic to $C_4$ or $C_2\times C_2$. We need to know how
$C_3$ acts by automorphisms on $C_4$ and $C_2\times C_2$, and how $C_4$ and
$C_2\times C_2$ act by automorphism on $C_3$. 

##### Case 1.

We first start with the group $(C_2\times C_2)\rtimes C_3$. We need the actions
by automorphism of $C_3$ on $C_2\times C_2$, that is the group homomorphisms
$C_3\to \operatorname{Aut}(C_2\times C_2)$. 

```
C2xC2<a,b> := AbelianGroup([2,2]);
C3<g> := CyclicGroup(3);
A := \operatorname{Aut}omorphismGroup(C2xC2);
```
We cannot iterate over an automorphism group. Thus
we construct a permutation representation `P` 
of `A`. 
```
p, P := PermutationRepresentation(A);
```
Now we construct a list with all the six maps 
$C_3\to \operatorname{Aut}(C_2\times C_2)$; not all are 
group homomorphisms. 
```
maps := [ hom<C3->A | <g,Inverse(p)(P!x)>> : x in P ];
```
Here, `Inverse(p)(P!x)` is the automorphism of $C_2\times C_2$ 
corresponding to the permutation `x` by the bijection `p`. We 
crucial fact here is that we cannot iterate over `A` but
we can do it over `P`. 

Now to get all semidirect products of the form $(C_2\times C_2)\rtimes C_3$ we
need to run over all _homomorphisms_ in the list `maps`. However, we can't use
the function `IsHomomorphism` for our maps. Thus we need our function to test
whether a map is a homomorphism: 
```
is_homomorphism := function(f)
  local dom, x, y;
  dom := Domain(f);
  for x in dom do
    for y in dom do
      if not (f(x*y) eq f(x)*f(y)) then
        return false;
      end if;
    end for;
  end for;
  return true;
end function;
```
This function is rather naive, but is more than enough for our purposes. So let
us use it. The code 
```
for f in maps do
  if is_homomorphism(f) then
    G := SemidirectProduct(C2xC2, C3, f);
    print GroupName(G);
  end if;
end for;
```
produces two groups, namely $C_2\times C_6$ and $\mathbb{A}_4$. Here
is the output: 
```
C2*C6
A4
A4
```

##### Case 2

What about semidirect products of the form $C_4\rtimes C_3$? In this case, we
will only get the cyclic group of order twelve. 
```
C3<g> := AbelianGroup([3]);
C4 := AbelianGroup([4]);
A := \operatorname{Aut}omorphismGroup(C4);
p, P := PermutationRepresentation(A);
maps := [ hom< C3->A | <g,Inverse(p)(P!x)> > : x in P ];
```
Now we need to use the function `is_homomorphism` we constructed before 
and we are done. The code 
```
{ GroupName(SemidirectProduct(C4,C3,f)) : f in maps | is_homomorphism(f) };
```
produces `{ C12 }`. 

##### Case 3

We now construct the groups of the form $C_3\rtimes C_4$. We now
that $\operatorname{Aut}(C_3)\simeq C_2$. So there is only one non-trivial 
automorphism of $C_3$, namely
$C_3\to C_3$, $x\mapsto -x$ (if the additive notation is used). 
```
C4<g> := AbelianGroup([4]);
C3 := AbelianGroup([3]);
A<a> := \operatorname{Aut}omorphismGroup(C3);
```
Note that our `a` is the automorphism $x\mapsto -x$ of $C_3$. 
In fact, the command 
```
a eq hom<C3->C3|x:->-x>;
```
returns `true`. Now we construct the 
group homomorphism $C_4\to \operatorname{Aut}(C_3)$ sending
the generator `g` of $C_4$ to the automorphism `a`: 
```
f := hom<C4->A|<g,a>>;
```
We can check that this `f` is a homomorphism, but we leave this
as an exercise. Now we construct the semidirect product and check
the structure of the group constructed: 
```
G := SemidirectProduct(C3,C4,f);
GroupName(G);
```
The code returns `C_3:C_4`, which means _a_ semidirect product 
of the form $C_3\rtimes C_4$. 

##### Case 4

There is one case left, namely the semidirect products of the form $C_3\rtimes
(C_2\times C_2)$. Assume that $C_2\times C_2=\langle a,b\rangle$. Let us first
construct the groups: 
```
C2xC2<a,b> := AbelianGroup([2,2]);
C3 := AbelianGroup([3]);
A := \operatorname{Aut}omorphismGroup(C3);
```
Thus we know that $\operatorname{Aut}(C_3)=\\{\operatorname{id},\alpha\\}$. There are four
possible homomorphisms $C_2\times C_2\to \operatorname{Aut}(C_3)$, as the generator $a$ and $b$ can be
mapped independently to either the identity or $\alpha$, Again, we use a permutation
representation to be able to iterate over an automorphism group: 
```
p, P := PermutationRepresentation(A);
maps := [ hom< C2xC2->A | <a,Inverse(p)(P!x)>, <b,Inverse(p)(P!y)>> : x, y in P ];
```
Now we run over `maps` and construct the corresponding semidirect products. The code
```
{ GroupName(SemidirectProduct(C3,C2xC2,f)) : f in maps };
```
produces only two groups (up to isomorphism): 
```
{ D6, C2*C6 } 
```
Therefore, in this case, we obtain the dihedral group of order twelve, 
and the direct product $C_2\times C_6$. 

