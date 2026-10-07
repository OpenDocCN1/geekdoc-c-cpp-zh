# 248 Learning SAS by Example: A Programmer's Guide, Second Edition

> Note: As with the FLOW option, this option affects only the listing output. It has no effect on other ODS destinations such as HTML or PDF. If your output destination is PRINTER, PDF, or RTF, you can use the COLUMNS=option in the ODS statement.

Here is the program:

# Program 15.13: Creating a Multi-column Report

```
title "Random Assignment - Three Groups";nproc report data=Learn.Assign panels=99
    headline Group;
    columns Subject Group;
    define Subject / display width=7;
    define Group / widths=5;
run;
```

The page size (PS) is set to 16 (which limits the number of lines per page to 16) so that you can see the effect of the PANELS=option. In this program, a DISPLAY was used for Subject (a numeric variable). This was not necessary because the default usage for Group (a character variable) is DISPLAY, and you would have a detailed report anyway. However, it is fine to include it. Here is the report:

Figure 15.12: Output from assignment - Three Groups

| Subject Group | Subject Group | Subject Group |
| 1 | C | 13 | A | 25 | C |
| 2 | B | 14 | A | 26 | B |
| 3 | B | 15 | C | 27 | C |
| 4 | A | 16 | C | 28 | A |
| 5 | B | 17 | C | 29 | B |
| 6 | A | 18 | B | 30 | B |
| 7 | C | 19 | B | 31 | B |
| 8 | C | 20 | B | 32 | B |
| 9 | B | 21 | C | 33 | C |
| 10 | A | 22 | C | 34 | C |
| 11 | C | 23 | C | 35 | A |
| 12 | C | 24 | C | 36 | C |

# 15.12 Producing Report Breaks

PROC REPORT can produce totals and subtotals on ANALYSIS variables using BREAK and RBREAK statements. RBREAK, which stands for report break, is used to report summary statistics (typically sums or means) at the top or bottom of a report. The BREAK statement is used to report summary statistics each time a GROUP or ORDER variable changes value. Let's look at a few examples.