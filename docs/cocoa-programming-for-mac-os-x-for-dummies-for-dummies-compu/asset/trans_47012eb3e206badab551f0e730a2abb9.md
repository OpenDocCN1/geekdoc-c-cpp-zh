
虽然您的代码显示的数字与运行时在界面中输入的实际数值非常接近，但它们并非精确的值。显然，您需要一种根据某些指南来格式化数字的解决方案。例如，您可能只关心两位小数的精度。

## 修正代码

不深入技术细节，浮点变量值的十进制部分可以有很多位数字。当 num1、num2 或它们的和拥有无法用二进制非循环序列表示的小数位时，就会存在舍入和截断问题。这些问题是基于计算机处理浮点数字的方式所固有的现实情况。

为了解决这个问题，一种解决方案是在显示答案之前对其进行格式化。Cocoa 的 NSNumberFormatter 类中有几行代码可以解决这个问题：

```
NSNumber *answerFormatter =
[[NSNumberFormatter alloc] init] autorelease];
[answerFormatter
setFormat:@"#,###.00;0.00; (###0)"];
[answerField cell setFormat:answerFormatter];
```

如果您看不懂这一大段令人望而生畏的代码，请不要感到害怕。这一章的主题是 Xcode，而不是像第 6 章那样的 Objective-C 代码。

前两行代码（顺便一提，它们只是出现在两行上的一个函数）创建了一个 NSNumberFormatter 对象。NSNumberFormatter 对象的目的是调节数字的格式。

接下来，代码向 answerFormatter 对象发送 setFormat 消息，并传递一个文本字符串。这个字符串指定了这个 NSNumberFormatter 对象允许哪些格式。该字符串包含三种格式，每种格式由分号分隔。您不必担心这三个字符串的具体格式，但为了提个醒，第一个定义正数的格式，第二个处理数字为 0 的情况，最后一个格式化负数。

最后，代码将 NSNumberFormatter 应用于界面中的 answerField。为了帮助您理解这段代码在整个大图景中的位置，以下是 Fusebox.m 完整源代码的列表（NSNumberFormatter 对象以粗体显示）。请注意，当您添加代码时，最后一个断点会相应移动。

```
@import "Fusebox.h"

@implementation Fusebox

-(IBAction)calculateAnswer:(id) sender {
    float num1,num2, floatValue;
    num1 = [numberField1 floatValue];
    num2 = [numberField2 floatValue];
    answer = num1 + num2;
    NSNumberFormatter *answerFormatter =
        [[NSNumberFormatter alloc] init] autorelease];

    [answerFormatter
        setFormat:@"##,##.0.00; (#,##.00)"];
    [answerField cell setFormatter:answerFormatter];

    [answerField setFloatValue:answer];

}
@end
```

现在您已经正确格式化了 answerField，请选择 Build > Build 并运行（Go to see your changes in action -> 选择“构建” > “构建并运行”以查看您的更改效果，直译保留原意即可，这里意译为：选择 Build > Build 并运行以查看您的更改效果）。您会看到结果，如**图 3-11** 所示。

**图 3-11**：使用 NSFormatter 对象，您可以指定应用程序如何显示浮点数。

![](img/ea40cad434a338535474e82c1a6ace20_75_0.png)

在您离开本章的调试部分之前，使用 Xcode 编写 Cocoa 应用程序时，您可能会遇到一种错误。将 Fusebox.m 中代码的最后一行更改为此：

```
[answerField setFloatValue:answer];
```

这次您故意遗漏了末尾的分号（这是一个即使专业开发人员也会犯下的常见错误）。选择 Build: Build 并运行（Go -> “构建”并“运行”）以查看会发生什么。结果是应用程序未按预期运行，并且在相关代码下方出现了一个错误叠加层，如**图 3-12** 所示。在代码左侧发生错误的地方的槽位中，还会出现一个带有白色 X 的圆圈。

![](img/ea40cad434a338535474e82c1a6ace20_76_0.png)

该错误准确地指出了问题的所在。在这种情况下，错误是 `}` 标记之前的语法错误。分号应该正好在 `}` 标记之前。修正代码并保存。

