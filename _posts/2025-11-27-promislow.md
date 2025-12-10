---
title: 'The Promislow group'
date: 2025-11-27
author: Silvia Properzi
categories:
  - questions
tags:
  - group
  - infinite group
  - Promislow group
---
About the Promislow group.
```
P<a,b> := Group < a,b | a^-1*b^2*a*b^2, b^-1*a^2*b*a^2 >;
> x := a^2;
> y := b^2;
> z := (a*b)^2;
> N := sub<P|x,y,z>;
> Q, p := quo<P|a^2,b^2,(a*b)^2>;
> IdentifyGroup(Q);
<4, 2>
> GroupName(Q);
C2^2
```
Some questions: 
* Why `Q := quo<P|N>` doesn’t work? 

It does! The type of a subgroup `N` of a group `G` should be the same as the
type of `G`. I think that in most cases, Magma views `N` as a literal subset of
`G` and doesn’t give an inclusion map, but it looks like it gives an inclusion
map in the case that the groups are finitely presented abelian.

* Why `IsAbelian(Q)` doesn’t work? 

The function `IsAbelian` is defined for `GrpLie`, `GrpFin`, `GrpPerm`,
`GrpMat`, `GrpPC` and `GrpGPC` while in this case `Q` is still a `GrpFP`; we
need to change the type!

