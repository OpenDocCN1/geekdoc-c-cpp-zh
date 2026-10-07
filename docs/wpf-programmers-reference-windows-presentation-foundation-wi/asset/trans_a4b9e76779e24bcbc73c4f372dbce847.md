

这种方法可能行得通（你可以将属性放在 `Control` 类中并让所有其他类继承它们），但还有许多其他属性可能需要类似的处理。例如，`DockPanel` 控件需要知道如何停齐子元素；`Canvas` 控件需要知道子元素的 `Top`、`Left` 以及其他位置属性；而 `Toolbar` 需要知道对包含的项使用何种 `OverflowMode`。

将所有这些属性都添加到 `Control` 类中不会让类变得臃肿，但它也不会为你提供一个通用的解决方案。如果你创建一个需要了解其他控件信息的新控件（例如，你创建了一个需要知道如何排列子元素的新容器类），你就需要重新构建 `Control` 基类以适应新控件。我怀疑微软是否可能为了协调 WPF 库并发布一个特殊的构建版本来添加你的属性。

> 面向对象的反对意见
将所有这些属性都添加到 `Control` 类中还会破坏类的封装性。这会使 `Control` 类了解过多关于其他类的信息，而这在本质上是不应该的。面向对象的纯主义者会认为，这种方法从一开始就是不合格的。

相反，WPF 采取了不同的方法，允许控件提供一个附加属性（attached property）供其他控件使用。例如，`Grid` 控件实际上实现了 `Grid.Row` 和 `Grid.Column` 附加属性，其他控件可以使用它们。

附加属性的语法是属性提供者的名称，后跟一个点，然后是属性名称。例如，`Grid` 控件的 `Row` 属性被称为 `Grid.Row`。

> 无限制的属性
提供附加属性的控件不会检查该属性在上下文中是否合理。例如，你可以给 `TextBox` 控件赋予一个 `Grid.Row`，即使它没有包含在 `Grid` 中。在这种情况下，该属性会被忽略。

遗憾的是，附加属性的语法与属性元素（property element）的语法非常相似。例如，图 9-5 显示的 `AttachedProperties` 示例使用了以下 XAML 代码。这段代码包含了几个附加属性和属性元素。

