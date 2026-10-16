
```csharp
MyAttachedPropertyProvider.GetMySample (e) != 
string.Empty)
{
list1.Items.Add(
$"{item.Name}":
{MyAttachedPropertyProvider.GetMySample(item)} ");
}
```

当你运行应用程序（无论是WPF还是UWP应用）时，你会在ListBox中看到两个按钮控件，其值如下：

+   - button1：示例值
+   - button2：42

到目前为止，附加属性的示例代码在WPF和通用Windows应用中是相同的，唯一的区别是WPF使用MainWindow控件而不是MainPage。然而，WPF有另一种遍历元素的方式。WPF和通用Windows应用都可以使用VisualTreeHelper来遍历可视树，该树包含运行时创建的所有元素，包括模板和样式。使用WPF还可以使用LogicalTreeHelper。这个辅助类遍历元素的逻辑树。逻辑树与设计时使用的树相同。这棵树也可以在Visual Studio的“文档大纲”中显示（参见图29.1）。

![](img/3d365b72b289213a91ade7eb366b8f35_1085_0.png)

使用LogicalTreeHelper，遍历子元素的方法可以修改如下。LogicalTreeHelper类提供了一个GetChildren方法，而不需要获取子元素的数量并使用for循环遍历它们（代码文件AttachedPropertyDemoWPF/MainWindow.xaml.cs）：

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

> 注意：第30章“使用XAML样式化应用”以及第31章至第35章将使用XAML演示许多不同的附加属性的实际应用——例如，来自容器控件（如Canvas、DockPanel和Grid）的附加属性，以及Validation类的ErrorTemplate属性。

## 标记扩展

使用标记扩展，你可以通过元素语法或属性语法来扩展XAML。如果XML属性包含花括号，那就是标记扩展的标志。通常，带属性的标记扩展被用作替代元素的简写表示法。

这种标记扩展的一个例子是StaticResourceExtension，它用于查找资源。下面是一个带有键gradientBrush1的线性渐变画刷资源（代码文件MarkupExtensionsUWP/MainPage.xaml）：

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

可以通过使用带属性语法的StaticResourceExtension来引用此资源，以设置Button的Background属性。属性语法由花括号和扩展类名（不带Extension后缀）定义：

```
<Button Content="Test" Background="{StaticResource gradientBrush1}" />
```

WPF还允许使用元素语法来使用属性简写记法的较长形式，如下一个代码片段所示。StaticResourceExtension被定义为Button.Background元素的子元素。ResourceKey属性通过一个属性设置为gradientBrush1。在前面的示例中，资源键不是通过ResourceKey属性设置的（那也是可以的），而是通过一个可以设置资源键的构造函数重载来设置的：

```
<Button Content="Test">
    <Button.Background>
        <StaticResourceExtension ResourceKey="gradientBrush1" />
    </Button.Background>
</Button>
```

### 创建自定义标记扩展

UWP应用只能使用预定义的标记扩展。而使用WPF，你可以创建自定义标记扩展。标记扩展通过定义一个派生自基类MarkupExtension的类来创建。大多数标记扩展都有Extension后缀（这种命名约定类似于属性的Attribute后缀，你可以在第16章“反射、元数据和动态编程”中了解）。对于自定义标记扩展，你只需要重写ProvideValue方法，该方法从扩展返回值。返回的类型通过MarkupExtensionReturnType特性标注在类上。在调用ProvideValue方法时，会传入一个IServiceProvider对象。通过这个接口，你可以查询不同的服务，例如IProvideValueTarget或IXamlTypeResolver。你可以使用IProvideValueTarget，通过TargetObject和TargetProperty属性访问标记扩展所应用到的控件和属性。你可以使用IXamlTypeResolver将XAML元素名称解析为CLR对象。自定义标记扩展类CalculatorExtension定义了double类型的X和Y属性，以及一个由枚举定义的Operation属性。根据Operation属性的值，会对X和Y输入属性执行不同的计算，并返回一个字符串（代码文件MarkupExtensionsWPF/CalculatorExtension.cs）：

