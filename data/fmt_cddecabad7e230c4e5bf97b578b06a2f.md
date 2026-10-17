
# 8.4.9.6 为自定义方法 FillCourseReaderTextBox 编码

在打开的 Course 表单页面上，将图 8.33 所示的代码放入 Course 类中，以创建此自定义方法。
让我们来看这段代码，看看它是如何工作的。

- A. 创建了一个计数器 `intIndex` 和文本框数组 `cbox`。前者用于 `for` 循环的计数器，以便从 `CourseReader` 中提取每一列，后者作为数据处理程序，接收每一列并将其显示在课程页面相关的文本框中。
- B. 使用 `while` 和 `for` 循环从 DataReader 中逐条获取所有课程信息。`Read()` 方法用于设置 `while` 循环的条件。返回 true 表示从 DataReader 中读取了有效数据，返回 false 则表示无法从 DataReader 中读取到有效数据，换句话之，没有可用数据且所有数据已读取完毕。`for` 循环使用 `FieldCount`–1 作为终止条件，因为 DataReader 中第一列的索引是 0 而不是 1。每个读取出的数据都被转换为字符串，并分配给文本框对象控件中相关的文本框。

至此，我们已经完成了该表单的所有编码工作。现在运行项目来测试此表单。点击 `IIS Express` 按钮运行项目。在打开的页面中输入用户名 `jerry` 和密码 `test`，从 `Selection` 控件中选择 `Course Information` 项目，然后选择 `Course` 页面。点击 `Back` 按钮按系检索所有课程并显示在 CourseList 框中。

点击 CourseList 中的任何项进行选择；与所选 `course_id` 相关的详细信息立即将在六个文本框中显示，如图 8.35 所示。
点击 `Back` 按钮返回 Selection 页面，你可以点击 `Selection` 页面上的任何其他项目来执行关联查询，或点击 `Exit` 按钮终止应用程序。我们的 Web 应用成功运行。

用于从 SQL Server 数据库查询数据的完整 Web 应用项目 `SQLWebSelect Project` 可以在 CRC Press ftp 站点 Students 文件夹下的 `Class Projects/Chapter 8` 文件夹中找到（参见第 1 章的图 1.2）。

在运行项目时，可能出现的 Bug 是当点击 CourseList 选择某个 `course_id` 时，服务器没有响应。这是因为 Course List 框的 `AutoPostBack` 属性未正确设置。可以通过将该属性设置为 `true` 来解决此问题，以便服务器将其回传。

# 在 ASP.NET 中访问数据

图 8.35 详细课程信息。

# 使用 C# 进行 SQL Server 数据库编程

在下一节中，我们将讨论如何向 SQL Server 数据库 Web 应用插入新记录。

# 8.5 开发 ASP.NET Web 应用向 SQL 数据库插入数据

在本节中，我们将讨论如何通过 Web 页面向 SQL Server 数据库插入新记录。为此，我们可以修改上一节开发的项目 `SQLSelect Project`，将其变为我们新的 Web 应用 `SQLWebInsert Project`。

执行以下操作将项目 `SQLWebSelect Project` 变为新 Web 应用 `SQLWebInsert Project`。

- 1. 打开 Windows 资源管理器或文件资源管理器，在本地机器（`C:\Chapter 8`）上找到 Web 应用文件夹 `SQLSelectSelection`。
- 2. 右键点击该解决方案文件夹并选择“复制项目”以复制包含项目的解决方案，并将该文件夹粘贴到本地机器的相同位置，例如 `C:\Chapter 8`。
- 3. 分别将文件夹名称重命名为 `SQLWebInsert Project` 和 `SQLWebInsert Project`。
- 4. 展开新的解决方案文件夹 `SQLWebInsert Solution`，点击新的项目文件夹 `SQLWebInsert Project` 以打开它。
- 5. 将以下两个文件的名称从 `SQLWebSelectProject.csproj` 和 `SQLWebSelectProject.csprojuser` 改为 `SQLWebInsertProject.csproj` 和 `SQLWebInsertProject.csprojuser`。
- 6. 现在双击新项目 `SQLWebInsertProject.csproj` 在 Visual Studio 2022 中打开它。

需要注意的一个关键点是，我们更改了解决方案和项目的名称，但项目的命名空间保持不变，因为将命名空间从 `SQLSelect_Project` 改为 `SQLWeb_Project` 将是一个非常复杂的过程。
让我们从 Faculty 页面开始，向我们 SQL 示例数据库中的 Faculty 表插入一条新的教师记录。

# 8.5.1 开发向 Faculty 表插入新记录的代码

要向我们示例数据库中的 Faculty 表插入一条新的教师记录，我们需要使用 Faculty 页面上的 Insert 按钮及其事件方法。此 Insert 按钮及其事件的功能是：

