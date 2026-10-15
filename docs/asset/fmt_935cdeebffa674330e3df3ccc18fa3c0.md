
这表明`Walk`是一个 public 方法，因此可供类外部的代码甚至当前项目外部的代码使用。任何引用该程序集的应用程序都可以使用此方法。作为 public 方法，它成为对象接口的一部分。

或者，你也可以对方法访问进行一定限制：

```
Friend Sub Walk()
```

通过使用`Friend`关键字声明方法，你表示它应仅对项目内部的代码成为对象接口的一部分；任何使用该程序集的其他应用程序或项目都将无法调用`Walk`方法。

`Private`关键字表示方法仅对你特定类内的代码可用：

```
Private Function Age() As Integer
```

`Private`方法非常有助于在每个类内部组织复杂的代码。有时这些方法包含非常冗长和复杂的代码。为了使代码更易理解，你可能会选择将其拆分为几个较小的例程，让主方法按正确顺序调用这些例程。此外，你可以在类内的多个位置使用这些例程，因此通过将其设为独立方法，可以实现代码重用。这些子例程绝不应被对象外部的代码调用，因此你将其设为`Private`。

### 方法参数

你经常希望在调用方法时向其传递信息。此信息通过参数提供给方法。例如，在`Person`类中，你可能希望`Walk`方法跟踪人随时间行走的距离。在这种情况下，`Walk`方法需要知道每次调用方法时人要走多远。以下代码是`Person`类的完整版本：

```
Public Class Person
    Private mName As String
    Private mBirthDate As Date
    Private mTotalDistance As Integer
    Public Sub Walk(ByVal distance As Integer)
        mTotalDistance += distance
    End Sub
    Public Function Age() As Integer
        Return CInt(DateDiff(DateInterval.Year, mBirthDate, Now()))
    End Function
End Class
```

使用此实现，`Person`对象会累加随时间行走的所有距离。每次调用`Walk`方法时，调用代码必须传递一个`Integer`值，表示要行走的距离。调用此方法的代码将类似于以下内容：

```
Dim myPerson As New Person()
myPerson.Walk(12)
```

参数使用`ByVal`关键字接受，这表示参数值是原始值的副本，而`ByRef`则创建对对象的引用。这是 Visual Basic 接受所有参数的默认方式。通常这是理想的，因为这意味着你可以在代码内部操作参数，改变其值而不会意外改变调用代码中的原始值。

如果你确实希望能够更改调用代码中的值，可以更改声明以通过引用传递参数，使用`ByRef`限定符：

```
Public Sub Walk(ByRef distance As Integer)
```

在这种情况下，你获得的是对原始值的引用（或指针），而不是副本。这意味着你对`distance`参数所做的任何更改都会反映回调用代码中，这与本章前面讨论的对象引用工作方式非常相似。

### 属性

.NET 环境提供了一种专门的方法类型，称为属性。属性是一种专门用于设置和检索数据值的方法。例如，你在`Person`类中声明了一个变量来包含姓名，因此`Person`类可能包含允许设置和检索该姓名的代码。这可以使用常规方法完成：

```
Public Sub SetName(ByVal name As String)
    mName = name
End Sub

Public Function GetName() As String
    Return mName
End Function
```

来自 `Person` 的代码片段

使用此类方法，你编写代码与对象交互：

```
Dim myPerson As New Person()

myPerson.SetName("Jones")
Messagebox.Show(myPerson.GetName())
```

虽然这完全可以接受，但使用属性后可以做得更好。属性样式方法将设置和检索值合并到单一结构中，并使类内的代码整体更流畅。你可以将这两个方法重写为单个属性。将以下代码添加到`Person`类中：

```
Public Property Name() As String
    Get
        Return _Name
    End Get
    Set(ByVal Value As String)
        _Name = Value
    End Set
End Property
```

来自 `Person` 的代码片段

随着 Visual Studio 2010 的引入，上面的代码可以用更简单的方式表示：

```
Public Property Name() As String
```

这种定义属性的方法实际上会创建一个名为`_Name`的字段，该字段未在代码中定义，而是由编译器创建。对于大多数在`get`或`set`期间不计算值的属性，这是最简单的方式来定义它。

通过使用属性方法，你可以使客户端代码更具可读性：

```
Dim myPerson As New Person()

myPerson.Name = "Jones"
Messagebox.Show(myPerson.Name)
```

属性方法同时声明作用域和数据类型：

```
Public Property Name() As String
```

在此示例中，你将属性的作用域声明为`Public`，但它可以使用与任何其他方法相同的范围选项声明 —`Public`、`Friend`、`Private`或`Protected`。

