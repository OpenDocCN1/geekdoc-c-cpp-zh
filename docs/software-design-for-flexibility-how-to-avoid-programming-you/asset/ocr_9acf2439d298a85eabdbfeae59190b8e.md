```
(define (vector-element-wise element-procedure)
(lambda vecs ; Note: this takes multiple vectors
(ensure-vector-lengths-match vecs)
(apply vector-map element-procedure vecs))
```

```
(define (ensure-vector-lengths-match vecs)
(let ((first-vec-length (vector-length (car vecs))))
(if any (lambda v)
  (not (n= (vector-length v)
      first-vec-length))
  veccs)
  (error "Vector dimension mismatch: vecs)))
```

The use of apply here is subtle. One way to think about it is to imagine that the language supported an ellipsis like this:

```
(define (vector-element-wise element-procedure)
(lambda v1 v2 ...)
(vector-map element-procedure v1 v2 ...))
```

Build the required arithmetic and show that it works for numerical vectors and for vectors with mixed numerical and symbolic coordinates.

+   b. Your vector addition required addition of the coordinates. The coordinate addition procedure could be the value of + operator that will be made available in the user environment by install-arithmetic!, or it could be the addition operation from the base vector extension. Either of these would satisfy many tests, and using the installed addition actually be more general. Which did you use? Show how to implement the other choice. How does this choice affect your ability to make future extensions to this system? Explain your reasoning.

Hint: A nice way to control the interpretation of operators in a procedure is to provide the procedure to use for each operator as arguments to a “maker procedure” that returns the procedure needed. For example, to control the arithmetic operations used in vector-magnitude one might write:

```
(define (vector-magnitude-maker + * sqrt)
(let ((dot-product (dot-product-maker + *)))
(define (vector-magnitude v))
```