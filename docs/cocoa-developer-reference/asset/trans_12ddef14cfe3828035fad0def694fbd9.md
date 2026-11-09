
图 19.22 中所示的*基于窗口的应用*模板包含一个应用委托及关联的 nib 文件，其中包含一个 `UIWindow` 实例。该模板是最基础（skeletal）的，并且没有视图控制器。你可以使用它来构建尽可能少占用内存的微型应用，直接将额外的功能、输出口（outlet）和动作方法添加到应用委托中。

你也可以将此模板作为使用导航控制器或标签栏的应用的起点。一般来说，对于这些应用类型，从其他预建模板开始更容易；但如果你的应用有独特的导航需求，从头构建它们可能更简单。

**图 19.22**

基于窗口的应用模板类似于基于视图的应用模板，但没有额外的控制器——没有它，就无法交换视图。

![](img/2b293e29fc15b0797f113b85dd429b6e_545_0.png)

## 构建一个简单的应用

既然你已经了解了 iOS 的关键特性，现在可以创建你的第一个应用了。这个应用比“Hello World”应用更复杂；它演示了如何使用简单功能构建视图，以及如何实现视图交换。

### 添加视图控制器子类

空白的灰色视图并不令人兴奋，但你即将改变这一点。你的新应用将有两个视图，并通过按钮在它们之间切换。首先创建 `UIViewController` 的两个新子类来容纳额外的视图。许多应用都使用 `UIViewController` 的子类，因此它包含在 Xcode 的文件模板列表中，并可以选择使用新类文件创建新的 nib 文件。

右键单击 Classes 文件夹，然后选择 Add > New File。在左上角选择 Cocoa Touch Class，并单击 UIViewController subclass 文件模板。确保选中 With Xib for user interface 选项。

单击 Next，并将新类保存为 `AViewController`。Xcode 会将其连同 nib 文件一起添加到项目中。重复此操作，添加另一个名为 `BViewController` 的新类，并带有其自己的独立 nib。

应用现在有三个视图控制器和三个 nib 文件——由模板生成的带有空白视图的原始控制器，以及两个新的视图控制器，如图 19.24 所示。对于一个双视图应用来说，三个控制器似乎有些多余，但它简化了项目。优点包括：

- **简化内存管理。** 视图控制器类在被释放后不能持有指向自身或其属性的指针。根控制器在管理其他视图时充当方便的指针存储，从而可以安全地释放它们。
- **简化事件处理。** 你可以将管理用户事件的代码包含在其视图控制器中，也可以让响应者链将它们传递给根控制器。这可以简化事件处理；与显式委托相比，编码更容易，而且“它就能正常工作”。
- **简化数据存储。** 尽管这并不完全符合官方的模型-视图-控制器（MVC）模式，但你可以向根控制器添加数据存储区或数据存储区接口，以管理应用的全部数据需求。

### 实现视图控制器

牢记这种设计模式后，你就可以开始编写应用代码了。首先，将额外的视图控制器作为属性添加到根控制器的头文件中。包含一个名为 `showBView:` 的动作方法，用于触发初始视图交换。

```objectivec
@class AViewController;
@class BViewController;
@interface FirstAppViewController : UIViewController {
    AViewController *aViewController;
    BViewController *bViewController;
}
@property (nonatomic, retain) AViewController *aViewController;
@property (nonatomic, retain) BViewController *bViewController;
- (IBAction) showBView: (id) sender;
@end
```

**图 19.24**

应用的完整类和资源列表包括一个应用委托、三个视图控制器类和四个 nib 文件。许多应用使用类似的设计，因此你可能希望保存此项目以便重用。

![](img/2b293e29fc15b0797f113b85dd429b6e_548_0.png)

在实现文件中，添加启动代码，释放原始的空灰色视图，并用 `AViewController.xib` 的内容替换它。这段代码位于根控制器的 `viewDidLoad` 方法中，该方法大致相当于 Cocoa 项目中的 `awakeFromNib`。

```objectivec
#import "FirstAppViewController.h"
#import "AViewController.h"
#import "BViewController.h"
@implementation FirstAppViewController
@synthesize aViewController, bViewController;
- (void)viewDidLoad {
    //Load the first view to replace the default view in the root
    //controller nib
    self.aViewController = [[AViewController alloc]
        initWithNibName: @"AViewController" bundle: nil];
    [self.view release];
    [self.view insertSubview:aViewController.view atIndex:0];
}
```

如果你保存新的 nib，构建并运行应用，它将加载并显示 AView nib 设计，如图 19.26 所示。

**图 19.26**

运行应用会加载新的 nib 并显示它。

![](img/2b293e29fc15b0797f113b85dd429b6e_550_0.png)

新按钮仍未关联。点击时它会闪烁，但不执行任何操作。要解决此问题，请向 `FirstAppViewController.m` 添加 `showBView:` 方法，并编写加载和显示 B 视图的代码。

```objectivec
- (IBAction) showBView: (id) sender
{
    self.bViewController = [[BViewController alloc] initWithNibName:
        @"BViewController" bundle:nil];
    [aViewController.view removeFromSuperview];
    [self.view insertSubview:bViewController.view atIndex:0];
}
```

这几乎与 `viewDidLoad` 中的代码相同。它加载 BViewController nib 文件，然后调用 `removeFromSuperview` 将之前可见的视图从视图数组中取消关联并释放它。最后一行将 B 视图插入层次结构中以便显示。

保存文件，然后在 Interface Builder 中选择 File▸ Reload All Class Files，以将新的 `showBView:` 方法添加为可关联的动作。单击视图中的圆角矩形按钮以选择它。在 Inspector 窗口中单击 Connections 选项卡，以显示事件列表。将按钮的 Touch Down 事件关联到 First Responder 对象，如图 19.27 所示。当浮动弹出菜单出现时，从中选择 `showBView:` 方法。

**图 19.27**

将按钮事件关联到 First Responder，它绕过类控制器并将事件发送到应用的根视图控制器。

![](img/2b293e29fc15b0797f113b85dd429b6e_551_0.png)

### 警告

用户事件列表是 UIKit 中的标准功能。对象在 IB 中显示完整列表，但大多数对象仅生成部分事件；例如，圆角矩形按钮不支持编辑，因此它们永远不会发送 Editing Changed 事件。文本字段不会生成 Touch Down 事件。如果视图没有按预期生成事件，请仔细检查你在此处关联的事件。

使用响应者链处理事件是一种巧妙的关联技术——关联到 First Responder 会绕过 AViewController，并将 Touch Down 事件直接发送到根控制器中的 `showBView:`。你可以使用这个技巧来处理几乎任何上下文中的任何事件类型，但这不符合 MVC 的规范，你应该将其保留给由根控制器处理的视图交换事件。如果你为 AViewController 扩展更多功能——按钮、滑块等——请按照通常方式将处理这些功能的代码添加到 AViewController.m 文件中。

现在你可以编辑 B 视图 nib，以显示一个较大的标签和另一个圆角矩形按钮，如图 19.28 所示。暂时将按钮保持未关联状态。

**图 19.28**

设计 B 视图，它与 A 视图非常相似，仅标签略有变化。

![](img/2b293e29fc15b0797f113b85dd429b6e_552_0.png)

保存编辑后的 nib，构建并运行应用。点击 A 视图中的按钮，B 视图就会出现，如图 19.29 所示。

**图 19.29**

测试 A 视图中的按钮是否显示 B 视图

![](img/2b293e29fc15b0797f113b85dd429b6e_553_0.png)

### 通过协议消息处理事件

接下来，向 B 视图添加代码以交换回视图；在完成此操作之前，B 视图中的按钮仍处于非活动状态。你可以重复之前的步骤，在根控制器中添加 `showAView:` 方法，稍微修改代码以加载 A 视图 nib，并通过 First Responder 将其关联到 B 视图中的按钮。这是最简单的解决方案，而且会完美运行。

这个示例演示了如何通过创建委托协议来解决该问题。与更简单的选项不同，协议可以在视图控制器之间传递参数。首先，向根视图控制器的接口添加一个新的委托协议。将 FirstAppViewController.h 中的声明改为：

```objectivec
@interface FirstAppViewController : UIViewController <ViewControllerDelegate>{
```
