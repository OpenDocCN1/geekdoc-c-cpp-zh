
你已经有一个返回值的 方法。与其重新实现该方法，不如将其链接到新的 `GetValues` 方法会更好。你可以轻松做到这一点，因为 `Implements` 子句允许你提供一个由逗号分隔的方法名称列表：

```
Private Function Value(ByVal index As Integer) As String _
    Implements IPrintableObject.Value, IValues.GetValue
```

```
Select Case Index
    Case 0
        Return CStr(EmployeeNumber)
    Case 1
        Return CStr(Age)
    Case Else
        Return Format(HireDate, "Short date")
End Select

End Function
```

`Employee` 中的代码片段

这与第 2 章中介绍的 `Handles` 关键字的用法非常相似。类中的单个方法，无论作用域或名称如何，都可以用于实现其他接口定义的任意数量的方法，只要参数和返回值的 数据类型都匹配即可。

### 组合接口和继承

你可以同时组合二级接口的实现和继承。当你继承自实现了接口的类时，你的新子类会自动获得基类的接口和实现。如果指定基类方法是可重写的，那么子类可以重写这些方法。这不仅重写了你原生接口的基类实现，还重写了接口的实现。例如，你可以按如下方式声明接口中的 `Value` 方法：

```
Public Overridable Function Value(ByVal index As Integer) As String _
    Implements IPrintableObject.Value, IValues.GetValue
```

现在它是 `Public`，因此可在你的原生接口上使用，并且是 `IPrintableObject` 和 `IValues` 接口的一部分。这意味着你可以在客户端代码中以三种方式访问该属性：

```
Dim emp As New Employee()
Dim printable As IPrintableObject = emp
Dim values As IValues = emp

Debug.WriteLine(emp.Value(0))
Debug.WriteLine(printable.Value(0))
Debug.WriteLine(values.GetValue(0))
```

请注意，你现在也在声明中使用了 `Overrides` 关键字。这意味着 `Employee` 的子类，例如 `OfficeEmployee`，可以重写 `Value` 方法。无论你直接调用对象还是通过接口调用，被重写的方法都将被调用。

在基类中组合接口的实现与可重写方法可以提供非常灵活的对象设计。

### 抽象

抽象是你可以在不考虑具有这些属性或行为的特定对象的情況下思考特定属性或行为的过程。抽象仅仅是语言创建“黑盒”代码的能力，将一个概念并在程序中创建该概念的抽象表示。

例如，`Customer` 对象是现实世界客户的抽象表示。`DataSet` 对象是一组数据的抽象表示。

抽象使你能够认识到事物如何相似并忽略差异，以一般术语而非具体细节思考。`TextBox` 控件是一个抽象，因为你可以将其放置在窗体上，然后通过设置属性来根据需要对其进行定制。Visual Basic 使你能够使用类定义抽象。

任何使开发人员能够创建可实例化对象的类的语言都满足此标准，Visual Basic 也不例外。你可以轻松创建一个类来表示客户，本质上提供了一个抽象。然后你可以创建该类的实例，其中每个对象都可以有自己的属性，表示特定的客户。

在 Visual Basic 中，你通过使用 `Class` 关键字创建类来实现抽象。要亲眼看到这一点，请打开 Visual Studio 并创建一个名为“`OOExample`”的新 Visual Basic Windows 窗体应用程序项目。项目打开后，使用 `Project ⇨ Add Class` 菜单选项向项目添加一个新类。将新类命名为 `Customer.vb`，并添加一些代码以使该类在抽象意义上代表现实世界的客户：

```
Public Class Customer
    Private mID As Guid = Guid.NewGuid
    Private mName As String
    Private mPhone As String

    Public Property ID() As Guid
        Get
            Return mID
        End Get
```

完成向导。如果你正在使用设计视图，`Customer` 类将显示为可用的数据源，如图 3-12 所示。

在窗口中单击 `Customer`。`Customer` 的显示应该会变为一个组合框。打开组合框，将选择从 `DataGridView` 改为 `Details`。这样，你就可以在窗体上获得对象的详细信息视图。打开 `Form1` 的设计器，将 `Customer` 类从“数据源”窗口拖到窗体上。结果应类似于图 3-13 所示的对话框。

![](img/d99870e80390742f93963da7be0b2e61_206_0.png)

### 图 3-12

![](img/d99870e80390742f93963da7be0b2e61_206_1.png)

### 图 3-13

现在你只需添加代码来创建 `Customer` 类的一个实例，作为窗体的数据源。双击窗体以打开其代码窗口，并添加以下代码：

```
Public Class Form1

    Private Sub Form1_Load(ByVal sender As System.Object, _
        ByVal e As System.EventArgs) Handles MyBase.Load

        Me.CustomerBindingSource.DataSource = New Customer()

    End Sub

End Class
```

#### 来自 Form1 的代码片段

你正在使用 Windows Forms 的数据绑定能力，将数据绑定到对象上的属性。稍后你会学到更多有关数据绑定的知识。目前，只要知道窗体上的控件会自动绑定到对象上的属性就够了。

现在你拥有一个简单的用户界面（UI），它既能显示 `Customer` 对象中的数据，也能更新这些数据，同时该对象为 UI 开发人员提供了客户的抽象表示。运行应用程序时，你会看到如图 3-14 所示的显示界面。

在这里，你显示了预先生成的 ID 值，并直接在窗体中输入了 `Name` 和 `Phone` 的值。

![](img/d99870e80390742f93963da7be0b2e61_206_2.png)

### 图 3-14

### 封装

也许面向对象概念中最重要的就是封装。封装的思想是：对象应该将其接口与实现完全分离。一个对象的所有数据和实现代码都应完全隐藏在其接口之后。这就是将对象视为黑盒的概念。

其思想是，你可以创建一个接口（通过在类中创建公共方法），只要该接口保持一致，应用程序就可以与你的对象交互。即使你完全重写某个方法中的代码，这一点也依然成立。接口独立于实现。

封装使你能够隐藏类的内部实现细节。例如，你用来查找素数的算法可能是专有的。你可以向最终用户公开一个简单的 API，但通过将算法封装在类中来隐藏算法中使用的所有逻辑。

这意味着，一个对象应该完全包含它所需的任何数据，并且应该包含操作这些数据所需的全部代码。程序应该通过接口与对象交互，使用对象的属性和方法。客户端代码绝不应直接操作对象拥有的数据。

> 程序通过向对象发送消息来与对象交互，指明它们希望调用哪个方法或属性。这些消息由其他对象或外部来源（如用户）生成。对象通过方法或属性对这些消息作出反应。

Visual Basic 类完全隐藏其内部数据和代码，并通过属性和方法与外部世界提供一个完善的接口。让我们看一个示例。选择“项目”➜“添加类”，将以下类添加到项目中；该代码定义了其原生接口：

```
Public Class Encapsulation

    Public Function DistanceTo(ByVal x As Single, ByVal y As Single) As Single

    End Function

    Public Property CurrentX() As Single
        Get

        End Get
        Set(ByVal value As Single)

        End Set
    End Property

    Public Property CurrentY() As Single
        Get

        End Get
        Set(ByVal value As Single)

        End Set
    End Property

End Class
```

![](img/d99870e80390742f93963da7be0b2e61_207_0.png)

这为类创建了一个接口。此时，你可以编写客户端代码与类交互，因为从客户端角度来看，你关心的只是接口。打开 `Form1` 的设计器，在窗体上添加一个按钮，然后在按钮的后置代码中编写以下代码：

```
Private Sub btnEncapsulation_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnEncapsulation.Click

    Dim obj As New Encapsulation
    MsgBox(obj.DistanceTo(10, 10))

End Sub
```

即使在 `Encapsulation` 类中没有实际代码，你仍然可以编写代码来使用该类，因为接口已经定义好了。

这是一个强大的想法。这意味着你可以快速创建类接口，让其他开发人员可以针对这些接口创建 UI 或应用程序的其他部分，而你仍在该接口背后创建实现。

从这里开始，在实现类方面，你几乎可以做任何你想做的事情。例如，要使用这些值来计算直线距离，请用以下代码覆盖之前的代码：

```
Imports System.Math

Public Class Encapsulation
    Private mX As Single
    Private mY As Single

    Public Function DistanceTo(ByVal x As Single, ByVal y As Single) As Single
        Return CSng(Sqrt((x - mX)^ 2 ^ (y - mY) ? 2))
    End Function

    Public Property CurrentX() As Single
        Get
            Return mX
        End Get
        Set(ByVal value As Single)
            mX = value
        End Set
    End Property

    Public Property CurrentY() As Single
        Get
            Return mY
        End Get
        Set(ByVal value As Single)
            mY = value
        End Set
    End Property
End Class
```

现在，当你运行应用程序并单击按钮时，会得到一个有意义的值。更棒的是，封装使你能够在不改变接口的情况下更改实现。例如，你可以将距离计算改为找出两点之间的距离（假设不允许斜向移动）：

```
Public Function DistanceTo(ByVal x As Single, ByVal y As Single) As Single
    Return Abs(x - mX) + Abs(y - mY)
End Function
```

这会导致程序运行时显示不同的值。你没有改变类的接口，因此正在运行的客户端程序完全不知道你已经从一种实现切换到了另一种实现。你在不改变客户端代码的情况下实现了行为的完全改变。这就是封装的本质。

当然，如果你对对象进行这样的更改，用户可能会遇到问题。如果应用程序开发时预期的是第一组行为，然后你更改为了第二组，可能会产生一些有趣的副作用。关键是客户端程序会继续运行，即使结果与你刚开始时完全不同。

### 多态

多态通常被认为与继承（将在后面讨论）直接相关。实际上，它在很大程度上是独立的。多态意味着你可以有两个具有不同实现或代码的类，但它们有一组公共的方法、属性或事件。然后你可以编写一个程序，该程序在该接口上操作，而不关心它在运行时操作的是哪种类型的对象。

#### 方法签名

要正确理解多态，你需要探索方法签名（有时也称为原型）的概念。所有方法都有签名，签名由方法的名称及其参数的数据类型定义。你可能会有这样的代码：

```
Public Function CalculateValue() As Integer

End Sub
```

在本例中，签名如下：

```
f()
```

如果向方法添加一个参数，签名将会改变。例如，你可以将方法改为接受一个 `Double`：

```
Public Function CalculateValue(ByVal value As Double) As Integer
```

那么，该方法的签名如下：

```
f(Double)
```

多态只是说，你应该能够编写在对象上调用方法的客户端代码，只要该对象提供的方法具备你所期望的方法签名，那么该对象是从哪个类创建的就无关紧要了。接下来的章节将介绍 Visual Basic 中多态的一些示例。

#### 实现多态

你可以使用多种技术来实现多态行为：

- 后期绑定

- 多个接口

- 反射

- 继承

后期绑定实际上使你可以实现“纯”多态，尽管要以性能和编程便利性为代价。通过多个接口和继承，你也可以实现多态。

with much better performance and ease of programming. Reflection enables you to use either late binding or multiple interfaces, but against objects created in a very dynamic way, even going so far as to dynamically load a DLL into your application at runtime so that you can use its classes. The following sections walk through each of these options to see how they are implemented and to explore their pros and cons.

### Polymorphism through Late Binding

Typically, when you interact with objects in Visual Basic, you are interacting with them through strongly typed variables. For example, in `Form1` you interacted with the `Encapsulation` object with the following code:

```
Private Sub btnEncapsulation_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnEncapsulation.Click

    Dim obj As New Encapsulation
    MsgBox(obj.DistanceTo(10, 10))

End Sub
```

Code snippet from Form1

The `obj` variable is declared using a specific type (`Encapsulation`) — meaning that it is strongly typed or early bound.

You can also interact with objects that are late bound. Late binding means that your object variable has no specific data type, but rather is of type `Object`. To use late binding, you need to use the `Option Strict Off` directive at the top of your code file (or in the project's properties). This tells the Visual Basic compiler that you want to use late binding, so it will allow you to do this type of polymorphism. Add the following to the top of the `Form1` code:

```
Option Strict Off
```
