
`Using`语句自动化了获取资源、执行一组语句然后释放资源的过程。例如，内部的`Using`语句由编译器处理，就像你写了以下代码：

```
Dim log As StreamWriter = New StreamWriter(fs)
Try
    log.WriteLine(entry)
Finally
    If log IsNot Nothing Then
        log.Dispose()
    End If
End Try
```

该语句有两种形式。在一种形式中，资源是作为语句的一部分声明的局部变量，被视为普通的变量声明语句。在另一种中，资源是表达式的结果。带有局部变量定义的`Using`语句可以一次获取多个资源，这等同于嵌套的`Using`语句。因此，之前的嵌套语句也可以如下所示编写，同时保持与嵌套版本完全一致的语义：

```
Using fs As FileStream = New FileStream("log.txt", FileMode.Append),
      log As StreamWriter = New StreamWriter(fs)
log.WriteLine(entry)
End Using
```

# Visual Basic 2008 (9.0)

.NET 3.5引入了新的语言集成查询`LINQ`技术。与`C# 3.0`一样，`Visual Basic 2008`为语言添加了许多优秀特性，允许程序员在创建数据处理操作时，表达他们想要得到什么，而不是表达他们如何获取结果。

该版本最令人兴奋的特性无疑是通过查询表达式支持`LINQ`，这些表达式因其可读性和表达力而非常流行。为了实现这种强度，语言中还引入了以下其他“语法降噪”特性，即使脱离查询表达式的上下文使用它们，它们也被证明是有用的：

- 局部变量类型推断
- 扩展方法
- 对象创建表达式
- Lambda 表达式
- 查询表达式
- 部分方法
- XML 字面量表达式
- 可空值类型修饰符
- 真正的条件运算符

让我们详细地查看这些特性。

## 局部变量类型推断

在`Visual Basic`语言中，有几个地方可以认为语法是“嘈杂”的——即开发者必须输入很多字符来表达他们的意图。例如，当你想要为字典声明局部变量并立即初始化它时，你使用的类似于下面的代码：

```
Dim myCodeTable As Dictionary(Integer, String) = New Dictionary(Integer, String)
```

在此定义中，`Dictionary(Integer, String)`表达式出现了两次，这可以被称为噪声。`Visual Basic 2008`有一个新的选项`Infer`，可以开启或关闭。开启它可以减少这种噪声，如下：

```
Option Infer
Dim myCodeTable = New Dictionary(Integer, String)
```

当你使用`Option Infer On`时，编译器会解析等号右边的表达式并推断其类型。如果你关闭推断（使用`Option Off`），之前的声明在语法上仍然是正确的。但在第一种情况下，`myCodeTable`的类型是隐式的。你同样可以在`For Each`语句和`Using`语句中使用该局部变量声明。

## 扩展方法

开发者经常为对象封装方法。一个很好的例子是检查字符串中的字符是否为大写的方法。这种声明可以放在标准模块中，如下：

```
Module StringHelper
  Public Function IsUpper(ByVal s As String) As Boolean
    For Each c In s
      If Not Char.IsUpper(c) Then Return False
    Next
    Return True
  End Function
End Module
```

使用这个助手方法时，你编写的代码如下：

```
Dim myString = "This is a String"
Dim isUpper = StringHelper.IsUpper(myString)
```

扩展方法提供了一种实现相同模式并使用更漂亮（更具可读性）语法的方法。扩展方法是应用了`System.Runtime.ExtensionAttribute`属性的方法。它们只能在标准模块中声明，并且至少有一个参数，指定它所扩展的类型。声明中的此细微变化使其成为扩展方法：

```
Imports System.Runtime.CompilerServices

Module StringHelper
  <Extension()>
  Public Function IsToUpper(ByVal s As String) As Boolean
  ...
  End Function
End Module
```

该方法在语法上可以使用，就像它是`String`的实例方法一样：

```
Dim myString = "This is a String"
Dim result = myString.IsToUpper()
```

## 对象创建表达式

`.NET Framework`内的类型高度依赖字段和属性的使用。在实例化新类时，创建如下代码是常见的：

```
Public Class Customer
  Public ID As Integer
  Public Name As String
  Public IsAccount As Boolean
End Class

Dim customer As Customer = New Customer
customer.ID = 112
customer.Name = "John Doe"
customer.IsAccount = True
```

对象创建表达式允许你使用更短且具表达力的语法重写上述代码，且语义完全相同：

```
Dim customer = New Customer(.ID = 112, .Name = "John Doe", .IsAccount = True)
```

对象创建表达式可以在构造函数参数之后可选地指定成员初始化器列表。这些初始化器以`With`为前缀，初始化器列表的解释方式就像在`With`语句的上下文中一样。

`Visual Basic 2008`最方便的特性之一是使用匿名对象创建表达式“即时”创建新类型的能力。对象创建表达式的成员初始化器可以完全省略类型名称。在这种情况下，将根据作为表达式一部分初始化的成员的类型和名称来构造一个匿名类型。考虑以下示例：

```
Module AnonymousType
  Sub Main()
    Dim order = New With {.ID = 101, .Date = #1/1/2010#, .ProductID = "Q3456", .Quantity = 123}
    Console.WriteLine("ProductID: {0}, Quantity: {1}", order.ProductID, order.Quantity)
  End Sub
End Module
```

