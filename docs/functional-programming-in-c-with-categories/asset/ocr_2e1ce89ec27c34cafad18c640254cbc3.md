+   3. Finally, we use another implication elimination →E which is the application g(f(x, y)).

![](bbox=[0.42, 0.14, 0.62, 0.18])

We proved in a strong deductive sense that by having as Hypotheses the T, U, T∧U→R1, R1→R2 we can get a R2.

# Type Theory

# Inhabited Types

If we had some other function g for example R1→T, there would not be any way to prove R2. The meaning of this in programming terms, is that there would not be any way to have a valid Compose of the following type without Compiler Errors:

```
Func<T, U, R2> Compose<T, U, R1, R2>(Func<T, U, R1> f, Func<R1, T> g) =>{ }
```

In type theory we say that the type ((T×U) → R1) →(R1 → T) →((T×U) → R2) is not inhabited. Of course, it might hold if we would add some additional “facts” about T and R2 for example that T is subtype R2. By adding this constraint where T:R2 this is typable:

```
Func<T, U, R2> Compose1<T, U, R1, R2>(Func<T, U, R1> f, Func<R1, T> g)
where T:R2 =>
(x, y) => g(f(x, y));
```

![](bbox=[0.26, 0.51, 0.42, 0.54])

In the case of simply typed lambda calculus, a type has an inhabitant if and only if its corresponding proposition is a tautology in Logic.

Another composition could be to pre-compose on the first argument some other function.

![](bbox=[0.27, 0.73, 0.76, 0.78])

```
Func<T0, U, R> PreCompose<T, U, R, T0>(Func<T, U, R> f, Func<T0, T> g) =>
(T0 x, U y) => f(g(x), y);
```