# Convert HR Data: Complete Program

PROC PRINT Output

| EmpID | Pay | Bonus | Phone | HireDate |
|---|---|---|---|--|
| 1036 | 52000 | 5200 | (303) 393-0956 | 04/13/2008 |
| 11048 | 32000 | 3200 | (919) 770-8292 | 08/25/2010 |
| 11052 | 49000 | 4900 | (301) 449-5239 | 06/08/2009 |

# Exercises

If you restarted your SAS session since the last exercise, open and submit the libname.sas program found in the data folder.

# Level 1

10. Using the PUT and INPUT Functions

The data set orion.shipped contains details about each product shipped to one of Orion Star's retail outlets in 2007.

Partial orion.shipped

| Product_ID | Ship_Date | Quantity | Price |
|---|---|---|--|
| 24080200021 | 05JAN2011 | 2 | $42.45 |
| 24080200035 | 04JAN2011 | 6 | $12.15 |
| 24020112225 | 04JAN2011 | 2 | $77.65 |
| 21020500002 | 09JAN2011 | 3 | $5.70 |

PROC CONTENTS Output for orion.shipped

| Variable | Type | Len | Format |
|---|---|---|--|
| 1 | Product_ID | Num | 8 | |
| 2 | Ship_Date | Num | 8 | DATE9. |
| 3 | Quantity | Num | 8 | |
| 4 | Price | Char | 7 | |