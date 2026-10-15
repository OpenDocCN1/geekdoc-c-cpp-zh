
来自 `Application.xaml` 的代码片段

这是一个很好的地方，可以稍作停顿来讨论 XAML 的基础知识。正如你所见，此文件以对 `Application` 节点的属性作为 `x:Class` 声明的引用开始。`x:` 代表一个别名，类似于你在 Visual Basic 中找到的别名，其中 `x:` 表示 `Class` 在模式 http://schemas.microsoft.com/winfx/2006/xaml 中定义，即 XAML 模式。你会注意到还有第二个声明用于 http://schemas.microsoft.com/winfx/2006/xaml/presentation。这个第二个声明是引用实际 WPF 库的那个。`Application` 节点属性中的最后一项是 `StartupUri`。此属性告诉编译器，当此应用程序启动时，下一步是打开 `MainWindow.xaml` 文件以找到要显示的窗口的定义。

类似于传统的 Windows Forms 应用程序，应用程序实际上并不定义一个窗口；相反，它定义了应用程序上下文，然后调用另一个类来创建窗口。然而，此文件是添加将在整个应用程序中应用的 XAML 资源的好地方。术语 `Resources` 指的是使用 XAML 可以声明对象的属性的方式。例如控件的颜色、形状和行为（以悬停、鼠标按下等形式）。

将这些 XAML 声明放在应用程序定义的 `Application.Resources` 部分中是跨应用程序中所有该类型控件共享它们的自然方式；但共享资源的细节在第 18 章中介绍。

### XAML 语法

`ProVB_XAML` 示例目前还没有什么用途，但它使得在上下文中讨论 XAML 变得更容易。下一步是更详细地查看 XAML 究竟是什么以及它与 WPF 的关系。XAML 是一种基于标记的协议。类似于 SOAP 和其他几种基于 XML 的格式，XAML 规范描述了一种可能开放的标准，用于描述用户界面元素。

无论 XAML 是否最终真正成为开放标准，微软都使用至少两个 XML 命名空间实现了 WPF。正如关于 `Application.xaml` 文件所述，一个命名空间专注于 XAML 的定义，第二个命名空间专注于 WPF 的自定义类。回到 `ProVB_XAML` `Application.xaml` 文件，包含以下命名空间声明：

```xml
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
```

前一行类似于 XML 的 `Imports` 语句，因为它指示将在关联 XML 文件中使用的节点和关键字集合。在这种情况下，`winfx/2006/xaml/presentation` 命名空间包含 WPF 的定义——不是 XAML 关键字的定义，而是 WPF 的定义。`presentation` 命名空间中包含的类是 WPF 的 .NET 实现。

要开始使用 XAML 标准的一部分的命令和控件，使用第二个命名空间引用：

```xml
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
```

此第二个引用用于所有 XAML 文件，以声明实际的 XAML 语言标准。根据惯例，它被别名为 `x:`。对于那些可能没有做过太多 XML 开发的人来说，这意味着在 XAML 中你会看到诸如 `x:Class`、`x:Code` 和其他类似节点之类的东西。`x:` 是必需的，以指示其后跟的是 XAML 语言的元素，而不是例如 WPF 或其他 .NET 库。`x:` 节点是实际的 XAML 声明。重要的是要记住 XAML 命名空间可以并且确实被用于 WPF 以外的事物。正如你在第 26 章中看到的那样，Windows Workflow Foundation 基于 XAML；它有自己的 `workflows` 命名空间。

.NET 4 框架引入的一项更改是，与原始 XAML 类不同，这些类嵌入在 `PresentationFramework.dll` 库中，并依赖于 `WindowsBase` 库，核心类现在已移至自己的单独 `System.Xaml.dll` 库中，仅依赖于 `mscorlib`、`System` 和 `System.Xml`。这有助于扩展核心 XAML 语言的原始语法和功能。

请注意，截至本文撰写时，没有计划让所有 XAML 语言功能与 Visual Studio 2010 编译器一起工作。如果你想利用尖端的 XAML 2009 功能，你需要利用未编译的 XAML。这可以通过将项目构建操作从 `Page` 设置为 `Resource` 来实现，你的 XAML 将在运行时动态解释。

### XAML 语言基础

XAML 被定义为一种语言，由一组元素、属性和相关对象组成。这些对象来自 XAML 命名空间，根据惯例每个类前都有 `x:`。.NET 扩展并将这些声明性结构映射到 .NET。

在进入语法之前，先看看 XAML 命名空间中你会找到的三种 XML 语句类别：

- attribute
- markup extension
- XAML directive

前述每一项都是在下面各节中更详细讨论的语言元素的一个独立类别。

#### Attributes

在 XML 中，属性是指与给定 XML 节点关联的命名属性。因此，XML 节点对象可能具有 `Name`、`Margin`、`Text` 等几个属性与之关联。这些属性在 XML 中位于 XML 节点的定义内。它们不包含在 XML 节点中，而是在其定义中，如下所示：

```xml
<object Name="anObject"></object>
```

