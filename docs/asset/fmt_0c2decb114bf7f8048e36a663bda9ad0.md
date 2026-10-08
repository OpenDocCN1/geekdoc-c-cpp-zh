
尽管还有很多内容未未说（尽管比你想象的要少），但本章的内容不仅是为了让你入门，还能让你在开发 iPhone 应用时持续进行下去。它提供了一个参考框架，你可以通过这个参考框架获得我在后续章节中随口抛出的概念——同时也为深入理解应用生命周期奠定了基础，让你能够驾驭详细的文档。

是时候进入真正有趣的内容了。

## 第三部分

从“哇，这真是个好主意”到 App Store

《第五次波浪》 由 Rich Tennant 著

@RICHTENNANT

![](img/d3e98c195a93c941d040bbbc53dc1bd8_136_0.png)

> *停止编写优先停车位分配程序吧。他们想加快咖啡壶/工位邻近程序的进度。*

## 在这一部分中 ...

你不是唯一梦想着 iPhone 应用能带来的财富和荣耀的人——你的作者也有梦想。在这一部分中，我将带你完成整个过程，开发那个虽然小但真实且具有某种功能的应用程序，你在第二部分中已经为它构建了用户界面。……你将看到如何添加应用所需的所有功能，甚至当你改变主意时该怎么办（无论是你发现了更好的实现某事的方法，还是你的用户要求如此）。最后，我会向你展示如何让你的应用程序在 iPhone 上运行并进入 App Store。这一切应该能让你一段时间内无忧无虑，但最后，你可以开始考虑乘坐私人喷气飞机环游世界，或者同样合理的事情。

## 第7 章

## 实际编写代码

## 本章内容

- 开始编写代码
- 使用你友好的 Xcode 编辑器
- 让 Xcode 创建访问器
- 修复水水工程（第一部分）
- 再次处理内存管理

如果你直接跳到了这一章，你可能很迫待要开始写代码了。我理解这种冲动，如果你准备好了，这一章以及后续章节——绝对能满足你的愿望。如果你从这里开始，然后发现其中一些内容很难进展，你可能想跳回一或两章，以便我为你补充一些在编写代码时需要掌握的概念，从而让你的编码体验更有效率——也更有趣！

## 系好带，是时候写代码了

之前的章节讨论了通用的设计原则，以及你可以使用的特定 iPhone 开发者工具（Xcode、Interface Builder）。例如在第 5 章中，你已经创建了一个功能完备的 iPhone 应用骨架（我的 ReturnMeTo 之宝）——现在你可以用所需的代码来充实它，将 ReturnMeTo 应用从一个只是呆在那里且看起来漂亮的东西变成一个真正能执行某些操作的东西。

快速回顾一下第 5 章，你会发现 ReturnMeTo 应用的很大一部分已经就位并准备就绪了。例如，如果你点击文本字段，确实会出现键盘——尽管你现在还用它做不了什么。文本字段和标签都是从 nib 文件自动创建的——这很棒——但你仍必须完成两个任务：

- 获取用户输入文本字段的内容。
- 在你创建的标签中显示用户输入。

实际上，你必须把它们连接起来，让左手知道右手在做什么。

幸运的是，该框架的设计允许你轻松且优雅地做到这一点。视图控制器可以引用对象……（等一下，OCR 文本在这里似乎碎片化）……Xcode 的快速帮助、头文件访问、文档窗口、帮助菜单和查找工具。通过这些工具，你可以快速访问特定类、方法或属性的文档。

# 第 7 章：实际编写代码

### Xcode 代码编辑器

你用于为 iPhone 应用编写代码的主要工具是 Xcode 编辑器。Apple 已经尽力让这个文本编辑器变得简单易用，以下功能证明了这一点：

