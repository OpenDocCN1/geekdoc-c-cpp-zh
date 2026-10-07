# Chapter 25: Introducing the SAS Macro Language 435

Figure 25.10: Partial Listing of Data Set Compare_to_Mean

# Listing of Data Set Compare_to_Mean

| Subject | WBC | RBC | Percent_RBC | Percent_WBC |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 7710 | 7.40 | 135% | 109% |
| 2 | 6560 | 4.70 | 86% | 93% |
| 3 | 5690 | 7.53 | 137% | 81% |
| 4 | 6680 | 6.85 | 125% | 95% |
| 5 | | 7.72 | 141% | |
| 6 | 6140 | 3.69 | 67% | 87% |
| 7 | 6550 | 4.78 | 87% | 93% |
| 8 | 5200 | 4.96 | 90% | 74% |
| 9 | | 5.66 | 103% | |
| 10 | 7710 | 5.58 | 104% | 109% |

Hopefully, this very brief introduction to SAS macros has shown you that the SAS macro language is not as scary as you might have thought and given you the courage to try them in your own programs.

# 25.10 Problems

Solutions to odd-numbered problems are located at the back of this book. Solutions to all problems are available to professors. If you are a professor, visit the book's companion website at support.sas.com/cody for information about how to obtain the solutions to all problems.

+   1. Use PROC PRINT to list the first five observations from data sets. Use the system macro variables &SYSDAY (returns the day of the week), &SYSDATE, and &SYSTIME to customize the title (see the following example, which was run on a Friday):

| Produced on Sunday, 10DEC2017 at 10:02 |
| Date | Price |
| :--- | :--- |
| 01/01/2017 | $34 |
| 01/02/2017 | $39 |
| 01/03/2017 | $39 |
| 01/04/2017 | $30 |
| 01/05/2017 | $35 |

2. Rewrite the following program using %LET to assign the starting and ending values of the loop to macro variables. Be sure these values are also printed in the PROC PRINT output.