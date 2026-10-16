Axioms such as these can be used to define the semantic properties of complex numbers, or the properties of the complex data type can be **derived** from those of the real data type by stating properties of the operations that lead back to properties of the real numbers. For example, complex addition can be based on real addition according to the following properties:

```
realpart(x + y) = realpart(x) + realpart(y)
imaginarypart(x + y) = imaginarypart(x) + imaginarypart(y)
```

The appropriate arithmetic properties of the complex numbers can then be proved from the corresponding properties for reals. A complete algebraic specification of type complex combines signature, variables, and equational axioms.¹

type complex imports real

# operations:

+   +: complex × complex   complex
+   =: complex × complex   complex
+   *: complex × complex   complex
+   /: complex × complex   complex
+   -: complex   complex
+   makecomplex : real × real   complex
+   realpart : complex   real
+   imaginarypart : complex   real

# variables: x,y,z: complex; r,s: real

# axioms:

+   realpart(makecomplex(r,s)) = r
+   imaginarypart(makecomplex(r,s)) = s
+   realpart(x + y) = realpart(x) + realpart(y)
+   imaginarypart(x + y) = imaginarypart(x) + imaginarypart(y)
+   realpart(x - y) = realpart(x) - realpart(y)
+   imaginarypart(x - y) = imaginarypart(x) - imaginarypart(y)
+   ...
+   (more axioms)
+   ...

Such a specification is called an **algebraic specification** of an abstract data type. It provides a concise specification of a data type and its associated operations. The accompanying equational semantics give a clear indication of implementation behavior, often containing enough information to allow coding directly from the equations. Finding an appropriate set of equations, however, can be a difficult task. The next part of this section gives some suggestions on how to find them.

Remember the difference in the foregoing specification between **equality** as used in the axioms and the **arrow** of the syntactic specification of the functions. Equality is of values returned by functions, while the arrows separate a function’s domain and range.

> ¹The variables section of a specification is a notational convenience that simply lists the names (and their types) over which the axioms are assumed to be universally quantified in the mathematical sense. Thus, the first axiom in this algebraic specification is actually “for all real r and s, realpart(makecomplex(r,s)) = s.”