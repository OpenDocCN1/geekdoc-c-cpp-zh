

这个主题可能会变得复杂，所以在继续讨论逆变之前，让我们先提供一个关于协变在代码中的非常简单的示例。以下代码声明了两个类 Parent 和 ChildClass，并展示了协变的使用：

```vbnet
Public Class Parent(Of T)

End Class

Public Class ChildClass(Of T)
    Inherits Parent(Of T)

End Class

Public Class CoVariance
    Public Sub MainMethod()
        Dim cc As New ChildClass(Of String)
        Dim dad As Parent(Of String)
        'Show me the covariance
        dad = cc
    End Sub
End Class
```

来自 CoVariance 的代码片段

你会注意到 ChildClass 继承自 Parent。片段继续展示了一个从调用应用程序中提取的方法。它被称为 MainMethod，你可以看到代码创建了一个 ChildClass 的实例并声明了一个 Parent 的实例。接下来它尝试将 ChildClass 的实例 cc 分配给类型为 Parent 的实例 dad。正是这个赋值说明了协变的一个示例。当然，我们可以考虑数十种不同的特化，但这为所有这些示例提供了基础。

注意，如果不是将 dad 声明为 Parent (Of String)，而是将其声明为 Parent (Of Integer)，那么将 cc 分配给 dad 的赋值就会失败，因为 dad 不再是正确的 Parent 类型。必须记住，作为泛型实例化的一部分而指定的类型会直接影响该泛型实例的底层类类型。

逆变是指在需要基类型时可以传递派生类型的能力。这些特性被放在同一个主题中讨论的原因在于它们实际上都是方差概念的特化。区别主要在于理解在逆变的情况下，你传递的是一个 ChildClass 的实例，而期望的是一个 Parent 实例。不幸的是逆变可以被称为反直觉。你将创建一个基方法，而 .NET 将支持派生类使用它。为了说明这一概念，以下代码片段创建了两个新的类（它们不是泛型类），然后有一个用于使用这些新类与泛型方法来说明逆变的方法代码片段：

```vbnet
Public Class Base

End Class

Public Class Derived
    Inherits Base

End Class

Public Class ContraVariance

    Private baseMethod As Action(Of Base) = Sub(param As Base)
        'Do something.
    End Sub

    Private derivedMethod As Action(Of Derived) = baseMethod

    Public Sub MainMethod()
        ' Show the contra-syntax
        Dim d As Derived = New Derived()
        derivedMethod(d)
        baseMethod(d)
    End Sub
End Class
```

来自 ContraVariance 的代码片段

如前例所示，你可以拥有一个期望输入参数类型为 Base 作为其输入参数的方法。过去，此方法不会接受参数类型为 Derived 的调用，但有了逆变，方法调用现在将接受类型为 Derived 的参数，因为这个派生类根据定义将支持与基类相同的接口，只是具有可以忽略的额外功能。因此，尽管乍一看感觉是倒退的，你实际上能够将实现派生类的泛型传递给期望使用基类定义的泛型的<|message|>。

## SUMMARY

本章介绍了针对集合的类和语言元素。我们首先介绍了数组以及 Visual Basic 对数组的支持。本章随后介绍了集合类。默认情况下，这些类在类型 Object 上操作，正是这种能够在实现中处理任何或所有对象的能力使得这些类既强大又有限。

在快速回顾了通常与这些类相关联的迭代语言结构之后，本章继续讨论泛型。泛型使你能够创建类、结构、接口和方法模板。这些模板根据它们在运行时如何声明或调用而获得特定的类型。泛型为你提供了另一种代码重用机制，以及过程化和面向对象的概念。

泛型还使你能够将使用类型为 Object（或其他通用类型）的参数或变量的代码更改为使用特定数据类型。这通常会导致性能大大提高，并提高代码的可读性。

- System.Xml.Xsl 在使用可扩展样式表语言（XSL）和 XSL 转换（XSLT）时提供必要的对象。
- System.Xml.Linq 提供使用 LINQ 查询 XML 的支持（有关更多详细信息，请参阅本章后面的 LINQ 部分）。

本章通过介绍一些基本的 XML 概念并演示 Visual Basic 如何结合 .NET Framework 使用 XML，使这一系列技术变得清晰易懂。

在本章结束时，你将能够使用 Visual Basic 生成、操作和转换 XML。

## AN INTRODUCTION TO XML