在 XAML 中，属性列表包括表 5-1 中的那些。请注意，在以下示例片段中，“`object`”一词可以用几种 WPF 对象之一替换，包括 `Application`、`Window`、`Button`、`Brush` 等。

**Table 5-1: XAML Attributes**

| XAML ATTRIBUTES | DESCRIPTION AND EXAMPLE |
|---|---|
| `x:Class` | 用于引用 XAML 文档的根类。每个文档可以与单个根对象关联。`<object x:Class="Window"></object>` |
| `x:ClassModifier` | 修改给定 XAML 文档的类定义。具体来说，它使你能够指示给定类不提供公共接口。Public 是默认值。`<object x:Class="Window" x:ClassModifier="Friend"></object>` |
| `x:FieldModifier` | 与类不同，类默认是公共的，对象中的字段默认使用 Friend 修饰符分配。如果你已在 XAML 中添加了一个对象，希望它可供其他类（在你的代码隐藏中）使用，则 `FieldModifier` 需要用 Friend 修饰符声明此字段。此属性只能与此处显示的具有 `x:Name` 属性的对象一起使用：`<object x:Name="LoginWindow" x:FieldModifier="Public"></object>` |
| `x:Key` | 一些对象，如 `Dictionary` 对象和其他集合对象，允许通过键索引项目。这样的键必须命名，此属性用于提供唯一的键名。请注意，大多数 XAML 应用程序利用资源字典，这是此属性的常见用途。键需要在其适用的对象范围内是唯一的。`<object.Resources> <SolidColorBrush x:Key="string"/></object.Resources>` |
| `x:Name` | 类似于键，但用于在应用程序范围内命名对象。这样的对象默认不是公共的，但通常代表你的应用程序使用的控件和相关用户界面对象。`<object x:Name="LoginWindow"></object>` |
| `x:Shared` | 这实际上映射到 Visual Basic 用户理解的 Shared 关键字含义。默认情况下，如果你的应用程序从 XAML 资源请求一个对象，那么你将获得所请求资源相同实例。你可以使用此属性，使得每次请求给定对象时都会创建一个该对象的新实例。`<ResourceDictionary><object x:Shared="false" /></ResourceDictionary>` |
| `x:Subclass` | 此属性可与 `x:Class` 声明结合使用。它本质上使你的 XAML 能够从另一个类继承；然而，作为 Visual Basic 用户，你不会使用此属性，因为你可以在与你的类关联的代码隐藏源文件中以更自然的方式执行此操作。`<object x:Class="class" x:Subclass="namespace.subclass"></object>` |
| `x:TypeArguments` | 此属性使你能够创建 `x:Type` 标记扩展的集合。此集合充当泛型类的构造函数的参数，以确保使用构造函数定义关联的类型。此属性必须与类声明一起使用，并且关联的类必须是泛型。此属性在 XAML 2009 中得到扩展，去除了此必须与类声明一起使用的限制。`<object x:Class="PageFunction" x:TypeArguments="{x:Type type1}"></object>` |

请注意，前述属性中没有一个实际上作为节点在 XML 中引用。相反，它们修改与节点关联的属性。因此，属性是修饰符，而不是下一类别的元素：标记扩展。正如名称 Extensible Application Markup Language 中“extensible”一词所暗示的那样，此模型的一个特性是格式允许定义扩展。这些扩展扩展了与该标记定义关联的基础元素。XAML 包含有限数量的此类扩展。与属性不同，标记扩展可用于创建 XML 节点或 XML 属性集合。当用于创建节点时，标记扩展允许在该节点内定义属性值。当用于允许创建属性集合时，它可以通过周围的大括号识别，如前述 `TypeArguments` 定义所示。

#### Markup Extensions

XAML 的标记扩展在表 5-2 中显示。

**Table 5-2: XAML 标记扩展**

| XAML 标记扩展 | 描述和示例 |
|---|---|
| `x:Array` | 用于提供数组支持。数组声明允许分配数据类型，以支持强类型和包含一系列元素。`<x:Array Type="object"> <myObject1/> <myObject2/></x:Array>` |
| `x:Null` | 等同于 Visual Basic 中的 `Nothing` 术语，但该扩展是基于 C#/C++ 关键字 `null` 实现的。会将对象属性设为 `null`，该属性在创建时可能不是或不是默认状态。`x:Null` 没有附加修饰符，通常作为节点实现，而不是属性，因为它引用其父节点的数值。`<object><object.property><x:Null/> </object.property></object>` |
| `x:Reference` | XAML 2010 新增，此扩展使您能够基于其命名属性在 XAML 元素之间创建引用。此扩展将允许您按名称定位标记中的另一个对象。有关更多信息，请参阅 `Markup.Reference` 类定义的实现。 |
| `x:Static` | 支持引用常量值、对象的共享属性和枚举值。与属性类似，它最常用作属性，格式为 `X:static "{namespace.class}"`。此扩展用于访问应用程序默认值，例如操作系统使用的系统颜色。`<object Background="{x:Static SystemColors .ControlBrush}"></object>` |
| `x:Type` | 如 `x:Typename` 属性之前介绍的，`x:Type` 扩展允许在创建泛型对象时指定类型。然而它还有第二个用途：指定属性类型。因此，如果您创建具有属性的对象，则 `x:Type` 扩展用于指定与该属性关联的类型。`<object><object.property> <x:Type TypeName="namespace .class"/></object.property></object>` |

