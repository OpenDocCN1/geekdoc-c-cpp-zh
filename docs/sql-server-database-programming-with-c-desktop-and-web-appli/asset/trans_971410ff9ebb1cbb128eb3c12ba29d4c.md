

# 使用 C# 进行 SQL Server 数据库编程

## 添加 Web引用
导航到 Web 服务 URL 并点击“添加引用”以添加所有可用服务。

![](img/d59a47501d0a20fc0460a49c469c6fb7_572_0.png)

| WebSelect | 在此 URL 找到 Web 服务： |
|---|---|
| 找到 1 个服务: | |
| - WebServiceSelect | |

Web引用名称：
WS_SQL_Select
[添加引用]

图 9.32 添加 Web 引用向导。

- 2) 然后以管理员模式打开另一个 Visual Studio.NET 2022 并打开我们的客户端项目 WinClientSelect Project。
- 3) 在“解决方案”窗口中右键点击我们的客户端项目 WinClientSelect Project，从弹出菜单中选择“添加 | 服务引用”项以打开“添加服务引用”向导。
- 4) 点击该窗口左下角的“高级”按钮，打开 Web 服务设置窗口。
- 5) 点击左下角的“添加 Web 引用”按钮打开 Web 引用向导，如图 9.32 所示。
- 6) 将我们在第 1 步中复制的代码粘贴到“添加 Web 引用”向导的 URL 框中，点击箭头按钮让 Studio.NET 进行搜索。
- 7) 当找到 Web 服务时，右侧面板会显示我们的 Web 服务名称，如图 9.32 所示。
- 8) 或者，你可以将此 Web 引用的名称从 localhost 更改为任何有意义的名称，在我们可以使用 WS_SQL_Select。点击“添加引用”按钮将此 Web 服务添加到我们的新客户端项目中。
- 9) 点击 Web 服务内置 Web 界面上的“关闭”按钮以结束我们的服务项目。

立即你会发现，位于 `Web References` 文件夹下的 Web 服务 `WS_SQL_Select` 已添加到客户端项目的“解决方案”窗口中。此引用就是所谓的 Web 服务代理类。

接下来，通过为我们的 Web 服务界面添加实用的控件并显示查询到的信息，来开发图形用户界面。

# ASP.NET Web 服务

### 9.3.10.2 为 Windows 客户端项目开发图形用户界面

对我们的新项目进行修改：

- 1) 将表单对象从默认名称 `Form1` 重命名为我们所需的名称 `WinClient Form.cs`。
- 2) 通过修改窗口的 `Name` 属性，将窗口表单对象从默认名称 `Form1` 重命名为我们所需的 `FacultyForm`。
- 3) 通过修改表单的 `Text` 属性，将表单标题从默认名称 `Form1` 重命名为 `CSE_DEPT Faculty Form`。

为了节省时间和空间，我们可以使用第 7 章开发的 `RTOUpdateDelete` 项目中的 GUI。从 `Students` 下的 `ClassDBs Projects Chapter 7` 文件夹打开（参考第 1 章图 1.2）。然后打开 `Faculty` 表，通过菜单 `编辑 | 全选` 选择该表单中的所有控件，然后通过 `编辑 | 复制` 菜单复制从此表单窗口选中的所有控件。

回到我们新的 Windows Web 客户端项目 `WinSelectProject`，打开我们的表单窗口并粘贴从 `RTOUpdateDelete` 项目中的 `Faculty` 表单中复制的那些控件。

`Query Method` 组合框的目的是从我们在 Web 服务项目中开发的三个查询方法中选择一个来获取所需的教职人员信息：

- 1) 方法 1：使用对象返回我们的查询信息。
- 2) 方法 2：使用存储过程返回我们的查询信息。
- 3) 方法 3：使用 `DataSet` 返回我们的查询信息。

`Faculty Name` 组合控件用于选择所需的教职人员作为 Web 句名称的输入参数。在此应用程序中，仅使用了 `Select`（选择）和 `Back`（返回）按钮。

