

```xml
VisualStudio.Shell.StartPage;component/Images/StartPage/
"
<vs:ImageButton>
</Grid>
<!-- 最近项目列表 -->
<Grid Row="1" HorizontalAlignment="Left" Width="779">
<GridRowDefinitions>
<RowDefinition Height="Auto" />
<RowDefinition Height="Auto" />
<RowDefinition Height="Auto" />
</GridRowDefinitions>
<TextBlock Text="Recent Projects" VerticalAlignment="Top"
Style="{DynamicResource StartPage.HeadingTextStyle}" 
x:Uid="RecentProjects" />
<ScrollView Row="1" HorizontalAlignment="Stretch"
Style="{DynamicResource StartPage.ScrollViewStyle}" 
VerticalScrollBarVisibility="Auto">
<ListBox
DataContext="{Binding RecentProjects}"
ItemsSource="{Binding Path=Items}" 
Background="Transparent"
BorderThickness="0" 
AutomationID="MruList" />
</ScrollView>
<!-- 最近项目计数标签 -->
<WrapPanel>
<TextBlock Foreground="{DynamicResource Brushes.StartPageTextBlock}" />
<TextBlock Row="2" Text="Number of recent projects: " />
<TextBlock Text="{Binding RecentProjects.Items.Count}" />
</WrapPanel>
</Grid>
</Grid>
```

尽管此列表看起来很长，但原始代码中的内容比原始的 `StartPage.xaml` 模板要短。原始文件中的大部分代码与信息标签页有关，这些内容已被移除。此列表使用了与列表 5-3 相同的模式来定义命令按钮，并使用了与列表 5-4 相同的代码来实现项目列表。命令按钮已更改为包含 `View.Tasklist` 和 `File.NewFile` 命令——请查看 `vs:ImageButton` 的 `CommandParameter` 属性。

最近项目计数标签由嵌入 `WrapPanel` 中的两个 `TextBlock` 元素组成。第二个元素的 `Text` 属性简单地绑定到 `RecentProjects.Items.Count` 路径以显示计数器。

编译并运行项目。然后转到“工具 > 选项”（Tools > Options），在“自定义启动页”组合框中选择“[已安装扩展] ModifiedStartPage 项”以显示新的启动页。第 5-31 页显示了这个新页面是如何加载的。

![](img/b5597c749e848b27b0d305153ae16106_217_0.png)

**图 5-31：在 ModifiedStartPage 项目实现的启动页**

## 访问 Visual Studio 上文

上一个示例显示了启动页访问了当前的 Visual Studio 上文。例如，最近项目列表通过以下声明绑定到它的列表框（在列表 5-4 和列表 5-5）：

```xml
<mru:MruListBox
DataContext="{Binding RecentProjects}"
ItemsSource="{Binding Path=Items}"
Background="Transparent"
BorderThickness="0"
AutomationProperties.AutomationId="MruList"/>
```

在这里，`MruListBox` 控件的 `DataContext` 绑定到其父级控件的 `RecentProjects` 数据源属性。

你可能还注意到 `MyControl` 属性通过以下绑定显示了应用程序名称：

```xml
<TextBlock
Text="{Binding Path=DTE.Name}"
FontSize="12"
HorizontalAlignment="Center"/>
```

在这里，父级控件数据上下文的 `DTE.Name` 属性提供了该名称。

启动页是一个 XAML 文件，由 Visual Studio 在启动时或在选项对话框中更改当前启动页时加载并解析。在加载 XAML 文件后，`LayoutRoot` 网格被实例化，其 `DataContext` 属性被设置为 `Microsoft.Internal.VisualStudio.PlatformUI.DataSource` 类的实例，该类可以在 `Microsoft.VisualStudio.Shell.10.0.dll` 程序集中找到。

表 5-5 总结了 `LayoutRoot` 网格数据上下文的属性。

### 表 5-5：Visual Studio 上文属性

| 属性 (PROPERTY) | 描述 (DESCRIPTION) |
| :--- | :--- |
| Customization | 是否允许自定义。 |
| CloseOpen | 启动页是否已关闭。 |
| ShowStartup | 启动时是否显示启动页。 |
| Source | 启动页的标识符。 |
| ExtensionId | 扩展程序的标识。 |
| TeamSupported | 是否支持团队 Foundation。 |
| TeamClient | 访问团队 Foundation。 |
| Links | 启动页中的链接。 |
| Rss | 启动页的数据。 |
| SelectedTabIndex | 索引。 |
| SelectedIndex | 选中的索引。 |
| DTE | DTE 属性。 |

