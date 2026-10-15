

这意味着你可以在 Person 类中通过添加以下代码来重写从 Object 类继承的 ToString 方法：

```
Public Overrides Function ToString() As String
    Return Name
End Function
```

此实现在调用 ToString 时会返回人员的 Name 属性作为结果。

> 默认情况下，ToString 返回类的类名。直到现在，如果你在 Person 对象上调用 ToString 方法，你会得到 InheritanceAndInterfaces.Person 的结果。InheritanceAndInterfaces 在你创建项目时代表你的程序集名称。

请注意，ToString 方法正在调用你同一类中的另一个方法——在本例中为 Name 方法。

你也可以使用 Me 关键字编写此例程：

```
Public Overrides Function ToString() As String
    Return Me.Name
End Function
```

这是多余的，因为 Me 是类中所有方法调用的默认值。这两种实现是相同的，因此通常会省略 Me 关键字以避免额外的输入。

要查看 ToString 方法现在如何工作，你可以更改 Form1 中的代码，使用此值而不是 Name 属性：

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click
    Dim objPerson As OfficeEmployee = New OfficeEmployee()

    With objPerson
        .Name = "Fred"
        .BirthDate = #1/1/1960#
        .Age = 20
        .OfficeNumber = "A42"

        txtName.Text = .ToString()
        txtBirthDate.Text = Format(.BirthDate, "Short date")
        txtAge.Text = CStr(.Age)
        txtOffice.Text = .OfficeNumber
    End With
End Sub
```

运行应用程序时，人员的姓名会适当显示，这是有意义的，因为 ToString 方法只是返回 Name 属性的结果。

之前，你查看了虚方法以及它们的工作方式。因为直接调用方法或使用 Me 关键字调用方法都会在当前对象上调用该方法，所以方法调用遵循与外部方法调用相同的规则。换句话说，你的 ToString 方法可能实际上并不会调用 Person 类中的 Name 方法，如果该方法已被继承链中更下游的类（如 Employee 或 OfficeEmployee 类）重写。

例如，你可以在 OfficeEmployee 类中重写 Name 属性，使其始终返回人员的非正式姓名，而不是常规姓名。你可以通过向 OfficeEmployee 类添加此方法来重写 Name 属性：

```
Public Overloads Overrides Property Name() As String
    Get
        Return MyBase.Name(NameTypes.Informal)
    End Get
    Set(ByVal value As String)
        MyBase.Name = value
    End Set
