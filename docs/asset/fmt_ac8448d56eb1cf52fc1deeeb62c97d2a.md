
```
OnButtonMouseMove source: Button button1, original source:
Border
```

当你使用隧道事件处理程序停止路由操作时，冒泡不会发生。这是隧道的一个重要特性。如果你在隧道事件处理程序中已经将 `Handled` 属性设置为 `true`，则冒泡事件永远不会发生：

```
OnGridPreviewMouseMove source: Button button1, original source:
Border
```

#### 使用 WPF 实现自定义路由事件

要在自定义类中定义冒泡和隧道事件，`MyDependencyObject` 被修改为支持值变化上的事件。为了支持冒泡和隧道事件，该类必须派生自 `UIElement` 而不是 `DependencyObject`，因为该类为事件定义了 `AddHandler` 和 `RemoveHandler` 方法。

为了使 `MyDependencyObject` 的调用方能够接收到关于值变化的信息，该类定义了 `ValueChanged` 事件。该事件使用显式的 `add` 和 `remove` 处理程序声明，其中调用了基类的 `AddHandler` 和 `RemoveHandler` 方法。这些方法需要 `RoutedEvent` 类型和委托作为参数。名为 `ValueChangedEvent` 的路由事件的声明与依赖属性非常相似。它被声明为静态成员，并通过调用 `EventManager.RegisterRoutedEvent` 方法进行注册。该方法需要事件名称、路由策略（可以是 `Bubble`、`Tunnel` 或 `Direct`）、处理程序的类型以及拥有类的类型。`EventManager` 类还使你能够注册静态事件并获取已注册事件的信息（代码文件 `DependencyObjectWPF/MyDependencyObject.cs`）：

```
using System;
using System.Windows;

namespace Wrox.ProCSharp.XAML
{
    class MyDependencyObject: UIElement
    {
        public int Value
        {
            get { return (int)GetValue(ValueProperty); }
            set { SetValue(ValueProperty, value); }
        }

        public static readonly DependencyProperty ValueProperty =
            DependencyProperty.Register(nameof(Value), typeof(int),
                typeof(MyDependencyObject),
                new PropertyMetadata(0, OnValueChanged, CoerceValue));

        // etc.
```

```
private static void OnValueChanged(DependencyObject d,
DependencyPropertyChangedEventArgs e)
{
    MyDependencyObject control = (MyDependencyObject)d;
    var e1 = new RoutedPropertyChangedEventArgs<int>
((int)e.OldValue,
        (int)e.NewValue, ValueChangedEvent);
    control.OnValueChanged(e1);
}

public static readonly RoutedEvent ValueChangedEvent =
    EventManager.RegisterRoutedEvent(nameof(ValueChanged),
RoutingStrategy.Bubble,
        typeof(RoutedPropertyChangedEventHandler<int>),
typeof(MyDependencyObject));

public event RoutedPropertyChangedEventHandler<int>
ValueChanged
{
    add
    {
        AddHandler(ValueChangedEvent, value);
    }
    remove
    {
        RemoveHandler(ValueChangedEvent, value);
    }
}

protected virtual void
OnValueChanged(RoutedPropertyChangedEventArgs<int> args)
{
    RaiseEvent(args);
}
}
```

现在你可以用冒泡功能使用它，就像之前对按钮 `MouseMove` 事件使用它一样。

#### 附加属性

而依赖属性是特定类型可用的属性，使用附加属性你可以为其他类型定义属性。某些容器控件为其子元素定义附加属性；例如，如果使用 `DockPanel` 控件，则其子元素可用 `Dock` 属性。`Grid` 控件定义 `Row` 和 `Column` 属性。

以下代码片段演示了这在 XAML 中的外观。`Button` 类没有 `Dock` 属性，但它是从 `DockPanel` 附加的：

```
<DockPanel>
    <Button Content="Top" DockPanel.Dock="Top" Background="Yellow" />
    <Button Content="Left" DockPanel.Dock="Left" Background="Blue"
```

