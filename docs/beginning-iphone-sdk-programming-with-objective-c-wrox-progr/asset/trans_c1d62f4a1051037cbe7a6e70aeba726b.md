
![](img/16991b58db5894715c4a443315e06a22_192_0.png)

图7-1

![](img/16991b58db5894715c4a443315e06a22_192_1.png)

图7-2

![](img/16991b58db5894715c4a443315e06a22_194_0.png)

图7-4

6. 在Xcode中右键单击Resources组，然后添加一个新文件。选择View XIB项并将其命名为MyView.xib。此时Xcode应如图7-5所示。

![](img/16991b58db5894715c4a443315e06a22_194_1.png)

图7-5

7. 回到Interface Builder中，在MainWindow.xib窗口中选择View Controller项，并查看其标识检查器窗口。在类下拉列表中选择MyViewController（参见图7-6）。现在视图控制器的名称将更改为My View Controller。

![](img/16991b58db5894715c4a443315e06a22_195_0.png)

图7-6

8. 查看My View Controller的属性检查器窗口，在NIB Name下拉列表中选择MyView（参见图7-7）。

![](img/16991b58db5894715c4a443315e06a22_195_1.png)

图7-7

```objc
#import <UIKit/UIKit.h>

@class MyViewController;

@interface WinBasedAppAppDelegate : NSObject <UIApplicationDelegate> {
    UIWindow *window;

    //---create an instance of the view controller---
    MyViewController *myViewController;
}

@property (nonatomic, retain) IBOutlet UIWindow *window;

//---expose the view controller as a property---
@property (nonatomic, retain) IBOutlet MyViewController *myViewController;

@end
```

在WinBasedAppAppDelegate.m文件中，插入以下以粗体显示的代码行：

```objc
#import "WinBasedAppAppDelegate.h"

#import "MyViewController.h"

@implementation WinBasedAppAppDelegate

@synthesize window;

//---synthesize the property---
@synthesize myViewController;

- (void)applicationDidFinishLaunching:(UIApplication *)application {
    // Override point for customization after application launch
    //---add the new view to the current window---
    [window addSubview:myViewController.view];
    [window makeKeyAndVisible];
}

- (void)dealloc {
    [myViewController release];
    [window release];
    [super dealloc];
}

@end
```

13. 在MainWindow.xib窗口中，按住Control键单击并将Win Based App App Delegate项拖到My View Controller项上（参见图7-10）。选择myViewController。这将把窗口与视图控制器关联起来。

![](img/16991b58db5894715c4a443315e06a22_198_0.png)

图7-10

![](img/16991b58db5894715c4a443315e06a22_198_1.png)

图7-11

14. 就这样！按Command-R在iPhone模拟器上测试应用程序。现在你应该会看到按钮出现在应用程序的主屏幕上（参见图7-11）。

> 注意 作为练习，你可能想要创建一个操作，在按下按钮时显示一个警报视图。

## 工作原理

当你使用基于窗口的应用程序模板创建iPhone项目时，Xcode只会为你的项目提供最少数量的项——一个MainWindow.xib文件和应用程序委托。你需要自行添加自己的视图控制器和视图。

在上述练习中，你首先向MainWindow.xib窗口添加了一个视图控制器项。然后你添加了一个UIViewController类的实例（你将其命名为MyViewController），以便它可以连接到刚刚添加的视图控制器。这个控制器类包含你将编写的用于处理视图与用户之间交互的代码。

你还在项目中添加了一个XIB文件（MyView.xib），代表Interface Builder中的一个视图。请注意，你需要执行多个步骤，将相关类连接到正确的XIB项和视图控制器项。

当应用程序完成启动后，你使用UIWindow实例的addSubview:方法将myViewController对象所代表的视图添加到窗口中，使其可见：

```objc
[window addSubview:myViewController.view];
```

## 以编程方式添加视图控制器

除了使用Interface Builder添加视图控制器和视图之外，一种常用的技术是在运行时以编程方式创建视图。这提供了很大的灵活性，尤其是在编写应用程序界面不断变化的游戏时。

在下面的动手实践中，你将学习如何使用UIViewController类的实例创建视图，然后以编程方式向其中添加视图。

### 动手实践   以编程方式添加视图控制器

1. 使用同一个项目，在Xcode中右键单击Classes组，然后添加一个新文件。选择UIViewController子类项并将其命名为MySecondViewController。此时Xcode应如图7-12所示。

2. 在WinBasedAppAppDelegate.m文件中，添加以下以粗体显示的代码：

```objc
#import "WinBasedAppAppDelegate.h"
#import "MyViewController.h"

#import "MySecondViewController.h"

@implementation WinBasedAppAppDelegate

@synthesize window;
@synthesize myViewController;

//---create an instance of the second view controller---
MySecondViewController *mySecondViewController;

- (void)applicationDidFinishLaunching:(UIApplication *)application {

    //---instantiate the second view controller---
    mySecondViewController = [[MySecondViewController alloc]
                              initWithNibName:nil
                              bundle:nil];

    //---add the view from the second view controller---
    [window addSubview:mySecondViewController.view];

    //---comment this out so that it doesn't load the myViewController---
    //[window addSubview:myViewController.view];
    [window makeKeyAndVisible];
}

- (void)dealloc {
    [mySecondViewController release];
}
```

![](img/16991b58db5894715c4a443315e06a22_199_0.png)

```objc
button = [UIButton buttonWithType:UIButtonTypeRoundedRect];
button.frame = frame;
[button setTitle:@"OK" forState:UIControlStateNormal];
button.backgroundColor = [UIColor clearColor];

//---add the views to the current View---
[self.view addSubview:label];
[self.view addSubview:button];

[super viewDidLoad];
}
```

## 创建并关联操作

在上一节中，你了解了可以在运行时以编程方式添加视图。在示例中，你还看到了如何向主视图添加标签和按钮视图。然而，你需要处理Button视图引发的事件，以便当用户按下它时，你可以执行一些工作。在第3章中，你学习了如何使用输出口和操作，以及如何使用Interface Builder将你的代码连接到它们。在下面的动手实践中，视图是使用代码创建的，因此你不能使用Interface Builder连接操作和输出口——你也不得不用代码来完成。

### 动手实践  将操作关联到视图

1. 使用上一节中创建的同一个项目，在MySecondViewController.h文件中声明buttonClicked:操作（以粗体显示），如下所示：

```objc
#import <UIKit/UIKit.h>

@interface MySecondViewController : UIViewController {
    UILabel *label;
    UIButton *button;
}

@property (nonatomic, retain) UILabel *label;
@property (nonatomic, retain) UIButton *button;

//---declaring the IBAction---
- (IBAction) buttonClicked: (id) sender;

@end
```

2. 在MySecondViewController.m文件中，为buttonClicked:操作提供实现：

```objc
- (IBAction) buttonClicked: (id) sender{
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Action invoked!"
                                                     message:@"Button clicked!"
```

3. 在MyViewController.m文件中，定义btnClicked:操作，如下所示：

```objc
-(IBAction) btnClicked:(id) sender{
    //---remove the current view; essentially hiding the view---
    [self.view removeFromSuperview];
}
```

4. 双击MyView.xib文件，在Interface Builder中进行编辑。按住Control键单击并将View窗口中的OK按钮拖到MyView.xib窗口的File's Owner项上，然后选择btnClicked:。

5. 回到Xcode，按Command-R测试应用程序。现在，当你单击主视图中的OK按钮时，将进入第二个视图（参见图7-15）。要关闭第二个视图，请按下OK按钮。

![](img/16991b58db5894715c4a443315e06a22_206_0.png)

图7-15

## 工作原理

对于这个示例，你只需使用addSubview:方法将要切换到的视图控制器的视图添加到当前视图：

```objc
//---add the view of the view controller to the current View---
myViewController = [[MyViewController alloc]
    initWithNibName:@"MyView" bundle:nil];
[self.view addSubview:myViewController.view];
```

要关闭视图，使用removeFromSuperview:方法：

```objc
//---remove the current view; essentially hiding the view---
[self.view removeFromSuperview];
```

