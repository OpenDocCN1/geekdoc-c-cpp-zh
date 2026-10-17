
图 8.24 用户定义的方法 `FillFaculty()` 代码。

## 使用 C# 进行 SQL 数据库编程

让我们仔细查看这段代码。

- A. 定义第一个计数器 `intIndex`，用于循环从示例数据库的 Faculty 表中获取每一列。
- B. 生成文本框数组 `box[]`，用于稍后通过循环填充存储在 `DataReader` 中的七列数据。
- C. 只要 `Read()` 方法为真，就会执行 `while` 循环，这意味着从 `DataReader` 中读取了有效记录。如果未从 `DataReader` 读取有效记录，该方法将返回 `false`。在此应用程序中，此 `while` 循环执行一次，因为从 `DataReader` 中只读取了一行（一条记录）。
- D. 利用 `for` 循环从 `DataReader` 对象中读取每个数据列，并通过 `box[]` 将它们分配给 Faculty 页上的关联文本框控件。`index` 用于识别 `DataReader` 的每一列。终端列数等于 `FieldCount - 2`，因为教师表的最后一列 `7` 是教师图像 `fimage`，这是一个不可计数的对象。教师记录的七列文本信息从列 `0` 到列 `6` 排（`FieldCount = 7`）。
- E. 由于图像以二进制数据格式存储在最后一列，因此我们需要获取并转换为 `byte[]`。
- F. 因为 Web 页面没有可用的 Picture 对象，我们需要将图像从 `byte[]` 数组转换为 64 位字符串，并将其分配给 Faculty 页中 Image 对象的 `ImageUrl` 属性。

最后，让我们处理 Back 按钮 `Click` 方法的代码。这段代码的功能在点击此按钮时返回 Selection 页。在 Faculty 页窗口的设计视图中双击 Back 按钮打开此方法，并输入图 8.25 所示的代码。

这段代码直观且易于理解。当用户点击此按钮时，执行 `Response` 对象的 `Redirect()` 方法将客户端从当前 Faculty 页重定向回 Selection 页。点击此按钮向服务器发送请求时，服务器将 Selection 页返回给客户端。

现在我们完成了 Faculty 页的所有代码开发。现在是我们运行项目进行测试了。点击 `IIS Express` 运行我们的项目。在登录页输入用户名用户名密码（例如 `jerry`），选择一个教师（如 `Yang Bai`），然后点击 Select 按钮从数据库检索选定的教师信息。与所选教师相关的所有信息都检索并显示在 Faculty 页中，如图 8.26 所示。

点击 Back 按钮返回 Selection 页，然后点击 Exit 按钮终止我们的项目。这样，我们的 Web 应用程序就成功了。

| SQLWebSelect Project | `cmdBack_Click(object sender, EventArgs e)` |
| :--- | :--- |
| `protected void cmdBack_Click(object sender, EventArgs e)` { 
  `Response.Redirect("Selection.aspx");`
 } |

图 8.25 Back按钮点击方法的代码。

## 在 ASP.NET 中访问数据

![](img/d59a47501d0a20fc0460a49c469c6fb7_465_0.png)

**图 8.26** 教员页面的状态。

接下来，我们需要创建下一个 Web 页面，*课程*（Course）页面，并将其添加到项目中，以便根据选定的教员选择并添加所有课程。

## 8.4.9 创建第四个用户界面 — 课程页面

要创建一个新的 Web 页面并将其添加到项目中，请转到“解决方案管理器”（Solution Explorer），右键点击我们的项目 **SQLWeb Project**，从弹出的菜单中选择**添加 | 新项**（Add | New Item）以打开**添加新项**窗口。在打开的窗口中，选择*Web 表单*（Web Form），并在**名称**（Name）框中输入 `Course.aspx` 作为新页面名称，点击**添加**（Add）按钮将其添加到项目中。

在打开的 Web 表单上，可以根据需要在该页面的任何位置添加控件。现在尝试使用某种技术将控件放置在页面窗口的理想位置。关键元素是每个添加的控件的**位置**（Position）属性，就像你之前为 Windows 应用程序所做的那样。在这个*课程*页面中，我们添加了两个控件：一个列表框、六个文本框和一个按钮控件。为了将这些控件定位到页面的所需位置，除了标签控件外，你必须将添加到此页面的所有控件的**格式 | 设置位置**（Format | Set Position）属性设置为**绝对**（Absolute）。这种位置的设置对于列表框（ListBox）控件尤为重要，尽管第二个面板可能无法添加到正确的位置。

