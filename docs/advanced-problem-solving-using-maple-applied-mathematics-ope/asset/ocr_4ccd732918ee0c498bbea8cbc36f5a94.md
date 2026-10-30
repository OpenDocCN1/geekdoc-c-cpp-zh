**TABLE 1.2: Maple Algebraic Functions**

| Command | Operation |
|---|---|
| `abs` | absolute value of real or complex argument |
| `arg` | argument of a complex number |
| `ceil` | least integer ≥ *x* |
| `conjugate` | conjugate of a complex number |
| `exp` | the exponential function: *e*ˣ = exp(*x*) = ∑<sub>k=0</sub><sup>∞</sup> *x*<sup>k</sup>/*k*! |
| `factorial, !` | the factorial function, factorial(*n*) = *n*! |
| `floor` | greatest integer ≤ *x* |
| `ln` | natural logarithm (with base *e* = 2.718...) |
| `log[b]` | logarithm to arbitrary base *b* |
| `log 10` | log to the base 10 |
| `max, min` | maximum/minimum of a list of real numbers |
| `RootOf` | function for expressing roots of algebraic equations |

We illustrate by taking the natural logarithm of our length and weight data.

```
ln_length := map(x → evalf(ln(x)), length_inches);
ln_length := [2.484906650, 2.639057330, 2.525728644, 2.772588722, 3.068052935]

ln_weight := map(x → evalf(ln(x)), weight_oz);
ln_weight := [2.708050201, 3.044522438, 2.302585093, 3.496507561, 3.713572067]
```

Some other functions that are available will be discussed in a later chapter when considering statistical operations that may be performed on columns of data: sums, means, standard deviation, and so forth. Table 1.3 presents a few examples of data transformations, with the Maple commands.

**TABLE 1.3: Examples of Maple Commands in the Worksheet**

| Expression | Typed Command |
|---|---|
| *x*² | `x^2` |
| 2*x*² + 2.5 + 9 | `2*x^2 + 2.5 + x + 9` |
| (*x*² + 2)<sup>0.5</sup> | `(x^2 + 2)^0.5` |