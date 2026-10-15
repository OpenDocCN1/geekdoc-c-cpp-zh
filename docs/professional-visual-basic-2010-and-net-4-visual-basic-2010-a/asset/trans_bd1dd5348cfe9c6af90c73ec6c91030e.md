

## TABLE 5-2: XAML 标记扩展

| XAML 标记扩展 | 描述和示例 |
|---|---|
| x:Array | 用于提供数组支持。数组声明允许分配数据类型，以支持强类型和包含一系列元素。 `<x:Array Type="object"> <myObject1/> <myObject2/></x:Array>` |
| x:Null | 等同于 Visual Basic 中的 Nothing 术语，但该扩展是基于 C#/C++ 关键字 null 实现的。会将对象属性设为 null，该属性在创建时可能不是或不是默认状态。x:Null 没有附加修饰符，通常作为节点实现，而不是属性，因为它引用其父节点的数值。 `<object><object.property><x:Null/> </object.property></object>` |
| x:Reference | XAML 2010 新增，此扩展使您能够基于其命名属性在 XAML 元素之间创建引用。此扩展将允许您按名称定位标记中的另一个对象。有关更多信息，请参阅 Markup.Reference 类定义的实现。 |
| x:Static | 支持引用常量值、对象的共享属性和枚举值。与属性类似，它最常用作属性，格式为 X:static "{namespace.class}"。此扩展用于访问应用程序默认值，例如操作系统使用的系统颜色。 `<object Background="{x:Static SystemColors .ControlBrush}"></object>` |
| x:Type | 如 x:Typename 属性之前介绍的，x:Type 扩展允许在创建泛型对象时指定类型。然而它还有第二个用途：指定属性类型。因此，如果您创建具有属性的对象，则 x:Type 扩展用于指定与该属性关联的类型。 `<object><object.property> <x:Type TypeName="namespace .class"/></object.property></object>` |

不要让最后一个扩展混淆你；标记扩展有两种使用方式——要么作为大括号中包含的属性，要么作为可能包含自己的属性和属性的节点。其中一些，例如 x:Static，始终作为属性出现；其他一些，例如 x:Null 和 x:Array，始终作为节点出现；当然 x:Type 可以在任一位置找到。到目前为止，所有 XAML 语言元素都用于在 XML 定义内操作。也就是说，它们定义属性和节点，只要你理解关键字的定义，你就能理解它引用的数据。

## XAML 指令

然而，有时你需要真正引用数据。例如，前面的任何扩展都不支持将其他 XML 数据嵌入到你的 XAML 文件中或直接从 XAML 文件中引用代码。这两种功能都基于 XAML 指令可用。XAML 指令使你能够嵌入不遵循 XML 格式规则的元素。有两个这样的指令，如表 5-3 所示。

## TABLE 5-3: XAML 指令

| XAML 指令 | 描述和示例 |
|---|---|
| x:Code | 使你能够直接将 Visual Basic 代码嵌入到你的 XAML 文件中。然而，虽然你可以这样做，但不应该这样做：这是非常糟糕的编码实践——不仅因为它将代码隔离在代码后置文件之外，而且因为此类代码使 XAML 依赖于编译的语言，并且它被隔离，更难以调试和维护。然而，你可能会遇到此类元素。通常，最好将任何嵌入的代码进一步嵌套在 x:Code 块内的 CDATA 块中，如以下示例所示，以便 XAML 解析引擎不会尝试解析代码。因此，代码块看起来类似于这样： <object><x:Code> <![CDATA[ 'VB code can be enclosed by a CDATA directive Sub MyMethod() End Sub ]]></x:Code></object> |
| x:XData | 你可能想要嵌入到 XAML 文档中的第二个非标准 XAML 项是另一个 XML 文档。例如，你可能想要显示一封电子邮件消息或已转换为 XML 的 Word 文档，因此你可能希望此数据位于你的 XAML 文档中。关键点是你不希望此额外的 XML 意外使用与你的 XAML 关联的相同标签信息。因此，你需要提供一个包含根数据节点的 x:XData 指令，其中包含你的自定义数据。请注意，在大多数情况下，此示例中的对象节点将是 System.Windows.Data.XMLDataProvider 而不是 Window 或其他对象。示例如下所示： <object><x:XData> <dataItems xmlns="yourNamespace">...</dataItems><elementDataRoot> </x:XData></object> |

如上所示，XML 定义的范围，即你在 XAML 文件中看到的内容，并不复杂。你可能想知道我们已经见过的控件、窗口，甚至应用程序对象在哪里。这些项目虽然是 WPF 实现的一部分，但不是核心 XAML 语言定义的一部分。它们是 WPF 扩展，并且是为什么你添加了对 Presentation 文件夹的第二个命名空间引用的原因。你在 XAML 中看到的所有其他属于此第二类别的内容也都可以从你的 .NET 应用程序中引用。

## 使用 XAML 声明工作流

在 .NET 3.0 和 3.5 中，XAML 与 WPF 紧密耦合。从 .NET 4.0 及以后开始，Microsoft 重点放在解耦这两项，并使 XAML 语法在多个不同领域中使用，例如 WPF、WF 和 WCF。毕竟，用 XAML 标记定义 WCF 端点的关键界面元素或定义绑定到数据服务的元数据，比说明复杂工作流或界面更好的方法是什么？

在 .NET Framework 4 中，工作流中使用的 XAML 已标准化为与 WPF 使用的相同库。为了说明这一点，打开 Visual Studio 并选择 File ⇨ New Project。然后，从 resulting New Project 对话框中，如图 5-3 所示，选择 Workflow Console Application 项目类型并将名称 ProVB_WFXAML 分配给你的新项目。

![](img/d99870e80390742f93963da7be0b2e61_282_0.png)

### FIGURE 5-3

创建此新项目将使你回到 Visual Studio 中，显示当前为空工作流的默认图形视图。由于创建自定义工作流不是本章的目标，请关闭该视图并在 Solution Explorer 中右键单击 Workflow1.xaml。选择 Code 视图，你将被 Figure 5-4 所示的原始 XAML 迎接。

![](img/d99870e80390742f93963da7be0b2e61_282_1.png)

### FIGURE 5-4

虽然此 XAML 显然与你在创建窗口时看到的不同，但它非常相似。请注意，在顶层，而不是引用窗口的应用程序，你有一个

activity。如下所示的列表，它随后引用类和一个新的库 Microsoft .VisualBasic.Activities：

```
<p:Activity x:Class="Workflow1" mva:VisualBasic.Settings="Assembly references and imported namespaces serialized as XML namespaces" xmlns:mva="clr-namespace:Microsoft.VisualBasic.Activities;assembly=System.Activities" xmlns:p="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:s="clr-namespace:System;assembly=mscorlib" xmlns:sad="clr-namespace:System.Activities.Debugger;assembly=System.Activities" xmlns:sapx="clr-namespace:System.Activities.Presentation.Xaml;assembly=System.Activities.Presentation" xmlns:mv="clr-namespace:Microsoft.VisualBasic;assembly=System" xmlns:s1="clr-namespace:System;assembly=System" xmlns:s2="clr-namespace:System;assembly=System.Xml" xmlns:s3="clr-namespace:System;assembly=System.Core" xmlns:scg="clr-namespace:System.Collections.Generic;assembly=System" xmlns:scg1="clr-namespace:System.Collections.Generic;assembly=System.ServiceModel" xmlns:scg2="clr-namespace:System.Collections.Generic;assembly=System.Core" xmlns:scg3="clr-namespace:System.Collections.Generic;assembly=mscorlib" xmlns:sd="clr-namespace:System.Data;assembly=System.Data" xmlns:sdl="clr-namespace:System.Data;assembly=System.Data.DataSetExtensions" xmlns:sl="clr-namespace:System.Linq;assembly=System.Core" xmlns:st="clr-namespace:System.Text;assembly=mscorlib" xmlns:x="http://schemas.microsoft.com/winxf/2006/xaml">
</p:Activity>
```

来自 workflow1 的代码片段

与 .NET 4 相关的与工作流的新功能之一是它们包含与 Visual Basic 相关的一些应用程序特定功能。你可能需要注意的是，此相同的 Visual Basic 库也用于 C# 工作流。此功能在第 27 章中有更详细的介绍。

然而，除了这个差异之外，你应该注意，主要默认的工作流 XAML 看起来与用于窗口的 XAML 相似。这当然是重点；通过创建通用的声明性语法，并扩展该语法以支持必要的核心语言功能，Microsoft 提供了创建由功能需求驱动的界面的标准方法。

## SUMMARY

本章向你介绍了声明式编程的概念以及 XAML 作为声明式编程语言的实现。如本章所述，XAML 专注于信息和实现结果所需的转换，而 Visual Basic 更专注于实现算法和状态变化的自定义逻辑。XAML 用于定义你想要的内容，而不是让你定义系统应该做什么以及如何做。在新用户界面设计元素上下文中，XAML 描述了它是什么、它与什么关联以及应用的任何转换以正确显示关联项。作为本章的一部分，你被介绍到以下内容：

- 声明式与命令式编程
- Visual Basic 对声明式编程的原生支持
- 使用 XAML 定义窗口和简单用户界面元素
- XAML 语法
- 使用 XAML 定义工作流过程

