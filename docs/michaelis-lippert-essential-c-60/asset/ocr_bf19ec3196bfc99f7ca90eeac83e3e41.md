# Chapter 14: Collection Interfaces with Standard Query Operators

# OUTPUT 14.9

```
Corporate
    Mark Michaelis (Chief Computer Nerd)
Finance
    Shane Kercheval (Chief Financial Officer)
Engineering
    Michael Stokesbury (Senior Computer Wizard)
Engineering
    Brian Jones (Enterprise Integration Guru)
Engineering
    Kevin Bost (Programmer Extraordinaire)
Engineering
    Thomas Heavy (Software Architect)
Information Technology
    Pat Dever (Enterprise Architect)
Philanthropy
    Eric Edmonds (Philanthropy Coordinator)
```

# Grouping Results with GroupBy()

In addition to ordering and joining a collection of objects, frequently you might want to group objects with like characteristics together. For the employee data, you might want to group employees by department, region, job title, and so forth. Listing 14.24 shows an example of how to do this with the GroupBy() standard query operator (see Output 14.10 to view the output).

# LISTING 14.24: Grouping Items Together Using System.Linq.IEnumerable.GroupBy()

```
using System;
using System.Linq;

// ...

IEnumerable<Employee> employees = CorporateData.Employees;

IEnumerable<IGrouping<int, Employee>> groupedEmployees =
    employees.GroupBy((employee) => employee.DepartmentId);

foreach (IGrouping<int, Employee> employeeGroup in
    groupedEmployees)
{
    Console.WriteLine();
    foreach (Employee employee in employeeGroup)
    {
        Console.WriteLine("\t" + employee);
    }
    Console.WriteLine(
```