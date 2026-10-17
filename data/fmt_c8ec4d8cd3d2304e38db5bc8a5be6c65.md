
| | TextWrapping | Wrap |
| | Text | |
| | VerticalAlignment | Top |
| | FontSize | 20 |
| 控件 | 属性 | 数值 |
| --- | --- | --- |
|（注） | | |

以下 XAML 标记显示了这些控件：

```
<TextBlock HorizontalAlignment="Left" Margin="330,190,0,0"
TextWrapping="Wrap">
<Text="ID" VerticalAlignment="Top" FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="460,190,0,0"
TextWrapping="Wrap">
<Text="Title" VerticalAlignment="Top" FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="620,190,0,0"
TextWrapping="Wrap">
<Text="First Name" VerticalAlignment="Top" FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="975,190,0,0"
TextWrapping="Wrap">
<Text="Last Name" VerticalAlignment="Top" FontSize="20"/>
```

| Control | Property | Value |
| --- | --- | --- |
| | TextWrapping | Wrap |
| | Text | Email |
| | VerticalAlignment | Top |
| | FontSize | 20 |
| First TextBox | x:Name | email |
| | HorizontalAlignment | Left |
| | Margin | 450,390,0,0 |
| | TextWrapping | Wrap |
| | Text | Leave Empty |
| | VerticalAlignment | Top |
| | Width | 400 |
| | FontSize | 20 |
| Second TextBlock | HorizontalAlignment | Left |
| | Margin | 300,540,0,0 |
| | TextWrapping | Wrap |
| | Text | Phone |
| | VerticalAlignment | Top |
| | FontSize | 20 |
| Control | Property | Value |
| --- | --- | --- |
| Second TextBox | x:Name | phone |
| HorizontalAlignment | Left |
| Margin | 450,540,0,0 |
| TextWrapping | Wrap |
| Text | Leave Empty |
| VerticalAlignment | Top |
| Width | 200 |
| FontSize | 20 |

这些控件的 XAML 标记应该如下所示：

点击此处查看代码图像

```
<TextBlock HorizontalAlignment="Left" Margin="300,390,0,0"
TextWrapping="Wrap"
Text="Email" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="email" HorizontalAlignment="Left"
Margin="450,390,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="400"
FontSize="20"/>
<TextBlock HorizontalAlignment="Left" Margin="300,540,0,0"
TextWrapping="Wrap"
Text="Phone" VerticalAlignment="Top" FontSize="20"/>
<TextBox x:Name="phone" HorizontalAlignment="Left"
Margin="450,540,0,0"
TextWrapping="Wrap" Text="" VerticalAlignment="Top" Width="200"
FontSize="20"/>
```

在设计视图中完成的表单应该如图像所示。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_977_0.png)

12. 在“调试”菜单上，选择“开始调试”以生成并运行应用程序。

应用程序启动并显示表单。你可以向表单中输入数据并从组合框中选择标题，但你还无法进行其他操作。然而，一个更大的问题是，取决于你屏幕的分率，表单看起来非常糟糕。（如果表单看起来正常，请拖动右边缘使其变窄）。显示器的右侧被截断了，大部分文本发生了换行，而且“姓”文本框被截断了。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_978_0.png)

13. 选择并拖动窗口的右侧以扩展显示，使文本和控件以在 Visual Studio 设计视图窗口中出现的方式显示。这是该表单设计的最佳尺寸。

14. 调整显示“客户”应用程序的窗口到其最小宽度。此时，表单的大部分消失了。部分 TextBlock 内容发生了换行，但表单在当前视图下显然是不可用的。

15. 返回到 Visual Studio，在“调试”菜单上，选择“停止调试”。

这节课是一个关于如何小心布局应用程序的教训。尽管应用程序在与设计视图相同大小的窗口中运行时看起来良好，但只要你一将窗口重新调整为更窄的视图，它就变得毫无用处（甚至完全没法用）。此外，应用程序假设用户将在处于横向模式的设备上查看屏幕。如果你临时将设计视图窗口切换到 12 英寸平板电脑设备形状，并选择纵向模式按钮，你就可以看到如果用户在支持不同方向的平板电脑上运行应用程序并旋转设备切换到纵屏模式，表单会是什么样子。（之后不要忘记切换回 13.3 英寸桌面设备形状。）

