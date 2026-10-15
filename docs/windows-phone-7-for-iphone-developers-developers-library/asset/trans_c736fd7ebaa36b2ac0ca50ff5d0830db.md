

阅读它，所以你需要遵循 MVVM Light 网站上的安装说明。你可以从 http://www.galasoft.ch/mvvm/getstarted 下载该库并找到文档和安装说明。在此网址你会找到指向安装说明、视频、文档以及下载库的链接。

在继续本章的其余部分之前，请确保你能够创建一个新的 MVVM Light (WP7) 应用程序，并且它能够编译并运行。当我坐在这里撰写本书时，MVVM Light 并没有自动安装实用程序。你需要解压模板和二进制文件并将它们放在适当的目录中。

为了展示 MVVM Light 的强大功能，我将带你逐步构建一个示例应用程序。这与之前章节中的示例有点不同，因为 MVVM Light 是一个提供支持架构原则的代码库。为了让它发挥作用，我们需要构建一个完整的应用程序。展示微小的孤立片段而不展示它们如何真正改善应用程序质量是没有意义的。

这个示例应用程序名为 Mnemuse，是为小说作家准备的工具。该工具允许作家从其 Windows Phone 7 设备存储和浏览角色、地点、场景、灵感、情节线、章节组织等。这让他们确信自己永远不会丢失重要想法，也永远不会忘记某个特定角色的头发颜色。注意，在本书撰写时，该应用纯粹是演示用途，并未在任何应用市场上架。

我们可以用非 MVVM 的方式构建这个应用程序。我可以创建一堆 XAML 页面并用直接的数据操作代码填满代码后置。我可以将孤立存储（或 Web 服务）I/O 放在直接由 UI 控件激活的位置。我甚至可以让一个页面实例化其他页面，并让主页面手动实例化并向详情页面馈送数据。最终用户可能永远不会知道我偷工减料了，也不会知道我的应用程序耦合紧密或无法测试。说实话，我可以这样做，并且就用户而言应用程序可能运行得相当不错，我甚至可能从该应用赚很多钱。

但我早上会尊重自己吗？不会。

因此我们将以 MVVM 的方式来做。

首先，我将创建一个新的 MVVM Light (WP7) 项目。当你这样做时，你会得到一个 MainPage.xaml，就像任何其他 WP7 应用程序一样。但你也会得到一个 ViewModel 文件夹，在该文件夹中有一个名为 MainViewModel 的类。通常视图（在我看来可以是页面或用户控件）与视图模型之间存在 1:1 的对应关系。视图模型是我们将要查看的该应用程序的第一个方面。

## Building a View Model

为视图模型提供代码支持是 MVVM Light 库的主要任务之一。随着开发人员在学习过程中不断进步，他们厌倦了构建产生意大利面条代码的应用程序，并希望获得更简洁、更优雅的东西。开发人员通常会自然地朝 MVVM 方向漂移。

MVVM 采用过程中的一个常见障碍是弄清楚如何管理视图模型的生命周期。有时开发人员会创建一个静态类来存储对所有视图模型的引用，以便在需要时这些模型会存在。接下来发生的事情通常是开发人员决定 MVVM 并不是一个好主意的地方：他们尝试在 XAML 视图与其静态视图模型之间建立绑定，结果变得很丑陋。让它工作所产生的行为往往比开发人员最初试图避免的意大利面条代码还要多。

引入 ViewModelLocator。这是由 MVVM Light 项目模板为我们提供的类。对于应用程序中的每个视图模型，该类维护一个静态属性，该属性保存该视图模型单例实例的引用。此外，还有非静态属性专门设计用于允许 XAML 绑定。这解决了试图保持视图代码“纯净”时最痛苦的方面之一，即有一个中央实用程序类（如果你喜欢模式标签，可以将其视为工厂）负责视图模型的实例化、绑定公开和生命周期管理。

在我们的示例应用程序中，主页面显示书籍列表，因为能够只在一次思考一本书的虚构作者实在是罕见。所以我们不仅需要我们的主视图模型来维护书籍列表，而且我们希望这个视图模型能够使用 ViewModelLocator 类进行绑定和定位。

