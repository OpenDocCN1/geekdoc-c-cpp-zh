multiplied by a unitless number, the result is the units of the quantity with units. So the unit arithmetic needs a multiplicative identity for unitless numbers—this is unit:none. The procedure simple-operation combines the operator, the test for applicability, and the procedure that implements the operation:

```
(define (unit-arithmetic)
  (make-arithmetic 'unit? '()
  (lambda (name)
    (if (eq? name 'multiplicative-identity)
        unit:none
        (default-object))
    (lambda (operator)
      (simple-operation
        unit?
        (unit-procedure operator)))))
```

We call unit-procedure to get the appropriate procedure for each operator:

```
(define (unit-procedure operator)
  (case operator
    (*) unit*
    (//) unit/
    ((remainder) unit:remainder)
    ((expt) unit:expt)
    ((invert) unit:invert)
    ((square) unit:square)
    ((sqrt) unit:sqrt)
    ((atan) unit:atan)
    ((abs ceiling floor negate round truncate)
      unit:simple-unary-operation)
    ((+ max min)
      unit:simple-binary-operation)
    ((acos asin cos log sin tan)
      unit:unitless-operation)
    ((angle imag-part magnitude make-polar make-rectangular
      real-part)
      ; first approximation:
      unit:unitless-operation))
  (else
    (if (eq? 'boolean (operator-codomain operator))
        (if (n:=1 (operator-arity operator)
          unit:unary-comparison
          unit:binary-comparison)
        unit:unitless-operation))))
```