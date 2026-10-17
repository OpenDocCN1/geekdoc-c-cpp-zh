

# Objective-C 常用语手册

## Objective-C 常用语手册

![封面](img/f809af90c16db41b6c7bed92e38de6ec_0_0.png)

| 总策划编辑 | 执行编辑 | 校对员 | 封面设计 |
| --- | --- | --- | --- |
| Mark Taub | Kristy Hart | Charlotte Luggen | Gary Adair |
| 策划编辑 | 项目编辑 | 出版 | 排字 |
| Mark Taber | Anne Goebel | 协调员 | Gloria Schurick |
| 开发编辑 | 拷贝编辑 | Vanessa Evans | |
| Michael Thurston | Bart Reed | | |

+ 10 与环境交互 185

## 致谢

在写一本关于 Objective-C 的书时，我应该感谢的第一个人是 Nicolas Road。我在开始读博士学位左右买了我的第一台 Mac，当时计划用它来写 Java 代码，不想学习一种专有语言。当我开始博士生涯时，发现自己正在和 Nicolas 工作，他是一个活跃的 GNUstep 贡献者。他说服了我 Objective-C 和 Cocoa 不仅适用于 Mac，它们都非常值得学习。他是完全正确的：Objective-C 是一门非常优雅的语言，而其配套的框架让开发变得异常简单。

下一个要感谢的人是 Fred Kiefer。Fred 是 GNUstep 中 AppKit 框架实现的维护者。他对这本书进行了极其详尽（读作：吹牛角尖）的技术审查，发现了几处解释得不够尽如人意的地方。如果你喜欢在读这本书，那么 Fred 应该享有大部分功劳。

最后，我需要感谢其他参与将这本书从我的文本编辑器送到你手中的每一个人，特别是最初向我提议这个想法的 Mark Taber。

## 我们想听听你的声音

作为本书的读者，你是我们最重要的批评家和评论者。我们重视你的意见，并想知道我们做得对的地方、哪里可以做得更好、你希望我们出版哪些领域的书籍，以及任何你愿意分享给我们的建议。

你可以直接发送电子邮件或写信给我，告诉我对比这本书的喜欢或不喜欢之处——以及我们可以做些什么来让我们的书籍更强大。

请注意，我无法帮助你解决与本书主题相关的技术问题，而且由于收到的邮件量很大，我可能无法回复每一条信息。

你在写信时，请务必包含书名和作者，以及你的姓名或邮箱地址。我会仔细审查你的评论，并将它们与参与本书的作者和编辑分享。

电子邮件：`mark.taber@pearson.com`

邮寄：

Mark Taber

副出版

Addison Wesley Publishing

800 East 96th Street

Indianapolis, IN 46240

## 读者服务

访问我们的网站并在`informit.com/aw`注册本书，方便访问书中可能提供的任何更新、下载或错误列表。

## 引言

布莱斯·帕斯卡（Blaise Pascal）曾写道：“我没有时间写一封短信，所以我写了一封长信。”这本短语书不到 350 页（小开本），是我写过的最短的一本书，试图将我想说的一切都塞进这样一个短小的卷册中是一项挑战。

当 Mark Taber 最初建议我写一本 Objective-C 短语书时，我并不确定它会是什么样子。自然语言的短语书是一系列短习语的列表，供那些发现自己需要快速一两句话的人使用。编程语言的短语书应该承担类似的角色。

本书并不是语言参考书。Apple 在`http://developer.apple.com`网站上提供了关于 Objective-C 语言的胜任参考资料。这不是一份详尽的教程；与我的另一本 Objective-C 书《Cocoa 编程开发手册》（Cocoa Programming Developer’s Handbook）不同，你找不到作为代码示例的完整程序。相反，你将看到非常短的 Objective-C 惯用示例，希望你可以在很多地方使用它们。

生活中最令人沮丧的事情之一就是发现书中的代码示例实际上无法运行。书中了两类代码列表。白色背景上的代码旨在说明一个简单的点。这些代码可能依赖于某些隐含的上下文，不应被视为可运行、可用的示例。

你在书中看到的大部分代码都在灰色背景上。在每个此类示例的底部，你会找到该列表取自的文件名。你可以从 InformIT 网站上的书籍页面下载它们：`http://www.informit.com/title/0321743628`

## 关于排版的说明

本书是用 Vim 编写的，使用了语义化标记。从这里开始，会生成三个不同的版本。其中两个使用`pdflatex`创建。如果你正在阅读纸质版或 PDF 版本，你看到的其中之一。这两个版本之间的唯一区别是打印版包含了裁切标记，以便打印机裁剪页面。

第三个版本是 XHTML，用于 ePub 版本。它是使用 EtoileText 框架创建的，该框架首先将 LaTeX 风格标记解析为树结构，然后执行一些转换以处理交叉引用和索引，最后生成 XHTML。它的代码全部是用 Objective-C 编写的。

如果你两个版本都能访问，你可能会发现 ePub 版的代码列表看起来稍微漂亮一点。这是因为 EtoileText 使用了另一个 Étoile 框架 SourceCodeKit 进行语法高亮。它使用了 Clang（一种现代 Objective-C 编译器）的一部分来标记代码列表。这意味着代码段被标注了与编译器看到的完全相同的语义类型。例如，它可以区分函数调用和宏实例化。

你可以在 Etoilé 的 subversion 仓库中找到所有执行此项操作的代码：`http://svn.gna.org/viewcvs/etoile/trunk/Etoile/`

# Objective-C 哲学

要理解 Objective-C，你需要理解其创建背后的哲学。与 C++、D 或 Java（这些语言被设计成新的类 C 语言）不同，Objective-C 是一门混合型语言。Objective-C 的设计者之一 Tom Love 将方括号语法描述为一个指示牌，标志你正在离开 C 进入 Object 的世界。

他说服了我 Objective-C 和 Cocoa 不仅适用于 Mac，它们都非常值得学习。他是完全正确的：Objective-C 是一门非常优雅的语言，而其配套的框架让开发变得异常简单。

下一个要感谢的人是 Fred Kiefer。Fred 是 GNUstep 中 AppKit 框架实现的维护者。他对这本书进行了极其详尽（读作：吹牛角尖）的技术审查，发现了几处解释得不够尽如意意的地方。如果你喜欢在读这本书，那么 Fred 应该享有大部分功劳。

最后，我需要感谢其他参与将这本书从我的文本编辑器送到你手中的每一个人，特别是最初向我提议这个想法的 Mark Taber。

## 对象模型

Objective-C 拥有类似于 Smalltalk 的对象模型。如果你来自 Java，你会发现这非常容易。如果你来自 Simula 家族语言（如 C++），你可能会觉得有点困难。

艾伦·凯（Alan Kay）将对象的想法描述为一种简单的分解练习。在解决问题时，你希望将其分解为简单的部分。运行程序部分的最简单实体与运行整个程序的实体相同：计算机。在艾伦·凯的愿景中，对象是通过交换消息通信的简单计算机模型。

这正是 Objective-C 及其父类 Smalltalk 中对象的行为。它们是相互传递消息的程序部分。通常，这些消息是同步传递的，所以它们的行为有点像函数调用，但意识到它们是不同的。

消息是比函数调用更高层次的抽象。函数调用非常。在许多架构上它是一条指令。在更像 RISC 的架构上，你将返回地址压入栈中然后跳转。在所有情况下，目标地址都是固定的。

当你发送消息时，如何处理完全取决于接收者。最典型的方法是调用与消息同名的方法，但也有其他替代方案。代理对象可以将消息转发给另一个对象，并在此之前对消息参数进行某些替换。

Simula 没有使用“面向对象”这一术语，但许多在 Smalltalk 之后的 Simula 类语言都采用了这一术语，导致了些困惑。这类家族的语言（如 C++）使用虚函数表（vtables）来实现某种表面上相似的东西。

Simula 风格的对象包含指向其 vtable（如果有父类则为多个 vtables）的指针。当你调用虚函数时，编译器会在 vtable 中创建一个偏移量，然后调用该偏移量处的函数。

这种差异的副作用之一是……

# 第 1 章：Objective-C 哲学

Objective-C 和 C++ 中的指针转换具有非常不同的语义。在 Objective-C 中，将指针从一种对象类型转换为另一种类型时，不会生成任何代码。这种转换只是对编译器类型检查器的提示。然而，在 C++ 中，指针转换会执行一些指针算术，使得通过转换指针的代码能够在正确的位置找到虚函数表（vtable）。这意味着在 Objective-C 中，你可以将任何对象类型转换为任何其他对象类型，而在 C++ 中，你需要使用一种特殊的转换。

这种区别非常重要。在 Objective-C 中，影响方法查找的唯一因素是对象的类型。在 C++ 和其他 Simula 家族语言中，查找还受到编译器认为的对象类型的影响。

## 两种类型系统的故事

让接触 Objective-C 的人感到困惑的问题之一是它拥有两套类型系统。如果你将原始实现视为一个预处理器，这就有说通了。Objective-C 预处理器会执行类似 Strongtalk¹ 的类型检查，然后由 C 编译器执行 C 类型检查。

> ¹ StrongTalk 是 Smalltalk 的一种方言，增加了可选的静态类型检查。创建该语言的团队后来去开发了 Java。值得注意的是，尽管 StrongTalk 是最快的 Smalltalk 实现之一，但编译器并没有使用类型信息进行优化。

C 具有结构化类型系统。基本类型的类型等价取决于两个类型具有相同的表示。复杂类型永远不会被视为等价。

Objective-C 增加了代数类型系统。对象的类型由其签名定义：即它声称将响应的消息。你可以隐式地将 Objective-C 对象转换为其父类，因为它保证响应父类所理解的所有消息。

你可以显式地将 C 对象转换为其他类型。例如，你可以将字典对象转换为数组对象。只要你随后发送的是字典和数组都能理解的消息，这种方法就是通行的。

## C 就是 Objective-C

Objective-C 最重要的特性之一是它是 C 的纯超集。你可以将 C 视为嵌入在 Objective-C 中用于低级任务的特定领域语言，将 Smalltalk 的一个子集视为嵌入在 Objective-C 中用于高层任务的特定领域语言。

使用纯 C 解决问题并没有什么错。许多人在学习 Objective-C 时会犯的错误之一是认为他们必须停止使用 C。对于很多事情，C 的解决方案是正确的。

注意：Objective-C 还有一个姐妹语言 Objective-C++，它与 C++ 的关系就像 Objective-C 与 C 的关系一样。Objective-C++ 是 C++ 的超集，允许你从 Objective-C 对象调用 C++ 代码，反之亦然。由于它们拥有完全不同的模型，你不能用 C++ 子类的 Objective-C 类，反之亦然；但你可以将 Objective-C 对象的指针作为 C++ 对象的字段，并将 C++ 对象的指针作为 Objective-C 对象的实例变量。

你可以在 Cocoa 框架中看到这一点。并不是一切都是对象。如果你请求字符串中的字符范围，你将使用`NSRange`结构——而不是 Objective-C 对象——它包含一个位置和一个长度。点、矩形等其他事物也以类似的方式表示。如果这些都是对象，就会消耗更多内存，操作变慢，而且并没有提供真正的灵活性。

面向对象的 Ingalls 测试²认为，你应该能够创建一个新的整数类型并将其用于定位屏幕上的窗口。Objective-C 未通过这项测试。

> ² 以提出该测试的 Smalltalk 设计者之一 Dan Ingalls 命名。

这在现实世界中并不是一个很有用的例子，因为大多数时候，设计新的整数类型会破坏许多期望整数具有标准行为的代码。

在 Objective-C 中，在不需要的情况下，你不必使用动态行为（如后期绑定和多态）。

## 语言与库

对于非常动态的语言，很难在语言和库之间划分界限。在 Smalltalk 中，语言中没有等同`if`语句。标准库定义了`True`和`False`单例类，它们响应`-ifTrue`：接收闭包作为参数的消息。所有复杂的流程控制结构（如循环或枚举）都是基于此实现的。

Objective-C 继承了 C 的流程控制，但所有的动态行为都由运行时库提供。这与 C 或 C++ 不同。你可以编译一个不调用 libc 或 libstdc++ 中任何函数的自立 C 或 C++ 二进制文件。然而，每一个不是纯 C 语言的 Objective-C 程序都必须链接`libobjc`才能工作。

该库传统上提供三个类：一个简单的根类、一个常量字符串的类和一个用于协议（protocols）的类。其中第一个提供了包括对象分配在内的功能，这在 C++、Java 和类似环境中是语言的一部分。另外两个是编译器可能生成的类。

大多数情况下，你不会使用这些类。过去二十年编写的几乎所有 Objective-C 代码使用了 OpenStep Foundation 框架的实现。OpenStep 是 NeXT 和 Sun 共同制定的一种规范，为跨平台应用程序提供现代的面向对象框架。

## Objective-C 的历史

“面向对象”一词是由 Alan Kay 在 20 世纪 60 年代提出的，Smalltalk 是他和其他人为演示这种编程风格而创建的语言。Smalltalk 开发于 70 年代，最广泛的版本于 1980 年发布。

然而，Smalltalk 运行得非常慢。为了正确运行它，你需要像 Xerox Alto 那样强大的计算机，拥有 512KB 内存，理想情况下是 2MHz 处理器。

Brad Cox 喜欢 Smalltalk 的想法，但他想要一种可以在他们负担得起的计算机上使用的语言。他的想法是将 Smalltalk（一种鼓励封装、松散耦合和代码重用的高层语言）与 C 结合。C 处于光谱的另一端，在封装方面几乎没有特性，没有动态分发，但有一个巨大的优势：它很快。

C 很大程度上基于 PDP-11 指令集。一个非常原始的 C 编译器就能产生非常快的代码。这在今天也是如此。如 LLVM、XLC 和 ICC 等编译器在优化上花费了大量精力，但几乎没有优化的 PCC 仍然能产生相当快的代码。

Brad Cox 和 Tom Love 于 1986 年创立了 StepStone，销售基于 Brad 早期面向对象预编译器的产品。该产品 Objective-C 是一个预处理器和一个小型 Objective-C 运行时库。预处理器生成的 C 代码可以使用你平台的 C 编译器进行编译。

1988 年，NeXT 了 StepStone 代码的许可并直接购买了 Objective-C 商标。NeXT 随后将预处理器重写为 GNU 编译器集（GCC）的前端。在法律斗争后，自由软件基金强制他们发布了代码，但他们保留了运行时库的私有。

GNU 项目编写了运行时库的替代品，但进行了一些更改。其中一个是 GNU 运行时中的选择器（selectors）与类型相关联。在 NeXT（以及 Apple）平台，选择器（selectors）只是字符串。这意味着 GNU 运行时可以在运行时捕获某些由于程序员错误导致的、堆栈损坏，而这些错误在 NeXT 运行时是不可见的。

另一个变化在消息发送的工作方式上。当你使用 NeXT 运行时发送消息时，编译器会将消息发送转换为对`objc_msgSend()`函数的调用。它会查找该方法然后调用它。遗憾的是，无法在 C 中实现这个函数。它必须为每个平台以及该平台上的每种调用约定用汇编语言编写。GNU 的解决方案是将其替换为`objc_msg_lookup()`函数，该函数返回一个指向函数的指针。这稍微慢一点，但意味着相同的代码可以在所有平台上运行。

Objective-C 从那时起没有发生太大变化。NeXT 在 1997 年被 Apple 收购，Objective-C 成为其 Rhapsody 操作系统 Yellow Box 的主要开发语言。这些后来分别重命名为 Cocoa 和 OS X。2003 年，Apple 在语言中添加了一些类似 Java 的异常原语。

下一组升级出现在 2007 年，当时 Apple 引入了 Objective-C 2。这对老牌的 Objective-C 程序员来说有些困惑，因为之前的版本——NeXT 发布的版本——已经是 Objective-C 4。

幸运的是，“2 是紧跟在 4 之后的数字”这种信念似乎没有进入 Cocoa 的任何排序代码中。




# 第 1 章：Objective-C 哲学

## Objective-C 2

Objective-C 2 增加了一些语法糖。它提供了一种新的枚举方式、一种合成访问器方法（synthesizing accessor methods）的方法，并引入了`垃圾回收`（garbage collection）。Objective-C 2 与其说是一个营销术语，倒不如说是一门真正的语言。你找不到用于选择它的编译器开关。某些功能（如非易碎性实例变量，non-fragile instance variables）仅在某些运行时可用。其他功能（如垃圾回收）在 iPhone 上不可用。声明式属性（Declared properties）是 Objective-C 2 特性中唯一在各处都通的特性，包括非 Apple 平台。

幸运的是，“2 是紧跟在 4 之后的数字”这种信念似乎没有进入 Cocoa 的任何排序代码中。

## 跨平台支持

强制 NeXT 将 GCC 的 Objective-C 前端作为自由软件发布，对于自由软件基金来说是一次公关胜利。遗憾的是，从长期跨平台支持的角度来看，这并不那么好。NeXT 发布的代码非常糟糕，在过去的十年里，很大程度上被 GCC 团队忽视了。

GCC 对 NeXTera Objective-C 有中等程度的支持，也支持新的异常处理关键字。GNUstep 项目提供了 Foundation 和 AppKit 框架的实现，这些是 NeXT 和 Mac 开发的核心。

2007 年，Apple 开始开发一种新编译器。Clang 是低级虚拟虚拟机（LLVM）针对 C 家族语言的前端：C、Objective-C 和 C++。它比 GCC 模块化得多，并且被设计用于代码补全、语法高亮和静态分析，而不仅仅是编译。Clang 在不同层级使用的代码之间有清晰的分离，并将运行时特定的代码隔离到单独的类中。

编译器只是 Objective-C 实现的一半。另一半是运行时库。GNU 运行时是使用 GCC 开发的，没有实现 Objective-C 2 所需的函数。为了解决这个问题，我在 Étoile 的一部分编写了一个框架，它实现了大部分缺失的功能，并实现了 Apple 在 OS X 10.5 中引入的公共运行时 API。

该框架现在是 GNUstep 的一部分。它的另一个副本已与 GCC 运行时的一个分支合并，该分支也是作为 GNUstep 项目的一部分开发的的。这被称为 GNUstep 运行时或`libobjc2`。

通过 Clang 和 GNUstep 项目提供的运行时，你可以获得对大多数 Objective-C 2 特性的完整支持，包括非易碎性实例变量。这意味着你可以在 Windows、Linux、*BSD、Solaris 等*系统上使用 Objective-C 2。至少有一个人已经在 QNX 上测试过它，它也可能在 Symbian 上运行。

如果你使用 GCC 版本的运行时配合 GNUstep 中的 Objective-C 2 框架，那么你可以获得一些功能，例如快速枚举和声明式属性，但你无法获得新 ABI 的任何好处。

## 编译 Objective-C 程序

```text
$ gcc scanner.m
未定义的的符号:
  _OBJC_CLASS_$NSAutoreleasePool, referenced from:
  _objc_classrefs_DATA@ in ccoRpaJq.o
  _objc_msgSend, referenced from:
  _main in ccoRpaJq.o
## On OS X
$ gcc --framework Foundation scanner.m
## On other platforms
$ gcc `gnustep-config --objc-flags --base-libs`
scanner.m
```

Clang 前端旨在作为 GCC 的无缝替换，因此在任何指令中看到`gcc`的地方，都可以将其替换为`clang`。在 OS X 上，GCC 安装在`/usr/bin/gcc`，所以它在你的路径中。对于版本较旧的 Xcode 工具，Clang 安装在`/Developer/usr/bin/clang`，因此你可能需要指定完整路径，或将此位置添加到你的路径中。在其他平台上，如果安装了它们，你通常可以在路径中同时找到它们。

如果你熟悉使用这些编译器中的之一编译 C 或 C++，你会发现 Objective-C 非常熟悉。你认为属于 Objective-C 语言组成的大部分内容实际上是由 Foundation 框架提供的。可以在不使用 Foundation 的情况下使用 Objective-C，但那是人们为了证明自己可以而这么做，而不是因为这实际上是明智的事。

（以及 Apple）平台，选择器只是字符串。这意味着 GNU 运行时可以在运行时捕获某些由于程序员错误导致的堆栈损坏，而这些错误在 NeXT 运行时是不可见的。

另一个变化在消息发送的工作方式上。当你使用 NeXT 运行时发送消息时，编译器会将消息发送转换为对`objc_msgSend()`函数的调用。它会查找该方法然后调用它。遗憾的是，无法在 C 中实现这个函数。它必须为每个平台以及该平台上的每种调用约定用汇语言编写。GNU 的解决方案是将其替换为`objc_msg_lookup()`函数，该函数返回一个指向函数的指针。这稍微慢一点，但意味着相同的代码可以在所有平台上运行。

Objective-C 从那时起没有发生太大变化。NeXT 在 1997 年被 Apple 收购，Objective-C 成为其 Rhapsody 操作系统 Yellow Box 的主要开发语言。这些后来分别重命名为 Cocoa 和 OS X。2003 年，Apple 在语言中添加了一些类似 Java 的异常原语。

下一组升级出现在 2007 年，当时 Apple 引入了 Objective-C 2。这对老牌的 Objective-C 程序员来说有些困惑，因为之前的版本——NeXT 发布的版本——已经是 Objective-C 4。

# Objective-C 入门

Objective-C，正如其名称所示，为 C 添加了对象。具体的，遵循 Smalltalk 模型的对象是类的实例。对象始终分配在堆上。

如果你已经熟悉 C，那么学习 Objective-C 语言将需要一个下午——如果你理解 Smalltalk 风格的对象 world，时间更短。这稍微有点误导性，当然。如果学习 Objective-C 真的那么简单，你会觉得买关于它的书有点亏。像 Smalltalk 一样，Objective-C 语言之所以如此简单，很大程度上是因为委托给了库。

原始 StepStone 版本的标准库非常小。现在大多数 Objective-C 代码使用基于 NeXT Foundation 框架的东西（无论是 Apple 的 Foundation、GNUstep Base 库还是 libFoundation）作为标准库。这提供了引用计数内存管理、标准数据结构、转发机制等。

## 声明 Objective-C 类型

```objective-c
NSMutableArray *mutableArray = [NSArray
new];
NSArray *array = mutableArray;
NSObject *object = array;
  id obj = mutableArray;
mutableArray = (NSMutableArray*)object;
  mutableArray = obj;
```

*自：`cast.m`*

## 声明 Objective-C 类型

始终通过指针引用。

在 Objective-C 的早期实现中（它会从 Objective-C 生成纯 C 代码），类被转换为描述对象布局的结构体定义。你仍然可以在 GCC 的错误信息中看到这种遗留，它偶尔会将对象称为“结构体（structures）”。



在 C 中，你需要显式的类型转换才能将任何结构体指针转换为其他类型的结构体指针。这一规则在 Objective-C 中稍微放宽了。任何对象的布局都由根类中的*实例变量 (ivars)* 定义，然后由层级结构中后续每个类中的实例变量定义。子类只能添加新变量，而不能删除或重新排列父类中的变量。这意味着，从内存布局来说，将指向一个类实例的指针转换为另一个类的指针总是安全的。

从面向对象的类型系统的角度来看，这也是安全的；任何子类始终会响应父类响应的所有消息。

Objective-C 中的对象指针通过类名标识，后跟一个星号（`*`），就像 C 语言结构体指针一样，但不需要 `struct` 关键字。你总是可以隐式将指向一个类实例的指针转换为其父类类的指针。这甚至对于间接子类也有效。例如，`NSMutableArray` 是 `NSArray` 的子类，而 `NSArray` 是 `NSObject` 的子类。你可以将 `NSMutableArray` 转换为 `NSArray` 或 `NSObject`。然而，反方向的转换需要显式转换。

Objective-C 还引入了一种新的指针类型：`id`。在转换规则方面，它大致类似于 `void*`。你可以隐式地将任何对象指针转换为 `id`，也可以隐式地将 `id` 转换为任何对象指针类型。

如果你习惯于无类型语言（如 Smalltalk、Ruby 或 Python），那么可能会诱惑你通独使用 `id` 类型。这在大多数情况下是安全的，尽管有一个例外。Objective-C 使用消息名称进行查找，并且不包含任何类型信息。这意味着你可以声明两个不同的（在不同类中）具有相同名称但类型不同的方法。当编译器生成消息发送时，它会使用接收者的类型来确定栈帧的布局。当在任何地方只有一个名为该名称的方法被发布时，就不需要类型信息。如果你想从外部对象访问实例变量，也需要静态类型，但这样做通常被认为是不良风格。虽然不需要指定静态类型信息，但通常是一个好主意。除了刚才提到的那种情况，它不会影响代码生成，但它会被编译器的语义分析阶段使用。这有助于在编译捕捉某些错误。

例如，如果你尝试向 `NSArray` 实例添加对象，编译器会警告你该对象不响应相关消息。这让你检查自己是否真的想用 `NSMutableArray`，或者是否需要为数组创建一个拷贝。

**注意：**在 C++ 中，通常使用 `const` 关键字描述对象为不可变。在 Objective-C 中，`const` 实际上是无用的。它指定对象的实例变量可能被直接修改，但这种情况很少发生。它不会改变可以发送给对象的消息，因此声明为 `const` 的对象仍然是可变的。

大多数时候，需要区分可变实例和不可变实例，Objective-C 程序员使用可变子类模式，即一个不可变类有一个可变子类。你可以隐式地将可变版本转换为不可变版本，但你不能让不可变实例变为可变。

`Class` 类型类似于 `id`，但它可能指向类。在 Objective-C 中，类是一个对象，所以你总是可以用 `id` 代替 `Class`，就像你可以用 `id` 代替特定的对象类型一样。标准 Objective-C 头文件中还定义了其他类型。¹ `SEL` 类型用于选择器（selectors），我们将在本章稍后部分查看它们。

¹如果你使用 Clang 编译，这些类型中的大多数都有内置定义，因此头文件是可选的。

最后一个是 `IMP`，代表实例方法指针（Instance Method Pointer）。该类型是指指向 Objective-C 方法的指针。大多数情况下，你完全不需要使用这种类型。它只用于 Objective-C 的某些非常动态的特性以及优化。我们将在第 19 章中查看你可能会使用它的地方。

## 发送消息

```objc
[anObject autorelease];
[anObject addObject:anotherObject];
[anObject setObject:anotherObject
      key:aThirdObject];
```

源：`exampleMessages.m`

Objective-C 对 C 语言的最重要的改进是发送消息。正如我在上一章中提到的，消息是一种高层次的流控制。

这是 Objective-C 中往往让来自 C++ 和 Java 等语言的人感到畏畏的部分，因为其语法直接取自 Smalltalk，对于更熟悉 C 语法的人来说看起来非常诡异。这是刻意为之。C语言中没有任何行为与 Objective-C 消息发送的行为相同，因此引入新语法突显了你也拥有了新的语义。记住 Tom Love 将其描述为一种混合语言，在纯 C 部分和“对象世界”之间有清晰的语法分离，对象世界具有类 Smalltalk 的语法来配合类 Smalltalk 的语义。

最简单的一种消息发送是不带参数的。这方面的一个例子可能是发送给数组的 `-count` 消息。注意消息前的减号。加号用于表示发送给类的消息。例如，你可能会获取数组中元素的数量：

```objc
size = [anArray count];
```

此段代码获取了数组的元素数量并将其存储在变量中。在 C++ 或 Java 等语言中，相应的操作类似于：

```cpp
size = anArray.size();
```

带有一个参数的消息看起来非常相似。如果你想向数组添加对象，你会使用：

```objc
[array addObject:anObject];
```

当消息有多个参数时，情况开始变得有点不同。与 Smalltalk 一样，每个参数都有独立的名称，所以你可以将对象插入特定的索引：

```objc
[array insertObject:anObject atIndex:anIndex];
```

从冒号可以看出它接受两个参数，从冒号之前的文本可以看出这些参数应该是什么。如果你向没有实现该方法的对象发送消息，将使用一系列回退方法。在默认实现中，最后一种将抛出异常（你可以在运行时捕获并绕过）。你也可以在发送消息之前询问对象是否知道如何处理。我们将在第 19 章中查看如何这样做。

在 Objective-C 中，像 Smalltalk 一样，类也是对象。你可以向它们发送消息，就像向对象发送一样。

注意：如果你向 `nil`（常量定义为 `(id)0`）发送消息，不会产生错误。相反，你会得到一个零值。这非常有用，因为你可以对之前消息发送的结果发送一串消息，如果其中一个返回了 `nil`，那么其余的仍然可以工作。这消除了 Objective-C 代码中许多对 `NULL` 的测试。向 `nil` 发送返回结构体的消息的行为是未定义的。如果你在在 SPARC 上编译的代码中执行此操作，程序将由于非法指令信号崩溃。在 OS X 上，结构体将填充随机值，就像栈上未初始化的结构体一样。在向对象发送返回结构体的消息之前，你应该始终检查对象是否为 `nil`。

这样做时，使用类名作为接收者。向类发送消息的最常见目的是创建该类的实例。在 Objective-C 中，类负责创建自己的实例。在 C++ 或 Java 中没有对应的 `new` 关键字。最接近的是 `+new` 消息，你可以将其发送给类。例如，你可能会创建一个可变数组：

```objc
id array = [NSMutableArray new];
```

尽管这看起来非常相似，但这种语言不保证此消息会产生什么结果。某些类可能会创建子类的实例，而某些类可能会返回单例实例。仅按照惯例，这为你提供了接收者的新实例。

## 理解选择器 (Selectors)

```
SEL new = @selector(new);
SEL set = @selector(setObject:forKey:);
```

来自 `selector.m`

在 C 语言中，你通过名称引用函数。函数名也可以用作指向该函数的指针。当你将 C 代码编译为汇编代码时，函数变成一个标签，可以通过调用指令或指令序列访问。

Objective-C 的流程控制更具动态性。你可以获取一个方法的指针，但在大多数情况下，你希望向对象发送一个特定的消息，而不是调用一个特定的方法。如果你调用一个特定的方法，你必须完全确定接收者确实是你预期的那个类。

在 C 语言中，你经常会将函数指针作为其他函数的参数。然后该函数将调用传递给它的函数。这的一个常见例子是 C 标准库中的 `qsort()` 函数。它对进行排序。

你可以使用选择器通过名称调用方法，正如我们将在第 19 章看到的。Foundation 框架中的许多方法接受选择器作为参数。这些用法与接受函数指针作为参数的 C 函数非常相似，用于延迟执行、回调、集合排序等。

## 声明类

```
@interface Integer : NSObject
  int integer;

  -(int)intValue;
  -(void)addInteger:(Integer*)other;
@end
@implementation Integer
  -(int)intValue { return integer; }
  -(void)addInteger:(Integer*)other {
    integer += [other intValue];
  }
end
```

**源自 `integer.m`**

当你创建一个新类时，你需要做两件事：描述它的公有接口并编写它的私有实现。你需要使用 Objective-C 关键字：`@interface`、`@implementation` 和 `@end`。

注意，所有新的 Objective-C 关键字都以 `@` 符号开头。这是因为该符号在 C 标识符中是不允许使用的。相比之下，C++ 引入了诸如 `class` 等标识符，这会破坏任何使用 `class` 作为变量名的 C 代码。

Objective-C 继承了 C 的编译模型，编译器期望单个文件，并通过让预处理器合并各种文件来实现分离。按照惯例，Objective-C 类的接口放在扩展名为 `.h` 的头文件中，而实现则放在 `.m` 文件中。没有人记得住为什么选择 `.m`。Objective-C 的设计者建议它可能代表“模块 (module)”、“方法 (methods)”或“消息 (messages)”。

由于头文件是由预处理器插入编译单元的，在 Objective-C 编译器看到它们之前，这种分离并不是强制执行的。C++ 和 C 中的不透明数据类型也是如此。

Objective-C 的一个稍微意外的方面是，实例变量（Java 和 C++ 称为“字段”）被声明为接口的一部分，而不是实现部分的一部分。这是早期 Objective-C 版本实现方式的产物。每个对象都被转换为 C 结构体，其第一个字段是该类的指针。为了生成这个结构体，编译器需要看到所有子类的所有实例变量。这种方法一个不幸的副作用是，修改类的布局意味着你必须重新编译所有的子类。

现在，有了非脆弱 ABI (non-fragile ABI)，你可以从子类中隐藏私有实例变量。对它们的每个引用都通过一个间接层。偏移量现在是一个变量，而不是编译时常量。

默认情况下，Objective-C 实例变量是保护的，这意味着它们只能由类或其子类访问。如果你在它们前面加上 `@private` 前缀，它们只对类可用；如果加上 `@public`，则可以在任何地方访问。这非常不常见。运行时对访问的检查很少，而且有几种机制可以绕过访问控制，因此通常将所有内容保持为保护状态，仅在私有类中将实例变量设为公开。

> 注意：Apple 的非脆弱 ABI 限制了 iv 偏移变量的可见性，如果你尝试从不同的编译单元访问私有实例变量，将产生硬错误。仍然可以通过使用运行时内省访问私有实例变量，而这种保护在其他运行时是不可用的。

类接口的基本结构包含三个部分。第一部分是新类在层次结构中位置的定义：

```
@interface ClassName : Superclass <protocols>
```

类名紧随 `@interface` 关键字之后。接着是一个冒号，然后是父类的名称。可以设计新的根类，但要正确地做到非常复杂，大多数情况下你将使用 `NSObject` 或 `NSProxy` 作为你的父类。

之后，你可能在在角括号中指定一个用逗号分隔的协议列表。Objective-C 中的协议类似于 Java 中的接口 (interfaces)。它们定义了对象必须实现的方法列表。

接下来是实例变量列表。它与在 C 中定义结构体的语法相同。一个只包含实例变量而没有方法的简单类定义看起来如下所示：

```
@interface NoMethods : NSObject
{
  int integer;
  NSObject *object;
  float floatingPoint;
}
@end
```

在 C 结构体定义中有效的任何内容在在这里都是有效的。如果你使用 Objective-C，你也可以添加。最后，你列出该类实现的公有方法。为了不在此处胡胡造一些内容，让我们看看真实的方法声明：

```
+ (id)new;
- (void)append:(NSString*)NSString;
```

方法声明前的加号表示这是附加到类上的消息。`id` 类型是 Objective-C 引入的一种新类型，大致类似于 C 中的 `void*`，但限于 Objective-C 对象。

