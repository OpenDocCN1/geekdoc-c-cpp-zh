
`IEnumerable<string>` `customerFirstNames` = `customers`
    .`Select`(cust => cust.`FirstName`);

```
你可以通过 `from` 和 `select` 查询运算符来重述此语句，如下：
```

点击此处查看代码图像

```
var customerFirstNames = from cust in customers
select cust.FirstName;
```

在编译时，C# 编译器会将此表达式解析为相应的 `Select` 方法。`from` 运算符为源集合定义了一个别名，`select` 运算符指定了使用该别名要检索的字段。结果是一个包含客户第一个名字的可枚举集合。如果你熟悉 SQL，请注意 `from` 运算符出现在 `select` 运算符之前。

沿着同样的思路，为了获取每个客户的姓和名，你可以使用以下语句。（你可能想参考之前基于 `Select` 扩展方法的相同示例。）

点击此处查看代码图像

```
var customerNames = from cust in customers
select new { cust.FirstName, cust.LastName };
```

使用 `where` 运算符过滤数据。以下示例显示了如何根据 "United States" 返回 `addresses` 数组中的公司名称：

点击此处查看代码图像

```
var usCompanies = from a in addresses
where String.Equals(a.Country, "United States")
select a.CompanyName;
```

对数据进行排序，使用 `orderby` 运算符，如下：

点击此处查看代码图像

```
var companyNames = from a in addresses
orderby a.CompanyName
select a.CompanyName;
```

你可以通过以下方式使用 `group` 运算符对数据进行分组：

点击此处查看代码图像

```
var companiesGroupedByCountry = from a in addresses group by a.Country;
```

注意显示分组数据的示例没有提供 `select` 运算符。你可以使用与之前的示例相同的代码遍历结果：

点击此处查看代码图像

```
foreach (var companiesPerCountry in companiesGroupedByCountry)
{
    Console.WriteLine($"{companiesPerCountry.Key}\t{companiesPerCountry.Count()} companies");
    foreach (var company in companiesPerCountry)
    {
        Console.WriteLine("\t{company.CompanyName}");
    }
}
```

对可枚举集合调用汇总函数：

点击此处查看代码图像

```
int numberOfCompanies = (from a in addresses select a.CompanyName).Count();
```

注意将表达式括在括号中。如果你想忽略重复值，请使用 `Distinct` 方法：

点击此处查看代码图像

```
int numberOfCountries = (from a in addresses select a.Country).Distinct().Count();
```

> 提示
在某些情况下，你可能计算集合中的行数，而不是集合中所有字段的值。在这种情况下，你可以直接对原始集合调用 `Count` 方法：

点击此处查看代码图像

```
int numberOfCompanies = addresses.Count();
```

你可以使用 `join` 运算符根据公共键合并两个集合。以下示例通过 `join` 运算符重述了返回每个集合中 `CompanyName` 列的客户和地址：

### 注意
LINQ 目前支持等值连接（基于等等的连接）。如果你是一个习惯于 SQL 的数据库开发者，可能熟悉基于 `>` 和 `<` 等运算符的连接，但 LINQ 未提供这些功能。

点击此处查看代码图像

```
var countriesAndCustomers = from a in addresses
join c in customers
on a.CompanyName equals c.CompanyName
select new { c.FirstName, c.LastName, a.Country };
```

### 注意
与 SQL 不同，LINQ 表达式中 `on` 子句的顺序很重要。你必须将你正在连接的项目（引用 `from` 子句中的集合数据）放在 `equals` 运算符的左侧，将与之连接的项目（引用 `join` 子句中的集合数据）放在右侧。

LINQ 提供了许多其他汇总信息、连接和搜索数据的方法。本节涵盖了最常用的功能。例如，LINQ 提供了 `Intersect` 和 `Union` 方法，你可以用它们执行集合操作。它还提供了 `Any` 和 `All` 等方法，用于判断集合中的项是否匹配指定的谓词。你可以使用 `Take` 和 `Skip` 方法划分可枚举集合。更多信息，请参见 Visual Studio 提供的文档中的 LINQ 部分。

# 查询 Tree<T> 对象中的数据

在本章到为止看到的示例显示了如何查询数组中的数据。任何实现 `IEnumerable<T>` 接口的集合类都可以相同的技术。在下面的练习中，你将为公司的员工建模创建一个新类。你将创建一个员工集合的 `BinaryTree` 对象，然后使用 LINQ 查询这些信息。你最初将直接调用 Linq 方法，然后修改代码使用查询运算符。

> 使用扩展方法从 BinaryTree 获取数据

1. 启动 Visual Studio 2022，如果它尚未运行。
2. 打开 `QueryTree` 解决方案，它位于文档文件夹中的 `\Microsoft Press\VCSABS\Chapter21\QueryTree` 文件夹。

解决方案中的项目包含 `Program.cs` 文件，它定义了你在之前的练习中看到的带有 `Main` 和 `doWork` 方法的 `Program` 类。解决方案还包含之前章节看到的 `BinaryTree` 项目副本。
3. 在解决方案资源管理器中，右键点击 `QueryTree` 项目，指向“添加”，然后选择“类”。
4. 在“添加新建项 - QueryTree”对话框中，在名称框中输入 `Employee.cs`，然后选择“添加”。
5. 将以下代码向 `Employee` 类中添加**粗体**的自动属性：

点击此处查看代码图像

```
class Employee
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string Department { get; set; }
    public int Id { get; set; }
}
```

6. 将随后的代码向 `Employee` 类中添加**粗体**的 `ToString` 方法。.NET Framework 中的类型在将对象转换为字符串表示时会使用此方法，例如当使用 `Console.WriteLine` 语句显示它时。

点击此处查看代码图像

```
class Employee : IComparable<Employee>
{
}
```

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

// var ITEmployees =
// empTree.Where(e => String.Equals(e.Department, "IT"));
// .Select(emp => emp) from e in empTree
var ITEmployees =
    where String.Equals(e.Department, "IT")
    select e;

- 3. 注释掉按部门分组员工的语句，并替换为代码所示加粗语句：
```
