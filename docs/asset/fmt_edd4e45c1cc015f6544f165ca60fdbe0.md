
```
Dim person As Employee = New OfficeEmployee()
```

正如你所期望的那样，基`Person`类的`New`方法作为`OfficeEmployee`对象构造过程的一部分被调用——简单的继承在起作用。然而，如果你在`OfficeEmployee`类本身中实现`New`方法，就会发生有趣的事情：

```
Public Sub New()
    Debug.WriteLine("OfficeEmployee constructor")
End Sub
```

注意，你没有使用`Overrides`关键字，也没有将`Person`中的方法标记为`Overridable`。这些关键字在此上下文中没有用处，实际上，如果你试图将它们用于构造函数方法，还会导致语法错误。

现在运行该应用程序时，你可能会期望只会调用`OfficeEmployee`中`New`的实现。当然，对于普通的被重写方法来说，确实如此。但`New`并没有被重写，因此当你运行应用程序时，两个实现都会运行，两行字符串都会输出到 IDE 的输出窗口中。

请注意，`Person`类中的实现先运行，随后是`OfficeEmployee`类中的实现。这是因为在创建对象时，继承链中所有类的构造函数都会被调用，从基类开始，逐一到所有子类。实际上，如果你在`Employee`类中实现一个`New`方法，你会发现它也会被调用：

```
Public Sub New()
    Debug.WriteLine("Employee constructor")
End Sub
```

当应用程序运行并单击按钮时，输出窗口会出现三行字符串。从`Person`类到`OfficeEmployee`类，三个构造函数方法都被调用了。

### 深入探讨构造函数

无参构造函数的规则相当简单直接，但一旦你开始在构造函数中要求参数，事情就会变得复杂一些。

要理解原因，你需要考虑即便是最简单的构造函数是如何被调用的。虽然你可能会认为它们是从基类开始，一直向下经过所有子类，最后到最终子类；但实际情况略有不同。

特别地，首先被调用的其实是子类的`New`方法。不过，Visual Basic 在编译时会自动在你的例程中插入一行代码。例如，在`OfficeEmployee`类中，你有这样一个构造函数：

```
Public Sub New()
    Debug.WriteLine("OfficeEmployee constructor")
End Sub
```

在幕后，Visual Basic 会替你插入一条实际上是对父类构造函数的调用。你也可以使用`MyBase`关键字手动完成这一操作，改动如下：

```
Public Sub New()
    MyBase.New()
    Debug.WriteLine("OfficeEmployee constructor")
End Sub
```

这一调用必须是构造函数中的第一行。如果你在该行之前放置任何其他代码，就会收到语法错误，提示你的代码无效。由于这一调用总是必需的，并且它始终必须是任何构造函数中的第一行，所以 Visual Basic 只是自动为你插入它。

注意，如果你没有通过实现`New`方法在类上显式提供构造函数，Visual Basic 会在幕后为你创建一个。这个自动创建的方法只有一行代码：

```
MyBase.New()
```

所有类都有构造函数，要么是你在编写`New`方法时显式创建的，要么是 Visual Basic 在编译类时隐式创建的。

> 构造函数有时被称为`ctor`，即`constructor`的缩写。`ILDASM`或`.NET Reflector`等工具经常使用这一术语。

通过始终在每个构造函数的第一行调用`MyBase.New`，可以保证实际上最先运行的是顶层基类中`New`的实现。每个子类都会调用父类的实现，一直沿着继承链向上，直到只剩基类为止。然后基类的代码运行，接着再依次运行各个子类的代码，如前所示。

### 带参数的构造函数

当构造函数不需要参数时，这一机制运行得很好；但如果构造函数确实需要一个参数，那么 Visual Basic 就无法自动替你进行该调用。毕竟，Visual Basic 怎么知道你想传递什么值作为参数呢？

为了了解其工作原理，请将`Person`类中的`New`方法改为要求一个`Name`参数。你可以使用该参数来初始化对象的`Name`属性：

```
Public Sub New(ByVal name As String)
    Me.Name = name
    Debug.WriteLine("Person constructor")
End Sub
```

现在，你的构造函数需要一个`String`参数，并使用它来初始化`Name`属性。你使用`Me`关键字使代码更易于阅读。有趣的是，编译器确实能够理解并正确编译以下代码：

```
Name = name
```

然而，阅读代码的开发人员可能根本看不明白这一点。通过用`Me`关键字作为属性名的前缀，你可以清楚地表明：你正在调用对象上的一个属性，并向它提供参数值。

此时，你的应用程序将无法编译，因为`Employee`类的`New`方法中存在错误。具体来说，Visual Basic 试图自动调用`Person`类的构造函数，但失败了，因为它不知道应该为这个新的`name`参数传递什么数据值。有三种方式可以解决这个错误：