注意，返回类型和参数的类型使用了与类型转换相同的语法。这突显了消息发送与函数调用之间的另一个重要区别。方法被编译为 C 函数，并在调用之前将其指针转换为这些类型。

类定义的实现部分要简单得多。它以 `@implementation` 指令开头，包含了类方法的定义，如下：

```
@implementation NewClass
+ (int)classVersion
{
    return 2;
}
- (void)log
{
    fprintf(stderr, "log message received");
}
@end
```

需要说明的一点是，你不需要声明类实现的所有方法。在类接口中声明的方法被视为私有的。调用它们将产生编译警告，类的未来版本可能会停止响应它们。

## 使用协议 (Protocols)

与类一样，Objective-C 中的协议也是对象。协议的行为是 Apple 在现代运行时更改过的内容之一。以前，协议通过名称识别，如果两个协议具有相同的名称，则被认为是等同的。这意味着如果你在不同的库中声明了同名的协议，你就无法判断对象实现了哪一个。更重要的是，你无法查找协议并查看它需要哪些方法。

从 Objective-C 2 开始，协议现在是唯一的。你现在可以通过名称获取协议并对其进行检查。这在旧模型中有时可行，但它取决于编译器是否输出了它的完整定义。

你可以使用 `@protocol()` 关键字获取协议的引用。这样做的主要基于是为了测试协议的遵循性。

```
if (![delegate conformsToProtocol: @protocol(DelegateProtocol)]) {
    testIndividualMethods = NO;
}
```

你可能会在设置代理的方法中使用类似这样的代码段。如果代理遵循协议，则保证实现了该协议中的所有方法，所以你不需要测试每一个。如果它不符合，你可能需要在发送每条消息之前对其进行测试。

协议（Protocols）为你提供了编译时和运行时的检查。你可以通过在类型名后的角括号中放入名称来要求对象符合某个协议。以下是一些示例：

```objc
id <NSCopying> a;
id <NSObject,NSCopying> b;
NSObject<NSCopying> *c;
```

在这里，你可以将任何实现 `NSCopying` 协议的对象赋值给 `a`。赋值给 `b` 的对象必须实现 `NSObject` 协议，任何继承自 `NSObject` 或 `NSPProxy` 的对象都会自动实现。最后，`c` 必须是 `NSObject` 的子类并且实现 `NSCopying` 协议。

如果你将一个对象赋值给要求符合某个协议的变量，而该协议不在其声明的列表中，编译器将生成警告——错误。这不是一个硬错误，因为尽管它没有声明遵守协议，但可能仍然实现了该协议所需的所有方法。

## 为类添加方法

```objc
@interface NSObject (Logging)
-(void)log;
@end
@implementation NSObject (Logging)
-(void)log
{
    NSLog("%@%@", self);
}
@end
```

*自：`logging.m`*

Objective-C 与 C++ 或 Java 等语言之间的最大区别之一是分类（categories）的概念。这些在 Smalltalk 中就已经存在，但是作为一种为了文档将方法分组在一起的方式。在 Objective-C 中，它们允许你为类添加方法，即使你没有源代码的访问权限。

分类的定义结构与类定义相似。分类不能更改类的实例变量，也不能更改其父类，因此这些指令中的这些部分被省略了。类名被添加在类名后的括号中。在前面的代码中，你可以看到一个简单的分类接口和实现，它为 `NSObject` 添加了一个 `-log` 方法。然后你可以向任何对象发送 `-log` 消息，并将其打印到控制台。注意，分类的接口和实现都是可选的。在下一节中，我们将查看为什么指定分类接口。

分类有一个特殊情况，即你声明了一个没有名称的分类接口。这被称为类扩展（class extension）。

## 为类添加方法

```
@protocol Collection
- (BOOL)isEmpty;
@end
@interface NSArray (Collection) <Collection> @end
@interface NSSet (Collection) <Collection> @end
@implementation NSArray (Collection)
- (BOOL)isEmpty
{
  return [self count] == 0;
}
@implementation NSSet (Collection)
- (BOOL)isEmpty
{
  return [self count] == 0;
}
@end
```

*自：`collection.m`*



与其他分类（其他分类应该伴随一个指定分类名称的独立 `@implementation` 指令）不同，在类扩展中声明的方法预计出现在该类的主 `@implementation` 指令中。你可以利用这一点来对私有方法进行前向声明。

使用最新的 Objective-C 编译器，你也可以在类扩展内部声明实例变量。为了使此起作用，你需要在编译时指定 `-fobjc-nonfragile-abi2` 标志。

## 使用非正式协议

```objc
@interface NSObject (InformalProtocol)
  - (id)doSomething;
  @end
  // 仅限 Objective-C 2:
  @protocol InformalProtocol
  @optional
  - (id)doSomething;
  @end
```

*自：informalProtocol.m*

通常，你想定义一组你希望类实现的方法，但这些方法是可选的。这在代理（delegates）中特别常见，你会在向代理发送消息之前，测试代理是否实现了给定的方法。

在 Objective-C 2 中，协议可以包含声明为可选的方法，但在那之前，使用分类实现非正式协议是常见做法。如果你为 `NSObject` 创建了一个接口，但没有为其提供接口定义，那么编译器将假设每个子类都响应接口中声明的消息，因此当你向对象发送其中任何一个消息时，它不会生成警告。

当然，并不是每个对象都会真的实现这些方法，因此在发送消息之前，你需要确保使用 `-respondsToSelector:` 来测试对象是否真的实现了它。

## 使用声明的属性合成方法

```objc
@interface Integer : NSObject
@property (nonatomic,assign) int integer;
@implementation Integer
@synthesize integer;
@end
```

*自：synth.m*

Objective-C 2 的大新增之一是声明属性（declared properties）。它们允许你定义访问器语义的某些方面，如果你不需要任何特殊处理，它们会自动合成相关方法。

属性还引入了一些新语法。它们是基于消息发送实现的。本章开头的示例将同时创建 `-integer` 和 `-setInteger:` 方法。你可以像调用任何其他方法一样调用它们，但你也可以使用点符号表示，如下：

```objc
obj.integer = 12;

int i = obj.integer;

obj.integer += 42;
```

最后一种情况是最有用的。将此扩展到传统的 Objective-C 消息语法看起来如下：

```objc
[obj setInteger:[obj integer] + 42];
```

在属性的语境下，`atomic` 意味着在不使用垃圾回收的情况下，set 和 get 方法将尝试获取同一个锁，因此当你在一个线程中设置它而在另一个线程中获取它时，对象不会被意外释放。在垃圾回收模式下，对于非对象属性，`nonatomic` 没有意义。属性可以是 `readwrite` 或 `readonly`，指示是否支持对其赋值。如果你定义了一个 `readwrite` 属性且没有使用垃圾回收，你还需要定义设置器的语义。

设置器行为有三个选项：`assign`、`retain` 和 `copy`。这些中的第一个通常用于代理，因为保留它们会创建循环。后两个选项仅适用于 Objective-C 对象。对于所有原始 C 类型，`assign` 是唯一的。

## 使用声明的属性合成方法

```objc
@interface NotReallyAtomic : NSObject
@property int a;
@end

int add(NotReallyAtomic *obj)
{
    obj.a += 1;
}
```

*自：nonatomic.m*

注意：有时你可能希望有一个读写属性，但在公共接口中仅设只读。类扩展提供了实现此点的机制。如果你在主接口中声明属性为只读，然后在类扩展中重新声明它，主实现中的 `@synthesize` 指令将创建 setter 和 getter。然而，在类扩展不可见的任何地方使用 setter 将导致编译错误。

使用其他两个选项中的哪一个通常取决于属性类型。如果它没有实现 `NSCopying` 协议，`retain` 是你的唯一选择。如果它实现了，你应该决定属性的别名是否会破坏你的选项，原因应该是显而易见的：非对象的东西不响应 `-retain` 或 `-copy` 消息。这种情况的例外是声明了 `__attribute__(NSObject)` 的 C 指针类型。Core Foundation 对象和块（见“使用闭包”章节）是此类常见的例子。它们暴露在没有显式暴露 Objective-C 类型的头文件中，但它们可以在 Objective-C 中作为 Objective-C 对象使用。

# 使用声明属性合成方法

`code`。如果可能的话，请使用 `copy`；否则，使用 `retain`。对于响应 `-copyWithZone:` 消息并返回 `self` 的不可变对象，这两者是等价的。

一旦你声明了属性接口，就必须提供一个实现。属性只是定义访问器方法的一种方式。上一个示例中的属性 `a` 是通过 `-a` 和 `-setA:` 方法实现的。第一个方法返回属性的值，第二个方法将其设置为新值。

> **注意：** 点符号语法（dot syntax）是 Apple 对 Objective-C 所做的最具争议的改变之一。它违反了 Objective-C 的核心原则之一——即语义应该始终使用新语法——因为它重用了“结构体-字段-访问器”的语法来发送消息。点符号语法对于对于糟糕的设计也非常有用；它鼓励了非常间接的引用，而这违反了迪梅特法则（Law of Demeter）。

你可以自己实现这些方法。你也可以从父类继承它们。如果是此类情况，编译器可能无法看到它们并生成警告。你可以通过为属性提供一行 `@dynamic` 代码来抑制这种警告。这告诉编译器这些方法确实存在，并将在运行时解析。

或者，你可以使用 `@synthesize` 来告诉编译器为你生成访问器方法。合成的属性方法指向与属性同名的实例变量。这些方法会调用运行时库函数，其参数为实例变量的偏移量以及一些指示属性类型的标志位。

在旧的 Objective-C ABI 中，所有实例变量都需要在 `@interface` 描述中声明，以便编译器将它们转换为 C 结构体。在非脆弱性 ABI（non-fragile ABI）中，情况并非如此。`@synthesize` 指令可以创建不属于类公共接口的新实例变量。

# 第 2 章：Objective-C 入门

## 理解 self、_cmd、super

```objc
id method(id self, SEL _cmd, ...);
```

来自：object.m

每个 Objective-C 方法都会被编译成一个函数。该函数有两个隐藏参数：`self` 和 `_cmd`。其中第一个是显而易见的：它是消息的接收者。`self` 将是该类的一个实例。如果是类消息，它将是类本身。在 C++ 中，`this` 关键字几乎等同于 Objective-C 中的 `self`，但有一个关键区别：`self` 不是关键字。它是一个参数名。在 C++ 中对 `this` 赋值会导致错误。而在 Objective-C 中对 `self` 赋值是被允许的。

# 理解 self、_cmd、super 45

第二个隐藏参数是消息的选择器（selector）。这对于消息转发等功能的正常工作是必不可少的。当你向一个对象不知道如何处理的对象发送消息时，它将构造一个封装了消息的 `NSInvocation` 对象，然后将其传递给 `-forwardInvocation:`。

由于这两个隐藏参数都不是关键字，你可以在方法之外将它们作为标识符使用，尽管 C 规范保留了以下划线开头的标识符用于实现，因此最好不要使用 `_cmd`。标准的作用域规则仍然适用，因此你可以在方法内部声明一个名为 `self` 的变量，并隐藏掉作为参数传递进去的版本。如果你这样做，编译器会生成警告，因为这是件很蠢的事，但在语义上是有效的。

`super` 伪变量要复杂一点。它只在用作消息的接收者时才有效。它会生成一条消息发送，其中 `self` 是接收者，但在父类而非当前类中查找方法。这就是你调用重写的方法的方法。

向 `super` 发送消息使用不同的方法查找函数，该函数接受指向 `objc_super` 结构体的指针作为参数。该结构包含了目标类和目标对象。

# 第 2 章：Objective-C 入门

父类在编译时就已经固定了。当你编译一个 Objective-C 类时，所有发送给 `super` 的消息将在类接口中定义为父类的类上进行查找。

对于大多数代码来说，这并不重要，但如果你在使用运行时库函数为类添加方法，就需要记住这一点。如果你要附加到新类上的方法向 `super` 发送消息，它将把消息发送到错误的类上。

值得注意的是，在带有 GNU 运行时的分类（categories）中，向父类发送的消息的实现方式是不同的。类实现上下文与编译器从 `@implementation` 上下文包含的代码生成的类结构体位于同一个编译单元中。只需通过查找并获取父类字段即可找到父类指针。

在分类中，类结构体是不可用的。它必须在运行时查找。这使得从定义在分类中的方法发送的父类消息速度变慢。Apple 运行时通过让链接器解析外部类引用来绕过这个问题。

动态查找的原因是为了支持类置换（class posing），这是一种一个类在运行时替换另一个类定义的技术。在现代 Apple 运行时，不再支持类置换。每个类都将其结构体导出为公共符号，因此链接器将在加载时解析类指针。

类置换与分类之间的交互在旧 Apple 运行时和 GNU 运行时之间细有不同，但你只需简单地避免类置换就可以避免担心这个问题。这本身也是个好主意。有很多边界情况，置换的行为并不如你预期的那样，而且非常容易用它写出对你来说运行良好但

## 理解 isa 指针

```c
typedef struct objc_object id;
struct objc_object {
  id isa;
};
```

来自：object.m

在 C++ 中，`this` 关键字几乎等同于 Objective-C 中的 `self`，但有一个关键区别：`self` 不是关键字。它是一个参数名。在 C++ 中对 `this` 赋值会导致错误。而在 Objective-C 中对 `self` 赋值是被允许的。

在 Objective-C 中，结构体和类是非常不同的。在引入非脆弱性 ABI 之前，你可以在结构体定义中使用来创建相同的布局，但你不能交叉使用类和结构体。

# 第 2 章：Objective-C 入门

对象和结构的区别在于你可以向类发送消息。这是因为结构中的第一个实例变量是指向类的指针。这个实例变量约定命名为 `isa`。当你定义一个新类时，必须记住添加这个变量。

²如果没有定义，Clang 会将其视为内置类型。

标准的作用域规则仍然适用，因此你可以在方法内部声明一个名为 `self` 的变量，并隐藏掉作为参数传递进去的版本。正如 `self` 和 `_cmd` 隐藏参数一样，`isa` 指针只是另一个实例变量；它不是关键字。对比一下 C++ 中调用虚方法的情况。一个具有虚方法的 C++ 对象包含一个指向虚表（vtable）的（隐藏）指针。虚表是一个简单的函数指针数组。当你调用方法时，编译器会解引用虚表指针并调用相应偏移处的函数。

你无法通过虚表来获取对象，它的布局是目标平台 ABI 的，而不是语言的一部分。`isa` 指针非常不同。它是一个显式的实例变量，因此可以像其他实例变量一样访问。它指向一个 `Class`，这是一个由 Objective-C 头文件提供的 `typedef`² 或者是不透明类型或指向公共 C 结构体的指针，取决于运行时。

## 理解 isa 指针

在类结构的具体布局为私有的运行时，你仍然可以找到用于检查它的函数。这些函数可以告诉你实例变量的偏移量、方法和属性的名称及类型签名、父类等。

你可以查看其他对象的 `isa` 指针。`id` 类型定义为一个 C 结构体（无访问控制），仅包含指向类的指针，因此你可以像读取结构体中的任何其他字段一样读取它。强烈不建议这样做。

Objective-C 对象可能会转发消息，你拥有的对象指针可能是一个代理。如果你想获取另一个对象的类，应该向它发送 `-class` 消息。这样做较慢，但在存在代理的情况下不会出错。

你可以通过向对象发送 `-isProxy` 消息来测试对象是否为代理，但如果你已经要发送一条消息了，完全可以直接发送一条消息来获取类。

## 初始化类

```objectivec
@implementation Init
+ (void)load
{
    NSLog(@"+load called");
}
+ (void)initialize
{
    NSLog(@"+initialize called");
}
- (id)init
{
    NSLog("-init called");
    return self;
}
@end

int main()
{
    [AutoreleasePool new];
    NSLog("@main() entered");
    id init = [[init alloc]];
    init = [[init alloc]];
    return 0;
}
```

- 出自：classInit.m

在 C++ 中，你可以通过将函数的返回值赋值给全局或静态变量来执行静态初始化。在 C 中，你可以使用扩展特性（例如 GCC 的 `__attribute__((constructor))`）来实现相同的效果。这些者会导致特定的函数在 `main()` 函数之前被调用。

要正确使用这些特性非常困难。它们调用的顺序是未定义的。Objective-C 有等效机制。当类注册到运行时（runtime）时，类的 `load` 方法会被调用，且在 `main()` 函数之前。

从此方法发送任意消息是不安全的。类本身、其所有父类以及常量字符串类都保证已经加载。其他类可能已经加载，但无法保证，即使它对你有效，如果加载顺序发生细微变化，它也可能失效。

更安全的替代方案是 `+initialize` 方法。当向该类发送第一个消息时，运行时会自动调用它。通常，第一个消息会类似于 `+alloc`，用于创建类的实例，但它也可能是请求类名或单例实例的消息。

`+initialize` 方法允许你对类所需的项进行懒初始化。它不会在 `main()` 函数之前被调用，因此所有内容都已加载，进程处于一个定义良好的状态。

如果你实现了这两个方法，你可以看到执行的顺序。首先，在类一被加载时就会调用 `+load` 方法。当运行时加载器完成完成后，它会调用 `main()` 函数。当你向类发送消息时，会先调用 `+initialize` 方法，然后是你实际调用的方法，最后你可以向返回的实例发送 `-init` 消息。

```text
1 a.out[2690:903] +load called
2 a.out[2690:903] main() entered
3 a.out[2690:903] +initialize called
4 a.out[2690:903] -init called
5 a.out[2690:903] -init called
```

输出自：classInit.m

注意 `+init` 方法只会被调用一次。当你第二次向该类发送消息时，它将被直接投递。`+initialize` 方法的调用也是线程安全的。如果你从不同的线程同时向同一个类发送两个消息，其中一个将阻塞，直到另一个运行完 `+initialize` 方法，然后两个都会继续执行。

## 读取类型编码

```c
typedef struct _s
{
    int i;
    float f;
    NSArray *a;
    char *str;
    unsigned short shorts[5];
} s;

int main(void)
{
    const char *encoding = @encode(s);
    printf("Encoding: %s\n", encoding);
    return 0;
}
```

*源自：type.m*

Objective-C 很大程度上依赖于运行时内省（introspection）。Objective-C 对象可以通过发送消息来被内省，但 C 类型则不然。为了帮助这一点，Objective-C 定义了一种将 C 类型编码为字符串的方法。每种基本类型都被编码为单个字符。例如，`int` 编码为 "i"，而 `unsigned long long` 编码为 "Q"。这种用大写字母表示无符号版本、小写字母表示有符号版本的约定适用于所有整数类型。

这些类型编码包含了任意复杂的 C 类型，正如从 `type.m` 示例的输出中看到的。

# 第 2 章：Objective-C 入门

```text
Encoding: {_s=if@*[5S]}
```

输出自：type.m

此示例给出了包含基本 C 类型、Objective-C 对象和 C 数组的结构体的类型编码。类型编码是由编译器响应 `@encode()` 指令生成的，该指令的使用方式与 `sizeof()` 类似，接收一个类型作为参数并返回类型编码。结构体本身由一对大括号表示。内部是结构体的名称，后面是等号，然后是每个元素的类型编码。

接下来的四个字符显示前四个字段的类型编码。这里有两点需要注意：第一，无论其静态类型信息如何，Objective-C 对象都被编码为 "@"；第二，`char*` 被编码为 `*`。所有指针都被编码为 `^` 后跟指向的类型，但字符串接受了特殊处理。

该编码的剩余部分是数组。它位于方括号中，元素数量后紧跟单个元素的类型。

只要你在 C 类型层级进行任何类型的内省，Objective-C 类型编码就会随处出现。如果你请求它，就能找到。注意：Apple 和 GNU 实现之间的主要区别之一是使用了选择器（selectors）。在 Foundation 框架的最新版本中，你会发现许多接收 block 参数方法。



## 使用闭包

```objectivec
int getCounter(void) {
    __block int counter;
    int(**block)(void) = ^(void) { return counter++; };
    return _Block_copy(block);
}

int main(void) {
    int(^block)(void) = getCounter();
    printf("%d\n", block());
    printf("%d\n", block());
    return 0;
}
```

- 出自：`block.m`

随着 10.6 的发布，Apple 为 C 语言引入了 block。尽管这些语言扩展，但它们通常与 Objective-C 配合使用。block 是闭包。这个名字源于 Smalltalk，Block 封装了变量。创建 block 的语法相当糟糕。它基于 C 函数指针的语法，但用脱字符替换了星号。

block 几乎可以像函数指针一样使用。你可以像调用函数一样调用它们，但你不能将它们转换为函数指针，因为它们的调用约定不同。

在示例中，`getCounter()` 函数返回一个实现计数器的 block。你每次调用这个块的结果比上一次大。这样做是因为创建 block 的作用域内的 `counter` 变量被声明为 `block` 修饰符。

block 引用的任何栈变量都将被复制到堆中并计数。当你调用 `_Block_copy()` 时，如果 block 在栈上，它会被复制到堆上；如果不在，则增加引用计数。

示例中 `getCounter()` 返回的每个 block 都有 `counter` 变量的副本，因为它是一个自动（栈）变量，因此后续的调用都会创建一个新版本。

像 Objective-C 对象一样，block 拥有 `isa` 指针并可以接收消息。它们是 `NSBlock` 私有抽象类的实例，该类实现了 `NSCopying` 协议。

block 的大部分对象行为并未文档。你可以将它们存储在 Objective-C 集合中，但不要依赖它们理解特定消息的能力。在最新版本的 Clang 中，block 也支持内省，将它们的类型暴露为 Objective-C 类型编码。

## 内存管理

如果你来自 C 或 C++ 背景，你可能习惯于跟踪对象的所有权并手动分配和销毁它们。如果你来自 Java 等语言，你可能习惯了让垃圾回收器为你处理这一切。

Objective-C 在语言层级并没有提供任何分配或释放内存对象的机制。这交给了 C 代码来处理。你通常通过向类发送 `+alloc` 消息来分配对象。这会调用类似 `malloc()` 的函数为对象分配空间。

随后向实例发送 `-dealloc` 消息将清理其实例变量并将其删除。

Foundation 框架为这种简单的手动内存管理增加了引用计数。一旦你理解了它的工作原理，会让生活变得简单得多。

# 第 3 章：内存管理

## 保留（Retaining）与释放（Releasing）

```objc
NSArray *anArray = [NSArray array];
anArray = [[NSArray alloc] init];
[anArray release];
```

来自：`retainRelease` 继承自 `NSObject` 有

每个对象都关联有一个引用计数。当这个引用计数达到 0 时，它会被销毁。使用 `+alloc` 或任何相关方法（如 `+new` 或 `+allocWithZone:`）创建的对象，其引用计数从 1 开始。

为了控制对象的引用计数，你向它发送 `-retain` 和 `-release` 消息。正如其名称暗示的，当你想要保留对对象的引用或想要释放现有的引用时，应该使用这些消息。`-retain` 消息会增加对象的引用计数，而 `-release` 消息会递减它。

你也可以向对象发送 `-retainCount` 消息来确定其当前的引用计数。人们很想用它来做优化，并在确定某个对象只有一个引用时调用某些特殊情况。这是一个非常糟糕的主意。正如名称所示，该方法告诉你是对象被保留的引用数量，而不是引用的总数。在栈上创建这些对象的指针时，通常不需要特意向它们发送 `-retain` 消息。这意味着一个对象即使引用计数只有一个，也可能在两个或多个地方被引用。

## 赋值给实例变量

```objc
(void)setString:(NSString*)aString {
    id tmp = [aString retain];
    [string release];
    string = tmp;
}
```

来自：`ivar.m`

在这种这样使用引用计数时，有几点你必须小心。考虑以下简单的 setter 方法：

```objc
(void)setString:(NSString*)aString {
    [string release];
    string = [aString retain];
}
```

来自：`ivar.m`

这看起来很合理。你释放了对旧值的引用，然后保留新值并对其赋值。在大多数情况下，这是有效的，但在少数情况下它无效，这会在调试时产生令人困惑。

如果 `aString` 和 `string` 的值相同会发生什么？在这种情况下，你向同一个对象发送了 `-release` 消息，然后是 `-retain` 消息。如果有其他代码引用了这个对象，它仍然可以工作；但如果没有，第一条消息将导致对象被销毁，而第二条消息将发送给悬悬指针。

该方法的更正确实现是先保留新对象，如本节开头所示。请注意，你应该接收 `-retain` 消息的结果，因为某些对象在被保留时会返回另一个对象。这非常罕见，但偶尔确实会发生。

最后，该方法不是线程安全的。如果你想要一个线程安全的 setter 方法，你需要保留新值，对结果和实例变量执行原子交换操作，然后释放旧值。然而，通常几乎无法推理支持这种细粒度并发的代码，而且它引起的缓存抖动（cache churn）将抵消并行带来的任何性能提升，因此这是一个糟糕的主意。如果你真的需要它，最好使用声明属性（declared properties）来合成访问器，而不是尝试自己编写。

## 避免引用循环（Retain Cycles）

```objc
- (void)setDelegate:(id)aDelegate
{
    delegate = aDelegate;
}
```

**来自：**`ivar.m`

纯引用计数的问题在于它无法检测循环。如果你有两个互相保留引用的对象，那么它们一个都不会被释放。

通常情况下，这不是一个主要问题。Objective-C 数据结构往往是无环的，但在某些常见情况下循环不可避免的。最常见的是委托模式（delegation pattern）。在这种模式下，一个对象通常实现某些机制并将策略委托另一个对象。AppKit 的大部分工作都是这样运行的。

代理需要对对象的引用，而对象也需要对其代理的引用。这立即创建了一个循环。解决这个问题的惯用法是对象不保留它们的代理。如果你将一个对象作为参数传递给 `-setDelegate:` 方法，你需要确保其他某个对象持有它的引用，否则它会被过早删除。

## 自动释放池（Autorelease Pools）

```objc
id returnObject(void)
{
    return [[Object new] autorelease];
}
int main(void)
{
    AutoreleasePool *pool = [AutoreleasePool new];
    id object = returnObject();
    [object retain];
    [pool drain];
    // 对象在此失效。
    [object release];
    return 0;
}
```

> 来自：`autorelease.m`

除了循环，引用计数的最大问题是会有一段很短的时间没有人拥有该引用。在 Objective-C 中，这个问题更为常见。许多方法返回临时对象。如果你返回的是临时对象，它需要被释放；如果你返回的是实例变量，则不需要。

解决这个问题的方案是自动释放池。当你向对象发送 `autorelease` 消息时，它会被添加到当前的自动释放池实例中。当该实例被销毁时，添加到它的每个对象都会收到 `-release` 消息。

`autorelease` 消息是一个延迟的 `-release` 消息。当你不再需要一个对象但其他人可能需要时，向它发送它。

如果你使用 `NSRunLoop`，在每次循环开始时会创建一个自动释放池，并在结束时销毁。这意味着临时对象直到循环结束才会被销毁。如果你正在执行创建大量临时对象的操作，你可能想要创建一个自动释放池，如下：

```objc
id pool = [AutoreleasePool new];
[object doSomethingThatCreatesLotsObjects];
[pool drain];
```

注意，销毁自动释放池时发送的是 `-drain` 消息而不是 `-release` 消息。这是因为在垃圾回收模式下，Objective-C 运行时会忽略 `-release` 消息。在这种模式下，`-drain` 消息为处理器提供了提示，但不会破坏池。

## 使用自动释放构造函数

```objc
(id)object
{ return [[self alloc] init] autorelease; }
```

> 来自：`namedConstructor.m`

我在上一节中提到过，使用 `+alloc` 创建的对象引用计数为 1。事实上，所有对象创建时引用计数都是 1，但通过命名构造函数（如 `+initWithFormat:` 或 `+array`）创建的对象也会被自动释放。

如果你通过这些机制之一创建了一个对象，如果你想保留它，就必须向它发送 `-retain` 消息。如果不这样做，它将在稍后自动释放池时被回收。

## 访问器中的自动释放对象

被销毁。这是在编写你自己的类时需要遵守的一个重要约定。如果有人使用命名构造函数（named constructor）创建了你某个类的实例，他会期望自己不需要手动释放该实例。一个典型的命名构造函数看起来就像本节开头的那个。

请注意，由于这是一个类方法，`self` 对象将是该类本身。通过向 `self` 发送 `+alloc` 消息而不是类名，该方法可以自动处理子类。

```objc
- (NSString*)stringValue
{  return [[string retain] autorelease];
}
```

> 自：`ivar.m`

Foundation 中实现的引用计数另一个常见问题是，你通常不会对仅在栈上引用的对象进行保留（retain）。假设你有像如下下面的代码：

```objc
NSString *oldString = [anObject stringValue];
[anObject setValue:newString];
```

如果 `-setStringValue` 方法是我我之前建议的那样实现，那么当你设置新字符串值时，`oldString` 引用的对象将被删除。这是一个问题。有两种可能的解决方案，都涉及到自动释放池（autorelease pools）。一种是在设置新值时对旧值进行自动释放（autorelease）。另一种就是本节开头 `-stringValue` 方法的定义。

这确保了字符串不会因为该对象执行的任何操作而被意外销毁。另一种常见的惯用法是用 `-copy` 消息代替 `-retain`。如果实例变量可能是可变的，那么这种方法就很有用。如果它是不可变的，`-copy` 将等同于 `-retain`。如果它是可变的，调用者将获得一个对象，该对象不会因为向该原始对象发送的其他消息而发生变化。

## 支持自动垃圾回收

```bash
$ gcc -framework Cocoa -fobjc-gc-only collected.m
$ gcc -framework Cocoa -fobjc-gc collected.m
```

从 OS X 10.5 开始，Apple 在 Objective-C 中引入了自动垃圾回收。这可以让程序员的工作变得更轻松，但在大多数情况下，它会带来性能损失。Apple 的回收器使用大量内存来跟踪活跃引用，因此在 iPhone 上不可用。它也不支持旧版本的 OS X，并且对 GNUstep 的支持有限，因此如果你想编写可移植的代码，应该避免使用垃圾回收。

如果你在垃圾回收模式下编译代码，所有的 `-retain`、`-release` 和 `-autorelease` 消息将被被忽略。编译器将为每个对堆的赋值操作自动插入对运行时（runtime）函数的调用。

代码必须带有垃圾回收支持进行编译才能使用垃圾器。这会在任何对堆内存的赋值上插入一组调用，在 Mac 运行时，这些函数声明在 `objc-auto.h` 中。

这些函数确保垃圾回收器能够感知到写入操作。这些这些是必要的，因为回收器是并发的。它将在后台线程运行，并在无法再找到对对象的引用时删除这些对象。必须通知回收器更新的指针，否则它可能会意外删除你刚刚创建引用的对象。

在为垃圾回收编译时，你有两个选项。如果你使用 `-fobjc-gc-only` 标志编译，你的代码将仅支持垃圾回收。如果你使用 `-fobjc-gc` 标志编译，代码将同时支持引用计数和自动垃圾回收。这在你编译框架时非常有用。你仍然必须记得在正确的位置添加 `-retain` 和 `-release` 调用，但你框架的用户就可以可以在开启或不开启回收的情况下使用它。

# 第 3 章：内存管理

```objc
/* Write barriers. 由编译器使用。 */
OBJC_GC_EXPORT id objc_assign_strongCast(id val, 
id *dest);
OBJC_GC_EXPORT id objc_assign_global(id val, id *
dest);
OBJC_GC_EXPORT id objc_assign_ivar(id value, id 
dest, ptrdiff_t offset);
OBJC_GC_EXPORT void *objc_memmove_collectable(
void *dst, const void *src, size_t size);
OBJC_GC_EXPORT id objc_read_weak(id *location);
OBJC_GC_EXPORT id objc_assign_weak(id value, id *
location);
```

> 自：`objc-auto.h`

## 与 C 互操作

在垃圾回收模式下，并不是所有的内存都会被扫描。任何通过 `malloc()` 分配的内容对垃圾回收器都是不可见的。如果你将一个对象指针作为 `void*` 参数传递给 C 函数，然后该函数将其存储在 `malloc()` 分配的内存中，它将对回收器变得不可见，尽管仍有对它的引用，它也可能被释放。

## 使用弱引用

通常，你会在执行此操作之前向对象发送 `-retain` 消息，但这在垃圾回收模式下不起作用。相反，你必须使用 `CFRetain()` 函数。这会增加对象的引用计数，无论回收器是否在运行。回收器只有在对象的保留计数为零且在追踪的内存中找不到对它们的任何引用时，才会释放对象。

当你完成一个不在回收器范围外的引用后，你需要调用 `CFRelease()`。遗憾的是，这并不是你需要使用这些函数的唯一情况。在某些情况下，当你将对象作为回调函数的参数传递时，也需要使用它们。

```objc
@interface WeakDelegate : NSObject
{
    __weak id delegate;
    @property __weak id delegate;
@end
@implementation WeakDelegate
    @synthesize delegate;
@end
```

> 自：`gc.m`

Apple 垃圾回收实现中最棒的特性之一是存在零弱引用（zeroing weak references）。未被保留的指针在垃圾回收之前的 Objective-C 文档中通常被称为“弱引用”。这些引用允许在对象的生命周期之外持续。遗憾的是，没有自动的方法来判断它们是否有效。

**注意：** 引用环境中的弱引用（例如引用代理）通常用于消除循环引用。在追踪环境中不需要这些，因此你可以在代理以及任何可能出现循环引用的地方使用强引用。

如果你在垃圾回收模式下声明对象指针 `__weak`，你将获得一个零弱引用。垃圾回收器在判断对象是否活跃时不会计算它。如果对对象的所有引用都是弱引用，它就可以被销毁。之后，读取弱引用将返回 `nil`。

弱引用通常用于通知等情况。你会对对象保持弱引用，只要它在其他地方被引用就保持消息，然后你可以对其清理。

Cocoa 现在提供了一些可以进行弱引用的集合。旧版本的 Foundation 框架提供 `NSMapTable` 和 `HashTable` 作为不透明 C 类型，并有一组使用它们的 C 函数。这些接口仍然可用，但在 10.5 中，Apple 将这两个 C 类型变成了类。

`NSMapTable` 类型是 `NSDictionary` 的通用形式，可以将任何指针大小的类型作为键值。通过垃圾回收，你可以使用该类来存储从强或弱对象指针的映射。这对于诸如 `NSNotificationCenter` 之类的功能非常有用，这样对象在注册通知时可以被回收，并在这种情况发生时可以自动从通知中心中移除。

## 分配扫描内存

```objc
id *buffer =
NSAllocateCollectable(
10 * sizeof(id),
NSScannedOption);
```

> 自：`gc.m`

如果你通过 `malloc()` 分配内存，它对垃圾回收器是不可见的。如果你想要，例如，一个包含对象的 C 数组，这就是问题。我们已经看了解决此问题的的一种解决方案。你可以对要存储的对象调用 `CFRetain()`。

对旧值执行 `CF-Release()`，然后将它们交换。

这并不是理想的，尽管它可以正常工作。



另一种选项是从垃圾回收器分配一块内存区域。`NSAllocateCollectible()` 函数类似于 `malloc()`，但有两个重要的区别。

第一，它返回的内存是被垃圾回收的。它没有对应的 `NSFreeCollectible()` 函数。当指向缓冲区的最后一个指针消失时，该缓冲区将被回收。

> 注意：Apple 的垃圾回收器不支持内部引用（interior references），因此你必须确保保留一个指向该区域起始位置的指针。指向缓冲区中间位置的指针不会阻止它被释放。

第二个区别是，该函数的第二个参数定义了你想要的内存类型。如果你将将缓冲区用于存储 C 类型，只需在这里传递 0 即可。如果你传递了 `NSScannedOption`，返回的缓冲区将被扫描为可能的对象指针所在位置，以及指向由 `NSAllocateCollectible()` 返回的其他内存区域的指针。

## Common Objective-C 模式

每种编程语言都鼓励一套不同的设计模式。理解 Foundation 框架中通用的常用模式，会让理解整个框架以及编写 Objective-C 代码变得简单得多。

本章概述了 Objective-C 中一些最常见的模式。如果你想阅读更多内容，可以在 Erik M. Buck 和 Donald A. Yacktman 写的《Cocoa Design Patterns》（Addison-Wesley, 2009）中找到更详细的概述。

## 支持两阶段创建

```objc
NSMutableString *buffer = [NSMutableString alloc] init];
NSArray *array = [[NSArray alloc] initWithObject: buffer];
```

源自：`allocInit.m`

你可能已经见过的一种模式是*两阶段创建模式*（two-stage creation pattern）。在传统的、NeXT 时代之前的 Objective-C 中，你通过向类发送 `+new` 消息来创建一个对象。当你实现一个新类时，你会重写 `+new` 来调用父类的实现，然后执行该类的初始化。

NeXT 改变了这一点，将对象的创建和对象的初始化分为两个不同的方法。`+new` 方法仍然有效，但现在它会向类发送 `+alloc` 消息，并向返回的对象发送 `-init` 消息。

`+alloc` 方法本身默认会调用 `+allocWithZone:`。它接受一个 `NSZone` 作为参数。这是一个封装了分配区域（allocation zone）的透明类型。这在 NeXT 系统上被大量使用，为了有效利用这些机器自带的极少量内存。它在 OS X 上表现并不理想，而且并不是所有的类都支持它，因此在许多现代 Objective-C 代码中，这是一个遗留特性。

当你创建一个新类时，你会重写 `-init` 方法，或者提供一个新的指定的初始化器（designated initializer）。

**注意：** 你可以在 GCC 中发现一些旧式创建方式的证据。当使用 `+new` 创建对象时，通常会先创建新实例，然后在类方法中将其赋值给 `self`。GCC 中有一部分代码用于支持这一点，允许从类方法访问实例变量。此功能在很久以前就被废弃了，所以现在你尝试这样做时会收到一个警告。

重写 `+alloc` 是非常罕见的。偶尔，人们这样做是为了实现类级池或强制执行单例，但这非常不常。如果你正在实现一个单例类，你可能会重写 `+alloc`，在存在现有实例时返回该实例。我们将在本章的稍后部分讨论这一点。

## 复制对象

源自：`copy.m`

Foundation 框架包含一个名为 `NSCopyObject()` 的函数。逻辑上可能会认为这会复制一个对象，你几乎是对的。它会创建一个与原始对象相同类的新对象，然后使用类似 `memcpy()` 的方法复制实例变量。

这对于仅有原始 C 类型作为实例变量的对象效果良好，但对于其他对象效果并不佳。对象指针在被复制时需要发送 `-retain` 消息。C 指针需要进行其他处理，特别是当它们是从某些其他库返回的透明类型时。

在没有关于对象之间确切关系信息的情况下，复制函数无法自动创建真正的副本。某些对象甚至不应该支持复制。例如，你期望封装了 socket 的对象的复制语义是什么？你会得到两个封装了同一个 socket 的对象吗？

真正知道如何制作对象副本的只有对象本身。如果对象实现了 `NSCopying` 协议，你可以向它发送 `-copyWithZone:` 消息来获取副本。它接受一个 `NSZone` 作为参数。

如今大多数代码都不再理会 `NSZone` 了。`NSObject` 提供了一个 `-copy` 方法，它只是以默认区域作为参数调用 `-copyWithZone:`。尽管你可能总是调用 `-copy`，但你应该实现 `-copyWithZone:`。

该方法通常开始于向接收者的 `isa` 指针发送 `+allocWithZone:` 消息，这会创建一个新实例。它可能会调用初始化器，也可能自己填充实例变量。

> 注意：如果你继承自一个实现了 `NSCopying` 协议的父类，你应该在你的 `-copyWithZone:` 实现中向 `super` 发送 `-copyWithZone:` 消息，然后只拷贝子类添加的实例变量。

由 `-copy`（或 `-copyWithZone:`）返回的对象应该被视为与 `+alloc`（或 `+allocWithZone:`）返回的对象相同的对待。它的初始引用计数为一，所以你必须记住向它发送 `-release` 或 `-autorelease` 消息以避免内存泄漏。

## 归档对象

```objc
void roundTripWithArchiver(id object, Class coder) {
    NSData *data = [coder archivedDataWithRootObject:object];
    id copy = [decoder unarchiveObjectWithData:data];
    NSCAssert(data, @"Archiving failed");
    NSCAssert(copy, @"Unarchiving failed");
    NSCAssert([object integer] == [copy integer], @"Integer wasn't copied");
    NSCAssert([object string] isEqual:[copy string], @"String wasn't copied");
}
```

源自：`archive.m`

通常，你需要程序的某些状态比单次调用更持久。你可以在属性列表中存储纯数据对象类型，正如我们在第 7 章中看到的，但对于任意对象呢？你可以以自定义（或公共）格式写入数据，然后从这些数据重新对象。为了让几个对象持久化就定义新的文件格式，对大多数程序员来说太费力。

幸运的是，Foundation 在 `NSCoding` 协议中提供了答案。它定义了两个方法：两个方法。许多标准类实现了该协议，你自己实现也容易。

作为参数传递这些方法的对象是 coder。这是一个封装了数据表示的类。在旧系统上，这通常是 `NSArchiver`，但在较新的系统中，它通常会是 `NSKeyedArchiver`。旧的 `NSArchiver`（类型化）接口仅允许写入一个值流。然而，键值存档支持存储类似字典的内容。它们允许存储键值对并以不同的顺序读取它们。

支持归档分为两个部分。你的对象必须能够将自己写入归档，并且必须能够将自己读回来。在 `-encodeWithCoder:` 方法中，你必须将对象的所有状态写入 coder。

这并不意味着对象的所有实例变量。某些对象的实例变量仅用于缓存可以从其他地方重构的信息。通常在唤醒（awakening）之后重构这些信息会更好。

同时支持键值和非键值的 coder 是个好主意。通常，非键值归档器用于瞬态编码（例如通过网络传输），而键值编码器（keyed coders）用于持久化数据。键值归档器为存档原始 C 类型提供了更方便的方法。你可以将这些视为 `encodeInt:forKey:` 消息。旧式的归档器只有一个方法用于存储原始 C 类型，该方法接收 Objective-C 类型编码和指向变量的指针。

```objc
- (void)encodeWithCoder:(NSCoder*)aCoder {
  if ([aCoder allowsKeyedCoding]) {
    [aCoder encodeInt:integer
      forKey:@"integer"];
    [aCoder encodeObject:string
      forKey:@"string"];
  } else {
    [aCoder encodeValueOfObjType:@encode(int)
      at:&integer];
    [aCoder encodeObject:string];
  }
}
```

源自：`archive.m`

相应的加载方法可能会稍微复杂一些。归档器会为它存储的每个对象存储类版本。当你更改对象的实例变量布局时，应该在 `+initialize` 中通过向自己发送 `+setVersion:` 消息来设置此。

`-initWithCoder:` 方法可能需要加载来自程序旧版本的归档文件，因此它应该检查版本，并在对应于旧版本时以不同的方式处理归档。

同样重要的是要记住调用这两个方法的父类实现，并且仅在父类符合 `NSObject` 协议时才这样做。如果它不符合，但某些你想要持久化的状态，则你需要负责归档这些状态以及你子类的实例变量。

```objc
- (id)initWithCoder:(NSCoder*)aCoder {
  if ([aCoder versionForClassName:[self className]] != 0) {
    [self release];
    return nil;
  }
  if ([aCoder allowsKeyedCoding]) {
    integer = [aCoder decodeIntForKey:@"integer"];
    string = [aCoder decodeObjectForKey:@"string"];
  } else {
    [aCoder decodeValueOfObjCType:@encode(int) at:&integer];
    string = [aCoder decodeObject];
    string = [string retain];
  }
  return self;
}
```

源自：`archive.m`

## 创建指定初始化器

```objc
- (id)initWithSelectorName:(NSString*)aSel arguments:(NSArray*)args {
    if (nil == (self = [super init]))
        return nil;
    selector = [asel copy];
    arguments = [args mutableCopy];
    return self;
}

- (id)initWithSelectorName:(NSString*)aSel {
    return [self initWithSelectorName:aSel arguments:nil];
}

- (id)init {
    return [self initWithSelectorName:arguments:nil];
}
```

源自：`designatedInit.m`

我们目前看到的大多数类都是使用 `-init` 方法初始化的。该方法是 NSObject 中的指定初始化器。如果你是 NSObject 的子类，你通常会重写此方法。当创建一个新的 NSObject 子类时，它的所有实例变量都被设置为零。然后，你的初始化器可以将其中一些变量设置为某个值，并获取对象所需的任何其他资源。

> **注意：** NSObject 中的 `-init` 方法什么都不做，它只是返回 `self`。这意味着在 NSObject 的直接子类中，人们很容易避免向 `super` 发送 `-init` 消息。这通常被认为是一种坏习惯，因为 NSObject 的分类可能会将此方法替换为实际执行操作的方法。

并不是所有类都将 `-init` 作为它们的指定初始化器。按照惯例，参数最多的初始化器是指定初始化器。所有其他初始化方法都会调用这一个。

这种方法使得子类化变得简单得多。许多类提供了许多用于初始化的便利方法。如果你必须在每个子类中重写所有这些方法，你最终将产生大量没有任何价值的代码。

如果父类使用指定初始化器模式，你只需要重写一个初始化器。本节中的示例取自 LanguageKit 中的 `LKMessageSend` 类。这是一个表示消息发送操作的抽象语法树节点。父类的指定初始化器是 `-init`，因此该类在其自己的指定初始化器中调用了它。该类重写了 `-init`，但重写的版本调用了该类的指定初始化器。

如果你是该类的子类，你只需要重写 `-initWithSelectorName:arguments:`，并且只有当你添加了需要初始化的实例变量时才需要这样做。向你的类发送 `-init` 消息的人将获得已初始化的实例。

## 强制执行单例模式

```objc
@implementation Singleton
static Singleton *sharedInstance;
+ (void)initialize {
    if ([Singleton class] == self) {
        sharedInstance = [self new];
    }
}
+ (Singleton*)sharedInstance {
    return sharedInstance;
}
+ (id)allocWithZone:(NSZone*)aZone {
    if (sharedInstance && [Singleton class] == self) {
        [NSException raise format:@"May create more than one instance."];
    }
    return [super allocWithZone:aZone];
}
@end
```

源自：`singleton.m`

单例是全局变量面向对象的版本。单例只有一个实例。Objective-C 中有很多这样的类，但它们都遵循相同的模式：运行时确保只创建一个实例。

## 代理

Objective-C 不支持多重继承。这并不是一个巨大的限制，因为多重继承很难用。*代理*（delegation）背后的思想与继承和原型类似：你允许一个对象定义另一个对象的行为子集。

你不会在 Foundation 框架中看到看到这种，但在 AppKit 或 UIKit 代码中非常常见。每个用户界面对象使用代理来让你定义响应用户界面事件的行为。

几种模式与代理有关，它们都与“应优先对象组合而非继承”的通用规则有关。这对于松耦合非常重要，因为它使得代码复用变得简单得多。

如果你有一个 C++ 类通过三个父类提供了行为的某些方面，那么修改它比修改一个将其功能委托给三个其他类的 Objective-C 类要困难得多。

## 提供外面模式

```objc
@interface Control : View
{
    id cell;
}
@end

@implementation Control
-(id)selectedCell {
    return cell;
}
-(BOOL)isEnabled {
    return [[self selectedCell] isEnabled];
}
-(void)setEnabled:(BOOL)flag {
    [[self cell] setEnabled:flag];
    [self needsDisplay:YES];
}
@end
```

源自：`facade.m`

代理的一种常见用途是外面模式（facade pattern）。它在一个公共接口中封装一个或多个私有对象。这在 Objective-C 中非常常用，用于提供类似于多重继承的功能，即一个对象结合了几个不同对象的行为，将其部分功能委托给每个对象。

AppKit 中的 NSControl 层次是这种方法的良好示例。该层次中的类继承自 NSView 的行为，并将行为委托给 NSText 子类。NSView 提供了功能例如图形上下文、事件处理以及与视图层级结构的交互。单元格（cell）提供了绘图等功能。本节顶部的示例是（非常）简化的 NSControl 版本。

当你点击 OS X 上的按钮时，你通常点击的是 NSButton 的实例，它是一个 NSControl 的子类，使用 NSButton 作为其实现。作为程序员，你几乎可以交替使用这些控件，也可以复用它们包含的单元格。例如，如果你在表格或大纲视图中看到按钮，它是由 NSButtonCell 绘制的，而不是 NSButton。

在第 19 章中，我们将介绍如何使用 Objective-C 的转发机制来快速方便地实现这种外模式（façade）。直接通过调用包装对象或多个对象的方法来实现它们也是可能的，而且很常见。

这种方法比多继承要灵活得多，因为它允许同一个类与许多不同的代理配合。在 C++ 中，你会使用模板类来实现相同的效果。它们有不同的优势。Objective-C 版本生成的代码要少得多，这意味着更好的指令缓存利用率。而 C++ 版本则在编译时更容易进行某些类别的优化（主要是内联）。

## 创建类簇



```objc
static Pair *placeHolder;
+ (void)initialize {
    if ([Pair class] == self) {
        placeHolder = [self alloc];
    }
}
+(id)allocWithZone:(NSZone*)aZone {
    if (nil == placeHolder) {
        placeHolder = [super allocWithZone:aZone];
    }
}
+(Pair*)initWithFloat:(float)a float:(float)b {
    return [[Pair alloc] initWithFloat:a float:b];
}
+(Pair*)initWithInt:(int)a int:(int)b {
    return [[Pair alloc] initWithInt:a int:b];
}
```

源自：`classCluster.m`

# 类簇

类簇（Class clusters）在 Objective-C 中非常常见。很多 Foundation 类都是类簇，你可能会发现实现一些自己的类簇是有用的。

类簇是一个抽象的父类，隐藏了具体的子类。这在 Objective-C 中比在许多其他语言中更容易，因为没有用于创建对象的关键字。当你向一个类发送消息请求一个新实例时，该类可能会返回它自身的实例，但也可能返回某些子类的实例。

如果你使用`+arrayWithObjects:`创建一个`NSArray`，你可能会得到一个包装了简单 C 数组的子类。如果你使用`+arrayWithArray;`，你可能会得到一个只引用另一个数组的实例。

另一个很好的例子是 `NSNumber`。它包装了一个单个 C 原始类型值。你可以用两个实例变量来实现它：一个所有可能值类型的联合体（union），另一个用于说明它是哪种类型。这会浪费大量空间且相当复杂。更简单的解决方案是为你支持的每个类型实现一个不同的子类。

大多数类簇都提供了命名的构造函数，例如`+numberWithFloat;`，它们创建正确子类的新实例。如果你通过`+alloc`创建它们，通常会返回一个占位符类，然后在响应`initialize`消息时获得真实的对象。

示例是一个`Pair`类。它没有声明任何实例变量，并且从不被直接使用。如果你向该类发送`+alloc`消息，你会得到一个单例实例。当你向它发送初始化消息时，你会得到两个私有子类之一的实例。

```objc
@implementation IntPair
- (Pair*)initWithInt:(int)a int:(int)b
{
    first = a;
    second = b;
    return self;
}
- (NSString*)description
{
    return [NSString stringWithFormat:@"%d, %d",
        first, second];
}
- (float)firstFloat { return (float)first; }
- (float)secondFloat { return (float)second; }
- (int)firstInt { return first; }
- (int)secondInt { return second; }
@end
```

源自：`classCluster`

这些具体子类中的每一个都很简单。它们都声明了两个实例变量：一个是 `int`，另一个是 `float`。它们各提供一个单一初始化方法（该方法仅从父类调用），然后重写其他方法。这个示例没有在父类中提供任何实用的方法。在实际实现中，你可能会看到根据显示的四个方法在父类中实现的比较或算术方法。或者，它们可能单独的分类（category）中提供。

类簇隐藏了所有的实现细节。你可以更改私有子类的任何方面，而无需修改甚至重新编译使用它们的代码。这就是为什么 Objective-C 中的代码复用比 C++ 等语言常见得的原因之一。在 Objective-C 中，很容易产生具有公共接口和私有实现的代码，而任何代码都不依赖于实现的任何方面。

子类化类簇通常需要实现少数原始方法。基于父类的实现的其他方法都是基于这些核心功能实现的。我们将在“子类化”部分详细讨论这一点。

# 使用运行循环

```objc
[NSRunLoop currentLoop];
```

源自：`timer.m`

定义大多数非平凡 Objective-C 程序结构的设计模式是运行循环（run loop）。在通常情况下，运行循环等待来自一个或多个事件源的数据，然后响应这些数据执行代码，从而提供了一种事件驱动的编程模型。Foundation 框架在`NSRLoop`中提供了运行循环的实现。如果你在编写应用程序，通常会自动获得它的实例。你也可以在命令行工具中手动创建一个。

应用程序的主循环监听来自窗口服务器的事件，对应按键、鼠标移动、触摸事件等。各种其他类向运行循环添加事件源。`NSTimer`类（我们将在第 8 章介绍）会向运行循环添加定时器事件源，例如允许你在特定时间执行某些操作。

通知机制（第 16 章介绍）允许通过运行循环传递程序内任意事件的通知，你还可以通过`NSFileHandle`为文件描述符注册。

运行循环本身与内存管理有关。每个运行循环迭代都有自己的释放池（autorelease pool）。这意味着在运行循环迭代期间发送了释放消息的对象将在迭代结束时被销毁（除非在其他地方保留）。由于这一点，以及运行循环用于传递用户输入事件的事实，最好尽可能减少单个运行循环迭代的工作量。在大多数程序中，你不需要直接与运行循环交互。它在后台运行，而其他类提供了更方便的接口。

# 数字

Objective-C 与 Smalltalk 之间大区别之一是 Objective-C 继承了完整的原始（非对象）C 类型。这些按大小从小到大排列为 `char`、`short`、`int`、`long` 和 `long long` 整数（带有符号和无符号变体），以及两个浮点类型：`float` 和 `double`。它们的所有行为与在 C 中完全相同，包括类型提升规则。你还会发现 Objective-C 编译器支持 `long double` 类型，这取决于架构。

注意，这与 Java 非常相似，Java 也有一少数非对象类型，但存在一些非常重要的区别。在 Java 中，内置类型被定义为固定大小。在 C 中，它们被定义为具有最小精度。例如，规范说 `int` 的大小是“执行环境架构建议的自然大小”，而在 Java 中，它被明确定义为“32位有符号补码整数”。

除了基本类型外，C 还支持通过 `typedef` 关键字为现有类型定义新名称。最常见的原因是规范并没有要求任何标准类型具有特定的大小，只需确保每种类型至少与前一个类型一样大。特别是在当前部署的平台中，`int` 分别为 16、32 和 64 位，因此你不能依赖这些类型的任何特定大小。

OS X 支持 `ILP32` 和 `LP64` 模式。这种缩写用于描述 C 类型中哪些类型的大小。`ILP32` 意味着 `int`、`long` 和指针（pointers）都是 32 位。`LP64` 意味着 `long` 是 64 位数值，并且隐含地其他值更小。相比之下，Microsoft Windows 在 64 位架构上是 `LLP64` 平台；`int` 和 `long` 保持为 32 位，只有指针和 `long long` 是 64 位。如果你假设可以安全地将指针转换为 `long`，就会产生问题——这种操作在世界上几乎包括 Win32 在内的所有平台上都有效，但在 Win64 上行不通。

将指针转换为整数是一个严重的问题。`long long` 类型至少是 64 位，因此在任何当前平台上，它都保证足够大以存储任何指针，但在任何 32 位或 16 位的平台上，它可能太大了。

## 在集合中存储数字

C99 引入了 `intptr_t` `typedef`，它的大小恰好是指针的大小。Apple 引入了一个等效类型：`NSInteger`。它贯穿整个 Cocoa 框架，且大小始终与指针相同。还有一个无符号版本 `NSUInteger`。

在 GUI 代码中，你经常会遇到 `CGFloat` 或 `NSFloat`。它们之间是等价的。它们的大小与指针相同，使得在 32 位平台上是浮点型（`float`），在 64 位平台上是双精度浮点型（`double`）。

## 在集合中存储数字

```objc
6 NSMutableArray *array = [NSMutableArray array];
7 [array addObject:[NSNumber numberWithInt: 12]];
```

> 来自 `numberInArray.m`

所有的标准 Objective-C 集合类都允许你存储对象，但通常你也想在它们中存储基本类型。解决办法是装箱（boxing）——将基本类型封装在对象中。

`NSValue` 类层次结构被用于此。`NSValue` 是一个设计用于封装单个基本值的类。这个类非常通用，是类簇（class cluster）的一个示例。当你创建一个 `NSValue` 实例时，你将得到某个专门用于存储不同类型数据的子类。如果你在 `NSValue` 中存储一个指针，你不希望该实例占据的空间像包含 `NSRect`（一个包含四个 `NSFloat` 的 C 结构体）那样大。

`NSValue` 的一个具体子类特别重要：`NSNumber`。该类旨在封装单个数值，并可以从任何 C 标准整数类型初始化。

这两个类的指定有构造函数都是 `+valueWithBytes:objcType:`。第一个参数是指向某个值的指针，第二个参数是该类型的 Objective-C 类型编码（type encoding）。类型编码是表示特定类型的字符串。它们被广泛用于 Objective-C 的内省（introspection）；你可以获取类中任何方法或实例变量的类型作为类型编码字符串，然后对其解析以获取相关的编译时类型。

你可以使用 `@encode()` 指令获取任何类型的类型编码。这类似于 C 语言中的 `sizeof()`，但它返回的不是整数大小，而是返回作为 C 字符串的类型编码。在处理类型编码时，一个非常方便的技巧是使用 `typeof()` GCC 扩展。它返回表达式的类型。你可以这样结合 `@encode()` 使用：

```objc
NSValue *value =
[NSValue valueWithBytes:&aPrimitive objcType:@encode(typeof(aPrimitive))];
```

这段代码段将返回一个封装 `aPrimitive` 的 `NSValue`，无论基本类型的类型如何都能正常工作。你可以将其封装在宏中，但这样做时要小心不要传递带有副作用的表达式。

注意，你必须传递指向基本值的指针。该方法将使用类型编码来确定基本类型的大小，然后进行拷贝。

更多时候，你会使用其他构造函数之一。例如，如果你想从一个整数创建一个 `NSNumber` 实例，可以这样做：

```objc
NSNumber *twelve = [NSNumber numberWithInt:12];
```

生成的对象可以被添加到集合中。`NSValue` 和 `NSNumber` 实例是有序的，因此你可以对包含 `NSNumber` 实例的集合进行排序。

```objc
NSArray *a = [NSArray arrayWithObjects:
[NSNumber numberWithUnsignedLong:LLONG_MAX],
[NSNumber numberWithInt:-2],
[NSNumber numberWithFloat:300.057],
[NSNumber numberWithInt:1],
[NSNumber numberWithDouble:200.0123],
[NSNumber numberWithLongLong:LLONG_MIN]
];
NSArray *sorted=[a sortedArrayUsingSelector:@selector(compare:)];
NSLog("%@", sorted);
```

> 来自 `numberArray.m`

`JSONArray.m` 示例将一组 `NSNumber` 实例存储在数组中，然后使用 `-compare:` 选择器对其进行排序。从输出可以看出，无论数字是如何创建的，排序都是强制的。

```text
(
  -9223372036854775808
  -2
  1
  200.0123
  300.057
  9223372036854775807
)
```

> 来自 `JSONArray.m`

## 执行算术运算

C 提供了两种处理数字的选项：整数和浮点值。浮点值由两个部分组成：尾数和指数。它们的值是尾数以指数为幂。

浮点值的问题在于它们是二进制的。这意味着它们的精度是根据二进制定义的，这并不总是你所需要的。例如对于金融应用程序，你可能需要精确地存储金额。

一种解决方案是使用定点算术。与其存储美元，你可能会存储分。你必须记住对值进行归一化，并且受限于整数类型的范围。

Objective-C 提供了另一种选择：小数点类型。`Decimal` 类型是一个表示小数值的 C 结构体。有点奇怪的是，没有 C API 来创建这些类型。你必须创建一个 `NSNumber` 然后向它发送 `adecidValue` 消息。

这两种方法都不特别快。小数被表示为数字数组，在两个数字经过归一化后，对这些数字进行操作。你可以预期获得与软件浮点实现相似的性能——可能略差，因为 `Decimal` 没有被广泛使用，因此它不是优化的重点。

`DecimalNumber` 是 `NSNumber` 的子类，所以我们在下一节中过的将 `NSNumber` 转换为字符串的方法都可以按预期工作。你还可以将它们转换为

# 第 5 章：数字

C 原始类型使用标准方法在数字对象上进行访问，但这些方法可能会截断或近似小数值。

## 字符串与数字之间的转换

```objc
6 int answer = [@"42" intValue];
7 NSString *answerString =
8 [NSString stringWithFormat:@"%d", answer];
9 NSNumber *boxedAnswer =
10 [NSNumber initWithInt:answer];
11 NSAssert([answerString isEqualToString:
12 [boxedAnswer string]
13 @"Both strings should be the same"]);
```

来自 `stratum.m`

在数字和字符串之间转换有多种方法。许多表示简单数据的对象都有如 `-intValue` 等的方法，用于返回接收者的整数表示。

`NSString` 在这一系列中拥有几个方法。如果你有一个包含数值的字符串，你可以向它发送 `-doubleValue`、`-floatValue`、`-intValue` 或 `-longLongValue` 消息来将它转换为其中任何一种类型。在 Foundation 的 64 位安全版本中，你也可以向它发送 `-intValue` 消息，这会返回一个 `NSInteger`。

从反方向操作（即从整数获取字符串）也有几种方法。我们在第 6 章中介绍其中一种：`NSString` 上的 `+stringWithFormat:` 方法允许你从任何原始 C 类型构造字符串，就像你使用 `sprintf()` 构造 C 字符串一样。

如果你已经有一个 `NSNumber` 实例中的数字，有两种获取字符串的方法，其中一种是另一种方法的封装。`-descriptionWithLocale:` 方法返回一个根据指定区域（locale）格式化数字生成的字符串。

事实上，这本身并没有执行转换。它是向一个新的 `NSString` 发送 `-initWithFormat:locale:` 消息。格式取决于数字的类型：例如，`double` 将使用 `"@0.16g"` 格式字符串进行转换。这会使用多达 16 位有效数字，并根据需要使用指数。

小数点分隔符取决于区域（locale）。如果你向 `NSNumber` 发送 `-stringValue` 消息，等同于发送 `nil` 作为参数的 `-descriptionWithLocale:`。这使用标准区域（canonical locale），意味着不进行任何本地化，因此结果在任何平台上都是相同的。

## 从字符串中读取数字

```objc
NSScanner *parser =
[NSScanner scannerWithString:@"1 plus 2"];

int operands[2];
NSString *operation;

[parser setCharactersToBeSkipped:
[NSCharacterSet whitespaceCharacterSet]];

[parser scanInt:operands];
[parser scanCharactersFromSet:
[NSCharacterSet letterCharacterSet]
string:&operation];
[parser scanInt:operands+1];
```

来自 `scanner.m`

任何 C 语言程序员学习的最先两件事之一就是使用 `printf()` 和 `scanf()` 函数。这两个函数非常、非常相似——一个几乎是另一个的反向操作——它们允许你构造格式化字符串并从中解析数据。我们已经看到 `NSString` 有一个类似于 `sprintf()` 的粗略对应物，因此你可以从格式字符串和变量构造字符串，但 `sscanf()` 的 Objective-C 等价物是什么呢？给定一个字符串，我们如何从它解析出值呢？答案在于 `NSScanner` 类。这个类是一个非常强大的分词器（tokenizer）类。你创建一个附加到字符串的 `NSScanner` 实例，然后从它一个接一个地扫描值。



你发送给扫描器的消息都具有相同的格式。它们接收一个变量指针并返回一个 `BOOL`，表示操作是否成功。扫描器在字符串中存储当前的扫描索引，仅在扫描成功时增加它，因此你可以尝试用不同的方式解析下一个字符。你还可以通过 `NSCanner` 轻松地实现向前读取和回溯。如果你向它发送一个 `-scanLocation` 消息，它会返回字符串中的当前索引。然后你可以尝试扫描几个内容以获取错误，并通过发送一个 `-setScanLocation:` 消息来回溯，重置旧索引。

`NSScanner` 最强大的方法之一是 `-scanCharactersFromSet:intoString:`。它从当前扫描点开始读取字符串，直到遇到一个不在指定集合中的字符为止。正如我们在第 6 章将看到的，你可以用任何任意字符集构造 `NSCharacterSet` 实例，也可以使用任何标准字符集。

本节开头的示例从字符串中读取了一个数字，然后是一个单词，最后是另一个数字。数字是使用 `-scanInt:` 方法读取的，但单词稍微复杂一些。它使用了一个 `NSCharacterSet`，在此情况下是所有字母的集合。

这并不是该示例中使用的唯一 `NSCharacterSet`。该扫描器还配置为跳过空白字符。发送给扫描器的 `setCharactersToBeSkipped:` 消息告诉它忽略作为参数传递的集合中的任何字符。传递空白字符告诉它跳过任何调用之间出现的空白。如果在向它发送扫描消息时，扫描器开始读取的位置恰好有该集合中的字符，它将跳过这些字符。在解析标记（token）期间，它不会跳过这些字符，因此在字符串中放入“1 2”会被视为两个独立的数字，而不是 12。

## 字符串操作

Objective-C 提供了两种字符串：C 字符串和 Objective-C 字符串（也称为字符串对象）。作为编译器扩展，GCC 也允许你使用 Pascal 字符串，但这些很少见，且仅为了兼容 Pascal 库而支持。

C 字符串是一种非常原始的数据类型。它是字符数组，以 `NULL` 字节终止。

Objective-C 字符串是高级别的抽象。它是一个类的实例，具有三个实例变量：`isa` 指针、一个指向 C 字符串的指针，以及一个包含 C 字符串长度的整数。当你访问 Objective-C 字符串中的单个字符时，使用 `unichar` 类型。这代表单个 UTF-16 字符。

Objective-C 字符串是变长编码。注意 UTF-16 也是变宽编码，且单个字符可能超过一个 UTF-16。让事情更复杂的是，如音符号之类的组合标记可能使用多个 Unicode 字符来表示单个字形。

在 OS X 上，Objective-C 字符串通过 Core Foundation (CF) 字符串无缝桥接（toll-free bridged）。常量 CF 字符串的表示与运行时 Objective-C 字符串类似，但有些不同。它们的 `isa` 指针设置为 Core Foundation 框架中的外部引用，因此它们不需要链接 Objective-C 运行时或 Foundation 框架即可工作。它们还有一个标志字段，允许内部表示为 UTF-8 或 UTF-16，取决于哪种更有效率。

常量 Objective-C 字符串通过在常量 C 字符串字量前加上 `@` 符号来创建，例如 `@"string"`。你也可以通过使用 `CFSTR` 宏创建常量 Core Foundation 字符串，在 C 和 Objective-C 代码中均如此。该宏调用编译器内置函数，生成一个常量字符串对象。

## 创建常量字符串

```objc
const char* cstring = "C string";
NSString *objectstring = @"Objective-C string";
CFStringRef cstring = CFSTR("Core Foundation");
```

来自 `constantStrings.m`

导致一些细微的错误。它将测试两个对象是否相同（identity），而不是相等（equal）。它测试它们是否是同一个对象，而不是它们是否具有相等的值。

比较两个指针比比较两个字符串快得多，甚至比发送消息还要快。在某些情况下，先尝试指针比较可能会更快。指针比较的结果是告诉你：这两个字符串是同一个，或者它们*可能是*同一个。它永远不会告诉你它们绝对是不同的。如果你经常比较相同的字符串，这可以使代码运行更快，但这通常是过早优化的范例。

如果你想测试两个字符串是否相等，应该使用 `-isEqualToString:` 方法。请注意，该方法期望参数是另一个 Objective-C 字符串。你可以通过向它们发送 `-isEqualTo:` 消息来比较任何两个 Objective-C 对象，但由接收者来决定它认为哪些其他对象是相等的。

在本节开头的示例中，编译器通常会合并常量字符串，因此 `twelve` 和字面量 `"12"` 将是同一个对象。这并不是保证的，但没有理由让编译器不这样做。

字符串与 `NSNumber` 实例之间的比较更有趣。你可能认为这会将字符串与向数字发送 `-stringValue` 的结果进行比较，但事实并非如此。

这一点很重要，因为相等必须具有交换律。如果 `[a isEqual: b]` 为真，那么很多代码会假设 `[b isEqual: a]` 为真。这在集合类中尤为如此。例如，如果你向 `NSMutableSet` 插入两个对象，而相等性在一个方向上成立而在另一个方向上不成立，那么结果是未定义的。

