
## Exploring Multiple Solutions

Not all scales have a theoretically clear factor structure at the onset of EFA. In addition, sometimes the extraction criteria contradict the proposed structure. In these cases, we need to explore multiple solutions. The GDS data fit this mold. After we reviewed the extraction criteria in Chapter 3, four different factor solutions were proposed: a one-factor, a three-factor, a five-factor, and an eight-factor solution. As a result, we are going to have to experiment and explore more than in previous examples. Let us remember that we want to favor parsimonious solutions. Also, because all proposed subscales relate to depression in some way, they should be correlated. We will therefore use an oblique rotation (direct oblimin) while exploring. As discussed in Chapter 2, the unweighted least squares (ULS) extraction method will be used for this non-normal data.

Before we get started, there are two useful options in the PROC FACTOR statement that can help us interpret the multifactor results that we are about to see: FUZZ and REORDER. The FUZZ option suppresses small loadings from being printed in the various factor loading matrices. This helps us identify moderate to large factor loading and subsequent factor structures easily and immediately. To use this option, we must specify the maximum factor loading we would like to suppress by setting FUZZ equal to that value (for example, FUZZ=.3). The REORDER option is used to reorder the rows in the matrix according to their factor loadings. By default, the variables in the first column of the factor loading matrices are presented in the same order in which they were put into the model on the VAR statement. This option allows these rows to be reordered and grouped for easier interpretation. The following syntax can be used to run the one-, five-, and eight-factor models. We will hold off from running the three-factor model and let you explore that on your own.

Please note, the variables in the previous examples were put into their respective models according to the theoretical factor each variable was associated with; thus, the REORDER option would not have provided substantially different factor loading matrices from what was presented.

```sas
**One-Factor;
*Note: no rotation is needed because only one factor is being extracted;
proc factor data=marsdata nfactors=1 method=ULS;
VAR GDS:;
run;
```

```sas
**Five-Factor;
proc factor data=marsdata nfactors=5 method=ULS rotate=OBLIMIN
fuzz=.3 reorder;
VAR GDS:;
run;
```

```sas
**Eight-Factor;
*Note: need to increase default max iterations to 60 using maxiter option
for a solution to be identified;
proc factor data=marsdata nfactors=8 method=ULS rotate=OBLIMIN
fuzz=.3 reorder;
VAR GDS:;
run;
```

Table 4.4 on page 76 presents the results for the one-factor and five-factor models. The item stems are reported in this table because we will need to do a little interpretation of the factors for ourselves. The one-factor solution was defensible based on the single large eigenvalue and MAP analysis found in Chapter 3. This single factor accounts for 23.80% of the variance and communalities that ranged from 0.05 to 0.47, which is not a strong result. As you can see, many loadings are low, and even the highest loadings are in the .60 to .70 range. This is likely due to the poor measurement (0, 1 only). If we select this one-factor solution, the final scale will likely represent a unidimensional latent depression construct.

## Table 4.4 Pattern loadings for GDS data with one factor and five factors extracted