- ► 将`name`参数设为`Optional`。
- ► 用另一个不需要参数的实现来重载`New`方法。
- ► 从`Employee`类内部手动提供`Name`参数值。

如果将`Name`参数设为`Optional`，就表示`New`方法可以带参数调用，也可以不带参数调用。因此，一个可行的选择是不带参数地调用该方法，这样 Visual Basic 默认的无参数调用就能正常工作。

如果重载`New`方法，那么你可以实现第二个不接受任何参数的`New`方法，这同样能让 Visual Basic 的默认行为像你所看到的那样工作。请记住，这种解决方案只会调用不带参数的`New`重载版本；需要参数的那个版本不会被调用。

修复该错误的最后一种方法，就是自己在`Employee`类的`New`方法中提供一个参数值。为此，请像下面这样修改`Employee`类：

```
Public Sub New()
    MyBase.New("George")
    Debug.WriteLine("Employee constructor")
End Sub
```

通过显式调用父类的`New`方法，你就能为它提供所需的参数值。此时，你的应用程序可以编译，但还无法运行。

### 构造函数、重载与变量初始化

这段代码中不容易看清的一点是，你实际上引入了一个非常隐蔽的 bug。`Person`类中的构造函数正在使用`Name`属性来设置值：

```
Public Sub New(ByVal name As String)
    Me.Name = name
    Debug.WriteLine("Person constructor")
End Sub
```

然而，`Name`属性被`Employee`类重写了，所以将要运行的是`Employee`类中的实现。不幸的是，该实现使用了一个`Dictionary`对象，而这个对象目前还不可用！事实证明，使用`New`语句在类中声明的任何成员变量（例如`Employee`中的`Dictionary`对象）都要等到该类的构造函数完成后才会被初始化：

```
Private mNames As New Generic.Dictionary(Of NameTypes, String)
```

因为你仍然处于`Person`的构造函数中，所以`Employee`的构造函数不可能已经完成。要解决这个问题，你需要稍微修改`Employee`类，使它不再依赖以这种方式创建的`Dictionary`。相反，你应该添加代码，在需要时创建它。

首先，修改`Employee`类中变量的声明：

```
Private mNames As Generic.Dictionary(Of NameTypes, String)
```

然后，更新`Name`属性，使其在需要时创建`Hashtable`对象：

```
Public Overloads Property Name(ByVal type As NameTypes) As String
Get
    If mNames Is Nothing Then mNames = New Generic.Dictionary(Of NameTypes, String)
    Return mNames(type)
End Get
Set(ByVal value As String)
    If mNames Is Nothing Then mNames = New Generic.Dictionary(Of NameTypes, String)
    If mNames.ContainsKey(type) Then
        mNames.Item(type) = value
    Else
        mNames.Add(type, value)
    End If
    If type = NameTypes.Normal Then
        MyBase.Name = value
    End If
End Set
End Property
```

来自 OfficeEmployee 的代码片段

这样可以确保在`Employee`类代码中创建`Dictionary`对象，即使其构造函数尚未完成。

### 更多带参数的构造函数

显然，你可能不想像在`Employee`类中那样在构造函数中硬编码一个值，因此你可以选择将该构造函数改为也接受一个`name`参数。请按照下面所示修改`Employee`类的构造函数：

```
Public Sub New(ByVal name As String)
MyBase.New(name)
    Debug.WriteLine("Employee constructor")
End Sub
```

当然，这只会让问题进一步加深，现在`OfficeEmployee`类的`New`方法中出现了编译错误。同样，你可以让该方法接受一个参数，以便按要求沿继承链向上传递，从而解决此问题。对`OfficeEmployee`进行如下修改：

```
Public Sub New(ByVal name As String)
    MyBase.New(name)
    Debug.WriteLine("OfficeEmployee constructor")
End Sub
```

最后，窗体中的代码不再有效。你试图创建一个`OfficeEmployee`实例，却没有传递参数值。请按下面所示更新该代码，然后就可以运行应用程序了：

```
Private Sub btnOK_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnOK.Click

    Dim person As Employee = New OfficeEmployee("Mary")

    With person
        .Name = "Fred"
    End With
```

在这里，你将一个`name`值传递给了`OfficeEmployee`的构造函数。此外，你还注释掉了直接设置`Name`属性的那行代码——这意味着构造函数中传入的值将显示在窗体中。

### Protected 作用域

你已经看到子类如何自动获得构成基类接口的所有`Public`方法和属性。`Friend`方法和属性也是如此；它们同样会被继承，并且仅对与子类处于同一项目中的其他代码可用。

`Private`方法和属性不会作为子类接口的一部分暴露出来，这意味着子类中的代码无法调用这些方法，任何使用你的对象的代码也无法调用。这些方法仅对基类自身的代码可用。这可能会让人感到困惑，因为`Private`方法中包含的实现会被继承，并被基类中的任何代码使用；只不过它们不能被任何其他代码调用，包括子类中的代码。

