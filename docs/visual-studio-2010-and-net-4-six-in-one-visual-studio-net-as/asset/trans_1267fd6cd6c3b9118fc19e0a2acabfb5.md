

```vb
Public Class LinkedNode(Of 
K As Structure,
N As (IComparable(Of N), New))
...
End Class
```

存在一种特殊的约束类型 `New`，它要求该类型能够用于 `New` 表达式。此外还有两种特殊的类型约束，限制了可以满足该约束的类型种类：

- `Class` 将类型参数限制为引用类型。
- `Structure` 将类型参数限制为值类型，但可空类型除外。

你可以使用开放类型或关闭类型使用泛型基类型，如下示例所示：

```vb
Public Class SortedNode(Of 
K As Structure,
N As (IComparable(Of N), New))
Inherits LinkedNode(Of K, N)
End Class
```

```vb
Public Class CodeNode(Of N As (IComparable(Of N), New))
Inherits LinkedNode(Of Integer, N)
...
End Class
```

```vb
Public Class TransferNode
Inherits LinkedNode(Of Integer, Transfer)
...
End Class
```

不仅是类型，你还可以使用泛型方法，如下所示：

```vb
Public Class MyUtilities
    Public Sub WriteToDebug(Of T) (ByVal item As T)
    ...
    End Sub
    Public Sub Serialize(Of T As ISerializable) (ByVal item As T)
    ...
    End Sub
End Class
```

即使是 `Shared`、`MustOverride` 和 `Overridable` 方法也可以利用泛型，如下所示：

```vb
Public MustInherit Class BaseClass
    Public Shared WriteToDebug(Of T) (ByVal item As T)
    ...
    End Sub
    Public MustOverride Sub AbstractMethod(Of T) (ByVal item As T)
```

```vb
Public Overridable Sub SomeMethod(Of T) (ByVal item As T)
  '
End Sub
End Class
```

```vb
Public Class SubClass
    Inherits BaseClass

    Public Overrides Sub AbstractMethod(Of T) (ByVal item As T)
      '
    End Sub
    Public Overrides Sub SomeMethod(Of T) (ByVal item As T)
      '
    End Sub
End Class
```

运算符和委托在背后被实现为方法，并且两者都支持具有泛型方法能力的泛型。这里有一个定义和使用委托的小示例：

```vb
Public Class UtilityClass(Of T)
    Public Delegate Generic(ByVal arg As T)
    Public Sub SomeMethod(ByVal arg As T)
      '
    End Sub
End Class
```

```vb
' 使用委托
Dim obj As UtilityClass(Of Integer) = New UtilityClass(Of Integer)()
Dim del As UtilityClass(Of Integer).GenericDelegate = AddressOf obj.SomeMethod
del(3)
```

在 .NET 2.0 中，反射被扩展以支持泛型类型参数。`System.Type` 现在可以表示具有特定类型参数的（关闭的）或未指定的（开放的）泛型类型。

此外，.NET 2.0 中的许多类型——特别是集合——已经更改或添加以支持泛型。例如，`Array` 现在拥有了十几个新的泛型方法，并且有许多泛型集合类，以提供与旧 .NET 1.1 集合类型相关的全新且性能提升的体验。

## 部分类型 (Partial Types)

类型定义必须完全在一个物理文件中这一限制在之前的 Visual Basic 版本中是一个瓶颈，使得开发者的工作变得不必要的困难。大型类型定义无法拆分，对于那些密集使用代码生成的人来说这尤其不利，因为生成的代码无法与用户定义的代码轻松分离。

部分类型解决了这个问题。通过使用 `Partial` 关键字，类、结构体和接口定义可以拆分为多个文件或同一文件中的多个分段。这解决了用户定义代码与生成代码的分离问题。在编译期间，类型定义的各个分区会被合并，包括特性、基类、接口和访问修饰符。

例如，你可以将 `SampleClass` 分为两个部分，如下示例所示：

```vb
--- SampleClass1.cs
<Serializable>()
Partial Public Class SampleClass
    Private _IsDisposed As Boolean
End Class
```

```vb
--- SampleClass2.cs
Partial Class SampleClass
    Implements IEquatable(Of SampleClass) As Boolean
    Implements System.IEquatable(Of SampleClass).Equals

    Public Function EqualsWithSample(ByVal other As SampleClass) As Boolean
        ...
    End Function
```

这些部分的合并将产生一个名为 `SampleClass` 的类，它实现了 `IEquatable(Of SampleClass)` 接口，并装饰了 `Serializable` 特性。

## 可空类型 (Nullable Types)

在 CLR 1.0 中，值类型的一个弱点是缺乏值类型的“可空性”。为了消除这一点，CLR 2.0 的设计者在运行时引入了可空类型的概念。引入了一个新的泛型 `System.Nullable(Of T)` 结构体，其中 `T` 应该是一个值类型。

Visual Basic 2005 语法允许为 `System.Nullable(Of T)` 实例赋值 `Nothing`，并将实例值与 `Nothing` 进行比较。`HasValue` 属性告知可空实例是否有值，如果有，则可以通过 `Value` 属性获取。

使用这些属性，你可以定义一个感知 `Nothing` 的 `Square` 方法，如下示例所示：

```vb
Public Function Square(ByVal n As Nullable(Of Integer)) As Nullable(Of Integer)
    Return IIf(n.HasValue, n.Value * n.Value, Nothing)
End Function
```

`Nullable(T)` 还定义了收窄转换运算符，将 `Nullable(T)` 转换为 `T`，如下：

```vb
Dim n As Nullable(Of Integer) = 5
Dim i As Integer = n
```

如果 `n` 没有值，则这种转换会导致运行时错误：

```vb
Dim n As Nullable(Of Integer) = Nothing
Dim i As Integer = n ' 运行时错误
```

