
框架类存在于应用程序类之下。例如，`.NET` 基础类库是一个所有 `.NET` 应用程序构建其上的框架。你也可以在 `.NET Framework` 之上构建自己的框架（见图 3-20）。

![](img/d99870e80390742f93963da7be0b2e61_220_1.png)

如果你采用这种观点，那么 `PrintableObject` 类根本就不是应用程序的一部分，而是应用程序构建其上的框架的一部分。如果是这样，那么 `Customer` 不是 `PrintableObject` 的特定情况这一事实就不那么重要了，因为你并不是说它是这样的东西，而是说它利用了框架功能的一部分。

要使所有这些工作正常进行，需要在框架本身的设计中进行大量的规划和深思熟虑。为了看到你面临的危险，请考虑你可能不仅想打印对象，还想将它们存储到文件中。在这种情况下，你可能不仅有 `PrintableObject`，还有 `SavableObject` 作为基类。

问题是，如果 `Customer` 应该同时可打印和可保存怎么办？如果所有可打印对象都是可保存的，你可能会得到如图 3-21 所示的结果。

![](img/d99870e80390742f93963da7be0b2e61_220_2.png)

另外，如果所有可保存的对象都是可打印的，你可能会得到如图 3-22 所示的结果。然而，这两种方法都不能真正提供一个体面的解决方案，因为很可能“可打印”的概念和“可保存”的概念是不同的，并且在这两种方式中都不是相互关联的。

面对这种问题时，最好避免使用继承，而应依赖于多个接口。

### 继承与多接口

虽然继承功能强大，但它主要用于实现 `is-a` 关系。有时你会有一些对象需要一个共同的接口，即使它们并不是某个提供该接口的基础类的特定情况。我们在讨论 `PrintableObject`、`SavableObject` 和 `Customer` 类时已经探讨过这个问题。

有时多接口是比继承更好的替代方案。创建和使用次要接口和多接口的语法已在讨论中提到。

多接口可以被视为实现 `is-a` 关系的另一种方式，尽管通常最好将继承视为 `is-a` 关系，而将多接口视为实现 `act-as` 关系的方式。

进一步考虑，我们可以说 `PrintableObject` 概念或许可以更好地表达为一个接口——`IPrintableObject`。

当类实现像 `IPrintableObject` 这样的次要接口时，你并不是在说你的类是一个可打印对象，你是在说它可以“充当”一个可打印对象。`Customer` 是一个 `Contact`，但同时它也可以充当一个可打印对象。这在图 3-23 中有所说明。

![](img/d99870e80390742f93963da63da7be0b2e61_221_0.png)

**FIGURE 3-22**

**FIGURE 3-23**

这种方法的缺点是，当你实现 `IPrintableObject` 时，你没有继承的实现。之前你已经看到如何在多个类中实现接口时重用通用代码。虽然没有继承那么自动或容易，但通过额外的工作，仍然可以重用实现代码。

### 应用继承与多接口

也许最好的了解继承和多接口如何交互的方法是看一个例子。回到原始的 `OOExample` 项目，以下示例结合了继承和多接口，创建了一个同时具有 `is-a` 和 `act-as` 关系的对象。作为额外的好处，你将使用 `.NET Framework` 的打印到打印机或打印预览对话框的能力。

#### 创建 Contact 基础类

你已经在项目中有了一个简单的 `Customer` 类，现在添加一个 `Contact` 基础类。选择 `Project ➜ Add Class` 并添加一个名为 `Contact` 的类：

```
Public MustInherit Class Contact
    Private mID As Guid = Guid.NewGuid
    Private mName As String
```

```
Public Property ID() As Guid
    Get
        Return mID
    End Get
    Set(ByVal value As Guid)
        mID = value
    End Set
End Property
Public Property Name() As String
    Get
        Return mName
    End Get
    Set(ByVal value As String)
        mName = value
    End Set
End Property
End Class
```

#### 派生 Contact

现在你可以让 `Customer` 类继承自这个基础类，因为它是一个 `Contact`。此外，由于你的基础类现在实现了 `ID` 和 `Name` 属性，你可以简化 `Customer` 中的代码，通过删除这些属性及其相关变量：

```
Public Class Customer
    Inherits Contact
    Private mPhone As String
    Public Property Phone() As String
    Get
        Return mPhone
    End Get
    Set(ByVal value As String)
        mPhone = value
    End Set
    End Property
End Class
```

这展示了将 `Customer` 派生自 `Contact` 的好处，因为你现在可以在所有其他类型的 `Contact` 中共享 `ID` 和 `Name` 代码。

#### 实现 IPrintableObject

你也知道 `Customer` 应该能够充当可打印对象。为了以可重用的方式实现这一点需要一些思考。首先，你需要定义 `IPrintableObject` 接口。