```
using System;
using System.Windows;
using System.Windows.Markup;
namespace Wrox.ProCSharp.XAML
{
    public enum Operation
    {
        Add,
        Subtract,
        Multiply,
        Divide
    }

    [MarkupExtensionReturnType(typeof(string))]
    public class CalculatorExtension: MarkupExtension
    {
        public CalculatorExtension()
        {
        }
        public double X { get; set; }
        public double Y { get; set; }
        public Operation Operation { get; set; }

        public override object ProvideValue(IServiceProvider serviceProvider)
        {

```

```
IProvideValueTarget provideValue =
serviceProvider.GetService(typeof(IProvideValueTarget))
    as IProvideValueTarget;
    if (provideValue != null)
    {
        var host = provideValue.TargetObject as
FrameworkElement;
        var prop = provideValue.TargetProperty as
DependencyProperty;
    }
    double result = 0;
    switch (Operation)
    {
        case Operation.Add:
            result = X + Y;
            break;
        case Operation.Subtract:
            result = X-Y;
            break;
        case Operation.Multiply:
            result = X * Y;
            break;
        case Operation.Divide:
            result = X / Y;
            break;
        default:
            throw new ArgumentException("invalid operation");
    }
    return result.ToString();
}
}
```

现在你可以使用该标记扩展：在第一个TextBlock中使用属性语法将值3和4相加，或者在第二个TextBlock中使用元素语法（代码文件MarkupExtensionsWPF/MainWindow.xaml）。

```
<Window x:Class="Wrox.ProCSharp.XAML.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:Wrox.ProCSharp.XAML"
    Title="MainWindow" Height="350" Width="525">
<StackPanel>
    <TextBlock Text="{local:Calculator Operation=Add, X=3, Y=4}"/>
    <TextBlock>
        <TextBlock.Text>
            <local:CalculatorExtension>
                <local:CalculatorExtension.Operation>
                    <local:Operation>Multiply</local:Operation>
                </local:CalculatorExtension.Operation>
<local:CalculatorExtension.X>7</local:CalculatorExtension.X>
<local:CalculatorExtension.Y>11</local:CalculatorExtension.Y>
            </local:CalculatorExtension>
        </TextBlock.Text>
    </TextBlock>
</StackPanel>
```

### 使用XAML定义的标记扩展

标记扩展提供了许多功能，事实上，本章已经使用了XAML定义的标记扩展。在“使用集合与XAML”一节中展示的`x:Array`被定义为标记扩展类`ArrayExtension`。对于该标记扩展，不能使用属性语法，因为要定义元素列表会很困难。

其他由XAML定义的标记扩展包括：`TypeExtension (x:Type)`，它根据字符串输入返回类型；`NullExtension (x:Null)`，可用于在XAML中将值设置为null；以及`StaticExtension (x:Static)`，用于调用类的静态成员。

目前仅面向通用Windows应用提供的XAML定义的标记扩展是编译绑定（`x:Bind`），用于实现具有更好性能的数据绑定。这种数据绑定将在第32章“Windows应用：用户界面”中介绍。

WPF、WF、WCF和通用Windows应用定义了特定于这些技术的标记扩展。WPF和通用Windows应用使用标记扩展来访问资源、进行数据绑定和颜色转换；WF应用在活动中使用标记扩展；WCF应用为终结点定义标记扩展。

## 总结

在本章中，你已经通过WPF和通用Windows应用的示例了解了XAML的核心功能。你还了解了一些特定特性，如依赖属性、附加属性、路由事件和标记扩展。通过这些特性，你不仅了解了基于XAML的技术的基础，还了解了如何将C#和.NET的特性（如属性和事件）应用于扩展用例。属性已得到增强，以支持更改通知和验证（依赖属性）。附加属性使你能够在控件本身不提供这些属性的情况下对控件使用这些属性。事件已通过冒泡和隧道功能得到增强。

所有这些特性为不同的XAML技术（如WPF、WF和UWP应用）奠定了基础。

下一章继续讨论XAML，主题是样式和资源。

