
## 总结

图 21.20 显示 Xcode 项目窗口，你可以在这里看到与分数计算器项目相关的所有文件。

![](img/e9df1bbea90586fb77610264e0c2bf7c_501_0.png)

图 21.20 分数计算器项目文件

以下总结了你创建 iPhone 分数计算器应用程序所遵循的步骤：

- 1. 创建一个新的单视图应用程序（Single View Application）。
- 2. 将你的 UI 代码输入 `FCVViewController.h` 和 `.m` 文件。
- 3. 向项目添加了 `Fraction` 和 `Calculator` 类。
- 4. 打开 `Main.storyboard` 创建 UI。
- 5. 将主窗口背景设置为浅灰色（Mercury）。
- 6. 创建了一个标签（label）和按钮，并将它们放置在 View 窗口内。
- 7. 按住 Control 点击并拖拽你在 View 窗口中创建的标签到 `UILabel` Outlet 属性显示上。
- 8. 从 View 窗口中的每个按钮按住 Control 点击并拖拽到相应的 IBAction 方法。对于每个数字按钮，你选择了 `clickDigit` 方法。同样，对于每个数字按钮，你将 `tag` 属性设置为相应的对应的数字 0–9，以便 `clickDigit` 方法能够识别是哪个按钮被按下了。

希望这段关于开发 iOS 应用的简要介绍能为你编写 iPhone 应用程序提供一个良好的开始。正如前面提到的，UIKit 提供了许多功能供你探索！

我们的分数计算器应用存在一些局限性。其中许多在随后的练习中得到了解决。

## 练习

- 1. 为分数计算器应用添加一个“转换”（Convert）按钮。按下按钮时，使用 `Fraction` 类的 `convertTo` 方法生成分数结果的数值表示。将结果转换为字符串并显示在计算器的显示器上。
- 2. 修改分数计算器应用，使得在输入分子之前按下 – 键时可以输入负分数。
- 3. 如果为第一个或第二个操作数的分母输入 0，则在分数计算器的显示器上显示字符串 `Error`。
- 4. 修改分数计算器应用，允许进行链式计算。例如，允许输入以下操作：

  1/5 + 2/7 - 3/8 =

# 附录 A

## 术语表

附录包含了你将遇到的许多术语的非正式定义。其中一些术语与 Objective-C 语言本身直接相关，而另一些则源于面向对象编程领域。在后一种情况下，提供了该术语在具体应用于 Objective-C 语言时的含义。

**抽象类（abstract class）** 定义用于使子类更易定义的类。实例是从子类创建的，而不是从抽象类创建。**参见** 具体的子类（concrete subclass）。

**访问器方法（accessor method）** 用于获取或设置实例变量值的方法。使用访问器方法设置和检索实例变量的值符合数据封装的方法论。

**Application Kit** 一个用于开发应用程序用户界面的框架，它包含菜单、工具栏和窗口等对象。它是 Cocoa 的一部分，通常称为 AppKit。

**ARC** 参见自动引用计数（Automatic Reference Counting）。

**归档（archiving）** 将对象数据的表示转换为稍后可以恢复（解档）的格式。

**数组（array）** 值的有序集合。数组可以定义为基础 Objective-C 类型，并在 Foundation 中通过 `NSArray` 和 `NSMutableArray` 类实现为对象。

## 自动引用计数 (ARC)

自动引用计数 (ARC) 一种由编译器管理与对象相关的内存的特性。在 Xcode 4.2 之前，iOS 程序员需要使用手动技术来管理内存，即必须使用 `retain`、`autorelease` 和 `dealloc` 方法。

**自动变量（automatic variable）** 在进入和退出语句时自动分配和释放的变量。自动变量的作用域限于定义它的块（block），且没有其他作用域。

**自动释放池（autorelease pool）** 一个跟踪被延迟释放对象的池。在 ARC 出现之前，它通过 `autorelease` 进行管理。

**位域（bitfield）** 包含特定宽度整数字段的结构。

**块（block）** Objective-C 语言的一种扩展，它可以捕获周围的变量。块可以作为参数传递。

**字符（character）** 位于对引号内的字符序列。如果以 @ 开头，则定义了一个类型为 `NSString` 的常量字符串。

**类（class）** 一一组相关的方法。通过实现（或继承）方法遵循协议。

**类方法（class method）** 通过类接收者调用的方法。参见实例方法。

**类对象（class object）** 一个标识类的对象。在其他地方，类方法通过 `class` 关键字被调用。

**簇（cluster）** 由其他类组成的抽象类。

**Cocoa** 由 Foundation、Core Data 和 Application Kit 框架组成的环境。

**Cocoa Touch** 由 Foundation、Core Data 和 UIKit 框架组成的环境。

**集合（collection）** 数组、字典或集合。

**编译时间（compile time）** 源代码被分析并转换为低级格式（对象代码）的时间。

**复合（composite）** 由其他类组成的类；通常作为子类的替代方案。

**具体的子类（concrete subclass）** 抽象类的子类。可以从具体的子类创建实例。

**遵循（conform）** 如果一个类直接或间接地采用了所有要求的方法，则遵循协议。

**常量字符串（constant string）** 编码在引号内的字符序列。如果以前有 `@`，则定义了一个 `NSString` 类型的常量字符串。

**数据封装（data encapsulation）** 注意数据存储在实例变量中，仅通过对象的方法访问。这维护了数据的完整性。

**代理（delegate）** 由另一个对象执行操作的对象。

**指定的初始化器（designated initializer）** 类中所有初始化方法（或子类中通过 super 调用）的方法。

**字典（dictionary）** 使用 `NSDictionary` 和 `NSMutableDictionary` 实现的键值对集合。

