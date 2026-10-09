Consider the example of employees and company departments. In Listing 15.19, we join each employee to his or her department and then list each employee with his or her corresponding department. Since each employee belongs to only one (and exactly one) department, the total number of items in the list is equal to the total number of employees—each employee appears only once (each employee is said to be normalized). Output 15.7 shows the results.

# **LISTING 15.19: An Inner Join Using System.Linq.Enumerable.Join()**

```
```csharp
using System;
using System.Linq;

// ... 

Department[ ] departments = CorporateData.Departments;
Employee[ ] employees = CorporateData.Employees;

IEnumerable< int Id, string Name, string Title, Department Department> items =
    employees.Join(
        departments,
        employee => employee.DepartmentId,
        department => department.Id,
        (employee, department) => (
            employee.Id,
            employee.Name,
            employee.Title,
            department
    ));

foreach (var item in items)
{
    Console.WriteLine(
        $"{ item.Name } { item.Title }");
    Console.WriteLine("\t" + item.Department);
}

// ...
```
```

# **OUTPUT 15.7**

```
```
Mark Michaelis (Chief Computer Nerd)
    Corporate
Michael Stokesbary (Senior Computer Wizard)
    Engineering
Brian Jones (Enterprise Integration Guru)
    Engineering
Anne Beard (HR Director)
    Human Resources
```
```

*continues*