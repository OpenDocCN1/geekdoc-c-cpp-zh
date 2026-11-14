by the fact that it was not tasted by panelists 4, 5, 6, 10, 11, and 12 who seem to rate recipes higher. Likewise, the non-centrality factor for the type I sums of squares for treatments (or recipes) will contain block effects as well as treatment effects. The solution to these problems is the same as shown in Section 3.5.3 for analyzing data from factorial designs with an unequal number of replicates per cell. That is, always use the type III sums of squares in SAS proc glm and the least squares means rather than marginal means. The commands to analyze the data in Table 7.1 are shown below.

```
data taste;
   input panelist recipe $ score;
   datalines;
1 A 5
.
.
.
proc glm;
   class panelist recipe;
   model score=recipe panelist;
   lsmeans recipe;
run;
```

The type III F3,9 value for testing recipes was 3.98, which is significant at the alpha = 0.05 significance level. The least squares means produced by proc glm are shown below. In order to detect which recipes differ, the estimate

| recipe | score | LSMEAN |
|---|---|---|
| A | 5.45833333 | |
| B | 6.20833333 | |
| C | 6.83333333 | |
| D | 4.83333333 | |

statements shown below could be added to the proc glm commands above.

```
estimate 'A-B' recipe 1 -1;
estimate 'A-C' recipe 1 0 -1;
estimate 'A-D' recipe 1 0 0 -1;
estimate 'B-C' recipe 0 1 -1;
estimate 'B-D' recipe 0 1 0 -1;
estimate 'C-D' recipe 0 0 1 -1;
```

This results in the output shown on the top of the next page. There it can be seen that the category scale score for recipe C is significantly higher than the score for recipe D at the alpha = 0.05 level, but that no other differences are significant. Another thing that should be noticed in the output is the fact that the standard error of the differences in means (shown in the third column) is