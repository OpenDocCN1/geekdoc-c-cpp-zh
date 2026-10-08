# 7.2 Conditional DO Loop Processing

| 26 | 2038 | 64,762,815.75 | 67,973,189.29 |

The results above were generated on February 14, 2012. Your values for Year might differ.

# Level 2

# 3. Using an Iterative DO Statement with a Conditional Clause

Orion's income last year was $50,000,000 and expenses totaled $38,750,000. Income is projected to increase at 1% per year and expenses are expected to increase at 2% per year.

+   a. Create a SAS data set named work.expenses that contains each year's projected income and expenses.

+   - Use an iterative DO statement with a conditional clause.

+   - Stop the loop when expenses exceed income or after 30 years, whichever comes first.

+   b. Print the results and format Income and Expenses with a dollar sign and two decimal places.

> Hint: Recall that an iterative DO statement with a conditional clause produces different results DO WHILE and DO UNTIL statements. The results below were generated using a DO UNTIL statement.

# PROC PRINT Output

| Obs | Income | Expenses | Year |
| 1 | $64,762,815.75 | $64,844,951.93 | 26 |

# Challenge

# 4. Using Other Loop Control Statements

+   a. Use an iterative DO statement to calculate projected income and expenses for the next 75 years.

+   - Investigate SAS documentation for information about other loop control statements such as CONTINUE and LEAVE.

+   - Include the appropriate loop control statement (CONTINUE/LEAVE) to stop the loop when expenses exceed income.

+   b. Print the results and format the values of Income and Expenses with dollar signs and two decimal places.

> Hint: Recall that the DO WHILE and DO UNTIL statements might produce different results.

# PROC PRINT Output

| Obs | Income | Expenses | Year |
| 1 | $64,762,815.75 | $64,844,951.93 | 26 |

Copyright \© 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.