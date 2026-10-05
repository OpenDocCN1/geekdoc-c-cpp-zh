The step procedure is used in the procedure evolve that advances the history by a given number of steps of size h. We explicitly use specialized integer arithmetic here (here the procedures named n:> and n:-) for counting steps. This will allow us to use different types of arithmetic for everything else without affecting counting.\2

```
(define evolver F h make-integrator)
(let ({integrator make-integrator F h})
n  (let ({stepper h integrator})
    (define n:> history n-steps)
      (if (n:> n-steps 0)
        (evolve (step history) (n:- n-steps 1))
        history)))
  evolve))
```

A second-order differential equation like equation 3.1 generally needs two initial conditions to determine a unique trajectory: x(t₀) and x(t₀) are sufficient to get x(t) for all t. The Stormer multistep integrator we are requires three history values, x(t₀), x(t-h), and x(t-2h), to compute the next value x(t+h). So to evolve the trajectory with this integrator we must start with an initial history that has three past values of x.

Consider the very simple differential equation:

> D²x(t) + x(t) = 0

In the form shown in equation 3.1 the right-hand side is:

```
(define F t x (- x))
```

Because all the solutions of this equation are linear combinations of sinusoids, we can get the simple sine function by initializing the history with three values of the sine function:

```
(define numeric-s0
(make-initial-history 0 .01 (sin 0) (sin -.01) (sin -.02)))
```

where the procedure make-initial-history takes the following arguments: