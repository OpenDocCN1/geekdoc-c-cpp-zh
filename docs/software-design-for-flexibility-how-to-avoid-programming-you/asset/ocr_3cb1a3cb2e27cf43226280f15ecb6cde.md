How does the ordering of extensions affect the properties of the resulting arithmetic? The following procedure makes points on the unit circle:

```
(define (unit-circle x)
(vector (sin x) (cos x))
```

If we execute each of the following expressions in environments resulting from installing vec-before-func and func-before-vec:

```
((magnitude unit-circle) 'a
((magnitude vector sin cos)) 'a
```

The result (unsimplified) should be:

```
(sqrt (+ (* (sin a) (sin a)) (* (cos a) (cos a))))
```

However, each of these expressions fails with one of the two orderings of the extensions. Is it possible to make an arithmetic for which both evaluate correctly? Explain.

# 3.2 Extensible generic procedures

Systems built by combinators, as in section 3.1, result in beautiful diamond-like systems. This is sometimes the right idea, and we will see it arise again, but it is very hard to add to a diamond. If a system is built as a ball of mud, it is easy to add more mud.

One organization for a ball of mud is a system erected on a substrate of extensible generic procedures. Modern dynamically typed programming languages, such as Lisp, Scheme, and Python, usually have built-in arithmetic that is generic over a variety of numerical quantities, as integers, floats, rationals, and complex numbers [115, 64, 105]. But systems built on these languages are usually not easily extensible the fact.

The problems identified in section 3.1.5 are the result of using the combinator add-arithmetics. To solve these problems we will abandon that combinator. However, the arithmetic package