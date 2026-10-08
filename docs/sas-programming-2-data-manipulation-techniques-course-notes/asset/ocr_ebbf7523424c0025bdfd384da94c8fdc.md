# Assigning an Alias for a SAS Table

You can specify an alias for a SAS table. The alias can replace the table name in a query. An alias can be any valid SAS name.

```
proc sql;
select s.Employee_ID, Employee_Name,
Job Title, Salary
from orion.sales mgmt as s,
orion.employee addresses as a
where s.Employee_ID=a.Employee_ID;
FROM SAS-table-1 <AS> alias-1,
SAS-table-2 <AS> alias-2 ...
```

# Output: Assigning an Alias for a SAS Table

PROC SQL Output

| Employee ID | Employee_Name | Employee Job Title | Annual Salary |
|---|---|---|--|
| 121144 | Capachitti, Renee | Sales Manager | $83,505 |
| 121143 | Favaron, Louis | Senior Sales Manager | $95,090 |
| 121145 | Lansberry, Dennis | Sales Manager | $84,260 |
| 121147 | Sneed, Christine | Secretary II | $29,145 |