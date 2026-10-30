# **Example 6.12. Hospital Births Redux.**

Revisit Example 6.10 with an additional predictor: the type of hospital, rural (0) or urban (1). The new data appears in Table 6.13.

**TABLE 6.13: Total Births vs. Caesarean Surgeries and Hospital Type**

|  | 3246 | 2750 | 2507 | 2371 | 1904 | 1501 | 1272 | 1080 | 1027 | 970 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **Total** |  |  |  |  |  |  |  |  |  |  |
| **Special** | 26 | 24 | 21 | 21 | 20 | 20 | 19 | 18 | 18 | 17 |
| **Type** | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 |

|  | 739 | 679 | 502 | 236 | 357 | 309 | 192 | 138 | 100 | 95 |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| **Total** |  |  |  |  |  |  |  |  |  |  |
| **Special** | 17 | 16 | 16 | 16 | 16 | 15 | 14 | 14 | 13 | 13 |
| **Type** | 1 | 1 | 1 | 1 | 1 | 0 | 1 | 0 | 0 | 0 |

The data has been entered as $B$: Total, $C$: Special, and $T$: Type. After loading the *Statistics* package, define the model.

```
```text
> model := exp(a + b·x + c·y);
                 model := e^(a+b·x+c·y)
```
```

Collect the data and use *NonlinearFit* to fit the model.

```
```text
> data := ⟨⟨C⟩ | ⟨T⟩ | ⟨B⟩⟩:

> outops := [leastsquaresfunction, degreesoffreedom, residualmeansquare,
             residualstandarddeviation, residualsumsquares];
  theLabels := ['Degrees of Freedom', ‘Residual Mean Square’,
                ‘Residual Standard Deviation’, ‘Residual Sum of Squares’];

> m := NonlinearFit(model, data, [x,y], output = outops)

> f := unapply(formal(m,1,5),x);
                  f := x → e^0.15397x+1.2047y+3.0022

> Matrix([theLabels, m2..5]);
  LinearAlgebra:-Transpose(%);

  ⎡ ‘Degrees of Freedom’                 17       ⎤
  ⎢ ‘Residual Mean Square’           124410.     ⎥
  ⎢ ‘Residual Standard Deviation’      352.72   ⎥
  ⎣ ‘Residual Sum of Squares’      2.1150 10^6  ⎦
```
```

Finishing the statistical analysis of the model is left as an exercise.