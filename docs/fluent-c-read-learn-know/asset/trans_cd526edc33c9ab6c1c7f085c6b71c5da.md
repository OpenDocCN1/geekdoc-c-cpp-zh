

## 任务列表

在本章中，我们将追溯重新定义 WPF 控件的可视化树和可视化行为的整个过程，从一些可用于构建控件模板的低级可视化组件开始。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_772_0.png)

## 构建控件

您可以在控件模板中使用任何 WPF 元素，但您通常会希望使用相当低级别的组件——您需要的是矩形或框架，而不是 TextBlock。我们之前没有理由探索这种图形，但现在有了，因此我们将首先快速查看提供此基本绘图功能的 WPF 元素。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_772_1.png)

## 控件模板

一旦我们弄清楚如何使用 WPF 绘图元素，就可以使用它们来构建控件模板，因此我们将接下来探讨这一点，以及如何查找（并命名）控件正常运行所必须存在的控件部分。我们还将研究几个特殊元素：ContentPresenter（嗯，用于呈现控件内容）和 TemplateBinding（用于将模板链接到控件的公共属性）。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_772_2.png)

## 可视化状态管理器

控件模板支持一种定义控件可视化行为的机制，它类似于触发器，但功能更强大，使用起来也更简单（一旦掌握诀窍）。VisualStateManager 由 .NET 4.0 控件协议支持，这也使其更加稳健。在本节中，我们将学习如何支持可视化状态，并最终修复上一章中未完全正常工作的按钮鼠标悬停效果。

与窗口的逻辑树类似，控件模板可以包含几乎任何 Framework 元素，但您通常希望在较低的可视化级别工作。您想要的是“带有虚线边框的矩形”，而不是 TextBox。WPF 有三类在此级别工作的元素：Shapes、Adorners 和 Decorators。我们在前几章中实际上使用过其中一些形状，但从未真正探索过它们，所以让我们现在来做吧。

### 形状

形状正是您所期望的；它们是基本的几何对象。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_773_0.png)

### 装饰器

装饰器位于其他元素之上。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_773_1.png)

Visual Studio 设计器中出现的边界框是装饰器的一个示例。

我们不会在本章中研究装饰器，但在下一章中将看到一个示例。

### 装饰器（Decorators）

装饰器以特定方式显示单个对象。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_773_2.png)

Border 是您将大量使用的装饰器。它在某些内容周围绘制边框，并在其后绘制背景。Button 的默认模板只是一个 Border 和一个内容呈现器。

### 绘制形状

Shape 抽象类及其具体子类在用户界面中呈现二维绘图。绘图本身是使用更低级别的一组类定义的，即 Geometry 及其子类，它们在数学上描述形状。

因为 Shape 是 FrameworkElement，所以它继承 Width、Height、RenderTransform 和 LayoutTransform 属性。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_774_0.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_774_1.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_774_2.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_774_3.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_774_4.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_774_5.png)

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_774_6.png)

Shape 不公开 Pen 属性，而是单独公开每个笔属性。这可能看起来很繁琐，但在实践中更高效。

FillRule 定义当定义 Polyline 或 Polygon 的路径与自身交叉时会发生什么。

Polyline 的 Points 集合在 XAML 中指定为 "x,y x,y x,y ..."

### 动手试试

这是一个在 Grid 中显示多个形状的窗口。您能复制它吗？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_775_0.png)

我在这里使用的点集是

```
20,20 50,85 90,20 130,85 170,20 210,85
```

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_775_1.png)

使用 Rectangle 的 RadiusX 和 RadiusY 属性来创建此效果。我使用的值为 20。

这是一个带有 LayoutTransform 的 Rectangle。

### 您做得怎么样？

这是我的版本：

```
<Window ... >
<Grid>
<Grid.ColumnDefinitions>
<ColumnDefinition />
<ColumnDefinition />
</Grid.ColumnDefinitions>
<Grid.RowDefinitions>
<RowDefinition />
<RowDefinition />
<RowDefinition />
</Grid.RowDefinitions>
<Ellipse Grid.Row="0" Grid.Column="0" Margin="10" Fill="Black" />
<Rectangle Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center" Width="75"
Height="75" Fill="Black" />
<Rectangle Grid.Row="2" Grid.Column="0" Margin="10" Fill="Black"
RadiusX="20" RadiusY="20" />
<Line Grid.Row="0" Grid.Column="1" X1="10" Y1="10" X2="240" Y2="90"
StrokeThickness="2" Stroke="Black" />
<Polyline Grid.Row="1" Grid.Column="1" Stroke="Black" StrokeThickness="2"
Points="20,20 50,85 90,20 130,85 170,20 210,85" />
<Rectangle Grid.Row="2" Grid.Column="1" Margin="10" Fill="Black">
<Rectangle.LayoutTransform>
<RotateTransform CenterX="200" CenterY="200" Angle="45" />
</Rectangle.LayoutTransform>
</Rectangle>
</Grid>
</Window>
```

### 装饰器

我们不会在本章中研究装饰器（它们的工作方式与装饰器非常相似），但 Decorator 类（尤其是 Border）几乎用于每个控件模板。您可以将 Decorator 视为内容控件和面板之间的中间体。与内容控件一样，Decorator 在其 Child 属性中包含单个元素。与面板一样，Decorator 的目的是显示其内容。但是，虽然面板专门用于排列其内容，但装饰器会以某种方式操纵它。

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_777_0.png)

BulletDecorator 在其内容旁边显示图像。

InkPresenter 用于将鼠标或触笔移动捕获为路径，例如在绘图程序中。

AdornerDecorator 承载装饰器。

Viewbox 装饰器的工作方式与 TileBrush 的 Viewbox 完全相同。

### 动手试试

您能向我们的示例中添加一个包含装饰器的第三列吗？

![](img/1dcd2af4ae4fa0eb5cf4ed5437ff121a_777_1.png)

这是一个设置了 Background 的 BulletDecorator。Image 使用属性语法指定。

这是一个带有灰色 Background 和黑色 BorderBrush 的 Border。

这是一个 Stretch 属性设置为 Fill 的 Viewbox。

### 您做得怎么样？

当然，您的图像会不同，但这是我的版本：

```
<Window ...>
<Grid>
...
<BulletDecorator Grid.Row="0" Grid.Column="2"
 Background="Gainsboro" Margin="10">
 <BulletDecorator.Bullet>
 <Image Source="Thinking Hat.tif" Width="50" />
 </BulletDecorator.Bullet>
 </BulletDecorator>
 <Rectangle Margin="10" Fill="Black" />
 </BulletDecorator>
 <Border Grid.Row="1" Grid.Column="2" Background="Gainsboro" Margin="10"
 BorderBrush="Black" BorderThickness="10">
 <Ellipse Width="50" Height="50" Fill="Black" />
 </Border>
 <Viewbox Grid.Row="2" Grid.Column="2" Stretch="Fill">
 <Image Source="Thinking Hat.tif" />
 </Viewbox>
</Grid>
</Window>
```

### 休息一下

与我们使用过的一些 WPF 元素相比，形状和装饰器类相当易于使用。它们的功能很简单，没有任何棘手的属性或结构需要担心。那么，在继续使用这些和其他对象构建控件模板之前，为什么不休息一下呢？

## 控件模板

现在我们已经了解了一些用于定义控件可视化树的最常见元素，让我们来看看使用控件模板实际执行此操作的语法。

控件模板可以定义为资源，或者（更常见地）作为样式的一部分。语法可能不会让您大吃一惊。

您可以为单个元素定义控件模板：

```
<Button>
<Button.Template>
<ControlTemplate TargetType="Button">
<ControlTemplate.Triggers>
... property and event triggers ...
</ControlTemplate.Triggers>
... Visual Tree ...
<VisualStateManager.VisualStateGroups>
... Visual States & Transitions ....
</VisualStateManager.VisualStateGroup>
</ControlTemplate>
</Button.Template>
</Button>
```

与内容控件一样，控件模板必须有一个单个子元素，该子元素又可以包含其他元素。

即使在元素定义中，也必须指定目标类型。

模板具有 Triggers 集合，就像 Style 一样。

我们将在本章后面讨论 VisualStateManager。

但通常是在样式内部完成的，以便多个元素可用：

控件模板在普通属性设置器内设置。

```
<Style TargetType="Button">
...
<Setter Property="Template">
<Setter.Value>
<ControlTemplate TargetType="Button">
...
</ControlTemplate>
</Setter.Value>
</Setter>
</Style>
```

您始终需要指定 TargetType。

