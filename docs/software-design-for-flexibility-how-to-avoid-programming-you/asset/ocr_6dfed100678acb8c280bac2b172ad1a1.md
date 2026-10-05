```
(lambda operator)
(lambda args (cons operator args))))
```

To use this newly defined arithmetic, we install it. It redefines the arithmetic operators to use this arithmetic:3

```
(install-arithmetic! symbolic-arithmetic-1)
```

install-arithmetic! changes the values of the user's global variables that are the names of the arithmetic operators defined in the arithmetic to their values in that arithmetic. For example, after this install:

```
(+ 'a b)
(+ a b)
```

```
(+ 1 2)
(+ 1 2)
```

We can observe the result of taking one step of the Stormer evolution:45

```
(pp (x 0)
((evolver F 'h stormer-2)
(make-initial-history 't 'h 'xt-ht 'xt-2h)
1)))
(+ (* 2 xt) (* -1 xt-h))
 (* (/ expt h 2) 12)
 (+ (* 13 negate xt) (* -2 negate xt-h))
(negate xt-2h))))
```

We could easily produce simplified expressions by replacing the cons in symbolic-arithmetic-1 with an algebraic simplifier, and then we would have a symbolic manipulator. (We will explore algebraic simplification in section 4.2).

This transformation was ridiculously easy, and yet our original design didn't make any provisions for symbolic computation. We could just as easily add support for vector arithmetic, matrix arithmetic, etc.

# Problems with redefining operators