# Table 9.7 Williams' Design and Data for Sprint Time Experiment

| Group | Subject | Period | Treat | Time | Subject | Period | Treat | Time |
|---|---|---|---|---|---|---|---|---|
| 1 | 1 | 1 | 1 | 5.47 | 7 | 1 | 2 | 5.68 |
| 1 | 1 | 1 | 1 | 6.03 | 8 | 1 | 2 | 5.90 |
| 1 | 1 | 2 | 3 | 5.00 | 7 | 2 | 3 | 5.27 |
| 1 | 2 | 2 | 3 | 5.42 | 8 | 2 | 3 | 5.70 |
| 1 | 1 | 3 | 2 | 5.08 | 7 | 3 | 1 | 5.23 |
| 1 | 2 | 3 | 2 | 5.38 | 8 | 3 | 1 | 5.54 |
| 2 | 3 | 1 | 2 | 7.69 | 9 | 3 | 3 | 5.97 |
| 2 | 4 | 1 | 2 | 6.32 | 10 | 1 | 3 | 7.87 |
| 2 | 3 | 2 | 1 | 7.03 | 9 | 2 | 1 | 5.73 |
| 2 | 4 | 2 | 1 | 7.03 | 10 | 2 | 1 | 5.73 |
| 2 | 4 | 2 | 1 | 6.32 | 10 | 2 | 1 | 7.87 |
| 2 | 3 | 2 | 1 | 7.03 | 9 | 2 | 1 | 5.73 |
| 2 | 4 | 2 | 1 | 7.03 | 10 | 2 | 1 | 5.73 |
| 2 | 3 | 3 | 3 | 7.57 | 9 | 3 | 2 | 4.97 |
| 2 | 4 | 3 | 3 | 5.77 | 10 | 3 | 2 | 6.97 |
| 3 | 5 | 3 | 3 | 8.05 | 11 | 1 | 1 | 6.19 |
| 3 | 5 | 1 | 3 | 7.51 | 12 | 1 | 2 | 7.39 |
| 3 | 6 | 2 | 2 | 7.12 | 11 | 2 | 1 | 5.66 |
| 3 | 6 | 2 | 2 | 6.49 | 12 | 2 | 2 | 6.55 |
| 3 | 5 | 3 | 1 | 7.18 | 11 | 3 | 3 | 5.57 |
| 3 | 6 | 3 | 1 | 6.35 | 12 | 3 | 3 | 7.09 |

The SAS commands to analyze the data with proc glm are shown below.

```
proc format;
value surface 1='cement' 2='track' 3='grass';
run;
proc glm;
Class subject period treat carry;
model y=subject period treat carry;
means treat carry;
format treat carry surface.;
run;
```

Running this code produces the following type III ANOVA table shown on the next page. Here it can be seen that the running surface caused a significant difference in running times, and that there were significant carryover effects.

The means statement estimates \(\mu + \hat{\tau}_i\) and \(\hat{\mu} + \hat{\lambda}_i\) in model 9.3. The result shown below the ANOVA table on the next page indicates that the rubberized running track produced the fastest running times, and that grass produced the slowest running times.