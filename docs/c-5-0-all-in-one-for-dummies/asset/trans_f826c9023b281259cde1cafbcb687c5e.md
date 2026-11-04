
## 列表 2-11（续）

```xml
<Label Grid.Row="3" Grid.Column="1" Content="City:"
       HorizontalAlignment="Stretch" HorizontalContentAlignment="Right" />
<TextBox Grid.Row="3" Grid.Column="2" HorizontalAlignment="Stretch" />
<Button Grid.Row="3" Grid.Column="3" Content="Lookup" Margin="3,0" />
<Label Grid.Row="4" Grid.Column="1" Content="State:"
       HorizontalAlignment="Stretch" HorizontalContentAlignment="Right" />
<Grid Grid.Row="4" Grid.Column="2">
    <Grid.RowDefinitions>
        <RowDefinition Height="*" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="Auto" />
        <ColumnDefinition Width="Auto" />
    </Grid.ColumnDefinitions>
    <TextBox Grid.Row="0" Grid.Column="0" HorizontalAlignment="Stretch" />
    <Label Grid.Row="0" Grid.Column="1" Content="Zip:"
           HorizontalAlignment="Right" />
    <TextBox Grid.Row="0" Grid.Column="2" HorizontalAlignment="Stretch" />
</Grid>
<Grid Grid.Row="6" Grid.Column="0" Grid.ColumnSpan="3">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto" />
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*" />
        <ColumnDefinition Width="Auto" />
        <ColumnDefinition Width="Auto" />
    </Grid.ColumnDefinitions>
    <Button Grid.Row="0" Grid.Column="1" Content="Save" Margin="3,0" />
    <Button Grid.Row="0" Grid.Column="2" Content="Close" Margin="3,0" />
</Grid>
</Grid>
```

而且没错，这就是大量的 XAML！WPF 的众多优点之一就是其灵活性，可以创建你能想象到的几乎任何外观和感觉。但是，有时（好吧，大多数时候），这需要大量的尖括号。

**图 2-13：** 简单的数据输入表单。

![](img/80ff26f06fc9ab951e1cd4257b867366_615_0.png)

**图 2-14：** 加宽的简单数据输入表单。

![](img/80ff26f06fc9ab951e1cd4257b867366_615_1.png)

除了使用 XAML 进行布局外，你还可以完全使用代码来实现所有所示的示例。“Shenanigans！”你说？不，这是真的——甚至包括行/列大小调整。

固定大小是通过为 ColumnDefinition 或 RowDefinition 的 Width 属性分配一个数字来指定的。将 Auto 或 * 分配给它更复杂，因为 Width 属性的类型是 GridLength。（参见列表 2-12。）

## 列表 2-12： 在代码中设置自动和星号大小

```csharp
//Set to Auto sizing
column1 = new ColumnDefinition();
column1.Width = new GridLength(1, GridUnitType.Auto);
//Set to Star sizing
column2 = new ColumnDefinition();
column2.Width = new GridLength(1, GridUnitType.Star);
```

有关完整示例（以及更多示例），请参阅此处找到的 MSDN 文档：

http://msdn.microsoft.com/en-us/library/system.windows.gridunittype.aspx

![](img/80ff26f06fc9ab951e1cd4257b867366_616_0.png)

## 荣誉提及的面板

除了已经讨论过的面板外，还有四个额外的专用布局面板。由于它们非常专用，我不会详细介绍：

- **TabPanel：** 处理 TabControl 上项目的布局。
- **ToolbarPanel：** 处理 Toolbar 中项目的布局。
- **ToolbarOverflowPanel：** 处理从 Toolbar 溢出的控件的布局。
- **VirtualizingStackPanel：** 用于大量数据绑定场景。仅渲染数据集合中的可见项。
- **InkCanvas：** 接受数字墨水输入的 Canvas 面板。用于平板电脑收集签名等场景。

## 探索常用的 XAML 控件

Visual Studio 2012 自带了大量控件（还有更多厂商提供的控件可供购买）。本节介绍更常用的控件。我更喜欢将可用控件分为三类：

- 仅显示控件
- 基本输入控件
- 基于列表的控件

本节中的所有控件都可绑定到数据（请参阅本迷你书第 3 章）并且可通过代码修改。

## 仅显示控件

四个主要控件专注于向用户显示信息：

- **Image：** Image 控件显示图像（类型为 .bmp、.gif、.ico、.jpg、.png、.wdp 和 .tiff）。为保留图像的纵横比，请设置 Width 或 Height，但不能同时设置两者。此外，DecodePixelWidth 应设置为与 Width 相同的大小。这将导致渲染引擎适当缩放图像，可能节省大量内存。