- 1. 为了向数据库插入新的教师记录，我们需要在 Faculty 页面的文本框中输入七项信息。这些信息包括 `faculty_id`、教师姓名、职称、办公室、学院和电子邮件。
- 2. 除了插入七项新的教师信息外，我们可能还需要插入一张与该姓名对应的新教师图像。在第 8.4.7 节创建 Faculty 页面时提到过，此页面添加了一个 FileUpload 组件 `FileloadImage`，它由一个带有“浏览”按钮的组合框表示。使用此 FileUploadimage 的目的是允许用户从计算机中浏览并选择一个教师图像文件，作为新的教师图像插入数据库中。如果无法选择新的教师图像，则应选择并使用原始教师图像。
- 3. 在所有文本框中输入所有信息后，你可以点击 Insert 按钮通过 Web 页面将此新记录插入到示例数据库的 Faculty 表中。

# 在 ASP.NET 中访问数据 447

现在让我们开始为此 Faculty 页面创建代码。编码过程可以分为三个部分：`Page_Load()` 的编码、Insert 按钮点击方法的编码以及其他自定义方法的编码。

# 8.5.2 开发 Page_Load 方法的代码

我们需要修改此 `Page_Load()` 方法内部的代码，使其能够从我们的示例数据库中检索当前或更新的教师。其原因是，执行此插入操作后教师将进行更新，在 ComboName 组合框中我们需要获取并更新他们任何一个人的详细信息。

打开 `Page_Load()` 方法，并将图 8.36 所示的代码输入到方法的底部。

唯一的修改是在此方法添加了新的自定义方法 `CurrentFaculty()`。使用此方法的目的是从我们示例数据库的 Faculty 表中获取当前或更新的教师，并将它们显示在 Faculty Name 组合框中，以便使用户可以选择它们执行操作。

在 Faculty 页面打开的代码窗口中，输入图 8.37 所示的代码生成此方法。让我们仔细查看这段代码看看它是如何工作的。

- 首先声明查询字符串，以从 Faculty 表查询所有当前教师姓名。
生成两个数据对象 `sCommand` 和 `sReader`，它们用于执行此数据查询。需要注意的是，为以下使用了特殊的初始化方法

**图 8.36** 修改后的 `Page_Load()` 方法代码。

**图 8.37** 自定义方法 `CurrentFaculty()` 的详细代码。

```
private void CurrentFaculty() {
 string cmd = "SELECT faculty_name FROM Faculty";
SqlCommand sCommand = new SqlCommand(cmd
```

# 使用 C# 进行 SQL Server 数据库编程

`SqlCommand` 通过其查询字符串和连接对象两个参数协同工作，简化了此赋值。然后调用 `SqlCommand` 对象的 `ExecuteReader()` 方法来运行查询。查询结果被返回并赋值给 `SqlDataReader` 对象 `reader`。

- C. 在 Faculty Name（教职名称）组合框填充了所有更新后的教职名称之前，必须对其进行清理，这一步是必要的，否则所有先的教职名称将与此新添加的内容合并。
- D. 使用带有 `Read()` 方法的 `while` 循环来检查并选取从 Faculty 表第一列（列 0）中检索到的每条数据，因为只检索了一个数据列（教职名称）。然后，将每一行分配或添加到 Faculty Name 组合框中。使用同步方法 `GetString(0)` 将检索到的行从对象转换为字符串值。
- E. 最后，释放所使用的两个对象 `reader` 和 `sCommand`。

接下来，让我们来构建插入（Insert）按钮事件方法的代码。

## 8.5.3 开发插入按钮点击方法的代码

在 Faculty 页面的设计视图中双击 Insert，打开 Insert 的 Click 方法，并将图 8.38 所示的代码输入到此方法中。让我们仔细查看这段代码看看它是如何工作的。

- A. 声明了插入查询字符串，它包含了八项信息，与数据库中 Faculty 表中的八列相关。
- B. 在方法中声明了数据组件和局部变量。`SqlCommand` 对象 `sqlCommand` 和一个本地整数变量 `intInsert` 用于执行数据插入操作，并持有代码执行结果的结果。

```
protected void cmdInsert_Click(object sender, EventArgs args)
{
    string cmdString = "INSERT INTO Faculty (faculty_id, faculty_name, title, office, college, email, image)" +
                      "VALUES (@faculty_id, @faculty_name, @title, @office, @phone, @college, @image)";
    SqlCommand sqlCommand = new SqlCommand(cmdString);
    int intInsert;
    if (FileUpload.HasFile)
{
        Response.Write("<alert>Select an insert file using FileUpload!</script>");
    }
    else
{
        SqlCommand.Connection = new SqlConnection("SqlConnection");
        SqlCommand.CommandType = CommandType.Text;
        SqlCommand.CommandText = cmdString;
        InsertParameters.Add(sqlCommand);
        intInsert = sqlCommand.ExecuteNonQuery();
        SqlCommand.Dispose();
        if (intInsert == 0)
        {
            Response.Write("<alert>The data insertion is failed!</script>");
        }
        cmdInsert.Enabled = false;
    }
}
```

