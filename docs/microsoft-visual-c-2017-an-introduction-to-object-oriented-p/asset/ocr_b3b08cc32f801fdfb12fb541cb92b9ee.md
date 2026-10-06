(continued)

```
while(recordIn != null) 
{
    fields = recordIn.Split(DELIM);
    emp.EmpNum = Convert.ToInt32(fields[0]);
    emp.Name = fields[1];
    emp.Salary = Convert.ToDouble(fields[2]);
    if(emp.Salary >= minSalary)
        WriteLine("{0
```

Figure 14-18 The FindEmployees program

![](bbox=[0.105, 0.506, 0.658, 0.893])

Figure 14-19 Typical execution of the FindEmployees program

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 02-200-202