

```xml
<AdaptiveTrigger MinWindowWidth="0" />
</VisualState.StateTriggers>
<VisualState.Setters>
    <Setter Target="RootSplitView.DisplayMode"
Value="Overlay"/>
</VisualState.Setters>
</VisualState>
</VisualStateGroup>
</VisualStateManager.VisualStateGroups>
```

## XAML 视图

自适应触发器可以帮助支持许多不同的窗口尺寸，同时也支持应用程序在手机和桌面上运行的布局。如果你的应用程序的用户界面差异超过使用 `RelativePanel` 能够解决的范围，最佳选择是使用不同的 XAML 视图。XAML 视图仅包含 XAML 代码，并使用与对应页面相同的代码隐藏。你可以为同一页面为每个设备族创建不同的 XAML 视图。

你可以通过创建文件夹 `DeviceFamily-Mobile` 来为移动设备定义 XAML 视图。设备特定的文件夹始终以 DeviceFamily 开头。其他受支持的设备族示例有 Team、Desktop 和 IoT。你可以使用此设备族名称作为后缀来指定对应设备族的 XAML 视图。你可以使用 XAML View Visual Studio 项目模板创建 XAML 视图。此模板创建 XAML 代码但不创建代码隐藏文件。此视图需要与应被替换的页面的名称相同。

除了为移动 XAML 视图创建不同的文件夹外，你也可以在与页面相同的文件夹中创建视图，但视图文件使用 `DeviceFamily-Mobile` 命名。

## 延迟加载

为了获得更快的 UI，你可以延迟控件的创建直到它们被需要。在小型设备上，一些控件可能根本不需要，但在更大的屏幕和更快的系统上则需要它们。在 XAML 应用程序的早期版本中，添加到 XAML 代码中的元素也会被实例化。在 Windows 10 中情况不再如此。在这里你可以按需延迟加载控件。

你可以使用自适应触发器进行延迟加载，以便在稍后时间仅加载某些控件。一个有用的示例场景是当你有一个用户可以调整大小以变大的较小窗口时。对于较小的窗口，一些控件不应可见，但在窗口变大时应可见。另一个延迟加载可能有用的场景是当布局的某些部分加载可能需要更长时间时。不要让用户等待直到看到完全加载的布局，你可以使用延迟加载。

要使用延迟加载，你需要将 `x:DeferLoadStrategy` 属性添加到控件中，如以下代码片段中 Grid 控件所示。此控件还需要分配一个名称（代码文件 LayoutSamples/Views/DelayLoadingSample.xaml）：

```xml
<Grid x:DeferLoadStrategy="Lazy" x:Name="deferGrid">
  <Grid.ColumnDefinitions>
    <ColumnDefinition />
    <ColumnDefinition />
  </Grid.ColumnDefinitions>
  <Grid.RowDefinitions>
    <RowDefinition />
    <RowDefinition />
  </Grid.RowDefinitions>
  <Rectangle Fill="Red" Grid.Row="0" Grid.Column="0" />
  <Rectangle Fill="Green" Grid.Row="0" Grid.Column="1" />
  <Rectangle Fill="Blue" Grid.Row="1" Grid.Column="0" />
  <Rectangle Fill="Yellow" Grid.Row="1" Grid.Column="1" />
</Grid>
```

要使此延迟控件可见，你所需要做的就是调用 FindName 方法来访问控件的标识符。这不仅使控件可见，还在控件被显示之前加载控件的 XAML 树（代码文件 LayoutSamples/Views/DelayLoadingSample.xaml.cs）：

```csharp
private void OnDeferLoad(object sender, RoutedEventArgs e)
{
  FindName(nameof(deferGrid));
}
```

当你运行应用程序时，你可以使用实时可视化树窗口验证包含 deferGrid 元素的树不可用（见图 32.21），但在调用 FindName 方法查找 deferGrid 元素后，deferGrid 元素将被添加到树中（见图 32.22）。

## 实时可视化树

```text
Search Live Visual Tree (Alt+ö)

+   [RootScrollViewer] (10)
+     [ScrollContentPresenter] (9)
+       [Border] (8)
+         [Frame] (7)
+           [ContentPresenter] (6)
+             [DelayLoadingSample] (5)
+             [Grid] (4)
+             [Button] (3)
+   [FullWindowMediaRoot]
+   [PopupRoot]
```

Figure 32.21

![](img/3d365b72b289213a91ade7eb366b8f35_1224_0.png)

Figure 32.22

## 命令

本章前面你已经看到如何为用户处理导航。你见过用于导航到不同页面的汉堡按钮和普通按钮。对于应用程序，你需要更多允许用户启动某些操作的控件。Windows 8 对将命令栏带入操作时用户从顶部或底部滑动有一些有趣的方面；隐藏的命令允许屏幕更简洁。一些非常重要的命令控件仍然可以直接放置在屏幕上。微软的 OneNote 有一个有趣的控件，只使用一个小圆圈；当用户点击它时，控件会变大以提供更多选项。此设计的问题是它最终不够直观。用户很难发现哪些应用程序允许从顶部或底部滑动，并且通常不知道他们可以这样做。随着 Windows 10，Windows 应用程序可以在小窗口而不是全屏中运行，这甚至带来更多问题。在 Windows 10 中，始终保持打开的命令栏是可以接受的——只需查看微软 OneNote 的新版本，它有一个看起来像 Ribbon 控件的命令控件。

> NOTE Ribbon 控件将在第 34 章讨论。

创建用户可激活的控件列表的一种简单方法是使用 CommandBar 和 AppBar 类。CommandBar 更容易使用但没有 AppBar 灵活。使用 CommandBar，你只能添加特定类型的控件，而 AppBar 允许你使用任何元素。

以下代码示例创建了一个位于页面顶部的 CommandBar。此 CommandBar 包含三个 AppBarButton 控件（代码文件 ControlsSample/Views/InkSample.xaml）：

```xml
<Page.TopAppBar>
    <CommandBar>
        <AppBarButton Icon="Save" Label="Save" Click="{x:Bind OnSave}" />
        <AppBarButton Icon="OpenFile" Label="Open" Click="{x:Bind OnLoad}" />
        <AppBarButton Icon="Clear" Label="Clear" Click="{x:Bind OnClear}" />
    </CommandBar>
</Page.TopAppBar>
```

Page 类包含 TopAppBar 和 BottomAppBar 属性以将应用栏定位在顶部或底部。这些属性在 Windows 8 中是必要的，但现在只是为了方便。你可以在页面中你希望它所在的位置定位应用栏。

AppBarButton 控件被定义为 CommandBar 的子元素。AppBar 按钮的符号可以以多种方式定义。使用 Icon 属性，你可以分配 BitmapIcon、FontIcon、PathIcon 或 SymbolIcon。 （阅读第 29 章，了解如何使用 Path 元素定义矢量图形。）使用 Icon 属性，你可以直接分配预定义符号，这反过来设置 SymbolIcon。预定义图标的示例有 Save、OpenFile 和 Clear。图 32.23 显示了展开模式下具有三个 AppBar 按钮控件的 CommandBar。在折叠模式下——你可以通过点击省略号按钮切换——Label 属性的值不会显示。

![](img/3d365b72b289213a91ade7eb366b8f35_1227_0.png)

Figure 32.24

CommandBar 还允许二级命令。如果需要更多不适合一行的命令——尤其是在移动设备上——你可以使用二级命令。二级命令可以分配给 CommandBar 元素的 SecondaryCommands 属性。

```xml
<CommandBar>
    <CommandBar.SecondaryCommands>
        <AppBarButton Label="One" Icon="OneBar" />
        <AppBarButton Label="Two" Icon="TwoBars" />
        <AppBarButton Label="Three" Icon="ThreeBars" />
        <AppBarButton Label="Four" Icon="FourBars" />
    </CommandBar.SecondaryCommands>
    <!-- etc. -->
```

在 Windows 10 中，二级命令通过点击省略号按钮打开，如图 32.25 所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1227_1.png)

Figure 32.25

## 编译数据绑定

编译数据绑定是使用在第 31 章引入并已在本章中提及的 x:Bind 的 Binding 标记扩展的更快替代方案。现在我们深入了解

