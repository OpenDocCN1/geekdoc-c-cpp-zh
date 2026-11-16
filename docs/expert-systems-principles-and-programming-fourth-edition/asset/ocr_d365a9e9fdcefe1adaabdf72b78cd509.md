Let's now define a fuzzy restriction R1(x). For example, the fuzzy set HEAVY could be defined as:

```
R1(x) = HEAVY = .6/140 + .8/150 + 1/160
```

The compositional rule of inference defines the fuzzy restriction on y values as:

```
R3(y) = R1(x) o R2(x,y)
```

where the composition operator, o, is the max-min operation:

```
max min (u1(x), u2(x,y))
x
```

Another way of viewing R3(y) is by interpreting it as the solution of the relational equations:

```
R1(x)
R2(x,y)
```

for R3(y). That is, given the fuzzy restriction of x and the fuzzy restriction on x and y, a fuzzy restriction on y can be deduced. Deductions like this comprise the calculus of fuzzy restrictions, which is the basis of approximate reasoning.

Using these definitions, R3(y) can be calculated as follows:

```
R3(y) = R1(x) o R2(x,y)
```

```
R3(y) = [0.0 0.0 0.6 0.8 1.0] o
```

| 1.0 | 0.7 | 0.4 | 0.2 | 0.0 |
|---|---|---|---|---|
| 0.7 | 1.0 | 0.6 | 0.5 | 0.2 |
| 0.4 | 0.6 | 1.0 | 0.8 | 0.5 |
| 0.2 | 0.5 | 0.8 | 1.0 | 0.8 |
| 0.0 | 0.2 | 0.5 | 0.8 | 1.0 |

where R1(x) is represented as a row vector. The nonzero elements of R3(y) are calculated as follows:

```
R3(120) = max min([.6,.4], [.8,.2])
= max(.4,.2) = .4
R3(130) = max min([.6,.6], [.8,.5], [1,.2])
= max(.6,.5,.2) = .6
```