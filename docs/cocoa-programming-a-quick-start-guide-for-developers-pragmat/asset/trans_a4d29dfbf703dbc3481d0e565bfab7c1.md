
所有内容都混杂在一起。这仍然比在冗长的源代码列表中搜索要好，但我们可以使用 #pragma mark 让它变得更好。将以下注释：

```objc
//Memory Management
```

替换为：

```objc
#pragma mark -
#pragma mark Memory Management
```

现在，方法的下拉列表看起来像这样：

![](img/9355405953264484a02198b0e3d25b7e_188_0.png)

#pragma mark - 会绘制水平分隔线，而 #pragma mark Memory Management 会生成粗体标题。⁹ 在所有小节的位置引入这些标题，你的代码就会变得更容易导航，正如我们在下一页看到的那样。¹⁰

我们的桌面和 iPhone Web 浏览器已经很好地为我们服务了。我用它们来演示在代码中创建类，以及在代码或 nib 中实例化对象。你已经编写并调用了带参数和不带参数的方法。

9. 不要在 - 后添加尾随空格，否则 #pragma mark - 在下拉列表中会呈现为短横线而不是水平线。
10. 如果你在单独的行上合成每个属性，它们将分别出现在单独的行上，而不是像我的那样全部显示在一行。

```objc
@implementation MobileBrowserViewController

Synthesizers
    address, webView, backButton, forwardButton, activityView

View Controller Utility Methods
    -disableView
    -enableWebView
    -loadURLFromTextField
    -resetButtons

Initialization
    -viewDidLoad

Web View Delegate methods
    -webViewDidStartLoad
    -webViewDidFinishLoad

Text Field Delegate methods
    -textFieldDidBeginEditing
    -textFieldShouldReturn

Memory Management
    -didReceiveMemoryWarning
    -dealloc
```

你已经使用过属性，并学会了管理内存。你已经通过动作和出口将应用程序连接起来，并学会了使用委托。这些是你作为 Cocoa 开发者会一直使用的一些基本技术。

但还有更多……

## 第11章：发布和监听通知

生活中有太多事情需要你跟踪。每隔几分钟甚至每天一次停下来检查所有事情的进展并不现实。对于大多数事情，你只想知道什么时候发生了变化。

也许你希望在股票达到某个价格时收到提醒。也许提醒应该改为发送给经纪人，并附带一组特定指令。你会如何设置呢？

你必须与通知中心约定好，你对了解某个特定事件感兴趣。在我们的例子中，这类似于“当 XXX 跌到 yyy 时告诉我”。你必须告诉通知中心它应该通知谁。它应该把通知发送给你，还是发送给某个代理？

现在，无论消息是发给我还是发给别人，我们都需要快速弄清楚如何处理它。我们一天会收到大量通知。如果上下文对我们来说是清晰的，就更容易解析它们并弄清楚下一步该做什么。在代码中，这通过告诉通知中心要向我们发送什么消息来实现。消息可能是买入或卖出。换句话说，我们是在告诉通知中心，它将为我们已经设置的目标发送什么动作。

然后，通知中心会把通知作为消息的一部分发送给我们的目标。在代码中，这意味着通知对象是消息的参数。通知将包含接收者可能需要的信息。你总能找到通知的名称以及关于谁发布了通知的信息。你还会获得可能需要用来处理该通知的其他信息。¹

1. 在本章中，我们不会研究这个通知对象。我们的示例将侧重于注册接收通知以及响应收到通知。我们将在第13章 *使用字典* 中回到这个主题，并向你展示如何使用通知对象。

### 11.1 练习：创建模型

我们的下一个运行示例将在应用程序启动和终止时显示其名称和图标。与浏览器一样，这个应用程序的目的不是构建一个功能齐全的应用程序，而是利用它来进一步了解 Cocoa 编程的各个方面。在本章中，我们将从通知开始。

创建一个新的 Cocoa 应用程序，并将其命名为 HelloApplication。记住，我们回到了 Mac OS X 应用程序的世界，因此不需要管理自己的内存。更改项目设置，使垃圾回收成为必需。从现在起，对于我们创建的每个项目，你都要这样做。

添加两个都继承自 NSObject 的类。CurrentApp 类将表示此应用程序的模型。暂时不要以任何方式自定义它。ActivityController 类将是我们的控制器。在 MainMenu.xib 中实例化它。在 ActivityController 的 awakeFromNib 中创建 CurrentApp 的实例，并将其存储到名为 currentApp 的属性中。

### 11.2 解决方案：创建模型

到现在，你应该已经为创建新项目和文件建立了一些肌肉记忆。你在创建 HelloApplication 时没有选中任何复选框。你创建了一个新文件 CurrentApp.m，它是一个继承自 NSObject 的 Objective-C 类。然后你对 ActivityController.m 重复了这一过程。

现在实例化你的类。在 Interface Builder 中，将一个 ActivityController 实例拖入 MainMenu.xib 的 Document 窗口。

在 Xcode 中，向 ActivityController.h 声明一个实例变量和一个名为 currentApp、类型为 CurrentApp 的属性。记得使用 @class 前向声明 CurrentApp 类。

![](img/9355405953264484a02198b0e3d25b7e_192_0.png)

```objc
#import <Cocoa/Cocoa.h>
@class CurrentApp;

@interface ActivityController : NSObject {
    CurrentApp *currentApp;
}
@property CurrentApp *currentApp;

@end
```

我希望你记得在 import 语句下方加入 CurrentApp 的前向声明。这个属性声明可能看起来有点“裸露”。如果没有垃圾回收，内存属性就必须是 retain。使用垃圾回收时，这等价于 assign，而 assign 是默认值，因此我们完全可以省略它。²

2. 当然，如果你是在 64 位机器上编写代码并面向 64 位机器，也可以省略实例变量。

在 ActivityController.m 中，你需要合成 currentApp，并在 awakeFromNib 中创建它的实例。务必导入 CurrentApp.h。

```objc
#import "ActivityController.h"
#import "CurrentApp.h"

@implementation ActivityController

@synthesize currentApp;

-(void)awakeFromNib {
    self.currentApp = [[CurrentApp alloc] init];
}
@end
```

### 11.3 注册通知

对象注册接收通知的方式如下：

```objc
[[NSNotificationCenter defaultCenter]
    addObserver:observerObject
    selector:@selector(methodName:)
    name:NameOfNotification
    object:notifyingObject];
```

零个、一个或多个对象可以针对同一通知向通知服务器注册，而一个对象可以注册任意多种它想要接收的通知类型。让我们更仔细地看看注册中使用的每个参数：

- 你正在向默认通知中心发送 addObserver:selector:name:object: 消息。
- 在我们的例子中，我们会把 observerObject 设置为 self，但它可以是任何有兴趣接收该通知的对象。这将是你设置由通知触发的动作的目标。
- selector 指定动作。这是属于观察者的方法名，当收到通知时将调用该方法。
  - 此方法名以冒号结尾，因为该方法将接收一个参数。
  - 这个单一参数是发送通知时传入的通知对象。
- name 是正在注册接收的通知名称。
- object 指你感兴趣其通知的对象。在我们的 SimpleBrowser 示例中，你可能不止一个 web view 在发布通知，而你可能只想监视其中特定的一个。你也可以传入 nil，以接收应用程序中任何对象发布的此类通知。

在股票示例中，observerObject 是你或你的代理。selector 是要执行的动作，例如 buy: 或 sell:。name 是你正在注册接收的通知，例如“价格跌到 $yyy”。object 可能是你正在监听的股票名称。

核心思想是：你通过传入一个将在特定对象上调用的方法名来注册监听某个通知。当该方法被调用时，它会接收一个 NSNotification 对象作为唯一参数。
