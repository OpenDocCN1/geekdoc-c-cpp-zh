

## 在 ASP.NET 中访问数据

`ExecuteCommand()` 是一个流行且强大的方法。实际上，该方法是当 LINQ to SQL 无法为特定场景提供充分解决方案时的一种透传机制。此方法返回一个整数（Int32），表示执行该方法后修改的行数。

该命令的语法与用于创建 ADO.NET 命令的语法几乎相同。唯一的区别在于参数指定的方式。具体来说，你通过将参数封装在花括号 `{...}` 中并从 0 开始编号来指定参数。该参数与参数数组中编号相同的对象相关联。

第一个参数表示要执行的非查询 SQL 命令，它应该是 `String` 格式。第二个参数是要传递给命令的对象或数组。如果数组中的对象数量少于命令字符串中标识的最高数字，将抛出异常。如果数组包含未在命令字符串中引用的对象，则不会抛出异常。

如果任何参数为 null，它将被转换为 `DBNull.Value`。
ExecuteCommand() 方法执行任何 SQL 相关的命令，例如：

- 1) 在选定的数据库中创建新表。
- 2) 执行任何非查询命令，如 Insert、Update 和 Delete，以从目标数据库中删除选表。

图 8.65 显示了该的一些示例代码。
另一个方法是 ExecuteQuery()，它可以用于执行任何查询 SQL 命令。使用该方法的代码示例如图 8.66 所示。

基于上面的代码，我们应该清楚地了解如何使用这些方法执行相关查询以获得我们所需的结果。
在 DataContext 中提供这些方法讨论的主要目的是扩展或合并我们的用法，以选择其他方式对数据进行查询。

图 8.65 使用 ExecuteCommand() 方法的一些真实代码示例。

```cs
// 使用 ExecuteQuery() 从 Student 表中查询一条记录
CSE_DEPTDataContext cse_dept = new CSE_DEPTDataContext();
var sr = cse_dept.ExecuteQuery<Student>(@"SELECT * FROM Student WHERE student_id = {0}", "J86577");
```

图 8.66 通过 ExecuteCommand() 方法查询学生表的代码示例。

## 474 使用 C# 进行 SQL Server 数据库编程

...各种方法。因为有时对于某些应用程序，LINQ to SQL 方法无法为特定场景提供充分支持，我们的情况也是如此：我们将 Faculty 声明为 ASP 页面的名称（Faculty.aspx），但该名称与我们的 Faculty 表重名。为了解决这个问题，我们将在接下来的章节中使用 ExecuteCommand() 方法来执行非查询命令，如 Insert、Update 或 Delete。

需要明确的一点是，ExecuteCommand() 方法是一个更强大的方法，可以执行许多 SQL 命令。

接下来，让我们使用它在示例中向 Faculty 表执行数据插入操作。

### 8.7.4.4 插入查询的代码

在 Faculty 页面的设计视图（Design View）中双击 Insert 按钮，打开其 Click 方法并输入图 8.67 所示的代码。

让我们仔细查看这些代码，看看它是如何工作的。

- A. 首先声明一个 `byte[]` 图像和一个整数变量 `intinsert`，因为我们需要在执行数据插入时插入教员图像。整数变量用于获取 ExecuteCommand() 的运行结果。

- B. 在向数据库中插入任何数据之前，我们需要检查用户在点击此 Insert 按钮时是否选择了有效图像。这可以通过检查 `FileUpload` 类的 `HasFile` 属性来实现。如果没有选择图像，则会显示警告消息提醒我们先执行。

| WebINSQLObject | cmdInsert_Click(object sender, EventArgs args) |
| :--- | :--- |
| A | byte[] image; intinsert; |
| B | if (FileUpload.HasFile) { Response.Write("<script>alert(\'Select an image using FileUpload!')</script>"); ... (code continues) ... |

FIGURE 8.67 插入按钮点击方法的代码。

### 在 ASP.NET 中访问数据

- C. 否则，调用用户自定义方法 getFacultyImage() 来获取选定的教员图像并插入我们的示例数据库。

- D. 然后执行 DataContext 类的 ExecuteCommand() 方法，向数据库中的 Faculty 表插入一条新记录。其中一点是调用此方法的格式。值占位符必须是花括号 `{ }` 格式，并从 0 开始编号。在这些占位符之后，真实的参数值将按相同的顺序附加。

- E. 在数据库中插入新记录后，我们需要调用另一个用户自定义方法 CurrentFaculty() 来更新我们的 Faculty Name 控件 ComboName，以反映该插入操作。

- F. ExecuteCommand() 返回一个整数值，该值等于被修改的行数。如果返回值为零，则意味着我们的数据插入失败，没有插入记录。将显示警告消息以指示这种情况。

- G. 否则，数据插入成功。通过调用另一个用户自定义方法 ClearFaculty()（代码如下所示），清除 Faculty 页面中的所有文本框。此外，禁用 Insert 按钮以避免插入重复记录。

- H. 对于用户自定义方法 ClearFaculty()，逻辑非常直观，没有任何技巧。首先生成文本框数组 `fbox[]` 以包含 Faculty 页面中的所有文本框。然后清除所有文本框。

### 8.7.4.5 更新查询的代码

在 Faculty 页面的设计视图中双击 Update 按钮，打开其 Click 方法并输入图 8.68 所示的代码。

| WebINSQLObject | cmdUpdate_Click(object sender, EventArgs args) |
| :--- | :--- |
| A | byte[] image; |
| B | if (FileUpload.HasFile) { |
| C | Response.Write("<script>alert(\'Select an image using FileUpload!')</script>"); |
| D | else { |
| E | image = getFacultyImage(); |
| F | var fi = (from f in cse_dept.Faculties where f.id == txtFacultyID.Text select f).First(); |
| G | fi.name = txtName.Text; |
| H | fi.title = txtTitle.Text; |
| | fi.phone = txtPhone.Text; |
| | fi.college = txtCollege.Text; |
| | fi.image = image; |
| | cse_dept.SubmitChanges(); |
| | ComboName.Items.Clear(); |
| | CurrentFaculty(); |
| | } |

FIGURE 8.68 更新按钮点击方法的代码。

### 8.7.4.6 删除按钮的代码

在 Faculty 页面的设计视图中双击 Delete 按钮，打开其 Click 方法并输入图 8.9 所示的代码。

| WebINSQLObject | cmdDelete_Click(object sender, EventArgs args) |
| :--- | :--- |
| protected void cmdDelete_Click(object sender, EventArgs args) { |
| A | var faculty = (from fi in cse_dept.Faculties where fi.id == txtFacultyID.Text select fi).First(); |
| B | cse_dept.Faculties.Delete(faculty); |
| C | cse_dept.SubmitChanges(); |
| D | // clean all textboxes
| | txtFacultyID.Text = string.Empty; |
| | txtName.Text = string.Empty; |
| | txtTitle.Text = string.Empty; |
| | txtOffice.Text = string.Empty; |
| | txtPhone.Text = string.Empty; |
| | txtEmail.Text = string.Empty; |
| E | PhotoBox.Image.Url = null; |
| F | ComboName.Items.Clear(); |
| G | CurrentFaculty(); |
| | } |

FIGURE 8.9 删除按钮点击方法的代码。

