
```html
      OnClick="BulletedList_Click" DisplayMode="LinkButton">

      <asp:ListItem>美国</asp:ListItem>

      <asp:ListItem>英国</asp:ListItem>

      <asp:ListItem>芬兰</asp:ListItem>

      <asp:ListItem>俄罗斯</asp:ListItem>

      <asp:ListItem>瑞典</asp:ListItem>

      <asp:ListItem>爱沙尼亚</asp:ListItem>

    </asp:BulletedList>

    <asp:Label ID="Label1" runat="server"></asp:Label>

  </form>

</body>

</html>
```

```csharp
<%@ Page Language="C#" %>
protected void BulletedList_Click(object sender, System.UI.WebControls.BulletedListEventArgs e)
{
    Label1.Text = "选中项的索引: " + e.Index +
    "<br>选中项的值: " + BulletedList1.Items[e.Index].Text;
}
```

```vb
Dim blSelectedValue As ListItem = BulletedList1.Items(e.Index)
```

```csharp
ListItem blSelectedValue = BulletedList1.Items[e.Index];
```

现在你已经看到了如何在代码中声明式地放置项创建项目符号列表，请看如何从存储在数据存储中的项创建项目符号列表。以下示例显示了如何使用 `BulletList` 控件来数据绑定来自数据存储的结果；所有信息均检索自一个 XML 文件。

第一步是在列表 3-31 中创建 XML。

### 列表 3-31：FileChoices

使用 `DataSourceID` 属性指向 `XmlDataSource` 以从 `FileChoices` 文件中填充 `BulletedList` 控件，列表 3-32：动态填充 BulletedList

```html
<% Page Language="VB" %>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
  <title>BulletedList 控件</title>
</head>
<body>
  <form id="form" runat="server">
    <asp:BulletedList ID="BulletedList1" runat="server"
      DataSourceID="XmlDataSource" DataField="Title">
    </asp:BulletedList>
    <asp:XmlDataSource ID="XmlDataSource" runat="server"
      DataFile="FileChoices.xml">
    </asp:XmlDataSource>
  </form>
</body>
```

在此示例中，你使用 `DataSourceID` 属性指向 `XmlDataSource`，通过 `Title` 属性从 `FileChoices` 文件填充 `BulletedList` 控件，图 3-6 显示了结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_215_0.png)

`XmlDataSource` 控件在绑定时仅暴露 XML 属性，因为之前的示例中 `Title` 是一个属性。如果你想处理元素，则可以使用 `XmlDataSource` 控件的 `TransformFile` 属性通过 XSLT 转换转换为元素。

# HiddenField 控件

多年来，开发者一直在 Web 页面中使用隐藏字段处理状态管理。`<input type="hidden">` 元素非常适合存储那些没有安全担忧的项目。这些项是存储在页面本身的占位符，而不是使用 Session 对象将数据与页面的视图状态交织。视图状态是存储信息的另一种方式，但许多开发者会关闭它以避免性能下降。

## 第 3 章：ASP.NET Web 服务控件

然而，要使用该文件，你必须对页面进行一些修改。例如，你需要在页面的 `<form>` 元素中添加 `entype="multipart/form-data"`。

ASP.NET 2.0 引入了一个新的 FileUpload 控件，它使文件上传到服务器的能力变得非常简单。当赋予页面上传文件的功能时，你只需要包含新的 `<asp:FileUpload>` 控件，ASP.NET 就会处理其余的所有工作，为页面的 `<form>` 元素添加 `enctype` 属性。

### 使用 FileUpload 控件上传文件

文件上传到服务器后，你还可以获取已上传文件的属性，并将它们显示给终端用户，或者在页面的后置代码中使用这些值。列表 3-34 显示了使用新 `FileUpload` 控件的示例。该页面包含一个 `FileUpload` 控件，以及一个按钮（Button）控件和一个标签（Label）控件。

#### 列表 3-34：使用新的 FileUpload 控件上传文件