该项目的功能是：当项目运行时，由于已从关联控件选择了所需的方法和教职人员名称，用户将点击 `Select` 按钮。我们的客户端项目将根据提供的 Web 引用连接到 Web 服务，并根据从 `Query method` 控件选择的方法调用相应的 Web 方法，从我们的示例数据库中检索所需的教职人员记录，并显示在此图形界面中。

现在让我们查看该项目的处理代码，以便使用上一节中的 Web 引用连接到我们的 Web 服务。

### 9.3.10.3 开发消费 Web 服务的代码

编码工作分为四个部分：

- 1) `FacultyForm` 构造函数的编码，用于初始化 `Query Method` 组合控件和 `Faculty Name` 组合控件。第一次初始化将设置三个用户可以选择的 Web 方法，以便从 Web 服务执行数据查询。第二次是设置一个用户可以选择的默认教职人员列表，以便执行相关的教职人员信息查询。
- 2) `Back` 按钮的 `Click` 方法的编码，用于终止项目。
- 3) `Select` 按钮的 `Click` 方法的编码。
- 4) 其他用户定义方法的编码，例如 `ShowFaculty()`、`ProcessObject()`、`FillFacultyObject()` 和 `FillFacultyDataSet()`。

主要代码在 `Select` 按钮的 `Click` 方法内部执行。正如我们讨论的，用户点击此按钮，需要使用我们在上一节中设置的 Web 引用建立到 Web 服务的连接。因此，我们需要首先在 Web引用上创建一个对象或实例化该 Web 服务以获取实例，然后我们通过该实例访问不同的 Web 方法来执行数据查询。此过程被称为实例化代理类并调用 Web 方法。实例化代理类的协议是：

```
WebReference.WebServiceInstance = new WebReference.WebService();
```

在此实例化后，就可以使用此实例建立客户端项目与我们的 Web 服务之间的连接。该方法的伪代码如下：

- A. 使用上述协议创建一个新的 Web 服务实例 `wsSelect`。
- B. 同样创建一个新的 `wsSQLResult`，它可以作为在 Web 服务中开发的的真实对象的映射。我们可以轻松地访问 Web 方法来执行数据查询，并通过将结果分配给映射对象来从返回的对象中选取结果。
- C. 创建一个新的 `DataSet` 对象，并将其用于调用返回 `DataSet` 的 Web 方法。
- D. 根据用户使用 `Query Method` 组合框选择的方法，可以使用不同的 Web 方法来执行数据查询。
- E. 将存储在真实对象中的返回数据分配给我们的映射对象，可以从该对象检索每条信息并显示在我们的图形用户界面中。
- F. 如果使用了 `DataSet` 方法，则将返回的 `DataSet` 对象分配给我们的映射 `DataSet`，并调用 `fillFacultyDataSet()` 方法将从 `DataSet` 提取的信息填充到客户端表单的文本框中。

现在我们开始编写 `Faculty Form` 构造函数的代码。

#### 9.3.10.3.1 开发 FacultyForm 类构造函数的代码

现在我们开始开发 `FacultyForm` 类构造函数的代码，以完成上述 1 中的初始化工作。

- 打开 `FacultyForm` 类的构造函数，并将图 9.33 所示的以下代码输入此方法。

| WinClientSelectFacultyForm | FacultyForm() |
|---|---|
| public FacultyForm() { |
| InitializeComponent(); |
| ComboName.Items.Add("Ying Bar"); |
| ComboName.Items.Add("David Blair"); |
| ComboName.Items.Add("Black Anderson"); |
| ComboName.Items.Add("Steve Johnson"); |
| ComboName.Items.Add("Geneney King"); |
| ComboName.Items.Add("Alice Brown"); |
| ComboName.Items.Add("Debby Angles"); |
| ComboName.Items.Add("Jeff Henry"); |
| ComboName.SelectedIndex = 0; |
| ComboMethod.Items.Add("Object Method"); |
| ComboMethod.Items.Add("Stored Procedure Method"); |
| ComboMethod.Items.Add("DataSet Method"); |
| ComboMethod.SelectedIndex = 0; |
| } | |
| A | B |

图 9.33 FacultyForm 类构造函数的代码。

