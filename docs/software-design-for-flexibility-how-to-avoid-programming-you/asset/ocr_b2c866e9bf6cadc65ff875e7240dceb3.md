For simple arguments, applying a literal function is just a matter of constructing the expression that is the application of the function expression to the arguments. But literal functions must also be able to accept differential objects as arguments. When that also happens, the literal function must construct (partial) derivative expressions for the arguments that are differentials. For the ith n-argument function the appropriate derivative expression is:

```
(define (deriv-expr i n fexp)
  (if (= n 1)
    (derivative ,fexp)
    ((partial ,i ,fexp)))
```

Some arguments may be differential objects, so a literal function must choose, for each argument, a finite part and an infinitesimal part. As just for binary arithmetic handlers, the maximal factor must be consistently chosen. Our literal functions are able to take many arguments, so this may seem complicated, but we wrote the maximal-factor procedure to handle many arguments. This is explained in section 3.3.3.

If there are no differential objects among the arguments we just cons up the required expression. If there are differential objects we need to make a derivative of the literal function. To do this we find a maximal factor from all of the arguments and separate the finite parts of the arguments—the terms that do not have that factor. (The infinitesimal parts are the terms that have factor.) The partial derivatives are themselves literal functions with expressions that are constructed to include the argument index. The resulting differential object is the inner product of the partial derivatives at the finite parts of the arguments with the infinitesimal parts of the arguments.

This is all brought together in the following procedure:

```
(define (literal-function fexp)
  (define (the-function . args)
    (if (any differential? args)
      (let ((n (length args))
            (factor (apply maximal-factor args))
            (let ((realargs
                  (map (lambda arg factor)
                    (finite-part arg factor))
                  args))
              (deltargs))))))))
```