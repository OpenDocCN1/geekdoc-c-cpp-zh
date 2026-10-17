
```csharp
@ Page Language="C#" %>
<script runat="server">
protected void AnalyzeName_Click(object sender, System.EventArgs args)
{
    NameComponent.NameFunctionsClass Name =
        new NameComponent.NameFunctionsClass();

    if (FirstName.Text.Length > 0)
    {
        string firstName = FirstName.Text.ToString();
        Name.setFirstName(ref firstName);
    }

    if (LastName.Text.Length > 0)
    {
        string lastName = LastName.Text.ToString();
        Name.setLastName(ref lastName);
    }

    if (FullName.Text.Length > 0)
    {
        string fullName = FullName.Text.ToString();
        Name.setFullName(ref fullName);
    }

    FirstName.Text = Name.get_FirstName();
    LastName.Text = Name.get_LastName();
    FullName.Text = Name.get_FullName();
    FullName.Length.Text = Name.FullNameLength.ToString();
}
</script>
```

现在你需要对上一步中创建的 ActiveX DLL 添加引用。请按照以下步骤操作：

- 1. 在解决方案管理器（Solution Explorer）对话框中右键点击你的项目。
- 2. 选择“添加引用”（Add Reference）项。
- 3. 在添加引用对话框中，选择第四个选项页“浏览”（Browse）。
- 4. 找到 `NameComponent.dll`。
- 5. 点击确定添加它。

如果你不再使用它，可以移除该引用。

## 手动释放 COM 对象

.NET 的优点之一是它的垃圾回收机制——它可以自动清理内存。然而，在使用 COM 互操作性时情况并不总是如此，.NET 无法知道何时从内存中释放 COM 对象，因为它没有内置的垃圾收集机制。

由于这种限制，你应该尽快使用 `System.Runtime.InteropServices.Marshal` 类中的 `ReleaseComObject` 方法来释放对象：

```csharp
System.Runtime.InteropServices.Marshal.ReleaseComObject(obj);
```

需要注意的是，如果你在对象超出作用范围之前尝试使用它，将会抛出异常。

## 错误处理

.NET 中的错误处理使用异常而不是 Visual Basic 应用程序使用的 HRESULT 值。坦率地说，RCW（运行类封装）完成了大部分两者之间的转换工作。

例如，列表 28-3 所示的代码。在这个示例中，如果分子或分母大于 1000，则会抛出用户错误。注意注意我们没有捕获除以零错误。观察 ActiveX 组件抛出错误时发生的情况。

### 列表 28-3：在 VB 中抛出错误

```vb
Public Function DivideNumber(Numerator As Double, 
Denominator As Double) As Double
If ((Numerator > 1000) Or (Denominator > 1000)) Then
Err.Raise vbObjectError + 1, 
"DivideComponent:Divide.DivideNumber", 
"Numerator and denominator both have to " + 
"be less than or equal to 1000."
End If
DivideNumber = Numerator / Denominator
End Function
```

## 第 28 章：使用业务对象

接下来，创建一个新的 ASP.NET 项目；添加 `DivideComponent.dll` 的引用（这将调用 Visual Studio 2008 创建其自身的 RCW 副本）。请记住，你也可以使用 `tlbimp` 可执行文件手动执行此操作。

现在，将列表 28-4 所示的代码添加到 ASP.NET 页面中。

### 列表 28-4：.NET 中的错误处理

```VB
<% Page Language="server" %>
<script runat='server'>
Protected Sub Calculate_Click(ByVal sender As Object, 
    ByVal e As System.EventArgs)

Dim Divide As New DivideComponent.DivideClass()

Try
    Answer.Text = Divide.Number(Numerator.Text, Denominator.Text)
Catch ex As Exception
    Answer.Text = ex.Message.ToString()
End Try

System.Runtime.InteropServices.Marshal.ReleaseObject(Divide)
End Sub
</script>
<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
<title>Using COM Components</title>
</head>
<<body>
<form id="form1" runat="server">
<p>
<Label ID="Label1" runat="server">Numerator:</Label>
&nbsp;
<TextBox ID="Numerator" runat="server"></asp:TextBox>
</p>
<p>
<Label ID="Label2" runat="server">Denominator:</Label>
&nbsp;
<TextBox ID="Denominator" runat="server"></asp:TextBox>
</p>
<p>
<Label ID="Label3" runat="server">
Numerator divided by Denominator:</Label>
&nbsp;
<asp:Label ID="Answer" runat="server" Font-Bold="True">0</asp:Label>
</p>
<asp:Button ID="Calculate"
runat="server"
OnClick="Calculate_Click"
Text="Calculate"
</button>
<p>
</form>
</body>
</html>
```

```csharp
<%@ Page Language="C#" %>

<script runat="server">
protected void Calculate_Click(object sender, System.EventArgs e)
{
DivideComponent.DivideClass myDivide = new DivideComponent.DivideClass();

try{
double numerator = double.Parse(Numerator.Text);
double denominator = double.Parse(Denominator.Text);
Answer.Text = myDivide.DivideNumber(ref numerator,
ref denominator).ToString();
}
 catch (Exception ex){
Answer.Text = ex.Message.ToString();
}
System.Runtime.InteropServices.Marshal.ReleaseComObject(myDivide);
}
</script>
```

第 28-4 行中的代码解析了用户输入的分子（Numerator）和分母（Denominator）值，导致 `Divider.dll` ActiveX 组件的除法失效。使用无效输入运行应用程序，将得到图 28-9 所示的结果。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1354_0.png)

图 28-9

取决于你运行 ASP.NET 应用程序时使用的语言，你将看到不同的数据集看到不同的值。对于有效输入，你当然总是能看到正确的结果；而对于任何超过 1000 的输入，你会看到 Visual Basic6 指出的错误描述，即分子和分母都必须小于等于 1000。

然而，对于无效的字符串，Visual Basic 2008 报告“Cast from string 'abc' to type 'Double' is not valid”，而 C# 报告“Input string was not in a correct format”。对于除以零，它们都报告“division by Zero”，因为该错误直接来自 Visual Basic6 运行时。

## 在 .NET 应用程序中部署 COM 组件

使用 .NET 应用程序部署 COM 组件非常简单；特别是与部署 ActiveX 控件相比。部署带有 COM 组件的 .NET 应用程序时，有两种场景：

- 使用私有程序集（private assemblies）
- 使用共享程序集（shared assemblies）

### 私有程序集

将 ActiveX 组件的或部分安装在 .NET 应用程序本地被视为安装私有程序集。在这种情况下，同一台机器上的每次 .NET 应用程序安装都至少拥有一份你所引用的 ActiveX 组件的互操作库（Interop library）副本，如图 28-10 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1355_0.png)

图 28-10

取决于你决定将 ActiveX 组件安装在应用程序本地，还是安装在所有调用应用程序的共享目录中。

曾经将 ActiveX 组件分离到单独的目录被认为是良好的做法，这样如果这些组件被其他应用程序引用，你就不需要再次注册或安装该文件。使用这种方法意味着当你升级组件时，会自动升级使用它的应用程序。然而，这种做法的效果并不理想。事实上，这种做法导致了“DLL 地狱”问题，实际上这也是微软开始推行私有 .NET 组件的主要原因。一旦你放置了组件，剩下的任务就是使用 `regsvr32` 注册 ActiveX 组件。

### 公共程序集

私有程序集的反面是公共程序集。公共程序集供其他应用程序共享 RCW DLL。为了创建公共程序集，你必须将 RCW 放入全局程序集缓存（GAC），如图 28-11 所示。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1356_0.png)

图 28-11

取决于你决定将 ActiveX 组件安装在应用程序本地，还是安装在所有调用应用程序的共享目录中。

GAC 位于 `C:\Windows\assembly`。通过 Windows 资源管理器将项目拖入此处非常简单。虽然 GAC 对所有人开放，但除非你有充分的理由，否则不建议将组件绑定到此处。

你也可以使用全局程序集工具 `Gacutil.exe` 从命令行向 GAC 添加项目。它允许通过构建脚本、makefile 和批处理文件操作全局程序集的内容。

