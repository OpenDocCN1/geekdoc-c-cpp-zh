
令人惊讶的事实，这段代码在 Visual Basic 2010 中开启 `Option Strict On` 的情况下可以编译并运行，尽管它在 Visual Basic 2008 中无法编译。

这种替换被称为**协变**（covariance）。在编程语言中，协变提供了使用比原始指定更派生类型的能力。协变和逆变（contravariance）是一对，提供了使用更少派生类型的能力。

> 理解变异（variance）的基础知识将帮助你成为一个更高产的开发者。请阅读第 24 章中的“变异概述”章节以了解更多关于变异背后的概念。

## Visual Basic 2010 中的变异

目前，C# 仅实现了理论上可以通过协变和逆变实现的部分行为。然而，CLR 设计师在这个新版本中取得的成果是重大且实用的。但是，Visual Basic 2010 和 C# 4.0 都具有在 CLR 中利用变异的所有特性。当前 Visual Basic 2010 的变异实现可以用以下几点来描述：

- 对于非泛型类型，通过变异与之前的 Visual Basic 版本相比没有任何变化。
- 为泛型类型提供变异的方法是将泛型类型的参数标记为变体（variant）。由于 CLR 的限制，变体参数可以在泛型接口和委托类型上声明。
- 变异仅在类型参数之间存在引用转换时才适用。例如，变异适用于 `IEnumerable(Of String)` 和 `IEnumerable(Of Object)`，因为 `String` 和 `Object` 之间存在引用转换。然而，从 `Integer` 到 `Object` 的转换是装箱转换，因此变异不适用于 `IEnumerable(Of Integer)` 和 `IEnumerable(Of Object)`。
- 变异不是自动的。编译器不会推断类型参数是协变的还是逆变的。开发者必须显式地声明他们的意图。

> 使用 `Option Strict Off` 时，Visual Basic 允许任何隐式转换且不会引发任何编译错误。当你故意使用变异时，强烈建议使用 `Option Strict On` 以在编译期间观察类型转换和转换问题。

## 协变

以下是协变的示例：

```
Public strings As IList(Of String) = New List(Of String)
Public objects As IEnumerable(Of Object) = strings
```

尽管这在开启 `Option Strict` 时无法在 Visual Studio 2008 中编译，但在 Visual Basic 2010 中可以正常工作。编译器接受了它，并为执行声明生成了正确的代码。此行为的关键在于 `IEnumerable(Of T)` 和 `IEnumerator(Of T)` 接口是使用变体类型参数 `T` 声明的：

```
Public Interface IEnumerable(Of T)
Inherits IEnumerable

Function GetEnumerator() As IEnumerator
End Interface
```

（注：此处为）
```
Public Interface IEnumerator(Of T)
Inherits IDisposable, IEnumerator
ReadOnly Property Current As T
End Interface
```

接口定义中唯一的更改——与之前的语言版本相比——`Out` 修饰符声明 `T` 只能出现在接口的输出位置——否则编译器将引发错误。这种限制使得（当然，它可以使得）接口在 `T` 上是协变的，这意味着如果 `X` 有到 `Y` 的引用转换，那么 `IEnumerable(Of X)` 就被视为 `IEnumerable(Of Y)`。

由于这个定义，对象序列可以包含对象的子类型，之前的代码可以工作。这种协变行为在与 LINQ 表达式关联时非常有用。

为了尝试这一点，请创建一个控制台应用程序并将其命名为 `CovarianceSample`。在项目中添加名为 `Pet.vb` 的新代码文件，并将列表 22-6 中的代码粘贴到此新文件中。

- 列表 22-6：Pet.vb

```
Public Inherits Class Pet
Public Property Name As String
Public Property Age As Integer

Public Shared Function ShackUpWith(
ByVal atHome As IEnumerable(Of Pet),
ByVal newComers As IEnumerable(Of Pet) As IEnumerable(Of Pet)

Return atHome.Union(newComers)
End Function

End Class
```

（图片）
```
Public NotInheritable Class Dog
Inherits Pet
End Class
```

```
Public NotInheritable Class Macaw
Inherits Pet
End Class
```

> [Pet.vb] 代码文件可在 Wrox.com 下载。

你拥有具有两个具体（`Dog` 和 `Macaw`）的抽象 `Pets`。这些类型旨在用于宠物商店应用程序，因此 `Pet` 有一个名为 `ShackUpWith` 的操作，处理宠物序列并返回它们。

修改如列表 22-7 所示的应用程序的 `Module.vb` 文件

## 列表 22-7：CovarianceSample 的 Module1.vb

（图片）
```
Option Strict On
Module Module

Sub Main()
    Dim Dogs As New List(Of Dog) From {
        New Dog(.Name = "Spike", .Age = 3),
        New Dog(.Name = "Murray", .Age = 12),
        New Dog(.Name = "Peach", .Age = 2)
    }

    Dim Macaws As New List(Of Macaw) From {
        New Macaw(.Name = "Georgey", .Age = 32),
        New Macaw(.Name = "Bella", .Age = 4),
        New Macaw(.Name = "Grey", .Age = 1)
    }

    Dim Youngsters =
        From pet in Dogs.ShackUpWith(Macaws)
        Where pet.Age < 5
        Select pet

    For pet in Youngsters
        Console.WriteLine(pet.Name)
    Next
End Sub
End Module
```
