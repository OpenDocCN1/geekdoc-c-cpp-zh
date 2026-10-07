CHAPTER 19: CREATING CUSTOM REPORTS

# TABLE 19.3 (Continued)

| Obs | REGION | AREA | SITE | UPSTAIRS | TYPE | MONTH | SALES_K |
|---|---|---|---|---|---|---||
| 11 | | W | | UPSTAIRS | STORE | NOV | 47 |
| 12 | | W | | UPSTAIRS | STORE | NOV | 73 |
| 13 | | N | | UPSTAIRS | KIOSK | NOV | 35 |
| 14 | | N | | DOWNSTAIR | STORE | NOV | 43 |
| 15 | | N | | UPSTAIRS | KIOSK | NOV | 26 |
| 16 | | S | | DOWNSTAIR | KIOSK | NOV | 40 |
| 17 | | S | | UPSTAIRS | STORE | NOV | 61 |
| 18 | | S | | UPSTAIRS | KIOSK | NOV | 32 |
| 19 | | E | | UPSTAIRS | STORE | NOV | 52 |
| 20 | | E | | DOWNSTAIR | KIOSK | NOV | 26 |

# HANDS-ON EXAMPLE

+   1. Open the program file ATAB1.SAS . Observe that the variable TYPE is identified as a categorical variable (CLASS), and that a table is constructed with that variable. As TYPE has two categories, we expect the table to consist of two cells, each with a count (N) that represents the number of items for group. Submit the code and observe the output given in Table 19.4.

```
PROC TABULATE DATA=MSASLIB.REGION;
CLASS TYPE;
TABLE TYPE;
RUN;
```

![](bbox=[0.385, 0.605, 0.615, 0.735])

+   2. Add another variable by modifying the CLASS and TABLE statements:

```
CLASS TYPE AREA;
TABLE TYPE*AREA;
```

where AREA values are the compass points N, S, E, and W. Submit this code and observe the results given in Table 19.5. Note that the first variable TYPE appears as the top categories for the table followed by the next division specified by the AREA variable.