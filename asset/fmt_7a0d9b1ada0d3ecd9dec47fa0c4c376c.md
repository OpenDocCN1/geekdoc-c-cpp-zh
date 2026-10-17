
```vb
<script runat="server">
    Protected Sub Button1_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        If Page.User.Identity.IsAuthenticated Then
            Profile.FirstName = TextBox1.Text
            Profile.LastName = TextBox2.Text
            Profile.Age = TextBox3.Text
            Profile.Member = Radiobutton1.SelectedItem.Text
            Profile.LastVisited = DateTime.Now.ToString()
            Label1.Text = "Stored information includes: <p>" &
                "First name: " & Profile.FirstName & &
                "<br>Last name: " & Profile.LastName & &
                "<br>Age: " & Profile.Age & &
                "<br>Member: " & Profile.Member & &
                "<br>LastVisited: " & Profile.LastVisited
        Else
            Label1.Text = "You must be authenticated!"
        End If
    End Sub
</script>
```

```html
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Personalization</title>
</head>
<body>
<form id="form1" runat="server">
    <p>First Name:<br>
    <asp:TextBox Id="TextBox1" runat="server"/></asp:TextBox></p>
    <p>Last Name:<br>
    <asp:TextBox Id="TextBox2" runat="server"/></asp:TextBox></p>
    <p>Age:<br>
    <asp:TextBox Id="TextBox3" runat="server" Width="50px"
        MaxLength="3"/></asp:TextBox></p>
    <p>Are you a member?<br>
    <asp:RadioButtonList Id="Radiobutton1" runat="server">
        <asp:ListItem Value="0">Yes</asp:ListItem>
        <asp:ListItem Value="1">No</asp:ListItem>
    </asp:RadioButtonList></p>
    <asp:Button Id="Button1" runat="server" OnClick="Button1_Click" Text="Submit" />
    <hr />
<asp:Label Id="Label1" runat="server"/></asp:Label>
</form>
</body>
</html>
```

```csharp
<@ Page Language="C#" %>
```

```csharp
<script runat="server">
    protected void Button1_Click(object sender, EventArgs e)
    {
        if (Page.User.Identity.IsAuthenticated)
        {
            Profile.FirstName = TextBox1.Text;
            Profile.LastName = TextBox2.Text;
            Profile.Age = TextBox3.Text;
            Profile.Member = Radiobutton1.SelectedItem.Text;
            Profile.LastVisited = DateTime.Now.ToString();

            Label1.Text = "Stored information includes:<p>" +
            "First name: " + Profile.FirstName +
            "<br>Last name: " + Profile.LastName +
            "<br>Age: " + Profile.Age +
            "<br>Member: " + Profile.Member +
            "<br>Last visited: " + Profile.LastVisited;
        }
        else
        {
            Label1.Text = "You must be authenticated;";
        }
    }
</script>
```

处理个性化属性的方法与你过去处理 `Session` 对象的方式类似，但请注意，个性化属性用于存储和检索，而不是基于键值（key-based）。因此，在使用它们时，你不需要记住键值。

个性化系统存储的所有项都属于某个特定的 .NET 数据类型。默认情况下，这些项被存储为 `String` 类型，并且你对存储的项具有早期绑定访问。要存储一个项，只需使用 `Profile` 对象直接填充个性化属性即可：

```csharp
Profile.FirstName = TextBox.Text;
```

要检索相同的内容，你只需获取此处所示 `Profile` 类的相应属性即可：

```csharp
Label1.Text = Profile.FirstName
```

使用 `Profile` 类以及代码视图中定义的所有个性化属性的巨大优势在于，该方法在你构建页面时提供了 IntelliSense 支持。当你在此视图中使用 `Profile` 类时，你定义的所有项都会通过 IntelliSense 功能列出可用选项。

![](img/7040c21013b8e6c23c612d6da3599ff8_632_0.png)

图 14-2

所有这些属性在 IntelliSense 中都是可用的，因为当你保存对 `web.config` 文件进行的个性化更改时，`Profile` 类在场景之间是隐藏并动态编译的。在 `web.config` 文件中保存后，这些属性将以严格类型的方式在整个应用程序可用。

当你运行列表 14-2 中的页面时，将产生图 14-3 所示的结果。

![](img/7040c21013b8e6c23c612d6da3599ff8_633_0.png)

图 14-3

除了使用早期绑定访问技术外，你还可以对存储在个性化引擎中的项使用后期绑定访问。列表14-3 显示了后期绑定访问技术。

## 列表 14-3：使用后期绑定访问

```vb
Dim myFirstName As String
myFirstName = CStr(Profile.Get("FirstName"))
```

除了早期绑定访问技术外，你还可以对存储在个性化引擎中的项使用后期绑定访问。列表14-3 显示了后期绑定访问技术。
