

Return (op1 + op2) / op2
End Function

End Module

Lambda 表达式提供了更简洁的语法和类型推断，使得可以用更直观的方式来描述操作委托：

```vb
Sub Main()
Dim op1 As Double = 12.3
Dim op2 As Double = 23.4
Dim operation As BinaryOperation = Function(x As Double, y As Double) (x + y) / y
Dim result As Double = operation(op1, op2)
End Sub
```

Lambda 表达式以 `Function` 关键字和参数列表开始。Lambda 表达式中的参数不能声明为 `Optional` 或 `ParamArray`，且不能属性属性与普通方法不同，Lambda 方法中省略参数类型不会自动推断为 `Object`。相反，当引用 Lambda 方法时，省略的参数类型将根据目标类型推断。

## 查询表达式

查询表达式提供了 LINQ 的“语言集成”体验，因为它们提供了类似于 SQL 的语法来描述查询。查询表达式以 `From` 或 `Aggregate` 符开始，并以任何查询运算符结束。表达式中间的其他有效子句包括 `From`、`Where`、`Join`、`Distinct`、`Take`、`While`、`Skip`、`Aggregate`、`Order By` 和 `Group By` 运算符。

来看一个例子：

```vb
Dim fruits As String = {"Apple", "Peach", "Orange", "Banana", "Lemon", 
"Pear", "Grapefruit", "Watermelon", "Plum"}

Dim filteredFruits =
From fruit In fruits
Where fruit.StartsWith("P") And fruit.Length < 20
Order By
Select fruit
```

这种表示法的优势在于，它描述了你想要的结果意图，而不是定义你如何获取它。

基础编译器将查询表达式翻译为方法调用。例如，`Where` 子句将翻译为 `Where` 方法的调用，`Order` 将翻译为 `OrderBy` 的调用，依此类推。这些方法成为被查询类型的扩展方法或实例方法。因此，在前面的示例中，代表 fruits 的类型必须具有这种特性。方法（而不是编译器）将在运行时决定如何执行查询。

查询表达式的这种扩展性使得 LINQ 成为一个非常强大的功能，它实现了从命令式数据处理模型向声明式模型的转变。

> 使用 LINQ 和查询表达式绝对超出了本书的范围。你可以找到许多关于 LINQ 的详细书籍，例如 Scott Klein 写的《Professional LINQ》（Indianapolis: Wiley, 2008）。你也可以查看《Visual Basic 语言规范》以获取更多信息。MSDN 也为你提供了 Visual Basic LINQ 示例，地址为 http://msdn.microsoft.com/en-us/library/bb397978.aspx。

## 部分方法

部分方法存在于类型中。如果方法指定了签名但没有方法体，则它就是部分方法。方法体由另一个具有相同名称和签名的方法声明提供，最可能在该类型的另一个部分声明中。

这提高了了性能，因为你不需要加载/创建不需要的方法。这是一个示例：

```vb
Collection.vb: 这是通常自动生成的类。
Partial Public Class CustomTypedCollection
Partial Private Sub BeforeAddingElement(ByVal element As CustomElement)
End Sub

Public Sub AddElement(ByVal element As CustomElement)
BeforeAddingElement(element)
End Class
```

```vb
Customization.vb: 这部分是开发者作为自定义添加的内容
Partial Public Class CustomTypedCollection
Private Sub BeforeAddingElement(ByVal element As CustomElement)
Console.WriteLine("Element " & element.ToString() & " is being added.")
End Sub
End Class
```

如果 `Customization.vb` 文件不包含 `BeforeAddingElement` 方法的实现部分，则 `Collection.vb` 中的该方法将不会编译。

当然，部分方法有一些限制。例如，它们必须是 `Sub`，不允许使用 `ByRef` 参数，不能有访问修饰符，且不能是 `Overridable`。

## XML 字面量表达式

.NET 编程语言中处理 XML 字面量的简单性是 Visual Basic 2008 核心功能中的独特特性。XML 字面量表示 XML 1.0 值，可以以 XML 文档、XML 元素、XML 处理指令、XML 注释或 CDATA 区的形式存在。使用 XML 字面量可以的操作非常多，这一节的内容就足以让你看不过来了。这里有一个短示例：

```vb
Module XMLLiterals
```

```vb
Dim Customer As XElement =
  <Customer ID="112" Name="John Doe" IsAccount="True"/>
Dim name = "Jane Doe"
Dim Customers As XDocument =
  <?xml version="1.0"?>
  <Customers>
    <Customer ID="112" Name="John Doe" IsAccount="True"/>
    <Customer ID="113" Name="<%= name %>" IsAccount="True"/>
    <Customer ID="114" Name="Alf Kiter" IsAccount="False"/>
  </Customers>
```

```vb
End Module
```

XML 字面量表达式的结果是一个类型为 `System.Xml.Linq` 命名空间中某种类型的值。如果如果这些类型可用，则 XML 字面量表达式将导致编译错误。

在之前的示例中，`Customer` 定义了一个 XML 元素 `Customers`，它从表达式开始就是一个 XML 文档。你可以看到 `Customers` 使用嵌入表达式 (`name`) 来创建一个 `Name` 属性设置为 Jane Doe 的 XML 文档。

XML 元素可以包含命名空间声明，如 XML 1.0 规范定义。你可以使用源文件的 `Imports` 部分来定义 XML 命名空间：

```vb
Imports xmlns="http://myOrg.com"
Imports xmlns:db="http://myOrg.com/myDB"
```

```vb
Module XMLNamespaces
Dim Customers As XDocument =
  <?xml version="1.0"?>
  <Customers>
    <Customer ID="112" Name="John Doe" IsAccount="True"/>
    <Customer ID="113" Name="Jane Doe" IsAccount="True"/>
    <Customer ID="114" Name="Alf Kiter" IsAccount="False"/>
    <db:Order xmlns:db="http://myOrg.com/OrderDB">
      <db:ProductID>Q123</db:ProductID>
      <db:Amount>100</db:Amount>
    </db:Order>
  </Customers>
```

```vb
End Module
```

第一个 `Import` 设置了默认 XML 命名空间，`db` 前缀用于在 http://myOrg.com/OrderDB 中定义的命名空间。你还可以使用成员表达式来访问 XML 文档表示的层次结构中的元素。以下示例显示了如何在 `XMLNamespaces` 模块中访问元素和属性：

```vb
Dim thirdCustomer As XElement = Customers..(2)
Dim thirdCustomerName As String = thirdCustomer.@Name
Dim thirdCustomerID As Integer = thirdCustomer.<db:ID>
Dim order As XElement = thirdCustomer.<db:Order>
```

`...descendants>` 运算符允许你进入所应用元素的元素的后代集合。`..qualifiedname` 运算符导航到单个元素。`.name` 和 `..qualified>` 运算符用于访问元素属性。