当然，编译器在后台创建了一个真实的类型，但并未向你暴露名称。在`Option On`的情况下，你不需要命名类型即可声明匿名类型，如下：

```
Option Infer
Dim order2 = New With {.Date = #12/31/2009#} '声明为匿名类型
```

默认情况下，匿名类型生成的属性是可读写的。除非使用`Key`修饰符，否则无法将匿名类型标记为只读：

```
Dim order = New With {Key .ID = 101, .Date = #1/1/2010#}
```

`Key`修饰符指定了唯一标识匿名类型所值的字段。

## Lambda 表达式

`Lambda`表达式提供了一种新的简洁语法来描述包含表达式的匿名函数，并用于创建委托。`Lambda`表达式定义了一个称为`Lambda`方法的匿名方法。`Lambda`方法方便内联传递给接受委托类型的方法。

在`Visual Basic 2005`中，你将使用显式委托，例如：

```
Module VB2005Module
  Delegate Function BinaryOperation(ByVal op1 As Double,
    ByVal op2 As Double) As Double

  Sub Main()
    Dim op1 As Double = 12.3
    Dim op2 As Double = 23.4
    Dim operation As BinaryOperation = AddressOf MyOperation
    Dim result As Double = operation(op1, op2)
  End Sub

  Function MyOperation(ByVal op1 As Double, ByVal op2 As Double) As Double
    Return op1 + op2
  End Function
End Module
```

在`Visual Basic 2008`中，你可以使用`Lambda`表达式代替：

```
Dim operation As BinaryOperation = Function(op1, op2) Return op1 + op2
```

Return (op1 + op2) / op2

End Function

End Module
```

`Lambda`表达式提供了更简洁的语法和类型推断，使得可以用更直观的方式来描述操作委托：

```vb
Sub Main()
Dim op1 As Double = 12.3
Dim op2 As Double = 23.4
Dim operation As BinaryOperation = Function(x As Double, y As Double) (x + y) / y
Dim result As Double = operation(op1, op2)
End Sub
```

`Lambda`表达式以`Function`关键字和参数列表开始。`Lambda`表达式中的参数不能声明为`Optional`或`ParamArray`，且不能属性属性与普通方法不同，`Lambda`方法中省略参数类型不会自动推断为`Object`。相反，当引用`Lambda`方法时，省略的参数类型将根据目标类型推断。

### 查询表达式

查询表达式提供了`LINQ`的“语言集成”体验，因为它们提供了类似于`SQL`的语法来描述查询。查询表达式以`From`或`Aggregate`符开始，并以任何查询运算符结束。表达式中间的其他有效子句包括`From`、`Where`、`Join`、`Distinct`、`Take`、`While`、`Skip`、`Aggregate`、`Order By`和`Group By`运算符。

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

基础编译器将查询表达式翻译为方法调用。例如，`Where`子句将翻译为`Where`方法的调用，`Order`将翻译为`OrderBy`的调用，依此类推。这些方法成为被查询类型的扩展方法或实例方法。因此，在前面的示例中，代表`fruits`的类型必须具有这种特性。方法（而不是编译器）将在运行时决定如何执行查询。

查询表达式的这种扩展性使得`LINQ`成为一个非常强大的功能，它实现了从命令式数据处理模型向声明式模型的转变。

> 使用`LINQ`和查询表达式绝对超出了本书的范围。你可以找到许多关于`LINQ`的详细书籍，例如`Scott Klein`写的《Professional LINQ》(`Indianapolis: Wiley, 2008`)。你也可以查看《Visual Basic 语言规范》以获取更多信息。`MSDN`也为你提供了`Visual Basic LINQ`示例，地址为`http://msdn.microsoft.com/en-us/library/bb397978.aspx`。

### 部分方法

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

如果`Customization.vb`文件不包含`BeforeAddingElement`方法的实现部分，则`Collection.vb`中的该方法将不会编译。

当然，部分方法有一些限制。例如，它们必须是`Sub`，不允许使用`ByRef`参数，不能有访问修饰符，且不能是`Overridable`。

### XML 字面量表达式

`.NET`编程语言中处理`XML`字面量的简单性是`Visual Basic 2008`核心功能中的独特特性。`XML`字面量表示`XML 1.0`值，可以以`XML`文档、`XML`元素、`XML`处理指令、`XML`注释或`CDATA`区的形式存在。使用`XML`字面量可以的操作非常多，这一节的内容就足以让你看不过来了。这里有一个短示例：

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

`XML`字面量表达式的结果是一个类型为`System.Xml.Linq`命名空间中某种类型的值。如果如果这些类型可用，则`XML`字面量表达式将导致编译错误。

在之前的示例中，`Customer`定义了一个`XML`元素`Customers`，它从表达式开始就是一个`XML`文档。你可以看到`Customers`使用嵌入表达式(`name`)来创建一个`Name`属性设置为`Jane Doe`的`XML`文档。

`XML`元素可以包含命名空间声明，如`XML 1.0`规范定义。你可以使用源文件的`Imports`部分来定义`XML`命名空间：

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

第一个`Import`设置了默认`XML`命名空间，`db`前缀用于在`http://myOrg.com/OrderDB`中定义的命名空间。你还可以使用成员表达式来访问`XML`文档表示的层次结构中的元素。以下示例显示了如何在`XMLNamespaces`模块中访问元素和属性：
