
## 基于窗口的应用程序模板

在本节中，您将发现使用 iPhone SDK 可以创建的另一种应用程序模板：基于窗口的应用程序模板。与基于视图的应用程序模板不同，基于窗口的应用程序模板默认不包含视图控制器。相反，它仅提供 iPad 应用程序的骨架，其余部分留给开发者——您需要添加自己的视图及其各自的视图控制器。正因为如此，基于窗口的应用程序为您提供了一个很好的方式来了解视图控制器的工作原理，并体会连接视图控制器和 XIB 文件所需的所有工作。当您了解视图控制器的工作原理后，您将能够创建更复杂的应用程序。

首先，执行以下试一试来编写一个基于窗口的应用程序，然后逐步向其添加视图控制器。

## 试一试  创建基于窗口的应用程序

*代码文件 windowBasedApp.zip 可在 Wrox.com 上下载*

- 1. 使用 Xcode 创建一个基于窗口的应用程序项目，并将其命名为 `windowBasedApp`。观察为此项目类型创建的文件（参见图 4-11）。除了通常的支持文件外，请注意只有一个 XIB 文件（`MainWindow.xib`）和两个委托文件（`windowBasedAppAppDelegate.h` 和 `windowBasedAppAppDelegate.m`）。
- 2. 按 Command-R 测试应用程序。在 iPhone 模拟器上显示一个空屏幕。这是因为基于窗口的应用程序模板仅提供简单 iPad 应用程序的骨架结构——只有一个窗口和应用程序委托。
- 3. 在 Xcode 中，双击 `MainWindow.xib` 在 Interface Builder 中编辑它。请注意，`MainWindow.xib` 窗口中有四项（参见图 4-12）：
  - File's Owner
  - First Responder
  - Window
  - Window Based App App Delegate
- 4. 从库窗口拖放一个视图控制器项到 `MainWindow.xib` 窗口（参见图 4-13）。您将在下一步中将此视图控制器项连接到您将添加到项目中的视图。

![](img/744c5ec15e15ca7891c98be71dc25d13_124_0.png)

![](img/744c5ec15e15ca7891c98be71dc25d13_124_1.png)

- 11. 在 windowBasedAppAppDelegate.m 文件中，插入以下以粗体显示的代码行：

```
#import "windowBasedAppAppDelegate.h"
#import "HelloWorldViewController.h"

@implementation windowBasedAppAppDelegate

@synthesize window;

//---synthesize the property---
//@synthesize viewController;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch
    //---add the new view to the current window---
    [window addSubview:viewController.view];
    
    [window makeKeyAndVisible];
    
    return YES;
}

- (void)dealloc {
    [viewController release];
    [window release];
    [super dealloc];
}

@end
```

- 12. 在 MainWindow.xib 窗口中，Control-单击并拖动 Window Based App App Delegate 项到 Hello World View Controller 项（参见图 4-20）。选择 viewController。这将把窗口与视图控制器关联起来。

- 13. 就这样！按 Command-R 在 iPhone 模拟器上测试应用程序。按钮出现在应用程序主屏幕上（参见图 4-21）。

![](img/744c5ec15e15ca7891c98be71dc25d13_129_0.png)

图 4-20

![](img/744c5ec15e15ca7891c98be71dc25d13_130_0.png)

图 4-21

## 工作原理

当您使用基于窗口的应用程序模板创建 iPad 项目时，Xcode 只为您提供项目中的最少项目——一个 MainWindow.xib 文件和应用程序委托。您应该添加自己的视图控制器和视图。

在前面的练习中，您首先向 MainWindow.xib 窗口添加了一个视图控制器项。然后您添加了 UIViewController 类的一个实例（您将其命名为 HelloWorldViewController），以便将其连接到您刚刚添加的视图控制器。此控制器类包含您将编写的代码，用于处理视图与用户之间的交互。

当应用程序完成启动后，您使用 UIWindow 实例的 addSubview: 方法将由 HelloWorldViewController 对象表示的视图添加到窗口中，使其可见：

```
[window addSubview:viewController.view];
```

## 以编程方式添加视图控制器和视图

另一种常用的技术是在运行时以编程方式创建视图，而不使用 Interface Builder。这提供了很大的灵活性，尤其是在编写游戏时，应用程序的 UI 不断变化。

在下面的试一试中，您将学习如何使用 UIViewController 类的实例创建视图，然后以编程方式向其添加视图。

## 试一试  以编程方式添加视图控制器和视图

- 1. 使用 windowBasedApp 项目，在 Xcode 中右键单击 Classes 组并添加新文件。选择 UIViewController 子类项并将其命名为 MySecondViewController。确保未选中“With XIB for user interface”复选框。Xcode 现在应如 图 4-22 所示。

![](img/744c5ec15e15ca7891c98be71dc25d13_131_0.png)

图 4-22

- 2. 在 windowBasedAppAppDelegate.m 文件中，添加以下粗体代码：

```
#import "windowBasedAppAppDelegate.h"
#import "HelloWorldViewController.h"

#import "MySecondViewController.h"

@implementation windowBasedAppAppDelegate

@synthesize window;
@synthesize viewController;

//---create an instance of the second view controller---
MySecondViewController *mySecondViewController;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    //---instantiate the second view controller---
    mySecondViewController = [[MySecondViewController alloc] initWithNibName:nil bundle:nil];
    //---add the view from the second view controller---
    [window addSubview:mySecondViewController.view];
    //---comment this out so that it doesn't load the viewController---
    //[window addSubview:viewController.view];
    [window makeKeyAndVisible];
    return YES;
}

- (void)dealloc {
    [mySecondViewController release];
    [viewController release];
    [window release];
    [super dealloc];
}
```

- 3. 在 MySecondViewController.h 文件中，插入以下粗体代码行：

```
#import <UIKit/UIKit.h>

@interface MySecondViewController : UIViewController {
    //---create two outlets - label and button---
    UILabel *label;
    UIButton *button;
}

//---expose the outlets as properties---
@property (nonatomic, retain) UILabel *label;
@property (nonatomic, retain) UIButton *button;

@end
```

- 4. 在 MySecondViewController.m 文件中，添加 viewDidLoad() 方法并修改 dealloc 方法：

```
@synthesize label, button;

- (void)viewDidLoad {
    //---create a CGRect for the positioning---
    CGRect frame = CGRectMake(230, 10, 300, 50);
    //---create a Label view---
    label = [[UILabel alloc] initWithFrame:frame];
    label.textAlignment = UITextAlignmentCenter;
    label.font = [UIFont fontWithName:@"Verdana" size:20];
    label.text = @"This is a label";

    //---create a Button view---
    frame = CGRectMake(230, 100, 300, 50);
    button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
    button.frame = frame;
    [button setTitle:@"OK" forState:UIControlStateNormal];
    button.backgroundColor = [UIColor clearColor];

    //---add the views to the View window---
    [self.view addSubview:label];
    [self.view addSubview:button];
    [super viewDidLoad];
}

- (void)dealloc {
    [label release];
    [button release];
    [super dealloc];
}
```

- 5. 按 Command-R 在 iPhone 模拟器上测试应用程序。标签和按钮视图出现在应用程序主屏幕上（参见图 4-23）。

## 工作原理

与之前的示例不同，在之前的示例中您向项目添加了视图控制器项、UIViewController 类的实例和 XIB 文件，此示例仅创建 UIViewController 类的实例并以编程方式将视图添加到主视图窗口。

在应用程序委托中，应用程序完成启动后，您创建已创建的 UIViewController 类的实例：

//---instantiate the second view controller---
mySecondViewController = [[MySecondViewController alloc]
initWithNibName:nil
bundle:nil];

您不需要 XIB 文件，因为您将使用的各种视图将以编程方式添加。因此 initWithNibName: 参数可以设置为 nil。

要加载由 UIViewController 类实例表示的视图窗口，您使用 UIWindow 实例的 addSubview: 方法：

//---add the view from the second view controller---
[window addSubview:mySecondViewController.view];
