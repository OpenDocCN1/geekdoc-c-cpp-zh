
## 测试 App

现在，保存项目，编译，希望你没有写错字，并在 iPhone 模拟器中运行它。你应该看到以下值：

+* 0.00 英里
+* 位置计数：1
+* 日期：（当前日期）
+* 纬度：37.73168
+* 经度：-122.030731
+* 不确定半径：100.00 米
+* 高度：0.00 米
+* 高度精度：米

## 第18章：GPS 与位置管理

如果你看到了这些值，那么恭喜！你编写了第一个位置位置应用程序。如果你遇到了问题或无法让应用程序工作，完整代码可以在 http://roybryant.net/iphone/chapter18/Distance-done.zip 获取。为了真正测试应用程序，你需要将其放入真实的设备。在第21章中，你将学习如何逐步将自己的应用安装到手机上，所以你可能想跳着看。当 Distance 在手机上后，你可以看到来自手机的实时更新流，你的距离不会永远停留在“0.00”。

## 总结

基于位置的应用无疑将成为你日常生活的一部分。通过使用 Core Location 框架，你可以轻松跟上潮流，为自己的应用程序添加位置支持。使用该 API 只需要两个类：`CLLocation` 和 `CLLocationManager`。使用 `CLLocation` 对象，你可以获取用户的纬度、经度甚至当前高度。由于存在某种程度的不准确，你可以访问 `CLLocation` 的 `horizontalAccuracy` 和 `verticalAccuracy` 属性来显示位置数据的可靠性。通过构建 Distance 应用，你学会了如何过滤错误的位置数据、将米转换为英里并从 `CLLocationManager` 获取更新。

下一章，学习与 iPhone OS 4.0 中两个令人兴奋的新 API 集成：iAd 和多任务处理。

# iAd 与多任务处理

# 第 19 章

## 本章内容

- iPhone OS 4.0
- iPhone 上如何实现多任务处理
- 在后台运行你的 App
- 在你的 App 中展示广告盈利
- 使用 iAd 框架

抱怨 iPhone 缺少功能是博主和技术记者的最喜欢的消遣。他们会写下类似的话：“如果没有第三方 App 支持，你如何把 iPhone 称为真正的手机呢？”以及“复制和粘贴功能在哪里？”以及“为什么没有多任务处理？”

Apple 本可以选择在 2007 年发布的首代 iPhone 中包含这些功能的半成品版本。然而，Apple 宁愿构建一个具有较少但质量出众的简单设备，而不是一个充斥着大量平庸功能的复杂设备。这种政策的结果是什么？Apple 拥有最成功的 App Store、最好的复制和粘贴功能，以及目前市场上任何手机中最省电的多任务处理系统。

在本章中，你将学习如何使用 4.0 多任务 API 在后台运行你的 App。你还将探索 iAd 框架，让你看到在你的 App 中产生广告收入是多么简单。

# iPhone OS 4.0

iPhone OS 4.0 是 iPhone OS 的一次重大升级。以下是你现在可以在应用程序中使用的一些 4.0 API：

- 多任务处理——你现在可以同时运行多个第三方应用程序。
- iAd——通过利用新的 iAd 框架，你可以通过向用户提供经 App Store 批准的广告来盈利。
- Game Center——你想构建一个多人游戏吗？通过 Game Center，你可以轻松地为游戏添加对匹配机制和排行榜。
- 本地通知——本地通知让你在你的 App 在后台运行时，能够向用户显示警报信息。例如，当你的聊天应用程序收到消息时，提醒用户。
- 事件集（Event Kit）——访问快速查看控制器以预览图像、文档和 PDF。
- 加密——安全地存储和读取敏感用户数据。
- 核心电话（Core Telephony）——访问用户的移动服务运营商。

> 注意事项
> 如需 iPhone OS 4.0 功能的完整列表，请访问 http://developer.apple.com/iphone 并搜索标题为“What’s New in iPhone OS 4”的文档。

然而，新 API 最大变化是增加了多任务处理。接下来的章节将详细介绍多任务处理在 iPhone OS 上如何工作，以及作为开发者在你的 App 中支持它必须执行的操作。

# 多任务处理

那么多任务处理到底是什么呢？多任务处理赋予你同时运行多个应用程序的能力。与大众认知相反，iPhone OS 一直具有多任务处理功能。例如，Mail 应用在未打开时会下载新的邮件。Safari 即使在你关闭 App 后，也可以从网站流式传输音频。然而，由于各种原因，Apple 过去没有为第三方开发者提供使用多任务处理的方法。直到现在。

# 入门使用多任务处理

> 定义
> 多任务处理是同时运行两个或多个应用程序的能力。

通过多任务处理，你可以编写一个聊天应用程序，在收到新消息时提醒用户。你可以在用户检查电子邮件时跟踪你的用户的位置。你可以在用户查看 Facebook 时为她播放音乐。由于 iPhone OS 4.0 中多任务处理的引入，完全新类别的应用程序现在已成为可能。

好了，这是一件大事。那么你该如何使用它呢？

并不是所有的 iPhone 设备都可以在后台运行 App。事实上，并不是所有的 iPhone OS 4.0 设备都能在后台运行。特别是运行 iPhone OS 4.0 的 3G iPhone 不支持多任务处理。

由于这一事实，在使用功能之前，你应该检查并确保支持多任务处理。你可以使用这段代码片段安全地检查多任务处理：

```
// 检查 App 是否可以在后台运行

// (BOOL)canRunInTheBackground

{

    Device *device = [UID currentDevice];

    BOOL backgroundSupported = NO;

    if ((device respondsToSelector:(isMultitaskingSupported)) {

        backgroundSupported = device.multitaskingSupported;

    }

    return backgroundSupported;

}
```

上述代码同时处理了 iPhone OS 4.0 设备（定义了 `isMultitaskingSupported` 方法的设备）和 iPhone OS 4.0 之前的设备（未定义 `isMultitaskingSupported` 的设备）。

可以在不检查是否已启用多任务处理的情况下完成大部分后台处理。然而，在需要知道的情况下，上述方法提供了一种简单的检查方式。

# 后台任务

大多数支持多任务处理的移动设备不需要程序员编写任何额外的代码。在这些设备上，在后台运行的 App 与你正在查看的 App 无异。然而，这些设备的电池寿命通常较差，因为操作系统必须努力工作以保持所有应用程序同时运行。

为了解决电池问题，Apple 以非常不同的方式实现了多任务处理。当用户从你的 App 切换到其他 App 时，你的 App 默认会被*挂起（suspended）*。挂起的应用不执行代码。

![](img/5ebee1dd8eb3ab735869e)

> 定义
> 挂起的应用是一个已停止但未被完全移除的应用。它们被保留在内存中，以便在用户切换回时快速启动。

如果你想在后台运行代码，必须通知操作系统。目前操作系统仅支持三种类型的任务：

- 播放音频
- 跟踪用户位置
- VOIP

要在你的 App 中支持一个或多个任务，你需要在 `Info.plist` 中包含 `BackgroundModes` 键。该键的值是一个数组，可能值为 `audio`、`location` 和 `voip`。如果没有设置 `BackgroundModes`，你的 App 将不在后台运行。

## 注意事项

在 `Info.plist` 中设置 `location` 键可以让你以最高精度跟踪位置。然而，这会迅速消耗电池。如果你的 App 不需要精确位置，你应该通过在 `locationManager` 上调用 `startMonitoringLocation` 来接收位置变化。注意，这种方法无需在 `Info.plist` 中设置 `location` 键即可向你的 App 传递位置更新。

![](img/5ebee1dd8eb3ab735)

## 第 19 章：iAd 与多任务处理

此外，执行后台处理的其他两种方法包括：

- 为完成任务请求更多时间——当 App 进入后台时，调用 `UIApplication` 的 `beginBackgroundTaskWithExpirationHandler:` 方法。任务完成后，通过调用 `endTask` 通知系统。
- 调度本地通知——要调度本地通知，创建一个 `ULocalNotification` 对象并将 `fireDate` 属性设置为闹钟响起的时间。你可以通过设置 `alertBody` 属性来自自定义闹钟文本，甚至可以通过在本地通知对象上设置 `soundName` 属性播放自定义声音。

> 定义
> 本地通知是 iPhone OS 4.0 的新功能，允许你向用户显示警报消息。本地通知的样式与短信警报完全相同，但你可以自定义它显示时的文本和声音。

在指示你的 App 已准备好进入后台后，你需要知道应用程序何时进入和退出后台。这一过程将在下一节解释。

# 后台处理的应用程序生命周期

在多任务处理之前，你的应用程序生命周期非常简单。你的 App 要么开启要么关闭。如果用户正在查看你的 App，它就是开启的。当他们点击主按钮时，App 就关闭了。

> 定义
> 应用程序生命周期描述了应用程序从创建到退出期间可能处于的不同状态。

会有两个方法调用你的应用程序以反映这两种状态。当 App 被创建时，`application:didFinishLaunchingWithOptions:` 方法会在 `UIApplicationDelegate` 上调用。当 App 即将退出时，`applicationWillTerminate:` 会在 delegate 上调用。

# 342 第 4 部分：你迫待使用的 API

现在 iPhone OS 已支持多任务处理，你的 App 可以同时在前台和后台运行。在 iPhone OS 4.0 中，应用程序 delegate 上调用了两个新方法，用于在 App 进入和退出这些状态时通知你：

- *applicationDidEnterBackground:*
- *applicationWillEnterForeground:*

## 定义

一次只向用户显示一个应用程序，即使该应用程序对用户不可见，或者被认为在后台运行，它仍被认为处于运行状态。

这些方法会在你的 App 进入和退出后台执行时通知你。当进入后台时，你应该保存应用程序的状态，因为你的 App 在后台运行时可能会被系统终止。当用户切换回你的 App 时，会调用 `applicationWillEnterForeground:` 方法。这是重绘界面并重新启用你在进入后台时关闭任何设置的绝佳位置。

## 崩溃与学习

请注意，用户可以在你的 App 于后台运行时手动退出它。当这种情况发生时，会立即调用 `applicationWillEnterTerminate:`。

## 有个小技巧

Apple 在其文档中对应用程序生命周期提供了非常棒的解释。前往 http://developer.apple.com/iphone，并在“iPhone Application Programming Guide”文档中找到名为“The Core Application Design”的页面获取这一优质资源。

## 示例代码

为了查看多任务处理在实践中是如何工作的，网上提供了几个示例项目：

- *本地通知 App*——第一个示例设置了一个在 App 进入后台 5 秒后响响的闹钟。该 Xcode 项目可以在此处获取：http://troybrant.net/iphonebook/chapter19/LocalNotifications.zip。

- **后台音频**——第二个 App 展示了如何在后台播放音频。Xcode 项目可以在此处获取：http://royvant.net/iphonebook/chapter19/BackgroundAudio.zip。

- **重大位置位置跟踪**——第三个 App 跟踪用户位置的变化。Xcode 项目可以在此处获取：http://royvant.net/iphonebook/chapter19/SignificantChangeLocationTracking.zip。

- **精确位置跟踪**——第四个 App 展示了如何在 App 在后台运行时获取精细位置数据。Xcode 项目可以在此处获取：http://royvant.net/iphonebook/chapter19/PreciseLocationTracking.zip。

务必检查示例项目中的 Info.plist 文件，以查看何时需要使用 `UIBackgroundModes` 以及何时不需要。

## 做一个良好的多任务公民

当你的 App 进入后台执行时，你需要遵循一些规则才能被认为是一个良好的后台应用程序。这些规则包括：

- **不要进行任何 OpenGL ES 调用**——如果你在后台运行时发出了任何 OpenGL ES 调用，iPhone OS 会立即终止你的应用程序。虽然这些规则中的大部分是建议性的，但这一条是强制性要求。

- **避免操作窗口和视图**——当你的 App 在后台运行时，用户在激活应用程序之前将看不到界面。通过将所有重绘操作排队到 App 回到前台时执行，来节省电池和处理能力。

- **在移动到后台之前保存应用程序数据**——你的应用程序可能会在后台被终止，因此要准备好在意外终止的情况下恢复状态。

可以在 http://developer.apple.com/iphone 上“iPhone Application Programming Guide”文档中名为“Executing Code in the Background”的页面找到最佳实践列表。

## iAd

除了多任务处理外，iPhone OS 4.0 还引入了 iAd 框架用于在你的应用程序中投放广告。下一节将详细介绍你如何通过显示广告为 App 产生额外收入。

你可能在想：“我到底凭什么要用广告骚扰我的用户呢？”答案是：通过广告，你可以免费发布 App 的同时产生收益。

你可能还在想：“移动广告太糟糕了。”我同意你的观点。事实上，史蒂夫·乔斯（Steve Jobs）在介绍 iPhone OS 4.0 的演讲中提到了移动广告的糟糕状况。正如 iPhone 是对手机的重新构想，iAd 试图通过向用户提供精美、高质量的广告来彻底改变移动广告。

## 工作原理

投放广告的过程非常简单。显示广告，然后赚钱。显示更多广告，赚更多钱。然而，你应该保持克制，确保你不会过度影响 App 的用户体验。

在撰写本文内容时，广告有两种标准尺寸：用于竖屏广告的 320x50 和用于横屏广告的 460x32。

要在你的 App 上显示广告，你需要在你的界面中插入一个横幅广告。iAd 框架提供了 `ADBannerView` 类来显示横幅广告。`ADBannerView` 显示一系列广告并处理用户交互。当你创建横幅视图时，该视图会自动在后台从 Apple 下载广告。当广告可见时，视图会循环显示一系列广告。

> 定义
横幅广告是一种在网上广泛使用的矩形广告。在移动设备上，横幅广告通常位于 App 界面的顶部或底部。

当用户点击横幅视图时，可能会发生许多事件。广告可以启动模态视图，甚至启动 Safari。注意，在启动 Safari 的情况下，你的程序会被挂起或在后台运行。

要获取广告何时加载、用户何时点击以及何时退出广告，你必须成为视图的代理。`ADBannerView` 协议为这些每个事件提供了回调。

这就是 iAd 的全部。框架由两个文件组成：横幅视图及其代理。下一节提供了在 App 中添加和显示横幅视图的示例代码。

## 示例代码

假设你想在一个（我们称之为 AdTestViewController）顶部显示一个带有广告的视图。该控制器的接口如下：

```objc
#import <UIKit/UIKit.h>
#import <iAd/iAd.h>
@interface AdTestViewController : UIViewController
<ADBannerView>
{
    UITableView *tableView;
    ADBannerView *bannerView;
}
@property (nonatomic, retain) IBOutlet UITableView *tableView;
@end
```

假设 `tableView` 属性已在 Interface Builder 中正确连接。在前面的代码中，注意视图控制器遵循 `ADBannerView` 协议，并且 `ADBannerView` 的引用存储在实例变量中。

TestViewController 的实现文件如下：

```objc
#import "AdTestViewController.h"
@implementation AdTestViewController
```

```objc
@synthesize tableView;
- (void)viewDidLoad
{
  if (!bannerView) {
    // 程序创建横幅视图
    bannerView = [[ADBannerView alloc] init];
    // 设置横幅视图的大小为 320x50
    bannerView.currentContentIdentifier = ADBannerSizeIdentifier320x50;
    // 设置代理
    bannerView.delegate = self;
    // 将横幅视图设置为表格头部
    tableView.headerView = bannerView;
  }
}
@end
```
