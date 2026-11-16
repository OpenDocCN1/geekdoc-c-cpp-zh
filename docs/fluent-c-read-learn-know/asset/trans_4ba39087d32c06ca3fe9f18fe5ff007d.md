

## 解决方案...

将上一页中日益复杂的事件处理程序集与使用 WPF 绑定实现的相同功能进行对比。我们所要做的就是指定想要的元素和属性，WPF 会处理其余所有事情。我知道我更愿意编写哪个版本。

这是我们的原始版本。我们不得不寻找可用的更改事件，并追踪一些不明显的 bug。而这仅仅是三个属性。如果有二十个，或者五十个呢？绑定到集合又如何？情况会迅速变得糟糕。

```
private void Window_SizeChanged(object sender, SizeChangedEventArgs e)
{
    WidthLabel.Content = Box.ActualWidth.ToString();
    HeightLabel.Content = Box.ActualHeight.ToString();
}

private void Box_TextChanged(object sender, TextChangedEventArgs e)
{
    if (this.IsLoaded)
        TextLabel.Content = Box.Text;
}
```

下面是使用 WPF 绑定的版本。我们只需要向 XAML 添加一个标记扩展。（当然，也可以在代码中完成）。这就是我们所要做的全部。在任何情况下。无需寻找可挂钩的事件，无需追踪奇怪而奇妙的无关问题...

```
<TextBox x:Name="Box" .../>
<Label Content="{Binding ElementName=Box, Path=ActualWidth}" .../>
<Label Content="{Binding ElementName=Box, Path=ActualHeight}" .../>
<Label Content="{Binding ElementName=Box, Path=Text}" .../>
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_0.png)

## 任务列表

本章将从探索 WPF 绑定的基础知识开始。你在其他场景中已经做过一些基本绑定，所以这可能看起来是旧闻，但随后我们将进入一些更有趣的内容，包括如何转换和格式化数据，以及如何绑定到整个数据集并导航它们。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_1.png)

## 创建绑定

在深入 WPF 绑定的复杂性之前，我们需要掌握基础知识，因此我们将先查看涉及的基本对象及其使用方法。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_2.png)

## 绑定到集合

接下来，我们将探索将整个数据集绑定到 ListBox、ComboBox 和 TreeView 等项控件。为了有效地使用这些控件，你需要知道绑定源中的数据是如何显示的，因此我们还将检查数据模板，它们只是你在上一章中学习如何构建的模板的另一种形式。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_805_3.png)

## 使用集合

WPF 提供了一些用于处理数据集合的有用函数。我们将从探索主从模式开始，该模式允许你显示在项控件中选定项的详细信息，然后探索绑定工具箱中的一些其他有用工具，包括如何过滤、排序和分组一组数据，以及如何将值转换为对你更有用的形式。

## 创建绑定

你在控件模板中使用 TemplateBinding 元素时已经编写过一种绑定表达式，但一般绑定语法略有不同，因此让我们从一个简单的示例开始。（我们将在过程中对其进行扩展。）

这是本章稍后将绑定的 ListBox。

此列中的元素……将被赋予此列中的名称。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_806_0.png)

我们将使用 TextBox 作为标签的源。

我们将在过程中绑定这些标签。

```
{Binding ElementName="<name>", Path="<property>"}
```

## 动动脑筋

准备好开始了吗？这是 Binding 对象的类图。使用它以及几页前的示例，你能完成以下任务吗？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_807_0.png)

- 1. 创建一个新项目并构建基本窗体。我的使用 Grid 作为根元素，包含三列和五行，但如果你有更好的主意，不需要以这种方式组织。确保为最后一列中的 TextBox 和标签指定第二列中列出的名称。
- 2. 为名为 TextLabel1 的 Label1 设置绑定，使其显示 TextBox 的内容。
- 3. 为名为 FontLabel1 的 Label1 设置绑定，使其显示 TextLabel1 的 FontStyle。
- 暂时不要处理 GridLabel1 和 Button；我们稍后会修复它们。
- 4. 运行应用程序。第一个 TextBox 何时更新？你认为需要设置 Binding 对象的哪个属性来更改此行为？

## 做得怎么样？

公平地说，WPF 绑定可能会变得相当复杂，但大多数时候，它就这么简单。

我省略了仅用于格式化窗口的 XAML，以便我们可以专注于绑定元素。

```
<Window ... >
<Grid ... >
<Grid.ColumnDefinitions ... />
<Grid.RowDefinitions ... />
<ListBox ... />
<Label ...TextSource:...</Label>
<Label ...TextLabel...</Label>
<Label ...FontLabel...</Label>
<Label ...GridLabel...</Label>
<TextBox x:Name="TextSource" ...>Sample Text</TextBox>
<Label x:Name="TextLabel" Content="{Binding ElementName=TextSource, Path=Text}" />
<Label x:Name="FontLabel" Content="{Binding ElementName=TextLabel, Path=FontStyle}" />
<Label x:Name="GridLabel" ...>...bound value...</Label>
<Button x:Name="UpdateButton" ...>Update Now</Button>
</Grid>
</Window>
```

还有其他选项，我们将在几页后查看其中几个，但绑定到元素的最简单方法是按名称。

以下是执行绑定的行。你已经看到了第一个示例。你解出第二个了吗？

## 休息一下

绑定有点复杂，所以在继续之前，为什么不休息一下呢？

## 绑定模式

在练习中，我让你思考可能使用哪个属性来控制绑定目标何时更新。答案是 UpdateSourceTrigger，它接受 UpdateSourceTrigger 枚举的一个成员。UpdateSourceTrigger 是控制 Binding 行为的两个属性之一。另一个是 BindingMode，它决定源和目标如何交互。我们将从探索第二个属性开始：BindingMode。

BindingMode 属性控制目标和源相互影响的方式。

大多数时候你会使用双向绑定。它告诉 Binding 对象在任一对象更改时更新两个对象。

单向绑定意味着目标对源没有影响。

当源和目标都不更改时，一次性绑定更高效。它设置初始值，然后忽略任何其他更改。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_809_0.png)

OneWayToSource 在许多情况下都不合理，但可以通过交换目标和源来诱骗 WPF 对非依赖属性执行单向绑定。这种技术最多只能算是一种权宜之计，但有时你别无选择。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_809_1.png)

## 更新触发器

控制 Binding 行为的另一个属性是 UpdateSourceTrigger，它正是说明名称所指的含义：它定义了源更新何时触发。不要将 UpdateSourceTrigger 与样式或事件触发器混淆。就像静态属性和静态资源一样，这些术语的含义不同。

UpdateSourceTrigger 仅在源实际被更新时适用，这意味着 Mode 必须是 TwoWay 或 OneWayToSource。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_810_0.png)

当 UpdateSourceTrigger 设置为 Explicit 时，你需要在 BindingExpression 上调用 UpdateSource()。（请记住，WPF 每当将 Binding 对象链接到绑定源上的属性时都会创建一个 BindingExpression。这允许你为多个源属性重用 Binding 对象。）

GetBindingExpression() 方法返回一个 BindingExpression 实例，供你在代码中使用。

```
BindingExpression be = TextLabel1.GetBindingExpression(Label.ContentProperty);
be.UpdateSource();
```

一旦你拥有 BindingExpression 的引用，UpdateSource() 方法就会告诉 Binding 执行延迟更新。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_810_1.png)

