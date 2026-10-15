

你之前创建的 Person 类。这次它会自动在正确的项目中创建它们。注意你也可以选择将新项添加为方法或字段以及属性。

接下来，向测试类添加第二个测试方法。这个第二个方法 ConstructorEmployeeInitializes 将定义一个测试，该测试也会构造一个新的 Employee，但这次使用一个接受三个参数来填充属性的构造函数：

```
<TestMethod()> Public Sub ConstructorEmployeeInitializes()
    Dim emp As New Person.Employee("Foo deBar", 33000, DateTime.Today)
    'confirm the properties are set
    StringAssert.Contains(emp.Name, "Foo deBar")
    Assert.AreEqual(emp.Salary, 33000D)
    Assert.AreEqual(emp.HireDate, DateTime.Today)
End Sub
```

来自 Person 的代码片段

再次出现了蓝色的波浪线，并且再次可以使用智能标记菜单通过从智能标记菜单中选择“在 Person.Employee 中生成构造函数存根”来创建新的构造函数。但是这样做时，更早的方法中的代码下方会出现更多行。现在使用默认构造函数创建新的 Employee 已变得无效，因为类中只有一个构造函数：接受三个参数的那个。幸运的是，为了减少对你打字手指的磨损，智能标记菜单使你能够向 Employee 类添加默认构造函数。测试类的最终结构如下：

```
<TestClass()> Public Class PersonTests
    <TestMethod()> Public Sub DefaultEmployeeInitializes()
        Dim emp As New Person.Employee
        'ensure default property values
        Assert.AreEqual(emp.Name, String.Empty)
        Assert.AreEqual(emp.Salary, Decimal.Zero)
        Assert.AreEqual(emp.HireDate, DateTime.MinValue)
    End Sub

    <TestMethod()> Public Sub ConstructorEmployeeInitializes()
        Dim emp As New Person.Employee("Foo deBar", 33000, DateTime.Today)
        'confirm the properties are set
        StringAssert.Contains(emp.Name, "Foo deBar")
        Assert.AreEqual(emp.Salary, 33000D)
        Assert.AreEqual(emp.HireDate, DateTime.Today)
    End Sub
End Class
```

来自 Person 的代码片段

当然，生成的代码并不完美。Visual Studio 没有简单的方法来确定每个属性应该是什么类型；而且如果你创建了方法，就没有办法确定这些方法的主体。生成的 Employee 类如下所示：

```
Public Class Employee

    Private _p1 As String
    Private _p2 As Integer
    Private _p3 As Date
    Sub New(ByVal p1 As String, ByVal p2 As Integer, ByVal p3 As Date)
        ' TODO: Complete member initialization
        _p1 = p1
        _p2 = p2
        _p3 = p3
    End Sub
    Sub New()
        ' TODO: Complete member initialization
    End Sub
```

```
Property Name As Object
Property Salary As Object
Property HireDate As Object
End Class
```

来自 Person 的代码片段

请注意，三个属性都已创建为 Object，并且构造函数的参数——虽然正确——并没有非常描述性的名称。因此，类的代码可以稍微清理一下：为构造函数参数赋予更有用的名称，并为三个属性应用正确的数据类型。在此期间，你也可以为 Salary 属性添加一些验证，禁止负值。编辑 Employee 类后，它应如下所示：

```
Public Class Employee
    Private _name As String
    Private _salary As Decimal
    Private _hireDate As Date

    Sub New(ByVal name As String,
            ByVal salary As Decimal,
            ByVal hireDate As Date)
        Me.Name = name
        Me.Salary = salary
        Me.HireDate = hireDate
    End Sub
    Sub New()
        Me.Name = String.Empty
        Me.Salary = Decimal.Zero
        Me.HireDate = DateTime.MinValue
    End Sub
    Property Name As String
        Get
            Return _name
        End Get
        Set(ByVal value As String)
            _name = value
        End Set
    End Property
    Property Salary As Decimal
        Get
            Return _salary
        End Get
        Set(ByVal value As Decimal)
            If value < 0 Then
                Throw New ArgumentOutOfRangeException("Salary cannot be negative")
            End If
            _salary = value
        End Set
    End Property
    Property HireDate As Date
        Get
            Return _hireDate
        End Get
        Set(ByVal value As Date)
            _hireDate = value
        End Set
    End Property
End Class
```

来自 Person 的代码片段

Name 和 HireDate 属性的简短版本可以保持原样，因为你没有在其中执行任何验证。请注意，构造函数并没有直接写入私有成员变量，而是调用属性。这确保了你添加到属性中的任何验证也适用于构造函数。对于 Salary 属性，它会测试传入的负值。如果发生这种情况，则会抛出新的异常。

向测试类 `PersonTests` 添加第三个测试方法。此测试将确认添加到 `Salary` 属性中的验证确实会抛出异常：

```
```vb
<TestMethod()> Public Sub SalaryCannotBeNegative()
    Try
        Dim emp As New Person.Employee("Foo deBar", -10, DateTime.Today)
        'if we get to this line, there is a problem
        'as the line should have triggered the exception
        Assert.Fail("Employee salary cannot be negative")
    Catch aex As ArgumentOutOfRangeException
        'this is caused by passing in a negative value
        'as it is expected, we'll ignore it
        'which will return a success for the test
    Catch ex As Exception
        'deal with other exceptions here
        Assert.Fail(ex.Message)
    End Try
End Sub
```
```

> *来自 Person 的代码片段*

这个测试乍一看有点违反直觉。记住你试图引发一个异常，所以这有点像编写双重否定。该方法首先尝试创建一个新的 `Employee`，传入与之前相同的 `Name` 和 `hireDate`，但现在 `Salary` 为负值。如果类已正确编码，这应该会抛出 `ArgumentOutOfRangeException`。因此，如果代码没有抛出异常，它将继续执行构造函数之后的代码，这意味着代码中存在问题。代码随后会使测试失败。如果相反抛出了正确的异常，代码会静默忽略它，这意味着测试会通过。这种构造测试的方法使你能够确保你的类已以防御方式定义。你现在应该能够运行这三个测试并看到它们通过。

在 Visual Studio 中使用“根据使用情况生成”功能可以在创建测试及其测试的类时节省大量时间。它使你能够先编写测试，然后几乎立即执行测试，同时为你提供所需类的核心。

## 其他 Visual Studio 版本

本章重点介绍 Visual Studio Professional 版中包含的测试功能。表 7-5 描述了 Premium 和 Ultimate 版本，它们在测试时包含大量额外的功能。

**表 7-5：** Visual Studio Premium 和 Ultimate 版本的功能

| 版本 | 功能 | 描述 |
|---|---|---|
| Premium | 代码覆盖率 | 此功能将分析你的代码和测试，并允许你确定类的功能有多少实际上被测试了。理想情况下，你希望此值尽可能高，因为这意味着你正在测试应用程序的大部分功能。 |
|  | 测试影响分析 | 此功能分析你的代码和测试并确定代码更改后需要哪些测试。如果你的测试数量很多，这可以节省大量时间，因为这意味着在更新代码后你只需要执行其中一部分。 |