End Property
```

来自 OfficeEmployee 的代码片段

Name 方法的这个新版本依赖于基类来实际存储值，但与请求时返回常规姓名不同，现在你始终返回非正式姓名：

```
Return MyBase.Name(NameTypes.Informal)
```

在你测试之前，需要增强表单中的代码以实际提供非正式姓名的值。对代码进行以下更改：

```
Private Sub btnOK_Click(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles btnOK.Click

    Dim objPerson As OfficeEmployee = New OfficeEmployee()

    With objPerson
        .Name = "Fred"
        .Name(NameTypes.Informal) = "Freddy"
        .BirthDate = #1/1/1960#
        .Age = 20
        .OfficeNumber = "A42"

        txtName.Text = .ToString()
        txtBirthDate.Text = Format(.BirthDate, "Short date")
        txtAge.Text = CStr(.Age)
        txtOffice.Text = .OfficeNumber
    End With
End Sub
```

来自 Form1 的代码片段

运行应用程序时，Name 字段会显示非正式姓名。即使 ToString 方法是在 Person 类中实现的，它也在调用 OfficeEmployee 类中 Name 的实现。这是因为类内部的方法调用遵循与类外部代码（如表单中的代码）调用虚方法相同的规则。使用或不使用 Me 关键字你都会看到这种行为，因为方法调用的默认行为是隐式地通过当前对象调用。

虽然从类内部调用的方法遵循虚方法的相同规则，但这对于被隐藏的方法并不成立。这里，从类内部调用被隐藏方法的规则与从类外部调用的规则不同。

要了解其工作原理，请将 OfficeEmployee 中的 Name 属性改为被隐藏的方法而不是被重写的方法：

```
Public Shadows Property Name() As String
    Get
        Return MyBase.Name(NameTypes.Informal)
    End Get
    Set(ByVal value As String)
        MyBase.Name = value
    End Set
End Property
```

> 没有办法直接沿着继承链向上导航超过直接的父类，因此如果你在子子类中，就无法直接访问基类中方法的实现。这种行为无论如何都不是一个好主意，这就是为什么不允许这样做。

MyBase 关键字可用于调用或使用父类中的任何 Public、Friend 或 Protected 元素。这包括基类上的所有元素，以及基类从继承链中更高层的其他类继承的任何元素。

你已经使用 MyBase 在 Employee 类中实现重写的 Name 属性时回调到基 Person 类。

> 任何子类中的代码都可以通过使用 MyBase 关键字调用基类上的任何方法。

你也可以使用 MyBase 在你隐藏了方法的情况下回调到基类实现。尽管当时没有说明，你已经在 OfficeEmployee 类中对 Name 属性的被隐藏实现中做到了这一点。粗体行指示你在从被隐藏方法内部调用到基类的位置：

```
Public Shadows Property Name() As String
    Get
        Return MyBase.Name(NameTypes.Informal)
    End Get
    Set(ByVal value As String)
        MyBase.Name = value
    End Set
End Property
```

来自 OfficeEmployee 的代码片段

MyBase 关键字使你能够将基类的功能按你认为合适的方式合并到你的子类代码中。

## MyClass 关键字

正如你所见，当你使用 Me 关键字或直接调用方法时，你的方法调用遵循调用虚方法和非虚方法的规则。换句话说，如 Name 属性前面所示，从 Person 类中的代码对 Name 的调用实际上会调用位于 OfficeEmployee 类中的重写版本的 Name。

虽然这种行为通常很有用，但有时你希望确保你确实运行的是来自你类的特定实现；即使子类重写了你的方法，你仍然希望确保你调用的是直接在你类中的方法版本。

也许你决定 Person 中的 ToString 实现应始终调用你在 Person 类中编写的 Name 实现，完全忽略任何子类中 Name 的重写版本。

这就是 MyClass 关键字大放异彩的地方。此关键字与 MyBase 类似，因为它提供了对方法（如对象引用）的访问——在这种情况下，是对包含你在使用 MyClass 关键字时编写的代码的类的实例的引用。这即使在实例化的对象是派生自你类的类的实例时也为真。

property in OfficeEmployee 使其成为重写的方法，而不是被隐藏的方法，以演示其工作原理：

```
Public Overloads Overrides Property Name() As String
    Get
        Return MyBase.Name(NameTypes.Informal)
    End Get
    Set(ByVal value As String)
        MyBase.Name = value
    End Set
End Property
```

来自 OfficeEmployee 的代码片段

有了此更改，并且基于你之前的测试，你知道 Person 中的 ToString 实现将自动调用 Name 属性的此重写版本，因为对 Name 方法的调用遵循虚方法的正常规则。事实上，如果你现在运行应用程序，表单上的 Name 字段将显示 Freddy，即人员的非正式姓名。

你可以通过使用 MyClass 来强制使用当前类中的实现。按如下方式更改 Person 中的 ToString 方法：

```
Public Overrides Function ToString() As String
    Return MyClass.Name
End Function
```

你现在正在调用 Name 方法，但你使用的是 MyClass 关键字。当你运行应用程序并单击按钮时，表单中的 Name 字段显示 Fred 而不是 Freddy，证明即使对象的实际数据类型是 OfficeEmployee，也调用了来自 Person 的实现。

ToString 方法是从 Person 调用的，因为 Employee 也不提供重写的实现。然后，由于你使用的是 MyClass 关键字，Name 方法直接从 Person 调用，明确地击败了你通常期望的默认行为。

## 构造函数

如第 2 章所述，你可以在类上提供一个名为 New 的特殊构造函数方法，当对象被实例化时它将是运行的第一段代码。你也可以通过构造函数方法接收参数，使创建对象的代码能够在创建过程中将数据传递给对象。

构造函数方法受继承的影响方式与常规方法不同。像 Person 类上的 BirthDate 这样的普通 Public 方法会自动被任何子类继承。从那里你可以重载、重写或隐藏该方法，如前所述。

### 简单构造函数

构造函数并不完全遵循相同的规则。为了探索差异，让我们在 Person 类中实现一个简单的构造函数方法：

```
Public Sub New()
    Debug.WriteLine("Person constructor")
End Sub
```

如果你现在运行应用程序，你将在 IDE 中的输出窗口中看到显示的文本。这即使在你的表单代码中创建的是 OfficeEmployee 类型的对象时也会发生：

```
Dim person As Employee = New OfficeEmployee()
```

正如你所期望的那样，基 Person 类的 New 方法作为 OfficeEmployee 对象构造过程的一部分被调用——简单的继承在起作用。然而，如果你在 OfficeEmployee 类本身中实现 New 方法，就会发生有趣的事情：

