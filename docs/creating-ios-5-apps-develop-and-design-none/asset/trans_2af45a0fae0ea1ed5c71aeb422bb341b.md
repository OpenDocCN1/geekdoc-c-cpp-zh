
![](img/fe9fea534a8e7868f811f7cd33da015f_30_0.png)

**图 1.12** 检查主视图控制器的类

接下来，segue（转场）和关系（relationships）定义了场景之间的连接。Segue 充当过渡。当应用触发一个 segue 时，它会使用指定的动画过渡到下一个场景。关系看起来很像 segue，但它们用于表示从属关系。容器控制器（如标签视图控制器）将使用关系连接到它们所管理的视图。

如果我们查看主视图控制器，可以看到它有一个指向所包含视图对象的视图插座变量（view outlet）。这意味着我们可以在控制器的代码中引用这个视图对象。我们还有一个来自反面视图控制器（flipside view controller）的引用插座变量。这仅表示反面视图控制器有一个指向主视图控制器的插座变量——我们稍后会看到（图 1.13）。这个场景中只有一个其他连接。点击 info 按钮；正如你所见，它有一个模态 storyboard segue，将其 `performSegueWithIdentifier:sender:` 方法连接到反面视图控制器。每当我们的 info 按钮被按下时，系统会自动调用该方法，触发到反面视图的 segue。

![](img/fe9fea534a8e7868f811f7cd33da015f_31_0.png)

![](img/fe9fea534a8e7868f811f7cd33da015f_31_1.png)

![](img/fe9fea534a8e7868f811f7cd33da015f_31_2.png)

**图 1.13** 主视图控制器的连接

**图 1.14** 反面视图控制器的连接

**图 1.15** 检查 segue 的属性

现在让我们看看反面视图控制器（**图 1.14**）。正如我们之前看到的，我们有一个指向主视图控制器的委托插座变量（delegate outlet）。这允许我们的反面视图控制器调用主视图控制器上的方法。具体来说，由于主视图控制器是反面视图控制器的委托，反面视图将期望主视图实现特定的方法来修改或控制反面视图的行为。反面视图控制器还有第二个插座变量，将其连接到它的视图。你可能已经猜到，这是一种通用模式。所有视图控制器都有一个连接到其视图的插座变量。

反面视图控制器还有两个传入连接。一个是我们在之前看到的 info 按钮的 segue。另一个表示来自 Done（完成）按钮的传入动作。我们稍后会看到这一点。

这个场景中只有另外两个连接。导航项在其 leftBarButtonItem 插座变量中引用了 Done 按钮。这会将栏按钮正确定位在导航栏中。此外，我们看到了从 Done 按钮到反面视图控制器的 done: 方法的动作连接。当按下 Done 按钮时，将调用此方法。

最后，选择 Attributes 检查器（从右数第三个图标），然后选择该 segue。这会显示我们 segue 的详细信息（**图 1.15**）。Identifier 字段允许我们在代码中标识这个 segue。Style 弹出菜单允许我们定义新视图的显示方式，而 Transition 弹出菜单允许我们定义从一个视图移动到下一个视图时使用的动画序列。在我们的例子中，这个 segue 名为 showAlternate。我们将以模态视图的方式呈现新场景，将旧视图水平翻转过来，在其背面显示新视图。

在大多数图形用户界面中，模态视图是一种必须先被关闭（通常通过点击确定或取消按钮）的视图，之后用户才能在应用中执行任何其他操作。这迫使用户专注于模态视图内的内容——他们必须先处理完其中的内容，然后才能继续。在桌面应用中，我们通常使用模态视图来显示诸如“保存”或“打印”对话框。在 iPhone 上，模态视图覆盖整个屏幕（不过 iPad 有更多额外的选项）。

那么，这一切意味着什么呢？我们正在追踪应用中的对象是如何创建的。UIApplicationMain() 方法创建了 UIApplication 和我们的 HWAppDelegate 类的一个实例。

接下来，UIApplicationMain() 在我们的应用的 info.plist 文件中查找主 storyboard。然后，它加载 storyboard 的初始场景，在我们的应用窗口中显示主视图控制器的视图。然后，我们的应用就可以接受用户输入了。

如果用户触摸 info 按钮，我们的 segue 就会启动。这会加载反面视图控制器，并将其显示为模态视图。当用户按下 Done 按钮时，它会调用反面视图控制器的 done: 动作。我们知道这会关闭反面视图，但我们还不知道这是如何工作的。要了解这一点，我们必须检查应用的代码。

## 检查代码

虽然 storyboard 让我们对应用有了一个很好的整体了解，但要真正理解它，我们需要深入研究代码。如果现在还不能完全理解，不用担心，我们将在第 2 章更详细地讲解 Objective-C。现在我们只是想了解各个事物是什么以及它们的作用。

让我们从 HWAppDelegate.h 开始。它声明了 HWAppDelegate 类的接口。你不会在这里发现任何非常令人惊讶的东西。HWAppDelegate 实现了 UIApplicationDelegate 协议——这使其能够充当应用委托。

委托（delegate）是一个代表另一个对象行事或与其协调的对象。委托通常充当主要的委派对象的助手。主对象将响应指定事件调用委托上预定义的方法。然后，委托使用这些方法来监视和控制委派对象。这使我们能够在不改变对象本身的情况下改变委派对象的行为。

我们还声明了 window 属性。当我们的应用加载 storyboard 时，它会实例化一个窗口对象并将其赋值给此属性。通常，iOS 应用有一个填满整个屏幕的窗口。这个窗口充当视图层次结构的根。它既创建了一个可以显示其他视图的空间，又将事件分发给适当的视图或子视图。

```objective-c
#import <UIKit/UIKit.h>

@interface HWAppDelegate : UIResponder <UIApplicationDelegate>

@property (strong, nonatomic) UIWindow *window;

@end
```

UIApplicationDelegate 协议定义了大量可选方法，我们可以实现这些方法来修改应用的行为。这些方法包括响应应用状态变化的方法，以及对本地、远程和系统通知的响应。你可以在开发文档中找到这些方法的完整列表。

在编辑器中点击 UIApplicationDelegate 一词，将在 Quick Help 检查器（Utilities 区域的上半部分）中显示该协议的简要描述。这种技术可以让我们快速了解任何类、方法或函数的描述。此外，Quick Help 检查器还包含指向其他资源的超链接。点击协议名称的超链接版本，Xcode 将打开开发文档中的完整描述。滚动到 Tasks 部分，即可查看方法的完整列表。

如果你打开 HWAppDelegate.m 文件，你会看到我们定义了其中几个方法——但它们都没有任何实际功能。目前，它们只是方法存根（stub）——占位符，等待我们填充细节。

```objective-c
#import "HWAppDelegate.h"

@implementation HWAppDelegate

@synthesize window = _window;

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // Override point for customization after application launch.

- (void)applicationWillEnterForeground:(UIApplication *)application
{
    /*
     Called as part of the transition from the background to the
     inactive state; here you can undo many of the changes made
     on entering the background.
     */
}
- (void)applicationDidBecomeActive:(UIApplication *)application
{
    /*
     Restart any tasks that were paused (or not yet started) while
     the application was inactive. If the application was
     previously in the background, optionally refresh the user
     interface.
     */
}
- (void)applicationWillTerminate:(UIApplication *)application
{
    /*
     Called when the application is about to terminate.
     Save data if appropriate.
     See also applicationDidEnterBackground:.
     */
}
@end
```
