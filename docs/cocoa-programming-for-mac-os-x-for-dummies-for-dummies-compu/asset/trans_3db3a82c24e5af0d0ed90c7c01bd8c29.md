
除了新的外观，**纹理化**（textured）属性还会改变设置了该属性的窗口行为。非纹理化窗口允许从标题栏拖动，而纹理化窗口则可以在窗口内除了控件边界以外的任何位置通过点击并拖动来进行移动。

当你第一次看到纹理化窗口酷炫的金属质感外观时，你会受到启发，想要让每个应用程序中的窗口都采用这种风格。毕竟，苹果公司在其许多应用程序（如 iTunes 和 iPhoto）中就是这么做的。

![](img/ea40cad434a338535474e82c1a6ace20_176_0.png)

在你开始将眼前所有窗口都设置为纹理化外观之前，请记住苹果指南建议仅当涉及硬件时才使用纹理化窗口。这解释了为什么你在许多涉及硬件（以某种方式）的苹果应用程序（如 iMovie 和 iPhoto）中能看到这种样式。虽然纹理化窗口看起来很诱人，但请尽量只在必要时使用它们。你的用户会感谢你的。

## 窗口尺寸调整

当你在代码中需要知道窗口大小时，使用 frame 方法，用法与此前本章中相同。它提供对窗口位置和尺寸的访问。要在代码中更改窗口大小，使用 setFrame 方法。你可以使用以下代码将窗口宽度调整为当前宽度的一半：

```c
- (IBAction)halfAsWide: (id) sender
{
    CGRect theFrame = [theWindow frame];
    theFrame.size.width = theFrame.size.width/2;
    [theWindow setFrame:theFrame display:YES];
}
```

如果你想缩放窗口而不强制用户点击该窗口上的缩放按钮，你只需调用窗口的 zoom 方法即可。

```c
[theWindow zoom];
```

## 设置窗口标题

有时你会想要更改显示在窗口标题栏上的标题。使用 setTitle 方法执行此操作非常简单：

```c
[theWindow setTitle:@"My New Window Title"];
```

![](img/ea40cad434a338535474e82c1a6ace20_176_1.png)

当然，你也可以在 Interface Builder 的检视器窗口中设置窗口标题。

如果窗口标题是文档名称，请改用 `setTitleWithRepresentedFilename` 方法而非 `setTitle`。该方法会将文件路径转换为适合查看的窗口标题：

```c
[theWindow setTitleWithRepresentedFilename:theFileName];
```

## 可透视的窗口

Cocoa 窗口有一个 alpha 设置，允许你设置窗口的半透明程度。要看到这种魔法效果，使用 `NSWindow` 的 `setAlpha` 方法，传入一个介于 0.0 和 1.0 之间的值。值为 1.0 表示窗口完全可见；值为 0.0 显示一个完全透明的窗口。以下这行代码使窗口 50% 透明：

```c
[theWindow setAlphaValue:0.5];
```

图 8-4 展示了 `setAlpha` 值为 0.5 和 1.0 的窗口之间的区别。

![](img/ea40cad434a338535474e82c1a6ace20_177_0.png)

## 附窗（Sheets）之下

除了你迄今使用过的普通窗口，Cocoa 还提供了一种特殊的动画窗口——附窗（sheet）。附窗在某种程度上是一种寄生窗口，因为它需要一个宿主（即父窗口）才能弹出。由于其功能与另一个窗口直接关联，它会凭空出现在其父窗口顶部，如 图 8-5 所示。你很可能已经熟悉附窗，因为许多常用应用程序都使用它们——尤其是在处理文件时。

除了打开时看起来很整洁外，附窗还服务于一个有用的目的。由于它们附着于父窗口，因此指示了任务的一个特定范围：即父窗口的范围。换句话说，如果一个附窗出现，你可以确定在关闭附窗之前，你在其中执行的任何操作都与父窗口相关。这是一个细微但重要的区别。

![](img/ea40cad434a338535474e82c1a6ace20_178_0.png)

附窗以特定方式行为——模态（modally）：它接管一个窗口，在用户关闭它之前，不允许用户在父窗口中执行任何其他操作。通常，用户必须做出某种决定后附窗才能被关闭。

