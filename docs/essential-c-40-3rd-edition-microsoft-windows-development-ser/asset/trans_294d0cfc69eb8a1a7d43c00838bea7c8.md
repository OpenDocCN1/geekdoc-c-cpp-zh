

列表中的数量等于员工总数——每个员工只出现一次（每个员工都被认为是规范化的）。输出 14.8 如下。

### 清单 14.21: 使用 System.Linq.Enumerable.Join() 进行内部连接

```
using System;
using System.Linq;
// ...
Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;
var items = employees.Join(
 departments,
 employee => employee.DepartmentId,
 department => department.Id,
 (employee, department) => new
 {
 employee.Id,
 employee.Name,
 employee.Title,
 Department = department
 });
foreach (var item in items)
{
 Console.WriteLine("{0} ({1})",
 item.Name, item.Title);
 Console.WriteLine("\t" + item.Department);
}
// ...
```

### 输出 14.8:

```
Mark Michaelis (Chief Computer Nerd)
Corporate
Michael Stokesbary (Senior Computer Wizard)
Engineering
Brian Jones (Enterprise Integration Guru)
Engineering
Jewel Flores (Bookkeeper Extraordinaire)
Finance
Robert Stokesbary (Expert Mainframe Engineer)
Information Technology
Paul R. Bramsman (Programmer Extraordinaire)
Engineering
Thomas Heavey (Software Architect)
Engineering
John Michaelis (Inventor)
Research
```

Join() 的第一个参数名为 inner。它指定 employees 连接到的集合 departments。接下来的两个参数是 lambda 表达式，用于指定两个集合如何连接。employee => employee.DepartmentId（参数名为 outerKeySelector）标识每个员工的键将是 DepartmentId。下一个 lambda 表达式 (department => department.Id) 将 Department 的 Id 属性指定为键。换句话说，对于每个员工，连接一个部门，其中 employee.DepartmentId 等于 department.Id。最后一个参数是匿名类型，即所选的结果项。在此示例中，它是一个带有 Employee 的 Id、Name 和 Title 以及带有连接部门对象的 Department 属性的类。

请注意在输出中，Engineering 出现多次——CorporateData 中每个员工一次。在此示例中，Join() 调用在所有部门和所有员工之间生成笛卡尔积，这样每当两个集合中都存在记录且指定的部门 ID 相同时，就会创建一条新记录。这种连接类型是内部连接。

数据也可以反向连接，使部门连接到每个员工，以列出每个部门到员工的匹配。请注意，输出中的记录数多于部门数，因为每个部门都有多个员工，且输出为每个匹配生成一条记录。如前所述，Engineering 部门出现多次，每个员工一次。

清单 14.22 和输出 14.9 中的代码与清单 14.21 中的代码类似，只是对象 Departments 和 Employees 颠倒了。传递给 Join() 的第一个参数是 employees，指示部门连接到的对象。接下来的两个参数是 lambda 表达式，用于指定两个集合如何连接：部门使用 department => department.Id，员工使用 employee => employee.DepartmentId。与之前一样，每当 department.Id 等于 employee.EmployeeId 时就会发生连接。最后一个匿名类型参数指定一个带有 int Id、string Name 和 Employee Employee 属性的类。

### 清单 14.22: 使用 System.Linq.Enumerable.Join() 的另一个内部连接

```
using System;
using System.Linq;
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
    Console.WriteLine("{0}",
        item.Name);
    Console.WriteLine("\t" + item.Employee);
}
// ...
```

### 输出 14.9:

```
Corporate
    Mark Michaelis (Chief Computer Nerd)
Finance
    Jewel Flores (Bookkeeper Extraordinaire)
Engineering
    Michael Stokesbary (Senior Computer Wizard)
    Marian Jones (Enterprise Integration Guru)
    Paul R. Bramsman (Programmer Extraordinaire)
Engineering
Information Technology
    Robert Stokesbary (Expert Mainframe Engineer)
Research
    John Michaelis (Inventor)
```

## 使用 GroupBy() 对结果进行分组

