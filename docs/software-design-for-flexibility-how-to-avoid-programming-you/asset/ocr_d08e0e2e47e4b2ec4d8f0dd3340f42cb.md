simplifying a two-step integration. Using a magic symbolic-expression simplifier we get a pretty readable expression. This can be useful for debugging a numerical process.

```
(* 2 (expt h 2) (f t xt))
(* -1/4 (expt h 2) (f (* -1 h) t) xt-2h))
(* 1/6 (expt h 2) (f (* -2 h) t) xt-2h))
(* 13/12
(expt h 2)
(f (+ h t))
(* (+ 13/12 (expt h 2) (f t xt))
(* -1/6 (expt h 2) (f (* -1 h) t) xt-2h))
(* 1/12 (expt h 2) (f (* -2 h) t) xt-2h))
(* 2 xt)
(* -1 xt-h)))
(* 3 xt)
(* -2 xt-h))
```

For example, notice that there are only four distinct top-level calls to the acceleration function f. The second argument to the fourth top-level call uses three calls to f that have already been computed. If we eliminate common subexpressions:

```
(let* ((G84 (expt h 2)) (G85 (f t xt)) (G87 (* -1 h))
(G88 (+ G87 t)) (G89 (f G88 xt-h)) (G91 (* -2 h))
(G92 (+ G91 t)) (G93 (f G92 xt-2h)))
(* 2 G84 G85)
(* -1/4 G84 G89)
(* 1/6 G84 G93)
(* 13/12 G84
(f (+ h t))
(* (+ 13/12 G84 G85))
(* -1/6 G84 G89))
(* 1/12 G84 G93)
(* 2 xt)
(* -1 xt-h)))
(* 3 xt)
(* -2 xt-h))
```

Here we clearly see that there are only four distinct calls to f. Though each integration step in the basic integrator makes three calls to f, the two steps overlap on two intermediate calls. While this is obvious for such a simple example, we see how symbolic evaluation might in understanding a numerical computation.