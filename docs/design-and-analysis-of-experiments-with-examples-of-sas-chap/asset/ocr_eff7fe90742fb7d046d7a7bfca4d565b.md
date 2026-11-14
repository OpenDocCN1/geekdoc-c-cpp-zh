will be q x ((-1)^2 + 1^2), where q is the number of times each level of the two-level factor is repeated in the design. Since the sum of squares (((-707107)^2 + 0^2 + .707107^2) = (.4082483^2 + .(-.816497)^2 + .4082483^2) = 1, and there are 24 replicates of each level of the three-level factors in the 72 runs of the design, the diagonal elements of X'X for each contrast of the three-level factors is 24. Since there are 36 replicates of each level of the two-level factors in the 72 runs, the diagonal element of the X'X for each two-level factor and interaction between two-level factors is 72. All of the regression coefficients in the 72-run design can be standardized to have the same variance by dividing each contrast by the square root of the diagonal element of the unstandardized X'X matrix. For example, in the commands below this is illustrated for factors A, B and E and F. This was done for all the coded factor levels and contrasts in the design resulting in an X'X that is equal to a 72 x 72 identity matrix. Recall that no interactions were created between three-level control factors because they are not estimable from the 3^3-1 control factor array.

```
data prodstd; set prod;
A=A1/sqrt(24) ;
Ac=Aq/sqrt(24) ;
B1=B1/sqrt(24) ;
Bq=Bq/sqrt(24) ;
E=E/sqrt(72) ;
F=XF/sqrt(72) ;
EF=EF/sqrt(72) ;
A1E=A1XE/sqrt(24) ;
AqE=AqXE/sqrt(24) ;
A1F=A1XF/sqrt(24) ;
AqF=AqXF/sqrt(24) ;
B1E=B1XE/sqrt(24) ;
BqE=BqXE/sqrt(24) ;
B1F=B1XF/sqrt(24) ;
BqF=BqXF/sqrt(24) ;
E1E=E1XE/sqrt(24) ;
EqE=EqXE/sqrt(24) ;
B1E=B1XE/sqrt(24) ;
BqF=BqXF/sqrt(24) ;
BqEF=BqXEF/sqrt(24) ;
B1EF=B1XEF/sqrt(24) ;
B1EF=B1XEF/sqrt(24) ;
BqEF=BqXEF/sqrt(24) ;
;
run;
proc print data=prodstd; var A1 B1 Bq C1 Cq D1 Dq E F G EF BG TG EFG
A1EF AqE1 A1F AqF A1C AqC A1E AqE A1F AqF A1EF AqEF A1EFG AqEFG
B1E BqE B1F BqF B1G BqG B1EF BqEF B1EG BqEG B1FG BqFG B1EFG BqEFG
C1E CqE C1F CqF C1G CqG C1EF CqEF C1EG CqEG C1FG CqFG C1EFG CqEFG
D1E DqE D1F DqF D1G DqG D1EF DqEF D1EG DqEG D1FG DqFG D1EFG DqEFG
;
```

The estimated regression coefficients were determined by proc glm and output to a file for plotting similar to the examples in Chapters 3 and 6 using the commands shown at the top of the next page.

The normal plot of the 71 regression coefficients (excluding the intercept) was constructed by modifying the code from Section 7.7.5 and the result is shown in Figure 12.11. Examining the plot and the list of coefficients printed