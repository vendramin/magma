# Problems, questions, exercises

### 27/11/2025

1. Given a function with more than one output, such as ```IsCoercible```, how can we get the second argument of the output?
2. Given a finite field $F$, is there a way to get a generator of the group $F^\times$?
3. Can we use parameters when doing computations with matrices? For example, given a $A=\begin{matrix} 1 & t \\ 1 & -1 \end{matrix}$, where $t$ is a parameter, can we compute the determinant of $A$ depending on $t$? If it is not possible, should we consider $A$ as a matrix with coefficients in some particular ring?
4. What type is a subgroup (or any substructure or quotient)? How can we access the inclusion map?
5. Check if ```IsNormal``` only checks invariance under conjugation of a subset and not that it is a subgroup.
6. Is it possible to get a random element of ```GroupAlgebra(ComplexField(), Sym(3))```? If not, what is the problem?
7. On group algebras: let $G$ be a group $G$ and $K$ a field,
   - How is $G$ embedded in $K[G]$?
   - Can we compute (some) units of $K[G]$
   - Can you compute (some) idempotents of $K[G]$?
8. About the Promislow group $P$
```Magma
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

   - Why `Q := quo<P|N>` doesn't work? It works!
   - Why `IsAbelian(Q)` doesn't work? `IsAbelian` is defined for `GrpLie`, `GrpFin`, `GrpPerm`, GrpMat, GrpPC and `GrpGPC` while in this case `Q` is still a `GrpFP`; we need to change the type!

9. Given a polynomial $f$, does `f(1)` work instead of `Evaluate(f, 1)`? No.
10. Given a polynomial $f$ with integer coefficients, how can I consider it as a polynomial with coefficients in other fields? Example:
```> P<x> := PolynomialRing(IntegerRing());
   > f := x^5-3*x+2;
   > Factorization(f);
   [
       <x - 1, 1>,
       <x^4 + x^3 + x^2 + x - 2, 1>
   ]
```

Can we obtain the factorization of $f$ in other fields (e.g. finite fields)?

11. Let G be a finite sporadic group (e.g. $G=M_{22}$). Can we compute (things that are in the ATLAS)
    - Different representations of $G$ 
    - The conjugacy classes of $G$? (conjugacy class fusion from (maximal) subgroups to $G$)
    - Some character tables related to $G$ (e.g. maximal subgroups, some normalizers, some centralizers...)?
