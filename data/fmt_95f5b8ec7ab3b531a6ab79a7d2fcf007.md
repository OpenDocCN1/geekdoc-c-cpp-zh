
换句话说，如果设备是 iPhone，那么我们就创建一个 `AssignmentViewController` 的新实例，配置它，并像以前一样将其推入导航栈。相反，如果我们在 iPad 上运行，则使用 `AssignmentViewController` 的现有实例，配置它，并使用这些信息重新加载网页浏览器。

## 2.4 使用子类针对不同的设备

我们的代码开始充满了对我们处于什么设备上的检查。请记住，维护代码花费的时间将远大于你编写代码花费的时间。在大型项目中，由于这些散落在各处的语句，在 iPhone 或 iPad 上追踪其行为将变得非常困难。

这些建议中并没有针对 iPad 的特定内容。当你认为代码中充满了条件判断时，使用你传统的工具箱技巧来拆分方法和类，以便代码的意图更加清晰。

例如，更健壮的方法是将类文件拆分为三个不同的类别。所有在两个平台之间共享的代码都放在共享文件中。你将为需要针对 iPhone 或 iPad 定制的代码创建子类。到下一节结束，我们的源代码将包含以下文件：⁵

![](img/06d76a71c379bfa5e6891245aa6bb22d_42_0.png)

首先，考虑 `RootViewController`。我们针对设备自定义其行为的唯一地方是在表格视图代理的 `tableView:didSelectRowAtIndexPath:` 方法的实现中。我们将从 `RootViewController` 类中删除此方法并创建两个实现它的子类。

创建一个名为 `RootViewController_Pad` 的 `RootViewController` 子类。头文件非常空闲。

- ⁵ 你可以添加三个名为 Shared、iPad 和 iPhone 的新分组，并将相应的源文件移动那里。

```
SplitVC/DailyShot66/Classes/RootViewController_Pad.h
```

```objc
#import "RootViewController.h"
```

```objc
@interface RootViewController_Pad : RootViewController {
}
@end
```

实现文件也没有什么内容。我们实现 iPad 特有的代码。你可以从 `RootViewController.m` 的 `tableView:didSelectRowAtIndexPath:` 方法复制并粘贴相应的行。

```
SplitVC/DailyShot66/Classes/RootViewController_Pad.m
```

```objc
#import "RootViewController_Pad.h"
#import "Assignments.h"
#import "AssignmentViewController.h"
```

```objc
@implementation RootViewController_Pad

-(void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
    self.assignmentVC.assignmentNumber = self.assignments.AtIndex:indexPathrow;
    [self.assignment.SelectedPage];
}

@end
```

我们将按照相同的模式处理 iPhone 情况。创建一个名为 `RootViewController_Phone` 的第二个 `RootViewController` 子类。

```
SplitVC/DailyShot66/Classes/RootViewController_Phone.h
```

```objc
#import "RootViewController.h"
```

```objc
@interface RootViewController_Phone : RootViewController {
}
@end
```

它的方法实现包含了 iPhone 特有的行为。再次从 `RootViewController.m` 的 `tableView:didSelectRowAtIndexPath:` 方法复制并粘贴相应的行。

```objc
@implementation RootViewController_Phone
```

```objc
(void)tableView:(UITableView *)tableView
    didSelectRowAtIndexPath:(NSIndexPath*)indexPath {
        AssignmentViewController *detailViewController = 
            [[AssignmentViewController alloc] 
            WithName:@"AssignmentViewController" bundle:nil];
        detailViewController.assignmentNumber = 
            self.assignments objectAtIndex:indexPath.row;
        [self.navigationController pushViewController:detailViewController
            animated:YES];

        [detailViewController release];
}
end
```

我们使用 `RootViewController` 的子类轻松地拆分了设备特定的行为。我们从 `RootViewController.m` 中删除了 `tableView:didSelectRowAtIndexPath:` 的实现。父类拥有所有表格视图的数据源方法，我们将设备特定的代理方法移动到了子类中。