问题在于，到目前为止的布局技术无法扩展并适应不同的设备形状和方向。幸运的是，你可以使用 Grid 控件的属性以及另一个称为“视觉状态管理器”（Visual State Manager）的功能来解决这些问题。

# 使用 Grid 实现表格化布局

你可以使用 Grid 控件来实现表格化布局。Grid 包含行和列，你可以指定其他元素应该放在哪些行和列中。

Grid 控件的妙之处在于，你可以指定其包含的行和列的大小为相对值。这样，如果网格缩小或增大以适应用户可能切换的不同设备形状和方向，行和列也可以随着网格按比例缩小或增大。网格中行和列的交叉点定义了一个单元格，如果你将控件放在单元格中，它们将随着行和列的缩小和增大而移动。因此，实现可扩展 UI 的关键将其分解为单元格集合，并将相关元素放在同一个单元格中。单元格甚至可以包含另一个网格，让你能够精细调整每个元素的精确位置。

如果你考虑“客户”应用程序，你可以看到 UI 分为两个主要区域：包含标题的头部和包含客户详情的正文。在这些区域之间留出一些间距并在表单底部留出边距，你可以为这些每个区域分配相对大小，如图所示。

| Adventure Works 客户 | 2x |
|---|---|
| ID | 标题 | 名字 | 姓 | x |
| | | | | | |
| 电子邮件 | | | | |10x |
| 电话 | | | | 2x |

该图仅显示了粗略的估计，但标题行是下方间距行的高度的两倍。正文行的高度是间距行的 10 倍，底部边距是间距高度的两倍。

为了保存每个区域中的元素，你可以定义一个具有四行的网格并在每行中放置适当的项目。然而，表单的正文可以用另一个更复杂的网格来描述，如图所示：

| | 标题 | 名字 | 姓 | y |
|---|---|---|---|---|
| ID | | | | y |
| | | | | 2y |
| 电子邮件 | | | | | y |
| | | | | 2y |
| 电话 | | | | | y |
| | | | | | 4y |
| z | z | z | 2z | 2z | z |

再次，每行的高度都是按相对值指定的，每列的宽度也是如此。此外，你可以清楚地看到“电子邮件”和“电话”的 TextBox 元素并不完全符合这个网格模式。如果你非常严苛，可能会选择在表单正体内定义更多的网格来使这些项目适应。然而，你应该记住此网格的目的：定义元素的相对位置和间距。因此，元素超出网格布局中单元格的边界是可以的。

在下一个练习中，你将修改“客户”应用程序的布局，使用这种网格格式来放置控件。

# 修改布局以扩展到不同的设备形状和方向

+ 1. 在“客户”应用程序的 XAML 名称中，在现有控件内部、TextBlock 控件之前添加另一个 Grid。为此 Grid 控件设置距离父控件左右边缘 10 像素的边距，距离顶部和底部 20 像素的边距，如下代码加粗所示：

点击此处查看代码图像

```
<Grid>
  <Grid Margin="10,20,10,20">
  </Grid>
  <TextBlock HorizontalAlignment="Left" TextWrapping="Wrap" Text="Adventure Works Customers" ... />
</Grid>
```

> 注意 可以将行定义为现有 Grid 控件的一部分，但为了保持与 UWP 应用一致的外，你应该在左侧和顶部留出一些空间。

+ 2. 在新的 Grid 控件中添加以下加粗的 `<RowDefinitions>` 部分：

点击此处查看代码图像

```
<Grid Margin="10,20,10,20">
  <Grid.RowDefinitions>
    <RowDefinition Height="2*"/>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10*"/>
    <RowDefinition Height="2*"/>
  </Grid.RowDefinitions>
</Grid>
```

`<RowDefinitions>` 部分定义了网格的行。在示例中，你定义了四行。你可以用绝对值指定行的大小，也可以使用 * 运算符表示大小是相对的，Windows 在应用程序运行时根据设备形状和屏幕分辨率自行计算行的大小。示例中的值与之前所示客户表单头部、正文、间距和底部边距的相对行大小对应。

+ 3. 将包含文本 Adventure Works Customers 的 TextBlock 控件移动到 Grid 控件内部，紧接 `</GridDefinitions>` 标签之后、 `</Grid>` 标签之前。