此属性的返回数据类型为`String`。属性可以返回几乎任何适合值性质的数据类型。在这方面，属性与使用`Function`关键字声明的方法非常相似。

尽管`Property`方法是一个单一结构，但它分为两部分：getter 和 setter。getter 包含在`Get...End Get`块中，负责按需返回属性的值：

```
Get
    Return mName
End Get
```

尽管此示例中的代码非常简单，但它可能更复杂，也许计算要返回的值，或应用其他业务逻辑来更改返回时的值。同样，更改值的代码包含在`Set...End Set`块中：

```
Set(ByVal Value As String)
    mName = Value
End Set
```

`Set`语句接受单个参数值来存储新值。然后块中的代码可以使用此值按适当方式设置属性的值。此参数的数据类型必须与属性本身的数据类型匹配。以这种方式声明参数使你能够在需要时更改用于参数值的变量名称。

默认情况下，参数名为`Value`，但你可以将其更改为其他名称，如下所示：

```
Set(ByVal NewName As String)
    mName = NewName
End Set
```

在许多情况下，你可以在此例程中应用业务规则或其他逻辑，以确保在实际更新对象内部数据之前新值是合适的。也可以将`Get`或`Set`块的范围限制为比属性本身更窄。例如，你可能希望允许任何代码检索属性值，但仅允许项目中的其他代码更改值。在这种情况下，你可以将`Set`块的作用域限制为`Friend`，而属性本身的作用域为`Public`：

```
Public Property Name() As String
    Get
        Return mName
    End Get
    Friend Set(ByVal Value As String)
        mName = Value
    End Set
End Property
```

来自 `Person` 的代码片段

新的作用域必须比属性本身的作用域更严格，并且可以限制`Get`或`Set`块，但不能同时限制两者。你未限制的那一个使用`Property`方法的作用域。

### 参数化属性

你创建的`Name`属性是单值属性的示例。你也可以创建属性数组或参数化属性。这些属性反映一系列或一组值。例如，人们通常有多个电话号码。你可能会将`PhoneNumber`属性实现为参数化属性，不仅存储电话号码，还存储每个号码的描述。要检索特定的电话号码，你将编写如下代码：

```
Dim myPerson As New Person()

Dim homePhone As String
homePhone = myPerson.Phone("home")
```

来自 `Person` 的代码片段

或者，要添加或更改特定的电话号码，你需要编写以下代码：

```
myPerson.Phone("work") = "555-9876"
```

不仅你在检索和更新电话号码属性，你也在更新一个特定的电话号码。这意味着一些事情。首先，你不能再使用一个简单的变量来保存电话号码，因为你现在存储的是号码列表及其关联的名称。其次，你实际上为你的属性添加了一个参数。你在每次属性调用时都将电话号码的名称作为参数传递。

要存储电话号码列表，可以使用`Hashtable`类。`Hashtable`与标准 VB `Collection`对象非常相似，但功能更强大——允许你测试特定元素的存在。向`Person`类添加以下声明：

```
Public Class Person
    Public Property Name As String
    Public Property BirthDate As Date
    Public Property TotalDistance As Integer
    Public Property Phones As New Hashtable
```

你可以通过向`Person`类添加以下代码来实现`Phone`属性：

```
Public Property Phone(ByVal location As String) As String
    Get
        Return CStr(Phones.Item(Location))
    End Get
    Set(ByVal Value As String)
        If Phones.ContainsKey(location) Then
            Phones.Item(location) = Value
        Else
            Phones.Add(location, Value)
        End If
    End Set
End Property
```

属性方法本身的声明与你之前看到的有一些不同：

```
Public Property Phone(ByVal location As String) As String
```

特别是，你为属性本身添加了一个参数`location`。该参数将充当电话号码列表的索引，在设置或检索电话号码值时必须提供。

由于`location`参数是在属性级别声明的，它对属性内的所有代码都可用，包括`Get`和`Set`块。在你的`Get`块中，你使用`location`参数从`Hashtable`中选择要返回的适当电话号码：

```
Get
    Return Phones.Item(location)
End Get
```

使用此代码，如果没有存储与`location`匹配的值，则会得到一个可捕获的运行时错误。

同样，在`Set`块中，你使用`location`来更新或添加`Hashtable`中的适当元素。在这种情况下，你使用`Hashtable`的`ContainsKey`方法来确定电话号码是否已存在于列表中。如果存在，则只需更新列表中的值；否则，你为该值添加一个新元素到列表中：

```
Set(ByVal Value As String)
    If Phones.ContainsKey(location) Then
        Phones.Item(location) = Value
    Else
        Phones.Add(location, Value)
    End If
End Set
```