你将使用 `.NET` 从 `System.Drawing` 命名空间提供的标准打印机制。如图 3-24 所示，通过选择 `Project → Add reference` 将 `System.Drawing.dll` 的引用添加到 `Interfaces` 项目。

![](img/d99870e80390742f93963da7be0b2e61_222_0.png)

完成之后，打开 `Interfaces` 项目中 `Interfaces.vb` 的代码窗口并添加以下代码：

```
Imports System.Drawing
Public Interface IPrintableObject
    Sub Print()
    Sub PrintPreview()
    Sub RenderPage(ByVal sender As Object, _
        ByVal ev As System.Drawing.Printing.PrintPageEventArgs)
End Interface
```

Code snippet from Interfaces

该接口确保任何实现 `IPrintableObject` 的对象都将具有 `Print` 和 `PrintPreview` 方法，以便你可以调用适当的打印类型。它还确保对象具有 `RenderPage` 方法，该方法可以由该对象实现以在打印页面上渲染对象的数据。

此时，你可以直接在 `Customer` 对象中实现处理打印所需的所有代码。这并不理想，因为其中一些代码将在任何想要实现 `IPrintableObject` 的对象中通用，而且最好找到一种共享该代码的方法。

为此，你可以创建一个新的类 `ObjectPrinter`。这是一个框架风格的类，因为它与任何特定应用程序无关，但可以在使用 `IPrintableObject` 的任何应用程序中使用。

通过选择 `Project → Add class` 向 `ObjectAndComponents` 项目添加一个名为 `ObjectPrinter` 的新类。该类将包含打印任何对象共用的所有代码。它使用 `.NET Framework` 类库提供的内置打印支持。要使用它，你需要导入几个命名空间，因此将以下代码添加到新类中：

```
Imports System.Drawing
Imports System.Drawing.Printing
Imports Interfaces
```

然后你可以定义一个 `PrintDocument` 变量，它将保存对打印机输出的引用。你还将声明一个变量来保存对实际要打印对象的引用。注意你正在使用 `IPrintableObject` 接口数据类型为此变量：

```
Public Class ObjectPrinter
    Private WithEvents document As PrintDocument
    Private printObject As IPrintableObject
```

现在你可以为任何实现 `IPrintableObject` 的对象创建启动打印过程的例程。此代码完全通用；你将在 `ObjectPrinter` 类中编写它，以便可以在其他类中重用：

```
Public Sub Print(ByVal obj As IPrintableObject)
    printObject = obj
    document = New PrintDocument()
    document.Print()
End Sub
```

Code snippet from Form1

同样，你可以实现一个方法来显示对象的打印预览。此代码也完全通用，因此在此处添加以便重用：

```
Public Sub PrintPreview(ByVal obj As IPrintableObject)
    Dim PPdlg As PrintPreviewDialog = New PrintPreviewDialog()
    printObject = obj
    document = New PrintDocument()
    PPdlg.Document = document
    PPdlg.ShowDialog()
End Sub
```

Code snippet from Form1

最后，你需要捕获由 `.NET` 打印机制自动引发的 `PrintPage` 事件。此事件由 `PrintDocument` 对象在确定需要将数据渲染到页面上时引发。通常，你会在此例程中放置将文本或图形绘制到页面表面的代码。然而，因为这是一个通用的框架类，你不会在这里做那件事；相反，将调用委托回你想要打印的实际应用程序对象：

```
Private Sub PrintPage(ByVal sender As Object, _
        ByVal ev As System.Drawing.Printing.PrintPageEventArgs) _
        Handles document.PrintPage
    printObject.RenderPage(sender, ev)
End Sub
```

> Code snippet from Form1

这使应用程序对象本身能够确定其数据应如何渲染到输出页面。你可以通过在 `Customer` 类上实现 `IPrintableObject` 接口来了解如何做到这一点：

```
Imports Interfaces
Public Class Customer
    Inherits Contact
    Implements IPrintableObject
```

> Code snippet from Interfaces

通过添加此代码，你要求 `Customer` 类实现 `Print`、`PrintPreview` 和 `RenderPage` 方法。为了避免在测试代码时浪费纸张，让 `Print` 和 `PrintPreview` 方法相同并仅执行打印预览显示，将此代码添加到 `Customer` 类：

```
Public Sub Print() _
    Implements Interfaces.IPrintableObject.Print
    Dim printer As New ObjectPrinter()
        printer.PrintPreview(Me)
End Sub
```

> Code snippet from Customer

注意你正在使用一个 `ObjectPrinter` 对象来处理执行打印预览的通用细节。事实上，你创建的任何实现 `IPrintableObject` 的类都将具有完全相同的代码来实现打印预览功能，依赖于你的通用 `ObjectPrinter` 来处理细节。

