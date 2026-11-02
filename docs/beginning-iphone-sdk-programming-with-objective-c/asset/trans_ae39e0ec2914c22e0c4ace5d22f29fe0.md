
构建标签栏应用程序时，您可以使用基于窗口的应用程序模板，或更方便地使用提供的标签栏应用程序模板。

以下“试用”使用标签栏应用程序模板创建项目并了解底层架构。按此处指示下载必要的项目文件。

## 试用 创建标签栏应用程序

*代码文件 [TabBarApplication.zip] 可在 Wrox.com 下载*

- 1. 使用 Xcode，创建一个新的标签栏应用程序项目并将其命名为 `TabBarApplication`。
- 2. 检查项目的内容（见图 8-3）。除了通常的应用程序委托文件外，它还包含一个视图控制器（`FirstViewController`）和两个 XIB 文件：`MainWindow.xib` 和 `SecondView.xib`。

![](img/aab2d775c46f70cd606f2e58e2521324_214_0.png)

图 8-3

3. 检查 TabBarApplicationAppDelegate.h 文件的内容，如下所示：

```objc
#import <UIKit/UIKit.h>
@interface TabBarApplicationAppDelegate : NSObject <UIApplicationDelegate, UITabBarControllerDelegate> {
    UIWindow *window;
    UITabBarController *tabBarController;
}
@property (nonatomic, retain) IBOutlet UIWindow *window;
@property (nonatomic, retain) IBOutlet UITabBarController *tabBarController;
@end
```

请注意，与通常的 UIViewController 类不同，您现在使用的是继承自 UIViewController 类的 UITabBarController 类。TabBarController 是一个专门的 UIViewController 类，包含一组视图控制器。

4. 应用程序加载完成后，UITabBarController 实例的当前视图将被加载，这一点在 TabBarApplicationAppDelegate.m 文件中很明显：

```objc
#import "TabBarApplicationAppDelegate.h"
@implementation TabBarApplicationAppDelegate
@synthesize window;
@synthesize tabBarController;
- (void)applicationDidFinishLaunching:(UIApplication *)application {
    // Add the tab bar controller's current view as a subview of the window
    [window addSubview:tabBarController.view];
}
```

5. 双击 MainWindow.xib 文件在接口构建器中编辑它。观察视图底部标签栏视图中包含的两个标签栏项视图。

> **注意** 标签栏项实际上由一个视图控制器和一个标签栏项对象组成。

6. 单击标记为 First 的第一个标签栏项（见图 8-4）。在标识检查器窗口中，注意到这是一个视图控制器，并且实现类是 `FirstViewController`。

![](img/aab2d775c46f70cd606f2e58e2521324_216_0.png)

图 8-4

7. 单击第二个标签栏项并查看其标识检查器窗口。注意它指向基础 `UIViewController` 类。现在，查看其属性检查器窗口（见图 8-5）。注意，在这种情况下，它是从另一个 NIB 文件 `SecondView` 加载其视图窗口。

> **注意** 如果您希望用户与第二个视图中的 UI 交互，您应该为其添加一个视图控制器类，以便您可以将其 outlet 和 action 连接到它。您很快就会看到如何做到这一点。

![](img/aab2d775c46f70cd606f2e58e2521324_217_0.png)

8. 返回 Xcode，按 Command-R 在 iPhone 模拟器上运行应用程序（见图 8-6）。现在您可以触摸屏幕底部的标签栏项在两个视图之间切换。

## 工作原理

基本上，标签栏应用程序的魔力在于使用 `UITabBarController` 类。如果您双击 `MainWindow.xib` 文件，您会看到它有一个标签栏控制器项（见图 8-7）。

![](img/aab2d775c46f70cd606f2e58e2521324_217_1.png)

![](img/aab2d775c46f70cd606f2e58e2521324_218_0.png)

图 8-7

标签栏控制器包含一组视图控制器。在这种情况下，其中包含两个视图控制器。UITabBarController 实例中的第一个视图控制器在添加到当前视图时始终显示：

```
- (void)applicationDidFinishLaunching:(UIApplication *)application {
    // Add the tab bar controller's current view as a subview of the window
    [window addSubview:tabBarController.view];
}
```

当用户触摸标签栏项时，每个对应的视图控制器都会被加载以显示其视图。

> **注意** 查看 MainWindow.xib 窗口的另一种方法是将其切换为在列表视图中显示（窗口左上角的第二个按钮）。这样可以快速检查标签栏控制器中包含的视图控制器集合。

## 添加标签栏项目

上一节演示了如何使用 SDK 提供的模板创建标签栏应用程序。默认情况下，应用程序模板仅包含两个标签栏项，因此在本节中，您将了解如何向现有标签栏添加更多标签栏项。

## 试用 — 添加标签栏项目

- 1. 使用同一项目，在接口构建器中，从库中将标签栏项拖放到标签栏视图上（见图 8-8）。

![](img/aab2d775c46f70cd606f2e58e2521324_219_0.png)

**图 8-8**

- 2. 选择新添加的标签栏项并查看其属性检查器窗口。将 Badge 属性设置为 5，将 Identifier 属性设置为 Search。（见图 8-9）。观察标签栏项外观的变化。

> **注意** 单击标签栏项的中心以便选择标签栏项；如果单击外部，则会选择视图控制器。

![](img/aab2d775c46f70cd606f2e58e2521324_220_0.png)

图 8-9

> **注意** Badge 属性是一种巧妙的方式，让您在标签栏项上设置一些数字或其他文本，以便它可以作为快速视觉提示提醒用户某些事情。

- 3. 返回 Xcode，右键单击 Resources 文件夹并选择添加 ⌥ 新文件。单击用户界面类别并选择视图 XIB。将文件命名为 SearchView.xib。
- 4. 在 Xcode 中右键单击 Classes 文件夹并选择添加 ⌥ 新文件。单击 Cocoa Touch Classes 类别并选择 UIViewController 子类。将文件命名为 SearchViewController.m（取消选中“带用户界面 XIB”选项，因为您已在上一步中创建了 XIB 文件）。
- 5. 双击新创建的 SearchView.xib 文件在接口构建器中打开它。向其添加搜索栏视图（见图 8-10）。

14. 就这样！按 Command-R 在 iPhone 模拟器上测试应用程序。您现在可以触摸第三个标签栏项（Search）来查看搜索栏（见图 8-14）。触摸搜索栏会自动显示键盘。输入完成后，触摸键盘上的搜索按钮即可隐藏键盘。

![](img/aab2d775c46f70cd606f2e58e2521324_224_0.png)

图 8-14

## 工作原理

在此示例中，您向标签栏视图添加了标签栏项视图，并将其连接到 XIB 文件及其对应的视图控制器。

添加新的标签栏项视图非常简单：只需从库中拖动标签栏项并将其拖放到标签栏视图中。或者，您可以通过 MainWindow.xib 窗口中标签栏控制器项的属性检查器窗口添加它（见图 8-15）。单击 +（加号）按钮添加新的视图控制器，标签栏视图会自动为您插入新的标签栏项视图。

![](img/aab2d775c46f70cd606f2e58e2521324_225_0.png)

图 8-15

## 以横向模式显示标签栏应用程序

在第 6 章中，您了解到 iPhone 应用程序中的屏幕旋转可以通过重写 shouldAutorotateToInterfaceOrientation: 方法轻松支持。要支持所有屏幕方向，您只需为此方法返回 YES，如下所示：

```
- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)
interfaceOrientation {
    return YES;
}
```

这样做会导致视图自动旋转以支持新的方向。对于标签栏应用程序，情况有点特殊。为了了解它有多不同，请继续对 FirstViewController.m 文件进行以下修改：

```
//---FirstViewController.m---
// (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)
// interfaceOrientation {
//     return YES;
// }
```
