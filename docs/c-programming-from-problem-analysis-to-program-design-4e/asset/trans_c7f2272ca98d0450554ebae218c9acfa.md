
### 示例 15.18

```xml
<!--Uncomment to see an alignment grid to help ensure your controls are
    aligned on common boundaries. The image has a top margin of
    -32px to account for the System Tray. Set this to 0 (or remove
    the margin altogether) if the System Tray is hidden. Before
    shipping remove this XAML and the image itself.-->

<!--<Image Source="/Assets/AlignmentGrid.png"
       VerticalAlignment="Top" Height="800"
       Width="480" Margin="0, -32, 0, 0" Grid.Row="0"
       Grid.RowSpan="2"
       IsHitTestVisible="False" />-->
```

一旦通过删除注释标记，取消包含 `Image Source="/Assets/AlignmentGrid.png"` 的那一行（如示例 15-18 所示）的注释，就会在手机 **设计器** 窗口中添加一个对齐网格。无需实际删除注释符号，你可以选中该行，然后按 **Ctrl+E, U**，或单击 Visual Studio 工具栏上的 **取消注释**。

用户界面的可用区域小得多，因此设计极其重要。构建直观的界面，注意不要令用户望而生畏，而应让他们对你的布局感到自在。专注于应用所提供的内容。在设计时专注于你试图达成的目标，并持续努力创建一个清晰、整洁、外观一致的应用。你应当为自己的工艺感到自豪，并让应用看起来美观。取消该部分代码的注释后，对齐网格可以帮助你完成这些工作。

## 代码隐藏文件

到目前为止，尚未在 `MainPage.xaml.cs` 文件中键入任何程序语句。这是代码隐藏文件，即存放事件处理程序方法代码的文件。如之前所见，你可以使用 **属性** 窗口中的 **事件** 图标来注册事件。双击控件仍会注册默认事件处理程序。

通过双击 **Go** 按钮，可为该按钮注册 Click 事件。这样做会打开 `.xaml.cs` 文件，并在该文件中放置 `btnGo_Click()` 事件处理程序方法的标头。在此方法中，从 `txtBxURL` 文本框中检索用户提供的文本。该值作为参数发送给 `WebBrowser` 控件的 `Navigate()` 方法。`btnGo_Click()` 事件处理程序如示例 15-19 所示。

### 示例 15.19

```csharp
private void btnGo_Click(object sender, RoutedEventArgs e)
{
    string site = txtBxURL.Text;
    webWindow.Navigate(new Uri(site, UriKind.Absolute));
}
```

如图 15-19 所示，Uri 类的对象作为参数发送给 Navigate( ) 方法。URI 代表通用资源标识符。C# 中的 Uri 类表示 URI，例如像 "http://WindowsPhone.com" 这样的网址。在 C# 中，你可以直接用字符串管理 URI 数据。Uri 类提供了许多属性，以及一种访问 URI 各部分的简便方式。你可以使用 Uri 类操作和组合 URI。在示例 15-19 中，通过检索在 txtBxURL 文本框中输入的字符串值，实例化了一个匿名、未命名的 Uri 对象。请注意，在第一条程序语句中，该值被存储在名为 site 的字符串变量中。字符串 site 是构造函数的第一个参数。Uri 构造函数的第二个参数是 Absolute。UriKind 可以取三个值之一：Relative、Absolute 或 RelativeOrAbsolute。这里，由于在文本框中键入了完整 URL 地址，因此选择了 Absolute。一旦获得 Uri 对象，就将其发送到 webWindow WebBrowser 对象。

启动此应用时，不会自动加载任何页面。相反，文本框中会出现 http://。这使用户能够补全他们想要访问的站点地址。

> 注意
> 有一个可以注册的 Loaded( ) 事件。如果你希望自动加载某个特定网页，可以注册一个 Loaded( ) 事件，并将你希望加载的网站地址作为第一个参数发送给 Navigate( ) 方法。

想在 GUI 上显示图像吗？将图片放入解决方案的 Assets 文件夹。Assets 是自动为你创建的项目文件夹之一。你会在“解决方案资源管理器”窗口中看到该文件夹。使其可用的一种简单方法是将它复制并粘贴到 Assets 文件夹中。要将图片放入 Assets 文件夹，你可以使用标准的 Windows 复制 (Ctrl+C) 和粘贴 (Ctrl+V) 快捷键。然后从工具箱中将 Image 控件拖放到手机设计器窗格上。使用标准的 Windows 大小调整手柄移动并调整 Image 控件的大小。要将 Image 控件链接到实际图片，请使用属性窗口中“常用”类别下列出的 Source 属性。下拉列表会显示应用程序可用的图像。如果你的图片存储在 Assets 文件夹中，你会看到它作为 Source 属性下的选项之一列出。

