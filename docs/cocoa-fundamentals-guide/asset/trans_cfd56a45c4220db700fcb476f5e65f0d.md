
# CHAPTER 1

# 什么是 Cocoa？

还有许多用于性能分析和其它开发任务的命令行工具。有些位于 `/usr/bin` 和 `/usr/sbin` 中，而一些由 Apple 开发的命令行工具则安装在 `<Xcode>/Tools` 中。对于这些工具中的许多，你可以查阅其手册页以获取使用信息。 （为此，在 Xcode 中选择 Help > Open page in Xcode，或在 Terminal shell 中输入 `man` 后跟工具名称）。

> **进一步阅读：** 有关可用于 Cocoa 开发的性能工具和应用程序的更多信息，以及与性能相关的概念、技术、指南和策略的信息，请参阅 *Cocoa Performance Guidelines* 涵盖了 Cocoa 的指南。

# Cocoa 框架

什么构成了 Cocoa 程序？并不是语言，因为你可以在 Cocoa 开发中使用多种语言。也不是开发工具，因为你也可以从命令行创建 Cocoa 应用程序（尽管这将是一项复杂、耗时的任务）。不，真正让所有 Cocoa 框架都具有——使它们与众不同的是——它们由对象组成，这些对象很大程度上继承自根类，并且最终基于 Objective-C 运行时。此说法也适用于所有 Cocoa 框架。

> **注意：** 关于根类的说法需要放在首位。Foundation 框架提供了另一个根，`NSProxy`；然而，`NSProxy` 在 Cocoa 编程中很少使用。其次，你可以创建自己的根类，但这将是一项大量工作（需要编写与 Objective-C 运行时交互的代码），可能不值得花费时间。

在任何系统上都有许多 Cocoa 框架，Apple 和第三方厂商一直在不断发布更多框架。尽管 Cocoa 框架众多，但在每个平台上都有两个核心框架脱颖而出：

- 在 OS X 中：Foundation 和 AppKit
- 在 iOS 中：Foundation 和 UIKit

除非你链接它们，否则 Foundation、AppKit 和 UIKit 框架对于 Mac OS X 的 Cocoa 应用程序开发至关重要。如果你链接（并使用 AppKit 的类），则无法为 iOS 开发 Cocoa 应用程序，除非你链接（并使用 UIKit 的类）。而且，除非你链接（并使用 Foundation 框架的类），否则你无法开发任何类型的 Cocoa 软件。 （在 Mac OS X 中，链接 Cocoa 伞形框架时会自动链接正确的框架。）Foundation 和 AppKit 中的类、函数、数据类型和常量以 "NS" 为前缀；UIKit 中的类、函数、数据类型和常量以 "UI" 为前缀。

> **注意：** 在 Mac OS X 10.5 版本中，Cocoa 框架被移植以支持 64 位寻址。iOS 也支持 64 位寻址。作为此工作的一个部分，对 Cocoa API 进行了各种通用更改，最显著的是引入了 NSInteger 和 NSUInt 类型（在适当的地方取代 int 和 unsigned）以及 CGFloat 类型（取代大多数 float 实例）。大多数应用程序无需立即进行 64 位转换，但对于那些需要转换的应用程序，提供了移植工具和指南。64-Bit Transition Guide for Cocoa 详细介绍了这些事项。

Cocoa 框架为你处理许多低级任务。例如，存储和操作整数和浮点值的类会自动为你处理这些值的字节序。

以下各节概述了三个核心 Cocoa 框架的功能和类，并描述了一些次要框架。由于每个核心框架都有数十个类，因此对核心框架的描述按其功能对类进行分类。尽管这些分类具有很强的逻辑基础，但也可以以其他方式合理地对类进行分组。

# Foundation

Foundation 框架定义了一层基础类，可用于任何类型的 Cocoa 程序。从 AppKit 中选择 Foundation 中的类的标准是用户界面。如果一个对象既不出现在用户界面中，也不是专门用于支持用户界面的，则其类属于 Foundation。你可以创建仅使用 Foundation 而不使用其他框架的 Cocoa 程序；例如命令行工具和 Internet 服务。

Foundation 框架的设计目标如下：

- 定义基本行为并为内存管理、对象可变性、通知等引入一致的约定。
- 支持国际化和本地化，其中包括（[content]
# CHAPTER 1

# 什么是 Cocoa？

还有许多用于性能分析和其它开发任务的命令行工具。有些位于 `/usr/bin` 和 `/usr/sbin` 中，而一些由 Apple 开发的命令行工具则安装在 `<Xcode>/Tools` 中。对于这些工具中的许多，你可以查阅其手册页以获取使用信息。 （为此，在 Xcode 中选择 Help > Open page in Xcode，或在 Terminal shell 中输入 `man` 后跟工具名称）。

> **进一步阅读：** 有关可用于 Cocoa 开发的性能工具和应用程序的更多信息，以及与性能相关的概念、技术、指南和策略的信息，请参阅 *Cocoa Performance Guidelines* 涵盖了 Cocoa 的指南。

# Cocoa 框架

什么构成了 Cocoa 程序？并不是语言，因为你可以在 Cocoa 开发中使用多种语言。也不是开发工具，因为你也可以从命令行创建 Cocoa 应用程序（尽管这将是一项复杂、耗时的任务）。不，真正让所有 Cocoa 框架都具有——使它们与众不同的是——它们由对象组成，这些对象很大程度上继承自根类，并且最终基于 Objective-C 运行时。此说法也适用于所有 Cocoa 框架。

> **注意：** 关于根类的说法需要放在首位。Foundation 框架提供了另一个根，`NSProxy`；然而，`NSProxy` 在 Cocoa 编程中很少使用。其次，你可以创建自己的根类，但这将是一项大量工作（需要编写与 Objective-C 运行时交互的代码），可能不值得花费时间。

在任何系统上都有许多 Cocoa 框架，Apple 和第三方厂商一直在不断发布更多框架。尽管 Cocoa 框架众多，但在每个平台上都有两个核心框架脱颖而出：

- 在 OS X 中：Foundation 和 AppKit
- 在 iOS 中：Foundation 和 UIKit

除非你链接它们，否则 Foundation、AppKit 和 UIKit 框架对于 Mac OS X 的 Cocoa 应用程序开发至关重要。如果你链接（并使用 AppKit 的类），则无法为 iOS 开发 Cocoa 应用程序，除非你链接（并使用 UIKit 的类）。而且，除非你链接（并使用 Foundation 框架的类），否则你无法开发任何类型的 Cocoa 软件。 （在 Mac OS X 中，链接 Cocoa 伞形框架时会自动链接正确的框架。）Foundation 和 AppKit 中的类、函数、数据类型和常量以 "NS" 为前缀；UIKit 中的类、函数、数据类型和常量以 "UI" 为前缀。

> **注意：** 在 Mac OS X 10.5 版本中，Cocoa 框架被移植以支持 64 位寻址。iOS 也支持 64 位寻址。作为此工作的一个部分，对 Cocoa API 进行了各种通用更改，最显著的是引入了 NSInteger 和 NSUInt 类型（在适当的地方取代 int 和 unsigned）以及 CGFloat 类型（取代大多数 float 实例）。大多数应用程序无需立即进行 64 位转换，但对于那些需要转换的应用程序，提供了移植工具和指南。64-Bit Transition Guide for Cocoa 详细介绍了这些事项。

Cocoa 框架为你处理许多低级任务。例如，存储和操作整数和浮点值的类会自动为你处理这些值的字节序。

以下各节概述了三个核心 Cocoa 框架的功能和类，并描述了一些次要框架。由于每个核心框架都有数十个类，因此对核心框架的描述按其功能对类进行分类。尽管这些分类具有很强的逻辑基础，但也可以以其他方式合理地对类进行分组。

# Foundation

