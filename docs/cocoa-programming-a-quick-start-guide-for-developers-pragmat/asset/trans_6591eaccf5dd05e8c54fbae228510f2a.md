
通常应如何表现。它不可能知道任何特定应用程序应如何表现。一种解决方案是让我们继承 NSApplication，并用自定义行为重写相应方法。在 Cocoa 应用程序中，我们往往采用不同的方法。我们为 NSApplication 指定一个委托对象，并且只实现需要实现的方法。那么什么是委托？你可以把它看作一个助手类，主类会把工作交给它。当主类（在这里是 Application）需要完成某项工作时，它会调用其委托类中的方法。

幸运的是，Cocoa Application 模板为我们创建了一个名为 HelloWorldAppDelegate 的应用程序委托。你可以在 Groups & Files 下的 Classes 文件夹中找到源文件。²

- HelloWorld
  - Classes
    - HelloWorldAppDelegate.h
    - HelloWorldAppDelegate.m
  - Other Sources
  - Resources
  - Frameworks
  - Products

Cocoa Application 模板创建了文件 HelloWorldAppDelegate.h 和 HelloWorldAppDelegate.m，这两个文件共同定义了类 HelloWorldAppDelegate。

在 HelloWorldAppDelegate.m 内部，有一个名为 applicationDidFinishLaunching: 的方法，其中包含以下注释：

```
// Insert code here to initialize your application
```

用日志行替换该注释，如下所示：

