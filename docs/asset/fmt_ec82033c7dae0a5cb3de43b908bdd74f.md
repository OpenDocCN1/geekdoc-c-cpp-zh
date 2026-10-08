
为了继续创建 WebControls 应用程序，在表上添加了一个标记为“Next Meeting”的按钮。记住，应用程序的最终结果如图 15-19 所示。点击“Next Meeting”按钮时，日历将更改为显示下次计算机俱乐部会议的日期。通过编程方式，将其设置为当前日期的七天后。然后使用选择语句测试会议日期，以确保日期不是星期日。如果是，则将会议设在下一个周一。示例 15-12 显示此按钮的事件处理方法。

```csharp
protected void ShowCalendar_Click(object sender, System.EventArgs e)
{
    Calendar1.SelectedDates.Clear();
    meetingDate = new DateTime(DateTime.Today.Year, DateTime.Today.Month, DateTime.Today.Day, 8,0,0);
    // 会议安排在今天一周后！
    meetingDate = meetingDate.AddDays(7);
    // 除非它是星期日——如果是的话，
    // 在周一见面。
    if (meetingDate.DayOfWeek.ToString() == "Sunday")
    {
        meetingDate = meetingDate.AddDays(1);
    }
    Calendar1.SelectedDate = meetingDate;
    lblMsg.Text = "Meeting on: " + meetingDate.ToShortDateString();
}
```

# 第15 章 Web 应用程序

## 验证、自定义和复合控件

![](img/45e6f245af31396d967c3186f196d331_986_0.png)

图 15-23 在 .aspx 和 .aspx.cs 文件之间切换

日历控件具有许多属性，包括 `SelectedDate` 属性。`SelectedDate` 用于选择显示的月份、日期和年份。`SelectedDate` 属性初始设置为当前日期。这是在页面加载时完成的。但你也可以通过编程或在设计期间通过属性窗口中的 `SelectedDate` 属性设置日期。在设计期间设置日期允许你在属性窗口中使用内置的日历控件，如图 15–24 所示。

![](img/45e6f245af31396d967c3186f196d331_987_0.png)

图 15-24 使用属性窗口设置 SelectedDate 属性

> 如果你打算通过编程设置日期，请使用 `Page_Load()` 事件处理方法。

日历控件基于 .NET `DateTime` 类，它允许你以不同的格式处理日期。在 `Page_Load()` 事件处理程序中添加了程序语句，将日期设置为应用程序运行时的当天。这在示例 15-11 中所示。注意语句被放置在 `try...catch` 异常块中。

### 示例 15-11

```csharp
private void Page_Load(object sender, System.EventArgs e)
{
    try {
        Calendar1.SelectedDate = DateTime.Today;
    } catch (System.Exception exc) {
        this.lblMsg.Text = exc.Message;
    }
}
```

### DateTime 类

为了通过编程方式处理 WebControls 应用程序中的日历，需要实例化 `DateTime` 类的对象。

`DateTime` 类具有许多实用的成员，可以与日历控件对象配合。表 15-4 显示了该类一些有趣的成员。

### 表 15-4 DateTime 类的成员

| DateTime 成员 | 描述 |
| :--- | :--- |
| `AddDays()`, `AddHours()`, `AddMinutes()` | 添加指定的天数、小时、分钟、月份或年份 |
| `AddMonths()`, `AddYears()` | 比较两个 DateTime 实例 |
| `Compare()` | 获取日期 |
| `Date` | 获取月份中的某一天 |
| `Day` | 获取星期几几（星期日为 0；星期六为 6） |
| `DayOfYear` | 获取一年中的第几天 |
| `DaysInMonth()` | 返回指定月份的天数 |
| `Hour` | 获取日期的的小数 |
| `Minute` | 获取日期的分钟 |
| `Month` | 获取日期的月份 |
| `Now` | 获取当前日期和时间 |
| `Parse()` | 将字符串转换为 DateTime 格式 |
| `Subtract()` | 从实例中减去指定的时间 |

### 表 15-4 DateTime 类的成员（续）

| DateTime 成员 | 描述 |
| :--- | :--- |
| `Today` - static | 获取当前日期 |
| `Year` | 获取当前年份 |
| `+`, `-`, `=`, `==`, `<`, `>`, `!=`, `<=` | 用于处理 DateTime 实例的运算符 |

