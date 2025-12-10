---
title: 'Three questions on group algebras'
date: 2025-11-27
author: Andrew Darlington
categories:
  - questions
tags:
  - group
  - algebra
  - group algebra
---
* How is the group embedded in the group algebra?

Let $K$ be a field, $G$ a group and $A=K[G]$ the group algebra. In Magma, for a
group algebra `A` and an element `g` of the group, writing `A!g` gives the
element $1_Kg\in A$. You can also recover `G` with `Group(A)`.

* Can we compute (some) units of a group algebra?

If the group algebra is finite, the best way I can find to do this is looping
through the elements of the group algebra and then asking if they are units or
not; this is done with the `IsUnit` function. If the group algebra is not
finite, then I don’t know yet, but you can certainly still test whether
specific elements are units or not with the same function.

* Can you compute (some) idempotents of a group algebra?

Similar to the previous point, but with the function `IsIdempotent`.


