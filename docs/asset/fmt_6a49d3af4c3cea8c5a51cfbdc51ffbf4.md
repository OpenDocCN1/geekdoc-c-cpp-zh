
<navigation:Frame x:Name="ContentFrame" Style="{StaticResource ContentFrameStyle}" Source="/Home" Navigated="ContentFrame_Navigated" NavigationFailed="ContentFrame_NavigationFailed">
    <navigation:Frame.UriMapper>
        <uriMapper:UriMapper>
            <uriMapper:UriMapping Uri="" MappedUri="/Views/Home.xaml"/>
            <uriMapper:UriMapping Uri="/{pageName}" MappedUri="/Views/{pageName}.xaml"/>
        </uriMapper:UriMapper>
    </navigation:Frame.UriMapper>
</navigation:Frame>

正如您所见，定义了两个映射：一个用于未映射 URI 时，另一个用于有人指定类似 `default.aspx#/About` 的页面时，在这种情况下它将加载 `Views` 文件夹中的 `About.xaml` 页面。本章后面您将了解如何添加页面以及它们的代码实际是什么样的。

## Silverlight Class Library

`Silverlight` 类库模板提供了一种将各种项目合并到其自己的程序集中的方法。这与向 Windows 窗体应用程序项目添加类库完全相同，但 Visual Studio 知道要定位 `Silverlight` 应用程序。这很重要，因为 `Silverlight` 运行的是 `.NET Framework` 的子集。

## SILVERLIGHT SOLUTION

虽然我们已经描述了您可以在 `Silverlight` 中创建的各种类型的解决方案，但 `Silverlight` 应用程序解决方案和 `Silverlight` 导航应用程序解决方案之间有许多共同点。本节涵盖它们的共同点，包括 `Silverlight` 应用程序中的常见文件。两种解决方案类型都具有相似的结构，包含 Web 应用程序和 `Silverlight` 应用程序。

### Web Application

创建的 Web 应用程序只是一个 ASP.NET 应用程序，其中包含一个页面来托管您的 `Silverlight` 控件。它还包含一个 `Silverlight.js` 文件，其中包含 JavaScript，可帮助用户在未安装 `Silverlight` 时提供帮助。它还创建了一个 `<project name>TestPage.aspx` 文件和一个 `<project name>TestPage.html` 文件，两者都用于显示 `Silverlight` 应用程序，但为您提供了两种不同的方式。唯一的区别是一个是 ASP.NET 页面，另一个是 HTML 页面。

### The ClientBin Folder and .xap File

Web 项目中还包含一个 `ClientBin` 文件夹。当您编译 `Silverlight` 应用程序时，它实际上被放置在此处。当 `Silverlight` 应用程序被编译时，它会创建一个 `.xap` 文件——一个包含您的 `Silverlight` 应用程序的压缩文件。您可以将 `.xap` 扩展名更改为 `.zip` 以在 Windows 资源管理器中查看其内容。

### Application Library Caching

现在您已经了解了 Visual Studio 存储 `Silverlight` 应用程序编译版本的位置，让我们来看一种优化其在该文件夹中存储内容的方法。随着构建包含对第三方控件和其他程序集的引用的更大应用程序，您可能会发现 `.xap` 文件的大小变得非常大。如果您知道其中几个程序集或库不会更改，您可能希望只缓存各个程序集但更新其他程序集。您可以使用应用程序库缓存来实现这一点。

要启用应用程序库缓存，只需右键单击 `Silverlight` 项目并选择属性。这将打开如图 19-4 所示的 `Silverlight` 构建选项。

![](img/d99870e80390742f93963da7be0b2e61_691_0.png)

**FIGURE 19-4**

只需勾选“通过使用应用程序库缓存来减小 XAP 大小”选项。现在当你编译 `Navigation` 示例时，它将在你的 `ClientBin` 文件夹中创建三个文件：应用程序的 `.xap` 文件，以及两个包含额外程序集的 `zip` 文件，以便它们可以在客户端缓存。

> 如果你正在开发一个将使用“启用在浏览器外运行应用程序”选项的应用程序，你将无法使用应用程序库缓存。

### Silverlight 应用程序

`Silverlight` 项目包含构成 `Silverlight` 应用程序的所有客户端逻辑。本节描述了你应该熟悉的几个文件以及它们存在的原因。

#### App.xaml

与 Windows Forms 应用程序类似，你有一个应用程序的起点，它包含在 `App.xaml` 文件中。该文件还包含未处理异常的逻辑。以下是 `App.xaml` 代码：

```
Partial Public Class App
    Inherits Application
    Public Sub New()
        InitializeComponent()
    End Sub
    Private Sub Application_Startup(ByVal o As Object, ByVal e As StartupEventArgs) Handles Me.Startup
        Me.RootVisual = New MainPage()
    End Sub
    Private Sub Application_UnhandledException(ByVal sender As Object,
        ByVal e As ApplicationUnhandledExceptionEventArgs) Handles Me.UnhandledException
        ' If the app is running outside of the debugger then report the exception using
        ' the browser's exception mechanism. On IE this will display a yellow alert
        ' icon in the status bar and Firefox will display a script error.
        If Not System.Diagnostics.Debugger.IsAttached Then
            ' NOTE: This will allow the application to continue running after an exception has been thrown
            ' but not handled.
            ' For production applications this error handling should be replaced with something that will
            ' report the error to the website and stop the application.
            e.Handled = True
            Dim errorWindow As ChildWindow = New ErrorWindow(e.ExceptionObject)
            errorWindow.Show()
        End If
    End Sub
End Class
```

来自 `App.xaml.vb` 的代码片段

正如你所见，`Application_Startup` 事件在你的 `Silverlight` 应用程序加载时首先被调用。`StartupEventArgs` 属性如果需要可以从 ASP.NET 或 HTML 页面传递参数。然后，它使用 `me.RootVisual` 属性来告诉 `Silverlight` 运行时显示哪个控件。

使用 `Application_UnhandledException` 函数，你可以为应用程序添加全局错误处理。这是放置未处理异常日志记录逻辑的最佳位置。

#### MainPage.xaml

现在你已经了解了应用程序如何启动，本节将介绍它将用于显示的内容。默认情况下，它将是一个 `UserControl`，并设置为 `app.xaml` 中的 `RootVisual`。用户控件由两个文件组成：包含布局信息的 `.xaml` 文件和包含与 UI 关联的类的 `.vb` 文件。以下是 `Navigation` 应用程序中的示例 `MainPage.xaml`：

```
<UserControl
    x:Class="SilverlightApplication1.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:navigation="clr-namespace:System.Windows.Controls;assembly=System.Windows.Controls.Navigation"
    xmlns:uriMapper="clr-namespace:System.Windows.Navigation;assembly=System.Windows.Navigation"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d" d:DesignWidth="640" d:DesignHeight="480">
    <Grid x:Name="LayoutRoot" Style="{StaticResource LayoutRootGridStyle}">
        <Border x:Name="ContentBorder" Style="{StaticResource ContentBorderStyle}">
            <navigation:Frame x:Name="ContentFrame"
                Style="{StaticResource ContentFrameStyle}"
                Source="/Home"
                Navigated="ContentFrame_Navigated" NavigationFailed="ContentFrame_NavigationFailed">
                <navigation:Frame.UriMapper>
                    <uriMapper:UriMapper>
                        <uriMapper:UriMapping Uri="" MappedUri="/Views/Home.xaml"/>
                        <uriMapper:UriMapping Uri="/(pageName)"
                            MappedUri="/Views/{pageName}.xaml"/>
                    </uriMapper:UriMapper>
                </navigation:Frame.UriMapper>
            </navigation:Frame>
        </Border>
        <Grid x:Name="NavigationGrid" Style="{StaticResource NavigationGridStyle}">
            <Border x:Name="BrandingBorder" Style="{StaticResource BrandingBorderStyle}">
                <StackPanel x:Name="BrandingStackPanel"
                    Style="{StaticResource BrandingStackPanelStyle}">
                    <ContentControl Style="{StaticResource LogoIcon}"/>
                    <TextBlock x:Name="ApplicationNameTextBlock"
                        Style="{StaticResource ApplicationNameStyle}"
                        Text="Application Name"/>
                </StackPanel>
            </Border>
            <Border x:Name="LinksBorder" Style="{StaticResource LinksBorderStyle}">
                <StackPanel x:Name="LinksStackPanel"
                    Style="{StaticResource LinksStackPanelStyle}">
                    <HyperlinkButton x:Name="Link1" Style="{StaticResource LinkStyle}"
                        NavigateUri="/Home"
                        TargetName="ContentFrame" Content="home"/>
                    <Rectangle x:Name="Divider1" Style="{StaticResource DividerStyle}"/>
                    <HyperlinkButton x:Name="Link2" Style="{StaticResource LinkStyle}"
                        NavigateUri="/About"
                        TargetName="ContentFrame" Content="about"/>
                </StackPanel>
            </Border>
        </Grid>
    </Grid>
</UserControl>
```

来自 `MainPage.xaml` 的代码片段

代码隐藏文件如下：

```
Imports System.Windows.Navigation
Partial Public Class MainPage
    Inherits UserControl
    Public Sub New()
        InitializeComponent()
    End Sub
    Private Sub ContentFrame_Navigated(ByVal sender As Object,
        ByVal e As NavigationEventArgs) Handles ContentFrame.Navigated
        For Each child As UIElement In LinksStackPanel.Children
            Dim hb As HyperlinkButton = TryCast(child, HyperlinkButton)
            If hb IsNot Nothing AndAlso hb.NavigateUri IsNot Nothing Then
                If hb.NavigateUri = e.Uri Then
                    VisualStateManager.GoToState(hb, "ActiveLink", True)
                Else
                    VisualStateManager.GoToState(hb, "InactiveLink", True)
                End If
            End If
        Next
    End Sub
    Private Sub ContentFrame_NavigationFailed(ByVal sender As Object,
        ByVal e As NavigationFailedEventArgs) Handles ContentFrame.NavigationFailed
        e.Handled = True
        Dim errorWindow As ChildWindow = New ErrorWindow(e.Uri)
```
