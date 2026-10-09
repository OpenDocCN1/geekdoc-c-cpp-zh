

外圈包含所有专利。交集部分同时包括发明人和专利，每存在一次发明人与专利的匹配，便会生成一条连线。如图所示，每位发明人可能拥有多项专利，而每项专利可以有一位或多位发明人。每项专利都有发明人，但在某些情况下，发明人尚未拥有专利。

![](img/ef6a8a417630b222bfb3f3b949facff0_665_0.png)

# 图 15.3：发明人与专利集合的维恩图

将交集中的发明人与专利进行匹配即为内连接。其结果是一个发明人/专利对的集合，在该集合中，每一对既存在专利也存在发明。左外连接包含左圆内的所有项，无论它们是否有对应的专利。在此示例中，右外连接与内连接相同，因为不存在没有发明人的专利。此外，左与右的指定是任意的，因此左右外连接之间实际上没有区别。然而，全外连接将包含两侧外部的记录；执行全外连接相对少见。

发明人与专利关系中的另一个重要特征是，它是一种多对多关系。每项单独的专利可以有一位或多位发明人（例如，飞行器的发明既归于奥维尔·莱特也归于威尔伯·莱特）。此外，每位发明人也可以拥有一项或多项专利（例如，本杰明·富兰克林既发明了双光眼镜也发明了留声机）。

另一种常见的关系是**一对多**关系。例如，公司的某个部门可能有许多员工。然而，每位员工在同一时间只能隶属于一个部门。（不过，与常见的一对多关系一样，加入时间因素后，它们可转化为多对多关系。某位员工可能从一个部门调到另一个部门，因此，随着时间推移，她可能与多个部门相关联，从而构成另一个多对多关系。）

代码清单 15.18 提供了员工和部门数据的示例清单，输出 15.6 展示了结果。

**代码清单 15.18：示例员工和部门数据**

```csharp
public class Department
{
    public long Id { get; set; }
    public string Name { get; set; }
    public override string ToString()
    {
        return Name;
    }
}

public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Title { get; set; }
    public int DepartmentId { get; set; }
    public override string ToString()
    {
        return $"{ Name } ({ Title })";
    }
}

public static class CorporateData
{
    public static readonly Department[] Departments =
        new Department[]
        {
            new Department(){
                Name="Corporate", Id=0},
            new Department(){
                Name="Human Resources", Id=1},
            new Department(){
                Name="Engineering", Id=2},
            new Department(){
                Name="Information Technology",
                Id=3},
            new Department(){
                Name="Philanthropy",
                Id=4},
            new Department(){
                Name="Marketing",
                Id=5},
        };

    public static readonly Employee[] Employees = new Employee[]
    {
        new Employee(){
            Name="Mark Michaelis",
            Title="Chief Computer Nerd",
            DepartmentId = 0},
        new Employee(){
            Name="Michael Stokesbury",
            Title="Senior Computer Wizard",
            DepartmentId=2},
        new Employee(){
            Name="Brian Jones",
            Title="Enterprise Integration Guru",
            DepartmentId=2},
        new Employee(){
            Name="Anne Beard",
            Title="HR Director",
            DepartmentId=1},
        new Employee(){
            Name="Pat Dever",
            Title="Enterprise Architect",
            DepartmentId = 3},
        new Employee(){
            Name="Kevin Bost",
            Title="Programmer Extraordinaire",
            DepartmentId = 2},
        new Employee(){
            Name="Thomas Heavey",
            Title="Software Architect",
            DepartmentId = 2},
        new Employee(){
            Name="Eric Edmonds",
            Title="Philanthropy Coordinator",
            DepartmentId = 4}}
};

class Program
{
    static void Main()
    {
        IEnumerable<Department> departments =
            CorporateData.Departments;
        Print(departments);

        Console.WriteLine();

        IEnumerable<Employee> employees =
            CorporateData.Employees;
        Print(employees);
    }

    private static void Print<T>(IEnumerable<T> items)
    {
        foreach (T item in items)
        {
            Console.WriteLine(item);
        }
    }
}
```