通常，当你想要比较字符串（或者实际上是任何对象）时，你不仅想知道它们是否相等，还想知道它们的顺序。这就是字符串对于字符串开始变得有些复杂的地方。给定两个数字，它们之间存在唯一的规范排序。而对于字符串，有几种定义良好的强序（strong orderings）。“etoile”、“Éto” 和 “Etoile” 应该按什么顺序排列？

如果你正在进行不区分大小的比较，第一个和最后一个将具有相同的排名。带音符号的字母是在不带音符号的变体之前之后，还是在所有不带音符号的字母之前之后，取决于区域（locale）。当你有一个文件列表时，如果将 “file10” 排在 “file2” 之前，用户可能会感到恼火，尽管这两个文件名的字典顺序是如此。

对于仅基于字符值的简单比较，你可以使用 `-compare:` 方法。此方法与所有其他比较结果一样，返回一个 `NSComparisonResult`，它是一个具有三个可能值的枚举类型：`NSOrderedAscending`、`NSOrderedSame` 和 `NSOrderedDescending`。如果你在向用户展示数据，应该使用 `-localizedCompare:`。这将根据为用户所选语言定义的规则返回两个字符串的顺序。这二者都是对这个通用比较方法的封装：

```objc
+ (NSComparison*)NSString
compare: (NSString*)aString
options: (NSStringCompareOptions)mask
range: (NSRange)range
locale: (id)locale;
```

这允许你指定一组选项，例如使用 `NSNumericSearch` 用于排序将 10 排在 9 之后，以及使用 `NSCaseInsensitiveSearch` 忽略大小写。将范围作为第三参数允许你将比较限制在接收者的子字符串中，而传递一个区域（locale）则允许你指定非 ASCII 字符的排序规则。值得注意的是，通常将 `nil` 作为区域意味着使用当前区域或规范区域。在这种情况下，传递 `nil` 意味着使用规范区域并对字符值进行数值比较。

## 逐个字符处理字符串

```objc
for (NSUInteger i=0; i<[aString length]; i++) {
  unichar c = [aString characterAtIndex:i];
  // Process c
}
```

*出自：`stringIterateSlow`*

`NSString` 类是一个类簇（class cluster）。它是一个抽象类，当你创建一个它的实例时，你得到的是某个私有子类的实例。任何 `NSString` 子类必须实现两个原始方法：`-length` 和 `-characterAtIndex:`。其中第一个方法返回长度，第二个方法返回字符串中特定索引处的字符。

如果你需要对字符串中的每个字符进行操作，你可以在简单的循环中对其进行迭代，并反复调用此方法。这种方式是非常无效的，因为每个字符都需要发送一次消息。这比访问 C 字符串中的字符要昂贵得多。这个版本还为每个字符发送一次 `-length` 消息，而只有在迭代过程中长度可能会发生变化时才需要这样做。

另一种替代方案是获取一个 C 字符串并对其进行处理。例如，你可以向字符串发送 `-UTF8String` 消息，然后处理返回的 C 字符串。虽然这听起来很合理，但记住该字符串可能很大，并且可能不是以 UTF-8 存储的，因此对象可能需要将其内部表示转换为 UTF-8，分配内存来存储它，然后稍后由自动释放池（或垃圾回收器）清理该块内存。

访问字符串中字符最高效的方法是 `-getCharacters:range:`。ObjectiveC 中以 `get` 开头的方法通常接受一个指向调用者分配的空间的指针并返回数据。这一点很重要，因为避免了每个字符发送一次消息。

## 逐个字符处理字符串

```objc
int semicolons = 0;
NSUInteger length = [str length];
SRange range = {0, 10};
while (range.location < length) {
  unichar buffer[10];
  if (range.location + range.length > length) {
    range.length = length - range.location;
  }
  [str getCharacters:buffer range:range];
  range.location += 10;
  for (unsigned i=0; i<range.length; i++) {
    unichar c = buffer[i];
    if (c == ' ') {
      semicolons++;
    }
  }
}
printf("Source file contained %d semicolons\n", semicolons);
```

*出自：`StringIter`*

注意正确设置范围。否则，你可能会在应用程序中引入一些安全漏洞。记住字符串对象隐藏了它们的编码。这段代码无论字符串如何存储都有效。如果它是 7 位 ASCII 或 UTF-8，转换为 UTF-16 非常快。如果它是 Mac Roman，可能会稍微慢一点，但仍然很快。

# 第 6 章：操作字符串

## 转换字符串编码

```objc
NSString *str =
  [NSString stringWith8String:"some text in a C string"];
const char *utf16 =
  [NSString usingEncoding:NSUTF16StringEncoding];
const char *utf32 =
  [NSString usingEncoding:NSUTF32StringEncoding];
const char *macRoman =
  [NSString usingEncoding:NSMacOSRomanStringEncoding];
```

*出自：`encodings.m`*

在 OpenStep 中，`NSString` 两个常用的方法 `-cString` 和 `+stringWithCString::` 在 C 字符串和 Objective-C 字符串之间进行转换。这些方法的问题在于 C 字符串不是感知编码的。

C 字符串是一个字节数组。你可以在其中存储任何你喜欢的字符数据。对其进行的所有操作都是外部定义的，因此字符编码的知识是外在的。这与 Objective-C 字符串的工作方式相反。

当你将 C 字符串转换为 Objective-C 字符串或反时，必须知道 C 字符串的编码是什么。C 标准是

## 转换字符串编码 123

库函数通过检查环境变量来确定应该是什么。遗憾的是，这会导致各种问题。如果你从套接（socket）或文件读取数据，然后使用这些函数从其构造 Objective-C 字符串，你将得到用户选择的文本编码，而不是创建文件的人所选择的编码。

这些方法现在都已废弃（deprecated），取而代之的是接受显式编码参数的方法。需要记住的一点是，任何多字节编码的默认都是大端（big-endian），这在 Objective-C 流行的 Motorola 68000 系列和 RISC 工作站上是有意义的，但在小端（little-endian）的 x86 处理器上就不那么合理了。

在某些某些拉丁字母变体的国家，最常见的文本编码是 UTF-8。它允许你用一个字节表示任何及大多数其他 ASCII 字符，用两个字节表示最常见的字符。`NSString` 提供了获取和设置 UTF-8 编码数据的便利方法：`-UTF8String` 和 `+stringWithUTF8String:`。在大多数代码中，每当你与 C 字符串之间进行转换时，都可以使用这些方法。

要从某种其他编码的 C 字符串创建字符串对象，你需要使用 `+stringWithCString:encoding:`。

> ¹如果你正在使用表意文字，UTF-8 的效率非常低。

## 124 第 6 章：处理字符串

该方法的第一个参数是 C 字符串，第二个参数是表示编码的枚举类型成员。如果数据来自旧的 Mac，你可能想要使用 `NSMacOSRomanStringEncoding`，这是 Mac OS 在获得旧 Unicode 支持之前的默认编码。如果你需要与旧的 Windows 系统进行交互，在大多数情况下你需要的编码是 `NSWindowsCP1252StringEncoding`。较新的 Windows 系统将使用 UTF-16，但它们更倾向于小端版本 `NSUTF16LittleEndianStringEncoding`。

如果你以特定的编码存储字符串数据，你通常会使用 `NSData` 实例而不是指针。这是一个非常简单的类，它封装了一个内存区域：一个指针和一个大小。因为它是一个对象，你可以对它进行内省（introspect），使用引用计数处理销毁并将其存储在集合中。在许多情况下，这比直接使用指针更方便。

## 修剪字符串

```objc
NSString *str = \
@"String with leading spaces ";
str = [str
stringByTrimmingCharactersInSet:\
[CharacterSet whitespaceCharacterSet]];
str = [str substringFromIndex: 2];
NSAscertain([str isEqualToString:@"String with leading spaces"],
@"Trimming failed"]);
```

源自：`trim.m`

通常，当你有一个字符串时，你想要修剪两端，移除固定数量的字符或来自特定集合的字符。第二种情况的一个常见例子是移除字符串前后的空白字符。Objective-C 字符串对象提供了许多方法来实现这一点。如果你只是想移除字符串的尾部或头部字符，`NSString` 的 `-WithRange:` 方法是最有用的。它将创建一个包含另一个字符串中某个字符范围的新字符串对象。对于不可变字符串来说，这是一个非常廉价的操作；它只是返回一个引用原始字符串中数据的字符串对象，而不会复制字符串。然而，当你在可变字符串上调用它时，它必须复制字符。

要从特定集合中移除字符，你需要理解 `NSCharacterSet` 对象。正如其名所示，该类封装了一个字符集。你可以从字符串创建这些集合，但也有许多预定义的集合，表示特定的定义良好的字符集。

该类的用法类似于 C 语言中的 `ctype.h` 函数。你可以对其发送 `-characterIsMember:` 消息来测试单个字符是否为集合的成员。例如，调用 C 库函数 `ispunct()` 等同于向通过 `+punctuationCharacterSet` 向 `NSCharacterSet` 获取的对象发送 `-characterIsMember:` 消息。

Objective-C 的版本更啰嗦，但它是通用的。字符集对象可以很容易地在代码中传递。`NSString` 类在许多地方使用了它们。例如，你可以请求字符串中给定集合内字符的范围，或者使用字符集定义的分隔符来分割字符串。

## 分割字符串

```objc
NSString *str =
@"String with\twords and spaces";
NSArray *wordsWithTab = [str
componentsSeparatedByString:" "];
NSArray *words = [str
componentsSeparatedByCharactersInSet:
[NSCharacterSet whitespaceCharacterSet]];
```

源自：`split.m`

## 分割字符串 127

在 Objective-C 中分割字符串有三种方法。第一种显而易见：简单遍历字符，直到找到方便分割的地方，然后使用 `-substringWithRange:` 创建新的标记（token）。这在通用情况下可行，但对于本该轻而易举的事来说太费精力了。

在 C 语言中，你可以使用 `strtok()` 函数或废弃的 `strtok()` 函数在发现特定集合中字符的地方分割字符串。`NSString` 上的 `-componentsSeparatedByCharactersInSet:` 方法工作方式几乎完全相同，尽管它接受一个 `NSString` 作为参数而不是字符串。

你可以通过使用 `+characterSetWithCharactersInString:` 构建字符集，使此方法表现得像 `strtok_r()`。`NSString` 方法返回子字符串的 `NSArray`。这与 C 语言函数的作用完全相同；在每有两个相邻字符的地方，你都会得到空字符串。



或者，你可以根据子字符串的出现来分割字符串。当分割符由多个字符组成时，这非常有用。

## 复制字符串

```objc
NSString *staticString = @"a string";
NSString *constantString = [staticString copy];
NSString *stringAlias = [constantString retain];
MutableString *mutableString = [stringAlias mutableCopy];
MutableString *mutableAlias = [mutableString retain];
```

源自：`stringcopy.m`

处理字符串是性能往往比预期慢得的地方之一。在任何具有内存内存的环境中，人们倾向于防御性复制对象以维护清晰的所有规则。

在 Objective-C 中，这种情况并不少见，更多代码面临的是相反的问题：在应该复制的地方保留了对象的引用。当你向 `NSString` 发送 `-copy` 消息时，它的效果与 `-retain` 相同。

你可能在想，为什么我们有两个功能相同的方法？答案很简单：`NSMutableString` 是 `NSString` 的子类。如果你向 `NSMutableString` 发送 `-retain` 消息，你会增加引用计数。如果你发送 `-copy` 消息，你将得到一个新对象。情况可能比这更复杂，因为某些 `NSMutableString` 子类支持写时复制行为，因此你会得到两个引用相同数据的对象，只有在你修改其中一个时才会产生真正的复制。

请记住，向任何 `NSString` 子类发送 `-copy` 消息始终会返回一个不可变字符串。如果你需要一个可变字符串，你必须使用 `-mutableCopy`。

这种模式出现在代码的几处基础框架中。大多数具有不可变父类和可变子类的类都会实现 `NSMutableCopying` 协议。向它们的可变或不可变实例发送 `-mutableCopy` 消息将为你返回一个可变子类的实例。

## 从模板创建字符串

```objc
int a = 12;
float b = 42.0;
const char *cString = "words";
id object = [NSString new];
NSString *string = 
[NSString stringWithFormat:
@"%d, %%f, %%s, %%@",
a, b, cString, object];
```

来自：`formatstring1.m`

如果你有 C 语言背景，你学过的第一个函数之一可能是 `printf()`。这是一个变参函数，它接受格式字符串作为第一个参数。格式字符串的内容随后定义了其他参数的类型。

Objective-C 作为 C 语言的后代继承了格式字符串的概念。Objective-C 的格式字符串与 C 的格式字符串几乎完全一样，但增加了一个。`%@` 格式说明符表示匹配的参数是一个对象。

对象应该知道如何描述自己。每个对象都应该响应 `-description` 消息，该消息返回一个描述对象的 `NSString`。许多类继承自这个 `NSObject`，它只返回类名和对象的内存地址。其他类提供了更方便的方法。例如，集合会将它们的内容导出为 NeXT 风格的属性列表。

**注意：** GNU 调试器 (gdb) 对 `-description` 方法有一些内置支持。当你对对象使用 `print-object` 命令（可以缩写为 `po`）时，它会调用对象的 `-description` 方法。这样做要小心，因为会在被调试进程中运行某些代码，这些代码可能也包含 bug。然而，当它正常工作时，非常有帮助。我们将在第 18 章详细讨论调试。

你可以使用一个类似于 `sprintf()` 的变参方法从格式字符串创建 Objective-C 字符串对象。第一个参数是一个包含某些格式说明的 Objective-C 字符串，其余参数是用于替换格式说明的变量。`formatstring.m` 示例展示了如何将格式字符串用于 `NSString`。该示例从传递给可执行程序的参数构造了一个字符串，并将其写入标准错误。注意，我们需要在这个程序开始时创建一个 `NSAutoreleasePool`。

# 第 6 章：操作字符串

```objc
int main(int argc, char **argv)
{
    [NSAutoreleasePool new];
    MutableString *str =
    [MutableString stringWithFormat:@"%d arguments: %d", argc];
    for (int i=0; i<argc; i++) {
        [str appendFormat:@"%s ", argv[i]];
    }
    NSLog(@"%@", str);
    return 0;
}
```

来自：`formatstring.m`

使用格式字符串会创建一些临时对象，这些对象是自动释放的（autoreleased）。如果你没有自动释放池（autore-lease pool），你将收到一个警告，提示这些对象泄漏了。在这个微不足道的程序中，它们反正是泄漏了；告诉自动释放池去收集它们没有意义，因为操作系统会在进程退出时收回这些内存。

这个示例创建了一个包含传递给程序的参数数量的可变字符串。然后，它遍历剩余的参数，将每个参数（作为 C 字符串）追加到可变字符串中。最后，它将结果传递给 `NSLog()`。

`NSLog()` 函数也使用格式字符串。人们很容易直接将 `str` 作为第一个参数传递。这在有人使用带有百分号 `%` 的字符串作为该程序的参数之前，运行良好。到那时，该函数将查看第二个参数并尝试解释它。不幸的是，并没有第二个参数，所以它将从寄存器中读取一个随机值。如果它将其解释为某种数字，并不是大问题。如果它将其解释为（C 字符串或 Objective-C 对象），它几乎肯定会崩溃。通过传递 `"%@”`，我们告诉 `NSLog()` 只有一个真实的参数，并且它是一个对象。

## 存储富文本

```objc
NSDictionary *keyword = [[NSDictionary dictionaryWithObject:@"keyword" forKey:@"type"] retain];
NSMutableAttributedString *program = [NSMutableAttributedString new];
NSAttributedString *fragment = [[NSAttributedString alloc] initWithString:@"int" attributes: keyword];
[program appendAttributedString:fragment];
```

来自：`richText.m`

字符串仅仅是字符列表。在显示字符串之前，你通常需要其他属性。这些属性描述了字体、大小、对齐方式和下划线样式等。

# 第 6 章：操作字符串

如果你正在编写处理结构化文本的内容——例如 HTML 或另一种语义标记形式（如 DocBook），那么这些属性可能是一级标题或有序列表。

Foundation 框架提供了一个类，用于为字符串分配任意属性。`NSAttributedString` 类允许你将字典附加到富属性字符串（attributed strings）的范围上。这些字典可以包含你想要的任何任意信息，包括语义标记。

AppKit 使用该类，并为字典定义了几个用于提供呈现标记的键。你可以用它将一个 `NSFont` 实例附加到文本范围，并让 AppKit 的文本系统以指定的字体显示该范围的文本。

该示例将程序片段构造为富属性字符串，并定义了用于定义关键字的属性。你可能随后有一个转换器（transform），获取该富属性字符串并生成一个使用呈现属性以便在文本视图中显示的版本，或者另一个用于从此生成 HTML。

记住 `NSAttributedString` 是通用的，这一点很重要。

## 使用集合

与我们看过的其他东西一样，有两种集合：有序的和无序的。前者如往常，是构建在后者之上的。

Objective-C 集合是更高层次的构造。每个 Objective-C 集合与 Objective-C 增加的大部分功能一样，都是一个对象。你通过发送消息与它们通信。

Foundation 框架包含了许多集合类，用于存储有序和无序数据，以及映射（maps）或集合（sets）。Objective-C 的大多数集合类都存储对象。与 C++ STL 集合（它们需要对其可能包含的类型进行完善）不同，Objective-C 集合是异构的。

大多数 Objective-C 集合（如字符串）都使用可变子类模式，即父类实现不可变集合的行为，而子类提供一个可变版本。所有遵循此模式的类都实现了 `NSMutableCopying` 协议，这意味着你可以向集合发送 `-mutableCopy` 消息并获得一个可变的副本，即使原始集合是不可变的。

大多数集合还是类簇（class clusters）。当你创建一个集合时，你将得到某个子类。公共类通常是抽象的。对用户友好的方法都是通过少数原始方法实现的。如果你创建自己的子类，你将需要自己实现这些方法。

## 使用数组

```objc
NSArray *array = [NSArray arrayWithObjects:
    @"array", @"containing", @"string", "objects", nil];
NSMutableArray *mutable = [array mutableCopy];
mutable sortUsingSelector:@selector(localizedCompare:)];
[mutable addObject:[NSNumber numberWithInteger:
12]];
[mutable removeAllObjects];
```

来自：`nsarray.m`

除了 C 数组外，Foundation 还提供了 `NSArray` 类及其可变子类 `NSMutableArray`。它们实现了一种抽象数据类型，从零开始的连续范围内的整数映射到对象。在内部，它可能由 C 数组、跳表列表或其他数据结构实现，取决于它是如何创建的。

例如，如果你通过合并两个不可变数组创建一个数组，你可能会得到一个内部不存储任何内容的复合数组，只需访问另外两个数组。或者你可能会得到一个全新的数组，取决于实现相关 `NSArray` 子类的开发者认为对于这种特定情况下这样做更有效。

一种变长方法，接收一个对象列表作为参数，并使用 `nil` 来表示列表的结束。当你使用变量作为此方法的参数时，必须小心确保没有哪个变量是 `nil`，否则数组将将其视为参数列表的结束并忽略后续的值。

**注意：** 大多数 Objective-C 集合都不允许你将 `nil` 存储为值。如果你需要表示一个空值而不是值的缺失，可以使用 `NSNull` 类。它提供了一个可以通过 `[NSNull null]` 访问的单例对象。

数组是类簇。`NSArray` 中的原始方法是 `-objectAtIndex` 和 `-count`。所有其他方法都是基于这两个方法实现的。当然，某些子类会实现更高效的这些方法，但如果你想创建一个新的 `NSArray` 子类，并且希望父类中的其他方法能够正常工作，你就必须实现这两个方法。

子类 `NSMutableArray` 稍微难一点；它又增加了六个原始方法。不过，大多数情况下你会直接使用数组而不是对它们进行子类。你可以使用 `-addObject:` 将对象插入可变数组（它将其添加到末尾），或者使用 `-insertObject:atIndex:` 将其插入到指定的索引。

## 操作索引

后一种方法会将数组中后续的所有对象向后移动一位以腾出空间。要替换对象，请使用 `-replaceObjectAtIndex:withObject:`。

## 操作索引

```
NSMutableSet *indexSet = 
[indexSet indexSetWithIndex:1];
[indexSet addIndexesInRange(5, 20)];
[array removeObjectsAtIndexes:indexSet];
```

来自：`indexSet.m`

数组通过整数索引。通常情况下，你想对数组中的一组值执行某些操作。一种名为 `NSIndexSet` 的特殊类用于存储一组索引。在内部，它存储的是范围集合（ranges），因此可以非常密集。

索引集的一个常见用途是在枚举数组时收集一组索引，然后在最后将它们全部删除。在枚举集合的同时从集合中删除对象是一个坏主意，在大多数情况下它会抛出异常。如果你将想要删除的每个索引都添加到索引集中，你就可以在完成枚举后一次性地删除它们。

涉及索引集的操作通常比涉及单个索引的相关操作更高效。即使在相对朴素的实现中也是如此，因为你需要发送的消息更少。你还可以避免一些边界检查。Objective-C 数组上的每个操作都会进行边界检查，以确保它不会引用超出数组范围的索引。使用索引集时，接收者只需要将 `-lastIndex` 的结果与数组的最后一个索引进行比较，然后就可以对索引集中的每一个元素进行操作而无需进行边界检查。

和其他集合一样，索引集分为可变和不可变版本。大多数情况下你会使用可变版本。你通过添加和删除单个索引（`NSInteger`）或范围来操作它。你可以使用索引集来存储对任何内容的索引，但它们在与 `NSArray` 结合使用时最有用，因为 `NSArray` 有几个方法设计为接收索引集作为参数。如果你只是想对数组元素的某些任意子集进行操作，通常可以把它们作为创建子数组的替代方案。

## 存储无序对象组

```
NSArray *array = [NSArrayWithObjects:
  @"set", @"object", @"containing",
  @"seven", @"objects", @"not",
  @"eight", @"objects", nil];
NSSet *set = [NSSet initWithArray:array];
MutableSet *mSet = [set mutableCopy];
NSCountedSet *cSet = [NSCountedSet initWithArray:array];
```

来自：`nsset.m`

如果你想存储一个没有定义顺序的对象集合，可以使用 `NSSet` 及其可变子类。这模拟了数学中的集合，因此插入两次同一个对象只会存储其中一个副本。

`NSSet` 如何确定对象之间的相等性是非常复杂的。相等性（Equality）不等同于标识性（Identity）；它不会存储两个相同对象的副本，但也不会存储两个具有相同的对象。它通过向其中一个对象发送 `-isEqual:` 消息，并将另一个对象作为参数，来判断两个对象是否相等。

实现 `NSSet` 最简单的方法是将每个新对象与每个现有对象进行比较。这会极其缓慢，所以 `NSSet` 并不是这样工作的。相反，它使用了 `-hash` 方法。每个对象都应该实现此方法并返回一个整数哈希值。

如果两个对象相等，它们必须具有相同的哈希值。像 `NSSet` 这样的集合根据它们的哈希值放入桶（buckets）中。在测试一个对象是否已经在集合中时，它只需要测试具有相同哈希值的对象即可。

因此，良好的哈希对于这些集合类的良好性能至关重要。幸运的是，作为这类集合中最常用的对象，`NSString` 已经有了良好的哈希实现。

这种方法的一个微小问题是，对象在集合中期间不能改变其哈希值。对于可变对象，在不破坏其他规则的情况下是不可能强制执行的。因此，在对象存储在集合期间不要修改它们是非常重要的。

一种集合是 `NSCountedSet`，它是 `NSMutableSet` 的子类，支持多次添加同一个对象。这为 `NSMutableSet` 增加了一个方法 `-countForObject:`，它返回特定对象被添加到集合的次数。注意：在 Java 中，计数集合被称为 bag。

值得注意的是，`NSCountedSet` 是 `NSMutableSet` 的子类，它的某些方法设计用于允许多次包含实例。

## 创建字典

```
NSMutableDictionary *dict = [NSMutableDictionaryWithObjects:@"1", @"2", nil];
[dict setObject:@"3" forKey:@"3"];
```

来自：`dictionary.m`

字典通过对象进行索引。通常，你想对字典中的一组值执行某些操作。一种特殊的类叫做 `NSIndexSet`，用于存储一组索引。在内部，它存储的是范围集合，因此可以非常密集。

索引集的一个常见用途是在枚举数组时收集一组索引，然后在最后将它们全部删除。在枚举集合的同时从集合中删除对象是一个坏主意，在大多数情况下它会抛出异常。如果你将想要删除的每个索引都添加到索引集中，你就可以在完成枚举后一次性地删除它们。

涉及索引集的操作通常比涉及单个索引的相关操作更高效。即使在相对朴素的实现中也是如此，因为你需要发送的消息更少。你还可以避免一些边界检查。Objective-C 数组上的每个操作都会进行边界检查，以确保它不会引用超出数组范围的索引。使用索引集时，接收者只需要将 `-lastIndex` 的结果与数组的最后一个索引进行比较，然后就可以对索引集中的每一个元素进行操作而无需进行边界检查。

和其他集合一样，索引集分为可变和不可变版本。大多数情况下你会使用可变版本。你通过添加和删除单个索引（`NSInteger`）或范围来操作它。你可以使用索引集来存储对任何内容的索引，但它们在与 `NSArray` 结合使用时最有用，因为 `NSArray` 有几个方法设计为接收索引集作为参数。如果你只是想对数组元素的某些任意子集进行操作，通常可以把它们作为创建子数组的替代方案。

如果你想存储一个没有定义顺序的对象集合，可以使用 `NSSet` 及其可变子类。这模拟了数学中的集合，因此插入两次同一个对象只会存储其中一个副本。



NSSet 如何确定对象之间的相等性是非常复杂的。相等性不等同于标识性；它不会存储两个相同对象的副本，但也不会存储两个具有相同的对象。它通过向其中一个对象发送`-isEqual:`消息，并将另一个对象作为参数，来判断两个对象是否相等。

实现`NSSet`最简单的方法是将每个新对象与每个现有对象进行比较。这会极其缓慢，所以`NSSet`并不是这样工作的。相反，它使用了`-hash`方法。每个对象都应该实现此方法并返回一个整数哈希值。

如果两个对象相等，它们必须具有相同的哈希值。像`NSSet`这样的集合根据它们的哈希值放入桶中。在测试一个对象是否已经在集合中时，它只需要测试具有相同哈希值的对象即可。

因此，良好的哈希对于这些集合类的良好性能至关重要。幸运的是，作为这类集合中最常用的对象，`NSString`已经有了良好的哈希实现。

这种方法的一个微小问题是，对象在集合中期间不能改变其哈希值。对于可变对象，在不破坏其他规则的情况下是不可能强制执行的。因此，在对象存储在集合期间不要修改它们是非常重要的。

一种集合是`NSCountedSet`，它是`NSMutableSet`的子类，支持多次添加同一个对象。这为`NSMutableSet`增加了一个方法`-countForObject:`，它返回特定对象被添加到集合的次数。注意：在 Java 中，计数集合被称为 bag。

值得注意的是，`NSCountedSet`是`NSMutableSet`的子类，它的某些方法设计用于允许多次包含实例。

字典通过对象进行索引。通常，你想对字典中的一组值执行某些操作。

```objc
NSMutableDictionary *dict = [NSMutableDictionaryWithObjects:@":@"2", nil];
[dict setObject:@"3" forKey:@"3"];
```

来自：`dictionary.m`

字典，通常称为 map 或关联数组，提供了通过其他对象索引的对象集合。最常见的，字典通过字符串索引。这并不是唯一的选项，但对可以作为键的类有一些限制。

字典与集合类似，并且相同的约束也适用。作为键的对象必须实现`NSCopying`协议。当你将一个键值对添加到字典时，值会被保留，但键会被复制。如果你传递一个不可变对象（如`NSString`），这种效果等同于保留它。最后，值得记住，只有使用字符串作为键的字典可以使用键值编码（参见第 11 章）。在同一个字典中使用不同类作为键时，你也应该非常小心它们的比较方法在传递其他类的实例时返回正确的值。

你在字典上最常用的方法是`-objectForKey:`，它返回与键关联的对象，如果没有为该键设置对象则返回`nil`。对于可变字典，你通常会使用`-setObject:forKey:`方法在字典中设置键值对。

```objc
for (id obj=[e nextObject];
nil!=obj;
obj=[e nextObject])
{
  [obj print];
}
NSLog("@Fast enumeration:");
for (id obj in a)
{
  [obj print];
}
NSLog("@Using blocks:");
[a enumerateObjectsUsingBlock:
^(id obj, NSInteger idx, BOOL *stop)
{
  [obj print];
}];
NSLog("@Avoiding enumeration:");
[a makeObjectsPerformSelector:@selector(print)];
```

来自：`enum.m`

你对集合执行的最常见任务之一是遍历集合中的每一个元素并进行某些处理。在 Objective-C 中执行此任务有很多方法。因为这是一项常见任务，新的执行方法不断被添加。对于数组，你可以遍历从 0 到`[array count]`的每一个索引并发送`-objectAtIndex:`消息。这是非常低效的。遍历集合的传统方法是使用枚举；一个`NSEnumerator`子类的实例。

> 注意：如果你是从 Java 转过来的，请在脑海中将 *iterator*（迭代器）替换为 enumerator（枚举器），你会发现你熟悉的绝大多数模式仍然有效。

你可以通过向集合发送`-objectEnumerator`消息来获取集合的枚举器。这个对象非常简单。它只响应两条消息，而你可能只会使用其中一个：`-nextObject`。它返回集合中的下一个对象，如果你已经枚举了集合中包含的所有对象，则返回`nil`。

凭借 Objective-C 2，Apple 引入了快速枚举（fast enumeration）。你可以对任何实现了`NSFastEnumeration`协议的集合使用该特性。该协议定义了一个方法，允许通过单次消息发送获取多个对象。确切的数量由调用者和接收者定义。编译器分配一个缓冲区并将其传递给接收者。接收者可以将某些对象拷贝到此缓冲区中；如果它内部以 C 数组（或一组数组）存储数据，则返回其内部存储区域的指针。

该协议中的方法被一种新的流程控制结构——`for..in`循环使用。当你使用它时，编译器将产生两个嵌套循环。在外部循环中，它将调用快速枚举方法，从集合中获取接几个对象。在内部循环中，它将遍历这个 C 数组。

## 遍历集合

你可以在没有编译器支持的情况下使用快速枚举。GNUstep 中的`GSFastEnumeration.h`头文件提供了`FOR_IN`和`END_FOR_IN`宏，这些宏会展开为与编译器用于`for..in`循环的相同的代码。这些宏非常复杂，因此最好不要尝试自己调用快速枚举方法。

从 OS X 10.6，Apple 引入了另一种遍历集合的新方法：使用 blocks。Blocks 是 C 语言的新扩展，但为了与 Objective-C 紧密协作而设计。像 Objective-C 对象一样，blocks 有一个`isa`指针。它指向一个实现`NSObject`协议的私有类，因此可以将 blocks 存储在集合中。它们还支持使用 Objective-C 类型编码进行反射，尽管这种支持尚未成为 OS X 公共接口的一部分。

大多数集合类现在都实现了使用 blocks 进行枚举的方法。使用这些方法可能很方便，尽管这会限制代码的可移植性。你可以通过将`NSEnumerationConcurrent`作为第一个参数传递给类似`-enumerateObjectsWithOptions:usingBlock:`的方法来执行并发枚举。通常当 block 在处理每个元素时需要较长时间执行，这种方法才可能带来性能提升。

每个集合都有不同的通过 blocks 进行枚举的方法。数组版本接受对象的索引作为参数，字典版本同时接受键和值，以此此类推。这些方法会比其他替代方案慢，因为它们需要为每个对象调用一次 block（这与调用函数的开销相同），但它们可以更具便利性。

在某些情况下，你可以完全避免枚举。例如，`NSArray`实现了一个`-makeObjectsPerformSelector`方法，以及另一个接受对象作为第二个参数的版本。如果你在枚举时所做的仅仅是向每个对象发送消息，你可以使用这些方法代替创建循环。

## 在集合中查找对象

```objc
NSArray *array = [NSArray arrayWithObjects:
@"a", @"group", @"of",
@"string", @"objects", nil];
NSSet *set = [NSSet setWithArray: array];
NSInteger i =
[array indexOfObjectIdenticalTo:@group];
if (NSNotFound == i)
 i = [array indexOfObject:@group];
NSString *original = [set member:@"string"];
```

> 来自：`object.m`

`NSArray`和`NSSet`都实现了`-containsObject:`方法，如果集合包含与参数相等的对象，则返回`YES`。这使用了我们之前在讨论集合类时过的相等性概念：如果向一个对象发送另一个另一个为参数的`-isEqual:`消息返回`YES`，则认为这两个对象相等。

在数组中，你可能想确切知道对象是什么，而不仅仅是它是否存在。有两个方法可以告诉你：`-indexOfObject:`和`-indexOfObjectIdenticalTo:`。后者使用指针比较来确定相等性。

所有这些方法在数组中都是缓慢的。它们都需要线性搜索，并且大多数方法需要向每个对象发送消息。通常，你只应该在小型数组或不频繁调的代码路径中使用它们。如果你需要经常执行这种反向映射，最好使用字典或类似的结构来存储这种反向关系。

对于集合，性能会有所不同。由于集合根据哈希值在桶中存储对象，因此集合可以快速排除大量不同的对象。显然，由于集合是无序的，没有用于查找对象索引的方法。但是，有一个方法可以查找与某个对象等等的存储对象。

`NSSet`的`-member:`方法返回与参数相等的存储对象。这对于确保对象的唯一性非常有用。`unique.m`示例展示了一个从 C 字符串构建唯一常量字符串对象的方法。如果你两次向此方法传递相同的 C 字符串，你将两次获得返回相同的`NSString`实例。

请注意，此函数不是线程安全的。在测试字符串是否在集合中与在不在时添加新字符串之间存在潜在的竞态条件。一个线程安全的版本需要你在调用`-member`后获取一个锁。

```objc
static NSMutableSet *unique_strings;
NSString *uniqueString(const char *str)
{
    NSString *new = [[NSString alloc]
        initWithUTF8String:str];
    NSString *old = [unique_strings member: new];
    if (nil != old)
    {
        [new release];
        return old;
    }
    unique_strings addObject:new;
    return new;
}
```

> 来自：`unique.m`

你始终可以使用指针比较来确定相等性，这在某些情况下可以获得巨大的速度优势。

## 集合的类化

```objc
- (NSInteger)count
{
  return [realArray count];
}
- (id)objectAtIndex:(NSInteger)anIndex
{
  return [realArray objectAtIndex:anIndex];
}
```

> 来自：`checkedArray.m`

所有标准集合都是类簇（class clusters）。这意味着为它们创建新的子类并不是简单的。父类是抽象的，而具体的子类是私有的（无法无法化它们）。

每个集合都文档了子类中必须实现的方法。最简单的方法是通过委托：只需将与要子化的集合类型相同的对象作为实例变量。`Array.m`示例使用了这种方法。

`TypedArray`类是`NSMutableArray`的子类。该类中的`realArray`实例变量是一个`NSMutableArray`。它在类的指定初始化器中创建，与其他任何创建`NSMutableArray`的代码一样，实际上是该类某个具体子类的实例。另一个实例变量是一个`Class`，用于检查插入对象的类型。

与异构的标准数组类不同，此版本要求插入的每个对象都是传递给初始化器的类的实例（或子类）。如果你尝试插入其他对象，此版本将静默失败，但你可以轻松修改它以抛出异常。

```objc
- (id)initWithType:(Class)aClass
{
  if (nil == (self = [super init]))
  {
    return nil;
  }
  type = aClass;
  realArray = [NSMutableArray new];
  return self;
}
- (void)dealloc
{
  [realArray release];
  [super dealloc];
}
```

# 第7章：处理集合

```objc
- (void)insertObject:(id)anObject
    atIndex:(NSUInteger)anIndex
{
    if (![anObject isKindOfClass:type]])
    {
        return;
    }
    [realArray insertObject:anObject
        atIndex:index];
}
- (void)removeObjectAtIndex:(NSUInteger)idx
{
  [realArray removeObjectAtIndex:idx];
}
```

源自`checkedArray.m`

`NSArray`或`MutableArray`都能正常工作。

> **注意：** 在 C++ 中，基本方法将是基类中的纯虚方法，编译器将阻止你直接实例化基类，或者任何没有实现这些方法的子类。Objective-C 中没有对应的机制。

子类化的更常见原因是你想为底层表示实现不同的数据结构。例如，如果你打算在数组的一端插入对象，然后从另一端删除它们，你可能想使用可调整大小的环形缓冲区（ring buffer）作为你的数组实现。

如果是这种情况，你仍然应该重写相同的方法，但这次要将它们替换为基于你自己的存储机制的实现。你仍然可以在任何可以使用基类的地方使用你的子类——包括将其传递给其他库——但将使用你自己的存储。

## 日期与时间

在 Objective-C 中，有两个概念包含在时间的通用概念范围内。一个是绝对时间（absolute times），另一个是时间间隔（time intervals）。时间间隔很容易处理。它们是简单的标量，通常以秒为单位。`NSTimeInterval`类型用于存储时间间隔。它通常被定义为双精度浮点值，为大多数用途提供了足够的精度。

你会在各种框架中找到其他表示时间间隔的方法。例如 OS X 上的 QTKit，它将时间间隔存储为有理数。这允许你重复相加它们而不会遇到由于浮点舍入误差导致的漂移，这在处理媒体时非常重要。在电影的长度范围内，复合浮点误差会导致视频和音频轨道明显地不同步。

时间间隔是两个绝对时间之间的差。绝对时间的定义相当困难。时区甚至不同的日历都使得定义绝对时间变得相对困难。Foundation 框架中许多与时间和日期相关的代码都是为了解决这个问题设计的。

## 查找当前日期

```objc
NSDate *now = [NSDate];
now =
[NSDate dateWithTimeIntervalSince1970:time(NULL)];
```

源自`date.m`

`NSDate`类封装了一个绝对时间值。它被存储为两个部分。一个是一个定义良好的固定点：纪元日期（epoch date）。另一个是自该纪元以来的时间间隔。

`NSDate`支持两个标准的纪元日期，它们都根据格里历历定义。一个是 UNIX 纪元，1970 年 1 月 1 日。这个纪元日期是随第一个 UNIX 系统定义的，后来被纳入 ISO C 标准。C 语言`time()`函数将返回自该日期以来的秒数。

另一个纪元时间是在 OpenStep 规范中定义的，被称为参考日期（reference date）。这稍微不那么主观一点；它是当前千纪的开始：2001 年 1 月 1 日。

`NSDate`的意义之一是让你不再需要知道你正在使用哪种参考日期。无论它们内部使用什么纪元，你都可以使用`-compare:`或任何相关方法来比较两个日期。

如果你使用`+alloc/-init`或`+date`创建新日期，它将被设置为当前时间。日期是可变对象，但通常最好将它们视为不可变对象。修改日期的方法只有一个：`-addTimeInterval:`。该方法在 OS X 10.6 中已被弃用，并且在旧代码中可能会引起问题，因为许多人倾向于忘记可以修改日期并直接保留它们，而不是复制它们。

## 第8章：日期与时间

## 为了显示而转换日期

```objc
NSDate *now = [NSDate date];
NSCalendar *cal = [NSCalendar currentCalendar];

unsigned int components = NSYearCalendarUnit;
NSInteger integer = 
[cal components
fromDate: now year];

NSString *date = [NSDateFormatter
localizedStringFromDate: now
DateFormatterLongStyle
timeStyle:
DateFormatterNoStyle];
```

源自`calendar.m`

`NSDate`存储一个绝对时间，但如果你向用户展示自 1970-01-01 以来的秒数，他们可能会有异议。当然，除非你的目标市场是机器人。

在过去的几百年里，西方世界大部分地区在某个时间点采用了格里历标准。最早的采用者（据测）经历了所有所有的 Bug，包括 1582 年的西班牙、葡萄牙和意大利。最近的是中国，在 1929 年。

这为本地化带来了一些严重的问题。如果你有一个代表 UNIX 纪元之前 120 年的日期，你如何显示它？在格里历中它是 1850 年 1 月 1 日，但如果你需要不同日历的日期会发生什么？

`NSFormatter`类为你解决了这个问题。它有一个方便的类方法`+localizedStringFromDate:dateStyle:setStyle:`，返回一个包含本地化日期时间的字符串。第二个第三第三参数分别描述了日期时间和组件所需的详细程度。其范围可以从没有任何，到非常简短的数字描述，再到写出完整月份和日期名称的长描述。

## 计算经过时间



```objc
NSDate *start = [NSDate date];
sleep(1);
NSTimeInterval elapsed = 0 - [start timeIntervalSinceNow];
```

源自`elapsed.m`

你可以通过向其中一个日期对象发送另一个作为参数的`-timeIntervalDate:`消息来找到两个日期对象之间的差。或者，为了找到一个日期是多久以前，你可以向它发送`-timeIntervalSinceNow`消息。如果日期在过去，这将给出一个负数，因此要找出自通过`+date`或`+new`创建日期以来经过了多少时间，你应该从零中减去这个值。

这不是计算经过时间最快的方法。`gettimeofday()`系统调用将在结构体中返回系统时间。这避免了创建对象和发送消息的代价，但工作量大一些，因为你需要处理该结构体。

你自己。该结构将秒和微秒存储在单独字段中，因此减法操作比仅比较两个标量值要费力。

## 从字符串解析日期

```objc
NSDate *isoDate = [NSDate dateWithString:
  @"1982-06-15 06:10:00 +0000"];

Locale *gb = [[NSLocale alloc] initWithLocaleIdentifier:@"en_GB"];
DateFormatter *formatter = [DateFormatter new];
[formatter setLocale:gb];
[formatter setDateFormat:];
[formatter setTextStyle:]; [formatter setTimeToStyle:];
NSDate *britishDate = [formatter dateFormatterString:  @"15/06/1982"];
```

来源：`stringdate.m`

`NSDate`类有一个构造函数，允许你从 ISO 8601 格式的字符串构建日期。当你解析用于交换的文件中的日期时，这非常有用，但在处理用户提供的数据时则并不那么有用。

如果你想从一个本地化的字符串创建日期，你需要回到`NSDateFormatter`类。该类封装了日期格式的一些描述，并可以在日期和字符串对象之间进行双向转换。

当你创建一个日期格式化器时，可以将区域设置（locale）设置为特定的区域，或者留给用户的当前区域设置。然后你可以使用该区域的标准时间和日期格式之一，或者通过`-setDateFormat:`方法显式指定一个。该方法接受模板字符串作为参数，但在大多数代码中都不建议使用它，因为它没有考虑到区域设置。

读取日期的你还有最后一种选择。如果你想从某些自定义格式读取日期，可以使用`NSScanner`从字符串中读取组件，然后构造一个`NSDateComponents`对象并将其传递给`NSCCalendar`来创建日期。`NSScanner`将在第 5 章中介绍。

## 接收定时器事件

```objc
- (void)periodic:(NSTimer*)theTimer
{
    NSLog("Timer fired");
}
- (void)start
{
    SEL sel = @selector(periodic:);
    [NSTimer scheduledTimerWithTimeInterval:1
                 target: self
                 selector: sel
                 userInfo: nil
                 repeats: YES];
    [[NSRunLoop currentRunLoop] run];
}
```

来源：`timer.m`

`NSTimer`封装了一个事件源，它会在特定时间产生事件。这在原理上与`alarm()`系统调用相似，尽管你可以同时调度多个定时器。

你几乎总是使用本节开始示例中的方法来构造定时器。该方法会在同一次操作中创建并调度一个新的定时器。

当时间间隔过去后，定时器将触发。随后，它会向一个对象发送消息。定义此消息的最简单方法是在创建定时器时传递一个选择器（selector）、一个目标（target）和一个字典。选择器必须对应一个接收一个参数的方法：一个`NSTimer`实例。你可以通过向定时器发送`-userInfo`消息来获取字典。

另一个构造函数接受一个`NSInvocation`作为参数。这种方法更难使用，但功能更强大，因为它允许使用带有任何参数的任何消息。

当你这样创建定时器时，它会被自动释放（autoreleased），但会被运行循环（run loop）对象保留。你只有在使用`NSRunLoop`时才能使用定时器。运行循环对象等待来自内核的事件——例如，定时器或文件描述符上的数据变为可用——然后响应这些事件发送消息。

如果你正在使用 AppKit 或 UIKit，你将自动使用运行循环。`NSApplication`和`UIApplication`类都会在内部创建一个运行循环实例。这些类在运行循环中注册，以接收来自显示服务器的用户界面事件的通知，然后将它们传递给窗口等。

如果你正在编写命令行应用程序或服务器，你仍然可以使用`NSRunLoop`。它是 Foundation 框架的一部分，但你必须手动创建它并告诉它运行。这非常简单，是在上一个示例中`-start`方法的最后一行完成的。

## 第 9 章：使用属性列表

属性列表（Property lists）是存储结构化数据的一种方式。你可以在属性列表中存储两个标准的 Foundation 集合类（数组和字典），以及大多数数据类型，如字符串、数字、日期等。

属性列表的设计初图是抽象的。它们不与特定的语言或特定的表示形式绑定。目前有三种定义的属性列表序列化格式。最老的是 OpenStep 属性列表格式。这是一种非常密集且人类可读的格式。遗憾的是，OS X 无法写入旧式的属性列表。它可以读取它们，但规范没有定义存储日期或其他少数几项内容的方法，因此向其写入是无效的。OpenStep 扩展了 OpenStep 属性列表格式，允许你存储所有新格式支持的内容。

在 OS X 中，Apple 引入了 XML 和二进制属性列表格式。XML 格式极其冗长，但优点是它可以被其他兼容 XML 的工具解析，并嵌入到其他 XML 文档中。

二进制表示解析速度非常快且非常密集，但由于是二进制格式，它不是人类可读的。

其他语言的某些库可以处理属性列表。WindowMaker 中的 WINGS 库可以读写它们，Core Foundation 包含的库也是如此。Foundation 框架也可以从 C 代码使用它们。

## 在属性列表中存储集合

```objc
NSArray *array = arrayWithObjects:@"array", @"containing", @"string", @"objects", nil;
[array writeToFile:example.plist atomically:NO];
```

来源：`writeplist.m`

数组和字典类实现了`-writeToFile:`。这些方法允许你使用默认属性列表格式将集合的内容导出到文件中。如果你在第二个参数传递`YES`，该方法将确保磁盘上的表示始终是一致的。它会将属性列表写入临时文件，并在完成后重命名该文件。

运行本节开始的代码将生成一个`example.plist`文件，根节点是一个数组，其中包含四个字符串。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PropertyList 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
 <array>
  <string>array</string>
  <string>containing</string>
  <string>string</string>
  <string>objects</string>
 </array>
</plist>
```

来源：`example.plist`

在当前的 OS X 中，这种方法将使用 XML 属性列表格式。如所示，这非常冗长。旧的 OpenStep 属性列表格式使用括号表示数组，双引号表示字符串，因此体积将小于一半。转换为二进制格式后文件大小从 294 字节减到 82 字节。

对于如此小的属性列表，空间的缩小无关紧要。两种格式都可能放入磁盘上的单个分配单元中，因此它们占据相同的磁盘空间。解析时间对两者来说都是微不足道的。

然而，对于较大的属性列表情况并非如此。例如，Safari 将你的历史记录存储在二进制属性列表中。目前，我的有 15MB。如果将其转换为 XML 格式，它会变成 34MB。解析开销也会增加，无论是在 CPU 时间还是内存占用。

它们不会以默认（XML）以外的任何格式写出属性列表版本。相反，你必须使用`NSPPropertyListSerialization`类，我们将在接下来的几节中讨论它。

所有的属性列表都是层次化的。它们不支持写入循环数据结构。此示例中的第二个数组包含一个指向它自身的指针。在写入属性列表时的行为是未定义的。在 OS X 上，只有在递归指针之前的元素会被存储在文件中。它之后的任何对象都会被忽略。

## 从属性列表中读取数据

```objc
NSArray *array =
[NSArray arrayWithContentsOfFile:@"example.plist"];
NSData *data = [NSData dataWithContentsOfFile:@"example.plist"];
NSMutableArray *mutable =
[PropertyListSerialization
propertyListData:data
mutabilityOption:PropertyListMutableContainersAndLeaves
format:NULL
errorDescription:NULL];
NSAssert([mutable isKindOfClassOfClass:[NSMutableArray class],
@"should have read a mutable array")
[[mutable objectAtIndex:0]
appendString:@"suffix"]];
```

节自：`readplist.m`

读取属性列表（property list）有两种方法。第一种是使用我们刚刚看到的写入方法的反向操作方法。所有支持属性列表序列化的集合类都具有`-initWithContentsOfFile:`初始化器，以及相应的构造函数。

这听起来很简单，但实际上存在一些复杂性。最重要的一点是，属性列表并不存储任何关于可变性的信息。例如，`NSString`和`NSMutableString`的存储方式完全相同。

当你读回一个属性列表时，你应该得到什么？如果你通过向`NSArray`类发送`+arrayWithContentsOf:`消息来读回一个数组，你将得到一个不可变数组。如果你向`NSMutableArray`发送相同的消息，你将得到一个可变数组。

对于属性列表的外部元素来说这没问题，但数组内部的对象呢？在这两种情况下，你得到的都将是填充了不可变对象的数组。这可能不是你想要的。

如果你想读回可变对象，则需要使用`NSPropertyListSerialization`。该类处理属性列表的读取和写入，并提供了比各种集合类更细粒度的控制。

> 注意：如果你阅读 Apple 的最新文档，你会发现你在`NSPropertyListSerialization`上使用的方法被标记为未来将弃用。这是因为该方法是在 Apple 开始使用`error:`参数期间引入的，但在引入`NSError`类之前。遗憾的是，目前推荐的用于替代它的方法尚未提供等等的功能。

当你使用该类读回属性列表时，可以传递一个可变性选项作为参数。这共有三种可能的选项。默认值是所有对象都是不可变的。本章开头示例中的选项走向了另一个极端，使所有内容都变成可变。在数组的一个字符串上添加后缀就演示了这一点。

第三种选项介于中间。它让容器对象变为可变，但其他对象（字符串、数字、日期等）保持不可变。当你只想修改属性列表的结构而不想修改叶元素时，这非常有用。

当你以这种方式读回属性列表时，属性列表序列化类会告诉你属性列表的格式。

## 转换属性列表格式

```objc
*file =
[NSString stringWithUTF8String:argv[1]];
NSData *data = [NSData dataWithContentsOfFile:file];
PropertyListFormat fmt;
id plist = [PropertyListSerialization propertyWithData:data
options: 0
format: &fmt
error: NULL];
if (fmt == NSPropertyListBinaryFormat_v1_0) {
  return 0;
}
data = [PropertyListSerialization dataWithPropertyList:plist
format:NSPropertyListBinaryFormat_v1_0
options: 0
error: NULL];
[data writeToFile:file atomically:NO];
```

来自`makebinaryplist.m`

在 OS X 上，你无法以 OpenStep 格式写入属性列表，但仍然可以使用另外两种形式。通常，你应该使用二进制格式存储私有数据，对任何用户可能想要用其他工具编辑的内容使用 XML 格式。这些并不是硬性规定。属性列表格式的意义在于你可以在这些表示之间进行无损转换，因此你可以在任何地方都使用二进制格式——因为它更紧凑且解析更快——并期望用户在想要修改它们时自行进行转换。

当你使用`NSPropertyListSerialization`写入文件时，可以选择要使用的格式。该类非常有帮助，它会在你读取时告诉你当前属性列表的格式是什么。

> 注意：本节开头示例中使用的方法是 OS X 10.6 引入的。如果你使用的是旧版本的 OS X，可以替换我们在上一节中看到的读取方法以及相应的写入方法。

为了效率考虑，将属性列表以二进制格式存储是非常常见的。你的用户会决定他们想在文本编辑器中翻看这些文件，因此他们会使用`plutil`工具将它们转换为 XML 格式。然后，他们当然会忘记将其转换回来，导致你的程序下次读取它们时会变得很慢。

如果你不是在每次程序运行时都修改属性列表，那么在加载它时检查格式是否仍为二进制格式，如果不是，则按该格式重写，这是值得的。

## 存储用户默认

```objc
NSUserDefaults *def =
[NSUserDefaults standardUserDefaults];
id persistentString =
[def stringForKey:@"example"];
NSLog(@"Old value: %@", persistentString);
if (argc > 1)
{
NSString *new =
[NSString stringWithUTF8String:argv[1]];
[def setObject:new forKey:@"example"];
}
[def synchronize];
```

节自：`defaults.m`

用户默认（user defaults）系统是属性列表最大的用户之一。用户默认系统会从各种来源读取数据。其中最有用的是命令行。默认有多个来源，它们按顺序加载并覆盖之前的来源。最后加载的优先级最高。通过传递参数设置`example`键。当你以这种方式读回属性列表时，属性列表序列化类会告诉你属性列表的格式。

## 存储用户默认

```text
$ ./a.out persistent
a.out[72216:903] Old value: (nil)
$ ./a.out new
a.out[72216:903] Old value: persistent
$ ./a.out -example arg store
a.out[72362:903] Old value: arg
$ ./a.out -example arg
a.out[72362:903] Old value: arg
$ ./a.out new
a.out[72363:903] Old value: store
$ plutil -convert xml \n~/Library/Preferences/a.out.plist
$ cat ~/Library/Preferences/a.out.plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN"
// "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>example</key>
  <string>new</string>
</dict>
</plist>
```

输出自：`defaults.m`

程序被运行了，但在第四次运行时没有被使用，因为一个参数替换了它。在第五次运行中，在没有`-example`参数的情况下，它再次可见。你可以通过`NSUserDefaults`显式地查看各个域，但很少有这种需求。

如果你正在编写一个命令行工具，这提供了一种非常方便的解析命令行参数的方法。你可以在默认系统中存储命令行参数的默认值，并让它们被用户自动覆盖，而无需任何解析代码。

## 在用户默认设置中存储任意对象



```
NSUserDefaults *def = [NSUserDefaults standardUserDefaults];
NSData *serialized = [def objectForKeyForKey:@"color"];

id favoriteColor = [NSKeyedArchiver unarchiveObjectWithData:serialized];

