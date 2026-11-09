
因此，我们不再使用这个：

```
[[NSString alloc] initWithFormat:@"Hello, %@!", self.name]
```

而是使用下面这个：

```
[NSString stringWithFormat:@"Hello, %@!", self.name]
```

这两个版本并不完全相同。我们来回顾一下我们的规则。

如果使用第一个版本创建字符串，那么你就拥有它，并负责释放它。当我们使用 alloc 时，我们会将引用计数加一，并且需要通过调用 release 或使用自动释放机制来释放该字符串。

另一方面，规则对于使用第二种方法创建的对象是怎么说的？我们没有显式使用 alloc 或 new 来创建字符串，也没有使用 retain 或 copy 来持有它。因此，我们不拥有它。

`stringWithFormat:` 被称为便利构造器，因为它用于创建并初始化一个对象，并将其已经自动释放后返回给我们。换句话说，下面这个：

```
[NSString stringWithFormat:@"Hello, %@!", self.name]
```

等价于这个：

```
[[[NSString alloc] initWithFormat:@"Hello, %@!", self.name] autorelease]
```

### 6.13 练习：创建并使用便利构造器

为 Greeter 类创建你自己的便利构造器，命名为 `greeterWithName:`。你需要在 Greeter.h 中声明它，并在 Greeter.m 中实现它。

重构 FlashlightAppDelegate.m 中的 `applicationDidFinishLaunching:` 方法，使用这个方法创建 Greeter 类的实例。在你完成向控制台写入之后，Greeter 将被自动释放，并且 Greeter 的 `dealloc` 方法将被调用。

## 第 7 章：出口与动作

Cocoa 编程使用模型-视图-控制器（MVC）将应用程序逻辑与外观和体验分离。对于模型，我们将使用 Xcode 以 Objective-C 创建应用程序逻辑。你已经看到如何使用 Interface Builder 创建视图。

控制器是模型与视图之间的桥梁。当用户点击按钮、在文本字段中输入，或对视图做任何操作时，控制器会响应这些动作，通常是通过向模型发送消息。同样，当模型发生变化时，控制器会更新视图，以便这些变化对用户可见。

控制器必须同时涉足两个世界。有一个类文件，你用它创建方法并向模型或视图发送消息。我们将在 Interface Builder 中创建控制器类的实例。这为我们提供了控制器的可视化表示，它存在于一个 nib 中，你用这个 nib 将控制器代码连接到你在 IB 中创建的可视组件。这有点像控制器的真实版本生活在代码中，而它的化身生活在 IB 中。

你将在下一章为我们的 Simple Browser 创建一个控制器。在本章中，我们将研究如何从 Interface Builder 中创建的那些 GUI 元素与你的代码通信，以及你的代码如何更改 GUI。一旦你熟悉了这些动作和出口，你会发现自己一直在使用它们。¹

1. 尽管我们从出口和动作的这种简单视图开始，但随着深入，我们会以更复杂的方式使用它们。

### 7.1 总体概览

设想我们有一个窗口，里面有一个按钮和一个文本字段。当用户点击按钮时，我们将在文本字段中显示“Hello, World!”。我们需要一种方法将按钮连接到代码，这样当按钮被点击时，我们的代码中会调用一个方法来完成工作。我们还需要某种连接回文本字段的方式，以便将其文本设置为“Hello, World!”

控制器连接到 UI 元素基本上有两种方式：

- **动作（Actions）：** 当按钮之类的元素想要发起由控制器执行的动作时使用的控制器方法
- **出口（Outlets）：** 指向控制器需要向其发送消息的 UI 元素的控制器实例变量

动作和出口是专门为 Interface Builder 中创建的连接而设计的。下面是基本流程。

![](img/9355405953264484a02198b0e3d25b7e_124_0.png)

当用户点击按钮时，会向指定的目标发送一条消息，以发起特定的动作。你在控制器中创建这个目标动作，并在 Interface Builder 中进行连接。动作只是一个在按钮被点击时会被调用的方法。

有时控制器需要与你使用 IB 创建的对象通信。一种方法是给控制器一个指向该对象的句柄。设想我们的控制器有一个出口，它是一个文本字段。换句话说，控制器有一个指向该文本字段的实例变量。就像墙上的插座一样，出口是控制器中的一个位置，可视化元素可以插入其中。

