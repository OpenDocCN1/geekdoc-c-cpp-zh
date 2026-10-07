

# 在 ASP.NET 中访问数据

像之前所样，打开 Faculty（教师）表单的代码页，我们首先在页面顶部添加与 SQL Data Provider 相关的命名空间，以便为 SQL Data Provider 的所有数据组件提供引用：

```
using System.Data;
using System.Data.SqlClient;
```

页面的代码可以分为三部分：Page_Load() 方法的代码、Select Click 方法的代码以及其他方法的代码。首先，让我们来处理 `Page_Load()` 方法的代码。

## 8.4.8.1 编写 Page_Load 方法的代码

在打开的代码页中，打开 `Page_Load()` 方法并输入图 8.22 所示的代码。
让我们仔细查看这段代码，看看它是如何工作的。

- A. 首先在此命名空间中添加了一些与服务器数据提供程序相关的命名空间，因为我们需要使用位于这些命名空间中的某些服务器数据组件。
- B. 创建了一个字段级文本框 `FacultyTextBox[]`，因为我们需要这个数组来存储七条教师信息并在这些文本框中显示它们。
- C. 在对数据库执行操作之前，我们需要确保设置了有效的数据库连接，以便允许我们在项目和数据库之间传输数据。利用 `Application` 状态（用于存储全局连接对象变量）在数据库未连接时进行检查并连接数据库。

| SQLSelectProject | Page_Load(object sender, EventArgs) |
| :--- | :--- |
| using System; using System.Web.UI.Controls; using System.Data; using System.Data.SqlClient; namespace SQLSelect_Project { public partial class Faculty : System.Web.UI.Page { private TextBox[] FacultyTextBox = new TextBox[]; protected void Page_Load(object sender, EventArgs e) { if ((SqlConnection)Application["sqlConnection"]).State == ConnectionState.Open) { ((SqlConnection)Application["sqlConnection"]).Open(); } } ComboName.Items.Add("Ying Balai"); ComboName.Items.Add("David Bhalla"); ComboName.Items.Add("Black Anderson"); ComboName.Items.Add("Steve Johnson"); ComboName.Items.Add("Jenney King"); ComboName.Items.Add("Alice Brown"); ComboName.Items.Add("Dobby Angles"); ComboName.Items.Add("Jeff Henry"); } } } |

图 8.22 `Page_Load()` 方法的代码。

- D. 随着项目的运行，用户每次点击 Select 按钮执行数据查询时，都会向数据库服务器和 Web 服务器发送请求（它们可以是同一台服务器）。然后，Web 服务器在收到此请求后（`IsPostBack = true`）将向客户端发布刷新后的 Faculty 页面。每次发生这种情况，`Page_Load()` 方法都会被激活并重复到组合框 `ComboName` 的末尾。为了避免这种重复，你需要检查页面的 `IsPostBack` 属性，并在项目启动时仅将教师成员添加到组合框中（`IsPostBack = false`）。关于 `AutoPostBack` 属性的详细讨论，请参考第 8.4.9 节。

接下来，我们需要开发 Select 按钮 Click 方法的代码，以便执行数据库查询。

## 8.4.8.2 编写 Select按钮方法的代码

这段代码的功能是对数据库进行查询，根据用户从 Faculty Name 组合框控件选择的教师检索教师信息，并将这些检索信息显示在 Faculty 页面的文本框和教师图像上。

在 Faculty 表单的设计视图中双击此 Select 按钮，打开其 Click 方法，并将图 8.23 所示的代码输入此方法中。
让我们仔细查看这段代码，看看它是如何工作的。

- A. 此处声明了包含 `SELECT` 语句的查询字符串，我们需要使用此字符串作为命令文本。该查询的动态参数是 `@name`，它是项目运行期间用户选择的教师。
- B. 此处声明了作为 `Command` 和 `DataReader` 对象的所有数据组件，我们需要它们在稍后执行数据查询。
- C. 通过将关联组件分配给 `Command` 对象进行初始化。这些组件包括存储在 `Application` 状态中的全局连接对象、`CommandType` 和 `CommandText`。

