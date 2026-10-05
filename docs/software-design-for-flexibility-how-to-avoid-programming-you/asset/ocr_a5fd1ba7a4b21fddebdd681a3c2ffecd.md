```
(cons (cdadr defn) ; =(DEFINE foo
(cddr defn))); ; (LAMBDA (p...) b...))
```

This completes the usual list of special forms that define the syntax of the language. Of course, the generic procedure implementation enables creation of new special forms easily, allowing the language to grow to make it more convenient to express computational ideas that were not well supported in the base language. A language with many different syntactic constructs may be difficult to learn, document, and use; this is a classic engineering tradeoff (remember Alan Perlis's maxim on page 159).

# 5.1.2 apply

The traditional Scheme apply takes two arguments, the procedure to be applied and the evaluated arguments to be passed to the procedure. This is sufficient for Scheme, because Scheme is a strict applicative-order language with only lexically scoped variables.

By generalizing apply to take three arguments—the unevaluated operands and the calling environment—we make possible to include procedures that require normal-order evaluation for some parameters (e.g., call by need) or procedures that make declarations on parameters, such as types and units. We will make some extensions like these in section 5.2. The environment argument also makes it possible to accommodate non-lexically scoped variables, but we will not do so; it is generally a bad idea. We will start out with Scheme applicative-order, with generic hooks for extension.

Our apply is a generic procedure with three arguments:

```
(define g:apply)
(simple-generic-procedure 'apply 3 default-apply))

(define (default-apply procedure operands calling-environment)
(error "Unknown procedure type"))
```

We need handlers for the various kinds of procedures. Some procedures, like arithmetic addition (usually named by the + operator), are strict: they need all of their arguments evaluated before they can compute a value. In Scheme all procedures are strict, including primitive procedures (implemented in the system or