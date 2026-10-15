
The transposed data set tran_out has one row and 20 columns (variables xx1 through xx20) containing the totals and a variable _NAME_, which has the value TOTAL (i.e., the name of the variable that is transposed).

## Display 9.8 Constructing a randomization test of two-population mean equality

```
data test;
  input Obs conc total;     * entering directly as alternative to ;
  datalines;                * permanent SAS data file reference;
  1     0    27
  2     0    32
  3     0    34
  4     0    33
  5     0    36
  6     0    34
  7     0    33
  8     0    30
  9     0    24
 10     0    31
 11   160    29
 12   160    29
 13   160    23
 14   160    27
 15   160    30
 16   160    31
 17   160    30
 18   160    26
 19   160    29
 20   160    29
;
run;

proc print data=test;
  title "NITROFEN: print of (0, 160) concentrations";
  var conc total;
run;

proc transpose data=test prefix=xx out=tran_out;
  var total;
run;

* add variable "type" to identify the observed data;
data obs_test; set tran_out;
  type = "O";     * identifies original data;
run;
```

### Display 9.8 (continued)

```
* check result of TRANSPOSE and the added variable;
proc print data=obs test;
title "Randomization test: observed data";
run;
/*
PROC PLAN used to generate a set of indices for the
randomization test.
*/
proc plan seed=8675309;
factors test=4000 ordered in=20;
output out=d_permut;
run;
/*
PROC TRANSPOSE restructures the data set output from PROC PLAN
*/
proc transpose data=d_permut prefix=in
    out=out_permut(keep=in1-in20);
by test;
run;

proc print data=out_permut;
run;
/*
Write out the original data along with a sample of
permuted indices to an external data file
*/
data _null_; set obs_test;
file 'C:\Users\baileraj.IT\Desktop\my-perm.data';
put type xx1-xx20;
run;

data _null_; set out_permut;
type = 'P'; * permutation data;
file 'C:\Users\baileraj.IT\Desktop\my-perm.data' mod;
/* mod option adds lines to existing file */
put type in1-in20;
run;
/* Excerpt from my-perm.data ...
O 27 32 34 33 36 34 33 30 24 31 29 28 27 30 31 30 26 29 20
P 8 14 4 11 3 2 12 1 6 13 17 9 1 16 9 19 20 7 10 18
P 12 2 8 10 13 7 9 16 4 19 15 3 5 14 17 1 20 11 6 18
P 18 17 13 14 5 8 19 16 3 12 11 9 10 7 2 20 4 6 1 15
... */
```

### Display 9.8 (continued)

```
data perm_data;
  array both{20} x1-x10 y1-y10;
    /* array for observed values */
  array ins{20} in1-in20;
    /* index array */
  array perms{20} xp1-xp10 yp1-yp10;
    /* array for permuted values */

infile 'C:\Users\baileraj.IT\Desktop\my-perm.data';
input type $ @;
  if type='O' then do;
    input x1-x10 y1-y10;
    obs_diff = mean(of x1-x10) - mean(of y1-y10);
    retain obs_diff x1-x10 y1-y10;
  end;
  else do;
    input in1-in20;

* permute observations according to indices in the array 'ins';
    do ii = 1 to 20;
      perms{ii} = both{ ins[ii] };
    end;

/* calculate test statistic for the permuted data and
   save an indicator variable denoting whether the
   value of the statistic for the permuted data set
   is at least as extreme as the observed test statistic.
*/
    perm_diff = mean(of xp1-xp10) - mean(of yp1-yp10);
    perm_ge = (perm_diff >= obs_diff);          * 1-tailed;
    perm_2tail = (abs(perm_diff) >= abs(obs_diff));  * 2-tailed;
    keep obs_diff perm_diff perm_ge perm_2tail;
    output;
  end;
run;

/*
PROC FREQ is used to construct the relative frequency of
randomization test yielding test statistic
(mean difference) for permuted samples at least
as extreme as mean difference observed in the data
*/

proc freq data=perm_data;
title "NITROFEN: randomization test -> upper-tail p-value";
table perm_ge perm_2tail;
run;
```

The output from PROC FREQ is shown in Display 9.9.

## 346 Statistical Programming in SAS

## Display 9.9 Output from a randomization test of two-population mean equality

| perm_ge | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|---------|-----------|---------|----------------------|--------------------|
| 0       | 3920      | 98.00   | 3920                 | 98.00              |
| 1       | 80        | 2.00    | 4000                 | 100.00             |

