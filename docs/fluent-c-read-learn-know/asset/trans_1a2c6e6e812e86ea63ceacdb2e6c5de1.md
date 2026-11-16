

## 事件参数

当我们在第14章探讨POCO事件时，我们看到在.NET中，一个事件始终接收两个参数：第一个是引发事件的对象，第二个是System.EventArgs或其后代之一的实例。使用路由事件时，这种基本模式不会改变，但第二个参数将是RoutedEventArgs或其后代之一的实例（RoutedEventArgs本身继承自EventArgs）。与POCO事件一样，参数可以告诉你很多关于事件的信息，而使用路由事件时，它还可以让你控制事件的行为。以下是RoutedEventArgs层次结构的一个分支：

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_643_0.png)

### 动动脑筋

你认为handled属性的作用是什么？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_643_1.png)

MSDN表示InputEventArgs用于“与输入相关的事件”。你认为这些是什么？

Source是RoutedEvent的参数之一。你认为RoutedEventArgs类为什么要添加两个额外的源属性？

## 做得怎么样？

你认为Handled属性的作用是什么？

如果在事件处理程序中将Handled设置为true，事件将停止隧道传递或冒泡。（但有办法绕过这一点，你将会看到。）

MSDN表示InputEventArgs用于“与输入相关的事件”。你认为那些是什么？

输入事件是由真实用户通过键盘、鼠标、触控笔或其他任何方式与应用程序交互时触发的事件。（你是否和我一样想要一款Microsoft Surface鼠标？）

Source是RoutedEvent的参数之一。你认为RoutedEventArgs类为什么要添加两个额外的源属性？

由于事件可以在元素树中向上和向下冒泡，因此最初触发事件的元素（OriginalSource）、发送事件的元素（Source）和处理事件的元素（Sender）可能不相同。

在大多数情况下，OriginalSource和Sender将相同，但OriginalSource通常是复杂控件的某个组件（在WPF中，几乎所有元素都是组合控件）。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_644_1.png)

Source是触发事件的元素。

Sender是处理事件的对象。

OriginalSource通常是Border或控件元素树中的其他某个元素。

## 探索RoutedEventArgs

实际上，你不需要经常使用Sender参数和源属性，但当你需要它们时，你真的需要它们，所以让我们花点时间来研究一下它们。要测试你改进后的方法版本：

### 创建WPF项目

你可以随意命名。

### 创建事件处理程序

我们将先构建一个显示三个参数的例程。这是我的版本，但你可以做得更花哨。如果你感到有灵感，可以尝试构建一个Window，在TextBox元素中显示这些值。重要的是，你的方法必须与我的具有相同的签名。（这是任何路由事件处理程序的标准签名。）

```
private void ShowArguments(object sender, RoutedEventArgs e)
{
    StringBuilder eventDetailsSB = new StringBuilder();
    eventDetailsSB.AppendLine("Event: " + e.RoutedEvent.Name);
    eventDetailsSB.AppendLine("Sender: " + sender.GetType().ToString());
    eventDetailsSB.AppendLine("Source: " + e.Source.GetType().ToString());
    eventDetailsSB.AppendLine("Original: " + e.OriginalSource.GetType().
    ToString());

    MessageBox.Show(eventDetailsSB.ToString());
}
```

### 触发事件

我们稍后将探讨触发事件的不同方式，但目前，只需将主窗口的Loaded事件属性（在XAML视图的属性窗口的“事件”部分中）设置为你的方法名。

### 测试它

运行应用程序，确保到目前为止所做的一切都能正常工作。Sender、Source和OriginalSource都应该是你的Window类的名称。

### 创建一些窗口元素

接下来，我们将向窗口添加一些元素，以便测试我们的事件处理程序。添加一个Button、TextBox、ListBox和一些RadioButtons（放在GroupBox内）。这是我的版本：