- **代码感应（Code Sense）：** 当你输入时，编辑器会通过文本补全你想要的内容。使用 Code Sense 非常有用，特别是如果你像我一样经常忘记函数的具体参数。当 Code Sense 激活时（默认开启），Xcode 会根据你输入的文本以及上下文提供它认为你可能想要输入的建议。你可以按 Tab 或 Return 接受建议。你也可以按 Esc 显示补全列表。
- **代码折叠（Code Folding）：** 通过代码折叠，你可以折叠正在处理的代码，只显示你关注的代码。你通过点击想要隐藏的代码左侧列来实现。
- **在头文件和实现文件之间切换：** 在编辑器上方的工具栏上，点击锁定最后一个图标即可在 h 和 .m（头文件和实现文件）之间切换，反之亦然。头文件让你看到类的实例变量和方法声明，而实际代码位于实现文件中。如果你查看项目窗口的 Groups & Files 格，你可以看到我们开始的类的单独的 .m 文件。
- **在新窗口中打开文件：** 双击文件名即可在新窗口中打开文件。这让那些拥有大显示器或多显示器的用户能够同时查看多个文件。例如，你可以查看一个类的方法以及它调用的同一个类甚至是另一个类的方法。

## 访问文档

像许多开发者一样，你可能会想要深入研究某些代码。这时你就会真正感激 Xcode 的快速帮助、头文件访问、文档窗口、帮助菜单和查找工具。通过这些工具，你可以快速访问特定类、方法或属性的文档。

# 120 第三部分：从“哇，真是个好主意”到 App Store

为了了解它是如何运作的，假设我打开了项目窗口，代码如图 7-1 所示。如果我想了解更多关于 `UIApplicationDelegate` 的信息该怎么办？

## 快速帮助 (Quick Help)

快速帮助是一个非侵入性的窗口，用于为单个符号提供文档。它会在行中弹出，尽管你可以在其打开后移动窗口，将快速帮助作为符号检查器（保持打开状态）。你也可以在 Xcode 偏好设置中自定义调试中的文档”窗口。

要获取某个符号的快速帮助，在文本编辑器中双击该符号（在此例中为 `UIApplicationDelegate`；见图 7-1）。

![](img/d3e98c195a93c941d040bbbc53dc1bd_141_0.png)

## 符号的头文件

头文件在代码中非常重要，因为它们是寻找类声明的地方，包含了所有的实例变量和方法声明。要获取符号的头文件，按住 ⌘ 并双击文本编辑器中的符号。例如，见图 7-2，我按下 ⌘ 然后双击了 `UIApplicationDelegate`。

# 第 7 章：实际编写代码

这同样适用于你创建的类。

![](img/d3e98c195a93c941d040bbbc53dc1bd_142_0.png)

图 7-2 `UIApplicationDelegate` 的头文件。

## 文档视图 (Documentation view)

文档视图允许你浏览和搜索 Xcode 参考库中的项目，以及你安装的任何第三方文档。

你通过按下 ⌘Option 并双击符号来访问文档（以获取 API 引用等）。这使你能够获取有关方法的文档，从而进一步了解框架类中的方法和属性。在图 7-3 中，我按下 ⌘Option 并双击了 `UIApplicationDelegate`。

使用文档视图，你可以浏览安装在计算机上的文档——包括 API 引用、指南以及关于特定工具或技术的文章合集。

它是获取方法文档或更多关于框架类中方法和属性信息的首选途径。（通过使用 API 引用，我发现视图具有 `frame`，我将在第 8 章中用它来决定滚动视图以保持文本字段可见。）

![](img/d3e98c195a93c941d040bbbc53dc1bd_143_0.png)

图 7-3：文档窗口。

## 帮助菜单 (Help menu)

帮助菜单字段还允许你搜索 Xcode 文档，并打开文档窗口和快速帮助。

你也可以右键点击符号，弹出一个菜单，该菜单提供了与帮助菜单中类似的选项（以及其他相关功能）。这在图 7-4 中所示。

## 查找 (Find)

Xcode 还可以帮助你在项目中查找内容。通过选择 `Edit>Find` 访问的子菜单提供了在项目中查找文本的选项。

你会发现，随着类的变大，你有时会想要在文件中查找单个符号，或者查找文件中所有的出现处。你可以通过选择 `Edit>Find` 或按下 `Cmd+F` 轻松实现，这会打开一个查找栏来搜索编辑器中的符号。在图 7-5 中，我在查找栏中输入了 `viewDidLoad`，Xcode 在文件中找到了所有 `viewDidLoad` 的实例并为我高亮显示了。

![](img/d3e98c195a93c941d040bbbc53dc1bd_144_0.png)

