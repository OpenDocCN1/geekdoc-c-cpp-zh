
如果一个类包含任何标记为 `MustOverride` 的方法，则该类本身也必须使用 `MustInherit` 关键字声明，否则会出现语法错误。

### `Public MustInherit Class Person`

这很有道理。如果要求在子类中重写方法，那么可以推断你的类不能直接实例化；它必须被子类化才能发挥作用。

让我们通过在 `Person` 中添加一个 `LifeExpectancy` 方法来看看这是如何工作的，该方法没有实现并且必须由子类重写：

```
Public MustOverride Function LifeExpectancy() As Integer
```

请注意，该方法没有 `End Function` 或任何其他相关代码。使用 `MustOverride` 时，你不能在类中为该方法提供任何实现。这种方法称为抽象方法或纯虚函数，因为它只定义接口，而没有实现。

以这种方式声明的方法必须在继承自基类的任何子类中被重写。如果你没有重写其中一个方法，子类将产生语法错误并且无法编译。你需要修改 `Employee` 类以提供此方法的实现：

```
Public Overrides Function LifeExpectancy() As Integer
    Return 90
End Function
```

此时你的应用程序可以编译和运行，因为你现在在 `Employee` 中重写了 `LifeExpectancy` 方法，因此满足了所需条件。

### 抽象基类

你可以将这两个概念结合起来，同时使用 `MustInherit` 和 `MustOverride`，创建所谓的抽象基类，有时也称为虚类。这是一个不提供实现、仅提供接口定义的类，子类可以基于此创建，如以下示例所示：

```
Public MustInherit Class AbstractBaseClass
    Public MustOverride Sub DoSomething()
    Public MustOverride Sub DoOtherStuff()
End Class
```

在创建框架或系统的高级概念元素时，此技术非常有用。任何继承 `AbstractBaseClass` 的类都必须实现 `DoSomething` 和 `DoOtherStuff`；否则将导致语法错误。

你还可以使用 `Event` 关键字将事件声明为接口的一部分：

```
Public Event AnEvent()
```

最后，你可以包含实际的变量或属性作为接口的一部分：

```
Public AnInteger As Integer
```

强烈不建议这样做，因为它直接将内部变量暴露给类外部的代码使用。由于变量可以直接被其他代码访问，你放弃了对值可能如何更改或代码可能如何被访问的任何控制。

与其将任何变量设为 `Public`，不如最好使用 `Property` 方法来公开该值。这样，你可以实现代码以确保内部变量仅设置为有效值，并且只有基于应用程序逻辑的适当代码才能访问该值。

### 使用原生接口

最终，任何类的原生（或主要）接口都是通过查看所有声明的范围不为 `Private` 的方法、属性、事件和变量来定义的。这包括从基类继承的任何方法、属性、事件或变量。

你习惯于与大多数对象的默认接口交互，所以这应该看起来很直接。考虑这个简单的类：

```
Public Class TheClass
    Public Sub DoSomething()

    End Sub

    Public Sub DoSomethingElse()

    End Sub
End Class
```

> Code snippet from `TheClass`

这定义了一个类，并通过扩展定义了基于此类实例化的任何对象所暴露的原生接口。原生接口定义了两个方法：`DoSomething` 和 `DoSomethingElse`。要使用这些方法，只需调用它们即可：

```
Dim myObject As New TheClass()

myObject.DoSomething()

myObject.DoSomethingElse()
```

> Code snippet from `Form1`

这就是你在第 2 章以及本章迄今为止所做的事情。然而，让我们来看看创建和使用次要接口，因为它们有点不同。

### 次要接口

有时让对象拥有不止一个接口是有帮助的，从而使你能够以不同的方式与对象交互。继承使你能够创建基类的特化子类。例如，你的 `Employee` 是一个 `Person`。在本节中，我们将引用本章前面创建的 `InheritanceAndInterfaces` 项目。

然而，有时你有一组对象，它们不是同一事物，但你希望能够将它们视为同一事物。你希望所有这些对象都表现得像同一事物，即使它们都不同。

例如，你可能在应用程序中有一系列不同的对象：产品、客户、发票等等。其中每一个都有适合各自对象的默认接口——并且每一个都是不同的类——因此这些类之间并没有自然的继承关系。同时，你可能需要为每种类型的对象生成打印文档，因此你希望让它们都作为可打印对象来表现。

> 本章将在后面更详细地讨论 is-a 和 act-as 关系。

要实现这一点，你可以定义一个通用接口，使其能够生成此类打印文档。你可以将其命名为 `IPrintableObject`。

> 按惯例，此类接口通常以大写字母“I”作为前缀，以表示它是一个正式接口。

你的每个应用程序对象都可以选择实现 `IPrintableObject` 接口。每个实现此接口的对象都必须包含代码以提供接口的实际实现，这与继承不同，在继承中基类的代码会被自动重用。