+ 4. 为 TextBlock 控件添加 `Grid.Row` 属性并将值设置为 0。

点击此处查看代码图像

```
<Grid Margin="10,20,10,20">
  <Grid.RowDefinitions>
    ...
  </Grid.RowDefinitions>
  <TextBlock Grid.Row="0" ... Text="Adventure Works Customers" ... />
</Grid>
```

这表示 TextBlock 元素应该放置在 Grid 控件的第一行中。（Grid 控件的行和列从 0 开始计数）。

`Grid.Row` 属性是一个附加属性（attached property）的示例。附加属性是控件从其所属的容器控件接收的属性。在网格之外，TextBlock 没有 `Row` 属性，因为这将毫无意义。当被放置在网格内部时，`Row` 属性被附加到 TextBlock 控件上，TextBlock 控件可以为其赋值。然后 Grid 就会使用该值来决定显示 TextBlock 控件的位置。附加属性很容易排序，因为它们具有 `容器类型.属性名` 的形式。

- 移除 TextBlock 控件的 `Margin` 属性，并将 `HorizontalAlignment` 和 `VerticalAlignment` 属性设置为 `Center`。这将导致 TextBlock 在行中居中显示。Grid 和 TextBlock 控件的 XAML 标记应该如下所示（对 TextBlock 的更改已用**粗体**标记）：

点击此处查看代码图片

```
<Grid Margin="10,20,10,20">
  </Grid.RowDefinitions>
  <TextBlock Grid.Row="0" HorizontalAlignment="Center"
TextWrapping="Wrap"
Text="Adventure Works Customers" VerticalAlignment="Center"
FontSize="50"/>
</Grid>
```

- 在 TextBlock 控件之后，添加另一个嵌套的 Grid 控件。该 Grid 控件将用于布局表体中的控件。它应该出现在外层 Grid 控件的第三行（大小为 10 的行），因此如下代码所示，将 `Grid.Row` 属性设置为 2：

点击此处查看代码图片

```
<Grid Margin="10,20,10,20">
  <Grid.RowDefinitions>
    <RowDefinition Height="2*"/>
    <RowDefinition Height="*"/>
    <RowDefinition Height="10*"/>
    <RowDefinition Height="2*"/>
  </Grid.RowDefinitions>
  <TextBlock Grid.Row="0" HorizontalAlignment="Center" ... />
```

```
<Grid Grid.Row="2">
</Grid>
...
</Grid>
```

7. 在新的 Grid 控件中添加以下 `<Grid.RowDefinitions>` 和 `<Grid.ColumnDefinitions>` 部分：

点击此处查看代码图片

```
<Grid Grid.Row="2">
<Grid.RowDefinitions>
<RowDefinition Height="*">
<RowDefinition Height="*">
<RowDefinition Height="2*">
<RowDefinition Height="*">
<RowDefinition Height="2*">
<RowDefinition Height="*">
<RowDefinition Height="*">
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
<ColumnDefinition Width="*">
<ColumnDefinition Width="*">
<ColumnDefinition Width="20*">
<ColumnDefinition Width="*">
<ColumnDefinition Width="20*">
<ColumnDefinition Width="2*">
<ColumnDefinition Width="20*">
<ColumnDefinition Width="2*">
<ColumnDefinition Width="*">
</Grid.ColumnDefinitions>
</Grid>
```

这些行和列定义指定了之前图中描述表体结构的每行每列的高度和宽度。在放置控件的每列之间有 20 像素的微小间距。

8. 将显示 ID、Title、First Name（名）和 Last Name（姓）标签的 TextBlock 控件移动到嵌套的 `<Grid.ColumnDefinitions>` 标签内部。

9. 将每个 TextBlock 控件的 `Grid.Row` 属性设置为 0（这些标签将出现在网格的第一行）。然后将 ID 标签的 `Grid.Column` 属性设置为 1，Title 标签的 `Grid.Column` 属性以及 First Name 标签的 `Grid.Column` 属性设置为 5，Last Name 标签的 `Grid.Column` 属性设置为 7。

- 10. 移除每个 TextBlock 控件的 `Margin` 属性，并将 `HorizontalAlignment` 和 `VerticalAlignment` 属性设置为 `Center`。这些控件的 XAML 标记应该如下所示（更改已用**粗体**标记）：

点击此处查看代码图片
