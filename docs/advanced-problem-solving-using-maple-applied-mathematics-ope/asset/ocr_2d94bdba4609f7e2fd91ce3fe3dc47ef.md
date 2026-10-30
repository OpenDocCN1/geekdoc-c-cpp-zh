The desired tolerance has not been achieved—we’re not finished.

```
Newton(x₂);
|x₃ − x₂| < 0.01;

x₃ := 1.290994624
0.000672043 < 0.01
```

We have a result! Checking the second derivative shows that p(1.29) = 13.6 is our maximum (to within 0.01).

Maple’s *Student[Calculus1]* package contains *NewtonsMethod* for finding the roots of a function. To use *NewtonsMethod* to find critical points, all we have to do is replace the function with its first derivative. We illustrate below.

```
with(Student[Calculus1]);

p := x → −2x³ + 10x + 5:
dp := D(p):
NewtonsMethod(dp, x = 1.0);

1.290994449

NewtonsMethod(dp, x = 1.0, output = sequence);

1.0, 1.333333333, 1.291666667, 1.290994624, 1.290994449

NewtonsMethod(dp, x = 0.3, output = plot);
```

![](bbox=[0.291, 0.481, 0.724, 0.735])

From the initial point x₀ = 0.3, at most 5 iteration(s) of Newton’s method for f(x) = −6x² + 10

Try *NewtonsMethod* with *output=animation*.