通过实现此通用接口，你可以编写一个例程，接受任何实现 `IPrintableObject` 接口的对象，然后打印它——同时完全不知道对象的“真实”数据类型或其原生接口可能公开的方法。在学习如何以这种方式使用接口之前，让我们先逐步了解实际定义接口的过程。

### 定义接口

你使用 `Interface` 关键字定义正式接口。这可以在项目的任何代码模块中完成，但放置此类定义的一个好位置是在标准模块中。接口定义了一组必须由选择实现接口的任何类公开的方法（`Sub`、`Function` 或 `Property`）和事件。

使用 `Project ▸ Add Module` 向项目添加一个模块，并将其命名为 `Interfaces.vb`。然后，在 `Module` 代码块本身之外，将以下代码添加到模块中：

```
Public Interface IPrintableObject

End Interface

Module Interfaces

End Module
```

来自 `Interfaces` 的代码片段

一个代码模块可以包含多个接口定义，这些定义必须存在于任何其他代码块之外。因此，它们不会放在 `Class` 或 `Module` 块内；它们与这些结构处于同一级别。

接口必须使用 `Public` 或 `Friend` 范围声明。声明 `Private` 或 `Protected` 接口会导致语法错误。在 `Interface` 代码块内，你可以定义构成特定接口的方法、属性和事件。由于接口的范围由 `Interface` 声明本身定义，因此你不能为单个方法和事件指定范围；它们都与接口本身具有相同的范围。

例如，添加以下代码：

```
Public Interface IPrintableObject
    Function Label(ByVal index As Integer) As String
    Function Value(ByVal index As Integer) As String
    ReadOnly Property Count() As Integer
End Interface
```

![](img/d99870e80390742f93963da7be0b2e61_200_0.png)

这定义了一个新的数据类型，有点像创建类或结构，你可以在声明变量时使用它。例如，你现在可以声明一个类型为 `IPrintableObject` 的变量：

```
Private printable As IPrintableObject
```

你也可以让你的类实现此接口，这要求每个类为接口上定义的三个方法提供实现代码。

在类中实现接口之前，让我们看看如何使用接口编写一个通用例程，可以打印任何实现 `IPrintableObject` 的对象。

### 使用接口

接口定义了对象如果选择支持接口则必须实现的方法和事件（包括参数和数据类型）。这意味着，仅凭接口定义，你就可以轻松编写能够与任何实现该接口的对象交互的代码，即使你不知道这些对象的原生数据类型会是什么。

为了了解如何编写此类代码，让我们创建一个简单的例程，在你的窗体中将数据显示到 IDE 的输出窗口中，该例程可用于任何实现 `IPrintableObject` 的对象。打开你的窗体代码窗口并添加以下例程：

```
Public Sub PrintObject(obj As IPrintableObject)
    Dim index As Integer

    For index = 0 To obj.Count
        Debug.Write(obj.Label(index) & ": ")
        Debug.WriteLine(obj.Value(index))
    Next
End Sub
```

![](img/d99870e80390742f93963da7be0b2e61_200_1.png)

请注意，你正在接受一个类型为 `IPrintableObject` 的参数。这就是二级接口的使用方式，即将一种类型的对象视为实际上是接口类型。只要传递给此例程的对象实现了 `IPrintableObject` 接口，你的代码就能正常工作。

在 `PrintObject` 例程中，你假设对象将作为 `IPrintableObject` 接口的一部分实现三个元素——`Count`、`Label` 和 `Value`。二级接口可以包含方法、属性和事件，就像默认接口一样，但接口本身是使用一些特殊语法定义和实现的。

现在你已经有一个通用的打印例程，你需要一种调用它的方法。打开 `Form1` 的设计器，添加一个按钮，并将其命名为 `btnPrint`。双击该按钮并在其后放置以下代码：

```
Private Sub btnPrint_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnPrint.Click

    Dim obj As New Employee("Andy")

    obj.EmployeeNumber = 123

obj.BirthDate = #1/1/1980#
obj.HireDate = #1/1/1996#

PrintObject(obj)
End Sub
```

![](img/d99870e80390742f93963da7be0b2e61_201_0.png)

此代码只是初始化一个 `Employee` 对象并调用 `PrintObject` 例程。当然，此代码会产生运行时异常，因为 `PrintObject` 期望一个实现 `IPrintableObject` 的参数，而 `Employee` 并未实现此类接口。让我们继续在 `Employee` 中实现该接口，以便你了解其工作原理。

### 实现接口

任何类（抽象基类除外）都可以通过使用 `Implements` 关键字来实现接口。例如，你可以通过添加以下行在 `Employee` 中实现 `IPrintableObject` 接口：

```
Public Class Employee
    Inherits Person
    Implements IPrintableObject
```