| Variable and Item Stem | 1-Factor 1 | 5-Factor 1 | 5-Factor 2 | 5-Factor 3 | 5-Factor 4 | 5-Factor 5 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| GDS09: Do you feel happy most of the time? | .607 | .766 | | | | |
| GDS07: Are you in good spirits most of the time? | .473 | .666 | | | | |
| GDS15: Do you think it is wonderful to be alive now? | .467 | .631 | | | | |
| GDS01: Are you basically satisfied with your life? | .591 | .464 | | | | |
| GDS05: Are you hopeful about the future? | .512 | .445 | | | | |
| GDS27: Do you enjoy getting up in the morning? | .376 | .346 | | | | |
| GDS08: Are you afraid that something bad is going to happen to you? | .401 | | | | | |
| GDS22: Do you feel that your situation is hopeless? | .552 | | .643 | | | |
| GDS03: Do you feel that your life is empty? | .629 | | .460 | | | |
| GDS17: Do you feel pretty worthless the way you are now? | .661 | | .408 | .372 | | |
| GDS23: Do you think that most people are better off than you are? | .418 | | .396 | | | |
| GDS25: Do you frequently feel like crying? | .578 | | .392 | | | |
| GDS10: Do you often feel helpless? | .618 | | .365 | | | |
| GDS18: Do you worry a lot about the past? | .421 | | .309 | | | |
| GDS21: Do you feel full of energy? | .448 | | | .499 | | |
| GDS20: Is it hard for you to get started on new projects? | .429 | | | .441 | | |
| GDS19: Do you find life very exciting? | .566 | .302 | | .439 | | |
| GDS02: Have you dropped many of your activities and interests? | .406 | | | .413 | | |
| GDS28: Do you prefer to avoid social gatherings? | .432 | | | .412 | | |
| GDS12: Do you prefer to stay at home, rather than going out and doing new things? | .356 | | | .400 | | |
| GDS29: Is it easy for you to make decisions? | .327 | | | | | |
| GDS04: Do you often get bored? | .534 | | | | .677 | |
| GDS11: Do you often get restlessness and fidgety? | .429 | | | | .495 | |
| GDS24: Do you frequently get upset over little things? | .400 | | | | .443 | |
| GDS16: Do you often feel downhearted and blue? | .684 | | | | .399 | |
| GDS13: Do you frequently worry about the future? | .418 | | | | | |
| GDS14: Do you feel you have more problems with memory than most? | .231 | | | | | .592 |
| GDS26: Do you have trouble concentrating? | .460 | | | | | .526 |
| GDS30: Is your mind as clear as it used to be? | .331 | | | | | .501 |
| GDS06: Are you bothered by thoughts you can't get out of your head? | .524 | | | .336 | | .336 |

Note: ULS extraction was used. Recall that one-factor solutions are not rotated, so the loadings might seem suboptimal. Only the pattern matrix is reported for the five-factor solution to conserve space.

This is calculated from the results in the table entitled “Variance Explained by Each Factor.” The explained variance is converted to a proportion by dividing it by the total variance (equal to the number of items in the model; in this case that is 30) and then multiplying by 100.

When the theoretically supported five factors are extracted, 37.03% of the variance is accounted for, and the communalities range from 0.15 to 0.64—better but not impressive. A few of the items do not have loadings greater than .3 on one of the factors (items 8, 29, and 13). Thus, if we were to proceed with this model we might consider dropping these items from the scale as they do not contribute to the desired constructs. Factors 1, 2, and 5 make some sense. The first factor could be interpreted as a construct of positivity, the second could be depression, and the fifth could be clarity of mind. However, we cannot find a conceptual difference between factors 3 and 4. In addition, the items loading on the factors do not match the theoretical framework and thus do not (to us) make sense. If it does not make sense in an alternative way, we would be reluctant to put it forward as the best model.

As you can see in Table 4.5 on page 79, the next possibility is an eight-factor solution, which was indicated not only by the Kaiser Criterion (eigenvalues greater than 1.0) but also by parallel analysis. With eight factors extracted, the model accounted for 43.68% of the variance, and communalities ranged from 0.17 to 0.82, slightly better than the five-factor model. This model includes a reduced version of the positivity construct (still factor 1), depression construct (now factor 3), and the clarity of mind construct (still factor 5); and most of the remaining factors do not make sense to us. Thus, these results are not any more interpretable. For the sake of space, we will leave the three-factor model to you to examine. It might be conceptually intriguing.

## Table 4.5 Eight-factor solution for GDS data

| Var: | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| GDS09 | .763 | | | | | | | |
| GDS07 | .705 | | | | | | | |
| GDS15 | .567 | | | | | | | |
| GDS05 | .379 | | | | | | | |
| GDS12 | | .983 | | | | | | |
| GDS28 | | .468 | | | | | | |
| GDS22 | | | .556 | | | | | |
| GDS25 | | | .458 | | | | | |
| GDS17 | | | .395 | | | | | .307 |
| GDS23 | | | .349 | | | | | |
| GDS16 | | | .315 | .325 | | | | |
| GDS10 | | | | | | | | |
| GDS04 | | | | .703 | | | | |
| GDS11 | | | | .555 | | | | |
| GDS24 | | | | .318 | | | | |
