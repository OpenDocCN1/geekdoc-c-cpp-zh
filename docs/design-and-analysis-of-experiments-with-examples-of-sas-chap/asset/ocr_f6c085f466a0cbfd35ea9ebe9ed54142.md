```
proc glm;
class treat;
model yield=treat;
estimate 'fertilizer effect' treat 1 -.33333 -.33333 -.33333;
estimate 'plowed vs broadcast' treat 0 1 -1 0;
estimate 'January vs April' treat 0 0 1 -1;
means treat/dunnett('A');
run;
```

| Parameter | Estimate | Standard Error | t Value | Pr > |t| |
|---|---|---|---|---|
| fertilizer effect | -8.80001200 | 0.82520231 | -10.66 | < .0001 |
| plowed vs broadcast | -3.80000000 | 0.97518951 | -3.90 | 0.0016 |
| January vs April | 0.10000000 | 0.91941749 | 0.11 | 0.9149 |

The P-values in the column labeled Pr > |t|, in the above output, can be interpreted the same way the P-values for the F-statistic were interpreted, and we can see that: (1) artificial fertilizers enhance yield, (2) broadcast application results in higher yields than plowed application, and (3) there is no significant difference in yield between April and January application time.

When factor levels are quantitative, such as the rise time in the bread dough rise experiment, preplanned comparisons often involve looking for the significance of linear or higher order polynomial trends in the response. Contrast coefficients, c_i, for testing orthogonal polynomial trends, can be obtained from SAS proc iml orpolf function. The required inputs for this function are a vector containing the levels of a quantitative factor and the degree of polynomial desired. The result is an orthogonal matrix with the contrast coefficients desired beginning in the second column. For example, for the bread dough rise experiment the commands

```
proc iml;
t={35 40 45};
C=orpol(t);
print C;
quit;
```

produce the result

| C |
|---|
| 0.5773503 -0.707107 0.4082483 |
| 0.5773503 0 -0.816497 |
| 0.5773503 0.7071068 0.4082483 |

The estimate commands in the following call to proc glm take the second and third columns as the coefficients for the linear and quadratic polynomials.

```
proc glm data=bread;
class time;
model height=time;
estimate 'Linear Trend' time -.707107 0 .707107;
estimate 'Quadratic Trend' time .4082483 -.816497 .4082483;
run;
```