```
<Window ... Loaded="ShowArguments">
<Grid>
<Button Content="Click Me" Name="button1" ... />
<TextBox Name="textBox1" ... >I'm some text</TextBox>
<ListBox Name="listBox1" ...>
<ListBoxItem>Pick Me!</ListBoxItem>
<ListBoxItem>No, Pick Me!</ListBoxItem>
</ListBox>
<GroupBox Header="Radio Group" Name="groupBox1" ...>
<StackPanel>
<RadioButton>First Item</RadioButton>
<RadioButton>Second Item</RadioButton>
<RadioButton>Third Item</RadioButton>
</StackPanel>
</GroupBox>
</Grid>
</Window>
```

确保设置ListBox的Width，使其大于两个项目。（几页后你就会明白原因...）

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_646_0.png)

## 添加事件处理程序

在WPF中，有三种方法可以为RoutedEvent添加事件处理程序。你可以在XAML中完成（这是简单的方法），可以使用一些C#语法糖来完成，或者可以通过调用AddHandler()方法来完成（这是最灵活的方法）。我们将尝试所有三种方法。

### 在XAML中添加处理程序

对象定义的事件在XAML中作为属性公开。要添加处理程序，只需将属性设置为你的处理程序名称。上一页的Window代码中有一个示例，但让我们将Loaded事件替换为MouseDown事件。你可以直接在XAML中完成，也可以在属性窗口中完成。（Visual Studio会保持它们同步。）

### 使用C#运算符添加处理程序

在代码中添加事件处理程序几乎同样简单，就是使用C# +=运算符。你只需要记住，你要将RoutedEventHandler分配给事件，因此你需要在代码中创建一个。基本语法是：

```
<object>.<Event> += new RoutedEventHandler(<Method>);
```

你可以单独创建RoutedEventHandler，但没有实际意义。

在MainWindow()构造函数中，在调用InitializeComponent()之后，将我们的通用处理程序添加到button1.Click事件。

### 使用AddHandler()添加处理程序

添加事件处理程序的最后一种方法是调用由UIElement类定义的AddHandler()方法。AddHandler()方法有两个重载：

```
<object>.AddHandler(<Event>, new RoutedEventHandler(<Method>));
or
<object>.AddHandler(<Event>, new RoutedEventHandler(<Method>, <HandledEventsToo>));
```

在这里，你需要使用事件标识符的名称，即名称以'Event'结尾的那个。

我们稍后将探讨第二个重载。目前，使用第一个AddHandler()方法将我们的通用处理程序添加到ListBox1元素的MouseDown事件。

### 试一试

你的MainWindow()构造函数现在应该如下所示（允许你对方法和窗体上的元素命名有所不同）。

```
public MainWindow()
{
    InitializeComponent();
    button1.Click += new RoutedEventHandler(ShowArguments);
    listBox1.AddHandler(MouseDownEvent, new RoutedEventHandler(ShowArguments));
}
```

在运行应用程序之前，考虑一下如果Click和MouseDown是冒泡事件（它们确实是），你预期会发生什么。当你点击下列每个位置时，你认为会发生什么？

- 在窗口上，任何控件之外
- 在Button上
- 在ListBox上
- 任何其他位置
- 在ListBoxItem上

理论上，窗口上的MouseDown应该显示MessageBox，然后是Button上的Click事件，对吧？ListBox应该为MouseDown显示MessageBox，然后（当事件冒泡到窗口时）应该再次显示。窗口应该在其他任何地方捕获MouseDown。至少，当我最初学习路由事件时，我是这么预期的。

现在运行应用程序，尝试点击不同的东西。结果不会是你预期的那样；这并不意味着你犯了错误。当你点击窗体的每个部分时会发生什么？（确保你既点击ListBox背景，也点击它包含的项目。）

### 显微镜下

事件处理程序不是响应事件的唯一方式。我们将在第20章中探讨触发器，你可以将其视为事件处理程序的XAML版本。

