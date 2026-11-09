
执行以下步骤，在 WPF 独立应用程序中使用 **TextBlock** 控件：

- 1. 启动 Visual Studio 2010。
- 2. 从菜单栏中 *选择* **文件→新建→项目**。此时将打开 **新建项目** 对话框。
- 3. 在 **新建项目** 对话框左侧窗格的 **已安装模板** 部分中 *选择* **Visual Basic→Windows**。
- 4. 在中间窗格中 *选择* **WPF 应用程序** 模板，以创建 WPF 独立应用程序。
- 5. 在 **名称** 文本框中输入应用程序的名称 **MyTextBlock**（也可在 CD 上获得），并在 **位置** 组合框中输入合适的应用程序位置。
- 6. 单击 **确定** 按钮关闭 **新建项目** 对话框，并创建 **MyTextBlock** 应用程序。
- 7. 将 **MainWindow.xaml** 文件的 XAML 视图中的默认代码*替换*为清单 5.6 中给出的代码：

**清单 5.6：** 显示 TextBlock 控件的代码

```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MyTextBlock Application" Height="250" Width="300">
    <Grid>
        <TextBlock Name="TextBlock1" Margin="10,10,0,0" Height="100" Width="200"
                   Text="This is a TextBlock control in a WPF application."
                   Foreground="white" Background="black" FontSize="17" FontWeight="Bold"
                   TextWrapping="Wrap" TextAlignment="Center" />
    </Grid>
</Window>
```

在清单 5.6 中，Window 元素的 Title 属性设置为 MyTextBlock Application。这意味着 MyTextBlock Application 文本将显示在窗口的标题栏上。Window 元素有一个 Grid 控件作为其子元素，而该 Grid 控件又包含一个 TextBlock 控件。TextBlock 控件的 Text 属性表示显示在控件上的文本。TextBlock 控件的 Foreground 和 Background 属性分别设置为 White 和 Black。这意味着 TextBlock 控件中的文本以白色显示，而控件背景以黑色显示。该控件的 FontSize 和 FontWeight 属性分别设置为 17 和 Bold，以使文本显示得更大。此外，TextWrapping 和 TextAlignment 属性分别设置为 Wrap 和 Center。这意味着文本（如果跨越多行）会在 TextBlock 控件中换行，并居中显示在 TextBlock 控件中。

- 8. 按键盘上的 **F5** 键运行应用程序。应用程序的输出如 Fig.VB-5.33 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_206_0.png)

Fig.VB-5.33

现在我们来讨论 Border 控件。

## 使用 Border 控件

WPF 中的 Border 控件允许您向其他 WPF 控件添加边框、背景或两者兼有。它只能有一个子控件，也就是说，不能将 Border 控件与多个子控件一起使用。Border 控件是 Border 类的一个实例。表 5.7 列出了 **Border** 类的重要属性：

**表 5.7：Border 类的重要属性**

| 属性 | 描述 |
|---|---|
| Background | 返回或设置另一个控件的背景 |
| BorderBrush | 返回或设置 Border 控件的颜色 |
| BorderThickness | 返回或设置 Border 控件的相对粗细 |
| CornerRadius | 返回或设置 Border 控件圆角的程度 |

执行以下步骤，在 WPF 独立应用程序中使用 **Border** 控件：

- 1. *启动* **Visual Studio 2010**。
- 2. 从菜单栏中 *选择* **文件→新建→项目**。此时将打开 **新建项目** 对话框。
- 3. 在 **新建项目** 对话框左侧窗格的 **已安装模板** 部分中 *选择* **Visual Basic→Windows**。
- 4. 在中间窗格中 *选择* **WPF 应用程序** 模板，以创建 WPF 独立应用程序。
- 5. 在 **名称** 文本框中输入应用程序的名称 **MyGridWithBorder**（也可在 CD 上获得），并在 **位置** 组合框中输入合适的应用程序位置。
- 6. *单击* **确定** 按钮关闭 **新建项目** 对话框，并创建 **MyGridWithBorder** 应用程序。
- 7. 将 **MainWindow.xaml** 文件的 XAML 视图中的默认代码*替换*为清单 5.7 中给出的代码：

**清单 5.7：显示 Border 控件的代码**

