The default handler is a procedure that always returns false, and at this time there is only one substantive handler, which retrieves the name of a named variable.

We also make the predicate that determines if its argument is a match variable generic, although at this time the only objects that satisfy match:var? are named variables.

```
(define match:var?
  (simple-generic-procedure 'match:var? 1)
  (constant-generic-procedure-handler match:var #f)))
```

```
(define-generic-procedure-handler match:var?
  (match-args match:named-var?)
  (constant-generic-procedure-handler #t))
```

# The compiler maps a pattern to the corresponding matcher:

```
(define (match:compile-pattern pattern)
  (cond ((match:var? pattern)
         (case (match:var-type pattern)
          ((?)) (match:element pattern))
          ((???) (match:segment pattern))
          (else (error "Unknown var type: pattern))))
         (list? pattern)
         (match:list (map match:compile-pattern pattern))
         (else ; constant)
         (match:eqv pattern))))
```

By varying this compiler, we can change the syntax of patterns any way like.

```
(run-matcher
  (match:compile-pattern '(a ((? b) 2 3) (? b) c))
  '(a (1 2 3) 1 c)
  match:bindings
  ((b 1 ?)))
```

# Exercise 4.5: Backtracking

In the example on page 177 we get multiple matches, returning #f from the success procedure print-all-matches. This is probably