实现附窗需要一些特殊的准备。要了解其工作原理，请启动 Xcode 并创建一个新的 Cocoa 应用程序。在项目窗口中，双击 MainMenu.xib 在 Interface Builder 中打开界面，然后执行以下步骤向项目添加附窗：

- 1. 将面板从库（如 图 8-6 所示）拖到你的 MainMenu.xib 文件窗口中。
- 2. 更改面板设置。通过选择 工具->检视器 打开检视器窗口，并取消勾选新面板的所有“样式”和“控件”设置，如 图 8-7 所示。还将新面板的标题更改为 Sheet。
- 3. 打开项目中的默认窗口（名为 Window），并向窗口添加一个 push button；然后，从第 1 步打开新面板，并向其中也添加一个 push button。

在运行时，默认窗口中的按钮会导致面板作为附窗打开。附窗中的按钮会导致附窗关闭。图 8-8 展示了按钮在其各自窗口中的外观。

![](img/ea40cad434a338535474e82c1a6ace20_179_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_180_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_180_1.png)

- 4. **向项目添加一个新对象。**  
  将对象类从库拖到 XIB 窗口（如 图 8-9 所示），并将其命名为 MySheetController。如果你在库中查找对象类有困难，可以通过库窗口底部的搜索字段进行搜索。
- 5. **向对象添加出口（outlets）和动作（actions）。**  
  按 ⌘+6 打开身份检视器，并在身份检视器的类出口（Class Outlets）部分为 `MySheetController` 类添加两个出口。为了跟随示例，将两个出口分别命名为 `theWindow` 和 `theSheet`。同样，为 `MySheetController` 类添加两个动作，并将动作重命名为 `openSheet` 和 `closeSheet`。图 8-10 展示了检视器窗口的外观。
- 6. **连接出口和动作：**
  - a. *从 MySheetController 实例按住 Control 键拖拽到主窗口，并将其连接到 theWindow 出口。*
  - b. *从 MySheetController 实例按住 Control 键拖拽到 MainMenu.xib 中的面板，并将其连接到 theSheet 出口。*
  - c. *从主窗口中的按钮按住 Control 键拖拽到 MySheet Controller 实例，并将其连接到 openSheet 动作。*
  - d. *从 Sheet 面板中的按钮按住 Control 键拖拽到 MySheet Controller 实例，并将其连接到 closeSheet 动作。*

![](img/ea40cad434a338535474e82c1a6ace20_181_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_182_0.png)

**图 8-10：**
向控制器添加出口和动作。

- 7. **创建类文件。**
  - a. *在项目窗口中点击 MySheetController，选择 类->编写文件，并保存为 MySheetController。*
  - b. *确保选中“创建 .h 文件”复选框，如 图 8-11 所示。*
  - c. *点击保存按钮。*

![](img/ea40cad434a338535474e82c1a6ace20_182_1.png)

**图 8-11：**
编写类文件。

- 8. **将新文件添加到 Xcode 项目。**  
  当你为 MySheetController 编写文件时，Interface Builder 会询问你是否要将文件添加到当前的 Xcode 项目（参见 图 8-12）。切换目标项目的复选框并点击添加按钮。
- 9. **退出 Interface Builder 并返回 Xcode，你会发现新文件。**

![](img/ea40cad434a338535474e82c1a6ace20_183_0.png)

**图 8-12：** 将新的类文件添加到 Xcode 项目。

- 10. **调整头文件。**  
  通过添加 **NSObject** 来更改接口定义，在 MySheetController.h 文件中像这样（更改的行以粗体显示）：

```c
#import <Cocoa/Cocoa.h>

@interface MySheetController : NSObject {
IBOutlet id theSheet;
IBOutlet id theWindow;
}
- (IBAction)closeSheet: (id) sender;
- (IBAction)openSheet: (id) sender;
@end
```

- 11. **更改 MySheetController.m 文件。**  
  该文件看起来像这样（更改的行以粗体显示）：

```c
#import "MySheetController.h"

@implementation MySheetController

- (IBAction)closeSheet: (id) sender
{
[theSheet orderOut:nil];
[NSApp endSheet:theSheet];
}

- (IBAction)openSheet: (id) sender
```
