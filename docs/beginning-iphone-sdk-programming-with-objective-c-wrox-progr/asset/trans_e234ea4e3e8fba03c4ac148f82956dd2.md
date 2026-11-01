
### 试一试 显示一系列图像

*代码文件 [Animations2.zip] 可在 Wrox.com 下载*

- 1. 使用 Xcode，创建一个新的基于视图的应用程序项目并将其命名为 Animations2。
- 2. 通过将它们拖放到 Xcode 中的 Resources 文件夹，将一系列图像添加到 Resources 文件夹。当添加对话框出现时，选择“如果需要则将项目复制到目标组的目录”复选框，以便将每张图像的副本复制到项目中。图 15-9 显示了添加的图像。
- 3. 在 Animations2ViewController.m 文件中，添加以下以粗体显示的语句：

```
- (void)viewDidLoad {
    NSArray *images = [NSArray
    arrayWithObjects:
                    [UIImage imageNamed:@"MacSE.jpeg"],
                    [UIImage imageNamed:@"imac.jpeg"],
                    [UIImage imageNamed:@"MacPlus.jpeg"],
                    [UIImage imageNamed:@"imac_old.jpeg"],
                    [UIImage imageNamed:@"Mac8100.jpeg"],
    nil];

    CGRect frame = CGRectMake(0,0,320,460);
    UIImageView *imageView = [[UIImageView alloc] initWithFrame:frame];
    imageView.animationImages = images;
    imageView.contentMode = UIViewContentModeScaleAspectFit;
    imageView.animationDuration = 3;    //---seconds to complete one set
                                        // of animation---
    imageView.animationRepeatCount = 0; //---continuous---
    
    [imageView startAnimating];
    
    [self.view addSubview:imageView];
    [imageView release];
    [super viewDidLoad];
}
```

![](img/16991b58db5894715c4a443315e06a22_380_0.png)

图 15-9

## 16 访问内置应用程序

### 本章你将学到什么

- 如何在应用程序内部发送电子邮件
- 如何在应用程序内部调用 Safari
- 如何在应用程序内部调用电话
- 如何在应用程序内部发送短信
- 如何访问相机和照片库
- 如何访问通讯录应用程序
- 如何从通讯录应用程序添加和删除联系人信息

iPhone 附带了许多内置应用程序，使其成为有史以来最受欢迎的移动设备之一。其中一些应用程序有通讯录、邮件、电话、Safari、短信和日历。这些应用程序执行了您对一部手机所期望的大多数任务。作为 iPhone 开发者，您还可以使用 iPhone SDK 提供的各种 API 从应用程序内部以编程方式调用这些应用程序。

在本章中，您将学习如何调用随 iPhone 一起捆绑的某些内置应用程序，以及如何从 iPhone 应用程序内部与它们进行交互。

### 发送电子邮件

发送电子邮件是 iPhone 用户执行的众多任务之一。iPhone 上的电子邮件发送是通过内置的 Mail 应用程序完成的，该应用程序是一个功能丰富的 HTML 邮件客户端，支持 POP3、IMAP、Exchange 电子邮件系统以及大多数基于网络的电子邮件，如 Yahoo! 和 Gmail。

有时您需要在 iPhone 应用程序中发送电子邮件。一个很好的例子是在应用程序中嵌入一个反馈按钮，用户可以点击它直接向您发送反馈。您有两种以编程方式发送电子邮件的方法：

- 构建自己的电子邮件客户端并实现与电子邮件服务器通信所需的所有必要协议
- 调用内置的 Mail 应用程序并让它为您发送电子邮件

除非您精通网络通信并熟悉所有电子邮件协议，否则最合理的选择是选择第二个选项——调用 Mail 应用程序来完成工作。下面的“试一试”向您展示了如何操作（您需要下载此处指出的代码文件来完成此示例）。

### 试一试 使用 Mail 应用程序发送电子邮件

*代码文件 [Emails.zip] 可在 Wrox.com 下载*

- 1. 使用 Xcode，创建一个基于视图的应用程序项目并将其命名为 Emails。
- 2. 双击 EmailViewController.xib 文件以在 Interface Builder 中编辑它。
- 3. 使用以下视图填充 View 窗口（见图 16-1）：
  - Label
  - TextField
  - Button

![](img/16991b58db5894715c4a443315e06a22_385_0.png)

图 16-1

- 4. 将以下以粗体显示的语句插入 EmailsViewController.h 文件中：

```
#import <UIKit/UIKit.h>

@interface EmailsViewController : UIViewController {
    IBOutlet UITextField *to;
    IBOutlet UITextField *subject;
    IBOutlet UITextField *body;
}

@property (nonatomic, retain) UITextField *to;
@property (nonatomic, retain) UITextField *subject;
@property (nonatomic, retain) UITextField *body;

- (IBAction) btnSend: (id) sender;

@end
```

- 5. 返回 Interface Builder，Control-click 并拖动 File's Owner 项目到三个 TextField 视图中的每一个，并分别选择 to、subject 和 body。
- 6. Control-click 并拖动 Button 视图到 File's Owner 项目并选择 btnSend:。
- 7. 将以下以粗体显示的代码插入 EmailsViewController.m 文件中：

```
#import "EmailsViewController.h"

@implementation EmailsViewController
@synthesize to, subject, body;

- (void) sendEmailTo:(NSString *) toStr
withSubject: (NSString *) subjectStr
withBody: (NSString *) bodyStr {

    NSString *emailString = [[NSString alloc]
    initWithFormat:@"mailto:%@?subject=%@&body=%@",
    [toStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding],
    [subjectStr
    stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding],
    [bodyStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding]];

    [[UIApplication sharedApplication] openURL:[NSURL URLWithString:emailString]];

    [emailString release];
}

- (IBAction) btnSend: (id) sender{
    [self sendEmailTo:to.text withSubject:subject.text withBody:body.text];
}

- (void)dealloc {
    [to release];
    [subject release];
    [body release];
    [super dealloc];
}
```

- 8. 按 Command-R 在真实 iPhone 上测试应用程序。图 16-2 显示了应用程序的运行情况。在用必要的信息填充 TextField 视图后，点击发送按钮以调用 Mail 应用程序并用您在应用程序中输入的所有信息填充它。点击 Mail 中的发送按钮会发送电子邮件。

> **NOTE** 请记住，此示例仅在真实设备上有效。在 iPhone 模拟器上测试将不起作用。附录 D 讨论了如何为测试准备您的 iPhone。

![](img/16991b58db5894715c4a443315e06a22_387_0.png)

图 16-2

### 它是如何工作的

调用 Mail 应用程序的魔力在于您在 sendEmailTo:withSubject:withBody: 方法中创建的字符串：

```
NSString *emailString = [[NSString alloc]
initWithFormat:@"mailto:%@?subject=%@&body=%@",
[toStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding],
[subjectStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding],
[bodyStr stringByAddingPercentEscapesUsingEncoding:NSASCIIStringEncoding]];
```

基本上，这是一个带有 mailto: 协议指示的 URL 字符串。各种参数，如 to、subject 和 body，被插入到字符串中。请注意，您使用 NSString 类的 stringByAddingPercentEscapesUsingEncoding: 方法对各种参数进行编码，使用正确的百分号转义，以便最终结果是一个有效的 URL 字符串。

要调用 Mail 应用程序，只需调用 sharedApplication 方法返回单例应用程序实例，然后使用 openURL: 方法调用 Mail 应用程序：

```
[[UIApplication sharedApplication] openURL:[NSURL URLWithString:emailString]];
[emailString release];
```

### 调用 Safari

如果您想在 iPhone 上调用 Safari Web 浏览器，您也可以使用 URL 字符串，然后使用应用程序实例的 openURL: 方法，如下所示：

```
[[UIApplication sharedApplication]
    openURL:[NSURL URLWithString: @"http://www.apple.com"]];
```

前面的代码片段调用 Safari 以打开 www.apple.com 页面（见图 16-3）。

![](img/16991b58db5894715c4a443315e06a22_388_0.png)

### 调用电话

要使用 iPhone 的拨号器拨打电话，请使用以下 URL 字符串：

```
[[UIApplication sharedApplication]
    openURL:[NSURL URLWithString:@"tel:1234567890*"]];
```

前面的语句使用指定的电话号码调用 iPhone 的拨号器。

> NOTE 请注意，前面的语句仅适用于 iPhone 而不适用于 iPod Touch，因为 iPod Touch 没有电话功能。此外，您需要真实设备来测试此功能；代码对 iPhone 模拟器没有影响。附录 E 讨论了如何为测试准备您的 iPhone。

### 调用短信

您也可以使用 URL 字符串通过短信应用程序发送短信消息：

```
[[UIApplication sharedApplication]
    openURL:[NSURL URLWithString:
    @"sms:96924065*"]];
```

前面的语句调用短信应用程序（见图 16-4）。

![](img/16991b58db5894715c4a443315e06a22_388_1.png)
