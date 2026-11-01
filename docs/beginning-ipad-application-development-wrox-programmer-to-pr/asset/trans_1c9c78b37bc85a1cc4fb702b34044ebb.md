

![](img/744c5ec15e15ca7891c98be71dc25d13_185_0.png)

图 5-11

6. 在 Xcode 中，编辑 KeyboardInputsViewController.h 文件，并添加以下粗体语句：

```objc
#import <UIKit/UIKit.h>

@interface KeyboardInputsViewController : UIViewController {
    IBOutlet UITextField *textField;
}

@property (nonatomic, retain) UITextField *textField;

- (IBAction) doneEditing:(id) sender;

- (IBAction) bgTouched:(id) sender;

@end
```

7. 在 Interface Builder 中，按住 Control 键单击并将 File's Owner 项拖动到 TextField 视图上。应该会出现 textField 出口。选择它。

8. 在 KeyboardInputsViewController.xib 窗口中，按住 Control 键单击并将圆角矩形按钮视图拖动到 File's Owner 项上（参见图 5-12）。选择 bgTouched: 操作。

## 视图加载时自动显示键盘

有时你可能希望立即将 TextField 视图设置为活动视图并显示键盘，而无需等待用户进行操作。在这种情况下，你可以使用视图的 `becomeFirstResponder` 方法。以下代码表明，一旦视图窗口加载完成，TextField 视图将成为第一响应者：

```objc
- (void)viewDidLoad {
    [textField becomeFirstResponder];
    [super viewDidLoad];
}
```

## 检测键盘是否出现

到目前为止，你已经看到了使用完键盘后隐藏键盘的各种方法。然而，有一个问题需要注意。当键盘出现时，它会占据屏幕的很大一部分。如果你的 TextField 视图位于屏幕底部，它会被键盘遮挡。作为程序员，你有责任确保该视图被重新定位到屏幕的可见部分。令人惊讶的是，SDK 并没有处理这个问题；你必须自己完成这项艰巨的工作。

> **注意**：iPad 的键盘在竖屏模式下高度为 264 像素，在横屏模式下高度为 352 像素。

不过，首先，理解几个与键盘相关的关键概念对你来说很重要：

- 你需要能够以编程方式知道键盘何时显示或隐藏。为此，你的应用程序需要注册 `UIKeyboardWillShowNotification` 和 `UIKeyboardWillHideNotification`。
- 你还需要知道当前正在编辑哪个 TextField 视图以及何时开始编辑，以便你可以将其重新定位到屏幕的可见部分。你可以通过 `UITextFieldDelegate` 协议中可用的两个委托方法——`textFieldDidBeginEditing:` 和 `textFieldDidEndEditing:`——来获取这两条信息。

搞糊涂了吗？别担心；下面这个“试一试”会让一切变得明白。

### 试一试 移动视图

*可从 Wrox.com 下载的代码文件 ScrollingViews.zip*

1. 使用 Xcode，创建一个新的基于视图的应用程序项目，并将其命名为 `ScrollingViews`。

![](img/744c5ec15e15ca7891c98be71dc25d13_190_0.png)

图 5-14

4. 在 Xcode 中，将以下以粗体突出显示的语句输入到 ScrollingViewsViewController.h 文件中并保存：

```objc
#import <UIKit/UIKit.h>

@interface ScrollingViewsViewController : UIViewController <UITextFieldDelegate> {
    IBOutlet UIScrollView *scrollView;
    IBOutlet UITextField *textField;
}
```

> **注意**：第 7 步很重要，因为它使委托方法（`textFieldDidBeginEditing:` 和 `textFieldDidEndEditing:`）能够由视图控制器处理。

![](img/744c5ec15e15ca7891c98be71dc25d13_193_0.png)

```objc
return NO;
}
-(void) dealloc {
    [textField release];
    [scrollView release];
    [super dealloc];
}
```

10. 在 Xcode 中保存项目并按 Command-R 将应用程序部署到 iPhone 模拟器上。图 5-18 显示，当你单击 TextField 视图时，键盘出现，TextField 视图（以及其他视图）会滚动到屏幕中央。要隐藏键盘，只需单击 Return 键，视图就会恢复到原始位置。

![](img/744c5ec15e15ca7891c98be71dc25d13_196_0.png)

图 5-18

### 工作原理

本示例演示了检测键盘是否出现的各种方法，以及如何重新定位相关视图，使其不被键盘遮挡。

首先，你声明了三个私有变量：

```objc
//---size of keyboard---
CGRect keyboardBounds;

//---size of application screen---
CGRect applicationFrame;

//---original size of ScrollView---
CGSize scrollViewOriginalSize;
```

keyboardBounds 用于存储键盘的大小（尤其是获取键盘的高度）。虽然你总是可以将键盘的高度硬编码为 264，但我不建议这样做，因为键盘的大小以后可能会发生变化。更好的做法是在运行时动态获取键盘的大小。

applicationFrame 用于存储屏幕的大小。与键盘的大小一样，最好在运行时动态获取这个值。

scrollViewOriginalSize 用于保存 ScrollView 视图的原始大小。这样做可以让你在用户完成编辑后（此时所有视图都需要移回其原始位置）将 ScrollView 恢复到其原始大小。

当视图加载时，你首先保存 ScrollView 视图的大小，并获取屏幕的大小：

```objc
-(void) viewDidLoad {
    scrollViewOriginalSize = scrollView.contentSize;
    applicationFrame = [[UIScreen mainScreen] applicationFrame];
    [super viewDidLoad];
}
```

在 viewWillAppear: 事件中（此方法在视图出现在屏幕之前调用），你注册两个通知——UIKeyboardWillShowNotification 和 UIKeyboardWillHideNotification。当键盘出现时（UIKeyboardWillShowNotification），会调用 keyboardWillShow: 方法。当键盘消失时，会调用 keyboardWillHide: 方法：

```objc
-(void) viewWillAppear:(BOOL)animated {
    //---registers the notifications for keyboard---
    [[NSNotificationCenter defaultCenter]
    addObserver:self
    selector:@selector(keyboardWillShow:)
    name:UIKeyboardWillShowNotification
    object:self.view.window];

    [[NSNotificationCenter defaultCenter]
    addObserver:self
    selector:@selector(keyboardWillHide:)
    name:UIKeyboardWillHideNotification
    object:nil];
}
```

在视图消失之前，你移除之前设置的通知：

```objc
-(void) viewWillDisappear:(BOOL)animated {
    [[NSNotificationCenter defaultCenter]
    removeObserver:self
    name:UIKeyboardWillShowNotification
    object:nil];

    [[NSNotificationCenter defaultCenter]
    removeObserver:self
    name:UIKeyboardWillHideNotification
    object:nil];
}
```

当你点击 TextField 视图时，会首先调用 textFieldDidBeginEditing: 方法。通过此方法，你可以知道正在编辑哪个 TextField 视图：

```objc
//---when a TextField view begins editing---
-(void) textFieldDidBeginEditing:(UITextField *)textFieldView {
    currTextField = textFieldView;
}
```

接下来，调用 keyboardWillShow: 方法。通过此方法，你尝试通过传递对 keyboardBounds 变量的引用来获取键盘的大小。现在你可以移动 ScrollView 视图，使 TextField 视图能够在键盘未覆盖的剩余可见空间中居中。你通过调用接下来定义的 moveScrollView: 方法来执行滚动：

```objc
//---when the keyboard appears---
-(void) keyboardWillShow:(NSNotification *) notification {
    //---gets the size of the keyboard---
    NSDictionary *userInfo = [notification userInfo];
    NSValue *keyboardValue =
    [userInfo objectForKey:UIKeyboardBoundsUserInfoKey];
    [keyboardValue getValue:&keyboardBounds];
    [self moveScrollView:currTextField];
}
```

在 moveScrollView: 方法中，你计算需要滚动的像素数，然后让 ScrollView 视图滚动其包含的视图，直到当前正在编辑的 TextField 视图位于屏幕可见区域的中心：

```objc
-(void) moveScrollView:(UIView *) theView {
    //---get the y-coordinate of the view---
    CGFloat viewCenterY = theView.center.y;
```

