```
Pat Dever (Enterprise Architect)
Information Technology
Kevin Bost (Programmer Extraordinaire)
Engineering
Thomas Heavey (Software Architect)
Engineering
Eric Edmonds (Philanthropy Coordinator)
Philanthropy
```

The first parameter for Join() has the name inner. It specifies the collection, departments, that employees joins to. The next two parameters are lambda expressions that specify how the two collections will connect: employee => employee.DepartmentId (with a parameter name of outerKeySelector) identifies that on each employee, the key will be DepartmentId. The next lambda expression (department => department.Id) specifies the Department's Id property as the key—in other words, for each employee, join a department where employee.DepartmentId equals department.Id. The last parameter is the resultant item that is selected. In this case, it is a tuple with Employee's Id, Name, and Title as well as a Department property with the joined department object.

Notice in the output that Engineering appears multiple times—once for each employee in CorporateData. In this case, the Join() call produces a Cartesian product between all the departments and all the employees such that a new record is created for every case where a record exists in both collections and the specified department IDs are the same. This type of join is an inner join.

The data could also be joined in reverse, such that department joins to each employee to list each department-to-employee match. Notice that the output includes more records than there are departments: There are multiple employees for each department, and the output is a record for each match. As we saw before, the Engineering department appears multiple times, once for each employee.

The code in Listing 15.20 (which produces Output 15.8) is similar to that in Listing 15.19, except that the objects, Departments and Employees, are reversed. The first parameter to Join() is employees, indicating what departments joins to. The next two parameters are lambda expressions that specify how the two collections will connect: department => department.Id for departments and employee => employee.DepartmentId for employees. As before, a join