[下载 Classes/HelloWorld/HelloWorldAppDelegate.m](#)

```objc
#import "HelloWorldAppDelegate.h"
@implementation HelloWorldAppDelegate
@synthesize window;

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSLog(@"Hello, World!");
}
@end
```

² 如果你找不到这些文件，你使用的可能是 Xcode 3.1 或更早版本，需要升级到 Xcode 3.2 或更高版本。

这个方法究竟是如何被调用的？我们并没有从 main() 中显式调用它。事实上，我们没有从任何地方显式调用它。

简单解释是：在运行时，应用程序完成启动后，应用程序对象会向它的委托发送 applicationDidFinishLaunching 消息。稍微详细一点的解释就是你在上一章看到的内容：如果委托没有实现这个方法，那么调用它时就会出现运行时错误。所以，真正发生的情况是：应用程序对象会检查并确保委托实现了该方法；如果实现了，它才发送消息。

![](img/9355405953264484a02198b0e3d25b7e_65_0.png)

要运行应用程序，首先通过“运行 > 控制台”或 ⇧ ⌘ R 显示控制台。接下来，通过选择“运行 > 清除控制台”、按下 ⌃ ⌘ R，或在可见时点击“清除控制台”按钮来清空控制台。最后，点击“构建并运行”（或使用其键盘快捷键 ⌘R）。

HelloWorld 应该会启动，出现一个空窗口，控制台应包含一行表示会话开始时间的内容，后面跟着一行带有时间戳、进程 ID 和我们创建的字符串的内容。我的看起来像这样：

```
HelloWorld[19673:10b] Hello, world!
```

稍微欣赏一下你的成果后，就可以退出 HelloWorld，回去继续工作了。

### 4.3 使用现有类

我们已经有了一个能漂亮地打印到控制台的“Hello, World”应用。下一步，我们将在代码中创建一个文本字段，将它添加到窗口中，稍作配置，然后在这个文本字段中显示“Hello, World!”。记住，我们的目标并不是在文本字段中打印出“Hello, World!”。如果那只是我们唯一的目标，我们完全可以直接从 Interface Builder 的库中拖出该控件，然后输入短语 *Hello, World!*³。Interface Builder 的经验法则很简单：只要能用 Interface Builder，就应该使用 Interface Builder。你在 Interface Builder 中能做的事情，没有什么是代码做不到的。除了非常特殊的情况，没有任何理由避免使用 Interface Builder。

本节就是这种特殊情况之一。本节的目标是积累使用代码来实例化、配置和使用一个并非由我们编写的类的经验。之后，我们就准备好创建并使用自己的类了。

为了让事情稍微简单一些，双击 MainMenu.xib 启动 Interface Builder，选择你的窗口，并使用大小检查器将窗口宽度设为 580、高度设为 90。遗憾的是，如果点击窗口内部，很容易误选视图。如果点击窗口的标题栏，那么大小检查器的标题栏应显示 *窗口大小*。

我也将窗口的最大和最小尺寸设为了这些尺寸，这样用户就无法调整窗口大小。这些尺寸没有什么神奇之处，但当我们创建并放置标签时，知道窗口尺寸会对我们有帮助。

那么，回想一下在我们的 SimpleBrowser 示例中，将文本字段放到窗口顶部时发生了什么。你从库中抓取一个文本字段，把它拖到窗口上并放下。它会自动添加到视图层级中。你的 Document 窗口看起来大致如下：

![](img/9355405953264484a02198b0e3d25b7e_66_0.png)

³ 在本例中用代码创建文本字段的一个附带好处是，它应该有助于说服你尽可能使用 Interface Builder。

尽管你当时可能没有注意，但窗口包含一个 ContentView。当你将文本字段拖放到窗口上时，你创建了一个 NSTextField 实例，并将它作为 ContentView 的子视图添加进去。

然后你重新定位了文本字段，并更改文本以显示你想要的内容。下面是我们可能在代码中这样做的方式：⁴

下载类：HelloWorld2/HelloWorldAppDelegate.m

```objc
#import "HelloWorldAppDelegate.h"
@implementation HelloWorldAppDelegate
@synthesize window;

-(void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSRect    labelLocation = NSMakeRect(20, 20, 540, 50);
    NSTextField *label = [[NSTextField alloc] initWithFrame:labelLocation];
    [label setStringValue:@"Hello, World!"];
    [[self.window contentView] addSubview:label];
}
@end
```

首先，我们创建一个 NSRect，用于保存标签的大小和位置信息。这与我们在第 2 章 *使用现有内容*（第 24 页）中使用 Interface Builder 所做的工作一致：当时我们调整了文本字段的大小，或在大小检查器中设置了它的尺寸。注意，NSMakeRect() 是一个 C 函数，而不是方法。在处理图形元素时，这相当典型。尽管现在这些信息肯定太多了，但 NSRect 或 NSPoint 是 C 结构体，而不是 Objective-C 对象。总会有相应的 C 函数（例如 NSMakeRect() 或 NSMakePoint()）来创建和配置这些元素。

接下来，我们创建一个名为 label 的 NSTextField 实例，并将其位置和尺寸设置为 labelLocation 变量所描述的值。我们将标签的字符串值设为 Hello, World!，并将该标签作为窗口内容视图的子视图添加进去。

---

⁴ 目前我假设你明白 *self.window* 指的是当前对象的窗口实例。我会在第 5 章 *实例变量与属性*（第 86 页）中解释点语法。

点击“构建并运行”，你应该会看到类似下面的内容：

![](img/9355405953264484a02198b0e3d25b7e_68_0.png)

我对这个项目当前的状态不太满意。当然，输出看起来很难看，我们会修正这一点，但我主要关心的是代码的状态。我们来稍微重构一下。

### 4.4 重构代码

时不时地从代码中退后一步，看看哪些地方需要清理，会很有帮助。现在我看了看，我不喜欢 labelLocation 这个名字。当然，我们完全可以去掉这个变量，直接内联创建 NSRect，而不使用解释性的临时变量。那会是一种解决方案。

如果我们改为选择重命名这个变量，那么需要考虑到它不仅是标签的位置，还包括标签的大小。你可能已经从方法名 initWithFrame 猜到，这两部分信息被收集在一个 NSRect 中，称为 frame（框架）。

让我们使用 Xcode 将变量名从 labelLocation 改为 labelFrame。在这种情况下，手动进行更改已经足够简单，但我想向你介绍如何使用 Xcode 执行几项重构。

我不知道你是否已经注意到，但当你点击 labelLocation 时（来吧，点一下它），所有 labelLocation 实例都会带下划线。⁵ 如果你将鼠标悬停在已选中的 labelLocation 周围、稍微靠右的位置，就会出现一个下拉箭头。这与你悬停在 Mail.app 中阅读的电子邮件里的电话号码或地址上时看到的界面相同。点击这个箭头，你应该会看到这里显示的选项：

```objc
-(void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    NSRect labelLocation = NSMakeRect(..., ..., ..., 50);
    NSTextField *label = [[NSTextField alloc] initWithFrame:labelLocation];
    [label setStringValue:...];
    [self.window addSubview:label];
}
```

⁵ 这里 labelLocation 只出现了一次，但你明白意思。