不要让最后一个扩展混淆你；标记扩展有两种使用方式——要么作为大括号中包含的属性，要么作为可能包含自己的属性和属性的节点。其中一些，例如 `x:Static`，始终作为属性出现；其他一些，例如 `x:Null` 和 `x:Array`，始终作为节点出现；当然 `x:Type` 可以在任一位置找到。到目前为止，所有 XAML 语言元素都用于在 XML 定义内操作。也就是说，它们定义属性和节点，只要你理解关键字的定义，你就能理解它引用的数据。

### XAML 指令

然而，有时你需要真正引用数据。例如，前面的任何扩展都不支持将其他 XML 数据嵌入到你的 XAML 文件中或直接从 XAML 文件中引用代码。这两种功能都基于 XAML 指令可用。XAML 指令使你能够嵌入不遵循 XML 格式规则的元素。有两个这样的指令，如表 5-3 所示。

**Table 5-3: XAML 指令**

| XAML 指令 | 描述和示例 |
|---|---|
| `x:Code` | 使你能够直接将 Visual Basic 代码嵌入到你的 XAML 文件中。然而，虽然你可以这样做，但不应该这样做：这是非常糟糕的编码实践——不仅因为它将代码隔离在代码后置文件之外，而且因为此类代码使 XAML 依赖于编译的语言，并且它被隔离，更难以调试和维护。然而，你可能会遇到此类元素。通常，最好将任何嵌入的代码进一步嵌套在 `x:Code` 块内的 `CDATA` 块中，如以下示例所示，以便 XAML 解析引擎不会尝试解析代码。因此，代码块看起来类似于这样：`<object><x:Code> <![CDATA[ 'VB code can be enclosed by a CDATA directive Sub MyMethod() End Sub ]]></x:Code></object>` |
| `x:XData` | 你可能想要嵌入到 XAML 文档中的第二个非标准 XAML 项是另一个 XML 文档。例如，你可能想要显示一封电子邮件消息或已转换为 XML 的 Word 文档，因此你可能希望此数据位于你的 XAML 文档中。关键点是你不希望此额外的 XML 意外使用与你的 XAML 关联的相同标签信息。因此，你需要提供一个包含根数据节点的 `x:XData` 指令，其中包含你的自定义数据。请注意，在大多数情况下，此示例中的对象节点将是 `System.Windows.Data.XMLDataProvider` 而不是 `Window` 或其他对象。示例如下所示：`<object><x:XData> <dataItems xmlns="yourNamespace">...</dataItems><elementDataRoot> </x:XData></object>` |

如上所示，XML 定义的范围，即你在 XAML 文件中看到的内容，并不复杂。你可能想知道我们已经见过的控件、窗口，甚至应用程序对象在哪里。这些项目虽然是 WPF 实现的一部分，但不是核心 XAML 语言定义的一部分。它们是 WPF 扩展，并且是为什么你添加了对 `Presentation` 文件夹的第二个命名空间引用的原因。你在 XAML 中看到的所有其他属于此第二类别的内容也都可以从你的 .NET 应用程序中引用。

### 使用 XAML 声明工作流

在 .NET 3.0 和 3.5 中，XAML 与 WPF 紧密耦合。从 .NET 4.0 及以后开始，Microsoft 重点放在解耦这两项，并使 XAML 语法在多个不同领域中使用，例如 WPF、WF 和 WCF。毕竟，用 XAML 标记定义 WCF 端点的关键界面元素或定义绑定到数据服务的元数据，比说明复杂工作流或界面更好的方法是什么？

在 .NET Framework 4 中，工作流中使用的 XAML 已标准化为与 WPF 使用的相同库。为了说明这一点，打开 Visual Studio 并选择 File ⇨ New Project。然后，从 resulting New Project 对话框中，如图 5-3 所示，选择 Workflow Console Application 项目类型并将名称 `ProVB_WFXAML` 分配给你的新项目。

![](img/d99870e80390742f93963da7be0b2e61_282_0.png)

#### FIGURE 5-3

创建此新项目将使你回到 Visual Studio 中，显示当前为空工作流的默认图形视图。由于创建自定义工作流不是本章的目标，请关闭该视图并在 Solution Explorer 中右键单击 `Workflow1.xaml`。选择 Code 视图，你将被 Figure 5-4 所示的原始 XAML 迎接。

![](img/d99870e80390742f93963da7be0b2e61_282_1.png)

#### FIGURE 5-4

虽然此 XAML 显然与你在创建窗口时看到的不同，但它非常相似。请注意，在顶层，而不是引用窗口的应用程序，你有一个 `activity`。如下所示的列表，它随后引用类和一个新的库 `Microsoft .VisualBasic.Activities`：
