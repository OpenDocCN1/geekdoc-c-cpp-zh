
```csharp
[ExpressionPrefix("*MyCustomExpression")]
[ExpressionEditor("*MyCustomExpressionEditor")]
public class MyThirdCustomExpression : ExpressionBuilder
{
    public override System.CodeDom.CodeExpression
    GetCodeExpression(BoundPropertyEntry entry, object parsedData, ExpressionBuilderContext context)
    {
        return new CodeCastExpression("Int64",
        new CodePrimitiveExpression(parsedData));
    }
    public override object ParseExpression(
        string expression, Type propertyType, ExpressionBuilderContext context)
    {
        return expression;
    }
    public override bool SupportsEvaluate
    {
        get {
          return true;
        }
    }
    public override object EvaluateExpression(object target,
    BoundPropertyEntry entry, object parsedData,
    ExpressionBuilderContext context)
    {
      return parsedData;
    }
}
```

如行 8-58 所示，如果你想重写 `EvaluateExpression` 方法，只需从 `SupportsEvaluate` 属性返回 `True` 即可。然后你做的只是从 `EvaluateExpression` 方法返回一个对象。

## 总结

在本章中，你学习了 ASP.NET 中的绑定。数据源控件（如 `LinqDataSource`、`SqlDataSource` 和 `XmlDataSource`）使得从任何源查询和显示数据几乎是一项易举的任务。通过使用数据源控件自身的向导，你学习了几乎不需要代码就能生成强大的数据访问功能。

你研究了初级开发者如何轻松地将数据源控件与 `GridView`、`ListView` 和 `DetailsView` 控件结合，用极少的代码创建强大的数据处理应用程序。

你看到 ASP.NET 包含了许多可以进行数据绑定的控件，并检查了包含在 ASP 中的控件功能。

# 分页

`GridView` 控件内置了分页和排序功能。使用模型绑定，你可以通过模型绑定的 `Select` 方法返回 `IQueryable<T>` 来利用这些功能。列表 9-3 显示了如何启用分页和排序。要实现分页和排序，你需要如列表 9-1 所示在 `GridView` 控件上启用分页和排序。

## 列表 9-3：使用模型绑定进行分页和排序

```vb
Private _context As New VB.CustomerContext()
Public Function SelectCustomers() As IQueryable(Of VB.Customer)
    Return _context.Customer.AsQueryable()
End Function
```

```csharp
CustomerContext _context = new CustomerContext();
public IQueryable<Customer> SelectCustomers()
{
    return _context.Customer.AsQueryable();
}
```

在此列表中，你会注意到 `Select` 方法返回了一个 `IQueryable`。当从模型绑定的 `Select` 方法返回 `IQueryable<T>` 且 `GridView` 控件上启用了排序/分页时，`GridView` 可以自动使用排序和分页功能。

# 过滤

通常，你需要对想要显示给用户的结果进行过滤。你不想返回表的所有记录。在上一章中，你学习了如何使用 `SqlDataSource` 控件中的 `Select` 参数来过滤数据。在模型绑定中，可以通过 `ValueProviders` 和 `ValueProvider` 属性来实现过滤。列表 9-4 显示了如何使用 `QueryString` 过滤数据值。在此示例中，使用诸如 ID=5 的查询字符串仅返回 ID 为 5 的记录。

## 列表 9-4：使用 QueryString 进行过滤

```vb
Public Function SelectCustomers(<System.Web.ModelBinding.QueryString> id As
System.Nullable(Of Integer)) As IEnumerable(Of VB.Customer)
If id.HasValue Then
    Return _context.Customer.Where(Function(c) c.ID = id).AsEnumerable()
Else
    Return _context.Customer.AsEnumerable()
End If
End Function
```

```csharp
public IEnumerable<Customer> SelectCustomers([System.Web.ModelBinding.QueryString] int? id)
{
    if (id.HasValue)
        return _context.Customer.Where(c => c.ID == id).AsEnumerable();
    else
        return _context.Customer.AsEnumerable();
}
```

# 第 9 章 模型绑定