> **输出 15.6**
>
> 公司总部
> 人力资源
> 工程
> 信息技术
> 慈善
> 市场营销
>
> 马克·迈克尔伊斯 (首席计算机极客)
> 迈克尔·斯托克斯伯里 (高级计算机巫师)
> 布莱恩·琼斯 (企业集成大师)
> 安妮·比尔德 (人力资源总监)
> 帕特·德弗 (企业架构师)
> 凯文·博斯特 (卓越程序员)
> 托马斯·希维 (软件架构师)
> 埃里克·埃德蒙兹 (慈善协调员)

我们在下一节关于数据连接的示例中使用这些数据。

## 使用 Join() 执行内连接

在客户端的对象世界中，对象之间的关系通常已经建立。例如，文件与其所在目录之间的关系分别通过 `DirectoryInfo.GetFiles()` 方法和 `FileInfo.Directory` 方法预先建立。然而，对于从非对象存储加载的数据，这种情况并不常见。相反，需要将数据连接起来，以便能够以符合数据逻辑的方式从一种对象导航到另一种对象。

以员工和公司部门为例。在代码清单 15.19 中，我们将每位员工与其所在部门连接，然后列出每位员工及其对应的部门。由于每位员工仅属于一个（且恰好一个）部门，因此列表中的总条目数等于员工总数——每位员工仅出现一次（即每位员工都处于规范化状态）。输出 15.7 展示了结果。

**代码清单 15.19：使用 System.Linq.Enumerable.Join() 的内连接**

```csharp
using System;
using System.Linq;

// ... 

Department[] departments = CorporateData.Departments;
Employee[] employees = CorporateData.Employees;

IEnumerable<(int Id, string Name, string Title, Department Department)> items =
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
        $"{ item.Name } ({ item.Title })");
    Console.WriteLine("\t" + item.Department);
}

// ...
```

**输出 15.7**

```text
马克·迈克尔伊斯 (首席计算机极客)
    公司总部
迈克尔·斯托克斯伯里 (高级计算机巫师)
    工程
布莱恩·琼斯 (企业集成大师)
    工程
安妮·比尔德 (人力资源总监)
    人力资源
帕特·德弗 (企业架构师)
    信息技术
凯文·博斯特 (卓越程序员)
    工程
托马斯·希维 (软件架构师)
    工程
埃里克·埃德蒙兹 (慈善协调员)
    慈善
```

Join() 的第一个参数名为 inner。它指定了员工所连接的集合，即 departments。接下来的两个参数是 Lambda 表达式，用于指定两个集合如何连接：employee => employee.DepartmentId（参数名为 outerKeySelector）表明在每个 employee 中，键将是 DepartmentId。下一个 Lambda 表达式（department => department.Id）将 Department 的 Id 属性指定为键——换句话说，对于每位员工，连接 DepartmentId 等于 department.Id 的部门。最后一个参数是选定的结果项。在此情况下，它是一个元组，包含 Employee 的 Id、Name 和 Title，以及包含已连接部门对象的 Department 属性。

注意在输出中，Engineering 出现了多次——CorporateData 中的每位员工各出现一次。在这种情况下，Join() 调用在所有部门和所有员工之间产生笛卡尔积，使得每当两个集合中均存在记录且指定的部门 ID 相同时，就会创建一条新记录。这种连接类型是内连接。

数据也可以反向连接，使部门连接到每位员工，以列出每个部门到员工的匹配项。注意输出中的记录数多于部门数：每个部门有多名员工，输出是每条匹配的记录。正如我们之前所见，Engineering 部门出现多次，每位员工各出现一次。

代码清单 15.20 中的代码（产生输出 15.8）与代码清单 15.19 类似，只是对象 Departments 和 Employees 的顺序被颠倒了。Join() 的第一个参数是 employees，表明 departments 连接到什么。接下来的两个参数是 Lambda 表达式，用于指定两个集合如何连接：departments 使用 department => department.Id，employees 使用 employee => employee.DepartmentId。与之前一样，连接