```
<Grid>
  <Grid.Background>
    <LinearGradientBrush EndPoint="0.5,0" StartPoint="0.5,0">
      <GradientStop Color="Yellow" Offset="0"/>
      <GradientStop Color="Red" Offset="1"/>
    </LinearGradientBrush>
  </Grid.Background>
  <Grid.RowDefinitions>
</Grid>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_198_0.png)

```
<RowDefinition Height="40"/>
<RowDefinition Height="*"/>
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*"/>
<ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>
<Label Content="Select Transaction" Foreground="Yellow"
HorizontalAlignment="Stretch" Grid.VerticalAlignment="Center"
Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"
<Label.Background>
<LinearGradientBrush>
<GradientStop Color="Yellow" Offset="0"/>
<GradientStop Color="Red" Offset="1"/>
</LinearGradientBrush>
</Label.Background>
<Button Margin="10" Grid.Row="1" Grid.Column="0">
<StackPanel>
<Label Content="Credit" HorizontalAlignment="Center"
Grid.Row="1" Grid.Column="1"/>
<Image Source="Credit.jpg" Height="60" />
</StackPanel>
</Button>
<Button Margin="10" Grid.Row="1" Grid.Column="1">
<StackPanel>
<Label HorizontalAlignment="Center" Content="Debit" />
<Image Source="Debit.jpg" Height="60" />
</StackPanel>
</Button>
</Grid>
```

`Grid` 控件包含三个元素属性：`Grid.Background`、`Grid.RowDefinitions` 和 `Grid.ColumnDefinitions`。这些描述了 `Grid` 控件的必须具有对象作为值的属性。

第一个 `Label` 有三个属性：`Grid.Row`、`Grid.Column` 和 `Grid.ColumnSpan`。这些属性由 `Grid` 提供，并告诉 `Grid` 如何定位它。

这个 `Label` 还有一个属性元素 `Label.Background`，它定义了 `Label` 的背景画刷。

第一个 `Button` 控件有两个附加属性 `Grid.Row` 和 `Grid.Column`，它们告诉 `Grid` 将其放置在何处。`Button` 包含一个 `StackPanel`，其中包含一个 `Label` 和一个 `Image`。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_199_0.png)

图 9-5

`Button` 的 `Label` 有附加属性 `Grid.Row` 和 `Grid.Column`。由于 `Label` 没有直接包含在 `Grid` 中，这些属性被忽略了。

第二个 `Button` 有 `Grid.Row` 和 `Grid.Column` 属性来告诉 `Grid` 如何定位它。

# 总结

本章解释了如何在 XAML 代码中使用属性。它解释了如何使用简单属性值、通过类型转换器转换的值、属性元素以及附加属性。这三类属性允许你定义 WPF 控件所需的属性值。

下一章描述了一组特别有用的属性：笔（pen）和画刷（brush）属性。它解释了如何构建简单和复杂的笔和画刷，这些工具决定了用于轮廓和填充文本、背景、线条、矩形和曲线等图形对象的颜色。

# 10

# 笔和画刷

笔和画刷决定了图形应用程序中最视觉直观的部分——颜色。

在图形术语中，*pen*（笔）决定了线性特征（如线条或圆形边缘）的颜色和样式。*brush*（画刷）决定了区域如何填充。例如，[图 10-1](#figure-10-1) 中绘制的椭圆用红色画刷填充，并用粗虚线紫色笔勾勒边缘。

本章描述了笔和画刷属性，并告诉你如何在 XAML 代码中设置它们。它解释了不同类型的笔和画刷以及决定它们外观的属性。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_202_0.png)

# 笔

*pen*（笔）定义了线性特征的颜色和几何形状，如线条、由 *Path* 控件定义的曲线，或椭圆矩形的边缘。

有趣的是，你认为由笔决定的某些颜色实际上是由画刷决定的。特别是，文本是通过用画刷填充形状而不是绘制来渲染的。如果你考虑手画（你通常会用笔），这有点违背直觉。

笔有几个不同的属性——都以单词 *stroke* 开头——决定了它的颜色和几何形状。

# 近距离观察

许多 *stroke* 属性除非你绘制的线性特征很粗，否则没有巨大差异。例如，`StrokeDashCap` 决定线端是矩形的、圆形的还是三角形的。如果线条只有 1 像素，你将无法区分。

记住，线条是可以缩放的，所以如果你的程序允许，用户可以放大线性特征直到这些属性产生巨大差异。图 10-2 所示的 `MagnifiedLines` 示例以五种不同的比例绘制同一条线条。在最粗的线条中，你可以看出线端是三角形的。

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_203_0.png)

以下代码显示 `MagnifiedLine` 如何绘制它最粗的线条。由于线条没有包含它的 `ViewBox` 宽，`ViewBox` 将其放大以适应：

```
<Line Stretch="Uniform" Height="20" Width="300" Margin="10,10,10,10">
<Line X1="0" Y1="0" X2="18.75" Y2="0" Stroke="Blue
StrokeDashArray="3" StrokeDashCap="Triangle"/>
</Line>
```

![](img/c9b2d394f4fc2f7e276f6a0a6fa9c2f6_203_1.png)

# Stroke

`Stroke` 属性决定线性特征的颜色。你可以通过两种方式指定颜色。WPF 理解 Red、Chartreuse、LavenderBlush 以及其他约 150 种颜色。以下 XAML 显示了 PensAndBrushes 示例如何绘制图 10-1 所示的椭圆。`Stroke` 属性使椭圆的边界变为紫色。

```xml
<Ellipse Fill="Red" Stroke="Purple"
Margin="0" StrokeThickness="10" StrokeDashArray="2,"/>
```

指定实色的第二种方法是给出其 `color components`。在两种情况下，RR、GG 和 BB 部分都包含两个十六进制数字，给出颜色、红色、绿色和蓝色组件（范围在 00 到 FF (255) 之间）。例如，值 `#FF0000` 是红色，而值 `#FFF00` 是黄色（红色和绿色部分相等）。

