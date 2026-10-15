

为控件定义一组通用样式并在应用程序中应用它们。WPF 样式可以设置任何 Dependency 属性并使用它来应用非格式特性，例如控件的行为。WPF 样式还使用模板来定义控件的外观。

在本节中，你将学习关于：

- WPF 中使用的样式
- WPF 中使用的不同类型的模板

## WPF 4.0 中的样式

WPF 中的样式允许你将一组属性应用于多个元素。例如，你可以通过更改其 FontSize 和 FontFamily 属性来更改 TextBlock 控件的样式。但是，如果你希望你的 TextBlock 控件共享某些属性，你可以为它们创建一个通用样式。

你可以通过使用 Style 属性将样式绑定到控件。样式设置元素的初始外观；然而，你可以覆盖在样式中设置的属性。样式相对于资源具有一些优势。样式允许你创建相关设置的组。它还通过使应用这些设置变得更容易来简化你的标记。Style 类的继承层次结构为：

```
System.Object
System.Windows.Threading.DispatcherObject
System.Windows.Style
```

你可以通过使用以下代码片段将 Style 类添加到你的 WPF 应用程序中：

```
<Style>
    <!-- Setters -->
</Style>
```

表 10.52 描述了 Style 类的 noteworthy 属性：

**Table 10.52: Showing the Noteworthy Properties of the Style Class**

| Property | Description |
| --- | --- |
| Setters | Sets the property values and attaches event handlers |
| Triggers | Allows you to change a style setting |
| Resources | Gets or sets a collection of resources you can use with your style |
| BasedOn | Creates a specialized style that inherits the settings of another style |
| TargetType | Gets or sets the type for which the style is intended |

如果你想创建更具体的样式，你可以使用容器控件的 resources 集合来定义它们，例如 Grid 控件或 StackPanel 控件。如果你想在整个应用程序中重用样式，你可以使用应用程序的 Resources 集合来定义它。你可以为派生自 FrameworkElement 或 FrameworkContentElement 类的任何元素设置样式。样式最常见的是作为资源声明。样式声明由包含一个或多个 Setter 对象的 Style 对象组成。每个 Setter 对象由 Property 和 Value 属性组成。你将在本章的 Immediate Solutions 部分学习如何使用样式。

## 模板

WPF 中的模板允许你自定义控件的外观和感觉。WPF 中的模板派生自 FrameworkTemplate 基类。WPF 中有两种类型的模板：ControlTemplate 和 DataTemplate。ControlTemplate 模板负责指定控件的视觉结构；而 DataTemplate 模板负责对象的图形表示。

## 触发器

Triggers 类定义了你想要应用于控件的样式类型。它们是条件设置的。例如，你可以在鼠标悬停在按钮上时更改按钮的背景颜色。触发器还可以通过 BasedOn 属性通过派生样式继承属性。触发器通过 Style.Triggers 集合链接到样式。每个样式可以有无限数量的触发器，每个触发器都是派生自 System.Windows.TriggerBase 命名空间的类的实例。

你也可以通过使用 FrameworkElement.Triggers 集合直接将触发器应用于元素，而无需创建样式。此触发器集合仅支持事件触发器。WPF 中使用的不同类型的触发器是：

- Property triggers
- Event triggers

让我们在以下各节中详细了解它们。

### 属性触发器

PropertyTrigger 触发器在属性值更改时做出反应。你可以通过两种方式将操作附加到 PropertyTrigger 触发器。首先，你可以使用 Trigger.EnterActions 属性设置在属性更改为你指定的值时执行的操作。其次，你可以使用 Trigger.ExitActions 属性设置在属性更改回其原始值时执行的操作。你将在本章的 Immediate Solutions 部分了解有关 PropertyTrigger 触发器的实际应用的更多信息。

### 事件触发器

PropertyTrigger 触发器与 EventTrigger 触发器之间的主要区别在于，虽然 PropertyTrigger 触发器等待属性更改发生，但 EventTrigger 触发器等待特定事件被触发。EventTrigger 触发器需要一系列修改与其附加的控件的操作。这些操作用于应用动画。EventTrigger 触发器特别基于事件的发生开始一组操作。当你使用 EventTrigger 触发器时，你需要选择不会干扰控件固有行为的事件。

