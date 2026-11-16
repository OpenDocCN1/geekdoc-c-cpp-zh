
## 将其整合

实现WPF路由事件的机制与你在上一章中学习的依赖属性机制几乎相同。

依赖属性使用DependencyProperty类型的字段封装了一个POCO属性。

WpfClass
Class
→ Window

Fields
◆ WpfDpProperty : DependencyProperty
◆ WpfRoutedEvent : RoutedEvent

Properties
▣ WpfDp : int

Events
⚡ WpfRouted : RoutedEventHandler

路由事件使用RoutedEvent类型的字段封装了一个POCO事件。

与依赖属性一样，RoutedEvent是一个独立的类，继承自DependencyObject。

RoutedEvent
Sealed Class

Properties
▣ HandlerType
▣ Name
▣ OwnerType
▣ RoutingStrategy

Methods
⚡ AddOwner

每个WPF对象都有一个从UIElement继承的CommandBindings属性，UIElement是FrameworkElement的基类。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_637_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_637_1.png)

UIElement.CommandBindings是CommandBinding对象的集合。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_637_2.png)

CommandBinding位于Command和对象之间。可以为同一个Command注册多个CommandBinding对象，从而允许同一命令在多个位置使用。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_637_3.png)

与对象关联的Command的引用存储在CommandBinding.Command属性中。

命令实现ICommand接口，该接口定义了两个方法和一个事件。我们将在几页后详细探讨它们，但基本上CanExecute()告诉WPF命令当前是否可用，而Execute()则执行...命令所做的任何操作。

## 任务列表

在本章中，我们将探讨WPF对象如何通过WPF属性和事件系统以及特殊的命令类进行通信和交互，这些命令类允许你集中管理应用程序行为。

### 路由事件

POCO事件允许感兴趣的一方通过为其创建处理程序来注册对事件的兴趣。POCO事件被称为直接事件，因为事件直接发送到处理程序，然后就结束了。在WPF中，事件可以以这种方式处理，但它们也可以从引发事件的对象向上冒泡到逻辑层次结构中的所有祖先，或从根元素向下隧道到引发对象。它们甚至可以通过PreviewEvent/Event对双向移动。在任何级别，事件都可以被处理或传递到下一级。

### 命令

大多数应用程序提供多种不同的方式来执行常见任务。以基本文本编辑为例。在大多数文本编辑器中，你可以选择一段文本并将其复制到剪贴板，方法是从“编辑”菜单中选择“复制”，或从右键单击选择时显示的上下文菜单中选择，或单击工具栏或功能区上的按钮，或键入键盘快捷键（按惯例为Ctrl+C）。在标准.NET应用程序中，你需要编写实际执行复制的代码，然后为每个事件编写代码来调用复制。这需要大量代码。还有诸如在未选中任何内容时禁用命令之类的事情。又是一大堆代码。在WPF中，所有这些行为都被抽象为一组以ICommand接口和CommandBindings集合为中心的类，该集合将对象与其应执行的命令关联起来。为了使事情更加容易，FCL定义了一组路由命令，其中包括应用程序执行的大多数标准操作（包括位于ApplicationCommands类中的Copy）。

## 独立练习

在我们探讨WPF为POCO事件系统添加的功能之前，花一分钟回顾一下事件如何映射到我们在第14章中探讨的观察者模式。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_639_0.png)

### 声明事件

第一步是在将引发事件的类中声明事件和处理程序委托，这并不正式属于观察者模式。声明名为MyEvent且使用默认System.EventArgs的事件的C#代码是：

为处理程序声明委托的语法是：

### 注册

观察者模式的第一个正式步骤是观察者注册对事件的兴趣。在C#中，有一些语法糖可以简化此操作。要将名为MyHandler的委托方法添加到MySubjectClass.MyEvent事件，你将使用以下语法：

### 通知

观察者模式的第二个步骤是在事件发生时通知观察者。按惯例，事件在名为On<Event>(<EventArgs> e)的方法中引发。给定一个名为MyEvent且使用MyEventArgs的事件，引发事件的方法的语法将是：

### 注销

观察者模式的最后（可选）步骤是观察者让主题知道它不再对事件感兴趣。C#提供了一些语法糖来注销处理程序。使用什么运算符来实现这一点？

## 路由事件...

大多数应用程序都是事件驱动的，POCO事件系统工作得相当好。但将其与此现实情况进行比较：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_640_0.png)

在传统厨房中，副厨师长（发音为“sue chef”）在订单分配给线路厨师准备之前检查订单，然后在订单提供给顾客之前再次检查订单。

如果我们要对这个过程进行建模，OrderPlaced 和 ItemPrepared 事件都会首先发送到 SousChef 类，该类将不得不为流程中的下一步引发其他事件。

每个 LineChef 都必须为 ItemAssigned 事件注册处理程序，而 SousChef 类必须为每个 LineChef 的 ItemPrepared 事件注册处理程序（这意味着 SousChef 必须了解每个 LineChef 实例，这本身也带来了问题）。

开始看起来相当复杂，不是吗？

## ...解决一个问题

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_641_0.png)

现在想象将同样的情况应用于WPF应用程序。

WPF Button 的默认结构由一个包含 Border 的 Grid 组成，而 Border 又包含 ContentPresenter。当用户单击按钮时，鼠标实际上可能位于这些对象中的任何一个之上。那么是谁引发了事件？你真的想为 Button、Grid、Border 和 ContentPresenter 注册相同的事件处理程序吗？我想你不想。

如果 Button.Content 设置为一个默认由 Grid、Border、ScrollViewer 和带有各自组件的 StackPanel 组成的 ListBox，那又会怎样？你想注册多少次该处理程序？

正如我们在第21章中将发现的，情况甚至更加复杂。Button 不必具有这种逻辑结构。它甚至可以在运行时更改其结构。因此，即使你愿意注册所有这些事件处理程序，你也无法知道哪些对象可能会引发事件。

当然，WPF的架构师们考虑到了这个问题，并提供了一个简洁的解决方案：路由事件。路由事件可以在元素树中上下传递，并可以在最合适的级别进行处理。让 Button 引发 Click 事件。这很合理、高效，并将逻辑动作（单击了按钮）与丑陋的细节（鼠标位于 ScrollViewer 内的 StackPanel 内的 ListItem 内……）分离开来。

## 路由策略

路由事件可以在元素树中上下传递，也可以表得有点像POCO事件，直接发送到特定类。从树顶部开始并向下移动的事件称为隧道事件，从事件源开始并向上移动的事件称为冒泡事件，而根本不移动的事件称为直接事件。

按惯例，隧道事件命名为 . . . Preview<Event>。

隧道事件从树顶部开始并向下移动。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_642_0.png)

冒泡事件从事件源开始并沿元素树向上移动。

与POCO事件一样，直接事件根本不移动。