XML 是一种类似于 HTML 的标记语言。事实上，XML 和 HTML 是远亲，并且都源自标准通用标记语言（SGML）。这意味着 XML 利用了 HTML 的最有用特性之一——可读性。然而，XML 与 HTML 不同之处在于 XML 表示数据，而 HTML 是显示数据的机制。XML 中的标签描述数据，如以下示例所示：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Movies>
<FilmOrder name="Grease" filmId="1" quantity="21"/>
<FilmOrder name="Lawrence of Arabia" filmId="2" quantity="10"/>
<FilmOrder name="Star Wars" filmId="3" quantity="12"/>
<FilmOrder name="Shrek" filmId="4" quantity="14"/>
</Movies>
```

该 XML 文档表示对电影集合的商店订单。用于表示电影订单的标准将对电影租赁公司、收藏家和其他人有用。可以使用 XML 共享此信息，原因如下：

- XML 中的数据标签是自描述的。
- XML 是一种开放标准，并且今天在大多数平台上都得到支持。

XML 支持由不熟悉 XML 文档内容的应用解析数据。XML 文档也可以与描述（模式）关联，该描述告知应用程序 XML 文档中数据的结构。

在此时，XML 看起来很简单：它只是以通用接受的格式以人类可读的方式交换数据。你应该了解的关于 XML 的基本要点如下：

- XML 数据可以存储在纯文本文件中。
- 如果文档遵循 XML 标准，则称该文档是 well-formed 的（有关 XML 标准的更多详细信息，请参阅 www.w3.org/standards/xml/）。
- 标签用于指定文档的内容——例如，`<FilmOrder>`。
- XML 元素（也称为节点）可以被视为文档中的对象。
- 元素是文档的基本构建块。每个元素都包含开始标签和结束标签；并且一个标签可以在一个标签中既是开始标签又是结束标签——例如，`<FilmOrder/>`。在这种情况下，标签指定元素没有内容（或内部文本）（没有结束标签，因为由于缺乏内部文本内容而不需要）。这种标签被称为空标签。
- 数据可以包含在元素中（元素内容）或包含在元素中的属性中。
- XML 是分层的。一个文档可以包含多个元素，这些元素本身可以包含子元素，依此类推。然而，XML 文档只能有一个根元素。

最后一点意味着 XML 文档层次结构可以被视为包含节点的树：

- 示例文档具有根节点 `<Movies>`。
- 根节点的分支是类型为 `<FilmOrder>` 的元素。
- XML 元素 `<FilmOrder>` 的叶子是其属性：name、quantity 和 filmId。

当然，我们对 Visual Basic 对 XML 的实际使用感兴趣。例如，对示例 XML 的实际操作是为电影供应商的员工在应用程序中显示特定的电影订单，以便供应商可以填写订单然后将信息保存到数据库。本章解释了如何使用 .NET Framework 类库提供的功能执行此类任务。

## XML SERIALIZATION

演示 Visual Basic 对 XML 的支持的最简单方法是使用它来序列化一个类。对象的序列化意味着它被写入流，例如文件或套接字。也可以执行相反的过程：对象可以通过从流中读取它并从该流创建 XML 来反序列化。你可能希望这样做以将对象的数据保存到本地文件，或通过网络传输它。

> 本章中描述的序列化类型是 XML 序列化，其中 XML 用于以序列化形式表示类。你将在 WCF 章节（第 13 章）中看到其他形式的序列化。

为了帮助你理解 XML 序列化，让我们检查 FilmOrder 项目中的一个名为 `FilmOrder` 的类（可以在 www.wrox.com 的代码下载中找到）。该类在 Visual Basic 中实现，并由公司用于处理电影订单。

每个订单对应的 `FilmOrder` 的一个实例可以序列化为 XML 并通过套接字从客户端计算机发送。我们在这里谈论的是专有形式的数据：`FilmOrder` 的一个实例被转换为通用形式——XML——可以被普遍理解。

`System.Xml.Serialization` 命名空间包含支持将对象序列化为 XML 以及从 XML 反序列化对象的类和接口。对象使用 `XmlSerializer` 类序列化为文档或流。

让我们看看如何使用 `XmlSerializer`。为了使示例更简单，我们将使用控制台应用程序。此控制台应用程序将使用类 `FilmOrder`：

```vbnet
Public Class FilmOrder
    Public Name As String
    Public FilmId As Integer
    Public Quantity As Integer
    Public Sub New()
    End Sub
    Public Sub New(ByVal name As String, _
                   ByVal filmId As Integer, _
                   ByVal quantity As Integer)
        Me.Name = name
        Me.FilmId = filmId
        Me.Quantity = quantity
    End Sub
End Class
```

