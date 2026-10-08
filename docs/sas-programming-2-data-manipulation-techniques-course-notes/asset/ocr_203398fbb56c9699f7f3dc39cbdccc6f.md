# 2.3 Selecting Variables and Observations

# Level 1

# 7. Specifying Variables and Observations

The data set orion.employee_organization contains information about employee job titles, departments, and managers.

Partial orion.employee_organization (424 Total Observations)

| Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|--|\| 120101 | Director | Sales Management | 120261 |
| 120102 | Sales Manager | Sales Management | 120101 |
| 120103 | Sales Manager | Sales Management | 120101 |
| 120104 | Administration Manager | Administration | 120101 |
| 120105 | Secretary I | Administration | 120101 |

+   a. Create two data sets: one for the Sales Department and another for the Executive Department.
* Name the data sets work.sales and work.exec.
* Output to these data sets depending on whether the value of Department is Sales or Executives, respectively. Ignore all other Department.
* The work.sales data set should contain three variables (Employee_ID, Job_Title, and Manager_ID) and have 201 observations.
* The work.exec data set should contain two variables (Employee_ID and Job_Title) and have four observations.

+   b. Print only the first six observations from work.sales.
* Use a data set option to display only the first six observations.
* Add an appropriate title.

```
PROC PRINT Output
Sales Employees
| Obs | Employee_ID | Job_Title | Manager_ID |
|---|---|---|--|\| 1 | 120121 | Sales Rep. II | 120102 |
| 2 | 120122 | Sales Rep. II | 120102 |
| 3 | 120123 | Sales Rep. I | 120102 |
| 4 | 120124 | Sales Rep. I | 120102 |
| 5 | 120125 | Sales Rep. IV | 120102 |
| 6 | 120126 | Sales Rep. II | 120102 |
```

+   c. Print selected observations from work.exec.
* Use data set options to process only observations 2 and 3.
* Add an appropriate title.

```
PROC PRINT Output
Executives
| Obs | Employee_ID | Job_Title |
|---|---|---|
```