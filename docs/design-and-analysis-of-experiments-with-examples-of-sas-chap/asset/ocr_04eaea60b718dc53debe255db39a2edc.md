# Figure 11.24 ADX Contour Plot in Restricted Region

![](bbox=[0.25, 0.1, 0.75, 0.45])

# Figure 11.25 ADX Response Trace Plot

![](bbox=[0.15, 0.55, 0.85, 0.72])

```
data polvoron;
input x1 x2 x3 y;
datalines;
.8 .15 .05 5.33
.4 .05 .05 5.87
;
proc glm;
model y=x1 x2 x1*x2 x1*x3 x2*x3 x1*x2*x3/p solution;
estimate 'beta1' intercept 1 x1 1;
estimate 'beta2' intercept 1 x2 1;
estimate 'beta3' intercept 1;
run;
```