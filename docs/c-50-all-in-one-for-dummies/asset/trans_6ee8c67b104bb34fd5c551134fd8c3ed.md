

# 592 探索常用的 XAML 控件

- 仅显示控件
- 基础输入控件
- 基于列表的控件

本节中的所有控件都可以绑定到数据（参见本微型书籍的第 3 章）并通过代码进行修改。

## 仅显示控件

有四种主要的控件专注于向用户显示信息：

- Image：Image 显示图像（.bmp, .gif, .ico, .jpg, .png, .wdp, .tiff 类型）。为了保持图像的比例，请设置 `Width` 或 `Height`，不要两个都设置。此外，应该将 `DecodePixelWidth` 设置为与 `Width` 相同的大小。这将导致渲染引擎缩放图像，从而节省大量内存。

顺便提一下，你几乎可以在 WPF 的任何地方放置图像——例如，在按钮上、标签内或文本段落的行内。这非常简单。我在这里不搞得太复杂，但我想让你知道这种可能性。

代码列表 2-13 显示了用于加载色轮图像的 XAML。仅设置了 `Width` 和 `DecodePixelWidth`。生成的窗口如图 2-15 所示。

### 代码列表 2-13：Image 控件

```xml
<Image Grid.Row="0" Grid.Column="0" Width="256" >
  <Image.Source>
    <Bitmap DecodePixelWidth="256" UriSource="/Images/1460_PaintPalette_256x256.png" />
  </Image.Source>
</Image>
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_617_0.png)

图 2-15：Image 控件。

TextBlock 和 Label：TextBlock 和 Label 控件都旨在向用户提供文本或其他内容，但有所不同。TextBlock 控件被设计为 label 的轻量级“小兄弟”，直接派生自 UIElement。

Label 控件提供了访问修饰符，并且派生自 ContentControl，这开启了更多的可能性。在字母前放置下划线 (_) 可以启用访问修饰符。要在 Label 中提供下划线，请使用双下划线。在 XAML 中，由于它是核心 XAML 语法，使用下划线是因为使用符号 (&) 会破坏 XAML。`Target` 属性指定当访问修饰符为键时接收焦点的控件。你可以使用 Binding 表达式，这在微型书籍的第 3 章中介绍。

TextBlock 和 Label 控件在列表 2-14 和图 2-16 所示。

### 代码列表 2-14：TextBlock 和 Label

```xml
<TextBlock Grid.Row="0" Grid.Column="0" Margin="5,0" HorizontalAlignment="Right"
           Text="TextBlock"/>
<Grid Grid.Row="1" Grid.Column="1" Margin="5,0"
      HorizontalAlignment="Stretch">
  <Label Grid.Row="0" Grid.Column="0" Margin="5,0" HorizontalAlignment="Stretch"
         Content="_Label__"
         Target="Binding ElementName=TextBox"/>
  <TextBox Name="SampleTextBox" Grid.Row="1" Grid.Column="1" Margin="5,0"
             HorizontalAlignment="Stretch" />
</Grid>
```

在示例中，控件中的 "Label" 是访问修饰符，双下划线在渲染输出中添加了一个下划线字符。

### 图 2-16：

TextBlock 和 Label 控件。

![](img/6df7bb88e9302e98442acc219cfbd7fc_618_0.png)

ProgressBar：最后一个仅显示控件是进度条。虽然技术上是 RangeBase 类的派类，但它没有通过 Slider 启用用户输入（见下一节）。图 2-17 显示了一个持续运动的条，其 `IsIndeterminate` 设置为 True。

```xml
<Grid>
  <Grid.RowDefinitions>
    <RowDefinition Height="Auto"/>
    <RowDefinition Height="Auto"/>
  </Grid.RowDefinitions>
  <ProgressBar Name="ConstantProgressBar" Grid.Row="0" Grid.Column="0"
               IsIndeterminate="True"
               Height="20" Width="200" Foreground="Blue"
               Background="White"/>
  <ProgressBar Grid.Row="1" Grid.Column="0" Maximum="100" Minimum="1"
               Value="50"
               IsIndeterminate="False" Height="20" Width="200"
               Foreground="Blue" Background="White"/>
</Grid>
```

图 2-17。
进度为 50% 的 ProgressBar 条。

![](img/6df7bb88e9302e98442acc219cfbd7fc_619_0.png)

## 基础输入控件

业务应用程序的主力是基础输入控件。你创建的每个窗口都能找到其中一些，而且它们非常直观。图 2-18 显示了单个窗口上的所有控件。以下是基础输入控件：

- TextBox 和 Password：TextBox 和 Password 都允许向窗口输入标准文本。Password 会混淆输入的字符（使用默认系统密码字符或开发者指定的字符），用于敏感信息。TextBox 通过 `Text` 属性暴露其内容。
- CheckBox：CheckBox 表示布尔值。`IsChecked` 属性允许三种状态选项。
- Radio buttons：单选按钮允许在一个组内进行单选。选项由 `GroupName` 决定。
- Slider：Slider 是范围输入。与 ProgressBar 类似，该控件接受 `Minimum`、`Maximum` 和 `Value`。
- DatePicker：Visual Studio 2012 新功能，DatePicker 控件提供了获取（或显示）日期的方法。
- Calendar：同样是 Visual Studio 2012 新功能，Calendar 为全显示模式。
- Button：Button 响应用户的点击。以下代码显示了使用事件处理程序实现的 Button。

