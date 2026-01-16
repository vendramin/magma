---
title: 'Structure constants'
date: 2026-01-16
author: VUB
categories:
  - questions
tags:
  - algebra 
  - structure constants
---
Are algebras given by structure constants better? 

Magma can work with finite-dimensional algebras, but this can be tricky. Let us
start with the _quaternion algebra_ $\langle i,j: i^2=j^2=-1, ij=-ji\rangle$.
We can introduce this algebra by generators and relations:
```
> F<a,b> := FreeAlgebra(Rationals(), 2);
> A<i,j> := quo<F|a^2+1,b^2+1,a*b+b*a>;
> i^2;
-1
> j^2;
-1
> i*j;
-j*i
> Dimension(A);
4
```
But the problem is that we cannot do very much with this presentation: asking
for a basis, the center, or the Jacobson radical produces an error message.

As an alternative, we can construct the algebra using its _structure
constants_.  Recall that if $A$ is an $n$-dimensional algebra with basis
$e_1,\dots,e_n$, its structure constants are the scalars $a_{ijk}$ such that
$e_ie_j=\sum_{k=1}^na_{ijk}e_k$ for all $1\leq i,j\leq n$. Let us 
construct the array of structure constants of the quaternion algebra. For this, let 
$n=4$, $e_1=1$, $e_2=i$, $e_3=j$ and $e_4=k$. Since 
$e_2e_1=e_2$
we get that 
$a_{211}=a_{213}=a_{214}=0$ and 
$a_{212}=1$. Similarly, 
since $e_2^2=-e_1$, 
$a_{221}=-1$ and $a_{222}=a_{223}=a_{224}=0$. In this way 
we get the structure constants:
```
> a := [[[ 0 : k in [1..4]] : j in [1..4]] : i in [1..4]];
> a[1][1][1] := 1;
> a[1][2][2] := 1;
> a[1][3][3] := 1;
> a[1][4][4] := 1;
> a[2][1][2] := 1;
> a[2][2][1] := -1;
> a[2][3][4] := 1;
> a[2][4][3] := -1;
> a[3][1][3] := 1;
> a[3][2][4] := -1;
> a[3][3][1] := -1;
> a[3][4][2] := 1;
> a[4][1][4] := 1;
> a[4][2][3] := 1;
> a[4][3][2] := -1;
> a[4][4][1] := -1;
```

Now we can construct the quaternion algebra as the 
algebra with that particular structure constants: 
```
> A := Algebra< Rationals(), 4 | a >;
> Dimension(A);
4
> Basis(A);
[ (1 0 0 0), (0 1 0 0), (0 0 1 0), (0 0 0 1) ]
> JacobsonRadical(A);
Algebra of dimension 0 with base ring Rational Field
> Center(A);
Algebra of dimension 1 with base ring Rational Field
> IsSimple(A);
true
```
Of course, we could have done this: 
```
> A<i,j> := QuaternionAlgebra<Rationals()|-1, -1>;
> Basis(A);
[ 1, i, j, k ]
> Center(A);
Associative Algebra of dimension 1 with base ring Rational Field
> JacobsonRadical(A);
Associative Algebra of dimension 0 with base ring Rational Field
> IsSimple(A);
true
```



