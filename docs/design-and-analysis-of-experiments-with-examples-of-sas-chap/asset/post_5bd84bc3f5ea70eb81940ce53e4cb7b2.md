
x. For the compartment model in Equation (10.7)

\(\frac{\partial f}{\partial \gamma_0} = e^{-k_1(x-t_0)} - e^{-k_2(x-t_0)}\)
\(\frac{\partial f}{\partial k_1} = -\gamma_0(x-t_0)e^{-k_1(x-t_0)}\)
\(\frac{\partial f}{\partial k_2} = -\gamma_0(x-t_0)e^{-k_2(x-t_0)}\)
\(\frac{\partial f}{\partial t_0} = \gamma_0 k_1 e^{-k_1(x-t_0)} - \gamma_0 k_2 e^{-k_2(x-t_0)}\)

The strategy is to create a grid of candidates in the independent variable _x_, calculate the values of the four partial derivatives using initial guesses of the parameter values at each candidate point, and then use proc optex to select a D-optimal subset of the grid. In the SAS code below the initial parameter estimates \(\gamma_0^0 = 2.65\), \(k_1^0 = .15\), \(k_2^0 = .72\) and \(t_0^0 = 0.41\) were used.

```
*Create a candidate grid in partial derivatives;
data grid;
k1=.15; k2=.72; gamma0=2.65; t0=.41;
do x=1 to 25 by 1;
fdk1=gamma0*exp(-k1*(x-t0))-(x-t0);
fdk2=gamma0*exp(-k2*(x-t0))*(x-t0);
fdkgamma=exp(-k1*(x-t0))-exp(-k2*(x-t0));
fdt0=gamma0*exp(-k1*(x-t0))*k1 - gamma0*exp(-k2*(x-t0))*k2;
output;
end;
run;
*Create D-optimal p point Design;
proc optex data=grid coding=orth;
model fdk1 fdk2 fdkgamma fdt0/noint;
generate n=4;
id x;
output out=desn1; run;
proc print data=desn1; run;
```

Since there are _p_ = 4 parameters in the model, proc optex will always generate at most _p_ = 4 distinct design points, therefore the option n=4 is used on the generate statement to eliminate any replicates in the file desn1. An experimenter can then replicate each design point as many times as necessary to get an estimate of experimental error. The code above results in the four distinct times for taking blood samples (1, 2, 5 and 13), and due to the form of the model and initial guesses of the parameters these points are far from equally spaced.

As stated by Bates and Watts (2007), the efficiency of the design for the nonlinear model will depend on the stage at which a researcher is in the investigation. If the form of the equation is known but not the parameter values, the design created by proc optex will be called an initial design. After the data is collected from an initial design and the model is fit, the parameter estimates will be an improvement on the initial estimates. Therefore, the initial guesses of the parameter values can be replaced by the estimates and the initial design can be augmented with p = 4 additional design points using the augment=desn1 option on the generate statement similar to the example shown in Section 6.5.2.

## 10.6 Fitting the Response Surface Model with SAS

This section will describe how to fit a response surface model using SAS proc rsreg and a nonlinear mechanistic model using SAS proc nlin.

### 10.6.1 Fitting a Linear Model and Checking for Curvature

If the factorial portion of a central composite design along with center points is completed in an initial block of experiments as described in Section 10.3.1, the linear model (10.6) should be fit to the data and checked for adequacy. If the linear model is adequate, the axial points and additional center points in the residual composite design will not be necessary. To check for adequacy the residual sums of squares from model 10.6 should be partitioned into the portion due to pure replication and the portion due to quadratic departure from the model. This can be easily done using SAS proc rsreg. For example, the SAS code below reads in the first eleven data points from Table 10.1, and calls proc rsreg for the analysis.

```
data grout1;
input run Wat_Cem BlackL SNF Work;
datalines;
1 0.33 0.12 0.08 109.5
2 0.33 0.12 0.12 120.0
3 0.33 0.18 0.08 110.5
4 0.33 0.18 0.12 124.0
5 0.35 0.12 0.08 117.0
6 0.35 0.12 0.12 130.0
7 0.35 0.18 0.08 121.0
8 0.35 0.18 0.12 131.0
9 0.34 0.15 0.10 117.0
10 0.34 0.15 0.10 117.0
11 0.34 0.15 0.10 115.0
;
proc rsreg data=grout1;
model work=Wat_Cem BlackL SNF;
run;
```