图 7-4：右点击 Delegate。

![](img/d3e98c195a93c941d040bbbc53dc1bd_144_1.png)

图 7-5：在文件中查找 viewDidLoad。

你也可以通过选择 `Edit→⌘+Find→Find in Project` 或按下 `⌘+Shift+F` 来查找项目。我按下 ⌘+Shift+F 打开了图 7-6 所示的窗口。我输入了 `ReturnMeViewController`，然后在下拉菜单中选择了 `Project`。你可以指定在哪些文件（打开项目文件等）中搜索（这是一个跟踪代码中某些内容的极佳功能）。

如果你在顶部的面板选择一行，如图 7-6 所示，该实例会在底部面板打开并被高亮显示。

![](img/d3e98c195a93c941d040bbbc53dc1bd_145_0.png)

图 7-6：项目查找。

## 为视图控制器添加 Outlet (Adding Outlets to the View Controller)

现在你已经对如何使用 Xcode 编辑器有了一些了解，是时候写代码了。在介绍编辑器之前，我提到需要为我们的 ReturnMeViewController 应用添加 Outlet——现在就开始这样做。方法如下：

- 转到 Xcode 项目窗口，在 `Groups & Files` 面板中，点击 `Classes` 旁的三角形展开文件夹。
- 从 `Classes` 文件夹选择 `ReturnMeViewController.h` —— 即 ReturnMeViewController 的头文件。

该文件的内容出现在 Xcode 编辑器的主面板中，如图 7-7 所示（当然，你还没有所有的代码——你将在第 4 步输入）。

![](img/d3e98c195a93c941d040bbbc53dc1bd_146_0.png)

图 7-7：ReturnMeViewController.h。

3. 在头文件中查找以下四行代码：

```objectivec
#import <UIKit/UIKit.h>

@interface ReturnMeViewController : UIViewController

IBOutlet *textField;
IBOutlet *label;

@end
```

学会了吗？很好。

4. 在 `@end` 之后输入以下行代码：

```objectivec
@property (atomic, retain) UITextField *textField;
@property (nonatomic, retain) UILabel *label;
```

完成后，你的代码应该像图 7-7。

这里的几行代码声明了 Outlet，它们会在应用程序启动时自动初始化为文本字段 (`textField`) 和标签 (`label`)。虽然这本该自动发生，但并没有。我必须帮它一下。

在过程化编程中，变量通常是公开的。在面向对象编程中，类的实例变量封装在对象内部，不应被直接访问。让它们初始化的方法是创建所谓的访问方法（accessor methods），它们允许读取对象的特定实例变量并（如果你需要的话）。创建访问方法是一个两步过程，从 `@property` 声明开始，它告诉编译器存在访问方法。

这就是你所做的；我根据 `@property` 声明编写了代码。你会注意到 `@property` 声明带有参数。这些参数指定了访问方法的行为——我将在下一节解释其含义。现在，只需知道你需要向它们添加内容。

5. 回到 `Groups & Files` 列表中的 `Classes`，选择 `ReturnMeViewController.m` —— 即 ReturnMeViewController 的实现文件。

6. 在实现文件中查找以下代码：

```objectivec
@import "ReturnMeViewController.h"
@implementation ReturnMeViewController
```

我们几乎就在顶部。

7. 在 `@implementation ReturnMeViewController` 之后、其他内容之前输入两行代码：

```objectivec
@synthesize textField;
@synthesize label;
```

完成后，你的代码应该像你在图 7-8 中看到的。

虽然 `@property` 声明告诉编译器存在访问方法，但它们仍然必须创建。在过去的日子里，你必须自己创建这些访问方法，在大型程序中这非常繁琐。坦率地说，每当你包含一个 `@synthesize`，Objective-C 都会为你创建访问方法。

8. 向下滚动 `ReturnMeViewController.m` 的代码直到遇到以下行：

```objectivec
(void)dealloc {
    [super dealloc];
}
```

你可以使用 `Command+F` 在单个文件中查找内容，而 `Shift+F` 则在所有项目文件中查找。

# 第 7 章：实际编写代码

# 127

![](img/d3e98c195a93c941d040bbbc53dc1bd8_148_0.png)

图 7-8：完成配件的添加。

