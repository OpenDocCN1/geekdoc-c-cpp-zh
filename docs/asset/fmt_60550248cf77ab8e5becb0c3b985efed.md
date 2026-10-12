
`Join()` 的第一个参数名为 `inner`。它指定了员工所连接的集合，即 `departments`。接下来的两个参数是 Lambda 表达式，用于指定两个集合如何连接：`employee => employee.DepartmentId`（参数名为 `outerKeySelector`）表明在每个 `employee` 中，键将是 `DepartmentId`。下一个 Lambda 表达式（`department => department.Id`）将 `Department` 的 `Id` 属性指定为键——换句话说，对于每位员工，连接 `DepartmentId` 等于 `department.Id` 的部门。最后一个参数是选定的结果项。在此情况下，它是一个元组，包含 `Employee` 的 `Id`、`Name` 和 `Title`，以及包含已连接部门对象的 `Department` 属性。

注意在输出中，`Engineering` 出现了多次——`CorporateData` 中的每位员工各出现一次。在这种情况下，`Join()` 调用在所有部门和所有员工之间产生笛卡尔积，使得每当两个集合中均存在记录且指定的部门 ID 相同时，就会创建一条新记录。这种连接类型是内连接。

数据也可以反向连接，使部门连接到每位员工，以列出每个部门到员工的匹配项。注意输出中的记录数多于部门数：每个部门有多名员工，输出是每条匹配的记录。正如我们之前所见，`Engineering` 部门出现多次，每位员工各出现一次。

代码清单 15.20 中的代码（产生输出 15.8）与代码清单 15.19 类似，只是对象 `Departments` 和 `Employees` 的顺序被颠倒了。`Join()` 的第一个参数是 `employees`，表明 `departments` 连接到什么。接下来的两个参数是 Lambda 表达式，用于指定两个集合如何连接：`departments` 使用 `department => department.Id`，`employees` 使用 `employee => employee.DepartmentId`。与之前一样，连接

只要 `department.Id` 等于 `employee.EmployeeId`，就会发生这种情况。最终的元组参数指定了一个类，其中包含 `int Id`、`string Name` 和 `Employee Employee` 项。（在表达式中指定名称是可选的，但此处用于增强清晰度。）

## 清单 15.20：使用 System.Linq.Enumerable.Join() 进行另一种内部连接

```csharp
using System;
using System.Linq;
// ... 
Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;
IEnumerable<(long Id, string Name, Employee Employee)> items =
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

## 输出 15.8

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

## 使用 GroupBy() 对结果进行分组

除了对对象集合进行排序和连接外，您通常可能还需要将具有相似特征的对象进行分组。对于员工数据，您可能希望按部门、地区、职位等对员工进行分组。清单 15.21 展示了如何使用 `GroupBy()` 标准查询运算符来实现这一点（参见输出 15.9 以查看输出）。

## 清单 15.21：使用 System.Linq.Enumerable.GroupBy() 对项目进行分组

```csharp
using System;
using System.Linq;
// ...
IQueryable<Employee> employees = CorporateData.Employes;
IQueryable<IGrouping<int, Employee>> groupedEmployees =
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
        "\tCount: " + employeeGroup.Count());
}
// ...
```

## 输出 15.9

```
Mark Michaelis (Chief Computer Nerd)
    Count: 1
Michael Stokesbary (Senior Computer Wizard)
Brian Jones (Enterprise Integration Guru)
Kevin Bost (Programmer Extraordinaire)
Thomas Heavey (Software Architect)
    Count: 4
Anne Beard (HR Director)
    Count: 1
Pat Dever (Enterprise Architect)
    Count: 1
Eric Edmonds (Philanthropy Coordinator)
    Count: 1
```

请注意，`GroupBy()` 调用输出的项类型为 `IGrouping<TKey, TElement>`，它有一个用于查询分组依据的键的属性（`employee.DepartmentId`）。但是，它没有用于组内项的属性。相反，`IGrouping<TKey, TElement>` 继承自 `IEnumerable<>`，允许使用 `foreach` 语句枚举组内的项，或将数据聚合为某种形式，例如项的计数（`employeeGroup.Count()`）。

## 使用 `GroupJoin()` 实现一对多关系

清单 15.19 和 15.20 几乎相同。任何 `Join()` 调用只需更改元组定义即可产生相同的输出。在尝试创建员工列表时，清单 15.19 提供了正确的结果。`Department` 最终成为代表连接后的员工的两个元组中的项。然而，清单 15.20 并不理想。鉴于对集合的支持，部门的更可取表示形式应该包含一个员工集合，而不是为每个部门–员工关系提供一个单独的元组。清单 15.22 展示了这一点；输出 15.10 展示了理想的输出结果。

## 清单 15.22：使用 System.Linq.Enumerable.GroupJoin() 创建子集合

```csharp
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
    foreach (Employee employee in item.Employees)
    {
      Console.WriteLine("\t" + employee);
    }
}
// ...
```

## 输出 15.10

```
Corporate
   Mark Michaelis (Chief Computer Nerd)
