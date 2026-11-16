Note: (a) unrotated factor matrix; (b) pattern matrix; (c) reference structure matrix; and (d) structure matrix.

# Which Method?

# Orthogonal vs Oblique

Orthogonal and oblique rotations will produce virtually identical solutions in the case where factors are perfectly uncorrelated. As the correlation between latent variables diverges from r = 0.00, the oblique solution will produce increasingly cleaner rotated factor patterns.

Using the following syntax, we can try each type of rotation on the engineering data and output a plot of the rotated factor loadings from the pattern matrix. We use ODS to plot the results, and request the plots of the factor loadings by including the PLOTS = LOADINGS option on the FACTOR statement.

```
```
ods graphics on; width = 4in height = 6in;
proc factor data = engdata nfactors = 2 method = printr priors = SMC
   rotate = VARIMAX plots = loadings ;
   VAR EngProb: INTERESTeng ;
run;
proc factor data = engdata nfactors = 2 method = printr priors = SMC
   rotate = QUARTIMAX plots = loadings ;
   VAR EngProb: INTERESTeng ;
run;
proc factor data = engdata nfactors = 2 method = printr priors = SMC
   rotate = EQUAMAX plots = loadings ;
   VAR EngProb: INTERESTeng ;
run;
proc factor data = engdata nfactors = 2 method = printr priors = SMC
   rotate = PROMAX plots = loadings ;
   VAR EngProb: INTERESTeng ;
run;
proc factor data = engdata nfactors = 2 method = printr priors = SMC
   rotate = OBLIMIN plots = loadings ;
   VAR EngProb: INTERESTeng ;
run;
ods graphics off;
```
```

Figure 4.3 on page 71 presents the rotated factor loading plots for the engineering data using each of the methods summarized earlier in the chapter. The two uppermost plots represent the oblique methods, but the remaining represent the orthogonal methods. Notice that the factor loadings in the oblique plots cluster around the axes. In contrast, the factor loadings in the orthogonal plots tend to cluster around a point slightly away from the axes.