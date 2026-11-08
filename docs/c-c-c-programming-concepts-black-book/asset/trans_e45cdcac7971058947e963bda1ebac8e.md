

```csharp
public Employee(int id, string name, string desg)
{
    this.empID = id;
    this.empName = name;
    this.designation = desg;
}
```

在代码清单 19.25 中，我们声明了一个 List 对象，其中包含 Employee 类的对象。在 LINQ 查询的 select 子句中，我们特意将 empID 和 empName 声明为单独的变量，以便后续引用它们。该程序的输出与代码清单 19.24 的输出相同。

## 联接运算符

联接操作基于特定条件将两个给定的关系连接起来。在 LINQ 中，联接操作借助以下两种联接运算符来执行：

- 联接
- 分组联接

C# 提供了 join 关键字，LINQ 查询使用该关键字实现 *联接* 运算符。与 SQL 中的内联接类似，*联接* 运算符也会选择那些满足联接条件的条目。LINQ 中的内联接表示两个集合或集之间的交集区域，如图 19.22 所示：

![](img/43c5f409f9b17790a628c4b4df854b61_660_0.png)

**图 19.22：展示内联接**

代码清单 19.26 展示了一个内联接操作的示例，该示例根据联接谓词将 Employee 类的一个对象与 Project 类的一个对象联接起来：

**代码清单 19.26：** 展示使用 join 关键字的联接操作示例

```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;

class Program
{
    public static void Main()
    {
        List<Employee> empList = new List<Employee>();
        empList.Add(new Employee(100, "James", "Team Member", 123));
        empList.Add(new Employee(200, "Jonathan", "Senior Manager", 124));
        empList.Add(new Employee(300, "Keith", "Team Member", 123));
        empList.Add(new Employee(400, "Jonny", "Manager", 123));
        empList.Add(new Employee(500, "Amy", "Senior Manager", 124));
        empList.Add(new Employee(600, "Leonardo", "Team Member", 123));

        List<Project> projList = new List<Project>();
        projList.Add(new Project(123, "Banking Project"));
        projList.Add(new Project(124, "Insurance Project"));
        var empSel = from emp in empList
                     join proj in projList
                     on emp.projectID equals proj.projectID
                     orderby proj.projectName
                     select new { id = emp.empID, name = emp.empName, projName = proj.projectName };

        foreach (var e in empSel)
        {
            Console.WriteLine("Employee ID: {0} Employee Name: {1} Project Name: {2}",
                e.id, e.name, e.projName);
        }
    }
}

class Employee
{
    public int empID;
    public string empName;
    public string designation;
    public int projectID;

    public Employee()
    {
    }

    public Employee(int id, string name, string desg, int pid)
    {
        this.empID = id;
        this.empName = name;
        this.designation = desg;
        this.projectID = pid;
    }
}

class Project
{
    public int projectID;
    public string projectName;

    public Project()
    {
    }

    public Project(int id, string name)
    {
        this.projectID = id;
        this.projectName = name;
    }
}
```

在前面的示例中，联接谓词使用两个类中共有的 ProjectID 成员变量构成。随后，控制台上会显示员工 ID、员工姓名以及员工所参与项目的名称。

```csharp
{
    Console.WriteLine("Employee ID: {0} Employee Name: {1} Project Name: {2} Department Name: {3}", e.id, e.name, e.projName, e.deptName);
}
}

class Employee
{
    public int empID;
    public string empName;
    public string designation;
    public int projectID;

    public Employee()
    {
    }

    public Employee(int id, string name, string desg, int pid)
    {
        this.empID = id;
        this.empName = name;
        this.designation = desg;
        this.projectID = pid;
    }
}

class Project
{
    public int projectID;
    public string projectName;
    public int deptID;

    public Project()
    {
    }

    public Project(int id, string name, int did)
    {
        this.projectID = id;
        this.projectName = name;
        this.deptID = did;
    }
}

class Department
{
    public int deptID;
    public string deptName;

    public Department()
    {
    }

    public Department(int did, string name)
    {
        this.deptID = did;
        this.deptName = name;
    }
}
```

我们修改了代码清单 19.26，在前面的程序中新增了一个新类 *Department*。*Department* 类与 *Project* 类相关。该程序输出员工 ID 以及他们的姓名、项目和部门名称。程序中使用的联接谓词包含两个联接条件。第一个条件用于获取 *Employee* 类与 *Project* 类之间的交集结果，第二个条件用于获取 *Project* 类与 *Department* 类之间的交集结果。该程序的输出如下：

```text
Employee ID: 100 Employee Name: James Project Name: Banking Project Department Name: BFS
Employee ID: 300 Employee Name: Keith Project Name: Banking Project Department Name: BFS
Employee ID: 400 Employee Name: Jonny Project Name: Banking Project Department Name: BFS
Employee ID: 600 Employee Name: Leonardo Project Name: Banking Project Department Name: BFS
Employee ID: 200 Employee Name: Jonathan Project Name: Insurance Project Department Name: INSR
Employee ID: 500 Employee Name: Amy Project Name: Insurance Project Department Name: INSR
```

## 左外联接

当对两个数据集执行左外联接时，它会根据联接谓词返回左侧数据集中的所有值，以及右侧数据集中匹配的值。图 19.23 表示左外联接中两个数据集的区域分布：

![](img/43c5f409f9b17790a628c4b4df854b61_664_0.png)

**图 19.23：展示左外联接**

在 LINQ 中，我们可以使用 *join* 关键字实现左外联接。代码清单 19.28 展示了一个左外联接操作的示例。

**代码清单 19.28：展示左外联接示例**

```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;

class Program
{
    public static void Main()
    {
        Employee james = new Employee(100, "James");
        Employee john = new Employee(200, "Jonathan");
        Employee keith = new Employee(300, "Keith");
        Employee jonny = new Employee(400, "Jonny");
        Employee amy = new Employee(500, "Amy");
        Employee leo = new Employee(600, "Leonardo");

        Certificate oracle = new Certificate("Oracle 11g certification", james);
        Certificate wcf = new Certificate("WCF certification", keith);
        Certificate sharePt = new Certificate("Sharepoint certification", james);
        Certificate dotnet = new Certificate(".NET Framework certification", amy);
        Certificate sqlServer = new Certificate("SQL Server 2008 certification", john);
        Certificate web = new Certificate("Web Application certification", keith);

        List<Certificate> certList = new List<Certificate>
        { oracle, wcf, sharePt, dotnet, sqlServer, web };
        List<Employee> empList = new List<Employee>
        { james, john, keith, jonny, amy, leo };

        var empSel = from emp in empList
                     join cert in certList
                     on emp equals cert.emp into gj
                     from subcert in gj.DefaultIfEmpty()
                     select new { empName = emp.empName, certName =
                                 (subcert == null ? "No certification Obtained" : subcert.name) };

        foreach (var e in empSel)
        {
            Console.WriteLine("Employee Name: {0} Certification Name: {1}", e.empName, e.certName);
        }
    }
}

class Employee
{
    public int empID;
    public string empName;

    public Employee()
    {
    }

    public Employee(int id, string name)
    {
        this.empID = id;
        this.empName = name;
    }
}

class Certificate
{
    public string name;
    public Employee emp;

    public Certificate()
    {
    }

    public Certificate(string name, Employee e)
    {
```