Foundation 框架定义了一层基础类，可用于任何类型的 Cocoa 程序。从 AppKit 中选择 Foundation 中的类的标准是用户界面。如果一个对象既不出现在用户界面中，也不是专门用于支持用户界面的，则其类属于 Foundation。你可以创建仅使用 Foundation 而不使用其他框架的 Cocoa 程序；例如命令行工具和 Internet 服务。

Foundation 框架的设计目标如下：

- 定义基本行为并为内存管理、对象可变性、通知等引入一致的约定。
- 支持国际化和本地化，其中包括（其中包括）捆绑技术和 Unicode 字符串。
- 支持对象持久化。
- 提供一定程度的操作系统独立性以支持可移植性。
- 提供程序化原语的对象包装器或等价物，例如数值、字符串和集合。它还提供了用于访问底层系统服务和实体的类，例如端口、线程和文件系统。

Cocoa 应用程序按定义链接 AppKit 框架或 UIKit 框架，必然必须链接 Foundation 框架，因为它们共享根类 NSObject，并且 AppKit 和 UIKit 的大多数方法和函数都有 Foundation 对象作为参数或返回值。一些 Foundation 类似乎是为应用程序设计的——NSManager 和 NSUserDefaults 就是两个例子——但它们包含在 Foundation 中，因为它们可以用于不需要用户界面的程序。

The Cocoa Frameworks
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

# CHAPTER 1

What Is Cocoa?

# Foundation Paradigms and Policies

Foundation 为 Cocoa 编程引入了若干范式和策略，以确保项目中对象在某些情况下的行为和期望一致：

- **对象保留和释放。** Objective-C 运行时和 Foundation 为 Cocoa 程序提供了两种确保对象在需要时存在、在不再需要时释放的方法。垃圾回收是在 Objective-C 2.0 中引入的，会自动跟踪并分解你不再需要的对象，释放内存。Foundation 仍然提供传统的内存管理方法。它制定了对象所有权策略，即对象对其创建、复制或显式保留的对象负责释放。`NSObject` 类和方法 `NSAutleasepool` 实现了延迟释放机制，Cocoa 程序对调用者负责的对象保留有一致的约定。有关垃圾回收和显式内存管理的更多信息，请参阅 [Object Retention and Disposal]。

iOS 垃圾回收不可用于运行在 iOS 上的应用程序。

- **可变类。** Foundation 中各种值类和容器类都有不可变类的可变变体，可变类是不可变类的子类。如果你需要动态更改此类对象的值或成员资格，你可以创建可变类的实例。由于它继承自不可变类，你可以将可变实例传递给接受不可变类型的 方法。有关对象可变性的更多信息，请参阅 "Object Mutability"（第 90 页）。

- **类簇。** 类簇是一组私有子类，抽象类充当其接口。根据上下文（特别是你用来创建对象的方法），会向你返回优化类的实例。例如，`NSString` 和 `NSMutableString` 充当针对不同存储类型优化的私有子类的代理。多年来，具体类的集合发生了多次变化，但并未破坏应用程序。有关类簇的更多信息，请参阅 "Class Clusters"（第 95 页）。

- **通知。** 通知是 Cocoa 中的主要设计模式。它基于广播机制，允许对象（称为观察者）被告知另一个对象在用户或系统事件的世界中所做或所遇到的情况。通知对象可能不知道观察者的存在或身份。有几种类型的通知：同步、异步和分布式。Foundation 通知机制由 `NSNotificationCenter`、`NSNotificationQueue` 和 `NSDistributedNotificationCenter` 类实现。有关更多信息，请参阅 "Notifications"（第 190 页）。

# Foundation Classes

Foundation 层次结构以 `NSObject` 类为根，该类（连同 `NSObject` 和 `NSCopying` 协议）定义了基本属性和行为。有关 `NSObject` 的更多信息，请参阅 "The Root Class"（第 66 页）。

其余的 Foundation 框架由相关的类组以及一些单独的类组成。有表示数据类型（如字符串和字节数组）的类，用于存储其他对象的类，表示系统信息的类，例如，以及类