附加属性的定义与依赖属性非常相似，如下一个示例所示。定义附加属性的类必须派生自基类 `DependencyObject` 并定义一个普通属性，其中 `get` 和 `set` 访问器调用基类的 `GetValue` 和 `SetValue` 方法。这就是相似之处的结束。不是调用 `DependencyProperty` 类的 `Register` 方法，现在调用 `RegisterAttached`，它注册一个附加属性，现在对每个元素都可用。

```
AttachedPropertyDemo[WPF|UWP]/MyAttachedPropertyProvider.cs:

public class MyAttachedPropertyProvider: DependencyObject
{
    public string MySample
    {
        get { return (string)GetValue(MySampleProperty); }
        set { SetValue(MySampleProperty, value); }
    }

    public static readonly DependencyProperty MySampleProperty =
        DependencyProperty.RegisterAttached(nameof(MySample),
        typeof(string),
        typeof(MyAttachedPropertyProvider), new
        PropertyMetadata(string.Empty);

    public static void SetMySample(UIElement element, string
    value) =>
        element.SetValue(MySampleProperty, value);

    public static int GetMyProperty(UIElement element) =>
        (string)element.GetValue(MySampleProperty);
}
```

> **NOTE** 你可能会认为 `DockPanel.Dock` 只能添加到 `DockPanel` 内的元素。实际上，附加属性可以添加到任何元素。然而，没有人会使用这个属性值。`DockPanel` 知道这个属性并从其子元素读取它以进行排列。

在 XAML 代码中，附加属性现在可以附加到任何元素。第二个 `Button` 控件，名为 `button2`，已附加属性 `MyAttachedPropertyProvider.MySample` 并分配了值 42。

```
AttachedPropertyDemo[WPF|UWP]/Main[Window|Page].xaml:

<Grid x:Name="grid1">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
        <RowDefinition Height="Auto" />
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>
    <Button Grid.Row="0" x:Name="button1" Content="Button 1" />
    <Button Grid.Row="1" x:Name="button2" Content="Button 2"
            local:MyAttachedPropertyProvider.MySample="42" />
    <ListBox Grid.Row="2" x:Name="list1" />
</Grid>
</Window>
```

在代码后置中执行相同的操作时，有必要调用类 `MyAttachedPropertyProvider` 的静态方法 `SetMyProperty`。不可能通过属性扩展 `Button` 类。`SetProperty` 方法获取应由属性扩展的 `UIElement` 实例和值。在以下代码片段中，属性附加到 `button1` 并将值设置为示例值（代码文件 `AttachedPropertyDemoWPF/MainPage.xaml.cs`）：

```
public MainPage()
{
    InitializeComponent();

    MyAttachedPropertyProvider.SetMySample(button1,"sample value");
    // etc.
}
```

要读取分配给元素的附加属性，可以使用 `VisualTreeHelper` 迭代层次结构中的每个元素并尝试读取其附加属性。`VisualTreeHelper` 用于在运行时读取元素的视觉树。`GetChildrenCount` 方法返回子元素的数量。要访问子元素，传递索引的 `GetChild` 方法返回该元素。该方法实现仅在元素为 `FrameworkElement` 类型（或其派生类型）时返回元素，并且如果使用 `Func` 参数传递的谓词返回 `true`。

```
private IEnumerable<FrameworkElement>
GetChildren(FrameworkElement element,
    Func<FrameworkElement, bool> pred)
{
    int childrenCount =
VisualTreeHelper.GetChildrenCount(rootElement);
    for (int i = 0; i < childrenCount; i++)
    {
        var child = VisualTreeHelper.GetChild(rootElement, i) as FrameworkElement;
        if (child != null && pred(child))
        {
            yield return child;
        }
    }
}
```

`GetChildren` 方法现在从页面构造器内部使用，以将所有具有附加属性的元素添加到 `ListBox` 控件：

```csharp
public MainPage()
{
    InitializeComponent();

    MyAttachedPropertyProvider.SetMySample(button1,"sample value");
    foreach (var item in GetChildren(grid1, e =>

MyAttachedPropertyProvider.GetMySample (e) != 

string.Empty)

{

list1.Items.Add(

$"{item.Name}":

{MyAttachedPropertyProvider.GetMySample(item)} ");

}
```

当你运行应用程序（无论是WPF还是UWP应用）时，你会在`ListBox`中看到两个按钮控件，其值如下：

- `button1`：示例值
- `button2`：42

到目前为止，附加属性的示例代码在WPF和通用Windows应用中是相同的，唯一的区别是WPF使用`MainWindow`控件而不是`MainPage`。然而，WPF有另一种遍历元素的方式。WPF和通用Windows应用都可以使用`VisualTreeHelper`来遍历可视树，该树包含运行时创建的所有元素，包括模板和样式。使用WPF还可以使用`LogicalTreeHelper`。这个辅助类遍历元素的逻辑树。逻辑树与设计时使用的树相同。这棵树也可以在Visual Studio的“文档大纲”中显示（参见图29.1）。

![](img/3d365b72b289213a91ade7eb366b8f35_1085_0.png)

使用`LogicalTreeHelper`，遍历子元素的方法可以修改如下。`LogicalTreeHelper`类提供了一个`GetChildren`方法，而不需要获取子元素的数量并使用`for`循环遍历它们（代码文件`AttachedPropertyDemoWPF/MainWindow.xaml.cs`）：

```csharp
public MainWindow()
{
    InitializeComponent();

    MyAttachedPropertyProvider.SetMySample(button1, "sample value");
}
```

```csharp
foreach (var item in LogicalTreeHelper.GetChildren(grid1).
    OfType<FrameworkElement>().Where(
        e => MyAttachedPropertyProvider.GetMySample(e) !=
string.Empty))
{
    list1.Items.Add(
        $"{item.Name}:
{MyAttachedPropertyProvider.GetMySample(item)}");
}
```

> 注意：第30章“使用XAML样式化应用”以及第31章至第35章将使用XAML演示许多不同的附加属性的实际应用——例如，来自容器控件（如`Canvas`、`DockPanel`和`Grid`）的附加属性，以及`Validation`类的`ErrorTemplate`属性。

#### 标记扩展

使用标记扩展，你可以通过元素语法或属性语法来扩展XAML。如果XML属性包含花括号，那就是标记扩展的标志。通常，带属性的标记扩展被用作替代元素的简写表示法。

这种标记扩展的一个例子是`StaticResourceExtension`，它用于查找资源。下面是一个带有键`gradientBrush1`的线性渐变画刷资源（代码文件`MarkupExtensionsUWP/MainPage.xaml`）：

```
<Page.Resources>

    <LinearGradientBrush x:Key="gradientBrush1"

StartPoint="0.5,0.0" EndPoint="0.5, 1.0">

        <GradientStop Offset="0" Color="Yellow" />

        <GradientStop Offset="0.3" Color="Orange" />

        <GradientStop Offset="0.7" Color="Red" />

        <GradientStop Offset="1" Color="DarkRed" />

    </LinearGradientBrush>

</Page.Resources>
```

可以通过使用带属性语法的`StaticResourceExtension`来引用此资源，以设置`Button`的`Background`属性。属性语法由花括号和扩展类名（不带Extension后缀）定义：

```
<Button Content="Test" Background="{StaticResource gradientBrush1}" />
```

WPF还允许使用元素语法来使用属性简写记法的较长形式，如下一个代码片段所示。`StaticResourceExtension`被定义为`Button.Background`元素的子元素。`ResourceKey`属性通过一个属性设置为`gradientBrush1`。在前面的示例中，资源键不是通过`ResourceKey`属性设置的（那也是可以的），而是通过一个可以设置资源键的构造函数重载来设置的：

```
<Button Content="Test">

    <Button.Background>

        <StaticResourceExtension ResourceKey="gradientBrush1" />

    </Button.Background>

</Button>
```
