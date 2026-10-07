```
input DLT doselevel cohortsize;
datalines;
0 1 3
0 2 3
1 3 3
0 3 3
1 4 3
1 4 3
2 5 3;
run;
```

```
/* Prespecified skeleton:
Four skeletons are used in this example,
each column corresponds to a skeleton.
*/
data skeleton skeleton;
input p1 p2 p3 p4;
datalines;
0.02 0.01 0.10 0.20
0.08 0.05 0.20 0.30
0.12 0.14 0.30 0.40
0.20 0.22 0.40 0.50
0.30 0.26 0.50 0.65
;
run;
```

```
/* Prior probability for each skeleton */
data priamodel;
input priormodel;
datalines;
0.25;
0.25;
0.25;
0.25;
run;
%BMACRM(currentdata,skeleton,priormodel,target=0.3,toxstop=0.9);
```

As shown in Figure 5.2 Four Prespecified Skeletons and Estimated Toxicity Probabilities in the BMA-CRM, the four skeletons represent quite different prior opinions on the dose toxicity curve. The BMA-CRM naturally integrates the posterior estimates from the individual CRM under each skeleton. Based on the cumulative data of the first seven treated patients, the estimated toxicity curve is also presented in Figure 5.2, and clearly dose level 4 should be recommended for the next cohort patients.

# Figure 5.2 Four Prespecified Skeletons and Estimated Toxicity Probabilities in the BMA-CRM