要在 ViewModelLocator 类中设置新的视图模型，我首先在实例构造函数中添加一个类似 CreateMain() 的方法调用。你将为每个视图模型在此处放置一个这样的调用。

首先你会看到 MainStatic 属性，它提供了视图模型的单例实例：

```
public static MainViewModel MainStatic
{
    get
    {
        if (_main == null)
        {
            CreateMain();
        }
        return _main;
    }
}
```

这里 _main 变量是一个私有静态成员。接下来我们有引用静态成员的非静态成员，用于支持数据绑定。

```
[System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Performance", "CA1822:MarkMembersAsStatic", Justification = "This non-static member is needed for data binding purposes.")]
public MainViewModel Main
```

```
{
    get
    {
        return MainStatic;
    }
}
```

接下来，按惯例我们有一个名为 ClearMain() 的方法来清理我们的主视图模型。使用此方法来释放视图模型可能正在使用的任何资源。在我的例子中，我在 _main 上调用 Cleanup() 方法，这是所有视图模型都具有的方法，然后将 _main 设置为 null。CreateMain() 方法只是实例化主视图模型的新实例。请记住，你绝不能在定位器类中直接操作视图模型。定位器类纯粹是生命周期管理器和数据绑定促进者。所有真正的初始化代码都在视图模型本身内进行。这让我来到了清单 16.1，我的书籍页面的 MainViewModel 类。

### Listing 16.1 MainViewModel.cs

```
using GalaSoft.MvvmLight;
using System.Collections.ObjectModel;
using GalaSoft.MvvmLight.Command;
using System.Windows;
using GalaSoft.MvvmLight.Messaging;
using Mnemuse.Messages;
using System.Threading;
using GalaSoft.MvvmLight.Threading;
using Microsoft.Phone.Controls;
using System;

namespace Mnemuse.ViewModel
{
    public class MainViewModel : ViewModelBase
    {
        private ObservableCollection<Book> books;
        private Book selectedBook;

        #region Singular Properties
        public string ApplicationTitle
        {
            get
            {
                return "Mnemuse";
            }
        }

        public string PageName
```

```
{
    get
    {
        return "Books";
    }
}

public string Welcome
{
    get
    {
        return "Welcome to MVVM Light";
    }
}

#endregion

public ObservableCollection<Book> Books
{
    get
    {
        return books;
    }
    set
    {
        books = value;
        RaisePropertyChanged("Books");
    }
}

/// <summary>
/// Initializes a new instance of the MainViewModel class.
/// </summary>
public MainViewModel()
{
    Books = new ObservableCollection<Book>();

    if (IsInDesignMode)
    {
        // Code runs in Blend -> create design time data.
        for (int x = 1; x < 6; x++)
        {
            Book b = new Book
            { Title = "Book " + x.ToString(),
              Description = "This is book " + x.ToString() };
            Books.Add(b);
        }
    }
```

```
}
}
else
{
    // Code runs "for real"
}
}
/////public override void Cleanup()
/////{ 
/////    // Clean up if needed
/////
/////    base.Cleanup();
/////}
}
}
```

现在我们有了视图模型，我们需要将视图绑定到它。过去（你知道，大约在第 8 章左右的美好时光），我曾在代码后置中以编程方式设置视图的 DataContext。虽然这种做法肯定能完成工作，而且很多人喜欢这样做，但我更喜欢以声明方式完成所有操作，并仅在最后手段时使用代码。因此，请看一下我的 MainPage.xaml 标记的顶部：

```
<phone:PhoneApplicationPage x:Class="Mnemuse.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:phone="clr-namespace:Microsoft.Phone.Controls;assembly=Microsoft.Phone"
    xmlns:shell="clr-namespace:Microsoft.Phone.Shell;assembly=Microsoft.Phone"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    FontFamily="{StaticResource PhoneFontFamilyNormal}"
    FontSize="{StaticResource PhoneFontSizeNormal}"
    Foreground="{StaticResource PhoneForegroundBrush}"
    SupportedOrientations="Portrait"
    Orientation="Portrait"
    mc:Ignorable="d"
    d:DesignWidth="480"
    d:DesignHeight="696"
    shell:SystemTray.IsVisible="True"
    DataContext="{Binding Main, Source={StaticResource Locator}}">
```

