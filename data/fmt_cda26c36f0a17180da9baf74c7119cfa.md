
- 对 XAML 浏览器应用程序 (XBAPs) 的改进

让我们详细探讨 WPF 4.0 的这些特性。

## 新的 WPF 控件

在 WPF 4.0 中，添加了三个新控件：`DataGrid`、`Calendar` 和 `DatePicker`，用于开发业务应用程序。这些控件使你能够重用应用程序的代码并创建丰富的客户端和 Web 应用程序。让我们在下一节中简要介绍这些控件。

### DataGrid

`DataGrid` 是一个控件，以网格格式显示数据库表中的数据。它以行和列的形式显示数据。此外，它会根据存储在其中的数据类型自动生成列，通过设置 `ItemsSource` 属性。你可以对 `DataGrid` 控件中存储的数据执行各种操作，例如分组、排序和筛选。此外，`DataGrid` 控件使你能够在单元格和行级别执行验证。在单元格级别验证时，你可以在另一用户更新值时验证绑定数据对象（单元格）的属性。然而，在行级别验证时，你可以在另一用户修改行中的数据时验证整个数据对象（行）。

> **NOTE**
> 要了解有关 `DataGrid` 控件的更多信息，请参阅第 25 章《Windows Forms 和 WPF 应用程序中的数据绑定》。

### Calendar 控件

`Calendar` 是一个控件，允许你从可视日历中选择日期。它可以作为单独的控件使用，也可以作为 `DatePicker` 控件的下拉部分。图 9.1 显示了 WPF 应用程序 `MainWindow` 中的 `Calendar` 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_342_0.png)

**图 9.1：在 MainWindow 中显示 Calendar 控件**

> **NOTE**
> 要了解有关 `Calendar` 控件的更多信息，请参阅第 12 章《在 Windows Forms 和 WPF 中使用图形和多媒体》。

### DatePicker

`DatePicker` 是一个控件，允许你通过在文本字段中输入日期或使用下拉 `Calendar` 控件来选择日期。图 9.2 显示了 WPF 应用程序 `MainWindow` 中的 `DatePicker` 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_342_1.png)

**图 9.2：在 MainWindow 中显示 DatePicker 控件**

![](img/e073a4882197be4ab61103cbe0bcb394_344_0.png)

**图 9.3：显示按钮控件的不同状态**

`ControlTemplate` 是一个类，用于指定控件的视觉结构和行为方面，以便这些方面可以在控件的多个实例之间共享。`VisualStateManager` 类使你能够为控件指定不同的状态以及控件的外观。

### 选择和插入符号画刷

在 WPF 4.0 中，添加了两个新的画刷，`Selection` 和 `Caret`，用于突出显示选定文本和绘制光标。这些画刷在输入和阅读控件上工作，例如 `TextBox`、`RichTextBox` 和 `FlowDocumentReader`。这些画刷以 `TextBoxBase` 类的属性形式存在。这些属性如下：

- `SelectionBrush` – 创建一个画刷以突出显示选定文本
- `CaretBrush` – 创建一个画刷以绘制光标

`TextBoxBase.SelectionBrush` 和 `TextBoxBase.CaretBrush` 属性属于 `System.Windows.Controls.Primitives` 命名空间。以下是这些属性的语法：

```csharp
public Brush SelectionBrush { get; set; }
public Brush CaretBrush { get; set; }
```

以下代码片段显示了使用 `SelectionBrush` 的示例：

```xml
<TextBox SelectionBrush="Yellow" SelectionOpacity="0.8" Foreground="Green">
You are using the SelectionBrush and CaretBrush properties.
</TextBox>
```

前面的代码片段创建一个文本框并向其中添加文本，`You are using the SelectionBrush and CaretBrush properties`。我们已将 `SelectionBrush` 属性指定为黄色。注意，还有另一个属性 `SelectionOpacity`，设置为 `0.8` 以自定义选定文本的外观。图 9.4 显示了 `SelectionBrush` 属性的使用：

![](img/e073a4882197be4ab61103cbe0bcb394_344_1.png)

**图 9.4：使用 SelectionBrush 属性显示高亮文本**

以下代码片段显示了使用 `CaretBrush` 属性的示例：

```xml
<TextBox Foreground="Green" CaretBrush="Red">
You are using the SelectionBrush and CaretBrush properties.
</TextBox>
```

前面的代码片段创建一个文本框并向其中添加文本，`You are using the SelectionBrush and CaretBrush properties`。我们已将 `CaretBrush` 属性指定为红色，将 `Foreground` 属性指定为绿色。图 9.5 显示了 `CaretBrush` 属性的输出：

![](img/e073a4882197be4ab61103cbe0bcb394_344_2.png)

**图 9.5：使用 CaretBrush 属性显示红色光标**

你可以在 `SelectionCaretBrushesUse` 应用程序（可在光盘中找到）中找到使用 `SelectionBrush` 和 `CaretBrush` 属性的代码。

## 新的 WPF 文本渲染堆栈

新的 WPF 文本渲染堆栈在渲染文本时带来了文本渲染清晰度、可配置性和对国际语言的支持方面的改进。此外，用户现在可以从自动、别名、灰度或 `ClearType` 文本渲染模式中进行选择。除了这些改进之外，文本堆栈现在还包括对显示优化字符布局的支持，以便生成与 Win32/GDI 文本清晰度相当的文本。此外，新的 WPF 文本渲染堆栈现在支持使用嵌入位图的字体来代替更小尺寸的字体。

## XBAP 的改进

您现在可以访问一个脚本对象，该对象使您能够与包含托管在超文本标记语言（HTML）框架中的 XBAP 的网页进行通信。此外，您现在可以通过修改项目以启用此权限，在部署 XBAP 时为其提供完全信任权限。

现在您已经了解了 WPF 4.0 的新功能，让我们继续探索 WPF 4.0 的架构。

## WPF 4.0 架构

尽管 WPF 4.0 是 .NET Framework 4.0 的一部分，但它包含托管和非托管组件。由于 WPF 4.0 的托管组件基于通用语言运行时（CLR），因此它们利用了 CLR 的各种功能，例如跨语言集成、类型安全和安全性、调试和异常处理以及垃圾回收。WPF 4.0 的大多数功能和特性都是通过托管组件提供的。除了托管组件之外，WPF 4.0 还包含一个名为媒体集成层（MIL 或 `milcore`）的非托管组件。图 9.6 显示了 WPF 4.0 的托管和非托管组件：

![](img/e073a4882197be4ab61103cbe0bcb394_345_0.png)

**图 9.6：显示 WPF 4.0 的托管和非托管组件**

在图 9.6 中，您可以看到 WPF 4.0 由托管组件组成，即 `PresentationFramework`、`PresentationCore`、`WindowsBase` 和 CLR，以及非托管组件，例如 `milcore`、`User32`、`WindowsCodecs`、`DirectX` 和 `Kernel`。图 9.6 中阴影显示的组件是与 WPF 4.0 应用程序一起工作所需的基本组件。让我们简要讨论这四个组件。

> **NOTE**
> WPF 4.0 的 CLR、`WindowsCodecs`、`User32`、`DirectX` 和 `Kernel` 组件是 Microsoft Windows Vista 操作系统的组成部分，超出了本书的范围。

### PresentationFramework

`PresentationFramework` 组件在 .NET Framework 4.0 中实现为 `PresentationFramework.dll` 程序集。此组件提供用于控制 WPF 4.0 应用程序的外观和呈现的类。例如，WPF 应用程序中的控件、布局、动画和数据绑定都由 `PresentationFramework` 组件处理。

### PresentationCore

`PresentationCore` 组件在 .NET Framework 4.0 中实现为 `PresentationCore.dll` 程序集。此组件提供了 WPF 4.0 中最常用的一些类型和功能。`PresentationCore` 组件提供的类和类型提供了某些基本功能，例如 WPF 4.0 中的属性、事件和消息。请注意，`PresentationCore` 组件不为 WPF 4.0 应用程序的 UI 提供数据类型，如 `PresentationFramework` 组件所提供的那样。

### WindowsBase

`WindowsBase` 组件在 .NET Framework 4.0 中实现为 `WindowsBase.dll` 程序集。此组件提供了基本 WPF 功能，例如线程、类型转换器和依赖属性。其中一些功能可以在 WPF 领域之外访问和使用。

### MIL 或 Milcore

`Milcore` 是 WPF 4.0 中的一个非托管组件。`Milcore` 与 `DirectX` 交互并充当 `DirectX` 与 CLR（以及托管 WPF 组件）之间的媒介或接口。由于与 `DirectX` 的这种交互，`milcore` 允许在 WPF 4.0 应用程序中显示 2-D 以及 3-D 图形内容，并且还允许您处理动画、渲染 3-D 场景等等。`Milcore` 具有一个合成引擎，该引擎使用 `DirectX` 的硬件和软件渲染来渲染 WPF 4.0 应用程序。请注意，`milcore` 能够仅因为它是非托管组件而为 WPF 应用程序使用 `DirectX`。

让我们现在继续学习由 WPF 4.0 的托管组件提供的类。

## WPF 4.0 类层次结构

托管组件为 WPF 提供了多种类型和类。所有 WPF 类都继承自 `System.Object` 类，后者是 .NET Framework 4.0 中所有类型和类的基类。图 9.7 显示了 WPF 类层次结构，即 WPF 类之间的关系：

![](img/e073a4882197be4ab61103cbe0bcb394_346_0.png)

**图 9.7：显示 WPF 4.0 类的层次结构**

在图 9.7 中，您可以看到一些重要 WPF 4.0 类的层次结构。现在，让我们详细了解这些类。

### System.Windows.Threading.DispatcherObject 类

`DispatcherObject` 类存在于 `System.Windows.Threading` 命名空间中以管理线程。WPF 应用程序默认情况下使用两个线程运行——一个用于 UI，另一个用于渲染。UI 线程是主执行线程，获取输入和事件，而渲染线程在后台运行。

通常，对于单个 WPF 应用程序只有一个 UI 线程。然而，可能存在多个 UI 线程，即您可以在多个线程上定义 UI 元素。这种多线程 UI 定义会导致 WPF 应用程序的处理变得复杂。因此，WPF 采用单线程单元（STA）模型使应用程序单线程化。有了 STA，WPF 应用程序现在与各种浏览器（如 Internet Explorer）兼容且可互操作。在 STA 模型中，可以有多个 UI 线程，但一次只有一个 UI 线程会运行。此外，您在一个 UI 线程上创建的 UI 元素仅属于该线程，不可供其他 UI 线程使用。这种现象称为线程亲和性。

多个线程之间的交互是通过调度程序实现的，即 `Dispatcher` 类的一个实例。每个线程都有一个调度程序，用于发送和接收 `User32` 消息以执行线程。在 WPF 4.0 中，UI 线程具有一个调度程序，其工作项排队在其中。调度程序根据其优先级执行工作项。调度程序只能管理一个线程的工作项。

请注意，调度程序的引用存储在 `DispatcherObject` 类的一个实例中。继承 `DispatcherObject` 类的所有类都具有单线程亲和性。此类为您提供了某些方法，以允许您检查除创建类的对象所在的线程之外的任何线程都不访问该对象。此外，`DispatcherObject` 类是 WPF 中大多数类和 UI 元素的基类。

### System.Windows.DependencyObject 类

`System.Windows.DependencyObject` 类允许其派生类使用依赖属性系统。任何继承 `DependencyObject` 类的类都可以使用并实现依赖属性。依赖属性是 CLR 属性，由 `System.Windows.DependencyProperty` 类支持并在 WPF 属性系统中注册。依赖属性的值取决于多个因素或输入，例如 WPF 对象的样式、主题和动画。依赖属性允许您使用表达式作为属性值、绑定数据、合并动画并应用样式。您将在本章后面了解更多关于依赖属性的内容。

> **Note**
> 您可以在图 9.7 中看到 `System.Windows.Freezable`、`System.Windows.ContentElement` 和 `System.Windows.Media.Visual` 类派生自 `System.Windows.DependencyObject` 类。

### System.Windows.Freezable 类

`System.Windows.Freezable` 类允许您处理具有可编辑和只读状态的对象。`Freezable` 类还提供了在对象发生变化时支持更改通知的功能。称为可冻结对象（`Freezable` 类的实例）的对象可以具有两种状态之一——未冻结（可编辑）或冻结（只读）。默认情况下，可冻结对象处于未冻结状态并可进行更改和修改。当未冻结对象发生变化时，会生成更改通知以使更改生效。

更改通知消耗大量系统资源，有时会对 WPF 应用程序的性能产生不利影响。在这种情况下，可冻结对象可以被冻结以提高 WPF 应用程序的性能，即对象被设为只读以防止对其进行任何更改。因此，系统资源不会用于更改通知。此外，冻结对象可以在不同线程之间共享。请注意，可冻结对象在以下条件下不能被冻结：

- 对象包含任何数据绑定或动画属性
- 对象包含任何由动态资源设置的属性
- 对象包含任何其他无法冻结的对象

对象冻结后，不能再更改或解冻。但是，您可以通过克隆它来创建冻结对象的可编辑副本。然后您可以编辑或更改克隆的可编辑副本。

> **Note**
> `DispatcherObject`、`DependencyObject` 和 `Freezable` 类存在于 `WindowsBase` 程序集中。

### System.Windows.Media.Visual 类

`System.Windows.Media.Visual` 类是用于 WPF 应用程序中渲染元素的基类。`Visual` 类提供了与渲染相关的功能，例如裁剪、变换和边界框计算。您可以裁剪元素的区域，对元素应用变换，或验证某个点是否位于给定边界内。

`Visual` 类通过在 `milcore` 中生成一种树状结构，即合成树，作为托管 WPF 组件与非托管 `milcore` 组件之间的链接。您在 WPF 应用程序中使用的每个视觉元素可能对应于合成树中的零个或多个合成节点。每个合成节点都有各种外观相关属性和用于渲染元素的特定渲染指令。合成节点一次遍历一个，并在节点上执行渲染指令以合成并显示元素。请注意，合成树和节点只能通过消息协议访问。

WPF 使用保留模式渲染系统，即完整的合成树由 `milcore` 组件缓存。这意味着当任何合成节点发生变化时，只有更改才会被传达给 `milcore` 组件。这确保了屏幕的重绘更快且更优化。请注意，合成节点使用画家算法进行渲染，其中较远的节点先渲染，位于前方的节点后渲染。使用此算法，更容易、更快地渲染复杂而精细的视觉效果，例如半透明或透明视觉效果。

### System.Windows.UIElement 类

`System.Windows.UIElement` 类提供了在 WPF 4.0 应用程序中实现基本功能的 API。例如 WPF 元素的布局和事件。您可以使用 `UIElement` 类的属性和方法来操作 WPF 应用程序中视觉元素的布局。`UIElement` 类引入了一种易于使用且灵活的布局模型。

灵活的布局模型包含两个阶段，即 `Measure` 和 `Arrange`。您可以在 `Measure` 阶段确定 WPF 应用程序中 UI 元素的大小。元素的大小可以根据其他元素的大小和位置而被确定多次。在 `Arrange` 阶段，元素的最佳位置被确定。WPF 中的灵活布局模型使元素更容易改变其大小和位置，并为元素提供动态布局。`UIElement` 类还为 WPF 应用程序提供对事件、输入和命令绑定的支持。

> **NOTE**
> `Visual` 和 `UIElement` 类由 `PresentationCore` 程序集提供。

### System.Windows.FrameworkElement 类

`System.Windows.FrameworkElement` 类是 `UIElement` 类与 WPF 框架级实现元素之间的接口（您直接在 XAML 或代码隐藏文件中使用的元素）。`FrameworkElement` 类不仅包含 `UIElement` 类提供的功能，还提供额外的功能来增强 WPF 应用程序。`FrameworkElement` 类具有各种属性，可帮助您在 WPF 应用程序中对 WPF 框架级视觉元素统一灵活地应用布局和样式。它还提供支持以树的形式指定不同的视觉元素、动画和故事板、数据绑定以及事件。

`FrameworkElement` 类有多个派生类，允许您处理控件、多媒体和 3-D 内容。一些继承 `FrameworkElement` 类的类包括 `Control`、`Panel` 和 `Shape` 类。现在，让我们逐一探索这些类。

### System.Windows.Controls.Control 类
