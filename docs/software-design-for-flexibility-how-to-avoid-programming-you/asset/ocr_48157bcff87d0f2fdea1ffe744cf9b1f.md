```
(define-syntax rule
(er-macro-transformer
  (lambda ((form rename compare))
    (let ((pattern (cadr form))
          (handler-body (caddr form)))
      (r-make-rule (rename 'make-rule))
      (r-lambda (rename 'lambda))))
  '(r-make-rule ,pattern
    (r-lambda
      (match:pattern-names pattern)
        ,handler-body)))))
```

We can least partially check this macro with the following magic incantation that ensures macros appear in an expression:

```
pp (syntax '(rule '* (? b) (? a))
  (and (expr<? a b)
    (* ,a ,b)))
  (the-environment))
(make-rule '* (? b) (? a))
  (lambda (b a)
  (and (expr<? a b)
    (list '* ,a))))
```

We see that the rule expands into a call to make-rule with the pattern and its handler procedure. This is the expression that is evaluated to make the rule. In more conventional languages, a macro, such as rule, expands directly into code that is substituted for the macro call. However, this process is not referentially transparent, because the macro expansion may use symbols that conflict with the user's symbols. In Scheme we try to avoid this problem, allowing a user to write hygienic macros that cannot cause conflicts. This is more complicated than just substituting one expression for another. We will not try to explain the problems or the solutions here, but we will just use the solutions described in the MIT/GNU Scheme reference manual [51].

# 4.2.4 Pattern-directed invocation

The rule executive, try-rules, can also be used to implement procedures that use patterns for dispatching on input properties. The arguments to a pattern operator are matched against the pattern