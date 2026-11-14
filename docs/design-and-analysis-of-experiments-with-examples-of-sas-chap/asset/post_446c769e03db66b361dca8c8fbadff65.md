
However, this leaves a dilemma. The MSE in the traditional ANOVA and the denominator for the F-tests for treatment effect and the block by treatment interaction is based on the variability of experimental units within the same treatment and block (in this case golfer). If the interaction between block (golfer) and treatment factor (tee height) were significant, its interpretation would imply that the optimal tee height could be different for different golfers. The golfers in the study were just a sample of golfers, and if the optimal tee height were different for them, there would be no way to recommend an optimal tee height for all readers of the Golf Magazine article. To make a general recommendation, the treatment factor should be tested using the block by treatment interaction mean square as the denominator of the F-test (another justification for using the block by treatment interaction as the denominator of the F-test for treatment effect will be given in Chapter 5, Section 8). An F-test for treatments constructed in this way is not made automatically in proc glm, but can be specified using the test statement as shown in the SAS commands below where id represents block or golfer id.

```
data rcb;
input id teeht cdistance;
datalines;
1 142
.
.
etc.
;
proc glm data=rcb;
class id teeht;
model cdistance=id teeht id*teeht;
test h=teeht e=id*teeht;
lsmeans teeht/pdiff adjust=tukey e=id*teeht;
run;
```

The h=teeht and e=id*teeht in the test statement specify the hypothesis to be H0 : τ1 = τ2 = τ3 and the error term to be brj . The e=id*teeht in the lsmeans statement also specifies the error term to be brj . The results of this analysis are shown on the next page. The table of type I sums of squares was left out since it was identical to the type III sums of squares.

It can be seen that the tee height is significant at the α = 0.0124 level. This is much different than the incorrect F-test in the table of type III sums of squares. There the tee height effect is significant at α < 0.0001 level. Sometimes the F-test for treatments may be significant in the type III table but insignificant in the result of the test statement. In that case, the result of the test statement should be used if you want to generalize conclusions.

Sometimes there is a more powerful test of treatment effects than can be obtained using the test statement to create F-test. If the block by treatment interaction is insignificant, the additive model yijk = μ + bi + τj + ϵijk can be fit to the data and the default F-test for treatments will use an MSE term that is a pooled or weighted average of the interaction and error term from model (4.8). If the interaction is negligible, the interaction mean square

| Source | DF | Sum of Squares | Mean Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Model | 26 | 128821.4813 | 4954.6724 | 72.90 | < .0001 |
| Error | 108 | 7340.7520 | 67.9699 | | |
| Corrected Total | 134 | 136162.2333 | | | |

| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| ID | 8 | 124741.4493 | 15592.6812 | 229.41 | < .0001 |
| TEEHT | 2 | 1723.9320 | 861.9660 | 12.68 | < .0001 |
| ID*TEEHT | 16 | 2356.1000 | 147.2563 | 2.17 | 0.0102 |

### Tests of Hypotheses Using the Type III MS for ID*TEEHT as an Error Term

| Source | DF | Type III SS | Mean Square | F Value | Pr > F |
| :--- | :--- | :--- | :--- | :--- | :--- |
| TEEHT | 2 | 1723.932000 | 861.966000 | 5.85 | 0.0124 |

is estimating the same experimental error as the error mean square. In that case, pooling these two mean squares increases the degrees of freedom for the error term and increases the power or sensitivity of the F-test for treatment effects. Normally the preliminary F-test of the interaction, which is used to decide whether to fit the additive model or not, is conducted at a higher significance level like \(\alpha = 0.25\). If the interaction is significant at the \(\alpha = 0.25\) level, use the `test` statement to create the appropriate F-test for treatment effects. If the interaction is not significant at \(\alpha = 0.25\), fit the additive model and use the F-test from the type I or type III table of sums of squares. This procedure is called the "Pool or not to Pool" procedure.

For the golf experiment, the interaction sum of squares is significant at the \(\alpha = 0.0102 < 0.25\) level, and thus the additive model should not be fit, and there is no more powerful F-test for treatments than the one that can be made using the `test` statement.

To interpret the meaning of the significant treatment effect in the golf experiment, the `lsmeans teeht/diff adjust=tukey e=id*teeht;` statement was used. This results in the table of means and the Tukey pairwise comparisons of means shown on the next page. The `e=id*teeht` option specifies the error term to be the means square for block by treatment interaction.