```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MyGridWithBorder Application" Height="250" Width="300">
    <Grid>
        <Border Name="Border1" BorderBrush="Gray" BorderThickness="15"
                CornerRadius="45" Background="Pink">
            <Border Name="Border2" Height="120" Width="170" BorderBrush="Black"
                    BorderThickness="9">
                <Button Name="Button1" Height="100" Width="150" Content="Border
                        Example" FontWeight="Bold"/>
            </Border>
        </Border>
    </Grid>
</Window>
```

在清单 5.7 中，Window 元素的 **Title** 属性设置为 **MyGridWithBorder Application**。这意味着 **MyGridWithBorder Application** 文本将显示在窗口的标题栏上。**Window** 元素有一个 **Grid** 控件作为其子元素，而该 **Grid** 控件又包含两个 **Border** 控件。第一个 **Border** 控件（**Border1**）应用于 **Grid**，其 **Background** 属性设置为 **Pink**。**Border** 控件的 **BorderBrush** 和 **BorderThickness** 属性分别设置为 **Gray** 和 15。此外，**Border1** 的 **CornerRadius** 属性设置为 45，也就是说，边框的圆角为 45 度。这意味着 **Grid** 控件具有粉红色背景和灰色边框，边框厚度为 15 个单位，圆角为 45 度。第二个 **Border** 控件（**Border2**）有一个 **Button** 控件作为其子元素。这意味着第二个边框应用于 **Button** 控件。**Border2** 的 **BorderBrush** 和 **BorderThickness** 属性分别设置为 Black 和 9。这意味着 **Button** 控件带有 9 个单位厚的黑色边框。

- 8. *按*键盘上的 **F5** 键运行应用程序。应用程序的输出如 Fig. VB-5.34 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_208_0.png)

Fig. VB-5.34

如 Fig.VB-5.34 所示，网格具有灰色边框；而 **Border Example** 按钮具有黑色边框。

## 使用 GridSplitter 控件

WPF 中的 GridSplitter 控件提供了一项独特功能，允许您重新分配 Grid 控件的单元格（行和列）之间的空间。使用 GridSplitter 控件时，Grid 控件的高度和宽度不会改变；只有网格单元格之间的空间会改变。GridSplitter 控件是 GridSplitter 类的一个实例。表 5.8 列出了 GridSplitter 类的重要属性：

| 属性 | 描述 |
|---|---|
| PreviewStyle | 返回或设置一个样式，该样式自定义 GridSplitter 控件预览指示器的外观、效果或其他样式特征；当 ShowsPreview 属性设置为 True 时显示该指示器 |
| ResizeBehavior | 返回或设置相对于定义 GridSplitter 控件的列或行，调整哪些列或行的大小 |
| ResizeDirection | 返回或设置一个值，指示 GridSplitter 控件是调整行的大小还是调整列的大小 |
| ShowsPreview | 返回或设置一个值，指示当用户拖动该控件时 GridSplitter 控件是否更新列或行的大小 |

执行以下步骤，在 WPF 独立应用程序中使用 **GridSplitter** 控件：

- 1. *启动* Visual Studio 2010。
- 2. 从菜单栏中 *选择* **文件→新建→项目**。此时将打开 **新建项目** 对话框。
- 3. 在 **新建项目** 对话框左侧窗格的 **已安装模板** 部分中 *选择* **Visual Basic→Windows**。
- 4. 在中间窗格中 *选择* **WPF 应用程序** 模板，以创建 WPF 独立应用程序。
- 5. 在 **名称** 文本框中输入应用程序的名称 **MyGridSplitter**（也可在 CD 上获得），并在 **位置** 组合框中输入合适的应用程序位置。
- 6. 单击 **确定** 按钮关闭 **新建项目** 对话框，并创建 **MyGridSplitter** 应用程序。
- 7. 将 **MainWindow.xaml** 文件的 XAML 视图中的默认代码*替换*为清单 5.8 中给出的代码：

**清单 5.8：显示 MainWindow.xaml 文件的代码**

```xml
<Window x:Class="MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="MyGridSplitter Application" Height="250" Width="300">
    <Grid>
        <Grid.RowDefinitions>
            <RowDefinition Height="100" />
            <RowDefinition Height="15" />
```