EventTrigger 类的继承层次结构如下：

```
System.Object
  System.Windows.Threading.DispatcherObject
    System.Windows.DependencyObject
      System.Windows.TriggerBase
        System.Windows.EventTrigger
```

你可以通过使用以下代码片段将 EventTrigger 类添加到 WPF 应用程序中：

```
<EventTrigger>
  <!--Actions-->
</EventTrigger>
```

你将在本章的 Immediate Solutions 部分了解有关 EventTrigger 触发器的实际应用的更多信息。

> **NOTE**
> 除了属性和事件触发器之外，还有其他类型的触发器。MultiTrigger 触发器允许你基于多个条件设置属性值。当控件的属性是数据绑定的时，你可以使用 DataTrigger 或 MultiDataTrigger 触发器。

## WPF 命令

命令是 WPF 中的一种输入机制，为处理输入数据提供了一种方式。命令的常见示例包括 Cut、Copy 和 Paste。WPF 中的命令基于 RoutedCommand 和 RoutedEvent 类。命令与简单事件处理程序之间的主要区别在于命令将操作与其逻辑分离。在 WPF 中使用命令的最简单方法是使用来自命令库类之一的预定义 RoutedCommand 类。

### 命令源

命令源触发命令。例如，Button 或 MenuItem 控件可以是命令源。WPF 中的命令源实现 ICommandSource 接口。

表 10.55 描述了 ICommandSource 接口的属性：

**Table 10.55: Properties of the ICommandSource Interface**

| Property | Description |
| --- | --- |
| Command | Executes when a command source is invoked |
| CommandTarget | Retrieves the Command object on which the command is executed |
| CommandParameter | Passes information to the handlers implementing a command |

ICommandSource 接口的 CommandTarget 属性仅在 ICommand 接口是 RoutedCommand 类时才适用。例如，如果在 ICommandSource 接口上设置了 CommandTarget 属性并且相应的命令不是 RoutedCommand 类，则命令目标将被忽略。

实现 ICommandSource 接口的 WPF 类是 ButtonBase、MenuItem 和 Hyperlink。这些类在被点击时调用命令。CanExecuteChanged 事件通知命令源命令执行当前命令的能力。命令源通过使用 CanExecute() 方法查询 RoutedCommand 类的当前状态，并在命令无法执行时禁用自身。当命令可用时，命令源会自动启用，当命令不可用时禁用。

### 命令目标

命令目标是执行命令的元素。命令源可以设置命令目标。如果未定义命令目标，则当前控件将用于命令目标。例如，如果 MenuItem 控件在具有 TextBox 控件和 PasswordBox 控件的应用程序中调用 Paste 命令，则目标可以是两个控件中的任何一个，具体取决于当前控件。

### 命令绑定

命令绑定将命令链接到特定 UI 区域的相关应用程序逻辑。WPF 中的命令绑定由 CommandBinding 类表示，该类包含 Command 属性，例如 PreviewExecuted、Executed 和 PreviewCanExecute。CommandBinding 类很重要，因为单个命令可能在应用程序的多个位置使用，并且在每个位置具有不同的意义。因此，你可以使用不同的命令绑定在应用程序的不同位置使用命令。

## Windows Forms 与 WPF 4.0 应用程序之间的互操作性

无需重写 WPF 的设计视图，你就可以在 WPF 应用程序中使用现有的 Windows Forms 控件，并在 Windows Forms 应用程序中使用新的 WPF 控件。要集成 Windows Forms 和 WPF，你需要来自 System.Windows.Forms.Integration 命名空间的类。此命名空间包含支持 Windows Forms 和 WPF 控件互操作的类。当你使用此命名空间的类时，你可以在 WPF 页面上托管 Windows Forms 控件，并在基于 Windows Forms 的应用程序中托管 WPF 元素。

表 10.56 描述了 System.Windows.Forms.Integration 命名空间的类：

**Table 10.56: Classes of the System.Windows.Forms.Integration Namespace**

| Class | Description |
| --- | --- |
| ChildChangedEventArgs | Provides data for the WindowsFormsHost.ChildChanged and ElementHost.ChildChanged events |
| ElementHost | Hosts a WPF control, which is a Windows Forms control |

