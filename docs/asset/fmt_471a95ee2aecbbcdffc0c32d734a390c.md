
`using System.Data;`

`using System.Data.SqlClient;`

接下来，我们需要为我们的连接对象创建一个类或字段级变量 `sqlConnection`。在类头下方输入以下代码：

```csharp
public SqlConnection sqlConnection;
```

此连接对象以后将由此项目中的所有 Web Forms 使用。

我们需要为 `Page_Load()` 方法编写代码，该方法类似于 Windows 应用程序中的 `Form_Load()` 方法。打开此事件方法，并将图 8.9 所示的代码输入到该方法中。

让我们仔细查看一下这段代码，看看它是如何工作的的。

- A. 向此项目添加了一些与系统数据和 SQL 数据提供程序相关的命名空间，因为我们需要使用这些组件来对示例 SQL Server 数据库执行数据操作。
- B. 声明了一个类级连接对象 `sqlConnection`，该对象以后将由项目中的所有 Web Forms 使用，以连接到我们的示例数据库。
- C. 就像我们在 Windows 应用程序的 `Form_Load()` 方法中所做的那样，我们需要在 `Page_Load()` 方法中执行数据库连接连接。创建一个包含数据库服务器名称、数据库名称和安全方法的连接字符串。
- D. 在 Application 状态函数中添加了一个新的数据库连接对象 `sqlConnection`，应用程序中的任何页面都可以通过访问此 Application 状态函数使用该对象。
- E. 连接对象 `sqlConnection` 被添加到 Application 状态函数中，应用程序中的任何页面以后都可以通过访问此 Application 状态函数。与 Windows 应用程序中的全局变量不同，无法通过在类声明的类变量前加上表单名称来访问类变量。

# 在 ASP.NET 中访问数据

| SQLWebSelect 项目 | Page_Load() |

```csharp
using System.Data;
using System.Data.SqlClient;
namespace SQLWebSelect_Project
{
    public class _Default :
    {
        public SqlConnection connection;
        protected void Page_Load(object sender, EventArgs args)
        {
            string connectionString = "Server-DESKTOP-24JUPFB\SQL2019EXPRESS;" + "Initial Catalog=CSE_DEPT;";
            connection = new SqlConnection(connectionString);
            Application["connection"] = connection;
            if (connection.State != ConnectionState.Open)
            {
                connection.Open();
            }
        }
}
```
图 8.9 `Page_Load` 方法。

# 在 ASP.NET 中访问数据

