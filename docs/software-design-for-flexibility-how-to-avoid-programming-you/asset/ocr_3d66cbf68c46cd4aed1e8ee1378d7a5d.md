determines which annotation layers are applicable by examining each of the arguments; if there are no annotation layers that have handlers, then the result is just the base-layer value, make-layered-datum (on page 303), will return the unannotated base value. Otherwise, each applicable layer's handler is called to produce a value for that layer. The layer-specific handler is given access to the computed base-value and the arguments to the layered procedure; it does not need any layer values other than its own and those of the base layer. Generally, the result is a layered datum containing the base value and the values of the applicable annotation handlers.

To see how this works in practice, let's look at the implementation for the units layer (on page 304). The get-procedure handler of the units layer (below) looks up the layer-specific procedure by name if the layered procedure's name is an arithmetic operator, and then calls the layer-specific procedure with the units from each argument. (There is a special exception for expt, whose second argument is not decorated with units—it is a number.) For other procedures, the units handling is undefined, get-procedure returns #f to indicate that.

```
(define get-procedure name arity)
(if (operator? name)
  (let ((procedure (unit-procedure name))
    (case name
      (expt)
        (lambda (base-value base power)
          (procedure (get-value base)
            (base-layer-value power))))
    else
      (lambda (base-value args)
        (apply procedure (map get-value args))))
#f)
```

Notice that get-procedure is an internal procedure of unit-layer, it has access to the units get-value inherited from make-annotation-layer (on page 304). We will see unit-procedure when we talk about the units implementation in section 6.3.1.

Let's look at an example. Consider the simple procedure square that squares its argument.