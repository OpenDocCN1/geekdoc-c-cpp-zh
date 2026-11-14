The quadratic model can be written in the independent factors as shown in Equation (11.15), which is the same as model 10.2,

\( y = \beta_0 + \beta_1 w_1 + \beta_2 w_2 + \beta_{11} w_1^2 + \beta_{22} w_2^2 + \beta_{12} w_1 w_2 + \epsilon, \quad (11.13) \)

and standard regression programs and contour plotting programs like SAS proc gcontour can be used to fit the model and produce contour plots over the simplex experimental region. This fact is illustrated in an example in the appendix of this chapter.

Sometimes the response in a mixture experiment may increase or decrease rapidly as one or more of the mixture components approach their lower boundary. These are called edge effects. Edge effects can cause a lack of fit in first- and second-degree polynomial models. Rather than increasing the order of the polynomial model, Draper and John (1977) suggested including inverse terms in the model, as shown in Equation (11.14), to model edge effects.

\( y = \beta_1 x_1 + \beta_2 x_2 + \beta_3 x_3 + \beta_{-1} x_1^{-1} + \beta_{-2} x_2^{-1} + \beta_{-3} x_3^{-1} + \epsilon \quad (11.14) \)

Including inverse terms when there are edge effects can greatly improve the fit of the model as will be demonstrated in an exercise.

# 11.3 Creating Mixture Designs in SAS

Simplex lattice and simplex centroid designs can be easily created using the SAS macros included in the AUTOCALL library or with the SAS ADX automated system. The example SAS code below uses the macros to first create an SLD{3,2} in three components x1, x2, and x3, and stores it in the file work.sld. The code then creates an SCD in four components and prints the resulting file work.scd.

```
%adxgen
%adxmix
%adxinit
%adxdsd(scd,x1 x2 x3,2)
%adxgen
%adxmix
%adxinit
%adxscd(scd,x1 x2 x3 x4,4)
proc print data=scd; run;
```

The output at the top of the next page shows the simplex-centroid design.