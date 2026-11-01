
![](img/16991b58db5894715c4a443315e06a22_101_0.png)

## 图 3-35

在 MyViewController.h 中，为 Web 视图创建一个 outlet 并将其作为属性公开：

```objc
#import <UIKit/UIKit.h>

@interface MyViewController : UIViewController {
    IBOutlet UIWebView *webView;
}

@property (retain, nonatomic) UIWebView *webView;

@end
```

返回 MyViewController.xib 文件，将 outlet 连接到 Web 视图。为验证连接是否正确建立，请右键单击 File's Owner 项目。你应该会看到图 3-36 所示的连接。

![](img/16991b58db5894715c4a443315e06a22_102_0.png)

## 图 3-36

在 MyViewController.m 文件中编写以下代码，以便在视图加载时在 Web 视图中显示 Apple.com 的网页：

```objc
#import "MyViewController.h"

@implementation MyViewController

@synthesize webView;

// Implement viewDidLoad to do additional setup after loading the view,
// typically from a nib.
- (void)viewDidLoad {
    NSString *strUrl = @"http://www.apple.com";
    //---create an URL object---
    NSURL *url = [NSURL URLWithString:strUrl];

    //---create an URL Request Object---
    NSURLRequest *request = [NSURLRequest requestWithURL:url];

    //---load the request in the UIWebView---
    [webView loadRequest:request];

    [super viewDidLoad];
}
- (void)dealloc {
    [webView release];
    [super dealloc];
}
@end
```

就这样！按 Command-R 在 iPhone 模拟器上测试应用程序。图 3-37 显示模拟器正在显示 Apple 的主页。

## 摘要

在本章中，您已了解 XIB 文件的使用以及 View Controllers 在 iPhone 应用程序中扮演的角色。理解 outlets 和 actions 的使用极其重要，因为它是 iPhone 开发的基石。在整本书中，您会经常遇到它们。

在下一章中，您将学习如何控制虚拟键盘，当用户尝试向应用程序输入数据时该键盘会自动弹出。

![](img/16991b58db5894715c4a443315e06a22_103_0.png)

图 3-37

## 练习

- 1. 使用代码声明并定义一个 UITextField 视图的 outlet。
- 2. 使用代码声明并定义一个 action。

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| 委托文件 | 委托文件包含在应用程序加载/卸载期间通常执行的代码。 |
| 视图控制器 | 视图控制器管理视图并执行导航和内存管理。 |
| 动作 | 动作是一种方法，可以处理 View 窗口中视图引发的事件（例如，当按钮被点击时等）。 |
| 出口 | 出口允许您的代码以编程方式引用 View 窗口上的视图。 |
| 使用代码添加 outlet | 使用 `IBOutlet` 关键字：<br>`IBOutlet UITextField *nameTextField;` |
| 使用代码添加 action | 使用 `IBAction` 关键字：<br>`- (IBAction)btnClicked:(id)sender;` |
| 连接动作 | 要链接动作，您始终从 View 窗口中的视图拖动到 File's Owner 项目上。 |
| 连接出口 | 要链接出口，您始终从 File's Owner 项目拖动到 View 窗口中所需的视图上。 |

- 3. 按 Command-R 在 iPhone 模拟器上测试应用程序。加载应用程序时，您会看到如图 4-2 所示的警报视图。

![](img/16991b58db5894715c4a443315e06a22_109_0.png)

- 4. 返回 Xcode，修改 otherButtonTitles 参数，将其设置为加粗显示的值：

```objc
UIAlertView *alert = [[UIAlertView alloc]
initWithTitle:@"Hello"
message:@"This is an alert view"
delegate:self
cancelButtonTitle:@"OK"
otherButtonTitles:@"Option 1",
@"Option 2", nil];
```

- 5. 在 UsingViewsViewController.h 文件中，添加以下加粗显示的行：

```objc
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController
<UIAlertViewDelegate> {
}

@end
```

- 6. 在 UsingViewsViewController.m 文件中，添加以下方法：

```objc
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:
(NSInteger)buttonIndex {

NSLog([NSString stringWithFormat:@"%d", buttonIndex]);
}
```

![](img/16991b58db5894715c4a443315e06a22_109_1.png)

- 7. 按 Command-R 在 iPhone 模拟器中测试应用程序。请注意，除了 OK 按钮外，现在还有两个额外的按钮（参见图 4-3）。
- 8. 点击任意一个按钮 — Option 1、Option 2 或 OK。
- 9. 在 Xcode 中，按 Command-Shift-R 查看调试器控制台窗口。观察打印的值。您可以多次重新运行应用程序并点击不同的按钮以观察打印的值。
- 10. 您应该观察到为每个被点击的按钮打印的值：
    - OK 按钮 — 0
    - Option 1 — 1
    - Option 2 — 2

## 其工作原理

要使用 UIAlertView，您首先实例化它并使用各种参数对其进行初始化：

```objc
UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Hello"
message:@"This is an alert view"
delegate:self
cancelButtonTitle:@"OK"
otherButtonTitles:nil];
```

第一个参数是警报视图的标题，您将其设置为 "Hello"。第二个是消息，您将其设置为 "This is an alert view"。第三个是委托，您需要将其设置为将处理 UIAlertView 对象触发的事件的对象。在本例中，您将其设置为 self，这意味着事件处理程序将在当前类中实现，即视图控制器。cancelButtonTitle 参数显示一个按钮以 dismiss 您的警报视图。最后，otherButtonTitles 参数允许您在需要时显示额外的按钮。如果不需要额外的按钮，只需将其设置为 nil 即可。

要以模态方式显示警报视图，请使用 show 方法：

```objc
[alert show];
```

对于警报视图的简单使用，您实际上不需要处理它触发的事件。点击 OK 按钮（在 cancelButtonTitle 参数中设置） simply dismisses 警报视图。

如果您想要多个按钮，则需要设置 otherButtonTitles 参数，如下所示：

```objc
UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Hello"
message:@"This is an alert view"
delegate:self
cancelButtonTitle:@"OK"
otherButtonTitles:@"Option 1", @"Option 2", nil];
```

请注意，您需要使用 nil 结束 otherButtonTitles 参数，否则将发生运行时错误。

现在您有三个按钮，您需要能够知道用户按下了哪个按钮——特别是 Option 1 还是 Option 2 是否被按下。为此，您需要处理 UIAlertView 类引发的事件。您通过确保您的视图控制器符合 UIAlertViewDelegate 协议来实现这一点：

```objc
@interface UsingViewsViewController : UIViewController <UIAlertViewDelegate> {
    //...
}
```

UIAlertViewDelegate 协议包含与警报视图关联的多个方法。要知道用户点击了哪个按钮，您需要实现 alertView:clickedButtonAtIndex: 方法：

```objc
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:
(NSInteger)buttonIndex {
    NSLog([NSString stringWithFormat:@"%d", buttonIndex]);
}
```

被点击按钮的索引将通过 clickedButtonAtIndex: 参数传入。

> **NOTE** 请参阅附录 D，了解 Objective-C 中协议概念的讨论。

## 使用操作表

虽然 Alert 视图可以显示多个按钮，但其主要用途仍然是作为在发生某事时提醒用户的工具。如果您需要显示一条带有多个供用户选择的选项的消息，则应使用操作表而不是 Alert 视图。*操作表* 显示一组按钮，用户可在其中选择一个。它始终从屏幕底部出现并锚定在屏幕两侧，提示用户操作表的详细信息与当前应用程序相关联。操作表使用的一个好例子是您在 Safari 中点击 "+" 按钮时。点击 "+" 按钮会显示一个操作表，您可以在其中添加书签、将当前页面添加到主屏幕，或邮件发送当前页面的链接。以下试一试将让您使用操作表。

## 试一试 使用操作表

- 1. 使用上一节创建的同一项目，按如下方式修改 `viewDidLoad` 方法（在 `UsingViewsViewController.m` 文件中）：

```objc
- (void)viewDidLoad {

    UIActionSheet *action = [[UIActionSheet alloc]
        initWithTitle:@"Title of Action Sheet"
        delegate:self
        cancelButtonTitle:@"OK"
        destructiveButtonTitle:@"Delete Message"
        otherButtonTitles:@"Option 1", @"Option 2", nil];
    [action showInView:self.view];
    [action release];
    [super viewDidLoad];
}
```

- 2. 在 `UsingViewsViewController.h` 文件中，添加以下加粗显示的语句：

```objc
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController
<UIActionSheetDelegate> {
}

@end
```
