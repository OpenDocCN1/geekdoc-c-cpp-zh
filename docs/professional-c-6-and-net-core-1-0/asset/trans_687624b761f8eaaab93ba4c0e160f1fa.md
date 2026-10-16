

```
new Country { Name="Norway", ImagePath ="Images/Norway.bmp" },
    new Country { Name="USA", ImagePath ="Images/USA.bmp" }
});
}
```

在 `StyledList` 类的构造函数中，代码隐藏文件里创建了只读属性 `Countries`，并通过 `CountryRepository` 的 `GetCountries` 方法填充（代码文件 `Templates[WPF|UWP]/StyledList.xaml.cs`）：

```
public ObservableCollection<Country> Countries { get; } =
    new ObservableCollection<Country>();

public StyledListBox()
{
    this.InitializeComponent();
    this.DataContext = this;
    var countries = new CountryRepository().GetCountries();
    foreach (var country in countries)
    {
        Countries.Add(country);
    }
}
```

DataContext 是下一章将要讨论的数据绑定功能。

在 XAML 代码中，定义了名为 `countryList1` 的 `ListView`。`countryList1` 只使用默认样式。`ItemsSource` 属性设置为 `Binding` 标记扩展，该扩展用于数据绑定。从代码隐藏文件中可以看到，绑定是针对 `Country` 对象数组进行的。图 30.18 展示了 `ListView` 的默认外观。默认情况下，只有 `ToString` 方法返回的国家名称会显示在简单列表中（代码文件 `Templates[WPF|UWP]/StyledList.xaml`）：

![](img/3d365b72b289213a91ade7eb366b8f35_1130_0.png)

图 30.18

```
<Grid>
    <ListView ItemsSource="{Binding Countries}" Margin="10" x:Name="countryList1" />
</Grid>
```

## ListView 项的 DataTemplate

接下来，你将之前创建的 `DataTemplate` 用于 `ListView` 控件。`DataTemplate` 可以直接赋值给 `ItemTemplate` 属性（代码文件 `Templates [WPF|UWP]/StyledList.xaml`）：

```
<ListView ItemsSource="{Binding Countries}" Margin="10" ItemTemplate="{StaticResource CountryDataTemplate}" />
```

有了这个 XAML，项将如图 30.19 所示显示。

![](img/3d365b72b289213a91ade7eb366b8f35_1131_0.png)

图 30.19

当然，也可以定义引用数据模板的样式（代码文件 `Templates [WPF|UWP]/Styles/ListTemplates.xaml`）：

```
<Style x:Key="ListViewStyle1" TargetType="ListView">
    <Setter Property="ItemTemplate"
        Value="{StaticResource CountryDataTemplate}" />
</Style>
```

并从 `ListView` 控件中使用此样式（代码文件 `Templates [WPF|UWP]/StyledList.xaml`）：

```
<ListView ItemsSource="{Binding Countries}" Margin="10"
```

## 项容器样式

数据模板定义了每个项的外观，同时每个项都有一个容器。`ItemContainerStyle` 可以定义每个项容器的外观——例如，当项被选中、按下等时，应使用哪些前景和背景画刷。为了便于查看容器的边界，设置了 `Margin` 和 `Background` 属性（`TemplatesUWP/Styles/ListTemplates.xaml`）：

```xml
<Style x:Key="ListViewItemStyle1" TargetType="ListViewItem">
    <Setter Property="Background" Value="Orange"/>
    <Setter Property="Margin" Value="5"/>
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="ListViewItem">
                <ListViewItemPresenter ContentMargin="{TemplateBinding Padding}"
                    FocusBorderBrush="{ThemeResource SystemControlForegroundAltHighBrush}"
                    HorizontalContentAlignment="{TemplateBinding HorizontalContentAlignment}"
                    PlaceholderBackground="{ThemeResource ListViewItemPlaceholderBackgroundThemeBrush}"
                    SelectedPressedBackground="{ThemeResource SystemControlHighlightListAccentHighBrush}"
                    SelectedForeground="{ThemeResource SystemControlHighlightAltBaseHighBrush}"
                    SelectedBackground="{ThemeResource SystemControlHighlightListAccentLowBrush}"
                    VerticalContentAlignment="{TemplateBinding VerticalContentAlignment}"/>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

对于 WPF，`ListViewItemPresenter` 不可用，但你可以按照以下代码片段使用 `ContentPresenter`（代码文件 `TemplatesWPF/Styles/ListTemplates.xaml`）：

```xml
<Style x:Key="ListViewItemStyle1" TargetType="{x:Type ListViewItem}">
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="{x:Type ListViewItem}">
                <Grid Margin="8" Background="Orange">
                    <ContentPresenter />
                </Grid>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

该样式与 `ListView` 的 `ItemContainerStyle` 属性关联。此样式的结果显示在图 30.20 中。该图清晰地展示了项容器的边界（代码文件 `Templates [WPF | UWP] / StyledList.xaml`）：

![](img/3d365b72b289213a91ade7eb366b8f35_1133_0.png)

图 30.20

```
<ListView ItemsSource="{Binding Countries}" Margin="10"
    ItemContainerStyle="{StaticResource ListViewItemStyle1}"
    Style="{StaticResource ListViewStyle1}" MaxWidth="180" />
```

## 项面板

默认情况下，`ListView` 垂直排列项。这不是项在此视图中的唯一排列方式；你也可以用其他方式排列它们，例如水平排列。在项控件中排列项是项面板的职责。

以下代码片段为 `ItemsPanelTemplate` 定义了一个资源，并将 `ItemsStackPanel` 水平排列而不是垂直排列（代码文件 `TemplatesUWP/Styles/ListTemplates.xaml`）：

```
<ItemsPanelTemplate x:Key="ItemsPanelTemplate1">
    <ItemsStackPanel Orientation="Horizontal" Background="Yellow" />
</ItemsPanelTemplate>
```

WPF 版本略有不同，它使用 `VirtualizingStackPanel` 而不是 `ItemsStackPanel`（代码文件 `TemplatesWPF/Styles/ListTemplates.xaml`）：

```
<ItemsPanelTemplate x:Key="ItemsPanelTemplate1">
    <VirtualizingStackPanel IsItemsHost="True"
Orientation="Horizontal" Background="Yellow"/>
</ItemsPanelTemplate>
```

以下 `ListView` 声明与之前使用相同的 `Style` 和 `ItemContainerStyle`，但添加了 `ItemsPanel` 的资源。图 30.21 展示了项现在水平排列的效果（代码文件 `Templates[WPF|UWP]/StyledList.xaml`）：

```
<ListView ItemsSource="{Binding Countries}" Margin="10"
    ItemContainerStyle="{StaticResource ListViewItemStyle1}"
    Style="{StaticResource ListViewStyle1}"
    ItemsPanel="{StaticResource ItemsPanelTemplate1}" />
```

![](img/3d365b72b289213a91ade7eb366b8f35_1134_0.png)

图 30.21

## ListView 控件模板

该控件仍然缺少滚动功能，以防项无法在屏幕上显示完整。可以通过为 `ListView` 控件定义模板来更改此行为。

`ListViewStyle2` 样式根据水平项对齐的要求定义了水平和垂直滚动条行为。此样式还包含对之前定义的数据模板和容器项模板的资源引用。通过设置 `Template` 属性，你现在还可以更改整个 `ListView` 控件的 UI（代码文件 `TemplatesUWP/Styles/ListTemplates.xaml`）：

```
<Style x:Key="ListViewStyle2" TargetType="ListView">
    <Setter Property="ScrollViewer.HorizontalScrollBarVisibility" Value="Auto"/>
    <Setter Property="ScrollViewer.VerticalScrollBarVisibility" Value="Disabled"/>
    <Setter Property="ScrollViewer.HorizontalScrollMode" Value="Auto"/>
    <Setter Property="ScrollViewer.IsHorizontalRailEnabled" Value="False"/>
    <Setter Property="ScrollViewer.VerticalScrollMode" Value="Disabled"/>
    <Setter Property="ScrollViewer.IsVerticalRailEnabled" Value="False"/>
    <Setter Property="ScrollViewer.ZoomMode" Value="Disabled"/>
    <Setter Property="ScrollViewer.IsDeferredScrollingEnabled" Value="False"/>
    <Setter Property="ScrollViewer.BringIntoViewOnFocusChange" Value="True"/>
    <Setter Property="ItemTemplate"
```