遗憾的是，我们应用程序的其他部分对这些新子类一无所知。让我们将应用程序代理分为 iPhone 和 iPad 类，并调用相应的 `RootViewController`。

## 2.5 分离应用程序代理

我们需要进行一些更改，以便使用相应的 `RootViewController` 子类。我们将为每个平台创建应用程序代理。我们将两个设备通用的代码放在基类 `DailyShootAppDelegate` 中。这是它的头文件：

```
ViewController/DailyShotMock/Classes/DailyShootAppDelegate.h
```

```objc
#import <UIKit/UIKit.h>

@interface DailyShootAppDelegate : NSObject <UIApplicationDelegate> {
}
@property (nonatomic, retain) UIWindow *window;
@property (nonatomic, retain) UINavigationController *navigationController;

@end
```

实现文件删除了对目标设备的检查。我们将推迟将初始视图添加到子类。

- 4. 如果你收到编译器警告或错误，请检查你是否添加了 @class 声明和导入，并且声明了 `loadSelectedPage` 方法。

这里是 DailyShootAppDelegate.m：

```
SplitVC/DailyShoot6/Classes/DailyShootAppDelegate.m
```

```objc
#import "DailyShootAppDelegate.h"

@implementation DailyShootAppDelegate

@synthesize window, navigationController;

- (BOOL)application:(UIApplication*)application
    didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {

    [self.window makeKeyAndVisible];

    return YES;
}

- (void)dealloc {
    [navigationController release], navigationController = nil;
    [window release], window = nil;
    [super dealloc];
}

@end
```

创建一个带有此头文件的 `DailyShootAppDelegate_Phone` 类：

```
SplitVC/DailyShoot6/Classes/DailyShootAppDelegate_Phone.h
```

```objc
#import <UIKit/UIKit.h>
#import "DailyShootAppDelegate.h"

@interface DailyShootAppDelegate_Phone : DailyShootAppDelegate {
}
@end
```

在 iPhone 的情况下，我们将导航控制器视图作为顶层视图，并调用父类的 `application:didFinishLaunchingWithOptions:` 方法。

```
SplitVC/DailyShoot6/Classes/DailyShootAppDelegate_Phone.m
```

```objc
#import "DailyShootAppDelegate.h"

@implementation DailyShootAppDelegate_Phone

- (BOOL)application:(UIApplication*)application
    didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {

    [self.window addSubview:self.navigationController.view];

    return [super application:application
        didFinishLaunchingWithOptions:launchOptions];
}

@end
```

同样，创建一个带有以下头文件的 `DailyShootAppDelegate_Pad` 类：

```
SplitVC/DailyShoot6/Classes/DailyShootAppDelegate_Pad.h
```

```objc
#import <UIKit/UIKit.h>
#import "DailyShootAppDelegate.h"

@interface DailyShootAppDelegate_Pad : DailyShootAppDelegate {
}
@property (nonatomic, retain) IBOutlet UISplitViewController *splitVC;
@end
```

我们需要在这个子类中为分屏视图控制器添加一个属性。

在实现中，我们将分屏视图控制器的视图作为顶层视图，并在 `dealloc` 方法中清理对象。

```
SplitVC/DailyShoot6/Classes/DailyShootAppDelegate_Pad.m
```

```objc
#import "DailyShootAppDelegate_Pad.h"

@implementation DailyShootAppDelegate_Pad

@synthesize splitVC;

- (BOOL)application:(UIApplication*)application
    didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {
    [self.window addSubview:splitVC.view];
    return [super application:application
        didFinishLaunchingWithOptions:launchOptions];
}

- (void)dealloc {
    [splitVC release];
    splitVC = nil;
    [super dealloc];
}

@end
```

我们几乎已经完成了。我们需要对 nib 文件进行一些细小的调整。在 IB 中打开 `MainWindow.xib` 文件，使用身份检查器（Identity Inspector）将 `DailyShootAppDelegate` 对象的类型更改为 `DailyShootAppDelegate_Phone`，并将 `RootViewController` 对象的类型更改为 `RootViewController_Phone`。

| Name | Type |
|---|---|
| File's Owner | UIApplication |
| First Responder | UIResponder |
| Daily Shoot App Delegate Phone | DailyShootAppDelegate_Phone |
| Window | UIWindow |
| Navigation Controller | UINavigationController |
| Navigation Bar | UINavigationBar |
| Root View Controller | RootViewController_Phone |
| Navigation Item | UINavigationItem |

同样，在 Interface Builder 中打开 `MainWindow-iPad.xib` 文件，再次使用身份检查器将 `DailyShootAppDelegate` 对象的类型更改为 `DailyShootAppDelegate_Pad`。

| Name | Type |
|---|---|
| File's Owner | UIApplication |
| First Responder | UIResponder |
| Daily Shoot App Delegate | DailyShootAppDelegate_Pad |
| Window | UIWindow |
| Split View Controller | UISplitViewController |
| Navigation Controller | UINavigationController |
| Navigation Bar | UINavigationBar |
| RootViewController_Pad (Root Vi...) | RootViewController_Pad |
| Navigation Item (Root View Co...) | UIBarButtonItem |
| Assignment View Controller | AssignmentViewController |

保存所有更改，编译并运行，一切都应该像以前一样运行。

哇！为了替换两个简单的 `if` 语句，感觉步骤有很多步骤。但另一方面，你的代码现在更具可读性和灵活性。你可能也发现，实现这些更改花费了很小的时间——只是当我们这些页面上明确说明它们时，看起来要做很多工作。

## 2.6 在详情视图（Detail View）中添加工具栏

接下来，让我们在 iPad 版本中由 `AssignmentViewController` 管理的视图顶部添加一个工具栏，但在 iPhone 版本中不添加。我们很快就会在 iPad 版本的竖屏模式下需要工具栏，将其也包含在横屏版本中使其看起来更整洁。我们在 iPhone 版本中已经有了导航栏，所以我们想确保不在那里添加额外的工具栏。

我们将创建一个 iPad 版本的 `AssignmentViewController` 类以及相应的 nib。选择 iPad 组，创建一个 `UIViewController` 子类的新文件。确保勾选了目标为 iPad 和创建 XIB 的选项框。将新类命名为 `AssignmentViewController_Pad`。

### 在详情视图中添加工具栏

在 `AssignmentViewController_Pad` 类中添加一个类型为 `UIToolbar` 的名为 `toolbar` 的属性，并将其标记为 outlet。将父类从通用的 `UIViewController` 更改为 `AssignmentViewController`。

```
SplitVC/DailyShoots/Classes/AssignmentViewController_Pad.h
```

```objc
#import "AssignmentViewController.h"

@interface AssignmentViewController_Pad : AssignmentViewController {
}
@property (nonatomic, retain) IBOutlet UIToolbar *toolbar;
@end
```

打开 `AssignmentViewController_Pad` nib 文件。在视图顶部放置一个工具栏，并用 `UIWebView` 填充其余部分。移除工具栏上的按钮。我们稍后会创建自己的按钮。在 web view 中选择“自适应比例”（Scales to Fit）。从 File's Owner 连接这些元素。现在我们为 `AssignmentViewController_Pad` 类编写实现：

```
SplitVC/DailyShoots/Classes/AssignmentViewController_Pad.m
```

```objc
#import "AssignmentViewController_Pad.h"

@implementation AssignmentViewController_Pad

- (BOOL)shouldAutorotateToInterfaceOrientation:(UIInterfaceOrientation)interfaceOrientation {
    return YES;
}

- (void)dealloc {
    [toolbar release];
    toolbar = nil;
    [super dealloc];
}

@end
```
