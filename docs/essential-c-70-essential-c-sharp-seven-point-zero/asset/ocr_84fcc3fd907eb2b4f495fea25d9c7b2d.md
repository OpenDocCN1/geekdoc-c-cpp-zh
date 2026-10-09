occurs whenever department.Id equals employee.EmployeeId. The final tuple parameter specifies a class with int Id, string Name, and Employee Employee items. (Specifying the names in the expression is optional but used here for clarity)

# **LISTING 15.20: Another Inner Join with System.Linq.Enumerable.Join()**

```
```csharp
using System;
using System.Linq;

// ... 

Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;

IEnumerable<long Id, string Name, Employee Employee>> items =
    departments.Join(
        employees,
        department => department.Id,
        employee => employee.DepartmentId,
        (department, employee) => (
            department.Id,
            department.Name,
            employee
        ));

foreach (var item in items)
{
    Console.WriteLine(item.Name);
    Console.WriteLine("\t" + item.Employee); 
}

// ...
```
```

# **OUTPUT 15.8**

```
```
Corporate
	Mark Michaelis (Chief Computer Nerd)
Human Resources
	Anne Beard (HR Director)
Engineering
	Michael Stokesbary (Senior Computer Wizard)
Engineering
	Brian Jones (Enterprise Integration Guru)
Engineering
	Kevin Bost (Programmer Extraordinaire)
Engineering
	Thomas Heavey (Software Architect)
Information Technology
	Pat Dever (Enterprise Architect)
Philanthropy
	Eric Edmonds (Philanthropy Coordinator)
```
```