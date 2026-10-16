
# 32 Windows应用程序：用户界面

## 本章内容

- 页面之间的导航
- 创建汉堡按钮
- 使用SplitView
- 使用RelativePanel进行布局
- 针对不同屏幕尺寸的自适应UI
- 使用AutoSuggest控件
- 使用Pen与InkCanvas
- 使用应用栏控件定义命令
- 编译绑定功能

## Wrox.com 本章代码下载

本章的wrox.com代码下载可在 http://www.wrox.com/go/professionalcsharp6 的Download Code选项卡中找到。本章代码包含一个大型示例，展示了本章的各个方面：

- 页面导航
- 应用程序外壳
- 布局
- 控件
- 编译绑定

## 概述

本章涉及的Windows应用程序是使用通用Windows平台（UWP）的应用程序，这些应用可在Windows 10设备上运行。本章介绍用户界面功能，如页面导航、创建页面布局、定义命令以允许用户执行某些操作、使用新的编译数据绑定，以及使用一些特殊控件。

前面的章节涵盖了XAML：第29章介绍了核心信息，第30章定义了应用程序的样式，第31章介绍了常用于基于XAML的应用程序的几种模式。

本章首先介绍与Windows应用用户界面元素相关的一些特定主题：使用UWP。为UWP创建的应用可以运行在Windows 10、Windows Phone以及其他设备系列上，如Xbox、HoloLens和物联网（IoT）。

本章首先介绍在页面之间创建导航，并使用新的系统返回按钮、汉堡按钮和SplitView来适应不同屏幕尺寸的导航控件。它涵盖了不同类型的页面，如Hub和Pivot控件，以实现不同类型的导航，本章还解释了如何创建自定义应用外壳。

您将了解如何使用VariableSizedWrapGrid和带有自适应触发器的RelativePanel创建单页布局。延迟加载可以更快地显示用户界面。

通过编译绑定，您可以看到另一个性能改进，它可以帮助您更早地检测错误。

在“控件”部分，您会看到一些新控件在实际中的应用，例如AutoSuggest控件和InkCanvas，它们支持使用笔、触摸屏和鼠标轻松绘图。

在阅读本章之前，您应熟悉第29、30和31章中讨论的XAML。本章仅介绍特定的UWP应用功能。

## 导航

如果您的应用程序由多个页面组成，您需要能够在这些页面之间导航。导航的核心是Frame类。Frame类使您能够使用Navigate方法导航到特定页面，并可选地传递参数。Frame类会维护一个您已经导航过的页面堆栈，从而可以向后导航、向前导航、限制堆栈中的页面数量等。

导航的一个重要方面是能够向后导航。在Windows 8中，返回导航通常由页面左上角带有返回箭头的按钮处理。Windows Phone始终有一个物理返回按钮。在Windows 10中，这些功能需要结合起来。以下各节将向您展示使用返回导航的新方法。

### 导航到初始页面

让我们开始创建一个包含多个页面的Windows应用，以便在页面之间导航。模板生成的代码包含App类中的OnLaunched方法，其中实例化了一个Frame对象，然后通过调用Navigate方法导航到MainPage（代码文件PageNavigation/App.xaml.cs）：

```
protected override void OnLaunched(LaunchActivatedEventArgs e)
{
    Frame rootFrame = Window.Current.Content as Frame;

    if (rootFrame == null)
{
    rootFrame = new Frame();

    rootFrame.NavigationFailed += OnNavigationFailed;

    if (e.PreviousExecutionState ==
ApplicationExecutionState.Terminated)
    {
        //TODO: Load state from previously suspended application
    }

    Window.Current.Content = rootFrame;
}

if (rootFrame.Content == null)
{
    rootFrame.Navigate(typeof(MainPage), e.Arguments);
}
Window.Current.Activate();
}
```

> 注意：源代码中有一个TODO注释，用于从之前挂起的应用程序加载状态。如何处理挂起将在第33章“高级Windows应用程序”中解释。

Frame类维护一个已访问页面的堆栈。GoBack方法可以在此堆栈中向后导航（如果CanGoBack属性返回true），而GoForward方法使您能够在向后导航后向前移动一页。Frame类还提供了几个用于导航的事件，例如Navigating、Navigated、NavigationFailed和NavigationStopped。

为了实际了解导航，除了MainPage之外，还创建了SecondPage和ThirdPage页面，以便在这些页面之间导航。从MainPage可以导航到SecondPage，再从SecondPage导航到ThirdPage，并传递一些数据。

由于这些页面之间存在公共功能，因此创建了一个基类BasePage，所有这些页面都派生自该类。BasePage类派生自基类Page，并实现了INotifyPropertyChanged接口以进行用户界面更新。

```
public abstract class BasePage : Page, INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;

    private string _navigationMode;

    public string NavigationMode
    {
        get { return _navigationMode; }
        set
        {
            _navigationMode = value;
            OnPropertyChanged();
        }
    }
}
```

```
protected virtual void OnPropertyChanged(
    [CallerMemberName] string propertyName = null)
{
    PropertyChanged?.Invoke(this, new
PropertyChangedEventArgs(propertyName));
}

// etc.
}
```

> 注意：接口INotifyPropertyChanged在第31章“XAML应用程序的模式”中讨论，用于实现更改通知。

### 重写页面类的导航

Page类作为BasePage的基类（以及XAML页面的基类）定义了导航中使用的方法。当页面被导航到时，会调用OnNavigatedTo方法。在此方法中，您可以读取导航的方式（NavigationMode属性）以及导航参数。当您离开页面时，首先调用的是OnNavigatingFrom方法。在这里，可以取消导航。当您离开此页面时，最后会调用OnNavigatedFrom方法。在这里，您应该清理通过OnNavigatedTo方法分配的一些资源（代码文件PageNavigation/App.xaml.cs）：

```
public abstract class BasePage : Page, INotifyPropertyChanged
{
    // etc.
    protected override void OnNavigatedTo(NavigationEventArgs e)
    {
        base.OnNavigatedTo(e);

        NavigationMode = $"Navigation Mode: {e.NavigationMode}";
        // etc.
    }

    protected override void
OnNavigatingFrom(NavigatingCancelEventArgs e)
    {
        base.OnNavigatingFrom(e);
    }

    protected override void OnNavigatedFrom(NavigationEventArgs e)
    {
        base.OnNavigatedFrom(e);
        // etc.
    }
}
```

### 在页面之间导航

让我们实现这三个页面。为了使用BasePage类，需要修改代码隐藏文件，以BasePage作为基类

```csharp
// (code file PageNavigation/MainPage.xaml.cs):
public sealed partial class MainPage : BasePage
{
    // etc.
}
```

基类的更改也需要在使用`BasePage`元素而不是`Page`的XAML文件中体现出来（代码文件`PageNavigation/MainPage.xaml`）：

```xml
<local:BasePage
    x:Class="PageNavigation.MainPage"

    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:PageNavigation"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d">
```

`MainPage`包含一个`TextBlock`元素，该元素绑定到`BasePage`中声明的`NavigationMode`属性，以及一个`Button`控件，其`Click`事件绑定到`OnNavigateToSecondPage`方法（代码文件`PageNavigation/MainPage.xaml`）：

```xml
<StackPanel Orientation="Vertical">
    <TextBlock Style="{StaticResource TitleTextBlockStyle}"
        Margin="8">
        Main Page</TextBlock>
    <TextBlock Text="{x:Bind NavigationMode, Mode=OneWay}"
        Margin="8" />
    <Button Content="Navigate to SecondPage"
        Click="OnNavigateToSecondPage"
        Margin="8" />
</StackPanel>
```

处理程序方法`OnNavigateToSecondPage`使用`Frame.Navigate`导航到`SecondPage`。`Frame`是`Page`类的一个属性，返回`Frame`实例（代码文件`PageNavigation/MainPage.xaml.cs`）：

```csharp
public void OnNavigateToSecondPage()
{
    Frame.Navigate(typeof(SecondPage));
}
```

当您从`SecondPage`导航到`ThirdPage`时，会向目标页面传递一个参数。该参数可以在绑定到`Data`属性的`TextBox`中输入（代码文件`PageNavigation/SecondPage.xaml`）：

```xml
<StackPanel Orientation="Vertical">
    <TextBlock Style="{StaticResource TitleTextBlockStyle}"
        Margin="8">
        Second Page</TextBlock>
    <TextBlock Text="{x:Bind NavigationMode, Mode=OneWay}"
        Margin="8" />
    <TextBox Header="Data" Text="{x:Bind Data, Mode=TwoWay}"
        Margin="8" />
</StackPanel>
```
