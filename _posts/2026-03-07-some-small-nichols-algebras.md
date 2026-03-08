---
title: 'Some small Nichols algebras'
date: 2026-03-07
author: Leandro Vendramin
categories:
  - questions
tags:
  - algebra 
  - Nichols algebra
  - structure constants
---
In [Heckenberger's course](https://leandrovendramin.org/heckenberger/) _Nichols
algebras and root systems_ there are three exercises where one needs to compute
the dimension of certain small Nichols algebras over certain
two-dimensional (complex) braided vector spaces of diagonal type. 

We need to construct quantum symmetrizers. First, we define the braiding
$c_i$ as an endomorphism of $V^{\otimes n}$. For this purpose, we simply compute
$c_i=\operatorname{id}^{\otimes (i-1)}\otimes
c\otimes\operatorname{id}^{\otimes(n-i-1)}$. 

````
> Braiding := function(c, i, n)
function> d := Isqrt(Nrows(c));
function> R := BaseRing(c);
function> return TensorProduct(TensorProduct(IdentityMatrix(R, d^(i-1)), c),\
 IdentityMatrix(R, d^(n-i-1)));
function> end function;
````
We also need the shuffle map, namely 
$\operatorname{id}+c_1+c_1c_2+\cdots+c_1c_2\cdots c_{n-1}$. 
```
> ProductOfBraidings := function(c, i, n)
function> m := Braiding(c, 1, n);
function> for k in [2..i] do
function|for> m := m*Braiding(c, k, n);
function|for> end for;
function> return m;
function> end function;
```
Now, to compute the quantum symmetrizer, we use the recursive formula 
$S_{n+1}=(S_n\otimes\operatorname{id})(
\operatorname{id}+c_1+c_1c_2+\cdots+c_1c_2\cdots c_n)$. 

```
> Symmetrizer := function(c, n)
function> d := Isqrt(Nrows(c));
function> R := BaseRing(c);
function> if n eq 1 then
function|if> return IdentityMatrix(R, d);
function|if> end if;
function> m := IdentityMatrix(R, d^n);
function> for i in [1..n-1] do
function|for> m := m + ProductOfBraidings(c, i, n);
function|for> end for;
function> return TensorProduct(IdentityMatrix(R, d), $$(c, n-1))*m;
function> end function;
```  
The following function computes the dimensions of homogeneous
components of a Nichols algebra:
```
> ComputeDimension := function(c, n)
function> if n eq 0 then
function|if> return 1;
function|if> else
function|if> return Rank(Symmetrizer(c, n));
function|if> end if;
function> end function;
``` 
Heckenberger's exercises are the following. 
Let $V$ be a complex vector space with basis $x_1,x_2$. The braidings 
are of the form $c(x_i\otimes x_j)=q_{ij} x_j\otimes x_i$ for $i,j\in\{1,2\}$. 
There are three braidings to consider:
1. $q_{11}=q_{22}=-1$ and $q_{12}q_{21}=1$.
1. $q_{11}=q_{22}=-1$ and $q_{12}q_{21}=-1$.
1. $q_{11}=q_{22}=-1$ and $q_{12}q_{21}=\omega$, where $\omega^2+\omega+1=0$. 

So we create a braiding for each $2\times 2$ matrix $q$.

````
> DimensionTwoDiagonalBraiding := function(q)
function> local R;
function> R := BaseRing(q);
function> return Matrix(R, [
function|return> [q[1,1], 0, 0, 0],
function|return> [0, 0, q[1,2], 0],
function|return> [0, q[2,1], 0, 0],
function|return> [0, 0, 0, q[2,2]]
function|return> ]);
function> end function;
````

Let us solve the exercise for the first braiding, namely 
````
> c := DimensionTwoDiagonalBraiding(Matrix(Rationals(), [[-1,-1],[-1,-1]]));
> c;
[-1  0  0  0]
[ 0  0 -1  0]
[ 0 -1  0  0]
[ 0  0  0 -1]
````
Now use the following code to get some dimensions of homogeneous components:
````
> c := DimensionTwoDiagonalBraiding(Matrix(Rationals(), [[-1,-1],[-1,-1]]));
> k := 0;
> dim := 0;
> repeat
repeat> d := ComputeDimension(c, k);
repeat> if not d eq 0 then
repeat|if> print d;
repeat|if> end if;
repeat> dim := dim+d;
repeat> k := k+1;
repeat> until d eq 0;
1
2
1
> dim 
4
````
For the second item, we need to consider the following braiding:
````
> c := DimensionTwoDiagonalBraiding(Matrix(Rationals(), [[-1,1],[-1,-1]]));
> c;
[-1  0  0  0]
[ 0  0  1  0]
[ 0 -1  0  0]
[ 0  0  0 -1]
````
The same code, applied to this braiding,
produces the sequence of dimensions 
`1, 2, 2, 2, 1` 
and hence an algebra of dimension 8. 
For the third exercise, the braiding is the following: 
````
> c := DimensionTwoDiagonalBraiding(Matrix(K, [[-1,w],[1,-1]]));
> c;
[-1  0  0  0]
[ 0  0  w  0]
[ 0  1  0  0]
[ 0  0  0 -1]
````
where `w` is a primitive cubic root of unity.  The dimensions of homogeneous
components are `1, 2, 2, 2, 2, 2, 1` and the dimension of the algebra is 12.

