

# 使用 TryCast

与 DirectCast 类似的方法是 TryCast。TryCast 将一种类型的值转换为另一种类型，但与 DirectCast 不同的是，如果它无法进行转换，则 TryCast 不会抛出异常。相反，如果转换无法执行，TryCast 只是简单地返回 Nothing。TryCast 仅适用于引用值；它不能与 Integer 或 Boolean 等值类型一起使用。

使用 TryCast，你可以编写如下代码：

```
Public Sub TryCast1 (ByVal obj As Object)
    Dim temp = TryCast(obj, Object)      If temp Is Nothing Then
        ' the cast couldn't be accomplished
        ' so do no work
    Else
        temp.DoSomething()
    End If
End Sub
```

如果你不确定是否可以进行类型转换，那么最好经常使用 TryCast。此函数避免了捕获 CType 或 DirectCast 可能抛出的异常的开销和复杂性，同时仍然为你提供了一种轻松地将对象转换为另一种类型的方法。

## 创建类

使用对象是相当直接和直观的。这是一种即使是最新手的程序员也能快速掌握并接受的东西。创建类和对象则稍微复杂一些且更有趣。

### 基本类

如前所述，对象仅仅是特定模板（类）的实例。类包含定义其对象行为的代码，并定义将包含对象个人数据的实例变量。

类使用 Class 关键字创建，并包含构成类的变量、方法、属性和事件的定义（声明）和实现（代码）。基于此类创建的每个对象都将具有相同的方法、属性和事件，以及由类中的字段定义自己的数据集合。

### Class 关键字

如果你想创建一个代表人 — Person 类 — 的类，你可以使用 Class 关键字：

```
Public Class Person

    ' Implementation code goes here

End Class
```

如你所知，Visual Basic 项目由一组扩展名为 .vb 的文件组成。每个文件可能包含多个类，这意味着在单个文件中你可以有类似这样的内容：

```
Public Class Adult
    ' Implementation code goes here.
End Class

Public Class Senior
    ' Implementation code goes here.
End Class
```

![](img/d99870e80390742f93963da7be0b2e61_123_0.png)

```
Public Class Child
' Implementation code goes here.
End Class
```

最常见且首选的方法是每个文件一个类。这是因为 Visual Studio 2010 解决方案资源管理器和代码编辑环境都旨在使从文件到文件导航以查找代码变得容易。例如，如果你创建一个包含所有这些类的单个类文件，解决方案资源管理器只显示一个条目，如图 2-13 所示。

![](img/d99870e80390742f93963da7be0b2e61_124_0.png)

## 图 2-13

然而，Visual Studio IDE 确实提供了 Class View 窗口。如果你决定在每个物理 .vb 文件中放置多个类，你可以使用图 2-14 所示的 Class View 窗口快速高效地浏览代码，在类之间跳转，而无需手动在特定代码文件中定位这些类。要显示 Class View，请从菜单中选择 View 然后 Class Window。

![](img/d99870e80390742f93963da7be0b2e61_124_1.png)

## 图 2-14

即使你坚持每个文件一个类，Class View 窗口也非常有用，因为它仍然为你提供了整个应用程序的基于类的视图。

本章在示例中使用每个文件一个类，因为这是最常见的方法。首先，打开 Visual Studio IDE 并创建一个名为“ObjectIntro”的新 Windows Forms Application 项目。选择 Project ➕ Add Class 菜单选项以向项目添加新的类模块。你将看到标准的 Add New Item 对话框。将名称更改为 Person.vb 并单击 Add。结果将是以下代码，它定义了 Person 类：

```
Public Class Person

End Class
```

Person 类创建后，你就可以开始添加代码来声明接口、实现行为并声明实例变量。

## 字段

字段是在类中声明的变量。它们将在应用程序运行时可用于每个单独的对象。每个对象都有自己的数据集合 — 基本上，每个对象都有字段的自己的副本。

之前，你了解到类只是一个用于创建特定对象的模板。你在类内定义的变量也只是模板 — 并且每个对象都有这些变量的自己的副本来存储其数据。

声明成员变量与在 Class 块结构内声明变量一样简单。将以下代码添加到 Person 类：

```
Public Class Person

    Private mName As String
    Private mBirthDate As Date
End Class
```

你可以使用以下关键字控制字段的作用域：

- Private — 仅对类内的代码可用
- Friend — 仅对项目/组件内的代码可用
- Protected — 仅对继承自该类的类可用（在第 3 章中详细讨论）
- Protected Friend — 可用于项目/组件内的代码以及继承自该类的类，无论是否在项目中（在第 3 章中详细讨论）
- Public — 可用于类外部的代码以及引用该程序集的任何项目

通常，字段使用 Private 关键字声明，使其仅对类每个实例内的代码可用。选择其他任何选项都应非常谨慎，因为所有其他选项都允许类外部的代码直接与变量交互，这意味着值可能会被更改，而你的代码永远不会知道发生了更改。

> 使字段保持 Private 的一个常见例外是使用 Protected 关键字，在第 3 章中讨论。

## 方法

对象通常需要提供可在处理对象时调用的服务（或函数）。使用它们自己的数据或作为参数传递给方法的数据，它们操纵信息以产生结果或执行操作。

声明为 Public、Friend 或 Protected 作用域的方法定义了类的接口。作用域为 Private 的方法仅对类本身内的代码可用，可用于为代码提供结构和组织。如前所述，每个方法内的实际代码称为 *implementation*，而方法本身的声明定义了接口。

方法只是编码在类内以实现你希望为对象用户提供的服务的例程。一些方法返回值或向调用代码提供信息。这些称为 *interrogative methods*。其他称为 *imperative methods*，只是执行操作而不向调用代码返回任何内容。

在 Visual Basic 中，方法使用类模块中定义对象的 Sub（用于 imperative 方法）或 Function（用于 interrogative 方法）例程实现。Sub 例程可能接受参数，但完成后不返回任何结果值。Function 例程也可以接受参数，并且始终生成可供调用代码使用的结果值。

使用 Sub 关键字声明的方法只是不返回值的。向 Person 类添加以下代码：

```
Public Sub Walk()

' implementation code goes here

End Sub
```

Walk 方法 presumably 包含在调用时执行一些有用工作但完成后没有结果值返回的一些代码。要使用此方法，你可能会编写如下代码：

```
Dim myPerson As New Person()
myPerson.Walk()
```

一旦你创建了 Person 类的实例，你就可以简单地调用 Walk 方法。

### 返回值的方法

如果你的方法确实生成应返回的某个值，你需要使用 Function 关键字：

```
Public Function Age() As Integer
    Return CInt(DateDiff(DateInterval.Year, mBirthDate, Now()))
End Function
```

请注意，在声明函数时必须指明返回值的数据类型。此示例返回方法的结果计算年龄。你可以使用 Return 关键字返回适当数据类型的任何值。

你也可以通过设置函数名本身的值来在不使用 Return 关键字的情况下返回值：

```
Public Function Age() As Integer
    Age = CInt(DateDiff(DateInterval.Year, mBirthDate, Now()))
End Function
```

这在功能上等同于之前的代码。无论哪种方式，你都可以使用类似以下的代码使用此方法：

```
Dim myPerson As New Person()
Dim age As Integer

age = myPerson.Age()
```

Age 方法返回一个 Integer 数据值，你可以根据需要在程序中使用它；在这种情况下，你只是将其存储在变量中。

### 指示方法作用域

在方法声明前添加适当的关键字指示作用域：

```
Public Sub Walk()
```

