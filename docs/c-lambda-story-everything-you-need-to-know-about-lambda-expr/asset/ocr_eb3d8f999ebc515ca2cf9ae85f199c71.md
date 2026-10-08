# The Syntax of Lambda Expression

Below you can find a “diagram” that illustrates the syntax for lambdas:

```
[] () qualifiers exception attr -> ret { /*code */ }
^ ^ ^
| | | |
| | optional: trailing return type
| optional: mutable, exception specification or noexcept, attributes
| parameter list (optional when no specifiers added)
lambda introducer with an optional capture list
```

Before we start it's handy to bring some core definitions from the C++ Standard:

From [expr.prim.lambda#2] :

> The evaluation of a lambda-expression results in a prvalue temporary. This temporary is called the closure object.

And from [expr.prim.lambda#3] :

> The type of the lambda-expression (which is also the type of the closure object) is a unique, unnamed non-union class type — called the closure type.