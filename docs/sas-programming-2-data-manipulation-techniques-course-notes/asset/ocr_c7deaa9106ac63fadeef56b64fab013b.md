# 4-18 Chapter 4 Reading Raw Data Files

| Field Description | Starting Column | Length of Field | Data Type |
| --- | --- | --- | --- |
| Salary | 64 | 8 | Numeric $100,000 |
| Country | 73 | 2 | Character 'AU' or 'US' |
| Birth Date | 76 | 10 | Numeric mm/dd/yyyy |
| Hire Date | 87 | 10 | Numeric mm/dd/yyyy |

+   a. Create a new SAS data set named *sales_staff* that contains the fields indicated by arrows in the layout table.

+   b. Print *sales_staff* and add an appropriate title.

Partial PROC PRINT Output (165 Total Observations) Australian and US Sales Staff

| Employee_ID | Last_Name | Job_Title | Salary | Date |
| --- | --- | --- | --- | --- |
| 120102 | Zhou | Sales Manager | 108255 | 12205 |
| 120103 | Dawes | Sales Manager | 87975 | 6575 |
| 120121 | Elvish | Sales Rep. II | 26600 | 6575 |
| 120122 | Ngan | Sales Rep. II | 27475 | 8217 |
| 120123 | Hotstone | Sales Rep. I | 26190 | 18901 |

# Level 2

+   2. Using Formatted Input and the Subsetting IF Statement

The raw data file *sales1.dat* has employee information for the Australian and U.S. sales staff. The record layout is shown in the table below.

Layout for *sales1.dat*

| Field Description | Starting Column | Length of Field | Data Type |
| --- | --- | --- | --- |
| Employee ID | 1 | 6 | Numeric |
| First Name | 8 | 12 | Character |
| Last Name | 21 | 18 | Character |
| Gender | 40 | 1 | Character |
| Job Title | 43 | 20 | Character |
| Salary | 64 | 8 | Numeric $100,000 |
| Country | 73 | 2 | Character 'AU' or 'US' |