当你向 `QueryString` 传递 Id=5 时，模型绑定系统会获取此值并作为参数传递给 `Select` 方法。由于我们使用的是 Entity Framework Code First，我们可以编写 LINQ 查询来过滤 ID 为 5 的客户列表，并将结果返回给 `GridView` 控件。

# 使用值提供者

列表 9-4 显示了如何使用 `QueryString` 值提供者属性来过滤结果。该属性告诉模型绑定系统在运行时将查询字符串中的值绑定到 `id` 参数。模型绑定系统会根据需要执行任何类型转换。

值提供者最终从 `ValueProviders` 获取值，并告诉模型绑定系统使用哪个 `ValueProvider`。表 9-1 显示了你可以从框架使用的值提供者属性。

## 表 9-1

| 值提供者属性 | 描述 |
| :--- | :--- |
| `Form` | 从 Form 集合中检索值 |
| `Control` | 从指定的控件中检索值 |
| `QueryString` | 从 QueryString 集合中检索值 |
| `Cookie` | 从 Cookie 集合中检索值 |
| `Profile` | 从 Profile 集合中检索值 |
| `RouteData` | 从 RouteData 集合中检索值 |
| `Session` | 从 Session 集合中检索值 |

# 使用查询过滤

本节介绍了一个高级示例，你需要根据来自另一个服务器控件的值来过滤值。例如，你可能经常需要从下拉列表中查找值。列表 9-5 显示了如何使用 `Control` 值提供者属性从下拉列表中检索值。它使用该值过滤结果并将其显示在 `GridView` 控件中。

## 列表 9-5：使用 Control 值提供者进行过滤

```asp
<asp:DropDownList ID="DropDownList" runat="server" ItemType="Customer"
    SelectMethod="SelectCustomersForDropDownList" AppendDataBoundItems="true"
    AutoPostBack="true"
    DataTextField="ID" DataValueField="ID">
<asp:GridView ID="GridView" runat="server" ItemType="Customer"
    SelectMethod="SelectCustomers">
```

### VB

```vb
Public Function SelectCustomers() As IEnumerable(Of VB.Customer)
    Return _context.Customer.AsEnumerable()
End Function

Public Function SelectCustomers(<System.Web.ModelBinding.Control> DropDown As
    System.Nullable(Of Integer)) As IEnumerable(Of VB.Customer)
    If DropDown.HasValue Then
        Return _context.Customer.Where(Function(c) c.ID = DropDown).AsEnumerable()
    Else
        Return _context.Customer.AsEnumerable()
    End If
End Function
```

### C#

```csharp
CustomerContext _context = new CustomerContext();

public IEnumerable<Customer> SelectCustomers()
{
    return _context.Customer.AsEnumerable();
}

public IEnumerable<Customer> SelectCustomers([System.Web.ModelBinding.Control] int? DropDown)
{
    if (DropDown.HasValue)
        return _context.Customer.Where(c => c.ID == DropDown).AsEnumerable();
    else
        return _context.Customer.AsEnumerable();
}
```

在此列表中，当从 `DropDownList` 控件中选择一个值时，`GridView` 将绑定到 `DropDownList` 控件的选定值。模型绑定系统获取 `DropDownList` 控件的选定值（在这种情况下为 ID），并使用 `Control` 值将其作为参数传递给 `SelectCustomers` 方法。

# 插入数据

记住，在 ASP.NET 中，模型绑定系统从 `GridView` 控件获取值并填充客户模型，该客户模型可以在服务器上使用。一旦调用 `InsertMethod`，你可以进行检查以查看模型是否存在错误。如果一切成功，你可以将此新客户添加到客户集合并将其保存到数据库。

我们看到的用于插入记录的绑定方法适用于简单情况。然而，数据控件将无法为模型的每个成员提供值，可能是因为这些成员是关系对象，或者它们没有在控件中渲染。在这些情况下，最好是获取主键，从数据源加载模型，并告诉模型绑定系统将数据控件中的值绑定到模型。列表 9-6 显示了如何使用该方法。

## 列表 9-6：使用主键作为参数

```asp
<asp:DetailsView runat="server" ItemType="Customer" SelectMethod="SelectCustomers"
InsertMethod="InsertMethod" AutoGenerateButton="true">
```

### VB

