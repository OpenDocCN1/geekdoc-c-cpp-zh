
如果你已经阅读了书中足够的代码并来到了这一步（第 11 章），很可能你在向界面添加按钮时不会遇到什么困难。如果你记得按钮使用了我在第 2 章中提到的 `Target-Action` 模式，你很快就能理解整个按钮的概念。

准备好了吗？让我们开始吧。

## Target-Action 模式

使用 `Target-Action` 模式（见第 2 章）让你的应用程序知道用户执行了某些操作。例如当他或她点击按钮时，你的应用程序应该做出响应——这通常在按钮调用你在代码中指定的某个方法时发生。被调用的方法（通常）位于该特定按钮所在的视图控制器中。对于我们的 `ReturnMeTO` 应用，该控制器将是 `ReturnToViewController`。

在 11-1 中我添加了一个 `UIControl`（按钮）。你可以看到，每当用户点击按钮时，它都会向 `ReturnMeViewController` 发送 `buttonPressed:` 消息。

故事结束——好吧，至少在点击按钮发生后结束了。这里是用一个控件（标签）替换另一个控件（按钮）。这根结底是一个管道问题，并说明了当你使用模型-视图-控制器（MVC）设计模式时，更改用户界面几乎是轻而易举的——它只需要在控制器中进行一点重新调整。而且，是的，在 Interface Builder 中也需要一点重新调整。

## 第 11 章：搞定按钮并返回首页 205

![](img/d3e98c195a93c941d040bbbc53dc1bd8_226_0.png)

图 11-1：完整的架构。

## 完善你的按钮代码

如果你在界面中添加了一个按钮，你需要添加一个方法来处理那些有人决定点击按钮的情况——换句话说，这就是*动作*（action）。

好了，该开始了。首先，你需要在接口中添加动作方法（如列表 11-1 所示）。你将在 `ReturnMeToViewController.h` 文件中完成操作。

### 列表 11-1：添加动作

```objc
@interface ReturnMeToViewController : ViewController<UITextFieldDelegate>

IBIBOutlet UITextField *textField;
IBIBOutlet UILabel *label;
BOOL moveViewUp;
CGFloat scrollAmount;
NSString *callNumber;

}

@property (nonatomic, retain) UITextField *textField;
```

（续）

### 列表 11-1（续）

```objc
@property (nonatomic, retain) UILabel *label;
@property (nonatomic, retain) NSString *callNumber;

- (void)scroll:(BOOL)movedUp;
- (void) updateCallNumber;
- (IBAction)buttonPressed:(id)sender;

@end
```

在这里我们声明了一个新方法——`buttonPressed`，并在它前面加上了一个新关键字——`IBAction`。

`IBAction` 是那些小技巧之一，类似于 `IBOutlet`，它们在代码中什么都不做，但提供了一种方式来通知 Interface Builder（因此其中有 IB）该方法可以作为目标连接（Target-connections）的动作。`IBAction` 所“做”的只是作为 Interface Builder 的动作——识别出这个方法（动作），以便你可以在 nib 文件中将其连接到某个对象（按钮）。在这方面，`IBAction` 技巧与我在第 7 章中讨论的 `IBOutlet` 机制相似。不过，如果你标记的是实例变量，那么这里标记的就是方法。大同小异。

在你启动 Interface Builder 并新按钮与 `ReturnViewController` 方法连接时，会用到 `IBAction`。如果你仔细想，`IBAction` 实际上被定义为 `void`，你只是声明了一个类型为 `void` 的新方法。

```objc
(IBAction)buttonPressed:(id)sender;
(void)buttonPressed:(id)sender);
```

这简单意味着你声明了一个不向调用者返回任何内容的方法。

你得到的实际名称可以是你想要的任何名称，但返回类型必须是 `IBAction`。通常该动作接受一个参数——通常定义为 `id`（指向对象实例变量的指针），命名为 `sender`。触发你动作的控件将使用 `sender` 向其传递一个引用。例如，如果你的方法由于点击按钮的结果被调用，那么参数 `sender` 将包含该按钮。

智者的建议——让 `sender` 包含被点击特定按钮的引用是一个非常实用的机制，即使你可能在 `ReturnMe` 应用程序中不会利用它。有了这个引用，你就可以访问被点击控件的变量。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_227_0.png)

第 11 章：搞定按钮并返回首页 207

好了，你已经声明了方法；任务列表上的下一项是将 `buttonPressed` 方法实际添加到实现文件 `ReturnMeViewController.m` 中。你可以在列表 11-2 中看到实现此操作的代码。我在这里添加了一个新的 `#pragma`，并在之后添加了方法。

```objc
#pragma mark - Target Action methods
```

为了保持我喜好的顺序，我把它放在之前

```objc
#pragma mark - "Model" methods
(void)updateCallNumber {
```

我这样做是因为我喜欢将“模型”方法与覆盖（override）方法和代理（delegate）方法分开。

### 列表 11-2：添加 buttonPressed:

```objc
(IBAction)buttonPressed:(id)sender {
textField.enabled = YES;
label.text = @"You found it, touch below";
textField.placeholder = @"You may now enter the number";
}
```

如果你觉得这段代码很眼熟，那么你的专注力加分。这些代码都不是全新的；我只是把它们从第 9 章重新组合的 `touchesBegin:` 方法中移动了，在那里我将它与标签绑定在了一起。我说过用户界面的变化大部分将是接线问题。这提醒了我——只要你打算构建按钮路线而不是标签路线，最好从 `touchesBegin:` 方法中删除代码。要查看需要删除哪些代码，请查看列表 11-3，我在其中注释掉了（使用双划线）以显示代码

### 列表 11-3：从 touchesBegin: 中移除代码：

```objc
(void)touchesBegin:(NSSet *)touches
withEvent:(UIEvent *) event {
// if (textField.enabled) {
// UITextField *touch = [touches anyObject];
// if (CGRectContainsPoint([label frame], 
// [touch locationInView:self.view])) {
// textField.enabled = YES;
// }//
```

### 列表 11-3（续）

```objc
// textField.placeholder = @"You may now enter the number";
// else {
// textField.enabled = NO;
// //}
}
```
