
这一步是必要的，因为 `BinaryTree` 类规定其元素必须是“可比较的”。

- 8. 在类定义中，将鼠标悬停在 `IComparable<Employee>` 接口上，选择出现的灯泡图标，然后在上下文菜单中选择“显式实现所有成员”（Implement all members explicitly）。

这生成了 `CompareTo` 方法的默认实现。请记住，当 `BinaryTree` 类在将元素插入树时需要比较元素时，会调用此方法。

- 9. 将 `CompareTo` 方法的主体替换为如下加粗代码。此 `CompareTo` 实现根据 `Employee` 对象的 `Id` 字段来比较 `Employee` 对象。

[点击查看代码图像]

```
int IComparable<Employee>.CompareTo(Employee other)
{
    if (other is null)
    {
        return 1;
    }
    if (this.Id > other.Id)
    {
        return 1;
    }
    if (this.Id < other.Id)
    {
        return -1;
    }
    return 0;
}
```

> 注意
关于 `IComparable<T>` 接口的描述，请参阅第 19 章。

- 10. 在代码编辑器中显示 `BinaryTree` 项目的 `Program.cs` 文件。然后在文件顶部添加以下指示程序：

```
using System.Linq;
using BinaryTree;
```

- 11. 在 `Program` 类的 `doWork` 方法中，删除 `// TODO:` 注释并添加如下加粗语句以构造并填充 `BinaryTree` 类实例：

[点击查看代码图像]

```
static void doWork()
{
    Tree<Employee> empTree = new Tree<Employee>(
        new Employee { Id = 1, FirstName = "Kim", LastName = "Abercrombie", Department = "IT" }
    );
    empTree.Insert(
        new Employee { Id = 2, FirstName = "Jeff", LastName = "Hay", Department = "Marketing" }
    );
    empTree.Insert(
        new Employee { Id = 4, FirstName = "Charlie", LastName = "Herb", Department = "IT" }
    );
    empTree.Insert(
        new Employee { Id = 6, FirstName = "Chris", LastName = "Preston", Department = "Sales" }
    );
    empTree.Insert(
        new Employee { Id = 3, FirstName = "Dave", LastName = "Barnett", Department = "Sales" }
    );
    empTree.Insert(
        new Employee { Id = 5, FirstName = "Tim", LastName = "Litton", Department = "Marketing" }
    );
}
```

- 12. 在 `doWork` 方法末尾添加如下加粗语句。此代码调用 `Select` 方法列出二进制树中找到的部门。

[点击查看代码图像]

```
static void doWork()
{
  Console.WriteLine("List of departments");
  var depts = empTree.Select(d => d.Department);

  foreach (var dept in depts)
  {
    Console.WriteLine($"Department: {dept}");
  }
}
```

- 13. 在“调试”（Debug）菜单中选择“无调试启动”（Start Without Debugging）。

应用程序应该输出以下部门列表：

+ List of departments
Department: IT
Department: Marketing
Department: Sales
Department: IT
Department: Marketing
Department: Sales

每个部门出现两次，是因为每个部门有两个员工。部门的顺序由 `Employee` 类的 `CompareTo` 方法决定，该方法使用员工的 `Id` 属性进行排序。第一个部门对应 Id 值为 1 的员工，第二个部门对应 Id 值为 2 的员工，以此类推。

- 14. 按回车返回 Visual Studio 2022。

- 15. 在 `Program` 类的 `doWork` 方法中，按照示例示例所示修改创建部门枚举集合的语句：

[点击查看代码图像]

```
var depts = empTree.Select(d => d.Department).Distinct();
```

`Distinct` 方法从枚举集合删除删除行。

- 16. 在“调试”菜单中选择“无调试启动”。然后验证应用程序现在只显示一次部门，如下：

```
List of departments
Department: IT
Department: Marketing
Department: Sales
```

- 17. 按回车查看 Visual Studio 2022。

- 18. 在 `doWork` 方法中添加如下加粗语句。此代码块使用 `Where` 方法过滤员工并仅返回 IT 部门的员工。`Select` 方法返回整行而不是投影特定的列。

[点击查看代码 doWork()]

```
static void doWork()
{
    Console.WriteLine("Employees in the IT department");
    var ITEmployees =
        empTree.Where(e => String.Equals(e.Department, "IT"));
```

- 19. 在上一步代码之后，在 `doWork` 方法末尾添加如下加粗代码。此代码使用 `GroupBy` 方法按部门对二进制树中的员工进行分组。外部 `foreach` 语句遍历每个组，显示部门名称。内部 `foreach` 语句显示每个部门员工的姓名。

[点击查看代码图像]

```
static void doWork()
{
    Console.WriteLine("All employees grouped by department");
    var employeesByDept = empTree.GroupBy(e => e.Department);
    foreach (var dept in employeesByDept)
    {
        Console.WriteLine($"Department: {dept.Key}");
        foreach (var emp in dept)
        {
            Console.WriteLine($"\t{emp.FirstName}\t{emp.LastName}");
        }
    }
}
```

- 20. 在“调试”菜单中选择“无调试启动”。验证应用程序的输出如下：

[点击查看代码图像]

+ List of departments
Department: IT
Department: Marketing
Department: Sales

+ Employees in the IT department
Id: 1, Name: Kim Abercrombie, Dept: IT
Id: 4, Name: Charlie Herb, Dept: IT

+ All employees grouped by department
Department: IT
Kim Abercrombie
Charlie Herb
Department: Marketing
Jeff Hay
Tim Litton
Department: Sales
Dave Barnett
Chris Preston

- 21. 按回车返回 Visual Studio 2022。

## 使用查询运算符从 BinaryTree 获取数据

- 1. 在 `doWork` 方法中，注释掉创建部门枚举集合的语句，并替换为如下加粗语句，使用 `from` 和 `select` 运算符：

[点击查看代码图像]

```
// var depts = empTree.Select(d => d.Department).Distinct();
var depts = (from d in empTree
    select d).Distinct();
```

- 2. 注释掉生成 IT 员工枚举集合的语句，并替换为如下加粗代码：

[点击查看代码图像]

```
// var ITEmployees =
// empTree.Where(e => String.Equals(e.Department, "IT"));
// .Select(emp => emp) from e in empTree
var ITEmployees =
    where String.Equals(e.Department, "IT")
    select e;
```

- 3. 注释掉按部门分组员工的语句，并替换为代码所示加粗语句：

[点击查看代码图像]

```
// var employeesByDept = empTree.GroupBy(e => e.Department);
var employeesByDept = from e in empTree
    group by e.Department;
```

- 1. 在“调试”菜单中选择“无调试启动”。然后验证程序的结果与之前一致。

[点击查看代码图像]

+ List of departments
Department: IT
Department: Marketing
Department: Sales
+ Employees in the IT department
Id: 1, Name: Kim Abercrombie, Dept: IT
Id: 4, Name: Charlie Herb, Dept: IT
+ All employees grouped by department
Department: IT
Kim Abercrombie
Charlie Herb
Department: Marketing
Jeff Hay
Tim Litton
Department: Sales
Dave Barnett
Chris Preston

## LINQ 与延迟计算

当你使用 LINQ 定义枚举集合时（无论是使用 LINQ 扩展方法还是使用查询运算符），请记住，应用程序并不是在执行 LINQ 扩展方法时实际构建集合；相反，只有在你遍历它时，才会进行枚举。这意味着在执行 LINQ 查询与检索查询所识别的数据之间，原始集合中的数据可能会发生变化。然而，你将始终获取最新的数据。例如，以下查询（你之前看到的）定义了一个包含美国公司的枚举集合：