属性在表 15-4 中显示时不带 ( ) `。

![](img/45e6f245af31396d967c3186f196d331_989_0.png)

## 在应用程序中使用日历控件

为了继续创建 WebControls 应用程序，在表上添加了一个标记为“Next Meeting”的按钮。记住，应用程序的最终结果如图 15-19 所示。点击“Next Meeting”按钮时，日历将更改为显示下次计算机俱乐部会议的日期。通过编程方式，将其设置为当前日期的七天后。然后使用选择语句测试会议日期，以确保日期不是星期日。如果是，则将会议设在下一个周一。示例 15-12 显示此按钮的事件处理方法。

### 示例 15-12

```csharp
protected void ShowCalendar_Click(object sender, System.EventArgs e)
{
    Calendar1.SelectedDates.Clear();
    meetingDate = new DateTime(DateTime.Today.Year, DateTime.Today.Month, DateTime.Today.Day, 8,0,0);
    // 会议安排在今天一周后！
    meetingDate = meetingDate.AddDays(7);
    // 除非它是星期日——如果是的话，
    // 在周一见面。
    if (meetingDate.DayOfWeek.ToString() == "Sunday")
    {
        meetingDate = meetingDate.AddDays(1);
    }
    Calendar1.SelectedDate = meetingDate;
    lblMsg.Text = "Meeting on: " + meetingDate.ToShortDateString();
}
```

# 验证、自定义和复合控件

959

`DataReader` 和 `DataSet` 类。用于填充这些控件的实际数据来自数组或数据库表等源。在第 14 章中，你已经体验过将 `DataReader` 对象和 `DataSet` 对象与 `DataAdapter` 对象结合使用。

我们鼓励你复习第 14 章中与从数据库表访问数据相关的章节。你会想起在第 14 章中，有一些视觉工具和向导可以将数据绑定到控件上。

![](img/45e6f245af31396d967c3186f196d331_992_0.png)

## 在应用程序中使用 DataGrid 控件

本章正在开发的 WebControls 应用程序包含一个 `DataGrid` 或 `GridView`，它显示来自 Access 数据库的实例。要将此控件添加到 Web 表单（Web form），你需要遵循之前介绍的设计指南。你可能想复习第 14 章中的示例 14-21。在标准 Windows 表单上显示来自 Access 数据库的数据。示例 14-21 实例化了 `DataSet` 和 `DataAdapter` 类的对象。这些类也被用于检索显示在 Web 表单上的数据。

`OLEDB` 数据提供程序你在第 14 章中了解到，.NET 将 ADO.NET 类组织在不同的提供程序命名空间中。这使得你能够使用一致的面向对象的方法处理 Oracle 和 Access 等不同的数据库。这些命名空间中的每一个都有带有提供程序类型前缀的类，其中 `OLEDB` 用于处理 Access 数据库。

Visual Studio 有一个 Data 选项卡可以访问工具箱（Toolbox）。其中包含了用于显示数据的控件，如 `GridView`、`DataList` 和 `DetailView`，以及用于连接到特定数据库的控件。这些包括 `AccessDataSource`、`SqlDataSource`、`XmlDataSource` 和 `ObjectDataSource`。所有控件都可以按照拖动其他控件对象（如按钮）完全相同的方式拖到你的表单中。

![](img/45e6f245af31396d967c3186f196d331_992_1.png)

## 连接到数据库

WebControls 应用程序添加了一个名为“查看当前成员”（See Current Members）的按钮。当用户点击按钮时，应该显示一个包含当前成员名称的表格。可以通过编写程序语句来填充控件并开发解决方案。这种方法将首先被探讨。然而，利用 Visual Developer 和 Visual Studio 提供的视觉工具，将说明另一种可以最大限度减少所需程序语句数量的方法。实例化 `Connection` 对象。使用与第 14 章中相同的连接字符串作为构造函数的参数。连接字符串标识提供程序为 Access 数据库。它还指定了数据库名称——包括指向数据库位置的完整路径。接下来的示例（示例 15-14）了组成 `btnShowMembers_Click()` 方法的语句。当你审阅代码时，请注意方法中出现的注释。对第 14 章中展示的代码需要微小的修改（仅需一行代码）。`DataBind()`

![](img/45e6f245af31396d967c3186f196d331_992_2.png)

![](img/45e6f245af31396d967c3186f196d331_992_3.png)

方法调用对于 Web 应用程序是不同的。为了使用 `DataGrid` 显示数据，Web 和 Windows 应用程序使用了 `DataAdapter` 和 `DataSet` 类的对象。

> 注意，数据库路径列为 "`DataDirectory|member.accdb`"。这是一个相对路径，表示数据库存储在数据目录中，默认是 `App_Data` 目录。

### 示例 15-14

```
protected void btnShowMembers_Click(object sender, System.EventArgs e)
{
    lblMembers.Visible = true;
}
try
{
    string connection =
        "Provider=Microsoft.ACE.OLEDB.12.0;" +
        "Data Source=|DataDirectory|member.accdb";
    OleDbConnection conn = new OleDbConnection(
        connection);
    string sql = "Select FirstName, LastName From Table " +
    " + memberTableOrder " +
    "By LastName Asc, FirstName Asc";
    OleDbCommand dbCmd = new OleDbCommand();
    dbCmd.CommandText = sql;
    dbCmd.Connection = conn;
    OleDbDataAdapter memberDataAdapter = new OleDbDataAdapter();
    memberDataAdapter.SelectCommand = dbCmd;
    DataSet memberDS = new DataSet();
    memberDataAdapter.Fill(memberDS);
    this.dataGrid.DataBind();
}
catch (System.Exception exc)
{
    this.lblMsg.Text = exc.Message;
}
```

> 如果你使用向导连接数据库，`asp:DataSource` 控件被添加到 .aspx 文件。

**从数据库检索数据**

验证、自定义和复合控件

`FirstName` 和 `LastName` 从 `memberTable` 中检索。SQL 语句按 `LastName` 排序。SQL 语句被设置为 `CommandText`。使用 `Fill()` 方法实例化 `DataAdapter` 类对象。注意这是与 Windows 应用程序不同的语句。

![](img/45e6f245af31396d967c3186f196d331_994_0.png)

> 记住，图 15-19 显示了所有控件添加且事件处理方法绑定后的应用程序。WebControls 的后置代码程序列表见示例 15-15。

### 示例 15-15

```
// WebControls
using System;
using System.Collections.Generic;
using System.Data;
using System.Web;
using System.Web.UI;
using System.Data.OleDb;

