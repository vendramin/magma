---
title: 'Given a function with more than one output, how can we get the second argument of the output?'
date: 2025-11-27
categories:
  - questions
tags:
  - basic
---
For types `A`, `B` and an object `x` of type `A`, if `x` is coercible into `B`,
then defining 
```> _, y := IsCoercible(B,x)
``` 
will assign the result of the coercion to `y` without assigning any value to. I
believe this will work for any number of arguments.