顺便说一下，你可以在 WPF 的几乎任何地方放置图像——例如，按钮上的图像、标签中的图像，或段落文本中的内联图像。而且操作相当简单。我在这里不做那么花哨的处理，但我想让你知道这种可能性。

列表 2-13 显示了加载显示色轮的图像的 XAML。仅设置了 Width 和 DecodePixelWidth。结果窗口显示在图 2-15 中。

### 列表 2-13： Image 控件

```xml
<Image Grid.Row="0" Grid.Column="0" Width="256" >
    <Image.Source>
        <BitmapImage DecodePixelWidth="256" UriSource="/Images/1460_PaintPalette_256x256.png"/>
    </Image.Source>
</Image>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_617_0.png)

**图 2-15：**
Image control.

### TextBlock 和 Label

TextBlock 和 Label 控件都设计用于向用户提供文本或其他内容，区别不大。TextBlock 控件设计为标签的轻量级“小兄弟”，直接派生自 UIElement。

Label 控件提供访问修饰符功能，并且还派生自 ContentControl，这提供了额外的可能性。在字母前放置下划线（_）可启用访问修饰符。要在 Label 中提供下划线，请使用双下划线。在 XAML 中，因为它本质上是 XML，所以使用下划线是因为和号会破坏 XAML。Target 属性指定在键入访问修饰符时接收焦点的控件。你必须使用 Binding 表达式，这在本书第 3 章中介绍。

TextBlock 和 Label 控件在列表 2-14 和图 2-16 中进行了说明。

### 列表 2-14： TextBlock 和 Label

```xml
<TextBlock Grid.Row="0" Grid.Column="0" Margin="5,0" HorizontalAlignment="Right" Text="Text_Block:" />
<TextBox Grid.Row="0" Grid.Column="1" Margin="5,0" HorizontalAlignment="Stretch" />
<Label Grid.Row="1" Grid.Column="0" Margin="5,0" HorizontalAlignment="Stretch" HorizontalContentAlignment="Right" Content="Label__Content:" Target="{Binding ElementName=SampleTextBox}" />
<TextBox Name="SampleTextBox" Grid.Row="1" Grid.Column="1" Margin="5,0" HorizontalAlignment="Stretch" />
```

在示例中，Label 内容中的“L”是访问修饰符，双下划线会在渲染输出中添加一个下划线字符。

图 2-16：
TextBlock
和 Label
控件。

![](img/80ff26f06fc9ab951e1cd4257b867366_618_0.png)

### ProgressBar

最后一个仅显示控件是进度条。虽然技术上是 RangeBase 类的后代，但它不像 Slider（见下一节）那样启用用户输入。图 2-17 显示了进度条示例。要使条形持续运动，请将 IsIndeterminate 属性设置为 True

```xaml
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <!--<RowDefinition Height="Auto"/>-->
    </Grid.RowDefinitions>
    <!--
        <ProgressBar Name="ConstantProgressBar" Grid.Row="0" Grid.Column="0"
                     IsIndeterminate="True" -->
                     Height="20" Width="200" Foreground="Blue"
                     Background="White" />
    <!--
        <ProgressBar Grid.Row="1" Grid.Column="0" Maximum="100" Minimum="1"
                     Value="50"
                     IsIndeterminate="False" Height="20" Width="200"
                     Foreground="Blue" Background="White"/>
    -->
</Grid>
```

![](img/80ff26f06fc9ab951e1cd4257b867366_619_0.png)

## 基本输入控件

业务应用程序的支柱是基本输入控件。你在创建的每个窗口上都会找到其中一些控件，它们非常简单直接。图 2-18 在单个 Window 上显示了所有这些控件。以下是基本输入控件：

- **TextBox and PasswordBox：** `TextBox` 和 `PasswordBox` 都允许向 Window 输入标准文本。`PasswordBox` 会混淆输入的字符（使用默认系统密码字符或开发者指定的字符），用于收集敏感信息。`TextBox` 通过 `Text` 属性公开其内容，`PasswordBox` 通过 `Password` 属性公开。

```xaml
<TextBox Text="Some Text" />
<PasswordBox PasswordChar="X" Password="Some Text" />
```

- **CheckBox：** 复选框通过 `IsChecked` 属性表示布尔值。`IsChecked` 属性可为空，这提供了三态显示（True、False、Unknown）。使用水平方向的 `StackPanel` 将 `CheckBox` 水平排列，并使用一些边距分隔各框：

```xaml
<StackPanel Orientation="Horizontal">
    <CheckBox IsChecked="True"
              Content="True" Margin="15,15" />
    <CheckBox IsChecked="False" />
</StackPanel>
```
