
## 添加控制器

您现在已经创建了一个模型（账户）和一个视图（界面）。为了让这两个对象相互通信，您需要在它们之间设置一个控制器类。您可以回到 Xcode 来实现一个控制器，但就目前而言，直接在 Interface Builder 中操作会更简单。

- 1. 在 Interface Builder 中，打开“库”窗口并搜索*对象*。将一个新的*NSObject*拖到项目窗口中。
  图 7-7 显示了新添加的对象。

- 2. 在项目窗口中选中新对象，按下 ⌘+6，并将类名更改为*AccountController*。
  这就是本项目中位于模型和视图之间的控制器类。图 7-8 展示了新的控制器类。

- 3. 在同一个“属性检查器”窗口中，为*AccountController*添加一个输出（outlet）和两个动作（action）。
  *display*输出指向您希望显示当前余额的标签（Label）字段。*withdraw*: 和 *deposit*: 动作对应模型中的相同功能。图 7-9 显示了新定义的输出和动作。

![](img/ea40cad434a338535474e82c1a6ace20_160_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_160_1.png)

![](img/ea40cad434a338535474e82c1a6ace20_161_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_161_1.png)

图 7-8：将新类命名为 AccountController。

![](img/ea40cad434a338535474e82c1a6ace20_161_2.png)

![](img/ea40cad434a338535474e82c1a6ace20_161_3.png)

图 7-9：为 AccountController 添加一个输出和两个动作。

- 4. 通过将 Withdraw 按钮按住 Control 键拖拽到项目窗口中的 AccountController 来连接界面。在出现的小黑色连接列表覆盖层中选择 `withdraw`:。
  图 7-10 显示了连接过程。

- 5. 通过将 Deposit 按钮按住 Control 键拖拽到项目窗口中的 AccountController 来连接界面。在出现的小黑色连接列表覆盖层中选择 `deposit`:。
  图 7-11 展示了连接。

- 6. 将 AccountController 按住 Control 键拖拽到界面中的空标签（Label）字段。在出现的小黑色连接列表覆盖层中选择 `display`。
  图 7-12 展示了该过程。

![](img/ea40cad434a338535474e82c1a6ace20_162_0.png)

图 7-10：将 Withdraw 按钮连接到 AccountController 中的 `withdraw` 动作。

![](img/ea40cad434a338535474e82c1a6ace20_162_1.png)

144 第二部分：即时 Cocoa 与 Objective-C 语言

![](img/ea40cad434a338535474e82c1a6ace20_163_0.png)

图 7-11：将 Deposit 按钮连接到 AccountController 中的 deposit: 动作。

![](img/ea40cad434a338535474e82c1a6ace20_163_1.png)

![](img/ea40cad434a338535474e82c1a6ace20_163_2.png)

图 7-12：将 AccountController 连接到空标签字段，并从选项列表中选择 display。

![](img/ea40cad434a338535474e82c1a6ace20_163_3.png)

- 7. 要创建控制器的文件，请在项目窗口中选择 `AccountController`，然后选择“文件 > 写入类文件”，将文件保存为 `AccountController`，并点击“保存”按钮，如图 7-13 所示。

![](img/ea40cad434a338535474e82c1a6ace20_164_0.png)

图 7-13：写入文件，并将其保存为 `AccountController`。

- 8. 点击“添加”按钮将文件添加到 Xcode 项目中（见图 7-14）。

- 9. 按下 ⌘+Q 退出 Interface Builder，并返回 Xcode。

- 10. 在 Xcode 中，点击 `AccountController.h` 文件以查看其内容，并找到以下行：

```objective-c
@interface AccountController : /* Specify a superclass  
(eg: NSObject or NSView) */ {
```

![](img/ea40cad434a338535474e82c1a6ace20_164_1.png)

图 7-14：将 `AccountController` 添加到银行账户项目中。

- 11. 通过将其更改为以下内容，为 `AccountController` 类指定一个父类：

```objective-c
@interface AccountController : NSObject {
```

- 12. 在接口文件中添加一个 `Account` 实例变量（`account`）：

```objective-c
@interface AccountController : NSObject {
IBOutlet id display;
Account *account;
}
- (IBAction)deposit :(id)sender;
- (IBAction)withdraw : (id) sender ;
@end
```

- 13. 打开 `AccountController.m` 文件，其中已有两个动作：

```objective-c
#import "AccountController.h"
@implementation AccountController
- (IBAction)deposit :(id)sender {
}

- (IBAction)withdraw : (id) sender {
}
@end
```

- 14. 通过添加 `deposit` 和 `withdraw` 的代码来实现这两个动作。同时，在该文件中添加一个 `awakeFromNib` 方法和一个 `dealloc` 方法。

在 awakeFromNib 中，您可以创建一个账户对象并将其分配给账户实例变量（account）。然后，通过将显示值设置为账户余额来更新界面中的显示。

在这个示例中，存款金额将始终为 $20（或您希望的任何面额），取款金额将始终为 $5。

```objective-c
#import "AccountController.h"
@implementation AccountController
-(void)awakeFromNib {
account = [[Account alloc] init];
[display setFloatValue:[account balance]];
}

- (IBAction)deposit :(id) sender {
[account deposit:20.00f];
[display setFloatValue:[account balance]];
}

- (IBAction)withdraw: (id) sender {
  [account withdraw:5.00f];
  [display setFloatValue:[account balance]];
}

- (void)dealloc {
  [account release];
  [super dealloc];
}

@end
```

- 15. 在 Xcode 中，选择“运行 -> 前往”以测试您的工作成果。

图 7-15 显示了已完成的应用程序。

![](img/ea40cad434a338535474e82c1a6ace20_166_0.png)

当运行应用程序时，AccountController 基于 Account 类创建一个新对象，并在视图中显示当前余额，该余额已由 Account 初始化为 100。当您点击“存款”按钮时，您向账户对象发送一条存款消息并更新界面。同样，当您点击“取款”按钮时，代码会向账户对象发送一条取款消息并更新界面。

希望您开始欣赏这种应用程序设计模式的优点。由于模型、视图和控制器都被分离开来，您可以在其他项目中重用这些类。假设您需要创建一个用于跟踪另一种账户类型的新应用程序。您无需重新创建 Account 类，只需使用现有的 Account 类即可。

如果将来某天您必须彻底改变您的记账模型，您可以移除 Account 类并用一个新类替换它。其余的代码和界面可以保持不变。所有这些好处都源于使用模型-视图-控制器（Model-View-Controller）设计模式。

## 第 8 章

## 带视图的窗口

### 本章内容

- 打开、关闭和隐藏窗口
- 将窗口定位在屏幕的任何位置
- 跟踪打开的窗口
- 更改窗口的外观
- 调整窗口大小
- 透过窗口看（透明性）
- 使用工作表（sheets）和代理（delegates）

基于图形用户界面（GUI）的应用程序中最重要的是元素是窗口。事实上，窗口的重要性使得来自雷德蒙德的家伙们（微软）用它来命名他们的操作系统。应用程序中的窗口就像您用来收集想法、显示信息和记录输入的纸片。

Cocoa 中的窗口同样重要。Mac OS X 继续着使 Mac OS 闻名的精美窗口传统，但 Cocoa 在过去理念的基础上进行了构建，并通过令人兴奋的新功能加以改进。在本章中，您将研究 Cocoa 应用程序中一些最常见的窗口功能。在此过程中，您将创建两个项目来演示这些功能。

## 处理窗口

由于窗口构成了几乎所有界面的基础，您在项目中会经常使用它们。您需要执行的一些最常见功能包括：

- 打开和关闭窗口
- 移动窗口
- 将窗口添加到“窗口”菜单

在接下来的部分中，您将发现如何完成所有这些任务以及更多。

### 打开和关闭窗口

当您在 Cocoa 项目中处理窗口时，通常会使用 Interface Builder 来设计它们。此外，如果您在 Interface Builder 中设计应用程序界面时保留一个窗口处于打开状态，那么当应用程序运行时，该窗口会自动打开。因此，如果您正在构建单窗口应用程序，甚至可能不需要发出打开窗口的命令。

假设 `theWindow` 是项目中的一个输出。在代码中关闭窗口就像下面这样简单：

```objective-c
[theWindow close];
```

`close` 方法会将窗口从视图中隐藏。如果您希望关闭窗口时同时从内存中释放该窗口，请也使用 `setReleasedWhenClosed` 方法：

```objective-c
[theWindow setReleasedWhenClosed: YES];
[theWindow close];
```

以这种方式关闭窗口后，窗口便消失了。其内容已从内存中移除。它不复存在。这意味着如果想再次看到该窗口，您必须完全创建一个新的窗口对象。如果窗口已从内存中释放，您必须像这样创建一个新的窗口：

```objective-c
theWindow = [[NSWindow alloc] init];
```

然后，为了显示该窗口，向其发送 `makeKeyAndOrderFront` 消息，如下所示：

```objective-c
[theWindow makeKeyAndOrderFront: self];
```

### 隐藏和显示窗口

如果您更喜欢保留窗口而不是将其从内存中删除，可以将其隐藏而不是关闭。隐藏窗口也是一个简单的任务。假设您的对象类中有一个名为 `theWindow` 的输出。该输出代表您界面中的一个窗口。要隐藏该窗口，`hideWindow` 动作可能如下所示：

```objective-c
- (IBAction)hideWindow: (id) sender
{
```
