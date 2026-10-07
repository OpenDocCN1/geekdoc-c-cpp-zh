# CHAPTER 15: NONPARAMETRIC ANALYSIS

technique if you do not have exact data values for the observations but you do have order statistics – that is, you do not know the actual response values, but you know which is the largest, the next largest, and so forth, to the smallest. In this case, the smallest value is recoded as 1 and the next to the smallest as 2, and so forth. Many nonparametric procedures are based on these.

The primary nonparametric test for comparing two groups discussed in this chapter is the Wilcoxon (sometimes called the Wilcoxon–Mann–Whitney test). The hypothesis is tested as follows:

+   $H_0$: The two groups have the same distribution (they come from the same population).
$H_a$: The two groups do not have the same distributions (they come from different populations).

The SAS procedure for testing these hypotheses is PROC NPAR1WAY. The procedure outputs several test results, but the focus will be on the Wilcoxon test. The syntax for NPAR1WAY is as follows:

```
PROC NPAR1WAY <options>;
```

Table 15.1 lists options and statements used with PROC NPAR1WAY

| Option | Explanation |
| --- | --- |
| DATA = datename | Specifies which data set to use |
| WILCOSON | Limits output to Wilcoxon-type tests |
| MEDIAN | Requests median test |
| VW | Requests Van der Waerden test |
| NOPRINT | Suppresses output |

Common statements for PROC NPAR1WAY

| | Explanation |
| --- | --- |
| CLASS vars; | Specifies grouping variable(s) |
| VAR vars; | Specifies dependent variable(s) |
| EXACT | Requests exact tests |
| BY, FORMAT, LABEL, WHERE | These statements are common to most procedures and may be used here |

# HANDS-ON EXAMPLE

This example illustrates how to compare two independent groups using nonparametric methods. In it, observations from two brands of fertilizers are compared to determine if one provides better growth (measured by height) than the other. (This is the same data used in ATTEST2.SAS, which was discussed in the Hands-on Example in the section “Running the Two-sample t-test in SAS” in Chapter 11.

1. Open the program file ANPAR1.SAS.

```
DATA FERTILIZER;
INPUT BRAND $ HEIGHT;
DATALINES;
```