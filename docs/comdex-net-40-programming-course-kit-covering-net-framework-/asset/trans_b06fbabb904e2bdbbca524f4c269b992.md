

```
```xml
<RowDefinition Height="*"/>
</Grid.RowDefinitions>
<Grid.ColumnDefinitions>
    <ColumnDefinition Width="50"/>
    <ColumnDefinition Width="80"/>
    <ColumnDefinition Width="*"/>
</Grid.ColumnDefinitions>
<Button Name="Button01" Grid.Row="0" Grid.Column="0" Background="Purple"
        Foreground="white" Content="Row1"/>
<GridSplitter Name="GridSplitter1" Grid.Row="1" Grid.ColumnSpan="3"
        Height="100" Width="245" ShowsPreview="true" ResizeDirection="Rows"
        ResizeBehavior="PreviousAndNext" HorizontalAlignment="Stretch"
        Background="Lavender" />
<Button Name="Button02" Grid.Row="2" Grid.ColumnSpan="3"
        Background="Navy" Foreground="white" Content="Row3"/>
</Grid>
</Window>
```

在清单 5.8 中，**Window** 元素的 **Title** 属性设置为 *MyGridSplitter 应用程序*。这意味着文本 *MyGridSplitter 应用程序* 显示在窗口的标题栏上。**Window** 元素有一个 **Grid** 控件作为其子元素，该控件被划分为九个单元格——三行三列。网格的第一行和第三行中有两个 **Button** 控件（**Button1** 和 **Button2**）。在第二行中，添加了一个 **GridSplitter** 控件。**GridSplitter** 控件的 **ShowsPreview** 属性设置为 **True**。将 **ShowsPreview** 属性设置为 **True** 会显示移动 **GridSplitter** 控件时如何调整行和/或列大小的预览。**GridSplitter** 控件的 **ResizeDirection** 和 **ResizeBehavior** 属性分别设置为 **Rows** 和 **PreviousAndNext**。这意味着 **GridSplitter** 控件只能调整行的大小，具体是上一行（第一行）和下一行（第三行）。

- 8. *按*键盘上的 F5 键运行应用程序。应用程序的输出出现，在网格的第二行中将 **GridSplitter** 控件显示为淡紫色条带（图 VB-5.35）。

- 9. 单击 **GridSplitter** 控件（图 VB-5.36）。出现一个带阴影的矩形区域，表示您可以在第一行和第三行之间重新分配的空间（图 VB-5.36）。

![](img/9862a98a1a2d3bb14334137965a1ec60_209_0.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_209_1.png)

- 10. *拖动*鼠标向上，将带阴影的矩形区域向上移动（图 VB-5.37）。

结果，第一行的宽度减小，第三行的宽度增大（图 VB-5.38）。

![](img/9862a98a1a2d3bb14334137965a1ec60_209_2.png)

![](img/9862a98a1a2d3bb14334137965a1ec60_209_3.png)

让我们讨论 Canvas 控件。

## 使用 Canvas 控件

考虑这样一种情况：您希望将控件放置在精确的位置，而不是在窗口（或页面）上移动它，也不是指定控件的边距来将其放置在适当位置。在这种情况下，可以使用 Canvas 控件，它允许您将其他控件（子控件）放置在其内部的精确或绝对位置。子控件通过相对于 Canvas 控件大小的坐标来定位。它是 Canvas 类的实例，而 Canvas 类派生自 Panel 类。表 5.9 列出了 Canvas 类的值得注意的属性：

| 属性 | 说明 |
|---|---|
| Bottom | 返回或设置一个值，该值指示 Canvas 控件底部与子控件底部之间的距离 |
| Left | 返回或设置一个值，该值指示 Canvas 控件左边框与子控件左边框之间的距离 |
| Right | 返回或设置一个值，该值指示 Canvas 控件右边框与子控件右边框之间的距离 |
| Top | 返回或设置一个值，该值指示 Canvas 控件顶部与子控件顶部之间的距离 |

> **表 5.9 中列出的属性是附加属性，并由 Canvas 控件的子控件使用。**

执行以下步骤，在 WPF 独立应用程序中使用 Canvas 控件：

- 1. 启动 Visual Studio 2010。
- 2. 从菜单栏中选择 **文件→新建→项目**。将打开 **新建项目** 对话框。
- 3. 在 **新建项目** 对话框左窗格的“已安装模板”部分中，选择 **Visual Basic→Windows**。
- 4. 在中间窗格中选择 **WPF 应用程序** 模板，以创建 WPF 独立应用程序。
- 5. 在 **名称** 文本框中输入应用程序名称 **MyCanvas**（也可在光盘中找到），并在 **位置** 组合框中为应用程序输入适当位置。
- 6. 单击 **确定** 按钮，关闭 **新建项目** 对话框并创建 **MyCanvas** 应用程序。
- 7. 将 **MainWindow.xaml** 文件的 XAML 视图中的默认代码替换为清单 5.9 中给出的代码：

### 清单 5.9：显示 **MainWindow.xaml** 文件的代码

```
```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MyCanvas Application" Height="250" Width="300">
    <Grid Background="Black">
        <Canvas Name="Canvas1" Height="100" Width="200" Background="LightYellow">
            <Button Name="Button1" Width="50" Height="25" Canvas.Top="15"
                    Canvas.Left="15" Background="Black" />
            <Button Name="Button2" Width="50" Height="25" Canvas.Bottom="15"
                    Canvas.Right="15" Background="Black" />
        </Canvas>
    </Grid>
</Window>
```
```

在清单 5.9 中，Window 元素的 Title 属性设置为 **MyCanvas Application**。这意味着文本 **MyCanvas Application** 显示在窗口的标题栏上。Window 元素有一个 Grid 控件作为其子元素，而 Grid 控件又有一个 Canvas 控件作为其子元素。Grid 控件的 Background 属性设置为 **Black**。Canvas 控件有两个按钮（名为 **Button1** 和 **Button2**）作为其子元素。**Button1** 出现在距离 **Canvas** 控件顶部和左侧各 15 个单位的位置。类似地，**Button2** 出现在距离 **Canvas** 控件底部和右侧各 15 个单位的位置。

- 8. **按**键盘上的 F5 键运行应用程序。应用程序的输出如图 VB-5.39 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_211_0.png)

图 VB-5.39

如图 VB-5.39 所示，**Canvas** 控件内出现两个按钮（黑色），该控件具有浅黄色背景。其中一个按钮出现在 **Canvas** 控件的左上角，另一个出现在 **Canvas** 控件的右下角。

## 使用 StackPanel 控件

假设您希望在 WPF 窗口（或页面）上放置多个控件，使一个控件出现在另一个控件上方，形成控件的垂直堆叠。在这种情况下，可以使用 **StackPanel** 控件，而不是使用 **Grid** 或 **Canvas** 控件并将控件放置在精确位置。**StackPanel** 控件是一个容器控件，允许您将子控件排列在垂直或水平堆叠中。默认情况下，**StackPanel** 控件的子控件垂直堆叠。垂直堆叠从 **StackPanel** 控件的顶部开始，到其底部结束。您也可以水平堆叠子控件。水平堆叠从 **StackPanel** 控件的左边缘开始，到其右边缘结束。**StackPanel** 控件是 **StackPanel** 类的实例，而 **StackPanel** 类派生自 **Panel** 类。表 5.10 列出了 **StackPanel** 类的值得注意的属性：

| 属性 | 说明 |
|---|---|
| CanHorizontallyScroll | 返回或设置一个值，该值指示 StackPanel 控件是否可以水平滚动 |
| CanVerticallyScroll | 返回或设置一个值，该值指示 StackPanel 控件是否可以垂直滚动 |
| Orientation | 返回或设置一个值，该值指示 StackPanel 控件的子控件是水平堆叠还是垂直堆叠 |

执行以下步骤，在 WPF 独立应用程序中使用 **StackPanel** 控件：

- 1. *启动* Visual Studio 2010。
- 2. *从菜单栏中选择* 文件→新建→项目。将打开新建项目对话框。
- 3. *选择*新建项目对话框左窗格中“已安装模板”部分中的 Visual Basic→Windows。
- 4. *选择*中间窗格中的 WPF Application 模板，以创建 WPF 独立应用程序。
- 5. 在 **名称** 文本框中输入应用程序名称 **MyStackPanel**（也可在光盘中找到），并在 **位置** 组合框中为应用程序输入适当位置。
- 6. 单击 **确定** 按钮，关闭 **新建项目** 对话框并创建 **MyStackPanel** 应用程序。
- 7. *替换* **MainWindow.xaml** 文件的 XAML 视图中的默认代码为清单 5.10 中给出的代码：

