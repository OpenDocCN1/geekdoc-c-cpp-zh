
他们希望购买。这正是 WPF 及其数据可视化能力发挥作用的地方。

可以提供模板来定义下拉列表中每个项的呈现方式。该模板可以包含任何视觉元素，例如图像、标签、文本框、工具提示、投影等！

图 1-1 展示了一个组合框的典型显示效果。此控件有局限性：它只能向用户传达一条信息，即用于表示汽车型号的文本。可以通过一些工作，根据列表中的选择在单独的控件中显示汽车型号的图像，但这仍然要求用户先做出选择，然后才能确切看到他们正在选择什么。相比之下，WPF 可以灵活地在每个组合框项中显示多条信息，就像一站式商店一样，提供用户做出决定所需的所有信息。（有关 WPF 组合框，请参见图 1-2。）

![](img/80ff26f06fc9ab951e1cd4257b867366_593_0.png)

**图 1-1：** 一个典型的组合框。

图 1-2 展示了 WPF 中的一个示例组合框。组合框项的呈现方式通过数据模板定义。（我在本迷你书的第 3 章中介绍数据模板。）此组合框中的每个项在呈现时都会向用户提供一个视觉提示以及多个数据字段。显示所有这些信息可以使用户在做出选择时做出明智的决定。

![](img/80ff26f06fc9ab951e1cd4257b867366_593_1.png)

**图 1-2：** 可视化数据——一个 WPF 组合框。

## XAML 简介

WPF 使你能够以声明方式构建用户界面。XAML（提示：它与 camel 押韵）构成了 WPF 的基础。XAML 与 HTML 类似，因为界面元素是使用基于标记的语法定义的。

![](img/80ff26f06fc9ab951e1cd4257b867366_594_0.png)

XAML 基于 XML，因此它必须是格式良好的，这意味着所有开始标记都需要结束标记，并且文档中包含的所有元素和属性都必须严格依据指定的架构进行验证。

默认情况下，在 Visual Studio 2012 中创建 WPF 应用程序时，生成的 XAML 文件中会表示以下架构：

- `http://schemas.microsoft.com/winfx/2006/xaml/presentation`：此架构表示默认的 Windows Presentation Foundation 命名空间。
- `http://schemas.microsoft.com/winfx/2006/xaml`：此架构表示一组映射到 CLR 对象的类。

大多数 CLR 对象都可以表示为 XAML 元素（抽象基类以及 CLR 中严格用于继承目的的一些其他非抽象基类除外）。XAML 元素映射到类；特性映射到属性或事件。

在运行时处理 XAML 元素时，会调用其基础类的默认构造函数，并实例化该对象；其属性和事件会根据 XAML 中指定的特性值进行设置。

我坚信，熟练使用 WPF 和 XAML 的最佳方式就是直接动手尝试。下一节将回顾更多 XAML 基础知识，并让你踏上 WPF 应用程序开发之路。

## 开始动手！创建你的第一个 WPF 应用程序

现在是时候放松一下了：停一会儿，去拿一杯含咖啡因的饮料，坐在舒适的椅子上，拉近电脑，准备好开始吧！

要创建你的第一个项目，请按以下步骤操作：

- 1. 打开 Visual Studio 2012。
- 2. 通过选择“文件 ⇒ 新建项目”创建新项目。
- 3. **在树中的 Visual C# 部分下的“已安装模板”区域中，单击“Windows”项。**
- 4. **从窗口中央的模板列表框中，选择“WPF 应用程序”。**
- 5. **在“名称”文本框中，输入 MyFirstWPFApplication。**  
  这还会将解决方案的名称设置为相同的值，这没问题（见图 1-3）。
- 6. **单击“确定”。**

Visual Studio 现在会自行完成工作，创建应用程序的解决方案结构。默认情况下，如图 1-4 所示，WPF 应用程序模板会创建两个 XAML 文件及其各自的代码隐藏文件：App.xaml（App.xaml.cs）和 MainWindow.xaml（MainWindow.xaml.cs）。

App.xaml 表示应用程序的入口点。这里定义了应用程序范围（全局范围）的资源和启动窗口（参见清单 1-1）。

资源是可重用对象的键控集合。可以使用 XAML 和 C# 创建和检索资源。资源可以是任何内容——数据模板、字符串数组，或用于为文本框背景着色的画笔。资源也是有范围的，这意味着它们可供整个 Application（全局）、Window、User Control，甚至仅可供特定控件使用。

![](img/80ff26f06fc9ab951e1cd4257b867366_595_0.png)

**图 1-3：** 在“新建项目”对话框中创建项目。

![](img/80ff26f06fc9ab951e1cd4257b867366_595_1.png)

**图 1-4：** WPF 应用程序解决方案结构。

![](img/80ff26f06fc9ab951e1cd4257b867366_596_0.png)

### 清单 1-1：App.xaml

```xml
<Application x:Class="MyFirstWPFApplication.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
    </Application.Resources>
</Application>
```

清单 1-1 显示了 Visual Studio 中 WPF 应用程序模板生成的 XAML。请注意，其中定义了 WPF 命名空间。表示 CLR 对象的命名空间将在 XAML 文件中用 x: 前缀加以区分。

StartupUri 值定义了应用程序执行后将显示的窗口。在此示例中，将显示 MainWindow.xaml 窗口。

x:Class 特性定义了此 XAML 文件的 C# 代码隐藏文件。如果打开 App.xaml.cs，你会看到其类名为 App，并且它继承自 Application 类（它是 XAML 文件的根元素）。

![](img/80ff26f06fc9ab951e1cd4257b867366_596_1.png)

C# 使用命名空间来组织和定位类。为了从特定命名空间创建对象，需要在类定义顶部使用“using”语法。与 C# 类似，XAML 也要求你声明文档中使用了哪些命名空间。命名空间通常定义为文档根元素内的一个特性：根元素是 XAML 文档中的第一个 XML 标记。XAML 使用 XML 语法定义命名空间——“xmlns”表示“XML namespace（XML 命名空间）”，它通常后跟冒号（:），然后是一个别名。此别名是该命名空间在整个 XAML 文档中的简写引用；你可以使用它来实例化该命名空间中某个类的对象。

例如，如果要从程序集 `MyTemplates.dll` 中添加命名空间 `MyTemplates.DataTemplates`，可以将命名空间定义为

`xmlns:myDTs="clr-namespace:MyTemplates.DataTemplates;assembly=MyTemplates.dll"`

然后，你就可以按如下方式从 MyTemplates.DataTemplates 命名空间实例化对象：

`<myDTs:MyClass></myDTs:MyClass>`

### 声明应用程序范围资源

为了演示全局应用程序范围资源的创建和使用，在本节中，你将创建一个资源，用于保存应用程序中使用的一个字符串。应用程序范围资源可供项目中定义的所有窗口和用户控件使用。请按以下步骤操作：

- 1. 添加位于 `mscorlib.dll` 程序集中的 `System` 命名空间。`String` 类就位于此处。
- 2. 为此，请将以下命名空间添加到 `App.xaml` 根元素：  
  `xmlns:sys="clr-namespace:System;assembly=mscorlib"`  
  现在，`String` 类可在整个 `App.xaml` 文档中使用。
- 3. 在 `Application.Resources` 标记之间创建资源，并添加以下 `String` 类元素：  
  `<sys:String x:Key="Purpose">Hello WPF World!</sys:String>`  
  此元素实例化一个 `String` 类型的对象，将其初始化为值 Hello WPF World!，并使用键 `Purpose` 进行键控。现在，通过请求资源“Purpose”，该资源可在整个 `MyFirstWPFApplication` 应用程序中使用（参见清单 1-2）。

### 清单 1-2：定义了资源和 System 命名空间的更新后 App.xaml

```xml
<Application x:Class="MyFirstWPFApplication.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:sys="clr-namespace:System;assembly=mscorlib"
    StartupUri="MainWindow.xaml">
    <Application.Resources>
        <sys:String x:Key="Purpose">Hello WPF World!</sys:String>
    </Application.Resources>
</Application>
```