另一个问题是面板的大小和背景颜色。当你向页面添加一个新面板时，该面板的背景颜色是透明的，这意味着你无法看到在面板旁边添加的内容。要查看这些，你需要通过执行以下步骤来定义面板的大小：

- 1) 点击新添加的面板以选择它，并进入**属性**（Property）窗口。
- 2) 将**高度**（Height）和**宽度**（Width）属性设置为所需的像素尺寸。

438 使用 C# 进行 SQL 数据库编程

| 类型 | ID | 文本 | 索引 | 背景颜色 | 字体 | 自动回传 |
|---|---|---|---|---|---|---|
| 面板 | Panel1 | | 16 | #COCOFF | | |
| 标签 | Label1 | 教员姓名 | 0 | | 加粗/较小 | | |
| 下拉列表 | ComboName | | 1 | | | |
| 列表框 | CourseList | | 17 | | 加粗/中等 | True |
| 面板 | Panel2 | | 18 | #COCOFF | 加粗/较小 | | |
| 标签 | Label2 | 课程 ID | 2 | | | |
| 文本框 | txtID | | 3 | | | |
| 标签 | Label3 | 课程名称 | 4 | | | |
| 文本框 | txtCourse | | 5 | | | |
| 标签 | txtCredit | | 6 | | 加粗/较小 | | |
| 文本框 | txt5 | 教室 | 8 | | 加粗/较小 | | |
| 文本框 | txtclass | | 9 | | | |
| 文本框 | txtSchedule | 安排 | 10 | | 加粗/较小 | | |
| 标签 | Label6 | 注册 | 12 | | 加粗/较小 | | |
| 文本框 | txtEnroll | | 13 | | | |
| 按钮 | cmSelect | 选择 | 14 | | 加粗/中等 | | |
| 按钮 | cmInsert | 插入 | 15 | | 加粗/较小 | | |
| 按钮 | cmUpdate | 更新 | 16 | | 加粗/中等 | | |
| 按钮 | cmDelete | 删除 | 17 | | 加粗/中等 | | |
| 按钮 | cmBack | 返回 | 18 | | 加粗/中等 | | |

![](img/d59a47501d0a20fc0460a49c469c6fb7_466_0.png)

在此应用程序中，`panel1` 和 `panel2` 的高宽度属性为：

- Panel1: 高度 – 40px，宽度 – 458px
- Panel2: 高度 – 161px，宽度 – 327px

你完成的课程页面应该与图 8.28 所示的页面匹配。在我们继续开发此 Web 表单的代码之前，我们必须强调 Web 应用程序中使用的列表框控件。Windows 应用程序和 Web 应用程序之间的列表框控件存在显著的差异问题。

### 8.4.9.1 列表框控件的 AutoPostBack 属性

列表控件中需要添加的一个重要属性是 `AutoPostBack` 属性。与 Windows 应用程序中列表框相反，如果用户点击并从列表框中选择一个项，服务器端不会创建 `SelectedChanged` 事件。这是因为当你在 Web 表单中添加新列表框时，列表控件的 `AutoPostBack` 属性的默认值被设置为 `false`。这意味着如果用户点击了列表框中的某项，`SelectedChanged` 事件只能在客户端创建，而不能发送到服务器。如你所知，当用户运行项目时，列表是运行在服务器端的。因此，无论你在客户端点击并更改列表框中的项目多少次，服务器端都不会创建任何事件。这意味着，点击列表框控件的操作在你的项目运行时无法被项目报告。

在这个项目中，我们需要使用此属性。为了解决这个问题，必须将 `AutoPostBack` 属性设置为 `true`。这样，当用户点击列表框中的项时，就可以触发 `SelectedChanged` 事件来获取教员信息。在本节中，我们只讨论 `AutoPostBack` 属性，以便在项目运行时让项目报告诸如插入、更新或删除操作。

在 ASP.NET 中访问数据

![](img/d59a47501d0a20fc0460a49c469c6fb7_467_0.png)

**图 8.28** 完成的课程页面。

将在后文讨论当我们在对数据库进行插入或更新时，这些 Web 页面如何选择和返回操作的。

在此应用程序中，`panel1` 和 `panel2` 的高宽度属性为：

- Panel1: 高度 – 40px，宽度 – 458px
- Panel2: 高度 – 161px，宽度 – 327px

你完成的课程页面应该与图 8.28 所示的页面匹配。在我们继续开发此 Web 表单的代码之前，我们必须强调 Web 应用程序中使用的列表框控件。Windows 应用程序和 Web 应用程序之间的列表框控件存在显著的差异问题。

### 8.4.9.1 列表框控件的 AutoPostBack 属性