有时你会希望在基类中创建一些方法，这些方法可以被子类以及基类调用，但不能被这些类之外的代码调用。基本上，你需要的是一种介于`Public`和`Private`访问修饰符之间的混合体——这些方法对于继承链中的类是私有的，但可供链内创建的任何子类使用。`Protected`作用域就提供了这种功能。

`Protected`方法在这一点上与`Private`方法非常相似：它们对任何调用你的对象的代码都不可用。相反，这些方法对基类内的代码以及任何子类内的代码可用。下表列出了所有可用的作用域选项：

| 作用域 | 说明 |
|---|---|
| `Private` | 仅对你类内部的代码可用 |
| `Protected` | 仅对继承自你的类的类可用 |
| `Friend` | 仅对你的项目/组件内部的代码可用 |
| `Protected Friend` | 对继承自你的类的类（在任何项目中）以及你的项目/组件内部的代码可用。这是`Protected`和`Friend`的组合。 |
| `Public` | 对你的类外部的代码可用 |

```
Public Class Person
    Private mName As String
    Private mBirthDate As String
    Private mID As String

    Protected Property Identity() As String
        Get
            Return mID
        End Get
        Set(ByVal value As String)
            mID = value
        End Set
    End Property
```

来自 Person 的代码片段

该数据字段表示分配给某人的任意标识号或标识值。这可以是社会保险号、员工号，或任何合适的内容。

有趣的是，该值目前无法在继承链之外访问。例如，如果你尝试在窗体的代码中使用它，你会发现你的`Person`、`Employee`或`OfficeEmployee`对象上都没有`Identity`属性。

然而，现在继承链内部可以使用`Identity`属性了。`Identity`属性对`Person`类中的代码可用，就像任何其他方法一样。有趣的是，尽管`Identity`对窗体中的代码不可用，但它对`Employee`和`OfficeEmployee`类中的代码可用，因为它们都是`Person`的子类。`Employee`是`Person`的直接子类，而`OfficeEmployee`是`Person`的间接子类，因为它是`Employee`的子类。

因此，你可以增强`Employee`类，通过使用`Identity`属性来实现一个`EmployeeNumber`属性。为此，请将以下代码添加到`Employee`类中：

```
Public Property EmployeeNumber() As Integer
    Get
        Return CInt(Identity)
    End Get
    Set(ByVal value As Integer)
        Identity = CStr(value)
    End Set
End Property
```

来自 Employee 的代码片段

这个新属性为员工暴露了一个数字标识值，但它使用内部的`Identity`属性来管理该值。你可以像处理任何其他作用域的元素一样，对`Protected`元素进行重写和隐藏。

### Protected 变量

到目前为止，我们一直专注于方法和属性以及它们如何通过继承进行交互。继承，尤其是`Protected`作用域，也会影响实例变量以及你使用它们的方式。

尽管不推荐，你仍然可以在类中使用`Public`作用域声明变量。这会使该变量对你的类内部和外部的代码都直接可用，允许任何与你的对象交互的代码直接读取或更改该变量的值。

变量也可以具有`Friend`作用域，这同样允许你的类中的任何代码或项目中的任何代码直接读取或更改该值。这通常也不被推荐，因为它破坏了封装。

> 与其使用`Public`或`Friend`作用域声明变量，不如使用`Property`来暴露该值，这样你就可以应用任何业务规则，在适当的情况下控制该值的更改方式。

当然，你知道变量可以具有`Private`作用域，而且这通常是常见做法。这使变量仅对你的类中的代码可访问，它是最严格的作用域。

然而，与方法一样，你也可以在声明变量时使用`Protected`作用域。这使变量对你的类中的代码以及任何从你的类派生的类中的代码可访问——一直延伸到整个继承层次结构的末端。

有时这很有用，因为它使你能向子类提供数据以及从子类接收数据，但可以在基类的代码中对该数据进行处理。同时，向子类暴露变量通常并不理想，你应该改用具有`Protected`作用域的`Property`方法，因为它们允许你的基类对值实施任何适当的业务规则，而不是仅仅希望子类的作者只提供好的值。

### 事件与继承

到目前为止，我们已经从继承的角度讨论了方法、属性和变量——它们如何被添加、重写、重载和隐藏。在 Visual Basic 中，事件也是对象接口的一部分，它们同样会受到继承的影响。

#### 继承事件

第 2 章讨论了如何声明、引发和接收对象的事件。你可以通过在类的顶部声明事件，将这样的事件添加到`Person`类中：

```
Public Class Person
    Private mName As String
    Private mBirthDate As String
    Private mID As String

    Public Event NameChanged(ByVal newName As String)
```

来自 Person 的代码片段

然后，你可以在类中每当该人的姓名发生变化时引发此事件：
