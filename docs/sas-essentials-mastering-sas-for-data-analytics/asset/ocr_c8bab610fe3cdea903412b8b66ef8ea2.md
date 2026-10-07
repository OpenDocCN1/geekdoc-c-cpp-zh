Upon further examination, you verify with the survey coordinator that an answer of
"MEX" or "M" for race should be corrected to "H," "W" should be corrected to "C,\nand "A" should be corrected to "AA". IF RACE is "X," "NA" or "" then set it to
blank (missing). The code to correct two of these items (which must appear after the
UPCASE case and before the IN () function) fixes

```
IF RACE="MEX" OR RACE="M" then RACE="H";
IF RACE="X" OR RACE="NA" then RACE="";
```

Enter these files. Submit the code and verify that the fixes work (including check-
ing log for error messages).

# 6.4.3 Check and Fix Incorrect Categories, Fix duplicated Variables

Two variables are MARRIED and SINGLE. The survey asked respondents their
marital status, and the information recorded in the data set where 1 means yes and 0
means no. Technically, these two variables should be the opposite of each other, and you
should only require one of them in the data set. However, if you look at the frequencies
of each PROC FREQ, you discover that they are not telling you the same thing.
To check and other categorical variables, use the PROC FREQ procedure. This is
illust in the next example

# HANDS-ON EXAMPLE

This example checks for incorrect entries using PROC FREQ and fixes the problems.

+   1. Open the program file DISCOVER1.SAS.

```
PROC FREQ data=MYSASLIB_cleaned;
TABLES MARRIED SINGLE TOP_REASON RACE GENDER HOW_ARRIVED;
run;
```

Submit the code and observe the results in Table 6.11. (Only some of the output is
shown here.) Note what you discover:

+   - There are codes for MARRIED that are incorrect.
- The two variables MARRIED and SINGLE are not the opposite of another as
you would expect. Typically, you'd only need one table or the other. In this case,
the researcher chooses to use the SINGLE table, so the MARRIED variable can be
deleted.
- Several values for TOP_REASON are incorrect.
- RACE still contains some incorrect values. (The previous fix didn't correct all the
problems.)

(continued)