> > **PETER SESTOFT**  Despite the point made in Eric’s annotation, there’s a small incompatibility between Microsoft’s C# 4.0 compiler and previous versions: The compiler cannot infer the type of the conditional expression in the right-hand side below, complaining that “there is no implicit conversion between ‘<null>’ and ‘<null>’”.
> >
> > The C# 2.0 compiler would accept this expression. The C# 4.0 compiler’s message hints at the possible existence of a “null type” inside the compiler, or at least in the minds of those who wrote the error message. Given the extremely contrived piece of code, the incompatibility is nothing to lose sleep over.

```
int? x = args.Length > 0 ? null : null;
```

> > **VLADIMIR RESHETNIKOV**  A notion of “null type” existed in earlier versions of the C# specification, but was eliminated in C# 3.0, which resulted in a slightly different behavior in corner cases. Currently, null literal is an expression that has no type.

The runtime processing of a conditional expression of the form `b ? x : y` consists of the following steps:

+   - First, `b` is evaluated, and the bool value of `b` is determined:
+     - If an implicit conversion from the type of `b` to `bool` exists, then this implicit conversion is performed to produce a bool value.
+     - Otherwise, the operator `true` defined by the type of `b` is invoked to produce a bool value.
+   - If the bool value produced by the step above is true, then `x` is evaluated and converted to the type of the conditional expression, and this becomes the result of the conditional expression.
+   - Otherwise, `y` is evaluated and converted to the type of the conditional expression, and this becomes the result of the conditional expression.

> > **BILL WAGNER**  To me, both the null coalescing operator and the conditional operator are like strong spices: When used sparingly, they are great enhancers. Chris points out usages where the null coalescing operator creates clearer code than the equivalent if-then-else statements. Like strong spices, overuse is painful and ruins what could otherwise be very pleasant.

![](bbox=[0.906, 0.506, 0.999, 0.707])