这个演示的要点是表明，当使用 Xcode 编程时，您可能会遇到不同类型的错误。有些错误（如本例所示）发生在构建和调试过程中，Xcode 会显示发生错误的位置。其他 bug 更难以追踪，例如前面的例子，因为应用程序在其他方面是功能正常的。对于这些情况，使用内置调试器来解决问题总是有益的。

## 移除断点

既然您已经完成了项目的调试，您可能希望移除已添加的断点。在 Xcode 中，查看 Fusebox.m 文件，并寻找代码编辑器左侧的断点。控制+单击（Control+click）一个断点，并从出现的上下文菜单中选择“移除断点”（remove Breakpoint）。对其余的断点执行相同的操作。**图 3-13** 显示了删除断点之前的上下文菜单。

> **提示** 允许您保留项目中设置的断点。您可以安全地保留它们而不给自己造成任何问题，只要您在不需要它们时停用它们即可。

![](img/ea40cad434a338535474e82c1a6ace20_77_0.png)

**图 3-13**：控制+单击（Control+ click）一个断点以移除它。

![](img/ea40cad434a338535474e82c1a6ace20_77_1.png)

## 去哪里寻求帮助

在某个时候，您将希望获取有关 Xcode 如何工作的更多信息。坦率地说，Apple 通过其内置文档已经为您提供了支持。选择 Help > Xcode Workspace Guide 以查看有关 Xcode 的内置文档。

内置帮助提供了关于 Mac OS X 开发各个方面的文档。它还包含有用的教程，帮助您开始使用 Xcode 进行 Cocoa 编程。

除了标准的帮助之外，Xcode 在代码编辑器中还提供了对 Cocoa 类和框架信息的一键访问。要测试此功能，请执行以下操作：

1.  选择 Fusebox.m 源代码。

    Xcode 在代码编辑器中显示该文件。

2.  定位源代码中您想要调查的关键字。

    例如，您可能想要了解 `setFloatValue` 方法。

3.  按住 Option 键，在 Fusebox.m 文件中双击 setFormatter。

    一个引用窗口打开，列出了 Cocoa 中各种 `setFloatValue` 方法（参见**图 3-14**）。

4.  从菜单中选择一个关键字。

    选择适当的 `setFloatValue` 方法以查看相应的文档。

![](img/ea40cad434a338535474e82c1a6ace20_78_0.png)

## 构建应用程序

现在您已经配置好项目，修改了其源代码，并浏览了其中的类，您已准备好构建最终的应用程序。选择 Build+ 和 Go。然后，Xcode 将编译、链接并执行生成的应用程序。

![](img/ea40cad434a338535474e82c1a6ace20_79_0.png)

您不一定非要构建并运行，尽管这可能是在 Xcode 中最常见的工作方式。您可以通过选择 Build+ Build 来构建项目而不运行它。这会编译、链接并创建目标应用程序，但不执行它。如果您更喜欢使用调试器，请选择 Build+ 和 Debug。**表 3-1** 列出了各种 Build 命令的键盘快捷键。

| 功能 | 键盘快捷键 | 它的作用 |
| :--- | :--- | :--- |
| Build | Cmd+B | 从当前项目构建应用程序 |
| Build and Run | Cmd+R | 构建应用程序然后执行它 |
| Build and Debug | Cmd+Y | 从当前项目构建并启动应用程序，然后启动调试器 |
| Clean | Cmd+Shift+K | 通过移除所有目标代码来清理当前项目 |

在标准菜单项和相应的键盘快捷键中，Xcode 通过工具栏项目窗口中的按钮为您提供对 Build 和 Run 功能的轻松访问。**图 3-15** 显示了此按钮的位置和功能。

每当您点击 Build and Go 工具栏按钮时，它会变成一个停止标志。在构建或调试过程中，您可以停止该进程。有时构建完成需要一段时间。如果您在构建之前忘记做某事，能够停止构建操作会非常方便。这样，您可以避免等待构建完成，并返回工作。

在成功完成构建后，您的新应用程序将出现在 Finder 中项目主文件夹的 Build 文件夹中。然后，您可以在任何使用 Mac OS X 的其他计算机上分发和运行此应用程序，这正是使用 Cocoa 进行编程的主要目标。

