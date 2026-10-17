
如果在应用程序运行时命令行上有单词 `"nodisplay"`，则会使用新的事件处理程序版本；否则，你继续使用消息框处理器。

`AddHandler` 的对应方法是 `RemoveHandler`。`RemoveHandler` 用于将事件处理程序从事件中分离。一个有用的例子是当你想将 `mPerson` 变量设置为 `Nothing` 或新的 `Person` 对象时。现有的 `Person` 对象已将其事件附加到处理程序，在你放弃对该对象的引用之前，必须释放这些引用：

```
If Microsoft.VisualBasic.Command = "nodisplay" Then
    RemoveHandler mPerson.Walked, AddressOf LogOnWalk
Else
    RemoveHandler mPerson.Walked, AddressOf OnWalk
End If
mPerson = New Person
```

Form1 中的代码片段

如果你不分离事件处理程序，旧的 `Person` 对象仍会保留在内存中，因为每个事件处理程序仍保持对该对象的引用，即使 `mPerson` 不再指向该对象。

这说明了为什么在大多数情况下 `WithEvents` 关键字和 `Handles` 子句更可取。`AddHandler` 和 `RemoveHandler` 必须成对使用；未能这样做可能会导致应用程序内存泄漏，而 `WithEvents` 关键字会自动为你处理这些细节。

### 构造函数方法

在 Visual Basic 中，类可以实现一个特殊的方法，该方法在对象创建时始终被调用。此方法称为 *构造函数*，并且始终命名为 `New`。

构造函数方法非常适合此类初始化代码，因为它在任何其他方法被调用之前始终运行，并且对一个对象只运行一次。当然，你可以根据类创建许多对象，并且构造函数方法将为每个创建的对象运行。

你也可以在自己的类中实现构造函数，使用它根据需要初始化对象。这就像实现一个名为 `New` 的 `Public` 方法一样简单。向 `Person` 类添加以下代码：

```
Public Sub New()
    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
End Sub
```

> Person 中的代码片段

在此示例中，你只是使用构造函数方法为创建的任何新 `Person` 对象初始化家庭和工作电话号码。

### 参数化构造函数

你也可以使用构造函数使参数在对象创建时传递给对象。这只需向 `New` 方法添加参数即可。例如，你可以按如下方式更改 `Person` 类：

```
Public Sub New(ByVal name As String, ByVal birthDate As Date)
    mName = name
    mBirthDate = birthDate
    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
End Sub
```

> Person 中的代码片段

通过此更改，每当创建 `Person` 对象时，你都会获得姓名和出生日期的值。然而，这改变了你创建新 `Person` 对象的方式。以前你有类似

```
Dim myPerson As New Person()
```

的代码，现在你将有类似

```
Dim myPerson As New Person("Bill", "1/1/1970")
```

的代码。

事实上，由于构造函数期望这些值，它们是强制性的——任何需要创建 `Person` 类实例的代码都必须提供这些值。幸运的是，有可选参数和方法重载等替代方案（它使你能够创建同一方法的多个版本，每个版本接受不同的参数列表）。这些主题将在本章后面讨论。

### 终止和清理

在 .NET 环境中，当对象不再有引用时，对象将被销毁，其占用的内存和资源将被回收。如本章前面所述，当你使用对象时，变量实际上保存对对象本身的引用或指针。如果你有类似

```
Dim myPerson As New Person()
```

现在你可以继续探讨一些更复杂的主题，以及之前所讨论内容的变体。首先，你将了解可以在类中实现的方法的一些高级变体，包括对事件背后底层技术的探索。

### 方法重载

方法通常接受参数值。例如，`Person` 对象的 `Walk` 方法接受一个 `Integer` 参数：

```vb
Public Sub Walk(ByVal distance As Integer)
    mTotalDistance += distance
    RaiseEvent Walked(distance)
End Sub
```

> 来自 Person 的代码片段

有时并不需要该参数。为了解决这个问题，你可以使用 `Optional` 关键字使该参数成为可选参数：

