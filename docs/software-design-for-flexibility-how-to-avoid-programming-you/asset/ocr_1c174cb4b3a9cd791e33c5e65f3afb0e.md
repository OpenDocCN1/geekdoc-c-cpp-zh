One classic application of unification matching is type inference: given a program and some type information about parts of the program, deduce type information about other parts of the program. For example, if we know that < is a procedure that takes two numerical arguments and produces a boolean value, then if we analyze the expression (g x y)), we can deduce that f and g are unary procedures; g accepts a boolean argument; f returns a numerical value; and x has a numerical value. If this information is used to deduce properties of the program that the expression is embedded in, we can learn a great deal about the program. Here is an analysis of the expression:

```
pp (infer-program-types '(g (< x y)))
(t type:17)
(t (type:procedure ((boolean-type)) ? type:17)) g)
(t (boolean-type)
(t (type:procedure (numeric-type) (numeric-type))
(boolean-type))
<
(t (numeric-type) x)
(t (numeric-type)
(t (type:procedure (? y:12) (numeric-type)) f)
(t (? y:12) y))))
```

This is the abstract tree of the given expression, annotated with types. Each subexpression x has been expanded into a typed expression of the form (t type x). For example, the reference to g has the type:

```
(type:procedure ((boolean-type)) ? type:17)
```

As expected, g is a procedure that accepts a boolean argument, but we have no information about its value. The unknown value type is represented by the pattern variable (? type:17).
Let's consider a more substantial example:

```
(define foo
(infer-program-types
'(define fact
(lambda n)
(begin
(define iter
(lambda (product counter
```