| perm_2tail | Frequency | Percent | Cumulative Frequency | Cumulative Percent |
|------------|-----------|---------|----------------------|--------------------|
| 0          | 3846      | 96.15   | 3846                 | 96.15              |
| 1          | 154       | 3.85    | 4000                 | 100.00             |

The two-tailed p-value from the randomization test, 0.0385, is quite similar to the p-value from the t-test.

In this chapter, data structure and arrays are emphasized. The use of a data structure for recoding variables is illustrated. Arrays are used in applications where a Monte Carlo p-value and a randomization test p-value are obtained. Using RETAIN statements, calculations over observations are highlighted. This feature is used in an example processing data from individuals who have multiple, but different, numbers of records. A randomization test showcases the power of the ARRAY and RETAIN statements.

- Cody, Ron, and Ray. Pass. 1995. SAS Programming by Example. Cary, NC: SAS Institute Inc.
- Edgington, Eugene. 1995. Randomization Tests. New York, NY: Marcel Dekker, Inc.
- Good, Phillip I. 2001. Resampling Methods: A Practical Guide to Data Analysis. 2nd Ed. New York, NY: Birkhauser Boston.
- Ripley, Brian D. 1981. Spatial Statistics. Hoboken, NJ: John Wiley & Sons, Inc.
- Waller, Lance A., and Carol Gotway. 2004. Applied Spatial Statistics for Public Health Data. Hoboken, NJ: John Wiley & Sons, Inc.

## 9.7 Exercises

- 1. The code for the randomization test in this chapter has an inherent inefficiency. The program performs the following check:

```
if type='O' then do;
```

However, type='O' only in the first line, but every line is checked. Modify this program to make it more efficient. **Hint:** You can use multiple INPUT statements in a DATA step.

- 2. A simple difference statistic is used in the two-group randomization test. Does it matter if the *t*-statistic is used? Conduct a randomization test using the *t*-statistic.

- 3. Perform a randomization test on the packaging and log-bacterial growth data.² In this problem, n₁=n₂=n₃=n₄=3. Use a statistic that measures the difference in the four group means. For example:

$$CSS=\sum_{i=1}^{4}(\bar{Y}_i-\bar{Y})^2$$

$\bar{Y}_i$ is the arithmetic mean of the iᵗʰ group and $\bar{Y}$ is the mean of all of the observations.

- 4. Data on three groups of subjects are arranged so that a group code (C, A, B) is followed by one or more scores for that group, which can span more than one record of raw data. Write a program to read these data and create a SAS data set with variables GROUP and SCORE, one set per observation. Generate an error message if you encounter an invalid group code (e.g., GROUP=D). Ignore numeric data until the next valid group code. Here are the sample data:

```
C 303 102 150 B 202 C 300 B 450 400 399
420 A 289 280 278 D 14 16 C 27 38
```

**Hint:** Read every data item in the raw data file as a character value. Test whether it is an A, B, or C. If it is one of these values, set GROUP equal to that value, and then read the numeric data. If it is not, convert the character you just read to a

> ² Meat data set usage based on the “Bacteria growth in meat” data set from Kuehl, R. O. *Statistical Principles of Research Design and Analysis*. 1st Ed. © 1994. Brooks/Cole, a part of Cengage Learning, Inc. ISBN: 9780534188047(0534188044).

number using the INPUT function. Based on Cody and Pass (1995), SCORE=INPUT(CHARVAR,5.) accomplishes this.

5. In Display 9.7, you have data with multiple start and stop times for each individual. But, start and stop times are paired for each individual. In the data set, you have the following:

```
1 15 25
2 10 12
2 18 22
3 6 12
3 14 15
3 17 23
```

Suppose that start and stop times are on different lines.

```
1 15
1 25
2 10
2 12
2 18
2 22
3 6
3 12
3 14
3 15
3 17
3 23
```

How do you modify the code in Display 9.7 to address this structure? What do you do if a person is still in the program (i.e., he or she has no stop time for his or her last start time)? For example, suppose all individuals are followed for 30 weeks. Individuals 1 and 3 are still receiving services at the end of the 30 weeks. Conduct a similar analysis as discussed previously (e.g., determine the number of admissions, length of first stay, total length of stay), and add the definition of an indicator variable representing whether the person is still in the system when the study ends.

```
1 15
2 10
2 12
2 18
2 22
3 6
3 12
3 14
3 15
3 17
```
