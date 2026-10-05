+   a. Sketch a plan for how to extend the combinators to use the more general arities. Note that you may not always be able to use arithmetic on the arities. What choices will you have to make in reformulating spread-combine? For example, what kinds of restrictions will be needed on the procedures f, g, and h in spread-combine?

+   b. Apply your plan and make it all work!

For any language there are primitives, means of combination, and means of abstraction. A combinator language defines primitives and means of combination, inheriting its means of abstraction from the underlying programming language. In our example, the primitives are functions, and the means of combination are the combinators compose, parallel-combine, spread-combine, and others we may introduce.

# Multiple values

Notice that parallel-combine and spread-combine are similar in that each is the application of a combiner h to the results of f and g. But we did not use compose to construct these combinators. To abstract this pattern we need to be able to return multiple values from the combination of f and g and then use those values as arguments for h. We could do this by returning a compound data structure, but a better way is to use the Scheme multiple-value return mechanism. Given multiple values we can define spread-combine as a composition of two parts, h and it of f and g;⁵

```
(define (spread-apply f g)
  (let ((n (get-arity f)) (m (get-arity g))
    (let ((t (+ n m)))
      (define (the-combination args)
        (assert (= (length args) t))
        (values (apply f (list-head args n))
              (apply g (list-tail args n))))
      (restrict-arity the-combination t))))))
```