列表控件中需要添加的一个重要属性是 `AutoPostBack` 属性。与 Windows 应用程序中列表框相反，如果用户点击并从列表框中选择一个项，服务器端不会创建 `SelectedChanged` 事件。这是因为当你在 Web 表单中添加新列表框时，列表控件的 `AutoPostBack` 属性的默认值被设置为 `false`。这意味着如果用户点击了列表框中的某项，`SelectedChanged` 事件只能在客户端创建，而不能发送到服务器。如你所知，当用户运行项目时，列表是运行在服务器端的。因此，无论你在客户端点击并更改列表框中的项目多少次，服务器端都不会创建任何事件。这意味着，点击列表框控件的操作在你的项目运行时无法被项目报告。

在这个项目中，我们需要使用此属性。为了解决这个问题，必须将 `AutoPostBack` 属性设置为 `true`。这样，当用户点击列表框中的项时，就可以触发 `SelectedChanged` 事件来获取教员信息。在本节中，我们只讨论 `AutoPostBack` 属性，以便在项目运行时让项目报告诸如插入、更新或删除操作。

## 8.4.9.2 开发选择所需课程的代码

为了选择所需的课程，我们需要编写以下代码：

- 1) 当用户从下拉框中选择教员并点击选择按钮时，将显示该教员教授的所有课程。
- 2) 当用户从列表框中选择一个课程时，将在文本框中显示详细信息。

上述代码可以分为四个部分：

- 1) 页面加载和结束方法。
- 2) 选择按钮的点击方法。
- 3) 列表的 `SelectedChanged` 事件。
- 4) 其他自定义方法。

在开始第一部分编码之前，我们需要在顶部添加 SQL Server 数据命名空间。

```csharp
using System.Data;
using System.Data.SqlClient;
```

现在让我们从 `Page_Load()` 方法开始编码。

### 8.4.9.3 页面加载和结束方法的编码

打开 `Page_Load()` 方法，并将图 8.29 所示的代码输入此方法。让我们仔细观察这段代码及其工作原理：

- A 页面添加了一些与 SQL Server 相关的命名空间，因为我们需要使用这些命名空间中的数据在数据库中执行操作。
- B 这段代码的功能是：我们可以执行任何查询来检查数据库连接可用。由于我们在登录页面和应用程序状态中创建了类级实例，如果我们的应用程序尚未连接到数据库，我们需要重新连接。
- C 以下代码用于初始化教员姓名下拉框，并利用 `Add()` 方法将所有教员添加到此下拉框中，供用户选择。

```csharp
protected void Page_Load(object sender, EventArgs args)
{
    if (((SqlConnection)Application["Connection"]).State != ConnectionState.Open)
        ((SqlConnection)Application["Connection"]).Open();
    if (!IsPostBack)
    {
        //这些项只能一次添加到下拉框中
        ComboName.Items.Add("Ying Bal");
        ComboName.Items.Add("David Bhalla");
        ComboName.Items.Add("Black Andersson");
        ComboName.Items.Add("Steve Johnson");
        ComboName.Items.Add("Jenney King");
        ComboName.Items.Add("Alice Brown");
        ComboName.Items.Add("Debby Angles");
        ComboName.Items.Add("Jeff Henry");
    }
}
```

图 8.29 `Page_Load()` 方法的代码。

# 在 ASP.NET 中访问数据

在项目运行时，选择其中一个以获取课程信息。这段代码存在一个潜在的错误。如第 8.4.9.1 节所述，当用户点击并从列表控件选择一个项目时，`AutoPostBack` 属性将设置为 `true`，该属性将发送回服务器，以指示用户已对此列表执行了操作。服务器接收到此属性后，将向客户端发回一个刷新后的页面（Page）；因此，`Page_load` 将再次运行，并发送一个刷新后的 Course 页面。此 `Page_load` 的执行结果是将所有教职成员的副本附加到组合框 `ComboName` 中成员的末尾。当用户点击并增加 `CourseList` 框时，教职成员的数量也会增加并显示在 `ComboName` 框中。为了避免这种重复，你需要在 Course 页面首次出现时添加所有成员，如果发生了任何其他 `AutoPostBack` 属性，则不进行操作。

返回按钮方法的代码与 Faculty 页面中的返回按钮类似。点击此按钮时，页面将切换到选择页面。使用服务器 Response 对象的 `Redirect()` 方法来实现此切换返回的功能。在 Course 页面的设计视图中双击返回按钮，并将以下代码输入其中：

```csharp
Response.Redirect("Selection.aspx");
```