这样，你就可以根据调用代码传递的参数添加或更新特定的电话号码条目。

### 只读属性

有时你可能希望属性为只读，以便无法更改它。例如，在`Person`类中，你可能有一个可读写的属性`BirthDate`，以及一个只读属性`Age`。如果是这样，`BirthDate`属性就是一个普通属性，如下所示：

```
Public Property BirthDate() As Date
```

相反，`Age`值是基于`BirthDate`的派生值。这不是应该直接更改的值，因此它是只读状态的完美候选。

你已经将`Age`方法实现为一个函数。从`Person`类中删除该代码，因为你将用`Property`过程替换它。函数过程和只读属性之间的区别非常微妙。两者都向调用代码返回一个值，并且无论哪种方式，对象都在运行由类模块定义的返回值的子例程。

区别更多是设计选择，而非编程上的。你可以完全不使用任何`Property`过程创建对象，只使用方法与对象交互即可。然而，`Property`过程显然是对象的属性，而`Function`可能是属性也可能是方法。通过仔细将所有属性实现为只读`Property`过程，而将任何询问性方法实现为`Function`过程，你可以创建更易读、更易理解的代码。

要使属性变为只读，请使用`ReadOnly`关键字并仅实现`Get`块：

```
Public ReadOnly Property Age() As Integer
    Get
        Return CInt(DateDiff(DateInterval.Year, mBirthDate, Now()))
    End Get
End Property
```

由于属性是只读的，如果你尝试实现`Set`块，将会得到语法错误。

### 仅写属性

与只读属性一样，有时属性应为仅写，即值可以更改但不能检索。

许多人有过敏症，因此`Person`对象可能需要了解该地区的环境过敏原。这不是应该从`Person`对象读取的属性，因为过敏原来自环境，而不是来自个人，但这是`Person`对象为了正常运行所需的数据。向类中添加以下变量声明：

```
Public Class Person
    Public Property Name As String
    Public Property BirthDate As Date
    Public Property TotalDistance As Integer
    Public Property Phones As New Hashtable
    Public WriteOnly Property Allergens As Integer
```

你可以按如下方式实现一个`AmbientAllergens`属性：

```
Public WriteOnly Property AmbientAllergens() As Integer
    Set(ByVal Value As Integer)
        mAllergens = Value
    End Set
End Property
```

要创建仅写属性，请使用`WriteOnly`关键字并仅在代码中实现`Set`块。由于属性是仅写的，如果你尝试实现`Get`块，将会得到语法错误。

### 默认属性

对象可以实现默认属性，有时可简化对象的使用，使其看起来像对象具有原生值。`Collection`对象就是这种行为的一个很好的例子，它有一个名为`Item`的默认属性，返回特定项的值，使你能够编写以下代码：

```
Dim mData As New HashTable()

Return mData(index)
```

默认属性必须是参数化属性。没有参数的属性不能标记为默认。这与 Visual Basic 的早期版本不同，在早期版本中任何属性都可以标记为默认。

我们的`Person`类有一个参数化属性——你之前构建的`Phone`属性。你可以使用`Default`关键字将其设为默认属性：

```
Default Public Property Phone(ByVal location As String) As String
    Get
        Return CStr(mPhones.Item(location))
    End Get
    Set(ByVal Value As String)
        If mPhones.ContainsKey(location) Then
            mPhones.Item(location) = Value
        Else
            mPhones.Add(location, Value)
        End If
    End Set
End Property
```

在此更改之前，你需要以下代码来使用`Phone`属性：

```
Dim myPerson As New Person()

MyPerson.Phone("home") = "555-1234"
```

现在，属性被标记为`Default`，你可以简化代码：

```
myPerson("home") = "555-1234"
```

正如你所见，不再需要引用属性名`Phone`。通过选择合适的默认属性，你可以使对象的使用更直观。

### 事件

方法和属性使你能够编写与对象交互的代码，按需调用特定功能。对象在处理过程中发生某些活动时提供通知通常很有用。你在控件中经常看到这种例子，其中按钮通过`Click`事件指示已被点击，或文本框通过`TextChanged`事件指示其内容已被更改。

对象可以引发自己的事件，提供一种强大且易于实现的机制，使对象能够通知客户端代码重要活动或事件。在 Visual Basic 中，事件使用标准的 .NET 委托机制提供；但在讨论委托之前，让我们先探讨如何在 Visual Basic 中处理事件。

#### 处理事件

我们都习惯于在表单中看到处理按钮`Click`事件的代码，例如以下代码：
