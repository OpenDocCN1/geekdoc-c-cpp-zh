
![](img/d4b18a89aece4a6ccac4cb886bdef5f7_70_0.png)

你需要添加一些代码，让这个操作执行一些有趣的操作。导航到 `TestAppAppDelegate.m` 文件（`TestAppAppDelegate` 类的实现文件），向下滚动找到 `-sayHello:` 方法。将其编辑为如下所示：

```objective-c
- (IBAction)sayHello:(id)sender {
    [[NSAlert alertWithMessageText:@"Important Message"
                     defaultButton:@"Hello Yourself"
                   alternateButton:nil
                       otherButton:nil
         informativeTextWithFormat:@"Hello World"] runModal];
}
```

点击 Run 按钮构建并运行应用程序。给 Say Hello 按钮一个测试点击，确保它正常工作。你应该会看到类似 **图 5.9** 的内容。当你满意后，退出应用程序，并导航回 `MainMenu.xib` 文件。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_71_0.png)

**图 5.10** TestApp 在文本字段中显示其 Hello World 消息

## 添加文本字段

也许你认为模态对话框被过度使用了，所以你想把文本放到应用程序窗口中的一个文本字段中。在对象库中找到 Text Field 控件，并将其拖入窗口。要与文本字段通信并将其字符串值设置为 Hello World，你需要为它创建一个 outlet。

要添加 outlet，从文本字段拖一条连接线到助理编辑器中的源代码。这次，将连接放在花括号内（因为 outlet 是类的实例变量）。选择 Outlet 连接类型，将其命名为 **textField**，然后按 Return 键完成添加 outlet。

现在你的代码有了对文本字段的引用，你可以修改操作，将消息显示在那里，而不是在模态对话框中。导航回 `TestAppAppDelegate.m` 文件中的 `-sayHello:` 操作，并将其改为如下所示：

```objective-c
- (IBAction)sayHello:(id)sender {
    [textField setStringValue:@"Hello World"];
}
```

构建并运行应用程序，验证一切是否正常。你的应用程序看起来应该类似 **图 5.10**。

## 布局

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_72_0.png)

**图 5.11** 不正确的布局行为

你已经学习了创建和连接简单用户界面的基础知识。然而有一个小问题。如果 TestApp 没有在运行，请再次运行它，并尝试调整窗口大小。控件固执地停在原地，拒绝做出任何智能的调整（**图 5.11**）。

自 Mac OS X 10.7 Lion 发布以来，有两种机制可以用来定义视图的大小和定位行为：最初的“弹簧和支柱”以及新的 Autolayout（自动布局）特性。

> **注：** 这两种布局机制都有定义良好的 API，允许你使用代码控制布局行为。由于本书专注于 Xcode 而不是 Cocoa 开发，因此不会涉及编码主题。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_0.png)

**图 5.13** 在自动调整大小控件中停用弹簧和支柱

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_1.png)

**图 5.14** 重叠的控件

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_2.png)

**图 5.15** 选择多个控件

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_75_3.png)

**图 5.16** 居中的控件

## 约束

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_77_0.png)

**图 5.18** 小窗口中被截断的控件

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_77_1.png)

**图 5.19** 设置窗口大小约束

再次运行 TestApp 并调整窗口大小。注意文本字段现在如何变大和缩小。还要注意，如果窗口变得太小，按钮会被截断，字段也会变得有点太窄（图 5.18）。这是弹簧和支柱模型的局限性：应用任何约束的唯一方法是设置一个最小大小，这样控件不会被挤在一起或截断。

最简单的修复是设置最小窗口大小。选择窗口，在大小检查器的约束部分，选中 Minimum Size 复选框，并设置一个合理的尺寸（例如 200 x 150），如图 5.19 所示。

现在当你运行 TestApp 并调整大小时，控件应该大致能各自安分守己。你可能需要调整最小窗口大小或文本字段及包含它的自定义视图的大小，才能得到正确效果。

## 在 Lion 中使用自动布局

如前所述，Lion（Mac OS X 10.7）引入了一种名为自动布局的新布局机制。尽管它确实比弹簧和支柱有巨大改进（并且还有一套用于代码中的漂亮布局语言），但在 Lion 及以上版本中，它的使用并不是强制性的。也就是说，弹簧和支柱机制仍然可以像以前一样工作。事实上，你必须为每个打算使用自动布局的 Interface Builder 文档打开自动布局，否则弹簧和支柱仍然占主导地位。相应地，自动布局只能用于面向 OS X 10.7 及以上版本的应用程序。

> **注：** 你需要运行 Xcode 4.1 或更高版本，才能使用编辑器的自动布局功能。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_77_2.png)

**图 5.20** Interface Builder 文档的文件设置

**图 5.21** Mac OS X 10.7 升级提示

## 激活自动布局

要为 `MainMenu.xib` 激活自动布局，请导航到该文件，并确保工具区可见且选中了文件检查器面板。在 Interface Builder 文档部分（图 5.20）中，勾选 Use Autolayout 复选框。

如果你的项目最低部署版本设置为较低版本，系统可能会提示你将其升级到 Mac OS X 10.7，如图 5.21 所示。点击 Continue and Upgrade 按钮接受升级。

> **注：** 接受自动布局升级并将最低部署版本设置为 10.7，意味着你的应用程序将无法在 Mac OS X 10.7 之前的版本上运行。如前所述，自动布局需要 10.7。

## 约束

你会立刻注意到一些不同。图 5.22 显示了 Interface Builder 对象停靠区中新的 Constraints 条目。约束是真实的对象，就像按钮和窗口一样。它们定义其所约束控件的尺寸和定位行为。因为它们是真实的对象，你可以在 Interface Builder 中像处理按钮或窗口一样选择、配置或删除它们。

图 5.23 显示了一个选中的垂直间距约束。该约束管理 Say Hello 按钮与自定义视图顶部边框之间的垂直间距。使用自动布局时，将控件拖入窗口或视图并使其对齐到辅助线，会自动创建系统认为适合保持最佳定位的约束。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_79_0.png)

**图 5.22**（顶部）添加到文档中的约束对象

**图 5.23**（左侧）选中的垂直间距约束

要修复此问题（并探索添加约束），请选择自定义视图，然后从主菜单中选择 Editor > Pin > Leading Space to Superview。再次选择自定义视图，并选择 Editor > Pin > Trailing Space to Superview。你的窗口应该看起来类似 **图 5.25**。

如果现在运行 TestApp，你会发现这并没有完全解决问题。虽然按钮与下方字段保持相同的距离，而且自定义视图似乎正在调整大小（从文本字段的左边缘跟随移动可以看出），但其他一切似乎都不太正常。

文本字段的修复很简单。将左右边缘对齐到自定义视图内部的蓝色辅助线（**图 5.26**），适当的约束就会自动为你创建。

图 5.27 显示了将文本字段边缘对齐到左右辅助线后添加的约束。这些约束表明你希望保持字段两侧与父视图边界两侧之间的空间。再次运行 TestApp 表明，自动布局约束现在的工作方式与最初的弹簧和支柱相同。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_81_0.png)

**图 5.25** 自定义视图的前导空间和尾随空间约束

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_81_1.png)

**图 5.26** 通过对齐辅助线创建约束

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_81_2.png)

**图 5.27** 新添加的约束

