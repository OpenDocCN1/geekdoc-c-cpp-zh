

## 墓碑化

到目前为止，在本章中你已经多次看到我使用“tombstoned（墓碑化）”这个术语；我想确保墓碑化的应用程序状态在这里得到特别说明。

如你所知，失去前台位置的应用程序会被停用。这个被停用的应用程序有机会在字典中保存临时状态。应用程序被停用但尚未被墓碑化的时间通常很短。如果应用程序在停用后没有被迅速重新激活，那么它就会被墓碑化。这意味着应用程序进程将被终止，但该应用程序的临时状态以及有关原始进程的一些其他信息会保留下来（也就是所谓的墓碑）。

当一个被墓碑化的应用程序被重新激活时，会创建该应用程序进程的一个新实例，但不会引发 Launching 事件，而是引发 Activated 事件，并且墓碑上留存的信息会被用来将应用程序恢复到停用之前的状态。

## 管理应用程序和页面状态

在本节的其余部分，我们将把到目前为止讨论的关于激活、停用、墓碑化和启动的信息充分利用起来。我们将利用这些信息构建一个与手机执行模型（Phone Execution Model）良好配合的应用程序，以提供无缝的用户体验。这个示例应用程序非常简单，只是将上次应用程序退出时的日期和时间存储在 PhoneApplicationService 的状态字典中。从现在开始，在本书的其余部分，我将把这个状态字典称为“墓碑状态”，因为后者比前者更容易阅读，也更容易说出口。

尽管这个应用程序很简单，但其中一些内容可能会带来非常宝贵的经验。首先，我没有把读写墓碑状态的代码放在 App.xaml.cs 的全局 Activated 和 Deactivated 事件中，而是把墓碑状态代码放在单个页面的 OnNavigatedTo 和 OnNavigatedFrom 事件中。

我喜欢这样做有几个原因。首先，如果你所有的临时状态“加载和恢复”代码都存在于应用程序级别，你就无法真正知道哪些内容在作用域内、哪些不在。为什么你需要为一个甚至还没有实例化的页面尝试保存临时状态呢？其次，如果你想在从墓碑状态恢复后对 GUI 产生可见的影响，那么由会受到状态恢复影响的页面来尽可能靠近 GUI 完成这些更新，会容易得多。

选择权在你手中，两种方案各有道理。决定如何以及何时使用墓碑状态是一个架构决策，对于你编写的每个应用程序都会有所不同；没有一条放之四海而皆准的固定配方能告诉你该怎么做。不过，你的应用程序必须遵守一些规则。

起初，你可能会想把整个视图模型对象（在许多情况下是一个深度嵌套的对象层次结构）塞进墓碑状态字典。尽管你可能很想这样做，但这样做不仅不可能，而且不是一个好主意。你只能在状态字典中存储基本数据类型。即使你能在状态字典中存储复杂的对象图，你也不会想这样做。那不是墓碑状态的用途。使用以下准则来确定是否应该将某个值存储在墓碑状态中：

你想要存储在墓碑状态中的值，是不是一个需要花费大量时间生成但可以存储为基本数据类型的值？你想要存储在墓碑状态中的值，是不是一个出于设计目的无法永久存储在磁盘上，但只需几个基本数据类型就能存储的值？如果这两个问题的答案有一个为“是”，那么你的应用程序就很有可能会从使用墓碑状态中获益。

我能想到的应该使用墓碑状态的最佳示例之一，可能就是位置感知应用程序。当应用程序启动时，它使用手机的 GPS 获取当前位置，然后将 Bing Maps 控件以该位置为中心。如果不使用墓碑状态，当用户短暂退出应用程序然后返回时，应用程序将重新获取 GPS 位置，这可能需要很长时间。通过将当前经度和纬度值缓存到墓碑状态字典中，你可以为用户提供更好的体验。这样，当你的应用程序被激活时，你可以让 Bing 地图以缓存的位置为中心，而无需重新获取位置。

要创建这个示例，请创建一个名为 ExecutionModelTest 的新 WP7 应用程序，并向主页面添加一个文本框控件。将 MainPage.xaml.cs 的代码隐藏文件修改为与清单 13.1 中显示的代码一致。

### 清单 13.1 在激活和停用期间使用墓碑状态

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using Microsoft.Phone.Controls;
using System.Threading;
using Microsoft.Phone.Shell;
using System.Diagnostics;

namespace ExecutionModelTest
{
public partial class MainPage : PhoneApplicationPage
{
private ViewModel vm;

// Constructor
public MainPage()
{
    InitializeComponent();

    vm = new ViewModel();
    this.DataContext = vm;
}

protected override void OnNavigatedTo(
    System.Windows.Navigation.NavigationEventArgs e)
{
    base.OnNavigatedTo(e);

    if (PhoneApplicationService.Current.StartupMode ==
        StartupMode.Activate)
    {
        IDictionary<string, object> state =
            PhoneApplicationService.Current.State;

        if (state.ContainsKey("LastLaunchDate"))
        {
            Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                vm.LastLaunchDate =
                    (DateTime)state["LastLaunchDate"];
            });
        }
        else
        {
            Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                vm.LastLaunchDate = DateTime.MinValue;
            });
        }
    }
}

protected override void OnNavigatedFrom(
    System.Windows.Navigation.NavigationEventArgs e)
{
    base.OnNavigatedFrom(e);

    IDictionary<string, object> state =
        PhoneApplicationService.Current.State;

    Debug.WriteLine(
        "storing value in tombstone state.");
    state["LastLaunchDate"] = DateTime.Now;
}
}
}
```

上述代码中引用的 ViewModel 类是一个简单的类，只包含一个属性。当该属性发生变化时，它会触发 PropertyChanged 事件，从而通知绑定了数据的 WP7 Silverlight GUI 值已更改。这个数据绑定的 GUI 包含前面提到的文本框，该文本框绑定到以下视图模型中的 LastLaunchDate 属性：

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
using System.ComponentModel;

namespace ExecutionModelTest
{
    public class ViewModel : INotifyPropertyChanged
    {
        private DateTime lastLaunchDate;

        public DateTime LastLaunchDate
        {
            get
            {
                return lastLaunchDate;
            }
            set
            {
                lastLaunchDate = value;
                NotifyPropertyChanged("LastLaunchDate");
            }
        }
    }

    private void NotifyPropertyChanged(string propName)
{
    if (PropertyChanged != null)
        PropertyChanged(this,
            new PropertyChangedEventArgs(propName));
    }
    public event PropertyChangedEventHandler PropertyChanged;
}
}
```

在你输入完代码（或执行随书附带的代码）后，启动应用程序。注意，当你首次启动应用程序时，文本框中的值等于 DateTime.MinValue。点击模拟器上的“开始”按钮，然后一秒钟后按下“返回”按钮。如果一切顺利，你会短暂地看到一个显示“正在恢复（Resuming）”的屏幕。这个屏幕会在应用程序被墓碑化并正在重新激活时出现。谢天谢地，这正是我们想要测试的场景。“正在恢复”屏幕消失后，应用程序会重新出现。这一次，应用程序不再显示 DateTime.MinValue，而是显示模拟器在上次应用程序退出时所知道的日期和时间。

关于使用墓碑状态，你最后需要知道的是，它非常难以调试。如果你的代码在应用程序被激活时执行，并且在尝试从墓碑状态字典中读取值时出了问题，那么很有可能会出现这样的情况：调试会话直接停止，模拟器卡在“正在恢复”屏幕上。下次启动应用程序时，由于之前的崩溃，模拟器甚至可能需要完全重启操作系统。简而言之，请在激活/停用事件处理程序之外测试你的墓碑状态操作代码（或者更好的是，编写单元测试，我将在本书后面部分介绍），这样在将其放入难以调试的事件处理程序之前，你可以确保它能正常工作。

## 小结

本章带你简要了解了手机执行模型。多任务处理是大多数桌面用户视为理所当然的功能。事实上，我们太习以为常，以至于手机制造商不遗余力地让他们的应用程序看起来像是在多任务运行，即使它们只是在以一种高效的方式假装多任务。

iPhone 和 Windows Phone 7 设备都是这样进行多任务处理的。尽管至少在撰写本文时，iPhone 可以在后台做一些 Windows Phone 7 做不到的事情，但两款设备上的多任务处理非常相似。本章向你展示了 WP7 应用程序是如何工作的，并带你了解了 WP7 应用程序生命周期中的各种事件和重要阶段。你学习了激活、停用、启动、关闭，以及“墓碑化”的含义。

掌握了这些知识，了解了当用户点击开始按钮、返回按钮，或者从磁贴或菜单启动你的应用程序时，底层真正发生了什么，你将能够更好地开发出流畅、无缝的用户体验，并达到 WP7 用户期望的表现。

