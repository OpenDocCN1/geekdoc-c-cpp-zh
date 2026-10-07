
# 606 使用 C# 进行 SQL Server 数据库编程

- 三个控件 ComboMethod.firstCourseID 和 CourseList 的 `AutoPostBack` 属性已设置为 `True`。这非常重要，否则如果它是默认值 `False`，则没有事件从服务器传回我们的客户端。

现在点击 IIS 服务器运行我们的 Web 项目。首先，让我们选择数据插入函数。在 `Method` 下拉框控件中选择存储过程方法（Stored Procedure Method）。然后在 `Faculty Name` 下拉框控件中选择默认教师“Ying Bai”，然后在相关的文本框中插入第一条课程记录（见 9.4.3.3.2 节中的图 9.74），然后点击“插入”（Insert）按钮。

执行类似的操作，在选择 `DataSet Method` 的插入第二条新记录（见 9.4.3.3.2 节中的图 9.75）。你运行的 Web 页面如图 9.92 所示。

为了验证这些数据插入，点击 `DataSet Method` 上的 `Select` 按钮，然后点击 `Stored Procedure Method`。结果如图 9.93 所示。

你可以发现，我们新插入的课程 CSE-668 和 CSE-526 已从数据库中添加并检索，并显示在列表框控件中。

要获取特定课程的详细信息，从列表框控件中点击所需的 `course_id`。立即，所选 `course_id` 的详细课程信息将显示在每个相关的文本框中，如图 9.94 所示。

你可以通过 `DataSet` 或存储过程方法从列表框选择不同的 `course_ids` 来尝试获取不同课程的详细信息。点击“返回”（Back）按钮终止我们的 Web 项目。

一个完成的 Web 服务客户端 `WebClientInsert` 页面可以在 CRC ftp 站 `Students` 文件夹下的 `Class DB Projects\Chapter 9\WebClientInsert Solution` 文件夹中找到，参考第 1 章的图 1.2。

接下来，我们需要处理通过 Web 服务更新和删除数据。

![](img/d59a47501d0a20fc0460a49c469c6fb7_634_0.png)

图 9.92 插入新课程记录的运行状态。

# ASP.NET Web Services

![](img/d59a47501d0a20fc0460a49c469c6fb7_635_0.png)

图 9.93 数据验证过程的运行状态。

![](img/d59a47501d0a20fc0460a49c469c6fb7_635_1.png)

图 9.94 获取详细课程信息的运行状态。

608 使用 C# 进行 SQL Server 数据库编程

## 9.5 构建 ASP.NET WEB SERVICE以更新和删除 SQL SERVER 数据库数据

在本节中，我们将讨论如何通过 Web 服务更新和删除数据库中 `Student` 表的记录。此服务项目中开发了两个 Web 方法：`SQLUpdateSP` 和 `SQLDeleteSP`。这两个方法都调用相关的存储过程来执行数据更新和删除操作。

打开 Studio 2022 并在 `C:\Chapter 9` 文件夹中创建一个新的 WCF 服务应用程序 `WebServiceUpDtProject`。然后，从解决方案管理器中右键点击新创建的项目，选择“添加 | 新项”打开添加新项向导。在左侧窗格选择“Web”，在中间窗格选择“Web 服务”。在“名称”框中输入 `WebServiceUpDt.asmx`，点击“添加”将其添加到项目。。正如我们在 9.3.3 节中所的那样，执行以下操作来构建此服务：

1. 修改命名空间（namespace）以创建我们的 Web 服务命名空间。
2. 创建一个自定义基类来处理错误检查代码，以保护我们真实的 Web 服务类。
3. 创建一个自定义返回类来存储所需的或更新的学生信息。该类是基于上述基类的派生类。
4. 向我们的 Web 服务类添加 Web 方法以访问示例数据库。
5. 开发这些 Web 方法的详细代码以执行 Web 服务。

现在让我们按照此顺序开始工作。

### 9.5.1 修改默认命名空间并添加数据库连接字符串

从解决方案管理器中双击主服务页面 `WebServiceUpDt.asmx`，将默认命名空间更改为图 9.95 步骤 A 所示的特殊命名空间。

| WebServiceUpDt 项目 | HelloWorld() |
| :--- | :--- |
| using System.Web.Services; namespace WebServiceUpDt { // <summary>WebServiceUpDt 描述</summary> [WebService(Namespace = "https://www.routledge.com/978-1023123354/")] [WebServiceBinding(ConformsTo=ToolItem(false))] [System.ComponentModel] // 要允许从脚本（如 ASP.NET AJAX）调用此服务，取消下行的注释。 // [System.Web.Script.Services.ScriptService] public class WebServiceUpDt : System.Web.Services.WebService [WebMethod] public string HelloWorld() { return "Hello World"; } } |

图 9.95 修改后的命名空间。

我们需要使用自己的命名空间来替换微软使用的默认命名空间，以告诉 ASP.NET 运行时我们的 Web 服务在运行时时加载的位置。这个特定的命名空间是唯一的，因为它是 CRC Press 的主页加上了书籍的 ISBN 编号。事实上，如果你喜欢，可以使用任何位置作为你的命名空间来存储我们的 Web 服务。

现在，像之前所做的，打开配置文件 `Web.config`，通过在文件末尾输入以下标签添加数据库连接字符串：

```
<connectionStrings>
  <add name="sql_conn" connectionString="Server=localhost\SQL2019EXPRESS;Initial Catalog=CSE_DEPT;UserID=SMART;Password=Happy2022;"/>
</connectionStrings>
```

确保此 `add name...` 是一行完整的单行代码，其中没有任何连接符号。在这里我们使用断连接符号是为了使这行代码在有限的空间内看起来更好。

人们可以在此配置文件的任何位置添加此连接字符串标签，例如在文件末尾或 `<configuration>` 结束之前。

### 9.5.2 创建我们自定义的基类和返回类

在解决方案管理器中右键点击我们的新项目，选择“添加 | 新项”以添加具有两个成员的新 C# 类 `SQLBase.cs`：

1. `Boolean SQLOK;`
2. `string SQLError;`

以类似的方式创建另一个 `SQLResult.cs`，它是基于 `SQLBase` 类的派生类，具有八个成员，如图 9.96 所示。

进入“文件 | 保存所有”项以保存这些操作。接下来，让我们集中在添加和创建 Web 方法以执行数据更新和删除操作上。

| WebServiceUpdt 项目 | StudentID |
| :--- | :--- |
| namespace WebServiceUpdt_Project {
  public class SQLBase {
    public string StudentID;
    public string StudentName;
    public float Gpa;
    public int Credits;
    public string Major;
    public string SchoolYear;
    public string Email;
    public byte[] Image;
  }}|

图 9.96 SQLResult 类的成员数据。

### 9.5.3 创建调用存储过程更新学生记录的 WEB 方法

`SQLUpdateSP()` 方法的功能是调用 SQL 存储过程来执行数据更新和删除。在本节中，我们将讨论如何通过 Web 服务更新和删除数据库中 `Student` 表的记录。此服务项目中开发了两个 Web 方法：`SQLUpdateSP` 和 `SQLDeleteSP`。这两个方法都调用相关的存储过程来执行数据更新和删除操作。

