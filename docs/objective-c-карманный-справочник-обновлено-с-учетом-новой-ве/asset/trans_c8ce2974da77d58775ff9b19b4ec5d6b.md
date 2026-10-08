

## 14 第1章：Objective-C 哲学

这是 Objective-C 2 所要求的。为了解决这个问题，我编写了一个作为 Étoilé 组成部分的框架，它实现了大部分缺失的功能，并实现了 Apple 随 OS X 10.5 引入的公共运行时 API。

该框架现在是 GNustep 的一部分，用于旧版本的 GCC 运行时。我还编写了一个新的运行时，支持旧的 GCC ABI 和一种新的非脆弱性（non-fragile）ABI，后者现在在功能上与 OS X 保持一致。它是作为 GNUestep 项目的一部分开发的，被称为 GNUestep 运行时或 libobjc2。

通过 Clang 和由 GNUestep 项目提供的运行时，你可以获得对所有 Objective-C 2 特性的完整支持，包括非脆弱性实例变量。这意味着你可以在 Windows、Linux、*BSD、Solaris 等*系统上使用 Objective-C 2。至少已经人在 QNX 上测试过它，它也可能运行在 Symbian 上。

如果你使用 GCC 版本的运行时，配合 GNUestep 中的 Objective-C 2 框架，那么你可以获得某些功能，例如快速枚举和声明属性，但你无法获得新 ABI 的任何好处。GCC 4.6 及更高版本也带有一个更新的运行时，提供了相同级别的兼容性，但不再需要 Objective-C 2 兼容框架。

## 编译 Objective-C 程序

## 编译 Objective-C 程序

```bash
$ gcc scanner.m
Undefined symbols:
"_OBJC_CLASS__NSAutleasePool", referenced
from:
  _objc_classrefs__DATA@00 in ccoRpaJq.o
"_objc_msgSend", referenced from:
  _main in ccoRpaJq.o

$ # 在 OS X 上
$ gcc -framework Foundation scanner.m
$ # 在其他平台上
$ gcc gnustep-config --objc-flags --base-libs scanner.m
```

Clang 前端旨在作为 GCC 的无缝替换，因此在任何指令中看到 gcc 的地方，都可以将其替换为 clang。在 OS X 上，GCC 安装在 `/usr/bin/gcc`，因此它在你的路径中。对于较旧版本的 Xcode 工具，Clang 安装在 `/Developer/usr/bin/clang`，因此你可能需要指定完整路径或将此位置添加到你的路径中。在其他平台上，如果安装了，你通常可以在路径中同时找到它们。

如果你熟悉使用这些编译器中的任一者编译 C 或 C++，你会发现编译 Objective-C 非常熟悉。如果你只需在命令行上指定一个源文件，编译器将尝试将其编译并链接为可执行文件。

## 第1章：Objective-C 哲学

**注意：** Apple 在其 2011 年开发者大会上的演讲表示“GCC 正在离开”。Apple 不再积极开发 GCC，因此它缺乏对最近添加的语言特性的支持，可能不会在未来的 Apple 开发者工具中发布。在编译器方面，Apple 的营销有些令人困惑。OS X 10.7 发布了被他们描述为“Apple LLVM 编译器 3.0”的东西。这是 Clang 大约在 2.9 和 3.0 版本之间中间位置的一个快照。如果你运行 `clang -version`，你将在输出中看到类似“based on LLVM 3.0svn”的内容。

在大多数情况下，这是不起作用的。Objective-C 程序需要其他库。在 OS X 上，编译器驱动程序支持一个额外的选项：`-framework`，它指定了一个包含头文件和共享库的框架包。这既是链接器选项，也是预处理器选项。

书中的示例都使用了 Foundation 框架。在其他平台上，这通常由 GNUStep Base 库实现。这些平台通常不支持 `-framework` 选项。`gnustep-config` 工具提供了替代方案。它将打印编译 Objective-C 所需的编译器选项，以及链接到基础（Foundation）或图形界面（AppKit）库的所需的选项。

就像 C 和 C++ 一样，你可以指定 `-c` 仅编译文件而不链接，并使用 `-o` 指定输出名称。如果你正在编译多个文件，你可能想使用比从命令行运行编译器更稍微高级一点的方法。

在 OS X 上，你可能会使用 XCode IDE。它允许你创建具有多种不同模板类型的项目。如果你需要在其他平台上编译这些项目，你可以在 GNustep 仓库中找到一个名为 `pbxbuild` 的工具，它可以编译它们。

如果你在其他平台上工作，你可以使用 GNustep Make 进行构建。这在 OS X 上同样适用，因此无论你选择哪种方案，都不应该因为你的构建系统而产生可移植性问题。

## Objective-C 入门

Objective-C 是对 C 语言的一组非常小的补充。Smalltalk 的第一个版本是作为一个赌注，认为在一张纸上指定整个通用语言是可能的。Objective-C 对 C 的扩展比 Smalltalk 稍微复杂一点，但并不多少。

如果你已经认识 C，那么学习 Objective-C 语言只需要一个下午——如果你已经理解了 Smalltalk 风格的面向对象，时间会更短。当然，这有一点误导性。如果学习 Objective-C 真的那么简单，你买一本关于它的书会觉得有点亏。像 Smalltalk 一样，Objective-C 语言之所以如此简单的很大原因之一是因为它委托（delegates）。

Objective-C 正如其名，为 C 添加了对象。在 Objective-C 的早期实现中，它非常小。它的设计目的是与 C 一起使用，事实也如此。对象的布局由根类的实例变量（ivars）定义，然后由层次结构中的每个后续类定义。子类只能添加实例变量，不能删除或重排父类的变量。这意味着从内存布局的角度来看，将一个类的指针转换为其父类的指针始终是安全的。从对象类型系统的角度来看，也是安全的；任何子类都会响应父类响应的所有消息。Objective-C 还引入了一个新的指针类型：`id`。在转换规则方面，它大致类似于 `void*`。你可以将任何对象指针转换为 `id`，也可以将 `id` 隐式转换为任何对象指针类型。在 C 中，你需要显式转换来将一个结构转换为另一个。

Objective-C 中的对象指针通过类名后跟星号来标识，就像 C 中的结构指针一样，但没有 `struct` 关键字。你可以隐式地将类实例指针转换为其父类指针。这对于间接父类同样有效。例如 `NSMutableArray` 是 `NSArray` 的子类，而 `NSArray` 是 `NSObject` 的子类。你可以将 `NSMutableArray` 转换为 `NSArray` 或 `NSObject`，反之亦然。转换需要显式转换。

如果你习惯无类型语言（如 Smalltalk、Ruby 或 Python），可能会倾向只使用 `id` 类型。这大部分是安全的，但有一个例外。Objective-C 使用消息名称进行查找，不包含任何类型信息。这意味着你可以在不同的类中声明名称相同但类型不同的方法。当编译器生成消息发送时，它使用接收者的类型来确定参数的类型。这反过来定义了调用帧的布局。当该名称在任何地方只有一个方法时，类型信息是不必须的。如果你想从对象外部访问实例变量，也需要静态类型，但这样做通常被认为是坏习惯。

虽然指定静态类型信息不是必须的，但通常是一个好主意。除了刚才提到的一种情况外，它不会影响代码生成，但它被用于

## 声明类型 21

## 声明类型

