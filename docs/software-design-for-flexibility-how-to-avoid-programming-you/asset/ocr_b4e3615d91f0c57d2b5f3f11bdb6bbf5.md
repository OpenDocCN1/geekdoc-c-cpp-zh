We can implement the coercion of numerical quantities to constant functions quite easily, by minor modifications to the procedure pure-function-extender:

```
(define (function-extender codomain-arithmetic)
(let ((codomain-predicate
    (arithmetic-domain-predicate codomain-arithmetic))
  (make-arithmetic 'function
    (disjoin codomain-predicate function)
      (list codomain-arithmetic))
  (lambda name codomain-constant)
    codomain-constant)
  (lambda operator codomain-operation)
    (make-operation operator
      (any-arg operator-arity operator)
        function?
      codomain-predicate)
  (lambda things)
    (lambda args)
      (apply-operation codomain-operation
        (map (lambda thing)
          ;; here is the coercion;
          (if function? thing)
            (apply thing args)
            thing))
        things))))
```

To allow the coercion of codomain quantities, such as numbers, to constant functions, the domain of the new function arithmetic must contain both functions and the elements of the codomain of the functions (the possible values of the functions). The operator implementation is applicable if any of the arguments is a function; and functions are applied to the arguments that are given. Note that the constant generator for the make-arithmetic doesn't need to rewrite the codomain constants as functions, since the constants can be used directly.

With this version we can

```
(install-arithmetic!
(extend-arithmetic function-extender combined-arithmetic))

((+ 1 cos) 'a)
(+ 1 (cos a))
```