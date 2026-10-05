parameter could be declared to require its argument satisfy given predicates, which could be types and units; etc.

# Implementing generalized formal parameters

To implement generalized formal parameters, we need a special applicator that handles the new cases. This is accomplished by adding a single handler to g:apply, similar to the earlier one for strict compound procedures (see page 246):

```
(define-generic-procedure-handler g:apply
 (match-args general-compound-procedure?
  operands?
  environment?))
 (lambda (procedure operands calling-environment)
 (if (not (n:= (length procedure-parameters))
  (length operands)))
 (error "Wrong number of operands supplied")
 (let ((params procedure-parameters procedure))
  (body procedure-body procedure)))
 (let (names map procedure-parameter-name params))
  (arguments
   (map (lambda operand)
    (g:handle-operand param)
     operand
     calling-environment))
   params
  operands)))
 (g:eval body
 (extend-environment names arguments
  (procedure-environment procedure)))))
```

This differs from the strictのである in two ways: first, we must extract the names of the parameters, since they could be wrapped in declarations; we must handle the operands specially, depending on the declarations. This is done by the generic procedure procedure-parameter-name and g:handleoperand.

The procedure procedure-parameter-name allows us to add declarations to a formal parameter and still be able to retrieve its name. The default handler is the identity function, so the name of an undecorated formal parameter is just itself.