The least squares means show the average driving distance for the tee height = 1 (entire ball below crown) is 171.45 yards. It is significantly less than the average driving distance (177.8 yds.) for tee height = 3 (bottom of ball at top of club-face) at the \(\alpha = 0.0125\) level and marginally significantly less than the distance (179.8 yds.) for tee height = 2 (half the ball above the crown). The average distance for tee heights 2 and 3 were not significantly different \(\alpha = 0.7192\). Therefore the recommendation to readers of the article was to tee their golf ball up so that at least half the ball is above the crown of the driver club-face in order to maximize their driving distance.

### Least Squares Means
Adjustment for Multiple Comparisons: Tukey
Standard Errors and Probabilities Calculated Using the Type III MS for ID*TEEHT as an Error Term

| TEEHGT | LSMEAN | Number |
|---|---|---|
| 1 | 171.537778 | 1 |
| 2 | 177.833778 | 2 |
| 3 | 179.837778 | 3 |

### Least Squares Means for effect TEEHGT
Pr > |t| for H0: LSMEAN(i)=LSMEAN(j)
Dependent Variable: CDISTANCE

| i/j | 1 | 2 | 3 |
|---|---|---|---|
| 1 | 0.0590 | 0.0125 | |
| 2 | 0.0590 | | 0.7192 |
| 3 | 0.0125 | 0.7192 | |

## 4.8 Two Block Factors LSD

It was first shown in agricultural experiments (Fisher, 1935) that the process of grouping experimental plots into homogeneous blocks might profitably be duplicated. For example, on the left side of Figure 4.3 we see a representation of a randomized block design RCB laid out in a field. In this design, one field, roughly square in shape, is divided into four rectangular blocks. Each block is further divided into four plots and the treatment levels (A, B, C, D) are randomly assigned to one plot within each block. In the figure the random assignment within the block is represented by each letter only appearing once in each row that represents a block. If there is a fertility gradient running from top to bottom in this field, the plots within a block will be more alike in fertility than plots in different blocks or rows, and the randomized block design would work well to reduce the variance of experimental errors within a block. If there were no clear gradient in the field, but adjacent plots tended to be

### Figure 4.3 Comparison of RCB and Latin Square Designs

| Block | RCB | Latin Square |
|---|---|---|
| 1 | B C D A | B D C A |
| 2 | A D C B | D C A B |
| 3 | B D A C | C A B D |
| 4 | C B A D | A B D C |

more alike than plots at different ends of the same block, a design like the one shown on the right side of Figure 4.3 assigns each treatment level only once to each row and once to each column. In that way, the variability from column to column can also be removed from the error sums of squares, further increasing the sensitivity for detecting treatment effects. The design shown on the right side of Figure 4.3 is called a Latin square design or LSD, and it is blocked both horizontally and vertically. The restriction with a LSD is that the number of row blocks equals the number of column blocks, which equals the number of levels of the treatment factor. This restriction will be relaxed in Chapter 7, where more general row-column blocking schemes will be discussed.

The model for a LSD is written

```
y_{ijk} = \mu + r_i + c_j + \tau_k + \epsilon_{ijk} \quad (4.9)
```

where \( r_i \) represents the row blocking factor, \( c_j \) represents the column blocking factor, and \( \tau_k \) represents the treatment factor. Like model (4.1) for the RCB design, no interactions are included in the model so that any differences in treatment factor levels can be generalized over rows and columns.

Latin square designs can be used whenever there are two independent blocking factors that can be used to group experimental units. For example, if an experiment were being conducted to determine the effect of tread design on the wear life of automobile tires, the experimental unit would be a wheel on a car and the treatment factor would be the tread design of the tire mounted on that wheel. It would make sense to block the experimental units by type of automobile, since tires may wear faster on heavier cars than they do on lighter cars. It would also make sense to block by position of the tire on a car since front right tires wear at a different rate than left rear tires, etc. These are independent blocking factors because all four wheel positions exist on any type car. To use a LSD, the number of tread types compared and the number of car types used in the study must be four in order to equal the number of wheel positions on a car. The row blocking factor in the Latin square would represent the type of car, with four alternatives ranging over the class of cars to which the experimenter would like to make inference. The column blocking factor would represent the position of a tire on the car (FL, FR, RL, RR), and the treatment factor would represent the four different tread designs being tested.

### 4.8.1 Creating and Randomizing Latin Square Designs

Latin square designs are easy to create by cyclically rotating the letters or symbols used to represent the treatment factor levels. For example, for a 5 x 5 Latin square, let the letters A, B, C, D, E, represent the levels of the treatment factor. Then the design is created as:
