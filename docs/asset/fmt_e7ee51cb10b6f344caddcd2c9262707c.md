
```xml
<asp:Repeater Id="Repeater" runat="server"
  DataSourceID="SqlDataSource">
  <HeaderTemplate>
  <table>
  </HeaderTemplate>
  <ItemTemplate>
  <tr>
    <td>
      <%# Container.DataItem("ProductID") %><br /> />
      <%# Container.DataItem("ProductName") %><br /> />
      <%# DataBinder.Eval(
        Container.DataItem, "UnitPrice", "{0:c}")
      %><br /> />
    </td>
  </tr>
  </ItemTemplate>
  <FooterTemplate>
  </table>
  </FooterTemplate>
</asp:Repeater>
```

如你从示例所示，你正在使用 `Repeater` 控件显示一系列员工。因为 `Repeater` 控件是模板控件，所以使用数据绑定在模板的正确位置输出特定的员工数据。

![](img/67a6707ff505c052edb96c0128fb3096_395_0.png)

图 8-13

在 ASP.NET 的后续版本中，内联数据绑定的概念基本上保持不变，但你被赋予了更简单的语法和几个强大的绑定工具来使用。

## 数据绑定语法

ASP.NET 包含三种执行数据绑定的方法。一种方法你可以继续使用现有的绑定方法，使用 `Container.DataItem("Name")`。

```
<% Container.DataItem("Name") %>
```

这种方法很好，因为它意味着如果你从 ASP.NET 的早期版本迁移，就不需要更改现有的网页了。如果你正在创建新的网页，你可能会使用最简单的绑定形式，即使用 `Eval` 方法：

```
<% Eval("Name") %>
```

你还可以继续使用 `Eval` 方法的格式化重载来对数据进行格式化：

```
<% Eval("HireDate",{0:mm dd yyyy") %>
```

在这些更改中，ASP.NET 包含了一种名为双向数据绑定的数据绑定。双向数据绑定允许你对绑定的数据支持读和写操作。这是通过使用 `Bind` 方法实现的，除了方法名不同，它的工作原理与 `Eval` 方法一样：

```
<% Bind("Name") %>
```

`Bind` 方法应该在如 `GridView`、`DetailsView` 或 `FormView` 等控件中使用，这些控件实现了对数据源的自动更新。

在使用数据绑定时，请记住 `<%` 和 `%>` 分隔符之间的任何内容都被视为一个表达式。这很重要，因为它在数据绑定时为你提供了额外的功能。例如，你可以附加额外的数据：

```
<% "Foo" + Eval("Name") %>
```

或者你甚至可以将求后的值传递给方法：

```
<% DoSomething(Eval("Name")) %>
```

## XML 数据绑定

由于 XML 在应用程序中非常流行，ASP.NET 也别包含了几种专门绑定到 XML 数据源的方法。这些数据绑定表达式为你提供了处理 XML 层次结构格式的强大方法。此外，除了方法名不同外，这些方法的工作与之前讨论的 `Eval` 和 `Bind` 方法完全相同。当你使用 `XmlDataSource` 控件时，应该使用这些绑定器。你使用的使用 `XPath` 类的第一个格式绑定如下代码所示：

```
<% XPath.Eval(Container.DataItem,"employees/employee/Name") %>
```

注意，在 XML 属性中指定列名后，XPath 查询遵循标准表达式，XPath 数据绑定表达式也有一种短格式：

```
<% Eval("employees/employee/Name") %>
```

此外，`Eval` 方法（`XPath` 数据绑定表达式）还支持对数据应用格式化：

```
<% Eval("employees/employee/HireDate",{0:mm dd yyyy") %>
```

`XPath` 使用所提供的 XPath 查询返回单个节点。如果你想从 `XmlDataSource` 控件返回多个节点，可以使用该类的 `Select` 方法。该方法返回一个与提供的 XPath 查询匹配的节点列表：

## 使用表达式和表达式生成器

表达式是 ASP.NET 在运行时解析的语句，用于返回一个数据值。ASP.NET 会自动使用表达式来执行某些操作，例如在解析 `SqlDataSource` 控件时检索数据库连接字符串，因此你已经在页面中见过这些语句了。`ConnectionString` 表达式显示在列表 8-53 中。

### 列表 8-53：一个连接字符串表达式

```
<asp:SqlDataSource ID="SqlDataSource" Runat="server"
    SelectCommand="SELECT * FROM [Customers]"
    ConnectionString="<% ConnectionString %> />
```

ASP.NET 尝试使用 ASP.NET 网页时，它会寻找包含在 `<% %>` 分隔符中的表达式。这指示 ASP.NET 这是一个要解析的表达式。如上一个列表所示，它尝试从 `web.config` 文件查找 `NorthwindConnectionString` 值。ASP.NET 知道通过 `ConnectionString` 表达式前缀执行此操作，允许 ASP.NET 使用 `StringBuilder` 类来解析该表达式。

ASP.NET 尝试使用 ASP.NET 网页时，它会寻找包含在 `<% %>` 分隔符中的表达式。这指示 ASP.NET 这是一个要解析的表达式。如上一个列表所示，它尝试从 `web.config` 文件查找 `NorthwindConnectionString` 值。ASP.NET 知道通过 `ConnectionString` 表达式前缀执行此操作，允许 ASP.NET 使用 `StringBuilder` 类来解析该表达式。

ASP.NET 包含几种表达式，包括从 `web.config` 文件中获取值的表达式，如列表 8-53 和 55 所示，演示了 `AppSettingsBuilder` 和 `ResourceBuilder`。

### 列表 8-54：使用 AppSettingsBuilder

```
<asp:Label runat="server" Id="Label"
    Text="<% AppSettings %> />
```

### 列表 8-55：使用 ResourceBuilder

```
<asp:Label runat="server" Id="Label"
    Text="<% Resources %> />
```

除了表达式生成器类，你还可以通过派生 `System.Web.Compilation.ExpressionBuilder` 基类来创建自己的表达式。该基类为你提供了 ASP.NET 解析你的表达式时需要覆盖的方法。列表 8-56 显示了一个简单的表达式生成器。

### 列表 8-56：使用表达式生成器

VB

```vb
<Expression("MyCustomExpression")>
<ExpressionEditor("MyExpressionEditor")>
Public Class MyCustomExpression
    Inherits ExpressionBuilder
    Public Overrides Function GetCodeExpression(
        ByVal entry As PropertyEntry,
```

### 列表 8-56（继续）

```
ByVal parsedData As Object,
ByVal context As ExpressionBuilderContext) _
As System.CodeDom.CodeExpression("Int64")
    Return New CodeCastExpression("Int64",
        New CodePrimitiveExpression(1000)))
End Function
End Class
```

C#

```csharp
[ExpressionPrefix("MyCustomExpression")]
[ExpressionEditor("MyExpressionEditor")]
public class MyCustomExpression : ExpressionBuilder
{
    public override System.CodeDom.CodeExpression GetCodeExpression(PropertyEntry entry, object parsedData, ExpressionBuilderContext context)
    {
        return new CodeCastExpression("Int64",
            new CodePrimitiveExpression(1000));
    }
}
```

在这个列表中，注意几点。首先，你从 `ExpressionBuilder` 派生了 `CustomExpression` 类。其次，你覆盖了 `GetCodeExpression`。该方法为你提供了执行此方法的有用参数，并返回一个 `CodeExpression` 对象。

> 注意 `CodeExpression` 是 .NET CodeDom 基础设施中的基类。派生自 `CodeExpression` 的类的提供了生成 .NET 代码的抽象方法。此 CodeDom 基础设施帮助你动态创建和运行代码。

`BoundProperty` 告诉你表达式具体绑定到什么。例如，在列表 54 和 55 中，Label 的 `Text` 属性绑定到 `AppSettings` 和 `Resources` 表达式。`parsedData` 对象包含 `ParseExpression` 方法解析并返回的任何数据，你将在本章后面看到。最后，`ExpressionBuilderContext` 允许你引用与表达式相关的虚拟路径或模板控件。

在你创建了生成器类后，要让 .NET 知道它。你可以通过在 `web.config` 文件的 `compilation` 节点中添加 `ExpressionBuilders` 节点来实现。注意其值为

`ExpressionPrefix` 被添加到 `ExpressionBuilder` 中，以帮助 ASP.NET 在运行时定位合适的表达式生成器类。

```
<compilation debug="true" strict="false" explicit="true">
<ExpressionBuilders>
  <add expressionPrefix="MyCustomExpression" type="MyCustomExpression"/>
</ExpressionBuilders>
</compilation>
```

`GetCodeExpression` 方法并不是 `ExpressionBuilder` 类中唯一可以重写的成员。其他几个成员包括 `ParseExpression`、`SupportsEvaluate` 和 `EvaluateExpression` 方法。

`ParseExpression` 方法允许你将表达式数据传递给 `GetCodeExpression` 方法。例如，在列表 8-56 中，`CodeCastExpression` 值 1000 是硬编码的。然而，如果你想允许开发者将该值作为表达式的一部分进行解析，只需如列表 8-57 所示使用 `ParseExpression` 方法。

### 列表 8-57：使用 ParseExpression

VB

```vb
<ExpressionPrefix("CustomExpression")>
<ExpressionEditor("CustomExpressionEditor")>
Public Class MySecondCustomExpression
Inherits ExpressionBuilder
  Public Override Function GetCodeExpression(
ByVal entry As BoundPropertyEntry,
ByVal parsedData As Object,
ByVal context As ExpressionBuilderContext)
As System.Code.Dom.CodeExpression
  Return New CodeCastExpression("Int64",
  CodePrimitiveExpression(parsedData))
End Function
Public Override Function ParseExpression(
ByVal expression As String,
ByVal propertyType As Type,
ByVal context As ExpressionBuilderContext) As Object
  Return expression
End Function
End Class
```

C#

```csharp
[ExpressionPrefix("MySecondCustomExpression")]
[ExpressionEditor("MySecondCustomEditor")]
public class MySecondCustomExpression : ExpressionBuilder
{
  protected override System.Code.Dom.CodeExpression
  GetCodeExpression(BoundPropertyEntry entry, object parsedData,
  ExpressionBuilderContext context)
  {
    return new CodeCastExpression("Int64",
    new CodePrimitiveExpression(parsedData));
  }
  public override object ParseExpression(
    string expression, Type propertyType,
    ExpressionBuilderContext context)
  {
    return expression;
  }
}
```

### 第 8 章 数据绑定

最后两个检查的表达式重写成员是 `SupportsEvaluate` 和 `EvaluateExpression` 成员。如果你在无编译场景下（使用 `specificationMode = "Page"` 指令）运行网站，则需要重写这些方法。`SupportsEvaluate` 属性返回一个布尔值，指示 ASP.NET 在页面以无编译模式执行时是否可以评估。如果返回 `True` 且页面以无编译模式执行，则使用 `EvaluateExpression` 方法返回数据值，而不是返回表示数据值对象的 `GetCodeExpression` 方法。参见 8-58。

### 列表 8-58：重写 SupportsEvaluate 和 EvaluateExpression

VB

```vb
<ExpressionPrefix("*MyCustomExpression")>
<ExpressionEditor("*MyCustomExpressionEditor")>
Public Class MyThirdCustomExpression
Inherits ExpressionBuilder
    Public Override Function GetCodeExpression(
    ByVal entry As BoundPropertyEntry,
    ByVal parsedData As Object,
    ByVal context As ExpressionBuilderContext) As System.Code.Dom.CodeExpression
        Return New CodeCastExpression("Int64",
        New CodePrimitiveExpression(parsedData))
    End Function

    Public Override Function ParseExpression(
    ByVal expression As String,
    ByVal propertyType As Type,
    ByVal context As ExpressionBuilderContext) As Object
        Return expression
    End Get
    End Property

    Public Override ReadOnly Property SupportsEvaluate As Boolean
    Get
        Return True
    End Get
    End Property

    Public Override Function EvaluateExpression(
    ByVal target As Object,
    ByVal entry As BoundPropertyEntry,
    ByVal parsedData As Object,
    ByVal context As ExpressionBuilderContext) As Object
        Return parsedData
    End Function
End Class
```

C#
