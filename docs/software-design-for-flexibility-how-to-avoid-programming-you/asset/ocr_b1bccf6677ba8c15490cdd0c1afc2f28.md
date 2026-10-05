s2) ;arbitrary
s1
(if (exact-zero? v2)
s2
(support-set-union s1 s2)))

Division (and arctangent, not shown) also has to examine the base layer to deal with zero arguments. If the dividend is zero, that is sufficient to support the result that the quotient is zero. The divisor won't ever be zero because the base-layer computation will have signaled an error and (support:/ base-value arg1 arg2

```
(define (let (v1 (base-layer-value arg1))
(s1 (support-layer-value arg1))
(s2 (support-layer-value arg2))
(if (exact-zero? v1)
s1
(support-set-union s1 s2)))
```

These optimizations for * and make sense only when we can prove that an argument is really zero, not an unsimplified symbolic expression.(But if an expression simplifies to exact zero we can use that fact!)

```
(define (exact-zero? x)
(and (n:number? x) (exact? x) (n:zero? x)))
```

The support-abstraction is implemented as a list starting with the symbol support-set

```
(define (%make-support-set elements)
(cons 'support-set-elements))
```

```
(define (support-set? object)
(and (pair? object)
(eq? 'support-set (car object))
(list? (cdr object))))
```

```
(define (support-set-elements support-set)
(cdr support-set))
```

along with a few extra utilities to complete the abstraction.

```
(define (make-support-set elements)
(if (null? elements))
```