```vb
Public Sub Walk(Optional ByVal distance As Integer = 0)
    mTotalDistance += distance
    RaiseEvent Walked(distance)
End Sub
```

> 来自 Person 的代码片段

然而，这并不能为你提供很大的灵活性，因为可选参数必须始终位于参数列表的最后。此外，这仅仅允许你传入或不传入该参数。假设你想做一些更奇特的事情，比如允许不同的数据类型，甚至是完全不同的参数列表。

方法重载恰好提供了这些能力。通过重载方法，你可以创建多个同名方法，每个方法接受不同的参数集，或不同数据类型的参数。

作为一个简单的示例，你不必在 `Walk` 方法中使用 `Optional` 关键字，而是可以使用重载。你保留原始的 `Walk` 方法，但同时添加另一个接受不同参数列表的 `Walk` 方法。将 `Person` 类中的代码改回如下：

```vb
Public Sub Walk(ByVal distance As Integer)
    mTotalDistance += distance
    RaiseEvent Walked(distance)
End Sub
```

> 来自 Person 的代码片段

现在创建另一个同名但参数列表不同的方法（在本例中没有参数）。在不删除或修改现有 `Walk` 方法的情况下，将这段代码添加到类中：

```vb
Public Sub Walk()
    RaiseEvent Walked(0)
End Sub
```

> 来自 Person 的代码片段

此时，你有两个 `Walk` 方法。区分它们的唯一方法是各自接受的参数列表：第一个需要一个 `Integer` 参数，第二个没有参数。

> 还有一个 `Overloads` 关键字。对于这里描述的简单方法重载，并不需要这个关键字，但在结合重载与继承时则需要它，这将在第 3 章中讨论。

你可以带参数或不带参数地调用 `Walk` 方法，如下面的示例所示：

```vb
objPerson.Walk(42)
objPerson.Walk()
```

只要每个 `Walk` 方法都有不同的方法签名，你就可以在类中拥有任意数量的 `Walk` 方法。

#### 方法签名

所有方法都有一个签名，签名由方法名称及其参数的数据类型定义：

```vb
Public Function CalculateValue() As Integer

End Function
```

在这个示例中，签名是 `f()`。字母 *f* 通常用于表示方法或函数。这里使用它是恰当的，因为你并不关心函数的名称；只有其参数列表才是重要的。

如果你向方法添加一个参数，则签名将被视为已更改。例如，你可以将方法改为接受一个 `Double`：

```vb
Public Function CalculateValue(ByVal value As Double) As Integer
```

在这种情况下，方法的签名是 `f(Double)`。

请注意，在 Visual Basic 中，返回值不是签名的一部分。你不能仅通过改变函数例程的返回值数据类型来重载它。要利用重载，必须是参数列表中的数据类型发生变化。

还要注意，参数的名称完全无关紧要；只有数据类型才是重要的。这意味着以下方法具有相同的签名：

```vb
Public Sub DoWork(ByVal x As Integer, ByVal y As Integer)

Public Sub DoWork(ByVal value1 As Integer, ByVal value2 As Integer)
```

在这两种情况下，签名都是 `f(Integer, Integer)`。

参数的数据类型定义了方法签名，但参数是通过 `ByVal` 还是 `ByRef` 传递则不影响签名。将参数从 `ByVal` 改为 `ByRef` 不会改变方法签名。

### 结合重载与可选参数

重载比使用可选参数更为灵活，但可选参数的优势在于它们可用于提供默认值，并使参数成为可选。

你可以结合这两个概念：重载一个方法，并让其中一个或多个方法利用可选参数。显然，如果过度使用，这种事情会变得非常令人困惑，因为你同时使用了两种类型的“重载”。

`Optional` 关键字会使单个方法有效地拥有两个签名。这意味着，将方法声明为

```vb
Public Sub DoWork(ByVal x As Integer, Optional ByVal y As Integer = 0)
```

就同时有了两个签名：`f(Integer, Integer)` 和 `f(Integer)`。

因此，当你将重载与可选参数一起使用时，其他重载方法不能匹配这两个签名中的任何一个。然而，只要其他方法不匹配任何一个签名，你就可以像前面讨论的那样使用重载。例如，你可以实现具有以下签名的方法

