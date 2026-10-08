
出现（例如，Key.snk）以及“用密码保护我的密钥文件”复选框。点击确定，密钥文件将立即被添加到项目中。

向导的用户界面是一个简单的列表框，如图 4-19 所示。

向导的用户界面是一个 WPF 表单，使用控件和数据绑定来保持 UI 逻辑的简单。向项目添加了一个名为 `CommentSelector.xaml` 的 WPF 控件项。列表 4-7 显示了定义它的 XAML 文件。

![](img/b5597c749e848b27b0d305153ae16106_143_0.png)

图 4-19：简单注释向导的 UI

# 列表 4-7：CommentSelector.xaml

可在 Wrox.com 下载

```
<Window x:Class="SimpleCommentWizard.CommentSelector"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xml"
xmlns:mc="http://schemas.microsoft.com/expression/2006/markup/2006"
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:src="clr-namespace:SimpleCommentWizard"
mc:Ignorable="d"
d:DesignHeight="300" d:DesignWidth="300" ResizeMode="NoResize"
Title="Comment Wizard"
Width="300" Height="220" WindowStartLocation="Center">
<Resources>
<src:CommentDescriptor x:Key="CommentTypes">
  <src:CommentDescriptor
  ShortName="No restriction"
  Description="你可以无限制地使用此程序。"/>
  <src:CommentDescriptor
  ShortName="AS"
  Description="按原样提供。"/>
  <src:CommentDescriptor
  ShortName="No use"
  Description="该程序无法在商业产品中使用。"/>
</src:CommentDescriptorCollection>
</Resources>
<DockPanel>
<DockPanel DockPanel.Dock="Bottom" Height="36" Margin="4">
<Button Name="OK" IsDefault="true" DockPanel.Dock="Right"
Width="80" Margin="4" Click="OK_Click">OK</Button>
<Button Name="CancelButton" HorizontalAlignment="Right"
DockPanel.Dock="Right" Width="80" Margin="4"
Click="Cancel_Click">Cancel</Button>
</DockPanel>
<StackPanel Margin="4">
<TextBlock x:Name="4">选择注释：</TextBlock>
<ListBox x:Name="CommentListBox" Margin="4" SelectedIndex="0"
ItemsSource="{StaticResource CommentTypes}">
</StackPanel>
</Window>
```
www.ebook.info

```
<DisplayMemberPath="ShortName" />
<Border BorderBrush="DarkGray" Margin="4" BorderThickness="2">
<TextBlock HorizontalAlignment="Stretch" TextWrapping="Wrap"
VerticalAlignment="Stretch" Padding="8,8,8,8"
Text="{Binding ElementName=CommentListBox, Path=SelectedItem.Description}"
Background="LightGoldenrod" />
</TextBlock>
</Border>
</StackPanel>
</DockPanel>
```
文件 [CommentSelector.xml] 可在 Wrox.com 下载

尽管你将 WPF 控件更改为了 WPF 窗口（如列表 4-7 所示），XAML 定义的后台代码非常简单。它对 OK 和 Cancel 按钮做出响应。

![](img/b5597c749e848b27b0d305153ae16106_144_0.png)

# 列表 4-8：CommentSelector.xml

```csharp
using System.Windows;

namespace SimpleCommentWizard
{
    public partial class CommentSelector : Window
    {
        public string SelectedComment { get; set; }
        public CommentSelector()
        {
            InitializeComponent();
        }

        private void OkButton_Click(object sender, RoutedEventArgs args)
        {
            var comment = CommentListBox.SelectedItem;
            SelectedComment = comment == null ? null : comment.Description;
            Close();
        }

        private void CancelButton_Click(object sender, RoutedEventArgs args)
        {
            SelectedComment = null;
            Close();
        }
    }
}
```
文件 [CommentSelector.xml.cs] 可在 Wrox.com 下载

`SelectedComment` 属性持有要插入源码的注释值。`CancelButton` 将设置为 `null`，`OkButton` 将其赋值为列表中注释的值。

`CommentListBox` 控件负责列出用户可以选择的注释。它绑定了列表 4-9 中定义的 `CommentDescriptor` 集合。

# 列表 4-9：CommentDescriptor.cs

```csharp
using System.Collections.Generic;

namespace SimpleCommentWizard
{
    class CommentDescriptor
    {
        public string ShortName { get; set; }
        public string Description { get; set; }
    }

    class CommentDescriptorCollection : List<CommentDescriptor>
    {
    }
```

> 文件 [CommentDescriptor.cs] 可在 Wrox 下载

向项目中添加名为 `CommentDescriptor.cs` 的新类，并将列表的内容复制到文件中。`CommentSelector.xml` 文件定义了一个键为 `CommentTypes` 的资源。

## 实现 IWizard

表 4-7 显示了实现 `IWizard` 接口的几个方法。

| 方法 | 描述 |
| --- | --- |
| BeforeOpenFile | 代码生成后运行向导逻辑，此时项将在其相应的编辑器中打开。该方法接受 `EnvDTE.WidgetItem` 类型的输入参数，描述要打开的项目。实现此方法时，你可以获取要打开的项目的信息，甚至更改项目的属性。 |
| ProjectFinishedGenerating | 项目生成完成后运行向导逻辑。只有当向导属于项目模板时，IDE 才会调用此方法。方法具有 `EnvDTE.Project` 类型的输入参数，描述项目。你可以使用此方法获取项目信息或更改项目结构。该方法是根据从用户处收集的信息向项目添加新文件或更改现有文件的占位符。 |
| ProjectItemFinishedGenerating | 项目项生成完成后运行向导逻辑。只有当向导属于项模板时，IDE 才会调用此方法。方法具有 `EnvDTE.ProjectItem` 类型的输入参数，描述生成的项。你可以使用此方法获取该项的信息或更改其属性。 |
| RunFinished | 向导完成所有任务后运行向导逻辑。你可以使用此方法清理向导使用的资源。 |
| RunStarted | 在模板运行开始时运行自定义向导逻辑。这是显示向导用户界面的方法。UI 可以从用户那里收集信息并据此构建模板。该方法有四个参数：`automationObject` —— 自动化对象的引用，允许访问代表 IDE 对象和服务的 `EnvDTE` 实例；`replacementsDictionary` —— 关联占位符及其替换值的字典。 |
| ShouldAddProjectItem | 表示项目项是否应添加到项目中。方法的参数是文件的完整路径。 |

表 4-7 显示的方法顺序并不反映它们触发的顺序和模式。以下是这些方法调用的真实顺序：

1. 在任何其他活动发生之前，对于任何类型的向导，都会调用 `RunStarted` 方法来初始化你的向导逻辑并通过 UI 从用户收集信息。
2. 模板系统使用替换字典（`RunStarted` 方法可以覆盖默认），并创建要添加到项目的文件列表。对于每个文件，都会调用 `ShouldAddProjectItem` 并传入文件的完整路径。从此方法返回 `true` 告诉模板系统向项目添加文件并在原始模板文件中添加任何替换。
3. 当所有文件添加完成后，将调用 `ProjectFinishedGenerating` 或 `ProjectItemFinishedGenerating` 方法之一，取决于它是项目还是项。在两种情况下，代表项目或项的自动化对象都会传递给相应的方法。
4. 对于每个在模板文件中 `OpenInEditor` 被设置为 `true` 的文件，都会调用 `BeforeOpenFile` 并传递代表该文件的自动化对象。
5. 在最后，调用 `RunFinished` 方法。

根据表 4-7 和上述描述的步骤，`IWizard` 接口的实现实际上没有那么复杂。列表 4-10 显示了简单注释向导如何完成这项工作。

