```
(map (lambda arg)
  (infinitesimal-part arg factor)
  args))
(let ((fxs (apply the-function realargs))
  (partials
    (map (lambda i)
      (apply (literal-function
        (deriv-expr i n fexp))
        realargs))
      (iota n))))
    (fold d+: fxs
      (map d:* partials deltargs))))
'(,fexp, @args))
the-function)
```

# Exercise 3.12: Functions with structured values

We made the extract-dx-part generic (page 110) so we could extend it for values other than differential objects and functions. Extend extract-dx-part to work with derivatives of functions that return vectors. Note: You also have to extend the replace-dx generic procedure (page 122) in the extractor.

# 3.4 Efficient generic procedures

In section 3.2.3 we dispatched to a handler by finding an applicable rule using the dispatch store provided in the metadata:

```
(define (generic-procedure-dispatch metadata args)
  (let ((handler
    (get-generic-procedure-handler metadata args))
    (apply handler args)))
```

The implementation of the dispatch store (page 98) we used (on page 89) to make the simple-generic-procedure constructor was rather crude. The simple dispatch store maintains the rule set as a list of rules. Each rule is represented as a pair of an applicability and a handler. The applicability is a list of lists of