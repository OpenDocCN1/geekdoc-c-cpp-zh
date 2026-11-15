```
// ...
Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;

var items = departments.Join(
    employees,
    department => department.Id,
    employee => employee.DepartmentId,
    (department, employee) => new
    {
        department.Id,
        department.Name,
        Employee = employee
    });

foreach (var item in items)
{
    Console.WriteLine("0"),
    item.Name);
    Console.WriteLine("\t" + item.Employee);
}
// ...
```

OUTPUT 14.9:

```
Corporate
Finance     Mark Michaelis (Chief Computer Nerd)
Jewel Floch (Bookkeeper Extraordinaire)
Engineering Michael Stokesbary (Senior Computer Wizard)
Engineering Marian Jones (Enterprise Integration Guru)
Engineering Paul R. Bramsman (Programmer Extraordinaire)
Engineering
Information Technology Robert Stokesbary (Expert Mainframe Engineer)
Research    John Michaelis (Inventor)
```

# Grouping Results with GroupBy()

In addition to ordering and joining a collection of objects, frequently you might want to group objects with like characteristics together. For the employee data, you might want to group employees by department,