
```csharp
{
    case GeoPositionStatus.Disabled:
        if (watcher.Permission ==
            GeoPositionPermission.Denied)
        {
            watcherStatus.Text =
                "Application is not allowed to use location services.";
        }
        else
        {
            watcherStatus.Text =
                "Location services not working properly.";
        }
        break;
    case GeoPositionStatus.Initializing:
        startLocationButton.IsEnabled = false;
        watcherStatus.Text = "Initializing...";
        break;
    case GeoPositionStatus.NoData:
        stopLocationButton.IsEnabled = true;
        watcherStatus.Text = "Active, but no location data.";
        break;
    case GeoPositionStatus.Ready:
        watcherStatus.Text = "Location data is available.";
        stopLocationButton.IsEnabled = true;
        break;
    }
}

private void stopLocationButton_Click(object sender,
    RoutedEventArgs e)
{
    watcher.Stop();
    watcherStatus.Text = "(not monitoring GPS)";
}
```

如果你在模拟器中运行它，你不会得到任何有用的信息，尽管当你点击开始按钮时它仍会报告 GPS 监视器处于活动状态。要看到实际效果，你需要在具有清晰 GPS 信号的应用程序上运行它。提示：不要从地下防空洞、掩体或密封地下室尝试此操作。

### Summary

本章首先概述了大多数现代智能手机提供的常见系统服务，包括 iPhone 和 Windows Phone 7。随后，我们浏览了 Windows Phone 7 应用程序可用的选择器和启动器。最后，我们通过探索应用程序可用的一些硬件服务结束了本章，例如加速度计、GPS，甚至 FM 收音机调谐器。

如果你一直从头阅读到这里，你现在应该对 Windows Phone 7 应用程序的能力和功能有非常好的理解，如何利用这些功能，以及如何使用 WP7 Silverlight 用户界面元素向用户呈现它们。

## Introduction to Application Tiles

> *想象力比知识更重要。因为知识是有限的，而想象力概括着世界的一切，推动着进步，给人类带来进化。*
>
> Albert Einstein

本章虽然简短，但为 Windows Phone 7 编程应用程序磁贴提供了有用的介绍。Windows Phone 7 应用程序磁贴的概念与 iPhone 或 iPad 上的某些概念之间不存在直接对应关系。在阅读本章时，你将看到应用程序磁贴所扮演的角色，它们如何涵盖 iOS 中存在的多个功能领域，以及它们如何提供 iOS 中不存在的一些功能。

本章还概述了如何在不使用推送通知的情况下操作这些磁贴，推送通知是下一章的主题。最后，在本章末尾，我将向你展示如何在服务器上做一些花哨的技巧，以绕过磁贴的一些限制，并在不发送任何推送通知的情况下创建令人难以置信的引人注目的磁贴。

### What Is a Tile?

当你解锁或打开 Windows Phone 7 设备并滑动主屏幕后，你看到的第一件事就是一组磁贴。此集合可滚动，通常应包含你最常用的应用程序。如图 11.1 所示，微软为你提供了一些开箱即用的磁贴，用于处理电话、联系人（包括 Facebook 等社交网络）、消息、电子邮件、图片、游戏（Xbox Live）和 Internet Explorer 等事项。

![](img/04a00d46bb1059867d95707babd62ee7_158_0.png)

图 11.1 充满应用程序磁贴的主屏幕。

这些磁贴主要有两个目的。第一个是为你提供一个易于点击的目标来启动你最常用的应用程序。你可以将其视为在桌面或系统托盘上（或 Mac OS X 上的 Dock）为应用程序创建快捷方式的移动等价物。其次，这些磁贴提供有意义的摘要信息，你可以利用它来决定是否要启动应用程序。

例如，电话磁贴显示你错过了多少通电话或等待的语音邮件数量。消息磁贴告诉你有多少条未读短信。Outlook 磁贴告诉你有多少封未读电子邮件。如果这些磁贴上的信息发生变化，你可以使用易于阅读的磁贴表面来决定是否要启动应用程序。另一个示例可能是天气磁贴，在代表当前天气条件的背景图像上显示当前温度。这为你提供了关于天气的最重要信息，如果你想要详细信息，可以点击磁贴启动完整的天气应用程序。

你在图 11.1 中看不到的是，非微软开发人员编写的应用程序磁贴（那可能就是你）可以有一个背景图像和一个叠加在背景图像上的数字徽章。这使你的磁贴能够通知用户应用程序内的项目可能需要他们的关注。下一节将向你展示如何创建自己的磁贴，并讨论使用它们时的一些限制和怪癖。

### Creating Your First Tile

磁贴很容易创建。事实上，开发人员无需做任何事情来创建它们，因为创建磁贴完全取决于最终用户。开发人员需要做的就是告诉应用程序清单，如果用户为开发人员的应用程序创建磁贴，应该使用哪个背景图像和标题文本。

要了解其工作原理，请创建一个新的 Windows Phone 7 应用程序。在解决方案资源管理器中右键单击项目并选择属性。向下扫描属性页到最后几项，你将看到应用程序的磁贴属性定义位置。你可以选择背景图像（默认 WP7 应用程序模板已为你提供了一个）和磁贴的标题文本。你在此处提供的文本必须足够短，以便显示在磁贴底部。将文本更改为你喜欢的任何内容，然后运行应用程序。

在模拟器中运行应用程序时，点击开始（飞行窗口）按钮。现在转到应用程序列表（屏幕右上角的右箭头）。在你刚刚创建的应用程序标题上左键单击并按住。你将看到两个选项，如图 11.2 所示：Pin to Start 和 Uninstall。

![](img/04a00d46bb1059867d95707babd62ee7_159_0.png)

图 11.2 按住应用程序上的手指/按钮。

如果在提示时选择 Pin to Start，模拟器会将你带回主屏幕，在那里你会看到你的磁贴。如果你没有安装任何其他磁贴，你的屏幕可能看起来像图 11.3 中的那样。

![](img/04a00d46bb1059867d95707babd62ee7_160_0.png)

现在当用户解锁设备时，他们会看到你应用程序的一个漂亮的大磁贴。他们可以点击此磁贴启动应用程序，也可以通过使用右箭头并在出现的列表中点击应用程序标题手动启动应用程序。

随新应用程序模板提供的默认背景是一个 173x173 24 位 PNG 文件。在为应用程序创建自己的背景图像时，你必须遵守此约定。主屏幕磁贴（至少由普通非微软开发人员创建的磁贴）始终为相同大小，并且大小不得超过 80KB。

### Working with Tile Schedules

许多应用程序会很满意将磁贴表面仅用作大型图标；一个用于品牌展示和超大手指点击目标的地方。然而，根据你编写的应用程序类型，你可能想要做更多的事情。你可能想要使你的应用程序磁贴具有一定的动态性。请注意我在这里说“一定程度”，因为我们将在下一章讨论推送通知时谈论如何使你的磁贴更加动态。

磁贴计划受手机本身的控制。你可以创建一个磁贴计划实例，该实例将导致你的应用程序磁贴更新一次、每周一次、每天一次或

