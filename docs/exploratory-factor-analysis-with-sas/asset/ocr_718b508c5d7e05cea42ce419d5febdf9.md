```
for a solution to be identified;
proc factor data=marsdata nfactors=8 method=ULS rotate=OBLIMIN
fuzz=.3 reorder;
VAR GDS.;
run;
```

Table 4.4 on page 76 presents the results for the one-factor and five-factor models. The item stems are reported in this table because we will need to do a little interpretation of the factors for ourselves. The one-factor solution was defensible based on the single large eigenvalue and MAP analysis found in Chapter 3. This single factor accounts for 23.80%1 of the variance and communalities that ranged from 0.05 to 0.47, which is not a strong result. As you can see, many loadings are low, and even the highest loadings are in the .60 to .70 range. This is likely due to the poor measurement (0, 1 only). If we select this one-factor solution, the final scale will likely represent a unidimensional latent depression construct.

# Table 4.4 Pattern loadings for GDS data with one factor and five factors extracted

| Variable and Item Stem | 1-Factor 1 | 5-Factor 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|---|
| GDS09: Do you feel happy most of the time? | .607 | .766 | | | | |
| GDS07: Are you in good spirits most of the time? | .473 | .666 | | | | |
| GDS15: Do you think it is wonderful to be alive now? | .467 | .631 | | | | |
| GDS01: Are you basically satisfied with your life? | .591 | .464 | | | | |
| GDS05: Are you hopeful about the future? | .512 | .445 | | | | |
| GDS27: Do you enjoy getting up in the morning? | .376 | .346 | | | | |
| GDS08: Are you afraid that something bad is going to happen to you? | .401 | | | | | |

1 This is calculated from the results in the table entitled “Variance Explained by Each Factor.” The explained variance is converted to a proportion by dividing it by the total variance (equal to the number of items in the model; in this case that is 30) and then multiplying by 100.