除了对对象集合进行排序和连接之外，您经常可能希望将具有相似特征的对象分组在一起。对于员工数据，您可能希望按部门、地区、职位等对员工进行分组。清单 14.23 展示了如何使用 GroupBy() 标准查询运算符来执行此操作（请参阅输出 14.10 以查看输出）。

### 清单 14.23: 使用 System.Linq.Enumerable.GroupBy() 对项目进行分组

```
using System;
using System.Linq;

// ...

IEnumerable<Employee> employees = CorporateData.Employees;

IEnumerable<IGrouping<int, Employee>> groupedEmployees =
    employees.GroupBy(employee => employee.DepartmentId);

foreach (IGrouping<int, Employee> employeeGroup in
    groupedEmployees)
{
    Console.WriteLine();
    foreach (Employee employee in employeeGroup)
    {
        Console.WriteLine("\t" + employee);
    }
    Console.WriteLine(
        "\tCount: " + employeeGroup.Count());
}

// ...
```

### 输出 14.10:

```
Mark Michaelis (Chief Computer Nerd)
Count: 1

Michael Stokesbary (Senior Computer Wizard)
Brian Jones (Enterprise Integration Guru)
Paul R. Bramsen (Programmer Extraordinaire)
Thomas Heavey (Software Architect)
Count: 4

Jewel Flores (Bookkeeper Extraordinaire)
Count: 1

Robert Stokesbary (Expert Mainframe Engineer)
Count: 1

John Michaelis (Inventor)
Count: 1
```

请注意，GroupBy() 调用输出的项类型为 IGrouping<TKey, TElement>，它具有一个属性，用于查询分组的键（employee.DepartmentId）。但是，它没有用于组内项的属性。相反，IGrouping<TKey, TElement> 派生自 IEnumerable<T>，允许使用 foreach 语句枚举组内的项，或将数据聚合为诸如项计数（employeeGroup.Count()）之类的内容。

## 使用 GroupJoin() 实现一对多关系

清单 14.21 和清单 14.22 几乎相同。只需更改匿名类型定义，任何 GroupJoin() 调用都可以生成相同的输出。在尝试创建员工列表时，清单 14.21 提供了正确的结果。department 最终成为表示连接员工的每个匿名类型的属性。但是，清单 14.22 并非最佳。考虑到对集合的支持，部门的首选表示形式应包含员工集合，而不是针对每个部门-员工关系的单个匿名类型记录。清单 14.24 演示了这一点；输出 14.11 显示了首选输出。

### 清单 14.24: 使用 System.Linq.Enumerable.GroupJoin() 创建子集合

```
using System;
using System.Linq;
// ...
Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;
var items = departments.GroupJoin(
    employees,
    department => department.Id,
    employee => employee.DepartmentId,
    (department, departmentEmployees) => new
    {
        department.Id,
        department.Name,
        Employees = departmentEmployees
    });

foreach (var item in items)
{
    Console.WriteLine("{0}",
        item.Name);
    foreach (Employee employee in item.Employees)
    {
        Console.WriteLine("\t" + employee);
    }
}

// ...
```

### 输出 14.11:

```
Corporate
Mark Michaelis (Chief Computer Nerd)
Finance
Jewel Flores (Bookkeeper Extraordinaire)
Engineering
Michael Stokesbary (Senior Computer Wizard)
Brian Jones (Enterprise Integration Guru)
Paul R. Bramsman (Programmer Extraordinaire)
Thomas Heavey (Software Architect)
Information Technology
Robert Stokesbary (Expert Mainframe Engineer)
Research
John Michaelis (Inventor)
```

为了实现首选结果，我们使用 System.Linq.Enumerable 的 GroupJoin() 方法。参数与清单 14.21 中的相同，只是所选的最终匿名类型不同。在清单 14.21 中，lambda 表达式的类型为 Func<Department, IEnumerable<Employee>, TResult>，其中 TResult 是所选的匿名类型。请注意，我们使用第二个类型参数 (IEnumerable<Employee>) 将每个部门的员工集合投影到结果部门匿名类型上。

（熟悉 SQL 的读者会注意到，与 Join() 不同，GroupJoin() 没有 SQL 等价物，因为 SQL 返回的数据是基于记录的，而不是分层的。）

