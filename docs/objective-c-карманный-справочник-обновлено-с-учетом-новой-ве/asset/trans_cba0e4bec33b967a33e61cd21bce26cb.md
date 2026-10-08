

# 第一章：Objective-C 哲学

这些可能是由编译器生成的。
在大多数情况下，你不会使用这些类中的任何一个。过去一二十年编写的几乎所有的 Objective-C 代码都使用了 OpenStep Foundation 框架的实现。OpenStep 是 NeXT 和 Sun 共同制定的一项规范，旨在为跨平台应用开发提供一个现代的面向对象的框架。NeXT 在他们的 OPENSTEP 操作系统和 Windows NT 上实现了它，而 Sun 则为 Solaris 提供了一个实现。稍后，GNU 项目交付了第三种实现：GNestep。

OpenStep 定义了两个框架：Foundation Kit（基础套件）和 Application Kit（应用套件），通常简写为 Foundation 和 AppKit。Foundation Kit 提供了开发者所有应用程序所需的核心功能，例如集合类、运行循环、通知分发、操作系统抽象等。Application Kit 构建在 Foundation 之上，为构建图形化应用程序提供额外支持。

Sun 的实现在最初发布后没有进行太多开发。Apple 在几年后收购了 NeXT，并将 OpenStep 环境重命名为 Yellow Box（黄色盒子），将其作为开发环境发布在 Rhapsody 和 Windows 上。随着 OS X 的发布，它再次被重命名，这次称为 Cocoa。

GNestep 项目仍在活跃开发，但现在跟进的是 Apple 对 OpenStep 规范的增强，以及核心规范的更新。这意味着 Foundation 框架几乎可以在任何地方使用，尽管 GNUstep 实现中缺少了一些最新的类和方法。你可以将 Foundation 框架认为是 Objective-C 的标准库。它提供了非复杂程序所需的许多特性。Objective-C 2 的几个特性是专门设计用来与 Foundation 配合使用的。你可以在没有 Foundation 的情况下使用它们，但前提是你必须实现某些等效的内容。

## Objective-C 的历史

“面向对象”一词由 Alan Kay（艾伦）在 20 世纪 60 年代创立，Smalltalk 是他和其他人用来演示这种编程风格的语言。Smalltalk 开发于 20 世纪 70 代，最广泛的版本发布于 1980 年。然而，Smalltalk 运行非常慢。要正确运行它，你需要一台强大的计算机，例如 Xerox Alto，配备 512KB 内存，且理想情况下至少有一个 2MHz 的处理器。Brad Cox 喜欢 Smalltalk 的构想，但他希望有一种语言可以让他用在人们负担得起的计算机上。他的主意是将鼓励封装、松耦合和代码复用的高级语言 Smalltalk 与 C 语言结合。C 语言处于光谱的极另一端，几乎没有封装，没有动态分发，但有一个巨大的优势：它很快。

C 语言很大程度上是基于 PDP-11 指令集的。一个非常原始的 C 编译器就能产生相当快的代码。这在今天也是如此。像 LLVM、XLC 和 ICC 等编译器在优化上投入了大量精力，但几乎没做优化的 PCC 仍然能产生相当快的代码。

Brad Cox 和 Tom Love 在 1986 年使用了 StepStone，销售了一种基于 Brad 早期“面向对象预编译程序”开发的产品。该产品（即 Objective-C）是一个预处理器和一个较小的 Objective-C 运行时库。预处理器生成 C 代码，你可以用你平台的 C 编译器对其进行编译。直到 2010 年，我还遇到过一家在商业产品中仍在使用 StepStone 编译器的公司。

1988 年，NeXT 购买了 StepStone 代码的许可，并直接购买了 Objective-C 的商标。随后，NeXT 将预处理器重写为 GNU 编译器集 (GCC) 的前端。在经过一些法律斗争后，自由软件基金强制他们发布了这些代码，但他们保留了运行时库的私有。GNU 项目随后编写了运行时库的替代品，但进行了一些更改。一个是 GNU 运行时中的选择器（selectors）关联了一个类型。在 NeXT（以及 Apple）平台上，选择器在运行时只是字符串，某些由程序员错误导致的堆栈损坏在 NeXT 运行时中是不可见的。

另一个更改在于消息发送的工作机制。当你使用 NeXT 运行时发送消息时，编译器会将消息发送转换为对 `objc_msgSend()` 函数的调用。它会查找方法然后调用它。遗憾的是，用 C 语言无法实现这个函数。它必须为每个平台以及该平台上的每种调用约定用汇编编写。解决方案是用 `objc_msg_lookup()` 函数来替换它，该函数返回一个函数的指针。这稍微要慢一点，但意味着相同的代码可以在所有平台上运行。

Objective-C 从此以后没有发生太大变化。NeXT 在 1997 年被 Apple 收购，Objective-C 被采纳为其新操作系统 Rhapsody 上 Yellow Box 的主要开发语言。这些后来分别重命名为 Cocoa 和 OS X。2003 年，Apple 在语言中添加了一些类似 Java 的异常处理机制。

下一组升级出现在 2007 年，Apple 引入了 Objective-C 2。这让老牌的 Objective-C 程序员感到有些困惑，因为之前的版本——即 NeXT 发布的版本——已经是 Objective-C 4。幸运的是，“2 是紧跟在 4 之后的数字”的想法似乎没有进入 Cocoa 的任何排序代码中。

Objective-C 2 增加了一些语法糖。它提供了一种新的枚举方式、一种合成访问器方法（accessor methods）的方法，并引入了垃圾回收。Objective-C 2 与其说更是一个营销术语，而不是一种真正的语言。你找不到专门针对它的编译器开关。某些特性（如非脆弱性实例变量）仅在某些运行时可用。其他特性（如垃圾回收）在 iPhone 上并不可用。声明属性（declared properties）是唯一在处处可用的 Objective-C 2 特性。从 iOS 5 和 Mac OS X 10.7，Apple 放弃了版本号，开始使用编译器版本来描述特性。在发布之前，这些新特性被称为 Objective-C 2.1，但 Apple 的营销部门决定不公开使用这个名称。这些新特性包括对数据隐藏更好的支持（使得实现细节更容易从公共头文件中移除），以及自动引用计数（它结合了垃圾回收和手动引用计数的大部分优点，但没有两者的大部分缺点）。

## 跨平台支持

强制 NeXT 将 GCC 的 Objective-C 前端作为自由软件发布对于自由软件基金会来说是一次公关胜利。遗憾的是，从长期跨平台支持的角度来看并不理想。NeXT 发布的代码非常糟糕，而且在过去的十年里，基本上被 GCC 团队忽略了。这在 GCC 4.6 之后有所改进，但仍落后于当前的 Objective-C 版本大约五年。GCC 对 NeXT 时代的 Objective-C 有良好的支持，也支持新的异常处理关键字。GNUstep 项目提供了 Foundation 和 AppKit 框架的实现，这是 NeXT 和 Mac 开发的核心。

2007 年，Apple 开始开发一个新的编译器。Clang 是底层虚拟机（LLVM）的前端，适用于 C 家族语言：C、Objective-C 和 C++。它比 GCC 更具模块化，设计初衷不仅用于编译，还用于代码补全、语法高亮和静态分析。Clang 在不同层的代码之间有清晰分离，并将运行时特定的代码隔离到单独类中。

编译器只是 Objective-C 实现的一半。另一半是运行时库。GNU 运行时是配合 GCC 开发的，并没有实现以下函数

