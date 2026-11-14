| Obs | rows | cols | tmts |
|---|---|---|---|
| 1 | Week 1 | Store 3 | 4 |
| 2 | Week 1 | Store 4 | 2 |
| 3 | Week 1 | Store 2 | 1 |
| 4 | Week 1 | Store 1 | 3 |
| 5 | Week 2 | Store 3 | 2 |
| 6 | Week 2 | Store 4 | 4 |
| 7 | Week 2 | Store 2 | 1 |
| 8 | Week 2 | Store 1 | 3 |
| 9 | Week 3 | Store 3 | 1 |
| 10 | Week 3 | Store 4 | 3 |
| 11 | Week 3 | Store 2 | 4 |
| 12 | Week 3 | Store 1 | 2 |
| 13 | Week 4 | Store 3 | 3 |
| 14 | Week 4 | Store 4 | 4 |
| 15 | Week 4 | Store 2 | 2 |
| 16 | Week 4 | Store 1 | 1 |

To verify that each treatment occurs once in each row and once in each column, we can print this design in the familiar Latin square layout using proc tabulate as shown below.

```
proc tabulate data=lad;
   class rows cols;
   var tmts;
   table rows, cols*(tmts*f=8.) / rts=10;
run;
```

| | Store 1 | Store 2 | Store 3 | Store 4 |
|---|---|---|---|---|
| | tmts | tmts | tmts | tmts |
| | Sum | Sum | Sum | Sum |
| Week 1 | 3 | 1 | 4 | 2 |
| Week 2 | 4 | 3 | 2 | 1 |
| Week 3 | 2 | 4 | 1 | 3 |
| Week 4 | 1 | 2 | 3 | 4 |