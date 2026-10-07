```
ILOOP=1;
SUM=0;
DO WHILE (ILOOP LT 5);
SUM=SUM+ILOOP;
ILOOP+1;
END;
```

# HANDS-ON EXAMPLE

This program illustrates the uses of the DO WHILE loop.

+   1. Open the program file DWHILE.SAS.

```
DATA TMP;
N=0;
SQUARESUM=0;
DO WHILE (N<5)
SQUARESUM=SQUARESUM+N**2; OUTPUT;
N+1;
END;
RUN;
PROC PRINT;
RUN;
```

The OUTPUT statement in the code causes SAS to save each SQUARESUM as a record in the data set TMP so you'll see the values at each iteration.

+   2. Run the program and observe the output data set given in Table 7.3. Why do the values of N range from 0 to 4?

+   3. Change the code to use a DO UNTIL to get the results.

+   4. Change the code to use an iterative DO loop to get the results.

# TABLE 7.3 Example of Using the DO WHILE Statement

| Obs | N | SQUARESUM |
|---|---|-|
| 1 | 0 | 0 |
| 2 | 1 | 1 |
| 3 | 2 | 5 |
| 4 | 3 | 14 |
| 5 | 4 | 30 |

One of the most powerful uses of the DO loop is realized when it is used in conjunction with an array. For example, suppose you take five systolic blood pressure readings on each subject. Suppose that if any of these readings are above 140, you want to classify the subject with the value HIGHBP=1, or else the subject will have the value HIGHBP=0. The following code could perform this task: