
其工作方式与之前相同。使用红色的 Tasks 停止标志停止正在运行的应用程序。

### 8.5 前向声明

对于上一节中遇到的错误，还有另一种解决方案：你可以在头文件中使用 @class 指令来代替 import 语句。

```objc
#import <Cocoa/Cocoa.h>
@class WebView;
@interface BrowserController : NSObject {
    WebView *myWebView;
}
@property(assign) IBOutlet WebView *myWebView;
-(IBAction) loadPreviousPage: (id) sender;
@end
```

在 BrowserController.h 文件中，编译器只需要知道 WebView 是一个合法的类。它不需要了解关于该类的任何其他信息。@class 指令正是做这件事的。它不会引入整个头文件来告诉我们 WebView 类型的对象能做什么——我们目前还不需要知道这些。它只是向我们保证存在一个名为 WebView 的类。

每当你在头文件中使用 @class 指令时，你很可能需要在实现文件中使用相应的 import 语句。现在就在实现文件顶部附近添加它吧。顺便也把 loadPreviousPage: 动作存根出来。

```objc
#import "BrowserController.h"
#import <WebKit/WebKit.h>

@implementation BrowserController

@synthesize myWebView;

-(IBAction) loadPreviousPage: (id) sender{
    NSLog(@"loadPreviousPage");
}

@end
```

点击 Build & Run。应该没有警告或错误，并且你的浏览器应该像之前一样运行。

### 8.6 连接控制器

回到 Interface Builder；在 Document 窗口中点击 Browser Controller 对象，然后打开 Connections 检查器。

在 Outlets 下，你现在会找到 myWebView，在 Received Actions 下你会看到 loadPreviousPage:。将 loadPreviousPage: 动作连接到 Back 按钮。现在 Back 按钮应该只连接到控制器，而不再直接连接到 web 视图。同时将 myWebView 出口连接到 web 视图。

保存你的工作，然后点击 Build & Run。输入几个 URL。试试 Back 按钮。目前，当你点击 Back 按钮时，loadPreviousPage: 消息会发送到 BrowserController 对象，该对象会在 Console 中打印方法名。

### 8.7 实现加载上一页

回到 Xcode，没有多少代码要写。当 Back 按钮将 loadPreviousPage: 消息发送给 BrowserController 对象时，BrowserController 对象只是转而将 goBack 消息发送给 myWebView。

我们唯一需要决定的是，将什么作为发送者发送给 web 视图。我们可以发送 self，也可以传递调用 loadPreviousPage: 的对象的身份。在我们的情况下，这并不重要。我决定采用后一种方法，将 Back 按钮作为发送者传递。

下载 CreatingAController/SimpleBrowser4/BrowserController.m：

```objc
-(IBAction) loadPreviousPage: (id) sender {
    [self.myWebView goBack:sender];
}
```

就是这样！点击 Build & Run，你又有了一个可用的 Back 按钮。

### 8.8 练习：完成控制器

向 BrowserController 添加另一个名为 loadNextPage: 的动作，并使用它让 Forward 按钮通过控制器工作。

完成之后，向 BrowserController 添加最后一个动作。将其命名为 loadURLFrom:，并使用它让来自文本字段的 URL 输入通过控制器工作。请记住，当点击 Enter 时，文本字段会向控制器发送一条消息，然后 web 视图需要向文本字段发送一条消息以获取文本字段的字符串值。你可以用不止一种方式做到这一点。你可能会想为文本字段引入一个出口。在这种情况下，你不必这样做。使用 sender 与文本字段通信。

### 8.9 解决方案：完成控制器

练习的前半部分与我们共同采取的步骤类似。你需要做三处更改。

首先，你需要使用 Xcode 向头文件 BrowserController.h 添加一个动作并保存：

```objc
-(IBAction) loadNextPage: (id) sender;
```

其次，回到 Interface Builder，选择 BrowserController。在 Connections 检查器中，从 loadNextPage 右侧的圆圈拖到 Forward 按钮以建立连接。保存你的工作。

最后，你需要实现该方法。查看 web 视图的连接，你可以看到需要调用的方法是 goForward。回到 Xcode，修改 BrowserController.m 以添加此方法：

下载 CreatingAnIconController/SimpleBrowser5/BrowserController.m

```objc
-(IBAction) loadNextPage: (id) sender
{
    [self.myWebView goForward:sender];
}
```

保存你的工作。点击 Build & Run，你应该会发现现在有了可用的 Back 和 Forward 按钮。输入几个 URL，你应该能够使用这些按钮在列表中前后移动。

对于练习的后半部分，我们将遵循三个类似的步骤。首先，在 Xcode 中向头文件添加一个名为 loadURLFrom: 的动作并保存：

```objc
-(IBAction) loadURLFrom: (id) sender;
```

在 IB 的 Document 窗口中选择 BrowserController，然后打开 Connections 检查器。

从 `loadURLFrom:` 右侧的圆圈拖到文本字段以建立连接。我们已经配置了文本字段，使其在用户按下 Enter 键时向其目标发送一个动作。你可以使用文本字段的 Attributes 检查器来确认 Action 值仍按此方式设置。保存你的工作。回到 Xcode，像这样实现你的方法：

下载 CreatingAnController/SimpleBrowsers/BrowserController.m

```objc
-(IBAction) loadURLFrom: (id) sender{
    [self.myWebView takeStringURLFrom:sender];
}
```

### 8.10 从 Nib 唤醒

回到第 4 章 *类和对象* 第 62 页，我们使用类似这样的组合创建并初始化了 Greeter 的实例：

```objc
[[Greeter alloc] initWithName:@"Maggie"];
```

我们能够在 `initWithName:` 方法中初始化变量并完成所需的任何自定义。我们在 BrowserController 中没有类似的方法，而且我们的 BrowserController 是在加载 nib 时初始化的，而不是通过显式调用 alloc 和某种形式的 init 来初始化。

稍后我会更深入地介绍当 nib 被取消归档并加载时会发生什么。目前，当应用程序启动时，nib 中归档的对象图会被重建。对象被创建，它们之间的连接被建立。接下来，在向最终用户显示任何内容之前，会向所有拥有该方法的对象发送一条 awakeFromNib 消息。<sup>5</sup> 只需将此方法添加到任何需要在初始化后立即执行任务的文件中：

```objc
-(void) awakeFromNib {
}
```

例如，我希望我们的浏览器在启动时加载默认网页。现在用户必须点击文本字段并按 Enter 才能加载页面。所以在 awakeFromNib 中，我将把文本字段的字符串值设置为 http://pragprog.com，然后让 web 视图显示此页面。这意味着我需要能够在浏览器窗口主体中与文本字段交互。我们需要为 NSTextField 在头文件中添加一个出口。我们把它称为 address。

```objc
#import <Cocoa/Cocoa.h>
@class WebView;
@interface BrowserController : NSObject {
    WebView *myWebView;
    NSTextField *address;
}
@property(assign) IBOutlet WebView *myWebView;
@property(assign) IBOutlet NSTextField *address;

-(IBAction) loadPreviousPage: (id) sender;
-(IBAction) loadNextPage: (id) sender;
-(IBAction) loadURLFrom: (id) sender;
@end
```

在 IB 中将 address 出口连接到文本字段。我还使用 Attributes 检查器移除了文本字段的默认值，但这并不重要。回到 Xcode，在 BrowserController.m 中合成 address，并为 awakeFromNib 添加以下内容：

```objc
-(void)awakeFromNib {
    [self.address setStringValue:@"http://pragprog.com"];
    [self loadURLFrom:self.address];
}
```

### 8.11 禁用和启用按钮

从可用性的角度来看，我们的 web 浏览器仍然存在一些根本性的问题。例如，一个问题就是按钮始终处于启用状态。这意味着用户随时都可以点击它们。如果我们只从 Objective-C 程序员的角度来看，我们知道这没问题。我们可以随意多次向 web 视图发送 goBack: 方法。如果没有上一页可加载，它也不会费心尝试。

但 Cocoa 编程的一个不同之处在于，我们需要从最终用户的角度来看待我们的应用程序。如果点击按钮没有意义，那么就应该有一个视觉提示让我们知道这一点。在本节中，你将编写启用和禁用按钮的代码。它基本能正常工作。

<sup>5</sup> 不会向未实现此消息的对象发送消息，这样你就不会遇到运行时错误。
