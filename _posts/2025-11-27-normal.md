---
title: 'On normal subgroups'
date: 2025-11-27
author: 'Andrew Darlington'
categories:
  - questions
tags:
  - group
  - normal subgroup
  - subgroup
---
Does `IsNormal` only check invariance under conjugation of a subset and
not that it is a subgroup? 

It looks like `IsNormal(G,N)` asks for both `G` and `N` to be groups. Also, I
think Magma would throw an error if `G` and `N` were closed under different
group operations. So in a way, `IsNormal` does exactly what we want.  
