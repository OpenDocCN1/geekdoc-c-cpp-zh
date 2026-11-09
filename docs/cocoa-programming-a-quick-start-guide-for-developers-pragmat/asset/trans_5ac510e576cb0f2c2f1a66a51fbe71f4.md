
当用户点击键盘上的 Go 时，URL 会被加载，同时我们让文本字段调用 resignFirstResponder 来收起键盘。我们还会重新启用 Web 视图。我们把这一切都放在委托方法 textFieldShouldReturn: 中。

```objc
-(BOOL) textFieldShouldReturn:(UITextField *)textField {
    [self loadURLFromTextField];
    [textField resignFirstResponder];
    [self enableWebView];
    return YES;
}
```

点击 Build & Run；你应该能够输入 URL，并点击 Go 加载相应网站。现在我们有了一个基本可用的浏览器。接下来让按钮正常工作。

### 10.7 使用第三个委托实现按钮

如果回看我们的 BrowserController，你会看到我们需要知道网页何时加载完成，以便重置按钮。要知道页面何时加载完成，唯一的方法是使用 UIWebViewDelegate。

我们将使用 MobileBrowserViewController 作为 Web 视图的委托。我们还会为 Forward 和 Back 按钮添加 outlet。现在我们的头文件如下所示：

```objc
#import <UIKit/UIKit.h>

@interface MobileBrowserViewController : UIViewController
                                      <UITextFieldDelegate> {
    UIWebView *webView;
    UITextField *address;
    UIBarButtonItem *backButton;
    UIBarButtonItem *forwardButton;
}
@property(nonatomic, retain) IBOutlet UIWebView *webView;
@property(nonatomic, retain) IBOutlet UITextField *address;
@property(nonatomic, retain) IBOutlet UIBarButtonItem *backButton;
@property(nonatomic, retain) IBOutlet UIBarButtonItem *forwardButton;

@end
```

在 Interface Builder 中打开 MobileBrowserViewController nib。我们需要建立五个连接。

- 1. 选择 File’s Owner，将 backButton outlet 连接到 Back 按钮，将 forwardButton outlet 连接到 Forward 按钮。
- 2. 选择 Web 视图，将其 delegate 连接到 File’s Owner。
- 3. 仍在 Web 视图中，将 goBack: 接收动作连接到 Back 按钮，将 goForward: 连接到 Forward 按钮。

保存你的工作。现在，像我们在桌面浏览器中那样实现按钮重置。别忘了合成属性。接下来，我们会从告知网页加载完成的委托方法中调用一个我们创建的方法，名为 resetButtons:。对于 iPhone，该方法是 webViewDidFinishLoad:。

```objective-c
-(void) resetButtons:(UIWebView *)theWebView {
    [self.backButton setEnabled:[theWebView canGoBack]];
    [self.forwardButton setEnabled:[theWebView canGoForward]];
}
-(void)webViewDidFinishLoad:(UIWebView *)theWebView {
    [self resetButtons:theWebView];
}
```

运行浏览器，导航到或输入第二个网页的 URL。页面加载后，Back 按钮应启用。点击 Back 按钮；你将返回上一页，同时 Forward 按钮会启用。我们已经在 iPhone 上实现了一个基本可用的 Web 浏览器。

### 10.8 练习：添加活动指示器

向应用程序添加一个 UIActivityIndicatorView。在 Interface Builder 中，将其 Style 设置为 Large White，并选中 Hide When Stopped 复选框。

你的活动指示器应在网站加载时旋转。Web 视图应保持禁用，直到页面加载完成。最后，如果你导航到某个页面，文本字段应显示该页面的 URL，而不是继续包含用户上次输入的 Web 地址。

### 10.9 解决方案：添加活动指示器

首先，将此 outlet 添加到你的 MobileBrowserViewController 头文件中：[8]

下载 iPhoneBrowser/MobileBrowser5/Classes/MobileBrowserViewController.h

```objc
#import <UIKit/UIKit.h>

@interface MobileBrowserViewController : UIViewController
                                      <UITextFieldDelegate> {
    UIWebView *webView;
    UITextField *address;
    UIBarButtonItem *backButton;
    UIBarButtonItem *forwardButton;
    UIActivityIndicatorView *activityView;
}
@property(nonatomic,retain) IBOutlet UIWebView *webView;
@property(nonatomic, retain) IBOutlet UITextField *address;
@property(nonatomic, retain) IBOutlet UIBarButtonItem *backButton;
@property(nonatomic, retain) IBOutlet UIBarButtonItem *forwardButton;
@property(nonatomic, retain) IBOutlet UIActivityIndicatorView *activityView;
@end
```

现在打开 nib 文件，将一个活动指示器视图拖到 Web 视图上方。使用 Connections inspector 将其连接到 outlet，然后使用 Attributes inspector 将其 Style 设置为 Large White，并选中 Hide When Stopped 复选框。保存你的工作，然后返回 Xcode。

我们可以在 webViewDidStartLoad: 和 webViewDidFinishLoad: 方法中完成所有需要的更改。此外，你可以移除 textFieldShouldReturn: 方法中对 enableWebView: 的调用。让我们停下来回顾一下本章编写的代码。我发现，我们只用这么少的代码就实现了 Web 视图、文本字段及其键盘、Forward 和 Back 按钮以及活动指示器，这令人印象深刻。

下载 iPhoneBrowser/MobileBrowser5/Classes/MobileBrowserViewController.m

```objc
#import "MobileBrowserViewController.h"

@implementation MobileBrowserViewController

@synthesize address, webView, backButton, forwardButton, activityView;
```

8. 请记住，一旦模拟器修复，你就可以从头文件中删除实例变量声明。

```objective-c
//View Controller Utility Methods
-(void) disableWebView {
    self.webView.userInteractionEnabled = NO;
    self.webView.alpha = 0.25;
}
-(void) enableWebView {
    self.webView.userInteractionEnabled = YES;
    self.webView.alpha = 1.0;
}
-(void) loadURLFromTextField {
    NSURL *url = [NSURL URLWithString:self.address.text];
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
    [self.webView loadRequest:request];
}
-(void) resetButtons: (UIWebView *) theWebView {
    [self.backButton setEnabled:[theWebView canGoBack]];
    [self.forwardButton setEnabled:[theWebView canGoForward]];
}

//Initialization
- (void)viewDidLoad {
    [super viewDidLoad];
    self.address.text = @"http://pragprog.com";
    [self loadURLFromTextField];
}

//Web View Delegate methods
-(void)webViewDidStartLoad:(UIWebView *) theWebView {
    [self disableWebView];
    [self.activityView startAnimating];
}
-(void)webViewDidFinishLoad:(UIWebView *)theWebView {
    [self enableWebView];
    [self.activityView stopAnimating];
    [self resetButtons:theWebView];
    self.address.text = [self.webView.request.URL absoluteString];
}

//Text Field Delegate methods
-(void)textFieldDidBeginEditing:(UITextField *)textField {
    [self disableWebView];
}
-(BOOL) textFieldShouldReturn:(UITextField *)textField {
    [self loadURLFromTextField];
    [textField resignFirstResponder];
    return YES;
}
```

```objc
//Memory Management
- (void)didReceiveMemoryWarning {
    // Releases the view if it doesn’t have a superview.
    [super didReceiveMemoryWarning];
}
- (void)dealloc {
    self.address = nil;
    self.webView = nil;
    self.backButton = nil;
    self.forwardButton = nil;
    self.activityView = nil;
    [super dealloc];
}
@end
```

我们使用了三个委托和一堆属性，而最长的方法体也只有四行。我希望，这次以 iPhone 应用的形式再次审视创建 Web 浏览器的过程，能帮助你感受到开发 Cocoa 应用程序的节奏。

### 10.10 使用 Pragma Marks 组织代码

我在上一个代码清单中添加了注释，以帮助将方法分类组织。这有助于我在浏览源代码时定位所需的方法，但还有更好的方法。

如果你查看编辑器窗口顶部，会看到几个下拉菜单。其中一个显示已打开的其他文件，并允许你在它们之间快速切换。另一个显示所有方法名。选择一个，你就会移动到源代码中的相应位置。它目前看起来像这样：

![](img/9355405953264484a02198b0e3d25b7e_187_0.png)