```vb
Public Sub DoWork(ByVal x As Integer, Optional ByVal y As Integer = 0)
```

和

```vb
Public Sub DoWork(ByVal data As String)
```

因为没有相互冲突的方法签名。事实上，使用这两个方法，你实际上创建了三个签名：

- `f(Integer, Integer)`

- `f(Integer)`

- `f(String)`

Visual Studio IDE 中内置的 IntelliSense 将指示你有两个重载方法，其中一个具有可选参数。这与创建三个不同的重载方法来匹配这三个签名不同，在后一种情况下，IntelliSense 会列出该方法的三个变体，你可以从中选择。

### 重载构造函数方法

在许多情况下，你可能希望构造函数接受用于初始化新对象的参数值，但也希望能够在未提供这些值的情况下创建对象。这可以通过方法重载（稍后讨论）或使用可选参数来实现。

构造函数方法上的可选参数遵循与任何其他 `Sub` 例程的可选参数相同的规则：它们必须是参数列表中的最后几个参数，并且你必须为可选参数提供默认值。

例如，你可以像下面这样修改 `Person` 类：

```vb
Public Sub New(Optional ByVal name As String = "", _
    Optional ByVal birthDate As Date = #1/1/1900#)
    mName = name
    mBirthDate = birthDate

    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
End Sub
```

> 来自 Person 的代码片段

前面的示例将 `Name` 和 `BirthDate` 参数都改为可选，并为两者提供了默认值。现在，你可以选择是否提供参数值来创建新的 `Person` 对象：

```vb
Dim myPerson As New Person("Bill", "1/1/1970")
```

或

```vb
Dim myPerson As New Person()
```

如果你不提供参数值，则将使用空字符串和 `1/1/1900` 的默认值，并且代码将正常工作。

### 重载构造函数

你可以将构造函数方法与方法重载的概念相结合，以允许以不同的方式创建类的实例。这是一种非常强大的组合，因为它为对象创建提供了极大的灵活性。

你已经探讨了如何在构造函数中使用可选参数。现在，让我们修改 `Person` 类中的实现，改用重载。按如下方式更改现有的 `New` 方法：

```vb
Public Sub New(ByVal name As String, ByVal birthDate As Date)
    mName = name
    mBirthDate = birthDate
    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
End Sub
```

> 来自 Person 的代码片段

With this change, you require the two parameter values to be supplied. Now add that second implementation, as shown here:

```
Public Sub New()
    Phone("home") = "555-1234"
    Phone("work") = "555-5678"
End Sub
```

This second implementation accepts no parameters, meaning you can now create `Person` objects in two different ways — either with no parameters or by passing the name and birth date:

```
Dim myPerson As New Person()
```

or

```
Dim myPerson As New Person("Fred", "1/11/60")
```

This type of capability is very powerful because it enables you to define the various ways in which applications can create objects. In fact, the Visual Studio IDE considers this, so when you are typing the code to create an object, the IntelliSense tooltip displays the overloaded variations on the method, providing a level of automatic documentation for the class.

### Shared Methods, Variables, and Events

So far, all of the methods you have built or used have been instance methods, methods that require you to have an actual instance of the class before they can be called. These methods have used instance variables or member variables to do their work, which means that they have been working with a set of data that is unique to each individual object.

With Visual Basic, you can create variables and methods that belong to the class, rather than to any specific object. In other words, these variables and methods belong to all objects of a given class and are shared across all the instances of the class.

You can use the `Shared` keyword to indicate which variables and methods belong to the class, rather than to specific objects. For instance, you may be interested in knowing the total number of `Person` objects created as the application is running — kind of a statistical counter.

#### Shared Variables

Because regular variables are unique to each individual `Person` object, they do not enable you to easily track the total number of `Person` objects ever created. However, if you had a variable that had a common value across all instances of the `Person` class, you could use that as a counter. Add the following variable declaration to the `Person` class:

```
Public Class Person
    Implements IDisposable
    Private Shared mCounter As Integer
```
