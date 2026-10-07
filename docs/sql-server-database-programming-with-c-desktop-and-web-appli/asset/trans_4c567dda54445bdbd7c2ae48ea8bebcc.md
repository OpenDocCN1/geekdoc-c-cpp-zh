

# ASP.NET 服务

| WebClientSQLUPdt | cmdDelete_Click(object sender, EventArgs e) |
| :--- | :--- |

```c
protected void cmdDelete_Click(object sender, EventArgs e)
{
    WebClientSQLUPdt wsDelete = new WebClientSQLUPdt.Project.wsServiceUpdt.Delete;
    wsDelete = new WebClientSQLUPdt.Project.wsServiceUpdt.WebServiceUpdt();
    WebClientSQLUPdt wsBase = new WebClientSQLUPdt.Project.wsSQLdt.Base;
    wsResult = new WebClientSQLUPdt.Project.wsSQLdt.Base();
    try
    {
        wsResult = wsDelete.DeleteStudentName(txtStudentName.Text);
        Response.Write("alert(" + errMsg + ")");
    }
    catch (Exception err)
    {
        errMsg = "Web service is error: " + err.Message;\n;
        Response.Write("alert(" + errMsg + ")");
    }
    if (wsResult.SQLOK == false)
    {
        Response.Write("alert(" + wsResult.Error + ")");
    }
    string[] st = new[] { txtID, txtStudentName, txtGPA, txtMajor, txtSchoolYear, txtEmail };
    for (int i = 0; i < st.Length; i++)
    {
        st[i].Text = String.Empty;
        ImageBox.Image = null;
    }
}
```

图 9.119 删除按钮方法的代码。

让我们来看这段代码，看看它是如何运行的。

创建了与我们的 Web 服务和基类相关的新实例，即 **wsSQLDelete** 和 **wsResult**，这些实例被用于访问我们在 Web 服务 **WebServiceUpdt Project** 中开发的 Web 方法 **wsDeleteStudentSP()**。关键点在于，我们当前项目的 **WebClientSQLUPdt_Project** 必须作为我们 Web 引用的前缀，因为该引用已添加到我们的当前项目中，但学生页面文件是在另一个项目或命名空间 **WebSelect_Project** 中构建的。创建了一个本地字符串变量 **errMsg**，它被用于解析错误源，该错误源将作为错误消息的一部分显示出来。

使用 Try-Catch 块调用了带有学生姓名 **txtName.Text**（作为标识符）的方法 **SQLDeleteSP**，以运行存储过程 **WebDeleteStudentSP()** 来对示例数据库执行此操作。

如果在数据删除操作期间遇到错误，将显示错误消息。需要注意的是此错误消息的显示格式。要在客户端的对话框中显示字符串，必须使用 JavaScript 函数 **alert("" + input_string + variable（其中该变量经过转义并由 "\\" 表示）作为参数）**。

除了系统错误检查方法外，我们还需要检查在 Web 服务项目返回类中定义的成员数据 **SQLOK**，以确保此数据删除操作无误。该成员数据返回 **false** 值表示删除过程中遇到了某些应用程序错误，并且存储在另一个成员 **Error** 中的错误源将被显示出来。

最后，执行清理工作，从文本框中清空所有与删除学生相关的信息。

G. 学生图片框也被清理了。

转到 **文件 | 保存所有内容** 菜单项以查看这些修改和开发。

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_656_0.png)

9.120 更新学生记录的运行结果。

现在我们已经完成了客户端数据更新和删除操作的所有开发。在运行此客户端项目以访问我们的 Web 服务对任何学生记录执行数据操作之前，请确保所有学生图片文件都已存储在您机器上的本地文件夹中，以便在项目运行时您能够从更新后的学生图片中选择一个。所有学生图片文件都可以在 CRC Press ftp 站点上的 Images@Students 文件夹中找到（参见第 1 章中的图 1.2）。之所以这样做是因为我们将使用虚拟文件夹或路径为我们的 Web 项目保存这些学生图片，以便它们在项目运行期间能够被找到。

首先运行我们的 Web 服务 WebServiceUpdate Project，然后通过点击 ILS Express 按钮运行我们的客户端项目 WebClientSQLUpdate Project。我们客户端项目的运行状态如图 9.120 所示。

与之前一样，我们想要更新学生记录 Tom Erica 为新的不同的信息或使用更新后的学生图片。然后，在打开的学生页面上，按照以下文本输入数据项作为更新后的学生记录：

| 学生 ID | T77896 |
| :--- | :--- |
| 姓名 | Toney Black |
| GPA | 3.20 |
| 学分 | 52 |
| 专业 | 信息系统工程 |
| 年级 | 大二 |
| 电子邮件 | tblack@college.edu |

现在到 FileUploadImage 控件并点击 Browse 按钮浏览到所有学生图片文件所在的虚拟文件夹或路径

选择学生图片文件 David.jpg，并点击 Open 按钮选择此图片文件。现在点击 Update 按钮执行此数据更新操作。更新结果如图 9.120 所示。点击 Back 按钮保存我们的项目。

为了确认此更新操作，通过服务器窗口打开我们的示例数据库 CSE_DEPT 和 Student 表，可以发现学生记录已更新。

# ASP.NET 服务

# 使用 C# 进行 SQL Server 数据库编程

![](img/d59a47501d0a20fc0460a49c469c6fb7_656_0.png)

9.120 更新学生记录的运行结果。

| 学生 ID | T77896 |
| :--- | :--- |
| 姓名 | Toney Black |
| GPA | 3.20 |
| 学分 | 52 |
| 专业 | 信息系统工程 |
| 年级 | 大二 |
| 电子邮件 | tblack@college.edu |

