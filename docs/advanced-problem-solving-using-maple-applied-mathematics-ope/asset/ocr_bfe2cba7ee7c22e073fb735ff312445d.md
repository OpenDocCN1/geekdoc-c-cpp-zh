To find the value of $a(72)$ we can either iterate the recurrence with `seq` or use `rsolve` to obtain a formula. Let’s start with iteration. (Remember to either use `restart` or open a new Worksheet to have a fresh Maple environment.) Since this is a simple recurrence, we’ll use a ‘short-cut’ procedure.

```
> a := n → piecewise(n > 0, 0.75 · a(n − 1) + 100, 0);
```

```
$$a := n \mapsto \begin{cases}0.75\,a(n-1)+100 & 0<n\\0 & otherwise\end{cases}$$
```

Asking Maple for $a(72)$ will perform the iterations and display the result.

```
> a(72);
```

```
$$399.999996$$
```

We could see all the iterates by using $\operatorname{seq}(k,a(k)),\ k=0..72$. Let’s attempt to find a formula by using `rsolve`. (Remember to `restart`.)

```
> rsolve({a(n + 1) = 0.75 · a(n) + 100, a(0) = 0}, a(n));
```

```
$$400 - 400\left(\frac{3}{4}\right)^n$$
```

Note that, in this case, Maple returned an exact answer even though we entered decimals.

What is the long-term level of drug in the patient’s bloodstream?

```
> limit(400 − 400 · 0.75^n, n = infinity);
```

```
$$400$$
```

Checking iterates would show that a patient’s bloodstream would have approximately 400 mg of the drug after 24 hours.

It’s time for a plot.

```
> pts := [seq([n, 400 − 400 · 0.75^n], n = 0..48)]:
```