
图 8.10

使用“大小”面板中的“放置”按钮使对象在窗口中居中。选中多个对象时，“放置”按钮上方的“对齐”按钮行处于活动状态。

![](img/2b293e29fc15b0797f113b85dd429b6e_204_0.png)

> **提示**
>
> 你在此示例中不会使用调整大小功能，但你会发现试验此功能很有用。对于在代码中实现自动旋转的 iPhone 应用程序来说，这一点尤其重要；关闭锚点和自动调整大小选项会强制视图中的对象自动旋转并重新定位自身。

你几乎完成了视图编辑。将左侧按钮编辑为显示“开始”，将右侧按钮文本编辑为显示“停止”。保存文件。现在你可以开始将 nib 中的对象链接到新的支持代码。

> **提示**
>
> 此时你可以构建并运行应用程序。加载后，你会看到窗口包含新对象。你可以点击这些按钮。它们会像通常的 Aqua 风格那样短暂变暗，但由于它们没有连接到代码，所以什么也不会发生。

## 理解链接、出口和动作

当你将 nib 对象链接到代码时，nib 中的每个活动对象都必须在代码中有对应对象。在此示例 nib 中，有两个按钮和一个文本字段，因此你必须在代码中声明两个按钮对象和一个文本字段对象。如前所述，“哑”的非交互对象不需要代码，但活动对象必须有一个代码对应对象，并且你必须将该对应对象链接到 IB 中与其关联的对象。

链接有两个端点和两种类型。出口用于读取和设置对象属性。动作用于响应消息。在代码端，出口使用 `IBOutlet` 指令定义。动作使用 `IBAction` 定义，但这并不总是强制要求。在 nib 文件端，链接使用可视化链接工具定义。

图 8.11 说明了出口和动作的用法。出口在代码中引用的对象与 nib 文件中的对象之间定义唯一链接。出口在链接的每一端恰好有一个对象。动作只有一个目标——一个事件处理方法——但可以由多个来源触发。

图 8.11

出口和动作的典型设计模式。此图展示了最简单、最常见的设计模式。也支持更复杂的模式；例如，接收到的动作在对象内部处理，而不是发送给另一个对象。

![](img/2b293e29fc15b0797f113b85dd429b6e_205_0.png)

> **提示**
>
> 从技术上讲，`IBOutlet` 告诉编译器在编译时让指针保持未定义。Cocoa 的 nib 加载器会在 nib 加载时于运行时返回该值。`IBAction` 是方法占位符。Objective-C 在运行时计算所有方法地址，因此该指令主要是为了清晰。

### 使用 IBOutlet 和 IBAction

要创建出口，请将 `IBOutlet` 指令插入对象的属性声明中。将

```objc
@property (assign) AClass *anInstance;
```

替换为

```objc
@property (assign) IBOutlet AClass *anInstance;
```

这就是所需的全部操作。其余过程在 IB 中完成。

![](img/2b293e29fc15b0797f113b85dd429b6e_206_0.png)

> **提示**
>
> 尽管创建出口非常简单，但可能更难记住你需要这样做。如果你遵循图 8.2 中的检查清单，就不会忘记。

`IBAction` 更复杂。在某些情况下，`IBAction` 指令是可选的，常规的 `void` 方法可以作为可接受的替代。此功能在 iPhone 和 OS X 上的实现方式不同。在 Mac 上，只要方法具有以下签名，Interface Builder 就会将其识别为 `IBAction`：

```objc
-(void) methodName: (id) sender;
```

你不需要将 `void` 替换为 `IBAction`，但动作必须具有此签名才能被识别。不允许任何变体。sender 参数持有指向触发消息的对象的指针。接下来描述动作。

此自动识别功能未在 iPhone 上实现。你必须包含 `IBAction` 指令。不过，你可以指定不带参数的动作。例如：

```objc
- (IBAction) methodName;
```

仅在 iPhone 上有效。`sender` 参数会被丢弃。

![](img/2b293e29fc15b0797f113b85dd429b6e_206_1.png)

> **注意**
>
> 有关 `sender` 的更多信息将在本章后面出现。

### 在接口中定义出口和动作

为了让应用程序尽可能简单，你将在应用程序委托中实现计数器。在典型应用程序中，委托会保留用于系统消息，而计数器功能会在子类化的窗口或自定义视图中实现。在实践中，这意味着至少要对一个额外对象进行子类化，并且不会给应用程序的功能或效率带来任何提升。仅在本示例中，你将把支持代码保留在委托中。