这会导致作为 `Employee` 实例创建的任何对象都公开该接口。添加此行代码并按 Enter 键会触发 IDE 在你的类中为接口添加骨架方法。你所需要做的就是为这些方法提供实现（编写代码）。

> 要实现接口，你必须实现该接口定义的所有方法和属性。

在实际实现接口之前，让我们先创建一个数组来包含数据字段的标签，以便你可以通过 `IPrintableObject` 接口返回它们。将以下代码添加到 `Employee` 类中：

```
Public Class Employee
    Inherits Person
    Implements IPrintableObject
    Private mLabels() As String = {"ID", "Age", "HireDate"}
    Private mHireDate As Date
    Private mSalary As Double
```

![](img/d99870e80390742f93963da7be0b2e61_201_1.png)

要实现接口，你需要创建具有与接口中定义的参数和返回数据类型相同的方法和属性。每个方法或属性的实际名称并不重要，因为你正在使用 `Implements` 关键字将内部方法名称链接到接口定义的外部方法名称。只要方法签名匹配，一切就绪。

这同样适用于作用域。虽然接口及其方法和属性是公开可用的，但你不必将实际的方法和属性声明为 `Public`。在许多情况下，你可以将其实现为 `Private`，这样它们就不会成为原生接口的一部分，而仅通过二级接口公开。

然而，如果你确实有一个具有方法签名的 `Public` 方法，你可以使用它来实现接口中的方法。这会产生一个有趣的副作用，即该方法同时为对象原生接口上的一个方法和二级接口上的一个方法提供实现。

在这种情况下，你将使用一个 `Private` 方法，因此它仅为 `IPrintableObject` 接口提供实现。通过向 `Employee` 添加以下代码来实现 `Label` 方法：

```
Private Function Label(ByVal index As Integer) As String _
    Implements IPrintableObject.Label

    Return mLabels(index)
End Function
```

这只是一个普通的 `Private` 方法，它从预先初始化的数组中返回一个 `String` 值。有趣的部分是方法声明上的 `Implements` 子句：

```
Private Function Label(ByVal index As Integer) As String _
    Implements IPrintableObject.Label
```

通过这种方式使用 `Implements` 关键字，你表明这个特定方法是 `IPrintableObject` 接口上 `Label` 方法的实现。私有方法的实际名称可以是任何名称。正是 `Implements` 子句的使用使得这一切得以工作。唯一的要求是参数数据类型和返回值数据类型必须与 `IPrintableObject` 接口方法定义的类型相匹配。

这与使用 `Handles` 子句来指示哪个方法应该处理事件非常相似。事实上，与 `Handles` 子句一样，`Implements` 子句允许你提供一个由逗号分隔的接口方法列表，由这一个函数来实现。

然后你可以继续通过向 `Employee` 添加以下代码来实现 `IPrintableObject` 接口定义的另外两个元素：

```
Private Function Value(ByVal index As Integer) As String _
    Implements IPrintableObject.Value

    Select Case index
        Case 0
            Return CStr(EmployeeNumber)
        Case 1
            Return CStr(Age)
        Case Else
            Return Format(HireDate, "Short date")
    End Select
End Function

Private ReadOnly Property Count() As Integer _
    Implements IPrintableObject.Count
    Get
        Return UBound(mLabels)
    End Get
End Property
```

现在你可以运行此应用程序并单击按钮。IDE 中的输出窗口将显示你的结果，显示适当的 ID、年龄和雇佣日期值。

任何对象都可以在 `IPrintableObject` 接口后面创建类似的实现，而你在窗体中的 `PrintObject` 过程将继续工作，而不管对象本身的原生数据类型如何。

### 重用通用实现

二级接口保证所有实现给定接口的对象都具有完全相同的方法和事件，包括相同的参数。

`Implements` 子句将你的实际实现链接到接口上的特定方法。例如，你的 `Value` 方法使用以下子句链接到 `IPrintableObject.Value`：

```
Private Function Value(ByVal index As Integer) As String _
    Implements IPrintableObject.Value
```

有时，你的方法可能能够作为一个或多个方法的实现，无论是在同一接口上还是在不同接口上。

将以下接口定义添加到 `Interfaces.vb`：

```
Public Interface IValues
    Function GetValue(ByVal index As Integer) As String
End Interface
```

此接口仅定义一个方法 `GetValue`。请注意，它定义了一个 `Integer` 参数和 `String` 返回类型，与 `IPrintableObject` 中的 `Value` 方法相同。即使方法名称和参数变量名称不匹配，重要的是参数和返回值的数据类型相匹配。

现在打开 `Employee` 的代码窗口。你将使其除了实现 `IPrintableObject` 接口外，还实现这个新接口：

```
Public Class Employee
    Inherits Person
    Implements IPrintableObject
    Implements IValues
```

`Employee` 中的代码片段
