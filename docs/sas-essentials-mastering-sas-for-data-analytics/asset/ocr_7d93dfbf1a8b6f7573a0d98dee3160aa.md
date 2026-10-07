With this information, you can continue cleaning the data set.

2. Open the program file MESSY3.SAS. Observe the code listed under the Step 3 comment lines. The code already includes the following fixes:

+   - The MARRIED variables are eliminated.
- Additional RACE fixes are included.

```
DROP MARRIED;
IF RACE NOT IN ('AA', 'H', 'C') THEN RACE="";
To fix the TOP_REASON problems, use an IF statement as shown in
this code (note that TOP_REASON) is a character variable.
IF TOP REASON NE "1"
TOP_REASON "2" and
TOP_REASON "3" then TOP_REASON="";
```

Submit the code and observe the results.
3. Go back to DISCOVER1.SAS, take the MARRIED variable from the TABLE statement and resubmit it to verify that all changes have been made. Note that for character variables the missing values are noted at the bottom of the table, and for the numeric value (TOP_REASON) the missing values category () is listed in the table.

# 6.4.4 Check and Out-of-Range Numeric Variables

Now that categorical variables have been cleaned, it is time to draw attention to the numeric measurement variables: AGE, ARRIVAL (Temperature), EDUCATION, and SATISFACTION. One way to take an initial look at numeric variables is with PROC MEANS. In particular, you are looking for unusual minimum and maximum values. The following example illustrates how to find problem values using PROC MEANS and how to correct them.

> HANDS-ON
This example corrects problems associated with numeric variables.

+   1. Open the program DISCOVER2 .SAS and submit it to create the table of means shown in Table 6.12. (The output depends on you doing the previous exercises correctly, so if you have not them your answer may differ.)

```
PROC MEANS MAXDEC=2 DATA=CLEAN CLEAN; RUN;
```

When you run PROC MEANS, it displays means of all numeric variables. Note in this case AGE is not included in the output. On further inspection, you see that AGE is a character-type variable in the data set. (A common problem when importing numeric is with the data from Excel or CSV files.) One way to convert this to numeric is with some minimum INPUT () function (see Appendix B). You also note problems with some
(continued)