点击 CounterAppDelegate.h。已定义指向窗口对象的出口，因此你可以看到正确语法的示例。如下所示，为 `NSTextField` 和两个 `NSButtonCell` 对象添加声明：

```objc
#import <Cocoa/Cocoa.h>
@interface TimerAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    NSButtonCell *startButton;
    NSButtonCell *stopButton;
    NSTextField *countText;
}
@property (assign) IBOutlet NSWindow *window;
@property (assign) IBOutlet NSButtonCell *startButton;
@property (assign) IBOutlet NSButtonCell *stopButton;
@property (assign) IBOutlet NSTextField *countText;
@end
```

> **注意**
>
> 你创建的是指向按钮单元格对象的出口，而不是指向按钮对象，因为在许多 IB 对象（包括按钮组）中，单元格对象才是活动且可编辑的元素。只有修改按钮内部的单元格对象，才能设置按钮的文本。然而，这条经验法则并不完全一致。文本字段包含一个单元格，但忽略它并通过直接指向字段本身的出口来设置文本会更容易。

如何知道 nib 中对象的名称？名称列在“文档”窗口的右列中，如图 8.12 所示。点击 Window (Counter) 及其所有子对象的展开三角形。“类型”列会列出对象名称。当你向 nib 添加对象时，如果还不知道它们的名称，可以使用此功能读取名称。

> **注意**
>
> 虽然必须使用标准 Cocoa 对象名称，但你可以自由选择指针名称。本示例为清晰起见使用了自解释的名称，但这些名称是任意的。

图 8.12

要查找对象名称，请查看“类型”列。在代码中创建出口时，必须使用相同的对象名称。

![](img/2b293e29fc15b0797f113b85dd429b6e_207_0.png)

你还需要定义三个动作方法——一个由按钮触发以开始计数，一个用于停止计数，一个用于重置计数。在属性声明之后、@end 指令之前添加这三个签名：

```objc
- (void) startCount: (id) sender;
- (void) stopCount: (id) sender;
- (void) resetCount: (id) sender;
```

至此接口完成，如图 8.13 所示。选择“文件”⇨“保存”以保存文件。

图 8.13

计时器项目的已完成接口。出口和动作已定义，但尚未实现。

![](img/2b293e29fc15b0797f113b85dd429b6e_208_0.png)

> **注意**
>
> 尽管有三个方法，但只有两个按钮。在本示例中，我将演示如何动态切换方法，重新编程一个按钮，使其根据计时器的状态触发两个不同的方法。创建单独的重置按钮同样实用，但动态选项更强大。

### 在实现中定义出口和动作

要完成代码的第一阶段，你将把新对象添加到实现中，并为新方法创建方法存根。在开发工作流的这个阶段，你有两个选择：你可以创建一个充满存根的原型实现，在 Interface Builder 中向其添加链接，然后返回代码完成实现；或者你可以编写代码的初稿，在 Interface Builder 中添加链接，并运行测试构建。

两种方法都有效，但第一种更简单、更易管理，因为你可以分阶段添加代码功能，分别实现和测试每个方法和每个事件。第二种方法更适合使用从现有应用程序复制的可用代码来实现处理程序方法。这里你将使用第一种方法。

在 Xcode 中选择 CounterAppDelegate.m。首先将新指针添加到文件中的 @synthesize 指令。接下来，为每个方法添加一个存根。最终实现应如下所示：

```objectivec
#import "CounterAppDelegate.h"
@implementation CounterAppDelegate
@synthesize window, startButton, stopButton, countText;
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    // Insert code here to initialize your application
}
- (void) startCount: (id) sender{
}
- (void) stopCount: (id) sender{
}
- (void) resetCount: (id) sender{
}
@end
```

保存文件。现在你可以开始将代码链接到 Interface Builder 中的对象。以下是你到目前为止所做工作的回顾：

1. 为 nib 中的每个“活动”对象添加了一个对象
2. 为这些对象创建了指针
3. 为每个对象添加了 IBOutlet 指令
4. 在接口中定义了一些动作方法
5. 为每个方法创建了存根实现

此检查清单是创建可供链接的代码端对象所需的最低要求。如你所见，这并不是一个优雅或简单的过程——而且当你完成 nib 端的链接后，还有更多阶段要进行。不幸的是，处理 nib 文件没有其他方法。每当你设计 nib 并为其创建支持代码时，都必须仔细完成这些步骤。通过练习，这个过程会变得更容易。

