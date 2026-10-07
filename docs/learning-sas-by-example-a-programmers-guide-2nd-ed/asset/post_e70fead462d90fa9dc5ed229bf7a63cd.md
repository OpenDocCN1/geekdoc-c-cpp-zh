
# 310 Learning SAS by Example: A Programmer's Guide, Second Edition

are chosen so that the column headings or labels are not split between rows, rather than the optimum value, to display a particular value. Here is the compact table produced by this program:

Figure 18.14: Output from Program 18.13

| | | RBC N Mean | WBC N Mean | Cholesterol N Mean |
|---|---|---|---|---|---|---|
| Female | Old | 242 | 5.5 | 7,106 | 208 | 195.9 |
| | | Young | 167 | 5.5 | 7,121 | 141 | 212.3 |
| | | Total | 409 | 5.5 | 7,112 | 349 | 202.5 |
| Male | Old | 309 | 5.4 | 6,939 | 279 | 199.1 |
| | | Young | 198 | 5.5 | 7,062 | 167 | 203.1 |
| | | Total | 507 | 5.5 | 6,988 | 446 | 200.6 |
| Total | Old | 551 | 5.5 | 7,012 | 487 | 197.7 |
| | | Young | 365 | 5.5 | 7,089 | 308 | 207.3 |
| | | Total | 916 | 5.5 | 7,043 | 795 | 201.4 |

## 18.9 Computing Row and Column Percentages

The statistic PCTN is used with CLASS variables to compute percentages. Program 18.14 demonstrates how this statistic is used. This program computes the numbers and percentages of each of the four blood types in a one-dimensional table.

Program 18.14: Computing Percentages in a One-Dimensional Table

```
title "Counts and Percentages";
proc tabulate data=Learn.Blood format=6;
class BloodType;
table BloodType*(n pctn);
run;
```

The output, while not too pretty, follows:

### Figure 18.15: Output from Program 18.14

# Counts and Percentages

| Blood Type | | | | |
|---|---|---|---|---|
| A | AB | O | |
| N | Pctn | N | Pctn | N | Pctn |
| 412 | 41 | 4 | 96 | 10 | 448 | 45 |

The numbers in the Pctn counts add up to 100%.

It's time to improve on this table's appearance. Let's add an ALL column, rename N and Pctn, and add percent signs to the percentage numbers. Here goes:

Program 18.15: Improving the Appearance of the Output from Program 18.14

```
proc format;
  picture pctfmt low-high='009.9%%';
run;

title "Counts and Percentages";
proc tabulate data=Learn.Blood;
class BloodType;
table(BloodType ALL)*(n*f=5. pctn*f=pctfmt7.1);
  keylabel n = 'Count'
  pctn = 'Percent';
run;
```

Several improvements were made in this program. A user-defined picture format was created with PROC FORMAT. This allows values up to three digits before the decimal place, with the right-most digit being printed (even if it is 0). The 0s in a format are place holders; the 9s are also place holders, but by printing leading 0s if necessary. The percent sign in the picture format is printed as is. You can read more about picture formats in SAS Help Center at http://go.documentation.sas.com.

Separate formats were created for N (5) and for Pctn (Pctfmt.1). Finally, a KEYLABEL statement was used to rename N and Pct to Count and Percent, respectively. By the way, the format width of 7 for the percentage values was chosen by the Percent column heading. Here is the table:

### Figure 18.16: Output from Program 18.15

# Counts and Percentages

| Blood Type | | | | | | | |
|---|---|---|---|---|---|---|---|
| A | AB | B | O | | | | |
| Count Percent Count Percent Count Percent Count Percent |
| 412 | 41.2% | 44 | 4.4% | 96 | 9.6% | 448 | 44.8% | 1000 | 100.0% |

312 Learning SAS by Example: A Programmer's Guide, Second Edition

## 18.10 Displaying Percentages in a Two-Dimensional Table

Here is where things get tricky. Let's make a table of Gender (rows) by BloodType (columns) and request N and PCTN, like this:

Program 18.16: Counts and Percentages in a Two-Dimensional Table

```
proc format;
    picture pctfmt low-high='009.9%%';
run;

title "Counts and Percentages in a Two-way Table";
proc tabulate data=Learn.Blood;
class Gender BloodType;
table (BloodType ALL)*
      (Gender ALL*n=f5. pctn*f=pctfmt7.1)/rows=25;
keylabel ALL='Both Genders'
      n = 'Count'
      pctn = 'Percent';
run;
```