| SQLWebSelectProject | cmdCancel_Click(object sender, EventArgs e) |
|---|---|
| protected void cmdCancel_Click(object sender, EventArgs e) { \n  if(sqlConnection.State == ConnectionState.Open) \n  sqlConnection.Close();\n  Response.Write("<script>window.close()</script>\");\n} } | |

**图 8.11** 取消按钮点击方法的代码。

这段代码的功能是：

- 我们首先需要检查数据库是否仍然连接到我们的 Web 表单。如果是，我们需要在终止 Web 应用程序之前关闭此连接。
- 服务器通过 `Response` 对象的 `Write()` 方法发送回一个命令，向 Web 应用程序发布一个 Javascript 的 `window.close()`。

需要注意的一个关键点是，使用此取消按钮重置我们的 Web 应用程序时，你必须将此取消按钮的 **Validation**（验证）过程重置为 **false**，以跳过下一节中为两个文本框 `txtName` 和 `txtPassword` 构建的验证过程。否则，你必须通过输入用户名和密码来通过此验证过程，以便在点击取消时处理我们的事件。

要重置属性，在登录页的 Design 模式下，选择取消按钮到属性窗口，并从 **Validation** 属性中选择 **false**。这样，你就可以直接关闭或终止我们的发布，而无需经过验证过程。

此时，我们已经完成了登录（Login）Web 表单的代码开发。在运行项目测试我们的 Web 页面之前，我们需要在客户端添加一些数据验证功能，以减轻服务器的负担。

## 8.4.3 在客户端验证数据

如第 8.3.3 节所述，为了减轻服务器的负担，我们应该尽力在客户端执行数据验证。换句话说，我们需要向服务器发送请求，我们需要确保发送到服务器的信息尽可能正确。ASP.NET 了一了一些工具来帮助我们完成这种数据验证。这五个验证控件如图 8.12 所示。

| 验证控件 | 功能 |
|---|---|
| RequiredField | 验证必填字段是否有有效数据为空 |
| RangeValidator | 验证值是否在数值范围内。该范围由用户提供的 MaximumValue 和 Minimum 属性定义。 |
| CompareValidator | 使用不同的操作符（如 'equal'、'greater'、'less'）以及由属性设置的值类型来验证给定的表达式。 |
| CustomValidator | 使用脚本函数验证给定的表达式。这种方法在数据验证中提供了最大的灵活性，但用户需要将其添加到 Web 页面并发送到服务器以获取其反馈。 |
| RegularExpression | 使用 ValidationExpression 属性验证值是否符合正则表达式，该属性应由用户提供。 |

**图 8.12** 验证控件。

# 426 使用 C# 进行 SQL Server 数据库编程

这五个控件都位于 Visual Studio 工具箱（Toolbox）窗口中的 Validation 选项卡中。

在这里，我们想使用第一个控件 `RequiredFieldValidator` 来验证页面中的两个文本框 `txtUsername` 和 `txtPassword`，以确保在项目运行时用户点击登录按钮时，它们都不是空的。

打开登录 Web 表单的 Design 模式，进入工具箱窗口并点击 Validation 选项卡将其展开。从工具箱中拖入 `RequiredFieldValidator` 控件放在用户名文本旁边。在属性窗口中为此控件设置以下属性：

| ErrorMessage: UserName Required |
| ControlToValidate: txtUsername |

对第二个 `RequiredFieldValidator` 执行类似的拖动和放置操作，放在密码文本旁边。在属性窗口中为此控件设置以下属性：

| ErrorMessage: PassWord is Required |
| ControlToValidate: txtPassword |

你完成的登录 Web 表单应该与图 8.13 所示。
现在点击 IIS Express 按钮运行项目以测试此数据验证，在不在两个文本框中输入任何数据的情况下，点击登录按钮。立即，会显示由 `RequiredFieldValidators` 创建的两个错误消息，要求用户输入这两项信息。输入用户名和密码后，再次点击登录，一个成功的

![](img/d59a47501d0a20fc0460a49c469c6fb7_454_0.png)

# 在 ASP.NET 中访问数据

登录消息被显示。因此你可以看到 `RequiredFieldValidator` 如何工作以减轻服务器的处理负载。

当我们运行我们的 Web 应用程序项目时，我们没有指定或选择 Web 浏览器，而是使用了默认浏览器 Google Chrome。然而，为了有效运行和执行我们在在本章中构建的 Web 应用程序，我们应该使用所需的 Web 浏览器 Internet Explorer。这是因为这种浏览器包含了更强大的工具和经典组件，以满足我们应用程序的功能和要求。

## 8.4.4 选择所需的浏览器以有效运行我们的 Web 应用程序项目

要选择 Internet Explorer 作为我们的 Web 浏览器，执行以下操作步骤：

- 1. 在打开的 Visual Studio 2012 和 SQLWebSelect 项目中，点击顶部 IIS 按钮旁边的下拉箭头。
- 2. 在打开的子菜单中，点击 Web Browser (Google Chrome) 项。
- 3. 从子菜单中勾选 Internet Explorer 进行选择。

现在默认浏览器已更改为顶部 IIS 按钮关联的 Internet Explorer。

使用 Internet Explorer 作为我们的 Web 浏览器时，最重要的功能之一是执行一些经典的 Web API 函数，以有效运行我们的 Web 应用程序并实现所需的功能。例如，为了有效终止我们的 Web 应用程序项目，我们使用了 Javascript 方法 `window.close()`。此方法可以有效停止我们的 Web 应用程序。然而，此方法只能在 Internet 浏览器下工作，其他浏览器均不行。

## 8.4.5 创建第二个用户界面 – 选择页面

现在让我们通过添加另一个 Web 页面（选择页）来开发我们的 Web 应用程序。正如我们在之前的章节中所做的那样，流程完成后，下一步是允许用户从选择表单中选择不同的功能以执行相关的数据操作。

此选择页的功能是允许用户访问不同的页面，通过选择不同的项目对数据库执行不同的数据操作（如插入、更新或删除数据）。此选择页需要执行以下工作：

- 1) 提供并显示所有选项以允许用户进行选择。
- 2) 根据用户的选择打开相关页面。

现在让我们构建此页面。为此，我们需要添加一个 New Web 页面。在解决方案管理器（Solution explorer）中右键点击我们的项目 SQLSelect Project，并从弹出菜单中选择 Add | New Item。在打开的窗口中，选择 Web Form 作为模板，并将 `Selection.aspx` 作为新页面的名称，然后点击 Add 按钮将此页面添加到我们的项目中。

在打开的 Web 表单上，将如图 8.14 所示的控件添加到页面。你完成的选择页面应该显示如图 8.15 所示的内容。

如上一节所述，在从工具箱窗口选取控件并拖入页面之前，你必须先使用键盘上的 Space 或 Enter 键来确定这些控件的位置。例外是，当你将所有控件的 Position 属性都设置为 Absolute 时，你就可以

接下来让我们为此选择页创建代码，允许用户选择不同的页面以执行相关的数据操作。

# 使用 C# 进行 SQL Server 数据库编程

