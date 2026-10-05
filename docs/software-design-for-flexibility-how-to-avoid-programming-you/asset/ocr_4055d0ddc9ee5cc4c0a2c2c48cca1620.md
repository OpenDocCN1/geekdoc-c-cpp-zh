abstraction is still useful, as is the idea of an extender. We will build an arithmetic package in which the operations use generic procedures that can be dynamically augmented with new behavior. We can then extend the generic arithmetic and add the extensions to the generic arithmetic.¹12

We will start by implementing generic procedures, which are procedures that can be dynamically extended by adding handlers after the generic procedures are defined. A generic procedure is a dispatcher combined with a set of rules, each of which describes a handler that is appropriate for a given set of arguments. Such a rule combines a handler with its applicability.

Let's examine how this might work, by defining a generic procedure named plus that works like addition with numeric and symbolic quantities:

```
(define simple-generic-procedure 'plus 2 #f))

(define-generic-procedure-handler plus
(all-args 2 number?)
(lambda (a b) (+ a b)))

(define-generic-procedure-handler plus
(any-arg 2 symbolic? number?)
(lambda (a b) (list '+ a b)))

(plus 1 2)
3

(plus 1 'a)
(+ 'a a)

(plus 'a 2)
(+ 'a 2)

(plus 'a 'b)
(+ 'a b)
```

The procedure simple-generic-procedure takes three arguments: The first is an arbitrary name to identify the procedure when debugging; the second is the procedure's arity. The third argument is used to provide a default handler; if none is supplied (indicated by #f), if no specific handler is applicable an error is signaled. Here plus is bound to the new generic procedure returned