The TABLE option, RTS=25 increases the row title space (the space for the row title). In the table, there are 25 spaces from the left-most line to the line preceding "Female". Here is the output:

Program 18.17: Output from Program 18.16

# Counts and Percentages in a Two-way Table

![](img/e9e15d85398955188e1c30ae5550_321.png)

The percentage values in this table represent the number of subjects in a cell (females with blood type A, for example) as a percentage of all subjects. Thus, the number of females who have blood type A (178) represents 17.8% of the total number of subjects (1000). Suppose you want the percentages to represent the distribution of blood types within each gender. That is, you want the percentages in each column to add to 100%.

## 18.11 Column Percentages

If you want the table to include column percentages, you need to modify Program 18.16. The original (hard) way to do this was to provide a denominator definition. Haworth's book, which was mentioned in the introduction to this chapter, discusses denominator definitions. Every way to do this is to use the keywords COLPCTN and PCTN, which compute column and row percentages. Specifically 18.17 uses the COLPCTN keyword to compute column percentages.

18.17: Using COLPCTN to Compute Column Percentages

```
title "Percents on the Column Dimension"
proc tabulate data=Learn.Blood;
class BloodType;
table (BloodType ALL='All Types')
      (Gender ALL)*f5.colpctn=fpctfmt7.1)/rows=25;
keylabel ALL = 'Both Genders'
n = 'Count'
colpctn = 'Percent';
run;
```

Gender and ALL are the factors in this table. For example, by using COLPCTN for PCTN, the percentages you see in the table are the value of 40.4% for females with blood type A is computed by dividing the number of females with blood type A (178) by the total number of females (440). One other change to make to this program: the KEYLABEL statement assigns the label Both Genders to the keyword. However, you want the label for ALL, associated with BloodType, to read All Types. Another way to assign a label in PROC TABULATE is to follow the variable name with an equal sign, followed by the label in quotation marks. That is why the bottom row of the table reads All Types.

### Figure 18.18: Output from Program 18.17

| | | Genders | | |
|---|---|---|---|---|
| | | Female | Male | Both Genders |
| Blood Type | Count | Percent | Count | Percent | Count | Percent |
| A | 178 | 40.4% | 234 | 41.7% | 412 | 41.2% |
| AB | 20 | 4.5% | 24 | 4.2% | 44 | 4.4% |
| B | 34 | 7.7% | 62 | 11.0% | 96 | 9.6% |
| O | 208 | 47.2% | 240 | 42.8% | 448 | 44.8% |
| All Blood Types | 440 | 100.0% | 560 | 100.0% | 1000 | 100.0% |

Row percentages are requested in a similar fashion, using the keyword ROWPCTN instead of COLPCTN.

314 Learning SAS by Example: A Programmer's Guide, Second Edition

## 18.12 Computing Percentages on Numeric Variables

There is another type of percentage calculation that is available in PROC TABULATE—you can compute the percentage of the SUM statistic that is represented by a column or row value. For example, the data set Sales contains variables Region and TotalSales. If you want to see the contribution to total sales made by each region, you can use the PCTSUM statistic. If you place PCTSUM on the region and TotalSales on the column dimension, you can use the PCTSUM statistic to see the regional contribution of sales as a percentage of total sales for all regions. Here is the program:

Program 18.18: Computing Percentages on a Numeric Value

```
title "Computing Percentages on a Numerical Value";
proc tabulate data=Learn.Sales;
class Region;
var TotalSales;
table (Region ALL) *=n*f=6. sum*f=dollar8.
pctsum*=pctfmt=?;

  keylabel ALL = 'All Regions'
n = 'Number of Sales'
sum = 'Sum'
pctsum = 'Percent'
label TotalSales = 'Total Sales';
run;
```

If you use CLASS variables on both dimensions of a table, you can use the two keywords COLPCTSUM and ROWPCTSUM in a similar manner to COLPCTN and ROWPCTN discussed in the previous section. In the table below, the column labeled Percent represents the sum of the variable TotalSales for each region divided by the sum of TotalSales for all regions.

### Figure 18.19: Output from Program 18

# Computing Percentages on a Numerical Value

| Total Sales | | | | | |
|---|---|---|---|---|---|
| Number of Sales | Sum | Percent | | | |
| Region | | | | | |
| East | 4 | $41,593 | 44.8% | | | |
| North | 5 | $36,825 | 39.7% | | | |
| South | 4 | $12,003 | 12.9% | | | |
| West | 2 | $2,290 | 2.4% | | | |
| All Regions | 15 | $92,710 | 100.0% | | | |