| SQLWebServerProject | cmdSelect_Click(object sender, EventArgs e) |
| :--- | :--- |
| A | protected void cmdSelect_Click(object sender, EventArgs e) { |
| B | string cmd = "SELECT faculty_id, faculty_name, title, phone, college, email, image FROM Faculty "; |
| C | string cmdString = cmd + " FACULTY_name = @name"; |
| D | SqlCommand sqlCommand = new SqlCommand(); |
| E | SqlDataReader sqlDataReader; |
| F | sqlCommand.Connection = new SqlConnection("ConnectionString"); |
| G | sqlCommand.CommandType = CommandType.Text; |
| H | sqlCommand.Parameters.Add("@name", SqlDbType.VarChar, Value = ComboName.Text); |
| I | sqlDataReader = sqlCommand.ExecuteReader(); |
| J | if (sqlDataReader.HasRows) { |
| K | FacultyPage(sqlDataReader); |
| L | } else { |
| M | Response.Write("<script>alert('No matched faculty found!')</script>"); |
| N | sqlDataReader.Close(); |
| O | sqlCommand.Dispose(); |
| P | } |

图 8.23 Select按钮的代码。

- D. 通过将动态参数名称和值分配给 `Parameter` 对象。
- E. 调用 `Command` 对象的 `ExecuteReader()` 方法执行查询以检索教师信息，并将其分配给 `DataReader` 对象。
- F. 通过检查 `DataReader` 的 `HasRows` 属性可以判断查询是否成功。如果大于零，则意味着从 Faculty 表中检索到了至少一行，查询成功，用户定义的方法 `FillFaculty()` 将在后续部分填充 Faculty 页上的文本框。
- G. 否则，如果 `HasRows` 属性等于零，则意味着没有从数据库中检索到行，查询失败。通过调用 `Response` 对象的 `Write()` 方法在客户端显示警告消息。
- H. 查询后释放用于此查询的所有数据组件。此时我们有了 Select 按钮 Click 方法的第一部分。现在是该方法的第二部分。

## 8.4.8.3 编写其他方法的代码

接下来处理 Faculty 页中其他方法的代码。这包括：
- 1) 用户定义的方法 `FillFaculty()`。
- 2) Back按钮的 Click 方法。

首先处理用户定义的方法 `FillFaculty()`。该方法的功能是用查询到的信息填充文本框并在页面中显示图像。Windows 应用程序和 Web 应用程序在显示图像的一个显著区别是，Web 应用程序利用 `System.Web.Controls.Image` 的 `ImageUrl` 属性访问匹配的教师照片，而在 Windows 应用程序中，必须使用 `System.Drawing` 来在文件上显示图像。

```csharp
private void FillFaculty(SqlDataReader FacultyReader)
{
  int index;
  TextBox[] fbox = { txtFacultyID, txtName, txtPhone, txtCollege, txtEmail };
  while (FacultyReader.Read())
  {
    for (index = 0; index < FacultyReader.FieldCount - 2; index++)
    {
      fbox[index].Text = FacultyReader.GetString(index);
      byte[] image = (byte[])FacultyReader["Image"];
      string img = Convert.ToBase64String(image);
      fbox[index].ImageUrl = String.Format("data:image/jpeg;base64,{0}", img);
    }
  }
}
```

图 8.24 用户定义的方法 `FillFaculty()` 代码。

## 使用 C# 进行 SQL 数据库编程

让我们仔细查看这段代码。

- A. 定义第一个计数器 `intIndex`，用于循环从示例数据库的 Faculty 表中获取每一列。
- B. 生成文本框数组 `box[]`，用于稍后通过循环填充存储在 DataReader 中的七列数据。
- C. 只要 `Read()` 方法为真，就会执行 `while` 循环，这意味着从 DataReader 中读取了有效记录。如果未从 DataReader 读取有效记录，该方法将返回 `false`。在此应用程序中，此 `while` 循环执行一次，因为从 DataReader 中只读取了一行（一条记录）。
- D. 利用 `for` 循环从 DataReader 对象中读取每个数据列，并通过 `box[]` 将它们分配给 Faculty 页上的关联文本框控件。index 用于识别 DataReader 的每一列。终端列数等于 `FieldCount – 2`，因为教师 表的最后一列 (7) 是教师图像 fimage，这是一个不可计数的对象。教师记录的七列文本信息从列 0 到列 6 排（FieldCount = 7）。
- E. 由于图像以二进制数据格式存储在最后一列，因此我们需要获取并转换为 `byte[]`。
- F. 因为 Web 页面没有可用的 Picture 对象，我们需要将图像从 `byte[]` 数组转换为 64 位字符串，并将其分配给 Faculty 页中 Image 对象的 `ImageUrl` 属性。

最后，让我们处理 Back 按钮 Click 方法的代码。这段代码的功能在点击此按钮时返回 Selection 页。在 Faculty 页窗口的设计视图中双击 Back 按钮打开此方法，并输入图 8.25 所示的代码。
这段代码直观且易于理解。当用户点击此按钮时，执行 `Response` 对象的 `Redirect()` 方法将客户端从当前 Faculty 页重定向回 Selection 页。点击此按钮向服务器发送请求时，服务器将 Selection 页返回给客户端。
现在我们完成了 Faculty 页的所有代码开发。现在是我们运行项目进行测试了。点击 IIS Express 运行我们的项目。在登录页输入用户名用户名密码（例如 `jerry`），选择一个教师（如 Yang Bai），然后点击 Select 按钮从数据库检索选定的教师信息。与所选教师相关的所有信息都检索并显示在 Faculty 页中，如图 8.26 所示。
点击 Back 按钮返回 Selection 页，然后点击 Exit 按钮终止我们的项目。这样，我们的 Web 应用程序就成功了。

| SQLWebSelect Project | cmdBack_Click(object sender, EventArgs e) |
| :--- | :--- |
| protected void cmdBack_Click(object sender, EventArgs e) { 
  Response.Redirect("Selection.aspx");
 } |

图 8.25 Back按钮点击方法的代码。