namespace WebControls
{
    public class WebForm1 : System.Web.UI.Page
    {
        protected DataSet memberDS;
        protected void Page_Load(object sender, EventArgs e)
        {
            try
            {
                Calendar1.SelectedDate = DateTime.Today;
            }
        }
    }
}
```

```
protected void btnShowCalendar_Click(object sender, System.EventArgs e)
{
    Calendar1.SelectedDates.Clear();
    DateTime meetingDate = new
    DateTime(DateTime.Today.Year,
             DateTime.Today.Month,
             DateTime.Today.Day, 8,0,0);
    // 会安排在
    // 今天一周后！
    meetingDate = meetingDate.AddDays(7);
    // 除非是周日——如果是的话
    // 我们在周一见面。
    if (meetingDate.DayOfWeek.ToString() == "Sunday")
    {
        meetingDate = meetingDate.AddDays(1);
    }
    Calendar1.SelectedDate = meetingDate;
    this.lblMsg.Text =
        "下周会议时间：" +
        meetingDate.DayOfWeek +
        "/" + meetingDate.Month +
        "/" + meetingDate.Day +
        " at " + meetingDate.Hour + ");
}
```

# 验证、自定义与复合控件

```cs
OleDbCommand dbCmd = new OleDbCommand();
dbCmd.CommandText = sql;
dbCmd.Connection = dbConn;

OleDbDataAdapter memberDataAap = new
OleDbDataAdapter();
memberDataAap.SelectCommand = dbCmd;
DataSet memberDS = new DataSet();
//DataSet 声明为保护类成员memberDataAdapter.Fill(memberDS, "memberTable");
// 绑定是唯一与 Windows 应用程序// 不同的部分
this.dataGrid.DataBind();

catch (System.Exception exc)
{
this.lblMsg.Text = exc.Message;
}
```

```csharp
protected void btnSubmit_Click(object sender, System.EventArgs e)
{
    this.lblSubmit.Text = "感谢 " + this.txtBfname.Text + "! 我们将与您联系... ";
    if (lstBxInterests.SelectedIndex > -1)
    {
        this.lblSubmit.Text += " 以讨论加入 " + " the \" " + this.lstBxInterests.SelectedItem.Text + "\" 团队.";
    }
}
```