Normally the model 10.6 could be fit using SAS proc glm with the model statement model work=Wat_Cem BlackL SNF Wat_Cem*BlackL Wat_Cem*SNF BlackL*SNF;. This would produce a report where the sums of squares for the corrected total has 10 degrees of freedom, the model has 6 degrees of freedom and the error has 4 degrees of freedom. Since `proc rsreg` was created for fitting the general quadratic model, it is not necessary to define the cross-product terms in the model statement. They are created by default. In addition `proc rsreg` creates quadratic terms. When the axial points are left out of the central composite design, all the quadratic terms become confounded. However, the third table of results produced by `proc rsreg` shows a test of the confounded quadratic terms. The results below show this table that resulted from the `proc rsreg` command above.

| Regression | DF | Type I Sum of Squares | R-Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Linear | 3 | 465.125000 | 0.9137 | 80.31 | 0.0023 |
| Quadratic | 1 | 37.878788 | 0.0744 | 19.62 | 0.0214 |
| Crossproduct | 3 | 0.250000 | 0.0005 | 0.04 | 0.9859 |
| Total Model | 7 | 503.253788 | 0.9886 | 37.24 | 0.0065 |
| Residual | DF | Sum of Squares | Mean Square | | |
| Total Error | 3 | 5.791667 | 1.930556 | | |

The sums of squares for Linear account simultaneously for the three linear terms in the model, and the sums of squares for Crossproduct account simultaneously for the three interaction terms in the model. The sums of squares for Quadratic accounts for the departure from linearity, and the sums of squares for Residual represents the pure error sums of squares due to replicate center points. When fitting model 10.6 with `proc glm` the sums of squares for Quadratic would be combined with the error sums of squares resulting in four degrees of freedom for error. The F-test on the quadratic term is a test of the adequacy of the linear model. Since it is significant at the \(\alpha = 0.05\) level in the above table, it indicates that the quadratic departure from the linear model is significant, and thus the linear model (10.6) is not adequate for representing the first eleven data points in Table 10.1. Therefore, if the experiments shown in Table 10.1 were to be run in two blocks, it would be necessary to run the second block that includes the axial points. This test for adequacy of the linear model can also be made using SAS ADX.

### 10.6.2 Fitting the General Quadratic Model

`proc rsreg` is most useful for fitting the general quadratic model and analyzing the fitted surface. For example, consider fitting the general quadratic model to the trebuchet data in Table 10.3. The commands to read the data and fit the model using `proc rsreg` are shown on the next page.

```
data trebuchet;
input run;
datalines;
1 4 10 2.5 33
2 8 10 2.5 85
...
proc rsreg;
model y=A B C/lackfit;
run;
```

Notice that the uncoded factor levels are read in the statements above. proc rsreg automatically codes and scales the factor levels and prints the coefficients for the model in coded and uncoded factor levels. The first table in the output on the next page shows the values that proc rsreg used to code and scale the factor levels. The second table in the results shows the summary statistics from the fit. The Response mean is simply the average of the response data and the Coefficient of Variation is \(\sigma\) = Root MSE divided by the Response Mean.

The third table of results shows the ANOVA partition shown in the last section. In this example it can be seen that the linear quadratic and cross-product terms in the model are all significant. The error sums of squares are also partitioned into the pure error sums of squares and the lack of fit sums of squares as a result of the lackfit option on the model statement. By doing this, a simple F-test can be made for the adequacy of the quadratic model. For example, the responses at the three center points in Table 10.3 are 88, 91 and 91. Therefore, the pure sums of squares due to replication are:

![](img/878b651cdbe9da3d6d22e64d64b8a54f_419_0.png)

The difference in the total error sums of squares (20.5) and the pure error sums of squares is called the lack of fit sums of squares. An F-test of the lack of fit sums of squares is a test of the adequacy of the quadratic model. In this case it is clearly insignificant, indicating that predictions made from the general quadratic model for this experiment can be considered just as accurate as running additional experiments, as long as no lurking variables change before additional experiments can be run.