很难找到将程序集安装到 GAC 的充分理由。如果我们必须选择这样做的时间，会在我们有一个在同一台机器上高度共享组件时。在企业环境中，我们避免使用 GAC。

## 第 28 章：使用业务对象

### 在非托管代码中使用 .NET

.NET 提供了 COM 互操作性的反面，允许你在非托管代码中使用新创建的 .NET 组件。本节讨论与 Basic 6 可执行文件的 .NET 组件。当你使用 OCX 或 DLL 代替可执行文件时，本节所示的技术是相同的。

COM 调用器（CCW）是 .NET 框架中启用非托管代码与 .NET 组件通信的组件。与 RCW 不同，CCW 不是随应用程序分发的独立 DLL。相反，CCW 是为你使用的每个 .NET 组件实例化的 .NET 框架的一部分。

图 28-12 显示了 CCW 如何在非托管代码和 .NET 组件之间进行转换，就像 RCW 在托管代码和 COM 代码之间进行转换一样。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1357_0.png)

图 28-12

### COM 调用器

COM 调用器或 CCW 如前所述，不像 RCW 那样是一个独立的 DLL。相反，CCW 使用一个基于 .NET 组件专门创建的类型库。这种类型被称为互操作类型库（Interop Type Library）。互操作类型库与非托管代码静态链接，以便该代码与 CCW 通信。

为了让 .NET 组件生成互操作类型库，你需要告诉 Visual Studio 2008 在构建组件时生成它。Visual Basic 和 C# 类库项目属性对话框的“编译”属性中都有相应的设置。

# 第 28 章：使用业务对象

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1358_0.png)

图 28-13

C# 的对话框略有不同，如图 28-14 所示。在两个对话框中，该属性都是“注册用于 COM”（Registered for COM Interop）。在 Visual Basic 中，你可以在编译（Compile）页面找到此属性；在 C# 中，你可以在属性页的生成（Build）选项卡找到它。

通过勾选框设置此选项后，构建项目时会生成一个独立的类型库 `.tlb`。这个 `.tlb` 文件是将 .NET 组件包含在 COM 程序中的。

在 Visual Basic 中，当你向 DLL 添加引用时，你会从 Visual Basic 项目的引用（References）部分导航到要添加的 ActiveX DLL。如果你使用 .NET 组件，无法通过这种方式进行正确引用，因为它们不是 ActiveX。相反，你引用的是互操作类型库（Interop Type Library），这使得相应的 .NET 组件的功能对你的应用程序可用。

.NET Framework 还为你提供了一种手动为 .NET 组件创建互操作类型库的方法。你通过一个名为“类型库导出器”（Type Library Exporter）的命令行工具来实现（与“用于 COM 互操作的类型导入”相比）。类型库导出器通过 `tlbexp.exe` 可执行文件调用。

![](img/eb54f286ad47e89bbf83e3e2d279e6dd_1359_0.png)

图 28-14

例如，对于下一个示例中 `NameComponent.dll` 的互操作类型库，你将使用以下命令：

```
tlbexp NameComponent.dll /out:NameComponentEx.tlb
```

`/out` 参数指定要创建的互操作类型库的名称。如果你省略此参数，将得到一个与 ActiveX 组件同名但扩展名为 `.tlb` 的文件。

当你没有使用 Visual Studio 2008 作为开发环境，或者你想对生成的程序集有更多控制权，或者你正在自动化连接到 .NET 组件的过程，类型库导出器就会非常有用。

# 在 COM 对象中使用 .NET 组件

下一个示例说明了如何在 COM 代码中使用 .NET 组件。首先，在 Visual Basic 或 C# 中编译位于列表 28-5 中的 .NET 代码。

在类库项目中输入代码后，构建该组件并将其命名为 Name-Component。请记得在项目页面中将“注册用于 COM 互操作”（Register for the COM Interop）设置为 `True`（通过勾选相应的框框），如图 28-13 所示（Visual Basic 代码）和图 28-14 所示（C#）。如果你没有使用 Visual Studio 2008，可以使用前述描述的 `tablexp.exe` 来生成类型库。

## 列表 28-5：.NET 组件
