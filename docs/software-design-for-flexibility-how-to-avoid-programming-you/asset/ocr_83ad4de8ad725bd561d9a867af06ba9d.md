(+ 1 (* 2 3) (/ 8 2))

Of course, this has the value 11. It is computed by evaluating the operator and the operands, then applying the value of the operator (the procedure) to the values of the operands (arguments).

This process can be clarified by reformulating the computation in continuation-passing style. Here we invent new operators **, //, and ++ to name continuation-passing style multiplication, division, and addition procedures:

```
(define (* ml m2 continue)
(continue (* m1 m2)))
```

```
(define (// n d continue)
(continue (/ n)))
```

```
(define (++ a1 a2 continue)
(continue (+ a1 a2)))
```

These procedures differ from the usual *, /, and in that they do not return to their caller; rather they are defined to call their argument with the value computed. The argument that receives the value is called the continuation procedure. We used continuation-passing style in sections 4.2.2 and 5.4.2 and also in the unifier on page 188.

The computation of (+ 1 (* 2 3) (/ 8 2)) in continuation-passing style looks like:

```
** 2 3
(lambda (the-product)      ; A
(// 8 2)
(lambda (the-quotient)      ; B
(++ 1-product-the-quotient
k))))
```

with k is the final continuation procedure, which takes one argument, which is the value 11 of the computation.26

In this example the procedure ** computes the product of 2 and 3 and calls its continuation procedure (the lambda expression labeled by comment A) with 6. Thus, in the body of A, the-product is bound to 6. In the body of A the procedure // computes the quotient of 8 and 2 and passes the resulting 4 to the procedure B,