# Joining on a Common Variable

A WHERE clause is used to specify join criteria and possibly other subsetting criteria. When the conditions are met, the rows are displayed in the output.

```
proc sql;
select sales mgmt.Employee_ID,
  Employee_Name,
  Job Title,
  Salary,
from orion.sales mgmt,
  orion.employee_addresses
where sales mgmt.Employee_ID =
  employee_addresses.Employee_ID;
quit; WHERE join-condition(s)
<AND other subsetting conditions>
```

![](bbox=[0.615, 0.292, 0.668, 0.303])

A WHERE clause can use logical operators to include join conditions as well as other subsetting conditions.

where sales mgmt.employee_id=employee_addresses.employee_id and Salary > 90000;

# Output: Joining on a Common Variable

PROC SQL Output

| Employee ID | Employee_Name | Employee Job Title | Annual Salary |
|---|---|---|--|
| 121144 | Capachitti, Renee | Sales Manager | $83,505 |
| 121143 | Favaron, Louis | Senior Sales Manager | $95,090 |
| 121145 | Lansberry, Dennis | Sales Manager | $84,260 |
| 121147 | Sneed, Christine | Secretary II | $29,145 |

An inner join is equivalent to a DATA step merge in which both data sets contribute to the merge and include matching observations. The following program is an equivalent process using the SORT procedure and a DATA step: