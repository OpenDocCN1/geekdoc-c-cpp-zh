

这里的关键行是绑定表达式 {Binding Main, Source={StaticResource Locator}}。这一行声明了我希望整个视图的数据上下文被设置为 Locator 对象上的 Main 属性，而 Locator 是一个全局资源。MVVM Light 项目模板在我们的 App.xaml 文件中放置了一些代码，声明了 ViewModelLocator 类的一个实例作为全局资源：

```
<Application.Resources>
    <vm:ViewModelLocator x:Key="Locator"
        d:IsDataSource="True" />
</Application.Resources>
```

现在我们有了视图模型定位器，并且我们的视图的数据上下文已被设置为视图模型的一个实例（记住，即使它是一个实例属性，它仍然指向一个静态单例），我们可以将一些 UI 绑定到视图模型，如下所示：

```
<TextBlock x:Name="ApplicationTitle"
    Text="{Binding ApplicationTitle}"
    Style="{StaticResource PhoneTextNormalStyle}" />
<TextBlock x:Name="PageTitle"
    Text="{Binding PageName}"
    Margin="-3,-8,0,0"
    Style="{StaticResource PhoneTextTitle1Style}" />
```

我们采用 MVVM 的第一阶段已经完成：使用视图模型。此时许多开发人员和许多架构师会坐下来思考：这次旅行真的有必要吗？

答案是否定的。也是否定的。正如我之前提到的，你可以以意大利面条式的风格搭建所有这些东西，也可以在代码后置中完成所有操作。到目前为止，我们所做的只是为我们的应用程序提供使用视图模型的方式。到目前为止你还没有看到任何真正的益处，因为你以前见过数据绑定，而且对你来说不应该有什么新意。接下来的是 MVVM Light 工具包的功能以及采用 MVVM 的好处，这些好处可能会（我不是开玩笑）永远改变你编写应用程序的方式。

## 是的，但它会混合吗？

熟悉为 iPhone 和 iPad 构建应用程序的开发人员对这个问题非常熟悉：设计表面几乎从未反映出准确的实时运行应用程序的表示。这取决于个人开发人员，但通常 Interface Builder 的设计表面体验与运行时体验完全不同（尤其是在处理具有自定义渲染的自定义视图时），开发人员完全跳过 IB 并在代码中完成所有操作。

对于 Silverlight、WPF 和 Windows Phone 7 应用程序来说，在某种程度上也是如此。很容易构建一个对设计工具极不友好的应用程序，以至于开发人员忽略了设计工具的存在，他们以“记事本方式”手工在 Visual Studio 中输入 XAML 来构建所有 UI。

设计工具排斥的解药存在，其名称是 MVVM。能够使用设计工具构建 UI 的最大问题是它们与底层数据模型缺乏合作和集成。通常，设计师并不关心（也不访问）由来自 Web 服务代理的 C# 类等生成的数据模型，因此，如果你的 UI 紧密耦合到服务代理类，那么在 Blend 等工具中使用你的 UI 就会变得非常困难。

在列表 16.1 中，你可能已经注意到 MainViewModel 类构造函数中的一行代码看起来像这样：

```
if (IsInDesignMode)
```

这个属性（由 MVVM Light 方便地为我们提供）使我们视图模型构造函数的能够创建一些虚拟数据。Blend 遵循数据绑定的链条并在设计时执行我们视图模型中的构造函数。通过与 MVVM 良好配合，我们的视图模型可以为诸如内置 Visual Studio 设计器和 Blend 等设计工具提供示例数据，我们（或更好的是专业设计师）可以使用这些数据来构建令人难以置信的用户界面。我将在本章后面介绍另一种技术，使用服务提供者，这甚至可以从视图模型的构造函数中隐藏 if 语句，使我们的代码更加干净——谁不喜欢干净的代码呢？图 16.4 显示了我们的主页面在 Blend 中的屏幕截图。请注意，程序生成的數據正在设计表面上显示。

![](img/04a00d46bb1059867d95707babd62ee7_231_0.png)

图 16.4 一个绑定到视图模型的视图在 Blend 中呈现。

## 第 16 章 分离你的关注点

现在我们有了视图、视图模型，甚至视图和视图模型之间的数据绑定，我们想要添加一些交互性。在某个时刻，用户将不得不与我们的应用程序交互。当他们这样做时，我们希望对该交互做出响应并执行一些代码。

在非 MVVM 应用程序中，我们可能会将响应用户交互的所有代码放在视图页面的代码后置中（例如，MainPage.xaml.cs）。虽然这本身并没有什么问题，但这种做法会导致代码难以测试（你将在下一章看到），难以维护，并且通常不够灵活，也不够干净。确实，有时需要代码后置代码，但正如我提到的，我喜欢在最后可能的时刻之前以声明方式完成所有操作。

我想向你展示的交互性是能够从列表中删除一本书的能力。为此，我们将使用 Silverlight/WP7 Toolkit 中提供的控件，你可以在 Codeplex 上找到它，网址为 http://silverlight.codeplex.com。该控件是 ContextMenu 控件。

```
<DataTemplate x:Key="bookItemTemplate">
<StackPanel Width="480">
<toolkit:ContextMenuService.ContextMenu>
<toolkit:ContextMenu>
<toolkit:MenuItem Header="delete book" Command="{Binding RemoveBookCommand}" />
</toolkit:ContextMenu>
</toolkit:ContextMenuService.ContextMenu>
<TextBlock Text="{Binding Title}" Style="{StaticResource PhoneTextLargeStyle}"/>
<TextBlock Text="{Binding Description}" Style="{StaticResource PhoneTextNormalStyle}"/>
</StackPanel>
</DataTemplate>
```

每本书都将由一个包含几项的堆栈面板表示，包括标题和描述的文本块。这很直接。这里的新控件是上下文菜单。菜单内有一个菜单项。乐趣从这里开始。

与其看到你在本书中到目前为止看到的典型的“单击”事件处理程序，现在有一个命令。更好的是，这个命令是视图模型上的一个属性。命令本质上只是包含对可执行代码的引用的对象的实例。它们提供了一种将用户界面元素绑定到代码的方法。

在不需要将该代码紧密耦合到代码后置的情况下执行。换句话说，随着命令成为视图模型的一部分，该代码现在是共享的并存储在视图模型本身上。这使得代码更容易找到，更容易维护，提供了一个单一的执行点（而不是你在代码后置实现中通常看到的多个潜在入口点），甚至可以被重用视图模型的不同视图重用。

让我们看看我们在视图模型上添加以支持删除书籍的命令属性。如果你的大脑已经校准到 MVVM 的思维方式，你可能已经在问自己：这个命令是在 Main 视图模型上还是在 Book 视图模型上？答案是在 Book 视图模型上。这是因为此数据模板绑定到一本书的列表，而这些书中的每一个都是 Book 视图模型的一个实例。

### Listing 16.2 Book.cs

```
using System;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Ink;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using GalaSoft.MvvmLight;
using GalaSoft.MvvmLight.Command;
using GalaSoft.MvvmLight.Messaging;
using Mnemuse.Messages;

namespace Mnemuse.ViewModel
{
public class Book : ViewModelBase
{
    private string title;
    private string description;

    public Book()
        : base()
    {
        InitializeCommands();
    }

    public RelayCommand RemoveBookCommand { get; private set; }
```
