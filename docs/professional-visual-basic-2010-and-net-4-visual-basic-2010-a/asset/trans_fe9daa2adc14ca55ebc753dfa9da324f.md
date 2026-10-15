

无论你处于设计视图还是源视图，都可以通过高亮控件在“属性”窗口中编辑其属性。更改属性将改变高亮控件的外观或行为。由于所有控件都继承自特定的基类（`WebControl`），你可以在选择控件时按住 Ctrl 键同时高亮多个控件，并一次性更改所有控件的基本属性。

使用上面介绍的技术将控件添加到 `Default.aspx` 中，使其在拆分视图中看起来如图 21-5 所示。这是一个简单的表单，允许用户输入姓名和电子邮件地址，并通过单击 Submit 按钮将它们提交给某个进程。页面正文的标记应类似于以下代码：

```
<body>
    <form id="form1" runat="server">
        <div>
            <asp:Label ID="Label1" runat="server" Text="Name: "></asp:Label>
            <asp:TextBox ID="NameTextBox" runat="server" Width="200px"></asp:TextBox>
            <br />
            <asp:Label ID="Label2" runat="server" Text="Email: "></asp:Label>
            <asp:TextBox ID="EmailTextBox" runat="server" Width="200px"></asp:TextBox>
            <br />
            <asp:Button ID="SubmitButton" runat="server" Text="Submit" />
            <br />
            <br />
            <asp:Label ID="ResultsLabel" runat="server" Text="Label"></asp:Label>
        </div>
    </form>
</body>
```

代码片段来自 Step01-ServerControls.aspx

![](img/d99870e80390742f93963da7be0b2e61_734_0.png)

图 21-5

## 事件

ASP.NET Web Forms 采用与 Windows 窗体类似的事件驱动模型。开发人员可以处理页面或页面上出现的控件生成的事件。例如，处理 Submit 按钮的 click 事件的代码如下所示：

```
Protected Sub SubmitButton_Click(ByVal sender As Object, ByVal e As EventArgs)
    Handles SubmitButton.Click
    'Code actions here
End Sub
```

ASP.NET Web Forms 事件与 Windows 窗体事件的关键区别在于事件发生时发生了什么。构成 Windows 窗体的对象与窗体一样存在，因此它们会在用户交互之间保持状态。由于 Web 的无状态模型，构成页面的对象（在示例项目中是指页面、标签、文本框和按钮）只存在足够长的时间来生成该页面的标记。一旦请求完成并将最终标记发送到客户端浏览器，组成页面的对象就成为孤立对象，等待垃圾回收。

由于原始对象不再可用，需要创建新的对象来运行事件代码。因此，当用户交互触发服务器端事件时，会向服务器发送一个包含事件信息的请求；页面和控件对象在服务器上创建；这些对象的内部状态使用请求中传递的信息设置；事件处理程序执行；然后将页面的更新版本发送回客户端浏览器。这个过程称为回发（postback）。

事件处理程序的代码可以采用传统的 ASP 风格，以内联方式放置在与标记相同的页面中，如下所示：

```
<script runat="server">
    Protected Sub SubmitButton_Click(ByVal sender As Object, ByVal e As EventArgs)
    Handles SubmitButton.Click
    'Code actions here
    End Sub
</script>
```

然而，更常见的方法是使用代码隐藏文件（有时称为 code-beside 文件）。使用代码隐藏模型的目的是将业务逻辑和表示逻辑分离到各自的文件中。这样可以更轻松地处理页面，尤其是在团队环境中，视觉设计师负责页面的 UI，程序员负责表示层背后的业务逻辑。代码隐藏文件通过 Page 指令的属性与 ASPX 文件关联。请注意，根据使用的是网站项目类型还是 Web 应用程序项目类型，Page 指令会略有不同。

```
<%@ Page Language="vb" AutoEventWireup="false"
    CodeBehind="Default.aspx.vb" Inherits="BasicWebForms._Default" %>
```

如何为服务器控件挂接这些事件？同样，该模型与 Windows 窗体中的模型类似。你可以在设计视图中双击控件来为该控件的默认事件添加处理程序，可以使用“属性”窗口中的“事件”视图（参见图 21-6），也可以使用代码编辑器顶部的下拉列表（参见图 21-7）。

![](img/d99870e80390742f93963da7be0b2e61_735_0.png)

![](img/d99870e80390742f93963da7be0b2e61_735_1.png)

在示例应用程序中，`Step02-Events.aspx` 是截止本节末尾的页面完整版本。

为 Submit 按钮的 Click 事件添加事件处理程序。在事件处理程序中，在 Result 标签中显示用户输入的姓名和电子邮件值。下面的代码将实现这一点：

```
Protected Sub SubmitButton_Click(ByVal sender As Object, ByVal e As EventArgs)
    Handles SubmitButton.Click
    ResultsLabel.Text = String.Format("You entered Name: {0} and Email: {1}",
        NameTextBox.Text, EmailTextBox.Text)
End Sub
```

代码片段来自 Step02-Events.aspx.vb

图 21-8 显示了单击 Submit 按钮之前的页面，图 21-9 显示了单击之后的页面。

![](img/d99870e80390742f93963da7be0b2e61_736_0.png)

图 21-8

![](img/d99870e80390742f93963da7be0b2e61_736_1.png)

图 21-9

## 页面生命周期

除了处理控件的事件之外，你通常还需要处理页面生命周期中引发的事件。这使你能够根据自己的需要定制页面的生成。

以下是页面生命周期中常用事件的列表。可能还有其他事件，但这些事件主要供创建自定义服务器控件的开发人员使用。

- 1. PreInit
- 2. Init
- 3. InitComplete
- 4. PreLoad
- 5. Load
- 6. LoadComplete
- 7. PreRender
- 8. SaveStateComplete
- 9. Unload

其中，最常用的是 Load 事件，通常用于初始化页面及其子控件的属性：

```
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Handles Me.Load
    ' Retrieve data from a database or service
    ' Use data to populate the properties of controls
End Sub
```

在示例应用程序中，`Step03-PageLifecycle.aspx` 是截止本节末尾的页面完整版本。

回到你的应用程序，添加一个下拉列表，让用户输入他们所在的州：

```
<asp:Label ID="Label3" runat="server" Text="State: "></asp:Label>
<asp:DropDownList ID="StateDropDown" runat="server" Width="200px">
</asp:DropDownList>
```

代码片段来自 Step03-PageLifecycle.aspx

在页面的 Load 事件中，我们将用几个州名填充此控件。我们还将更新 Submit 按钮的 Click 事件处理程序，以输出选定的州：

```
Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs)
    Handles Me.Load
    ResultsLabel.Text = String.Empty
    StateDropDown.Items.Add("New York")
    StateDropDown.Items.Add("California")
    StateDropDown.Items.Add("Florida")
End Sub

Protected Sub SubmitButton_Click(ByVal sender As Object, ByVal e As EventArgs)
    Handles SubmitButton.Click
    ResultsLabel.Text = String.Format(
        "You entered Name: {0}, Email: {1}, and State: {2}",
        NameTextBox.Text, EmailTextBox.Text, StateDropDown.Text)
End Sub
```

代码片段来自 Step03-PageLifecycle.aspx.vb

现在运行示例，看似工作正常，但如果在单击 Submit 按钮至少一次后检查 State 下拉列表中的项，你会注意到它们出现了多次（参见图 21-10）。似乎控件中的值在页面请求之间被持久化了，而 `Page_Load` 事件处理程序中的代码是在向现有项中添加，而不是从头填充项集合。