Human Resources
   Anne Beard (HR Director)
Engineering
   Michael Stokesbary (Senior Computer Wizard)
   Brian Jones (Enterprise Integration Guru)
   Kevin Bost (Programmer Extraordinaire)
   Thomas Heavey (Software Architect)
Information Technology
   Pat Dever (Enterprise Architect)
Philanthropy
   Eric Edmonds (Philanthropy Coordinator)
```

为了达到理想的结果，我们使用 `System.Linq.Enumerable` 的 `GroupJoin()` 方法。参数与清单 15.19 中的相同，除了最终选择的元组。在清单 15.19 中，Lambda 表达式的类型为 `Func<Department, IEnumerable<Employee>>`，`(long Id, string Name, IEnumerable<Employee> Employees)`。请注意，我们使用第二个类型参数（`IEnumerable<Employee>`）将每个部门的员工集合投影到结果部门元组上；因此，结果集合中的每个部门都包含一个员工列表。

（熟悉 SQL 的读者会注意到，与 `Join()` 不同，`GroupJoin()` 没有 SQL 等效方法，因为 SQL 返回的数据是基于记录的，而不是分层的。）

## 高级主题

### 使用 GroupJoin() 实现外部连接

前面的内部连接是*等值连接*，因为它们基于键的等效评估。只有当两个集合中都有对象时，记录才会出现在结果集合中。然而，在某些情况下，即使对应的对象不存在，创建记录也是可取的。例如，仅仅因为市场部没有任何员工，而从最终部门列表中排除市场部可能并不合适，如果我们将其包含在内并附带一个空员工列表会更好。为了实现这一点，我们使用 `GroupJoin()` 和 `SelectMany()` 以及 `DefaultIfEmpty()` 的组合来执行左外部连接。这在清单 15.23 和输出 15.11 中进行了演示。

## 清单 15.23：使用 SelectMany() 和 GroupJoin() 实现外部连接

```csharp
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
    }).SelectMany(
    departmentRecord =>
        departmentRecord.Employees.DefaultIfEmpty(),
    (departmentRecord, employee) => new
    {
        departmentRecord.Id,
        departmentRecord.Name,
        Employees =
            departmentRecord.Employees
    }).Distinct();
foreach (var item in items)
{
    Console.WriteLine(item.Name);
    foreach (Employee employee in item.Employees)
    {
        Console.WriteLine("\t" + employee);
    }
}
// ...
```

## 输出 15.11

```
Corporate
    Mark Michaelis (Chief Computer Nerd)
Human Resources
    Anne Beard (HR Director)
Engineering
    Michael Stokesbary (Senior Computer Wizard)
    Brian Jones (Enterprise Integration Guru)
    Kevin Bost (Programmer Extraordinaire)
    Thomas Heavey (Software Architect)
Information Technology
    Pat Dever (Enterprise Architect)
Philanthropy
    Eric Edmonds (Philanthropy Coordinator)
Marketing
```

## 调用 SelectMany()

在某些情况下，您可能拥有集合的集合。清单 15.24 提供了此类场景的一个示例。`teams` 数组包含两个团队，每个团队都有一个包含球员姓名的字符串数组。

## 清单 15.24：调用 SELECTMANY()

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
// ...
(string Team, string[] Players)[] worldCup2006Finalists = new[]
{
    (
        TeamName: "France",
        Players: new string[]
        {
            "Fabien Barthez", "Gregory Coupet",
            "Mickael Landreau", "Eric Abidal",
            "Jean-Alain Boumsong", "Pascal Chimbonda",
            "William Gallas", "Gael Givet",
            "Willy Sagnol", "Mikael Silvestre",
            "Lilian Thuram", "Vikash Dhorasoo",
            "Alou Diarra", "Claude Makelélé",
            "Florent Malouda", "Patrick Vieira",
            "Zinedine Zidane", "Djibril Cisse",
            "Thierry Henry", "Franck Ribery",
            "Louis Saha", "David Trezeguet",
            "Sylvain Wiltord",
        }
```