| Type | ID | Text | TabIndex | BackColor | Font |
|---|---|---|---|---|---|
| Label | Label1 | Make Your Selection: | 0 | #E0E0E0 | Bold/Large |
| DropDown | ComboSelection | | 1 | | |
| Button | cmdSelect | Select | 2 | | Bold/Medium |
| Button | cmdExit | Exit | 3 | | Bold/Medium |

**图 8.14** 选择方法的控件，可以将任何一个控件移动到任何位置。

![](img/d59a47501d0a20fc0460a49c469c6fb7_456_0.png)

**图 8.15** 完成的选择页面。

### 8.4.6 开发选择页代码以打开其他页面

首先运行选择页以生成 Web 配置文件。点击 **IIS** express 运行此页面，然后点击页面右上角的 **Close** 按钮关闭它。

在解决方案管理器中右键点击 **Selection.aspx** 并点击 **View Code** 项以打开 Selection Web 表单的代码页。首先，让我们在页面顶部添加 SQL 数据相关的命名空间，以提供对所有 数据提供程序的引用：

```
using System.Data;
using System.Data.SqlClient;
```

然后将图 8.16 所示的代码输入 `Page_load()` 方法中，将所有选择项添加到组合框 `ComboSelection` 中，允许用户根据项目结果进行选择。

这段代码的功能非常直观。使用 `Add()` 方法将三条 CSE 部门信息添加到组合框 `ComboSelection` 中，这些信息将由用户选择作为项目结果。

接下来我们需要为两个按钮“Select”和“Exit”创建代码。首先为 **Select** 按钮编写代码。在解决方案窗口中右键点击 **Selection.aspx** 并点击 **View Designer** 项打开 Selection Web 表单，然后双击 **Select** 按钮打开其方法。将图 8.17 所示的代码输入此方法中。

这段代码的功能非常简单。根据用户选择的信息，使用服务器的 **Response** 对象打开相关的 Web 页面，具体通过使用服务器 **Response** 对象的 `Redirect()` 方法来实现。所有三个页面将在后续节中被创建并讨论。

# 在 ASP.NET 中访问数据

| SQLWebSelect 项目 | Page_Load(object sender, EventArgs e) |
| :--- | :--- |
| using System.Data;using System.Data.SqlClient;namespace SQLWebSelectProject { public partial class Selection : System.Web.UI.Page { protected void Page_Load(object sender, EventArgs e) { ComboSelection.Items.Add("Faculty Information"); ComboSelection.Items.Add("Course Information"); ComboSelection.Items.Add("Student Information"); } } | | | |

图 8.16 选择页面 `Page_Load()` 方法的代码实现。

| SQLWebSelect 项目 | cmdSelect_Click(object sender, EventArgs e) |
| :--- | :--- |
| protected void cmdSelect_Click(object sender, EventArgs e) { if (ComboSelection.Text == "Faculty Information") Response.Redirect("Faculty.aspx");else if (ComboSelection.Text == "Student Information") Response.Redirect("Student.aspx");else if (ComboSelection.Text == "Course Information") Response.Redirect("Course.aspx"); } | | | |

图 8.17 选择按钮点击事件的代码实现。

最后，让我们处理退出（Exit）点击方法的代码。这段代码的功能是关闭数据库连接和 Web 应用程序。在选择页面的设计视图（Design View）中双击退出按钮以打开此方法。将图 8.18 所示的代码输入到此方法中。

让我们仔细观察这段代码，看看它是如何工作的。
首先，需要检查数据库是否仍然连接到我们的应用程序。如果是，则使用带有 `Close()` 方法的全局连接对象来关闭数据库连接。然后调用服务器 `Response` 对象的 `Write()` 方法来关闭 Web 应用程序。关键点是 `Application` 函数存储了一个对象，在本例中为连接对象。为了访问和使用存储在 `Application` 全局函数中的该对象，必须在其之前显式地加上类型转换 `SqlConnection`；因此，需要两层括号。

| SQLWebSelect 项目 | cmdExit_Click(object sender |

图 8.18 退出按钮点击方法的代码实现。

![](img/d59a47501d0a20fc0460a49c469c6fb7_458_0.png)

图 8.19 第二个页面的运行状态——选择页面。

否则将遇到编译错误，因为编译器无法将存储在 `Application` 状态函数中的通用对象转换为特定的连接对象（Connection object）。

我们现在已经完成了选择页面的编码。在运行项目测试此页面之前，我们需要对登录页登录按钮的 `Click` 方法中的代码进行一些修改，以便应用程序在登录成功后从登录页面切换到选择页面。

打开登录页和登录按钮的 `Click` 方法，在 `sqlReader.Close();` 方替换 `if(sqlReader.HasRows == true)` 块内的主体代码：
