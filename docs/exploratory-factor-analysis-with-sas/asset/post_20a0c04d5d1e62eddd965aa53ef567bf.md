
Note: (a) unrotated factor matrix; (b) pattern matrix; (c) reference structure matrix; and (d) structure matrix.

## Which Method?

### Orthogonal vs Oblique

Orthogonal and oblique rotations will produce virtually identical solutions in the case where factors are perfectly uncorrelated. As the correlation between latent variables diverges from r = 0.00, the oblique solution will produce increasingly cleaner rotated factor patterns.

Using the following syntax, we can try each type of rotation on the engineering data and output a plot of the rotated factor loadings from the pattern matrix. We use ODS to plot the results, and request the plots of the factor loadings by including the PLOTS = LOADINGS option on the FACTOR statement.

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

Figure 4.3 on page 71 presents the rotated factor loading plots for the engineering data using each of the methods summarized earlier in the chapter. The two uppermost plots represent the oblique methods, but the remaining represent the orthogonal methods. Notice that the factor loadings in the oblique plots cluster around the axes. In contrast, the factor loadings in the orthogonal plots tend to cluster around a point slightly away from the axes.

This is because these factors are modestly correlated, but the orthogonal mandate to maintain a 90° angle between axes means that the centroids of the clusters cannot move closer to the axis lines.

In this case, the difference between the oblique and orthogonal methods is not great, but it is noticeable. This is a small but clear example of the higher efficacy of oblique rotations to create clear patterns of results in EFA where the factors are indeed correlated. As far as we are aware, there is no rationale for using orthogonal rotation instead of oblique rotation (except tradition). Furthermore, if factors are uncorrelated, orthogonal and oblique solutions will yield very similar results. Thus, if there is uncertainty about the relationship between the factors, we would recommend using an oblique rotation.

## Figure 4.3 Engineering data using different rotation methods

### Rotation Method: Promax (power = 3)

![](img/29951003f0d11c9d825feb73bff9c8e6_83_0.png)

### Rotation Method: Oblimin (tau = 0)

![](img/29951003f0d11c9d825feb73bff9c8e6_83_1.png)

### Rotation Method: Varimax

![](img/29951003f0d11c9d825feb73bff9c8e6_83_2.png)

### Rotation Method: Quartimax

![](img/29951003f0d11c9d825feb73bff9c8e6_83_3.png)

### Rotation Method: Equamax

![](img/29951003f0d11c9d825feb73bff9c8e6_83_4.png)

## Methods within a Camp

We know that choosing between the orthogonal and oblique rotation camps can make a difference in the final results; but how important is the decision about the specific method after you have chosen your camp? Out of the orthogonal methods, varimax rotation is the most commonly used, and it is the default in many programs. One might conclude it is the orthogonal method of choice. Out of the oblique methods, promax rotation is recommended as the most desirable rotation method (Thompson, 2004). Let's test whether the recommended methods produce different results than their alternatives.

The SDQ contains three scales (parent relations, mathematics, and English) that are minimally correlated (r = 0.15, 0.22, 0.26). Since the theoretical factors are correlated, we should use an oblique rotation method. The two common oblique methods reviewed in this chapter are promax rotation and direct oblimin rotation. The syntax to run these two analyses is presented below. We use maximum likelihood extraction since the method seemed appropriate for this data. (See Chapter 2.)

```
proc factor data = sdqdata nfactors = 3 method = ml rotate = PROMAX;
VAR Math: Par: Eng:;
run;
proc factor data = sdqdata nfactors = 3 method = ml rotate = OBLIMIN;
VAR Math: Par: Eng:;
run;
```

Table 4.2 on page 73 and Table 4.1 on page 73 display the factor loadings for each of these rotation methods and Table 4.3 on page 74 displays the inter-factor correlations. Both oblique rotation methods yield similar results. As expected, the initial unrotated factor loadings for each method are identical. These should be identical because they represent the distribution of the unique variance of the factor loadings before the factors are rotated. These initial factor loadings would be very difficult to interpret as the loadings for a variable tend to be of moderate size across all of the factors. The rotated factor loadings, in both the pattern matrix and structure matrix, are nearly identical. These solutions are what we would expect given the theoretical model that the scale was developed with. The final rotated solutions give us a clear, theoretically consistent factor structure with subscale items aligning as expected.

