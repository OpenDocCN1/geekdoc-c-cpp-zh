For example, in a simple use of PROC FREQ, to obtain counts of the number of subjects observed in each category of group (GP), use the following:

```
PROC FREQ; TABLES GP; RUN;
```

To produce a cross-tabulation table of GENDER by treatment GP, use

```
PROC FREQ; TABLES GENDER*GP; RUN;
```

The variables specified in the TABLES statement can be either type categorical/character or numeric (where numeric values represent discrete categories). To request chi-square

# TABLE 10.3 Sample TABLES Statements

| Table | Description |
| --- | --- |
| TABLES A; | Specifies frequencies for a single variable |
| TABLES A*B; | Specifies a cross-tabulation between two variables |
| TABLES A*B B*C X*Y; Also, TABLES A* (B C D); is the same as TABLES A*B A*C A*D; | Specifies several cross-tabulation tables |
| TABLES (A - C)*; is the same as TABLES A* B*X C*X; | Uses a range of variables in a TABLES statement |

# TABLE 10.4 Options for the Table Statement

| Option | Description |
| --- | --- |
| AGREE | Requests kappa statistic (inter-rater reliability). To include significance tests for kappa, add a TEST statement. For example, TABLES A*B /AGREE; TEST KAPPA; |
| RELRISK | Requests relative risk calculations |
| FISHER | Requests' Exact test for tables greater than 2x2 |
| SPARSE | Requests all possible combinations of variable levels even when a combination never occurs |
| MISSING | Requests that missing values be treated as nonmissing |
| CELLCHI2 | Displays the contribution to chi-square for each cell |
| NOCOL | Suppresses percentages for each cell |
| NOCUM | Suppresses cumulative and cumulative percentages in one-way frequency tables and in list format |
| NOFREQ | Suppresses frequency count for each cell |
| NOPERCENT | Suppresses row and column percentage in cross-tabulation tables, or cumulative percentages in one-way frequency tables and in list format |
| NOPRINT | Suppresses tables but displays statistics |
| NOROW | Suppresses row percentage for each cell |
| TESTP=(list) | Specifies a test based on percentages for the chi-square test (see the goodness-of-fit example) |