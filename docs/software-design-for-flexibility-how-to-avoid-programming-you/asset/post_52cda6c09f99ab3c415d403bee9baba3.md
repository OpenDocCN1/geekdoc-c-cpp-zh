
For example we want to compute a second derivative we must take a derivative of a derivative function. The evaluation of such a function will have two infinitesimals in play. To enable the computation of multiple derivatives and derivatives of functions of several variables we define an algebra of differential objects in “infinitesimal space.” The objects are multivariate power series in no infinitesimal increment exponent greater than one.

A differential object is represented by a tagged list of the terms of the power series. Each term has a coefficient and a list of infinitesimal incremental factors. The terms are kept sorted, in descending order. (Order is the number of incrementals. So $\delta dx$ is higher than $\delta x$ or $\delta y$.) Here is a quick and dirty implementation:

```scheme
(define differential-tag 'differential')

(define (differential? x)
  (and (pair? x) (eq? (car x) differential-tag)))

(define (diff-h)
  (if (differential? h)
    (cdr h)
    (list (make-diff-term h ')))))
```

The list is just the cdr of the differential object. However, if we are given an object that is not explicitly a differential object, for example a number, we coerce it to a differential object with a single term and no incremental factors. When we make a differential object from a (presorted) list of terms, we always try to return a simplified version, which may be just a number, which is not explicitly a differential object:

```scheme
(define (make-differential terms) ; Nonzero terms
  (let ((terms
    (filter
      (lambda (term)
        (let ((coeff (diff-coefficient term))
          (not (number? coeff) (= coeff 0))))
    terms)) 0))
    (cond ((null? terms)
      (and (null? (cdr terms)))
            ;; Finite part only:
            (null? (diff-factors (car terms))))
    (diff-coefficient (car terms))))

```scheme
  ((every diff-term? terms)
  (cons differential-tag terms)
  (else (error "Bad terms")))
```

In this implementation the terms are also represented as tagged lists, each containing a coefficient and an ordered list of factors.

```scheme
(define diff-term-tag 'diff-term)

(define (make-diff-term coefficient factors)
  (list diff-term-tag coefficient factors))

(define (diff-term? x)
  (pair? x) (eq? (car x) diff-term-tag))
```

```scheme
(define diff-coefficient x)
  (cadr x))
```

```scheme
(define diff-factors x)
  (caddr x))
```

To compute derivatives we need to be able to add and multiply differential objects:

```scheme
(define d:+ x y)
  (make-differential
  (+diff-termlists diff-terms x) (diff-terms y)))
```

```scheme
(define d:* x y)
  (make-differential
  (*diff-termlists diff-terms x) (diff-terms y)))
```

and we also need this:

```scheme
(define (make-infinitesimal dx)
  (make-differential (list (make-diff-term 1 (list dx))))
```

Addition of term lists is where we enforce and use the sorting of terms, with higher-order terms coming earlier in the lists. We add two terms only if they have the same factors. And if the sum of the coefficients is zero we do not include the resulting term.

```scheme
(define (+diff-termlists l11 l12)
  (cond ((null? l11) l12)
        ((null? l12) l11)
        (else
```scheme
  (let ((t1 (car l11)) (t2 (car l12)))
    (cond ((equal? (diff-factors t1) (diff-factors t2))
              (let ((newcoeff (+ (diff-coefficient t1)
                              (diff-coefficient t2)))
                (if (and (number? newcoeff)
                    (= newcoeff 0))
                    (+diff-termlists (cdr l11) (cdr l12))
                  (cons
                    (make-diff-term newcoeff
                      (diff-factors t1))
                    (+diff-termlists (cdr l11)
                      (cdr l12))))))
          ((diff-term? t1 t2)
            (cons t1 (+diff-termlists (cdr l11) (cdr l12))))
          (else
            (cons t2
              (+diff-termlists l11 (cdr l12))))))))
```

Multiplication of term lists is straightforward, if we can multiply individual terms. The product of two term lists l11 and l12 is the term list resulting from adding up the term lists resulting from multiplying every term in l1 by every term in l12.

```scheme
(define *diff-termlists l11 l12)
  (reduce (lambda (x y)
    (+diff-termlists x y)
    '()
    (map (lambda (t1) (map (lambda (t2)
      (*diff-terms t1 t2))
    l12))))
```

A term has a coefficient and a list of factors (the infinitesimals). A differential object may have an infinitesimal with an exponent greater than one, because $\delta x = 0$. Thus, when we multiply two terms we must check that the lists of factors are merging no factors in common. This is the reason that *diff-terms returns a list of the product term or an empty list, to be appended in *diff-termlists. We keep the factors sorted when we merge the two lists; this makes it easier to sort the terms.

```scheme
(define *diff-terms x y)
  (let ((fx (diff-factors x)) (fy (diff-factors y)))
    (if (null? (ordered-intersect fx fy))
      (list (make-diff-term
        (*diff-coefficient x) (diff-coefficient y)
          (ordered-union fx fy))
      '())))

## Finite and infinitesimal parts

A differential object has a finite part and an infinitesimal part. Our diff:binary-proc procedure is not correct for differential objects with more than one infinitesimal. To ensure that the parts of x and y are selected consistently we actually use:

```scheme
(define (diff:binary-proc f d0 d1)
  (define (bop x)
    (let ((factor (maximal-factor x)))
      (let ((dx (infinitesimal-part x))
            (dy (infinitesimal-part y))
            (xe (finite-part x))
            (ye (finite-part y)))
        (d+: xe ye)
        (d*: dx dy)
        (d*: xe dy)))))
```

where factor is chosen by maximal-factor so that both x and y contain it in a term with the largest number of factors. The finite part of a differential object is all terms except for terms containing the maximal factor in a term of highest order, and the infinitesimal part is the remaining terms, all of which contain that factor. Consider the following computation:

```
f(x + dx, y + dy) = f(x, y) + ∂f(x, y) · dx + ∂f(x, y) · dy + ∂f(x, y) · dxdy

The highest-order term ∂f(x, y) · dxdy is symmetrical with respect to x and y. The crucial point is that we may break the differential object into parts in any way consistent with any one of the maximal factors (here dx or dy) being primary. It doesn't matter which is chosen, because mixed partials commute.

```scheme
(define (finite-part x [optional factor])
  (if (differential? x)
    (let ((factor (maximal-factor x)))
      (make-differential
        (filter (lambda term)
          (memv factor (diff-factors term))
          (diff-terms x))))
    x))

(define (infinitesimal-part x [optional factor])
  (if (differential? x)
    (let ((factor (maximal-factor x)))
      (make-differential
        (filter (lambda term)
          (memv factor (diff-factors term))
          (diff-terms x))))
    0))

(define (default-maximal-factor x factor)
  (if factor
    factor
    (maximal-factor x)))
```

## How extracting really works

As explained on page 114, to make it possible to take multiple derivatives or to handle functions with more than one argument, a differential object is represented as a multivariate power series in which no infinitesimal increment has exponent greater than one. Each term in this series has a coefficient and a list of incremental factors. This complicates the extraction of the derivative with respect to one incremental factor. Here is the real story:

In the case where a differential object is returned we must find the terms of the result that contain the infinitesimal factor dx for the derivative we are evaluating. We collect those terms, removing dx from each. If there are no terms left after taking the ones with dx, the value of the derivative is zero. If there is exactly one term left, which has no differential factors, then the coefficient of that term is the value of the derivative. But if there are remaining terms with differential factors, we must return the differential object with those residual terms as the value of the derivative.

```scheme
(define (extract-dx-differential value dx)
  (let ((dx-diff-terms
    (filter-map
      (lambda term)
        (let ((factors (diff-factors term)))
          (and (memv dx factors)
            (make-diff-term (diff-coefficient term))
              (delv dx factors))))
      (diff-terms value))))
    (cond ((null? dx-diff-terms) 0)
          ((and (null? (cdr dx-diff-terms))
                (null? (diff-factors (car dx-diff-terms))))
            (diff-coefficient (car dx-diff-terms)))
          (else (make-differential dx-diff-terms)))))
```

## Higher-order functions

For many applications we use our automatic differentiator to work correctly for functions that return values as:

```scheme
((derivative
  (lambda (x))
    (lambda (y z)
      (* x y z))))
2)
3
4)
;Value: 12
```

Including literal functions and partial derivatives makes this even more interesting.

```scheme
((derivative
  (lambda (x))
    ((partial 1) (literal-function 'f))
      x 'v)))
'u)
((partial 0) ((partial 1) f) u v))
```
