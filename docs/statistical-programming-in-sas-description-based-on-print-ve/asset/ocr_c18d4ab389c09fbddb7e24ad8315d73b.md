# Display 8.23 Output from PROC PRINT for the different indicator variables

| Obs | literacy | cat_literacy1 | cat_literacy2 | cat_literacy3 | cat_literacy4 |
|---|---|---|---|---|---|
| 1 | -99.00 | 0 | 1 | . | . |
| 2 | 25.55 | 1 | 1 | 1 | 1 |
| 3 | 73.70 | 2 | 2 | 2 | 2 |
| 4 | 83.00 | 3 | 3 | 3 | 3 |
| 5 | 99.90 | 4 | 4 | 4 | 4 |
| 6 | 107.00 | 0 | 0 | . | . |
| 7 | . | 0 | 1 | . | . |

Look at the first method that defines the variable cat literacy1. When literacy=54, the first condition (0<literacy<=53) is FALSE. The second condition (53<literacy<=76) is TRUE. The third condition (76<literacy<=90) is FALSE. The fourth condition (90<literacy<=100) is FALSE. Consider the following expression:

```
cat_literacy1 = 1*(0<literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

If TRUE =1 and FALSE =0, this expression evaluates to the following:

```
cat literacy1 = 1*(0) + 2*(1) + 3*(0) + 4*(0) = 2
```

If you want the missing values of LITERACY preserved, or if you want values outside of the valid range to be assigned missing values, then this code does not behave as expected. If LITERACY is missing (.), or if it has a value outside of the range that is tested (-99 to 107), then none of the conditions are TRUE and cat_literacy1=0.

The second method leads to other behavior worth noting. Consider the following expression:

```
cat_literacy2 = 1*(literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

This method assigns cat literacy2=1 if LITERACY is -99 or missing. This assignment occurs because condition (literacy<=53) is TRUE for -99 (no surprise