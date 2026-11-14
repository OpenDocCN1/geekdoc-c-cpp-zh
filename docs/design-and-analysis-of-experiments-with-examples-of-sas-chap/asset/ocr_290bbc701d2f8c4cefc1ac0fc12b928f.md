comes non-orthogonal and effects must be estimated by regression, but Wang and Wu have shown that the D-efficiency remains quite high. Usually some type of regression subset selection procedure is used in order to identify the most appropriate model. For the data in Table 6.11, the SAS commands below, create interaction columns and use proc reg to perform an all-subsets regression.

```
data castf; set castf;
*Note Defines Interactions;
AB=A*B; AC=A*C; AD=A*D; AE=A*E; AF=A*F; AG=A*G;
BC=B*C; BD=B*D; BE=B*E; BF=B*F; BG=B*G;
CD=C*D; CE=C*E; CF=C*F; CG=C*G;
DE=D*E; DF=D*F; DG=D*G;
EF=E*F; EG=E*G;
FG=F*G;
proc reg data=castf;
model y=A B C D E F G AB AC AD AE AF AG BC BD BE BF BG CD CE
CF CG DE DF DG EF EG FG/selection=rsquare best=4 stop=4;
run;
```

The results shown below indicate that when two variables are considered in the model, the model which includes main effect F and the interaction FG fits best and has an R² = 0.8925, compared to the R² = 0.5867 for the model that the authors fit to the data (which included main effects D and F). The best model with three variables in the equation only raises R² from 0.8925 to 0.9526 and the third variable is probably not needed. The model including F and FG is the model found in the other papers which have reanalyzed this data by various procedures.

| Model | R-Square | Variables in Model |
|---|---|---|
| 1 | 0.4474 | FG |
| 1 | 0.4451 | F |
| 1 | 0.4377 | AE |
| 1 | 0.1812 | BC |
| 2 | 0.8925 | F FG |
| 2 | 0.6638 | AE FG |
| 2 | 0.6621 | F AE |
| 2 | 0.6238 | BD FG |
| 3 | 0.9526 | F AE FG |
| 3 | 0.9313 | F BD FG |
| 3 | 0.9190 | D F FG |
| 3 | 0.9118 | F BD FG |
| 4 | 0.9686 | F AE EF FG |
| 4 | 0.9660 | F AE CD FG |
| 4 | 0.9643 | F AD AE FG |
| 4 | 0.9642 | F BD GF FG |