当你探索控件及其成员时，会看到许多与 Windows 应用程序中使用的相同的控件和属性。控件数量更少，但仍然非常丰富，并提供大量功能。例如，如果你希望应用程序启动时文本框获得焦点，可以将 txtBxURL.Focus( ) 添加到 Loaded( ) 事件处理程序方法中。这样做会在应用启动时将光标定位到文本框中，并自动显示手机键盘。此应用程序未这样做。除了 btnGo_Click( ) 事件处理程序方法中包含的内容之外，此应用程序未添加其他程序语句。Click="btnGo_Click" 标记已添加到 .xaml 文件中。下一节将讨论 .xaml 代码。

## XAML 代码

查看 .xaml 文件时，请注意使用 Grid 控件将项放置在页面上。名为 LayoutRoot 的顶层 Grid 有一个 StackPanel。该 StackPanel 名为 TitlePanel，并带有标记 Grid.Row="0"。另一个名为 ContentPanel 的 Grid 放置在 Grid.Row="1"。选择 Windows Phone 应用模板时，这些内容会默认添加。查看示例 15-20 中的文件内容，可以看到 StackPanel 上 TextBlock 对象的 Text 标记的值。

### 示例 15.20

```xml
<phone:PhoneApplicationPage
    <!--Tags at the top of the .xaml file and the comments relating to
        localization are not shown here due to space constraints.-->

    <!--LayoutRoot is the root grid where all page content is placed-->
    <Grid x:Name="LayoutRoot" Background="Transparent">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>

        <!--TitlePanel contains the name of the application and page title-->
        <StackPanel x:Name="TitlePanel" Grid.Row="0"
                    Margin="12,17,0,28">
            <TextBlock Text="Windows 8 App"
                       Style="{StaticResource PhoneTextNormalStyle}"
                       Margin="12,0,0,0"/>
            <TextBlock Text="Web Browser"
                       Margin="9,-7,0,0"
                       Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>

        <!--ContentPanel - place additional content here-->
        <Grid x:Name="ContentPanel" Grid.Row="1"
              Margin="12,0,12,0">
            <TextBox x:Name="txtBxURL"
                     TextWrapping="Wrap" Text="http://"
                     Margin="0,0,0,75" Height="530"/>
            <Button x:Name="btnGo" Content="Go"
                    Margin="364,10,0,0" HorizontalAlignment="Left"
                    Width="92" Click="btnGo_Click"/>
            <phone:WebBrowser x:Name="webWindow" Margin="10,82,0,0"
                              Height="515" Width="436"/>
        </Grid>
    </Grid>
</phone:PhoneApplicationPage>
```

示例 15-20 未显示自动插入到 .xaml 文件顶部的 XML 标记。回想一下 `Image Source="Assets/AlignmentGrid.png"` 标记，它表明 .xaml 文件中的放置网格已取消注释。回顾示例 15-18。该网格仅用于开发。注释建议在部署应用程序之前移除该文件和 `Image Source` 标记。设计达到可接受程度后，通过删除 `Image Source` 标记和多余注释行来移除对齐网格。

## 运行应用

完成设计并准备好测试和调试后，你可以像处理其他 Visual Studio 项目一样生成解决方案。**生成** 菜单中有 **生成解决方案** 和生成项目的选项，快捷键分别为 **F6** 和 **Shift+F6**。与其他类型的项目一样，你可以跳过此步骤，并使用 **开始调试** 或 **开始执行（不调试）** 启动应用程序。在此之前，你需要确定应用的输出将显示在哪里。你有两个选项。如果有 Windows 8 Phone 设备，可以将其部署到设备。或者，你可以使用 Visual Studio Windows 8 Phone 模拟器。模拟器使你能够看到应用在 Windows 8 设备上的外观。两个选项都有你可能会遇到的问题。下一节将讨论这些问题。

### 部署到模拟器

已安装的 SDK 中包含一个 Windows Phone 模拟器。该模拟器在 Windows PC 上作为 Hyper-V 虚拟机运行。它拥有与“真实”手机相同的大部分软件。你可以使用 PC 鼠标和/或键盘控制模拟器。你可以执行位置和方向模拟、管理模拟器环境，甚至更改模拟器上的设置。

要使用模拟器，你必须在支持二级地址转换 (SLAT) 的 64 位计算机上运行 Windows 8 专业版操作系统或更高版本。i3、i5、i7 和 i9 等基于 Intel 的处理器支持 SLAT，基于 Nehalem、Westmere 或 Sandybridge 微架构的 CPU 也支持 SLAT。模拟器无法在 Windows 8 家庭版下运行。你可以仅运行 Windows 8 家庭版来设计和创建应用程序，但要启动模拟器，必须使用运行 Windows 8 专业版的计算机。此外，模拟器要求启用 Hyper-V，而该功能在 Windows 8 家庭版中不可用。

> 注意
> Hyper-V 是虚拟机管理器，是一种创建并运行虚拟机的软件。必须启用 Hyper-V 功能。如果你收到错误消息“无法启动 Windows Phone 模拟器，因为你的 PC 缺少 Hyper-V 先决条件”，并且你运行的是 Windows 8 专业版，则可能需要转到“控制面板”>“程序和功能”>“启用或关闭 Windows 功能”，然后选中 Hyper-V 旁边的复选框以启用它。

