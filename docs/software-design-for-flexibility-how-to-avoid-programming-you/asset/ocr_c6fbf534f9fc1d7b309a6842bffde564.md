# Exercise 3.7: Literal vectors and matrices

It is also possible to have arithmetic on literal matrices and literal vectors with an algebra of symbolic expressions of vectors and matrices. Can you make symbolic algebra of these compound structures play well with vectors and matrices that have symbolic numerical expressions as elements? Caution: This is quite hard. Perhaps it is appropriate as part of a long-term project.

# 3.3 Example: Automatic differentiation

One remarkable application of extensible generic procedures is automatic differentiation.¹14 This is a beautiful way to obtain a program that computes the derivative of the function computed by a given program.¹15 Automatic differentiation is now an important component in machine learning applications.

We will see that a simple way to implement automatic differentiation is to extend the generic arithmetic primitives to work with differential objects, a new compound data type. This will enable the automatic differentiation of symbolic as well as numerical functions. It will also enable us to make automatic differentiation work with higher-order procedures—procedures that return other procedures as values.

Here is a simple example of automatic differentiation to illustrate what we are talking about:

```
((derivative (lambda x) (expt x 3))) 2)
12
```

Note that the derivative of the function that computes the cube of its argument is a new function, which when given 2 as its argument returns 12 as its value.

If we extend the arithmetic to handle symbolic expressions, and we do some algebraic simplification on the result, we get: