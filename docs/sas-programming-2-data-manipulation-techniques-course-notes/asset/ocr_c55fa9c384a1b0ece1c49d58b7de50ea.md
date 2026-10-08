# 2.2 Writing to Multiple SAS Data Sets 2-27

# Level 1

# 4. Creating Multiple SAS Data Sets

The data set orion.employee_organization contains information about employee job titles, departments, and managers.

Partial orion.employee_organization (424 Total Observations)

| Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|--|
| 12101 | Director | Sales Management | 120261 |
| 120102 | Sales Manager | Sales Management | 120101 |
| 120103 | Sales Manager | Sales Management | 120101 |
| 120104 | Administration Manager | Administration | 120101 |
| 120105 | Secretary I | Administration | 120101 |

+   a. Create a separate data set for each department.

Name the data sets work.admin, work.stock, and work.purchasing

Use conditional logic and explicit OUTPUT statements to write these data sets depending on whether the value of Department is Administration, Stock & Shipping, or Purchasing, respectively. Ignore all other Department values.

Hint: Be careful with capitalization and the spelling of the Department values.

+   b. Print work.admin and verify your results. Add an appropriate title.

Partial work.admin (34 Total Observations)

| Obs | Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|---|--|
| 1 | 120104 | Administration Manager | Administration | 120101 |
| 2 | 120105 | Secretary I | Administration | 120101 |
| 3 | 120106 | Office Assistant II | Administration | 120104 |
| 4 | 120107 | Office Assistant III | Administration | 120104 |
| 5 | 120108 | Warehouse Assistant II | Administration | 120104 |

+   c. Print work.stock and verify your results. Add an appropriate title.

Partial work.stock (26 Total Observations)

Stock and Shipping Employees

| Obs | Employee_ID | Job_Title | Department | Manager_ID |
|---|---|---|---|--|
| 1 | 120670 | Shipping Manager | Stock & Shipping | 120659 |
| 2 | 120671 | Shipping Agent III | Stock & Shipping | 120670 |
| 3 | 120672 | Shipping Manager | Stock & Shipping | 120659 |
| 4 | 120673 | Shipping Agent II | Stock & Shipping | 120672 |
| 5 | 120677 | Shipping Manager | Stock & Shipping | 120659 |

+   d. Print work.purchasing and verify your results. Add an appropriate title.

Copyright © 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.