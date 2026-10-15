The 4000 lines of PARMEST are processed in groups of two lines. The first line corresponds to the intercept based on the IF check (if variable="Intercept" then b0 = estimate;). This estimate is not immediately written to the data set because the b0 and b1 estimates need to be paired. The RETAIN statement holds the value of the intercept while the next line is processed. (For more information about the RETAIN statement, see Chapter 9.) The first five lines and last five lines of the data set produced are output by the following code:

```
proc print data=ParmEst2;  * a nice debugging check;
    title "first 5/last 5 lines from the PARMEST2 data set";
    where iexpt <= 5 or iexpt > 1995;
run;
```

The output matches the data structure that is needed for later analysis.

| Obs | iexpt | b0 | b1 |
|---|---|---|---|
| 1 | 1 | 3.89332 | 1.33037 |
| 2 | 2 | 3.91362 | 1.25442 |
| 3 | 3 | 3.14595 | 1.47832 |
| 4 | 4 | 2.88033 | 1.52853 |
| 5 | 5 | 3.46571 | 1.46000 |
| 1996 | 1996 | 2.84155 | 1.42434 |
| 1997 | 1997 | 3.00608 | 1.42357 |
| 1998 | 1998 | 2.43907 | 1.57462 |
| 1999 | 1999 | 3.20998 | 1.33068 |
| 2000 | 2000 | 2.41439 | 1.55405 |

Note: The SAS log confirms that 4000 observations from PARMEST were processed and that 2000 observations were generated in the PARMEST2 data set.

```
NOTE: There were 4000 observations read from the data set WORK.PARMEST.
NOTE: The data set WORK.PARMEST2 has 2000 observations and 3 variables.
```

At this point, you can feel confident that the code is correct, and you can now focus on the analysis of primary interest—exploring the sampling distribution of the intercept and slope estimates from simple linear regression. The sampling distribution of the intercept and slope estimates is centered at the values of the underlying parameters that were set as part of generating the regression data. (See Display 4.22.) This is not a surprise because you know that these estimates are unbiased. By the way, what do you see when you compare the observed standard deviation of b1 over the 2000 simulated data sets to the value of s(b1)? Is it what you expected?