### 7.2 使用出口

使用 Cocoa Application 模板创建一个新项目，取消选中所有复选框，并将其命名为 HelloWorldPro。

将这一行添加到 HelloWorldProAppDelegate.m：

```
Download Outlets/HelloWorldPro/HelloWorldProAppDelegate.m

#import "HelloWorldProAppDelegate.h"

@implementation HelloWorldProAppDelegate

@synthesize window;
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    self.window.backgroundColor = [NSColor greenColor];
}
@end
```

点击 Build & Run，你的窗口应该会出现，背景色设置为绿色。这是怎么发生的？我们向 window 属性发送了一条消息来更改其背景色。那条消息是如何传达到作为 nib 文件一部分的实际 NSWindow 的？

要实现这一点，有两个重要步骤。首先，查看 HelloWorldProAppDelegate 类的头文件：

```
Download Outlets/HelloWorldPro/HelloWorldProAppDelegate.h

#import <Cocoa/Cocoa.h>

@interface HelloWorldProAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
}
@property (assign) IBOutlet NSWindow *window;
@end
```

你看到 IBOutlet 关键字被塞进 window 的 @property 声明中间了吗？这告诉 Interface Builder 将 window 包含在 HelloWorldProAppDelegate 每个实例的出口列表中。

双击 MainMenu.xib 文件（记住你可以在 Resources 下找到它）。当 nib 在 Interface Builder 中打开时，查看 Document 窗口，并选择 HelloWorldProAppDelegate 类的实例。²

2. 如果 Document 窗口不可见，你始终可以使用 ⌘0 或 Window > Document 将其调出。

![](img/9355405953264484a02198b0e3d25b7e_126_0.png)

![](img/9355405953264484a02198b0e3d25b7e_126_1.png)

打开它的 Connections inspector（Tools > Connections inspector）。window 出口已经连接到同一个 nib 中的 NSWindow 对象。

![](img/9355405953264484a02198b0e3d25b7e_126_2.png)

如果你愿意，也可以查看 NSWindow 对象的连接，你会看到 window 被列为引用出口。

因此，你可以这样想象事件顺序。我们在 HelloWorldProAppDelegate 类中有一个 window 变量和属性。我们有一个 nib，其中包含 HelloWorldProAppDelegate 的一个实例和 NSWindow 的一个实例。

![](img/9355405953264484a02198b0e3d25b7e_126_3.png)

![](img/9355405953264484a02198b0e3d25b7e_126_4.png)

window 属性隐藏在 HelloWorldProAppDelegate 内部。你在上一章看到我们可以在代码中访问该属性，但如何在 Interface Builder 中连接到它？第一步是将该属性标记为 IBOutlet。我把这个 outlet 想象成……上的一个把手

在文本字段中对文本进行两端对齐，使用 Attributes inspector 调整字体大小，并保存你的工作。

为 HelloWorldProAppDelegate 的头文件中的该文本字段添加一个新属性，并将其声明为出口。在应用程序启动后，使用该出口打印“Hello, World!”。

回到 Interface Builder，将该出口连接到文本字段。

点击 Build & Run，你应该会看到窗口中有一个绿色背景，上面有一个文本字段，显示消息“Hello, World!”

### 7.4 解决方案：创建并使用出口

使用 Xcode 和 Interface Builder 是有节奏的。你会在它们之间来回切换。你应该已经毫无困难地在 Interface Builder 中拖入一个文本字段并将其定位到窗口中。在回到 Xcode 之前，查看 HelloWorldProAppDelegate 的 Connections inspector。它应该和之前看起来完全一样，只有一个处于活动连接状态的出口。

接下来的部分挺酷的。将下面两行高亮行添加到你的头文件中：

```objective-c
#import <Cocoa/Cocoa.h>

@interface HelloWorldProAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    NSTextField *textField;
}
@property (assign) IBOutlet NSWindow *window;
@property (assign) IBOutlet NSTextField *textField;
@end
```

你已经向 HelloWorldProAppDelegate 添加了一个名为 textField 的实例变量，并声明了相应的属性。但对我们当前目的更重要的是，你已经将 textField 标记为出口。保存头文件，然后在 Interface Builder 中点击回 Connections inspector。

你看到了吗？
