of variance or minimum eigenvalue criteria, so we will be able to confirm our interpretation of one of the criteria with the SAS interpretation. It is always better to have SAS check us if possible!

```
*Using the scree option;
proc factor data = engdata method = PRINIT priors = SMC SCREE;
var EngProbSolv: INTERSTeng: ;
run;

*Using the ODS system;
ods graphics on;
proc factor data = engdata method = PRINIT priors = SMC plots = SCREE;
var EngProbSolv: INTERSTeng: ;
run;
ods graphics off;
```

Both of the PROC FACTOR statements above will produce the following table related to the Kaiser Criterion, minimum eigenvalue, and proportion of variance. Figure 3.1 on page 38 displays the initial eigenvalue estimates produced before the extraction method is used to iteratively converge on a solution. We use the initial estimates because these are generally identical across extraction method.1 In this example, the Kaiser Criterion would tell us to extract two factors because only the first two rows (which represent potential factors to extract) have eigenvalues that are greater than 1. Based on the minimum eigenvalue criteria, we would retain only factors that account for .75 of an eigenvalue or more (i.e., the average eigenvalue or the total extracted variance divided by the number of items: 10.6068/14). This would also have us retain two factors. Finally, the proportion of variance criteria would recommend we retain two factors because 100% of the common variance is explained by two factors. The text at the bottom of the figure tells us that SAS plans to retain two factors based on the proportion of variance criteria.