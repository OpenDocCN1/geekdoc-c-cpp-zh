# Display 8.43 Generating a Monte Carlo estimate of P(0<Z<1.645)

```
data area_est;
retain n_under 0;                * initialize counter - aside: n_under=0 - also works;
seed1 = 98765;                  * seed specified;
call streaminit(seed1);

const = 1/sqrt(2*arcos(-1));    * bring constant calc. outside loop;
n_pts = 4000;
zmul t = 1.96;                  * 95% Confidence interval requested;
Area_rectangle = 1.645*.400;

do ii = 1 to n_pts;             * REPEAT { . . . ;
/* generate data [x, f(x)] in a rectangle containing the
                                   f(x) = density for N(0,1) */
x = 1.645*RAND('uniform');
y = 0.400*RAND('uniform');

/* determine proportion of points that lie below f(x) */
iunder = (y<= const*exp(-x*x/2) );
n_under = n_under + iunder;
p_est = n_under/ii;

/* derive the area estimate, SE and CI  */
AUC_hat = Area_Rectangle * p_est;
SE_AUC_hat = Area_Rectangle * sqrt(p_est * (1-p_est) / n_pts);
LCL = AUC_hat - zmult * SE_AUC_hat;
UCL = AUC_hat + zmult * SE_AUC_hat;

output;
end;                            * . . . };

/* write out the results */
put "Area est. = " AUC_hat;
put "(SE = " SE_AUC_hat ")";
put "CI: [" LCL "," UCL "]";
run;
```

The estimated integral and associated pointwise CIs are extracted from the SAS log and reproduced:

```
Area est. = 0.4522105
(SE = 0.004823385 )
CI: [0.4427566653 ,0.4616643347 ]
```

The estimate of P(0<Z<1.645) is 0.452 (95% CI: 0.442, 0.462). You knew the answer was 0.45. It is interesting to see how the estimated integral and associated pointwise CIs changed as the number of randomly generated points increased.

As a final observation, code to generate a plot of the estimated area versus the number of simulated points is included. And, code to generate a plot of the generated points identified with a different symbol depending on whether the point is below or above the