```VB
<% Page runat="server">
Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
    If FileUpload.HasFile
        Try
            FileUpload.SaveAs("C:\uploads" & \
            FileUpload.FileName)
            Label1.Text = "File name: " & \
            FileUpload.PostedFile.FileName & "<br>" &
            "File size: " & \
            FileUpload.PostedFile.ContentLength & " kb<br>" &
            "Content type: " & \
            FileUpload.PostedFile.ContentType
        Catch ex As Exception
            Label1.Text = "ERROR: " & ex.Message.ToString()
    End Try
    Else
        Label1.Text = "You have not specified a file."
    End If
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>FileUpload Server Control</title>
</head>
<body>
<form id="form1" runat="server">
    <p>
        <asp:FileUpload ID="FileUpload1" runat="server" />
        <asp:Button ID="Button1" runat="server" Text="Upload" OnClick="Button1_Click" />
    </p>
    <asp:Label ID="Label" runat="server"></asp:Label>
</form>
</body>
</html>
```

```csharp
<%@ Page Language="C#" AutoEventWireup="false" %>
<script runat="server">
    protected void Button1_Click(object sender, EventArgs args)
    {
        if (FileUpload1.HasFile)
        {
            try
            {
                FileUpload1.SaveAs("C:\uploads\" + FileUpload1.FileName);
                Label1.Text = "File name: " + FileUpload1.PostedFile.FileName + "<br>" +
                              "File size: " + FileUpload1.PostedFile.ContentLength + " kb<br>" +
                              "Content type: " + FileUpload1.PostedFile.ContentType;
            }
            catch (Exception ex)
            {
                Label1.Text = "ERROR: " + ex.Message();
            }
        }
        else
        {
            Label1.Text = "You have not specified a file.";
        }
    }
</script>
```

从这个示例中，你可以看到整个过程非常简单。页面上的按钮启动了上传过程。`FileUpload` 本身并不启动上传过程；必须通过另一个事件（如 `Button_Click`）来启动。

首先需要注意的一点是 `FileUpload` 控件位于页面上。ASP.NET 3.5 通过添加适当的 `enctype` 属性修改了页面的表单元素。同样注意，`FileUpload` 控件被转换为 `<input type="file">` 元素。

