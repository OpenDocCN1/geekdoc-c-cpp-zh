```
raw data . . .
logcount condition
7.66 Plastic
6.98 Plastic
7.80 Plastic
5.26 Vacuum
5.44 Vacuum
5.80 Vacuum
7.41 Mixed
7.33 Mixed
7.04 Mixed
3.51 Co2
2.91 Co2
3.66 Co2
```

**Hints:** You can use @ as part of a PUT statement to put the values of multiple observations on the same line in the text file. You can use functions such as MEAN and VAR in DATA step programming to find summary statistics. Alternatively, you can use PROC MEANS with a CLASS statement to set a condition and create an output data set with the summary statistics. This output summary statistics data set could be merged with the original raw data set.

2. Fifty animals were exposed to one of five concentration levels of nitrogen (10 animals per group, but some observations might be missing in the data). The data was recorded separately for three broods produced by each of the 50 animals. Thus, each animal can have data in each of the three brood data sets. A particular animal is uniquely identified by the ID variable. Produce a combined data set containing observations (animals and IDs) that has data on all three broods. In addition, construct an additional variable for the total number of young produced in all three broods. Compare the different joins for this data. In particular, construct the following:

+   a. Brood1 [inner join] Brood2 [inner join] Brood3
+   b. (Brood1 [left join] Brood2) [left join] Brood3
+   c. (Brood1 [right join] Brood2) [right join] Brood3
+   d. Brood1 [full join] Brood2 [full join] Brood3

Print the results for the different combined data sets. Multiple observations are given on each line.