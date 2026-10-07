# 300 Learning SAS by Example: A Programmer's Guide, Second Edition

Figure 18.1: Listing of Data Set Learn.Blood (First 10 Observations)

| Subject | Gender | BloodType | AgeGroup | WBC | RBC | Chol |
|---|---|---|---|---|---|-|
| 1 | Female | AB | Young | 7710 | 7.40 | 258 |
| 2 | Male | AB | Old | 6560 | 4.70 | |
| 3 | Male | A | Young | 5690 | 7.53 | 184 |
| 4 | Male | B | Old | 6680 | 6.85 | |
| 5 | Male | A | Young | | 7.72 | 187 |
| 6 | Male | A | Old | 6140 | 3.69 | 142 |
| 7 | Female | A | Young | 6550 | 4.78 | 290 |
| 8 | Male | O | Old | 5200 | 4.96 | 151 |
| 9 | Male | O | Young | | 5.66 | 311 |
| 10 | Female | O | Young | 7710 | 5.55 | |

# 18.2 A Simple PROC TABULATE Table

Although PROC TABULATE can create complex tables, there are only three operators that control a table's appearance. Let's start out by running PROC TABULATE with all the defaults and selecting a single CLASS variable, like this:

Program 18.1: PROC TABULATE with All the Defaults and a Single CLASS Variable

```
title "All Defaults with One CLASS Variable";nproc tabulate data=Learn.Blood;
class Gender;
table Gender;
run;
```

PROC TABULATE uses a CLASS statement where you specify variables that represent categories (often character variables) to compute frequencies or percentages. In Program 18.1, Gender is selected as the CLASS variable. The TABLE statement specifies the table's appearance. Any variable listed in a TABLE statement must be listed in a CLASS statement or a VAR statement (to be discussed shortly). Here is the output: