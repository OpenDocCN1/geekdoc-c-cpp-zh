

4. 保存 `KeyboardInputsViewController.xib` 文件，然后在 Xcode 中按下 Command-R，在 iPhone 模拟器上运行应用程序。当应用程序加载后，键盘最初是隐藏的；当用户点击 TextField 视图时，键盘会自动出现（见图 5-2）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_178_0.png)

图 5-2

3. 保存 `KeyboardInputsViewController.xib` 文件。
4. 在 `KeyboardInputsViewController.m` 文件中，为 `doneEditing:` 操作提供实现：
5. 保存项目并按下 Command-R，在 iPhone 模拟器上运行应用程序。
6. 当应用程序出现在 iPhone 模拟器上时，点击 TextField 视图。键盘应该会出现。使用键盘在视图中输入一些文本，完成后点击 Return 键。现在键盘会消失。

```objc
#import "KeyboardInputsViewController.h"

@implementation KeyboardInputsViewController

-(IBAction) doneEditing:(id) sender{
[sender resignFirstResponder];
}
```

## 工作原理

你刚刚所做的是将 TextField 视图的 Did End on Exit 事件与你创建的 `doneEditing:` 操作连接起来。当你使用键盘编辑 TextField 视图的内容时，点击键盘上的 Return 键会触发 TextField 视图的 Did End on Exit 事件。在这种情况下，它会调用 `doneEditing:` 操作，其中包含以下语句：

```objc
[sender resignFirstResponder];
```

这里的 `sender` 指的是 TextField 视图，而 `resignFirstResponder` 要求 TextField 视图放弃其 First-Responder 状态。本质上，这意味着你不再想与 TextField 视图交互，也不再需要键盘。因此，键盘应自行隐藏。

> **注意** 视图中的 First Responder 总是指用户当前正在交互的视图。在此示例中，当你点击 TextField 视图时，它成为 First Responder 并自动激活键盘。

隐藏键盘的另一种方式是当用户点击 TextField 视图以外的区域时。这种方法更自然，不需要用户手动点击键盘上的 Return 键来隐藏键盘。下面的 Try It Out 展示了如何实现这种方法。

## TRY IT OUT 关闭键盘（技巧 2）

1. 使用 KeyboardInputs 项目，双击 `KeyboardInputsViewController.xib` 文件，使用 Interface Builder 编辑它。

2. 向 View 窗口添加一个 Round Rect Button 视图（见图 5-9）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_183_0.png)

图 5-9

3. 选中 Round Rect Button 视图后，选择 Layout → Send to Back。这将使按钮显示在其他控件的后面。

4. 调整 Round Rect Button 视图的大小，使其覆盖整个屏幕（见图 5-10）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_184_0.png)

图 5-10

5. 在 Attributes Inspector 窗口中，将 Round Rect Button 视图的 Type 设置为 Custom（见图 5-11）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_185_0.png)

图 5-11

6. 在 Xcode 中，编辑 `KeyboardInputsViewController.h` 文件，并添加以下粗体语句：

```objc
#import <UIKit/UIKit.h>

@interface KeyboardInputsViewController : UIViewController {
    IBOutlet UITextField *textField;
}

@property (nonatomic, retain) UITextField *textField;

-(IBAction) doneEditing:(id) sender;

-(IBAction) bgTouched:(id) sender;

@end
```

7. 在 Interface Builder 中，按住 Control 键并将 File's Owner 项拖到 TextField 视图上。应该会出现 `textField` 出口。选择它。

8. 按住 Control 键并将 Round Rect Button 视图拖到 `KeyboardInputsViewController.xib` 窗口中的 File's Owner 项上（见图 5-12）。选择 `bgTouched:` 操作。

11. 就这样。在 Xcode 中按下 Command-R 将应用程序部署到 iPhone 模拟器上。然后，尝试以下操作：

- 点击 TextField 视图以调出键盘。
- 完成后，点击键盘上的 Return 键来关闭它。或者，点击 TextField 视图之外的任何空白区域来关闭键盘。

## 工作原理

在此示例中，你添加了一个 Round Rect Button 视图来覆盖应用程序 View 窗口中的所有空白区域。本质上，该按钮充当一张网，捕获 View 窗口上 TextField 视图之外的所有触摸。因此，当用户点击键盘和 TextField 视图之外的屏幕时（或在真设备上触摸），Round Rect Button 会触发 Touch Up Inside 事件，该事件由 `bgTouched:` 操作处理。在 `bgTouched:` 操作中，你明确要求 `textField` 放弃其 First-Responder 状态，从而导致键盘消失。

此示例中使用的技巧即使你的视图上有多个 TextField 视图也适用。假设你有三个 TextField 视图，其出口名为 `textField`、`textField2` 和 `textField3`。在这种情况下，`bgTouched:` 操作如下所示：

```objc
-(IBAction) bgTouched:(id) sender{
[textField resignFirstResponder];
[textField2 resignFirstResponder];
[textField3 resignFirstResponder];
}
```

因此，当调用 `bgTouched:` 操作时，所有三个 TextField 视图都会被要求放弃其 First-Responder 状态。对当前不是 First Responder 的视图调用 `resignFirstResponder` 方法是无害的；因此，上述语句是安全的，不会在运行时导致异常。

## 理解响应者链

前面的 Try It Out 是响应者链运行的一个很好的示例。在 iPad 中，事件通过一系列事件处理程序传递，这些处理程序称为响应者链。当你触摸 iPad 屏幕时，iPad 会生成事件，这些事件会沿着响应者链向上传递。响应者链中的每个对象都会检查自己是否能处理该事件。在前面的示例中，当用户点击 Label 视图时，Label 视图会检查自己是否能处理该事件。由于 Label 视图不处理 Touch 事件，因此该事件会沿着响应者链向上传递。你添加的大背景按钮现在成为下一个检查事件的对象。由于它处理 Touch Up Inside 事件，因此该事件被按钮消耗。

总之，响应者链中位置较高的对象首先检查事件，并在事件适用时处理它。任何对象都可以阻止事件在响应者链中的传播，如果它只部分处理事件，也可以将事件继续向上传递。

2. 使用 ScrollView 视图填充 View（见图 5-13）。调整 ScrollView 视图的大小，使其覆盖整个屏幕。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_189_0.png)

图 5-13

3. 向 ScrollView 添加 Label 视图、TextField 视图和 Round Rect Button 视图（见图 5-14）。将 Label 视图的文本设置为“Enter some text here”，将按钮的文本设置为“OK”。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_190_0.png)

图 5-14

4. 在 Xcode 中，将以下以粗体突出显示的语句输入到 `ScrollingViewsViewController.h` 文件中并保存：

```objc
#import <UIKit/UIKit.h>

@interface ScrollingViewsViewController : UIViewController <UITextFieldDelegate> {
    IBOutlet UIScrollView *scrollView;
    IBOutlet UITextField *textField;
    UITextField *currTextField;
}

@property (nonatomic, retain) UITextField *textField;
@property (nonatomic, retain) UIScrollView *scrollView;

@end
```

5. 在 Interface Builder 中，按住 Control 键并将 File's Owner 项拖到 TextField 视图上（见图 5-15）。选择 `textField`。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_191_0.png)

6. 按住 Control 键并将 File's Owner 项拖到 ScrollView 视图上（见图 5-16）。选择 `scrollView`。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_192_0.png)

图 5-16

7. 按住 Control 键并将 TextField 视图拖到 File's Owner 项上（见图 5-17）。选择 `delegate`。

