```
((derivative lambda (x) (expt x 3))) 'a
(* 3 (expt a 2))
```

The full power of the programming language is available, including higher-order procedures. This kind of system is useful in working with the very large expressions that occur in interesting physics problems.¹10

Let's look at a simple application: the computation of the roots of an equation by Newton's method. The idea is that we want to find values of x for which f(x) = o. If f is sufficiently smooth, and we have a sufficiently close guess x0, we can improve the guess by computing a new guess x1 by the formula:

```
$x_{n+1} = x_n - \frac{f(x_n)}{Df(x_n)}$
```

This can be repeated, as necessary, to get a sufficiently accurate result. An elementary program to accomplish this:

```
(define (root-newton f initial-guess tolerance)
(let ((Df (derivative f)))
(define (improve-guess xn)
(- xn (/ (f xn) (Df xn))))
(let loop ((xn initial-guess))
(let (xn+1 (improve-guess xn))
(if (close-enuff xn xn+1 tolerance)
nn+1
(loop xn+1)))))
```

Notice that the local procedure named Df in root-newton is a procedure that computes the derivative of the function by the procedure passed as f.
For example, suppose we want to know the angle θ in the first quadrant for which cos(θ) = sin(θ). (The answer is π/4 ≈ .7853981633974484) We can write:

```
(define (cs theta)
 (- (cos theta) (sin theta)))
```