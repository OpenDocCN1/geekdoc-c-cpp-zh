The MAXID option is used in the following example to identify which subjects had the maximums for each value of any classification variables. This option allows us to add a new variable to the OUTPUT data set, which takes on the value of the ID variable for the maximum observation.

```
```sas
title1 '7.4.1a Using MAXID';
title2 'One Analysis Variable';
proc summary data=advrpt.demo;
    class race;
    var ht;
    output out=stats
        mean=meanHT
        max=maxHt ❶
        maxid(ht (subject))=maxHtSubject ❷
        ;
run;
proc print data=stats;
    run;
```
```

The maximum for the analysis variable HT is requested ❶ for each RACE. We would also like to know which SUBJECT had the maximum HT ❷ (the subject number is to be stored in the variable MAXHTSUBJECT).

Using the same generalized option syntax as was discussed in the previous section, there are several variations of the syntax for the MAXID option shown in this example. In this case there is a single analysis variable and a single ID variable.

| 7.4.1a Using MAXID |  |  |  |  |  |  |
|---|---|---|---|---|---|---|
| One Analysis Variable |  |  |  |  |  |  |
| Obs | race | _TYPE_ | FREQ_ | meanHT | max Ht | maxHt Subject |
| 1 |  | 0 | 76 | 67.6053 | 74 | 209 |
| 2 | 1 | 1 | 42 | 68.4762 | 74 | 209 |
| 3 | 2 | 1 | 18 | 67.6667 | 72 | 201 |
| 4 | 3 | 1 | 8 | 65.0000 | 68 | 215 |
| 5 | 4 | 1 | 4 | 64.5000 | 65 | 244 |
| 6 | 5 | 1 | 4 | 66.5000 | 68 | 212 |

When there is more than one analysis variable, the MAXID statement can be expanded following the same syntax rules as were discussed in Section 7.3.

In this example the subject number of the tallest and of the heaviest subjects in the study are to be displayed.

```
```sas
var ht wt;
output out=stats
        mean= meanHT MeanWT
        max=maxHt maxWt
        maxid(ht(subject) wt(subject))=maxHtSubject MaxWtSubject
        ;
```
```

| 7.4.1b Using MAXID |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| Two Analysis Variables |  |  |  |  |  |  |  |  |  |
| Obs | race | _TYPE_ | FREQ_ | meanHT | MeanWT | max Ht | max WT | maxHt Subject | MaxWt Subject |
| 1 |  | 0 | 76 | 67.6053 | 162.237 | 74 | 240 | 209 | 203 |
| 2 | 1 | 1 | 42 | 68.4762 | 176.143 | 74 | 215 | 209 | 208 |
| 3 | 2 | 1 | 18 | 67.6667 | 166.333 | 72 | 240 | 201 | 203 |
| 4 | 3 | 1 | 8 | 65.0000 | 112.000 | 68 | 133 | 215 | 215 |
| 5 | 4 | 1 | 4 | 64.5000 | 113.500 | 65 | 115 | 244 | 230 |
| 6 | 5 | 1 | 4 | 66.5000 | 147.000 | 68 | 147 | 212 | 211 |