if (nil == favoriteColor) {
    favoriteColor = [UIColor blackColor];
    serialized = [NSKeyedArchiver
        archivedDataWithRootObject:favoriteColor
        setObject:serialized forKey:@"color"];
    [def synchronize];
}
```

*来自：`colordefault.m`*

通常情况下，你想在默认设置中存储基础 Foundation 数据类型以外的内容。一个常见的例子是颜色。如果你允许用户以任何方式自定义界面，通常你他们选择的颜色在程序调用之间保持持久。这很容易；只需在默认设置中存储 `NSColor` 对象即可。

嗯，如果属性列表（property lists）和扩展用户默认支持 `NSColor` 对象，那就很简单了。遗憾的是，它们不支持。不过，你可以在默认设置中存储 `NSData` 实例。如果你有某种将其转换为数据的机制，就可以将其存储在默认设置中。

幸运的是，有一种许多常用对象都支持通用方法。任何实现了 `NSoding` 协议的对象都可以使用 `NSCoder` 子类进行序列化和反序列化。

与属性列表不同，`NSCoder` 机制支持任意对象和循环。遗憾的是，它要求对象实现 `NSoding` 协议，因此它不适用于所有对象。然而，它适用于很多对象，而且复用它来存储默认设置中的对象是非常轻易的。

如果你经常这样做，可以很容易地为 `NSUserDefaults` 写一个分类（category），添加 `-colorForKey` 和 `-setColor:forKey:` 方法。这些方法可以接收一个 `NS` 实例，使用 coder 进行序列化，然后恢复它。

如果你想要一个更通用的解决方案，可以添加 `-setEncodedObject:forKey:` 方法。这将将接收一个 `id<NSCoding>` 作为参数，并使用本章开头示例中的代码进行存储。

如果你想在默认设置中存储不支持 `NSoding` 协议的对象，你有两个选择。第一，你可以为它添加 `NSoding` 支持。这涉及实现 `-encodeWithCoder:` 和 `-initWithCoder:` 方法，你可以在分类中实现这些方法。第二是进行其他类型的转换。许多对象都有 `-stringValue` 和 `-initWithString:` 方法。你只需要在存储之前将它们转换为字符串，并在从默认设置读取它们时从字符串创建新对象，就可以将它们存储在默认设置中了。

## 与环境交互

Objective-C 通常用于类 Unix 平台，并从那里继承了环境的概念。这包括工作目录、环境变量等概念。

在传统的 Objective-C 环境中，你被预期要以与从 C 程序中完全相同的方式获取这些值。通过 OpenStep，Sun 和 NeXT 引入了 `NSProcessInfo` 类，它提供了更高层次的抽象。

此部分的动机之一是，OpenStep 程序预计运行在 OPENSTEP、Solaris 和 Windows NT 上。所有这些平台在环境理念上都有细微差异，因此需要一些抽象来隐藏它们。

## 获取环境变量

```
int main(int argc, char *argv, char **envp) {
    // C 方式
    while (*envp) {
        printf("%s\n", envp);
        envp++;
    }
    printf("Working Directory: %s\n", getenv("PWD"));

    // Objective-C 方式
    [NSAutleasePool new];
    NSDictionary *env = [[NSProcessInfo processInfo] environment];
    for (NSString *key in env) {
        NSLog("%: %@", key, [env objectForKey:key]);
    }
    NSLog("Working Directory: %@", [env objectForKey:@"PWD"]);
    return 0;
}
```

*来自：`env.m`*

环境变量可以通过三种方式访问。标准 C 不提供在 `main()` 函数之外获取它们的方法。在大多数 Unix 平台上，你可以从 `/proc` 文件系统读取它们，但从 C 代码中没有简单的方法可以获取它们。

在 Objective-C 中，你始终可以通过向 `NSProcessInfo` 发送 `-arguments` 消息获取参数。这返回一个包含所有选项 Objective-C 字符串的 `NSArray`。然后你可以按照任何喜欢的方式处理它们。

注意：没有 Objective-C 代码设置环境变量的方法。修改环境变量通常通过调用 函数来实现。这在类 Unix 平台上有效，但在 Windows 上则无效。你可以通过向 `NSTask` 发送 `-Environment` 方法来设置一个新的字典。

## 解析命令行参数

```
int main(int argc, char **argv) {
  [NSAutleasePool new];
  NSUserDefaults *d = [NSUserDefaults standardUserDefaults];
  NSString *file = [d stringForKey:@"file"];
  if (nil == file) {
    fprintf(stderr, "USAGE: %s -file {filename}", argv[0]);
    return 1;
  }
  NSLog("Using file %@", file);
  return 0;
}
```

*来自：`args.m`*

这种方式访问参数并不常见。解析命令行参数最简单的方法（正如我们在上一章看到的）是使用 `NSUserDefaults` 中的 `NSArgumentDomain`。当 Objective-C 程序启动时，所有的命令行参数都会读取并插入字典，该字典会被默认系统使用。

这使得提供命令行参数以及可配置的默认值变得非常容易。当你使用这种方法时，你永远不会与参数交互。相反，你向默认系统请求某个键的值，它会返回一个可能来自持久存储位置的值，也可能来自命令行。

在 EtoileFoundation 框架中，我们提供了一个 `ETGetOptionsDictionary()` 函数，它封装了标准的 `getopt()` 函数。这提供了一种 Objective-C 风格的运行 Unix 风格命令行参数的方法。如果你在 Objective-C 中编写 Unix 风格的工具，可以使用它。否则，使用默认系统更好。

## 获取用户的区域设置

```
NSLocale *locale =
[NSLocale autoupdatingCurrentLocale];
NSString *language =
[locale objectForKey: NSLocaleIdentifier];
NSString *humanReadableLanguage =
[locale displayNameNameForKey: NSLocaleIdentifier value:];
```

来自：`locale.m`

如果你的程序以任何方式与用户直接交互，你可能在某个时间点需要对其进行本地化。Objective-C 为此提供了许多丰富的设施。

`NSLocale` 对象封装了一个区域设置。有几种方法可以获取该类的实例。如果你向它发送 `+systemLocale` 消息，你将获得系统区域设置。然而，这通常不是你应该使用的。它是当用户当前区域设置无法正常工作时的备用区域设置。

你可以通过两种方式获取用户的当前区域设置。发送 `+currentLocale` 消息返回一个封装了当前区域设置的 locale 对象。如果用户选择了新的区域设置，会发布 `NSCurrentLocaleDidChangeNotification`，你可以为新的区域设置获取一个新的 locale 对象。

或者，你可以向该类发送 `+autoupdatingCurrentLocale` 消息。这返回一个始终表示当前区域设置的 locale 对象，即使它发生了变化也是如此。这可能会稍微令人困惑，因为对该对象的具有相同参数的两次连续调用可能会返回不同的值。

如果你想支持在程序运行时更改区域设置，那么避免缓存从 locale 对象返回的数据是非常关重要的。如果你向用户展示了保留在屏幕上的内容，你应该确保监控了这些通知并更新了它们，即使你使用的是一个自动更新的 locale 对象。

## 支持突然终止

```
NSProcessInfo *p =
[NSProcessInfo processInfo];
[p enableSuddenTermination];
// 执行初始化
[p disableSuddenTermination];
// 执行其他不能在此处
// 中断的操作。
modifyFiles();
[p enableSuddenTermination];
```

来自：`suddenDeath.m`

传统上，进程终止有两种选项。进程可以优雅地退出，通过到达一个停止的安全点然后调用 `exit()`，或者到达 `main()` 函数中的 `return` 语句。或者，它也可以突然退出，接收一个未处理的信号，包括诸如段错误之类的信号。

在这两种情况下，内核都会回收其所有的共享资源，但在突然终止的情况下，这些资源中的某些可能被留在了不一致的状态。一个典型的例子是正在修改中的文件。

这在过去是像文字处理器这样的复杂应用程序中的一个大问题。它们会打开文件进行写入，开始修改，然后崩溃，导致文件处于一种非常难以恢复内容的状态。

你可以通过使用大多数 Foundation 对象上的原子写入设施来避免这一点，这些设施会将内容写入临时文件然后将其重命名，因此写入要么完全成功，要么完全失败——它甚至不会处于已失败的状态。

对于 OS X 10.6，Apple 引入了突然终止机制。背后的理论是，许多程序在退出时花费大量时间在对象的析构函数上，而这些对象除了释放操作系统将回收的内存外没有其他影响。通过突然终止，进程可以声明它没有任何未保存的数据。操作系统可以自由地杀死它，而不是请求它优雅退出。

这对于长时间空闲的长期运行后台任务特别有用。它们通常会被内核换出。当你要求它们优雅退出时，需要将大量的代码和数据换入以处理。通过突然终止，交换文件中的页面将只需标记为可重用。

在你的应用程序中支持突然终止非常简单。你调用 `NSProcessInfo` 的两个方法，在某些不能中断的操作的两侧各调用一次。

注意：如果你在带有 `NSDocument` 基础设施的 AppKit 中使用它，你就不需要做任何事情。当任何文档有未保存的数据时，你的应用程序将被标记为不支持突然终止。

这些方法被称为 `-disableSuddenTermination` 和 `-enableSuddenTermination`，但这些名称略有误导性。它们实际上并没有启用和禁用突然终止，而是修改一个计数器。当计数器达到 0 时，应用程序被标记为可杀死。这意味着你可以在不同的线程中使用或嵌套它们而不会产生任何问题。计数器从1开始，所以你显式地向进程对象发送 `-enableSuddenTermination` 消息来启用它。如果你正在创建一个应用程序，可以通过在应用程序包的属性列表文件中设置一个键来避免这种情况。

Cocoa 应用程序与命令行工具不同，通常以包（bundles）的形式分发。这些应该是被图形文件管理器视为文件的目录。NeXT 非常有效地利用它们在同一个应用程序中存储针对不同操作系统的二进制文件，允许文件服务器包含一个用于 OPENSTEP、Solaris 甚至 Windows 的单个应用程序。该包包含的内容之一是属性列表，称为 `info.plist`，它描述了应用程序的一些属性，例如其主类的名称、启动时加载的资源等。初始的突然终止状态就是这些属性之一。

# 键值编码 (Key-Value Coding)

典型程序的大量代码涉及访问和修改对象状态的方面。

键值编码（KVC）机制旨在为设置和获取对象的属性提供抽象接口。它与键值观察（KVO）机制相结合，KVO 提供了一种观察另一个对象特定属性更改的抽象方法。

KVC 让你像操作字典一样与每个对象交互。无论属性是如何存储的，你都使用相同的机制来读取和写入属性。主要的优势是它消除了大量编写自定义控制器的需求。

## 通过键访问值

（注：代码块未翻译）

```
[object setValue: @"42"
forKey: @"integer"];
int value =
[[object valueForKey: @"integer"
intValue];
NSAssert(value == 42,
@"值设置并检索");
```

来自：`kvc.m`

（注：代码块注释已翻译）

## 确保 KVC 合规性

（注：代码块未翻译）

```
@interface KeyPublic : NSObject @end
@implementation KeyPublic @end
@interface KeyIVar : KeyPublic
{
  int integer;
}
end
@implementation KeyIVar @end
```

来自：`kvc.m`

（注：代码块未翻译）

当你使用 KVC 方法时，你几乎总是调用 `NSObject` 中的实现。这些实现尝试确定如何访问属性。

它们首先查找的地方是访问器方法。按照惯例，Objective-C 类提供 `-property` 和 `-setProperty:` 方法来读取和设置“属性”。如果你的类提供了这些方法，它们就会被调用。

还会寻找其他几种方法，包括对于布尔属性的类似 `-isProperty` 等内容。

```
@interface KeyAccessor : KeyIVar @end
@implementation KeyAccessor
- (int)integer
{
    return integer;
}
- (void)setInteger:(int)aVal
{
    integer = aValue;
}
@end
@interface KeyProperty : KeyPublic
@property int integer;
@end
@implementation KeyProperty
@synthesize integer;
@end
```

来自：`kvc.m`

如果此失败，该类将收到 `+accessInstanceVariablesDirect` 消息。如果返回 YES，KVC 方法将查找一个与属性名称匹配的实例变量并使用它。`NSObject` 中此方法的实现返回 YES，因此你只需要重写它就可以防止 KVC 查找实例变量。

最后，如果此失败，KVC 代码将调用两个回退方法之一，取决于你是在设置属性还是获取属性。

这两个方法是 `-valueForUndefinedKey:` 和 `-setValue:forUndefinedKey:`。

```objc
@interface KeyFallback : KeyPublic
{
    NSMutableDictionary *dict;
}
@end
@implementation KeyFallback
- (id)valueForUndefinedKey:(NSString)*aKey
{
    return [dict forKey:aKey];
}
- (void)setValue:(id)aValue
  forUndefinedKey:(NSString)*aKey
{
    [dict setValue:aValue
       forKey:aKey];
}
@end
```

来自：`kvc.m`

这些方法是支持 KVC 的最后机会。如果你实现了它们，对于所有你没有直接支持的键，你应该调用父类的实现。如果在根类上调用，它将抛出异常，表示你没有妥善处理该键。

如果你使用声明的属性来合成访问器方法，你将免费获得 KVC 兼容性。`kvc.m` 示例展示了你实现同一个 KVC 属性的所有不同方法。

此示例使用了一个公共类和若干个私有子类，它们都支持该属性。你可以交替使用所有这些类的实例，至少在存储该键时如此。更重要的是，你可以使用类似 `KeyVar` 或 `KeyFallback` 进行原型设计，以后切换到其他方案。

回退方法在原型设计时特别有用。当你开始创建时，创建一个私有字典实例，并通过 KVC 访问对象上的所有属性。一旦你确定了类真正需要的属性，你就可以用一组访问器替换回退实现，并作为一个独立步骤，将 KVC 调用替换为直接的消息发送。

你可能已经注意到此示例的一个点是，KVC 只处理对象，但实例变量是一个 `int`。以某种方式，这仍然有效。这是因为 KVC 执行了 `auto-boxing`。我们通过将 `@12` 作为参数传递给 `-setValue:forKey:` 来设置此属性。在发现属性是整数后，KVC 代码向字符串对象发送了 `-intValue` 消息。

在反方向，它构造了一个封装原始值的 `NSNumber`。如果实例变量或访问器方法使用对象类型，这段代码将被跳过。注意，KVC 只访问运行时类型信息。

# 理解键路径 201

并且所有对象类型在类型编码中都被编码为 "@"。

这意味着你可以使用 KVC 将一个 `NSString` 实例设置为声明为 `NSArray` 的实例变量的值。当你尝试这样做时，KVC 不会产生任何错误，编译器也不会；然而，当它下一次向字符串发送如 `-objectAtIndex:` 的消息时，将抛出异常。



如果你正在为对象类型编写 KVC 访问器，你可能想添加一个断言语句来检查对象是否具有兼容的类。

## 理解键路径

到为止，我们查看了获取和设置单个键值的方法。这非常有用，但它没有展示出 KVC 的完整活性。

我们用于 KVC 的大部分内容都可以无需 KVC 轻松完成。如果你让一个对象访问另一个对象的特定属性，且不想硬编码，你只需要存储一个选择器并使用标准的 Objective-C 消息发送机制来调用它。

如果属性存储在该对象上，这种方法运行良好，但如果你想要一个间接属性会怎样？你可以存储一个选择器数组，并使用每个选择器获取中间对象，但这太繁了。

# 第 11 章：键值编码

通过 KVC，你可以使用键路径（key paths）。这些是包含键名和点的简单字符串。如果你想访问对象的某个属性的属性，那么可以使用键路径在单次操作中完成。

注意：访问声明属性的点符号表示法看起来与 KVC 表示法非常相似，两者很容易混淆。这是很遗憾的，因为它们完全无关。点表示法直接生成到访问器方法的消息。接收键路径的 KVC 方法是更高层次的抽象。这是点表示法被广泛讨厌的原因之一。

遗憾的是，这种相似性是故意的。在公开发布之前，Apple 员工使用 KVC 术语来指代声明的属性，两者可能旨在联系更密切。

键路径的巨大优势在于，例如，一个通用视图对象只需要存储一个指向模型对象的指针。它不需要指向模型内部各种组件的指针，可以通过键路径访问这些组件。

例如，如果你有一个显示人物信息的视图，你可以使用`"father.mother"`键路径连接家族树中的副本，依此类推。

键路径常用于绑定（bindings）。

这些是连接视图的通用控制器。

## 观察键

来自：`kvo.m`

# 第 11 章：键值编码

获取键是有用的，但它并不特殊。KVC 的真正威力来自 KVO，它让你监控变化。绑定机制使用 KVC 和 KVO 来消除许多情况下的控制器。当视图想要修改模型时，它使用 KVC。当模型变化时，视图从 KVO 获取通知并更新自身以反映变化。

注册 KVO 观察者与接收通知（见第 16 章）类似，但有几点不同。最重要的之一是，KVO 通知始终发送到同一个方法。示例代码开第一个方法展示了这应该是什么样的。

在这个示例中，这是一个类方法。大多数情况下你会使用实例方法，但记住类也是对象，因此你可以在任何地方使用它们。

实现非常简单；它只是记录键的新值。第二个方法展示了如何注册通知。方法中的`change`参数是一个字典，在这个版本中它包含键的新值。它只包含新值，因为这是我们要求的。

## 确保 KVO 兼容性

添加观察方法的`options`参数是一个位域。你可以请求新值、旧值或两者都有。你还可以在变化前后请求通知。

这让你能够轻松执行诸如记录对象更改的任务，这对于实现撤销支持很有帮助。如果你的模型对象遵循 KVO 兼容性，你可以获取每次变化的通知，保存旧值并在稍后（使用 KVC）还原。这种实现撤销的逻辑可以与模型对象的实现细节完全解耦。

## 确保 KVO 兼容性

```objc
self setValue: "@42"
forKey: "@aKey"
self.aKey = 12;
self willChangeValueForKey: "@aKey"
aKey = 47;
self didChangeValueForKey: "@aKey";
```

来自：`kvo2.m`

KVO 就像 Objective-C 的其他部分一样并不是魔法。如果你使用 KVC 访问器设置键，向观察者发送通知是轻而的。如果你直接设置实例变量会怎样？遗憾的是，答案非常简单：什么都不会发生。

直接设置实例变量只是一个存储到内存中。目前没有简单的方法可以自动检测内存中的某个值是否被修改。这意味着你必须将对实例变量的直接访问封装在本节开头代码段所示的两次调用包围起来。

如果需要，这些调用将触发 KVO 通知。请注意，如果你是在调用访问器方法（accessor method），则不需要发送这些消息。这是 Objective-C 晚绑定的优势之一。

实现 KVO 的代码相当复杂，并使用了 Objective-C 的一些高级特性。当你为某个键（key）注册观察者时，该键的 setter 方法将被一个特殊版本取代，该版本负责处理通知。

KVO 可能是 Foundation 框架中看起来最像“魔法”的部分。值得记住，KVO 所做的一切你自己的代码都能做到。它并不依赖于未公开的接口、编译器修改或类似的技巧。如果你愿意，可以在自己的代码中实现等效的功能。你可以查看 GNUstep 的实现来了解如何做到这一点。

在 GNUstep 和 OS X 上，KVO 机制都是通过`isa-swizzling`实现的。这是一种技巧，在对象创建后将对象的`isa`指针切换指向不同的类。通常，这种技巧会与运行时类创建相结合，以便你在类层次结构中插入一个新的叶子节点，并让对象的`isa`指针指向它。

幸运的是，KVO 作为 Foundation 框架的一部分，其目的在于让你无需确切知道它们的工作原理，除非你对此特别感兴趣。然而，KVO（以及其他机制）使用`is-swizzling`实现有一个重要的副作用：这意味着你不应该依赖于对象的`isa`指针指向特定类或保持未修改状态。

如果你想测试一个对象是否是特定类的实例，请使用`-isMemberOfClass:`或`-isKindOfClass:`。向对象发送`-class`消息来获取其类，而不要仅仅检查`isa`指针。

## 处理错误

大多数代码都包含 bug。良好的代码会意识到这一点并优雅地处理它们。真正优秀的代码使用形式化方法来证明没有 bug，但大多数人负担不起这种真正优秀的代码。

书中的大多数示例代码都假装错误从未发生过。这本书的页数较少，为任何示例编写适当的错误处理代码会很快被大量与示例要点无关的内容填满。

大多数可以在运行时检测到的错误都源于一个函数或方法使用无效输入调用另一个方法。处理此类问题的最佳方法很大取决于语言。例如，Erlang 不鼓励在模块级别进行防御性编程；如果你的模块处于未定义状态，你应该杀死它并创建一个新版本。在 C 语言中，你被鼓励验证每一个输入并检查每一个返回值。在 Java 中，你可以通过异常来推迟错误处理。Lisp 和 Smalltalk 则允许在错误发生时检查堆栈，并动态修复产生错误输入的代码。

在这一方面，Objective-C 介于 C 和 Java 之间。某些错误最好在最接近产生源的地方进行处理，而另一些错误可以通过报告原因并退出来处理。

从 NeXT 时代起，Objective-C 就有了所谓的异常（exceptions），但它们直到最近才得像其他语言中的异常。

## 异常的运行时差异

异常处理在运行时是非常困难的。在抛出异常和捕获异常之间，需要进行堆栈回溯。在像 Smalltalk 这样的语言中，这非常容易。在 Java 和类似的语言中，这通常通过返回异常来实现。在 Objective-C 中，这种方法是不可能的，因为在抛出异常时需要执行清理代码。

## 异常的抛出与捕捉

```objc
NSArray *array = [NSArray array];
@try {
    [array objectAtIndex: 0];
}@catch (NSException *e) {
    NSLog("@@Caught exception %@", e);
}
```

来自：`exception.m`

旧 Objective-C 代码可能包含以`NS_DURING`开头的块。这些是定义`setjmp`风格异常处理的旧宏。在较新的 Foundation 框架中，它们被定义在`NSException.h`中以便使用新的异常处理关键字。

这些旧宏有几个局限性，即使它们作为新关键字的包装器使用也是如此。首先，它们只允许捕获`Exception`实例。其次，它们没有等同于`@finally`（运行清理代码并继续回溯），尽管你可以通过捕获异常然后重新抛出来模拟这种行为。

这些宏使用起来非常不方便。你必须在`NS_DURING`块内部使用`NS_VALUERRETURN`或`NS_VOIDRETURN`来进行返回，以确保你已经从异常处理栈中移除了清理代码。

```objc
67 #define NS_DURING @try {
68 #define NS_HANDLER } @catch (NSException *
      localException) {
69 #define NS_ENDHANDLER }
70 #define NS_VALUERETURN(v,t) return (v)
71 #define NS_VOIDRETURN return
```

来自：`NSException.h`

现在，异常处理代码看起来非常像 Java 或 C++。但有一些限制。抛出`NSException`以外的对象可能有效，但这是不被支持的。在 OS X 上，这是因为当使用旧运行时编译时，抛出的对象可能会被旧的`NS_HANDLER`宏捕获，而该宏期望的是一个`NSException`实例。在 GCC 运行时（但不是 GNUstep 运行时）中，可能会抛出一个未在运行时恰当注册的类实例，导致在回溯库中发生崩溃。完全不支持抛出非对象类型。

抛出异常的最佳方法仍然向`NSException`实例发送`-raise`消息。你也可以使用`@throw`关键字抛出任意对象，但如果它不起作用，请不要感到惊讶。如果你使用的是 GNU 运行时或现代 Apple 运行时，它可能有效，但你正在做一些未经过充分测试的事情。

## 使用异常对象

```objc
[NSException raise: NSGenericException
format: @"This is an example"]
```

来自：`throwexception.m`

`NSException`类曾用于实现`longjmp()`缓冲区栈，并在需要时跳转到栈顶端。现在，回溯完全由运行时和回溯库完成，但`NSException`仍用于封装异常。

异常包含三个组件：名称（name）、原因（reason）和用户信息字典（user info dictionary）。名称此类异常的唯一标识符。这只是一个字符串，但通常会使用符号常量（例如`NSRangeException`），这样你在捕获异常时就可以对异常进行指针比较。

描述（description）是人类可读的描述。这通常只用于调试，因此本地化并不重要。理解发生了什么比你的用户理解发生了什么更重要。最后，用户信息字典是一个包含某些键值对的`NSDictionary`。抛出异常的代码完全决定了在里面放入什么，尽管大多数抛出异常的方法都说明了它们将在用户信息字典中放入的内容。你可以用此将任意信息传递到捕获异常的地方。因为它是字典，你可以决定稍后添加额外的键，而不会破坏与现有代码的二进制兼容性。这是通常会使用不可变字典——即`NSDictionary`而不是`NSMutableDictionary`——的情况之一，因为捕获代码不期望能够修改它。如果你给异常附加一个字典，通常会使用`NSDictionary`的`+dictionaryWithValuesAndKeys`构造函数来创建一个单次性的不可变字典进行抛出。

在最近的 OS X 版本中，异常对象还有一些有助于调试的额外信息。向它发送`-callStackReturnAddresses`消息将给你一个包含`NSNumber`的`NSArray`，指向栈上所有函数的返回地址。这并不是特别有用，但随 OS X 10.6 引入的`-callStackSymbols`方法可以给你提供异常创建时栈上所有函数或方法的名称。

后一种方法由未处理异常的处理程序使用，每当回溯异常未被捕获时就会调用它，以便在程序终止前打印堆栈跟踪。你可能想要使用`NSSetUncaughtExceptionHandler()`函数将此处理程序替换为你自己的函数。如果你有错误报告机制，那么拥有未处理异常的堆栈追踪将非常有用。

# 第 12 章：处理错误

## 使用异常管理内存

```objc
id pool = [NSAutoreleasePool new];
id array = [NSArray new];
@try {
    throw(array);
}@catch (id e) {
    NSLog("Caught exception %@", e);
    e = [e retain];
    [pool drain];
    [e autorelease];
    pool = nil;
    @throw;
}@finally {
    [array release];
    [pool drain];
}
```

来自：`releaseexcept.m`

异常处理让内存管理变得稍微复杂。如果你在方法中创建了一个新对象并在结束释放它，你必须考虑到异常实际上是经过伪装的非局部跳转（non-local goto），并且突然有很多种从你的方法返回的路径。每一个函数调用或消息发送都变成了一个潜在的返回路径。

你可以通过在`@try`块末尾添加一个`@finally`块来轻松地解决这个问题。无论是通过结束`@try`块还是通过抛出异常退出，该块中的代码都会执行。

**注意：** 在 Java 中，你也可以将异常用作局部跳转，通过抛出异常并在同一方法中捕获它来向虚拟机宣告这种路径。这在 Objective-C 中也是可能的，但效率极低。`@throw()`语句会调用`objc_exception_throw()`函数，它会调用回溯库函数。这将读取栈帧的 DWARF 数据并调用 Objective-C 个性函数。该函数将读取更多的 DWARF 数据，比较异常类与 catch 块，并将指令指针设置为 catch 语句的地址。在 Java 中，虚拟机会将此翻译为跳转到 catch 块。如果你必须使用这种模式，在 Objective-C 中请使用`goto`语句。然而，最好避免它，寻找一种不忽视结构化编程理念的解决方案。

另一个可能问题是传入异常对象。异常对象通常是自动释放的。这意味着在手动内存管理下，它们会在当前释放池删除时被删除。

这在大多数代码中不是问题。你最常用的释放池在整个运行循环期间持续。然而，有时你会创建自己的释放池。

如果你在`@finally`块中清理了释放池（这似乎是显见的解决方案），你会遇到一个问题。异常对象会在回溯你的栈帧时被删除，而上一个栈帧可能会崩溃，因为它引用了悬空指针。

为了避免这种情况，你必须确保保留该异常对象，并在之后再次对其自动释放。这就是为什么抛出`NSException`以外的对象的坏主意之一。

要正确实现这一点，你需要一个通用的捕获子：一个类型为`id`的`@catch`语句。这将捕获所有的 Objective-C 异常。记住，C++ 异常仍然不会在此块中被捕获，因此如果你在使用外部异常进行回溯，你仍然需要一个`@finally`块来处理清理工作。你可以在`@catch`子句中将释放池的指针设置为`nil`，防止它被释放两次。

## 传递错误代理（Error Delegates）

```objc
23 NSFileManager *fm = [NSFileManager defaultManager
24]; [fm copyPath:source
25 destination
26 handler:[ErrorHandler new]];
```

来自：`errordelegate.m`

在 Common Lisp 中，你有“可恢复异常”（resumable exceptions）的概念。这与 Objective-C、Java、C++ 等语言中常见的“回溯异常”（unwinding exceptions）形成对比。可恢复异常不会展开栈；它会执行异常处理代码然后继续执行。

在 Objective-C 中没有直接的对应物，但你可以通过将错误代理作为参数传递给方法来实现这一结果。NS 中的旧版 API 就是这样工作的。它们的最后一个参数是一个对象，当操作遇到问题时，会向该对象发送消息。

该方法返回一个指示操作是否应该继续的`BOOL`。如果错误代理没有处理这些条件，你可以通过抛出异常将此与代码中的回溯异常结合起来。

我在 LanguageKit 框架中使用这种模式来报告编译器错误和警告。当编译器遇到错误时，它会调用错误代理中的方法。默认实现只是将消息打印到控制台，但其他实现可以转换抽象语法树以移除错误。如果它返回`YES`，编译器会回溯并再次尝试检查。如果返回`NO`，编译器将抛出异常，该异常将由调用编译器的代码捕获。

通常情况下，在操作过程中任何可能遇到修复问题的地方，你都应该使用这种模式。例如，在加载引用其他文件的文件时可以使用它。如果引用的文件之一缺失，默认选项是终止。然而，错误代理可以通过某些固定的翻译或提示用户来提供新路径。

## 返回错误值（Error Values）

```objc
- (BOOL)trySomething;
- (id)tryDoSomethingWithObject:(id)anObject
  error:(NSError**)*error;
```

## 使用 NSError

来自：`errorReturn.m`

在 C 语言中，常见的模式是成功时返回零，返回某个非零值表示错误条件。这在 Objective-C 中不那么流行，但返回一个表示操作是否成功的`BOOL`值是相对常见的。

大多数时候，这是通过此类变更方法（mutate methods）实现的，这种方法的目的是影响对象的某种变化，而不是获取值，因此返回值没有被用于其他地方。

这种模式的示例是 NSStream 上的`setProperty:forKey:`方法。它尝试设置流的属性，如果成功则返回`YES`。注意，这与 C 语言的模式相反，C 语言在失败时返回 true。

## 使用 NSError



```objective-c
NSError *error = nil;
NSStringEncoding enc;
NSString *str = [NSString
    stringWithContentsOfFile:@"DoesNotExist"
    usedEncoding:&enc
    error:&error];
if (nil != error) {
    NSLog(@"Error: %@",
        [error localizedDescription]);
}
```

来自：`nserror.m`

Apple 在 OS X 10.2 中引入的几个方法接受 `NSString**` 作为参数。这用于返回一个报告错误的第二个值。如果调用后指向的变量为 `nil`，则说明操作成功。否则，它包含一个描述错误的字符串。

这有一些显而易见的局限性。对于向用户报告来说，字符串是可以的，但对于恢复错误来说并不有用。如果你想在代码中处理错误，你需要以某种方式解析该字符串。

当 Apple 发布 Safari 10.2.7 版本时，他们添加了一个新类：`NSError`。它几乎总是通过作为方法最后一个参数传递的指针返回。错误对象看起来与异常对象非常相似。它有一个名称（称为领域/domain）和一个关联的字典。

与异常对象不同，字典有几个预定义的键。这些包括本地化错误描述（localized error description）。你可以在无需任何额外处理的情况下将其展示给用户。

错误对象有时还包含恢复策略（recovery strategy）。恢复尝试对象（recovery attempt object）可以尝试从错误中恢复。对于某些错误来说这是可能的，但通常当你尝试做某些可行但不安全的操作时，你会得到错误。当发生这种情况时，你应该将错误展示给用户，然后调用恢复尝试者。

如果你用过 Common Lisp，这种模式看起来会很熟悉，它是可重启异常的一种即时表形式。

## 访问目录和文件

如果你正在使用 AppKit，对于大多数文件系统相关的任务你有两个选择。来自 Foundation 框架的 `NSFileManager` 类提供了许多用于操作文件和目录的低级方法。来自 Application Kit 的 `NSWorkspace` 类提供了更抽象的形式。

`NSWorkspace` 的许多功能被委托给工作空间进程（workspace process）。在旧的 NeXT 系统上，这是一个单一程序，而在 OS X 上，其功能的各个部分由窗口服务器和 Finder 实现。

正因如此，当无法保证工作空间进程存在时（例如在可能通过连接运行的命令行工具中），考虑使用更高层次的版本就是没有意义的。UIKit 框架没有 `NSWorkspace` 的等效物。如果你的目标平台是 Cocoa Touch，你必须使用更低级的 API。

## 读取文件

```objective-c
NSData *copy = [NSData initWithContentsOfFile:file];
NSData *mapped = [NSData initWithContentsOfMappedFile:file];
NSData *read = [[NSFileHandle fileForReadingAtPath:file] readDataToEndFile];
```

来自：`readFile.m`

Unix 系统通常访问文件的方法：`read()` 和 `mmap()` 系统调用。大多数其他系统——至少是具有内存管理单元（MMU）的硬件——都有这些等效物。前者将字节流从文件复制到缓冲区。后者将文件数据映射到内存区域。

Foundation 提供了两个大致对应这些方法的类。`NSData` 类封装了一个包含未类型数据的内存区域。你可以通过各种选项从文件创建该类的实例。

## 读取文件

对于小文件，你可以直接使用封装 `read()` 调用并将文件副本读取到内存的版本。对于大文件，你可能希望使用 `dataWithContentsOfMappedFile`。

后者的优势是它与操作系统的虚拟内存子系统交互良好。当你耗尽物理内存时，你不需要为包含映射文件的页分配交换空间；你只需要丢弃它们，并在下次访问时重新读入。

这对于内存非常小且没有虚拟内存的平台非常有用。例如，3GS 之前的 iPhone 只有 128MB RAM，且它们没有任何交换空间。如果你将一个 4MB 的文件读取到内存中，你就耗尽应用程序可用空间的大部分。

相比之下，如果你创建一个代表文件的映射数据对象，系统将根据需要以 4KB 为块读入数据，并在不再需要时将其驱逐。如果你在创建新对象时耗尽了内存（例如），内核将从内存中驱逐映射文件以腾出空间。如果你已经读取了文件，它就无法这样做，因此它只会耗尽内存并杀死你的应用程序。

如果你只想一次读取文件的一部分，你应该使用 `NSFileHandle`。该类封装了文件描述符并实现了 Objective-C 和 C 标准库支持的相同基本操作的不同版本。你可以通过一次操作从文件句柄中读取所有数据，但更多情况下你会读取下一个可用的位。

你可以通过向文件句柄发送 `-readDataOfLength:` 消息来读取固定大小的数据块。该类的大多数其他方法对于从文件中读取数据并不特别有用；它们用于与套接（sockets）交互。我们将在第17章再次查看此类类。

## 移动和拷贝文件

```objective-c
FileManager *fm = [NSFileManager new];
if (shouldMove)
{
    [fm copyItemAtPath:source
       pathTo:destination
       error:nil];
}
else
{
    [fm moveItemAtPath:source
       pathTo:destination
       error:nil];
}
```

源：`fileCopy.m`

`NSFileManager` 类封装了整个文件系统并允许你对其进行操作。该类为 Objective-C 开发者暴露了类似于 Apple Finder 和 Windows 资源管理器向用户暴露的类型的功能。在 OS X 10.5 之前，你使用的方法将一个对象作为最后一个参数。在拷贝或移动操作进行期间，会向该对象发送消息。这些消息例如，会询问在发生错误后是否继续。

随着 10.5 的发布，Apple 决定大幅更改接口。我们现在使用的方法采用了我们在第12章中讨论过的新错误报告模式，因此最后一个参数是一个指向 `NSError*` 的指针，用于返回错误。消息现在发送给对象的代理（delegate）。这意味着你现在必须从单个线程使用 `NSFileManager`。在 10.5 之前，该类是单例模式的一个示例。缓存 `+defaultManager` 方法的返回值（该方法返回单例实例）是非常常见的做法。现在，这种使用缓存版本的代码是不安全的，因为它们可能从不同的线程被调用。

如果你正在编写代码，应该确保在每次想要使用它时都创建一个新的 `NSFileManager` 实例并在之后销毁它，否则你可能会导致消息发送到错误的代理。如果不这样做，两个线程可能会同时为单例文件管理器设置代理，导致其中一个接收到所有通知，而不是每个线程都接收它感兴趣的通知。

注意：这是一个缺乏思考的软件设计示例。更好的解决方案是将代理存储在线程字典中（参见第14章）。如果你处于需要对单例类进行类似更改的境，请考虑这种方法，或者简单地保留回调的额外参数。不要要求更改现有代码来支持你的新接口。

如果你在文件管理器上使用旧的、已弃的方法，配合单例是线程安全的。如果你没有调用任何发送代理消息的方法，使用单例也是安全的。这很遗憾，因为这意味着当你拷贝文件时可能需要创建一个新的 `NSFileManager` 实例，即使你已经有一个指向单例实例的指针。

## 获取文件属性

```objective-c
NSFileManager *fm = [NSFileManager defaultManager];
Dictionary *attrs = [fm attributesOfItemAtPath:@"fileAttributes.m" error:NULL];
NSString *fileType = [attrs fileType];
NSNumber *creator = [attrs objectForKey:NSFileManagerHFSCreatorCode];
```

`fileAttributes.m`

`NSFileManager` 类封装了大多数标准的 POSIX 文件系统操作函数。在 C 中，你通常使用 `stat()` 函数来查找文件信息。该函数接受一个结构体指针作为参数，并在其中填充有关文件的信息。

这种方法的局限性显而易见：你不能在不破坏使用它的现有代码的情况下向结构体添加新字段。`NSFileManager` 版本要灵活得多。`-attributesOfAtPath:error:` 方法返回一个 `NSDictionary`，在字典中添加额外条目而不破坏二进制兼容性是非常轻易的。

从这个示例中你会注意到，我们可以向字典发送 `-fileID` 消息来获取值。该方法是 `NSDictionary` 的一部分，返回与 `NSFileType` 键对应的字典条目。还有几个类似的字典方法。

在 OS X 上，你比其他 POSIX 平台多几位文件元数据。HFS+ 为每个文件存储创建者代码和一个类型代码。这些现在不再被频繁使用，但在 Classic MacOS 上，它们被代替文件扩展名来确定打开文件的正确应用程序。

## 操作路径

```objective-c
NSString *home = @"~\
```

源：`path.m`

许多 UNIX 代码通过使用 `sscanf()` 和 `sprintf()` 函数来操作路径。当你需要将代码移植到 Windows 或 Symbian 时，这会引起很多问题，例如它们的文件系统布局和路径分隔符是不同的。

OpenStep 从一开始就被设计为可以在不同的操作系统家族之间移植。`NSString` 类提供了几个旨在操作路径的方法。

尽管这些方法操作的是字符串，但它们暴露了一个更抽象的接口。你可以添加或删除路径组件，路径组件是路径中的单个项目（文件或目录）。你还可以修改文件扩展名。

在 OS X 上，像任何 UNIX 系统一样，有一个单一根文件夹，由单个斜杠表示。子目录由斜杠分隔，文件扩展名由点分隔。在 Windows 上，

在处理路径的代码中，不值得过度担心效率。对文件系统进行的几乎任何操作都是昂贵的。

## 判断文件是否存在

**注意：** 不要使用这种机制来创建临时文件。如果你这样做，那么在测试文件是否存在和创建它之间存在潜在的竞态条件。请改用 C 库的 `mkstemp()` 函数。Foundation 框架有一个该函数的封装，如果你想留在对象世界，可以使用它。

```objective-c
FileManager *fm = [NSFileManager defaultManager];
BOOL isDir;
if ([fm fileExistsAtPath:path isDirectory:&isDir]) {
    if (isDir)
        printf("Folder exists\n");
    else
        printf("File exists\n");
}
```

源：`fileExists.m`

判断文件存在的简单方法是访问它并检查错误。这并不优雅，尽管 `fileExists:isDirectory:` 正是这样做的。它测试路径上的对象是否存在，并告诉你它是否为目录。

对于 Java 等语言来说，这可能看起来很奇异。C 以及 Objective-C 只支持返回单个值，但此方法需要返回两个值：是否存在以及是否为目录。有几种实现方法。一种是定义一个枚举类型，带有 `nothing`、`file` 和 `directory` 元素。

这会让所有使用此方法的代码变得简单，因此无法看出为什么没有这样做。当你意识到你可以将 `NULL` 作为第二个参数时，答案就显而易见了。如果你这样做，该方法将不再测试路径对象是否为目录。这是一个很小的节省，因此不明这是否是一个明智的设计选择。

## 使用 Bundle

```objective-c
CFBundle *mainBundle = [NSBundle mainBundle];
NSLog("%@ links against: %@",
    [mainBundle executablePath],
    [NSBundle allFrameworks]);
```

源：`bundles.m`

在 Apple System 7 及之前的版本中，文件系统支持两个卷：代码卷和数据卷。数据卷被用于存储任意资源。随着 Mac OS 8.1 的发布，Apple 引入了 HFS+，支持任意数量的卷，使得文件在包含任意子项的能力上与目录相同。NTFS 具有相同的功能。

OS X 仍然支持资源卷，并在不支持它们的文件系统（如 UFS 和 FAT）上将数据存储在隐藏文件中，但不建议使用它们。将包含卷的文件拷贝到其他文件系统是一个问题。如果你用 OS X 将文件拷贝到 FAT 磁盘，然后用 Windows 从该磁盘拷贝，你将不会拷贝隐藏文件，因此卷中的数据将会丢失。

与此同时，NeXT 走了另一个方向。如果卷让文件像目录，为什么不直接使用目录呢？NeXTSTEP 在标准 UNIX 文件系统之上通过目录提供了类似卷的功能。

## 使用包（Bundles）

文件存放的位置。

被视为文件的目录称为包（bundles）。对于原始的低级文件系统操作和其他操作系统来说，它们看起来像目录。例如，如果你将一个 OS X 应用程序包拷贝到 USB 驱动器并在 Windows 上查看，它看起来就像任何其他目录一样。然而，当你在 Finder 中查看它时，它看起来像是一个单一文件。

在几乎任何 Objective-C 程序中，你会使用的两种包是框架（frameworks）和应用程序（applications）。这两者都包含一些可执行代码（程序或共享库）和一组资源。

具体的布局取决于系统。

GNUstep 使用旧的 NeXT 风格包布局，而 OS X 使用的是一种稍微简单的布局。你可以轻松地产生同时具有 GNUstep 和 Cocoa 布局的包，允许同一个 `.app` 包在无需重新编译的情况下在系统之间迁移。

你可以通过向 `NSBundle` 发送 `+mainBundle` 消息获取应用程序的主包。`NSBundle` 是一个用于封装包的类。它跟踪所有动态加载的包。

包天生支持本地化。资源存储在每个本地化不同的子目录中，并可以根据需要加载。`-pathForResource:ofType:` 方法将返回包资源目录中，具有指定扩展名的命名资源的本地化版本。

## 第 13 章：访问目录和文件

注意：命令行工具通常不存储在包中。然而，它们仍然有一个主包对象。该对象将包含主可执行文件的目录作为其路径。

你可以在代码中使用此方法来获取存储在你的应用程序包或从任何加载的包中的资源文件的本地化版本。如果你的代码在一个框架中，你可能想从框架包中获取资源。这比从主包获取代码要稍微复杂一些。

`+bundleForClass:` 方法将给你提供包含指定类代码的包。如果你认为未来可能会将某个类移动到框架中，那么在加载资源时使用此方法是一个好主意。

## 在系统位置查找文件

```objective-c
NSArray *dirs =
    NSSearchPathForDirectoriesInDomains(
        NSLibraryDirectory,
        NSAllDomainsMask,
        YES);
```

源自：`frameworkLoader.m`

在 OS X 上，文件系统的布局定义得非常明确。你可能可以硬编码路径并期望它们正常工作。如果你将代码移植到其他平台，你会发现事情会发生严重损坏。

这是 OpenStep 程序员经常遇到的问题之一。例如，在 Solaris、OPENSTEP 和 Windows NT 之间迁移代码需要为每个平台更改许多硬编码的路径。

在 Apple 收购 NeXT 后，他们发布了新版本的 OPENSTEP，带有 MacOS 兼容层和一个名为 Rhapsody 的新用户界面。它使用了与 OPENSTEP 相同的 NeXT 文件系统层次结构，并在根目录下包含一个 `/NeXT` 文件夹，其中包含了该层次结构中非类 UNIX 部分。

通过 Rhapsody DR2，Apple 对目录布局进行了一些重大更改，这种布局现在对 OS X 用户来说很熟悉。为了方便使用并支持 Windows 上的 YellowBox（Cocoa）——该产品不久后就停止了——他们引入了 `NSSearchPathForDirectoriesInDomains()`。

此函数返回一个特定用途的目录数组。当你调用此函数时，第一个参数描述了你想要的目录类型。这可能是应用程序目录、库目录等。第二个参数是文件系统作用域。

OS X 像 OPENSTEP 一样，将文件系统层次结构划分为多个作用域，这些作用域的内容大致相同，但用途不同。这些作用域是有序的，因此你应该优先使用高优先级作用域中的文件。四个作用域如下：

- **User（用户）**：该作用域位于用户主目录下。这里的文件是用户私有的，并完全由用户控制。
- **Local（本地）**：包含机器本地文件的作用域。在 OS X 上，这包括了 `/Library` 目录等内容，该目录可能被本地系统管理员修改。
- **Network（网络）**：在该作用域中看到任何内容是非常罕见的。你将在独立机器或作为异构网络一部分机器上看不到它。它用于由网络管理员控制的目录。
- **System（系统）**：最后一个作用域包含系统文件。通常，你不应该向该作用域中的任何位置写入内容，尽管你可以从那里读取。你做的任何修改可能在用户下次更新系统时被撤回。

并不是每个类型的目录都存在于每个作用域。例如，系统作用域中没有 documents 目录，如果有的话也没有意义。

最后一个参数告诉函数是否展开路径中的波浪号（tildes）。你几乎总是在这里传递 `YES`。

`frameworkLoader.m` 示例展示了我们在本章中过的几项内容。此示例加载了一个命名的框架。因为框架是包，你可以使用 `NSBundle` 来加载它们。

此示例首先获取系统中所有 Library 目录的列表。然后按顺序查找，以测试每个目录中是否存在名为该框架且具有 `.framework` 扩展名的目录。



如果存在名称正确的对象，示例程序告诉 `NSBundle` 加载它。你可以使用这段代码在运行时懒懒加载框架，而不是显式地链接到它们。或者，你可以修改它，在库目录中的应用程序插件目录中查找，在这种情况下你应该查找 `NSApplicationSupportDirectory`。如果你构建

```
11 NSArray *dirs = =
12 NSSearchPathForDirectoriesInDomains(
13 NSLibraryDirectory,
14 NSAllDomainsMask,
15 YES);
16 for (NSString *dir in dirs) {
17   NSString *f = [[dir stringPathComponent:@"Frameworks"]
28                pathExtension:@"framework"];
29   BOOL isDir = NO;
30   if ([fm fileExistsAtPath:f isDirectory:&isDir]) {
31     NSBundle *bundle = [NSBundle bundleWithPath:f];
32     if ([bundle load]) {
33       NSLog(@"Loaded bundle %@", f);
34       return YES;
35     }
36   }
37 }
```

源自：`frameworkLoader.m`

# 线程 (Threads)

原始的 NeXT 操作系统是构建在 Mach 之上的，OS X 也是如此。Mach 从一开始就支持线程，并且是第一批类 UNIX 系统之一。更最近，POSIX 线程 API 提供了一种跨平台的创建线程的方法。

你几乎不会想直接使用 Mach 线程——它们不符合 UNIX 模型且使用起来很复杂——但你可能希望直接使用某些 POSIX 线程函数。

## 创建线程

```
10 - (void)processInThread
11 {
12   SEL sel = @selector(process:);
13   [Thread
14     detachThreadSelector:sel
15     addTarget:self
16     withObject:nil);
17 }
```

源自：`thread.m`

线程被封装在 `NSThread` 对象中。这些对象封装了 POSIX 线程并提供了一些方便方法。

从 10.5 开始，有两种创建新线程的方法。传统的方法类似于创建 POSIX 线程的标准方式，而第二种旨在让 Java 程序员感到更熟悉。

当你创建一个新的 POSIX 线程时，你在新线程中调用一个带有 `void*` 参数的函数。当你使用 `NSThread` 创建新线程时，你执行类似的操作，向一个对象发送消息并将另一个对象作为参数。

更 Java 风格的创建线程的方法是子类 `NSThread` 并重写 `-main` 方法。然后你可以创建你的线程对象的实例并向它发送 `-start` 消息来开始运行。

当你创建一个新线程时，它并不已经有一个自动释放池（autorelease pool），因此最常见的做法是先创建一个自动释放池，或者为线程创建一个新的运行循环（run loop）。

在 Objective-C 中，创建一个新线程是一个昂贵的操作，就像在 C 中一样。该过程必须从内核获取新线程栈所需的某些新内存，创建调度所需的所有用户空间和内核数据结构，并为线程本地存储（thread-local storage）映射额外的空间。因此，在创建线程后，让它们保持一段时间是一个好主意。

在线程中创建一个新的运行循环是实现这一目标的好方法。你可以在其中注册定时器触发，监控文件描述符是否有新数据，并在新线程中使用事件驱动的编程风格。

## 控制线程优先级

```objectivec
double oldPriority = [NSThread threadPriority];
[NSThread setThreadPriority: 0];
[[NSThread mainThread] setThreadPriority: 1];
```

来自: `threadPriority.m`

`NSThread` 实现了 `threadPriority` 和 `setThreadPriority:` 方法，它们既是类方法也是实例方法。当发送给类时，它们控制当前线程的优先级。当发送给实例时，它们控制该对象封装的线程的优先级。

线程的优先级决定了它将获得多少 CPU 时间以及在获得 CPU 访问权限之间需要等待多久。通过底层的 POSIX 线程优先级 API，你还可以设置调度策略。执行这些操作函数都是 POSIX 实时扩展的一部分，这些扩展还提供了信号队列等。Objective-C API（尚未）暴露这些功能。

使用此 API 设置的优先级是 0 到 1 之间的双精度浮点值。这些值将被缩放到调度器可以理解的某些整数范围内，因此你应该记住微小的差异会被舍入。

POSIX 规范为线程定义了两种竞争范围（contention scopes）。线程的优先级定义了是否允许其获取 CPU 时间的基值，该值根据它已经获得了多少以及距离上次获取已过了多久来被缩放。竞争范围决定了哪些线程在竞争 CPU 时间。使用系统竞争范围（system contention scope），线程与系统中的所有其他线程竞争。使用进程竞争范围（process contention scope），它只与属于同一进程的线程竞争。

OS X 只实现了系统范围，这意味着高优先级线程将从其他进程中低优先级的线程那里夺取处理器时间。如果你将线程优先级设置为大于 0.5，请记住这会对系统的其他部分产生负面影响。

这不会导致完全的饥饿。在 OS X 10.6 中，在纯 CPU 密集型任务中，最高线程优先级的获得的 CPU 时间比最低优先级分配的略多一倍。大多数任务将涉及某些等待磁盘数据的时间。处于阻塞状态的线程无论优先级如何，都不会消耗任何 CPU 时间。

OS X 上的调度策略与传统的 UNIX 模型相矛盾，在传统模型中，只有超级用户才能提高进程的优先级。有点有趣的是，OS X 最新版本的线程优先级对线程获取 CPU 时间数量的影响实际上比拥有该线程的进程优先级更大。这意味着，虽然你不能提高进程的优先级，但可以通过提高你进程中所有线程的优先级来实现相同的效果。

防止普通用户增加进程优先级的原始设计是为了防止一个用户获得不公平的 CPU 时间。OS X 系统倾向于单用户机器，因此这个问题不那么严重，但仍然可能夺走同一用户下更重要任务的处理器时间。例如，实时视频捕捉对性能非常敏感，如果你的程序决定将其优先级设得足够高导致捕获应用程序丢帧，用户可能会非常恼火。

设置线程优先级时要体贴。通常情况下，你应该只使用 0 到 0.5 之间的范围。只有在绝对没有其他选择的情况下，才将线程设置为高于默认级别。不要仅仅因为你正在进行 CPU 密集型操作并希望它运行得快就这样做。

## 同步线程

```objectivec
static NSObject *lock;
static NSMutableArray *messages;
void recordLogMessage(NSString *msg)
{
  [lock lock];
  @try {
    [messages addObject:msg];
    NSLog("%@", msg);
  }
  @finally {
    [lock unlock];
  }
}
```

来自: `lock.m`

你可以通过多种方式同步两个线程。执行此类同步的类都遵循 `NSLocking` 协议。它定义了两个方法：`-lock` 和 `-unlock`。

简单的锁类是 `NSLock`，它实现了互斥锁（mutex）。一次只能有一个线程锁定它，因此向它发送 `-lock` 消息会导致任何其他向同一对象发送 `-lock` 消息的线程阻塞，直到你发送相应的 `-unlock` 消息。

这对于保护较短的临界区非常有用。对于较长的临界区，`NSRursiveLock` 通常更有用。如果你在同一个线程中向 `NSLock` 发送两个 `-lock` 消息，就会导致死锁。只要你发送相同数量的 `-unlock` 消息，你可以向 `NSRursiveLock` 发送任意 `-lock` 消息。这在可能从已获取锁的代码调用的方法非常有用。

传统上，这些类的问题是它们与异常处理集成得不是很好。如果你获取了锁然后抛出了异常，锁将永远不会释放。当 Apple 引入 `@synchronized` 关键字时，它们还将锁与对象关联，并确保在抛出异常时释放它。

通常来说，使用 `@synchronized` 关键字处理线程本地数据不是个好主意。尽管它让生活变得简单了一些且对 Java 程序员来说熟悉，但其实现效率低下。你可以通过确保在 `@finally` 块中发送 `-unlock` 消息来实现相同的效果。如果你确定调用的方法或函数不会抛出异常，可以避免 `@try` 和 `@finally` 块，但在现代运行时它们并没有性能开销。

## 存储线程特定数据

```objectivec
NSMutableDictionary *threadDict = [[NSThread currentThread] threadDictionary];
[threadDict setObject:@"default" forKey:@"NewKey"];
```

来自: `threadDict.m`

一旦有了线程，你通常希望存储某些线程私有的数据。Cocoa 中的一个例子是当前图形上下文，它必须对任何绘制代码可用，但不能在线程间共享。

通常，你使用 `pthread_set_specific()` 函数来实现这一点，它存储与当前线程关联的指针。这通常通过在寄存器中存储内存区域地址，并使用该区域开始的固定偏移量对应每个线程特定数据来实现。这意味着每个线程都需要空间，即使你只将其中一个设置为非 NULL。

如果 Cocoa 这样存储图形上下文，每个线程都需要一个字的空间，尽管大多数程序只需要在一个或两个线程中有有效的图形上下文。

解决此的方法是**线程字典**（thread dictionary）。这是一个与线程关联的可变字典。每个线程只需要一个字来存储此指针，但你可以在其中存储任意数量的对象。只有与给定键关联的线程才需要空间来存储它。

通过向当前线程发送 `-threadDictionary` 消息来访问线程字典。你可以像操作任何其他字典一样操作它。当线程退出时，字典会被销毁。因为字典会保留其参数，这意味着仅从线程字典引用的任何对象的析构函数运行后将被释放。

你可以利用此在线程退出时运行代码，但并不推荐这样做。线程在退出前会发布 `NSThreadWillExitNotification`。

它们会退出，所以如果你想运行某些清理代码，只需观察这一点即可。

> 在大多数平台上，你可以使用 `__thread` 关键字，这是 GCC 的扩展，用于将变量存储在线程本地存储中。Darwin 加载器不支持线程局部段（thread-local sections），因此在 OS X 上是不可能的。这可能很快就会改变，因为 C 和 C++ 标准的后续版本都包含了类似的功能。

线程字典（thread dictionary）提供了在嵌套栈帧之间传递参数的良好方法。有时你想设置某些半全局状态，这些状态会在整个方法调用的期间持续，并被该作用范围内的所有方法访问。

经典的 Cocoa 示例是图形上下文对象，它在视图层次结构的根部被设置，然后由所有嵌套调用修改和使用。在 LanguageKit 中，我使用了相同的模式来允许 AST 节点访问编译器对象。在这两种情况下，缺乏紧耦合意味着同一个方法（在同一个对象上）可以在两个不同的线程中被调用，且上下文不同。

## 等待条件

```
(void)addToQueue {
    [condition lock];
    queueSize++;
    [condition signal];
    [condition unlock];
}
(void)main {
    while (1) {
        id pool = [NSAutleasePool new];
        [condition lock];
        while (queueSize == 0) {
            [condition wait];
        }
        queueSize--;
        [condition unlock];
        NSLog("Processed data from queue");
        [pool release];
    }
}
```

来自：`condition.m`

通常，你想让一个线程睡眠并唤醒另一个线程去执行某些操作。POSIX 线程 API为此提供了条件变量（condition variables）。

条件变量与互斥配对。当你等待条件变量时，你首先获取互斥，然后原子地释放它并在条件变量上睡眠。当条件变量被信号时，你会醒来并原子地重新获取互斥。你可以将条件变量视为在线程之间传递互斥锁的方法。

OpenStep 封装了这种低级原语：`NSConditionLock`。与 POSIX 版本不同（POSIX 需要在每次调用时与互斥锁关联），这个类包含了自己的互斥锁并实现了 `NSLocking` 协议。

这意味着你可以将条件锁当作锁使用，尽管那样会浪费资源。除了锁之外，条件锁还关联了一个整数变量，表示条件。当你在条件锁上睡眠时，你可以指定一个值。只有当条件锁被赋予该值信号时，你的线程才会被唤醒。

当你正在等待的条件是一个整数值时，条件锁非常方便，但在其他情况下就不那么方便。通常，你希望一个线程在对象进入特定状态时醒来。使用低级 POSIX 函数实现这一点非常容易，因为它们要求你自己测试条件，但使用 `NSConditionLock` 则没那么容易。

为了解决这个问题，Apple 引入了 `NSCondition` 类。这是对 POSIX 互斥锁和条件变量的简单封装。你可以锁定它，在上面睡眠时释放锁，然后从另一个线程中向它发送信号以唤醒它。

# 等待条件 257

当你从对 `Condition` 的睡眠中醒来时，条件对象将处于锁定状态。你必须测试你的条件，然后要么解锁条件对象，要么回到睡眠状态。

在几乎所有使用条件变量的场景中，都会使用相同的模式。通常，它让你在线程之间建立生产者-消费者关系。消费者线程需要一直睡眠，直到有数据等待它。生产者线程在有数据供它时需要唤醒消费者线程。

本节开头的示例展示了类中的两个方法。`-addToQueue` 方法预计从生产者线程被调用，而 `-main` 方法实现了消费者线程。

消费者线程的代码展示了线程化对象的几个重要特征。它没有使用 `NSRunLoop`，而是实现了自己的运行循环（一个无限循环），并在每次迭代中显式地创建和销毁自动释放池。在每次迭代中，它首先锁定条件，如果没有数据在等待，则释放锁并睡眠。

生产者线程随后可以锁并向条件发送信号。当发生时，消费者线程将在锁可用后立即醒来。生产者通过释放锁允许了这一点。

消费者线程获取下一段数据进行处理并释放锁。在这个示例中，增加和递减共享变量被用作向共享数据结构添加某些数据的代理。

**注意：** 从条件变量唤醒线程的操作序列是非常昂贵的，因此如果可能，最好应该避免。对于两个线程之间的通信，我通常倾向于使用无锁环形缓冲区（lockless ring buffer），它在空一段时间后会切换到锁定模式。Apple 的 Grand Central Dispatch（GCD）在内部实现了这种模型，因此你可以直接使用，而无需自己编写环形缓冲区代码。

# Blocks 与 Grand Central

Objective-C 最近添加的特性之一是支持 *blocks*，也称为 *closures*（闭包）。Blocks 是 *Smalltalk* 的一部分，但由于某些原因在 Objective-C 中被省略。Smalltalk 使用它们进行流控制，而 Objective-C 继承了 C 流控制原语，因此不需要它们。编译器和运行时库额外的复杂性，加上速度上的*代价*，意味着它们最初对 Objective-C 来说并不是高优先级。

闭包是一个可以在某些作用域内创建并引用该作用域内变量的函数。通常，一个函数可能会引用三类：全局、参数和局部变量。它可能只存在于全局作用域。相比之下，block 可以在函数内部声明，甚至在另一个 block 内部。

## 将变量绑定到 Blocks

```
int (^add)(int, int) = ^int(int a, int b) {
    return a + b;
};
```

来自：`blockScope.m`

你可以将函数视为 block 的一种特例。函数在概念上是一个声明在全局作用域内的 block。

因此，block 最简单的情况等同于函数。它们在实现上略有不同，但在这种情况下差异很小。

block 最简单的情况就是函数。它接受某些参数，产生某些输出，并且不引用自身作用域之外的任何内容。本节开头的代码展示了这种 block 的示例。该声明位于全局作用域，看起来是冗长形式。

另一种 block 会引用声明时函数的作用域的内容。你可以在 `blockScope.m` 的其余部分看到这种 block。

这个 block 引用了两个变量。`counter` 是静态变量，这意味着它存储在从程序映像映射的内存中。

# 第 15 章：Blocks 与 Grand Central



```c
10 void(^getCounter(void))(void)
11 {
12   static int counter;
13   int c = counter;
14   void(^block)(void) = ^(void)
15   {
16     printf("current: %d ", counter);
17     printf("old: %d\n", c);
18 };
19   counter++;
20   return _Block_copy(block);
21 }
22
23 int main(void)
24 {
25   void(^block)(void) = getCounter();
26   block(); block();
27   void(^block2)(void) = getCounter();
28   block2(); block2();
29   block(); block();
30   return 0;
```

来自：`blockScope.m`

```
1 current: 1 old: 0
2 current: 1 old: 0
3 current: 2 old: 1
4 current: 2 old: 1
5 current: 2 old: 0
6 current: 2 old: 0
```

输出自：`blockScope.m`

传统的闭包（closure）指的是外层作用域中的真实变量，而不是副本。你可以通过使用 `__block` 修饰符声明变量来实现这种行为。这种实现方式非常复杂：变量会从栈上移动到堆内存中一个引用计数的代码块中。这意味着对它的任何引用都将指向同一个变量。`blockCapture.m` 示例演示了这一点，该函数创建了两个关联的计数器。

```c
typedef int(^counter_t)(void);
void linkedCounters(counter_t *a, counter_t *b)
{
    __block int c = 0;
    *a = ^(void) { return ++c };
    *b = ^(void) { return ++c };
    *a = _Block_copy(*a);
    *b = _Block_copy(*b);
    c++;
}

int main(void)
{
    counter_t pre, post;
    linkedCounters(&post, &pre);
    printf("%d %d, %d %d\n",
        pre(), post(), pre(), post());
    return 0;
}
```

> 来自：`blockCapture.m`

这两个计数器都引用内存中的同一个变量：一个返回它的值然后对其递增；另一个先对其递增再返回值。当你运行此程序时，你会发现调用一个 block 会影响下一次调用另一个 block 的返回值。

```
2 2, 4, 4
输出自：blockCapture.m
```

当你下一次调用 `linkedCounters()` 函数时，你将获得一对 block，它们指向一个新的计数器变量。请注意 `static` 和 `__block` 存储类型修饰符之间的区别。它们都具有相似的效果，即将变量从栈上移出并允许其生存周期比函数更长，但它们的工作方式非常不同。

当你将变量声明为 `static` 时，对它的每一个引用都将指向同一块内存。当你将变量声明为 `__block` 时，对它的每一个引用都将指向同一块内存，但每当你进入声明该变量的作用域时，你都会获得一个新副本。

## 使用 Blocks 管理内存

```objc
__block int counter;
int(^block)(void) = { return counter++; };
block = [block retain];
_Block_release(block);
```

来自：`blockMemory.m`

Cocoa 中的内存管理传统上使用引用计数。Blocks 的工作方式也是如此。有两个函数控制 block 的引用计数。`_Block_copy()` 函数增加其引用计数，而 `_Block_release()` 函数则减少它。

第一个函数没有命名为 `_Block_retain()`，是为了显式地表示返回的 block 可能不是作为参数传递的那个。在某些情况下，block 可能会分配在栈上，然后在被复制时被复制到堆上。

在 Objective-C 中，你也可以向 block 发 `-retain` 和 `-autorelease` 消息，就像发送任何其他对象一样。事实上，你可以向 block 发送任何想要的消息，但它们只对少数消息响应。如果你向 block 发送任何消息，编译器不会给出警告，但你会得到运行时异常。

被 block 引用的变量的内存管理可能更难理解。`blockRetain.m` 示例展示了两个引用对象的 block。第一个获取了对象指针的副本，第二个由于 `__block` 存储修饰符而获取了共享引用。

当你 retain 持有对象指针副本的 block 时，对象也会隐式地、自动地被 retain。注意这只会发生一次。当你 retain 该 block 时：

```objc
id a = [@"@a" mutableCopy];
__block id b = [@"@b" mutableCopy];
unsigned long (^refCountA)() = ^(
    { return [a retainCount]; };
unsigned long (^refCountB)() = ^(
    { return [b retainCount]; };
printf("%ld %ld\n", refCountA(), refCountB());
refCountA = _Block_copy(refCountA);
refCountB = _Block_copy(refCountB);
printf("%ld %ld\n", refCountA(), refCountB());
```

输出自：`blockRetain.m`

```
1 1
2 2
```

## 在后台执行操作

```objc
id a = [@"@a" mutableCopy];
__block id b = [@"@b" mutableCopy];
unsigned long (^refCountA)() = ^(
    { return [a retainCount]; };
unsigned long (^refCountB)() = ^(
    { return [b retainCount]; };
printf("%ld %ld\n", refCountA(), refCountB());
```

来自：`blockRetain.m`

```objc
dispatch_queue_t q = dispatch_get_global_queue(0,0);
__block int count = 0;
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ printf("%d\n", count); });
```

输出自：`blockdispatch.m`

```
3
```

## 创建自定义工作队列

```objc
dispatch_queue_t q =
    dispatch_queue_create("Example",0);
    __block int count = 0;
    dispatch_async(q, ^(void){ count++; });
    dispatch_async(q, ^(void){ count++; });
    dispatch_async(q, ^(void){ printf("%d\n", count); });
```

来自：`libdispatchFIFO.m`

Grand Central 默认创建了三个并发队列。这些队列在三个优先级级别注册：低、默认和高。在每个队列上并发运行的任务数量取决于系统的负载和 CPU 可用的核心。你可以通过上一节中看到的 `dispatch_get_global_queue()` 函数获取这些核心中一个的句柄。

创建一个并发队列是没有意义的。推入并发队列的块将按照推入的顺序开始执行，但它们可能会以任意顺序完成，并且可能有任意数量的任务同时运行。

还有一个特殊的队列，旨在在主线程上运行。你可以通过 `dispatch_get_main_queue()` 获取它的引用。该队列在 OS X 10.6 上用于实现运行循环（run loop）。

该队列是一个 FIFO（先进先出）队列，你可能希望创建类似的队列。FIFO 队列类似于轻量级线程。它按顺序执行，一次执行一个块。线程和队列之间的关系是变化的。取决于各种因素，所有的队列最终可能会在不同的线程上并发运行，也可以在单个 OS 线程上执行。

你通过调用 `dispatch_queue_create()` 创建一个新的 FIFO 队列。当你有一系列需要按定义顺序执行但又与程序其他部分大部分独立的任务时，这非常有用。这有助于减少对显式同步的需求。

本章开头的示例向一个新队列推入了了三个增加计数器的块和一个打印其最终值的块。这些块都是相关的；以错误的顺序执行它们是一个非常糟糕的主意。通过这种方法，它们彼此之间的执行顺序是有保证的，但对于程序的其他部分来说则不如此。这意味着你不需要在计数器变量上加任何锁，除非你计划从队列外部访问它。

## 通知 (Notifications)

Objective-C 鼓励松耦合，Foundation 框架中没有什么比通知机制更能体现这一点的了。通知是为任意数量的监听器实现回调的简单方法。

你可以根据特定的名称、特定的对象或两者兼有来监听通知。通知本身包含一个发送者、一个名称以及与之关联的字典，因此对象可以向监听通知的对象传递任意长度的信息。

如果你使用通知，将使你的类可复用变得非常容易。你不需要期望每个想要监听你的类发送事件的类都实现特定的接口，你只需要发布通知即可。任意数量的类可以监听来自同一个对象的通知，而你的类不需要实现存储这些类引用的任何逻辑。

## 请求通知 (Requesting Notifications)

```objc
- (void)notify:(NSNotification*)note
{
    NSLog("Received %@", note);
}
- (void)registerListener
{
    NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
    [nc addObserver:self
             selector:@selector(notify:)
                 name:@"Example"
                 object:nil];
}
- (void)dealloc
{
    NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
    [nc removeObserver:self];
    [super dealloc];
}
```

来自：`notify.m`

要监听通知，你需要在当前线程的 `NSNotificationCenter` 对象注册这些感兴趣。这是通知的路由点。当通知被发布时，它会被发送到通知中心，然后转发给所有感兴趣的。

大多数情况下，你将使用默认通知中心。可以为不同的用途创建不同的通知中心，但最常用的是标准的那个。它通过向 `NSNotificationCenter` 发送 `+defaultCenter` 消息获取。

注册通知时，向中心发送 `-addObserver:selector:name:object:` 消息。注意消息中的 `selector` 参数。单个对象可能在不同的方法上接收不同的通知。这非常有用，因为这意味着你不需要测试收到了什么种的通知，可以将不同的事件处理器干净地分离到不同的方法中。

在注册观察者时，对象或通知名称可以是 `nil`。这允许你注册接收特定对象发送的所有消息，或者接收特定类型的所有通知（无论其发送者是谁）。

这些对于调试其他任何事物更有用。例如，你可以写一个日志切面，监听所有特定类型的通知并记录发送者。

监听通知时需要记住的重要的一点是，通知中心不会保留你的对象。如果你的对象在销毁时仍注册了接收通知，那么当下次发送这些通知之一时，你的程序将会崩溃。

为了避免这种情况，请确保在 `-dealloc` 方法中向通知中心发送 `-removeObserver:` 消息。如果你忘记这样做，崩溃将不会明显。你将在回溯中看到很多奇怪的东西，包括通知中心。

## 发送通知 (Sending Notifications)

```objc
NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
[nc postNotificationName:@"Example" 
                   object:@"sender" 
                   userInfo:nil];
```

来自：`notify.m`

发布通知比注册监听还要简单。发布通知对象的标准方法构造一个 Notification 对象然后发送它。

在实践中，我认为我从未见过那样做的代码。通知中心有一些便利方法，可以在单个操作中构造并发布通知。

发送通知最常见的方法是 `postNotificationName:object:userInfo` 方法。此这种方法的简化版本，它省略了 `userInfo` 参数并等同于传递 `nil`。

注意，对象——通知的发送者——是作为参数指定的。这意味着可能可以发送声称来自另一个对象的通知。这意味着例如，外观模式（facades）或 C 代码可以代表其他对象发送通知。

## 入队通知 (Enqueuing Notifications)

```objc
NSNotificationQueue *nq = [NSNotificationQueue defaultQueue];
NSNotification *note = [NSNotification notificationName:@"Example" 
object:@"sender"];
[nq enqueueNotification:note postingStyle:NPostWhenIdle];
[[nq currentRunLoop] run];
```

来自：`notify.m`

有时，你的代码可能会产生大量的通知，或者产生不需要立即处理的通知。`NSQueue` 类解决了这两个问题。

通知队列可以延迟交付通知并合并它们。与 `NotificationCenter` 不同，队列没有构造通知的便利方法，你必须自己完成。然后以三种发布样式之一发布通知。

在这个示例中，通知的交付被延迟到运行循环中没有其他事件时。定时器和文件描述符上的数据就绪具有优先级。或者，你可以在下一次运行循环迭代或立即发布。

如果你发送大量相同类型的通知，缓存通知对象是一个好主意。反复将同一个对象传递给通知队列是非常便宜的，它可以自动只发送一次通知。

如果你使用较长的方法入队通知，参数之一是 `coalesceMask:`，它决定了如何合并通知。你可以合并具有相同名称的通知、具有相同发送者的通知，或者两者。

合并配合 `NPostWhenIdle` 发布样式最有用。你可以在代码忙碌时多次发送相同的通知，然后当没有其他事件需要处理时，通知队列将只发布通知的一个副本。这对于触发某些低优先级后台工作的代码片段非常理想。

在 Foundation 框架内对其进行了扩展，为应用程序之间的通信提供了一种（简单的）机制。`NSDSistributedNotificationCenter` 类是 `NSNotificationCenter` 的子类，它可以向其他应用程序广播通知。此扩展需要一些更改。普通通知带有一个发送者，该发送者是指向某个对象的指针。在具有另一个地址空间的进程中，指向对象的指针并不特别有用，因此分布式通知使用字符串作为发送者。可以是任何你喜欢的字符串，但通常是应用程序名称。

通知可以关联字典。在应用程序内部，这些字典可以包含任何对象，但对于广播，它们被限制为可以存储在属性列表（property lists）中的对象（参见第 9 章）。

**注意：** 在 OS X 上，只有一种分布式通知中心类型，向与发送者具有相同用户 ID 的运行应用程序发送通知。GNUstep 提供了另外两个：一个用于与计算机上的所有应用程序通信（无论用户是谁），另一个用于在局域网内广播通知。

分布式通知的传递语义也略有不同。当你发布一个（普通）通知时，它是同步传递的。发送对象已经拥有了 CPU 的控制权。其方法的栈帧位于栈顶，它可以自由地将程序流委托给通知中心，然后由通知中心将其委托给通知监听器。

对于分布式通知，情况并非如此。你不能在函数的中间¹中断另一个进程正在执行的操作，因此你必须等待到一个合适的点。

分布式通知通过与运行循环（run loop）交互处理这个问题。要接收分布式通知，你必须使用 `NSRunLoop`。`distributedNotify.m` 是一个简单的程序，每当它的新实例启动时，都会写入一条日志消息。

该类的 `-init` 方法执行了所有的实际工作。首先，它为分布式通知注册了观察者。该对象是 `nil`，因此它将从任何发送者接收此通知。然后它构建了通知。`user info` 字典包含一个键值对，用于存储进程 ID（PID）。

发布通知后，它启动了运行循环。程序将处于阻塞状态，直到某些运行循环事件发生。该程序中只有一个事件定义了处理程序，因此它所做的就是：

> ¹嗯，你可以这样做；信号（signals）正是这样做的，但从信号处理程序中可以执行的操作是非常有限的。

## 在应用程序之间发送通知



```objectivec
- (id)init
{
  NSDistributedNotificationCenter *c =
    [NSDistributedNotificationCenter
    defaultCenter];

  [c addObserver:self
      selector:@selector(newCopyStartedDidStart)
      name:ProcessDidStart
      object:nil
      suspensionBehavior:NSNotificationSuspensionBehaviorHold];

  ProcessInfo *pinfo = [NSProcess processInfo];
  Number *pid = [NSNumber initWithInt:[processIdentifier]];
  NSDictionary *userInfo = [Dictionary
    dictionaryWithObject:pid
    forKey:@"pid"];

  [c postNotificationName:ProcessDidStart
      object:[pinfo processName]
      userInfo:userInfo
      options:0];

  [[NSRLoop currentRunLoop] run];
}
```

来自：`distributedNotification.m`

每当发布`ProcessDidStart`通知时，都会接收`-newCopyStarted`消息，这只有在运行该程序的另一个副本时才会发生。

如果你编译并运行此示例，你会看到它接收到了自己的通知，因此它会告诉你是它已经启动。如果你运行另一个副本，你将收到每个运行实例发送的日志消息，告诉你关于新实例的信息。

这是一个非常简单的例子，但使用分布式通知处理更复杂的事件也很容易。例如，我在 XMPPKit 中使用它们，在用户更改在线状态时通知所有运行的应用程序。其他程序监听此变化，并将新的状态消息推送到微博客站点。

## 网络访问

编写网络感知应用程序的标准跨平台方法是 Berkeley Sockets API。它是作为开发 TCP/IP 的同一项资助的一部分编写的，并设计为与协议无关。

大多数语言都有此 API 的实现。在 Objective-C 中，你像既往一样可以自由使用 C 版本，它提供了低级接口的所有功能。

然而，大多数情况下，这付出了大量努力却收益极小。Foundation 框架提供了几个类，使得编写网络应用程序变得更加容易。使用这些抽象有时会让你丢失一些低级 API 的功能，但并不多。

## 封装 C Sockets

```objectivec
return
[[NSFileHandle alloc]
    initWithFileDescriptor:s
    closeOnDealloc:YES];
```

来自：`NSFileHandle+Socket.m`

我们在第 13 章简要查看了 `NSFileHandle` 类，我提到过它封装了一个文件描述符。socket API 的设计基于 UNIX 的“万物皆文件（即使在不合逻辑时也是如此）”模型，因此 socket 也是文件描述符。你可以使用与任何其他文件描述符相同的函数调用来对 socket 进行读写操作。

你也可以使用 `NSFileHandle` 来封装 socket。这允许你使用低级 API 创建一个符合你精确规范的 socket，然后使用更抽象的方式与创建的 socket 交互。如果你需要使用高级 API 无法方便暴露的低级 socket API 的任何部分，那么这就是你可以使用的唯一解决方案。在其他情况下，它通常是最方便的。

将 socket 封装在文件描述符对象中最大的优势是你可以轻松地将其与运行循环集成。这让你能够非常容易地编写事件驱动代码。

## 封装 C Sockets

**注意：** 记住 Objective-C 的目标是为 C 程序员提供便利。不要仅仅为了使用而使用 Objective-C API，只有当它们比 C API 更适合解决你的问题时才使用。使用一个对 C API 进行简单封装的 Objective-C API 会增加开销和复杂性，但不会让你的代码变得更容易。

巨大的优势是你可以对 socket 使用 Objective-C 引用计数。如果你在创建 `NSFileHandle` 时向 `closeOnDealloc:` 参数传递 `YES`，那么文件描述符会在对象被销毁时关闭。

如果你向对象发送 `-waitForInBackgroundAndNotify` 消息，它会被添加到运行循环等待的文件描述符列表中。在下一次运行循环中，如果有数据在等待，`NSFileHandle` 对象将发布通知。如果你为此通知注册了处理程序，你就可以读取新数据。

该方法的文档某种具有误导性。它声称该方法将创建一个线程。事实上，在 OS X 上，运行循环使用 `queue()` API¹并调用此

¹GNUStep 可能会使用 `poll()` 或 `select()` 代替。

## 第 17 章：网络访问

方法将另一个文件描述符添加到它等待的列表中。在 OS X 10.6 上，这是通过使用中央调度（GCD）来实现发布通知的，但核心功能是相同的。

最后一个优势是你就不再需要考虑缓冲区了。当你从 socket 读取数据时，你通常需要分配一个缓冲区并将指针传递给 `read()` 或 `recv()` 系统调用。使用文件描述符对象，你需要 NSData 实例。

如果你正在编写大量的字符串，你可能考虑在 `NSFileHandle` 上添加一个分类，提供 `-writeUTF8String` 和 `-readUTF8String` 方法，或者为你协议使用的编码提供等效方法，以便直接获取和发送字符串。

## 连接服务器

```objectivec
InputStream *in;
OutputStream *out;
NSHost *host = [NSHost hostWithName:
@example.com];
NSStream getStreamsToHost:host
port:80
inputStream:&in
outputStream:&out];

[in open];
```

来自：`nsstream.m`

Objective-C 提供了一组类似于 Java 的流类用于网络通信，以及底层的 UNIX 接口。遗憾的是，这些流版本并不特别有用。它们没有提供一种整洁的方式来添加像压缩之类的过滤器或在连接过程中进行加密协商，而许多现代协议都需要这些功能。

然而，最令人困扰的局限性是它们很难支持 SRV 记录。这些是 DNS 记录，用于发布服务到端口的映射，以及主机名到 IP 地址的映射。它们被 DNS-SD 使用，但由于 IP 地址的短缺，它们在公网的层级 DNS 中也变得越来越常见。

如果你在 OS X 上使用 POSIX `getaddrinfo()` 函数查询服务器地址，你将提供一个主机名和服务名。系统会将这些项映射到任何支持的协议上的网络地址和端口号。

当你构造一个 `NSStream` 时，必须将端口号指定为整数。这意味着它在任何使用 DNS SRV 记录的服务上都将失败。但是，如果你使用 `getaddrinfo()`并将生成的 socket 封装在 `NSFileHandle` 中，它就能正常工作。在 EtoileFoundation 中，我们为 `NSFileHandle` 提供了一个分类（category），允许你直接从主机名和协议创建文件句柄，封装了这一调用。

## 第 17 章：网络访问

```c
hints.ai_family = PF_UNSPEC;
hints.ai_socktype = SOCK_STREAM;
// 请求流地址。
error = getaddrinfo(server, service, &hints, &res0);
if (error) { return nil; }

int s = -1;
for (struct addrinfo *res = res0; res != NULL && s < 0; res = res->ai_next)
{
    s = socket(res->ai_family, res->ai_socktype, res->ai_protocol);
    // 如果 socket 失败，尝试下一个地址
    if (s < 0) { continue; }

    // 如果连接失败，尝试下一个地址
    if (connect(s, res->ai_addr, res->ai_addrlen) < 0) {
        close(s);
        s = -1;
        continue;
    }
}
freeaddrinfo(res0);
```

> 出自：`NSFileHandle+Socket.m`

该分类在 `NSFileHandle+Socket.m` 示例中显示。当你调用 `getaddrinfo()` 时，你以 C 字符串提供服务器和服务类型，以及一组指示你想要的 socket 类型的提示（hints）。然后你会得到一个 `addrinfo` 结构体数组，其中包含了构造连接 socket 所需的信息。

这些项按照解析器认为最佳的顺序排列，因此你通常会轮尝试每一个，直到找到一个可以运行的。如果你同时具有 IPv6 和 v4 访问能力，那么如果存在指向两者的 DNS 条目，这段代码将都会尝试两者。

## 跨网络共享对象

```objectivec
NSMutableDictionary *object = [NSMutableDictionary new];
NSConnection *conn = [NSConnection new];
[conn setRootObject:object];
if ([conn registerName:@"sharedDict"]) {
    [NSRunLoop currentRunLoop run];
}
```

> 出自：`doPublish.m`

Objective-C 最强大且最少被使用的部分之一是分布式对象系统。如果你向一个对象发送消息，而该对象不知道如何处理它，那么它将接收一个 `-forwardInvocation:` 消息，该消息包含一个封装了该消息的对象。

就像 Objective-C 中的其他所有内容一样，你可以检查这个对象。它会告知你选择器（selector）、参数数量以及所有参数的类型和值。

Foundation 框架包含一个类 `NSDistanceObject`，它利用了这一点。远端对象是一个代理，用于将消息转发到远程对象。远程对象可能在不同的进程中，甚至在不同的计算机上。

如果你将对象作为参数传递给发送远端对象的的消息，那么它们可能会被复制，或者在远端创建一个远程代理来将消息传回。

使用分布式对象非常简单。任何使用它们的程序都分为部分：客户端和服务器。服务器向其他进程提供对象，而客户端连接到服务器并访问它们。

默认情况下，对象仅在本地机器上共享。若要在跨网络共享它们，你必须在注册对象时使用 `NSSocketPortNameServer`。

```objectivec
NSMutableDictionary *object = (id)[NSConnection rootProxyForConnectionWithRegisteredName:@"sharedDict" host:nil];
NSLog("Object: %@", object);
[object setObject:@"Value" forKey:@"aKey"];
NSLog("Object: %@", object);
```

> 出自：`doAccess.m`

本章开始的示例显示了一个在进程间共享 `NSMutableDictionary` 实例的简单程序。注意，你必须使用 `NSRLoop` 来服务分布式对象。分布式对象系统用于通信的 IPC 通道（Mach端口或 socket）添加到循环（run loop）中。当另一个进程向该端口发送消息时，某些数据通过该通道到达，DO 系统会收到通知。

随后它从接收到的数据构造一个 `NSInvocation` 并调用它，然后返回结果。

```text
doAccess[85613:903] Object: 
doAccess[85613:903] aKey = Value;
```

源自 `doAccess.m`

## 寻找网络节点

```objectivec
ProcessInfo *pi = [ProcessInfo processInfo];
NSString *name = [NSString stringWithFormat:@"%@", pi userName];
NSService *service = [[NSService alloc] initWithDomain:@".local" type:@"@" port:123];
NSServiceBrowser *sb = [NSServiceBrowser new];
[sb setDelegate:self];
[sb searchForOfType:@"@" inDomain:@".local"];
[service publish];
```

源自 `netservice.m`

```objectivec
ProcessInfo *pi = [ProcessInfo processInfo];
NSString *name = [NSString stringWithFormat:@"%@", pi userName];
NSService *service = [[NSService alloc] initWithDomain:@".local" type:@"@" port:123];
NSServiceBrowser *sb = [NSServiceBrowser new];
[sb setDelegate:self];
[sb searchForOfType:@"@" inDomain:@".local"];
[service publish];
```

类型：

多年来，NetBIOS 和 AppleTalk 在局域网中很常见，直到它们被 TCP/IP 取代。IETF 的 ZeroConf 工作组提议多播 DNS (mDNS) 作为解决方案。DNS 是一种可扩展的发布方式，但它与 mDNS 结合时最有用。这两个标准的组合通常被称为 Bonjour，并通过 `NSService` 类暴露给 Objective-C。这允许应用程序发布 DNS-SD 记录并查找特定服务的所有记录。

许多应用程序在 OS X 上使用它。Safari 使用它共享书签；iChat 使用它查找联系人；iTunes 使用它共享音乐；系统使用它查找共享文件夹和打印机。如果你正在编写任何类型的网络应用程序，使用 `NSService` 发布节点可能会很有帮助。

当你发布服务时，必须指定一个唯一的名称。如果你在使用分布式对象（我们将在本章末尾介绍），可以使用此处作为你服务的对象的名称，并忽略 Bonjour 系统的 DNS 底层。对于其他情况，你发布的端口通常更有用，而名称将是你呈现给用户的。

你使用 `NSServiceBrowser` 类搜索节点。这在用法上有点复杂。发布服务是同步的；你向 `NSService` 实例发送 `-publish` 消息，服务就会发布。搜索是异步的，并且需要活跃的运行循环。

当你向浏览器发送消息时，它将传输 DNS 请求。可能一段时间后才会响应，你可能不想在搜索时停止用户操作，因此此方法立即返回。

当它收到响应时，该类将向其代理发送带有新 `NSService` 实例的消息，描述找到的每个服务器。它将一直监听，直到你发送 `-stop` 消息。在很多情况下，你永远不会发送此消息。你可以让浏览器在进程的生命周期内在后台运行，并在每当局域网出现新节点时收到通知。然后你就可以触发用户界面更新显示新的对等。这就像 iTunes 所做的，当网络上出现新的共享播放列表时，将它们添加到库中。

# 调试 Objective-C

程序员分为两种：一类是第一次就能写出完美代码的人，另一类是确实存在的人。如果你属于第一类，可以跳过本章。如果你属于后一类，那么你会有这样时候：尝试运行代码并发现它的运行并不符合预期。

这是一种令人沮丧的体验，但如果你能快速修复问题，这种挫败感就会减轻很多。在本章中，我们将观察定位 Objective-C 程序中 bug 原因的一些技术。

## 检查对象

```objectivec
@interface DebugObject : NSObject @end
@implementation DebugObject
- (NSString*)description
{
    return @"Not a very helpful message";
}
@end
void debug(id anObject) {};
```

来自：`description.m`

在大多数情况下，当你调试一个 Objective-C 程序时，你会使用 GNU 调试器（GDB），它对 Objective-C 有一些内置支持。如果你通过 Xcode，那么你实际上是通过图形化界面使用 GDB。你可以从“运行”（Run）菜单访问命令行界面。这通常很有用，因为 Xcode 只为调试器的最常用功能提供了 GUI，而不是涵盖所有功能。

GDB 有两个特性使得它非常适合 Objective-C。第一个特性是它带有一个内置的 Objective-C 解析器和解释器，因此你可以在调试器中编写 Objective-C 表达式并以这种方式检查变量。第二个是 `print-object` 命令。

该命令会打印一个对象。它的实现原理向对象发送一个 `-description` 消息，返回一个描述对象的 `NSString`。这意味着它只对有效对象有效。如果你尝试对过早释放或内存已损坏的对象使用此命令：



```
$ gdb ./a.out
(gdb) break debug
Breakpoint 1 at 0x10000e4d: file description.m,
   line 10.
(gdb) r
Starting program: a.out
Breakpoint 1, debug (anObject=0x100111bc0) at
   description.m:10
10 void debug(id anObject) {}
(gdb) print anObject
$1 = (id) 0x100111bc0
(gdb) print-object anObject
Not a very helpful message
(gdb) print-object [NSObject new]
<NSObject: 0x10011c30>
(gdb) print-object [anObject class]
DebugObject
(gdb) print-object [anObject className]
DebugObject
(gdb) print-object anObject->isa
DebugObject
```

输出来自：`description.m`

那么调试器要么崩溃，要么捕获到段错误信号。

该方法在 `NSObject` 中的默认实现只是打印类名和地址。其他各种标准对象以不同的方式实现它。例如，集合类（Collection classes）以属性列表格式打印它们的内容。

这个示例返回了一个非常没有用的信息，但在你的代码中，你应该尝试提供更有帮助的信息。

## 识别内存问题

```
id pool = [NSAutoreleasePool new];
MutableString *str = [MutableString
WithString: @"example"];
pool = [NSAutoreleasePool new];
NSSet *set = [NSSetWithObject:str];
```

**来自：`prematureDealloc`**

Objective-C 中的常见问题之一。如果你在某处遗漏了一个 `-retain` 消息，你就会在不增加引用计数的情况下持有一个指针。如果其他地方有它的引用，或者它被自动释放（autoreleased），那么这个指针可能会保持很长时间有效直到突然变得失效。

当指针失效时，你通常会在 Mac 运行时的 `objc_msgSend()` 中或 GNU 运行时的 `objc_msg_lookup()` 中遇到崩溃。这是因为运行时尝试查找处理消息的方法，但类指针现在指向了某个无效的内容。

在调试器中，通过向上移动堆栈直到找到消息接收者（message receiver），你可以非常容易地找到那个被释放的对象。你还可以使用 `NSZombie` 类。当设置了环境变量 `NSZombieEnable` 时，对象将不会被释放。相反，它们的类将被设置为 `NSZombie`，它只会记录日志：

```
$ gcc -framework Cocoa -g prematureDealloc.m &&
./a.out
Segmentation fault
$ gdb ./a.out
(gdb) r
Starting program: a.out
Program received signal EXC_BAD_ACCESS, Could not
access memory.
Reason: KERN_INVALID_ADDRESS at address: 0x00000007a0000010
0x0000007ff829111c in objc_msgSend (
(gdb) up 6
# 0x00000001000000ef in main ()
prematureDealloc.m:9
$ NSSet *set = [NSSet setObject:str];
(gdb) print-object anObject
$1 = (id) 0x100111bc0
(gdb) print-object [NSObject new]
(gdb) print-object
Program received signal EXC_BAD_ACCESS, Could not
access memory.
Reason: KERN_INVALID_ADDRESS at address: 0x00000007a0000010
0x0000007ff829111c in objc_msgSend (
(gdb) up 6
# 0x00000001000000ef in main ()
prematureDealloc.m:9
$ NSSet *set = [NSSet setObject:str];
(gdb) print-object anObject
Not a very helpful message
(gdb) print-object [NSObject new]
<NSObject: 0x10011c30>
(gdb) print-object [anObject class]
DebugObject
(gdb) print-object [anObject className]
DebugObject
(gdb) print-object anObject->isa
DebugObject
```

如果你在 `objc_exception_throw()` 上设置断点，就可以捕获所有异常，无论它们是如何被抛出的。这也会捕获像字符串这样在 OS 上未正式支持但仍然有效的。

## 监控异常

在 C 代码中，标准库提供了 `assert()` 宏，当谓词参数为假时它会记录消息并调用 `abort()`。Objective-C 的版本略有不同。

```
void throw(void)
{
    [[NSException exceptionWithName:@"ExampleException" reason:@"Watch this" object:nil] throw];
}
```

如果你在 `objc_exception_throw()` 上设置断点，你就能看到它是在被抛出的。

```
$ gdb ./a.out
(gdb) break objc_exception_throw
Breakpoint 1 at 0x10000e4d
(gdb) r
Starting program: a.out
Terminating app due to uncaught exception
'ExampleException', reason: 'Watch this'
```

## 断言预期（Assertions）

更有用。

Foundation 提供了两个宏：`NSAssert()` 和 `NSCAssert()`。如果你在使用 C99（你应该这样做），那么这些是变变宏；否则你将需要使用固定数量参数的变体，例如 `NSAssert1()`。`NSAssert()` 会引用 `self`，因此可以在 Objective-C 方法体中使用。`NSAssert()` 可以在 C 函数中使用。

与 C 语言的变体不同，这些宏在断言为假时不会中止程序（abort）。相反，它们会向每个线程的断言处理器对象发送一条消息。该对象默认是 `NSAssertionHandler` 的实例，并且当你触发断言时，它会抛出一个 `NSInternalConsistencyException`。你可以捕获它并恢复，但大多数情况下，它会到达堆栈顶端并导致程序中止。

如果你想实现其他行为，可以创建 `NSAssertionHandler` 的自己的子类，并重写一个或两个断言处理方法。这个示例忽略了 C 函数中的断言，仅在遇到它们时记录一条消息。

```
$ ./a.out
a.out[40031:903] Ignoring assert on line 21 of
   main in $@
```

输出自：`assert.m`

想要重写此功能是非常寻常的，但某些很好的理由你可能会这样做。最明显的理由之一是错误报告。当遇到断言时，意味着你的程序发生了严重的错误。你可能想要收集一些关于导致这种情况的情况的信息，并将其上传到错误跟踪系统，而不是仅仅是崩溃。

你可以通过定义 `NS_BLOCK_ASSERTERTS` 宏来禁用断言。这通常只在性能敏感的代码中值得这样做。通常，浪费一点 CPU 时间比在未定义状态下继续运行要好。

## 记录调试消息（Logging Debug Messages）

```objc
(void)log
{
    NSLog("%s:%d:%s (%@) Log message", __FILE__,
         __LINE__, __PRETTY_FUNCTION__, self);
}
```

**源自：** `nslog.m`

我们已经在很多代码中使用 `NSLog()` 函数。当你在终端中运行应用程序时，传递给 `NSLog()` 的消息将进入标准错误流。在 OS X 上，`NSLog()` 图形应用程序会将消息发送到系统控制台。在 Microsoft Windows 上，通过 GNUstep，它们将进入系统事件监视器。`Log()` 函数写入一个格式化字符串，前面带有日期、时间、进程名称和进程 ID。当你在格式化字符串中使用 `%@` 标识符时，它使用与调试器完全相同的方法获取对象的字符串表示。

GNUstep Additions 框架提供了一系列日志宏，`NSDebugLog()` 族。它们封装了 `NSLog()`，但只有在用户详细信息设置了特定值时才记录日志。这使得根据每个方面或每个框架开启或关闭日志变得非常简单。

你还可以使用编译器在构建格式化字符串时定义的特殊宏。`__FILE__` 宏是一个包含当前源文件名称的 C 字符串字符串。`__LINE__` 宏是一个整数，包含当前行号。最后，`__PRETTY_FUNCTION__` 宏会展开为包含当前方法或函数名称的 C 字符串。

```
1 ./a.out
2 2010-03-11 15:57:43.200 a.out[40861:903] nslog.m
   :9-[Log log] (<Log: 0x100112b70>) Log
   message
```

输出自：`nslog.m`

## Objective-C 运行时（The Objective-C Runtime）

正如我在书开头提到的，一个 Objective-C 的实现由两部分组成：编译器和运行时库。编译器获取源代码，并将动态部分转换为对运行时库的调用。

运行时库是用 C 语言编写的，这意味着它是用 Objective-C 的子集编写的。运行时库的所有接口（包括由编译器生成的代码调用的接口）对 Objective-C 代码都是可用的。

Objective-C 中所有动态的内容都由运行时库实现。显而易见的例子是消息发送（message sending）。当你发送一条消息时，运行时负责决定由谁来处理它。

这并不是运行时库的唯一责任。它还处理该语言所有的内省（introspection）功能。它跟踪所有的类和协议元数据，并将其暴露给程序员。

当你使用键值编码（key-value coding）时，你是在（间接））使用 Objective-C 运行时函数来查找接收者上的方法和实例变量。

# 通过名称发送消息（Sending Messages by Name）

```objc
id obj = [NSObject new];
SEL sel = SelectorFromString("@release");
IMP release = [obj methodForSelector:sel];
release(obj, sel);
```

源自：`methodByName`

Objective-C 方法是通过一个间接层调用的 C 函数。其具体实现方式在不同的运行时之间略有不同。在 NeXT 和 Apple 运行时中，简单的消息发送是使用 `objc_msgSend()` 函数实现的。

遗憾的是，这并不是你需要的唯一函数。该函数被声明返回一个 `id`，并将与任何具有相同调用约定的方法工作。例如，在 Darwin/x86 上，对象指针在 `eax` 寄存器中返回。当你发送一条消息时，运行时负责决定由谁来处理它。

这并不是运行时库的唯一责任。它还处理该语言所有的内省功能。它跟踪所有的类和协议元数据，并将其暴露给程序员。

当你使用键值编码时，你是在（间接））使用 Objective-C 运行时函数来查找接收者上的方法和实例变量。

Objective-C 中所有动态的内容都由运行时库实现。显而易见的例子是消息发送。当你发送一条消息时，运行时负责决定由谁来处理它。

这并不是运行时库的唯一责任。它还处理该语言所有的内省功能。它跟踪所有的类和协议元数据，并将其暴露给程序员。

当你使用键值编码时，你是在（间接））使用 Objective-C 运行时函数来查找接收者上的方法和实例变量。

Objective-C 中所有动态的内容都由运行时库实现。显而易见的例子是消息发送。当你发送一条消息时，运行时负责决定由谁来处理它。

遗憾的是，这并不是你需要的唯一函数。该函数被声明返回一个 `id`，并将与任何具有相同调用约定的方法工作。例如，在 Darwin/x86 上，对象指针在 `eax` 寄存器中返回。

1. Objective-C 运行时

## 通过名称发送消息

```objc
id obj = [NSObject new];
SEL sel = SelectorFromString("@release");
IMP release = [obj methodForSelector:sel];
release(obj, sel);
```

源自：`methodByName`

Objective-C 方法是通过一个间接层调用的 C 函数。其具体实现方式在不同的运行时之间略有不同。在 NeXT 和 Apple 运行时中，简单的消息发送是使用 `objc_msgSend()` 函数实现的。

遗憾的是，这并不是你需要的唯一函数。该函数被声明返回一个 `id`，并将与任何具有相同调用约定的方法工作。例如，在 Darwin/x86 上，对象指针在 `eax` 寄存器中返回。

Objective-C 中所有动态的内容都由运行时库实现。显而易见的例子是消息发送。当你发送一条消息时，运行时负责决定由谁来处理它。

这并不是运行时库的唯一责任。它还处理该语言所有的内省功能。它跟踪所有的类和协议元数据，并将其暴露给程序员。

当你使用键值编码时，你是在（间接））使用 Objective-C 运行时函数来查找接收者上的方法和实例变量。

Objective-C 中所有动态的内容都由运行时库实现。显而易见的例子是消息发送。当你发送一条消息时，运行时负责决定由谁来处理它。

遗憾的是，这并不是你需要的唯一函数。该函数被声明返回一个 `id`，并将与任何具有相同调用约定的方法工作。例如，在 Darwin/x86 上，对象指针在 `eax` 寄存器中返回。

# 按名称查找类（Finding Classes by Name）

```objc
Class nswiew = ClassFromString("NSView");
if (Nil == nswiew)
{
    NSLog("@Not linked against AppKit");
}
else
{
    id view = [nswiew new];
    NSLog("@View: %@", view);
}
```

源自：`weakClass`

运行时责任之一是存储所有加载类的表。你可以遍历此表，查看每个类，也可以使用它按名称查找类。后者对于实现弱引用（weak references）特别有用。这些引用由运行时直接支持，但尚未通过语言暴露。弱引用的背后思想是你可以可选地使用一个类。

你可能会在一个使用了 Foundation 类的框架中编写代码，如果你链接了 AppKit，就可以使用 AppKit 类。这样该框架就可以任何有 Foundation 实现的地方工作，但在可用时会利用 AppKit 特性。你还可以使用这种机制避免对第三方框架的依赖。

# 测试对象是否理解某个方法（Testing If an Object Understands a Method）

```
$ gcc -framework Foundation -g -std=c99 weakClass.m && ./a.out
a.out[53194:903] Not linked against AppKit
$ gcc -framework Cocoa -g -std=c99 weakClass.m && ./a.out
a.out[53184:903] View: <NSView: 0x1001163b0>
```

输出自：`weakClass.m`

注意当此示例链接到 Cocoa（链接 AppKit 和 Foundation）和 Foundation 时输出的差异。如果 `NSView` 类存在，它会创建一个实例。如果不存在，它就会记录一条消息。

你还可以将这种机制用于必须与框架旧版本向后兼容的代码。如果你使用这种机制查找新类，你将得到一个可以处理它们不存在时情况的 `Nil` 值。

```objc
sel sel = @selector(delegateMethod:)
if ([delegate respondsToSelector:sel]) {
    [delegate delegateMethod:self];
}
```

源自：`respondsToSelector.m`

Objective-C 代码倾向于利用非正式

## 第19 章：Objective-C 运行时

协议（protocols）。这些是代理（delegate）可以选择实现的消息组。

当你编写使用这些协议的代码时，需要在发送消息之前测试类是否实际上实现了该方法。

**注意：** 这并不完全正确。你也可以在 `@try` 块中发送消息，并在类不理解该方法时捕获抛出的异常。然而，考虑到抛出异常的开销，这并不是推荐的方法。

幸运的是，这样做非常简单。`NSObject` 实现了 `respondsTo:` 方法，用于测试接收者是否处理带有选择器的消息。

该方法不仅由 `NSObject` 实现，也是 `NSObject` 协议的一部分。其他根类也会实现它。这对于转发（forwarding）非常重要。



在`NSObject`中，该方法调用运行时函数`class_respondsToSelector()`。在其他类中，实现方式不同。如果你直接使用运行时函数，代码将非常脆弱。

大多数时候，你想要知道发送给的对象是否会处理消息，而不是它是否有一个处理消息的方法。这些概念在 C++ 等语言中是相同的，但在 Objective-C 中非常不同。

## 消息转发

当你向代理发送`respondsToSelector:`消息时，它将测试真实对象是否有该选择器的方法。被代理的对象可能是另一个代理，它将转发请求。

你也可以通过向类发送`conformsTo:`消息来测试协议遵循情况。注意这仅测试类是否声明采用该协议。类可以在不实现所有方法的情况下采用协议（尽管不应该这样做），但更常见的是类实现协议中的所有方法。

```objc
@interface Facade : NSObject
{
    id delegate;
}
@implementation Facade
    -(id)forwardingTargetForSelector:(SEL)aSel
    {
        return delegate;
    }
    -(void)forwardInvocation:(Invocation*)anInv
    {
        [anInv invokeWithTarget:delegate];
    }
@end
```

## 转发

来自`forward.m`

Objective-C 中的消息旨在类似于 Smalltalk 消息，而不是 C 函数。它们是后期绑定的并且是可以反射的。在底层，它们使用 C 函数实现，但这是一个实现细节。你可以假定消息是在对象之间传递的、经过反射并由方法处理的。

当你向一个没有对应方法的对象发送消息时，Objective-C 仍然有一些方法来处理它。这些方法在 Objective-C 的发展过程中发生了很大。

在旧的 Objective-C 代码中，`forward::`方法被调用。这是一个变长方法，要求接收者知道栈帧结构。NeXT 用`forwardInvocation:`方法替换了它。这种机制非常灵活，但性能并不理想。创建栈帧的开销比正常的消息发送高出数百倍。这意味着在任何性能敏感的地方都不应使用这种机制。

如果你使用这种转发机制，你必须实现`methodSignatureForSelector:`方法。它返回一个代表与消息相关的栈帧的对象。`Invocation`类在封装消息时使用它。

从 10.5 开始，Apple 引入了一种更快的转发机制。如果你的对象实现了`forwardingTargetForSelector`方法，当缺少选择器时它会被调用。它可以返回一个对象，消息将改为传递给该对象。

> 注意：GNU 运行时使用的两阶段消息发送机制不支持这种机制，旧版本的 Apple 运行时也是如此。如果你使用的是最近的 Apple 运行时带有非脆弱 ABI 的运行时，将获得速度优势。否则，你的代码仍然可以工作，只是速度很慢。

这使得像外壳模式（façade pattern）这样的设计变得非常简单。你可以快速将任何你不理解的方法委托给你的代理。如果你需要在调用代理方法之前或之后进行额外处理，只需实现该方法并显式调用代理方法。

318 第19 章：Objective-C 运行时

## 查找类

```objc
int classCount =
objc_getClassList(NULL, 0);
Class *classList =
calloc(classCount, sizeof(classList));
objc_getClassList(classList, classCount);
for (int i=0; i<classCount ; i++)
{
    [classes addObject:
    NSStringFromClass(
    classList[i]]);
}
free(classList);
[classes sortUsingSelector:@selector(compare:)];
```

来自`classTree.m`查找 Objective-C 类有两种方法。如果你知道名称，可以直接使用`NSClassFromString()`函数。它接受一个字符串对象作为参数并返回类，如果没有注册该名称的类则返回 Nil。

如果你不知道类的名称，你需要采取不同的方法。在某些情况下，你可能想知道一个类但尚不知道它的名称。例如，如果你有一个插件架构，你可能会允许用户指定要加载的 bundle，然后想要收集特定类的所有子类，或者所有遵循给定协议的类。

> **注意：** 在测试类的协议遵循情况时，最好使用运行时函数，而不是发送`+conformsToProtocol:`消息。许多类使用`+initialize`进行懒初始化，向它们发送消息会导致即使你没有实际在使用该类也会运行这段代码。

`objc_getClassList()`函数将给你类的数组。它接受两个指针作为参数，一个是用于返回类的数组，另一个是缓冲区的大小。如果你用 NULL 作为第一个参数调用它，它不会返回任何类，但会告诉你有多少个。

一旦你有了这个数组，就可以遍历它并检查这些类。在这个示例中，我只是将类名存储在数组中并排序。在下一节中，你将看到如何获取类名并打印每个类的实例变量和方法。

如果你正在搜索符合特定协议的类，那么你应该使用`class_conformsToProtocol()`函数。这会告诉你该类是否符合指定的协议。如果是，你就可以将其添加到已加载的插件列表中。

## 检查字符

```objc
const char *name = [className UTF8String];
printf("%s\n\tivars:\n", name);
Class cls = NSClassFromString(className);
unsigned int ivarCount;
Ivar *ivars=class_copyivarList(cls, &ivarCount);
for (unsigned int i=0; i<ivarCount; i++)
{
    printf("%s\t%s\n", ivar_getName(ivars[i]));
}
free(ivars);
unsigned int methodCount;
Method *methods=class_copyMethodList(cls, &methodCount);
printf("%s\n\tmethods:\n", name);
for (unsigned int i=0; i<methodCount; i++)
{
    printf("%s\t%s\n", method_getName(methods[i]));
}
free(methods);
```

随着时间的推移，演进 ABI 会变得更容易。类结构的布局可以通过修改编译器和运行时来更改，而不需要更改任何其他代码。`classTree.m`示例打印了系统中所有类的实例变量和方法。你可以访问到更多的元数据。例如，实例变量存储了它们的类型以及距离对象起始位置的偏移。

这些信息被用于 KVC（键值编码）的实现。当你为一个键设置值且 KVC 允许直接访问实例变量时，它会首先找到一个名称匹配的实例变量。然后它会找到类型并确定是否需要对对象进行解箱（unbox）。最后，它会将 ivar 偏移量加到对象指针，然后在该地址执行赋值。

它对访问器方法（accessor methods）执行类似的操作。方法存储了它们的名称、类型和方法指针。类型信息非常重要，因为它允许其他代码构建调用帧。通过检查访问器方法的类型，KVC 代码可以将方法指针强制转换为正确的类型然后调用它，从而设置或获取特定的属性。在较新的运行时中，对于声明的属性也存储了元数据。你对类所设置的几乎任何内容都可以通过调用运行时函数进行检查。

# 第19 章：Objective-C 运行时

你无法获取单个方法的源代码的情况。

## 创建新类

```objc
#include <objc/runtime.h>
id fakeDealloc(id self, SEL _cmd, ...)
{
    NSLog("@%s sent a -dealloc message", self);
}
void makeIndestructible(id obj)
{
    Class new = objc_allocateClassPair(obj->isa, "Fake", 0);
    class_addMethod(new, @selector(dealloc), (IMP)fakeDealloc, "v@");
    objc_registerClassPair(new);
    obj->isa = new;
}
```

来自: `newClass.m`

在运行时创建新类是非常罕见的，但它确实为非常动态的行为或优化提供了很多机会。我们已经看了实现此点的 Foundation 框架。键值观察（KVO）机制创建新类来拦截访问器方法的调用。

在运行时创建类最重要的的一点是，它展示了 Objective-C 的核心原则之一：编译器所做的一切都不是魔法。你可以在自己的 C 代码中生成编译器从 Objective-C 代码中生成的所有内容。当然，编译器可能会在优化结果方面做得更好，而 Objective-C 版本会更简单。如果情况并非如此，Objective-C 就没什么意义了。

创建一个新类涉及三个步骤。首先，你分配类对（class pair），然后你添加方法、实例变量和协议，最后向运行时注册该类对。

**注意：** “类对”（class pair）这个术语可能看起来很困惑。你源代码中的每个 Objective-C 类在运行时都会编译为两个类。对象是类的实例，而类是*元类*（metaclass）的实例。实例方法附加到类上，而类方法附加到元类上。当你向类发送消息时，将使用该*元类*来查找对应的方法。

当你分配类对时，你必须提供父类、新类的名称以及在类结构末尾添加的空间大小。新类的名称必须是唯一的。如果你调用两次函数，本节的示例代码将无法工作。解决此问题的简单方法是在静态变量中保留一个计数器，每次创建新类时原子性地增加它，并将其附加到类名字符串上。

当类类创建与 *isa-swizzling* 结合时，类末尾的额外空间可以非常有用。更改现有类的 *isa* 指针让你添加方法，但不能添加实例变量。不过，你可以在类结构的末尾创建一些空间并在那里存储额外数据。调用`object_getIndexedIvars()`并将类作为参数将给你该数据的起始地址。

你可以使用此功能来实现其他对象模型。例如，我曾它为 Objective-C 添加了基于原型的（prototype-based）面向对象特性，允许闭包作为方法并添加到单个对象中。

## 索引

- category, 35, 183

- abstract superclass, 94

- CF, 见 Core Foundation

- associative array, 143

- Clang, 13

- class cluster, 93, 101, 119, 136, 138, 152

- auto-boxing, 200

- autorelease pool, 65

- class extension, 37

- class version, 82

- closures, 56, 259

- Cocoa bindings, 203

- bag, 142

- blocks, 56, 259

- condition variables, 255

- Bonjour, 293

- contention scopes, 248

- boxing, 101

- Core Foundation, 114

- bundles, 239

- C integers, 100

- declared properties, 39

- canonical locale, 109, 118

- + defaults domain, 178

- + filesystem domain, 242

- + delegation pattern, 63, 90

- + designated initializer, 84

- + forwarding, 316

- + distributed objects, 289

- + DNS discovery, 293

- + DNS-SD, 见 discovery

- + garbage collection, 31

- + GCC, 见 Collection

- + GDB, 见 debugger

- + delegate, 221

- + error domain, 224

- + error recovery, 224

- + event driven programming, 97

- + eventter, 98

- + exceptions, 210

- + fast enumeration, 120, 146

- + Grand Central Dispatch, 286

- + facade pattern, 91

- informal protocols, 313

- instance variables, 19

- intrinsic types, 99

- isa-swizzling, 206, 324

- + ivars, 见 instance variables

- + libdispatch, 267

- + libobjc, 见 runtime

- + LLVM, 见 Level Machine

- + LP64, 100

- + map, 143

- + mDNS, 见 multicast

- + memory unit, 228

- + message forwarding, 316

- metaclass, 323

- + MMU, 见 memory management

- + multicast DNS, 293

- + key paths, 202

- + key-value coding, 144, 195

- + key-value observing, 195

- + KVC, 见 key-value coding

- + KVO, 见 key-value observing

- + mutable subclass, 21, 136

- + Calendar class, 161, 166

- + mutex, 见 exclusion lock

- + mutual exclusion lock, 251

- + CharacterSet class, 111, 125

- + Coder class, 183

- + Coding protocol, 81, 183

- + nonatomic, 41

- + notification, 273

- + ComparisonResult, 117

- + UIApplication class, 167

- + ConditionLock class, 256

- + Archiver class, 81

- + Control class, 99

- + Copying protocol, 79, 143

- + Assert() macro, 305

- + CountSet class, 142

- + Assertion-Handler class, 305

- + Data class, 124, 228

- + AttributedString class, 134

- + Date class, 158

- + DateComponents class, 162, 166

- + AutoreleasePool class, 65, 131

- + Formatter class, 161, 165

- + Bundle class, 239, 243

- + Decimal type, 106

- + Font class, 134

- + DecimalNumber class, 106

- + IndexSet class, 139

- Dictionary class, 196, 217, 233

- Integer type, 100

- Invocation class, 45, 167, 291, 317

- DistantObject class, 290

- Locale class, 190

- Distributed-Notification-Center class, 279

- NSLog() function, 132, 306

- Document class, 193

- NSMutableArray class, 19, 137

- Numerator class, 146

- MutableCopying protocol, 129, 136

- Error class, 174, 224

- MutableString, 128

- Exception class, 214, 302

- Fast-Enumeration protocol, 146

- NetService class, 293

- FileHandle class, 97, 221, 229, 284

- NetService-Browser class, 294

- FileManager class, 227, 230, 233

- Notification class, 276

- + Notification-Queue class, 277

- + Set class, 141

- + Stream class, 223, 287

- + Null class, 138

- NSString class, 119, 142, 234

- Number class, 94, 102, 200

- + Task class, 187

- + Object class, 30, 34, 60, 84, 131, 197

- + Thread class, 246

- + TimeInterval type, 157



- `Object` debugging support, 299
- `Timer` class, 97, 166
- `Object` protocol, 314
- `UserDefaults` class, 178, 189
- `ProcessInfo` class, 185
- `Value` class, 101
- PropertyList Serialization class, 172, 174, 177
- `View` class, 91
- `Workspace` class, 227
- `Proxy` class, 30, 34
- `Zombie` class, 300
- `RecursiveLock` class, 251
- `NSRunLoop` class, 65, 97, 167, 257, 280, 291
- Objective-C runtime library, 10, 309
- `NSScanner` class, 110, 166

## 索引

Objective-C 类型编码, 102

单例模式, 87, 94, 231

字符串对象, 113

# P

`plutil` 工具, 177

异常终止, 192

过早优化, 116

# T

原始类型方法, 96

线程字典, 232

属性列表（property lists）, 80, 131, 279

免费桥接, 114

纯虚方法, 154

两阶段创建模式, 76

类型化选择器, 55

# R

参考日期, 158

# U

替换方法, 36

`UIApplication` 类, 167

可恢复异常, 221

`unichar` 类型, 114

运行循环（run loop）, 97, 167, 180, 294

# V

# S

变长参数函数, 130

变长参数方法, 131, 138

`SEL` 类型, 21, 27

虚函数表, 3

选择器（selector）, 27, 45, 311, 316

`vtables`，见虚函数表

# X

`XCode`, 16, 298

# W

# Z

弱类引用, 312

零成本异常处理, 212

工作区进程, 227

弱引用置零, 72
