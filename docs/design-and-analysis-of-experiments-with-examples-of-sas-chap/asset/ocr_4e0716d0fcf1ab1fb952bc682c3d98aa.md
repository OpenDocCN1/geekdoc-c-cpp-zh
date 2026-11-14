```
data drug;
input trt r1-r5;
dose=0.0; rate=r1; output; dose=0.5; rate=r2; output;
dose=1.0; rate=r3; output; dose=1.5; rate=r4; output;
dose=2.0; rate=r5; output; keep rat dose rate;
datalines;
1 .60 .80 .82 .81 .50
2 .81 .61 .79 .78 .77
;
proc glm;
class rat dose;
model rate=rat dose;
output out=s p=prate r=rrate;
run;
```

$y_{ij} = \mu + b_j + \tau_i + \epsilon_{ij}$. The experimental error, represented by $\epsilon_{ij}$, is the effect of the state of rat $i$ during the run when it received dose $j$. If data were presented without describing the experimental unit and the randomization process, the model could be easily misspecified as $y_{ij} = \mu + \tau_i + \epsilon_{ij}$ resulting in the wrong analysis and conclusions.

The ANOVA table resulting from the correct model specification in SAS appears below. The table of type III sums of squares is not shown because it is identical to the type I sums of squares. The $F$-tests show that there is a significant difference in treatment factor levels.

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| Model | 13 | 2.12866600 | 0.16374354 | 19.61 | <.0001 |
| Error | 36 | 0.30055200 | 0.00834867 | | |
| Corrected Total | 49 | 2.42921800 | | | |

| Source | DF | Type I SS | Mean Square | F Value | Pr > F |
|---|---|---|---|---|---|
| rat | 9 | 1.66845800 | 0.18538422 | 22.21 | <.0001 |
| dose | 4 | 0.46020800 | 0.11505200 | 13.78 | <.0001 |

To interpret the differences in treatment factor levels comparisons of means should be made. Since the factor levels are quantitative, orthogonal polynomial contrasts as described in Section 2.8 are useful. The results of the estimate statement calculating the linear, quadratic, and cubic contrasts are shown at the top of the next page. They show that there is a quadratic trend in lever press rate over the dose of the drug. This trend can be visualized by plotting the means as a function of dose.

The SAS commands below the output table on the next page produce the graph in Figure 4.1. Here the quadratic trend line, produced by the `degree=2` option on the `reg` statement, is added to the plot and shows that the lever press rate increases as a function of dose until it reaches a maximum somewhere between 1.0 and 1.5 milligrams per kilogram of body weight.