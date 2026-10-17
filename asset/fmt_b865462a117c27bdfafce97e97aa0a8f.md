
| `EnterActions`, `ExitActions` | 而不是定义 setter，你可以定义 `EnterActions` 和 `ExitActions`。在这两个属性中，你可以定义一组 `TriggerAction` 元素。`EnterActions` 在触发器开始时触发（对于属性触发器，当 `Property`/`Value` 组合适用时）；`ExitActions` 在其结束前触发（就在 `Property`/`Value` 组合不再适用时）。可通过这些操作指定的触发器操作派生自基类 `TriggerAction`，例如 `SoundPlayerAction` 和 `BeginStoryboard`。使用 `SoundPlayerAction`，你可以开始播放声音。`BeginStoryboard` 与本章后面讨论的动画一起使用。

#### MultiTrigger

属性触发器在属性值更改时触发。如果需要因为两个或多个属性具有特定值而设置触发器，可以使用 `MultiTrigger`。

`MultiTrigger` 具有 `Conditions` 属性，可指定属性的有效值。它还具有 `Setters` 属性，可让你指定需要设置的属性。在以下示例中，为 `TextBox` 元素定义了一种样式，使得当 `IsEnabled` 属性为 `True` 且 `Text` 属性值为 `Test` 时触发器适用。尝试在空白文本框中输入 Test。如果两者都适用，则 `TextBox` 的 `Foreground` 属性将设置为 `Red`（代码文件 `TriggerSamples/MultiTriggerWindow.xaml`）：

```
<Window x:Class="TriggerSamples.MultiTriggerWindow"

xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"

    Title="Multi Trigger" Height="300" Width="300">

<Window.Resources>

    <Style TargetType="TextBox">

        <Style.Triggers>

            <MultiTrigger>

                <MultiTrigger.Conditions>

                    <Condition Property="IsEnabled" Value="True" />

                    <Condition Property="Text" Value="Test" />

                </MultiTrigger.Conditions>

                <MultiTrigger.Setters>

                    <Setter Property="Foreground" Value="Red" />

                </MultiTrigger.Setters>

            </MultiTrigger>

        </Style.Triggers>

    </Style>

</Window.Resources>

<Grid>

    <TextBox />

</Grid>

</Window>
```

#### 数据触发器

当绑定到控件的数据满足特定条件时，数据触发器就会触发。在下面的示例中，使用了一个 `Book` 类，该类根据图书的出版商显示不同的内容。

`Book` 类定义了属性 `Title` 和 `Publisher`，并重载了 `ToString` 方法（代码文件：`TriggerSamples/Book.cs`）：

```
public class Book
{
    public string Title { get; set; }
    public string Publisher { get; set; }

    public override string ToString() => Title;
}
```

在 XAML 代码中，为 `ListBoxItem` 元素定义了一个样式。该样式包含 `DataTrigger` 元素，这些元素绑定到与项一起使用的类的 `Publisher` 属性。如果 `Publisher` 属性的值是 `Wrox Press`，`Background` 设置为 `Red`。对于出版商 `Dummies` 和 `Wiley`，`Background` 分别设置为 `Yellow` 和 `DarkGray`（代码文件：`TriggerSamples/DataTriggerWindow.xaml`）：

```
<Window x:Class="TriggerSamples.DataTriggerWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    Title="Data Trigger" Height="300" Width="300">
<Window.Resources>
    <Style TargetType="ListBoxItem">
        <Style.Triggers>
            <DataTrigger Binding="{Binding Publisher}" Value="Wrox Press">
        <Setter Property="Background" Value="Red" />
    </DataTrigger>
    <DataTrigger Binding="{Binding Publisher}"
Value="Dummies">
        <Setter Property="Background" Value="Yellow" />
    </DataTrigger>
    <DataTrigger Binding="{Binding Publisher}"
Value="Wiley">
        <Setter Property="Background" Value="DarkGray" />
    </DataTrigger>
</Style.Triggers>
</Style>
</Window.Resources>
<Grid>
    <ListBox x:Name="list1" />
</Grid>
</Window>
```

在代码隐藏文件中，名为 `list1` 的列表被初始化为包含多个 `Book` 对象（代码文件：`TriggerSamples/DataTriggerWindow.xaml.cs`）：

```
public DataTriggerWindow()
{
    InitializeComponent();

    list1.Items.Add(new Book
    {
        Title = "Professional C# 6 and .NET Core 1.0",
        Publisher = "Wrox Press"
    });
    list1.Items.Add(new Book
    {
        Title = "C# 5 All-in-One for Dummies",
        Publisher = "For Dummies"
    });
    list1.Items.Add(new Book
    {
        Title = "HTML and CSS: Design and Build Websites",
        Publisher = "Wiley"
    });
}
```

运行应用程序时，`ListBoxItem` 元素会根据出版商的值进行格式化，如[图 34.11](#)所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1314_0.png)

#### 图 34.11

对于 `DataTrigger`，必须为 `MultiDataTrigger` 设置多个属性（类似于 `Trigger` 和 `MultiTrigger`）。

> 注意：数据触发器会在绑定数据变化时更新用户界面（前提是实现了 `INotifyPropertyChanged` 接口）。本章后面的“实时整形”部分包含一个示例。

#### 菜单和功能区控件

许多数据驱动的应用程序包含菜单、工具栏或功能区控件，使用户能够控制操作。从 WPF 4.5 开始，功能区控件也可用，因此这里会同时介绍菜单和功能区控件。

在本节中，你将创建两个新的 WPF 应用程序：`BooksDemoMenu` 和 `BooksDemoRibbon`，以及贯穿本章使用的库 `BooksDemoLib`——不仅用于菜单和功能区控件，还用于命令和数据绑定。该应用程序显示单本图书、图书列表和图书网格。操作从关联了命令的菜单或功能区控件中启动。

#### 菜单控件

使用 WPF 可以轻松创建菜单，只需使用 `Menu` 和 `MenuItem` 元素，如下面的代码片段所示，其中包含两个主菜单项：`File` 和 `Edit`，以及一组子菜单条目。字符前的 `_` 标记特殊字符，用户无需使用鼠标即可轻松访问菜单项。使用 `Alt` 键可使这些字符可见，并可借助该字符访问菜单。其中一些菜单项分配了命令，下一节将对此进行讨论（代码文件：`BooksDemoMenu/MainWindow.xaml`）：

```
<Window x:Class="Wrox.ProCSharp.WPF.MainWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="clr-namespace:BooksDemo"
    Title="Books Demo App" Height="400" Width="600">
<DockPanel>
    <Menu DockPanel.Dock="Top">
        <MenuItem Header="_File">
            <MenuItem Header="Show _Book" />
            <MenuItem Header="Show Book_s" />
            <Separator />
            <MenuItem Header="E_xit" />
        </MenuItem>
        <MenuItem Header="_Edit">
            <MenuItem Header="Undo" Command="Undo" />
            <Separator />
            <MenuItem Header="Cut" Command="Cut" />
            <MenuItem Header="Copy" Command="Copy" />
            <MenuItem Header="Paste" Command="Paste" />
        </MenuItem>
    </Menu>
</DockPanel>
</Window>
```

运行应用程序后，会得到如图 34.12 所示的菜单。由于命令尚未激活，这些菜单还不能使用。

![](img/3d365b72b289213a91ade7eb366b8f35_1316_0.png)

图 34.12

#### 功能区控件

功能区控件是菜单控件的替代方案。Microsoft Office 2007 是首个附带 Microsoft 功能区控件发布的应用。推出后不久，许多旧版 Office 的用户抱怨说，他们无法在新 UI 中找到想要的操作。在 Office 2007 之前没有用过 Office 的用户对新 UI 的体验更好；他们能够轻松找到旧版用户难以发现的操作。

当然，如今功能区控件在许多应用程序中都非常常见。自 Windows 8 起，Windows 操作系统附带的许多工具中都使用了功能区——例如 Windows 资源管理器、画图和写字板。

WPF 功能区控件位于命名空间

```
System.Windows.Controls.Ribbon
```

并且需要引用程序集

```
System.Windows.Controls.Ribbon.
```

图 34.13 显示了示例应用程序的功能区控件。窗口标题左侧最顶行是快速访问工具栏。第二行最左侧的项是应用程序菜单，其后是两个功能区选项卡：主页和功能区控件。选中的主页选项卡显示两个组：剪贴板和显示。这两个组都包含一些按钮控件。

![](img/3d365b72b289213a91ade7eb366b8f35_1317_0.png)

图 34.13

`Ribbon` 控件在下面的代码片段中定义。`Ribbon` 元素的第一个子元素由 `QuickAccessToolBar` 属性定义。该工具栏包含两个引用了小图像的 `RibbonButton` 控件。这些按钮为用户提供直接访问，以便快速轻松地完成操作（代码文件：`BooksDemoRibbon/MainWindow.xaml`）：

```xml
<Ribbon DockPanel.Dock="Top">
  <Ribbon.QuickAccessToolBar>
    <RibbonQuickAccessToolBar>
      <RibbonButton SmallImageSource="Assets/one.png" />
      <RibbonButton SmallImageSource="Assets/list.png" />
    </RibbonQuickAccessToolBar>
  </Ribbon.QuickAccessToolBar>
  <!-- etc. -->
</Ribbon>
```

要将这些按钮从快速访问工具栏直接放到窗口的边框（chrome）中，需要将基类改为 `RibbonWindow` 类，而不是 `Window` 类（代码文件：`BooksDemoRibbon/MainWindow.xaml.cs`）：

```csharp
public partial class MainWindow : RibbonWindow
{
```

在代码隐藏中更改基类也需要在 XAML 代码中做相应更改，以使用 `RibbonWindow` 元素：

```xml
<RibbonWindow x:Class="Wrox.ProCSharp.WPF.MainWindow"

    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"

             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:Wrox.ProCSharp.WPF"
             Title="Books Demo App" Height="400" Width="600">
```

应用程序菜单通过 `ApplicationMenu` 属性定义。应用程序菜单定义了两个菜单项——第一个用于显示图书，第二个用于关闭应用程序：

```xml
<Ribbon.ApplicationMenu>
  <RibbonApplicationMenu SmallImageSource="Assets/books.png">
<RibbonApplicationMenuItem Header="Show _Book" />
<RibbonSeparator />
<RibbonApplicationMenuItem Header="Exit" Command="Close" />
</RibbonApplicationMenu>
</Ribbon.ApplicationMenu>
```

在应用程序菜单之后，`Ribbon` 控件的内容是通过使用 `RibbonTab` 元素来定义的。选项卡的标题使用 `Header` 属性定义。`RibbonTab` 包含两个 `RibbonGroup` 元素。每个 `RibbonGroup` 元素都包含 `RibbonButton` 元素。通过按钮，可以设置 `Label` 以显示文本，并设置 `SmallImageSource` 或 `LargeImageSource` 属性以显示图像：
