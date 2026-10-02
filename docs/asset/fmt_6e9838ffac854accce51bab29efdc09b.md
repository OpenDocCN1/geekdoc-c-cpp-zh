
接下来，你为上一步中创建的 ActiveX DLL 添加引用。请按照以下步骤操作：

1. 在解决方案资源管理器中右键点击你的项目。
2. 选择“添加引用 (Add Reference)”菜单。
3. 在“添加引用”对话框中，选择“浏览 (Browse)”选项卡。
4. 通过浏览到其位置找到 `NameComponent.dll` 对象。
5. 点击“确定”将 `NameComponent.dll` 添加到选组件列表中并关闭对话框。

> 注意：如果你没有使用 Visual Studio 2012 或代码后页面，你仍然可以通过类型库转换器手动创建 RCW 来为你的 COM 添加引用，然后在页面中使用 `imports` 语句 (VB) 或 `using` 语句 (C#)。

使用“添加引用”对话框选择组件后，系统会为该组件创建一个 RCW 并将其添加到你的应用程序中。就是这些！只需运行应用程序即可查看 COM 互操作层的工作情况。当点击“分析”按钮时，“名”、“姓”和“全名”文本框中的字段将发送到 RCW，然后传递给 `NameComponentDLL` ActiveX 控制。数据以相同的方式检索，以填充文本框并指示全名的长度。

# 在 C# 中访问复杂的 COM 成员

有时，COM 对象的某些成员无法正确地向 C# 暴露。在前面的示例中，String 属性没有暴露，但 Long 属性 (`FullName`) 却暴露了。

当你发现问题时，你就知道出问题了，因为尽管你可以看到该属性，但无法编译应用程序。例如，对于 C#，不要使用列表 B-2 所示的代码，而是使用 `NameComponent.dll` ActiveX 组件的以下属性：

```csharp
if (FirstName.Text.Length > 0)
    FirstName.Text.ToString();
```

`FirstName` 属性看起来没问题。它出现在智能提示中，但当你想要使用它时，请使用 `set_FirstName` 和 `get_FirstName`。此外，这些方法期望 `ref` 参数而不是 String。在列表 B-2 的示例中，使用了两个步骤来正确这样做：首先将 String 赋值给本地变量，然后使用 `ref` 传递变量。

.NET 的优点之一是它有自己的垃圾收集器——它可以自我清理。在使用 COM 互操作时，情况并不总是如此，因为 COM 对象没有 .NET 依赖的内置垃圾收集机制。.NET 不知道何时从内存中释放 COM 对象。

因此，你应该使用 `System.Runtime.InteropServices.Marshal.ReleaseObject` 方法尽早从内存中释放 COM 对象：

# 错误处理

.NET 中的错误处理使用异常而不是 Visual Basic 使用的 HRESULT 值。幸运的是，RCW 完成了大部分两者之间的转换工作。

以列表 B-3 所示的代码为例。在这个示例中，如果分子或分母大于 1000，将抛出一个自定义错误。同样注意，它没有捕获除以零错误。当 ActiveX 组件自行抛出错误时会发生什么。

首先通过将列表 B-3 中的代码编译到 `DivideComponent.dll` ActiveX 组件中的 `DivideClass` 类开始。

# B-3：在 VB 中抛出错误

```vb
Public Function Divide(Numerator As Double, 
    Denominator As Double) As Double

If ((Numerator > 1000) Or (Denominator > 1000)) Then
    Err.Raise vObjectError + 1, "DivideComponent:DivideNumber", "Numerator and denominator both have to be less than or equal to 1000."

DivideNumber = Numerator / Denominator
```

接下来，创建一个新的 ASP.NET 项目；添加对 `DivideComponent.dll` 的引用（调用 RCW 创建其副本）。请记住，你也可以使用 `tlbimp` 手动执行此操作。现在，将列表 B-4 中的代码添加到页面中。

### 列表 B-4：.NET 中的错误处理

```vb
<%@ Language="VB" %>

<script runat="server">
    Protected Sub Calculate_Click(ByVal sender As Object, ByVal e As System.EventArgs)
        Dim Divide As New DivideComponent.DivideClass()
        Try
            Answer.Text = Divide.DivideNumber(Numerator.Text, Denominator.Text)
        Catch e As Exception
            Answer.Text = e.Message.ToString()
        End Try
        System.Runtime.InteropServices.Marshal.ReleaseComObject(Divide)
    End Sub
</script>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>使用 COM 组件</title>
</head>
<body>
    <form id="form1" runat="server">
        <p>
            <asp:Label ID="Label1" runat="server">分子:</asp:Label>
            <asp:TextBox ID="Numerator" runat="server"></asp:TextBox>
        </p>
        <p>
            <asp:Label ID="Label2" runat="server">分母:</asp:Label>
            <asp:TextBox ID="Denominator" runat="server"></asp:TextBox>
        </p>
        <p>
            <asp:Label ID="Label3" runat="server">分子除以分母:</asp:Label>
            <asp:Label ID="Answer" runat="server" Font-Bold="True"></asp:Label>
        </p>
        <p>
            <asp:Button ID="Calculate" runat="server" OnClick="Calculate_Click" Text="计算"></asp:Button>
        </p>
    </form>
</body>
</html>
```

### 列表 B-4（继续）

```csharp
<%@ Page Language="C#" %>

<script runat="server">
    void Calculate_Click(object sender, EventArgs e) {
        DivideComponent.DivideClass myDivide = new DivideComponent.DivideClass();
        try {
            double numerator = double.Parse(Numerator.Text);
            double denominator = double.Parse(Denominator.Text);
            Answer.Text = myDivide.DivideNumber(numerator, denominator).ToString();
        } catch (Exception ex) {
            Answer.Text = ex.Message.ToString();
        }
        System.Runtime.InteropServices.Marshal.ReleaseComObject(myDivide);
    }
</script>
```