文件上传后，第一个检查（在 `Button_Click` 事件处理程序中）会检查是否真的将一个文件引用放置在了 `<input type="file">` 中。如果指定了文件，则将尝试使用 `FileUpload` 控件的 `SaveAs` 方法将引用的文件上传到服务器。该方法接受一个 `String` 参数，该参数应该包含你想保存文件的位置。在列表 3-34 使用的 `String` 参数中，你可以看到文件被保存到名为 `Uploads` 的文件夹，该文件夹位于 `C:\` 盘。

`PostedFile.FileName` 属性用于将保存的文件命名为与其源文件相同的名称。如果你想为文件重命名，只需以以下方式使用 `SaveAs` 方法：

```
FileUpload.SaveAs("C:\Uploads\UploadedFile.txt")
```

你也可以为文件指定一个上传时的时间名称：

```
FileUpload.SaveAs("C:\Uploads\" + System.DateTime.Now.ToString() + ".txt")
```

上传成功完成后，页面上的标签将填充已上传文件的元数据。在示例中，获取并显示了文件的名称、大小和类型，以便用户查看。当文件上传到服务器时，生成的界面类似于图 3-37 所示。

![](img/eb54f286ad47e89bbf833e2d279e6dd_219_0.png)

图 3-37

将文件上传到另一个服务器可能是一个容易出错的过程。在代码中使用适当的异常处理来上传文件是非常关重要的。

### 赋予 ASP.NET 上传文件的权限

当用户通过应用程序中的 `FileUpload` 控件将文件上传到 Web 服务器时，可能会遇到错误。可能是因为目标文件夹对于 ASP.NET 使用的账户是不可写的。这就是为什么使用 `Try-Catch` 语句来上传文件。

### 理解大小限制

你可能会在使用 `FileUpload` 控件遇到问题，但你应该意识到存在某些限制。当通过应用程序上传时，默认限制为 4 MB (4096 KB)；如果上传大于该的文件，传输将失败。这种现象被称为拒绝服务攻击。然而，NET 的巨大优点之一是可以更改默认设置。要更改允许的文件大小，你可以在根 `web.config`（位于 `C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\config`）或应用程序的 `web.config` 中进行更改。

`web.config` 中的 `<httpRuntime>` 部分见列表 3-35。

## 第 3 章：ASP.NET 服务器控件

此示例将 `maxRequestLength` 属性的值更改为 10 KB（约 10 MB）。通过此项设置，您的用户可以向服务器上传大小为 10 MB 的文件。在更改 `maxRequestLength` 属性时，请注意 `executionTimeout` 属性的设置。该属性设置了请求在服务器 ASP.NET 关闭连接（无论是否完成）之前尝试执行的时间（以秒为单位）。默认值是 90 秒。如果超过了此时间限制，用户将在浏览器中收到超时错误。如果您打算允许较大的请求，请记住它们耗的时间会比较小的请求更长。如果您增加了 `maxRequestLength` 属性的大小，应该检查是否也设置了 `executionTimeout` 属性。

> 如果您处理的是较小文件，建议通过减小 `maxRequestLength` 属性的值来减少分配给请求的大小。这可以保护您的应用程序免受拒绝服务攻击。

在 `web.config` 文件中进行这些更改将适用于服务器上的所有应用程序。如果您只想对当前工作的应用程序应用此设置，请在应用程序的 `web.config` 文件中应用 `<httpRuntime>` 节点，这将覆盖根 `web.config` 文件中的任何设置。确保您的节点位于配置文件中 `<system.web>` 节点之间。

### 从同一页面上传多个文件

到目前为止，您已经看到了一些如何轻松将文件上传到服务器的示例。现在，让我们看看如何从单个页面向服务器上传多个文件。

Microsoft .NET Framework 中没有内置功能允许您从单个 ASP.NET 页面上传多个文件。然而，只需稍作努力，您就可以轻松完成此任务，就像过去使用 .NET 1.x 一样。

技巧是将 `System.IO` 类导入到您的 ASP.NET 页面中，然后使用 `HttpFileUpload` 类（注：此处通常指相关集合处理）来捕获 `Request` 对象中发送的所有文件。这种方法允许您从单个页面上传任意数量的文件。

如果您愿意，完全可以简单地单独处理页面上的每一个 `FileUpload` 控件，如列表 3-36 所示。

#### 列表 3-36：单独处理每个 FileUpload 控件

```VB
If FileUpload1.HasFile Then
  Handle file
End If
If FileUpload2.HasFile Then
  Handle file
End If
C#
if (FileUpload1.HasFile) {
  // Handle file
}
```

```csharp
if (FileUpload2.HasFile) {
    // Handle file
}
```

如果您处理的文件上传数量有限，这种方法是有效的；但同时在某些情况下，您可能想使用 `HttpFileCollection` 类来处理文件。如果您在 ASP.NET 中处理的是动态生成的服务器控件列表，这一点尤为真实。

作为一个示例，您可以构建一个包含三个上传控件和一个提交提交按钮（使用 `Button` 控件）的 ASP.NET 页面。当用户点击提交按钮且文件提交到服务器后，后台代码将处理这些文件并将它们保存到服务器上的特定位置。文件保存后，将显示 ASP.NET 页面中提交的文件信息（见列表 3-37）。

#### 列表 3-37：向服务器上传多个文件

```VB
Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
Dim filePath As String = "C:\Uploads"
Dim uploadedFiles As HttpFileCollection = Request.Files
Dim i As Integer = 0
Do Until i = uploadedFiles.Count
    Dim userPostedFile As HttpPostedFile = uploadedFiles(i)
    Try
        If (userPostedFile.ContentLength > 0) Then
            Label.Text += "File #:" & (i + 1) & "<br>"
            Label.Text += "File Content Type: " & & \
                userPostedFile.ContentType & "<br>"
            Label.Text += "File Size: " & & \
                userPostedFile.ContentLength & "<br>"
            Label.Text += "File Name: " & & \
```