# 在 ASP.NET 中访问数据

- C. `FileUpload` 对象允许用户选择并获取要插入数据库的教职图片。如果用户在七个文本框中输入了七项信息进行插入，形成了一个新的教职记录，但忘记选择教职图片，通过检查 `FileUploadImage` 的 `HasFile` 属性可以判断是否选择了有效的教职图片。如果该属性为 `false`，则向用户显示警告消息要求其选择图片。
- D. 否则，如果 `HasFile` 属性返回 `True`，意味着选择了有效的教职图片，则可以初始化 `SqlCommand` 对象来执行此数据插入操作。
- E. 稍后将构建自定义方法 `InsertParameters()`，其作用是将所有输入参数赋值给命令对象的 `Parameters` 属性。
- F. 调用命令对象的 `ExecuteNonQuery()` 方法运行插入查询以执行此数据插入操作。
- G. 执行清理工作以释放方法中使用的所有对象。
- H. `ExecuteNonQuery()` 方法将返回一个值，指示此数据插入是否成功。此返回数据的值等于成功插入 Faculty 表的行数。如果返回 0，则意味着没有行被插入数据库，此时将使用此方法显示警告消息。否则，数据插入成功。
- I. 在数据插入操作完成后，将执行另一个自定义方法 `CurrentFaculty()`，从我们的数据库中获取当前或更新的成员，并将更新后的教职名称显示到 Faculty Name 组合框中。
- J. 在记录插入到数据库后，禁用插入按钮。为了避免向数据库多次插入同一条记录，当 Faculty ID 文本框的内容发生变化时，插入按钮将再次启用，这意味着将插入一条新的教职记录。

接下来让我们处理所有其他方法的代码开发，包括所有将用于此数据插入操作的相关自定义方法。

## 8.5.4 开发其他方法的代码

其他方法的代码包括以下内容：

- 1. `faculty_id` 文本框的 `System TextChanged` 事件。
- 2. 自定义方法 `InsertParameters()`。
- 3. 自定义方法 `getFacultyImage()`。

如所述，当新的教职记录成功插入到示例数据库的 Faculty 表后，应禁用插入按钮以避免重复插入。然而，当另一条教职记录准备好插入时，该按钮应重新启用。通过检查 `faculty_id` 文本框的内容，我们可以识别是否准备好插入新的教职记录。如果该内容发生变化，意味着输入了新的 `faculty_id`，该文本框的 `TextChanged` 事件会被触发，在该事件上，我们将启用按钮。

要实现这一点，在 Faculty 页面的设计视图中双击 `faculty_id` 文本框以打开其 `TextChanged` 事件方法，并输入代码行：

```c
cmdInsert.Enabled = true ;
```

自定义方法 `InsertParameters()` 的详细代码如图 8.39 所示。

# 使用 C# 进行 SQL Server 数据库编程

**图 8.39** 方法 `InsertParameters()` 的代码

```
private void InsertParameters(SqlCommand cmd) {
  byte[] bimage;
  bimage = getFaceImage();
  cmd.Parameters.Add("@id", SqlDbType.Char).Value = tfaceID.Text;
  cmd.Parameters.Add("@name", SqlDbType.Char).Value = tname.Text;
  cmd.Parameters.Add("@title", SqlDbType.Char).Value = ttitle.Text;
  cmd.Parameters.Add("@office", SqlDbType.Char).Value = toffice.Text;
  cmd.Parameters.Add("@phone", SqlDbType.Char).Value = tphone.Text;
  cmd.Parameters.Add("@college", SqlDbType.Char).Value = tcollege.Text;
  cmd.Parameters.Add("@email", SqlDbType.Char).Value = temail.Text;
  cmd.Parameters.Add("@image", SqlDbType.Binary).Value = bimage;
}
```

**图 8.40** 自定义方法 `getFaceImage()` 的详细代码

这段代码直观且易于理解。通过第一个 `byte[]` 数组生成图像，并调用另一个自定义方法 `getFaceImage()` 来获取选定的脸。通过使用命令对象 `Parameters` 类的 `Add()` 方法将每项新信息分配给输入参数。

# 在 ASP.NET 中访问数据

E. 然后，将选定的教师图像文件通过系统方法 `SaveAs()` 保存到该默认或新创建的文件夹中。

F. 通过将教师图像名称赋值给 `ImageUrl` 属性，将选定的教师图像显示在教师图像框（PictureBox`）中。
