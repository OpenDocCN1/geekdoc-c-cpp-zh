*Do not call `sqrt` with a negative argument. For industrial-strength code, always check that the arguments you pass to math functions are valid.*

Function arguments may be constants, variables or more complex expressions. If `c = 13.0`, `d = 3.0` and `f = 4.0`, then the statement

```
```cpp
cout << sqrt(c + d * f) << endl;
```
```

displays the square root of `13.0 + 3.0 * 4.0 = 25.0`—namely, `5.0`. Some math library functions are summarized in **Fig. 6.2**. In the figure, the variables `x` and `y` are of type `double`.

# Fig. 6.2 Math library functions.

| Function | Description | Example |
|---|---|---|
| `ceil(x)` | rounds *x* to the smallest integer not less than *x* | `ceil(9.2)` is `10.0` |
|  |  | `ceil(-9.8)` is `-9.0` |
| `cos(x)` | trigonometric cosine of *x* (*x* in radians) | `cos(0.0)` is `1.0` |
| `exp(x)` | exponential function *e*<sup>*x*</sup> | `exp(1.0)` is `2.718282` |
|  |  | `exp(2.0)` is |