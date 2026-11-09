
![](img/9862a98a1a2d3bb14334137965a1ec60_703_0.png)

图 ASP-11.12

这些文件的说明如下：

- **ASP.NET 文件：**承载 **MainPage.xaml** 文件，并在 Silverlight 应用程序运行时加载。在我们的示例中，ASP.NET 文件是 **SilverlightApplication1TestPage.aspx**（图 ASP-11.12）。此页面是 Silverlight 4.0 应用程序的默认启动页。
- **HTML 文件：**承载 Silverlight 应用程序。在我们的示例中，HTML 文件是 **SilverlightApplication1TestPage.html**。
- **JavaScript 帮助文件：**提供 **createObject()** 和 **createObjectEx()** 等方法，用于将 Silverlight 应用程序嵌入网页。**createObject()** 和 **createObjectEx()** 方法用于在承载 Silverlight 应用程序的 aspx 或 html 测试页中创建并初始化 Silverlight 内容。在我们的示例中，Silverlight 帮助文件是 **Silverlight.js**。

除这些文件外，还有一个重要文件是在编译 Silverlight 应用程序后创建的。它称为**应用程序包**，扩展名为 **.xap**。**.xap**（读作 zap）文件包含运行 Silverlight 应用程序所需的所有文件和资源，如图 ASP-11.13 所示：

![](img/9862a98a1a2d3bb14334137965a1ec60_703_1.png)

图 ASP-11.13

请注意，只有在编译 Silverlight 应用程序后才能看到 .xap 文件。此文件出现在 Silverlight 应用程序项目文件夹内的 **Bin\Debug** 文件夹中。

![](img/9862a98a1a2d3bb14334137965a1ec60_704_0.png)

> 在“解决方案资源管理器”窗口中，您可能无法查看 Silverlight 应用程序项目文件夹内的 .xap 文件。要查看 .xap 文件，请单击“解决方案资源管理器”窗口工具栏中的“显示所有文件”按钮。

.xap 文件是部署单元，包含 Silverlight 应用程序的应用程序清单和程序集。应用程序清单以 **AppManifest.xaml** 存储，是一个 XAML 文件，其中包含 Silverlight 应用程序中所用程序集的列表。它使用 **Deployment** 和 **AssemblyPart** 元素将所需程序集列表以及应用程序程序集添加到应用程序中。编译应用程序后，应用程序程序集位于 **Bin\Debug** 文件夹中，其名称与 Silverlight 应用程序相同。例如，名为 **SilverlightApplication1** 的 Silverlight 应用程序的应用程序程序集是 **SilverlightApplication1.dll**。

![](img/9862a98a1a2d3bb14334137965a1ec60_704_1.png)

> 您可以将 .xap 文件的扩展名改为 .zip，并提取其中包含的文件。

现在让我们了解可在 Visual Studio 2010 中用于创建 Silverlight 应用程序的控件。

## Silverlight 应用程序中使用的控件

Visual Studio 2010 提供了各种控件来构建 Silverlight 4.0 应用程序的 UI。可以使用 XAML 和代码隐藏文件将这些控件添加到 Silverlight 应用程序中。默认情况下，会为 Silverlight 应用程序的 UI 创建 MainPage.xaml 文件。您可以在此文件中使用各种 XAML 元素来设计应用程序。您还可以将元素相互嵌套，并根据需要设置这些元素的不同属性。

在 Silverlight 中，控件由不同的 XAML 元素表示。添加到 Silverlight 应用程序中的控件或元素会成为分层树的一部分，随后呈现该树以向客户端显示控件。在 Silverlight 应用程序中，UserControl XAML 元素是分层树的根元素，默认情况下，UserControl 元素有一个 Grid 元素作为其子元素。如果要在应用程序中添加任何控件，需要将该控件放在 Grid 元素内，使其成为 Grid 元素的子元素。

表 11.1 列出了可在 Silverlight 4.0 应用程序中使用的各种控件：

表 11.1：Silverlight 4.0 中的控件

| 控件 | 描述 | XAML 元素示例 |
|---|---|---|
| AutoCompleteBox | 表示一个控件，该控件包含一个文本框和一个下拉列表，用户可在文本框中输入内容，下拉列表根据用户输入显示所有可能的匹配项。 | `<sdk:AutoCompleteBox x:Name="ACB" />` |
| Border | 允许您为其他控件添加边框和背景。 | `<Border BorderBrush="Blue" BorderThickness="3"/>` |
| Button | 允许您提供一个响应鼠标和键盘事件的按钮。 | `<Button Content="Hello" ClickMode="Press"/>` |
| Calendar | 允许您查看日历并处理日、月和年。 | `<Calendar DisplayMode="Month" IsTodayHighlighted="True"/>` |
| Canvas | 允许您在指定位置定位和排列所包含的控件。 | `<Canvas>`<br>`<Button Content="Hello" Canvas.Left="50" Canvas.Top="50"/>`<br>`</Canvas>` |
| CheckBox | 允许您提供便于选择选项的复选框。复选框可以处于选中、未选中或不确定状态。 | `<CheckBox ClickMode="Press" IsChecked="False" Content="Apple" />` |
| ComboBox | 允许您通过下拉列表显示项列表。 | `<ComboBox x:Name="selectFontSize" Width="80" Height="23">`<br>`<ComboBoxItem Content="1" />`<br>`<ComboBoxItem Content="2" IsSelected="True" />`<br>`<ComboBoxItem Content="3" />`<br>`<ComboBoxItem Content="4" />`<br>`</ComboBox>` |
| ContentControl | 指包含内容的控件。多个控件派生自 ContentControl 类。 | `<ContentControl Content="Silverlight" />` |
| DataGrid | 允许您以包含若干行和列的网格形式显示数据。 | `<sdk:DataGrid ItemsSource="Silverlight" AutoGenerateColumns="true" ColumnHeaderHeight="30" AlternatingRowBackground="Orchid" />` |
| DataPager | 提供一种 UI，有助于以多页形式显示大量数据集合。 | `<sdk:DataPager x:Name="DP1" PageSize="5" AutoEllipsis="True" NumericButtonCount="3" DisplayMode="PreviousNext" />` |
| DatePicker | 允许您从给定日历中选择特定日期，或键入所需日期。 | `<sdk:DatePicker IsTodayHighlighted="True" SelectedDateFormat="Short" />` |
| Ellipse | 允许您提供椭圆形形状。 | `<Ellipse Fill="Red" Height="50" Width="100" />` |
| Grid | 允许您按行和列排列所包含的控件。 | `<Grid Background="Yellow" ShowGridLines="True">`<br>`<Grid.RowDefinitions>`<br>`<RowDefinition Height="50" />`<br>`<RowDefinition Height="50" />`<br>`</Grid.RowDefinitions>`<br>`<Button Content="Silverlight" Grid.Row="0" />`<br>`</Grid>` |
| GridSplitter | 允许您提供一个可移动的 UI 元素，用于调整网格行与列之间的间距。 | `<sdk:GridSplitter Grid.Row="1" ShowsPreview="True" Height="10" Width="300" />` |
| HyperlinkButton | 允许您显示带超链接的按钮。 | `<HyperlinkButton Content="URL for Google" NavigateUri="http://www.google.com/" />` |
| Image | 允许您显示 .png 或 .jpg 图像。 | `<Image Height="300" Width="300" Source="Garden.jpg" />` |
| ItemsControl | 允许您显示项集合。许多允许显示项集合的控件都继承此控件的属性。 | `<ItemsControl ItemsSource="Silverlight" Height="270" Margin="100,0,0,0" />` |
| Label | 允许您显示简单的标题或消息。 | `<sdk:Label Content="Hello, this is a Label control" VerticalAlignment="Center" HorizontalAlignment="Center" />` |
| ListBox | 允许您显示项列表。 | `<ListBox Width="80" Height="100">`<br>`<ListBoxItem Content="Apple" Background="Yellow" />`<br>`<ListBoxItem Content="Mango" Background="Orange" />`<br>`<ListBoxItem Content="Strawberry" Background="Plum" />`<br>`</ListBox>` |
| MediaElement | 允许您承载音频和视频文件。 | `<MediaElement Height="100" Width="100" Source="Wildlife.wmv" />` |
| PasswordBox | 允许您输入用户无法查看和识别的密码字符。 | `<PasswordBox x:Name="PwdBox" Margin="210,0,0,0" Height="35" Width="200" PasswordChar="*" HorizontalAlignment="Left" />` |
| ProgressBar | 允许您指示任何操作的进度。 | `<ProgressBar x:Name="prgbar" Value="100" Margin="178,10,143,10" Maximum="200" Height="15" IsIndeterminate="False" />` |
| Popup | 允许您临时在其他控件上方显示信息。 | `<Popup IsOpen="True" HorizontalOffset="20" VerticalOffset="50">`<br>`<Popup.Child>`<br>`<Button x:Name="button1" Content="Hello" Height="30" Width="100" />`<br>`</Popup.Child></Popup>` |
| RadioButton | 允许您显示单选按钮来表示一个选项。 | `<RadioButton ClickMode="Press" Content="Apple" Margin="10,0,0,0" />`<br>`<RadioButton ClickMode="Press" Content="Mango" Margin="10,50,0,0" />`<br>`<RadioButton ClickMode="Press" Content="Strawberry" Margin="10,90,0,0" />` |