9. 在 `- (void) dealloc` 行和 `[ super dealloc; ]` 行之间输入以下两行代码：

```
[textField release];
[label release];
```

新代码看起来应该像图 7-9 所示。

如果你还记得我在之前的几个章节中对内存管理的痴迷，你就能认出 `release` 是一个释放不再需要的内存占用的工具。（那些还没有听过我关于内存管理的演讲的同学，在本章的晚些时候会有机会听听。）

现在，它已经交到你的视图控制器（view controller）了。退后一步，欣赏一下你的心力之作。然后进入下一节，看看你为到 `ReturnMeViewController.m` 和 `ReturnMeViewController.h` 文件中添加的代码片段是如何符合使用 Objective-C 语言的基本原理的。

![](img/d3e98c195a93c941d040bbbc53dc1bd8_148_1.png)

图 7-9：做一点内存管理。

# 128 第三部分：从“哇，这是个好主意”到 App Store

## Objective-C 属性 (properties)

你很快就会发现，你将经常地使用属性。在上一节中，我让你盲目地跟随我的操作并添加了属性。但现在你可能已经发现，我不认为你应该盲目地做事，所以在这一节中，我来解释一下关于属性你需要了解的知识。

现在，你可能记得，在面向对象编程中，类的实例变量被封装在对象内部，不应该被直接访问。如果你需要为程序中的其他对象为那个特定的实例变量创建访问器方法（accessor methods）。（这在上一节中听起来很熟悉。）

例如，在第 9 章中，你将为 `ReturnMeToAppDelegate` 添加一个名为 `savedNumber` 的实例变量。这样做是为了存储当有人找到你丢失的 iPhone 时要拨打的电话号码。`ReturnMeToAppDelegate` 会在应用程序终止时保存它，并在启动时加载它。`ReturnMeToViewController` 需要访问它以便在视图中显示，并在用户输入新号码时更新它。

提供访问对象实例变量的方法被称为访问器方法，它们实际上是获取（使用 `getter` 方法）和设置（使用 `setter` 方法）实例变量的值。虽然你可以自己编写这些方法，但这可能相当繁琐。这就是属性大显身手的地方。Objective-C 的“声明属性（Declared Properties）”功能提供了一种简单的方法来声明和实现对象的访问器方法。编译器可以根据你在属性声明中告诉它的方式，自动为你合成这些访问器方法。

Objective-C 通过接口文件中的 `@property` 声明结合实现文件中的 `@synthesize` 声明，为你生成 getter 和 setter 方法。带有属性的 getter 和 setter 方法的默认名称是属性名的 `whateverThePropertyName:`（用于 getter）和 `setWhateverThePropertyNameIs:`（用于 setter）（你将斜体部分替换为实际的属性名）。例如，在我们 `ReturnMeToApplication` 中生成的访问器中，`textField` 是 getter，而 `setTextField:` 是 setter。同样，`label` 的名称在 getter 和 setter 中分别是 `label` 和 `setLabel:`。

话虽如此，归根结底，你在代码中做三件事就能让编译器为你创建访问器：

- 1. 在接口文件中声明实例变量。
- 2. 在同一个接口文件中为该实例变量添加 `@property` 声明（通常带有 `nonatomic` 和 `retain` 属性）。
- 3. 这就是你之前所做的。

## 132 第三部分：从“哇，这真是好主意”到 App Store

记住

你必须保存你的代码；否则，Interface Builder 将无法找到它。

+ 2. 在项目窗口中，双击 `ReturnMeToViewController.xib` 以启动 Interface Builder。

Interface Builder 随之出现在屏幕上，带有主 nib 窗口和用于检查的 View 窗口。（有关 Interface Builder 机制的更多信息，请参阅第 5 章。）

+ 3. 按住控制键（control），点击主 nib 窗口中的 File's Owner，并将其拖动到 View 窗口中的 label 字段上，如图 7-10 所示。

你需要使用控制键，否则你只会拖动 File's Owner 图标，而不是建立连接。

当光标悬停在 label 字段上时，你应该看到 label 的值（650 555 1212）。（如果你记得的话，那是你在第 5 章创建 label 时设置的值。）

![](img/d3e98c195a93c941d040bbbc53dc1bd8_153_0.png)
