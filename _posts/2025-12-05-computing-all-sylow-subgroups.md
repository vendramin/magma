---
title: 'Computing all Sylow subgroups'
date: 2025-11-27
author: VUB
categories:
  - questions
tags:
  - group
  - Sylow subgroup
  - subgroup
  - conjugation
---
How can we quickly get all Sylow subgroups
of a given group?

To compute Sylow subgroups we have the function 
`SylowSubgroup`, but this function returns
only one Sylow subgroup. 
How can we quickly get them all? Here is an answer: 
```
S3 := Sym(3);
P := SylowSubgroup(S3,2);
{ P^x : x in S3 };
```
Possibly faster: conjugate the Sylow subgroup computed 
by each element of a (right) transversal of the Sylow. 
The code 
```
t := Transversal(S3,P);
{ P^x : x in t };
```
produces the same result as before, namely 
```
{
    Permutation group acting on a set of cardinality 3
    Order = 2
        (1, 3),
    Permutation group acting on a set of cardinality 3
    Order = 2
        (1, 2),
    Permutation group acting on a set of cardinality 3
    Order = 2
        (2, 3)
}    
```
Alternatively, we can also use the function `Conjugates`. The command 
```
Conjugates(S3,P);
```
produces the same output as before. 