```vb
Private _context As New VB.CustomerContext()

Public Function SelectCustomers() As VB.Customer
    Return _context.Customer.First()
End Function

Public Sub InsertCustomer(customer As VB.Customer)
    _context = New VB.CustomerContext()
    If ModelState.IsValid Then
        _context.Customer.Add(customer)
    End If
End Sub
```

### C#

```csharp
CustomerContext _context = new CustomerContext();

public Customer SelectCustomers()
{
    return _context.Customer.First();
}

public void InsertCustomer(Customer customer)
{
    _context = new CustomerContext();
    if (ModelState.IsValid)
    {
        _context.Customer.Add(customer);
    }
}
```

# 更新数据

我们用于插入记录的绑定方法适用于简单情况。然而，数据控件将无法为模型的每个成员提供值，可能是因为这些成员是关系对象，或者它们没有在控件中渲染。在这些情况下，最好是获取主键，从数据源加载模型，并告诉模型绑定系统将数据控件中的值绑定到模型。列表 9-7 显示了更新方法如何更新记录。

## 列表 9-7：使用主键作为参数的模型更新

```asp
<asp:DetailsView runat="server" ItemType="Customer" SelectMethod="SelectCustomers"
UpdateMethod="UpdateCustomer" AutoGenerateButton="true" DataKeyNames="ID">
```

### VB

```vb
Private _context As New VB.CustomerContext()

Public Function SelectCustomers() As VB.Customer
    Return _context.Customer.First()
End Function

Public Sub UpdateCustomer(id As Integer)
    _context = New VB.CustomerContext()
    Dim customer = _context.Customer.Where(Function(c) c.ID = id).First()
    TryUpdateModel(customer)
    If ModelState.IsValid Then
    End If
End Sub
```

### C#

```csharp
CustomerContext _context = new CustomerContext();

public Customer SelectCustomers()
{
    return _context.Customer.First();
}

public void UpdateCustomer(int id)
{
    _context = new CustomerContext();
    var customer = _context.Customer.Where(c => c.ID == id).First();
    TryUpdateModel(customer);
    if (ModelState.IsValid)
    {
    }
}
```

列表 9-7 显示了如何更新记录。所有数据绑定控件都有一个名为 `DataKeyNames` 的属性，它可以唯一标识一条记录。该属性包含主键字段的名称。当 `DetailsView` 控件执行更新操作时，模型绑定系统会将 `DataKeyNames` 属性的值填充到更新方法中。此参数（`id`）现在持有主键（ID）的值，可用于检索用户正在更新的特定记录。当你调用 `TryUpdateModel` 时，模型绑定系统会将用户在插入或更新记录时指定的值更新到客户模型中。

> **注意**：正如你通过设置控件上的 `UpdateMethod` 属性来执行更新操作，你也可以设置 `DeleteMethod` 来对记录执行删除操作。

## 在模型绑定系统中验证记录

在大多数情况下，在将记录保存到数据库之前，你需要对记录进行某些自定义业务逻辑验证。模型绑定使得这种场景的实现非常简单，并产生更整洁实现。如果你在 `ObjectDataSource` 中使用验证规则，则无法将异常从业务层传回到页面。你最终会在业务层抛出异常，在控件中捕获它，然后显示自定义的错误消息。这使得代码更加实际。

模型绑定系统的优势在于它将绑定与验证清晰地分离。你可以非常轻松地使用自定义验证。来自模型绑定系统的验证错误通过验证摘要（Validation Summary）显示，因此便于自定义 UI 并保持代码整洁。

在 ASP.NET Web Forms 中启用绑定的一个好处是，你可以接入不同的验证机制。例如，你可以使用数据注解（Data Annotations），它允许你为模型的任何元数据添加属性。模型绑定系统可以在验证期间使用这些元数据。列表 9-8 显示了如何告诉模型绑定系统 `FirstName` 字段是必须的。

## 列表 9-8：添加数据注解

### VB

```vb
<Required()>
Public Property FirstName() As String
    Get
        Return m_FirstName
    End Get
    Set(value As String)
        m_FirstName = value
    End Set
End Property
```

### C#

```csharp
[Required()]
public string FirstName { get; set; }
```
