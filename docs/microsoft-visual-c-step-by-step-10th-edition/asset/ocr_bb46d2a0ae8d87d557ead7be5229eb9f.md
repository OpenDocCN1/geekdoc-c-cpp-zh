```
// var employeesByDept = empTree.GroupBy(e => e.Department);
var employeesByDept = from e in empTree
group e by e.Department;
```