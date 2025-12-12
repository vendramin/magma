---
title: 'Join and meet'
date: 2025-12-05
author: VUB
categories:
  - questions
tags:
  - ring
  - group
  - subgroup
---
Let $G=\mathbb{Z}/24$, $H=\langle 4\rangle$ and 
$K=\langle 6\rangle$. Then $H+K\simeq C_{12}$ and 
$H\cap K\simeq C_{2}$. Let us do this with Magma: 
```
R := ResidueClassRing(24);;
G<g> := AdditiveGroup(R);
H := sub<G|4*g>;
K := sub<G|6*g>;
GroupName(H+K);
GroupName(H meet K);
```
This produces the following result: 
```
C12
C2
```
We can indeed check that $H+K=\langle 2\rangle$ and 
$H\cap K=\langle 12\rangle$. In fact, 
both commands we see here 
```
H+K eq sub<G|2*g>;
H meet K eq sub<G|12*g>;
```
return `true`. 