你还需要实现 `RenderPage` 方法，这就是你实际将对象数据放到打印页面上的地方：

```
Private Sub RenderPage(ByVal sender As Object, _
    ByVal ev As System.Drawing.Printing.PrintPageEventArgs) _
    Implements IPrintableObject.RenderPage
    Dim printFont As New Font("Arial", 10)
    Dim lineHeight As Single = printFont.GetHeight(ev.Graphics)
    Dim leftMargin As Single = ev.MarginBounds.Left
    Dim yPos As Single = ev.MarginBounds.Top
    ev.Graphics.DrawString("ID: " & ID.ToString, printFont, Brushes.Black, _
        leftMargin, yPos, New StringFormat())
    yPos += lineHeight
    ev.Graphics.DrawString("Name: " & Name, printFont, Brushes.Black, _
        leftMargin, yPos, New StringFormat())
    ev.HasMorePages = False
End Sub
```

> Code snippet from Customer

所有这些代码都特定于你的对象，这是有意义的，因为你正在渲染特定的数据以供打印。然而，你无需担心是打印到纸上还是打印预览的细节；这是由你的 `ObjectPrinter` 类处理的，而它又使用 `.NET Framework`。这使你能够专注于在应用程序类中生成页面输出。

通过在 `ObjectPrinter` 中泛化打印代码，你已经实现了可通过 `IPrintableObject` 接口使用的重用级别。只要你想打印 `Customer` 对象的数据，就能让它充当 `IPrintableObject` 并调用其 `Print` 或 `PrintPreview` 方法。要看到此功能的工作方式，向 `Form1` 添加一个新按钮控件并使用以下代码：

```
Private Sub btnPrint_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles btnPrint.Click
    Dim obj As New Customer
    obj.Name = "Douglas Adams"
    CType(obj, IPrintableObject).PrintPreview()
End Sub
```

Form1 中的代码片段

此代码创建一个新的 `Customer` 对象并设置其 `Name` 属性。然后你使用 `CType` 方法通过其 `IPrintableObject` 接口访问该对象以调用 `PrintPreview` 方法。

当你运行应用程序并单击按钮时，你将获得一个打印预览显示，显示对象的数据（见图 3-25）。

![](img/d99870e80390742f93963da7be0b2e61_225_0.png)

图 3-25

### 要深入到什么程度？

到目前为止讨论的大多数示例都说明了如何基于单个父类创建子类。这称为单级继承。事实上，继承可以有多层深。例如，你可能拥有如图 3-26 所示的深层层次结构。

从 `System.Object` 的根到 `NAFTACustomer` 你有四层继承。这可以描述为四级继承链。

关于继承链应该有多深并没有硬性规定，但传统智慧和在 `Smalltalk` 和 `C++` 等其他语言中使用继承的一般经验表明，继承链越深，维护应用程序就越困难。

出现这种情况有两个原因。首先是脆弱基类或脆弱超类问题，稍后会讨论。第二原因是深层的继承层次结构往往会严重降低代码的可读性，因为对象的代码分散在许多不同的类中，所有这些类都由编译器组合起来创建你的对象。

采用面向对象设计和编程的原因之一是为了避免所谓的意大利面条代码，即你查看的任何代码几乎都做不了什么有用的事情，反而调用其他应用程序中其他

![](img/d99870e80390742f93963da7be0b2e61_225_1.png)

图 3-26

部分的各种其他过程和例程。要确定意大利面条代码发生了什么，你必须追踪许多例程并在脑海中拼凑出它的含义。

面向对象编程可以帮助你避免这个问题，但它绝对不是灵丹妙药。事实上，当你创建深层继承层次结构时，你通常是在创建意大利面条代码，因为层次结构中的每一层不仅扩展了前一层的接口，而且几乎总是添加功能。因此，当你查看最终的 `NAFTACustomer` 类时，它可能几乎什么都不做。要弄清楚它做什么或如何表现，你必须追踪前四层类的代码，而且你可能甚至没有其中一些类的代码，因为它们可能来自你购买的其他应用程序或类库。

一方面，你有重用代码的好处；另一方面，你也有这样的缺点：一个对象的代码实际上分散在五个不同的类中。在使用继承设计系统时请记住这一点——尽可能使用最少的层级来提供所需的功能。

### 脆弱基类问题

你已经探讨了在何处适合使用继承以及在何处不适合。你还探讨了如何将继承和多个接口结合使用，以便在类中同时实现 `is-a` 和 `act-as` 关系。

前面我提到，虽然继承是一个非常强大且有用的概念，但如果使用不当也可能非常危险。你已经在对 `is-a` 关系的误用讨论中看到了这种危险，以及如何使用多个接口来避免这些问题。