In this example, the type of oblique rotation used did not make a difference. They resulted in the same clear factor structures and only minor differences in loadings. Many others (for example, Gorsuch, 1983; Kim & Mueller, 1978) have drawn similar conclusions. The methods within the orthogonal and oblique camps tend to produce similar results.

### Table 4.1 Unrotated and rotated factor loadings for SDQ data using promax rotation

| Var: | 1 | 2 | 3 | 1 | 2 | 3 | 1 | 2 | 3 |
|---|---|---|---|---|---|---|---|---|---|
| | Unrotated Factor Loadings | | | Rotated Pattern Matrix | | | Rotated Structure Matrix | | |
| Math1 | .802 | -.373 | .088 | .901 | -.038 | -.037 | .887 | .149 | .087 |
| Math2 | .810 | -.298 | .070 | .862 | .010 | .013 | .866 | .201 | .143 |
| Math3 | .828 | -.301 | .083 | .881 | .001 | .023 | .885 | .198 | .153 |
| Math4 | -.572 | .212 | -.004 | -.600 | -.050 | .021 | -.608 | -.176 | -.080 |
| Par1 | .360 | .349 | -.524 | .004 | .717 | .027 | .164 | .725 | .205 |
| Par2 | -.252 | -.293 | .533 | .058 | -.679 | .049 | -.083 | -.654 | -.111 |
| Par3 | .426 | .370 | -.613 | .030 | .826 | .003 | .211 | .833 | .212 |
| Par4 | -.359 | -.335 | .388 | -.037 | -.583 | -.103 | -.180 | -.616 | -.253 |
| Par5 | .367 | .315 | -.568 | .020 | .748 | -.026 | .179 | .746 | .162 |
| Eng1 | .348 | .634 | .309 | -.004 | .035 | .778 | .118 | .227 | .786 |
| Eng2 | .310 | .636 | .419 | -.015 | -.078 | .840 | .092 | .127 | .818 |
| Eng3 | .406 | .644 | .378 | .052 | -.013 | .844 | .174 | .208 | .848 |
| Eng4 | -.257 | -.552 | -.179 | .059 | -.105 | -.608 | -.053 | -.242 | -.625 |

Note: Primary factor loadings for rotated solutions are highlighted.

### Table 4.2 Unrotated and rotated factor loadings for SDQ data using direct oblimin rotation

| Var: | 1 | 2 | 3 | 1 | 2 | 3 | 1 | 2 | 3 |
|---|---|---|---|---|---|---|---|---|---|
| | Unrotated Factor Loadings | | | Rotated Pattern Matrix | | | Rotated Structure Matrix | | |
| Math1 | .802 | -.373 | .088 | .900 | -.043 | -.030 | .887 | .147 | .079 |
| Math2 | .810 | -.298 | .070 | .863 | .004 | .019 | .866 | .199 | .135 |
| Math3 | .828 | -.301 | .083 | .882 | -.005 | .029 | .884 | .197 | .145 |
| Math4 | -.572 | .212 | -.004 | -.601 | -.046 | .017 | -.608 | -.174 | -.075 |
| Par1 | .360 | .349 | -.524 | .006 | .718 | .022 | .167 | .725 | .213 |
| Par2 | -.252 | -.293 | .533 | .057 | -.681 | .054 | -.086 | -.654 | -.119 |
| Par3 | .426 | .370 | -.613 | .032 | .826 | -.003 | .214 | .833 | .221 |
| Par4 | -.359 | -.335 | .388 | -.040 | -.582 | -.100 | -.182 | -.617 | -.259 |
| Par5 | .367 | .315 | -.568 | .022 | .749 | -.031 | .183 | .746 | .171 |
| Eng1 | .348 | .634 | .309 | .005 | .024 | .779 | .114 | .232 | .786 |
| Eng2 | .310 | .636 | .419 | -.006 | -.089 | .842 | .087 | .133 | .818 |
| Eng3 | .406 | .644 | .378 | .062 | -.025 | .846 | .170 | .213 | .847 |
| Eng4 | -.257 | -.552 | -.179 | .052 | -.097 | -.608 | -.050 | -.247 | -.627 |

Note: Primary factor loadings for rotated solutions are highlighted.

### Table 4.3 Factor correlations

| | Promax Results | | Direct Oblimin Results | |
|---|---|---|---|---|
| | Factor 1 | Factor 2 | Factor 1 | Factor 2 |
| Factor 2 | .218 | | .220 | |
| Factor 3 | .148 | .248 | .134 | .265 |