**指令（directive）** 在 Objective-C 中，以符号 @ 开头的特殊结构。`@interface`、`@implementation`、`@end` 和 `@class` 都是指令示例。

**分布式对象（distributed objects）** 一个应用程序中的 Foundation 对象与另一个（可能运行在另一台机器上）的 Foundation 对象通信的能力。

**动态绑定（dynamic binding）** 在运行时而不是编译时间确定要调用的方法。

**类型（typing）** 在运行时而不是编译时间确定对象所属的类。也参见静态类型。

**封装（encapsulation）** 参见数据封装。

**外部变量（extern variable）** 参见全局变量。

**工厂方法（factory method）** 参见类对象。

**正式协议（formal protocol）** 在 `@protocol` 下声明的一组相关方法。不同的类（不一定相关）可以通过实现（或继承）方法来采用正式协议。也参见正式协议。

**转发（forwarding）** 将消息及其关联参数发送另一个方法执行的过程。

**Foundation 框架（Foundation framework）** 一组类、函数和协议，构成了应用程序开发的基础，提供了如内存管理、文件和 URL 访问、归档任务以及处理集合、字符串和日期对象的设施。

**框架（framework）** 一组相关的函数、文档、头文件和其他资源的集合。例如，Cocoa 框架用于在 OS X 上开发图形应用程序。

**函数（function）** 由名称标识的语句块，可以接受传递给它的一个或多个参数，并可以返回返回值。函数可以是静态的（相对于定义它的文件），也可以是全局的，从而可以在其他文件中定义的函数或方法中调用。

# 垃圾回收 (garbage collection)

垃圾回收一种运行时内存管理系统，能够自动释放被引用对象所使用的内存。iOS 运行时环境不支持垃圾回收。

`gcc` 由自由软件基金会 (FSF) 开发的编译器名称，`gcc` 支持许多编程语言，包括 C、Objective-C 和 C++。

`gdb` 配合 `gcc` 使用程序标准调试工具。

`getter` 方法 (`getter method`) 一种获取实例变量值的访问器方法。参见方法 (`method`)。

全局变量 (`global variable`) 定义在任何方法或函数之外的变量，可以被同一文件中的任何方法或函数访问，也可以通过被声明为 `extern` 的其他源文件访问。

头文件 (`header file`) 包含定义、宏和变量声明的文件，通过 `#import` 或 `#include` 语句包含在程序中。

`id` 一个可以持有任何类型对象指针的通用类型。

不可变对象 (`immutable object`) 值不能被修改的对象。Foundation 框架中的示例包括 `NSString`、`NSDictionary` 和 `NSArray` 对象。参见可变 (`mutable`)。

实现部分 (`implementation section`) 类的一个部分，包含对应接口部分（或协议定义指定）中方法的实际代码（即实现）。

非正式协议 (`informal protocol`) 一组逻辑上相关的方法，声明为某个分类 (`category`)，其他声明为根类的一个分类。与正式协议不同，非正式协议中的所有方法并不需要实现。参见协议 (`protocol`)。

继承 (`inheritance`) 将方法和变量从带有根对象的类传递给子类的过程。

实例 (`instance`) 类的具体表示形式。实例是通过向类对象发送 `alloc` 或 `new` 消息创建的实例。

实例方法 (`instance method`) 可以由类的实例调用的方法。参见方法 (`method`)。

实例变量 (`instance variable`) 定义在接口部分（或继承自父类）中，包含在对象的每个实例中。实例方法可以直接访问这些变量。

`Interface Builder` 是 OS X 下的一个工具，用于为应用程序构建图形化用户界面。

接口部分 (`interface section`) 用于声明类、实例变量和方法的部分。对于每个方法，它都声明了参数类型和返回类型。参见实现部分 (`implementation section`)。

国际化 (`internationalization`) 参见本地化 (`localization`)。

`isa` 定义在根对象中的特殊变量，所有对象都继承它。`isa` 变量用于在运行时标识对象所属的类。它也被用于存储有关对象的额外信息。

链接 (`linking`) 将一个或多个对象文件转换为可执行程序的过程。

局部变量 (`local variable`) 作用域局限于其定义的块的变量。变量可以是方法、函数或语句块的局部变量。

通知 (`notification`) 向已注册在特定事件发生时接收警报（通知）的对象发送消息的过程。

本地化 (`localization`) 使程序适用于特定区域运行的过程。

# 预处理器 (preprocessor)

`superclass`（超类）特定类的类的父类。参见 `super`。

`synthesized method`（合成方法）编译器自动为你创建的 setter 或 getter 方法。它被添加到 Objective C 2.0 语言中。

`UIKit` 一个用于为 iOS 设备开发应用程序的框架。除了提供用于处理窗口、按钮和标签等 UI 元素的类外，它还定义了处理加速度计和触摸界面等设备特定特性的类。`UIKit` 是 Cocoa Touch 的一部分。

`Unicode character`（Unicode 字符）一种表示包含数百万字符的字符集的标准。`NSString` 和 `MutableString` 类与包含 Unicode 字符的字符串一起。

`union`（联合体）一种聚合数据类型，例如包含具有相同存储区域成员的结构体。在任何时刻，这些成员中只有一个可以占据该存储区域。

`Xcode` 一种用于 OS X 和 iOS 程序开发的编译和调试工具。

`XML` 扩展性标记语言。OS X 上生成的属性列表（property lists）的默认格式。

## 附录 B

## 通讯录示例源代码

为了参考起，这里是你在第二部分“Foundation 框架”中使用的通讯录示例的完整接口和实现文件。这包含了 AddressCard 和 AddressBook 类的定义。你应该在你的系统中实现这些类；扩展类定义以使其更实用、更强大。这是你学习该语言并熟悉构建程序、处理类和对象以及使用 Foundation 框架的极佳方法。

### AddressCard 接口文件

```
```
