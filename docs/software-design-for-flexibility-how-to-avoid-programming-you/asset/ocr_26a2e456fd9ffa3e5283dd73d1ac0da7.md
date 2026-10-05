the maximal factors (here δ or dy) being primary. It doesn't matter
which is chosen, because mixed partials of R → R commute.25

```
(define (finite-part x #!optional factor)
(if (differential? x)
 (let ((factor default-maximal-factor x))
  (make-differential
    (remove (lambda term)
      (memv factor (diff-factors term))
      (diff-terms x))))
 x))
```

```
(define (infinitesimal-part x #!optional factor)
(if (differential? x)
 (let ((factor default-maximal-factor x))
  (make-differential
    (filter (lambda term)
      (memv factor (diff-factors term))
      (diff-terms x))))
 0))
```

```
(define default-maximal-factor x factor)
(if (default-object? factor)
 (maximal-factor x)
 factor))
```

# How extracting really works

As explained on page 114, to make it possible to take multiple
derivatives or to handle functions with more than one argument, a
differential object is represented as a multivariate power series in
which no infinitesimal increment has exponent greater than one.
Each term in this series has a coefficient and a list of infinitesimal
incremental factors. This complicates the extraction of the derivative
with respect to one incremental factor. Here is the real story:

In the case where a differential object is returned we must find
th terms of the result that contain the infinitesimal factor dx for
the derivative we are evaluating. We collect those terms, removing
dx from each. If there are no terms left after taking the ones with
dx, the value of the derivative is zero. If there is exactly one term left,
which has no differential factors, then the coefficient of that term is
the value of the derivative. But if there are remaining terms with