Note that the items output from a `GroupBy()` call are of type `IGrouping<TKey, TElement>`, which has a property for the key that the query is grouping on (`employee.DepartmentId`). However, it does not have a property for the items within the group. Rather, `IGrouping<TKey, TElement>` derives from `IEnumerable<>`, allowing for enumeration of the items within the group using a `foreach` statement or for aggregating the data into something such as a count of items (`employeeGroup.Count()`).

# **Implementing a One-to-Many Relationship with `GroupJoin()`**

Listings 15.19 and 15.20 are virtually identical. Either `Join()` call could have produced the same output just by changing the tuple definition. When trying to create a list of employees, Listing 15.19 provides the correct result. `Department` ends up as an item of both tuples representing the joined employee. However, Listing 15.20 is not ideal. Given support for collections, a preferable representation of a department would have a collection of employees rather than a single tuple for each department–employee relationship. Listing 15.22 demonstrates; Output 15.10 shows the preferred output.

# **LISTING 15.22: Creating a Child Collection with System.Linq.Enumerable.GroupJoin()**

```
```
using System;
using System.Linq;

// ...

Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;

IEnumerable<(long Id, string Name, IEnumerable<Employee> Employees)>
items =
    departments.GroupJoin(
        employees,
        department => department.Id,
        employee => employee.DepartmentId,
        (department, departmentEmployees) => (
            department.Id,
            department.Name,
            departmentEmployees
        )
);

foreach (var item in items)
{
    Console.WriteLine(item.Name);
}
```
```