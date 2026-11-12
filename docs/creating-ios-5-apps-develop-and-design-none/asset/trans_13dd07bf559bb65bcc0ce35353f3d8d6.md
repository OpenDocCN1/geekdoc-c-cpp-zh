

表 4.1 文本字段属性

| 属性名 | 值 |
|---|---|
| 对齐 | 居中 |
| 大写 | 无 |
| 自动更正 | 否 |
| 键盘 | 数字和标点 |
| 返回键 | 完成 |
| 自动启用返回键 | 开 |

![](img/fe9fea534a8e7868f811f7cd33da015f_180_0.png)

**图 4.3** 完成后的“输入重量”视图控制器场景

呼，设置项真不少。我们逐一来说明。我们希望将输入限制为有效的十进制数字。另外，既然我们只允许输入数字，那么启用自动更正和大写就没有意义了。我们不妨将它们关闭。“数字和标点”键盘提供了我们需要的所有按键（所有数字、一个返回键，以及——对于美式英语——一个句点）。实际上它允许的字符过多，因此我们需要过滤输入。稍后我们会讲到这一点。

最后两个设置将帮助我们创建更简洁的用户界面。本质上，我们希望在用户按下返回键时自动创建一个新的 WeightEntry 对象并切换到图形视图。这减少了输入新重量所需的点击次数。为了支持这一点，我们将返回键的标签改为“完成”，以更好地传达我们的意图。更重要的是，自动启用返回键意味着只要文本字段为空，返回键就会处于禁用状态。一旦用户输入了一些文本，系统会自动启用返回键。这与我们的输入过滤相结合，将确保每当按下返回键时，我们都能得到一个有效的重量条目。

现在界面应该与 **图 4.3** 一致。基本框架已经就绪，但我们要对它稍作美化。

## 秘密 **键盘选项**

> 从 iOS 4.1 开始，出现了一种新的键盘类型：UIKeyboardTypeDecimalPad。这种键盘只有数字、一个小数点和一个退格键。乍一看，它似乎非常适合这个项目。然而，它没有返回键——而我们确实希望允许用户直接从键盘提交重量值。
>
> 我们可以添加一个返回键（也许在一个自定义输入附件视图中；请参阅《iOS 文本、Web 和编辑编程指南》），但这会创建更复杂的用户界面。
>
> iOS 5.0 增加了另一种键盘类型：UIKeyboardTypeTwitter。虽然对这个项目来说并不特别有用，但 Twitter 键盘是为编写推文而优化的。它会显示所有字母以及 @ 和 # 键。
>
> 不幸的是，这两个选项都没有出现在 Interface Builder 中——至少在当前版本的 Xcode 中没有。相反，你必须在代码中设置文本字段的 keyboardType 属性。这并不难。在 viewDidLoad 方法中，只需添加 self.weightTextField.keyboardType = UIKeyboardTypeDecimalPad; 或 self.weightTextField.keyboardType = UIKeyboardTypeTwitter;。

## 设置自动旋转和自动调整大小

我们希望视图能够旋转到任意方向。这需要两个步骤。首先，我们必须修改控制器以允许自动旋转。

打开 EnterWeightViewController.m，并导航到 shouldAutorotateToInterfaceOrientation: 方法。如果控制器的视图可以旋转到给定的 interfaceOrientation，该方法应返回 YES。在默认实现中，它只允许旋转到正立的纵向方向。

要允许应用旋转到任意方向，只需让该方法返回 YES，如下所示：

```
- (BOOL)shouldAutorotateToInterfaceOrientation:
    (UIInterfaceOrientation)interfaceOrientation {
    return YES;
}
```

![](img/fe9fea534a8e7868f811f7cd33da015f_182_0.png)

![](img/fe9fea534a8e7868f811f7cd33da015f_182_1.png)

**图 4.4** 自动旋转正常，但自动调整大小不起作用。

**图 4.5** 将控件锁定在视图顶部

然而，如果你运行应用，可能会注意到自动旋转仍然不起作用。无论你如何转动设备，界面都锁定在纵向方向。

这是因为有一个诀窍。默认情况下，只有当所有包含的视图控制器都支持自动旋转时，标签视图才允许自动旋转。对 `HistoryViewController` 和 `GraphViewController` 做同样的修改，然后再次运行应用。

而且……仍然不起作用。好吧，我说谎了。这里有两个诀窍。当我们创建自定义标签视图时，结果发现我们无意中覆盖了标签栏默认的 `shouldAutorotateToInterfaceOrientation:` 实现。打开 `TabBarController.m`，删除 `shouldAutorotateToInterfaceOrientation:` 方法。这将恢复默认行为。最后再运行一次。它应该终于能按预期旋转了。不幸的是，我们又遇到了另一个问题（图 4.4）。在新的更宽的视图中，UI 元素没有正确地调整大小或重新定位。

要解决这个问题，请再次打开 `MainStoryboard.storyboard`。选择“输入今天的重量”标签，并打开“大小”检查器。自动调整大小控件允许我们将对象的位置锁定到顶部、底部、左侧或右侧。它还允许我们自动水平或垂直拉伸和收缩控件。

默认情况下，视图锁定在左侧和顶部。我们希望它锁定到顶部——但我们希望它保持在视图中居中。点击“自动调整大小”控件左侧的红色 I 形条以将其关闭。在“自动调整大小”控件中进行更改后，请检查“示例”预览，以确保控件的行为符合你的预期。在这种情况下，当尺寸变化时，它应保持在视图顶部居中（图 4.5）。

当然，我们仍然可以在 Interface Builder 中创建按钮，并将其分配为新的顶级对象。然后我们可以使用 Interface Builder 配置其设置。遗憾的是，这实际上对我们没有多大帮助，因为我们在编辑时无法直观地检查它。综合考虑，也许最简单的方法就是直接在代码中创建按钮。

打开 EnterWeightViewController.h，并添加以下属性和操作：

```
@property (nonatomic, strong) WeightHistory* weightHistory;
@property (strong, nonatomic) IBOutlet UITextField *weightTextField;
@property (strong, nonatomic) IBOutlet UILabel *dateLabel;
@property (strong, nonatomic) UIButton* unitsButton;
- (IBAction)saveWeight:(id)sender;
- (IBAction)changeUnits:(id)sender;
```

接下来，切换到实现文件并合成该属性。

```
@synthesize unitsButton=_unitsButton;
```

现在，向下滚动到 viewDidLoad 方法。按如下所示修改它：

```
- (void)viewDidLoad
{
    [super viewDidLoad];
    self.unitsButton = [UIButton buttonWithType:UIButtonTypeCustom];
    self.unitsButton.frame = CGRectMake(0.0f, 0.0f, 25.0f, 17.0f);
    self.unitsButton.backgroundColor = [UIColor lightGrayColor];
    self.unitsButton.titleLabel.font =
    [UIFont boldSystemFontOfSize:12.0f];
    self.unitsButton.titleLabel.textAlignment =
    UITextAlignmentCenter;
    [self.unitsButton setTitle:@"lbs"
                     forState:UIControlStateNormal];
    [self.unitsButton setTitleColor:[UIColor darkGrayColor]
                        forState:UIControlStateNormal];
    [self.unitsButton setTitleColor:[UIColor blueColor]
                        forState:UIControlStateHighlighted];
    [self.unitsButton addTarget:self
                         action:@selector(changeUnits:)
               forControlEvents:UIControlEventTouchUpInside];
    self.weightTextField.rightView = self.unitsButton;
    self.weightTextField.rightViewMode = UITextFieldViewModeAlways;
}
```

我们首先创建一个自定义按钮，然后对其进行配置。它高 17 点、宽 25 点，背景为浅灰色。我们还配置了它的标题。它使用 12 点粗体系统字体，并且居中对齐。标题居中很重要；当用户更改单位时，我们会在按钮的标签之间切换“lbs”和“kg”。将标签居中可以使按钮具有良好、一致的外观，即使标签大小发生变化也是如此。

接下来，我们将默认标题设置为“lbs”，然后为不同的控件状态分配文本颜色。通常文本为深灰色，但当按钮被高亮时，文本会变为蓝色。

我们还将 changeUnits: 操作分配给按钮的 UIControlEventTouchUpInside 事件。这等同于在 Interface Builder 中将按钮的 Touch Up Inside 事件与所需操作建立连接。当 unitsButton 被触摸时，系统将调用 changeUnits:。

最后，我们将单位按钮分配给文本字段的 rightView 属性。这将使它出现在文本字段内部右侧。然后我们设置视图模式，使我们的按钮始终可见。

和往常一样，由于我们在 viewDidLoad 中分配了按钮，我们应该在 viewDidUnload 中将其清除。向下导航到 viewDidUnload 并添加以下代码行：

```
self.unitsButton = nil;
```

最后，为我们的 changeUnits: 操作添加一个方法存根。在将更改单位视图添加到我们的 storyboard 之后，我们将充实这个方法。

```
- (IBAction)changeUnits:(id)sender {
    // method stub
}
```

