
# Objective-C 编程入门指南

![](img/22d1310b7c22ea2d48cd2058929a5cda_0_0.png)

专业编程人员的必备参考

Developer's Library 系列书籍旨在为实践程序员提供关于其日常工作中使用的编程语言和技术的独特、高质量参考资料和教程。

Developer's Library 的所有书籍均由专家技术从业者编写，他们擅长以对其他程序员有用的方式组织和展示信息。

核心书目包括各领域最优秀、最受赞誉的书籍：

Developer's Library 系列书籍可在大多数零售和在线书店购买，也可以通过 Safari Books Online (safari.informit.com) 进行订阅。

## 开发者库

纽约 · 多伦多 · 蒙特尔 · 伦敦 · 慕尼黑 · 巴黎 · 马德里

ISBN 978-0-321-81190-5 (平装)。

- 1. Objective-C (计算机编程语言) 2. 面向对象编程 (计算机科学) 3. Macintosh (计算机)-编程。

I. 标题

005.1'17-dc23

第二次印刷：2012年3月

## 警告与免责声明

批量购买或特殊销售时，Pearson 提供优厚的折扣。欲了解更多信息，请联系：

收购编辑：Mark Taber

开发编辑：Michael Thurston

执行编辑：Sandra Schroeder

项目编辑：Mandie Frank

索引编辑：Heather McNeill

校对：Sheri Cain

技术编辑：Wendy Muir

出版协调：Vanessa Evan

设计：Gary Aydar

排字：Mark Shirar

致 Roy 和 Ve，“只是向左跳了一下。”

- 索引 493

## 目录

- 1 引言 1
  - 你将从书中中学到 2
  - 本书是如何组织的 3
  - 支持 5
  - 致谢 5
  - 第四版前言 6
- 2 Objective-C 编程 7
  - 编译与运行程序 7
  - 使用 Xcode 8
  - 使用终端 17
  - 第一个程序的解释 19
  - 显示变量的值 23
  - 总结 25
  - 练习题 25
- 3 类、对象与方法 27
  - 什么是对象？27
  - 实例与方法 28
  - 处理分数的 Objective-C 类 30
  - `@interface` 部分 33
  - 命名选择 34
  - 类方法与实例方法 35
  - `@implementation` 部分 37
  - 程序部分 39
  - 访问实例变量与数据封装 45
  - 总结 49
  - 练习题 49
- 4 数据类型与表达式 51
  - 数据类型与常量 51
  - `int` 类型 51
  - `float` 类型 52
  - `char` 类型 52
  - 修饰符：`long`, `long long`, `short`, `unsigned` 和 `signed` 53
  - `id` 类型 54
  - 算术表达式 55
  - 运算符优先级 55
  - 整数算术与一元减运算符
  - 取模运算符 60
  - 整数与浮点转换 61
  - 类型转换运算符 63
  - 赋值运算符 64
  - 计算器类 65
- 5 程序循环 71
  - `for` 语句 72
  - 输入 79
  - 嵌套 `for` 循环 81
  - `while` 语句 84
  - `do` 语句 88
  - `break` 90
  - `continue` 语句 90
  - 总结 91
  - 练习题 91
- 6 决策判断 93
  - `if` 语句 93
  - `if-else` 结构 98
  - 复合关系测试 100
  - 嵌套 `if` 语句 105
  - `switch` 语句 114
  - 布尔变量 117
  - 总结 122
  - 练习题 124
- 7 类的进阶 127
  - 接口与实现文件 127
  - 合成访问器 132
  - 使用点操作符的属性 134
  - 方法的多个参数 135
  - 扩展类 137
  - 局部变量 140
  - `static` 关键字 141
- 8 继承 151
  - 一切从根部开始 151
  - 寻找正确的方法 155
  - 添加新方法 156
  - 分配对象 160
  - `@class` 指令 161
  - 所有对象 165
  - 重写方法 169
  - 总结 171
  - 练习题 174
- 9 多态、动态类型与动态绑定 177
  - 同名、不同类 177
  - `id` 类型 180
  - 编译时与运行时检查 182
  - 动态绑定与 `id` 类型 184
  - 使用动态类型的参数和返回类型 185
  - 使用 `@try` 提问 189
  - 练习题 192
- 10 变量与数据类型的进阶 195
  - 初始化对象 195
  - 重温作用域 198
  - 控制实例变量的指令 198
  - 属性、合成访问器与实例变量进阶 200
  - 全局变量 200
  - 静态变量 202
  - 枚举数据类型 205
  - `typedef` 语句 208
  - 类型转换 209
  - 转换规则 210
  - 位运算符 211
  - 位与运算符 212
  - 位包含或运算符 213
  - 位异或运算符 214
  - 位取反运算符 214
  - 左移运算符 216
  - 右移运算符 216
- 11 分类与协议 219
  - 分类 219
  - 类扩展 224
  - 关于分类的注意事项 225
  - 协议与委托 226
  - 委托 229
  - 非正式协议 229
  - 复合对象 230
  - 练习题 231
- 12 预处理器 233
  - `#define` 语句 233
  - 高级定义类型 235
  - `#import` 语句 240
  - 条件编译 241
  - `#ifdef`, `#endif`, `#else` 241
  - `#if` 和 `#elif` 预处理器语句 `undefined` 241
  - `#undef` 语句 244
  - 练习题 245
- 13 底层 C 语言特性 247
  - 函数 247
  - 数组 252
  - 结构 258
  - 指针 263
  - 块 270
  - 练习题 275
- 14 Foundation 框架简介 277
  - Foundation 框架 277
  - 使用文档 279
  - 练习题 281
- 15 数字与字符串对象 283
  - 数字对象 283
  - 字符串对象 288
  - 练习题 295
- 16 集合 297
  - 数组 297
  - 字典 304
  - 集合 308
  - 练习题 311
- 17 文件系统 313
  - `NSFileManager` 313
  - `NSFileHandle` 317
  - `NSProcessInfo` 320
  - 练习题 322
- 18 对象拷贝 413
  - 拷贝的 `copy` 方法 413
  - 浅拷贝与深拷贝 416
  - 实现 `<Copying>` 协议 418
  - Setter 与 Getter 方法 421
  - 练习题 423
- 19 归化 425
  - 使用属性列表 (PropertyList) 归化 425
  - 使用 `NSKeyedArchiver` 归化 427
  - 编码与解码方法 429
  - 使用 `NSData` 创建自定义归化 436
  - 使用 Archiver 对象 439
  - 练习题 441
- 20 Cocoa 与 Cocoa Touch 443
  - 框架层 443
  - Cocoa Touch 444
- 21 编写 iOS 应用 447
  - iOS SDK 447
  - 你的第一个 iPhone 应用 447
  - 创建一个新的 iPhone 应用 449
  - 进入你的代码 452
  - 设计界面 455
  - 一个 iPhone 应用 461
  - 定义 ViewController 464
  - Cocoa 类 469
  - 处理界面的 iPhone 类 473
  - 设计 UI 474
  - 总结 475
  - 练习题 476
- 术语表 479
- 通讯录示例代码 487
- 索引 493

## 关于作者

Stephen Kochan 是多本 C 语言畅销书籍的作者或合著者，包括《Programming in C》(Sams, 2004)、《Programming in ANSI C》(Sams, 1994) 和《Topics in C》(Wiley, 1991)，以及其他书籍如《Exploring the Unix System》(Sams, 1992) 和《Unix Shell Programming》(Sams, 2003)。自 1984 年第一台 Mac 发布以来，他一直在 Mac 上进行编程，并作为 Apple Press Library 的一部分编写了《Programming C for the Mac》。2003 年，Kochan 编写了《Programming in Objective-C》(Sams, 2003)，随后推出了另一本关于 Mac 的书籍《BeginningScript》(Wiley, 2004)。

## 关于技术审查

Wendy Mui 是旧金山地区的程序员和软件开发经理。在通过 Steve Kochan 书籍第二版学习 Objective-C 后，她加入了 Bump Technologies，在那里利用客户端应用和 API/SDK 为第三方开发者发挥她的编程技巧。

在接触 iOS 之前，Wendy 曾在硅谷和旧金山的其他许多科技公司度过成长期。她在加州大学伯克利分校攻读数学学位期间对编程产生了浓厚兴趣。工作之余，Wendy 正在练习四段跆拳道。

Michael Trent 自 1997 年起就开始编写 Objective-C——在此之前就开始编写 Mac 了。他是 Steven Frank 网站 cooadev.com 的常驻贡献者，是许多书籍和杂志的技术审查员，并偶尔参与 Mac OS 开源项目。目前，他正使用 Objective-C 和 Apple 的 Cocoa 框架为 Mac OS X 构建专业的视频应用。Michael 拥有计算机科学学士学位和音乐学士学位，他住在加利福尼亚州圣克拉拉。

# 第1章 引言

iPhone 于 2007 年发布，开发者们竞相渴望为这台革命性的设备开发应用程序。起初，Apple 并不欢迎第三方应用程序开发。公司安抚渴望成为 iPhone 开发者的方法是允许他们开发基于 Web 的应用程序。Web 应用程序在 iPhone 内置的 Safari 浏览器中运行，需要用户连接到托管应用程序的网站才能运行。开发者对 Web 应用程序的许多固有局限性并不满意，Apple 随后宣布开发者将能够为 iPhone 开发所谓的原生应用程序（native applications）。

原生应用程序驻留在 iPhone 的操作系统中，就像 iPhone 内置应用程序（如联系人、股票和天气）运行在设备上运行一样。iPhone 的操作系统实际上是 Mac OS X 的一个版本，这意味着可以在 Mac Pro 上对应用程序进行开发和调试。事实上，Apple 很快发布了一个功能强大的软件开发工具包（SDK），允许快速进行 iPhone 应用程序的开发和调试。iPhone 模拟器的出现使得开发者可以直接在自己的开发系统上调试应用程序，而避免了在实际 iPhone 或 iPad touch 设备上下载和测试程序的需要。

随着 2010 年 iPad 的推出，Apple 开始泛化用于操作系统和 SDK 的术语，以支持具有不同物理尺寸和屏幕分辨率的不同设备。iOS SDK 允许我们为任何 iOS 设备开发应用程序，截至本书时，iOS 5 是该操作系统的当前版本。

## 你将从书中学到什么

当我考虑写一本关于 Objective-C 的教程时，我必须要做一个基础性的决定。在其他关于 Objective-C 的书籍中，我可以把书设定为读者已经知道如何编写 C 语言。我也可以从使用其丰富的例程库（例如 Foundation 和 UIKit 框架）的角度来教授这门语言。有些书籍还采取了如何使用开发工具的方法，例如 Mac 的 Xcode 和以前被称为 Interface Builder 的工具来设计 UI。

在采用这种方法时，我遇到了几个问题。首先，在学习 Objective-C 之前学习整个 C 语言是错误的。C 是一种过程化语言，包含许多在 Objective-C 编程中并非必要的特性，特别是在初学者阶段。诉诸于这些某些特性违背了遵循良好的面向对象编程模式的初衷。在学习面向对象的语言之前先学习过程化语言的所有细节并不是一个好主意。这会让程序员从错误的方向开始，并为培养面向对象编程风格提供错误的引导和心态。仅仅因为 Objective-C 是 C 语言的扩展，并不意味着你必须先学 C。

## 本书的结构

因此，我决定不先教 C，也不假设具备该语言的先知识。相反，我决定采取一种非传统的方法，从面向对象编程的角度，将 Objective-C 和底层 C 语言作为一种单一的集成语言来教授。本书的目的正如其名所示：教你如何使用 Objective-C 进行编程。它并没有详细教你如何开发用于输入和调试程序的工具，也没有提供关于如何开发交互式图形应用程序的深度指导。在你学会了如何用 Objective-C 编写程序之后，你可以在其他地方详细学习所有这些。事实上，当你拥有了坚实的 Objective-C 编程基础时，掌握这些将会容易得多。如果你有以前的经验，本书并不假设任何前提。事实上，如果你是一个初级程序员，只要通过奉献和努力，你就应该能够学习 Objective-C 作为你的第一门编程语言。根据我收到的对本书预览的反馈，其他读者在这方面已经取得了成功。

本书通过示例来讲解 Objective-C。当我介绍语言的每一项新特性时，我通常会提供一个小型程序示例来阐明该特性。正如画画胜千言一样，选择恰当的示例也是如此。强烈鼓励你运行每个程序（所有程序在网上均可用），并将你系统上获得的结果与书中显示的进行进行比较。通过这种方式，你不仅将学习这门语言及其语法，还将熟悉编译和运行 Objective-C 程序的过程。

本书分为三个逻辑分部分。第一部分“Objective-C 语言”教授该语言的基础知识。第二部分“Foundation 框架”教授如何使用构成 Foundation 框架的丰富预定义类。第三部分“Cocoa、Cocoa Touch 和 iOS SDK（Cocoa, Cocoa Touch, and the iOS SDK）”将为你提供 Cocoa 和 Touch 框架的概述，然后带你完成使用 SDK 开发简单 iOS 应用程序的过程。

框架（Framework）是一组逻辑上组合的类和例程，使得程序开发变得更容易。Objective-C 的大部分编程都基于可用的框架。

第 2 章“用 Objective-C 编程”从教你如何用 Objective-C 编写第一个程序开始。因为这不属于 Cocoa 或 iOS 编程，所以图形用户界面（GUI）没有被广泛教授，在第三部分之前几乎从未被提及。因此，使用了一种向程序输入并产生输出的方法。书中的大多数示例从键盘获取输入并在窗格中产生输出：如果你使用命令行，则是 Terminal 窗口；如果你使用 Xcode，则是调试输出面板。

第 3 章“类、对象和方法（Classes, Objects, and Methods）”涵盖了面向对象编程的基础。本章引入了一些术语，但保持在最低限；我引入了定义类的机制以及向实例或对象发送消息的方法。导师和资深 Objective-C 程序员会注意到，我使用静态类型来声明对象，以便编译器捕获更多错误，使程序更具自文档性。由于这种方法，`id` 类型和威力直到第 9 章“多态、动态类型和动态绑定（Polymorphism, Dynamic Typing, and Dynamic Binding）”才会被充分探讨。

第 4 章“数据类型和表达式（Data Types and Expressions）”描述了 Objective-C 的基础数据类型以及如何在程序中使用它们。

第 5 章“循环（Program Logging）”引入了你在程序中使用的三种循环语句：`for`、`while` 和 `do`。逻辑判断是任何计算机语言的基础。第 6 章“逻辑判断（Making Decisions）”详细介绍了 Objective-C 语言的 `if` 和 `switch` 语句。第 7 章“关于类（On Classes）”深入探讨了类和对象的使用。本章介绍了方法、方法的多个参数以及局部变量。

第 8 章“继承（Inheritance）”引入了继承的概念。这一特性使得程序开发变得更容易，因为你可以利用上述许多情况。继承和子类的概念使得修改类定义变得更容易。

第 9 章讨论了 Objective-C 语言的三个基本特性。多态、动态类型和动态绑定是本章涵盖的概念。10-13 章完成了对 Objective-C 语言的讨论，涵盖了初始化对象、块、协议、分类、预处理器和指针等问题。底层的 C 特性（包括函数、数组、结构）在开发面向对象的应用时通常是非必要的（通常也是最好的）。建议在第一次阅读本书时学习第 13 章“底层 C 语言特性（Underlying C Language Features）”，仅在需要进一步了解语言的特定特性时返回查看。13 章还引入了 C 语言的一项最新新增，即块（blocks）。这将让你了解如何编写函数，后者的语法源于前者。

第二部分从第 14 章“Foundation 框架简介（Introduction to the Foundation Framework）”开始，该章节介绍了 Foundation 框架以及如何使用其大量的文档。

15-19 章涵盖了 Foundation 框架的重要特性。这些包括数字和字符串对象、集合、文件系统、内存管理以及对象的复制和存档过程。

当你完成第二部分时，你将能够使用 Foundation 框架开发相当复杂的 Objective-C 程序。

第三部分从第 20 章“Cocoa 和 Cocoa Touch 简介（Introduction to Cocoa and Cocoa Touch）”开始。在这里，你将获得用于在 Mac 和你的 iOS 设备上开发复杂的图形应用程序所需的框架的快速概述。

第 21 章“编写 iOS 应用程序”介绍了 iOS SDK 和 UIKit 框架。本章将阐述编写简单 iOS 应用程序的逐步方法，随后将是一个更复杂的计算器应用程序，该程序允许你使用 iPhone 进行分数的算术计算。



由于面向对象的编程术语涉及大量的术语，附录 A“术语表”提供了一些常用术语的定义。

附录 B“通讯录示例源代码”提供了两个类的源代码，这两个类在本书的第二部分被广泛开发和使用。类定义了地址卡和通讯录。方法允许你执行各种操作，如从通讯录中添加和删除地址卡、查找某人、列出通讯录内容等。

在学习了如何编写 Objective-C 程序之后，你可以向几个方向继续发展。你可能想学习底层的 C 编程语言——或者你可能想开始编写运行在 `Mac OS X` 上的 Cocoa 程序，或者开发更复杂的 iOS 应用程序。

如果你访问 `classroomM.com/objective-c`，你会发现一个内容丰富的论坛。你可以在那里获得源代码（你将找不到所有示例的“官方”源代码，因为我坚信学习的很大程度上发生在手动输入程序示例并学习如何识别和纠正错误的过程中）、练习题答案、勘误表、测验以及向我和论坛成员提问。该论坛已变成了一个由活跃成员组成的丰富社区，他们乐意帮助其他成员解决问题并回答问题。请光临、加入并参与进来吧！

我要感谢几位在准备本书第一版期间提供帮助的人员。首先，我要感谢 Tony Iannino 和 Steven Levy 审阅手稿。我很感谢 Mike Gaines 提供的意见。

我还想感谢我的技术编辑 Jack Purdum（第一版）和 Mike Trent。我很幸运能让 Mike 审阅了本书的第一版。他为我写过的任何书中提供了最详尽的审阅。他不仅指出了弱点，还慷慨地提供了自己的建议。根据 Mike 在第一版中的评论，我改变了教授内存管理的方法，并试图确保书中的每一个程序示例都是“无泄漏”的。这在第四版之前，而随着 ARC 的引入，对内存管理的强强调已变得过时了。Mike 还为我的 iPhone 编程章节提供了无价的建议。

从第一版开始，Catherine Babin 提供了封面照片，并为我提供了许多精美的图片供选择。朋友提供的封面艺术让这本书变得更加特别。

我非常感谢 Pearson 的 Mark Tabor（感谢所有版本），他忍受了所有的延迟，并友善地配合我的时间安排工作，并容忍我错过截止日期。我非常感谢 De Haan 和 Wendy Mui，他们对第二版进行了不可思议的、自发的校对（同时也感谢 Wendy 在第三版中的工作）。他们对细节的细致入微关注导致了一份既有排版错误也有实质性错误的列表，这些错误在第二次印刷中得到了解决。出版者注：这两双眼睛是无价的！

正如引言开头提到的，丹尼斯·里奇（Dennis Ritchie）发明了 C 语言。他还是 Unix 操作系统的共同发明者，这是 `Mac OS X` 和 iOS 的基础。遗憾的是，世界在短短一周内同时失去了丹尼斯·里奇和 Steve Jobs。本书的第三版已经写完成，那是两个对我的职业产生了深远影响的人物。毋庸说，如果没有他们，这本书就不会存在。

最后，我想感谢 `classroomM.com/objective-c` 论坛的成员，感谢他们所有的反馈、支持和鼓励的话。

# 第四版序言

当我 2011 年 6 月参加苹果的全球开发者大会（WWDC）时，我感到非常惊喜。第三版原定于几周后发布。在 2011 年的 WWDC 上，苹果推出了 ARC（自动引用计数）。在 ARC 之前，开发者需要手动管理对象的生命周期。由于 ARC 的引入，我们不再需要考虑这些问题。Mike 还为我的 iPhone 编程章节提供了无价的意见。

第 21 章“编写 iOS 应用程序”介绍了 iOS SDK 和 UIKit 框架。本章将阐述编写简单 iOS 应用程序的逐步方法，随后将是一个更复杂的计算器应用程序，该程序允许你使用 iPhone 进行分数的算术计算。

# 第 1 章 引言

从第一版开始，Catherine Babin 提供了封面照片，并为我提供了许多精美的图片供选择。朋友提供的封面艺术让这本书变得更加特别。

我非常感谢 Pearson 的 Mark Tabor（感谢所有版本），他忍受了所有的延迟，并友善地配合我的时间安排工作，并容忍我错过截止日期。我非常感谢 De Haan 和 Wendy Mui，他们对第二版进行了不可思议的、自发的校对（同时也感谢 Wendy 在第三版中的工作）。他们对细节的细致入微关注导致了一份既有排版错误也有实质性错误的列表，这些错误在第二次印刷中得到了解决。出版者注：这两双眼睛是无价的！

正如引言开头提到的，丹尼斯·里奇（Dennis Ritchie）发明了 C 语言。他还是 Unix 操作系统的共同发明者，这是 `Mac OS X` 和 iOS 的基础。遗憾的是，世界在短短一周内同时失去了丹尼斯·里奇和 Steve Jobs。本书的第三版已经写完成，那是两个对我的职业产生了深远影响的人物。毋庸说，如果没有他们，这本书就不会存在。

最后，我想感谢 `classroomM.com/objective-c` 论坛的成员，感谢他们所有的反馈、支持和鼓励的话。

# 第 2 章 编译和运行程序

在左侧窗格中，你会看到一个标记为 `Mac OS X` 的部分。选择 `Application`。在右上窗格中，选择 `Command Line Tool`，如上一图所示。在接后出现的窗格中，选择你的应用程序名称。在 `Product Name`（产品名称）处输入 `prog1`，并确保 `Type`（类型）选了 `Foundation`。此外，确保勾选了 `Use Automatic Reference Counting`（使用自动引用计数）。你的屏幕应该像图 2.4 所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_26_0.png)

图 2.4 启动一个新项目：指定产品名称和类型

点击 `Next`（下一步）。出现的下拉菜单允许你指定包含与项目相关文件的项目文件夹的名称。在这里，你还可以指定你想要存储项目文件夹的位置。根据图 2.5，我们将把项目存储在桌面（Desktop）上一个名为 `prog1` 的文件夹中。

![](img/22d1310b7c22ea2d48cd2058929a5cda_27_0.png)

图 2.5 选择项目文件夹的位置和名称

点击 `Create`（创建）按钮创建你的新项目。Xcode 将打开一个类似于图 2.6 所示的窗口。注意，如果你以前用过 Xcode 或更改过它的任何选项，你的窗口可能会看起来不同。

![](img/22d1310b7c22ea2d48cd2058929a5cda_28_0.png)

图 2.6 Xcode prog1 项目窗口

## 编译和运行程序

现在是输入你的第一个程序了。在左侧窗格中选择文件 `main.m`（你可能需要点击展开三角形来显示位于项目名称下的文件）。你的 Xcode 窗口现在应该如图 2.7 所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_29_0.png)

图 2.7 文件 main.m 和编辑窗口

Objective-C 源文件使用 `.m` 作为文件名的最后两个字符（称为扩展名）。表 2.1 列出了其他常用的文件名扩展名。

### 表 2.1 常见文件名扩展名

| 扩展名 | 含义 |
| --- | --- |
| `.c` | C 语言源文件 |
| `.cc`, `.cpp` | C++ 语言源文件 |
| `.h` | 头文件 |
| `.m` | Objective-C 源文件 |
| `.mm` | Objective-C++ 源文件 |
| `.pl` | Perl 源文件 |
| `.o` | 对象（编译后）文件 |

回到你的 Xcode 项目窗口，右侧窗格显示名为 `main.m` 的文件的内容，该文件由 Xcode 作为模板文件自动为你创建，包含以下行：

```objc
// main.m
// prog1
//
// Created by Steven Koch on 7/7/11.
// Copyright 2011 ClassroomRoom, Inc.. All rights reserved.
//import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool (
        // insert code here...
        NSLog("*Hello World!");
    )
    return 0;
}
```

你可以在此窗口内编辑你的文件。对 Edit（编辑）窗口中显示的程序进行修改以制作程序 2.1。以两个斜杠字符（`//`）开头的行是注释；你在编辑窗口中的程序现在应该像这样（不用担心你的注释是否匹配）。

### 程序 2.1

```objc
// 第一个程序示例

#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSLog("Programming is fun!");

        return 0;
    }
}
```

### 注意事项

不要担心屏幕上为文本显示的所有颜色。Xcode 用不同的颜色表示值、保留字等。当你开始编写更多程序时，这将被证明是非常有用的，因为它可以指示潜在错误的来源。

现在是编译并运行你的第一个程序了——在 Xcode 术语中，这被称为 `building`（构建）和 `running`（运行）。在此之前，我们需要显示一个显示程序结果（输出）的窗格。你可以通过选择 `View`（视图）下的菜单项来实现。当你悬停在此图标上时，它会显示“Hide or show the Debug area（隐藏或显示调试区域）”。你的窗口现在应该如图 2.8 所示。每当向其中写入数据时，Xcode 通常显示调试区域。

![](img/22d1310b7c22ea2d48cd2058929a5cda_31_0.png)

图 2.8 显示 Xcode 调试区域

现在，如果你按下工具栏左上角的 `Run`（运行）按钮，或者从 `Product`（产品）菜单中选择 `Run`，Xcode 将通过两步过程：首先构建然后运行你的程序。后者只有在你的程序中没有发现错误时才会发生。

如果你在程序中犯了错误，你看到的错误标记为带有感叹号的红色停止——这些被称为致命错误（fatal errors），在修正这些错误之前你无法运行程序。`Warnings`（警告）由带有感叹号的黄色三角形表示——你仍然可以运行程序，但通常情况下你应该检查并修正它们。在带有所有警告的情况下运行程序后，你看到的输出如图 2.9 所示。

```
All Output:
```



```
// main.m
// prog1
//
// Created by Steven Koch on 7/7/11.
// Copyright 2011 ClassroomRoom, Inc.. All rights reserved.
//import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool (
        // insert code here...
        NSLog("*Hello World!");
    )
    return 0;
}
```

你可以在此窗口内编辑你的文件。对 Edit 窗口中显示的程序进行修改以制作程序 2.1。以两个斜杠字符（`//`）开头的行是注释；你在编辑窗口中的程序现在应该像这样（不用担心你的注释是否匹配）。

### 程序 2.1

// 第一个程序示例

```
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
```

```
@autoreleasepool {
    NSLog("Programming is fun!");

    return 0;
}
```

### 注意事项

不要担心屏幕上为文本显示的所有颜色。Xcode 用不同的颜色表示值、保留字等。当你开始编写更多程序时，这将被证明是非常有用的，因为它可以指示潜在错误的来源。

现在是编译并运行你的第一个程序了——在 Xcode 术语中，这被称为 building（构建）和 running（运行）。在此之前，我们需要显示一个将显示程序结果（输出）的窗格。你可以通过选择 View 下的菜单项来实现。当你悬停在此图标上时，它会显示“Hide or show the Debug area（隐藏或显示调试区域）”。你的窗口现在应该如图 2.8 所示。每当向其中写入数据时，Xcode 通常会自动显示调试区域。

![](img/22d1310b7c22ea2d48cd2058929a5cda_31_0.png)

图 2.8 Xcode 调试区域显示

现在，如果你按下工具栏左上角的 Run 按钮，或者从 Product 菜单中选择 Run，Xcode 将通过两步过程：首先构建然后运行你的程序。后者只有在你的程序中没有发现错误时才会发生。

如果你在程序中犯了错误，你看到的错误标记为带有感叹号的红色停止符号——这些被称为致命错误，在修正这些错误之前你无法运行程序。`Warnings`（警告）由带有感叹号的黄色三角形表示——你仍然可以运行程序，但通常情况下你应该检查并修正它们。在带有所有警告的情况下运行程序后，你看到的输出如图 2.9 所示。

```
All Output:
```

（注：由于提供的原文在末尾出现重复且截断，此处翻译基于提供的文本片段进行结束。）

# 你的第一个程序的详解

将你的程序存储（或简单地使用当前目录）添加到 shell 的 `PATH` 变量中。让我们采用第一种方法：

```
$ ./prog1 Execute prog1
2008-06-08 18:48:44.210 prog1[7985:10b] Programming is fun!
$
```

你应该注意，从终端编写和调试 Objective-C 程序是一种有效的方法。然而，这不是一个良好的长期策略。如果你想构建 Mac OS X 或 iOS 应用程序，仅仅执行可执行文件是不够的，它们需要被“打包”成一个应用程序包（application bundle）。在 Terminal 应用程序中完成这一点并不容易，这是 Xcode 的专长之一。因此，我建议开始学习使用 Xcode 来开发你的程序。这其中有一个学习曲线，但这些付出将是非常值得的。

# 你的第一个程序的详解

既然你已经熟悉了编译和运行 Objective-C 程序所涉及的步骤，让我们仔细观察这第一个程序。这里再次给出它：

```objc
// main.m
// prog1
//
// Created by Steve Kochan on 7/7/11.
// Copyright 2011 ClassroomM, Inc.. All rights reserved.
//
```

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {

    NSLog(@"Programming is fun!");

    return 0;
}
```

在 Objective-C 中，小写字母和大写字母是不同的。此外，Objective-C 并不在乎你在行的哪个位置开始输入——你可以在行的任何位置开始你的语句。你可以利用这一点来开发出更易读的程序。

程序的开头几行引入了注释（comment）的概念。注释语句在程序中用于记录程序说明并增强其可读性。注释告诉程序的读者——无论是程序员还是其他人谁负责维护该程序的责任——仅仅是程序员在编写特定程序或特定语句序列时脑海中的考虑内容。

你可以通过两种方式在 Objective-C 程序中插入注释。一种是使用两个连续的斜杠（`//`）。编译器会忽略这些斜杠之后直到行尾的任何字符。

你也可以用这两个字符和 `/*` 开始注释。这种注释标记了注释的开始。这类类型的注释必须结束。要结束注释，你使用字符和 `*/` 且不包含任何嵌入的空格。包括起始的 `/*` 和结束的 `*/` 在内的所有字符都被视为注释语句的一部分，并被 Objective-C 编译器忽略。这种形式的注释通常用于注释多行代码，如下例所示：

```objc
/*
此文件实现了一个名为 Fraction 的类，
表示分数。方法允许对分数
进行操作，例如加法、减法等。
*/
```

如需获取更多信息，请参阅文档：

`/usr/docs/classes/fractions.pdf`

```objc
/*
```

你使用哪种风格的注释完全取决于你。只需注意你不能嵌套这种风格的注释。

养成在编写程序或输入计算机时在程序中插入注释的习惯，有三个原因。首先，在程序逻辑仍然留在脑海中时记录程序，比在程序完成后回去重新思考逻辑要容易得多。其次，通过在程序调试阶段插入注释，你可以在帮助你（以及他人）阅读逻辑错误被隔离和调试期间，从注释中获益。但它也有助于指向逻辑的源头。最后，我从未发现过哪个真正喜欢记录程序的程序员。事实上，在你完成程序调试后，你可能会放弃回到程序中插入注释的念头。在开发程序时插入注释会让这个有时枯燥的任务变得稍微容易处理一些。

程序 2.1 中的这一行告诉编译器定位并处理一个名为 `Foundation.h` 的文件。

```objc
#import <Foundation/Foundation.h>
```

这是一个系统文件——也就是说，它不是你创建的文件。`#import` 表示将该文件中的信息包含到程序中，就像该文件的内容在这一点被直接输入到程序中一样。你导入 `Foundation.h` 文件是因为它包含了程序中所使用的其他类和函数的信息。

在程序 2.1 中，这一行指定了程序的名称为：

```objc
int main (int argc, const char * argv())
```

`main` 是一个特殊名称，精确指示了程序从哪里开始执行。在 `main` 之前的保留字 `int` 指定了返回值的类型，

# 你的第一个程序的详解

即一个整数（很快就会关于它的更多介绍）。我们现在忽略左括号和右括号之间的内容；这些与命令行参数有关。

现在你已经向系统标识了 `main`，准备好精确指定此例程要执行的操作。这是通过将例程中的所有程序语句封装在一对括号内完成。在最简单的情况下，语句就是一个以分号终止的表达式。系统将包含在括号之间的所有程序语句视为 `main` 例程的一部分。

`main` 中的该行读取为

```objc
@autoreleasepool {
```

在 `{` 和匹配的结束 `}` 之间的任何程序语句都在一个名为 autoreleasepool（自动释放池）的范围内执行。自动释放池是一种允许系统在创建新对象时高效管理应用程序所使用的内存的机制。详细信息请见第 1 章。

# 显示变量的值

```
#import <Foundation/Foundation.h>

int main (int argc, const char *argv[]){
    @autoreleasepool {
        NSLog(@"Testing...\n...1\n...2\n...3");
    }
    return 0;
}
```

## 程序 2.3 输出

Testing...

1

...2

...3

# 显示变量的值

`NSLog` 不仅可以显示简单的语句，还可以显示变量的值和计算结果。程序 2.4 使用 `NSLog` 例程来显示两个数字 50 和 25 相加的结果。

```
#import <Foundation/Foundation.h>

int main (int argc, const char *argv[]){
    @autoreleasepool {
        int sum;
        sum = 50 + 25;
        NSLog(@"The sum of 50 and 25 is %i", sum);
    }
    return 0;
}
```

### 程序 2.4 输出

The sum of 50 and 25 is 75

在设置好自动释放池之后，`main` 函数内部的第一个程序语句定义了类型为整数变量 `sum`。在程序中使用变量之前，必须定义所有的程序变量。

变量的定义告诉 Objective-C 编译器程序应该如何使用它。编译器需要这些信息来生成正确的指令，以便在变量中存储和从中检索值。定义为 `int` 类型的变量只能存储整数值——即没有小数位的值。整数值的示例有 3、5、-20 和 0。带有小数的数字（如 2.14、2.455 和 27.0）被称为浮点数，它们是实数。

整数变量 `sum` 在定义了两个整数 50 和 25 之后，特意留了一个空行。我们在视觉上将变量的声明与程序语句隔离开来；这完全是一个风格问题。有时在程序中添加单行空行可以提高程序的可读性。

程序语句的读取方式与大多数其他编程语言一样：

```
sum = 50 + 25;
```

数字 50 被（如加号所示）加到变量 25 上，结果被（如赋值运算符等号所示）存储在变量 `sum` 中。程序 2.4 中的 `NSLog` 调用现在有两个封装在括号内的参数。注释中的第一个参数和后续参数用逗号隔开。`NSLog` 例程允许显示字符串。然而，你通常也希望显示某些程序变量的值。在这种情况下，你希望在显示完这些字符后显示变量 `sum` 的值：

The sum of 50 and 25 is

第一个括号内的第一个字符是 `NSLog` 函数识别的特殊字符。紧跟在百分号（`%`）之后的字符指定了在该位点处要显示什么种类型的值。在上一个程序中，`NSLog` 例程识别出字母 `i` 表示要显示一个整数值。

每当 `NSLog` 在字符字符串中找到 `%i` 字符时，它会自动显示传递给例程的下一个参数的值。由于 `sum` 是 `NSLog` 的下一个参数，因此它的值会自动显示在 "The sum of 50 and 25 is" 之后。现在尝试预测程序 2.5 的输出。

```
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {

    @autoreleasepool {
        int value1 = 50;
        int value2 = 25;
        int sum = value1 + value2;
        NSLog(@"The sum of %i and %i is %i", value1, value2, sum);
    }
  return 0;
}
```

## 程序 2.5 输出

The sum of 50 and 25 is 75

`main` 函数内部的第二个程序语句定义了三个名为 `value1`、`value2` 和 `sum` 的变量，类型均为 `int`。该语句也可以使用三个独立的语句等价表示如下：

```
int value1;
int value2;
int sum;
```

在定义了三个变量后，程序将值 50 赋值给变量 `value1`，将 25 赋值给 `value2`。计算这两个变量之和并将结果赋值给变量 `sum`。

现在对 `NSLog` 例程的调用包含四个参数。再次，第一个参数（通常称为格式字符串）向系统描述如何显示剩余参数。`value1` 的值将紧随在短语“The sum of.”之后。同样，`value2` 和 `sum` 的值将打印在格式字符串中下一次出现 `%` 字符的地方。

# 总结

在读完这章关于使用 Objective-C 开发程序的介绍性章节后，你应该对在 Objective-C 中编写程序涉及的内容有良好的理解——你应该能够独立开发一个小型程序。在下一章中，你将开始探索这种强大且灵活的编程语言的一些复杂之处。但首先，请尝试随后的练习，以确保你理解了本章介绍的概念。

## 练习

- 1. 输入并运行本章中提供的五个程序。将每个程序产生的输出与每个程序后给出的输出进行比较。

- 2. 写一个程序显示以下文本：

   在 Objective-C 中，字母的大小写是敏感的。

   `main` 是程序执行的地方。

   大括号包围例程中的程序语句。

   所有的程序语句必须以分号结束。

# 第 2 章 Objective-C 编程

- 3. 你预期的以下程序的输出是什么？

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])

{

  @autoreleasepool {

    int i;

    i = 1;

    NSLog(@"...%i");

    NSLog(@"...%i", i);

    NSLog(@"...%i", i + 2);

  }

  return 0;

}
```

- 4. 写一个程序，从 87 中减去 15 并显示结果，以及相应的消息。

- 5. 识别以下程序的语法错误。输入并运行修正后的程序，以确保你识别了所有的错误：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char *argv[])

{

  @autoreleasepool {

    int sum;

    sum = 25 + 37;

    NSLog(@"The answer is %i", sum);

  }

  return 0;

}
```

- 6. 你预期的以下程序的输出是什么？

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])

{

  @autoreleasepool {

    int answer, result;

    answer = 100;

    result = answer - 10;

    NSLog(@"The result is %i\n", result + 5);

  }

  return 0;

}
```

# 表 3.1 对对象的操作

| 对象 | 你对它进行的操作 |
| --- | --- |
| 你的汽车 | 驾驶它、加油、洗车、保养 |

表 3.1 中列出的操作可以对你的汽车进行，也可以对其他汽车进行。例如，你姐姐会开她的车、洗洗车、加油等等。

## 实例与方法

类的唯一出现情况被称为**实例**（instance），而对实例上执行的操作被称为*方法*（methods）。在某些情况下，方法既可以应用于类的某个实例，也可以应用于类本身。例如，“洗你的车”适用于一个实例（事实上，上文，表 3.1 中列出的所有方法都可以被视为实例方法）。而查找制造商会应用到该类的汽车类型，那么它就是一个类方法（class method）。

假设你有两辆从装配线上出来且看起来一模一样的汽车：它们具有相同的内饰、相同的漆色等。它们刚开始时轮胎可能是相同的，但随着每辆车被各自的所有者使用，其独特的特征或属性就会发生变化。例如，一辆车最后可能有一道划痕，而另一辆车的行驶里程可能更多。每个实例或对象不仅包含了从工厂获取的关于属性的信息，还包含了它的特征。这些特征可以动态地变化。当你开车时，油箱会耗尽，汽车会变脏，轮胎每次使用后都会变松一点点。

对对象应用方法可能会影响该对象的*状态*（state）。如果你的方法是“给我的汽车加油”，那么在执行该方法后，你汽车的油箱就是满的。这时该方法就影响了汽车的油箱。

核心概念是：对象是类的唯一表示，每个对象都包含某些信息（数据），这些数据通常对该对象是私有的。方法提供了访问和更改这些数据手段。

Objective-C 语言具有以下应用于类和实例的语法：

```
[ClassInstance method:];
```

在此语法中，左括号后面跟着一个类或该类的实例的名称，后面跟着一个或多个空格，然后是你想要执行的方法。最后，用右括号和分号结束。当你要求一个类或实例执行某些操作时，你说你是在向它发送一条消息（message）；消息的接收者被称为接收者（receiver）。因此，查看之前描述的通用格式的另一种方式如下：

`[ receiver message ];`

让我们回到之前的列表并用这种新语法写下所有内容。在此之前，你需要先获取你的新车。去工厂买它，如下所示：

```
yourCar = [Car new];      获取一辆新车
```



# 第 3 章 类、对象与方法

你向 `Car` 类（消息的接收者）发送一条消息，要求它给你一辆新车。生成的对象（代表你独特的汽车）随后被存储在变量 `yourCar` 中。从现在起，`yourCar` 可以用来引用你从工厂获取的汽车实例。

因为你去了工厂，所以这个方法被称为工厂方法或类方法。在你新车上的其他操作将是实例方法，因为它们适用于你的汽车。以下是你可能为你的汽车编写的一些示例消息表达式：

```
[yourCar prep];       // 为首次使用做准备
[yourCar drive];       // 驾驶你的汽车
[yourCar wash];        // 洗洗你的汽车
[yourCar getGas];      // 如果需要，给你的汽车加油
[yourCar service];     // 保养你的汽车
```

```
[yourCar topDown];   // 如果是敞篷车
[yourCar topUp];
currentMileage = [yourCar odometer];
```

这个示例显示了一个返回信息的实例方法——推测是里程表上的当前里程。我们在程序中存储了名为 `currentMileage` 的信息。

这里有一个方法接受参数的示例，该参数指定了一个特定的值，该值在不同方法的调用之间可能不同：

```
[yourCar setSpeed: 55]; // 将速度设置为 55 英里
```

你姐姐苏（Sue）可以为她自己的汽车实例使用相同的方法：

```
[sues drive];
[sues wash];
[sues getGas];
```

对不同的对象应用相同的方法是面向对象编程的核心概念之一，你将在以后学到更多内容。

你可能不需要在程序中处理汽车。你的对象将是面向计算机的事物，例如窗口、矩形、文本段，或者可能甚至是一个计算器或歌曲播放列表。就像你用于汽车的方法一样，你的方法可能看起来很相似，如下所示：

```
[myWindow erase];               // 清除窗口
theArea = [myRect area];        // 计算矩形的面积
[userText spellCheck];          // 对某些文本进行拼写检查
[deskCalculator clear];         // 清除上一次输入
[favoritePlaylist showSongs];   // 显示收藏播放列表中的歌曲
[phoneNumber dial];             // 拨打电话号码
[myTable reloadData];           // 显示更新后的数据
n = [aTouch tapCount];          // 存储显示被点击的次数
```

## 一个用于处理分数的 Objective-C 类

现在是时候在 Objective-C 中定义一个实际类，并学习如何处理该类的实例了。你将先学习过程。作为结果，实际的程序示例看起来可能并不实用。假设你需要处理分数，你可能会从这里开始：

```
int numerator, denominator;
numerator = 1;
denominator = 3;
```

在 3.1 中，分数通过整数分子和分母表示，并分别赋值为 1 和 3。如果你需要在程序中存储很多分数，这可能会很笨拙。如果可以将分数定义为一个单一实体，并用一个名称（如 `myFraction`）来引用它的分子和分母就好了。在 Objective-C 中可以这样做，它从定义一个新类开始。以下是程序，随后是其工作原理的详细解释。

## 程序 3.2

```
// 处理分数的程序 - 类版本
```

```objc
#import <Foundation/Foundation.h>

//--- 接口部分 (interface section) ---
@interface Fraction : NSObject
- (void) print;
- (void) setNumerator:(int) n;
- (void) setDenominator:(int) d;
@end

//--- 实现部分 (implementation section) ---
@implementation Fraction
{
    int numerator;
    int denominator;
}

- (void) print
{
    NSLog("%i/%i", numerator, denominator);
}

- (void) setNumerator:(int) n
{
    numerator = n;
}

- (void) setDenominator:(int) d
{
    denominator = d;
}
@end

int main(int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *myFraction;
        // 创建 Fraction 的实例
        myFraction = [Fraction alloc];
        myFraction = [myFraction init];
        // 设置分数为 1/3
        [myFraction setNumerator: 1];
        [myFraction setDenominator: 3];
        // 使用 print 方法显示分数
        NSLog(@"The value of myFraction is:");
        [myFraction print];
    }
    return 0;
}
```

## 程序 3.2 输出

```
The value of myFraction is:
1/3
```

## @interface 部分

如你从程序 3.2 的注释所示，该程序在逻辑上被分为三个部分：

- `@interface` 部分（接口部分）
- `@implementation` 部分（实现部分）
- `program` 部分（程序部分）

`@interface` 部分描述了类及其方法，而 `@implementation` 部分描述了数据（来自该类的对象将存储的实例变量），并包含了实现接口部分中声明的方法的实际代码。最后，`program` 部分包含了执行程序意图的程序代码。

> 注意：你也可以在接口部分中为类声明实例变量。在实现部分进行此项操作的功能是从 Xcode 4.2 开始添加的，并且被认为是定义类的更好方法。你将在后面的章节中学习更多关于其原因的知识。

这些每一个部分都是每个 Objective-C 程序的一部分，尽管你可能不需要自己编写每一个部分。正如你所看到的，每个部分通常被放在自己单独的文件中。不过，目前，我们将它们全部保存在同一个文件中。

### 选择名称

在第 2 章“Objective-C 编程”中，你使用了几个变量来存储整数值。例如，你在程序 2.4 中使用了变量 `sum` 来存储两个整数 50 和 25 相加的结果。

Objective-C 语言允许你在变量中使用除整数以外的数据类型，只要在程序中使用该变量之前对它进行了正确的声明即可。变量可以用于存储浮点数、字符，甚至是对象（指针，或者更准确地说，是对象的引用）。

命名的规则非常简单：它们必须以字母或下划线开头，后面可以跟任意字母（大小写）、下划线和数字 0–9 的组合。以下是有效名称列表：

- `sum`
- `pieceFlag`
- `i`
- `myLocation`
- `numberOfOfMoves`
- `sysFlag`
- `ChessBoard`

另一方面，由于上述原因，以下名称是无效的：

- `sumValue $`：`$` 不是有效字符。
- `piece flag`：不允许嵌入空格。
- `3Spencer`：名称不能以数字开头。
- `int`：这是一个关键字。

`int` 不能用作变量名，因为它的用法对 Objective-C 编译器有特殊含义。这种用法被称为保留名或保留字。通常，任何对 Objective-C 编译器具有特殊意义的名称都不能作为变量名。

始终记住，在 Objective-C 中，大写字母和小写字母是区分的。在那里，变量名 `sum`、`Sum`、`SUM` 分别指代不同的变量。正如所述，在命名类时，要用大写字母开头。另一方面，实例变量、对象和方法名通常以小写字母开头。为了可读性，名称内部使用大写字母来指示新单词的开头，如下例所示：

- `AddressBook`：这可能是一个类名。
- `currentEntry`：这可能是一个对象。
- `current_entry`：

## @interface 部分详解

当你定义一个新类时，你必须告诉 Objective-C 编译器该类源自何处。也就是说，你必须命名它的父类。接下来，你需要定义在处理来自此类的对象时可以使用的操作类型，或称为方法。正如你将在后面的章节中学到的，你还会在程序中这个名为 `@interface` 部分的特殊部分里列出被称为属性的项。该部分的通用格式如下：

```objc
@interface NewClassName: ParentClassName
propertyAndMethodDeclarations;
@end
```

按照惯例，类名以大写字母开头，尽管这不是强制要求的。这使得阅读你程序的人只需查看名称的第一个字符，就能将类名与其他类型的变量区分开来。



按照惯例，类名以大写字母开头，尽管这不是强制要求的。这使得阅读你程序的人只需查看名称的第一个字符，就能将类名与其他类型的变量区分开来。让我们稍微离开一下谈谈 Objective-C 中的命名规则。

### 选择名称

在第 2 章“Objective-C 编程”中，你使用了几个变量来存储整数值。例如，你在程序 2.4 中使用了变量 `sum` 来存储两个整数 50 和 25 相加的结果。

Objective-C 语言允许你在变量中使用除整数以外的数据类型，只要在程序中使用该变量之前对它进行了正确的声明即可。变量可以用于存储浮点数、字符，甚至是对象（指针，或者更准确地说，是对象的引用）。

命名的规则非常简单：它们必须以字母或下划线开头，后面可以跟任意字母（大小写）、下划线和数字 0–9 的组合。以下是有效名称列表：

- `sum`
- `pieceFlag`
- `i`
- `myLocation`
- `numberOfOfMoves`
- `sysFlag`
- `ChessBoard`

另一方面，由于上述原因，以下名称是无效的：

- `sumValue $`：`$` 不是有效字符。
- `piece flag`：不允许嵌入空格。
- `3Spencer`：名称不能以数字开头。
- `int`：这是一个关键字。

`int` 不能用作变量名，因为它的用法对 Objective-C 编译器有特殊含义。这种用法被称为保留名或保留字。通常，任何对 Objective-C 编译器具有特殊意义的名称都不能作为变量名。

始终记住，在 Objective-C 中，大写字母和小写字母是区分的。在那里，变量名 `sum`、`Sum`、`SUM` 分别指代不同的变量。正如所述，在命名类时，要用大写字母开头。另一方面，实例变量、对象和方法名通常以小写字母开头。为了可读性，名称内部使用大写字母来指示新单词的开头，如下例所示：

- `AddressBook`：这可能是一个类名。
- `currentEntry`：这可能是一个对象。
- `current_entry`：

## @interface 部分

如你从程序 3.2 的注释所示，该程序在逻辑上被分为三个部分：

- `@interface` 部分
- `@implementation` 部分
- `program` 部分

`@interface` 部分描述了类及其方法，而 `@implementation` 部分描述了数据（来自该类的对象将存储的*实例变量*），并包含了实现接口部分中声明的方法的实际代码。最后，`program` 部分包含了执行程序意图的程序代码。

> 注意：你也可以在接口部分中为类声明实例变量。在实现部分进行此项操作的功能是从 Xcode 4.2 开始添加的，并且被认为是定义类的更好方法。你将在后面的章节中学习更多关于其原因的知识。

这些每一个部分都是每个 Objective-C 程序的一部分，尽管你可能不需要自己编写每一个部分。正如你所看到的，每个部分通常被放在自己单独的文件中。不过，目前，我们将它们全部保存在同一个文件中。

## @interface 部分详解

当你定义一个新类时，你必须告诉 Objective-C 编译器该类源自何。也就是说，你必须命名它的*父类*。接下来，你需要定义在处理来自此类的对象时可以使用的操作类型，或称为*方法*。正如你将在后面的章节中学到的，你还会在程序中这个名为 `@interface` 部分的特殊部分里列出被称为*属性*的项。该部分的通用格式如下：

```objc
@interface NewClassName: ParentClassName

propertyAndMethodDeclarations;

@end
```



按照惯例，类名以大写字母开头，尽管这不是强制要求的。这使得阅读你程序的人只需查看名称的第一个字符，就能将类名与其他类型的变量区分开来。让我们稍微离开一下谈谈 Objective-C 中的命名规则。

### 选择名称

在第 2 章“Objective-C 编程”中，你使用了几个变量来存储整数值。例如，你在程序 2.4 中使用了变量 `sum` 来存储两个整数 50 和 25 相加的结果。

Objective-C 语言允许你在变量中使用除整数以外的数据类型，只要在程序中使用该变量之前对它进行了正确的声明即可。变量可以用于存储浮点数、字符，甚至是对象（指针，或者更准确地说，是对象的引用）。

命名的规则非常简单：它们必须以字母或下划线开头，后面可以跟任意字母（大小写）、下划线和数字 0–9 的组合。以下是有效名称列表：

- `sum`
- `pieceFlag`
- `i`
- `myLocation`
- `numberOfOfMoves`
- `sysFlag`
- `ChessBoard`

另一方面，由于上述原因，以下名称是无效的：

- `sumValue $`：`$` 不是有效字符。
- `piece flag`：不允许嵌入空格。
- `3Spencer`：名称不能以数字开头。
- `int`：这是一个关键字。

`int` 不能用作变量名，因为它的用法对 Objective-C 编译器有特殊含义。这种用法被称为保留名或保留字。通常，任何对 Objective-C 编译器具有特殊意义的名称都不能作为变量名。

始终记住，在 Objective-C 中，大写字母和小写字母是区分的。在那里，变量名 `sum`、`Sum`、`SUM` 分别指代不同的变量。正如所述，在命名类时，要用大写字母开头。另一方面，实例变量、对象和方法名通常以小写字母开头。为了可读性，名称内部使用大写字母来指示新单词的开头，如下例所示：

- `AddressBook`：这可能是一个类名。
- `currentEntry`：这可能是一个对象。
- `current_entry`：

## @interface 部分

如你从程序 3.2 的注释所示，该程序在逻辑上被分为三个部分：

- `@interface` 部分
- `@implementation` 部分
- `program` 部分

`@interface` 部分描述了类及其方法，而 `@implementation` 部分描述了数据（来自该类的对象将存储的*实例变量*），并包含了实现接口部分中声明的方法的实际代码。最后，`program` 部分包含了执行程序意图的程序代码。

> 注意：你也可以在接口部分中为类声明实例变量。在实现部分进行此项操作的功能是从 Xcode 4.2 开始添加的，并且被认为是定义类的更好方法。你将在后面的章节中学习更多关于其原因的知识。

这些每一个部分都是每个 Objective-C 程序的一部分，尽管你可能不需要自己编写每一个部分。正如你所看到的，每个部分通常被放在自己单独的文件中。不过，目前，我们将它们全部保存在同一个文件中。

## @interface 部分详解

当你定义一个新类时，你必须告诉 Objective-C 编译器该类源自何处。也就是说，你必须命名它的*父类*。接下来，你需要定义在处理来自此类的对象时可以使用的操作类型，或称为*方法*。正如你将在后面的章节中学到的，你还会在程序中这个名为 `@interface` 部分的特殊部分里列出被称为*属性*的项。该部分的通用格式如下：

```objc
@interface NewClassName: ParentClassName

propertyAndMethodDeclarations;

@end
```



按照惯例，类名以大写字母开头，尽管这不是强制要求的。这使得阅读你程序的人只需查看名称的第一个字符，就能将类名与其他类型的变量区分开来。让我们稍微离开一下谈谈 Objective-C 中的命名规则。

### 选择名称

在第 2 章“Objective-C 编程”中，你使用了几个变量来存储整数值。例如，你在程序 2.4 中使用了变量 `sum` 来存储两个整数 50 和 25 相加的结果。

Objective-C 语言允许你在变量中使用除整数以外的数据类型，只要在程序中使用该变量之前对它进行了正确的声明即可。变量可以用于存储浮点数、字符，甚至是对象（指针，或者更准确地说，是对象的引用）。

命名的规则非常简单：它们必须以字母或下划线开头，后面可以跟任意字母（大小写）、下划线和数字 0–9 的组合。以下是有效名称列表：

- `sum`
- `pieceFlag`
- `i`
- `myLocation`
- `numberOfOfMoves`
- `sysFlag`
- `ChessBoard`

另一方面，由于上述原因，以下名称是无效的：

- `sumValue $`：`$` 不是有效字符。
- `piece flag`：不允许嵌入空格。
- `3Spencer`：名称不能以数字开头。
- `int`：这是一个关键字。

`int` 不能用作变量名，因为它的用法对 Objective-C 编译器有特殊含义。这种用法被称为保留名或保留字。通常，任何对 Objective-C 编译器具有特殊意义的名称都不能作为变量名。

始终记住，在 Objective-C 中，大写字母和小写字母是区分的。在那里，变量名 `sum`、`Sum`、`SUM` 分别指代不同的变量。正如所述，在命名类时，要用大写字母开头。另一方面，实例变量、对象和方法名通常以小写字母开头。为了可读性，名称内部使用大写字母来指示新单词的开头，如下例所示：

- `AddressBook`：这可能是一个类名。
- `currentEntry`：这可能是一个对象。
- `current_entry`：

## @interface 部分

如你从程序 3.2 的注释所示，该程序在逻辑上被分为三个部分：

- `@interface` 部分
- `@implementation` 部分
- program 部分

`@interface` 部分描述了类及其方法，而 `@implementation` 部分描述了数据（来自该类的对象将存储的*实例变量*），并包含了实现接口部分中声明的方法的实际代码。最后，program 部分包含了执行程序意图的程序代码。

> 注意：你也可以在接口部分中为类声明实例变量。在实现部分进行此项操作的功能是从 Xcode 4.2 开始添加的，并且被认为是定义类的更好方法。你将在后面的章节中学习更多关于其原因的知识。

这些每一个部分都是每个 Objective-C 程序的一部分，尽管你可能不需要自己编写每一个部分。正如你所看到的，每个部分通常被放在自己单独的文件中。不过，目前，我们将它们全部保存在同一个文件中。

## @interface 部分详解

当你定义一个新类时，你必须告诉 Objective-C 编译器该类源自何。也就是说，你必须命名它的*父类*。接下来，你需要定义在处理来自此类的对象时可以使用的操作类型，或称为*方法*。正如你将在后面的章节中学到的，你还会在程序中这个名为 `@interface` 部分的特殊部分里列出被称为*属性*的项。该部分的通用格式如下：

```objc
@interface NewClassName: ParentClassName

propertyAndMethodDeclarations;

@end
```



按照惯例，类名以大写字母开头，尽管这不是强制要求的。这使得阅读你程序的人只需查看名称的第一个字符，就能将类名与其他类型的变量区分开来。让我们稍微离开一下谈谈 Objective-C 中的命名规则。

### 选择名称

在第 2 章“Objective-C 编程”中，你使用了几个变量来存储整数值。例如，你在程序 2.4 中使用了变量 `sum` 来存储两个整数 50 和 25 相加的结果。

Objective-C 语言允许你在变量中使用除整数以外的数据类型，只要在程序中使用该变量之前对它进行了正确的声明即可。变量可以用于存储浮点数、字符，甚至是对象（指针，或者更准确地说，是对象的引用）。

命名的规则非常简单：它们必须以字母或下划线开头，后面可以跟任意字母（大小写）、下划线和数字 0–9 的组合。以下是有效名称列表：

- `sum`
- `pieceFlag`
- `i`
- `myLocation`
- `numberOfOfMoves`
- `sysFlag`
- `ChessBoard`

另一方面，由于上述原因，以下名称是无效的：

- `sumValue $`：`$` 不是有效字符。
- `piece flag`：不允许嵌入空格。
- `3Spencer`：名称不能以数字开头。
- `int`：这是一个关键字。

`int` 不能用作变量名，因为它的用法对 Objective-C 编译器有特殊含义。这种用法被称为保留名或保留字。通常，任何对 Objective-C 编译器具有特殊意义的名称都不能作为变量名。

始终记住，在 Objective-C 中，大写字母和小写字母是区分的。在那里，变量名 `sum`、`Sum`、`SUM` 分别指代不同的变量。正如所述，在命名类时，要用大写字母开头。另一方面，实例变量、对象和方法名通常以小写字母开头。为了可读性，名称内部使用大写字母来指示新单词的开头，如下例所示：

- `AddressBook`：这可能是一个类名。
- `currentEntry`：这可能是一个对象。
- `current_entry`

## @interface 部分

如你从程序 3.2 的注释所示，该程序在逻辑上被分为三个部分：

- `@interface` 部分
- `@implementation` 部分
- `program` 部分

`@interface` 部分描述了类及其方法，而 `@implementation` 部分描述了数据（来自该类的对象将存储的*实例变量*），并包含了实现接口部分中声明的方法的实际代码。最后，`program` 部分包含了执行程序意图的程序代码。

> 注意：你也可以在接口部分中为类声明实例变量。在实现部分进行此项操作的功能是从 Xcode 4.2 开始添加的，并且被认为是定义类的更好方法。你将在后面的章节中学习更多关于其原因的知识。

这些每一个部分都是每个 Objective-C 程序的一部分，尽管你可能不需要自己编写每一个部分。正如你所看到的，每个部分通常被放在自己单独的文件中。不过，目前，我们将它们全部保存在同一个文件中。

## @interface 部分详解

当你定义一个新类时，你必须告诉 Objective-C 编译器该类源自何。也就是说，你必须命名它的*父类*。接下来，你需要定义在处理来自此类的对象时可以使用的操作类型，或称为*方法*。正如你将在后面的章节中学到的，你还会在程序中这个名为 `@interface` 部分的特殊部分里列出被称为*属性*的项。该部分的通用格式如下：

```objc
@interface NewClassName: ParentClassName

propertyAndMethodDeclarations;

@end
```



# 类、对象与方法

按照惯例，类名以大写字母开头，尽管这不是强制要求的。这使得阅读你程序的人只需查看名称的第一个字符，就能将类名与其他类型的变量区分开来。让我们稍微离开一下谈谈 Objective-C 中的命名规则。

## 选择名称

在第 2 章“Objective-C 编程”中，你使用了几个变量来存储整数值。例如，你在程序 2.4 中使用了变量 `sum` 来存储两个整数 50 和 25 相加的结果。

Objective-C 语言允许你在变量中使用除整数以外的数据类型，只要在程序中使用该变量之前对它进行了正确的声明即可。变量可以用于存储浮点数、字符，甚至是对象（指针，或者更准确地说，是对象的引用）。

命名的规则非常简单：它们必须以字母或下划线开头，后面可以跟任意字母（大小写）、下划线和数字 0–9 的组合。以下是有效名称列表：

- `sum`
- `pieceFlag`
- `i`
- `myLocation`
- `numberOfOfMoves`
- `sysFlag`
- `ChessBoard`

另一方面，由于上述原因，以下名称是无效的：

- `sumValue $`：`$` 不是有效字符。
- `piece flag`：不允许嵌入空格。
- `3Spencer`：名称不能以数字开头。
- `int`：这是一个关键字。

`int` 不能用作变量名，因为它的用法对 Objective-C 编译器有特殊含义。这种用法被称为保留名或保留字。通常，任何对 Objective-C 编译器具有特殊意义的名称都不能作为变量名。

始终记住，在 Objective-C 中，大写字母和小写字母是区分的。在那里，变量名 `sum`、`Sum`、`SUM` 分别指代不同的变量。正如所述，在命名类时，要用大写字母开头。另一方面，实例变量、对象和方法名通常以小写字母开头。为了可读性，名称内部使用大写字母来指示新单词的开头，如下例所示：

- `AddressBook`：这可能是一个类名。
- `currentEntry`：这可能是一个对象。
- `current_entry`：

## @interface 部分

如你从程序 3.2 的注释所示，该程序在逻辑上被分为三个部分：

- `@interface` 部分
- `@implementation` 部分
- `program` 部分

`@interface` 部分描述了类及其方法，而 `@implementation` 部分描述了数据（来自该类的对象将存储的*实例变量*），并包含了实现接口部分中声明的方法的实际代码。最后，`program` 部分包含了执行程序意图的程序代码。

> **注意**：你也可以在接口部分中为类声明实例变量。在实现部分进行此项操作的功能是从 Xcode 4.2 开始添加的，并且被认为是定义类的更好方法。你将在后面的章节中学习更多关于其原因的知识。

这些每一个部分都是每个 Objective-C 程序的一部分，尽管你可能不需要自己编写每一个部分。正如你所看到的，每个部分通常被放在自己单独的文件中。不过，目前，我们将它们全部保存在同一个文件中。

当你定义一个新类时，你必须告诉 Objective-C 编译器该类源自何处。也就是说，你必须命名它的*父类*。接下来，你需要定义在处理来自此类的对象时可以使用的操作类型，或称为*方法*。正如你将在后面的章节中学到的，你还会在程序中这个名为 `@interface` 部分的特殊部分里列出被称为*属性*的项。该部分的通用格式如下：

```objc
@interface NewClassName: ParentClassName

propertyAndMethodDeclarations;

@end
```

## @implementation 部分

正如所述，`@implementation` 部分包含了你在 `@interface` 部分中声明的方法的实际代码。你需要指定要在此类的对象中存储什么类型的数据。也就是说，你描述了类将包含的数据成员。这些成员被称为**实例变量**（instance variables）。作为术语的一部分，你称在 `@interface` 部分中声明了方法，而在 `@implementation` 部分中定义了它们（即，提供了实际代码）。`@implementation` 部分的一般格式如下：

```objc
@implementation NewClassName

{
  memberDeclarations;
}

methodDefinitions;

@end
```

`NewClassName` 是在 `@interface` 部分中用于类时使用的相同名称。你可以使用末尾的冒号后跟父类，就像我们在 `@interface` 部分中做的那样：

```objc
@implementation Fraction: NSObject
```

然而，这是可选的，且通常不这样做。

`memberDeclarations` 指定了在 `Fraction` 中存储了什么类型的数据，以及这些数据类型的名称。正如你所看到的，该部分被包含在自己的大括号内。对于你的 `Fraction` 类，这些声明表示 `Fraction` 有两个整数成员，分别称为 `numerator`（分子）和 `denominator`（分母）：

```objc
int numerator;
int denominator;
```

在此部分中声明的成员被称为实例变量。每当你创建一个对象时，也会创建一个新的且唯一的实例变量集。因此，你有两个 `Fraction` 对象，一个称为 `fracA`，另一个称为 `fracB`，它们都将拥有自己的一组实例变量——也就是说，`fracA` 和 `fracB` 各自拥有各自独立的分子和分母。Objective-C 系统会自动跟踪这一点，这是使用对象时更棒的特性之一。

`@implementation` 部分的 `methodDefinitions` 部分包含了 `@interface` 部分中指定的每个方法的代码。与 `@interface` 部分类似，每个方法定义都首先识别方法的类型（类方法或实例方法）、其返回类型以及参数及其类型。然而，它不是以分号结尾，而是紧跟在方法后面的冒号，并包含在一组括号内。这里指出，你可以使用特殊的 `@synthesize` 指令让编译器自动为你生成方法。这将在第 7 章中详细介绍。

考虑程序 3.2 中的 `@implementation` 部分：

```objc
//--- @implementation section ---
@implementation Fraction
{
    int numerator;
    int denominator;
}

-(void) print {
    NSLog(@"%i/%i", numerator, denominator);
}

-(void) setNumerator:(int) n {
    numerator = n;
}

-(void) setDenominator:(int) d {
    denominator = d;
}
@end
```

`print` 方法使用 `NSLog` 显示实例变量 `numerator` 和 `denominator` 的值。但此方法指的是哪个 `numerator` 和 `denominator` 呢？它指的是消息接收者对象中的实例变量。这是一个重要的概念，我们很快就会回到这里。

`setNumerator:` 方法将你调用的整数参数 `n` 存储在实例变量 `numerator` 中。同样，`setDenominator:` 将其参数 `d` 的值存储在实例变量 `denominator` 中。

## program 部分

程序部分包含解决特定问题的代码，如果有必要，它可以分布在许多文件中。你必须有一个名为 `main` 的例程，正如我们之前提到的。那里是你的程序始终开始执行的地方。这里是程序 3.2 中的 `program` 部分：

```objc
// program section ---
int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *myFraction;
        // 创建一个 Fraction 实例并初始化它
        myFraction = [Fraction alloc];
        myFraction = [myFraction init];
        // 设置分数为 1/3
        [myFraction setNumerator: 1];
        [myFraction setDenominator: 3];
        // 使用 print 方法显示分数
        NSLog(@"The value of myFraction is:%@", [myFraction print]);
    }
    return 0;
}
```



在 `main` 内部，你通过以下行定义了一个名为 `myFraction` 的变量：
`Fraction *myFraction;`

这一行显示 `myFraction` 是一个 `Fraction` 类型的对象；也就是说，`myFraction` 用于存储来自你新的 `Fraction` 类的值。变量名前的星号在下文中会有更详细的描述。

现在你有了一个用来存储 `Fraction` 的对象，你需要创建一个，就像请求工厂为你造一辆新车一样。这是通过以下行实现的：
`myFraction = [Fraction alloc];`

`alloc` 是 `allocate`（分配）的缩写。你想为一个新分数分配内存空间。这个表达式向你新创建的 `Fraction` 类发送消息：
`[Fraction alloc];`

## 第 3 章 类、对象和方法

你正在使用 `Fraction` 类来应用 `alloc` 方法，但你从未定义过 `alloc` 方法，它是从父类继承来的。第 8 章“继承”将详细讨论这个主题。

当你向一个类发送 `alloc` 消息时，你会得到该类的新实例。在程序 3.2 中，返回的值存储在你的 `myFraction` 内部。`alloc` 方法保证将对象的所有实例变量置零。然而，并不意味着对象已经为了使用而正确初始化。你需要在分配对象后对其进行初始化。

这是通过程序 3.2 中的语句实现的，内容如下：
`myFraction = [myFraction init];`

再次，你在这里使用了一个并不是你自己编写的方法。`init` 方法初始化类的实例。注意，你正在向 `myFraction` 发送 `init` 消息。也就是说，你想在这里初始化一个特定的 `Fraction` 对象，所以你不是向类发送它——而是向类的实例发送。在继续之前，请确保你理解这一点。

`init` 方法也会返回一个值——即初始化的对象。你将返回值存储在你的 `myFraction` 中。
在 Objective-C 中，分配类新实例然后对其初始化的双行序列操作通常会将这两个语句组合在一起，如下：
`myFraction = [[Fraction alloc] init];`

这个内部消息首先被求值：
`[Fraction alloc]`

如你所知，这个消息表达式的结果是实际分配的 `Fraction`。你没有像之前那样将分配结果存储在变量中，而是直接对它应用 `init` 方法。所以，再次，你分配了一个新的 `Fraction` 然后对其进行初始化。初始化的结果随后赋值给 `myFraction` 变量。
最后一种简便技术是，分配和初始化通常直接整合到声明行中，如下所示：

```
myFraction = [[Fraction alloc] init];
```

回到程序 3.2，你现在准备好设置你的分数的数值了。程序执行了以下操作：
设置分数为 1/3

```
[myFraction setNumerator:1];
[myFraction setDenominator:3];
```

第一条消息语句向 `myFraction` 发送 `setNumerator:` 消息。提供的参数是值 1。控制权传递到你为 `Fraction` 类定义的 `setNumerator:` 方法中。Objective-C 系统知道要使用该类中的哪个方法，因为它知道 `myFraction` 是来自 `Fraction` 类的对象。

## program 部分 41

在 `setNumerator:` 方法内部，传递的值 1 被存储在变量 `n` 中。该方法中的单行程序代码将该值存储在实例变量 `numerator` 中。因此，你有效地将 `myFraction` 的分子设置为了 1。

接下来是在 `myFraction` 上调用 `setDenominator:` 方法的消息。参数 3 被赋值给 `setDenominator:` 方法内部的变量 `d`。值随后存储在 `denominator` 实例变量中，完成了将值 1/3 赋值给 `myFraction` 操作。现在你准备好显示你的分数的数值了，你通过程序 3.2 中的以下代码来实现：

```
// 使用 print 方法显示分数
```

```
NSLog(@"The value of myFraction is:%@",
[myFraction]);
```

`NSLog` 调用仅显示了以下文本：
The value of myFraction is:

消息表达式调用了 `print` 方法：
`[myFraction];`

在 `print` 方法内部，实例变量 `numerator` 和 `denominator` 的值用斜杠字符分隔并显示。

> 注意
> 过去，iOS 程序员负责通过向对象发送 release 消息来告诉系统他们何时在使用该对象。这是通过一种名为手动引用计数（manual reference counting）的内存管理系统实现的。从 Xcode 4.2 开始，程序员不再需要担心这些，依靠它们在需要时释放内存。这是通过被称为自动引用计数（Automatic Reference Counting，简称 ARC）的机制实现的。当你使用 Xcode 4.2 或更高版本编译新应用程序时，ARC 是默认开启的。

看起来你写了很多代码在程序 3.2 中复制程序 3.1 中实现的内容。这对于这个简单的例子是如此；然而，使用对象的最终目标是让你的程序更容易编写、维护和扩展。你以后会意识到这一点。

让我们回到 `myFraction` 的声明：
`Fraction *myFraction;`

这一行显示 `myFraction` 是一个 `Fraction` 类型的对象；也就是说，`myFraction` 用于存储来自你新的 `Fraction` 类的值。变量名前的星号在下文中会有更详细的描述。

现在你有了一个用来存储 `Fraction` 的对象，你需要创建一个，

## 第 3 章 类、对象和方法

位于内存中。当你像所示第一次声明 `myFraction` 时，它的值是未定义的（undefined），因为它没有被设置为任何值，也没有默认值。我们可以将 `myFunction` 想象成一个存储值的盒子。初始时，盒子包含某些未定义的值，因为它还没有被分配任何值。这在图 3.2 中所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_58_0.png)

图 3.2 声明 `Fraction *myFraction;`

当你分配一个新对象（例如使用 `alloc`）时，内存中会留出足够的空间来存储对象的数据，这包括其实例变量的空间以及额外额外的空间。存储数据的位置（数据的引用）由 `alloc` 程返回，并赋值给变量 `myFraction`。这一切都发生在程序 3.2 执行的这条语句中。

```
myFraction = [alloc];
```

对象的分配以及在 `myFunction` 中存储该对象的引用如图 3.3 所示。

| | 0 numerator |
|---|------|
| myFraction | 0 denominator |

图 3.3 myFraction 与数据之间的关系

> 注意
> 对象中存储的数据比这里所示的要多，但你不需要担心。你会注意到实例变量被显示为设置为 0。这目前正由 `alloc` 方法处理。然而，对象仍然没有被妥善初始化。你仍然需要在新分配的对象上使用 `init` 方法。

注意图 3.3 中的有向线。这表示了变量 `myFraction` 与分配的对象之间建立的连接。（`myFraction` 内部的值实际上是一个内存地址。对象的数据就存储在该内存地址上。）

随后，在程序 3.2 中，分数的分子和分母被设置了。图 3.4 描绘了完全初始化的 Fraction 对象，其分子被设置为 1，分母被设置为 3。

接下来的示例展示了你如何在程序中处理多个分数。在程序 3.3 中，你将一个分数设置为 2/3，另一个设置为 3/7，并显示了它们。

| 1 numerator |
|---|---|
| 3 denominator |

图 3.4 设置分数的分子和分母

# 程序 3.3

```objc
// 处理分数的程序 - 续
#import <Foundation/Foundation.h>

//@interface section ---
@interface Fraction: NSObject
-(void) print;
-(void) setNumerator:(int) n;
-(void) setDenominator:(int) d;
@end

//@implementation section ---
@implementation Fraction
{
int numerator;
int denominator;
}
-(void) print
{
NSLog("@%i/%i", numerator, denominator);
}
-(void) setNumerator:(int) n
{
numerator = n;
}
-(void) setDenominator:(int) d
{
denominator = d;
}
@end
```

## 第 3 章 类、对象和方法

```objc
//--- 程序部分 ---
int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *frac1 = [[Fraction alloc] init];
        Fraction *frac2 = [[Fraction alloc] init];
        // 将第一个分数设置为 2/3
        [frac1 setNumerator: 2];
        [frac1 setDenominator: 3];
        // 将第二个分数设置为 3/7
        [frac2 setNumerator: 3];
        [frac2 setDenominator: 7];
        // 显示分数
        NSLog(@"First fraction is:%@", frac1);
        [frac1 print];
        NSLog(@"Second fraction is:%@", frac2);
        [frac2 print];
    }
    return 0;
}
```

# 程序 3.3 输出

First fraction is:
2/3
Second fraction is:
3/7

`@interface` 和 `@implementation` 部分与程序 3.2 保持不变。程序创建了两个 Fraction 对象，`frac1` 和 `frac2`，并将 2/3 赋值给第一个分数，将 3/7 赋值给第二个。注意，当 `setNumerator:` 方法应用于 `frac1` 将其分子设置为 2 时，实例变量 `frac1` 的实例变量 `numerator` 被设置为 2。同样，`frac2` 使用相同的方法将其分子设置为 3，它独特的实例变量 `numerator` 被赋值为值 3。每当你创建一个新对象时，它都会获得自己的一组独特的实例变量。3.5 描述了这一点。

| Object | frac1 | frac2 |
| --- | --- | --- |
| Instance Variables | numerator 2 | numerator 3 |
| | denominator 3 | denominator 7 |

图 3.5 独特的实例变量

根据哪个对象接收消息，就会引用正确的实例变量。因此，每当 `setNumerator:` 使用方法内部的名称时，引用的都是 `frac1` 的分子：

```
[frac1 setNumerator: 2];
```

这是因为 `frac1` 是消息的接收者。

# 访问实例变量和数据封装

你已经看到分数可以通过名称直接访问 `numerator` 和 `denominator` 两个实例变量。事实上，实例方法始终可以访问它的实例变量。然而，类方法不能，因为它只处理类本身。但是，如果你想从 `main` 程内部访问实例变量呢？你不能直接访问，因为它们是隐藏的。这种对用户隐藏细节的事实被称为封装。数据封装在程序员和类之间提供了一个良好的隔层。

你可以通过编写特殊方法来访问类中的实例变量，以设置和获取它们的值。我们编写了 `setNumerator` 和 `setDenominator` 来设置实例变量。为了获取这些变量，你需要编写两个方法，相应地访问接收消息的 Fraction。结果是返回对应的整数值。这里是你的新方法的声明：

```objc
(int) numerator;
(int) denominator;
```

## 第 3 章 类、对象和方法

这里是定义：

```objc
-(int) numerator
{
    return numerator;
}
```

```objc
-(int) denominator
{
    return denominator;
}
```

注意方法名称与它们访问的实例变量名称相同（尽管起初看起来可能有点奇怪）；实际上这是常见的做法。程序 3.4 测试了你的新方法。

```objc
// 访问实例变量的程序 - 续
#import <Foundation/Foundation.h>

//---- interface 部分
@interface Fraction: NSOObject
-(void) print;
-(void) setNumerator:(int) n;
-(void) setDenominator:(int) d;
-(int) numerator;
-(int) denominator;
@end
```

```objc
//---- implementation 部分----
@implementation Fraction
{
int numerator;
int denominator;
}
-(void) print
{
    NSLog("%d/%d", numerator, denominator);
}
-(void) setNumerator:(int) n
{
numerator = n;
}
-(void) setDenominator:(int) d
{
    denominator = d;
}
-(int) numerator
{
    return numerator;
}
-(int) denominator
{
    return denominator;
}
@end
```

```objc
//---- program 部分 ---
int main(int argc, char *argv[]) {
    @autoreleasepool {
        Fraction *myFraction = [[Fraction alloc] init];
        // 将分数设置为 1/3
        [myFraction setNumerator:1];
        [myFraction setDenominator:3];
        // 使用我们的新方法显示分数
        NSLog("%value of myFraction is:%d/%d",
               [myFraction numerator], [myFraction denominator]);
    }
    return 0;
}
```

程序 3.4 输出
The value of myFraction is 1/3

## 第 3 章 类、对象和方法

这条 `NSLog` 语句显示了向 `myFraction` 发送的两个消息：第一个是获取其分子的值，第二个是它的分母值。

```
NSLog("@value of myFraction is:%d/%d", [myFraction numerator], [myFraction denominator]);
```



所以，在第一情况下，分子将发送给 `Fraction` 对象 `myFraction`。在该方法中，代码将访问并返回 `numerator` 实例变量的值。`Fraction` 的 `numerator` 将被访问并返回。返回的整数随后传递给 `NSLog` 显示。

对于第二种情况，将调用 `denominator` 来访问并返回 `myFraction` 的分母值，随后传递给 `NSLog` 显示。逐渐地，设置实例变量的方法通常被称为 setter（存器），用于获取实例变量的方法被称为 getter（取器）。对于 `Fraction` 类，`setNumerator` 和 `setDenominator` 是 setter，`numerator` 和 `denominator` 是 getter。总而言，setter 和 getter 也称为访问器方法（accessor methods）。

确保你理解 setter 和 getter 之间的区别。setter 不返回值，因为它们的作用是接收参数并将相应的实例变量设置为该参数。在这种情况下不需要返回任何值。设置实例变量的值是 setter 的目的，所以 setter 通常不返回值。另一方面，getter 的目的是“获取”存储在对象中的实例变量的值并将其发送给程序。为了实现这一点，getter 必须使用 `return` 语句返回实例变量的值。

再次，这种不能在类编写的方法之外设置或获取实例变量的值，而必须编写 setter 和 getter 方法来完成的观点，就是数据封装的原则。你使用方法来访问这些通常对“外部世界”隐藏的数据。这为实例变量提供了一个中心化的路径，并防止其他代码更改这些值，这会让你的程序更难以追踪、调试和修改。

我们还应该指出，有一个名为 `new` 的方法结合了 `alloc` 和 `init` 的动作。因此，这行代码可以分配并初始化一个新的 `Fraction`：

```objc
Fraction *myFraction = [Fraction new];
```

通常使用两步法（分配和初始化）更好，这样你从概念上理解正在发生两个不同的事件：你先创建一个新对象，然后对其进行初始化。

# 总结

现在你已经了解如何定义自己的类、创建该类的对象或实例，以及向这些对象发送消息。我们将在后面的章节中重新回到 `Fraction` 类。你将学习如何向方法传递多个参数，如何将类定义划分到单独的文件，以及如何使用继承和动态绑定等核心概念。然而，现在是学习更多关于 Objective-C 数据类型和编写表达式的时间。首先，尝试完成后续练习以测试你对本章涵盖的重要要点的理解。

## 练习

- 1. 以下哪些名称是无效的？为什么？
  `Int` `playNextSong` `6_05`
  `_calloc` `Xx` `alphaBetaRoutine`
  `clearScreen` `-1312` `z`
  `Reinitialize` `A$`

- 2. 根据本章汽车的示例，想一个你每天使用的对象。为该对象识别一个类，并写出你对该对象的五个动作。

- 3. 根据练习 2 中的列表，使用以下语法将你的列表重写为这种格式：
  `[instance method];`

- 4. 想象你除了汽车外还拥有一艘船和一辆摩托车。列出你对这些每种物品会执行的动作。这些动作之间有重叠吗？

- 5. 根据问题 4，假设你有一个类 `Vehicle` 和一个对象 `myVehicle`，它可以是 `Car`、`Motorcycle` 或 `Boat`。想象你写了以下代码：
  `[myVehicle prep];`
  `[myVehicle getGas];`
  `[myVehicle service];`

  你是否看到能够对可能来自几个类之一的对象应用某个动作有什么优势？

- 6. 在 C 这样的过程化语言中，你考虑动作，然后编写代码在各种对象上执行该动作。参考汽车示例，你可能会在 C 中写一个过程来洗车、洗船、洗摩托车等。如果你采用这种方法并想添加一种新的车辆类型（参见上一个练习），你认为与面向对象的方法相比，使用这种过程化方法有什么优缺点？

- 7. 定义一个名为 `XYPoint` 的类，存储笛卡尔坐标 (x, y)，其中 x 和 y 是整数。定义方法来单独设置点的 x 和 y 坐标并取回它们的值。编写一个 Objective-C 程序来实现你的新类并对其进行测试。

## 数据类型与表达式

在本章中，我们将查看基本数据类型，并描述在 Objective-C 中形成算术表达式的基本规则。

## 数据类型与常量

你已经遇到过 Objective-C 的基本数据类型 `int`。正如你所见，声明为 `int` 类型的变量可以只包含整数值——即不包含小数位的值。

Objective-C 编程语言还提供了其他三种数据类型：`float`、`double` 和 `char`。声明为 `float` 类型的变量可以用于存储浮点数（包含小数位的值）。`double` 类型与 `float` 相同，通常范围是其两倍。最后，`char` 数据类型可以用于存储单个字符，例如字母 a、数字 6 或分号（更多此类信息请见后文）。

在 Objective-C 中，任何字面量数字、单个字符或字符串都称为常量。例如，数字 58 代表一个常量值。字符串 `@"Programming in Objective-C is fun."` 是常量字符串对象的示例。完全由常量组成的表达式称为常量表达式。因此，这个表达式是一个常量表达式，因为表达式的每一项都是一个常量值：

```
128 + 7 - 17
```

但如果 `i` 被声明为整数变量，那么这个表达式就不代表常量表达式：

```
128 + 7 - i
```

## 类型 int

整数常量由一个或多个数字组成的序列组成。序列前面的减号表示该值为负值。值 158、-10 和 0 都是整数常量的有效示例。数字之间不允许嵌入空格，且不能使用逗号。（因此，值 12,000 不是有效的整数常量，必须写成 12000。）

每个值，不论是字符、整数还是浮点数，都有与其相关的取值范围。这个范围与存储特定类型数据而分配的存储空间有关。通常，该数量在语言中没有定义；它通常取决于你运行的计算机，因此被称为**实现或机器依赖的**。例如，一个整数变量可能占用你计算机的 32 位，或者可能存储在 64 位中。如果使用 64 位，那么在整数变量中存储的数字将比使用 32 位大得多。

### 注意

在 Mac OS X 下，你可以选择编译为 32 位或 64 位应用程序。在一种情况下，`int` 占用 32 位；在另一种情况下，则使用 64 位。

## 类型 float

你可以使用类型为 `float` 的变量来存储包含小数位的值。浮点数的特征是存在小数点。值 `3.`、`.125`、`.8` 和 `-.0001` 都是浮点常量的有效示例。要显示浮点值，可以使用 `NSLog` 转换字符 `%f` 或 `%g`。

浮点常量也可以用所谓的科学计数法表示。值 `1.7e4` 就是这种表示法。正如前面提到的，`double` 类型与 `float` 相同，范围是其两倍。

## 类型 char

`char` 数据类型可以用于存储单个字符，例如字母 a、数字 6 或分号（更多此类信息请见后文）。

在 Objective-C 中，可以使用字符 `%c` 来显示 `char` 的值。

# 程序 4.1

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        int integerVar = 100;

        float floatingVar = 331.79;

        double doubleVar = 0.84e+11;

        char charVar = 'W';

        NSLog("integerVar = %i", integerVar);

        NSLog("floatingVar = %f", floatingVar);

        NSLog("doubleVar = %e", doubleVar);

        NSLog("doubleVar = %g", doubleVar);

        NSLog("charVar = %c", charVar);

    }

    return 0;

}
```

# 程序 4.1 输出

```
integerVar = 100
floatingVar = 331.790000
doubleVar = 8.440000e+11
doubleVar = 8.44e+11
charVar = W
```

在程序输出的第二行，注意赋值给 `floatingVar` 的值 331.79 实际上显示为 331.790009。这种不准确性在计算机内部表示数字时尤为常见。你在计算器上处理数字时可能遇到过某种不准确性。如果你在计算器上用 1 除以 3，得到的结果是 .3333333 带有额外的 3。这串 3 是计算器对三分之一的近似值。但计算器只能容有限的位数，因此机器固有的不准确性适用于此处：某些浮点值无法在计算机内存中精确表示。

# 修饰符：long、long long、short、unsigned 和 signed

如果将修饰符 `long` 直接放在 `int` 声明之前，那么声明的整数变量在某些计算机系统上具有扩展范围。`long int` 声明的示例可能是：

```
long int factorial();
```

此声明将变量 `factorial` 定义为长整型（long integer）。与 `float` 和 `double` 一样，`long` 变量的范围取决于你特定的计算机系统。
要使用 `NSLog` 显示 `long int` 的值，在格式字符之前使用字母 `l` 作为修饰符。这意味着可以使用格式字符 `%li` 来以十进制格式显示 `long int` 的值。
你也可以使用 `long int` 变量或 `long double` 来存储具有更大范围的浮点数。
当 `short` 修饰符放在 `int` 声明前面时，它告诉 Objective-C 编译器所声明的变量用于存储小型整数值。使用 `short` 变量的主要动机是为了节省内存空间，当程序需要大量内存而可用内存有限时，这可能会成为问题。
可以放在 `int` 变量前的最后一个修饰符用于确保变量仅存储正数。以下代码向编译器声明变量 `counter` 仅包含正值：

```
unsigned int counter;
```

将整数变量的使用限制在仅存储正整数，可以扩展整数变量的范围。

## 类型 id

`id` 类型用于存储任何类型的对象。在某种意义上，它是一种泛型。例如，此行代码将 `graphicObject` 声明为 `id` 类型变量：

```
id graphicObject;
```

可以声明方法返回 `id` 类型的值，如下所示：

```
- (id) newObject: (int) type;
```

这代码声明了一个实例方法 `newObject`，它接受一个名为 `type` 的参数，并返回一个 `id` 类型的值。
`id` 类型是书中经常用到的重要数据类型。为了完整性，我们在这里简要提到了它。`id` 类型是 Objective-C 中非常重要的特性——多态和动态绑定的基础，这些特性在第 9 章“多态、动态类型与动态绑定”中会有详尽的讨论。

### 表 4.1 基础数据类型

| 类型 | 常量示例 | NSLog 字符 |
|---|---|---|
| char | 'a', '\n' | %c |
| short int | | %hi, %hx, %ho |
| unsigned short int | - | %hu, %hx, %ho |
| int | 12, -97, 0FFE0, 0177 | %i, %x, %o |
| unsigned int | 12u, 100U, 0xFFu | %u, %x, %o |
| long int | 12L, -2001, 0xFFFF | %li, %lx, %lo |
| unsigned long int | 12UL, 100ul, 0xFFEE | %u, %lx, %lo |
| long long int | 0xe5e5e5LL, 50011 | %lli, %llx, %llo |
| unsigned long long int | 12ull, 0xffULL | %llu, %lx, %lo |
| float | 12.34f, 3.1e-5, 0x1p50, 0x1p-1 | %f, %e, %g, %a |
| double | 12.34, 3.1e-5, 0x1p3 | %f, %e, %g, %a |
| long double | 12.34L, 3.1e-51 | %Lf, %Le, %Lg |
| id | nil | %p |

> 注意
> 在表中，整数常量前的领先零表示该常量是八进制（基 8）表示，而开头的 `0x`（或 `0X`）表示它是十六进制（基 16）表示。写为 `0x.1p3` 的数字代表十六进制浮点常量。不用担心这些格式，为了完整性，它们被总结在表格中。此外，诸如 f、L (LL)、u (U) 和 ll (LL) 等后缀也可以显式地将常量表示为 float、long long、unsigned 和 long long。

在 Objective-C 中，正如在几乎所有的编程语言中，加号 (`+`) 用于相加两个值，减号 (`-`) 用于减去两个值，星号 (`*`) 用于相乘两个值，斜杠 (`/`) 用于除法两个值。这些运算符被称为二元算术运算符，因为它们在两个值或项上操作。

## 运算符优先级

你已经看到如何在 Objective-C 中执行像加法这样的简单操作。下面的程序进一步说明了减法、乘法和除法操作。程序执行的最后两个操作引入了这样一个概念：一个运算符相对于另一个运算符具有更高的优先级（precedence）。事实上，Objective-C 中的每个运算符都有与其相关的优先级。这种优先级用于确定包含多个运算符的表达式如何计算：优先级较高的运算符先计算。包含相同优先级运算符的表达式从左到右或从右到左计算，取决于运算符。这被称为运算符的结合律。

## 程序 4.2

```c
// 阐述各种算术运算符的使用

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        int a = 100;
```



# 算术表达式

在前三个语句中，我们在 `int` 和 `a`、`b` 以及 `result` 的声明之间插入了额外的空格，以对齐每个变量的声明。这使得程序更具可读性。你可能注意到之前的程序中，每个运算符周围都留有空格。这并不是强制要求的，完全是为了美观。通常情况下，你可以在任何允许单个空格的地方添加额外的空格。如果生成的程序更容易阅读，那么多按几次空格键是值得的。

程序 4.3 中第一个 `NSLog` 调用中的表达式强化了运算符优先级的概念。该表达式的求值过程如下：

1. 除法的优先级高于加法，`a` 的值 (25) 除以 5。得到中间结果 5。
2. 乘法的优先级也高于加法，将中间结果 5 乘以 `b` 的值，得到一个新的中间结果 10。
3. 执行 6 和 10 的加法运算，得到最终结果 16。

第二个 `NSLog` 语句引入了一个新的转折。你可能认为将 `a` 除以 `b` 再乘以 `b` 应该返回 `a` 的值（已设置为 25）。但事实并非如此，如输出的 24 所示。计算机在过程中某个地方丢失了一个比特吗？大不像。事实是，该表达式是使用整数算术进行求值的。

如果你回看变量 `a` 和 `b` 的声明，你会记得它们都被声明为 `int` 类型。每当表达式中待求值的项由两个整数组成时，Objective-C 系统将使用整数算术执行操作。在这种情况下，数字的所有的小数部分都会丢失。在这里，当 `a` 的值除以 `b` 的值（即 25 除以 2）时，你得到的中间结果是 12 而不是 12.5。将此中间结果乘以 2 得到最终结果 24，从而解释了“数字”的丢失。

正如你从程序 4.3 的最后一个 `NSLog` 语句看到的，如果你使用浮点类型的整数执行相同的操作，你将获得预期的结果。

使用 `float` 变量还是 `int` 变量应该根据变量的意图用途来决定。如果你不需要任何小数，请使用整数变量。生成的程序将更高效——也就是说，在许多计算机上它的执行速度会更快。另一方面，如果你需要小数精度，选择是显而易见的。你必须回答的问题是使用 `float` 还是 `double`。这个问题的答案取决于你处理的数字所需的精度以及它们的大小。

在最后一个 `NSLog` 语句中，`a` 的值通过减号运算符取了反。一元运算符（`unary operator`）作用于单个值，而二运算符（`binary operator`）作用于两个值。负号实际上具有双重角色：作为二运算符，它用于减去两个值；作为一元运算符，它用于对一个值取反。

一元减运算符的优先级高于所有算术运算符，除了一元加 (`+`)，后者的优先级相同。因此，以下表达式会导致 `-a` 与 `b` 的乘法：

```c
c = -a * b;
```

# 模运算符

本章介绍的最后一个算术运算符是模运算符，它的符号是百分号 (`%`)。请尝试通过分析程序 4.4 的输出来确定该运算符是如何工作的。

## 程序 4.4

```objc
// 模运算符
#import <Foundation/Foundation.h>

int main(int argc, char * argv[]) {
    @autoreleasepool {
        int a = 25, b = 5, c = 10, d = 7;
        NSLog("%i %% %i = %i", a, b, a % b);
        NSLog("%i %% %i = %i", a, c, a % c);
        NSLog("%i %% %i = %i", a, d, a % d);
        NSLog("%i / %i * %i + %i %% %i = %i", a, d, d, a, d, a / d * d + a % d);
    }
    return 0;
}
```

## 程序 4.4 输出

```
a % b = 0
a % c = 5
a % d = 4
a / d * d + a % d = 25
```

注意 `main` 函数内部在一条语句中定义并初始化变量 `a`、`b`、`c` 和 `d` 的语句。

如你所知，`NSLog` 使用紧跟百分号后面的字符来决定如何打印下一个参数。然而，如果紧接着的是另一个百分号，那么如果你认为模运算符 `%` 的功能是给出第一个值除以第二个值的余数，那么你是正确的。在第一个例子中，25 除以 5 的余数是 0。如果你将 25 除以 10，你将得到余数 5，如第二行输出验证的那样。将 25 除以 7 得到余数 4，如第三行输出所示。

现在让我们关注语句中求值的最后一个算术表达式。你意识到在 Objective-C 中两个整数值之间的操作是使用整数算术执行的。因此，两个整数除法产生的任何余数都会被丢弃。如表达式 `a / d` 所示，将 25 除以 7 得到我们的中间结果 3。将此值乘以 `d` 的值（即 7），产生中间结果 21。最后，加上 `a` 除以 `d` 的余数（如表达式 `a % d` 所示），得到最终结果 25。这个值与变量 `a` 的值相同并非巧合。通常，在假设 `a` 和 `b` 都是整数的情况下，该表达式将始终等于 `a` 的值：

```c
a / b * b + a % b
```

在 Objective-C 中，模运算符 `%` 定义为仅与整数值工作。就此而言，模运算符的优先级与乘法和除法运算符相等。这意味着，如下的表达式

```c
table + value % TABLE_SIZE
```

将被求值为：

```c
table + (value % TABLE_SIZE)
```

# 整数与浮点数转换

为了有效地开发 Objective-C 程序，你必须理解 Objective-C 中用于浮点值和整数值隐式转换的规则。程序 4.5 演示了一些简单的转换。

## 程序 4.5

```objc
// Objective-C 中的基础转换
#import <Foundation/Foundation.h>

int main(int argc, char * argv[]) {
  @autoreleasepool {
    float f1 = 123.45;
    int i1 = (int)f1;
    NSLog("%f to %i", f1, i1);

    int i2 = -150;
    float f2 = (float)i2;
    NSLog("%d to %f", i2, f2);

    float f3 = 25.0;
    int i3 = (int)f3;
    NSLog("%f to %i", f3, i3);

    int i4 = 25 / 2;
    float f4 = (float)i4;
    NSLog("%d to %f", i4, f4);
  }
  return 0;
}
```

## 程序 4.5 输出

```
123.450000 to 123
-150 to -150.000000
12.500000 to 12
12 to 12.500000
```

当 Objective-C 中将浮点值赋值给整数变量时，小数部分会被截断。当之前的程序将 `f1` 的值赋值给 `i1` 时，123.45 被截断，这意味着只有其整数部分 123 被存储在 `i1` 中。程序的第一行输出证实了情况如此。

将整数变量赋值给浮点变量不会改变数字的值；系统只是将其转换并存储在浮点变量中。程序的第二行输出证实了 `i2` 的值 (-150) 被正确转换并存储在浮点变量 `f2` 中。

程序的最后两行输出说明了构造算术表达式时要记住的两点。第一点与整数算术有关，只要表达式中的两个操作数都是整数（适用于短整数、无符号整数和长整数），操作将按照整数算术规则执行。因此，除法产生的任何小数都会被丢弃，即使结果被赋值给浮点变量（正如我们在程序中所做的）。当整数 `i2` 除以整数常量时，系统执行整数除法。因此，-150 除以 100 的结果 -1 是存储在浮点变量 `f1` 中的值。

上一个程序中的下一个除法操作涉及一个整数变量和一个浮点常量。在 Objective-C 中，如果两个值中的任意一个是浮点变量或常量，则它们之间的任何操作都将作为浮点操作执行。因此，当 `i2` 的值除以 `100.0` 时，系统将该除法运算视为浮点除法并产生结果 -1.5，然后将其赋值给浮点变量 `f1`。

# 类型转换运算符

你已经看到在声明和定义方法时，将类型括在括号内的作用是声明返回类型和参数类型。在表达式内部使用时，它具有不同的用途。

程序 4.5 中的最后一次除法如下所示，引入了类型转换运算符：

```c
f2 = (float) i2 / 100; // 类型转换运算符
```

类型转换运算符的作用是将 `i2` 的值转换为指定的类型，以便评估表达式。这不会以任何方式永久地影响 `i2` 的值；它是一个一元运算符，行为与其他一元运算符相似。就像表达式 `-a` 对 `a` 的值没有永久影响一样，表达式 `(float)` 也是如此。

类型转换运算符的优先级高于除元运算符和加减运算符以外的所有算术运算符。如果有必要，你始终可以使用括号来强制按任何顺序对项进行求值。

类型转换运算符的另一个使用示例是表达式：

```c
(int) 29.55 + (int) 21.99
```

在 Objective-C 中的求值结果为：

```c
29 + 21
```

因为将浮点值转换为整数的效果之一是截断浮点值。表达式：

```c
(float) 6 / (float) 4
```

产生的结果为 1.5，以下表达式也是如此：

```c
(float) 6 / 4
```

类型转换运算符通常用于将泛型 `id` 类型的对象强制转换为特定类的对象。例如，以下行将 `id` 变量 `myNumber` 的值转换为 `Fraction` 对象：

```objc
id myNumber;
Fraction *myFraction;
...
myFraction = (Fraction *) myNumber;
```

转换的结果被赋值给 `Fraction` 变量 `myFraction`。

# 赋值运算符

Objective-C 语言允许使用以下格式将算术运算符与赋值运算符结合：

```c
op=
```

在此格式中，`op` 是任何算术运算符，包括 `+`、`-`、`*`、`/` 或 `%`。此外，`op` 可以是后续讨论的位移和掩码位运算符。考虑此语句：

```c
count += 10;
```

所谓“加赋值”运算符 `+=` 的是将运算符右侧的表达式加到运算符左侧的表达式，并将结果存回运算符左侧的变量中。上语句等价于此语句：

```c
count = count + 10;
```

以下表达式使用“减赋值”赋值运算符从 `counter` 的值减去 5：

```c
counter -= 5
```

它等价于此表达式：

```c
counter = counter - 5
```

这是一个稍微复杂的表达式：

```c
a /= b + c
```

它除以等号右侧出现的任何内容——或除以 `b` 和 `c` 的和——并将结果存储在 `a` 中。先执行加法是因为加法运算符的优先级高于赋值运算符。事实上，除了逗号运算符外，所有运算符的优先级都高于赋值运算符，而所有赋值运算符的优先级相同。

在这种情况下，此表达式与以下表达式相同：

```c
a = a / (b + c)
```

使用赋值运算符的动机有三点：第一，程序状态变得更容易编写，因为运算符左侧的内容不需要在右侧重复。第二，生成的表达式通常更易读。第三，使用这些运算符可以使程序运行更快，因为编译器有时可以生成更少代码来评估表达式。

# 计算器类

现在是时候定义一个新类了。我们将创建一个 `Calculator` 类，它是一个简单的四功能运算计算器，你可以用它对数字进行加、乘、减、除。类似于普通的计算器，这一个必须跟踪运行总和，即通常说的累加器（`accumulator`）。因此，方法必须允许将累加器设置为特定值、将其清空（或设置为零），并在完成后检索其值。程序 4.6 包含了该新类的定义和一个用于运行你的计算器的测试程序。

## 程序 4.6

```objc
// 实现一个 Calculator 类
#import <Foundation/Foundation.h>

@interface Calculator : NSObject

// 累加器方法
- (void)setAccumulator:(double)value;
- (void)clear;
- (double)accumulator;

// 算术方法
- (void)add:(double)value;
- (void)subtract:(double)value;
- (void)multiply:(double)value;
- (void)divide:(double)value;

@end

@implementation Calculator {
    double accumulator;
}

- (void)setAccumulator:(double)value {
    accumulator = value;
}

- (void)clear {
    accumulator = 0;
}

- (double)accumulator {
    return accumulator;
}

- (void)add:(double)value {
    accumulator += value;
}

- (void)subtract:(double)value {
    accumulator -= value;
}

- (void)multiply:(double)value {
    accumulator *= value;
}

- (void)divide:(double)value {
    accumulator /= value;
}

@end

int main(int argc, char * argv[]) {
    @autoreleasepool {
        Calculator *deskCalc = [[Calculator alloc] init];
        [deskCalc setAccumulator:100.0];
        [deskCalc add:200.0];
        [deskCalc divide:15.0];
        [deskCalc subtract:10.0];
        [deskCalc multiply:5];
        NSLog(@"The result is %f", [deskCalc accumulator]);
    }
    return 0;
}
```

## 程序 4.6 输出

```
The result is 50.000000
```

方法的定义非常直接。`Calculator` 类只有一个存储值的 `double` 实例变量。注意调用方法的消息：

```objc
[deskCalc multiply:5];
```

参数是一个整数，但方法期望一个 `double`。虽然发生了自动转换，但在调用时提供正确的类型是更好的做法。与你可能处理许多分数的 `Fraction` 类不同，你可能希望定义一个新类来这样做。我们将在第 10 章详细讨论类型转换和位操作。

## 练习

1. 下列常量哪些是无效的？
   - `123.456`
   - `0X10.5`
   - `0001`
   - `0xFFFF`
   - `123.5e2`
   - `0Xab5`
   - `1234L`
   - `096`

2. 写一个程序使用以下公式将 27°华氏 (`F`) 转换为摄氏 (`C`)：
   `C = (F - 32) / 1.8`
   注意你不需要定义类来进行此计算。只需评估表达式即可。

3. 你预期以下程序的输出是什么？

```objc
#import <Foundation/Foundation.h>

int main(int argc, char * argv[]) {
    @autoreleasepool {
        char c, d;
        c = 'd';
        d = c;
        NSLog(@"%c", d);
    }
    return 0;
}
```



# 练习题

## 4. 写一个程序评估此处所示式（以计算指数），直接进行乘法——Objective-C 中没有幂运算符：

`3x - 5x² + 6`

## 5. 写一个程序评估该表达式并显示结果（记住使用指数格式显示结果）：

`(3.31 x 10⁻⁶ + 2.01 x 10⁻⁹) / (7.16 x 10⁻⁸ + 2.01 x 10⁻⁹)`

## 6. 复数包含两个部分的数：实部和虚部。如果 a 是实部 b 是虚部，则使用记法表示该数：

`a + bi`

编写一个 Objective-C 程序定义一个新类 `Complex`。遵循 `Fraction` 类建立的范式，为你的新类定义以下方法：

```
-(void) setReal:(double) a;
-(void) setImaginary:(double) b;
-(void) print; // 显示为 a + bi
-(double) real;
-(double) imaginary;
```

编写一个测试程序来测试你的新类和方法。

## 7. 假设你正在开发一个处理图形对象的程序库。首先定义一个名为 `Rectangle` 的新类。目前，只需跟踪矩形的宽度和高度。编写方法来设置矩形的宽度和高度、获取这些值，并计算面积和周长。假设这些对象描述的是积分网格上的矩形，例如计算机屏幕。在这种情况下，假设矩形的宽度和高度为整数。

以下是 `Rectangle` 类的 `@interface` 部分：

```
@interface Rectangle: NSObject
-(void) setWidth:(int) w;
-(void) setHeight:(int) h;
-(int) width;
-(int) height;
-(int) area;
-(int) perimeter;
@end
```

编写实现部分和一个测试程序来测试你的新类和方法。

## 8. 程序 4.6 中的 `add:`、`subtract:`、`multiply:` 和 `divide:` 方法没有返回值。修改这些方法，使其执行计算后返回累加器的值。测试新方法。

## 9. 完成练习题 8 后，向 `Calculator` 类中添加以下方法并测试它们：

```
-(double) changeSign; // 累加器的符号
-(double) reciprocal; // 1/累加器
-(double) xSquared; // 累加器的平方
```

## 10. 为程序 4.6 中的 `Calculator` 类添加内存功能。实现以下方法声明并测试它们：

```
-(double) memoryClear; // 清除内存
-(double) memoryStore; // 将累加器设置为内存
-(double) memoryRecall; // 将内存设置为累加器
-(double) memoryAdd:(double) value; // 将值加入内存
-(double) memorySubtract:(double) value; // 从内存中减去值
```

最后两个方法在设置累加器的同时也会对内存执行指定的操作。让所有方法都返回累加器的值。

# 第 5 章 程序循环

在 Objective-C 中，你可以通过几种方式重复执行一段代码。这些循环能力是本章的主题，由以下部分组成：

- `for` 语句
- `while` 语句
- `do` 语句

我们从一个简单的示例开始：数数。

如果你将 15 颗弹珠排列成三角形，你得到的布局可能看起来如图 5.1 所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_87_0.png)

三角形的第一行包含一个弹珠，第二行包含两颗弹珠，依此类推。通常情况下，形成包含 n 行的三角形所需的弹珠数是从 1 到 n 的整数之和。这个和被称为三角形数。

如果你从 1 开始，第四个三角形数就是连续整数 1-4 的和（`1 + 2 + 3 + 4`），即为 10。

假设你想写一个程序来计算并显示第八个三角形数的值。显然，你可以在脑海中轻松地算出这个数，但为了起见，让我们假设你想用 Objective-C 写一个程序来完成这项任务。程序 5.1 展示了这样一个程序。

## 程序 5.1

```
#import <Foundation/Foundation.h>

// 计算第八个三角形数的程序
int main (int argc, char * argv[]) {
    @autoreleasepool {
        int triangularNumber;

        triangularNumber = 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8;

        NSLog("The eighth triangular number is %i", triangularNumber);

        return 0;
    }
}
```

### 程序 5.1 输出

第八个三角形数是 36

程序 5.1 的技术对于计算较小的三角形数很好用，但如果你需要找到第 200 个三角形数的值，会发生什么？修改程序 5.1 来显式加上从 1 到 200 的所有整数显然非常麻烦。幸运的是，有一种简单的方法。

计算机的基本属性之一是重复执行一组语句的能力。这些循环能力使程序员能够编写包含重复过程的简洁程序，否则这些过程可能需要数千甚至数百万条程序语句才能完成。Objective-C 语言包含了三个程序循环的语句。

## for 语句

让我们来看一个使用 `for` 语句的程序。程序 5.2 的目的是计算第 200 个三角形数。看看你是否能确定 `for` 语句是如何工作的。

## 程序 5.2

```
// 计算第 200 个三角形数的程序
// for 语句的介绍
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, triangularNumber;
        triangularNumber = 0;

        for ( n = 1; n <= 200; n = n + 1 )
            triangularNumber += n;

        NSLog("The 200th triangular number is %i", triangularNumber);
    }

    return 0;
}
```

### 程序 5.2 输出

第 200 个三角形数是 20100

需要对程序 5.2 进行解释。计算第 200 个三角形数所采用的方法与上一个程序中计算第 8 个三角形数的方法实际上是相同的。计算第 200 个三角形数的方法是将 `triangularNumber` 设置为 0。在程序 5.2 中，`for` 语句用于初始化变量为 1。你可以看到，赋值是一个有效的表达式形式。

`for` 语句的第一个部分 `init_expression` 用于在循环开始前设置值。在程序 5.2 中，这部分用于将 `n` 的初始值设置为 1。

`for` 语句的第二个部分 `loop_condition` 指定了循环继续的条件。换句话说，只要该条件满足。再次引用程序 5.2，`for` 语句的 `loop_condition` 由以下关系表达式指定：

`n <= 200`

这个表达式可以读作“n 小于等于 200”。小于等于运算符（即小于号字符后紧跟等号 [=]）是 Objective-C 语言提供的几种关系运算符之一。这些运算符用于测试条件。答案是条件满足则为真，如果不满足则为假。

`for` 语句的一般格式如下：

```
for ( init_expression; loop_condition; loop_expression )
    program statement
```

括号内的三个表达式——`init_expression`、`loop_condition` 和 `loop_expression` 设置了循环的环境。紧随其后的程序语句（当然以分号结束）将根据 `for` 语句中指定的次数执行。

关系运算符的优先级低于所有算术运算符。这意味着，例如，表达式 `a < b + c` 的求值方式为 `a < (b + c)`。

这是你所预期的。如果 a 的值小于 b + c 的值，则为真，否则为假。

### 表 5.1 关系运算符

| 运算符 | 含义 | 示例 |
|---|---|---|
| `==` | 等于 | `count == 10` |
| `!=` | 不等于 | `flag != DONE` |
| `<` | 小于 | `a < b` |
| `<=` | 小于等于 | `low <= high` |
| `>` | 大于 | `points > POINT_MAX` |
| `>=` | 大于等于 | `j >= 0` |

可以等价表示为：

`n < 201`

回到之前的示例，程序语句形成了 `for` 循环的体——`triangularNumber += n;`——只要关系测试的结果为真，它就会重复执行；在本例中，只要 `n` 的值小于或等于 200，它就会执行。该程序语句的作用是将 `n` 的值加到 `triangularNumber` 的值上。

当 `loop_condition` 不再满足时，将立即执行紧接在 `for` 循环之后的程序语句。在这个程序中，循环结束后将继续执行 `NSLog` 语句。

`for` 语句的最后一个组成部分包含一个表达式，该表达式在每次执行循环体时都会被求值。在程序 5.2 中，`loop_expression` 将 `n` 的值加 1。因此，在将 `n` 的值加到 `triangularNumber` 的值之后，`n` 的值就会增加 1，其范围从值 1 到 201。

值得注意的是，`n` 达到的最后一个值 201 并没有加到 `triangularNumber` 的值上，因为循环一旦循环条件不再满足，或者一旦 `n` 等于 201，循环就会终止。

总结，`for` 语句的执行过程如下：

1. 首先求值初始表达式。该表达式通常将循环内部使用的变量（通常称为索引变量）设置为某个初始值（如 0 或 1）。
2. 求值循环条件。如果条件不满足（表达式为假），循环立即终止。继续执行紧接在循环之后的程序语句。
3. 执行构成循环体的程序语句。
4. 求值循环表达式。该表达式通常用于更改索引变量的值，通常通过对其加 1 或减 1 来实现。
4. 回到步骤 2。

请记住，循环条件在进入循环时立即被求值，在循环体执行一次之前。还要记住，不要在循环结束的右括号后加分号，因为这会立即结束循环。

程序 5.2 实际上在达到最终目标的过程中生成了前 200 个三角形数，因此生成一个这些数字的表格可能会很不错。为了节省空间，假设你只想打印前 10 个三角形数的表格。程序 5.3 完成了这项任务。

## 程序 5.3

```
// 生成三角形数表格的程序

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, triangularNumber;

        NSLog("TABLE OF TRIANGULAR NUMBERS");
        NSLog(" n  Sum from 1 to n");
        NSLog("--  --------------------");

        triangularNumber = 0;

        for ( n = 1; n <= 10; ++n) {
            triangularNumber += n;
            NSLog("%i  %i", n, triangularNumber);
        }
    }

    return 0;
}
```

### 程序 5.3 输出

| n | Sum从 1 to n |
|---|---|
| 1 | 1 |
| 2 | 3 |
| 3 | 6 |
| 4 | 10 |
| 5 | 15 |
| 6 | 21 |
| 7 | 28 |
| 8 | 36 |
| 9 | 45 |
| 10 | 55 |

在程序 5.3 中，三个 `NSLog` 语句的作用仅仅是提供一个总标题并为输出列标记。

在显示了相应的标题后，程序计算了前 10 个三角形数。变量 `n` 用于计数你正在计算的从 1 到 `n` 之和的当前数字，变量 `triangularNumber` 用于存储三角形数 `n` 的值。

`for` 语句的执行通过将变量 `n` 的值设置为 1 开始。

如前所述，紧接在 `for` 语句之后的程序语句构成了程序循环体。但如果你想重复执行的不只是单个语句，而是一组程序语句，会发生什么？这可以通过将所有程序语句封装在一对大括号中来实现。此时，系统会将这组语句（或块）视为一个单一实体。通常情况下，任何允许使用单条语句的 Objective-C 程序中，如果可以使用语句块，那么你也应该将循环体封装在大括号内。

因此，在程序 5.3 中，将 `n` 加到 `triangularNumber` 值中的表达式和紧随其后的 `NSLog` 语句共同构成了程序循环体。请特别注意作为 `for` 循环部分的程序语句的方式。通过快速观察，你可以很容易地确定哪些语句构成了输入此循环的部分：

```
for ( n = 1; n <= 10; ++n) {
    triangularNumber += n;
    NSLog("%i  %i", n, triangularNumber);
}
```

在这里，左大括号放在了 `for` 之后的一行。这完全是风格问题，对程序没有影响。

下一个三角形数通过将 `n` 的值加到上一个三角形数来计算。第一次通过 `for` 循环时，上一个三角形数 0，因此当 `n` 等于 1 时，`triangularNumber` 的新值就是 `n` 的值。

当循环体执行一次后，循环表达式被求值。你可能会注意到 5.3 的最后一行没有对齐。你可以通过替换程序 5.3 中相应的 `NSLog` 语句来解决这个小烦恼：

`NSLog("%2i  %i", n, triangularNumber);`

看起来奇怪的表达式：

`++n`

是一个有效的 Objective-C 表达式。它引入了 Objective-C 语言中一种新的（独特的）运算符：增量运算符。该运算符的作用是对引起的操作加 1。加 1 是程序中如此常见的操作，以至于专门创建了一个运算符。因此，表达式 `++n` 等于表达式 `n + 1`。起初你可能会觉得 `n + 1` 更易读。

当然，任何提供加 1 运算符的编程语言如果没有相应的减 1 运算符是不完整的。正如你所猜的，该运算符的名称是减量运算符，它用双减号表示。因此 Objective-C 中的表达式

`bean_counter = bean_counter - 1`

可以使用减量运算符等价表示，如下：

`--bean_counter`

这在示例中取决于个人偏好。然而，你将在第 13 章“底层语言特性”中学习运算符的前置或后置性质在复杂表达式中的作用。

因此，通过使用 `%2i` 字段宽度规范，你确保了至少使用两列来显示 `n` 的值；你还确保了 `triangularNumber` 的值是对齐的。

## 键盘输入

程序 5.2 计算了第 200 个三角形数，仅此而已吗？如果你其实想计算第 50 个或第 100 个三角形数呢？嗯，如果是那样，你就必须修改程序，使 `for` 循环执行正确的次数。你还需要修改 `NSLog` 语句以显示正确的消息。

一个更简单的解决方案可能是询问你想要想要计算哪一个三角形数。然后，在你给出答案后，程序就可以计算所需的三角形数。你可以使用一个名为 `scanf` 的例程来实现这种解决方案。`scanf` 例程在概念上与 `NSLog` 例程相似。`NSLog` 用于用于显示值，而 `scanf` 用于允许程序员向程序中输入值。如果你正在编写一个使用图形用户界面（UI）的 Objective-C 程序（例如 Cocoa 或 iOS 应用程序），你可能在程序中完全不会使用 `NSLog` 或 `scanf`。

程序 5.4 询问用户应该计算哪个三角形数，进行计算并显示结果。

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int n, number, triangularNumber;

        NSLog(@"What triangular number do you want?");
        scanf("%i", &number);

        triangularNumber = 0;

        for ( n = 1; n <= number; ++n) {
            triangularNumber += n;
        }

        NSLog(@"Triangular number %i is %i\n", number, triangularNumber);
    }

    return 0;
}
```

在接下来的程序输出中，用户输入的数字（**100**）被设置为粗体，以将它与程序显示的输出区分开。

### 程序 5.4 输出

What triangular number do you want?

**100**

Triangular number 100 is 5050

根据输出，用户在终端输入了结果 5050。如果用户想计算那些三角形数，他们也可以同样轻松地输入数字 10 或 30。



# 程序循环

## 程序 5.4 说明

程序 5.4 中的第一个 `NSLog` 语句用于提示用户输入一个数字。当然，提醒用户他们输入了什么总是好的。`scanf` 的第一个参数是格式化字符串，它不以 `@` 字符开头。与 `NSLog` 的第一个参数是一个 `NSString` 对象不同，`scanf` 是一个 C 风格字符串，因为 C 风格字符串前面没有 `@` 字符。

格式化字符串告诉 `scanf` 从控制台（或终端窗口，如果你使用 Terminal 应用程序编译程序的话）读取何种类型的值。在 `NSLog` 中，使用 `%i` 字符来指定一个整数值。

该例程的第二个参数指定了用户输入的值要存储在何处。在这种情况下，变量前的 `&` 字符是必要的。我们并不是提供变量数字的值，而是指定了我们想要存储该值的地方。现在不用担心那个。当我们在第 13 章讨论指针时，会详细地讨论这个字符（它实际上是一个运算符）。

根据前面的讨论，你现在可以看到 `scanf` 调用如何指定读取一个整数并存储到代表用户想要计算的三角形数的变量中。

在用户输入此数字（并按下键盘上的 Enter 键表示数字输入完成）后，程序计算请求的三角形数。这与程序 5.2 的做法相同；唯一的区别在于不是使用 200 作为限制，而是使用 `number` 作为限制。

> **注意**
>
> 在带有数字键盘的键盘上按下 Enter 键可能导致你输入的数字无法发送到程序。请使用键盘上的 Return 键。

计算出所需的三角形数后，将显示结果。此时，程序执行完毕。

## 嵌套 for 循环

程序 5.4 为用户提供了灵活性，让程序计算任何所需的三角形数。但假设用户有一个五个需要计算的三角形数列表呢？在这种情况下，用户只需执行程序五次，每次输入列表中要计算的下一个三角形目标。

实现相同目标的另一种方法，而且对于学习 Objective-C 来说是一种要有趣得多的方法，是让程序来处理这种情况。这最好的实现方式是在程序中插入一个循环，以重复整个系列计算五次。你可以使用 `for` 语句来设置这样一个循环。程序 5.5 及其相关输出说明了这种技术。

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[])
{
    @autoreleasepool {
        int number, triangularNumber, counter;

        for ( counter = 1; counter <= 5; ++counter ) {
            NSLog(@"What triangular number do you want?");
            scanf("%i", &number);

            triangularNumber = 0;

            for ( n = 1; n <= number; ++n ) {
                triangularNumber += n;
            }

            NSLog(@"Triangular number %i is %i", number, triangularNumber);
        }

        return 0;
    }
}
```

## 程序 5.5 输出

```text
What triangular number do you want?
12
Triangular number 12 is 78
What triangular number do you want?
25
Triangular number 25 is 325
What triangular number do you want?
50
Triangular number 50 is 1275
What triangular number do you want?
75
Triangular number 75 is 2850
What triangular number do you want?
100
Triangular number 100 is 5050
```

## for 语句

### for 循环变体

在离开对循环的讨论之前，我们应该提到一些允许的语法变体。在编写 `for` 循环时，你可能会发现你想在循环开始前初始化多个变量，或者你可能想在循环中评估多个表达式。你可以在任何字段中包含多个表达式，只要你用逗号分隔它们。例如，如下所示：

```objc
for ( i = 0, j = 0; ++i )
```

在循环开始前，`i` 的值设置为 0，`j` 的值设置为 0。这两个表达式 `i = 0` 和 `j = 0` 用逗号隔开，并且都被视为循环的 `init_expression` 字段的一部分。作为另一个例子，`for` 循环如下：

```objc
for ( i = 0, j = 100; i < 0; ++i, j -= 10 )
```

两个索引变量 `i` 和 `j` 分别设置为 0 和 100。每次执行循环体后，`i` 的值增加 1，`j` 的值减少 10。正如你可能在某个字段中包含多个表达式一样，你也需要从语句中省略一个或多个字段。你可以通过省略字段并用分号标记其位置来实现。`for` 语句中省略字段最常见的应用发生在不需要评估初始表达式时。在这种情况下，你可以只需留 `init_expression` 字段为空，但仍需包含分号：

```objc
for ( ; j != 100; ++j )
```

该语句可能用于在进入循环前已经设置了某些初始值。省略了 `looping_condition` 字段的 `for` 循环实际上建立了一个无限循环——即在理论上永远执行。只要使用其他方法退出循环（例如在稍后讨论的 `return`、`break` 或 `goto` 语句），这种循环就可以使用。你也可以在 `for` 循环内部的输入表达式中定义变量。这是通过我们过去定义变量的典型方式。例如，以下可以用于设置一个具有定义并初始化值为 1 的整数变量的 `for` 循环：

```objc
for ( int counter = 1; counter <= 5; ++counter )
```

变量 `counter` 仅在 `for` 循环执行期间已知（它被称为局部变量），并且在循环外部无法访问。

## while 语句

`while` 语句扩展了 Objective-C 语言的循环能力。这种频繁使用的结构的语法如下：

```
while ( expression )
    program statement
```

括号内指定的表达式会被求值。如果表达式的结果为真（true），则执行紧随其后的程序语句。在执行该语句（或用大括号括起来的多个语句）后，再次对表达式的值进行求值。如果求值结果为真，则执行程序语句。这个过程将持续，直到表达式最终求值为假（false），此时循环终止。程序的执行将从程序语句之后的后续语句继续进行。

作为其用法的示例，以下程序设置了一个 `while` 循环，该循环仅从 1 计数到 5。

### 程序 5.6

```objc
// 此程序引入了 while 循环。

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int count = 1;

        while ( count <= 5 ) {
            NSLog("%d", count);
            ++count;
        }
    }

    return 0;
}
```

### 程序 5.6 输出

```text
1
2
3
4
5
```

### while 语句说明

程序最初将 `count` 的值设为 1；随后开始执行 `while` 循环。因为 `count` 的值小于或等于 5，所以执行紧随其后的语句。大括号将 `NSLog` 语句和增加 `count` 的语句共同定义为 `while` 循环体。从程序的输出可以看出，该循环执行了五次，或者直到 `count` 的值达到 5 为止。

你可能通过这个程序意识到，你可以使用 `for` 语句轻松地完成相同的任务。事实上，`for` 语句始终可以转换为等效的 `while` 语句，反之亦然。对于通用格式：

```
for ( init_expression; loop_condition; loop_expression )
    program statement
```

可以等效地用 `while` 语句的形式表示如下：

```
init_expression;
while ( loop_condition )
{
    program statement
    loop_expression;
}
```

当你熟悉了 `while` 语句的使用后，你将更好地理解何时使用 `while` 语句符合逻辑，何时应该使用 `for` 语句。通常情况下，执行预定义次数的循环是实现 `for` 语句的首选方案。此外，如果初始化表达式、循环表达式和循环条件都涉及同一个变量，那么 `for` 语句是正确的选择。

下一个程序提供了 `while` 语句用法的另一个示例。该程序计算两个整数的最大公约数。两个整数的最大公约数（我们以后简写为 `gcd`）是能够整除这两个整数的最大整数值。例如，10 和 15 的 `gcd` 是 5，因为 5 是能够整除 10 和 15 的最大整数。

用于得到任意两个整数 `gcd` 的过程（或算法）基于欧几里得在公元前 300 年左右开发的程序。步骤如下：

| 问题 | 步骤 |
| :--- | :--- |
| 寻找两个非负整数 u 和 v 的最大公约数。 | 步骤 1：如果 v 等于 0，则我们完成了，gcd 等于 u。 |
| | 步骤 2：计算 `temp = u % v`，`u = v`，`v = temp`，并返回步骤 1。 |

不要担心上述算法工作原理的细节——深信它即可。我们在这里更关注的是开发一个寻找最大公约数的程序，而不是分析算法是如何运行的。

在将寻找最大公约数的解决方案以算法的形式表示后，开发计算机程序变成了一项简单的任务。对算法步骤的分析表明，只要 `v` 的值不等于 0，步骤 2 就会重复执行。这种认识导致我们在 Objective-C 中使用 `while` 语句对该算法进行自然实现。

### 程序 5.7

```objc
// 寻找两个非负整数的最大公约数
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int u, v, temp;

        NSLog(@"Enter two integers:");
        scanf("%d %d", &u, &v);

        while (v != 0) {
            temp = u % v;
            u = v;
            v = temp;
        }

        NSLog(@"The greatest common divisor is %d", u);
    }

    return 0;
}
```

### 程序 5.7 输出

```text
Enter two integers:
10 15
The greatest common divisor is 5
```

### 程序 5.7 输出（另一个）

```text
Enter two integers:
48 18
The greatest common divisor is 6
```

## do 语句

`do` 语句仅仅是 `while` 语句的易位，将循环条件放置在循环的末尾而不是开头。其语法如下：

```
do
    program statement
while ( expression );
```

程序语句会被执行一次，然后对表达式求值。如果表达式的求值结果为真，则循环继续重复执行。当表达式的求值结果为假时，循环终止，并按照正常顺序执行程序中的下一条语句。

程序 5.8 使用了 `while` 语句来反转数字的各位。回到程序并确定如果用户输入数字 0 而不是 13579，会发生什么。`while` 语句的循环将永远不会被执行，输出将不会显示任何内容。如果你使用 `do` 语句代替 `while` 语句，你就可以确保程序循环至少执行一次，从而保证在所有情况下都至少显示一个数字。程序 5.9 展示了 `do` 语句的使用。

### 程序 5.9

```objectivec
// 用于反转数字各位的程序
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int number, right_digit;

        NSLog(@"Enter your number.");
        scanf("%i", &number);

        do {
            right_digit = number % 10;
            NSLog(@"%i", right_digit);
            number /= 10;
        }
        while ( number != 0 );
    }
    return 0;
}
```

### 程序 5.9 输出

```text
Enter your number.
135
5
3
1
```

### 程序 5.9A 输出（重新运行）

```text
Enter your number.
0
0
```

从程序的输出中可以看出，当向程序输入 0 时，程序正确地显示了数字 0。

## break 语句

有时在执行循环时，你可能希望在特定条件发生时立即离开循环——例如，你可能检测到了错误条件，或者在列表中找到了你寻找的数据。你可以使用 `break` 语句来实现这一目的。`break` 语句的执行会导致程序立即退出其正在执行的循环，无论它是 `for`、`while` 还是 `do` 循环。循环中的后续语句将被跳过，正在执行的循环也将终止。程序执行将从循环之后的任何语句继续。

如果在一组嵌套循环中执行了 `break`，则只有执行该 `break` 的内层循环会被终止。

`break` 语句的格式简单为关键字 `break` 后跟一个分号，如下：

```objc
break;
```

## continue 语句

`continue` 语句与 `break` 语句相似，不同之处它不会导致循环终止。在执行 `continue` 语句的点上，`continue` 语句之后直到循环结束的所有语句都将被跳过。循环的执行将正常继续。

`continue` 语句最常用于根据某些条件跳过循环内部的一组语句，然后继续执行循环。`continue` 语句的格式如下：

```objc
continue;
```

在变得熟悉编写程序循环并能够优雅地退出循环之前，不要使用 `break` 或 `continue` 语句。这些语句太容易被滥用，可能导致程序难以理解。

# 总结

现在你已经熟悉了 Objective-C 语言提供的所有基本循环结构，已经准备好学习另一类语言语句，它们使你能够在程序执行期间做出决策。下一章将详细描述这些决策能力。

## 练习题

1. 编写一个程序，生成并显示一个从 1 到 10 的整数 $n$ 的 $n$ 和 $n^2$ 的表格。确保打印相应的列标题。
2. 通过此公式也可以为任何整数值 $n$ 生成三角形数：
   `triangularNumber = n * (n + 1) / 2`
   例如，第 10 个三角形数 55 可以计算出来。

# 第 6 章 决策制定

## if 语句

在向用户显示消息以及在 `number` 中存储整数值后，程序将测试 `number` 的值以检查它是否小于零。如果是，则执行接下来的程序语句，该语句会对 `number` 的值取反。如果 `number` 的值不小于零，则此程序语句将被自动跳过。（如果它已经是正数，你就不想对其取反。）随后，程序将显示 `number` 的绝对值，并结束执行。

让我们来看另一个使用 `if` 语句的程序。我们将在 `Fraction` 类中添加一个名为 `convertNum()` 的方法。该方法将提供以数字形式表示的分数的值。换句话说，它将把分子除以分母，并将结果作为双精度浮值返回。因此，如果你有一个分数 1/2，你希望该方法返回值 0.5。

此类方法的声明可能如下所示：

```objc
- (double) convertNum;
```

这是你编写其定义的方式：

```objc
- (double) convertNum
{
    return numerator / denominator;
}
```

嗯，并不是。按照目前的定义，这个方法实际上有两个严重的问题。你能发现它们吗？第一个问题与算术转换有关。回想 `numerator` 和 `denominator` 都是整数实例变量。当你除以两个整数时会发生什么？正确，是整数除法！如果你想转换分数 1/2，之前的代码将给你零！这可以通过类型转换运算符在除法发生之前将一个或两个操作数转换为浮点值，从而轻松地纠正：

```objc
(double) numerator / denominator
```

考虑到此运算符相对较高的优先级，在除法发生之前，`numerator` 的值首先被转换为 `double`。此外，你不需要转换 `denominator`，因为算术转换规则已经为你考虑了这一点。

该方法的第二个问题是，你应该检查除以零的情况（你应该始终检查这一点！）。该方法的调用者可能会无意中忘记设置分数的分母，或者可能将分数的分母设置为零，而你不希望你的程序异常终止。

`convertNum` 方法的修改版本在此：

```objc
- (double) convertNum
{
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}
```

我们决定如果分数的分母为零，则返回特殊值 `NAN`（代表“不是数字”）。该符号定义在一个名为 `math.h` 的系统头文件中，该文件会自动导入到你的程序中。让我们在程序 6.2 中使用这个方法。

## 程序 6.2



```objc
@import <Foundation/Foundation.h>

@interface Fraction : NSObject

-(void) print;
-(void) setNumerator:(int) n;
-(void) setDenominator:(int) d;
-(int) numerator;
-(int) denominator;
-(double) convertToNum;
@end

@implementation Fraction
int numerator;
int denominator;

-(void) print {
    NSLog("@%i/%i", numerator, denominator);
}

-(void) setNumerator:(int) n {
    numerator = n;
}

-(void) setDenominator:(int) d {
    denominator = d;
}

-(int) numerator {
    return numerator;
}

-(int) denominator {
    return denominator;
}
```

## if 语句

```objc
- (double) convertToNum
{
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}
@end
```

```objc
int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc] init];
        Fraction *bFraction = [[Fraction alloc] init];
    }

    [aFraction setNumerator: 1]; // 第1个分数是 1/4
    [aFraction setDenominator: 4];

    [aFraction print];
    NSLog("%s");
    NSLog("%f", [aFraction convertToNum]);

    [bFraction print]; // 从未赋值
    NSLog("%s");
    NSLog("%f", [bFraction convertToNum]);

    return 0;
}
```

## 程序 6.2 输出

1/4

=0.25

0/0=

nan

在将 `aFraction` 设置为 1/4 后，程序使用 `convertToNum` 方法将分数转换为十进制值。该值随后显示为 0.25。第二种情况，`bFraction` 的值没有被显式设置，因此它的分子和分母被初始化为零，这是实例变量的默认值。这解释了 `print` 方法的结果。它还导致 `convertToNum` 方法内部的 `if` 语句返回值 NAN，你会注意到它实际上由 `NSLog` 显示为 nan。

# 第6章 决策

## if-else

如果有人问你某个特定的数字是偶数还是奇数，你可能会通过检查数字的最后一位来判断。如果这个数字是 0, 2, 4, 6 或 8，你会很容易说该数字是偶数。否则，你会声称该数字是奇数。

计算机判断某个特定数字是偶数还是奇数的更简单方法不是通过检查数字的最后一位看它是否是 0, 2, 4, 6 或 8，而是简单地判断数字是否能被 2 整除。如果是，数字就是偶数；否则，它就是奇数。

你已经看到模运算符 `%` 用于计算一个整数除另一个整数的余数。如果除以 2 的余数为 0，数字就是偶数；否则是奇数。现在让我们写一个程序来判断一个数字是否能被 2 整除，然后显示相应的消息。在讨论偶数数的开始时，这种情况经常需要一个特殊的结构。在 Objective-C 中，这被称为 `else`，它的通用格式如下：

### 程序 6.3

```objc
#import <Foundation/Foundation.h>

main (int argc, char * argv[]) {
    @autoreleasepool {
        int number_test, remainder;

        NSLog("输入要测试的数字：");
        scanf("%d", &number_test);

        remainder = number_test % 2;

        if (remainder == 0) {
            NSLog("它是偶数。");
        }

        if (remainder != 0) {
            NSLog("它是奇数。");
        }
    }

    return 0;
}
```

## if 语句

### 程序 6.3 输出

输入要测试的数字：

245

它是奇数。

在输入数字后，程序计算出除以 2 的余数。第一个 `if` 语句测试余数是否等于零。如果是，显示“它是偶数”。第二个 `if` 语句测试它是否不等于零。如果是这种情况，显示“它是奇数”。

你可以将两个 `if` 语句合并单独的 `if-else`。你会发现这个新程序减少了程序的复杂性并提高了其可读性。

## 程序 6.4 偶数或奇数（版本2）

```objc
// <foundation/Foundation.h>
#import <Foundation.h>

main(int argc, char * argv[]) {
    @autoreleasepool {
        int number_test, remainder;

        NSLog("输入要测试的数字：");
        scanf("%d", &number_test);

        remainder = number_test % 2;

        if (remainder == 0) {
            NSLog("它是偶数。");
        } else {
            NSLog("它是奇数。");
        }
    }

    return 0;
}
```

### 程序 6.4 输出

输入要测试的数字：

1234

它是偶数。

### 程序 6.4 输出（重新运行）

输入要测试的数字：

6551

它是奇数。

> 别忘记双等号 (`==`) 是相等性测试，而单等号是赋值运算符。在 `if` 语句内部无意使用赋值运算符会导致很多头疼的问题。

## 复合关系测试

到目前为止在本章中使用的语句都是两个数字之间的简单关系测试。程序 6.1 比较了 `number` 的值与零，而程序 6.2 比较了分的分母与零。有时变得需要（尽管并非必须）使用更复杂的测试。例如，你想统计考试中在 70 到 79 之间（包含边界）的分数数量。在这种情况下，你希望将分数的值不仅与一个限制比较，还要与 70 和 79 这两个限制比较，以确保它落在指定的范围内。

Objective-C 语言提供了执行此类复合关系测试所需的机制。复合关系测试是由逻辑与或逻辑或运算符连接的一个或多个简单关系测试。这些运算符分别由字符对 `&&` 和 `||`（两个竖线字符）表示。例如，下面的 Objective-C 语句仅当 `grade` 的值大于或等于 70 且小于 79 时，才会增加 `grades_70_to_79` 的值：

```objc
if ( grade >= 70 && grade <= 79 )
    ++grades_70_to_79;
```

同样地，以下语句在 `index` 小于 0 或大于 99 时，会导致执行 `NSLog` 语句：

```objc
if ( index < 0 || index > 99 )
    NSLog("Error - index out of range");
```

复合运算符可以在 Objective-C 中用于形成极其复杂的表达式。Objective-C 语言赋予了程序员构建表达式的终极灵活性，但这种灵活性是程序员经常滥用的能力。简单的表达式总是更容易阅读和调试的。

在构建复合关系表达式时，请大量使用括号来辅助阅读表达式，避免因对 `or` 逻辑运算符优先级的错误假设而导致麻烦。（`||` 运算符的优先级低于任何算术或关系运算符，但高于 `&&` 运算符。）空格也可以提高表达式的可读性。在 `&&` 和 `||` 周围留出额外的空格可以在视觉上将这些运算符与它们连接的表达式隔离开来。

为了在实际程序中演示复合关系测试的使用，让我们写一个程序来测试一个年份是否能被 4 整除（闰年）。然而，你可能没有意识到，被 100 整除的年份不是闰年，除非它也能被 400 整除。首先，你可以尝试思考如何为这种条件设置测试。首先计算年份除以 4、100 和 400 后的余数，并将这些值赋值给命名恰当的变量，例如 `rem_4`、`rem_100` 和 `rem_400`。然后你可以测试这些余数，以确定闰年所需的标准。

如果我们重新重新表述之前对闰年的定义，我们是否可以说：如果一个年份能被 4 整除且不能被 100 整除，或者能被 400 整除，那么它就是闰年？停一下参考最后这句话，验证它是否与之前陈述的定义等价。既然我们已经用这些术语重新定义了它，将其转换为程序语句就变成了一项直接的任务，如下：

```objc
if ( (rem_4 == 0 && rem_100 != 0) || rem_400 == 0 )
    NSLog("It's a leap year.");
```

以下子表达式周围的括号不是必须的：

```objc
rem_4 == 0 && rem_100 != 0
```

这是因为表达式无论如何都会那样求值：记住 `&&` 的优先级高于 `||`。

事实上，在这个特定的示例中，下面的测试效果同样好：

```objc
if ( rem_4 == 0 && ( rem_100 != 0 || rem_400 == 0 ) )
```

如果你在测试之前添加几语句来声明变量并允许用户从终端输入年份，你就会得到一个判断年份是否为闰年的程序，如程序 6.5 所示。

## 程序 6.5

```objc
// 此程序判断一个年份是否为闰年

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int year, rem_4, rem_100, rem_400;

        NSLog(@"Enter the year to be tested: %i");
        scanf("%i", &year);

        rem_4 = year % 4;
        rem_100 = year % 100;
        rem_400 = year % 400;

        if ( (rem_4 == 0 && rem_100 != 0) || rem_400 == 0 ) {
            NSLog(@"It's a leap year.");
        } else {
            NSLog(@"Nope, it's not a leap year.");
        }
    }

    return 0;
}
```

### 程序 6.5 输出

Enter the year to be tested:

1955

Nope, it's not a leap year.

### 程序 6.5 输出（重新运行）

Enter the year to be tested:

2000

It's a leap year.

### 程序 6.5 输出（重新运行）

Enter the year to be tested:

1800

Nope, it's not a leap year.

之前的示例使用了一个非闰年年份，因为它不能被 4 整除（1955）；一个闰年年份，因为它能被 400 整除（2000）；以及一个不是闰年的年份，因为它能被 100 整除但不能被 400 整除（1800）。为了完成测试用例的运行，你应该尝试一个能被 4 整除且不能被 100 整除的年份。这留给你练习。

我们提到过 Objective-C 在程序中赋予了程序员极大的灵活性。例如，在上一个程序中，你不需要手动计算中间结果 `rem_4`、`rem_100` 和 `rem_400`。然而，我们可以使用复合运算符来简化逻辑。

复合运算符可以在 Objective-C 中用于形成极其复杂的表达式。Objective-C 语言赋予了程序员构建表达式的终极灵活性，但这种灵活性是程序员经常滥用的能力。简单的表达式总是更容易阅读和调试的。

在构建复合关系表达式时，请大量使用括号来辅助阅读表达式，避免因对 `or` 逻辑运算符优先级的错误假设而导致麻烦。（`||` 运算符的优先级低于任何算术或关系运算符，但高于 `&&` 运算符。）空格也可以提高表达式的可读性。在 `&&` 和 `||` 周围留出额外的空格可以在视觉上将这些运算符与它们连接的表达式隔离开来。

## 嵌套 if 语句

在讨论 if 语句时，我们经常遇到嵌套 if，即一个 if 语句位于另一个 if 语句内部。例如：

```objc
if (isOver == NO) {
    if (isTurn == YES) {
        [object doAction];
    } else {
        [object do otherAction];
    }
} else {
    [object finishGame];
}
```

注意 `else` 子句与测试语句关联，而不是测试游戏是否结束的 if 语句。通用规则是 `else` 总是与最后一个不包含 `else` 的语句关联。

你可以更进一步，在上述示例的最外层语句中添加一个 `else` 子句：

```objc
if (isOver == NO) {
    if (isTurn == YES) {
        [object doAction];
    } else {
        [object do otherAction];
    }
} else {
    [object finishGame];
}
```

这是因为 `else` 子句与最后一个未匹配的 `else if` 相关联。当内层的 `if` 不包含 `else` 但外层的 `if` 包含时，你可以使用大括号来强制不同的关联。大括号的作用是结束 `if` 语句。因此，以下语句实现了所需的效果：

```objc
if ([chessGameGameOver] == NO )
  if ([chessGamewhoseTurn] == YOU )
    [chessGameyourMove];

else
  [chessGame finish];
```

## else if 结构

你已经看到当对两个可能的条件进行测试时，`else` 语句是如何发挥作用的——数字是偶数还是奇数；或者年份是闰年还是不是。然而，你所做的编程决策绝不是非黑即白的。任务是编写一个程序，如果用户输入的数字小于二则显示 -1，如果等于零显示 0，如果大于零则显示 1。（这实际上是通常所符号函数的实现）。在这种情况下，你之前可能需要三次测试来确定输入的数字是负数、零还是正数。简单的 `if-else` 结构将不起作用。或者在这种情况下，你可以始终恢复到三个独立的语句，但这种解决方案不可行——特别是当测试不是互斥的时候。

你可以通过向 `else` 子句中添加一个 `if` 语句来处理上述情况。我们提到过 `else` 之后的语句可以是任何有效的 Objective-C 程序语句，那么为什么不要用一个呢？因此，在一般情况下，你可以写成

```objc
if ( expression 1 )
  program statement 1
else
  if ( expression 2 )
    program statement 2
  else
    program statement 3
```

这有效地将 `if` 语句从二值逻辑决策扩展到了三值逻辑决策。你可以按照刚才所示的方法在 `else` 子句中继续添加 `if` 语句，有效地将决策扩展到 n 值逻辑决策。

前面的结构使用得非常频繁，因此通常被称为 `else if` 结构，并且格式通常与之前所示的不同：

```objc
if ( expression 1 )
  program statement 1
else if ( expression 2 )
  program statement 2
else
  program statement 3
```

这种格式上的改进提高了语句的可读性，并更清楚地表明正在进行三路决策。

下一个程序通过实现之前讨论的符号函数来说明 `else if` 结构。

## 程序 6.6

// 实现符号函数的程序

### 程序 6.6 输出

请输入一个数字：

1121

Sign = 1

## if 语句

### 程序 6.6 输出（重新运行）

请输入一个数字：

-158

Sign = -1

### 程序 6.6 输出（重新运行）

请输入一个数字：

0

Sign = 0

如果输入的数字小于零，sign 被赋值为 -1；如果数字等于零，sign 被赋值为 0；否则，该数字必须大于零，因此 sign 被赋值为 1。

下一个程序分析在终端中输入的字符，并将其分类为字母（a-z 或 A-Z）、数字（0–9）或特殊字符（其他任何）。为了从终端读取单个字符，在 `scanf` 调用中使用了格式字符 `%c`。

## 程序 6.7

```objc
// 此程序对从键盘输入的单个字符进行分类
```

```objc
#import <Foundation/Foundation.h>
int main (int argc
```

# 第 6 章 做出决策

### 程序 6.7 输出

输入单个字符：

&

这是一个特殊字符。

### 程序 6.7 输出（重新运行）

输入单个字符：

8

它是一个数字。

### 程序 6.7 输出（重新运行）



输入单个字符：

B

它是一个字母。

> **注意**
>
> 如程序示例所示，最好在 `scanf` 格式化字符串的 `%c` 之前放一个空格（如 `" %c"`）。这将导致 `scanf` “跳过”输入中的任何所谓的空白字符（例如换行符、回车符、制表符、行进符）。省略该空格可能会导致 `scanf` 读取到你意料之外的字符。虽然在这个示例中可能不是问题，但在处理本章中的其他示例（包括练习题）时，每当你需要读取单个字符时，记住这是好的。

在读取字符后的第一个测试确定 `char` 变量 `c` 是否为字母。这是通过测试字符是小写字母还是大写字母来实现的。前面的测试通过以下表达式完成：

```
(c >= 'a' && c <= 'z')
```

如果 `c` 在字符 'a' 到 'z' 的范围内，则该表达式为真；即 `c` 是小写字母。后面的测试通过此表达式完成：

```
(c >= 'A' && c <= 'Z')
```

如果 `c` 在字符 'A' 到 'Z' 的范围内，则该表达式为真；即 `c` 是大写字母。这些测试在以 ASCII 格式存储字符的计算机系统中有效。

如果变量 `c` 是字母，则显示“It's an alphabetic character”。否则，如果 `c` 是数字，则显示“It's a digit”。否则，显示“It's a special character”。

## if 语句

如果输入的数字小于零，`sign` 被赋值为 -1；如果等于零，`sign` 被赋值为 0；否则，数字必须大于零，因此 `sign` 被赋值为 1。

下一个程序分析在终端中输入的字符，并将其分类为字母（a-z 或 A-Z）、数字（0–9）或特殊字符（其他任何）。为了从终端读取单个字符，`scanf` 调用中使用了格式字符 `%c`。

## if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

## if 语句

将输入发送给程序。通常，当你从终端读取数据时，直到按下 Return 键。

## if 语句

如果输入的数字小于零，`sign` 被赋值为 -1；如果等于零，`sign` 被赋值为 0；否则，数字必须大于零，因此 `sign` 被赋值为 1。

下一个程序分析在终端中输入的字符，并将其分类为字母（a-z 或 A-Z）、数字（0–9）或特殊字符（其他任何）。为了从终端读取单个字符，`scanf` 调用中使用了格式字符 `%c`。

## if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

## if 语句

如果输入的数字小于零，`sign` 被赋值为 -1；如果等于零，`sign` 被赋值为 0；否则，数字必须大于零，因此 `sign` 被赋值为 1。

## if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

## if 语句

如果输入的数字小于零，`sign` 被赋值为 -1；如果等于零，`sign` 被赋值为 0；否则，数字必须大于零，因此 `sign` 被赋值为 1。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

# if 语句

数字 0 到 9。事实上，字符 '0' 内部表示为 48，'1' 为 49，以此类推。显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

> **注意**
>
> 最好使用标准库中的 `islower` 和 `isupper` 函数，以完全避免内部表示问题。这样做，请在程序中包含 `#import <ctype.h>` 行。然而，我们在这里仅是为了说明目的。

显示“It's a special character”。否则，如果 `c` 是字母，则显示“It's an alphabetic character”。

字母。这些测试在以 ASCII 格式存储字符的计算机系统中有效。

如果变量 `c` 是字母，则显示“It's an alphabetic character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

显示“It's a digit”。否则，如果 `c` 不是数字，则显示“It's a special character”。

# if 语句 111

```
char operator;
Calculator *deskCalc = [[Calculator alloc] init];
```

```
NSLog("%Type in your expression.");
scanf("%lf %c %lf", &value1, &value2);
```

```
[deskCalc setAccumulator: value1];
if (operator == '+')
    [deskCalc add: value2];
else if (operator == '-')
    [deskCalc subtract: value2];
else if (operator == '*')
    [deskCalc multiply: value2];
else if (operator == '/')
    [deskCalc divide: value2];
```

```
NSLog("%.2f", [deskCalc accumulator]);
```

return 0;

}

## 程序 6.8 输出

Type in your expression.
123.5 + 59.3
182.80

## 程序 6.8 输出（重运行）

Type in your expression.
198.7 / 26
7.64

## 程序 6.8 输出（重运行）

Type in your expression.
89.3 * 2.5
223.25

## 布尔变量

## 117

```c
return 0;
```

## 程序 6.9 输出

输入你的表达式。
178.99 - 326.8
-147.81

表达式已读取，`operator` 的值将连续与每个 `case` 的值进行比较。当找到匹配项时，将执行包含在 `case` 内部的语句。随后，`break` 语句将执行流移出 `switch` 语句，此时程序执行完成。如果没有哪个 `case` 匹配 `operator` 的值，则会执行 `default` 情况，并显示“Unknown operator.”。

在之前述的程序中，`default` 情况中的 `break` 语句实际上是不必要的，因为在该 `switch` 语句之后没有其他语句了。然而，记住在每个 `case` 结束包含 `break` 是一个良好的编程习惯。
编写 `switch` 语句时，请记住任意两个 `case` 的值不能相同。你可以将多个值与一组特定的程序语句关联。这只需通过在要执行的公共语句之前列出多个值即可实现（在每个 `case` 中，值之前使用关键字 `case`，值之后使用冒号 `:`）。例如，在接下来的 `switch` 语句中，如果 `operator` 等于星号 `*` 或小写的 `x`，则执行 `multiply` 方法：

```objc
switch ( operator ) {
  case '*':
  case 'x':
    [descCalc multiply: value2];
    break;
}
```

## 布尔变量

几乎任何学习编程的人很快都会面临编写程序生成质数表的任务。为了唤起你的记忆，如果 `p` 不能被 1 和自身以外的任何整数整除，那么它就是一个质数。第一个质数定义为 2。下一个质数是 3，因为它不能被 1 和 3 以外的任何整数整除；而 4 不是质数，因为它能被 2 整除。

## 第 6 章 选择

你可以采取多种方法来生成质数表。例如，如果你的任务是生成 50 以内的所有质数，那么生成此类表格最直接（也是最简单）的算法只需测试每个整数 `p` 是否能被 2 到 `p-1` 之间的所有整数整除。如果任何这样的整数能整除 `p`，那么 `p` 就不是质数；否则，它就是一个质数。程序 6.10 生成了从 2 到 50 的质数列表。

```objc
// Program 6.10
// 生成质数表的程序
```

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
  @autoreleasepool {
    int p, d, isPrime;

    for ( p = 2; p <= 50; ++p ) {
      for ( d = 2; d < p; ++d ) {
        if ( p % d == 0 )
          isPrime = 0;
      }

      if ( isPrime != 0 )
        NSLog("%i", p);
    }
  }

  return 0;
}
```

## 程序 6.10 输出

```
2
3
5
7
11
13
17
19
23
29
31
37
```

```objc
if ( 100 )
NSLog("This will always be printed.");
```

## 第 6 章 选择

导致了 `NSLog` 语句的执行，因为 `if` 语句中的条件（在本例中为简单值 100）是非零，因此满足了条件。

在本章的每个程序中，我们都使用了“非零表示满足”和“零表示不满足”的概念。这是因为在 Objective-C 中评估任何关系表达式时，如果表达式满足，则赋予其值 1；如果表达式不满足，则赋予值 0。因此，对语句

```objc
if ( number < 0 )
number = -number;
```

的评估过程实际上按如下方式进行：评估关系表达式 `number < 0`。如果满足条件——即 `number` 小于 0——则表达式的值为 1；否则，其值为 0。

该语句测试表达式评估的结果。如果结果非零，则执行紧随其后的语句；否则，跳过该语句。
之前的决策也适用于 `for`、`while` 和 `do-while` 语句内部条件的评估。复合关系表达式（如 `while` 中的表达式）的评估按照之前述概述的方式进行：

```objc
while ( char != '=' && count != 80 )
```

如果两个条件都有效，结果为 1；但如果任一条件无效，评估结果则为 0。`while` 循环终止；否则继续执行。

回到程序 6.10 和标志（flags）的概念，在 Objective-C 中，使用如下表达式来测试标志的值是否为真是完全合法的：

```objc
if ( isPrime )
```

此表达式等同于以下：

```objc
if ( isPrime != 0 )
```

为了方便地测试标志是否为假，我们使用逻辑取反运算符 `!`。在表达式表达式中，我们测试 `isPrime` 的值是否为假（将此语句读为“如果不是 isPrime”）：

```objc
if ( !isPrime )
```

通常，像这样的表达式会对表达式的逻辑值取反：

```
! expression
```

所以，如果 `expression` 为 0，逻辑取反运算符就会产生 1。逻辑取反运算符可以翻转标志的值，如

```objc
my_move = !expression;
```

## 布尔变量

## 137

## 布尔变量

## 121

## 条件运算符

## 123

```objc
s = (x < 0) ? -1 : x;
```

## 布尔变量

## 138

```objc
// Program 6.10
// 生成质数表的程序
```

```objc
p, d, isPrime

Program 6.10
// 生成质数表的程序
#import <Foundation/Foundation.h>

int main(int argc, char * argv[]) {
    @autoreleasepool {
        int p, d, isPrime;

        for ( p = 2; p <= 50; ++p ) {
            for ( d = 2; d < p; ++d ) {
                if ( p % d == 0 )
                    isPrime = 0;
            }

            if ( isPrime == YES )
                NSLog("%i", p);
        }
    }

    return 0;
}
```

## 139

```objc
max_value = ( a > b ) ? a : b;
```

条件 `x < 0` 首先被测试，当之前的语句执行时。通常会在条件周围加上括号以辅助语句的可读性。这通常不需要，因为条件运算符的优先级非常低——实际上比除了赋值运算符和逗号运算符以外的所有运算符都低。

如果 `x` 的值小于 0，则评估 `?` 之后的表达式。该表达式简单的常量整数 -1，当 `x` 小于 0 时赋值给变量 `s`。

如果 `x` 的值小于0，则评估 `:` 之后的表达式。所以如果 `x` 大于等于 0，`x` 的值被赋值给 `s`。

如果 `:` 之后的表达式（else 部分）包含另一个条件运算符，你可以实现 `else if` 子句的效果。例如，程序 6.6 中的 `sign` 函数可以使用两个条件运算符在一行程序中编写，如下：

```objc
sign = ( number < 0 ) ? -1 : (( number == 0 ) ? 0 : 1);
```

如果 `number` 小于0，`sign` 被赋值为 -1；如果 `number` 等于 0，`sign` 被赋值为 0；否则，前一个表达式中 `else` 部分的括号实际上是不必要的。这是因为条件运算符从右到左关联，这意味着单个表达式中多次使用该运算符，如下

```
el1 ? e2 : e3 ? e4 : e5
```

它们从右到左分组并按如下评估：

```
el1 ? e2 : ( e3 ? e4 : e5 )
```

## 练习

- 1. 编写一个程序，要求用户输入两个整数值。测试这两个数字，确定第一个是否能被第二个数字整除，然后在终端显示适当的消息。
- 2. 程序 6.8A 即使输入了无效运算符或尝试除以零，也会显示累加器中的值。修复这个问题。
- 3. 修改 `Fraction` 类的 `print` 方法，使整数以整数的形式显示（例如分数 5/1 应该显示为简单的 5）。同时修改该方法，将分子为 0 的分数显示为简单的零。
- 4. 编写一个作为简单打印计算器的程序。该程序应允许用户输入如下格式的表达式：

```
operator
```

程序应识别以下运算符：

```
+ - * / E
```

`S` 运算符告诉将累加器设置为输入的数字，`E` 运算符告诉程序执行结束。算术运算在累加器的内容上进行，并将输入的数字作为第二个操作数。以下是一个运行示例，展示了程序应该如何运行：

```
Begin Calculations
```



# 练习题

## 计算器程序示例

```text
10 Set Accumulator to 10
= 10.0000000 Contents of Accumulator
2 / Divide by 2
= 5.0000000 Contents of Accumulator
55 - Subtract 55
= -50.000000
100.25 Set Accumulator to 100.25
= 100.250000
4 * Multiply by 4
= 401.000000
0 E End of program
= 401.000000
End Calculations.
```

让程序能够检测除以零的情况，并检查未知运算符。注意：使用在程序 6.8 中开发的 `Calculator` 类来执行计算。注意：记得在 `scanf` 格式字符串中使用空格字符（例如 `"%f %c"`）来跳过输入中的空白字符。

## 练习 5

我们开发了程序 5.9 来反转在终端输入的整数的数字位。然而，如果你输入负数，该程序运行得并不好。找出在这种情况下会发生什么，然后修改程序以正确处理负数。这意味着，如果用户输入 `-8645`（例如），程序的输出应该是 `5468`。

## 练习 6

编写一个程序，获取终端输入的整数，并提取并显示整数的每个数字的英文名称。如果用户输入 `932`，程序应该显示如下：

```text
nine
three
two
```

（记住，如果用户只输入 `0`，要显示零。）注意：这个练习很有挑战性！

## 练习 7

程序 6.10 有几处低效的地方。其中一个低效源于检查偶数。由于任何大于 2 的偶数显然不可能是质数，程序可以简单地跳过所有可能的质数和可能的因子。内部循环也是低效的，因为 `p` 的值总是除以从 2 到 `p-1` 的所有 `d` 值。如果你在 `for` 循环的条件中添加对 `isPrime` 值的测试，就可以避免这种低效。通过这样，你可以设置 `for` 循环，只要没有找到因子且 `d` 的值小于 `p`，循环就继续。修改程序 6.10 以包含这两个更改；然后运行程序以验证其操作。

# 第 7 章 类进阶

在本章中，你将继续学习如何处理类以及编写方法。你还将应用在上一章中学到的某些概念，例如完成程序循环、做出决策以及处理表达式。首先，我们讨论如何将程序拆分为多个文件，以便更容易处理大型程序。

## 分离接口文件和实现文件

是时候习惯将类声明和定义放在不同的文件中了。如果你正在使用 Xcode，创建一个名为 `FractionTest` 的新项目。在 `main.m` 文件输入输入程序。

### 程序 7.1 主测试程序：`main.m`

```objectivec
#import "Fraction.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *myFraction = [[Fraction alloc] init];
        // 将分数设置为 1/3
        [myFraction setNumerator: 1];
        [myFraction setDenominator: 3];
        // 显示分数
        NSLog(@"The value of myFraction is:%@");
        [myFraction print];
    }
    return 0;
}
```

注意，此文件不包含 `Fraction` 类的定义。然而，它导入了一个名为 `Fraction.h` 的文件。

通常，类声明（即 `@interface` 部分）存放在它自己的文件中，命名为 `class.h`。定义（即 `@implementation` 部分代码）通常存放在同名的文件中，使用扩展名 `.m`。因此，让我们 `Fraction` 类的声明放在 `Fraction.h` 文件中，将定义放在 `Fraction.m` 中。

要在 Xcode 中执行此操作，从菜单中选择 `New File`。在左窗格中，选择 `Cocoa Touch`。在右上窗格中，选择 `Objective-C`。你的窗口应该如图 1 所示。

请再次注意，测试程序 `main.m`（在本章开头显示）包含了接口文件 `Fraction.h`，而不是实现文件 `Fraction.m`。接口部分提供了当你需要在另一个文件中使用该类时，编译器需要的所有关于类的信息。实现部分包含了方法的实际代码，Xcode 在你构建应用程序时会负责将这些代码与你编写任何其他代码包含在一起。接口文件包含类的公共信息——即你与类的用户共享的信息。另一方面，实现部分包含私有信息——实例变量和代码。

> **注意事项**
>
> 事实上，代码可能存储在其他地方，例如 Framework 库，当在你构建应用程序时，Xcode 会自动从库中提取它。

现在，你已经将程序拆分成了三个独立的文件。对于一个小型程序来说，这似乎很繁琐，但当你开始处理更大的程序并与其他程序员共享类声明时，它的用处就会显而易见。

你现在可以像以前一样编译并运行程序：从 Product（产品）菜单中选择 Run（运行），或直接点击工具栏上的 Run 按钮。

如果你是从命令行编译程序，请给 Objective-C 编译器提供两个 `.m` 文件名。使用 Clang 时，命令行看起来如下：

```bash
clang -fobjc-arc -framework Foundation Fraction.m main.m -o FractionTest
```

这将构建一个可执行文件 `FractionTest`。这里是运行程序后的输出。

### 程序 7.1 输出

```text
myFraction 的值是：
1/3
```

## 合成访问方法

从 Objective-C 2.0 开始，你可以让系统自动为你生成 setter 和 getter 方法（统称为访问方法）。到目前为止，我们还没有展示如何这样做，因为学习如何编写这些方法对你来说很重要。这是语言提供的一项非常方便的功能，所以现在是时候学习如何利用这一特性了。

第一步是在你的接口部分使用 `@property` 指令来标识你的属性。这些属性的命名通常与你的实例变量相同，尽管不必如此。在我们的 `Fraction` 类中，两个实例变量 `numerator` 和 `denominator` 就属于这一类。以下是添加了新 `@property` 指令的新接口部分。

```objectivec
@interface Fraction : NSObject
@property int numerator, denominator;
-(void) print;
-(double) convertToNum;
@end
```

注意，我们不再包含 getter 和 setter 方法的定义：`numerator`、`denominator`、`setNumerator:` 和 `setDenominator:`。我们将让 Objective-C 编译器自动为我们生成或合成这些方法。这是如何实现的？只需在实现部分使用 `@synthesize` 指令即可，所示。

```objectivec
#import "Fraction.h"

@implementation Fraction
@synthesize numerator, denominator;

-(void) print {
    NSLog("%i/*%i", numerator, denominator);
}

-(double) convertToNum {
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}
@end
```

注意，当你使用 `@property` 指令时，不再需要在实现部分中声明相应的实例变量。如果你想的话可以仍然声明，但不再是必须的，因为编译器会处理这一点。

接下来的这一行告诉 Objective-C 编译器为两个属性 `numerator` 和 `denominator` 生成一对 getter 和 setter 方法：

```objectivec
@synthesize numerator, denominator;
```

通常情况下，如果你有一个属性 `x`，在实现部分包含以下行，就会调用编译器自动合成一个名为 `x` 的 getter 方法和一个名为 `setX` 的 setter 方法。

```objectivec
@synthesize x;
```

尽管这看起来可能不是大事，但让编译器为你做这件事是值得的，生成的访问方法将是高效的，并且可以在多线程、多机器、多核心上安全运行。

现在回到程序 7.1，并按照指示对接口和实现部分进行更改，以便为你为你合成访问方法。验证在不对 `main.m` 进行任何更改的情况下，你仍然从程序获得相同的输出。

## 使用点操作符访问属性

Objective-C 语言允许你使用更方便的语法访问属性。要获取存储在 `myFraction` 中的 `numerator` 的值，你可以这样写：

```objectivec
[myFraction numerator]
```

这会将 `numerator` 发送到 `myFraction` 对象，从而返回所需的值。在 Objective-C 中，你也可以写以下等效表达式：

```objectivec
myFraction.numerator
```

这里的通用格式是：

```objectivec
instance.property
```

你也可以使用类似的语法来赋值：

```objectivec
instance.property = value
```

这等同于编写表达式：`[instance setProperty:value]`

在程序 7.1 中，使用以下代码行将你的分数的分子和分母设置为 1/3：

```objectivec
[myFraction setNumerator: 1];
[myFraction setDenominator: 3];
```

这里是编写这相同的两行的等效方法：

```objectivec
myFraction.numerator = 1;
myFraction.denominator = 3;
```

在本文的剩余部分，我们将使用这些特性来合成方法并通过点操作符访问属性。值得注意的是，如果你有一个 getter 方法，你就可以在你通常编写的方法中使用点操作符，写出这样的表达式。

## 添加新方法

接下来，在实现文件中添加新方法的定义。

### 程序 7.2 实现文件：`Fraction.m`

```objectivec
#import "Fraction.h"

@implementation Fraction
@synthesize numerator, denominator;

-(void)print {
    NSLog("%i/%i", numerator, denominator);
}

-(double)convertToNum {
    if (denominator != 0)
        return (double)numerator / denominator;
    else
        return NAN;
}

-(void)setTo:(int)n over:(int)d {
    numerator = n;
    denominator = d;
}
@end
```

`setTo:over:` 方法简单地将它的两个整数参数 `n` 和 `d` 赋值给分数的对应的实例变量 `numerator` 和 `denominator`。这里有一个测试程序可以用来尝试你的新方法：

### 程序 7.2 测试文件：`main.m`

```objectivec
#import "Fraction.h"

int main(int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc] init];
        [aFraction setTo:100 over:200];
        [aFraction print];
        [aFraction setTo:1 over: 3];
        [aFraction print];
        return 0;
    }
}
```

### 程序 7.2 输出

```text
100/200
1/3
```

## 不带参数名称的方法

在创建方法名称时，参数名称实际上是可选的。例如，你可以这样声明一个方法：

```objectivec
- (int) set: n: (int) d;
```

注意，与之前的示例不同，这里为方法的第二个参数没有提供名称。这个方法被命名为 `set::`，两个冒号意味着该方法接受两个参数，尽管它们并不是都经过命名。

要调用 `set::` 方法，你使用冒号作为参数分隔符，如下所示：

```objectivec
[aFraction set: 1 : 3];
```

在编写新方法时省略参数名称不是良好的编程风格，因为这会让程序更难以追踪，并让方法参数的意图不够直观。

## 分数上的操作

让我们继续处理 `Fraction` 类。首先，你将编写一个方法，允许你将一个分数加到另一个分数上。你将该方法命名为 `add:`，并接受一个分数作为参数。以下是新方法的声明：

```objectivec
-(void) add: (Fraction*) f;
```

注意参数 `f` 的声明：`(Fraction*) f`。这表示 `add:` 方法的参数是指向 `Fraction` 类对象的引用。星号是必要的，因此以下声明是不正确的：`(Fraction) f`。

你将把分数作为参数传递给你的 `add:` 方法，并将让该方法将其加到消息的接收者上；以下消息表达式将 `Fraction bFraction` 加到 `Fraction aFraction` 上：

```objectivec
[aFraction add: bFraction];
```

作为一个快速复习，要相加分数 `a/b` 和 `c/d`，你执行以下计算：

```text
a/b + c/d = (ad + bc)/bd
```

将此新方法的代码放在 `@implementation` 部分：

```objectivec
// 将一个分数加到接收者上
-(void) add:(Fraction*)f {
    // 加两个分数：
    // a/b + c/d = ((a*d) + (b*c)) / (b*d)
    numerator = numerator * f.denominator + denominator * f.numerator;
    denominator = denominator * f.denominator;
}
```

不要忘记你可以通过其字段 `numerator` 和 `denominator` 来引用消息的接收者 `Fraction`。换句话说，在 `add:` 方法内部，你通过名称引用你发送消息的对象的实例变量。

另一方面，你不能以那种方式引用参数 `f` 的实例变量。相反，你必须通过它的名称 `f` 来识别对象。然后你可以通过点运算符访问 `f` 来获取相应的实例变量（或通过向 `f` 发送适当的消息）。

因此，`add:` 方法中的第一条语句：

```objectivec
numerator = numerator * f.denominator + denominator * f.numerator;
```

意思是：取第一个分数（消息的接收者）的分子，乘以参数的分母（`numerator * f.denominator`），并将该结果与接收者的分母与参数的分子的乘积相加（`denominator * f.numerator`）。相加最终结果随后存储在接收者的分子中。这里的关键在于，你要完全理解何时在引用接收者，何时在引用参数。

假设你已经为接口和实现文件添加了新 `add:` 方法之前的声明和定义。程序 7.3 是一个示例测试和输出。

### 程序 7.3 测试文件：`FractionTest.m`

```objectivec
#import "Fraction.h"

int main (int argc, char *[]) {
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc] init];
        Fraction *bFraction = [[Fraction alloc] init];
        // 将两个分数设置为 1/4 和 1/2 并它们相加
        [aFraction setTo:1 over: 4];
        [bFraction setTo:1 over: 2];
        // 打印结果
        [aFraction print];
        NSLog("%@*s");
        [bFraction print];
        NSLog("%@*s");
        [aFraction add:bFraction];
        [aFraction print];
    }
    return 0;
}
```

### 程序 7.3 输出

```text
1/4
+
1/2
=
3/4
```

测试程序是直接的。两个分数，名为 `aFraction` 和 `bFraction`，被分配并初始化。将两个分数设置为 1/4 和 1/2 并它们相加。注意，在 `add:` 方法中，你修改了接收者的值。此外，在调用 `add:` 方法之前，你显示了 `aFraction` 的值。

## 局部变量

你用于引用方法的参数名称也是局部变量。当方法执行时，传递给方法的参数会被复制到这些变量中。由于方法处理的是参数的副本，它无法更改原始值。假设你有一个如下定义的 `calculate` 方法：

```objectivec
(void) calculate:(double)x {
    x *= 2;
}
```



另外假设你使用以下消息表达式调用它：
`[myData calculate:ptVal];`

当方法执行时，包含在变量 `ptVal` 中的内容被复制到局部变量 `x`。在 `calculate` 内部修改 `x` 的值对 `ptVal` 产生影响。

## 第 7 章 类进阶

```objc
++pageCount;
...
return pageCount;
}
```

局部静态变量在程序启动时仅会被设置为 0，并且在连续调用 `showPage` 方法时保留其值。
将 `pageCount` 设为局部静态变量与将其设为实例变量之间的区别。在前一种情况下，`pageCount` 计算的是所有调用 `showPage` 方法的对象打印的页面数。在后一种情况下，变量将计算每个单独对象打印的页面数，因为每个对象都拥有自己的 `pageCount` 副本。

请记住，静态变量和局部变量只能在定义它们的方法内部被访问。因此，静态变量 `pageCount` 只能在 `showPage` 内部被访问。你可以在任何方法之外声明该变量（通常在你的实现文件开头），以便让任何方法都能访问它，例如：

```objc
#import "Printer.h"

static int pageCount;
```

```objc
@implementation Printer
...
@end
```

现在，文件中包含的任何实例方法或类方法都可以访问 `pageCount` 变量。第 10 章“变量与数据类型进阶”将更详细地介绍变量作用域主题。

回到函数，你可以将 `reduce` 方法的代码整合到你的 `Fraction.m` 实现文件中。别忘了在 `Fraction.h` 接口文件中也声明 `reduce` 方法。这样，你就可以在程序 7.4 中测试你的新方法了。在这里我们展示了所有三个文件：接口文件、实现文件和测试程序。

## 程序 7.4 接口文件：Fraction.h

```objc
#import <Foundation/Foundation.h>

// 定义 Fraction 类

@interface Fraction : NSObject

@property numerator, denominator;

-(void) print;

-(void) setTo:(int)n over:(int)d;

-(double) convertToNum;

-(void) add:(Fraction *)f;

-(void) reduce;

@end
```

## 程序 7.4 实现文件：Fraction.m

```objc
#import "Fraction.h"

@implementation Fraction

@synthesize numerator, denominator;

-(void) print {
    NSLog("%i/%i", numerator, denominator);
}

-(double) convertToNum {
    if (denominator != 0)
        return (double) numerator / denominator;
    else
        return NAN;
}

-(void) setTo:(int)n over:(int)d {
    numerator = n;
    denominator = d;
}

// 向接收者添加一个 Fraction

-(void) add:(Fraction *) f {
    // 相加两个分数：
    // a/b = c/d = ((a*d) + (b*c)) / (b * d)
    numerator = numerator * f.denominator + denominator * f.numerator;
    denominator = denominator * f.denominator;
}

-(void) reduce {
    int u = numerator;
    int v = denominator;
    int temp;

    while (v != 0) {
        temp = u % v;
        u = v;
        v = temp;
    }

    numerator /= u;
    denominator /= u;
}

@end
```

## 程序 7.4 测试文件 main.m

```objc
#import "Fraction.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *aFraction = [[Fraction alloc] init];
        Fraction *bFraction = [[Fraction alloc] init];

        [aFraction setTo:1 over:4]; // 将第一个分数设置为 1/4
        [bFraction setTo:1 over:2]; // 将第二个分数设置为 1/2

        [aFraction add:bFraction];

        [aFraction add:bFraction]; // 输出加法结果
        [aFraction print];
    }
    return 0;
}
```

## 扩展类定义与接口文件

因此，`resultFraction` 结束存储我们在 `add:` 方法中分配的 `Fraction` 对象的引用。

你已经开发了一个用于处理分数的的方法库。事实上，这里是接口文件的完整列表，你可以看到你通过这个类所实现的所有成就：

```objc
#import <Foundation/Foundation.h>

@interface Fraction : NSObject

@property int numerator, denominator;

-(void) print;
-(void) setTo:(int)n over:(int)d;
-(double) convertToNum;
-(void) add:(Fraction *)f;
-(void) reduce;

@end
```

你可能不需要处理分数，但这些示例展示了你如何通过添加新方法来不断完善和扩展一个类。你可以将此接口文件交给另一个处理分数的人员，这对于那个人编写处理分数的程序来说已经足够了。如果那个人需要添加新方法，他可以直接通过扩展自己的子类并添加新方法来完成。你将在下一章中学习如何这样做。

## 练习题

- 1. 为 `Fraction` 类添加方法以完善分数的算术运算。在每个情况下都对方法内的结果进行约分：
  `// subtract:(Fraction *) f;`
  `// 将接收者乘以参数；`
  `-(Fraction *) multiply:(Fraction *) f;`
  `// 将接收者除以参数；`
  `-(Fraction *) divide:(Fraction *) f;`

- 2. 修改你的 `Fraction` 类中的 `print` 方法，使其接受一个额外的 `BOOL` 参数，指示分数在显示时是否应该约分。如果需要约分（如果参数为 `YES`），请确保不要对分数本身进行任何永久更改。

- 3. `Fraction` 类能处理负分数吗？例如，你可以加上 -1/4 和 -1/2 并得到正确的结果吗？当你认为有了答案时，写一个测试程序来尝试。

- 4. 修改 `Fraction` 的 `print` 方法，将大于 1 的分数以混合数的形式显示。例如，分数 5/3 应该显示为 1 2/3。

- 5. 第四章“数据类型与表达式”中的练习 6 定义了一个用于处理复数的类 `Complex`。添加一个名为 `add` 的新方法，用于相加两个复数。相加时分别加上实部和虚部，如下：

```
(5.3 + 7i) + (2.7 + 4i) = 8 + 11i
```

根据以下方法声明，让 `add:` 方法存储并返回作为一个新 `Complex` 数的结果：
`-(Complex *) add: (Complex *) complex;`

- 6. 结合第四章练习 6 开发的 `Complex` 类以及本章练习 6 中的扩展，创建单独 `Complex.h` 和 `Complex.m` 接口和实现文件。创建一个测试程序文件来测试一切。

# 第 8 章 继承

在本章中，你将学习使面向对象编程如此强大的关键原理之一。通过继承的概念，你将在现有的类定义的基础上进行构建，并为你自己的应用程序进行定制。

## 一切从根部开始

你在第三章“类、对象与方法”中学习了父类（parent class）的概念。一个没有父类的类本身位于层次结构的顶端，被称为根类（root class）。在 Objective-C 中，你有能力定义自己的根类，但你通常不想这样做。相反，你将希望利用现有的类。到目前为止我们定义的所有类都是根类 `NSObject` 的后代，你已经在接口文件中指定了它：

```objc
@interface Fraction: NSObject
@end
```

`Fraction` 类派生自 `NSObject`。由于 `NSObject` 位于层次结构的顶端（即它上方没有其他类），它被称为根类，如图 8.1 所示。`Fraction` 类被称为子类（child or subclass）。

![](img/22d1310b7c22ea2d48cd2058929a5cda_167_0.png)

图 8.1 根类与子类

## 第 8 章 继承

从术语的角度来看，我们可以谈论类、子类和父类。类似地，我们可以谈论类、子类和子类。你将熟悉这两种术语。

每当定义一个新类（新根类除外）时，该类都会继承某些内容。例如，来自父类的（非私有的）实例变量和方法隐式地成为新类定义的一部分。这意味着子类可以访问这些方法和实例变量，就像它们是直接定义在类定义中一样。

请注意，要让子类直接访问的实例变量必须在接口部分声明，而不是像我们整本书中所做的那样在实现部分声明。在实现部分声明或合成的实例变量是私有实例变量，子类无法直接访问。相反，你将希望使用它们显式定义或合成的 getter 和 setter 来访问它们的值。

一个简单的例子（尽管是人为构造的）有助于说明继承这一核心概念。这里有一个对象类 `ClassA` 的声明，它包含一个名为 `initVar` 的方法（注意这里我们在接口部分声明了实例变量 `x`，以便子类访问）：

```objc
@interface ClassA: NSObject
  int x;
  -(void) initVar;
@end
```

`initVar` 方法简单地将 `ClassA` 实例变量的值设置为 100：

```objc
@implementation ClassA
-(void) initVar {
  x = 100;
}
@end
```

现在让我们也定义 `ClassB`：

```objc
@interface ClassB: ClassA
-(void) printVar;
@end
```

```objc
@implementation ClassB
-(void) printVar {
    NSLog("%d", x);
}
@end

int main (int argc, char *argv[]) {
    @autoreleasepool {
        ClassB *b = [[ClassB alloc] init];
        [b initVar];
        [b printVar];
    }
    return 0;
}
```

## 程序 8.1 输出

```
x = 100
```

检查父类。如果定义了该方法，则使用该方法。如果未定义，则继续搜索。

会一直检查父类，直到发生以下两种情况之一：要么找到一个包含指定方法的类，要么在回溯到根类后仍未找到该方法。如果发生了第一种，你就大功告成了；如果发生了第二种，你就有问题，并会生成如下所示的警告消息：

```
warning: `ClassB` may not respond to `-inity`
```

在这种情况下，你无意中尝试向一个类型为 `ClassB` 的变量发送名为 `inity` 的消息。编译器会告诉你，来自该类的对象不知道如何响应此类方法。这是在检查了 `ClassB` 的方法及其回溯到根类的父类方法后得出的（在本例中，根类是 `NSObject`）。

你将在第 9 章“多态、动态类型和动态绑定”中学习更多关于系统如何检查执行的正确方法的知识。

## 通过继承扩展：添加新方法

继承通常用于扩展类。例如，假设你被分配了任务，开发一些类来处理 2D 图形对象，如矩形、圆形和三角形。目前，我们只需关注矩形。回到第 4 章“数据类型和表达式”中的练习，并从

```objc
@interface Rectangle: NSObject
@property width, height;
-(int) area;
-(int) perimeter;
@end
```

你已经合了设置矩形宽度和高度以及返回这些值的方法，以及你自己计算其面积和周长的方法。让我们添加一个方法，允许你通过同一次消息调用设置矩形的宽度和高度，如下所示：

```objc
-(void) setWidth:(int)w andHeight:(int)h;
```

假设你将这个新类声明写在一个名为 `Rectangle.h` 的文件中。以下是实现文件 `Rectangle.m` 的可能样子：

```objc
#import "Rectangle.h"
@implementation Rectangle
@synthesize width, height;

-(void) setWidth:(int)w andHeight:(int)h {
  width = w;
  height = h;
}

-(int) area {
  return width * height;
}

-(int) perimeter {
  return (width + height) * 2;
}
@end
```

每个方法的定义都足够直接。程序 8.2 显示了一个用于测试它的主例程。

## 程序 8.2

```objc
#import "Rectangle.h"
int main (int argc, char * argv[]) {
  @autoreleasepool {
    Rectangle *myRect = [[Rectangle alloc] init];

    [myRect setWidth: 5 andHeight: 8];

    NSLog(@"Rectangle: w = %i, h = %i", myRect.width, myRect.height);
    NSLog(@"Area = %i, Perimeter = %i", [myRect area], [myRect perimeter]);
  }
  return 0;
}
```

## 程序 8.2 输出

```
Rectangle: w = 5, h = 8
Area = 40, Perimeter = 26
```

`myRect` 被分配并初始化；然后将其宽度设置为 5，高度设置为 8。输出的第一行验证了这一点。接下来，通过适当的消息调用计算矩形的面积和周长，并将返回的值传递给 `NSLog` 进行显示。

假设你需要处理正方形。你可以定义一个名为 `Square` 的新类，并在其中定义与你的 `Rectangle` 类类似的方法。或者，你可以意识到正方形只是矩形的一种特殊情况，宽度和高度恰好相同。

因此，处理这种情况的一种简单方法是创建一个名为 `Square` 的类并使其成为 `Rectangle` 的子类。目前，你可能想要添加的方法是将正方形的边长设置为特定值并获取该值。程序 8.3 显示了你新类 `Square` 的接口和实现文件。

## 程序 8.3 Square.h 接口文件

```objc
#import "Rectangle.h"

@interface Square: Rectangle

-(void) setSide:(int) s;
-(int) side;
@end
```

## 程序 8.3 Square.m 实现文件

```objc
@implementation Square

-(void) setSide:(int) s {
    [self setWidth:s andHeight:s];
}

-(int) side {
    return self.width;
}
@end
```

`Square` 类是 `Rectangle` 的子类，在头文件 `Rectangle.h` 中声明。你不需要在这里添加任何实例变量，但你确实添加了名为 `setSide:` 和 `side` 的新方法。注意，`side` 方法无法直接访问 `Rectangle` 的 `width` 变量；它是私有的，因此 `Square` 类无法访问。然而，getter 方法是从父类继承的，可以访问 `width` 的值。

你可能记得编写表达式 `self.width` 等同于编写 `[self width]`。这向 `side` 消息的接收者发送 `width` 消息。换句话说，你执行的是 getter 方法 `width`，而不是直接访问实例变量 `width`（正如你所讨论的，你可以这样做）。这是一个你需要理解的重要概念。

正方形只有一条边，但你将其表示为两条，这对于 `Square` 类的用户是可以接受的。`setSide` 利用了你已经拥有的 `Rectangle` 类的方法来设置宽度和高度。如果你正在编写一个绘图应用程序，这个点可能代表矩形在窗口中的位置，正如图 8.4 所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_176_0.png)

图 8.4 在窗口中绘制的矩形

在图 8.4 中，矩形的原点显示在 (x1,y1)。

你可以扩展 `Rectangle` 类，将矩形原点的 x, y 坐标存储为两个单独的值。你可能会意识到，在开发图形应用程序时，你需要处理大量的坐标，因此定义名为 `XYPoint` 的类（你可能在第 3 章练习 7 中遇到过这个题）：



```objc
#import <Foundation/Foundation.h>
```

```objc
@interface XYPoint: NSObject
@property int x, y;
-(void) setX:(int) xVal andY:(int) yVal;
@end
```

# 第 8 章 继承

## 点类与对象分配

`Rectangle` 类存储矩形的尺寸。在现实世界的图形应用程序中，你可能需要跟踪各种额外信息，例如矩形的填充颜色、线条颜色、窗口内的位置（原点）等。你可以轻松地扩展类来处理矩形原点的概念。假设“原点”意味着矩形在某个笛卡尔坐标系 (x,y) 中的左下角位置。如果你正在编写一个绘图应用程序，这个点可能代表矩形在窗口中的位置，正如图 8.4 所示。

`setSide` 利用了你已经拥有的 `Rectangle` 类的方法来设置宽度和高度。对于 `Square` 类的用户来说，你不需要做其他操作。`setSide` 对于你的新类 `Square` 输出。

## 程序 8.3 测试程序

```objc
#import "Square.h"
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        Square *mySquare = [[Square alloc] init];
        [mySquare setSide:5];
        NSLog(@"Area = %i, Perimeter = %i", [mySquare area], [mySquare perimeter]);
    }
    return 0;
}
```

## 程序 8.3 输出

```
Square = 5
Area = 25, Perimeter = 20
```

## 通过继承扩展：添加新方法

现在回到你的 `Rectangle` 类。你想要存储矩形的原点，因此你会在 `Rectangle` 类定义中添加一个名为 `origin` 的实例变量：

```objectivec
@implementation Rectangle
{
  XYPoint *origin;
  ...
}
```

添加一个方法来设置和获取矩形的原点似乎是合理的。为了说明一个重要的点，我们现在不会为 `origin` 生成访问器方法。相反，我们将手动编写它们。

### @class 指令

现在你可以处理矩形（以及正方形！）并能够设置它们的宽度、高度和原点。首先，让我们完整查看你的 `Rectangle.h` 接口文件：

```objc
#import <Foundation/Foundation.h>

@class XYPoint;

@interface Rectangle: NSObject
@property int width, height;

-(XYPoint *) origin;
-(void) setOrigin:(XYPoint *) pt;
-(void) setWidth:(int) w andHeight:(int) h;
-(int) area;
-(int) perimeter;
@end
```

你在 `Rectangle.h` 头文件中使用了一个新指令：

```objc
@class XYPoint;
```

你需要这样做是因为编译器在遇到 `XYPoint` 为 `Rectangle` 定义的某个实例变量之一时，需要知道 `XYPoint` 是什么。类名也分别用于你的 `setOrigin:` 和 `origin` 方法的参数和类型声明。你还有另一种选择：你可以转而导入头文件，如下：

```objc
#import "XYPoint.h"
```

使用 `@class` 指令更高效，因为编译器不需要导入并处理整个 `XYPoint.h` 文件（尽管它很小）；它只需要知道 `XYPoint` 是一个类的名称。如果你需要引用 `XYPoint` 类的某个方法（例如在实现部分），那么 `@class` 指令将是不够的，因为编译器需要更多信息；它需要知道该方法接受多少个参数、这些参数的类型是什么，以及方法的返回类型是什么。

所以，确保你理解这里使用 `@class` 指令的作用。它只是在告诉编译器 `XYPoint` 是一个类的名称。这样，当它看到这一行时：

```objectivec
XYPoint *origin;
```

它知道 `origin` 是来自名为 `XYPoint` 的类的对象。这就是编译器在该点需要知道的所有信息。

让我们填充 `XYPoint` 类和 `Rectangle` 方法的空白，以便你可以在程序中测试一切。

首先，程序 8.4 显示了 `Rectangle` 类的新方法。

```objectivec
// Program 8.4 Rectangle.m 添加的方法
#import "XYPoint.h"

-(void) setOrigin:(XYPoint *) pt
{
  origin = pt;
}

-(XYPoint *) origin
{
  return origin;
}
@end
```

接下来是完整的 `XYPoint` 和 `Rectangle` 类定义，其之后是一个用于尝试它们的测试程序。

### 程序 8.4 XYPoint.h 接口文件

```objc
#import <Foundation/Foundation.h>

@interface XYPoint: NSObject
@property int x, y;
-(void) setX:(int) xVal andY:(int) yVal;
@end
```

### 程序 8.4 XYPoint.m 实现文件

```objectivec
#import "XYPoint.h"

@implementation XYPoint
@synthesize x, y;

-(void) setX:(int) xVal andY:(int) yVal
{
  x = xVal;
  y = yVal;
}
@end
```

### 程序 8.4 Rectangle.h 接口文件

```objc
#import <Foundation/Foundation.h>

@class XYPoint;

@interface Rectangle: NSObject
@property int width, height;

-(XYPoint *) origin;
-(void) setOrigin:(XYPoint *) pt;
-(void) setWidth:(int) w andHeight:(int) h;
-(int) area;
-(int) perimeter;
@end
```

### 程序 8.4 Rectangle.m 实现文件

```objectivec
#import "Rectangle.h"

@implementation Rectangle
{
  XYPoint *origin;
}

@synthesize width, height;

-(void) setWidth:(int) w andHeight:(int) h
{
  width = w;
  height = h;
}

-(void) setOrigin:(XYPoint *) pt
{
    origin = pt;
}

-(int) area
{
    return width * height;
}

-(int) perimeter
{
    return (width + height) * 2;
}

-(XYPoint *) origin
{
    return origin;
}
@end
```

### 程序 8.4 测试程序

```objectivec
#import "Rectangle.h"
#import "XYPoint.h"

int main (int argc, char *argv[]) {
    @autoreleasepool {
        Rectangle *myRect = [[Rectangle alloc] init];
        XYPoint *myPoint = [[XYPoint alloc] init];

        [myPoint setX:100 andY:200];
        [myRect setOrigin:myPoint];
        [myRect setWidth:5 andHeight:8];

        NSLog(@"w = %d, h = %d", myRect.width, myRect.height);
        NSLog(@"Origin at %p", (void *)myRect.origin);
        NSLog(@"Area = %d", [myRect area]);
        NSLog(@"Perimeter = %d", [myRect perimeter]);
    }
    return 0;
}
```

```cpp
[origin set pt.x and pt.y]
// error: member 'x' is something not a structure or union
// error: member 'y' is something not a structure or union
// error to 'set' not found
// without a matching method signature will be assumed to return 'int' and '...' as arguments.
```

图 8.8 编译器错误信息

哎呀！问题在于，你在修改后的方法中引用了 `XYPoint` 类的一些实例变量，因此编译器需要比 `@class` 指令更多的信息。在这种情况下，你必须回到你的 `Rectangle.h` 头文件，并将该指令替换为导入（import），如下所示：

```objc
#import "XYPoint.h"
```

## 程序 8.5B 输出

```
原点 at (100, 200)
Origin at (100, 200)
```

在离开本节之前，让我们考虑 `Rectangle` 类的访问器（getter）部分。假设在程序 8.4 的测试程序中，你在设置 `Rectangle` 的值之后插入了以下行代码：

```objective-c
XYPoint *theOrigin = myRect.origin;
theOrigin.x = 200;
theOrigin.y = 300;
```

你认为这段代码执行后 `myRect.origin` 会发生什么变化？没错，它的原点会被改变为 (200, 300)。访问器返回的原点对象是“脆弱的”。任何人都可以据此更改它的 x 或 y 值。出于这个原因，编写返回对象的访问器最安全的方法是创建一个对象的副本并返回副本。这样，你就可以保护实例变量不被意外修改。我们在这里不会做此更改，将其留作你自己的练习。请注意，如果你在返回对象之前对其复制，将会面临性能开销。在设计类时，你需要判断这种权衡是否值得。

## 重写方法

我们在在本章早些时候提到，你不能通过继承来移除或减去方法。然而，你可以通过重写来改变继承方法的定义。

回到你的两个类 `ClassA` 和 `ClassB`，假设你想为 `ClassB` 编写自己的 `initVar` 方法。你已经知道 `ClassB` 将继承在 `ClassA` 中定义的 `initVar` 方法，但你可以创建一个同名的新方法来替换继承的方法吗？答案是肯定的，你通过定义一个同名的新方法来实现。与父类同名的方法将替换、重写继承的定义。你的新方法必须与你正在重写的方法具有相同的返回值，并带有相同数量和类型的参数。

程序 8.6 显示了一个简单的示例来说明这一概念。

```objective-c
// Program 8.6
#import <Foundation/Foundation.h>

// ClassA 声明和定义
@interface ClassA: NSObject
{
    int x; // 将被子类继承
}
-(void) initVar;
@end

@implementation ClassA
-(void) initVar
{
    x = 100;
}
@end

// ClassB 声明和定义
@interface ClassB: ClassA
-(void) initVar;
-(void) printVar;
@end

@implementation ClassB
-(void) initVar // 添加的方法
{
    x = 200;
}

-(void) printVar
{
    NSLog(@"x = %i", x);
}
@end

int main (int argc, char * argv[]) {
    @autoreleasepool {
        ClassB *b = [[ClassB alloc] init];
        [b initVar]; // 使用 B 中的重写方法
        [b printVar]; // 显示 x 的值;
        return 0;
    }
}
```

## 程序 8.6 输出

```
x = 200
```

显然，消息 `[b initVar]` 导致了 `ClassB` 中定义的 `initVar` 方法被使用，而不是像上一个例子那样使用 `ClassA` 中定义的那个。图 8.9 释了这一点。

| | 实例变量 | 方法 |
|---|---|---|
| 对象 | | |
| ClassA | x | initVar |
| ClassB | x | initVar, printVar |

图 8.9 重写 initVar 方法

### 哪个方法被选中了？

我们涵盖了系统如何使用层级结构来将方法应用到对象上。如果你在不同的类中有同名方法，则正确方法的选择将基于消息接收者的类。程序 8.7 使用了与之前相同的 `ClassA` 和 `ClassB` 的类定义。

```objective-c
// Program 8.7
#import <Foundation/Foundation.h>

// 插入 ClassA 和 ClassB 的定义

int main (int argc, char *argv[]) {
    @autoreleasepool {
        ClassA *a = [[ClassA alloc] init];
        ClassB *b = [[ClassB alloc] init];

        [a initVar]; // 使用 ClassA 方法
        [a printVar]; // 显示 x 的值;

        [b initVar]; // 使用重写的 ClassB 方法
        [b printVar]; // 显示 x 的值;
    }
    return 0;
}
```

当你编译此程序时，你会得到此警告信息：

```
warning: 'ClassA' may not respond to '-printVar'
```

发生了什么？查看 `ClassA` 的声明和定义：

```objective-c
@interface ClassA: NSObject
{
    int x;
}
-(void) initVar;
@end
```

在定义子类时，你不仅可以添加新方法，还可以添加新的实例变量。在两种情况下，效果都是累积的。你永远无法通过继承来减去方法或实例变量；你只能添加——在方法的情况下，即重写。

所以，回顾一下，你想创建一个子类？

- 你想通过添加一些新方法或实例变量来扩展类的功能。
- 你想创建一个类的特殊版本（例如，某种类型的图形对象）。
- 你需要通过重写一个或多个方法来改变类的默认行为。

## 抽象类

用什么术语来结束本章最合适呢？我们在这里引入它，是因为它与继承的概念直接相关。

有时，创建类是为了方便他人创建子类。出于这个原因，这些类被称为抽象类，或者等价于抽象子类。方法和实例变量定义在类中，但没有人期望从该类创建实例。

在第二部分“Foundation 框架”中涵盖的 Foundation 框架许多许多抽象类。例如，Foundation 的 `NSNumber` 是为了处理数字创建的抽象类。整数和浮点数通常具有不同的存储需求。`NSNumber` 的子类对应每种数值类型。由于这些子类与其抽象父类不同，实际上存在，因此被称为具体子类。每个具体子类都在 `NSNumber` 伞类下的所有类统称为一个簇。当你向 `NSNumber` 类发送消息来创建一个新的整数对象时，将使用适当的子类为整数对象分配必要的存储空间，并恰当地设置其值。这些子类实际上是私有的。你不会通过抽象父类直接访问它们。抽象父类为处理所有类型的数字对象提供了一个公共接口，并免除了你必须知道在你的数字对象中存储了何种类型的数字，以及如何设置和检索其值的负担。

诚然，这个讨论可能看起来有点“抽象”（抱歉！）。不用担心——在这里只需要一个该概念的基本图示就足够。

## 练习题

1. 在程序 8.1 中添加一个新类 `ClassC`，它是 `ClassB` 的子类。创建一个 `initVar`，将实例变量 `x` 的值设置为 300。编写一个例程，声明 `ClassA`、`ClassB` 和 `ClassC` 的对象并调用它们的 `initVar` 方法。

2. 在处理高分辨率设备时，你可能需要使用一种坐标系统，允许你将点指定为浮点值而不是整数（iOS 使用结构 `CGRect` 来处理矩形。在处理此类矩形时，所有的坐标和大小都表示为浮点数）。修改本章中的 `XYPoint` 和 `Rectangle` 类以处理浮点数。矩形的宽度、高度、面积和周长也应该支持浮点数。



- 3. 修改程序 8.1 以添加一个新类 `ClassB2`，它像 `ClassB` 一样是 `ClassA` 的子类。关于 `ClassB` 和 `ClassB2` 之间的关系你有什么说明？识别 `NSObject` 类、`ClassA`、`ClassB` 和 `ClassB2` 之间的层级关系。`ClassB` 的父类是什么？`ClassB2` 的父类是什么？一个类可以有多少个子类，又有多少个父类？

- 4. 为 `Rectangle` 类编写一个名为 `translate:` 的方法，接受 `XYPoint` 对象作为参数。让它通过指定的向量移动矩形的原点。注意：平移意味着将点从一个地方移动到另一个地方。

- 5. 定义一个名为 `GraphicObject` 的新类，并使其成为 `NSObject` 的子类。在你的新类中定义实例变量如下：

```objc
int fillColor;  // 颜色
BOOL filled;     // 对象是否被填充？
int lineColor; // 线颜色
```

编写方法来设置和检索之前定义的变量。使 `Rectangle` 类成为 `GraphicObject` 的子类。定义新类 `Circle` 和 `Triangle`，它们也是 `GraphicObject` 的子类。编写方法来设置和检索这些对象的各种参数，并计算圆的周长和三角形的周长。

- 6. 为 `Rectangle` 类编写一个名为 `containsPoint:` 的方法，接受 `XYPoint` 对象作为参数：

```objc
-(BOOL)containsPoint:(XYPoint *)aPoint
```

如果矩形包含指定的点，该方法返回 `YES`，否则返回 `NO`。

- 7. 为 `Rectangle` 类编写一个名为 `intersect:` 的方法，接受一个矩形作为参数，并返回一个表示两个矩形之间叠区域的矩形。例如，给定图 8.10 所示的两个矩形，该方法应该返回一个原点在 (0,0)、宽度为 50、高度为 60 的矩形。如果矩形不相交，则返回一个宽度和高度为 0 且原点在 (0,0) 的矩形。

![图 8.10 相交矩形](img/8.10.png)

- 8. 为 `Rectangle` 类编写一个名为 `draw` 的方法，使用虚线和垂直字符绘制一个矩形。以下代码序列

```objc
Rectangle *myRect = [[Rectangle alloc] init];
[myRect setWidth:10 height:3];
[myRect draw];
```

将产生以下输出：

```
--------
|       |
|       |
--------
```

> 注意：你应该使用 `printf` 来绘制你的字符，因为 `NSLog` 在每次被调用时都会显示换行。

# 多态、动态类型与动态绑定

在本章中，你将学习 Objective-C 语言的特性，这些特性使其成为一种如此强大的语言，并将其与 C++ 等其他面向对象的语言区分开来。本章描述了三个核心概念：多态、动态类型和动态绑定。多态允许开发程序时，使得不同类的对象共享相同的名称。动态类型将对象所属类的确定推迟到程序执行时。动态绑定将对象上要调用的实际方法的确定推迟到程序运行时。

## 多态：相同名称，不同类

程序 9.1 显示了 `Complex` 类的接口文件，它用于在程序中表示复数。

```objc
// 程序 9.1 Complex.h 接口文件
// Complex 类的接口文件

#import <Foundation/Foundation.h>

@interface Complex: NSObject
@property double real, imaginary;
-(void)print;
-(void)setReal:(double)a andImaginary:(double)b;
-(Complex *)add:(Complex *)f;
@end
```

## 程序 9.1 Complex.m 实现文件

你应该已经在第 7 章“关于类的更多”的练习 5 和 6 中完成了该类的实现部分。我们添加了额外的 `setReal:andImaginary:` 方法，通过一条消息同时设置数字的实部和虚部，并合成了访问器方法。如下所示：

```objc
// Complex 类的实现文件

#import "Complex.h"

@implementation Complex

@synthesize real, imaginary

-(void)print
{
    NSLog("%g + %gi", real, imaginary);
}

-(void)setReal:(double)a andImaginary:(double)b
{
    real = a;
    imaginary = b;
}

-(Complex *)add:(Complex *)f
{
    Complex *result = [[Complex alloc] init];

    result.real = real + f.real;
    result.imaginary = imaginary + f.imaginary;

    return result;
}
@end
```

## 程序 9.1 测试程序 main.m

// 共享方法名：多态

```objc
#import "Fraction.h"
#import "Complex.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        Fraction *f1 = [[Fraction alloc] init];
        Fraction *f2 = [[Fraction alloc] init];
        Fraction *fracResult;
        Complex *c1 = [[Complex alloc] init];
        Complex *c2 = [[Complex alloc] init];
        Complex *compResult;

        [f1 setTo:1 over:2];
        [f2 setTo:2 over:3];
        fracResult = [f1 add:f2];
        [fracResult print];

        [c1 setReal:18.0 andImaginary:2.5];
        [c2 setReal:-5.0 andImaginary:3.2];
        compResult = [c1 add:c2];
        [compResult print];
    }
    return 0;
}
```

## 程序 9.1 输出

```
1/3
2/4
3/5
18 + 2.5i
-5 + 3.2i
13 + 5.7i
```

# 动态绑定与 id 类型

第 4 章简要提到了 `id` 数据类型，并指出它是通用对象类型。也就是说，`id` 可存储属于任何类的对象。当程序执行期间使用它在变量中存储不同类型的对象时，这种数据类型的威力就得到了发挥。学习程序 9.2 及其相关的输出。

## 程序 9.2 测试程序 main.m

```objc
// 演示动态类型与绑定

#import "Fraction.h"
#import "Complex.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        id dataValue;
        Fraction *f1 = [[Fraction alloc] init];
        Complex *c1 = [[Complex alloc] init];

        [f1 setTo:2 over:5];
        [c1 setReal:10.0 andImaginary:2.5];

        // 第一个 dataValue 获取了一个分数
        dataValue = f1;
        [dataValue print];

        // 现在 dataValue 获取了一个复数
        dataValue = c1;
        [dataValue print];

        return 0;
    }
}
```

## 程序 9.2 输出

```
2/5
10 + 2.5i
```

变量 `dataValue` 被声明为 `id` 对象类型。因此，`dataValue` 可以用于持有程序的任何类型的对象。注意声明行中没有星号：

`id dataValue;`

将 `Fraction f1` 设置为 2/5，将 `Complex c1` 设置为 (10 + 2.5i)。赋值语句

`dataValue = f1;`

将 `Fraction f1` 存储在 `dataValue` 中。现在，你可以对 `dataValue` 做什么？嗯，你可以对 `dataValue` 调用任何你在 `Fraction` 上可以使用的方法，尽管 `dataValue` 的类型是 `id` 而不是 `Fraction`。但如果 `dataValue` 可以存储任何类型的对象，系统又是如何知道要调用哪个方法的呢？也就是说，当它遇到消息表达式

`[dataValue print];`

它如何知道要调用哪个方法？你为 `Fraction` 和 `Complex` 类都定义了方法。正如之前提到的，答案在于 Objective-C 系统始终跟踪对象所属的类。这也取决于动态类型和动态绑定的概念——即系统在运行时（而不是编译时）对对象的类做出决定，因此动态地决定调用哪个方法。

因此，在程序执行期间，在系统向 `dataValue` 发送 `print` 消息之前，它首先检查存储在 `dataValue` 内部对象的类。在程序 9.2 的第一种情况下，该变量包含一个 `Fraction` 对象，使用了 `Fraction` 类中定义的 `print` 方法。这通过程序的输出验证了这一点。

在第二种情况下，发生了相同的事情。首先，将 `Complex` 数赋值给 `dataValue`。接下来，执行以下消息表达式：

```objc
[dataValue print];
```

这一次，由于 `dataValue` 包含属于 `Complex` 类的对象，因此选择了该类对应的方法进行执行。

这是一个简单的示例，但你可以将此概念推广到更复杂的应用程序。当与多态结合时，动态绑定和动态类型允许你轻松编写代码，向来自不同类的对象发送相同的消息。

例如，考虑一个用于在屏幕上绘制图形对象的 `draw` 方法。你可能为你的每个图形对象定义了不同的方法，例如文本、圆形、矩形等。如果在此处要绘制的特定对象在一个 `id` 变量 `currentObject` 中（例如），你只需向它发送 `draw` 消息即可在屏幕上绘制它：

```objc
[currentObject draw];
```

你甚至可以对其进行测试，以确保存储在 `currentObject` 中的对象确实响应 `draw` 方法。你将在本章节后的“向类提问”部分查看到如何做到这一点。

# 编译时与运行时检查

由于存储在 `id` 变量内部的对象类型在编译时是不确定的，某些操作会被推迟到运行时——即程序执行时。

考虑以下代码序列：

```objc
Fraction *f1 = [[Fraction alloc] init];
[f1 setReal:10.0 andImaginary:2.5];
```

回想起 `setReal:andImaginary:` 方法适用于复数而不是分数，当你编译包含该行的程序时，会发出此消息：

> 'Fraction' may not respond to 'setReal:andImaginary:'

Objective-C 编译器知道 `f1` 是一个 `Fraction` 对象，因为它被那样声明的。当它看到消息表达式时

```objc
[f1 setReal:10.0 andImaginary:2.5];
```

它也知道 `Fraction` 类没有 `setReal:andImaginary:` 方法（也没有继承该方法）。因此，它发出了之前显示的警告消息。

现在考虑以下代码序列：

```objc
id dataValue = [[Fraction alloc] init];
...
[dataValue setReal:10.0 andImaginary:2.5];
```

这些行不会产生编译器的警告消息——编译器在处理你的文件时不知道 `dataValue` 内部存储的是什么类型的对象（不，编译器并没有提前发现变量内部存储了一个 `Fraction` 对象！）。

在运行包含这些行的程序之前，没有报告错误消息。程序崩溃，错误包含许多行，其中一行看起来像：

`-[Fraction setReal:andImaginary:]: unrecognized selector sent to instance 0x103f00`

当程序执行时，系统首先检查存储在 `dataValue` 内部的对象类型。由于 `dataValue` 中存储了一个 `Fraction`，运行时系统寻找为 `Fraction` 类定义的 `setReal:andImaginary:` 方法。由于找不到此类方法，将显示错误消息并终止程序。

## id 数据类型与静态类型

如果 `id` 可以用来存储任何对象，你为什么不把所有都声明为 `id` 呢？由于几个原因，你希望在编译期间发现错误，而不是在执行期间。如果你将其推迟到运行时，你可能在太晚的时候发现程序无法工作。使用静态类型的另一个原因是它可以让程序更具可读性。考虑以下声明：

```objc
id f1;
```

对比

```objc
Fraction *f1;
```

你认为哪一个更容易理解——也就是说让 `f1` 的意图更清晰？静态类型与意义变量名（我们在之前的示例中没有选择）的结合可以在很大程度上使程序自文档化。

> 你不能对 `id` 变量使用点运算符；如果你尝试这样做，编译器将给你一个错误。

# 动态类型下的参数和返回值

如果你使用动态类型来调用方法，请注意以下规则：如果同名方法在你的多个类中实现，每个方法必须在参数类型和返回值上一致，以便编译器为你的消息生成正确的代码。

编译器会在每个类声明时进行一致性检查。如果一个或多个方法在参数或返回值上冲突，编译器会发出警告消息。然而，`Fraction` 和 `Complex` 类包含 `add:` 方法。`Fraction` 类接收其参数并返回一个 `Fraction` 对象，而 `Complex` 类接收并返回一个 `Complex` 对象。如果 `f1` 和 `myFract` 是 `Fraction` 对象，而 `myComplex` 是 `Complex` 对象，那么如下语句

```objc
result = [myFract add:f1];
```

和

```objc
result = [myComplex add:comp];
```

就不会引起任何问题。这是因为在两种情况下，消息的接收者都是静态类型的，编译器可以检查在接收者类定义的统一用法。

如果 `dataValue` `dataValue2` 是 `id` 变量，语句

```objc
result = [dataValue add:dataValue2];
```

会导致编译器生成 `add:` 方法的参数并通过假设处理其返回值。

在运行时，Objective-C 运行时系统将检查存储在 `dataValue` 内部对象的类，并从正确的类中选择适当的方法进行执行。在更通用的情况下，编译器可能会生成错误的代码向方法传递参数或处理其返回值。

例如，如果一个方法返回一个对象而另一个方法返回一个整数。如果两个方法之间的不一致仅仅是不同类型的对象（例如，`Fraction` 的 `add:` 方法接收一个 `Fraction` 对象作为参数并返回一个，而 `Complex` 的 `add:` 方法接收并返回一个 `Complex` 对象），编译器仍然会生成正确的代码，因为内存地址（即指针）是作为对象的引用传递的。

# 关于类的提问

当你开始处理可能包含来自不同类对象的变量时，你可能需要提出诸如下的问题：

- 这个对象是 `Rectangle`（矩形）吗？
- 这个对象支持 `print`（打印）方法吗？
- 这个对象是 `GraphicObject` 类的成员还是其后代类之一？

你可以利用这些问题的答案来执行不同的代码序列、避免错误，或者在程序执行时检查程序的完整性。

表 9.1 总结了 `NSObject` 类支持的提问此类问题的基本方法。在该表中，`class-object` 是一个类对象（通常通过类方法生成），而 `selector` 是 `SEL` 类型的值（通常通过 `@selector` 指令创建）。

## 表 9.1 用于处理动态类型的方法

| 方法 | 问题或操作 |
| :--- | :--- |
| `-(BOOL) isKindOfClass:` | 该对象是 `class-object` 的成员还是其后代类？ |
| `-(BOOL) isMemberOfClass:` | 该对象是 `class-object` 的成员吗？ |
| `-(BOOL) respondsToSelector:` | 该对象能响应由 `selector` 指定的方法吗？ |
| `+(BOOL) instancesRespondToSelector:` | 指定类的实例能响应 `selector` 吗？ |
| `+(BOOL) isSubclassOfClass:` | 该类是指定类的子类吗？ |
| `-(id) performSelector:` | 应用由 `selector` 指定的方法。 |
| `-(id) performSelector:withObject:` | 传递参数 `object` 并应用 `selector` 指定的方法。 |



# 第 9 章 多态、动态类型和动态绑定

此处未涵盖其他方法。其中一种方法允许你询问一个对象是否符合某个协议（参见第 11 章，“分类与协议”）。其他方法则允许你询问有关方法解析的问题（本文未涉及）。

要从类名或其他对象生成类对象，你向它发送类消息。因此，要从名为 `Square` 的类获取一个类对象，你写道：

```
[Square class]
```

如果 `mySquare` 是 `Square` 对象的实例，你可以通过编写以下代码获取它的类：

```
[mySquare class]
```

要查看变量 `obj1` 和 `obj2` 中存储的对象是否来自同一类的实例，你写道：

```
if ([obj1 class] == [obj2 class])
```

```
...
```

要查看 `myFract` 是否是 `Fraction` 类对象，你对表达式的结果进行测试，例如：

```
[myFract isMemberOfClass: [Fraction class]]
```

要生成表 9.1 中列出的所谓选择器（selectors）之一，你对方法名应用 `@selector` 指令。例如，以下代码会为 `alloc` 方法产生一个 `SEL` 类型的值，你已知它是一个继承自 `NSObject` 类的方法：

```
@selector (alloc)
```

以下表达式为你在 `Fraction` 类中实现的 `setTo:over:` 方法产生一个选择器（记住方法名中的冒号）：

```
@selector (setTo:over:)
```

要查看 `Fraction` 类的实例是否响应 `setTo:over:` 方法，你可以测试表达式的返回值，如下所示：

```
[Fraction instancesRespondTo: @selector (setTo:over:)]
```

记住，该测试涵盖了继承的方法，而不仅仅是直接在类定义中定义的方法。

`performSelector` 方法及其变体（表 9.1 中未显示）允许你向对象发送消息，其中消息可以是存储在变量中的选择器。例如，考虑这段代码序列：

```
SEL action;
id graphicObject;
...
action = @selector (draw);
[graphicObject performSelector:action];
```

## 关于类的提问

在这个示例中，由 `SEL` 变量 `action` 指向的方法发送给存储在 `graphicObject` 中的任何图形对象。推测，该方法在程序执行期间可能会变化——也许基于用户的输入——尽管我们把 `action` 显示为 `draw`。为了确保对象能够响应该操作，你可能想使用类似的代码：

```
if ((graphicObject respondsToSelector:action) == YES)
    [graphicObject performSelector:action]
else
    // 此处编写错误处理代码
```

> **注意**
>
> `respondsToSelector:` 方法在 iOS 中被广泛用于实现代理（delegation）概念。正如你将在第 10 章“变量与数据类型”中学到的，系统将给你选择，在你的类中实现一个或多个方法来处理事件或提供信息（例如表格中的节数）。为了让系统确定你是否实现了某个特定方法，它将使用 `respondsToSelector` 来检查是否可以将事件处理委托给你的方法。如果你没有实现该方法，它将处理事件本身，无论默认行为是什么。

你也可以采用其他策略：你可以使用 `forwardInvocation:` 方法将消息转发给另一个对象处理，但涵盖如何这样做超出了本文的范围。

程序 9.3 对定义的 `Square` 和 `Rectangle` 类提问了一些问题。尝试在查看输出之前预测该程序的运行（第 8 章，“继承”）。

### 程序 9.3

```
#import "Square.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        Square *mySquare = [[Square alloc] init];

        if ([mySquare class] == [Square class])
            NSLog("mySquare is a member of Square class");

        if ([mySquare isMemberOfClass:[Rectangle class]])
            NSLog("mySquare is a member of Rectangle class");

        if ([mySquare isMemberOfClass:[NSObject class]])
            NSLog("mySquare is a member of NSObject class");
    }
    return 0;
}
```

### 程序 9.3 输出

```
mySquare is a member of Square class
mySquare is a kind of Square
mySquare is a kind of Rectangle
mySquare is a kind of NSObject
```

```
// isKindOf

if ([mySquare isKindOfClass:[Square class]])
    NSLog("mySquare is a kind of Square");

if ([mySquare isKindOfClass:[Rectangle class]])
    NSLog("mySquare is a kind of Rectangle");

if ([mySquare isKindOfClass:[NSObject class]])
    NSLog("mySquare is a kind of NSObject");

// respondsTo:

if ([mySquare respondsToSelector:@selector(setSide)])
    NSLog("mySquare responds to setSide:");

if ([mySquare respondsToSelector:@selector(setWidth:over:)])
    NSLog("mySquare responds to setWidth:over:");

if ([Square respondsToSelector:@selector(alloc)])
    NSLog("Square class responds to alloc method");

// instancesRespondTo:

if ([Rectangle instancesRespondTo:@selector(setSide)])
    NSLog("Instances of Rectangle responds to setSide:");

if ([Square instancesRespondTo:@selector(setSide)])
    NSLog("Instances of Square responds to setSide:");

// isSubclassOf:

if ([Square isSubclassOf:[Rectangle class]])
    NSLog("Square is a subclass of Rectangle");
```

# 使用 @try 处理异常

良好的编程规范要求你尝试预测程序中可能出现的问题。你可以通过测试可能导致程序异常终止的条件并处理这些情况，例如通过记录消息并优雅地终止程序或采取某些正确的操作。例如，在本章中，我们将学习如何测试一个对象是否响应特定的消息。在避免错误的情况下，在程序执行时进行此类测试可以避免向对象发送未识别的消息。当尝试发送此类未识别的消息时，你的程序通常会通过抛出一个所谓的“异常”来立即终止。

看看程序 9.4。我们在 `Fraction` 类中没有定义名为 `noNoSuchMethod` 的方法。当你编译程序时，你将收到相关的警告消息。

### 程序 9.4

```
#import "Fraction.h"
int main (int argc, char * argv[]) {
    @autoreleasepool {
        Fraction *f = [[Fraction alloc] init];
        @try {
            [f noNoSuchMethod];
        } catch (NSException *exception) {
            NSLog("@Execution continues!");
        }
    }
    return 0;
}
```



## 表 9.1 用于处理动态类型的方法

| 方法 | 问题或操作 |
| :--- | :--- |
| `(-BOOL) isKindOfClass:class-object` | 该对象是 `class-object` 的成员还是其后代类？ |
| `(-BOOL) isMemberOfClass:class-object` | 该对象是 `class-object` 的成员吗？ |
| `(-BOOL) respondsToSelector:selector` | 该对象能响应由 `selector` 指定的方法吗？ |
| `(+BOOL) instancesRespondToSelector:selector` | 指定类的实例能响应 `selector` 吗？ |
| `(+BOOL) isSubclassOfClass:class-object` | 该对象是指定类的子类吗？ |
| `(-id) performSelector:selector` | 应用由 `selector` 指定的方法。 |
| `(-id) performSelector:selector withObject:object` | 传递参数 `object` 并应用 `selector` 指定的方法。 |
| `(-id) performSelector:selector withObject:object1 withObject:object2` | 使用参数 `object1` 和 `object2` 应用 `selector` 指定的方法。 |

# 第 9 章 多态、动态类型和动态绑定

此处未涵盖其他方法。其中一种方法允许你询问一个对象是否符合某个协议（参见第 11 章，“分类与协议”）。其他方法则允许你询问有关方法解析的问题（本文未涉及）。

要从类名或其他对象生成类对象，你向它发送类消息。因此，要从名为 `Square` 的类获取一个类对象，你写道：

```
[Square class]
```

如果 `mySquare` 是 `Square` 对象的实例，你可以通过编写以下代码获取它的类：

```
[mySquare class]
```

要查看变量 `obj1` 和 `obj2` 中存储的对象是否来自同一类的实例，你写道：

```
if ([obj1 class] == [obj2 class])
```

...

要查看 `myFract` 是否是 `Fraction` 类对象，你对表达式的结果进行测试，例如：

```
[myFract isMemberOfClass: [Fraction class]]
```

要生成表 9.1 中列出的所谓选择器（selectors）之一，你对方法名应用 `@selector` 指令。例如，以下代码会为 `alloc` 方法产生一个 `SEL` 类型的值，你已知它是一个继承自 `NSObject` 类的方法：

```
@selector(alloc)
```

以下表达式为你在 `Fraction` 类中实现的 `setTo:over:` 方法产生一个选择器（记住方法名中的冒号）：

```
@selector(setTo:over:)
```

要查看 `Fraction` 类的实例是否响应 `setTo:over:` 方法，你可以测试表达式的返回值，如下所示：

```
[Fraction instancesRespondToSelector: @selector(setTo:over:)]
```

记住，该测试涵盖了继承的方法，而不仅仅是直接在类定义中定义的方法。

`performSelector` 方法及其变体（表 9.1 中未显示）允许你向对象发送消息，其中消息可以是存储在变量中的选择器。例如，考虑这段代码序列：

```
SEL action;
id graphicObject;
...
action = @selector(draw);
[graphicObject performSelector:action];
```

## 关于类的提问

在这个示例中，由 `SEL` 变量 `action` 指向的方法发送给存储在 `graphicObject` 中的任何图形对象。推测，该方法在程序执行期间可能会变化——也许基于用户的输入——尽管我们把 `action` 显示为 `draw`。为了确保对象能够响应该操作，你可能想使用类似的代码：

```
if ((graphicObject respondsToSelector:action) == YES)
    [graphicObject performSelector:action]
else
    // 此处编写错误处理代码
```

> **注意**
>
> `respondsToSelector:` 方法在 iOS 中被广泛用于实现代理（delegation）概念。正如你将在第 10 章“变量与数据类型”中学到的，系统将给你选择，在你的类中实现一个或多个方法来处理事件或提供信息（例如表格中的节数）。为了让系统确定你是否实现了某个特定方法，它将使用 `respondsToSelector` 来检查是否可以将事件处理委托给你的方法。如果你没有实现该方法，它将处理事件本身，无论默认行为是什么。
>
> 你也可以采用其他策略：你可以使用 `forwardInvocation:` 方法将消息转发给另一个对象处理，但涵盖如何这样做超出了本文的范围。

程序 9.3 对定义的 `Square` 和 `Rectangle` 类提问了一些问题。尝试在查看输出之前预测该程序的运行（第 8 章，“继承”）。

### 程序 9.3

```
#import "Square.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        Square *mySquare = [[Square alloc] init];

        if ([mySquare class] == [Square class])
            NSLog("mySquare is a member of Square class");

        if ([mySquare isMemberOfClass:[Rectangle class]])
            NSLog("mySquare is a member of Rectangle class");

        if ([mySquare isMemberOfClass:[NSObject class]])
            NSLog("mySquare is a member of NSObject class");
    }
    return 0;
}
```

### 程序 9.3 输出

```
mySquare is a member of Square class
```

(此处省略)

---

### 程序 9.3 完整测试代码

```
// isKindOf

if ([mySquare isKindOfClass:[Square class]])
    NSLog("mySquare is a kind of Square");

if ([mySquare isKindOfClass:[Rectangle class]])
    NSLog("mySquare is a kind of Rectangle");

if ([mySquare isKindOfClass:[NSObject class]])
    NSLog("mySquare is a kind of NSObject");

// respondsTo:

if ([mySquare respondsToSelector:@selector(setSide)])
    NSLog("mySquare responds to setSide:");

if ([mySquare respondsToSelector:@selector(setWidth:over:)])
    NSLog("mySquare responds to setWidth:over:");

if ([Square respondsToSelector:@selector(alloc)])
    NSLog("Square class responds to alloc method");

// instancesRespondTo:

if ([Rectangle instancesRespondToSelector:@selector(setSide)])
    NSLog("Instances of Rectangle responds to setSide:");

if ([Square instancesRespondToSelector:@selector(setSide)])
    NSLog("Instances of Square responds to setSide:");

// isSubclassOf:

if ([Square isSubclassOfClass:[Rectangle class]])
    NSLog("Square is a subclass of Rectangle");
```



# Asking Questions About Classes

If one method returned an object and the other returned an integer, for example. If the inconsistency between two methods is just a different type of object (for example, the `Fraction`'s `add` method takes a `Fraction` object as its argument and returns one, and the `Complex`'s `add:` method takes and returns a `Complex` object), the compiler will still generate the correct code because memory addresses (that is, pointers) are passed as references to objects anyway.

# Asking Questions About Classes

As you start working with variables that can contain objects from different classes, you might need to ask questions such as the following:

- Is this object a rectangle?
- Does this object support a `print` method?
- Is this object a member of the `Graphics` class or one of its descendants?

You can use the answers to these questions to execute different sequences of code, avoid an error, or check the integrity of your program while it's executing.

Table 9.1 summarizes the basic methods that the `NSObject` class supports for asking these types of questions. In this table, `class-object` is a class object (typically generated with the `class` method), and `selector` is a value of type `SEL` (typically created with the `@selector` directive).

# Table 9.1 Methods for Working with Dynamic Types

| Method | Question or Action |
| :--- | :--- |
| `(-BOOL) isKindOfClass:class-object` | Is the object a member of `class-object` or a descendant? |
| `(-BOOL) isMemberOfClass:class-object` | Is the object a member of `class-object`? |
| `(-BOOL) respondsToSelector:selector` | Can the object respond to the method specified by `selector`? |
| `(+BOOL) instancesRespondToSelector:selector` | Can instances of the specified class respond to `selector`? |
| `(+BOOL) isSubclassOfClass:class-object` | Is the object a subclass of the specified class? |
| `(-id) performSelector:selector` | Apply the method specified by `selector`. |
| `(-id) performSelector:selector withObject:object` | Apply the method specified by `selector` passing the argument `object`. |
| `(-id) performSelector:selector withObject:object1 withObject:object2` | Apply the method specified by `selector` with the arguments `object1` and `object2`. |

# Chapter 9 Polymorphism, Dynamic Typing, and Dynamic Binding

Other methods are not covered here. One enables you to ask whether an object conforms to a protocol (see Chapter 11, "Categories and Protocols"). Others enable you to ask about resolving methods (not covered in this text).

To generate a class object from a class name or another object, you send it the `class` message. So to get a class object from a named `Square`, you write the following:

```
[Square class]
```

If `mySquare` is an instance of a `Square` object, you get its class by writing this:

```
[mySquare class]
```

To see whether the objects stored in the variables `obj1` and `obj2` are instances from the same class, you write:

```
if ([obj1 class] == [obj2 class])
```

...

To see if `myFract` is a `Fraction` class object, you test the result from the expression, like:

```
[myFract isMemberOfClass: [Fraction class]]
```

To generate one of the so-called selectors listed in Table 9.1, you apply the `@selector` directive to a method name. For example, the following produces a value of type `SEL` for the method `alloc`, which you know is a method inherited from the `NSObject` class:

```
@selector(alloc)
```

The following expression produces a selector for the `setTo:over:` method that you implemented in your `Fraction` class (remember the colon characters in the method names):

```
@selector(setTo:over:)
```

To see whether an instance of the `Fraction` class responds to the `setTo:over:` method, you can test the return value from the expression, like this:

```
[Fraction instancesRespondToSelector: @selector(setTo:over:)]
```

Remember, the test covers inherited methods, not just those directly defined in the class definition.

The `performSelector:` method and its variants (not shown in Table 9.1) enable you to send a message to an object, where the message can be a selector stored inside a variable. For example, consider this code sequence:

```
SEL action;
id graphicObject;
...
action = @selector(draw);
[graphicObject performSelector:action];
```

# Asking Questions About Classes 187

In this example, the method indicated by the `SEL` variable `action` is sent to whatever graphical object is stored in `graphicObject`. Presumably, the method may vary during program execution—perhaps based on the user's input—even though we've shown the action as `draw`. To ensure that the object can respond to the action, you might want to use something like this:

```
if ([graphicObject respondsToSelector:action] == YES)
    [graphicObject performSelector:action];
else
    // error handling code here
```

> **Note**
>
> The `respondsToSelector:` method is used extensively in iOS for implementing the concept of delegation. As you'll learn in Chapter 10, "On Variables and Data Types," the system will give you the option to implement one or more methods in your class to handle events or provide information (such as the number of sections in a table). In order for the system to determine whether you have implemented a particular method, it will use `respondsToSelector:` to see if it can delegate the handling of the event to your method. If you don't implement the method, it will take care of the event itself, whatever the default behavior is.

You can employ other strategies as well: You can forward the message to another object to handle using the `forwardInvocation:` method, but covering how to do this is beyond the scope of this text.

Program 9.3 asks some questions about the `Square` and `Rectangle` classes defined in Chapter 8, "Inheritance." Try to predict the results from this program before looking at the actual output.

## Program 9.3

```
#import "Square.h"

int main(int argc, char *argv[])
{
    @autoreleasepool {
        Square *mySquare = [[Square alloc] init];

        if ([mySquare class] == [Square class])
            NSLog(@"mySquare is a member of Square class");

        if ([mySquare isKindOfClass:[Rectangle class]])
            NSLog(@"mySquare is a kind of Rectangle");

        if ([mySquare isKindOfClass:[NSObject class]])
            NSLog(@"mySquare is a kind of NSObject");
    }
    return 0;
}
```

## Program 9.3 Output

```
mySquare is a member of Square class
mySquare is a kind of Square
mySquare is a kind of Rectangle
mySquare is a kind of NSObject
```

# 188 第 9 章 Polymorphism, Dynamic Typing, and Dynamic Binding



// isKindOfClass

```objc
if ([mySquare isKindOfClass:[Square class]])
    NSLog("mySquare is a kind of Square");

if ([mySquare isKindOfClass:[Rectangle class]])
    NSLog("mySquare is a kind of Rectangle");

if ([mySquare isKindOfClass:[NSObject class]])
    NSLog("mySquare is a kind of NSObject");
```

// respondsToSelector:

```objc
if ([mySquare respondsToSelector:@selector(setSide)])
    NSLog("mySquare responds to setSide:");

if ([mySquare respondsToSelector:@selector(setWidth:over:)])
    NSLog("mySquare responds to setWidth:over:");

if ([Square respondsToSelector:@selector(alloc)])
    NSLog("Square class responds to alloc method");
```

// instancesRespondToSelector:

```objc
if ([Rectangle instancesRespondToSelector:@selector(setSide)])
    NSLog("Instances of Rectangle responds to setSide:");

if ([Square instancesRespondToSelector:@selector(setSide)])
    NSLog("Instances of Square responds to setSide:");
```

// isSubclassOf:

```objc
if ([Square isSubclassOf:[Rectangle class]])
    NSLog("Square is a subclass of Rectangle");
```

```objc
}
return 0;
}
```

尽管收到了警告信息，你仍然可以继续运行程序。如果你这样做，你可能会看到程序异常终止，并伴有类似于程序 9.4 所示的错误。

## 程序 9.4 输出

```
*** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason:
-[FractionNoSuchMethod]: unrecognized selector to instance 0x103f000
*** Call stack at first throw:
```

为了避免此类情况下的异常终止，你可以将一个或多个语句放在一个特殊的语句块中，其格式如下：

```objc
@try {
  statement
  statement
}
@catch (Exception *exception) {
  statement
  statement
}
```

`@try` 块中的每个语句都会按正常方式执行。然而，如果块中的某一个语句抛出了异常，执行不会终止，而是立即跳转到 `@catch` 块并在那里继续。在那个块内部，你可以处理该异常。这里一个合理的操作序列是记录错误消息、清理并终止执行。

程序 9.5 展示了异常处理。后面是程序的输出。

## 程序 9.5 异常处理

```objc
#import <Fraction.h>

int main (int argc, char * argv[]) {
  @autoreleasepool {
    NSArray *myArray = [NSArray array];
    @try {
      [myArray objectAtIndex: 2];
    }
    @catch (NSException *exception) {
      NSLog(@"Caught %@@", exception.name, exception.reason);
      NSLog(@"Execution continues");
      return 0;
    }
  }
}
```

## 程序 9.5 输出

```
Caught NSRange ***: [NSArray objectAtIndex]: index 2 beyond bounds for empty array

Execution continues
```

程序 9.5 设置了一个数组（你将在第 15 章学习如何操作）。然后它使用 `NSArray` 对象的 `objectAtIndex:` 方法引用数组中一个不存在的元素：随后执行了 `@catch` 块。`NSException` 对象包含了作为参数传递给该块的异常信息。当异常发生时，如你所见，该方法获取了异常的名称，`reason` 方法提供了原因（由运行时自动提供）。

在执行完 `@catch` 块中的最后一个语句后（我们这里只有一个），程序将继续执行紧随该块之后的语句。在这种情况下，我们使用一个 `NSLog` 调用来验证异常已经继续而没有终止。

这是一个非常简单的示例，说明了如何在程序中捕获异常。`@finally` 块可以用于包含代码，无论 `@try` 块中的语句是否抛出异常，这些代码都会执行。

`throw` 允许你抛出自己的异常。你可以用它来抛出一个特定的异常，或者在 `@catch` 块内部抛出与进入该块时相同的异常，如下所示：

你可能在自己处理完异常后想这样做（也许是为了为你自己清理工作）。你可以让系统为你处理剩余的工作。

你可以拥有多个链式连接的 `@catch` 块，以捕获并处理不同类型的异常。在错误发生之前对其进行测试，比在发生后再捕获它们被认为是更好的编程实践。

总的来说，你不希望异常在程序运行时发生。在方法中测试错误并返回一个值作为错误指示，比抛出异常要好。强烈建议，如果你捕获了异常，你的意图应仅是为了清理并终止你的应用程序。为什么呢？因为 Apple 不保证在抛出异常后，你的应用程序将处于可以继续程序执行的良定义状态。

## 注意

你必须将方法名更改为 `add:` 以外名称。那是因为系统的 `NSObjectController` 类也有一个 `add:` 方法。正如“动态类型中的参数和返回类型”部分所述，如果不同类中存在同名的多个方法，且返回类型在编译时未知，编译器将执行一致性检查，以确保这些同名方法之间的参数和返回类型是一致的。

5. 给定本文中使用的 `Fraction` 和 `Complex` 类定义以及以下定义：

```objc
Fraction *fraction = [[Fraction alloc] init];
Complex *complex = [[Complex alloc] init];
id number = [[Complex alloc] init];
```

确定以下消息表达式的返回值。然后将它们输入程序以验证结果。

```objc
[fraction isMemberOfClass: [Complex class]];
[complex isMemberOfClass: [NSObject class]];
[complex isKindOfClass: [NSObject class]];
[fraction isKindOfClass: [Fraction class]];
[fraction respondsToSelector: @selector (print)];
[complex respondsToSelector: @selector (print)];
[fraction instancesRespondToSelector: @selector (print)];
[number respondsToSelector: @selector (print)];
[number isKindOfClass: [Complex class]];
[[number class] respondsToSelector: @selector (alloc)];
```

# 10 关于变量和数据类型的更多内容

在本章中，我们将详细介绍变量作用域、对象的初始化方法以及数据类型。

对象的初始化值得特别关注，我们在这里对此予以重视。在第 7 章“类的更多”中，我们简要讨论了实例变量以及静态和局部变量的作用域。我们将更多地讨论静态变量并引入全局变量的概念。此外，你可以使用某些指令更精确地控制实例变量的作用域。

## 初始化对象

你以前见过这种模式：分配一个新实例并初始化它，使用如下序列：

```objc
myFract = [[Fraction alloc] init];
```

我们在这里没有写 `init` 方法；我们使用继承自父类的，即 `NSObject`。

在这些方法被调用之后，你通常会给新对象赋值，如下：

```objc
[myFract setTo:1 over:3];
```

通过设置初始值来初始化对象的过程通常合并到一个方法中。例如，你可以定义 `initWith:over:`

一个包含许多实例变量的类通常也有几个初始化方法。例如，Foundation 框架中的 `NSArray` 类包含以下初始化方法：

```objc
initWithArray:
initWithArray:copyItems:
initWithContentsOfFile:
initWithContentsOfURL:
initWithObjects:
initWithObjects:count:
```

数组可以分配并按如下序列初始化：

```objc
myArray = [[NSArray alloc] initWithArray:...];
```

类中所有的初始化方法以 `init` 开始是一种常见做法……如你所见，`NSArray` 的初始化方法遵循这一惯例。在编写初始化方法时，你应该遵循以下策略。

你可能希望在类中的某个对象被初始化时执行某些操作。例如，创建类通过一个或多个实例变量使用和引用对象的完美位置。一个完美的例子就是 `Rectangle` 类：在 `init` 方法中分配矩形的 `XYPoint` 起点是合理的。为此，你必须重写继承的方法。

有一个重写 `init` 的标准“模板”，它看起来如下：

```objc
- (id)init
{
    self = [super init];
    if (self) {
        // 在此处编写初始化代码
    }
    return self;
}
```

此方法调用了父类初始化器。执行父类初始化器可以确保任何继承的实例变量都正确初始化。

你必须将执行父类 `init` 方法的结果赋值回 `self`，因为初始化器有权更改对象在内存中的位置（这意味着它的引用将会改变）。

如果父类初始化成功，返回的值将是非空值，正如语句所测试的那样。正如注释所示，在随后的块内部，你可以放置你自己的自定义初始化代码。这通常涉及分配和初始化你类中的实例变量。

如果你的类包含多个初始化器，则其中一个应该是你的**指定初始化器**（designated initializer），而所有其他初始化方法都应该使用它。通常情况下，它是你最复杂的初始化方法（通常是参数最多的那一个）。创建一个指定初始化器可以将你的主初始化代码集中在单个方法中。任何派生你类的子类都可以重写你的指定初始化器，以确保新实例得到适当的初始化。

基于这一选择，你的 `Fraction` 类的初始化方法 `initWith:over:` 看起来如下：

```objc
- (Fraction *) initWith:(int) n over:(int) d
{
    self = [super init];

    if (self) {
        [self setTo:n over:d];
    }
    return self;
}
```

在父类初始化（并根据返回非零值判断初始化成功）之后，你使用 `setTo:over:` 方法来设置 `Fraction` 的分子和分母。与其他初始化方法一样，你应当返回初始化后的对象，你也确实这样做了。

程序 10.1 测试了你新编写的 `initWith:over:` 初始化方法。

## 程序 10.1

```objc
#import "Fraction.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        Fraction *a = [[Fraction alloc] initWith:1 over:3];
        Fraction *b = [[Fraction alloc] initWith:3 over:7];

        [a print];
        [b print];
    }
    return 0;
}
```

## 程序 10.1 输出

```
1/3
3/7
```

为了遵循前面提到的关于指定初始化器的规则，你还应该修改 `Fraction` 类中的 `init`。如果你的类可能会被子类化，这一点尤为重要。

`init` 方法看起来可能像这样：

```objc
- (id) init
{
    return [self initWith:0 over:1];
}
```

注意 `init` 被定义为返回 `id` 类型。这是为可能被子类化的类编写方法的通用规则。在这种情况下，子类将不会是与父类同类型的对象。为了保持一致性，你必须回到 `initWith:over:` 方法并将其类型改为 `id`。

当你的程序开始执行时，它会向你类的所有方法发送 `initialize` 调用。如果你有一个类和子类，父类将接收第一个消息。此消息只会向每个类发送一次，并保证在向该类发送任何其他消息之前发送。目的是让你在该点执行任何初始化工作。例如，你可能想要初始化与该类相关的静态变量。

## 作用域重温

你可以通过多种方式影响程序中的变量。你可以对实例变量以及位于函数外部或内部的普通变量进行操作。在接下来的讨论中，我们使用“模块”（module）一词指代包含在源文件中的任意数量的方法或函数。

### 控制实例变量作用域的指令

你知道实例变量的作用域限于类的实例方法。因此，任何实例方法都可以通过名称直接访问其实例变量，而无需任何特殊操作。



# 变量作用域与数据类型详解

## 接口部分实例变量的继承与访问控制

你还知道在接口部分（`interface section`）声明的实例变量会被子类继承。继承的实例变量也可以从该子类中定义的任何方法通过名称直接访问。同样，这不需要任何特殊操作。

当你在接口部分声明实例变量时，可以在它们前面放置四个指令，以更精确地控制它们的作用域：

- `@protected`——在类及任何子类中定义的方法可以直接访问随其后的实例变量。这是接口部分定义的实例变量的默认设置。
- `@private`——在类中定义的方法可以直接访问随其后的实例变量，但子类不能访问。这是实现部分（`implementation section`）中定义的实例变量的默认设置。
- `@public`——在类以及任何其他类或模块中定义的方法可以直接访问随其后的实例变量。
- `@package`——对于 64 位镜像（`images`），可以在实现该类的实例任何地方访问该实例变量。

如果你想定义一个 `Printer` 的类，将两个名为 `pageCount` 和 `tonerLevel` 的实例变量设为私有，且仅允许 `Printer` 类中的方法访问，你可以使用如下所示的接口：

```objc
@interface Printer
{
@private
    int pageCount;
    int tonerLevel;
@protected
    // 其他实例变量
}
@end
```

任何派生 `Printer` 的子类都无法访问这两个实例变量，因为它们被设为私有了。

这些特殊指令就像“开关”；在其中一个指令之后出现的所有变量（带有标记变量声明结束的右括号），除非使用了另一个指令，否则都具有指定的作用域。在之前的示例中，`@protected` 指令确保随其后的实例变量（直到 `}`）可以被子类和 `Printer` 类方法访问。

`@public` 指令使得实例变量可以通过指针运算符 (`->`) 被其他方法或函数访问，这将在第 13 章“底层 C 语言特性”中介绍。将实例变量设为公共不被认为是良好的编程实践，因为它违背了数据封装的概念（即类隐藏其实例变量）。

## 关于属性、合成访问器和实例变量的更多信息

编码规范的当前趋势（Xcode 4 已采用此趋势）是使用下划线 (`_`) 作为实例变量的前导字符。因此，你在 Xcode 生成的模板代码中看到的任何以 `_` 开头的变量引用都是实例变量。

## 全局变量

如果你在程序的开头（任何方法、函数外部）编写语句 `int gGlobalVar = 5;`，则它的值可以在任何地方被访问。按照惯例，使用小写 `g` 作为全局变量的首字母。

```objc
Foo *myFoo = [[Foo alloc] init];
Log("%i", gGlobalVar);
```

```objc
[myFoo setGlobalVar:100];
Log("%i", gGlobalVar);
}
return 0;
```

在上一个程序中变量 `gGlobalVar` 的定义使得任何进行了适当 `extern` 声明的方法（函数）都能访问它的值。假设你的 `Foo` 方法 `setGlobalVar:` 如下：

```objc
(void) setGlobalVar:(int) val
{
extern int gGlobalVar;
gGlobalVar = val;
}
```

该程序产生以下输出：

```
100
```

这证明了 `setGlobalVar:` 方法能够访问并更改外部变量 `gGlobalVar` 的值。

如果许多方法需要访问 `gGlobalVar` 的值，在文件开头只进行一次 `extern` 声明将非常繁琐。然而，如果只有一个或少数几个方法需要访问此变量，那么在每个方法中分别进行 `extern` 声明也是有意义的；这会让程序更有条理，并将特定变量的使用隔离在那些真正使用它的函数中。注意，如果变量定义在包含访问该变量的代码文件中，则不需要单独的 `extern` 声明。

## 静态变量

这个例子正好违背了数据封装和面向对象编程的良好技巧。然而，你可能需要处理值在不同方法调用之间共享的变量。虽然通过限制访问 `setter` 和 `getter` 方法来将其“隐藏”在 `Foo` 类内部可能并不合理，但更好的方法是为这些操作定义专门的方法。

你现在知道，任何定义在方法之外的变量不仅是全局变量，也是外部变量。在许多情况下，你希望定义一个变量是全局的而不是外部的。换句话说，你希望定义一个全局变量对于特定模块（文件）是局部的。如果没有特定类定义内部之外的其他方法需要访问该特定变量，那么这样定义变量是有意义的。

### 重温作用域

你可以通过在包含特定类实现的文件中将变量定义为 `static` 来实现这一点。

如果在任何方法（或函数）之外，以下语句使得 `gGlobalVar` 的值在定义它所在的文件中出现的后续任何点都是可访问的，但对于其他文件中包含的方法或函数是不可见的：

```objc
static int gGlobalVar;
```

记住，类无法访问实例变量（你可能想过为什么这样）。然而，你可能希望一个类方法能够设置和访问变量。一个简单的例子是一个类分配器，你希望跟踪它分配了多少个对象。你可以通过在类的实现文件中设置一个静态变量来实现这一点。分配方法就可以直接访问此变量，因为它不是实例变量。类的变量不需要知道这个变量的存在。由于它在实现文件中被定义为 `static` 变量，它的作用域被限制在那个文件中。用户无法直接访问它，也不会违背封装的概念。如果在类外部访问了该变量的值，你可以写一个方法来获取该变量的值。

项目 10.2 通过增加两个新方法扩展了 `Fraction` 类的定义。类方法 `allocF` 分配一个新的 `Fraction` 并跟踪它分配了多少个 `Fraction`，而 `count` 方法返回 `count`。请注意，该方法也是一个类方法。它本可以实现为实例方法，但向类询问它分配了多少个实例，比向类的某个特定实例发送消息更有意义。

这些是准备添加到 `Fraction.h` 头文件中的两个新类方法的声明：

```objc
+(Fraction *) allocF;
+(int) count;
```

注意，继承的 `alloc` 方法没有被重写；相反，你需要自己的分配器方法。你的方法将利用继承的 `alloc` 方法。将此代码放在你的 `Fraction.m` 实现文件中：

```objc
static int counter;
```

```objc
@implementation Fraction

+(Fraction *) allocF
{
    extern int counter;
    ++counter;

    return [Fraction alloc];
}
```

```objc
+(int) count
{
    extern int gCounter;

    return gCounter;
}
// Fraction 类的其他方法放在这里

@end
```

## 注意

重写 `alloc` 不被认为是良好的编程习惯，因为该方法涉及内存的物理分配。你不应该参与到那个层级。

`gCounter` 的 `static` 声明使得实现文件中定义的任何方法都能访问它，但并不会让它可以从外部文件访问。`allocF` 方法简单地递增 `gCounter` 变量，然后使用 `alloc` 创建一个新的 `Fraction` 并返回结果。`count` 方法只需返回计数器的值，将其访问与读者隔离。

记住，这两个方法中不需要 `extern` 声明，是因为 `gCounter` 变量定义在文件中。它只是为了帮助方法的读者理解正在访问一个方法之外的变量。变量名中的 `g` 前缀对读者也起到相同的作用；由于某些原因，大多数程序员通常不包含 `extern` 声明。

程序 10.2 测试了新方法。

```objc
Program 10.2
#import "Fraction.h"

int main(int argc, char *argv[])
{
    @autoreleasepool {
        Fraction *a, *b, *c;

        NSLog("Fractions allocated: %i", [Fraction count]);

        a = [[Fraction alloc] init];
        b = [[Fraction alloc] init];
        c = [[Fraction alloc] init];

        NSLog("Fractions allocated: %i", [Fraction count]);
    }
    return 0;
}
```

## 枚举类型

### 程序 10.2 输出

```
Fractions allocated: 0
Fractions allocated: 3
```

当程序开始执行时，`gCounter` 的值被设置为 0（记住，如果你想对类进行任何特殊初始化，例如设置静态变量，可以重写初始化方法）。在使用 `allocF` 分配并初始化三个 `Fraction` 后，方法获取计数器，结果为 3。你也可以为类添加一个 setter 方法来重置计数器或设置为特定值。但在本应用中不需要。

### 枚举类型定义与使用

Objective-C 语言允许你指定可以赋值给变量的值范围。枚举数据类型的定义由关键字 `enum` 初始化。紧随该关键字的是枚举类型的名称，随后是一组在大括号内的标识符，它们定义了可以赋值给该类型的值。例如，以下语句定义了一个数据类型 `flag`：

```objc
enum flag { false, true };
```

理论上，该数据类型在程序内部可以赋值 `true` 和 `false`。遗憾的是，如果违反这一规则，Objective-C 编译器不会生成警告信息。

要声明一个 `enum flag` 变量，再次使用关键字 `enum`、类型名称，然后是变量列表。因此，以下语句定义了两个类型为 `flag` 的变量 `endOfData` 和 `matchFound`：

```objc
enum flag endOfData, matchFound;
```

（理论上）可以赋值给这些变量的值只有名称 `true` 和 `false`。因此，如下语句

```objc
endOfData = true;

and

if ( matchFound == false )
```

是可以的。

如果你想让枚举标识符关联特定的整数值，可以在定义数据类型时将整数赋值给标识符。列表中随之出现的枚举标识符将被分配连续的整数值，从指定的整数值加 1 开始。

在下面的定义中，定义了一个枚举数据类型 `direction`，其值为 `up`、`down`、`left` 和 `right`：

```
enum direction { up, down, left = 10, right };
```

编译器给 `up` 赋值 0，因为它出现在列表第一个；给 `down` 赋值 1，因为它紧随其后；给 `left` 赋值 10，因为它显式地分配了该值；给 `right` 赋值 11，因为它是列表中前一个枚举的增值。

枚举标识符可以共享相同的值。例如，在

```
enum boolean { no = 0, false = 0, yes = 1 };
```

向 `boolean` 变量赋值值 `no` 或 `false` 都会分配值 0；赋值值 `yes` 或 `true` 都会分配值 1。

另一个枚举数据类型定义的示例是，它定义了 `month` 类型，该类型可以赋值给该类型的变量，并定义了一年的月份名称：

```
enum month { january = 1, february, march, april, may, june, july, august, september, october, november, december };
```

Objective-C 编译器还将枚举标识符视为整数常量。如果你的程序包含以下两行代码，值 2 将被赋值给 `thisMonth`（而不是名称 `february`）：

```
enum month thisMonth;
```

```objectivec
thisMonth = february;
```

程序 10.3 显示了一个使用枚举数据类型的简单程序。该程序读取一个月份数字，然后进入 `switch` 语句来查看输入的是哪个月份。记住，编译器将枚举视为整数常量，因此它们是有效的 `case` 值。变量 `days` 被赋值为指定月份的天数，并在退出 `switch` 语句后显示其取值。程序中还包含一个特殊的测试，用于检查该月份是否为二月。

### 程序 10.3

```c
#import <Foundation/Foundation.h>
// 打印月份的天数
int main (int argc, char *argv[]) {
    @autoreleasepool {
        enum month { january = 1, february, march, april, may, june,
        july, august, september, october, november,
        december };

        enum month amon;
        int days;

        NSLog(@"Enter month number: ");
        scanf("%i", &amonth);

        if ( days != 0 )
            NSLog(@"Number of days is %i", days);

        if ( amonth == february )
            NSLog(@"...or 29 if it's a leap year");

        return 0;
    }
}
```

### 程序 10.3 输出

```
Enter month number:
5
Number of days is 31
```

### 程序 10.3 输出（重新运行）

```
Enter month number:
2
Number of days is 28
...or 29 if it's a leap year
```

你可以为枚举数据类型变量显式分配一个整数值；你应该使用类型转换操作符这样做。因此，如果 `monthValue` 是一个值为6 的整数变量，那么这个表达式是允许的：

```
lastMonth = (enum month) (monthValue - 1);
```

如果不使用类型转换，编译器（遗憾的是）不会对此报错。
在使用带有枚举数据类型的程序时，尽量不要依赖枚举值被视为整数这一事实。相反，应将它们视为不同的数据类型。枚举数据类型为你提供了一个带有整数数值的符号化名称。如果你之后需要更改该数字的值，必须在定义枚举的地方进行更改。如果你基于枚举数据类型的实际值做出假设，就违背了使用枚举的这种处。
在定义枚举数据类型时，允许某些变体：可以省略类型名称，并且可以声明变量为所定义的特定枚举数据类型。一个显示这两种选项的示例语句

```
enum { east, west, south, north } direction;
```

定义了一个（无名的）枚举数据类型，其值为 `east`、`west`、`south` 或 `north`，并声明变量 `direction` 为该类型。

在块（`block`）内定义枚举数据类型会将定义的作用域限制在数块内。另一方面，在程序开头（在任何块之外）定义枚举数据类型，将使该定义对整个文件全局可见。

在定义枚举数据类型时，你必须确保枚举标识符与同一作用域内的其他变量和其他枚举标识符相比是唯一的。

## typedef 语句

Objective-C 提供了一种功能，允许程序员为数据类型分配一个别名。这是通过名为 `typedef` 的语句实现的。下面的语句将名称 `Counter` 定义等同于 Objective-C 数据类型 `int`：

```c
typedef int Counter;
```

你随后可以声明变量为 `Counter` 类型，如下句所示：

```
Counter j, n;
```

Objective-C 编译器将之前显示的变量 `j` 和 `n` 的声明视为普通的整数变量。在这种情况下，使用 `typedef` 的主要优势在于它为变量定义提供了可读性。`j` 和 `n` 的定义体现了这些变量在程序中的意图。以普通方式将它们声明为 `int` 将无法体现这些变量的预期用途。

下面的 `typedef` 将 `NumberObject` 名称定义为一个 `Number` 对象：

```c
typedef NS*NumberObject;
```

随后声明为 `NumberObject` 类型的变量，如
`NumberObject myValue, myResult;`

被处理得就像：
`myValue, myResult;`

要定义新类型，遵循以下步骤：

1. 编写作为所需类型定义的语句。
2. 在变量名称通常出现的位置插入该类型。
3. 在所有内容前放置 `typedef` 关键字。

作为定义枚举类型的示例，为了定义 `direction`，遵循以下步骤：

```
typedef enum { east, west, north, south } Direction;
```

有了这个 `typedef`，你随后可以声明为 `Direction` 类型，如下：

`Direction step1, step2;`

## 数据类型转换

第 4 章“数据类型与表达式”简要讨论了在评估表达式时系统有时会自动进行转换。你也查看了如何使用转换操作符来显式规定转换。由于 `total` 和 `n` 都是整数变量，`total` 的值被转换为 `float`：

```objectivec
average = (float) total / n;
```



# 第 10 章 变量与数据类型详解

变量 `total` 的值在执行操作之前转换为 `float`，从而确保除法以浮点形式进行。

## 转换规则

Objective-C 编译器在处理由不同数据类型组成的表达式时遵循严格的规则。

以下总结了操作数转换时发生的顺序：

- 如果任意一个操作数是 `long double`，另一个将被转换为 `long double`，这将结果的类型。
- 如果任意一个操作数是 `double`，另一个将被转换为 `double`，这将结果的类型。
- 如果任意一个操作数是 `float`，另一个将被转换为 `float`，这将结果的类型。
- 如果任意一个操作数是 `_Bool`、`char`、`short int` 或位域，或者是枚举数据类型，它将被转换为 `int`。
- 如果任意一个操作数是 `long int`，另一个将被转换为 `long int`，这将结果的类型。
- 如果任意一个操作数是 `long int`，另一个将被转换为 `long int`，这将结果的类型。
- 如果到达这一步，两个操作数都是 `int`，这就是结果的类型。

这实际上是操作数转换步骤的简化版本。当涉及无符号操作数时，规则会变得复杂，但本文不再详细说明。

从这一系列步骤中意识到，当你到达“这就是结果的类型”的步骤时，你已经完成了转换过程。

作为遵循这些步骤的示例，让我们看看如何评估以下表达式，其中 `f` 被定义为 `float`，`i` 为 `long int`，`s` 为 `short int` 变量：

```
f * i + 1 / s
```

## 位运算符

接下来，`l` 除以 `s`，这是 `long int` 除以 `short int`。步骤 4 告诉你是 `short int` 将被提升为 `int`。继续，步骤 6 显示，由于操作数之一 (`l`) 是 `long int`，另一个操作数将被转换为 `long int`，这将是结果的类型。因此，此除法将产生一个 `int` 类型的值，并移除除法的任何小数部分。

最后，步骤 3 表明，如果表达式中的操作数类型为 `float`（如 `f * i` 相乘的结果），另一个操作数将被转换为 `float` 类型，这将是结果的类型。因此，在 `l` 除以 `s` 后，操作结果将转换为 `float` 类型并加到 `f` 和 `i` 的乘积中。上述表达式的最终结果将是一个 `float` 类型的值。

记住，类型转换始终可以用于显式强制转换并控制特定表达式的求值方式。

如果你在之前的表达式求值中不想 `l` 的除法被截断，你可以将其中一个操作数强制转换为 `float` 类型，从而强制求值作为浮点除法执行：

```
f * i + (float) 1 / s
```

在这个表达式中，`l` 在执行除法操作之前将转换为 `float`，因为类型转换运算符的优先级高于除法运算符。由于除法的操作数之一将是 `float` 类型，另一个操作数 (`s`) 将被自动转换为 `float` 类型，这将是结果的类型。

### 位运算符

Objective-C 语言中的各种运算符用于表示整数值的特定位。表 10.1 展示了这些运算符。

**表 10.1 位运算符**

| 符号 | 操作 |
| :--- | :--- |
| `&` | 位与 (AND) |
| `|` | 位或 (OR) |
| `^` | 位异或 (XOR) |
| `~` | 取反 |
| `<<` | 左移 |
| `>>` | 右移 |

> **注意**
> 你在 Objective-C 程序中可能很少甚至不使用位运算符，尽管你会在框架头文件中遇到它们。由于这些内容对新初学者来说可能有点晦涩，你可以直接跳过这一节，并在必要时以后再回来。

表 10.1 中列出的所有运算符除取反运算符 (`~`) 外，都是二进制运算符，因此需要两个操作数。位操作可以在任何类型的整数值上执行，但不能在浮点值上执行。在后续示例中，你将学习如何在二进制表示和十六进制之间转换。一个十六进制（16 进制）数字由 4 位组成。表 10.2 显示了这些基之间的转换方法。

**表 10.2 二进制、十进制和十六进制等值值**

| 二进制值 | 十进制值 | 十六进制值 |
| :--- | :--- | :--- |
| 0000 | 0 | 0 |
| 0001 | 1 | 1 |
| 0010 | 2 | 2 |
| 0011 | 3 | 3 |
| 0100 | 4 | 4 |
| 0101 | 5 | 5 |
| 0110 | 6 | 6 |
| 0111 | 7 | 7 |
| 1000 | 8 | 8 |
| 1001 | 9 | 9 |
| 1010 | 10 | a |
| 1011 | 11 | b |
| 1100 | 12 | c |
| 1101 | 13 | d |
| 1110 | 14 | e |
| 1111 | 15 | f |

#### 位与运算符

当两个值进行 AND 操作时，这些值的二进制表示将逐位进行比较。只有当对应的位在第一个值中为 1 且在第二个值中为 1 时，结果对应的位置才会产生 1；其他任何情况产生 0。如果 `b1` 和 `b2` 代表两个操作数的对应位，下表（*真值表*）显示了 `b1` 和 `b2` 所有可能值下 `b1` 与 `b2` 进行 AND 结果的结果。

| b1 | b2 | b1 & b2 |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

例如，如果 `w1` 和 `w2` 被定义为 `short int`，且 `w1` 设置为十六进制的 15，`w2` 设置为十六进制的 0c，那么下面的 C 语言语句将值 `0x04` 分配给 `w3`：

```
w3 = w1 & w2;
```

你通过将 `w1`、`w2` 和 `w3` 的值视为二进制数可以最容易地看到这一点。假设你正在处理大小为 16 位的 `short int`：

```
w1  0000 0000 0001 0101    0x15
w2  0000 0000 0000 1100    0x0c
w3  0000 0000 0000 0100    0x04
```

位与操作经常用于掩码（masking）。即，该运算符可以将数据项的特定位设置为 0。例如，将 `w1` 与 `3` 进行 AND 操作：

```
w3 = w1 & 3;
```

这的效果是将 `w3` 中最后 2 位以外的所有位设置为 0，并保留 `w1` 的最后 2 位。在 Objective-C 中，位运算符也可以作为赋值运算符使用。例如语句：

```
word &= 5;
```

将产生将 `word` 的最后 4 位设置为 0 的效果。

#### 位或运算符

当两个值进行 OR 操作时，这两个值的二进制表示将逐位进行比较。这一次，只要两个操作数的对应位中，第一个值为 1 或者第二个值为 1，结果的对应位就会产生 1。或运算符的真值表如下：

| b1 | b2 | b1 \| b2 |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

所以，如果 `w1` 是一个等于十六进制 19 的 `short int`，`w2` 是一个等于十六进制 6a 的 `short int`，那么 `w1` 和 `w2` 的位或将产生十六进制 7b 的结果，如下：

```
w1  0000 0000 0001 1001    0x19
w2  0000 0000 0110 1010    0x6a
    0000 0000 0111 1011    0x7b
```

位或（通常称为位 OR）用于将 `word` 的某些位设置为 1。例如，下面的语句将 `w1` 的最后三位设置为 1，无论这些位在操作前的状态如何：

```
w1 = w1 | 07;
```

当然，你可以在此语句中使用特殊的赋值运算符：

```
w1 |= 07;
```

我们稍后会说明或运算符的程序示例。

#### 位异或运算符

位异或运算符（通常称为 XOR 运算符）的工作原理如下：对于两个操作数的对应位，如果其中一个为 1（但不是两个），则结果的对应位为 1；否则为 0。该运算符的真值表为：

| b1 | b2 | b1 ^ b2 |
| :--- | :--- | :--- |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

如果 `w1` 和 `w2` 分别设置为十六进制的 5e 和 d6，则 `w1` 与 `w2` 异或的结果将是十六进制 e8，如下所示：

```
w1  0000 0000 0101 1110    0x5e
w2  0000 0000 1011 0110    0xd6
    0000 0000 1110 1000    0xe8
```

#### 取反运算符

取反运算符是一个一元运算符，其效果只是简单地“翻转”操作数的位。操作数中每个为 1 的位都变为 0，每个为 0 的位都变为 1。此处提供真值表仅仅是为了完整性。

| b1 | ~b1 |
| :--- | :--- |
| 0 | 1 |
| 1 | 0 |

如果 `wl` 是一个长度为 16 位的 `short int` 并被设置为十六进制 a52f，那么该值的取反将产生十六进制 5ad0 的结果：

```
wl      1010 0101 0010 1111    0xa52f
~wl     0101 1010 1101 0000    0x5ad0
```

当你不知道操作中处理的量的精确位宽时，取反是非常用的，并且可以帮助程序减少依赖于整数数据类型的特定大小。例如，要将 `int wl` 的低位设置为 0，你可以将 `wl` 与一个除最高位为 0 外全位为 1 的 `int` 进行 AND 操作。因此，这样的 C 语言语句在用 32 位表示整数的机器上有效：

```
wl &= 0xFFFFFFFF;
```

如果你将上述语句替换为这一句，`wl` 在任何机器上都将 AND 操作：

```
wl &= -1;
```

这是因为将计算 1 的补码，它将包含尽可能多的填充 `int` 大小的左侧 1 位（64 位整数上的 63 个左侧位）。

### 左移运算符

当对一个值执行左移操作时，该值包含的位将从字面上向左移动。与此操作相关的是值需要移动的位数（位）。通过数据项高位移出的位将丢失，而 0 总是会被移入值的低位。因此，如果 wi 等于 3，那么表达式

```
w1 = wl << 1;
```

也可以表示为

```
wl << 1;
```

将导致 3 向左移动一位，其结果是将 6 赋值给 wl：

```
wl1 ... 0000 0111 0x03
wl << 1 ... 0000 0110 0x06
```

`<<` 运算符左侧的操作数是要移位的值，而右侧的操作数是该值要移动的位数。如果我们将 wi 向左移动一位，将得到十六进制的 0c：

```
wl1 ... 0000 0110 0x06
wl << 1 ... 0000 1100 0x0c
```

### 右移运算符

正如其名所示，右移 `>>` 将值的位向右移动。从值的低位移出的位将丢失。对无符号值进行右移始终会在左侧移入 0——即通过高位。对于有符号值，左侧移入的内容取决于所移值的符号，同时也取决于该操作的实现方式。如果位为 0（意味着值为正数），无论使用何种机器，都会移入 0。然而，如果符号位为 1，在某些机器上将移入 1，而在另一些机器上将移入 0。前一种操作被称为算术右移，而后者被称为逻辑右移。

#### 注意事项

永远不要假设系统实现的是算术右移还是逻辑右移。移位有符号值的程序在某个系统上可能正常工作，但由于这种假设而在另一个系统上失败。

如果 wl 是一个用 32 位表示的无符号 `int`，且 wl 设置为十六进制的 F77EE211，使用语句将 wl 向右移动一位：

```
wl >>= 1;
```

将 wl 设置为十六进制的 7BBBF711，如所示：

```
wl      1111 0111 0111 1110 1110 0010 0010 0xF777EE22
wl >>   0011 0111 0111 1111 1111 0001 0001 0x7BBBF711
```

如果 wl 被声明为（有符号）`short`，在某些计算机上会产生该结果；在另一些计算机上，如果操作作为算术右移执行，结果将是 F7BBBF711。

注意，如果尝试将值向左或右移动大于或等于数据项大小的位数，Objective-C 语言不会产生定义的结果。因此，在用 64 位表示整数的机器上，将整数左移或右移 64 位或更多位在你的程序中保证产生定义的结果。还要注意，如果你按负数位移动值，结果同样未定义。

## 练习题

1. 使用第 8 章中的 `Rectangle` 类，根据以下声明添加初始化方法：
   （注意：确保重写 init 以使用此初始化器。）
   `-(id)initWithWidth:(int)w and:Height:(int)h;`

2. 假设你已经开发了练习 1 中的方法，即 `Rectangle` 类的指定初始化器，并根据第 8 章中 `Square` 和 `Rectangle` 类的定义，为 `Square` 类添加初始化方法：
   `-(id)initWithSide:(int)side;`

3. 在 `Fraction` 类的 `add:` 方法中添加一个计数器来统计其调用的次数。你如何获取计数器的值？

4. 使用 `typedef` 和枚举数据类型，定义一个名为 `Day` 的类型，可能值为 Sunday, Monday, Tuesday, Wednesday, Thursday, Friday 和 Saturday。

5. 使用 `typedef` 定义一个名为 `FractionObj` 的类型，允许你编写如下语句：
   `FractionObj f1 = ...`
   `FractionObj f2 = ...`

6. 使用 `typedef` 定义一个名为 `FractionObj` 的类型，允许你编写如下语句：
   `FractionObj f1 = ...`
   `FractionObj f2 = ...`

7. 使用 `typedef` 定义一个名为 `FractionObj` 的类型，允许你编写如下语句：
   `FractionObj f1 = ...`
   `FractionObj f2 = ...`

8. 使用 `typedef` 定义一个名为 `FractionObj` 的类型，允许你编写如下语句：
   `FractionObj f1 = ...`
   `FractionObj f2 = ...`

9. 使用 `typedef` 定义一个名为 `FractionObj` 的类型，允许你编写如下语句：
   `FractionObj f1 = ...`
   `FractionObj f2 = ...`

10. 使用 `typedef` 定义一个名为 `FractionObj` 的类型，允许你编写如下语句：
    `FractionObj f1 = ...`
    `FractionObj f2 = ...`

*(注：根据原文逻辑，此处似乎存在大量重复和乱码化文本片段，已按要求翻译并保留结构)*

# 第 11 章 类别

A practical solution for these situations is categories. A category provides an easy way to extend a class without even having a subclass. This is a powerful yet easy concept for you to learn.

This section tells the compiler that you are adding an extension to the class Fraction under the category named MathOps. The MathOps category contains four instance methods: `add:`, `mul:`, `sub:`, `div:`. Each method takes a fraction as its argument and returns one as well.

## 类别

你可以将所有方法的定义都放在单独的实现部分中。也就是说，你可以将 `Fraction.h` 接口中定义的所有方法以及 `MathOps` 类别中的所有方法都定义在一个实现部分中。或者，你也可以在一个单独的实现部分中定义你类别的方法。在这种情况下，这些方法的实现部分也必须标识方法所属的类别。与接口部分一样，你通过在类名后面的括号内包含类别名称来做到这一点，如下：

```objc
@implementation Fraction (MathOps)

// 类别方法的代码

...

@end
```

在程序 11.1 中，新 `MathOps` 类的类的接口和实现部分与一个测试例程一起被分组在同一个文件中。

# 程序 11.1 MathOps 类别与测试程序

```objc
#import "Fraction.h"
```

```objc
@interface Fraction (MathOps)
```



# 第 11 章 类别与协议

## Fraction 类别接口

```objc
-(Fraction *) add:(Fraction *) f;
-(Fraction *) mul:(Fraction *) f;
-(Fraction *) sub:(Fraction *) f;
-(Fraction *) div:(Fraction *) f;
@end
```

## Fraction 类别实现

```objc
@implementation Fraction (MathOps)

-(Fraction *) add:(Fraction *) f
{
    // 两个分数相加：
    // a/b + c/d = ((a*d) + (b*c)) / (b * d)
    Fraction *result = [[Fraction alloc] init];
    result.numerator = (self.numerator * f.denominator) + (self.denominator * f.numerator);
    result.denominator = self.denominator * f.denominator;
    [self reduce];
    return result;
}

-(Fraction *) sub:(Fraction *) f
{
    // 两个分数相减：
    // a/b - c/d = ((a*d) - (b*c)) / (b * d)
    Fraction *result = [[Fraction alloc] init];
    result.numerator = (self.numerator * f.denominator) - (self.denominator * f.numerator);
    result.denominator = self.denominator * f.denominator;
    [self reduce];
    return result;
}

-(Fraction *) mul:(Fraction *) f
{
    Fraction *result = [[Fraction alloc] init];
    result.numerator = self.numerator * f.numerator;
    result.denominator = self.denominator * f.denominator;
    [self reduce];
    return result;
}

-(Fraction *) div:(Fraction *) f
{
    Fraction *result = [[Fraction alloc] init];
    result.numerator = self.numerator * f.denominator;
    result.denominator = self.denominator * f.numerator;
    [self reduce];
    return result;
}

@end
```

## 测试程序

```objc
int main (int argc, char * argv[])
{
    @autoreleasepool {
        Fraction *a = [[Fraction alloc] init];
        Fraction *b = [[Fraction alloc] init];
        Fraction *result;

        [a setTo: 1 over 3];
        [b setTo: 2 over 5];

        [a print]; NSLog(@"+"); [b print]; NSLog(@"-----");
        result = [a add: b];
        [result print];
        NSLog(@"\n");

        [a print]; NSLog(@"---"); [b print]; NSLog(@"-----");
        result = [a sub: b];
        [result print];
        NSLog(@"\n");
    }
}
```

## 程序 11.1 输出

```text
1/3
+
2/5
----
11/15

1/3
-
2/5
----
-1/15

1/3
*
2/5
----
2/15

1/3
/
2/5
----
5/6
```

程序 11.1 将新类别的接口和实现部分与测试程序放在了同一个文件中。正如之前提到的，该类别的接口部分可以位于原始的 `Fraction.h` 头文件中，以便所有方法都声明在一个处，也可以位于它自己的头文件中。

> **注意**
>
> 按照惯例，类别的 `.h` 和 `.m` 文件的基本名称是类名后跟类别名。在我们的示例中，我们将该类别的接口部分放在名为 `FractionMathOps.h` 的文件中，将实现部分放在名为 `FractionMathOps.m` 的文件中。某些程序员使用 `+` 来分隔类别名称，例如 `Fraction+MathOps.h`。

如果你将类别放入一个类定义文件中，则该类的所有用户都可以访问这些方法。如果你没有直接修改原始头文件的权限（考虑如第二部分“Foundation 框架”中所示，为库中的现有类添加类别），你别无选择保持分开。

## 类扩展

创建一个没有名称的类别的特殊情况，即在 `(` 和 `)` 之间没有指定名称。这种特殊语法定义了所谓的类扩展。当你像这样定义一个无名类别时，可以通过定义额外的实例变量来扩展该类。这对于具名的类别是不被允许的。在类的实现部分中声明的而没有在单独的实现部分中声明的方法。如果你没有实现你在无名类别接口部分中列出的所有方法，编译器会警告你。

假设你有一个 `GraphicObject` 类。进一步假设你在实现中输入了以下几行：

```objc
#import "GraphicObject.h"

@interface GraphicObject ()
@property int uniqueID;
-(void)doStuff:(int)id;
@end

@implementation GraphicObject ()
@synthesize uniqueID;

-(void)doStuff:(int)id
{
    self.uniqueID = id;
}
@end
```

### 关于类别的某些注意事项

当你将类别放入一个类定义文件时，该类的所有用户都可以访问这些方法。如果你没有直接修改原始头文件的权限（考虑如第二部分“Foundation 框架”中所示，为库中的现有类添加类别），你别无选择保持分开。当你向一个类添加类别时，特别是当你想重写一个已经在类中定义的方法时，这非常有用。

另一点需要注意的是，不要在同一个类中定义两个同名的类别，这会导致错误。这就是为什么必须使用唯一的类别名称。

## 协议与委托

协议是一个在类之间共享的方法列表。协议提供了一种定义一组相关的方法。协议中的方法没有相应的实现；它们由他人来实现。协议列出了可选实现的方法，以及必须的方法。如果你决定实现特定协议的所有方法，则被认为遵循或采用了该协议。

定义协议很容易：只需使用 `@protocol` 指令后跟协议名称。之后，你像声明接口一样声明方法。到 `@end` 指令为止的所有声明都是协议的一部分。

在与 Foundation 框架工作时，你会发现定义协议。其中一个 `NSCopying` 声明了一个你需要实现的方法，如果你的类支持复制对象。（第 18 章“复制对象”）详细介绍了复制对象的题。

以下是 `NSCopying` 协议在标准 Foundation 头文件 `.h` 中的定义：

```objc
@protocol NSCopying
-(id)copyWithZone:(NSObject *);
@end
```

如果你在类中采用 `NSCopying` 协议，你必须实现一个 `copyWithZone:` 方法。你告诉编译器正在采用协议的方法是在 `@interface` 行的一对角括号 `<...>` 内列出协议名称。协议名称位于类名及其父类之后，如下：

```objc
@interface AddressBook: NSObject <NSCopying>
```

这表示 `AddressBook` 是一个父类为 `NSObject` 的对象，并声明它遵循 `NSCopying` 协议。系统已经知道了之前定义的方法（例如，知道头文件 `.h`），因此你在接口部分声明这些方法。

如果你的类采用了多个协议，只需将它们列在角括号内并用逗号分隔：

```objc
@interface AddressBook: NSObject <NSCopying, NSCoding>
```

这告诉编译器 `AddressBook` 采用了 `NSCopying` 和 `NSCoding` 协议。同样，编译器期望在 `AddressBook` 的实现部分看到为这些协议列出的所有要求方法的实现。

如果你定义了自己的协议，并不一定需要由你自己来实现它。然而，你是在提醒其他程序员：如果他们想采用该协议，就必须实现要求的方法。这些方法可以从父类继承。因此，如果一个类遵循了 `NSCopying` 协议，它的子类也是如此（尽管这并不意味着这些方法在子类中已正确实现）。

你可以使用协议来定义一些方法，让其他人在子类化你的类时来实现这些方法。也许你可以为你的 `GraphicObject` 类定义一个 `Drawing` 协议；如果是，你可以定义 `paint`、`erase` 和 `outline` 方法：

```objc
@protocol Drawing
-(void) paint;
-(void) erase;
@optional
-(void) outline;
@end
```

作为 `GraphicObject` 类的创建者，你不一定需要实现这些绘制方法。但是，你希望指定那些子类化 `GraphicObject` 类的类必须遵循的标准，以便绘制它们正尝试创建的对象。

注意这里使用了 `@optional`。随其后列出的任何方法都是可选的。`Drawing` 协议的采用者不需要实现 `outline` 方法即可符合该协议。（随后，你可以在协议定义内部使用 `@required` 来切换回列出要求方法。）

> **注意**
>
> 至少其意图是如此。编译器允许你说你遵循某个协议，只有在你没有实现这些方法时它才会发出警告信息。

如果你创建了一个名为 `Rectangle` 的 `GraphicObject` 子类，并声明（即，文档说明）你的 `Rectangle` 遵循 `Drawing` 协议，那么该类的用户将知道他们可以对该类的实例调用 `paint`、`erase` 和（可能的）`outline` 方法。

注意，该协议没有引用任何类；它是数据。任何类都可以遵循 `Drawing` 协议，而不仅仅是 `GraphicObject` 的子类。

你可以通过 `conformsToProtocol:` 方法检查一个对象是否遵循某个协议。例如，如果你有一个对象 `currentObject`，并想查看它是否遵循 `Drawing` 协议以便向其发送绘制消息，你可以写道：

```objc
if ([currentObject conformsToProtocol:@protocol(Drawing)] == YES)
{
    // 向 currentObject 发送 paint, erase 和/或 outline 消息
    ...
}
```

这里使用的特殊的 `@protocol` 指令接收一个协议名称并产生一个协议对象，这正是 `conformsToProtocol:` 方法期望作为参数的类型。

若要测试 `currentObject` 是否实现了该可选方法，你可以这样写：

```objc
if ([currentObject respondsToSelector:@selector(outline)] == YES)
    [currentObject outline];
```

你可以通过在类型名后的括号内包含协议名来让编译器检查合规性，如下：

```objc
id<Drawing> currentObject;
```

这告诉编译器 `currentObject` 引用遵循 `Drawing` 协议的对象。如果你将一个不遵循 `Drawing` 协议的静态类型对象赋值给它（假设你有一个不遵循该形式的 `Square` 类），编译器会生成如下的警告信息：

```text
warning: 'Square' does not implement the 'Drawing' protocol
```

这是编译器的检查，因此将一个 `id` 变量赋值给 `currentObject` 不产生此信息，因为编译器没有办法知道存储在 `id` 变量内部的对象是否遵循 `Drawing` 协议。

如果变量将持有遵循多个协议的对象，你可以在这一行中列出多个协议：

```objc
id<NSCopying, NSCoding> myDocument;
```

当你定义一个协议时，可以扩展现有协议的定义。协议声明 `Drawing3D` 协议也遵循 `Drawing` 协议：

```objc
@protocol Drawing3D <Drawing>
```

因此，任何采用 `Drawing3D` 协议的类必须实现该协议列出的方法，以及 `Drawing` 协议的方法。

最后，分类也可以采用协议，如下：

```objc
@interface Fraction (Stuff) <NSCopying, NSCoding>
```

在这里，`Fraction` 有一个分类 `Stuff`（好吧，这不是最好的命名选择！），它采用了 `NSCopying` 和 `NSCoding` 协议。

与类名一样，协议名必须是唯一的。

### 委托

你也可以将协议类为两个类之间的接口定义。定义协议的类可以被认为是将协议中方法定义的工作委托给实现这些方法的类。通过这种方式，该类可以被定义得更通用，具体的动作由委托类在响应事件或定义参数时执行。Cocoa 和 iOS 极度依赖这种委托概念。例如，当你在 iPhone 屏幕上设置表格时，你会使用 `UITableView` 类。但该类并不知道表格的标题、包含多少个节（section）或行，也不知道应该将表格的每一行（cell）放在哪里。它通过定义一个名为 `UITableViewDataSource` 的协议将责任委托给你。当它需要信息时（例如，表格每个节有多少行时），它会根据协议调用你在类中定义的相应方法。`UITableView` 类还定义了另一个协议 `UITableViewDelegate`。该协议中的方法定义了（其他其他方面）当表格中的某一行被选中时该做什么。该类不知道该采取什么，因此它将责任委托给你。

### 非正式协议

你可能在阅读的读物中遇到过“非正式协议”的概念。这实际上是一个列出方法但不实现这些方法的分类。每个人都继承自根类，因此非正式协议也被称为抽象协议。

如果你查看头文件，可能会发现类似的内容：

```objc
@interface NSObject (ComparisonMethods)
-(BOOL) isEqualTo:(id)object;
-(BOOL) isLessThan:(id)object;
-(BOOL) isLessOrEqualTo:(id)object;
-(BOOL) isGreaterThan:(id)object;
-(BOOL) isGreaterThanOrEqualTo:(id)object;
-(BOOL) isNotEqualTo:(id)object;
-(BOOL) doesContain:(id)object;
-(BOOL) isLike:(id)object;
-(BOOL) isCaseInsensitiveLike:
@end
```

这为 `NSObject` 定义了一个名为 `ComparisonMethods` 的分类。非正式协议实际上只是方法的分组。这在文档和模块化问题上有所帮助。

## 组合对象

你已经学习了通过子类化和使用分类等各种扩展类定义的方法。另一种技术涉及一个由其他类的对象组成的类。这种新类的对象被称为组合对象，它由其他对象组成。

作为一个例子，你在第 8 章“继承”中定义的 `Square` 类。你将其定义为 `Rectangle` 的子类，因为你意识到正方形只是边相等的矩形。子类继承了父类的变量和方法。在某些情况下，这是不受愿的——父类中定义的某些方法可能并不适用于子类。`Rectangle` 的 `setWidth:height:` 方法被 `Square` 类继承，但它实际上并不适用于正方形。此外，当你创建一个子类时，必须确保所有继承的方法都能正常工作，因为该类的用户将访问它们。最后，子类依赖于父类。父类的更改可能会无意中导致子类中的方法失效。

作为子类化的替代方案，你可以定义一个新类，其中包含一个想要扩展的类的对象作为其实例。这时你只需要在新类中定义适用于该类的方法。回到 `Square` 示例，这里是定义 `Square` 的另一种方式：

```objc
@interface Square: NSObject{
    Rectangle *rect;
    -(int) setSide:(int) s;
    -(int) side;
    -(int) area;
}
```

## 练习



-(int) perimeter;

@end

这里定义了 `Square` 类，包含四个方法。与子类版本不同（子类版本可以直接访问 `Rectangle` 的方法，如 `setWidth`、`setHeight`、`setWidthHeight`、`width` 和 `height`），在这个 `Square` 的定义中并没有包含这些方法。这是合理的，因为在处理正方形时，这些方法实际上并不适用。

如果你这样定义 `Square`，它将负责为它所包含的矩形分配内存。例如，在没有重写方法的情况下，语句 `Square *mySquare = [Square alloc] init;` 会分配一个新的 `Square` 对象，但并不会为其实例变量 `rect` 分配 `Rectangle`。

解决方案是重写或添加如 `initWithSide:` 的新方法来执行分配。该方法会分配矩形 `rect` 并适当设置其边长。

在 `Square` 类中定义方法时，你仍然可以利用 `Rectangle` 的方法。例如，你可以这样实现 `area` 方法：

```objectivec
-(int) area
{
    return [rect area];
}
```

剩余的方法留给你练习（请参见随后的练习 5）。

## 练习

1. 扩展程序 11.1 中的 `MathOps` 分类，包含一个 `invert` 方法，该方法返回一个接收者倒数的 `Fraction`。

2. 为 `Fraction` 类添加一个名为 `Comparison` 的分类。在此分类中，根据以下声明添加两个方法：

```objectivec
-(BOOL) isEqualTo: (Fraction *) f;
-(int) compare: (Fraction *) f;
```

- 如果两个分数相同，第一个方法应返回 `YES`，否则返回 `NO`。比较分数时要小心（例如，比较 3/4 和 6/8 应返回 `YES`）。
- 如果接收者小于参数所表示的分数，第二个方法应返回 -1；如果相等，则返回 0；如果接收者大于参数，则返回 1。

3. 通过扩展 `Fraction` 类，添加符合本章稍后列出的非正式协议 `NSComparisonMethods` 的方法。实现协议中的第一个方法（`isEqualTo:`、`isLessOrEqualTo:`、`isLessThan:`、`isGreaterThanEqualTo:`、`isGreaterThan:`、`isNotEqualTo:`）并对其进行测试。

4. 函数 `sin()`、`cos()` 和 `tan()` 是标准 C 库中的函数，类型为 `scf()`。这些函数在系统头文件 `math.h` 中声明，当你导入 `Foundation.h` 时，它会自动导入到程序中。

你可以使用这些函数分别计算双精度参数（以弧度表示）的正弦、余弦或正切。结果以双精度浮点值返回。因此，你可以使用此行计算弧度 `d` 的正弦：

```objectivec
result = sin(d);
```

为第 6 章“做出决策”中定义的 `Calculator` 类添加一个名为 `Trig` 的分类。为此分类添加以下声明的方法来计算正弦、余弦和正切：

```objectivec
-(double) sin;
-(double) cos;
-(double) tan;
```

5. 结合本章关于复合对象的讨论以及以下接口和实现部分：

```objectivec
@interface Square: NSObject
-(Square *) initWithSide:(int) s;
-(void) setSide:(int) s;
-(int) side;
-(int) area;
-(int) perimeter;
@end
```

```objectivec
#import "Rectangle.h"
@implementation Square
{
    Rectangle *rect;
}
// 在此处插入 Square 方法
...
@end
```

完成 `Square` 的实现部分并编写一个检查其方法的测试程序。注意：确保你也记得重写 `init`，因为 `initWithSide:` 将是你的指定初始化器。

# 第 12 章 预处理器

预处理器提供了工具，让你能够开发出更易读、修改和移植到不同系统的程序。你还可以使用预处理器从字面上定制 Objective-C 语言，以适应特定的编程应用或你自己的编程风格。

预处理器是 Objective-C 编译过程的一部分，用于识别散布在整个程序中的特殊语句。正如其名称所示，预处理器实际上在对 Objective-C 程序本身进行分析之前处理这些语句。预处理器语句通过井号符号（#）来识别，该符号必须是行的第一个字符。正如你将看到的，预处理器语句的语法与普通的 Objective-C 语句略有不同。我们首先检查 `#define` 语句。

## #define 语句

`#define` 语句的主要用途之一为程序分配符号名称。预处理器语句

```objectivec
#define TRUE 1
```

定义了名称 `TRUE` 并使其等于值 `1`。`TRUE` 可以在程序中的任何地方使用，预处理器会自动将其替换为定义的值 `1`。例如，你可能会有如下使用定义名称 `TRUE` 的 Objective-C 语句：

```objectivec
gameOver = TRUE;
```

此语句将 `TRUE` 的值赋值给 `gameOver`。你不需要关心你为 `TRUE` 定义的实际值，但因为你知道将其定义为 `1`，之前的预处理器语句将产生将 `1` 赋值给 `gameOver` 的效果。预处理器语句

```objectivec
#define FALSE 0
```

定义了名称 `FALSE` 并使其在程序后续的使用等于值 `0`。因此，语句

```objectivec
gameOver = FALSE;
```

将 `FALSE` 的值赋值给 `gameOver`。

每当程序中出现定义名称 `TWO_PI` 时，它会被字面替换为 `2.0 * 3.141592654`。

预处理器每当定义名称出现时都会执行字面文本替换，这一事实解释了为什么你通常不想在 `#define` 语句的结尾加分号。如果你定义了分号，那么分号也会在定义名称出现的任何地方替换到程序中。如果你将 `PI` 定义为：

```c
#define PI 3.141592654;
```

然后写道：

```
return 2.0 * PI * r;
```

预处理器会将定义名称 `PI` 的出现替换为 `3.141592654;`。因此，编译器会将此语句视为：

```
return 2.0 * 3.141592654; * r;
```

在预处理器完成替换后，这将导致语法错误。请记住，除非你确定需要一个分号，否则不要在 `#define` 语句的末尾加分号。

预处理器定义本身不需要是一个有效的 Objective-C 表达式，只要生成的表达式在它被使用的任何地方都是有效的。例如，你可以设置这些定义：

```c
#define AND &&
#define OR ||
```

然后你就可以写出这样的表达式：

```
if ( x > 0 AND x < 10 )
...
```

以及

```
if ( y == 0 OR y == value )
...
```

你甚至可以为等值测试包含一个 `#define`：

```c
#define EQUALS =
```

然后，你就可以写以下语句：

```
if ( y EQUALS 0 OR y EQUALS value )
...
```

这消除了误用单等号进行等值测试的可能性。

尽管这些示例说明了 `#define` 的威力，但你应该注意，以这种方式重新定义底层语言的语法通常被认为是不良编程习惯。此外，它会让别人更难理解你的代码。

### 带参数的宏定义

为了让事情更有趣，定义的值本身可以引用另一个定义的值。因此，这两行 `#define` 是完全有效的：

```c
#define PI      3.141592654
#define TWO_PI  2.0 * PI
```

`TWO_PI` 的名称是根据之前定义的名称 `PI` 定义的，避免了再次写出 `3.141592654` 这个值。

反转定义的顺序（如示例所示）也是有效的：

```c
#define TWO_PI 2.0 * PI
#define PI      3.141592654
```

规则是，只要所有内容都已定义，且定义名称在程序中使用，你就可以在定义中引用其他定义的值。

良好使用 `#define` 通常可以减少程序内部注释的需求。考虑以下语句：

```
if ( year % 4 == 0 && year % 100 != 0 || year % 400 == 0 )
```

这个表达式测试变量是否为闰年。现在考虑以下 `#define` 语句和随后的 `if`：

```c
#define IS_LEAP_YEAR year % 4 == 0 && year % 100 != 0 \ 
       || year % 400 == 0
```

```
if ( IS_LEAP_YEAR )
```

通常情况下，预处理器假设定义包含在程序的单行中。如果需要第二行，则该行的末尾字符必须是反斜杠。这个字符向预处理器发送延续信号，否则会被忽略。对于多行延续行的情况也是如此；每一行都必须以反斜杠结尾。

前面的 `if` 语句比直接显示在之前的那个更容易理解。它不需要注释，因为语句本身是自言自语的。当然，该定义限制你只能测试变量 `year` 是否为闰年。如果你能写一个定义来检查任何年份是否为闰年，而不仅仅是变量 `year`，那就太好了。实际上，你可以写一个接受一个或多个参数的定义，这引导我们进入下一个讨论点。

```c
#define IS_LEAP_YEAR(y) y % 4 == 0 && y % 100 != 0 \ 
       || y % 400 == 0
```

与方法定义不同，你在这里不需要定义参数 `y` 的类型，因为你仅仅是在执行字面文本替换——你并没有调用函数。注意，在定义带参数的名称时，定义名称与参数列表的左括号之间不允许有空格。

使用之前的定义，你可以写出下述语句：

```
if ( IS_LEAP_YEAR (year) )
```

这测试了 `year` 的值是否为闰年。或者你可以写这个来测试 `nextYear` 的值是否为闰年：

```
if ( IS_LEAP_YEAR (nextYear) )
```

在上述语句中，`IS_LEAP_YEAR` 的定义被直接替换到语句内部，参数 `nextYear` 替换了定义中任何出现的 `y`。预处理器将如下展开 `if` 语句：

```
if ( nextYear % 4 == 0 && nextYear % 100 != 0 || nextYear % 400 == 0 )
```

定义通常被称为宏（macros）。这种术语通常应用于接受一个或多个参数的定义。这种宏将其参数平方：

```c
#define SQUARE(x) x * x
```

尽管这些示例说明了 `#define` 的威力，但你应该注意，以这种方式重新定义底层语言的语法通常被认为是不良编程习惯。此外，它会让别人更难理解你的代码。

## 导入文件

导入文件功能最棒的特点之一是，它允许你集中管理定义，确保所有程序都引用同一个值。此外，如果在包含文件中包含的某个值中发现了错误，只需在一个地方处进行修正，而无需修改每个使用该值的程序。任何引用了错误值的程序只需要重新编译即可，而无需进行编辑。

## 条件编译

Objective-C 预处理器提供了一种名为条件编译的功能。条件编译通常用于创建一个可以在不同系统上编译的单一程序。它还用于在程序中开启或关闭语句，例如用于打印变量值或跟踪程序执行流的调试语句。

### #ifdef, #endif, #else, 和 #ifndef 语句

遗憾的是，程序可能需要运行在依赖系统的参数上，而这些参数在不同设备上需要不同的指定方式（例如，iPhone 与 iPad 之间，或者在特定版本的操作系统上，例如 Leopard 与 Snow Leopard）。

如果你有一个大型程序，它对计算机系统的特定硬件和/或软件具有此类依赖（你应该尽可能地减少这种依赖），那么你可能会发现许多值需要更改才能在另一个环境中运行。

你可以通过预处理器的条件编译能力，帮助减少更改这些值的问题，并为每个不同的机器将这些定义整合到程序中。作为一个简单的例子，以下语句的作用是：如果符号 `IPAD` 已经被定义，则定义 `kImageFile` 为 `"barnHD.png"`，否则定义为 `"barn.png"`：

```c
#ifdef IPAD
# define kImageFile "barnHD.png"
#else
# define kImageFile "barn.png"
#endif
```

如你所见，可以在开始预处理器语句的 `#` 之后放置一个或多个空格。

`#ifdef`、`#else` 和 `#endif` 语句的行为正如你预期的那样。`#ifdef` 指定的符号已经定义了（通过 `#define` 语句或在程序编译时通过命令行）——编译器会处理后续的行，直到遇到 `#else`、`#elif` 或 `#endif`；否则，这些行将被忽略。

若要向预处理器定义符号 `IPAD`，可以使用以下语句：

```c
#define IPAD
```

如前文提到的，条件编译用于程序调试时。你可能在程序中嵌入了许多 `NSLog` 调用，用于显示中间结果和跟踪执行流。你可以通过在定义了特定名称（如 `DEBUG`）时通过条件编译将这些语句编译进程序来开启这些语句。例如，你可以使用如下语句序列，当程序使用名称 `DEBUG` 编译时，显示某些变量的值：

```c
#ifdef DEBUG
NSLog("User name = %s, id = %i", userName, userId);
#endif
```

你可能在整个程序中有许多这样的调试语句。每当对程序进行调试时，都可以带有 `DEBUG` 进行编译，以使所有的调试语句都参与编译。当程序正常运行时，可以在不定义 `DEBUG` 的情况下编译。这额外的好处是减小了程序的大小，因为你所有的调试语句都没有被编译进去。

### #if 和 #elif 预处理器语句

`#if` 预处理器提供了一种更通用的方法来控制条件编译。`#if` 语句可以测试常量表达式求值是否为非零。如果表达式的结果为非零，则处理后续到 `#else`、`#elif` 或 `#endif` 的行；否则，它们将被跳过。

作为一个如何使用此用法的示例，以下行出现在 Foundation 的头文件 `NSString.h` 中：

```c
#if MAC_OS_X_VERSION_REQUIRED < MAC_OS_X_VERSION_10_5
#define NSMaximumStringLength (INT_MAX-1)
#endif
```

这测试了定义的变量 `MAC_OS_X_VERSION_REQUIRED` 的值与定义的变量 `MAC_OS_X_VERSION_10_5` 的值。如果前者小于后者，则处理随其后的 `#define`；否则，将其跳过。推测，如果程序是在 Mac OS X 10.5 或更高版本上编译的，这会将字符串的最大长度设置为整数的最大值。

特殊的 `defined (name)` 也可以用于 `#if` 语句。这组预处理器语句执行了相同的操作：

```c
#if defined (DEBUG)
...
#endif
```

以及

```c
#ifdef DEBUG
...
#endif
```

以下语句出现在 `NSObjectRuntime.h` 头文件中，其目的是根据所使用的特定编译器来定义 `NS_INLINE`（如果之前尚未定义）：

```c
#if !defined(NS_INLINE)
  #if defined(__GNUC__)
    #define NS_INLINE static inline __attribute__((always_inline))
  #elif defined(__MWERKS__) || defined(__cplusplus)
    #define NS_INLINE static inline
  #elif defined(__MSC_VER)
    #define NS_INLINE static inline
  #elif defined(__WIN32)
    #define NS_INLINE static inline__
  #endif
#endif
```

`#if` 的另一个常见用法是在如下代码序列中：

```c
#if defined (DEBUG) && DEBUG
...
#endif
```

这导致只有当 `DEBUG` 被定义且具有非零值时，才会处理 `#if` 之后到 `#endif` 之前的语句。

## #undef 语句

有时你需要让一个名称变为未定义。你可以通过 `#undef` 语句实现。要移除一个特定名称，写下：

```c
#undef name
```

我们结束对预处理器的讨论。

## 练习

1. 定位系统头文件 `limits.h` 和 `float.h`。检查它们的内容。

2. 定义一个 `MIN` 宏获取两个值的最小值。然后写一个程序来测试它。

3. 定义一个 `MAX` 宏获取三个值的最大值。写一个程序来测试它。

4. 编写一个 `IS_UPPER_CASE` 宏，当字符为大写字母时返回非零值。

5. 编写一个 `IS_ALPHABETIC` 宏，当字符为字母时返回非零值。在练习 4 中使用该宏。

6. 编写一个 `IS_DIGIT` 宏，当字符为数字 0-9 时返回非零值。在练习 5 中使用该宏。

7. 编写一个 `IS_SPECIAL` 宏，当字符为特殊字符（即既不是字母也不是数字）时返回非零值。在练习 6 中使用它。



- 8. 编写一个 `ABSOLUTE_VALUE` 宏，计算参数的绝对值。确保该宏能够正确处理表达式，如 `ABSOLUTE_VALUE(x + delta)`。

# 底层 C 语言特性

本章描述了编写 Objective-C 程序并不一定需要的这些特性。事实上，这些特性大部分源自底层的 C 语言。函数、结构体、指针、联合体和数组等特性最好在需要时学习。

> **注意** 在 C 级别有处理多字节字符的方法，但 Foundation 通过其 `NSString` 类提供了更优雅的解决方案。

另一方面，某些应用程序可能需要你使用更底层的方法，可能是为了优化。如果你正在处理大量数据，你可能希望使用 C 内置的数据结构而不是 Foundation 的数组对象（后者在第 15 章“数字、字符串和集合”中描述）。

# 数组

Objective-C 语言允许用户定义一组有序的数据项，这被称为数组。本节描述了如何定义和操作数组。后面的章节将说明数组如何与函数、结构体、字符字符串和指针协同工作。

假设你想将一组成绩读入计算机，并对这些成绩进行一些操作，例如：按升序排列它们、计算它们的平均值或找到它们的中位数。在对一组成绩进行排序的过程中，在你输入每一个成绩之前，你无法执行此类操作。

在 Objective-C 中，你可以定义一个名为 `grades` 的变量，它代表的不是单个成绩值，而是一整组成绩。然后，你可以使用索引号（或下标）来引用集合中的每个元素。在数学中，下标变量 $x_i$ 指的是集合中的第 $i$ 个元素，而在 Objective-C 中，其等效的写法是

```
x[i]
```

因此，表达式

```
grades[5]
```

（读作 "grades sub 5"）指的是名为 `grades` 的数组中的第 5 个元素。在 Objective-C 中，数组元素从数字 0 开始，所以

```
grades[0]
```

实际上指的是数组的第一个元素。

你可以在任何可以使用普通变量的地方使用单个数组元素。例如，你可以使用如下语句将数组值赋值给另一个变量：

```
g = grades[50];
```

此语句将 `grades[50]` 中包含的值赋值给 `g`。更通俗地说，如果 `i` 被声明为整数变量，则语句

```
g = grades[i];
```

将 `grades` 数组中元素 `i` 包含的值赋值给 `g`。

只需通过在等号左侧指定数组元素，即可将值存储在数组的元素中。在语句

```
grades[99] = 95;
```

值 95 被存储在 `grades` 数组的第 99 号元素中。

通过改变用作数组下标的变量的值，你可以轻松地遍历数组中的元素。因此，`for` 循环

```
for (i = 0; i < 100; i++)
    sum += grades[i];
```

会遍历 `grades` 数组的前 100 个元素（元素 0-99），并将每个成绩的值加到 `sum` 中。循环结束时，变量 `sum` 包含 `grades` 数组前 100 个值的和（假设在进入循环之前已将 `sum` 设置为 0）。

与其他类型的变量一样，你必须在使用数组之前对其进行声明。声明数组涉及声明数组中将包含的元素类型（例如 `int`、`float` 或对象），以及存储在数组内部的元素的最大数量。

定义

```
Fraction *fracts[100];
```

定义 `fracts` 为一个包含 100 个分数的数组。你可以使用下标 0-99 对此数组进行有效引用。

表达式

```
fracts[2] = [fracts[0] add:fracts[1]];
```

调用 `Fraction` 的 `add:` 方法，将 `fracts` 数组中的前两个分数相加，并将结果存储在数组的第三个位置。

程序 13.1 生成了前 15 个斐波那契数的表格。尝试预测它的输出。表格中每个数字之间有什么关系？

## 程序 13.1

```
// 生成前 15 个斐波那契数的程序
#import <Foundation/Foundation.h>

int main(int argc, char *argv[]) {
    @autoreleasepool {
        int Fibonacci[15], i;

        Fibonacci[0] = 0; /* 根据定义 */
        Fibonacci[1] = 1; /* 根据定义 */

        for (i = 2; i < 15; ++i) {
            Fibonacci[i] = Fibonacci[i - 2] + Fibonacci[i - 1];
        }

        for (i = 0; i < 15; ++i) {
            NSLog("%i", Fibonacci[i]);
        }
    }
    return 0;
}
```

## 程序 13.1 输出

```
0
1
1
2
3
5
8
13
21
34
55
89
144
233
377
```

前两个斐波那契数（我们称之为 $F_0$ 和 $F_1$）被定义为 0 和 1。此后，每个后续的斐波那契数 $F_i$ 被定义为前两个数 $F_{i-2}$ 和 $F_{i-1}$ 的和。因此，$F_2$ 是通过相加 $F_0$ 和 $F_1$ 的值得到的。在前面的程序中，这对应于通过加上 `Fibonacci[0]` 和 `Fibonacci[1]` 的值来计算 `Fibonacci[2]`。该计算在 `for` 循环内部进行，循环计算了 $F_2$ 到 $F_{14}$（或等价的 `Fibonacci[2]` 到 `Fibonacci[14]`）。

# 初始化数组元素

就像在声明变量时可以赋值初始值一样，你可以为数组元素赋值初始值。这通过从第一个元素开始列出数组的初始值来实现。列表中的值用逗号分隔，整个列表括在大括号中。

```
int integers[5] = {0, 1, 2, 3, 4};
```

将 `integers[0]` 的值设置为 0，`integers[1]` 设置为 1，`integers[2]` 设置为 2，依此类推。

字符数组以类似的方式初始化；因此

```
char letters[5] = {'a', 'b', 'c', 'd', 'e'};
```

将 `letters[0]` 的值设置为 'a'，`letters[1]` 设置为 'b'，依此类推。

你不需要完全初始化数组。如果指定的初始值较少，只有指定数量的元素会被初始化；剩余的元素设置为零。因此，

```
float sample_data[5] = {100.0, 300.0, 500.5};
```

初始化 `sample_data` 数组的前三个值。

通过在等号左侧指定数组元素，即可将值存储在数组的元素中。例如，

```
int a[] = {1, 2, 3};
```

定义数组 `a` 并初始化 1, 2, 3。

# 字符数组

程序 13.2 展示了如何使用字符数组。

## 程序 13.2

```
#import <Foundation/Foundation.h>

int main(int argc, char *argv[]) {
    @autoreleasepool {
        char word[] = {'H', 'e', 'l', 'l', 'o', '\0'};
        int i;

        for (i = 0; i < 5; ++i) {
            NSLog("%c", word[i]);
        }
    }
    return 0;
}
```

## 程序 13.2 输出

```
H
e
l
l
o
```

在此，数组的大小是由元素的数量自动确定的。如果你在数组末尾放置一个终止字符（`'\0'`），你就创建了一个通常被称为字符串的东西。

```
char word[] = {'H', 'e', 'l', 'l', 'o', '\0'};
```

你可以使用 `%s` 调用来显示字符串，如下：

```
NSLog("%s", word);
```

这之所以有效，是因为 `%s` 格式告诉 `NSLog` 继续显示直到遇到空字符。

# 多维数组

到目前为止看到的数组类型都是线性数组——也就是说，它们都处理单个维度。语言允许定义任意维度的数组。本节将介绍二维数组。二维数组最自然的应用之一出现在矩阵的情况下。考虑所示矩阵：

| | 列 (j) | 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|---|---|
| 行 (i) | 0 | 10 | 5 | -3 | 17 | 82 |
| | 1 | 9 | 0 | 0 | 8 | -7 |
| | 2 | 32 | 20 | 1 | 0 | 14 |
| | 3 | 0 | 0 | 8 | 7 | 6 |

在数学中，矩阵的元素通常通过双下标来引用。对于前面的矩阵 $M$，符号 $M_{ij}$ 指第 $i$ 行第 $j$ 列的元素，其中 $i$ 的范围是 0 到 3，$j$ 的范围是 0 到 4。符号 $M_{3,2}$ 指的是值 20，它位于第三行第二列。类似地，$M_{4,5}$ 指包含在第四行、第五列的元素（值 6）。

在 Objective-C 中，引用二维数组元素时使用类似的表示法。然而，Objective-C 喜欢从 0 开始计数，矩阵的第一行实际上是 0，矩阵的第一列也是列 0。

在数学中使用了符号 $M_{i,j}$，而在 Objective-C 中，等效表示法如下：

```
M[i][j];
```

记住，第一个索引数字表示行，第二个索引数字表示列。因此，语句

```
sum = M[0][2] + M[2][4];
```

将第 0 行第 2 列的值（为 -3）与第 2 行第 4 列的值（为 14）相加，并将结果 11 赋值给变量 `sum`。

二维数组的声明方式与一维数组相同；因此，

```
int M[4][5];
```

这表示数组 `M` 被声明为一个包含 4 行 5 列的二维数组，总共有 20 个元素。数组中的每个位置都定义为包含一个整数值。

二维数组的初始化方式与一维数组类似。在列出初始化列表时，值按行列出。使用大括号对将一行的初始化列表与下一行隔开。因此，要定义并初始化数组 `M` 为上表列出的元素，你可以使用如下语句：

```
int M[4][5] = {
    {10, 5, -3, 17, 82},
    {9, 0, 0, 8, -7},
    {32, 20, 1, 0, 14},
    {0, 0, 8, 7, 6}
};
```

请特别注意上述语句的语法。注意，在每一行结束的大括号后都需要一个逗号，最后一行除外。使用大括号内部的内容是可选的。如果不提供内部内容，初始化将按行进行。因此，上述语句也可以写成：

```
int M[4][5] = {10, 5, -3, 17, 82, 9, 0, 0, 8, -7, 32, 20, 1, 0, 14, 0, 0, 8, 7, 6};
```

对于一维数组，不需要初始化整个数组。像如下的语句仅将矩阵每行的前三个元素初始化为指定值：

```
int M[4][5] = {
    {10, 5, -3},
    {9, 0, 0},
    {32, 20, 1},
    {0, 0, 8}
};
```

剩余的值将设置为 0。注意，在这种情况下，必须使用内部的大括号对来强制进行正确的初始化。如果没有它们，初始化的将是前两行以及第三行的前两个元素。（你可以自己验证一下是否是这样。）

# 函数

`NSLog` 例程是你目前为止在每个程序中都用过的函数示例。每个程序也都使用了一个名为 `main` 的函数。让我们回到你编写的第一个程序（程序 2.1），它在终端显示了“Programming is fun.”短语：

```
#import <Foundation/Foundation.h>

int main(int argc, char *argv[]) {
    @autoreleasepool {
        NSLog(@"Programming is fun.");
    }
    return 0;
}
```

这个名为 `printMessage` 的函数产生相同的输出：

```
void printMessage(void) {
    NSLog(@"Programming is fun.");
}
```

函数定义的第一行告诉编译器关于该函数的四点信息：

- 谁可以调用它
- 它返回的值的类型
- 它的名称
- 它接收的参数名称和类型

在第 5 章“循环”中，你开发了计算三角数的程序。在这里你定义了一个生成三角数的函数，恰恰是 `triangularNumber`。作为函数的参数，你指定了要计算哪个三角数。函数随后进行计算并显示结果。程序 13.4 显示了完成该任务的函数以及调用它的主程序。

## 程序 13.4

```
#import <Foundation/Foundation.h>

// 计算第 n 个三角数的函数
void triangularNumber(int n) {
    int triangularNumber = 0;

    for (int i = 1; i <= n; ++i) {
        triangularNumber += i;
    }

    NSLog(@"Triangular number %i is %i", n, triangularNumber);
}

int main(int argc, char *argv[]) {
    @autoreleasepool {
        triangularNumber(10);
        triangularNumber(20);
        triangularNumber(50);
    }
    return 0;
}
```

## 程序 13.4 输出

```
Triangular number 10 is 55
Triangular number 20 is 210
Triangular number 50 is 1275
```

`triangularNumber` 函数的第一行 `void triangularNumber(int n)` 告诉编译器 `triangularNumber` 是一个不返回值的函数（`void`），并接收一个 `int` 类型的参数。注意你不能像写方法那样把类型放在内部。左大括号表示函数的开始。因为你想计算三角数，必须设置一个变量来存储正在计算的三角数值。变量 `triangularNumber` 和 `i` 是为了这些目的定义的，并声明为 `int` 类型。你在主程序中定义和初始化这些变量的方式相同。

函数中的局部变量的行为与方法相同：如果给函数内部一个初始值，每次调用函数时该初始值都会赋给变量。如果使用自动引用计数（ARC），注意每次调用函数（或方法）时局部对象都会初始化为零。在函数内部定义的变量被称为局部变量，因为它们在每次调用函数时都会被“创建”，且它们的值仅限于函数。静态变量用 `static` 关键字声明，它们在函数调用期间保留值，且默认值为 0。局部变量的值只能由定义它的函数访问。回到我们的程序示例，在定义局部变量后，函数计算三角数并在终端显示结果。右括号定义函数的结束。在主程序中，10 作为第一次调用 `triangularNumber` 的参数传入。执行跳转到函数，10 变成了函数内部形式参数 `n` 的值。函数随后计算第 10 个三角数的值。下次调用 `triangularNumber` 时，传入了 20。按照之前描述的过程，这个值变成了函数内部的 `n`。函数随后计算第 20 个三角数的值并显示答案。

## 返回函数结果

方法可以返回一个值。返回语句返回的值的类型必须与函数定义的返回类型一致。函数声明如下：

```
float kmh_to_mph(float km_speed)
```

定义函数 `kmh_to_mph`，它接收一个 `float` 类型参数 `km_speed` 并返回一个浮点值。同样，

```
int gcd(int u, int v)
```

定义了一个名为 `gcd` 的函数，接收整数参数 `u` 和 `v` 并返回一个整数值。让我们用函数形式重写程序 5.7 中的最大公约数算法。函数的两个参数是我们想要计算最大公约数的两个数（见程序 13.5）。

## 程序 13.5

```
#import <Foundation/Foundation.h>

// 此函数找到两个
// 整数值的最大公约数并返回结果

int gcd(int u, int v) {
    int temp;

    while (v != 0) {
        temp = u % v;
        u = v;
        v = temp;
    }

    return u;
}

int main(void) {
    @autoreleasepool {
        int result = gcd(150, 35);
        NSLog(@"The gcd of 150 and 35 is %i", result);

        result = gcd(1026, 405);
        NSLog(@"The gcd of 1026 and 405 is %i", result);

        NSLog(@"The gcd of 83 and 240 is %i", gcd(83, 240));
    }
    return 0;
}
```

## 程序 13.5 输出

```
The gcd of 150 and 35 is 5
The gcd of 1026 and 405 is 27
The gcd of 83 and 240 is 1
```

函数 `gcd` 被定义为接收整数参数。函数通过其形式参数名 `u` 和 `v` 引用这些参数。在将变量 `temp` 定义为 `int` 类型后，程序计算并返回这两个整数的最大公约数。

该语句

```
result = gcd(150, 35);
```

表示调用函数 `gcd`，并传入参数 `150` 和 `35`，并将该函数返回的值存储在变量 `result` 中。



如果省略函数的返回类型声明，编译器将假设该函数返回一个整数——如果它确实返回了值的话。许多程序员利用这一点，省略了返回整数函数的返回类型声明。然而，这是一种糟糕的编程习惯，你应该尽量避免。编译器会警告你返回类型默认为 `int`，这表明你正在做错误的事情！

函数的默认返回类型与方法不同。回想一下，如果没有为方法指定返回类型，编译器将假设它返回一个 `int` 类型的值。同样，你应该始终为方法声明返回类型，而不是依赖这一事实。

## 声明返回类型和参数类型

我们之前提到过，Objective-C 编译器默认返回 `int` 类型的值。更具体地说，每当调用一个函数时，除非发生以下情况之一，否则编译器都会假设该函数返回一个 `int` 类型的值：

- 在遇到函数调用之前，程序中已经定义了该函数。
- 在遇到函数调用之前，已经声明了函数返回的值。声明函数的返回类型和参数类型被称为**原型声明**（prototype declaration）。

函数声明不仅用于声明函数的返回类型，还用于告诉编译器函数接受多少个参数以及这些参数的类型是什么。这类似于在定义新类时在 `@interface` 部分中声明方法。

若要将 `absolute` 声明为一个返回 `float` 类型值并接受单个同样为 `float` 类型参数的函数，可以使用以下原型声明：

```
float absoluteValue(float);
```

如你所见，你必须在括号内指定参数类型，而不是它的名称。如果你愿意，还可以在类型后可选指定一个“虚拟”名称：

```
float absoluteValue(float x);
```

# 第 13 章 底层 C 语言特性

这个名称不需要与函数定义中使用的名称相同——编译器反正会忽略它。

编写原型声明的一种万无一失的方法直接是从函数的实际定义中复制第一行。记得在末尾加上分号。

如果函数接受变数量的参数（例如 `NSLog` 和 `scanf` 的情况），必须通知编译器。声明

```
void NSLog(NSString *format, ...);
```

告诉编译器 `NSLog` 接受它的第一个参数，后面跟着任意数量的额外参数（使用 `...`）。`NSLog` 声明在特殊的文件 `Foundation/Foundation.h` 中，这也是你一直放在程序开头放置下面这一行的原因之一：

```
#import <Foundation/Foundation.h>
```

如果没有这一行，编译器会假设 `NSLog` 接受固定数量的参数，这可能会导致生成错误的代码。

如果你在调用之前已经放置了函数的定义或声明了函数及其参数，编译器在调用函数时会自动将你的数值参数转换为相应的类型。

考虑关于函数的一些提示和建议：

- 默认情况下，编译器假设函数返回 `int`。
- 在定义返回 `int` 的函数时，请按此定义。
- 在定义不返回值的函数时，请将其定义为 `void`。
- 如果你之前定义或声明了函数，编译器会将你的参数转换以匹配函数预期的参数。

为了安全起见，请声明程序中的所有函数，即使它们在被调用之前已经定义。（你以后可能决定将它们移动到文件的其他位置，甚至移动到另一个文件中。）一个好的策略是将函数声明放在头文件中，并只需将该文件导入到你的模块中。

函数默认是外部的。也就是说，函数的默认作用范围是它可以被链接的任何文件中所包含的任何函数或方法调用。你可以通过将其设为 `static` 来限制函数的作用范围。你通过在函数声明前放置 `static` 关键字来实现，如下：

```
static int gcd (int u, int v)
{
```

> 从技术上讲，它定义在 `NSObjectRuntime.h` 中，该文件是从 `Foundation.h` 内部导入的。

## 静态函数

静态函数只能由包含该函数定义的文件的其他函数或方法调用。

## 函数、方法和数组

要向函数或方法传递单个数组元素，请按通常方式将该数组元素作为参数指定。因此，如果你有一个计算平方根的 `squareRoot` 函数，并想获取 `averages[i]` 的平方根并将结果赋值给变量 `sq_root_result`，那么这样的语句就可以工作：

```
sq_root_result = squareRoot(averages[i]);
```

将数组传递给函数或方法是完全另一回事。要传递数组，你必须在函数或方法调用的内部列出数组的索引，而不带任何下标。例如，如果你假设 `grade_scores` 已经声明为一个包含 100 个元素的数组，表达式

```
minimum(grade_scores)
```

将数组 `grade_scores` 中包含的全部 100 个元素传递给名为 `minimum` 的函数。自然地，`minimum` 函数必须预期接收一个数组作为参数，并进行相应的形式参数声明。该函数在以下中查找最小值：

```
// 在数组中寻找最小值的函数

int minimum (int values[], int numElements)
{
    int minValue, i;

    minValue = values[0];

    for (i = 1; i < numElements; i++) {
        if (values[i] < minValue)
            minValue = values[i];
    }

    return (minValue);
}
```

Block 以插入符号 `^` 标识。其后紧跟该 Block 所接受的括号参数列表。在我们的案例中，该 Block 不接受任何参数，因此我们像在函数定义一样使用了 `void`。

你可以将此 Block 赋值给名为 `printMessage` 的变量，只要该变量已经过正确声明（这里的语法变得复杂了）：

```
void (^printMessage)(void) =
^(void) {
    NSLog("Programming is fun.");
}
```

在等号左侧，我们指定 `printMessage` 是一个指向不接受参数且不返回返回值的 Block 的指针。注意，赋值语句以分号结束。

执行通过变量引用的 Block 的与调用函数相同：

`printMessage();`

程序 13.6 将这些内容整合成了一个示例。

### 程序 13.6

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        void (^print_message)(void) =
        ^(void) {
            NSLog("Programming is fun.");
        }
        print_message();
    }
    return 0;
}
```

### 程序 13.6 输出

Programming is fun.

程序 13.7 是程序 13.4 的重写，使用 Block 代替函数。Block 可以在全局定义也可以在局部定义。在这种情况下，我们在 `main` 外部定义 Block，使其在作用范围内是外部且全局的。

# 第 13 章 底层 C 特性

### 程序 13.7

```
#import <Foundation/Foundation.h>

// 计算第 n 个三角形数的 block

void (*calculateTriangularNumber)(int) =
^(int n) {
    int i, triangularNumber = 0;

    for ( i = 1; i <= n; ++i )
        triangularNumber += i;
    
    NSLog(@"Triangular number %i is %i", n, triangularNumber);
}

int main (int argc, char * argv[]) {
    @autoreleasepool {
        calculateTriangularNumber(10);
        calculateTriangularNumber(20);
        calculateTriangularNumber(50);
    }
    return 0;
}
```

### 程序 13.7 输出

Triangular number 10 is 55

Triangular number 20 is 210

Triangular number 50 is 1275

比较程序 13.4 中的函数语法与程序 13.7 中定义的 Block。Block 变量 `calculateTriangularNumber` 定义为接受一个 `int` 参数且不返回返回值。

正如本节开头提到的，Block 可以返回一个值。这里是程序 13.5 重写为 Block 形式的 gcd（最大公约数）：

```
int (*gcd)(int, int) =
^(int u, int v) {
    int temp;

    while ( v != 0 ) {
        temp = u % v;
        u = v;
        v = temp;
    }

    return u;
};
```

Block 可以访问其定义作用域内的变量。该变量的值是 Block 定义时的值。这在程序 13.8 中得到了阐明。

### 程序 13.8

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int foo = 10;

        void (*printFoo) (void) =
            ^(void) {
                NSLog(@"foo = %i", foo);
            };

        foo = 15;

        printFoo();
        return 0;
    }
}
```

### 程序 13.8 输出

foo = 10

Print Block 可以访问局部变量 `foo` 的值。注意显示的值是 10 而不是 15。这是因为它是 Block 定义时的值，而不是执行时的值。

你不能默认修改定义在 Block 外部的变量值。因此，如果你尝试在 Block 内部更改 `foo` 的值（见程序 13.9），你将收到编译器的错误信息：Assignment of read-only variable 'foo'。

### 程序 13.9

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int foo = 10;

        void (*printFoo)(void) =
          ^(void) {
            NSLog(@"foo = %i", foo);
            foo = 20; // ** 这一行会导致编译错误
          }

        foo = 15;

        printFoo();
        NSLog(@"foo = %i", foo);
        return 0;
    }
}
```

如果你在程序 13.9 中局部变量 `foo` 的定义之前插入 Block 修饰符，使其读起来像：

- `__block int foo = 10;`

并运行程序，你将得到两行输出：

```
foo = 15
foo = 20
```

第一行显示 `foo` 的值现在是调用 Block 此时的值。第二行证实了 Block 能够将 `foo` 的值更改为 20。

Objective-C 语言提供了另一种对元素进行工具：结构体（structures）。你可以定义一个名为 `date` 的结构体，它由三个组件组成：月、日、年。

```c
struct date {
  int month;
  int day;
  int year;
};
```

与 `int`、`float` 或 `char` 类型的变量不同，处理结构体时需要特殊的语法。结构体的成员通过指定变量名、后跟一个点和成员名来访问。例如，将 `today` 的日设置为 21，你可以写：

```
today.day = 21;
```

注意变量名、点和成员名之间不允许有空格。现在等一下！这不不是用于访问对象属性的运算符吗？回想我们写

```
myRect.width = 12;
```

是为了调用 Rectangle 对象的 setter 方法，传递参数值 12。这里没有混淆：编译器会确定点左侧是结构体还是对象，并妥善处理这种情况。

回到 `struct date` 示例，将 `today` 的年设置为 2011，你可以使用：

```
today.year = 2011;
```

最后，测试月的值以检查它是否等于 12，可以使用如下语句：

```
if ( today.month == 12 )
next_month = 1;
```

程序 13.10 将之前的讨论整合到一个实际程序中。

### 程序 13.10

```
#import <Foundation/Foundation.h>

int main(int argc, char * argv[])
{
  @autoreleasepool {

  struct date
{
    int month;
    int day;
    int year;
  }

  struct date today;

  today.month = 9;
  today.day = 25;
  today.year = 2011;

  NSLog(@"Today's date is %i/%i/%2i.\*", today.month,
        today.day, today.year % 100);
  }

  return 0;
}
```

因此，为今天存储结构变量的三个整数成员预留内存。

赋值后，通过一个适当的 `NSLog` 调用可以显示结构中包含的值。`today.year` 除以 100 的余数在传递给 `NSLog` 函数之前会进行计算，这样年份部分就只显示为 `1`。`NSLog` 中的 `%.2i` 格式字符指定了至少显示两个字符，从而强制显示 `today` 的前导零。

在表达式求值时，结构体成员遵循与 Objective-C 语言中普通变量相同的规则。整数结构成员除以另一个整数的操作将作为整数除法执行，如下：

```
century = today.year / 100 + 1;
```

假设你想写一个简单的程序，接受今天的日期作为输入并向用户显示明天的日期。乍一看，这似乎是一个非常简单的任务。你可以要求用户输入今天的日期，然后通过一系列语句计算明天的日期，如下：

```
tomorrow.month = today.month;
tomorrow.day = today.day + 1;
tomorrow.year = today.year;
```

当然，上述语句对于大多数日期都可以正常工作，但有两种情况无法被正确处理：

- 如果今天的日期是月份的最后一天
- 如果今天的日期是年底（即，如果今天的日期是 12 月 31 日）

轻松判断今天的日期是否为月末的一种方法是设置一个整数数组，对应每个月份的天数。在数组内对特定月份进行查找即可得到该月份的天数。

## 初始化结构体

初始化结构体与初始化数组类似——元素被简单地列在一对括号内，并用逗号分隔元素。

要将日期变量 `today` 初始化为 2011 年 7 月 2 日，可以使用以下语句：

```
struct date today = { 7, 2, 2011 };
```

与初始化数组一样，列出的值可以比结构体包含的值少。

```
struct date today = { 7 };
```

这会将 `today.month` 设置为 `7`，但不会给 `today.day` 或 `today.year` 任何初始值。在这种情况下，它们的默认初始值是未定义的。

可以使用以下符号以任何顺序指定特定成员进行初始化：

`.member = value`

在初始化列表中，例如：

```
struct date today = { .month = 7, .day = 2, .year = 2011 } ;
```

以及

```
struct date today = { .year = 2011 } ;
```

最后一条语句将结构中的年份设置为 `2011`。正如你所知，另外两个成员是未定义的。

## 嵌套中的结构体

Objective-C 在定义结构体方面提供了极大的灵活性。例如，你可以定义一个本身包含其他结构体作为其一个或多个成员的结构体，也可以定义包含数组的结构体。

你在第 10 章“变量和数据类型的更多内容”中学习了 `typedef` 语句。在你的 iOS 程序中，你将经常需要处理矩形。例如，矩形定义了 iPhone 或 iPad 屏幕上窗口的大小和位置。它们还定义了子窗口（称为子视图）的位置和大小。使用了 `typedef` 定义的三种基本数据类型：

1. `CGPoint`，描述一个 (x,y) 点
2. `CGSize`，描述宽度和高度
3. `CGRect`，是一个包含原点 (`CGPoint`) 和大小 (`CGSize`) 的矩形

以下是 Apple `CGGeometry.h` 头文件中的 `typedef` 定义：

/* Points. */

```
struct CGPoint {
  CGFloat x;
  CGFloat y;
}
typedef struct CGPoint CGPoint;
```

/* Sizes. */

```
struct CGSize {
  CGFloat width;
  CGFloat height;
}
typedef struct CGSize CGSize;
```

/* Rectangles. */



# 第 13 章 C 语言底层特性

话得差不多，是时候看看指针到底是如何工作的。假设你按如下定义了一个名为 `count` 的变量：

```
int count = 10;
```

你可以定义另一个名为 `intPtr` 的变量，通过以下声明可以间接访问 `count` 的值：

```
int *intPtr;
```

星号告诉 Objective-C 系统，变量 `intPtr` 的类型是指向 int 的指针。这意味着程序将使用 `intPtr` 来间接访问一个或多个整数变量的值。

你已经见过我们在之前的程序 `scanf` 调用中是如何使用 `&` 运算符的。这个单目运算符称为地址运算符，它在 Objective-C 中创建一个指向变量的指针。如果 `x` 是特定类型的变量，表达式 `&x` 就是指向该变量的指针。如果你愿意，可以将表达式 `&x` 赋值给任何声明为与 `x` 类型相同指针的指针变量。

因此，根据给出的 `count` 和 `intPtr` 的定义，你可以写如下语句：

```
intPtr = &count;
```

以建立 `intPtr` 和 `count` 之间的间接引用。地址运算符赋值给变量 `intPtr` 的不是 `count` 的值，而是指向该值的指针。图 13.1 展示了 `intPtr` 和 `count` 之间的连接。有向线说明 `intPtr` 并不直接包含 `count` 的值，而是包含一个指向变量 `count` 的指针。

![](img/22d1310b7c22ea2d48cd2058929a5cda_290_0.png)

图 13.1 指向整数的指针

通过指针变量 `intPtr` 引用 `count` 的内容，你需要使用间接运算符，即星号 (`*`)。如果 `x` 被定义为 `int` 类型，语句

```
x = *intPtr;
```

将通过 `intPtr` 间接引用的值赋值给变量 `x`。由于 `intPtr` 之前被设置为指向 `count`，这条语句的效果是将变量 `count` 中包含的值（即 10）赋值给变量 `x`。

程序 13.11 结合了上述语句，并演示了两个基础的指针运算符：地址运算符 (`&`) 和间接运算符 (`*`)。

## 程序 13.11

```
// 说明指针的程序

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        int count = 10, x;
        int *intPtr;

        intPtr = &count;
        x = *intPtr;
    }
    return 0;
}
```

## 程序 13.11 输出

count = 10, x = 10

变量 `count` 和 `x` 以正常方式声明为整数变量。在下一行，变量 `intPtr` 被声明为类型“指向 int 的指针”。注意，这两行声明可以合并为一行：

```
int count = 10, x, *intPtr;
```

接下来，将地址运算符应用于变量 `count`，其效果创建一个指向该变量的指针，程序将该指针赋值给变量 `intPtr`。

执行语句

```
x = *intPtr;
```

过程如下：间接运算符告诉 Objective-C 系统将变量 `intPtr` 视为包含指向另一个数据项的指针。该指针用于访问所需的数据项，该数据项由指针变量指定。由于你在声明变量时要求编译器让 `intPtr` 指向整数，编译器知道表达式 `*intPtr` 引用的值是一个整数。此外，由于你在上一条语句中将 `intPtr` 设置为整数变量 `count`，该表达式间接访问了 `count` 的值。

程序 13.12 展示了指针变量的一些有趣属性。该程序使用了指向字符的指针。

## 程序 13.12

```
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        char c = 'Q';
        char *charPtr = &c;

        NSLog("%@%%c %%c", c, *charPtr);

        c = '/';
        NSLog("%@%%c %%c", c, *charPtr);

        *charPtr = '(';
        NSLog("%@%%c %%c", c, *charPtr);
    }

    return 0;
}
```

## 程序 13.12 输出

```
Q Q
//
(
```

变量 `c` 被定义并初始化为字符 'Q'。在程序的下一行，变量 `charPtr` 被声明为类型“指向字符的指针”，这意味着存储在该变量中的任何值都应被视为对字符的间接引用（指针）。注意，你可以以正常方式为该变量赋初值。你在程序中赋给 `charPtr` 的值是变量 `c` 的指针，该值通过对变量 `c` 应用地址运算符获得。（注意，这种初始化将产生编译器错误，因为在表达式中引用其值之前，必须先声明 c。）

变量 `charPtr` 的声明及其初始值的赋值可以用两个独立的语句等效表示，如下：

```
char *charPtr;
charPtr = &c;
```

（而不是通过以下语句：

```
char *charPtr;
*charPtr = &c;
```

## 指向结构体的指针

变量 `charPtr` 的声明及其初始值的赋值可以用两个独立的语句等效表示，如下：

```
char *charPtr;
charPtr = &c;
```



# 第 13 章 C 语言底层特性

变量 `count` 和 `x` 以正常方式声明为整数变量。在下一行，变量 `intPtr` 被声明为类型“指向 int 的指针”。注意，这两行声明可以合并为一行：

```c
int count = 10, x, *intPtr;
```

接下来，将地址运算符应用于变量 `count`，其效果创建一个指向该变量的指针，程序将该指针赋值给变量 `intPtr`。

执行语句：

```c
x = *intPtr;
```

过程如下：间接运算符告诉 Objective-C 系统将变量 `intPtr` 视为包含指向另一个数据项的指针。该指针用于访问所需的数据项，该数据项由指针变量指定。由于你在声明变量时要求编译器让 `intPtr` 指向整数，编译器知道表达式 `*intPtr` 引用的值是一个整数。此外，由于你在上一条语句中将 `intPtr` 设置为整数变量 `count`，该表达式间接访问了 `count` 的值。

程序 13.12 展示了指针变量的一些有趣属性。该程序使用了指向字符的指针。

## 程序 13.12

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        char c = 'Q';
        char *charPtr = &c;

        NSLog("%@%%c %%c", c, *charPtr);

        c = '/';
        NSLog("%@%%c %%c", c, *charPtr);

        *charPtr = '(';
        NSLog("%@%%c %%c", c, *charPtr);
    }

    return 0;
}
```

## 程序 13.12 输出

```
Q Q
/
(
```

变量 `c` 被定义并初始化为字符 'Q'。在程序的下一行，变量 `charPtr` 被声明为类型“指向字符的指针”，这意味着存储在该变量中的任何值都应被视为对字符的间接引用（指针）。注意，你可以以正常方式为该变量赋初值。你在程序中赋给 `charPtr` 的值是变量 `c` 的指针，该值通过对变量 `c` 应用地址运算符获得。（注意，这种初始化将产生编译器错误，因为在表达式中引用其值之前，必须先声明 c。）

变量 `charPtr` 的声明及其初始值的赋值可以用两个独立的语句等效表示，如下：

```c
char *charPtr;
charPtr = &c;
```

（而不是通过以下语句：

```c
char *charPtr;
*charPtr = &c;
```）

## 指向结构体的指针

```c
datePtr->day = 25;
datePtr->year = 2011;

NSLog ("Today's date is %i/%i/%i.", datePtr->month, datePtr->day, datePtr->year % 100);
}
return 0;
}
```

## 程序 13.13 输出

今天的日期是 9/25/11。

## 指针、方法与函数

你可以像平常一样将指针作为参数传递给方法或函数，也可以让函数返回一个指针作为结果。如果你仔细想，你会发现这正是 `alloc` 和 `init` 方法一直以来都在做的事情——返回指针。我们将在本章的末尾详细介绍这一点。

现在考虑程序 13.14。

## 程序 13.14

```objc
// 作为函数参数的指针
#import <Foundation/Foundation.h>

void exchange (int *pint1, int *pint2)
{
    int temp;

    temp = *pint1;
    *pint1 = *pint2;
    *pint2 = temp;
}

int main (int argc, char * argv[])
{
    @autoreleasepool {
        void exchange (int *pint1, int *pint2);
        int i1 = -5, i2 = 66, *p1 = &i1, *p2 = &i2;

        NSLog("i1 = %i, i2 = %i", i1, i2);
        exchange(p1, p2);
        NSLog("i1 = %i, i2 = %i", i1, i2);

        exchange(&i1, &i2);
        NSLog("i1 = %i, i2 = %i", i1, i2);
    }
    return 0;
}
```

## 程序 13.14 输出

```
i1 = -5, i2 = 66
i1 = 66, i2 = -5
i1 = -5, i2 = 66
```

`exchange` 函数的作用是交换其两个参数指向的两个整数值。局部变量 `temp` 用于在交换时保存其中一个整数值。它的值被设置为 `pint1` 所指向的整数。将 `pint2` 指向的整数复制到 `pint1` 所指向的整数中，然后将 `temp` 的值存储在 `pint2` 所指向的整数中，从而完成交换。

`main` 程序定义了变量 `i1` 和 `i2`，值分别为 -5 和 66。接着定义了两个指针 `p1` 和 `p2`，并将它们分别指向 `i1` 和 `i2`。程序随后显示 `i1` 和 `i2` 的值，并调用 `exchange` 函数，将两个指针（`p1` 和 `p2`）作为参数传递。`exchange` 函数交换 `p1` 指向的整数的值与 `p2` 指向的整数的值。由于 `p1` 指向 `i1`，该函数交换了 `i1` 和 `i2` 的值。第二次 `NSLog` 输出的输出验证了交换正常工作。

第二次调用 `exchange` 稍微有点意思。这一次，函数的参数是通过对 `i1` 和 `i2` 这两个变量应用地址操作符在栈上生成的指向 `i1` 和 `i2` 的指针。由于表达式 `&i1` 产生一个指向变量 `i1` 的指针，这符合函数对第一个参数的类型预期（指向整数的指针）。第二个参数也是如此。正如你从程序的输出所示，`exchange` 函数完成了它的工作，并将 `i1` 和 `i2` 的值恢复到了它们的原始值。

详细学习程序 13.14。它通过一个短小的示例说明了在 Objective-C 中处理指针的关键概念。

## 指针与数组

如果你有一个名为 `values` 的 100 个整数数组，你可以定义一个名为 `valuesPtr` 的指针，可以使用以下语句访问该数组包含的整数：

```objc
int *valuesPtr;
```

当你定义一个用于指向数组元素的指针时，你不需要将指针类型指定为“指向数组的指针”，而是将指针指定为指向数组中所包含的元素类型。

如果你有一个名为 `fracts` 的 `Fraction` 对象数组，你可以以类似的方式定义一个用于 `fracts` 中元素的指针：

```objc
Fraction **fractsPtr;
```

要将 `valuesPtr` 设置为 `values` 数组的第一个元素，你只需要写：

```objc
valuesPtr = values;
```

在这种情况下不使用地址操作符，因为 Objective-C 编译器将不带下标的数组名出现视为数组第一个元素的指针。因此，简单地指定不带下标的 `values` 就会产生一个指向 `values` 第一个元素的指针。

产生指向 `values` 起点指针的等效方法是对数组的第一个元素应用地址操作符。因此，语句

```objc
valuesPtr = &values[0];
```

具有相同的目的，即将一个指向 `values` 第一个元素的指针放在指针变量 `valuesPtr` 中。

要显示 `fractsPtr` 指向的 `fracts` 数组中的 `Fraction` 对象，你需要写下语句：

```objc
[*fractsPtr print];
```

当你想要访问数组元素时，使用指针的真正威力就发挥出来了。增和递减运算符（`++` `--`）在处理指针时非常有用。对指针应用增运算符的效果与指针加 1 相同，而减运算符的效果与指针减 1 相同。对于定义为 `char` 的 `textPtr`，语句

```objc
++textPtr;
```

会让 `textPtr` 指向文本的下一个字符。类似的，语句

```objc
--textPtr;
```

会让 `textPtr` 指向文本的前一个字符（假设在此语句之前它指向文本的开头）。

在 Objective-C 中比较两个指针是完全有效的。这在比较同一个数组中的指针时特别有用。例如，你可以通过与最后一个元素比较来测试 `valuesPtr` 是否指向数组的结尾。因此，表达式 `valuesPtr > &values[99]` 如果 `valuesPtr` 指向数组的最后一个元素则为真（非零），否则为假（零）。根据我们之前的讨论，你可以将之前的表达式替换为等效的：

```c
valuesPtr > values + 99
```

这是因为不带下标的 `values` 是指向数组开头的指针。（记住这等同于编写 `&values[0]`。）

程序 13.15 阐述了数组指针。`arraySum` 函数计算整数数组中包含元素的和。

## 程序 13.15

```objc
// 计算整数数组元素的函数

#import <Foundation/Foundation.h>

int arraySum(int array[], int n)
{
    int sum = 0, *ptr;
    int arrayEnd = array + n;

    for ( ptr = array; ptr < arrayEnd; ++ptr )
        sum += *ptr;

    return (sum);
}

int main (int argc, char * argv[])
{
    @autoreleasepool {
        int arraySum(int array[], int n);
        int values[10] = { 3, 7, -9, 3, 6, -1, 7, 9, 1, -5 };

        NSLog("The sum is %i", arraySum(values, 10));
    }
    return 0;
}
```

在 `arraySum` 函数内部，整数指针 `arrayEnd` 在 `array` 的最后一个元素之后被定义并设置。设置了一个 `for` 循环来遍历 `array` 的元素；进入循环时，`ptr` 的值被设置为指向 `array` 的开头。每次循环，`ptr` 所指向的 `array` 元素都会加到 `sum` 中。`for` 循环增加 `ptr` 的值，使其指向 `array` 中的下一个元素。当 `ptr` 超过 `array` 的结尾时，退出 `for` 循环并将 `sum` 的值返回给调用者。

## 是数组还是指针？

要将数组传递给函数，你只需指定数组名称，就像你之前调用 `arraySum` 函数时做的那样。但我们在本节也提到，为了产生指向数组的指针，你只需要指定数组名称。这意味着在调用 `arraySum` 函数时，传递给函数的是指向数组值的指针。事实确实如此，这也是为什么你可以在函数内部更改数组的元素。

但是如果传递给函数的是指针，函数内部的形式参数难道不是声明为指针吗？换句话说，在 `arraySum` 函数的声明中，为什么没有使用这种声明？

```c
int *array;
```

函数内部对数组的所有引用难道不应该使用指针变量来实现吗？

为了回答这些问题，我们必须首先重申关于指针和数组的说法。我们提到过，如果 `valuesPtr` 的元素类型与数组 `values` 的元素类型相同，那么表达式 `"valuesPtr + i"` 等同于表达式 `values[i]`，前提是 `valuesPtr` 已设置为指向 `values` 的开头。由此得出的是，你可以使用表达式 `*(values + i)` 来引用数组 `values` 的第 `i` 个元素——通常情况下，如果 `x` 是任何类型的数组，表达式 `x[i]` 在 Objective-C 中可以表示为 `*(x + i)`。

正如你所见的，指针和数组在 Objective-C 中是紧密相关的，这就是为什么你可以在 `arraySum` 函数内部将 `array` 声明为“int 数组”类型或“int 指针”类型。这两种声明在之前的程序中都是有效的——试一下吧。

如果你将使用索引号来引用数组元素，请将相应的形式参数声明为数组。这正确地反映了函数对数组的使用。同样，如果你将参数作为指向数组的指针，请将其声明为指针类型。

## 字符字符串指针

使用数组指针的一个常见应用是指向字符字符串的指针。其原因在于符号上的便利性和效率。为了展示你如何方便地使用字符字符串指针，让我们写一个名为 `copyString` 的函数，将一个字符串拷贝到另一个字符串。如果你使用普通的数组索引方法编写此函数，可能会这样编写该函数：

```c
void copyString(char to[], char from[])
{
    int i;
    for ( i = 0; from[i] != '\0'; ++i )
        to[i] = from[i];

    to[i] = '\0';
}
```

循环在空字符复制到 `to` 数组之前退出，因此解释了函数中最后一条语句的必要性。如果你使用指针编写 `copyString`，就不再需要索引变量 `i`。程序 13.16 显示了指针版本。

## 程序 13.16

```c
#import <Foundation/Foundation.h>

void copyString(char *to, char *from)
{
    for ( ; *from != '\0'; ++to, ++from )
        *to = *from;

    *to = '\0';
}

int main (int argc, char *argv[])
{
    @autoreleasepool {
        char string1[] = "A string to be copied.";
        char string2[50];

        copyString(string2, string1);
        NSLog("%@", string2);

        copyString(string2, "So is this.");
        NSLog("%@", string2);
    }
    return 0;
}
```

## 程序 13.16 输出

```
A string to be copied.
So is this.
```

`copyString` 函数将两个形式参数 `to` 和 `from` 定义为字符指针，而不是字符数组，正如之前的 `copyString` 版本中所做的那样。这反映了函数将如何使用这两个变量。

进入一个循环（无初始条件），将 `from` 指向的字符串拷贝到指针中。每次循环，`from` 和 `to` 指针都会增加 1。这使得 `from` 指针指向从源字符串拷贝的下一个字符，并将 `to` 指针指向目标字符串中存储下一个字符的位置。

当 `from` 指针指向空字符时，退出 `for` 循环。函数随后清除目标字符串末尾的空字符。

在 `main` 例程中，调用了两次 `copyString` 函数——第一次将 `string1` 的内容拷贝到 `string2`，第二次将常量字符串 "So is this." 的内容拷贝到 `string2`。

## 字符字符串与指针

调用

```c
copyString(string2, "So is this.");
```

在程序中有效，意味着当使用常量字符字符串时，它被视为指向其第一个字符的指针。这是 C 和 Objective-C 中的共同特性。字符串字面量存储在内存的只读区域，尝试直接修改它们会导致崩溃。然而，由于 `copyString` 将字符拷贝到可变数组 `string2` 中，这是完全安全的。

## 重新回顾递增递减运算符

到目前为止，每当你使用增运算符时，它都是表达式中唯一的运算符。当你写下表达式 `++x` 时，你知道这会将变量 `x` 的值加 1。正如你所见的，如果 `x` 是数组的指针，这将使 `x` 指向数组的下一个元素。

你可以在包含其他运算符的表达式中使用增减运算符。在这种情况下，更精确地了解这些运算符的工作方式变得非常重要。

每当你使用增减运算符时，你总是将它们放在要增或要减的变量之前。为了增加变量 `i`，你只需写道：

```c
++i;
```

你也可以将增运算符放在变量之后，如下：

```c
i++;
```

这两个表达式都是有效的，并且都产生相同的结果——增加 `i` 的值。在第一种情况下，由于 `++` 位于操作数之前，递增操作被更精确地识别为前增。在第二种情况下，由于 `++` 位于操作数之后，该操作被识别为后增。

同样的讨论也适用于递减运算符。因此语句

```c
--i;
```

在技术上，它执行的是 `i` 的预递减，而语句

```c
i--;
```

执行的是 `i` 的后递减。两者的最终结果相同，都是将 `i` 的值减 1。

当加法和减运算符被用于更复杂的表达式时，这些运算符的“前”和“后”性质的区别就会体现出来。



# 预递增/后递增与预递减/后递减运算符

假设你有两个整数 `i` 和 `j`。如果你将 `i` 的值设置为 0 并编写语句

```
j = ++i;
```

赋值给 `j` 的值将是 1——而不是你可能预期的 0。在预递增运算符的情况下，值在被表达式中使用之前会先增加。因此，在上述表达式中，`i` 的值首先从 0 增加到 1，然后将该值赋值给 `j`，就就像是改写了以下两个语句：

```
++i;
j = i;
```

如果你在语句中使用后递增运算符

```
j = i++;
```

`i` 在其值被赋值给 `j` 之后才会增加。所以，如果在执行上一个语句之前 `i` 为 0，那么 0 会赋值给 `j`，然后 `i` 会增加 1，就好像是使用了这些语句一样：

```
j = i;
++i;
```

另一个例子是，如果 `i` 等于 1，语句

```
x = a[--i];
```

具有将 `a[0]` 的值赋值给 `x` 的效果，因为变量 `i` 在其值被用于索引 `a` 之前已经递减了。语句

```
x = a[i--];
```

将 `a[1]` 的值赋值给 `x`，是因为 `i` 在其值被用于索引 `a` 之后才递减。

作为预/后递增递减运算符区别的第三个例子，函数调用

```
NSLog("@%i", ++i);
```

会先增加 `i`，然后将其值发送给 `NSLog` 函数；而调用

```
NSLog("@%i", i++);
```

则在值发送给函数之后才增加 `i`。所以，如果 `i` 等于 100，第一个 `NSLog` 调用将在终端上显示 101，而第二个 `NSLog` 调用将显示 100。无论哪种情况，在语句执行后，`i` 的值都将等于 101。

在我们介绍程序之前关于该主题的最后一个例子，如果 `textPtr` 是一个字符指针，表达式

```
*++textPtr
```

首先增加 `textPtr`，然后获取它所指向的字符；而表达式

```
*textPtr++
```

在其值增加之前先获取 `textPtr` 所指向的字符。在任何一种情况下，括号都不是必需的，因为 `*` 和 `++` 运算符的优先级相同，但它们是从右到左结合的。

# 优化 copyString 函数

让我们回到程序 13.16 中的 `copyString` 函数并将其重写为赋值。由于 `to` 和 `from` 指针在 `for` 循环内部的赋值语句执行后每次都会增加，因此它们将作为后递增操作合并到赋值语句中。程序 13.16 修改后的 `for` 循环变为：

```
for ( ; *from != '\0'; )
    *to++ = *from++;
```

循环内部赋值语句的执行过程如下：先获取 `from` 指向的字符，然后 `from` 增加到源字符串中的下一个字符。所引用的字符被存储在 `to` 指向的位置；然后 `to` 增加到目标字符串中的下一个位置。

之前的语句有点啰嗦，因为它没有初始表达式也没有循环表达式。事实上，用 `while` 循环的形式表达逻辑会更好。这在程序 13.17 中实现，该程序展示了 `copyString` 函数的新版本。`while` 循环利用了 Objective-C 程序员所熟悉的事实：空字符等于值 0。

## 程序 13.17

```c
// 将一个字符串拷贝到另一个的函数
// 指针版本 2

#import <Foundation/Foundation.h>

void copyString(char *to, char *from) {
    while (*from != '\0') {
        *to++ = *from++;
    }
    *to = '\0';
}

int main(int argc, char *argv[]) {
    @autoreleasepool {
        void copyString(char *to, char *from);

        char string1[] = "A string to be copied.";
        char string2[50];

        copyString(string2, string1);
        NSLog("%s", string2);

        copyString(string2, "So is this.");
        NSLog("%s", string2);
    }
    return 0;
}
```

**程序 13.17 输出：**

```
A string to be copied.
So is this.
```

# 指针操作

正如你在本章中所看到的，你可以对指针进行加或减整数操作。此外，你可以比较两个指针以查看它们是否相等，或者一个指针是否小于或大于另一个。允许指针的唯一其他操作是两个相同类型的指针相减。在 Objective-C 中，两个指针相减的结果是两个指针之间包含的元素数量。如果 `p1` 指向任意类型的数组，而 `p2` 指向同一数组中后续的元素，表达式 `p2 - p1` 代表这两个指针之间的元素数量。

# 指针与内存地址

在结束对指针的讨论之前，我们应该指出它们具体实现的细节。计算机内存可以被概念化为存储单元的顺序集合。计算机内存的每个单元都有一个与其相关的数字，即地址。通常，计算机内存的地址编号从 0 开始。在大多数计算机系统中，一个单元是一个字节。

计算机使用内存来存储计算机程序的信息，并存储与之相关的变量的值。所以如果你声明一个类型为 `int` 的变量 `count`，系统会在程序执行期间分配内存位置来存放 `count` 的值。例如，该位置可能是内存内部的地址 `0x00FF16`。

幸运的是，你不需要担心分配给变量的具体内存地址——系统会自动处理它们。然而，每个变量都关联一个唯一的内存地址这一知识将有助于理解指针的操作。

每当你在 Objective-C 中对变量应用地址运算符时，生成的值是该变量在内存内部的实际地址。（显然，这就是地址名称的由来。）语句

```
intPtr = &count;
```

将内存中分配给变量 `count` 的地址赋值给 `intPtr`。因此，如果 `count` 位于地址 `0x00FF16`，则该语句将该地址赋值给 `intPtr`。

对指针变量应用间接运算符，如表达式

```
*intPtr
```

其效果是将该内存地址包含的值获取出来，并根据指针变量声明的类型进行解释。所以 `intPtr` 的类型是指向 `int` 的指针，系统会将存储在 `intPtr` 提供的内存地址中的值解释为整数。

# 它们不是对象！

现在你已经学会了如何定义数组、结构体、字符字符串和联合体，以及如何在程序中操作它们。记住一个根本性的点：**它们不是对象**。因此，你不能向它们发送消息。你无法利用它们来充分利用诸如 Foundation 框架的内存分配策略等特性。这就是我鼓励你跳过这一章稍后再回来的原因之一。通常情况下，学习使用 Foundation 中将数组和字符串定义为对象的类，比使用语言内置的类型对你更有帮助。只有在你真的需要时才诉诸本章中定义的类型——但希望你不需要！

# 其他语言特性

某些语言特性无法很好地归类到其他任何章节，因此我们包含了它们。

## 复合字面量

复合字面量是一个括在括号内的类型名，后面跟着一个初始化列表。它创建了一个指定类型的匿名值，其作用域限于创建它的块；如果在任何块之外定义，则具有全局作用域。在后一种情况下，初始化器必须是常量表达式。

考虑一个例子：

```
(struct date) {.month = 7, .day = 2, .year = 2011}
```

这个表达式产生了一个具有指定初始值的 `struct date` 类型结构体。你可以将其赋值给另一个 `struct date` 结构体，如下：

```
theDate = (struct date) {.month = 7, .day = 2, .year = 2011 };
```

或者你可以将其传递给期望 `struct date` 类型参数的函数或方法，如下：

```
setName((struct date) {.month = 7, .day = 2, .year = 2011});
```

此外，你可以定义结构体以外的类型。例如，如果 `intPtr` 的类型为 `int *`：

```
intPtr = (int [100]) { [0] = 1, [50] = 50, [99] = 99 };
```

（这出现在程序的任何地方）将 `intPtr` 指向一个包含 100 个整数的数组，其中 3 个元素按指定方式初始化。如果未指定数组的大小，则由初始化列表决定。

# 第13章 底层语言特性

## goto 语句

执行 `goto` 语句会导致程序直接跳转到指定的位点。为了识别在程序的哪个位置进行跳转，需要一个标签。标签是一个与变量名规则相同的名称；它必须紧跟一个冒号。标签直接放在要跳转的语句之前，并且必须出现在与 `goto` 相同的函数或方法中。

例如，该语句

```
goto out_of_data;
```

会导致程序立即跳转到由 `out_of_data:` 标签标记的语句。该标签可以位于函数或方法的任何地方。

懒惰的程序员经常使用 `goto` 语句跳转到代码的其他部分。`goto` 语句中断了程序正常的顺序流。结果是程序变得更难以追踪。在程序中使用大量的 `goto` 可能导致无法理解。由于这个原因，`goto` 语句不被认为是良好编程风格的一部分。

## 空语句

Objective-C 允许在任何可以出现普通程序语句的地方放置孤立的分号。这种语句被称为空语句，其效果是什么都不做。这看起来可能没用，但程序员经常在 `while`、`for` 和 `do` 语句中使用它。例如，以下语句的目的是将标准输入（默认是你的终端）读取的所有字符存储在字符数组中，直到遇到换行符为止。该语句使用了库函数 `getchar`，它从标准输入读取并返回单个字符：

```
while ((c = getchar()) != '\n')
    ;
```

所有操作都在 `while` 语句的循环条件部分执行。之所以需要空语句，是因为编译器会将循环表达式后面的语句视为循环的体。如果没有空语句，编译器将把程序中随其后的任何语句视为程序循环的体。

## 逗号运算符

可以说，优先级图谱的底端是逗号运算符。在第 5 章“程序循环”中，我们指出在 `for` 语句内部，你可以通过逗号分隔在任何字段中包含多个表达式。例如，起始如下的 `for` 语句

```
for (i = 0, j = 100; i != 10; ++i, j -= 10)
```

在循环开始之前将 `i` 的值初始化为 0，`j` 的值初始化为 100，并在循环体执行后增加 `i` 的值并从 `j` 的值减去 10。因为 Objective-C 中的所有运算符都会产生一个值，因此逗号运算符的值是最右侧表达式的值。

## sizeof 运算符

尽管你可以对程序中的数据类型的大小做出假设，但有时你需要知道这些信息。这可能是在使用 `malloc` 等库函数进行动态内存分配时，或者向文件写入或存档时。Objective-C 提供了一个 `sizeof` 运算符，可以用它确定数据类型或对象的大小。`sizeof` 运算符返回指定项目按字节的大小。`sizeof` 运算符的参数可以是变量、数组、基础类型名称、派生类型名称或表达式。例如，编写

```
sizeof(int)
```

给出了存储整数所需的存储大小。如果 `x` 被声明为 100 个整数的数组，表达式

```
sizeof(x)
```

将给出存储 100 个 `x` 整数所需的存储大小。

> 如果 `myFract` 是一个包含两个 `int` 实例变量（分子和分母）的对象，表达式
>
> ```
> sizeof(myFract)
> ```
>
> 在任何将指针表示为 4 字节的系统上产生值 4。事实上，`sizeof` 对任何对象产生的值是因为你请求的是指针数据的大小。要获取存储 `Fraction` 对象实例的实际结构体的大小，你应该写如下：
>
> ```
> sizeof(*myFract)
> ```
>
> > 在你的 MacBook Air 上，这得到了值 12。这是分子和分母各占 4 字节，加上本章末尾“工作原理”部分提到的 `isa` 成员占的 4 字节。

# 杂项语言特性

可以使用命令行参数，以便在执行程序的同时指定你想要查找的单词含义，如下例所示：

```
lookup aerie
```

这消除了程序提示用户输入单词的需要，因为该单词已经在命令行中输入了。如果执行了上一个命令，系统将自动将 `argv[1]` 中指向字符串 `"aerie"` 的指针传递给 `main` 函数。请记住，`argv[0]` 将包含指向程序名称的指针，在这种情况下它将是 `"lookup"`。

主程序可能如下所示：

```c
#include <Foundation/Foundation.h>

struct entry {
    char *word;
    char *definition;
};

int lookup(struct entry dictionary[], char search[], int entries) {
    int i;
    for (i = 0; i < entries; ++i) {
        if (strcmp(search, dictionary[i].word) == 0)
            return i;
    }
    return -1;
}

int main(int argc, char *argv[]) {
    @autoreleasepool {
        struct entry dictionary[100] = {
            {"aardvark", "a burrowing African mammal"},
            {"abyss", "a bottomless pit"},
            {"acumen", "mentally sharp; keen"},
            {"addle", "to mentally confused"},
            {"aerie", "a high nest"},
            {"affix", "to append; attach"},
            {"agar", "a jelly made from seaweed"},
            {"ahoy", "a nautical call of greeting"},
            {"aigrette", "an ornamental cluster of feathers"},
            {"ajar", "partially opened"}
        };
        int entries = 10;
        int entryNumber;

        if (argc != 2) {
            NSLog(@"No word typed on the command line.");
            return 1;
        }

        entryNumber = lookup(dictionary, argv[1], entries);

        if (entryNumber != -1) {
            NSLog(@"%s", dictionary[entryNumber].definition);
        } else {
            NSLog(@"Sorry, %s is not in my dictionary.", argv[1]);
        }
    }
    return 0;
}
```



主程序测试以确保在程序执行后输入了单词。如果没有输入，或者输入了多个单词，`argc` 的值将不等于 2。程序将向标准错误输出错误信息并终止，返回退出状态 1。

如果 `argc` 为 2，则调用 `lookup` 函数在字典中查找 `argv[1]` 所向的单词。如果找到了该单词，则显示其定义。

记住，命令行参数是以字符串的形式存储的。因此，带有命令行参数 2 和 16 执行程序（如 `power 2 16` 所示），会在 `argv[1]` 中存储一个指向字符串 "2" 的指针，在 `argv[2]` 中存储一个指向字符串 "16" 的指针。如果程序需要解释参数（正如我们怀疑 `power` 程序所做的那样），程序必须对它们进行转换。程序库中有几种规则可以进行此类转换：`sscanf`、`atof`、`strtod` 和 `strtol`。在第二部分中，你将学习如何使用 `NSProcessInfo` 类以 `c strings` 类型的字符串对象形式访问命令行参数。

# 第 13 章 底层 C 语言特性

## 工作原理

如果我们不在先一起尝试几件事的情况下就完成本章，将是非常遗憾的。因为 Objective-C 语言的底层是 C 语言，所以值得提及两者之间的一些联系。你可以忽略这些实现细节，也可以理解其工作原理，就像学习指针地址有助于你理解指针一样。我们在这里不会写得太详细；只需陈述关于 Objective-C 和 C 之间关系的四个事实。

## 事实 #1：实例变量存储在结构中

当你定义一个类及其实例变量时，这些实例变量实际上存储在一个结构体（structure）中。你可以如何操作对象；它们实际上是结构体，其成员就是你的实例变量。当你使用 `alloc` 分配一个新对象时，会留出足够的空间来存放这些结构体之一。

结构中的继承成员之一（它来自根对象）是一个受保护的成员，称为 `isa`，它用于标识对象所属的类。由于它是结构的一部分（因此也是对象的一部分），它会随对象一起携带。通过这种方式，运行时系统始终可以通过查看其 `isa` 成员来识别对象的类（即使你将它赋值给一个通用的 `id` 对象变量）。

### 工作原理

你可以通过将成员设置为 `@public`（第 10 章中的讨论）来直接访问对象的结构成员。例如，如果你对 `Fraction` 类的分子（numerator）和分母（denominator）成员这样做，你可以在程序中使用如下表达式：

```
myFract->numerator
```

来直接访问 `Fraction` 对象 `myFract` 的分子成员。但我们强烈建议不要这样做。正如我们在第 10 章提到的，这违背了数据封装的原则。

## 事实 #2：对象变量实际上是一个指针

当你定义一个对象变量时，例如 `Fraction *myFract;`，

你正在定义一个名为 `myFract` 的指针变量。该变量被定义为指向你的类型 `Fraction`（这是你的类名称）的实体。当你分配一个 `Fraction` 的新实例时：

```
myFract = [Fraction alloc];
```

你正在内存中分配空间来存储一个新的 `Fraction`（即用于存放一个结构体的空间），然后将返回的指针存储在指针 `myFract` 内部。

当你将一个对象变量赋值给另一个变量时，例如 `myFract2 = myFract;`，

你只是在复制指针。两个变量指向内存中某处的同一个结构体。

## 事实 #3：方法是函数，消息表达式是函数调用

方法是真实的。当你调用方法时，你是在调用与接收者关联的函数。因此，关于传递参数、返回值和自动变量的所有规则，无论是对于函数还是方法都是相同的。Objective-C 编译器使用类名和方法名为每个函数创建一个唯一的名称。

## 事实 #4：id 类型是通用指针

因为对象是通过指针（即内存地址）引用的，所以你可以在 `id` 变量之间自由赋值。返回 `id` 类型的方法返回内存中某个对象的指针。

## 练习

- 写一个函数计算浮点数数组的平均值并返回结果。
- `Fraction` 类中的 `reduce` 方法找到分子和分母的最大公约数以简化分数。修改该方法，使其使用程序 15 中的 `gcd` 函数。你认为应该将该函数放在哪里？将函数设置为静态（static）有什么好处？你认为使用 `gcd` 函数还是像之前直接将代码合并方法更好？为什么？
- 一种被称为埃拉托尼筛（Sieve of Eratosthenes）的算法可以生成质数。该过程的算法所示。编写一个实现该算法的程序。让程序找到直到 n=150 的所有质数。与文中计算质数的方法相比，该算法有什么特点？
  - 步骤 1：定义一个整数数组 `P`。将所有元素 $P_i$ 设置为 0，$2 \le i \le n$。
  - 步骤 2：将 $i$ 设置为 2。
  - 步骤 3：如果 $i > n$，算法终止。
  - 步骤 4：如果 $P$ 为 0 且 $i < n$，将 $P_i$ 设置为 1。
  - 步骤 5：对于所有满足 $ij \le n$ 的整数值 $j$，将 $P_{ij}$ 设置为 1。
  - 步骤 6：将 $i$ 加 1 并返回步骤 3。
- 如文所述，定义 `Date` 类而不是 `date` 结构体更符合面向对象编程的概念。定义这样一个类，并带有相应的 `setter` `getter` 方法。还添加一个名为 `dateUpdate` 的方法来返回参数的后一天。
- 写一个函数将传递给它的数组中的 `Fraction` 相加，并作为 `Fraction` 返回结果。
- 为 `struct date` 写一个名为 `Date` 的类型定义，以便你可以进行如 `Date todays;` 的声明。

你是否认为将 `Date` 定义为类（class）而不是结构体（structure）有什么优势？你是否认为会有任何缺点？

7. 给定以下定义：

```objc
char *message = "Programming in Objective-C is fun";
char message[] = "You said it";
int x = 100;
```

确定以下集合中的每个 `NSLog` 调用是否有效，以及它的输出是否与该集合中的其他调用相同。

```
*** set 1 ***
NSLog("@%s", "Programming in Objective-C is fun");
NSLog("@%s", "Programming in Objective-C is fun");
NSLog("@%s", message);
```

```
*** set 2 ***
NSLog("@%s", "You said it");
NSLog("@%s", message2);
NSLog("@%s", &message2[0]);
```

```
*** set 3 ***
NSLog("@@said it");
NSLog("@%s", message2 + 4);
NSLog("@%s", &message2[4]);
```

8. 编写一个程序，在终端中打印出所有的命令行参数，每行一个。注意将包含空格字符的参数包含在引号内的效果。

9. 下列哪个语句会产生输出 `This is a test?`？请解释原因。

```
NSLog("@@This is a test");
NSLog("@@This is a test");
```

```
NSLog("@%s", "This is a test");
NSLog("@%s", "This is a test");
```

```
NSLog("@%s", "This is a test");
NSLog("@%s", "This is a test");
```

```
NSLog("@@%@", "This is a test");
NSLog("@@%@", "This is a test");
```

10. 将程序 13.14 中的交换函数重写为一个代码块（block）并进行测试。

# Foundation 框架简介

框架（Framework）是一系列在逻辑上组合在一起的类、方法、函数和文档，使得开发程序变得更容易。在 Mac OS X 上，有超过 90 个框架可用于开发应用程序，让你能够轻松地处理 Mac 的通讯录结构、刻录 CD、播放 DVD、使用 QuickTime 播放电影、播放歌曲等。

Foundation 框架为你所有的程序开发提供了基础，它是本书第二部分的主题，它让你能够处理基础对象（如数字和字符串）以及对象集合（如数组、字典和集合）。其他功能还提供了处理日期和时间、使用自动内存管理、处理底层文件系统、存储（或归档）对象，以及处理点和矩形等几何数据结构的功能。

Application Kit 包含了大量的类和方法，用于开发交互式图形应用程序。这些方法提供了轻松处理文本、菜单、工具栏、表格、文档和窗口的能力。在 Mac OS X 中，“Cocoa”这一术语统指 Foundation 框架、Application Kit 以及一个名为 Core Data 的第三个框架。Cocoa Touch 则统指 Foundation、Core Data 和 UIKit 框架。第三部分“Cocoa、Cocoa Touch 和 iOS SDK”对这一主题提供了更详细的内容。

## Foundation 文档

你应该利用存储在系统中的 Foundation 文档（如果你选择了下载本地副本），在 Apple 网站上也可以访问在线文档。大多数文档以 HTML 文件的形式存在供浏览器查看，或以 Acrobat 文件的形式存在。这些文档包含了对所有 Foundation 类以及所有实现的方法和函数的描述。我将 Foundation 文档的 URL 保存为浏览器的书签，这样我就可以轻松查询有关 Foundation 类的信息。

# 第 14 章 Foundation 框架简介

如果你正在使用 Xcode 开发程序，可以通过多种方式轻松地访问文档。你可以从 Help（帮助）菜单进入 Xcode Help（主文档窗口。此窗口允许你轻松搜索并访问存储在计算机本地或在线可用的文档。图 14.1 显示了在 Xcode Help 窗口中搜索字符串 "NSString" 的结果。

![](img/22d1310b7c22ea2d48cd2058929a5cda_320_0.png)

图 14.1 使用 Xcode 进行参考文档

如果你在 Xcode 中编辑文件，并想要获取头文件、方法或类的即时文档，只需将光标置于想要搜索的类、方法或变量上，按住 Option 键并点击。你将获得所选内容的简要摘要。图 14.2 显示了当鼠标光标位于文本 `NSString` 上、按下 Option 键并点击鼠标时出现的面板。

在出现面板的右上角，你会注意到两个图标：第一个是书的图标，第二个是里面有一个字母 `i`。如果你点击前者，Xcode 将为所选的类、协议、定义或方法搜索文档。如果你点击后者，将显示包含所选项目定义的头文件。这种 Quick Help（快速帮助）还允许通过链接（如果可用）快速访问其他引用、相关文档以及使用指定类或方法的示例代码。这真的是一个非常棒且方便的工具，你应该学会使用它！

## Foundation 文档

![](img/22d1310b7c22ea2d48cd2058929a5cda_321_0.png)

图 14.2 NSString 的快速引用

你也可以通过选择 View（视图）、Utilities（工具）、Quick Help（快速帮助）来开启 Quick Help 面板，使其在你程序中输入或选择项目时自动更新。这将提供类似于图 14.3 所示的窗口，它默认显示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_321_1.png)

图 14.3 显示在面板中的快速帮助。

你也可以在 Apple 网站上访问在线参考库：http://developer.apple.com/library/mac/navigation/index.html 进行导航。在该地址，你还可以找到有关特定编程问题的文档，例如内存管理、字符串和文件管理。

除非你在 Xcode 中订阅了特定的文档集，否则在线文档可能比磁盘存储的更更新。

以上就是对 Foundation 框架的简单介绍。

## 数字、字符串和集合

本章描述了如何处理 Foundation 提供的基础对象。这些包括数字、字符串和集合，集合指的是以数组、字典和集合形式处理对象组的能力。

# 第 15 章 数字、字符串、集合

## 程序 15.1

```objc
// 处理数字
```

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @leaseleasepool {
        NSNumber *myNumber, *floatNumber, *intNumber;
        NSInteger *myInt;

        // integer 类型值
        intNumber = [NSNumber numberWithInteger:100];
        myInt = [intNumber integerValue];
        NSLog("%li", (long) myInt);

        // long 类型值
        myNumber = [NSNumber numberWithLong: 0abcdef];
        NSLog("%lx", [myNumber longValue]);

        // char 类型值
        myNumber = [NSNumber numberWithChar: 'X'];
        NSLog("%c", [myNumber charValue]);

        // float 类型值
        floatNumber = [NSNumber numberWithFloat: 100.00];
        NSLog("%f", [floatNumber floatValue]);

        // double
        myNumber = [NSNumber numberWithDouble: 12345e+15];
        NSLog("%lg", [myNumber doubleValue]);

        // 此处访问错误
        NSLog("%li", (long) [myNumber integerValue]);

        // 测试两个 Number 是否相等
        if ([intNumber isEqualToNumber:floatNumber] == YES) {
            NSLog("%@Numbers are equal");
        } else {
            NSLog("%@Numbers are not equal");
        }
    }
}
```

### 数字对象 309

```objc
// 测试一个 Number 是否小于、等于或大于第二个个 Number
if ([intNumber compare:myNumber] == NSOrderedAscending) {
    NSLog("First number is less than second");
}

return 0;
```



## 程序 15.1 输出

```
100
abdef
X
100
1.2345e+19
0
Numbers are equal
First number is less than second
```

`NSNumber` 类包含了一些方法，允许你创建带有初始值的 `NSNumber` 对象。例如，下面这行代码
`intNumber = [NSNumber initWithInteger:100];`
创建了一个值为 100 的对象。

在 `NSLog` 中，我们将 `NSInteger myInt` 转换为 `long` 类型，并使用格式化字符串确保即使程序为 32 位架构编译，值也能被正确解析和显示。
对于每种基本数据类型，一个类方法都会分配一个 `NSNumber` 对象并将其设置为指定值。这些方法以 `numberWith` 开头，后跟类型，例如 `numberWithLong:`；依此类推。此外，还可以使用实例方法将之前分配的 `NSNumber` 对象设置为指定值。这些方法都以 `initWith:` 开头，例如 `initWithLong:` 和 `initWithFloat:`。
表 15.1 列出了获取 `NSNumber` 对象的类方法和实例方法，以及获取其值的对应实例方法。

## 第 15 章 数字、字符串和集合

> **注意**
> 在 4.2 之前的 Xcode 版本中，使用哪个版本的方法更为重要。类会创建一个被自动释放（autoreleased）的对象，而通过 `alloc` 创建的对象则由你在使用完毕后负责释放内存。Objective-C 引入自动引用计数 (ARC) 意味着不再有强烈的理由去使用其中一种方法而非另一种，因为内存管理现在由系统自动处理。

### 表 15.1 NSNumber 创建与检索方法

| 创建与初始化方法 | 初始化方法 | 检索实例方法 |
| --- | --- | --- |
| `numberWithChar:` | `initWithChar:` | `charValue` |
| `numberWithUnsignedChar:` | `initWithUnsignedChar:` | `unsignedValue` |
| `numberWithShort:` | `initWithShort:` | `shortValue` |
| `numberWithUnsignedShort:` | `initWithUnsignedShort:` | `unsignedValue` |
| `numberWithInteger:` | `initWithInteger:` | `integerValue` |
| `numberWithUnsignedInteger:` | `initWithUnsignedInteger:` | `unsignedIntegerValue` |
| `numberWithInt:` | `initWithInt:` | `intValue` |
| `numberWithUnsignedInt:` | `initWithUnsignedInt:` | `unsignedIntValue` |
| `numberWithLong:` | `initWithLong:` | `longValue` |
| `numberWithUnsignedLong:` | `initWithUnsignedLong:` | `unsignedValue` |
| `numberWithLongLong:` | `initWithLongLong:` | `longlongValue` |
| `numberWithUnsignedLongLong:` | `initWithUnsignedLongLong:` | `unsignedLongLongValue` |
| `numberWithFloat:` | `initWithFloat:` | `floatValue` |
| `numberWithDouble:` | `initWithDouble:` | `doubleValue` |
| `numberWithBool:` | `initWithBool:` | `boolValue` |

回到程序 15.1，程序使用这些类来创建 `long`、`char`、`float` 和 `NSNumber` 对象。注意在你通过这一行代码创建一个 `double` 后
`myNumber = [NSNumber numberWithDouble: 12345e+15];`

发生了什么，然后你尝试用下面这行代码（错误地）并并显示值：
`NSLog("%li", (long) [myNumber integerValue]);`

我们显示的输出是 0，你可能会得到不同的结果，因为这种访问是无效的。
此外，你不会收到系统的错误信息。通常情况下，确保在 `NSNumber` 对象中存储值后以一致的方式检索它，是你的责任。

### 数字对象

在 `if` 语句内部，表达式

```objc
[intNumber isEqualToNumber:floatNumber]
```

使用 `isEqualToNumber:` 方法数值上比较两个 `NSNumber` 对象。程序测试返回的 `BOOL` 值以判断数字是否相等。你可以使用 `compare:` 方法测试一个数字是否小于、等于或大于另一个数字。表达式

```objc
[intNumber compare:myNumber]
```

如果第一个数字小于第二个数字，返回 `NSOrderedAscending`；如果数字相等，则返回 `NSOrderedSame`；如果第一个数字大于第二个，则返回 `NSOrderedDescending`。

### 字符串对象

你以前在程序中遇到过字符串对象。每当你在双引号内包含字符序列，例如

```objc
@"Programming is fun"
```

你在 Objective-C 中创建一个字符字符串对象。Foundation 框架支持名为 `NSString` 的类来处理字符串对象。C 风格字符串由 `char` 字符组成，`NSString` 由 `unichar` 字符组成。根据 Unicode 标准，`unichar` 是多字节字符。这使得你能够处理包含字符的字符集。幸运的是，你不需要担心字符串中字符的内部表示，因为 `NSString` 类会自动处理。通过使用该类的方法，你可以更轻松地开发本地化应用程序——即适用于世界上不同语言的应用。

#### 关于 NSLog 函数

下面的程序 15.2 显示了如何定义 `NSString` 对象并为其分配初始值。它还展示了如何使用格式化符 `%@` 显示 `NSString` 对象。

##### 程序 15.2

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSString *str = @"Programming is fun";
        NSLog("%@", str);
    }
    return 0;
}
```

##### 程序 15.2 输出

编程很有趣

在这一行中

```objc
NSString *str = @"Programming is fun";
```

常量对象字符串 "Programming is fun" 被赋值给 `NSString` 变量 `str`。
然后使用 `NSLog` 显示该值。
`NSLog` 的格式化字符 `%@` 不仅可以显示 `NSString` 对象，还可以显示其他对象。例如，给定

```objc
NSNumber *intNumber = [NSNumber numberWithInteger:100];
```

调用 `NSLog` 方法

```objc
NSLog("%@", intNumber);
```

产生以下输出：

```
100
```

#### description 方法

你可以使用 `%@` 格式化字符显示数组、字典和集合的所有内容。事实上，只要你重写了类继承的 `description` 方法，就可以用它显示你自定义类的对象。如果你没有重写该方法，`NSLog` 只会显示所属的类名以及对象在内存中的地址。`description` 方法的默认实现继承自 `NSObject` 类。

下面是一个你可以添加到你的 `Fraction` 类实现中的 `description` 方法示例，用于格式化 `Fraction` 对象。它使用了 `NSString` 的 `stringWithFormat:` 方法；该方法与 `NSLog` 相似，但与函数不同，该方法的目的是返回格式化后的字符串作为结果，而不是将其写入控制台：

```objc
- (NSString *) description {
    return [NSString stringWithFormat:@"%@/%@", numerator, denominator];
}
```

> **注意**
> 诸如 `stringWithFormat:` 等方法允许提供任意数量的参数（在这种情况下，为格式化字符串和待格式化的数据）。参数以逗号分隔的值列表的形式提供给方法。

在你的 `Fraction` 类中定义了该方法（以及恰当的带有两个 `Fraction` 对象 `f1` 和 `f2` 的语句）后，你就可以在程序中编写如下所示的语句：

```objc
sum = [f1 add:f2];
NSLog(@"The sum of %@ and %@ is %@", f1, f2, sum);
```

为了得到如下单行输出：

The sum of 1/2 and 1/4 is 3/4（1/2 和 1/4 的和为 3/4）

为你的类添加自定义的 `description` 方法是一个很好的调试工具——它允许你以有意义的方式显示你的对象。

#### 可变对象与不可变对象

当你通过编写如下表达式创建字符串对象时

```objc
@"Programming is fun"
```

你创建了一个内容不能更改的对象。这被称为**不可变对象**。`NSString` 类处理不可变字符串。通常，你可能想要处理可以更改其字符的字符串。例如，你可能想从字符串中删除某些字符，或对字符串执行搜索并替换操作。这类字符串通过 `NSMutableString` 类进行处理。

程序 15.3 显示了在程序中处理不可变字符字符串的基本方法。

##### 程序 15.3

```objc
// 基本字符串操作
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSString *str1 = @"This is string A";
        NSString *str2 = @"This is string B";
        NSString *res = @"res";
        NSComparisonResult compareResult;

        // 统计字符数量
        NSLog(@"Length of string: %lu", [str1 length]);

        // 将一个字符串拷贝到另一个
        res = [NSString stringWithString:str1];
        NSLog(@"copy: %@", res);

        // 将一个追加到另一个末尾
        str2 = [str1 stringByAppendingString:str2];
        NSLog(@"Concatenation: %@", str2);

        // 测试两个字符串是否相等
        if ([str1 isEqualToString:res] == YES)
            NSLog(@"str == res");
        else
            NSLog(@"str != res");

        // 测试一个字符串是否小于
```

##### 程序 15.3 输出

```
Length of str1: 16
Copy: This is string A
Concatenation: this is string A string B
str1 = res
str1 < str2
Uppercase conversion: THIS IS STRING A
Lowercase conversion: this is string a
Original string: This is string A
```

程序 15.3 首先声明了两个不可变的 `NSString` 对象：`str1`、`str2` 和 `res`。
前两个初始化为常量字符串对象。声明语句

```objc
NSComparisonResult compareResult;
```

声明 `compareResult` 用于存储稍后在程序执行的字符串比较的结果。

你可以使用 `length` 方法统计字符串中的字符数量。它返回一个 `NSUInteger` 类型的无符号整数值。输出验证了字符串

`This is string A`

包含 16 个字符。语句

```objc
res = [NSString stringWithString:str1];
```

显示了如何使用另一个字符串的内容创建一个新字符串。生成的 `NSString` 对象被赋值给 `res`，然后显示以验证结果。这里对字符串内容进行了实际拷贝，而不仅仅是内存中同一个字符串的引用。这意味着 `str1` 和 `res` 指向不同的字符串对象，这与仅仅执行简单的赋值不同：

```objc
res = str1;
```

正如我们之前讨论过的，这仅仅会创建内存中同一个对象的另一个引用。

`stringByAppendingString:` 方法可以连接两个字符字符串。因此，表达式

```objc
[str1 stringByAppendingString:str2];
```

创建了一个新字符串，由字符 `str1` 后接 `str2` 组成。`isEqualToString:` 方法用于判断两个字符串是否相等。如果你需要确定字符串的顺序，可以使用 `compare:` 方法。例如，如果第一个字符串小于第二个，它返回 `NSOrderedAscending`；如果第一个字符串大于第二个，返回 `NSOrderedDescending`；如果它们相等，则返回 `NSOrderedSame`。如果你想执行不区分大小写的比较，可以使用 `caseInsensitiveCompare:` 方法。

`uppercaseString` 和 `lowercaseString` 方法是程序 15.3 中最后的，用于将字符串转换为大写和小写。再次，转换不会影响原始字符串。这是一个非常重要的点。让我们结合图表再次来看。图 15.1 显示了变量 `res` 和 `str1` 刚刚被声明并初始化。变量 `res` 没有设置任何初始值，所以它的内容显示为空。另一方面，`str1` 被设置为指向存储在内存某处的常量对象 `@"This is string A"`。

```objc
NSString *str1 = @"This is string A"
// str1 = "This is string A"

NSString *res;
// res //
```

图 15.1 不可变字符串对象的声明与初始化

当我们在程序 15.3 中向 `str1` 发送 `uppercaseString` 消息时，我们得到了由字符 `str1` 创建的新字符串，该字符串对象中的任何小写字母都被替换为大写字母。如图 15.2 所示。

```objc
NSString *str1 = @"This is string A"
// str1 = "This is string A"
res = [str1 uppercaseString]
// res // THIS IS STRING A
```

图 15.2 向字符串对象发送 uppercaseString 消息

注意，`str1` 仍然指向原始字符串对象，创建了一个新的字符串对象。

向 `str1` 发送 `lowercaseString` 消息的方式相同：一个新对象由 `str1` 的所有大写字母转换为小写组成。新创建的字符串的引用存储在变量 `res` 中。如图 15.3 所示。注意，不再有对上一步中创建的大写字符串的引用。你不需要担心这一点；系统的内存管理机制会为你清理。

```objc
NSString *str1 = @"This is string A"
// str1 = "This is string A"
res = [str1 lowercaseString]
// res // this is string a
```

图 15.3 向字符串对象发送 lowercaseString 消息

## 第 15 章 数字、字符串与集合

程序 15.4 展示了处理字符串的额外方法。这些方法允许你从字符串中提取子字符串，还可以在一个字符串中搜索另一个字符串的出现。

某些方法要求你通过范围来标识子字符串，即一个索引号加上字符计数。索引号从零开始，因此字符串中的前三个字符由数字对 (0, 3) 指定。`NSString` 类（以及其他 Foundation 类）的一些方法使用特殊数据类型 `NSRange` 来创建范围指定。它实际上是一个包含两个成员（`location` 和 `length`）的结构类型定义（typedef），每个成员的类型都是 `NSInteger`。程序 15.4 使用了这种数据类型。

> **注意**
> 你可以在第 13 章“底层 C 语言特征”中阅读关于结构的内容。不过，你可能从本章随后的讨论中获得足够的信息来操作它们。

##### 程序 15.4

```objc
// 字符串操作 - 继续
#import <Foundation/Foundation.h>

int main(int argc, char * argv[]) {
    @autoreleasepool {
        NSString *str = @"This is string A";
        NSString *res;
        NSRange subRange;

        // 提取字符串的前 3 个字符
```



# 第 15 章 数字、字符串与集合

## 字符串对象

```objc
res = [str substringToIndex:3];

NSLog("First 3 chars of str: %@", res);

// 从索引 5 开始提取到末尾

res = [str substringFromIndex:5];

NSLog("Chars from index 5 of str: %@", res);

// 提取索引 8 到 13 的字符（6 个字符）

res = [[str substringFromIndex:8] substringToIndex:6];

NSLog("Chars from index 8 through 13: %@", res);

// 实现相同功能的简单方法

res = [str substringWithRange:NSMakeRange(8, 6)];

NSLog("Chars from index 8 through 13: %@", res);

}
}
```

### 在另一个字符串中定位字符串

```objc
subRange = [str rangeOfString: @"string A"];

NSLog("String is at index %lu, length is %lu",
subRange.location,subRange.length);
```

```objc
subRange = [str rangeOfString: @"string B"];

if (subRange.location == NSNotFound)
    NSLog("String not found");
else
    NSLog("String is at index %lu, length is %lu",
    subRange.location,subRange.length);
```

```objc
return 0;

}
```

## 程序 15.4 输出

First 3 chars of str1: Thi
Chars from index 5 of str1: string A
Chars from index 8 through 13: string
Chars from index 8 through 13: string
String is at index 8, length is 8
String not found

`substringToIndex:` 方法创建一个从字符串起始字符开始到但不包含指定索引号的子字符串。因为索引从 0 开始，参数 `3` 会从字符串中提取第 0、1、2 3 个字符，并返回结果的字符串对象。对于任何接受索引号作为其中一个参数的方法，如果你提供了无效的索引号，将会收到 "Range out of bounds"（范围越界）的错误消息。

`substringFromIndex:` 方法返回一个从接收者指定索引处的字符开始一直到字符串末尾的子字符串。

```objc
res = [[str substringToIndex:8] substringFromIndex:6];
```

展示了如何结合这两个方法来从字符串内部提取字符子字符串。`substringFromIndex:` 方法首先用于提取从索引 8 到字符串末尾的字符；然后将 `substringToIndex` 应用于结果以获取前六个字符。结果是代表原始字符串中字符范围 ( 8, 6 ) 的子字符串。

`substringWithRange` 方法一步到位完成了我们刚刚分两步完成的操作：它接收一个范围并返回指定范围内的字符。特殊函数

```objc
NSMakeRange(8, 6)
```

根据其参数创建一个范围并返回结果。该结果作为参数传递给 `substringWithRange:` 方法。

要在另一个字符串中定位一个字符串，你可以使用 `rangeOfString:` 方法。如果从接收者内部找到了指定的字符串，返回的范围将精确指定该字符串所在的位置。如果未找到，返回的范围的 `location` 成员将被设置为 `NSNotFound`。

因此，语句

```objc
subRange = [str rangeOfString:@"string*"];
```

将方法返回的 `NSRange` 结构赋值给 `NSRange` 变量 `subRange`。记住 `subRange` 不是对象值，而是一个结构变量（程序中 `subRange` 的声明也没有包含星号——这通常是你没有处理对象的良好线——一个显著的例外是 `id` 类型）。它的成员可以通过结构成员运算符点 `()` 获取。因此，表达式 `subRange.location` 给结构中 `location` 成员的值，而 `subRange.length` 提供 `length` 成员。这些值被传递给 `NSLog` 函数进行显示。

## 可变字符串

`MutableString` 类可以用于创建可以更改字符的字符串对象。由于该类是 `NSString` 的子类，因此所有 `NSString` 的方法都可以。

当我们谈论不可变对象时，我们指的是字符串内部的实际字符。可变或不可变对象始终可以设置为完全不同的字符串。在这种情况下，`str` 首先被设置为常量字符串。在程序的后面，它被设置为可变对象。程序 15.5 展示了处理可变字符串的一些方法。在这种情况下，`str` 可以被声明为可变或不可变对象。请务必理解这一点。

## 程序 15.5

// 字符串操作 - 可变字符串

```objc
#import <Foundation/Foundation.h>

 main(int argc, char * argv[]) {

    autoreleasepool {

        NSString *str = @"This is string A";

        NSString *search;

        NSMutableString *mstr;

        NSRange substr;

        // 从...中创建可变字符串

        mstr = [NSMutableString stringWithString:str];

        NSLog(@"%@", mstr);

        // 插入字符

        [mstr insertString:@"mutable" atIndex:7];

        NSLog(@"%@", mstr);

        // 在末尾有效插入

        [mstr insertString:@" string B" atIndex:[mstr length]];

        NSLog(@"%@", mstr);

        // 删除字符

        [mstr deleteCharactersInRange:NSMakeRange(16, 13)];

        NSLog(@"%@", mstr);

        // 查找第一个并用于删除

        substr = [mstr rangeOfString:@"string B"];

        if (substr.location != NSNotFound) {

            [mstr deleteCharactersInRange:substr];

        }

        NSLog(@"%@", mstr);

        // 搜索并替换所有

        search = @"This is";

        substr = [mstr rangeOfString:search];

        while (substr.location != NSNotFound) {

            [mstr replaceCharactersInRange:substr withString:@"X"];

            substr = [mstr rangeOfString:search];

        }

        NSLog(@"%@", mstr);

        return 0;

    }

}
```

## 程序 15.5 输出

This is string A
This is mutable string A
This is mutable string A and string B
This is mutable string A and string B and C
This is mutable string B and C
This is mutable string C
X B and C

使用 `rangeString` 方法返回的范围作为参数来删除这些字符。

你可以使用 `setString` 直接设置可变字符串对象的内容。使用此方法将 `mstr` 设置为字符串 "This is string A"，而 `replaceCharactersInRange:withString:` 方法会将字符串中的某些字符替换为另一个字符串。两个字符串的大小不需要相等，也可以是不等长度；你可以在该语句中将一个字符串替换为另一个 `mstr`：

```objc
[mstr replaceCharactersInRange:NSMakeRange(8, 8)
String:@"mutable string"];
```

请注意，如果替换字符串也包含搜索字符串（例如，将字符串替换为 "string"），你将会导致无限循环。
其次，如果替换字符串为空（即它不包含任何字符），你实际上是删除了搜索字符串的所有出现处。一个空字符字符串对象通过一对相邻的引号来指定，引号之间没有空格：

```objc
replace = @"";
```

当然，如果你只想删除字符串的某一个出现处，可以像你已经见过的的那样使用 `deleteCharactersInRange:` 方法。

最后，`NSMutableString` 类还包含一个 `replaceOccurrencesOfString:options:range:` 方法，你可以用它对字符串进行“查找并替换所有”。事实上，你可以用这一条语句替换程序 15.5 中的循环：

```objc
[mstr replaceOccurrencesOfString:search
withString:replace
options:nil
range:NSMakeRange(0, [mstr length])];
```



这实现了相同的结果，并避免了可能出现的无限循环风险，因为该方法防止了这种情况的发生。

`NSString` 类包含了超过 100 个可以与字符串对象一起工作的方法。表 15.2 总结了一些最常用的方法，表 15.3 列出了 `NSMutableString` 类提供的一些额外方法。其他 `NSString` 方法（例如处理路径名和将文件内容读取到字符串中）将在本书的剩余部分不断向你介绍。你应该查看 `NSString` 类的文档，以更好地了解你可以使用的各种方法。

## 字符串对象

### 表 15.2 常用 NSString 方法

| 方法 | 描述 |
| --- | --- |
| `+(id) stringWithContentsFile: path encoding: enc; error: err` | 创建一个新字符串，并设置为由 `path` 指定的文件内容，使用字符编码 `enc`；如果 `err` 非空，则在 `err` 中返回错误 |
| `+(id) stringWithContentsOfURL: url encoding: enc; error: err` | 创建一个新字符串，并设置为 `url` 的内容，使用字符编码 `enc`；如果 `err` 非空，则在 `err` 中返回错误 |
| `+(id) string` | 创建一个空字符串 |
| `+(id) stringWithString: nsstring` | 创建一个新字符串，并将其设置为 `nsstring` |
| `+ (NSString *) stringWithFormat: format, arg1, arg2, arg3...` | 根据指定的格式和参数 `arg1`, `arg2`, `arg3`... 创建一个新字符串 |
| `- (id) initWithWithString: nsstring` | 将新分配的字符串设置为 `nsstring` |
| `- (id)initWithContentsOfFile: path encoding: enc; error: err` | 将字符串设置为由 `path` 指定的文件内容 |
| `- (id)initWithContentsOfURL: url encoding: enc; error: err` | 使用字符编码 `enc` 将字符串设置为 `url` (`NSURL *`) 的内容，如果 `err` 非空，则在 `err` 中返回错误 |
| `-(NSUInteger) length` | 返回字符串中的字符数 |
| `-(char) characterAtIndex: i` | 返回索引 `i` 处的 Unicode 字符 |
| `-(NSString *) substringFromIndex: i` | 返回从 `i` 字符到末的子字符串 |
| `-(NSString *) substringWithRange: range` | 根据指定的范围返回子字符串 |
| `-(NSString *) substringToIndex: i` | 返回从字符串开始到索引 `i` 字符的子字符串 |
| `-(NSComparator *) caseInsensitiveCompare: nsstring` | 忽略大小写比较两个字符串 |
| `-(NSComparator *) compare: nsstring` | 比较两个字符串 |
| `-(BOOL) hasPrefix: nsstring` | 测试字符串是否以 `nsstring` 开头 |
| `-(BOOL) hasSuffix: nsstring` | 测试字符串是否以 `nsstring` 结尾 |
| `-(BOOL) isEqualToString: nsstring` | 测试两个字符串是否相等 |
| `- (NSString *) capitalizedString` | 返回一个每个单词首字母大写的字符串（并将每个单词的其余字母转换为小写） |
| `- (NSString *) lowercaseString` | 返回一个转换为小写的字符串 |
| `- (NSString *) uppercaseString` | 返回一个转换为大写的字符串 |
| `- (const char *) UTF8String` | 返回一个转换为 UTF-8 字符字符串的字符串 |
| `- (double) doubleValue` | 返回字符串的双精度浮点表示 |
| `- (float) floatValue` | 返回字符串的浮点表示 |
| `- (NSInteger) integerValue` | 返回字符串的 `NSInteger` 表示 |
| `- (int) intValue` | 返回字符串的整数表示 |

在表 15.2 和 15.3 中，`url` 是 `NSURL` 对象，`path` 是指定文件路径的 `NSString` 对象，`nsstring` 是 `NSString` 对象，`n` 是表示字符串中有效字符数的 `NSInteger`，`enc` 是指定字符编码的 `NSStringEncoding`，`err` 是发生错误时描述错误的 `NSError`，`size` 和 `opts` 是 `NSInteger`，`range` 是指示字符串内有效范围的 `NSRange`。

表 15.3 中的方法要么创建或修改 `MutableString` 对象。`NSString` 对象在本文后续被广泛使用。如果你需要将字符串解析为标记，可以查看 Foundation 的 `NSScanner` 类。

### 表 15.3 常用 MutableString 方法

| 方法 | 描述 |
| --- | --- |
| `+ (id) stringWithCapacity: size` | 创建一个包含 `size` 个字符的字符串 |
| `(id) initWithCapacity: size` | 初始化一个容量为 `size` 的字符串 |
| `(void) setString: nsstring` | 将字符串设置为 `nsstring` |
| `(void) appendString: nsstring` | 在接收者末尾追加 `nsstring` |
| `(void) deleteCharactersInRange: range` | 删除指定范围内的字符 |
| `(void) insertString: nsstring atIndex: i` | 在索引 `i` 处向接收者中插入 `nsstring` |
| `(void) replaceCharactersInRange: range` | 替换指定范围内的字符 |

## 第 15 章 数字、字符串与集合

### 程序 15.6 输出

| 月份名称 |
| :--- |
| 1 一月 |
| 2 二月 |
| 3 三月 |
| 4 四月 |
| 5 五月 |
| 6 六月 |
| 7 七月 |
| 8 八月 |
| 9 九月 |
| 10 十月 |
| 11 十一月 |
| 12 十二月 |

你可以使用类方法 `arrayWithObjects:` 来创建一个以对象列表作为元素的数组。在这种情况下，对象按顺序列出并用逗号分隔。这种语法用于可以接受变数量参数的方法。为了标记列表的结束，必须将 `nil` 指定为列表的最后一个值——它不会被存储在数组内部。

在程序 15.6 中，我们将通过参数 `arrayWithObjects:` 指定的 12 个值设置给 `monthNames`。

数组中的元素通过其索引数字来标识。与 `NSString` 类似，索引从 0 开始。一个包含 12 个元素的数组具有有效的索引数字 0–11。要使用索引数字检索数组的元素，你需要使用 `objectAtIndex:` 方法。

程序简单地执行一个 `for` 循环，使用 `objectAtIndex:` 方法从数组中提取每个元素。每个检索到的元素都通过 `NSLog` 显示。

程序 15.7 简单地创建一个包含 10 个数字对象的数组，其值范围从 0 到 9。通过使用简单的 `for` 循环检索这些值，然后仅使用 `NSLog` 字符串格式中的 `%d` 格式字符显示整个数组。在在本章的后半部分，你将学习另一种被称为“快速枚举”（fast enumeration）的技巧，你也可以用它遍历数组的元素。

### 程序 15.7

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        NSMutableArray *numbers = [NSMutableArray array];

        NSNumber *myNumber;

        int i;

        // 创建一个包含数字 0-9 的数组

        for (i = 0; i < 10; ++i) {

            myNumber = [NSNumber initWithInteger:i];

            [numbers addObject: myNumber];

        }

        // 遍历数组并显示值

        for (i = 0; i < 10; ++i) {

            myNumber = [numbers objectAtIndex:i];

            NSLog("%@*", myNumber);

        }

        // 观察 NSLog 如何仅用一个 % 显示它

        NSLog("%===== Using a single NSLog*");

        NSLog("%@*", numbers);

    }

}
```

### 程序 15.7 输出

```
2010-11-12 15:25:42.701 prog15.7[639:903] 0
2010-11-12 15:25:42.704 prog15.7[639:903] 1
2010-11-12 15:25:42.704 prog15.7[639:903] 2
2010-11-12 15:25:42.704 prog15.7[639:903] 3
2010-11-12 15:25:42.705 prog15.7[639:903] 4
2010-11-12 15:25:42.705 prog15.7[639:903] 5
2010-11-12 15:25:42.706 prog15.7[639:903] 6
2010-11-12 15:25:42.706 prog15.7[639:903] 7
2010-11-12 15:25:42.706 prog15.7[639:903] 8
2010-11-12 15:25:42.706 prog15.7[639:903] 9
2010-11-12 15:25:42.707 prog15.7[639:903] ===== Using a single NSLog
2010-11-12 15:25:42.707 prog15.7[639:903] (
0,
1,
2,
3,
4,
5,
6,
7,
8,
9)
```

## 第 15 章 数字、NSLog 与集合

（在这里我们保留了所有的 `NSLog` 输出，以便区分第一、二组输出在外观上的差异。）

`NSMutableArray` 的 `array` 方法只是简单地为你创建一个空的可变数组对象。数组中的元素数量未指定，数组可以根据你的需要任意变大。

记住，你不能将整数等基本类型存储到数组之类的集合中。因此，我们为 `i` 的每个值（范围从 0 到 9）创建一个 `NSNumber` 对象。

`addObject:` 将一个对象添加到数组末尾。在这里你添加从 `i` 的整数值创建的每个 `NSNumber` 对象。

程序进入一个 `for` 循环来显示数组中的每个数字对象。

最后，在程序 15.7 中，你展示了 `NSLog` 格式字符串中使用单个 `%` 就可以一次性显示整个 `numbers` 数组。

> `NSLog` 是如何知道如何显示存储在数组中的对象的？

## 第 15 章 数字、字符串和集合

这里有新的 `setName:` 和 `setEmail:` 方法，它们可以减少一些工作：

```objc
(void) setName:(NSString *)theName
{
    if (name != theName)
        name = [NSString stringWith:theName];
}
```

```objc
(void) setEmail:(NSString *)theEmail
{
    if (email != theEmail)
        email = [NSString stringWith:theEmail];
}
```

该测试是为了防止有人向设置器（setter）发送一个已经存储在实例变量中的对象。如果传递的对象与存储的对象相同，我们就不需要进行任何操作了。

# 合成访问器方法

现在我们已经讨论了编写访问器方法 `setName:` 和 `setEmail:` 的方法，你也理解了这些原理。正如我们在之前的版本中所做的那样，我们可以系统自动为你生成这些访问器方法。考虑 AddressCard 接口的第二个版本：

```objc
#import <Foundation/Foundation.h>
```

```objc
@interface AddressCard: NSObject

@property (copy, nonatomic) NSString *name, *email;

-(void) print;

@end
```

这一行

```objc
@property (copy, nonatomic) NSString *name, *email;
```

列出了这些属性的 `copy` 和 `nonatomic` 属性。`copy` 属性用于在设置器方法中创建实例变量的副本，就像在你写的版本中所做的那样。默认属性是不复制，而是执行简单的赋值（即默认属性 `assign`），正如我们最近讨论的，这在在这种情况下是不正确的方法。

`nonatomic` 属性表示你不需要担心多个线程尝试同时访问实例变量时可能发生的竞态条件。第 18 章“拷贝对象”将更详细地讨论这个主题。

程序 15.9 是新的 AddressCard 实现文件，它指定访问器方法是合成的。（注意，我们在这里删除了对实例变量的显式声明，因为我们已经为它们列出了属性。）

### 程序 15.9 实现文件：带有合成方法的 AddressCard.m

```objc
#import "AddressCard.h"

@implementation AddressCard

@synthesize name, email;

-(void) print {
    NSLog("@=============================\
```

现在让我们为你的 AddressCard 类添加另一个方法。你可能希望通过一次调用同时设置卡片的名称和电子邮箱字段。要这样做，请添加一个新方法 `setName:andEmail:`。新方法看起来如下：

```objc
-(void) setName:(NSString *)theName andEmail:(NSString *)theEmail {
    self.name = theName;
    self.email = theEmail;
}
```

记得编写

```objc
self.name = theName;
```

等同于编写

```objc
[self setName:theName];
```

你可能还想要一个 `initWith:andEmail:` 初始化方法，但我们在这里不显示它。

并因此，它使用了实例变量的设置器方法。这与编写
`name = theName;` 形成对比，后者跳过了设置器，并直接将参数的值赋值给实例变量。

通过依赖合成的设置器方法来设置相应的实例变量（而不是在方法内部直接设置它们），你增加了一层抽象，从而使程序对其内部数据结构的依赖稍微降低。你还利用了合成的属性属性，在这种情况下，它们是 `copy` 而不是 `assign` 赋值给实例变量。

### 程序 15.9 测试程序

```objc
#import "AddressCard.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSString *aName = @"Julia Kochan";
        NSString *aEmail = @"jewls337@axlc.com";
        NSString *bName = @"Tony Lannino";
        NSString *bEmail = @"tony.iannino@techfitness.com";
        AddressCard *card1 = [[AddressCard alloc] init];
        AddressCard *card2 = [[AddressCard alloc] init];
        [card1 setName:aName andEmail:aEmail];
        [card2 setName:bName andEmail:bEmail];
        [card1 print];
        [card2 print];
    }
    return 0;
}
```



## 程序 15.9 输出

| ============== |
| Julia Kochan             |
| jewls337@axlc.com         |
|                           |
|      0              |
| ==============             

## AddressBook 类

`AddressCard` 类看起来运行良好。如果你想处理很多 `AddressBook` 呢？将它们收集起来是有意义的，这正是你通过定义一个名为 `AddressBook` 的类来实现的。`AddressBook` 类将存储地址簿名称和一组 `AddressCard`，你把它们存储在数组中。你可能想要创建一个地址簿，向其中添加新的联系卡，列出内容，并搜索地址簿、删除条目、编辑现有条目、进行排序，甚至对其内容进行拷贝。

让我们从简单的接口文件开始（参见程序 15.10）。

## 程序 15.10 AddressBook.h 接口

```objc
#import <Foundation/Foundation.h>

#import "AddressCard.h"

@interface AddressBook : NSObject

@property (copy, nonatomic) NSString *name;

@property (strong, nonatomic) NSMutableArray *book;

-(id)initWithName:(NSString *)name;

-(void)addCard:(AddressCard *)theCard;

-(NSUInteger)entries;

-(void)list;

@end
```

## 第 15 章 数字、字符串和集合

`initWith:` 方法设置数组。`addCard:` 方法向地址簿添加 `AddressCard`。`entries` 方法返回地址簿中的联系卡数量。`list` 方法提供其内容。程序 15.10 显示了 `AddressBook` 的实现。

```objc
NSLog("=================================");

@end
```

属性的 `strong` 在第 17 章“内存管理与自动引用计数”中有更详细的描述。

## 程序 15.10 AddressBook.m 实现

```objc
#import "AddressBook.h"

@implementation AddressBook

@synthesize name, book;

-(id)initWithName:(NSString *)name
{
    self = [super init];
    if (self) {
        name = [NSString stringWith:name];
        book = [NSMutableArray array];
    }
    return self;
}

-(void)addCard:(AddressCard *)theCard
{
    [book addObject:theCard];
}

-(NSUInteger)entries
{
    return [book count];
}

-(void)list
{
    NSLog("Contents of: %@", name);
    for (AddressCard *theCard in book) {
        NSLog("%-20s %-32s", theCard.name UTFString, theCard.email UTFString);
    }
}

@end
```

# 第15章 数字、字符串与集合

## 程序 15.10 测试程序

```objc
#import "AddressBook.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        NSString *name = @"Julia Kochan";
        NSString *email = @"jewls337@axlc.com";
        NSString *tname = @"Tony Iannino";
        NSString *email = @"tony.iannino@techfitness.com";
        NSString *dname = @"Stephen Kochan";
        NSString *email = @"steve@classroomM.com";
        NSString *dname = @"Jamie Baker";
        NSString *demail = @"jbaker@classroomM.com";

        AddressCard *card1 = [[AddressCard alloc] init];
        AddressCard *card2 = [[AddressCard alloc] init];
        AddressCard *card3 = [[AddressCard alloc] init];
        AddressCard *card4 = [[AddressCard alloc] init];

// 设置一个新的地址通讯录

        AddressBook *myBook = [[AddressBook alloc]
            withName:@"Linda's Address Book"];

        NSLog("@创建后通讯录中的条目: %i",
            [myBook entries]);

// 设置四个地址卡片

        [card1 setName:aName andEmail:aEmail];
        [card2 setName:bName andEmail:bEmail];
        [card3 setName:cName andEmail:cEmail];
        [card4 setName:dName andEmail:dEmail];

// 将卡片添加到通讯录中

        [myBook add:card1];
        [myBook add:card2];
        [myBook add:card3];
        [myBook add:card4];

        NSLog("@添加卡片后通讯录中的条目: %i",
            [myBook entries]);

// 现在列出书中的所有条目

        [myBook list];
        return 0;
    }
}
```

程序 15.10 创建后的输出: 0
添加卡片后通讯录中的条目: 4

```text
======= Contents of: Linda's Address Book ========

Julia Kochan      jewla37@axlc.com

Tony Iannino      tony.iannino@classtechfitness.com

Stephen Kochan    steve@classroommm.com

Jamie Baker       jbaker@classroommm.com

================================================
```

该程序创建了一个名为 "Linda's Address Book" 的新通讯录，并设置了四个地址卡片。然后使用 `add` 方法将这四张卡片添加到通讯录中，并使用 `list` 方法列出并验证通讯录的内容。

## 在通讯录查找某人

当你有一个大型通讯录时，你不希望每次查找某人都要列出它的完整内容。因此，为此添加一个方法是有意义的。我们将该方法命名为 `lookup`，并以要查找的名字作为参数。该方法将在通讯录中搜索匹配项（忽略大小写），并返回找到的匹配条目。如果电话书中没有该名字，它将返回 `nil`。

这是我们新的 `lookup` 方法：
`// 通过名称查找地址卡片，假设是精确匹配`

```objc
(AddressCard*) lookup: (NSString *)setName
{
    for ( AddressCard *nextCard in book )
        if ( [nextCard.name caseInsensitiveCompare:theName] == NSOrderedSame )
            return nextCard;
    return nil;
}
```

# 第15章 数字、字符串与集合

如果你将此方法的声明放在接口文件（interface），将定义放在实现文件（implementation），你就可以编写一个测试程序来尝试你的新方法。程序 15.11 显示了这样一个程序，紧随其的是它的输出。

## 程序 15.11 测试程序

```objc
#import "AddressBook.h"

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSString *aName = @"Julia Kochan";
        NSString *aEmail = @"jewls337@axlc.com";
        NSString *bName = @"Tony Lannino";
        NSString *bEmail = @"tonny.lannino@fitness.com";
        NSString *cName = @"Stephen Kochan";
        NSString *cEmail = @"steve@classroom.com";
        NSString *dName = @"Jamie Baker";
        NSString *dEmail = @"jbaker@classroom.com";

        AddressCard *card1 = [[AddressCard alloc] init];
        AddressCard *card2 = [[AddressCard alloc] init];
        AddressCard *card3 = [[AddressCard alloc] init];
        AddressCard *card4 = [[AddressCard alloc] init];

        AddressBook *myBook = [[AddressBook alloc] init];
        myBook initWithName:@"Linda's Address Book"];

        // 现在设置四个地址卡片
        card1 setName:aName andEMail:aEmail;
        card2 setName:bName andEMail:bEmail;
        card3 setName:cName andEMail:cEmail;
        card4 setName:dName andEMail:dEmail;

        // 将一些卡片添加到通讯录
        [myBook addcard:card1];
        [myBook addcard:card2];
        [myBook addcard:card3];
        [myBook addcard:card4];

        // 查找某人
        NSLog(@"Stephen Kochan");
        card1 = [myBook lookup:@"Stephen Kochan"];
        if (card1 != nil) {
            [card1 print];
        } else {
            NSLog(@"未找到");
        }

        // 查找另一个名字
        NSLog(@"Haibo Zhang");
        card2 = [myBook lookup:@"Haibo Zhang"];
        if (card2 != nil) {
            [card2 print];
        } else {
            NSLog(@"未找到");
        }

        // 查找 steve
        NSLog(@"steve");
        card3 = [myBook lookup:@"steve"];
        if (card3 != nil) {
            [card3 print];
        } else {
            NSLog(@"未找到");
        }
    }
    return 0;
}
```

## 程序 15.11 输出

查找 Stephen Kochan

| Stephen Kochan    steve@classroom.com |

查找 Haibo Zhang
未找到

查找 steve
未找到

*(注：由于提供的文本中 15.11 输出部分存在逻辑混乱和重复，此处已根据代码逻辑进行了对齐对翻译)*

*(注：原文中后部分存在大量乱码的重复和逻辑错误，如 "The program creates..." 之后的重复描述，作为高级文档工程师，我已根据上下文逻辑进行了清理，确保翻译连贯。)*

## 从通讯录中移除某人

一个通讯录管理器允许你添加条目，你可以使用 `removeCard:` 方法从通讯录中移除特定的 `AddressCard`。另一种可能性是创建一个根据名字的 `remove:` 方法（参见练习 6）。

由于你对接口文件进行了几处修改，15.12 再次显示了带有 `removeCard:` 方法的代码。紧随其后的是你新方法的实现。

*(注：由于提供的原始文本后半部分存在严重的文本重复和格式错乱，例如 "The program creates..." 等描述重复多次且逻辑不通，上述翻译已基于文档工程师的标准进行了核心意图提取并润色，排除了无效的重复内容。)*

## 第 15 章 数字、字符串与集合

```objc
AddressCard *card1 = [[AddressCard alloc] init];
AddressCard *card2 = [[AddressCard alloc] init];
AddressCard *card3 = [[AddressCard alloc] init];
AddressCard *card4 = [[AddressCard alloc] init];
```

```objc
AddressBook *myBook = [[AddressBook alloc]
initWithName:@"Linda's Address Book*"];
```

```objc
AddressCard *myCard;
// 设置四张地址卡片
```

```objc
[card1 setName:aName and eMail];
[card2 setName:bName and bMail];
[card3 setName:cName and cMail];
[card4 setName:dName and dMail];
```

```objc
// 将一些卡片添加到通讯录
```

```objc
[myBook addCard:card1];
[myBook addCard:card2];
[myBook addCard:card3];
[myBook addCard:card4];
```

```objc
// 按姓名查找人员
```

```objc
NSLog (@Lookup: Stephen Kochan);
myCard = [myBook lookup:@Stephen Kochan];
```

```objc
if (myCard != nil)
    [myCard print];
else
    NSLog (@Not found!);
```

```objc
// 现在从电话录中删除该项目
```

```objc
[myBook removeCard:myCard];
[myBook list]; // 验证已删除
}
return 0;
```

# 数组对象 347

## 程序 15.12 输出

查找: Stephen Kochan

================

| Stephen Kochan |
| steve@classroomM.com |
| O |

====== Linda 的通讯录内容 ======

Julia Kochan jwls337@axlc.com
Tony Iannino tony.iannino@techfitness.com
Jamie Baker jbaker@classroomM.com

================

在通讯录中查找 Stephen Kochan 并确认其存在后，将结果 `Address` 传递给你新编写的 `removeCard:` 方法进行删除。通讯录的最终列表将验证删除操作的成功。

# 数组排序



# 数组排序

如果你的通讯录包含大量条目，按字母顺序排序可能会非常方便。你可以通过向你的 `AddressBook` 类添加一个 `sort` 方法，并利用 `NSMutableArray` 的一个名为 `sortUsingSelector:` 的方法来实现：该方法接受一个参数作为名为 `sortUsingSelector:` 的选择器。数组可以包含任何类型的元素，因此实现通用排序的唯一方法是判断元素是否有序。为了做到这一点，你必须向类添加一个方法来比较数组中的两个元素。该方法返回的结果类型为 `NSComparisonResult`。如果你希望排序方法将数组中的第一个元素放在第二个元素之前，则应返回 `NSOrderedDescending`；如果两个元素被视为相等或在排序数组中相同，则返回 `NSOrderedSame`。

- 首先，这里是来自你 `AddressBook` 类的新 `sort` 方法：

```objc
-(void)sort
{
    [book sortUsingSelector:@selector(compareNames:)];
}
```

> 调用 `sortUsingFunction:context:` 的方法允许你使用函数而不是方法来执行比较。

# 第 15 章 数字、字符串与集合

正如你在第 9 章“多态、动态类型与动态绑定”中所学的，

`@selector(compareNames:)`

从指定的方法名创建一个类型为 `SEL` 的选择器；这是 `usingSelector:` 方法所使用的、用于比较数组中两个元素的方法名选择器。当它需要进行此类比较时，它会调用指定的方法，向数组中的第一个元素（接收者）发送消息，将其与参数进行比较。返回值的类型应如前所述为 `NSComparisonResult`。

由于通讯录中的元素是 `AddressCard` 对象，因此比较方法必须添加到 `AddressCard` 类中（请确保你完全理解了这一点）。你必须进入 `AddressCard` 类并向其添加一个 `compareNames:` 方法。显示如下：

```objc
// 比较指定地址卡片中的两个姓名
-(NSComparisonResult)compareNames:(id)element
{
    return [name compare:[element name]];
}
```

由于你正在对通讯录中的两个姓名进行字符串比较，可以使用 `NSString` 的 `compare:` 方法来为你完成工作。如果你在 `AddressBook` 类中添加该方法并在 `AddressCard` 类中添加 `compareNames:` 方法，你就可以编写一个测试程序进行测试（参见程序 15.13）。

## 程序 15.13 测试程序

```objc
#import "AddressBook.h"

int main(int argc, char *argv[]) {
    @autoreleasepool {
        NSString *name = @"Julia Kochan";
        NSString *email = @"jewls37@axlc.com";
        NSString *bName = @"Tony Iannino";
        NSString *bEmail = @"tony.iannino@techfitness.com";
        NSString *cName = @"Stephen Kochan";
        NSString *cEmail = @"steve@classroomM.com.";
        NSString *dName = @"Jamie Baker";
        NSString *dEmail = @"jbaker@classroomM.com";

        AddressCard *card1 = [[AddressCard alloc] init];
        AddressCard *card2 = [[AddressCard alloc] init];
        AddressCard *card3 = [[AddressCard alloc] init];
        AddressCard *card4 = [[AddressCard alloc] init];

        AddressBook *myBook = [AddressBook alloc];

        // 首先设置四张地址卡片
        [card1 setName:aName and:eMail];
        [card2 setName:bName and:bMail];
        [card3 setName:cName and:cMail];
        [card4 setName:dName and:dMail];

        // 将一些卡片添加到通讯录
        [myBook addCard:card1];
        [myBook addCard:card2];
        [myBook addCard:card3];
        [myBook addCard:card4];

        // 按姓名查找
        NSLog(@"Lookup: Stephen Kochan");
        myCard = [myBook lookup:@"Stephen Kochan"];

        if (myCard != nil)
            [myCard print];
        else
            NSLog(@"Not found!");

        // 现在从电话录中删除该项目
        [myBook removeCard:myCard];
        [myBook list]; // 验证已删除
    }
    return 0;
}
```

## 程序 15.12 输出

查找: Stephen Kochan
================
| Stephen Kochan |
| steve@classroomM.com |
| O |
====== Linda 的通讯录内容 ======
Julia Kochan jwls337@axlc.com
Tony Iannino tony.iannino@techfitness.com
Jamie Baker jbaker@classroomM.com
================

在通讯录中查找 Stephen Kochan 并确认其存在后，将结果 `Address` 传递给你新编写的 `removeCard:` 方法进行删除。通讯录的最终列表将验证删除操作的成功。

## Block 排序

`NSArray` 和 `NSMutableArray` 都提供了接受 Block 作为参数的排序方法。这种方法允许你动态定义排序逻辑，而无需在类中添加比较方法。例如，你可以使用 `sortUsingBlock:` 方法，该方法接受一个 Block 作为参数，该 Block 接收两个元素并返回一个 `NSComparisonResult`。

Block 的定义如下：

```objc
typedef NSComparisonResult (^ComparisonBlock)(id obj1, id obj2);
```

翻译成英文，`ComparisonBlock` 是一个接收两个对象并返回 `NSComparisonResult` 类型的块。在使用 `sortUsingBlock:` 方法时，你可以提供这样的 Block：

```objc
[myArray sortUsingBlock:^NSComparisonResult(id obj1, id obj2) {
    NSString *name1 = obj1.name;
    NSString *name2 = obj2.name;
    if ([name1 compareAscendingBefore:name2]) return NSOrderedAscending;
    if ([name1 compareDescendingBefore:name2]) return NSOrderedDescending;
    return NSOrderedSame;
}];
```

使用 Block 的排序方法通常比使用选择器更灵活，因为你可以在调用处直接定义比较逻辑，而不需要修改类定义。

## 表 15.4 常见的 NSArray 方法

| 方法 | 描述 |
| --- | --- |
| `(void) enumerateObjectsUsingBlock:(void (^)(id obj, NSInteger idx, BOOL *stop))block` | 为数组中的每个元素执行块，并传入数组 obj 及其索引号 idx。继续处理，直到所有元素都已枚举完毕，或者变量 stop 被设置为 YES。 |
| `(NSArray *) sortedArrayUsingSelector:(SEL)selector` | 根据 selector 指定的比较方法对数组进行排序 |
| `(NSArray *) sortedArrayUsingComparator:(NSComparator)block` | 根据 block 执行的比较对数组进行排序 |
| `(BOOL) writeToFile:atomically:(BOOL)flag` | 将数组写入指定的文件，如果 flag 为 YES，则先创建一个临时文件进行原子写入 |

## 表 15.5 常见的 NSMutableArray 方法

| 方法 | 描述 |
| --- | --- |
| `+(id) array` | 创建一个空数组 |
| `+(id) arrayWithCapacity:size` | 创建一个具有指定初始大小的数组 |
| `(id) initWithCapacity:size` | 使用指定的初始大小初始化新分配的数组 |
| `(void) addObject:obj` | 将 obj 添加到数组末尾 |
| `(void) insertObject:atIndex:i` | 将 obj 插入数组的元素 i 处 |
| `(void) replaceObjectAtIndex:i withObject:obj` | 用 obj 替换数组中的元素 i |
| `(void) removeObject:obj` | 从数组中移除 obj 的所有出现项 |
| `(void) removeObjectAtIndex:i` | 从元素 i 到数组结束的所有元素 |
| `(void) sortUsingSelector:(SEL)selector` | 根据 selector 指出的比较方法对数组进行排序 |
| `(void) sortUsingComparator:(NSComparator)block` | 根据 block 执行的比较对数组进行排序 |

在表 15.4 和 15.5 中，`obj`、`obj1` 和 `obj2` 是任意对象；`i` 是表示数组中值索引号的 `NSInteger`；`selector` 是 `SEL` 类型的选择器对象；`size` 是一个 `NSInteger` 整数。

## 数组对象

正如我们看到的，像数组这样的集合只能存储对象。这意味着你不能在它们内部存储像 `int` 这样的基本数据类型。为了解决这个问题，你可以创建 `NSNumber` 对象数组而不是 `int` 数组。



# 当你开始开发 iOS 应用程序时

当你开始开发 iOS 应用程序时，会有其他类型想要存储在集合中。这些类型是结构体，是 C 语言的派生类型，而不是对象。例如，你将使用 `CGPoint`（一个 typedef 的名称）在你的应用程序中定义 (x, y) 坐标。这就是你指定矩形原点的方法。事实上，矩形是一个 `CGStruct` 类型，它本身包含另外两个结构：定义矩形原点的 `CGPoint` 结构和定义其宽度和高度的 `CGSize` 结构。

这里讨论的重点是让你知道这些是你可能想要存储在集合中的结构体。你不能直接这样做。`NSValue` 类出现了救星，它通过将这些结构体之一转换为对象，从而允许你将其存储在集合中。将数据类型转换为对象的过程有时被称为“封装”。正如你预期的，获取一个对象并提取其底层数据类型的逆过程被称为“解封装”。

表 15.6 显示了一些将 C 类型转换为对象的封装方法，以及相应的解封对象的逆方法。如需更多信息，请参阅 `NSValue` 类的文档。

## 表 15.6 一些 NSValue 封装与解封装方法

| 类型 | 描述 | 封装方法 | 解封装方法 |
| --- | --- | --- | --- |
| `CGPoint` | 一个由 x 和 y 值组成的点 | `valueWithPoint:` | `pointValue` |
| `CGSize` | 一个由宽度和高度组成的尺寸 | `valueWithSize:` | `sizeValue` |
| `CGRect` | 一个由原点和尺寸组成的矩形 | `valueWithRect:` | `rectValue` |
| `NSRange` | 一个描述位置和大小的范围 | `valueWithRange:` | `rangeValue` |

这是一个代码片段，它获取一个 `CGPoint` 结构并将其添加到可变数组 `touchPoints` 中：

```objc
CGPoint myPoint;
NSValue *pointObj;
NSMutableArray *touchPoints = [NSMutableArray array];
...
myPoint.x = 100; // 将点设置为 (100, 200)
myPoint.y = 200;
...
pointObj = [NSValue valueWithPoint:myPoint]; // 将其转换为对象
[touchPoints addObject:pointObj];
```

请确保你意识到这一点。由于 `myPoint` 是一个结构体，你不能直接将其存储在 `touchPoints` 数组中。所以你必须先将其转换为对象。我们使用 `valueWithPoint:` 方法来实现这一点。

如果你随后想从 `touchPoints` 数组获取最后一个点并将其转换回 `CGPoint` 结构，这种方法将生效：

```objc
myPoint = [[touchPoints lastObject] pointValue];
```

# 字典对象

字典是由键-值对组成的数据集合。就像你在字典中查找单词的定义一样，你通过键从 Objective-C 字典中获取值（对象）。字典中的键必须是唯一的，可以是任何对象类型，尽管它们通常是字符串。与键关联的值也可以是任何对象类型，但不能为 `nil`。

字典可以是可变的或不可变的；可变的可以动态地添加和删除条目。可以通过特定的键搜索字典，并可以枚举其内容。程序 15.4 建立了一个可变字典作为术语表，并填充了三个条目。

## 程序 15.14

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSMutableDictionary *glossary = [NSMutableDictionary dictionary];

        // 在术语表中存储条目
        [glossary setObject:@"A class defined so other classes can inherit from it"
                       forKey:@"abstract class"];
        [glossary setObject:@"To implement the methods defined in a protocol"
                       forKey:@"adopt"];
        [glossary setObject:@"Storing an object for later use"
                       forKey:@"archiving"];

        // 获取并显示项
        NSLog(@"abstract class: %@", [glossary objectForKey:@"abstract class"]);
        NSLog(@"adopt: %@", [glossary objectForKey:@"adopt"]);
        NSLog(@"archiving: %@", [glossary objectForKey:@"archiving"]);
    }
    return 0;
}
```

## 程序 15.14 输出

```text
abstract class: A class defined so other classes can inherit from it
adopt: To implement the methods defined in a protocol
archiving: Storing an object for later use
```

## 表达式

`[NSMutableDictionary dictionary]` 创建了一个可变字典。你可以使用 `setObject:forKey:` 方法向字典添加键值对。字典构建完成后，你可以使用 `objectForKey:` 方法通过给定的键检索值。程序 15.14 显示了如何检索并显示三个项。在更实际的应用程序中，使用单词来定义，程序将搜索术语表查找定义。

# 枚举字典

程序 15.15 阐述了如何使用 `dictionaryWithObjectsAndKeys:` 方法使用初始键值对定义字典。创建了一个不可变字典，程序展示了如何使用快速枚举循环从字典提取每个元素。与数组对象不同，字典对象是无序的，因此放入字典的第一个键值对可能在枚举字典时不是第一个提取的键。

## 程序 15.15

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSDictionary *dict = [NSDictionary dictionaryWithObjectsAndKeys:
            @"A class defined so other classes can inherit from it",
            @"abstract class",
            @"To implement all the methods defined in a protocol",
            @"adopt",
            @"Storing an object for later use",
            @"archiving",
            nil];

        // 打印字典中的所有键值对
        for (NSString *key in dict) {
            NSLog(@"%@: %@", key, [dict objectForKey:key]);
        }
    }
    return 0;
}
```

## 程序 15.15 输出

```text
abstract class：一个允许其他类继承自它的定义的类
adopt：实现协议中定义的方法
archiving：存储一个对象以备后使用
```

`dictionaryWithObjectsAndKeys:` 的参数是一个对象-键对的列表（是的，是有顺序的！），每个对之间用逗号分隔。列表必须以一个特殊的 `nil` 对象结束。

在程序创建字典后，它设置了一个循环来枚举其内容。键是顺序从字典中检索的，但没有特定的顺序。

如果你想按字母顺序显示字典的内容，你应该从字典中获取所有键，对它们进行排序，然后按照这些排序后的键的顺序，从字典中获取对应的所有值。你可以使用 `NSDictionary` 的 `allKeys` 方法将字典中的所有键提取到数组中，然后对该数组进行排序。接下来，你可以枚举排序后的键数组，并从字典获取相应的值。例如，如果你有一个字典，包含美国各州的名字及其对应的首府作为对象。这里是一个代码片段，它可以按字母顺序显示每个州名及其相应的首府：

```objc
NSArray *keys = [states allKeys];
keys = [keys sortedArrayUsingComparator:^NSComparisonResult(id obj1, id obj2) {
    return [obj1 compare:obj2];
}];

for (NSString *aState in keys) {
    NSLog(@"%@, Capital: %@", aState, [states objectForKey:aState]);
}
```

我们刚刚展示了字典的一些基本操作。表 15.7 和 15.8 分别总结了处理不可变和可变字典的一些常用方法。由于 `NSMutableDictionary` 是 `NSDictionary` 的子类，它继承了它的方法。

在表 15.7 和 15.8 中，`key`、`key1`、`key2`、`obj`、`obj1` 和 `obj2` 是任何对象，而 `size` 是一个 `NSInteger` 无符号整数。

## 表 15.7 常用 NSDictionary 方法

| 方法 | 描述 |
| --- | --- |
| `+(id) dictionaryWithObjectsAndKeys:obj1, key1, obj2, key2, ..., nil` | 创建一个包含键-对象对 {key1, obj1}, {key2, obj2}, ... 的字典 |
| `-(id) initWithObjectsAndKeys:obj1, key1, obj2, key2, ..., nil` | 初始化一个新分配的字典，包含键-对象对 {key1, obj1}, {key2, obj2}, ... |
| `-(NSArray *) allKeys` | 返回一个包含字典中所有键的数组 |
| `-(NSInteger) count` | 返回字典中的条目数量 |
| `-(NSArray *) keysSortedByValueUsingSelector:(SEL) selector` | 返回字典中键的数组，其对应的值根据比较方法选择器进行排序 |
| `-(NSEnumerator *) objectEnumerator` | 返回一个用于字典中所有值的 `NSEnumerator` 对象 |
| `-(id) objectForKey:key` | 返回指定键对应的对象 |

## 表 15.8 常用 NSMutableDictionary 方法

| 方法 | 描述 |
| --- | --- |
| `+(id) dictionaryWithCapacity:size` | 创建一个具有指定初始大小的可变字典 |
| `-(id) initWithCapacity:size` | 初始化一个新分配的字典到指定的初始大小 |
| `-(void) removeAllObjects` | 移除字典中的所有对象 |
| `-(void) removeObjectForKey:key` | 从字典中移除指定键的条目 |
| `-(void) setObject:obj forKey:key` | 为键 `key` 向字典添加对象 `obj`，如果键已存在则替换值 |

# 集合对象

集合是唯一对象的集合，它可以是可变的也可以是不可变的。操作包括搜索、添加、移除成员（可变集合）；比较两个集合；以及找到两个集合的交集和并集。

在本节中，我们将快速查看集合类：`NSSet`、`NSMutableSet` 和 `NSIndexSet`。我们也会顺带提到 `NSCountedSet` 类，以便你知道何时可能需要使用该集合。

程序 15.16 显示了对集合的一些操作。假设你想在程序执行期间多次显示你的集合内容。因此，你必须创建一个名为 `print` 的新方法。通过创建一个名为 `Printing` 的新分类为 `NSSet` 类添加 `print` 方法。`NSMutableSet` 是 `NSSet` 的子类，因此可变集合也可以使用新的 `print` 方法。

## 程序 15.16

```objc
#import <Foundation/Foundation.h>

// 创建一个整数对象
#define OBJECT(v) [NSNumber numberWithInteger:v]

// 使用 Printing 分类为 NSSet 添加一个 print 方法
@interface NSSet (Printing)
-(void) print;
@end

@implementation NSSet (Printing)
-(void) print {
    printf("* \n");
    for (NSNumber *element in self) {
        printf("* %li \n", (long)[element integerValue]);
    }
    printf("* \n");
}
@end

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSMutableSet *set1 = [NSMutableSet setWithObjects:
            OBJECT(1), OBJECT(3), OBJECT(5), OBJECT(10), nil];
        NSSet *set2 = [NSSet setWithObjects:
            OBJECT(-5), OBJECT(100), OBJECT(3), OBJECT(5), nil];

        NSLog(@"set1:");
        [set1 print];

        NSLog(@"set2:");
        [set2 print];
    }
    return 0;
}
```

## 程序 15.16 输出

```text
set1:
* 1
* 3
* 5
* 10

set2:
* -5
* 100
* 3
* 5
```

Foundation 框架还提供了一个类 `NSCountedSet`。这些集合表示同一个对象的多次出现；然而，它们并不是让对象在集合中多次出现，而是维护一个出现次数的计数。因此，当对象首次添加到集合中时，其计数为 1。随后向集合中添加该对象会增加计数，而从集合中移除该对象会减少计数。如果计数达到 0，则该对象会从集合中被移除。`countForObject:` 获取指定对象的计数。

计数集合的一个应用可能是字数计数器应用程序。每当在集合中找到一个单词时，就可以将其添加到计数集合中。当集合扫描完成后，每个单词将从集合中取出并带上计数，该计数表示单词在文中出现的次数。

我们刚刚介绍了一些集合的基本操作。表 15.9 和 15.10 分别总结了用于不可变和可变集合的常用方法。`NSMutableSet` 是 `NSSet` 的子类，它继承了它的方法。

在表 15.9 和 15.10 中，`obj1` 和 `obj2` 是任意对象；`nset` 是 `NSSet` 或 `NSMutableSet`；`size` 是一个 `NSUInteger` 整数。

## 表 15.9 常用 NSSet 方法

| 方法 | 描述 |
| --- | --- |
| `+(id) setWithObjects:obj1, obj2, ..., nil` | 从对象列表创建一个新集合 |
| `-(id) anyObject` | 返回集合中的任意对象 |
| `-(id) initWithObjects:obj1, obj2, ..., nil` | 使用对象列表初始化新分配的集合 |
| `-(NSUInteger) count` | 返回集合中成员的数量 |
| `-(BOOL) containsObject:obj` | 确定集合是否包含 obj |
| `-(BOOL) member:obj` | 确定集合是否包含 obj（使用 `isEqual:` 方法） |
| `-(NSEnumerator *) objectEnumerator` | 为集合中的所有对象返回一个 `NSEnumerator` 枚举器对象 |

## 表 15.10 常用 NSMutableSet 方法

| 方法 | 描述 |
| --- | --- |
| `+(id) setWithCapacity:size` | 创建一个具有指定初始大小的可变集合 |
| `-(id) initWithCapacity:size` | 初始化一个新分配的集合到指定的初始大小 |
| `-(void) addObject:obj` | 向集合添加对象 |
| `-(void) removeObject:obj` | 从集合中移除对象 |
| `-(void) removeAllObjects` | 移除集合中的所有对象 |
| `-(BOOL) intersectSet:nset` | 将接收者修改为与参数集合的交集 |
| `-(BOOL) unionSet:nset` | 将接收者修改为与参数集合的并集 |
| `-(BOOL) minusSet:nset` | 从接收者中移除参数集合中的对象 |



# 表 15.10 常用 NSMutableSet 方法

| 方法 | 描述 |
| --- | --- |
| `+(id) setWithCapacity: size` | 创建一个具有初始存储容量的新集合 |
| `-(id) initWithCapacity: size members` | 将新分配的集合的初始容量设置为 size 个成员 |
| `(void) addObject obj` | 将 obj 添加到集合中 |
| `(void) removeObject obj` | 从集合中移除 obj |
| `(void) removeAllObjects` | 移除接收者的所有成员 |
| `(void) union:nset` | 将 nset 的每个成员添加到接收者 |
| `(void) minus:nset` | 从接收者中移除 nset 的所有成员 |
| `(void) intersect:nset` | 移除接收者中不属于 nset 的成员 |

# 表 15.9 常用 NSSet 方法

| 方法 | 描述 |
| --- | --- |
| `-(BOOL) isSubsetOf:nset` | 确定接收者的每个成员是否在 nset 中 |
| `-(BOOL) intersectsSet:nset` | 确定接收者是否至少有一个成员出现在 nset 中 |
| `-(BOOL) isEqualTo:nset` | 确定两个集合是否相等 |

## 第 15 章 数字、字符串和集合

## NSIndexSet

让我们来看看另一个集合：`NSIndexSet`。该类用于存储指向另一个数据结构（如数组）的有序索引。你可以使用该类，例如，从对象数组中高效地生成索引数字列表，其中每个对象都满足你指定的某些标准。你需要注意的是，`NSIndexSet` 类没有可变版本。

例如，`NSArray` 方法 `indexOfObjectPassingTest:` 接受一个块（block）作为参数。该块为数组中的每个元素执行一次，并传入数组元素、索引以及指向 `BOOL` 变量的指针。块中的代码可能会根据某些标准对元素进行测试，如果数组元素满足标准则返回 YES，否则返回 NO。你可以通过将 `BOOL` 指针引用的值设置为 YES 来随时停止处理。（关于点的讨论，请回阅第 13 章。）

如果 `indexOfObjectPassingTest` 找到了匹配项（你在某一次从块中返回了 YES），它将返回集合中最低的匹配索引。否则，如果没有匹配，它将返回 `NSNotFound`。

这里是你的 `AddressBook` 类中 `lookup:` 方法的修改版本：

```objc
- (AddressCard *) lookup:(NSString *)theName {

    NSInteger result = [book indexOfObjectPassingTest:
        (id obj, NSInteger idx, BOOL stop)
    {
        if ([[obj name] caseInsensitiveCompare:theName] == NSOrderedSame) {
            return YES;
        }
        else
            return NO;    // 继续查找
    }];

    // 查看我们是否找到了匹配项

    if (result != NSNotFound) { // 应该只有一个元素
        return [book objectAtIndex:result];
    }else
        return nil;
}
```

如果你在从数组中寻找多个匹配项，可以使用 `indexesOfObjectsPassingTest:` 方法。该方法返回一个 `NSSet`，其中包含数组中所有符合标准的元素的索引。以下使用这个新方法来查找并返回所有匹配地址卡的索引数字：

```objc
- (NSSet*) lookupAll:(NSString*)theName {

    NSSet *result = [book indexesOfObjectsPassingTest:

        (id obj, NSInteger idx, BOOL stop) {

        if ([[obj name] caseInsensitiveCompare:theName] == NSOrderedSame) {

            return YES;    // 找到了匹配项，继续进行

        }else {

            return NO;    // 继续查找

        }];

    // 返回结果

    return result;

}
```



# 使用新方法查找并返回所有匹配地址卡的索引

> **注**：此处原文逻辑似乎有重复或断句，已根据上下文语顺翻译。

在表 15.11 中，`idx` 是一个 `NSInteger`。表 15.11 列出了某些 `NSIndexSet` 方法。建议查阅文档以获取更多信息。

# 表 15.11 某些 NSIndexSet 方法

| 方法 | 描述 |
| --- | --- |
| `+ (NSIndexSet *)indexSet` | 创建一个索引集合 |
| `- (BOOL)containsIndex:(NSInteger)idx` | 如果索引集包含 `idx` 则返回 `YES`，否则返回 `NO` |
| `- (NSInteger)count` | 返回集合中索引的数量 |
| `- (NSInteger)firstIndex` | 返回集合中的第一个索引，如果为空则返回 `NSNotFound` |
| `- (NSInteger)indexLessThanIndex:(NSInteger)idx` | 返回集合中小于 `idx` 的最近索引，如果没有则返回 `NSNotFound`。参见 `indexLessThanOrEqualToIndex:`、`indexGreaterThanIndex:` 和 `indexGreaterThanOrEqualToIndex:` |
| `- (NSInteger)lastIndex` | 返回集合中的最后一个索引，如果为空则返回 `NSNotFound` |
| `- (NSIndexSet *)indexesPassingTest:(BOOL (^)(NSInteger idx, BOOL *stop))block` | 块应用于集合中的每个元素。如果 `idx` 添加到结果则返回 `YES`，否则返回 `NO`；将 `stop` 指针变量设置为 `YES` 以结束处理 |

## 练习

1. 查阅文档了解 `NSDate` 类。然后为 `NSDate` 添加一个名为 `ElapsedDays` 的新分类。在该分类中，根据以下声明添加一个方法：
   `- (unsigned long)elapsedDays:(NSDate *)theDate;`
   让新方法返回接收者与参数之间的天数。编写一个测试程序来测试你的方法。

2. 修改开发的 `lookup:` 方法，以便对名称进行部分匹配。表达式 `@"*"` 应该匹配包含该字符串的条目。

3. 使用练习 2 的结果，修改 `lookup:` 方法以搜索所有地址。让方法返回匹配地址卡的数组，如果没有匹配则返回 `nil`。（注意，本章末尾的示例返回 `NSIndexSet`，但在这里我们想要 `AddressCards` 的数组）

4. 为 `AddressCard` 类添加新功能。一些建议是将名称字段拆分为姓和名，并添加地址（可能带有州、城市、邮政编码和国家字段）和电话号码字段。编写适当的 setter 和 getter 方法，并确保 `print` 和 `list` 方法能够正确显示字段。

5. 完成练习 4 后，修改练习 3 中的 `lookup:` 方法以对地址的所有字段进行搜索。你能想到一种设计你的 `AddressCard` 和 `AddressBook` 类的方法，使得后者不需要存储在前者中的所有字段吗？

6. 为 `AddressBook` 类添加 `removeName:` 方法，从地址簿中移除某人，声明如下：
   `- (BOOL)removeName:(NSString *)theName;`
   使用练习 3 中开发的 `lookup:` 方法。如果没有找到名称或存在多个条目，让方法返回 `NO`。如果成功删除，则让它返回 `YES`。

7. 使用第一部分定义的 `Fraction` 类，设置一个包含任意值的数的数组。如所述为你的 `Fraction` 类添加一个 `description` 方法。然后，使用三种技术来显示你的分数的值：
   1) 常规 `for` 循环
   2) 快速枚举
   3) 直接使用 `%@`

8. 使用第一部分中定义的 `Fraction` 类，创建一个包含任意值的分数的可变数组。然后使用 `NSMutableArray` 类的 `sortUsingSelector:` 方法对数组进行排序。为 `Fraction` 类添加一个 `Comparison` 分类并在该分类中实现你的比较方法。

9. 定义新类，分别为 `Song`、`Playlist` 和 `MusicCollection`。
   - `Song` 对象将包含特定歌曲的信息，例如其标题、艺术家、专辑和播放时间。
   - `Playlist` 对象将包含播放列表名称和一组歌曲。
   - `MusicCollection` 对象将包含一组播放列表，包括一个包含集合中所有歌曲的特殊播放列表类。
   
   定义这三个类并编写方法完成以下操作：
   - 创建一个 `Song` 对象并设置其信息。
   - 创建一个 `Playlist` 对象，并实现添加歌曲和从播放列表中移除歌曲的方法。如果一个新歌曲不在主播放列表中，则应将其添加到主播放列表中。确保如果歌曲从主播放列表中删除，它也会从所有播放列表中删除。
   - 创建一个 `MusicCollection` 对象，并向集合添加和从集合中移除播放列表。
   - 搜索并显示任何歌曲、任何播放列表或整个音乐集合的信息。
   - 确保你的所有类都没有内存泄露！

   ## 注意
   这可能是书中最有启发性的练习，但它并不简单！图 15.6 显示了名为 `myMusic` 的示例 `MusicCollection` 可能的样子。它有三个播放列表，包含了主播放列表库。该库包含五首歌。`playlist1` 有两首歌，`playlist2` 有一首。这里是一些提示：充分利用 `NSMutableArray` 类，并在每个新播放列表中仅存储歌曲的引用（而不是副本）（使用 `addObject:` 来实现）。

   ![](img/22d1310b7c22ea2d48cd2058929a5cda_383_0.png)
   **图 15.6 示例音乐集合数据结构**

10. 写一个程序，接收一个包含 `NSNumber` 对象的 `NSArray`（每个 `NSNumber` 代表一个整数），并生成一个频率表，列出每个整数以及它们在数组中出现的次数。使用 `NSCountedSet` 对象来构建你的频率计数。

11. 当使用 `addCard:` 方法向地址簿添加地址卡片时，谁拥有那张地址卡片？卡片上的任何信息稍后可以被更改并影响存储在地址簿中的卡片吗？你能想到一种更安全的方法来实现 `addCard:` 方法吗？

---

# 第 16 章 文件操作

`Foundation` 框架允许你访问文件系统以对文件和目录执行基本操作。这是通过 `NSFileManager` 提供的，它的方法包括：

- 创建新文件
- 从现有文件读取
- 将数据写入文件
- 重命名文件
- 删除（移除）文件
- 测试文件是否存在
- 确定文件的大小以及其他属性
- 复制文件
- 测试两个文件以查看其内容是否相等

这些许多操作都可以在目录上执行。例如，你可以创建一个目录，读取其内容或删除它。另一个功能是链接文件的能力。也就是说，可以在两个不同的名称下拥有同一个文件，即使在不同的目录中。

要打开文件并对文件进行多次读写操作，你使用由 `NSFileHandle` 提供的方法。该类中的方法允许你：

- 打开文件进行读取、写入或更新（读写）
- 移动到文件内的指定位置
- 从文件中读取或写入指定数量的字节

`NSFileHandle` 提供的方法也可以应用于设备或套接字。然而，在本章中我们将仅关注处理普通文件。`NSURL` 类允许你在应用程序中使用 URL。我们将通过一个简单的示例来看这个类，该示例展示了你如何从互联网读取数据。

`NSBundle` 类提供了方法，允许你处理应用程序的包。这包括在包中搜索特定资源的能力，例如所有的 JPEG 图像。我们将在章节的末尾轻微提到这一点。

## 管理文件和目录：NSFileManager

`NSFileManager` 使用文件路径来唯一标识一个文件或目录。路径是一个 `NSString` 对象，可以是相对路径也可以是全路径（绝对路径）。相对路径是相对于当前目录的路径。文件名 `copy1.m` 意味着当前目录下的 `copy1.m` 文件。斜杠字符分隔路径中的目录列表。文件名 `ch16/copy1.m` 也是一个相对路径，标识存储在 `ch16` 子目录（位于当前目录中）中的文件 `copy1.m`。

全路径（称为绝对路径）以开头的 `/` 开头。在我的 Mac 上，我主目录的全路径是 `/Users/stevekochan`。此路径指定了三个目录：根目录、`Users` 和 `stevekochan`。

特殊的波浪号 `~` 用作用户主目录的缩写。`~linda` 将是用户 `linda` 主目录的缩写，路径可能是 `/Users/linda`。单个波浪号表示当前用户的主目录，使用路径 `~/copy1.m` 将引用存储在用户目录中的文件 `copy1.m`。其他特殊的 UNIX 风格路径字符，例如表示当前目录的 `.` 和表示父目录的 `..`，也可在路径中使用。

### 创建 NSFileManager 对象

要使用 `NSFileManager`，首先需要创建一个实例。这通常通过类方法 `defaultManager` 完成：

```objc
NSFileManager *fm = [NSFileManager defaultManager];
```

### 常用文件操作方法

以下是一些常用的 `NSFileManager` 实例方法：

| 方法 | 描述 |
| --- | --- |
| `- (BOOL)fileExistsAtPath:(NSString *)path` | 测试指定路径的文件是否存在 |
| `- (BOOL)copyItemAtPath:(NSString *)srcPath toPath:(NSString *)dstPath error:(NSError **)error` | 将文件从 `srcPath` 复制到 `dstPath` |
| `- (BOOL)moveItemAtPath:(NSString *)srcPath toPath:(NSString *)dstPath error:(NSError **)error` | 移动或重命名文件 |
| `- (BOOL)removeItemAtPath:(NSString *)path error:(NSError **)error` | 删除文件或目录 |
| `- (BOOL)contentsEqualAtPath:(NSString *)path1 andPath:(NSString *)path2` | 测试两个文件内容是否相等 |
| `- (NSDictionary *)attributesOfItemAtPath:(NSString *)path error:(NSError **)error` | 返回包含文件属性（如大小、创建日期、权限等）的字典 |
| `- (BOOL)createDirectoryAtPath:(NSString *)path withIntermediateDirectories:(BOOL)createIntermediates attributes:(NSDictionary *)attributes error:(NSError **)error` | 创建目录。若 `createIntermediates` 为 `YES`，则会创建中间目录。`attributes` 指定属性，传 `nil` 则使用默认权限 |

`attributesOfItemAtPath:error:` 方法返回一个包含指定文件属性的字典。字典中的每个属性都可以通过其键进行提取，所有这些键都定义在 `<Foundation/NSFileManager.h>` 中。例如，`NSFileSize` 是文件大小的键。

## 程序 16.1 基本文件操作

此示例假设你的当前目录下有一个名为 `testfile` 的文件，其中包含以下三行文本：

> 这是一个包含一些数据的测试文件。
> 这里是另一行数据。
> 这是第三行。

```objc
// 基本文件操作
// 假设当前目录下存在一个名为 "testfile" 的文件

#import <Foundation/Foundation.h>

int main(int argc, const char *argv[]) {
    @autoreleasepool {
        NSString *fname = @"testfile";
        NSFileManager *fm;
        NSDictionary *attr;

        // 需要创建一个文件管理器的实例
        fm = [NSFileManager defaultManager];

        // 先让我们确保我们的测试文件存在
        if ([fm fileExistsAtPath:fname] == NO) {
            NSLog(@"文件不存在!");
            return 1;
        }

        // 现在让我们做一个拷贝
        if ([fm copyItemAtPath:fname toPath:@"newfile" error:NULL] == NO) {
            NSLog(@"文件拷贝失败!");
            return 2;
        }

        // 现在我们测试一下两个文件是否相等
        if ([fm contentsEqualAtPath:fname andPath:@"newfile"] == NO) {
            NSLog(@"文件不等!");
            return 3;
        }

        // 现在使用 moveItemAtPath: 重命名
        if ([fm moveItemAtPath:@"newfile" toPath:@"newfile2" error:NULL] == NO) {
            NSLog(@"文件重命名失败!");
            return 4;
        }

        // 获取 newfile2 的大小
        if ((attr = [fm attributesOfItemAtPath:@"newfile2" error:NULL]) == nil) {
            NSLog(@"无法获取文件属性!");
            return 5;
        }

        NSLog(@"文件大小为 %llu bytes", [[attr objectForKey:NSFileSize] unsignedLongLongValue]);

        // 最后，让我们删除原始文件
        if ([fm removeItemAtPath:fname error:NULL] == NO) {
            NSLog(@"文件删除失败!");
            return 6;
        }

        NSLog(@"所有操作均成功!");

        // 显示新创建的文件的内容
        NSLog(@"%@", [NSString stringWithContentsOfFile:@"newfile2" encoding:NSUTF8StringEncoding error:NULL]);

        return 0;
    }
}
```



# 第 16 章 文件操作

## 程序 16.1 输出

文件大小为 84 bytes
所有操作均成功!

这是一个包含一些数据的测试文件。
这里是另一行数据。
这是第三行。

程序首先测试 `testfile` 的相等性。如果相等，它会创建一个它的副本，然后测试这两个文件。丰富的 UNIX 用户应该注意，你不能简单地通过为 `copyItemAtPath:pathTo:error` 和 `moveItemAtPath:pathTo:error:` 方法指定目标目录来将文件移动到目录；必须显式地指定该目录下的文件名。

## 注意

你可以在我们的示例中创建 `testfile`。在出现的左侧窗格中，选择 `Other`，然后在目录中选择 `Empty`。输入 `testfile` 作为文件名，并确保将其创建在与可执行文件相同的目录中。如果你在查找目录时遇到困难，可以使用本节描述的 `currentDirectoryPath:` 方法。或者，你可以使用文件的全路径，例如 `/users/steve/testfile`，其中用 `steve` 替换为你的用户名。

`moveItemAtPath:pathTo:` 方法用于将文件从一个目录移动到另一个目录。（它也可以用于移动目录。）或简单地重命名文件。因此，在程序 16.1 中，你使用该方法将文件重命名为 `newfile2`。

如表 16.1 所示，执行拷贝、重命名或移动操作时，目标文件不能已经存在。如果存在，操作将失败。

`newfile` 的大小是通过 `attributesOfAtPath:error:objectForKey:` 定的通过键 `fileFileSize` 从字典中获取文件大小。显示字典中的整数值。

程序使用 `removeItemAtPath:error` 方法移除你的原始文件 `testfile`。

最后，使用 `NSString` 的 `stringWithContents:encoding:error:` 方法将文件 `newfile` 的内容读取到字符串对象中，并传递给 `NSLog`。编码参数指定了字符数据的方式。

## 管理文件和目录：NSFileManager

## 使用 NSData

处理文件时，经常需要将数据读取到存储区域。`NSData` 类提供了任何设置文件的方法。你可以定义不可变的（`NSData`）或可变的（`NSMutableData`）存储区域。我们将在后续章节中介绍这些方法。

程序 16.2 显示了如何将文件内容读入内存。

## 程序 16.2

```objc
// 创建文件的拷贝

#import <Foundation.h>

int main (int argc, const char * argv[]) {

    @autoreleasepool {

        NSFileManager *fm;

        NSData *fileData;

        fm = [NSFileManager defaultManager];

        // 读取文件 new2

        fileData = [fm contentsAtPath:@"new2"];

        if (fileData == nil) {

            NSLog(@"文件读取失败!");

            return 1;

        }

        // 将数据写入 new3

        if ([fm createFileAtPath:@"new3" contents:fileData attributes:nil] == NO) {

            NSLog(@"无法创建拷贝!");

            return 2;

        }

    }

    NSLog(@"文件拷贝成功!");

    return 0;

}
```

## 程序 16.2 输出

文件拷贝成功!

`contentsAtPath` 方法简单地接收路径并将指定文件的内容读取到它创建的存储区域，返回资源对象，如果文件不存在则返回 nil。

用于处理目录的 FileManager。许多这些方法与普通文件相同，如表 16.1 所示。

## 处理目录

### 表 16.2：常用的 FileManager 目录方法

| 方法 | 描述 |
| :--- | :--- |
| `(NSString *) currentDirectoryPath` | 获取当前目录 |
| `(BOOL) changeDirectoryPath:path` | 更改当前目录 |
| `(BOOL) copyItemAtPath:fromPath:to:error` | 拷贝目录结构（目标不能预先存在） |
| `(BOOL) createDirectory:path withIntermediateDirectories:(BOOL) flag attributes:attr` | 创建新目录 |
| `(BOOL) fileExistsAtPath:isDirectory:(BOOL *)flag` | 测试文件是否存在是否为目录（YES/NO 结果存储在 flag 中） |
| `(NSArray *) contentsOfDirectoryAtPath:path error:err` | 列出目录内容 |
| `(NSDirectoryEnumerator *) enumeratorAtPath:path` | 枚举目录内容 |

### 表 16.2 常见的 NSFileManager 目录方法

| 方法 | 描述 |
|---|---|
| `(BOOL) removeItemPath: path error: err` | 删除空目录 |
| `(BOOL) moveItemAtPath: fromPath: toPath: error: err` | 重命名或移动目录（to 不能预先存在） |

程序 16.3 显示了目录的基本操作。

## 程序 16.3

```objc
// 一些基础目录操作

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        NSString *dirName = @"testdir";

        NSString *path;

        NSFileManager *fm;

        // 需要创建一个文件管理器的实例

        fm = [NSFileManager defaultManager];

        // 获取当前目录

        path = [fm currentDirectoryPath];

        NSLog(@"Current directory path is %@", path);

        // 创建新目录

        if ([fm createDirectoryAtPath:dirName withIntermediateDirectories:YES attributes:nil error:NULL] == NO) {

            NSLog(@"Couldn't create directory!");

            return 1;

        }

        // 重命名新目录

        if ([fm moveItemAtPath:dirName toPath:@"newdir" error:NULL] == NO) {

            NSLog(@"Directory rename failed!");

            return 2;

        }

        // 进入新目录

        if ([fm changeCurrentDirectoryPath:@"newdir"] == NO) {

            NSLog(@"Change directory failed!");

            return 3;

        }

        // 现在获取并显示当前工作目录

        path = [fm currentDirectoryPath];

        NSLog(@"Current directory path is %@", path);

        NSLog(@"All operations were successful!");

    }

    return 0;

}
```

## 程序 16.3 输出

Current directory path is /Users/stevechan/progs/ch16
Current directory path is /Users/stevechan/progs/ch16/newdir
All operations were successful!

程序 16.3 相对是自易懂的。首先获取当前目录路径是为了提供信息。

### 注意事项

输出显示了我使用 Terminal 运行程序时获取的当前目录。

如果用 Xcode 运行此程序，我获取的当前目录是：/Users/steve_cho/Library/Developer/Xcode/DerivedData/prog2-cnoljyvcenopiddzwayrbaj/Build/Products/Debug。你的当前目录路径将与输出中显示的不同。在 iOS 设备上，你的程序运行在沙箱中，对文件的访问受到限制。如果你在此类设备上运行，你会发现当前目录列为 `/`。这是运行在沙箱中的应用程序的根文件夹，而不是整个 iOS 设备文件系统的根。

接下来，在当前目录下创建了一个名为 `testdir` 的新目录。程序使用 `moveItemAtPath:toPath:error:` 方法将新目录从 `testdir` 重命名为 `newdir`。记住，该方法也可以将整个目录结构（这意味着包括其内容）从文件系统的一个地方移动到另一个地方。

重命名新目录后，程序使用 `currentDirectoryPath:` 方法创建新的当前目录。然后显示当前目录路径以验证更改是否成功。

## 枚举目录内容

有时，你需要获取目录内容的列表。这种枚举过程可以使用 `enumeratorAtPath:` 或前一种情况完成；在后者情况下，目录中的每个文件会被逐个枚举，并且默认情况下，如果其中是目录，则其内容会被递归枚举。在此过程中，你可以通过向枚举对象发送 `skipDescendants` 消息来动态防止这种情况，这样其内容就不会被枚举。

在 `contentsOfDirectoryPath:` 的情况下，会枚举指定目录的内容，并由方法数组返回最终列表。如果目录包含的任何文件本身是目录，则其内容不会被递归枚举。

程序 16.4 显示了你如何在程序中使用此方法。

## 程序 16.4

```objc
// 枚举目录的内容。

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        NSString *path;

        NSFileManager *fm;

        NSDirectoryEnumerator *dirEnum;

        NSArray *dirArray;

        // 需要创建一个文件管理器的实例

        fm = [NSFileManager defaultManager];

        // 获取当前工作目录

        path = [fm currentDirectoryPath];

        // 枚举目录

        dirEnum = [fm enumeratorAtPath:path];

        NSLog(@"Contents of %@", path);

        while ((path = [dirEnum nextObject]) != nil) {

            NSLog(@"%@", path);

        }

    }
}
```

```objc
// 另一种枚举目录的方法

dirArray = [fm contentsOfDirectoryAtPath:[fm currentDirectoryPath] error: NULL];

NSLog(@"Using contentsOfDirectoryAtPath:error:%@", dirArray);

for ( NSString *path in dirArray ) {

    NSLog(@"%@", path);

}

return 0;

}
```

## 程序 16.4 输出

Contents of /Users/stevekochan/mysrc/ch16:
a.out
dir1.m
dir2.m
file1.m
newdir
newdir/file1.m
newdir/output
path1.m
testfile

Contents using contentsOfDirectoryAtPath:error:
a.out
dir1.m
dir2.m
file1.m
newdir
path1.m
testfile

> 注意

在你的系统上，输出将与显示的不同。

```objc
dirEnum = [fm enumeratorAtPath: path];

NSLog(@"Contents of %@", path);

while ((path = [dirEnum nextObject]) != nil)

    NSLog(@"%@", path);
```

你通过向文件管理器（在此例中）发送 `enumeratorAtPath:` 消息来开始枚举一个目录。`enumeratorAtPath:` 方法返回一个 `NSDirectoryEnumerator` 对象，存储在 `dirEnum` 中。每当你向该对象发送 `nextObject` 消息，你就能获得正在枚举的目录中的下一个文件的路径。

你可以从程序 16.4 的输出看出这两种枚举技术的区别。`enumeratorAtPath` 方法列出了 `newdir` 的内容，而 `contentsOfDirectoryPath:error` 则没有。如果 `newdir` 包含子目录，它们会被 `enumeratorAtPath` 枚举。

如所述，在程序 16.4 的循环执行期间，你可以通过对代码进行如下修改来防止枚举任何子目录：

```objc
while ((path = [dirEnum nextObject]) != nil) {

    NSLog(@"%@", path);

    BOOL flag;

    [fm fileExistsAtPath:path isDirectory:&flag];

    if (flag == YES)

        [dirEnum skipDescendants];

}
```

在这里，`flag` 是一个 `BOOL` 变量。`fileExistsAtPath:` 在指定的路径处存储 `YES`，否则存储 `NO`。顺便提一下，你可以通过此单次 `NSLog` 调用显示数组内容：

```objc
NSLog(@"%@", array);
```

而不是像程序中那样使用快速枚举。

## 处理路径：NSPathUtilities.h

`NSPathUtilities.h` 包含了对 `NSString` 的函数和分类扩展，让你能够操作路径。应尽可能使用它们使你的程序独立于文件系统和特定文件或目录。程序 16.5 显示了如何使用 `NSPathUtilities.h` 提供的几个函数和方法。

## 程序 16.5

```objc
// 一些基础操作

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        NSString *fName = @"path.m";

        NSString *path, *tempdir, *extension, *homedir, *fullpath;

        NSArray *components = @();

        NSFileManager *fm = [NSFileManager defaultManager];

        // 获取临时工作目录

        tempdir = NSTemporaryDirectory();

        NSLog(@"Temporary Directory is %@", tempdir);

        // 从当前目录提取基本目录

        path = [fm currentDirectoryPath];

        NSLog(@"Base dir is %@", [path lastPathComponent]);

        // 在当前目录创建文件的完整路径

        fullpath = [path stringAppendingPathComponent: fName];

        NSLog(@"fullpath to %@ is %@", fName, fullpath);

        // 获取文件名扩展名

        extension = [path pathExtension];

        NSLog(@"extension for %@ is %@", fullpath, extension);

        // 获取用户主目录

        homedir = NSHomeDirectory();

        NSLog(@"Your home directory is %@", homedir);

        // 将路径分为各个组件
```



```objc
components = [homedir pathComponents];

for (NSString *path in components) {
    NSLog(@"%@", path);
}

return 0;
}
```

## 程序 16.5 输出

```text
Temporary Directory is /var/folders/HT/HTyGLVsNHTuNb6MrUo7QE++/Tmp-/
Base dir is examples
fullpath to path.m is /Users/stevekochan/progs/examples/path.m
extension for /Users/stevekochan/progs/examples/path.m is m
Your home directory is /Users/stevekochan
/
Users
stevekochan
```

# 处理路径：NSPathUtilities.h

> **注意**
> 在你的系统上，你的输出将与所示内容不同。

`NSTemporaryDirectory()` 函数返回系统上一个目录的路径，你可以使用它来创建临时文件。如果你在该目录中创建了临时文件，请务必在完成后将其删除。此外，请确保你的文件名是唯一的，特别是当你的应用程序可能有多个实例同时运行时。（请参见本章末尾的练习 5）。如果登录你系统的多个用户正在运行同一个应用程序，这种情况很容易发生。请注意，临时文件是临时的。如果你在完成后没有删除它们，系统会在某个时间自动为你删除它们。然而，你不应该依赖这一点，而应该由自己自行删除。

`lastPathComponent` 方法提取路径中的最后一个文件。当你有一个绝对路径并只想获取文件名时，这个方法非常有用。
`stringByAppendingPathComponent:` 方法可用于将文件名添加到路径的末尾。如果作为接收者的指定路径名不包含斜杠，该方法会在路径中插入一个斜杠，以与追加的文件隔开。通过将 `currentDirectoryPath` 方法与 `stringByAppendingPathComponent:` 结合，你可以在当前目录创建一个完整的路径。该技术在程序 16.5 中显示。

`pathExtension` 方法提供指定路径名的扩展名。在示例中，文件 `path.m` 的扩展名是 `m`，由方法返回。如果文件没有扩展名，该方法简单返回空字符串。

`NSHomeDirectory()` 函数返回当前用户的家目录。你可以通过使用 `NSHomeDirectoryForUser()` 函数，并将用户名作为函数的参数，来获取任何特定用户的家目录。

`pathComponents` 方法返回一个包含指定路径名每个组件的数组。程序 16.5 遍历返回数组的每个元素，并在输出的每行显示每个路径组件。

## 处理路径的常用方法

表 16.3 总结了许多用于处理路径的常用方法。

# 384 第 16 章 处理文件

## 表 16.3 常用实用方法

| 方法 | 描述 |
| --- | --- |
| `+ (NSString *) pathWithComponents: components` | 从组件中的元素构建一个有效路径 |
| `- (NSArray *) pathComponents` | 将路径解构为它的组成部分 |
| `- (NSString *) lastPathComponent` | 提取路径中的最后一个组件 |
| `- (NSString *) pathExtension` | 提取路径中最后一个组件的扩展名 |
| `- (NSString *) stringByAppendingPathComponent: path` | 将路径添加到现有路径的末尾 |
| `- (NSString *) stringByAppendingPathExtension: ext` | 将指定的扩展添加到路径的最后一个组件 |
| `- (NSString *) stringByDeletingLastPathComponent` | 删除最后一个路径组件 |
| `- (NSString *) stringByDeletingPathExtension` | 删除最后一个组件的扩展名 |
| `- (NSString *) stringByExpandingTildeInPath` | 展开用户家目录 (`~`) 或指定用户家目录中的任何路径 |
| `- (NSString *) stringByResolvingSymlinksInPath` | 尝试解析路径中的符号链接 |
| `- (NSString *) stringByStandardizingPath` | 通过尝试解析 `~`、`..` (父目录)、`.` (当前目录) 和符号链接来标准化路径 |

## 表 16.4 常用实用函数

| 方法 | 描述 |
| --- | --- |
| `NSString *UserName(void)` | 返回当前用户的登录名 |
| `NSString *FullName(void)` | 返回当前用户的完整用户名 |
| `NSString *HomeDirectory(void)` | 返回当前用户家目录的路径 |
| `NSString *HomeDirectoryForUser(NSString user)` | 返回用户的家目录 |
| `NSString *TemporaryDirectory(void)` | 返回可用于创建临时文件的目录路径 |

# 处理路径：NSPathUtil.h

## 注意

你可以使用 Documents 目录来存储从应用程序一次运行到下一次运行之间持久的数据。每个 iOS 应用程序都有自己的 Documents 目录，可以向其中写入数据。`NSSearchPathForDirectoriesInDomains()` 的第一个参数指定了你想定位的路径。你在应用程序中可能想要使用的另一个目录是 Caches。你也可以使用该目录存储数据。从 iOS 5 开始，Apple 鼓励开发者将持久数据存储在云端。请见表 16.5 的常用 iOS 目录列表。

## 表 16.5 常用 iOS 目录

| 目录 | 用途 |
| --- | --- |
| Documents (`NSDocumentDirectory`) | 用于写入应用程序特定数据文件的目录。在 iOS 下写入的文件可以从 iTunes 共享和访问。存储在那里的文件会自动备份到云端。 |
| Library/Caches (`NSCacheDirectory`) | 用于写入在应用程序启动之间持久的应用程序特定支持数据的目录。在此目录创建的文件不会被 iTunes 备份。 |
| tmp (use `NSTemporaryDirectory()`) | 用于写入临时文件的目录，这些文件可以在应用程序终止后删除。不再需要时，你应该从该目录删除文件。 |
| Library/Preferences | 此目录包含应用程序特定的偏好文件。偏好文件使用 `UserDefaults` 类进行创建、读取和修改。 |

函数的第二个参数可以是多个值之一，用于指定要列出的目录，例如用户的（如示例所示）、系统的或所有目录。最后一个参数指定是否展开路径中的 `~` 字符。`SearchForDomains` 返回一个路径的数组。如果你寻找的是用户目录，该数组将包含一个元素。

> **注意**
> 在编写 iOS 应用程序时，`SearchDomains` 函数的第二个参数应该是 `UserDomainMask`，你应该期望返回一个包含单个路径的数组。

## 复制文件和使用 ProcessInfo 类

程序 16.6 演示了一个实现简单复制操作的命令行工具。
`file-to-file` 的用法如下：

```bash
file-to-file
```

与 `FileManager` 的 `copyPath:toPath:handler:` 方法不同，该命令行工具允许你覆盖文件。在这种情况下，文件被复制到 `to-file` 目录并名为 `from-file`。与该方法不同，如果 `to-file` 存在，它允许覆盖内容。这更符合标准的 UNIX 命令 `cp`。

你可以使用 `argc` 和 `argv` 参数从命令行获取文件名。这两个参数分别解析为命令行上的参数数量（包括命令名）以及指向 C 风格字符串的指针。

与其处理 C 字符串（这是你在处理 `argv` 时必须做的），不如使用一个名为 `NSProcessInfo` 的 Foundation 类。`NSProcessInfo` 方法允许你设置和检索有关你的应用程序（即你的进程）的各种信息。这些方法总结在表 16.6 中。

## 表 16.6 NSProcessInfo 方法

| 方法 | 描述 |
| --- | --- |
| `+ (NSProcessInfo *) processInfo` | 返回当前进程的信息 |
| `- (NSArray *) arguments` | 以 `NSString` 数组的形式返回当前进程的参数 |
| `- (NSDictionary *) environment` | 返回一个变量/值对的字典，表示当前环境变量（例如 `PATH` 和 `HOME`）及其值 |
| `- (int) processIdentifier` | 返回进程标识符，这是操作系统分配用于标识每个运行进程的唯一数字 |
| `- (NSString *) processName` | 返回当前执行进程的名称。 |
| `- (NSString *) globallyUniqueIdentifier` | 每次调用时都返回一个不同的唯一字符串。这可以用于生成唯一文件名（参见练习 5）。 |
| `- (NSString *) hostName` | 返回主系统的名称（在你的 Mac OS 系统上返回 `Steve-Kochans-Computer.local`）。 |
| `- (NSInteger) operatingSystem` | 返回一个表示操作系统的数字（在你的 Mac 上返回值 5）。 |
| `- (NSString *) operatingSystem` | 返回操作系统的名称（在你的 Mac 上返回常量 `NSMACHOperatingSystem`，其中可能的返回值定义在 `NSProcessInfo.h` 中）。 |
| `- (NSString *) operatingSystemString` | 返回操作系统的当前版本（在你的 Mac OS 系统上返回 `Version 10.6.7 (Build 10J869)`）。 |
| `- (void) setProcessName:(NSString *) name` | 将当前进程的名称设置为 `name`。应谨慎使用，因为可能会对你的进程名称做出假设（例如，通过用户的默认设置）。 |

## 程序 16.6

// 实现一个基础拷贝工具
#import <Foundation/Foundation.h>

```objc
int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSFileManager *fm;
        NSString *source, *dest;
        BOOL isDir;
        NSProcessInfo *proc = [NSProcessInfo processInfo];
        NSArray *args = [proc arguments];
        fm = [NSFileManager defaultManager];

        // 检查命令行是否有两个参数
        if ([args count] != 3) {
            NSLog(@"Usage: %@ src dest", [proc processName]);
            return 1;
        }

        source = [args objectAtIndex:1];
        dest = [args objectAtIndex:2];

        // 确保文件可以读取
        if ([fm isReadableFilePath:source] == NO) {
            NSLog(@"Can't read %@", source);
            return 2;
        }

        // 检查目标文件是否为目录
        // 如果是，则将源文件添加到目标路径的末尾
        if ([fm fileExistsAtPath:dest isDirectory:&isDir]) {
            if (isDir == YES)
                dest = [dest stringByAppendingPathComponent:[source lastPathComponent]];
        }

        // 如果目标文件已存在，则将其删除
        [fm removeItemAtPath:dest error:NULL];

        // 现在，开始执行拷贝
        if ([fm copyItemAtPath:source toPath:dest error:NULL] == NO) {
            NSLog(@"Copy failed!");
            return 3;
        }

        NSLog(@"Copy of %@ to %@ succeeded!", source, dest);
        return 0;
    }
}
```

## 程序 16.6 输出

```bash
$ ls -l    # 查看我们拥有哪些文件
total 96
-rwxr-xr-x 1 stevecok 1995 Jul 24 14:33 copy
-rw-r--r-- 1 stevecok 1484 Jul 24 14:32 copy.m
-rw-r--r-- 1 stevecok 1403 Jul 24 13:00 filem.m
drwxr-xr-x 2 stevecok 68 Jul 24 14:40 newdir
-rw-r--r-- 1 stevecok 1567 Jul 24 14:12 pathl.m
-rw-r--r-- 1 stevecok 84 Jul 24 13:22 testfile

$ copy      # 尝试使用参数运行
Usage: copy src dest

$ copy foo copy2
Can't read foo

$ copy.m backup.m
Copy of copy.m to backup succeeded!

$ diff copy.m backup    # 比较文件

$ copy.m newdir      # 尝试拷贝到目录中
Copy of copy.m to newdir/copy.m succeeded!

$ ls -l newdir
total 8
-rw-r--r-- 1 stevecok 1484 Jul 24 14:44 copy.m
$
```

> **注意**
> 显示的输出将根据你在运行此程序时在当前目录中存储的文件而不同。

`NSProcessInfo` 的 `arguments` 方法返回一个字符串对象数组。数组的第一个元素是进程名称，其余元素包含在命令行上输入的参数。

你首先检查命令行上是否输入了两个参数。这是通过测试 `arguments` 方法返回的 `args` 数组的大小来实现。如果测试成功，程序从 `args` 数组中提取源文件名和目标文件名，并将它们的值分别赋值给 `source` 和 `dest`。

程序接下来检查文件是否可以读取，如果不能，则发出错误消息并退出。

语句

```objc
[fm fileExistsAtPath:dest isDirectory:&isDir];
```

检查由 `dest` 指定的文件以判断它是否为目录。正如你之前一样，答案（YES 或 NO）被存储在变量 `isDir` 中。

## 文件操作

下一章将详细介绍使用 `FileManager` 和 `NSFileHandle` 类进行文件操作。



检查由 `dest` 指定的文件以判断它是否为目录。正如你之前一样，答案（YES 或 NO）被存储在变量 `isDir` 中。

## 文件操作

下一章将详细介绍使用 `FileManager` 和 `NSFileHandle` 类进行文件操作。

`NSProcessInfo` 的 `arguments` 方法返回一个字符串对象数组。数组的第一个元素是进程名称，其余元素包含在命令行上输入的参数。

你首先检查命令行上是否输入了两个参数。这是通过测试 `arguments` 方法返回的 `args` 数组的大小来实现。如果测试成功，程序从 `args` 数组中提取源文件名和文件名，并将它们的值分别赋值给 `source` 和 `dest`。

程序接下来检查文件是否可以读取，如果不能，则发出错误消息并退出。

语句

```objc
fm fileExistsAtPath:dest isDirectory:&isDir;
```

检查由 `dest` 指定的文件以判断它是否为目录。正如你之前一样，答案（YES 或 NO）被存储在变量 `isDir` 中。

# 文件操作：NSFileHandle

表 16.7 NSFileHandle 方法

| 方法 | 描述 |
| --- | --- |
| `-(void) seekToFileOffset: offset` | 设置当前文件偏移 |
| `-(unsigned long long) seekToEndFile` | 将文件偏移置于文件末尾 |
| `-(void) truncateAtOffset: offset` | 设置大小（如果需要） |
| `-(void) close` | 关闭文件 |

未显示获取标准输入、标准输出、错误和空设备的 `NSFileHandle` 方法。这些方法的形式为 `fileHandleWithDevice`，其中 `Device` 可以是 `StandardInput`、`StandardOutput`、`StandardError` 或 `NullDevice`。

同样未显示的后台写入数据，即异步。

注意 `NSFileHandle` 类不提供创建文件。这必须通过 `FileManager` 完成，正如我们之前描述的那样。所以，句 `fileHandleForAtPath:` 和 `fileHandleForUpdatingAtPath:` 都假设文件存在，如果不存在则返回 `nil`。在这种情况下，文件偏移设置为文件开头，因此写入（或更新模式）从文件开头开始。此外，如果你在 UNIX 下编程，你应该知道打开文件进行写入不会截断文件。如果这是你的意图，你需要自己这样做。

程序 16.7 打开本章开头创建的原始 testfile，读取其内容并将其拷贝到名为 testout 的文件。

```objc
// 一些基础的文件操作

// 假设当前工作目录下存在名为 "testfile" 的文件

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        NSFileHandle *inFile, *outFile;

        NSData *data;

        char *buffer;

        // 打开文件 testfile 进行读取

        inFile = [NSFileHandle fileHandleForReadingAtPath: @"testfile"];

        if (inFile == nil) {

            NSLog(@"Open of testfile for reading failed!");

            return 1;

        }

        // 如果必要，先创建输出文件

        [[NSFileManager defaultManager] createFileAtPath:@"testout" 
                                                 contents:nil attributes:nil];

        // 现在打开 outfile 进行写入

        outFile = [NSFileHandle fileHandleForWritingAtPath:@"testout"];

        if (outFile == nil) {

            NSLog(@"Open of testout for writing failed");

            return 2;

        }

        // 截断输出文件，因为它可能包含数据

        [outFile truncateAtOffset:0];

        // 从 infile 读取数据并写入 outfile

        buffer = [inFile readDataToEndOfFile];

        [outFile writeData:buffer];

        // 关闭两个文件

        [inFile closeFile];

        [outFile closeFile];

        // 验证文件内容

        NSLog(@"%@", [NSString stringWithContentsOfFile:@"testout" encoding:NSUTF8StringEncoding error:NULL]);

        return 0;

    }
}
```

## 程序 16.7 输出

这是一个包含一些数据的测试文件。
这是另一行数据。
还有第三行。

## 基础文件操作：NSFileHandle

`readDataToEndOfFile` 方法一次读取最多 `UINT_MAX` 字节的数据，该值定义在 `<limits.h>` 中并等于 `FFFFFFFF`。这对于你要编写的任何应用程序都足够大。你也可以拆分操作以执行较小规模的读写。你甚至可以使用 `readDataOfLength:` 方法在文件和时间之间设置一个满字节的缓冲区。你的缓冲区大小应为 8,192 (8kb) 或 131,072 (128kb) 字节。通常使用 2 的幂次方，因为底层操作系统通常以数据块的大小执行 I/O 操作。你可能想在你的系统上尝试不同的值，看看什么效果最好。

如果读取到达文件末尾而没有读取到任何数据，它将返回一个空的 `NSData` 对象（即一个没有任何字节的缓冲区）。你可以对缓冲区应用 `length` 方法并进行相等测试，以检查文件中是否还有数据需要读取。

如果你打开一个文件进行更新，偏移量将设置为文件的开头。你可以通过在文件中寻道来更改该偏移量，然后在文件上执行读取或写入操作。因此，要跳到句柄为 `databaseHandle` 的文件的第 10 个字节，你可以编写以下消息表达式：

```objc
[databaseHandle seekToFileOffset: 10];
```

相对定位是通过添加当前文件偏移量并对其加或减来实现的。因此，要跳过文件中后续 128 个字节，请写入：

```objc
[databaseHandle seekToFileOffset:
    [databaseHandle offsetInFile] + 128];
```

并在文件中回退等于五个整数的位置，请写入：

```objc
[databaseHandle seekToFileOffset:
    [databaseHandle offsetInFile] - 5 * sizeof(int)];
```

程序 16.8 将一个文件的内容追加到另一个文件中。它通过打开第二个文件进行写入，寻到文件末尾，然后将第一个文件的内容写入第二个文件。

## 程序 16.8

```objc
// 将文件 "fileA" 追加到 "fileB" 的末尾

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        NSFileHandle *inFile, *outFile; // 固定指针语法

        NSData *buffer;

        // 打开 fileA 进行读取

        inFile = [NSFileHandle fileHandleForReadingAtPath:@"fileA"];

        if (inFile == nil) {

            NSLog(@"Open of fileA for reading failed");

            return 1;

        }

        // 打开 fileB 进行更新

        outFile = [NSFileHandle fileHandleForWritingAtPath:@"fileB"];

        if (outFile == nil) {

            NSLog(@"Open of fileB for writing failed");

            return 2;

        }

        // 寻到 outFile 的末尾

        [outFile seekToEndOfFile];

        // 读取 infile 并将其内容写入 outFile

        buffer = [inFile readDataToEndOfFile];

        [outFile writeData:buffer];

        // 关闭两个文件

        [inFile closeFile];

        [outFile closeFile];

        // 验证其内容

        NSLog(@"%@", [NSString stringWithContentsOfFile:@"fileB"
            encoding:NSUTF8StringEncoding error:NULL]);
    }

    return 0;
}
```

运行程序 16.8 之前 fileA 的内容：
这是第一个文件的第 1 行。
这是第一个文件的第 2 行。

运行程序 16.8 之前 fileB 的内容：
这是第二个文件的第 1 行。
这是第二个文件的第 2 行。

## 程序 16.8 输出

```
Contents of file

这是第二个文件的第 1 行。

这是第二个文件的第 2 行。

这是第一个文件的第 1 行。

这是第一个文件的第 2 行。
```

你可以从输出中看到第一个文件的内容已成功追加到第二个文件的末尾。顺便提一下，`seekToEndOfFile` 在执行寻道后返回当前文件偏移量。我们选择忽略该值；如果需要，你可以在程序中使用该信息来获取文件的大小。

## NSURL 类

`NSURL` 类为你的程序中提供了一种处理 URL 地址的方便方法。例如，给定一个指向互联网文件路径的 HTTP 地址，你可以通过几个方法调用轻松读取该文件的内容。你会在 Foundation 中找到许多将 `NSURL` 对象作为参数的方法。只需记住 `NSURL` 对象不是 `http://www.apple.com` 字符串对象，但可以使用 `URLWithString:` 方法从字符串对象轻松创建一个。程序 16.9 显示了如何从网络地址读取 HTML 内容到程序中。

## 程序 16.9

```objc
// 读取存储在 URL 中的文件内容

#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {

    @autoreleasepool {

        NSURL *myURL = [NSURL URLWithString: @"http://classroom.com"];

        NSString *myHomePage = [NSString stringWithContentsOfURL:myURL
            encoding:NSUTF8StringEncoding error:NULL];

        NSLog(@"%@", myHomePage);

    }

    return 0;

}
```

## 程序 16.9 部分输出

```
<!DOCTYPE html "-//W3C//DTD XHTML 1.0 Transitional//EN"
//"http://www.w3.org/TR/xhtml1/DTD/xhtml-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml"><head>

<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

<meta http-equiv="Content-Style" content="text/css" />

<meta name="google-site-verification" content="JT75blymBQDitXRRXbnCrVucO0zgjlyy" />

<title>iPhone Online Course and iPhone Programming</title>
```



## 练习

该方法返回一个路径名称数组。如果你的 JPEG 文件没有存储在应用程序的子目录下，你可以将 `inDirectory` 的值指定为 `"@"`：

`NSBundle` 类中还有更多方法你将学到。请查看文档以获取详情。

## 练习

1. 修改在程序 16.6 中开发的复制程序，使其能够接受多个源文件并将其复制到目录中，类似于标准的 UNIX `cp` 命令。
   `$ copy copy1.m file1.m file2.m progs`

   应该将 `copy1.m`、`file1.m` 和 `file2.m` 拷贝到 `progs` 目录。确保指定了多个源文件，且最后一个参数是一个已存在的目录。

2. 编写一个名为 `find` 的命令行工具，它接受两个参数。第一个是开始搜索的目录，第二个是要定位的文件名。因此，命令行
   `$ find /Users proposal.doc`
   `/Users/stevechan/Documents/proposals/proposal.doc`

   将从 `/Users` 开始搜索文件系统以定位文件 `proposal.doc`。如果找到文件，则打印完整路径（如所示）；如果未找到，则打印适当的消息。

3. 编写你自己的版本的标准 UNIX 工具 `basename` 和 `dirname`。

4. 使用 `NSProcessInfo` 编写一个程序，用于显示其每个方法返回的所有信息。

5. 给本章描述的 `NSPathUtils.h` 函数 `NSTemporaryDirectory` 和 `NSProcessInfo` 方法 `globallyUniqueString`，为 `NSString` 添加一个名为 `TempFiles` 的分类，并在名为 `temporaryFileName` 的方法中，每次调用时返回一个不同的唯一文件名。

6. 修改程序 16.7，使得每次读取和写入 `kBufSize` 字节的文件，其中 `kBufSize` 定义在程序的开头。务必在大文件上测试该程序（即大于 `kBufSize` 字节的文件）。

7. 打开一个文件，每次读取 128 字节内容，并将其写入终端。使用 `NSFileHandle` 的 `fileHandleWithStandardOutput` 方法获取终端输出的句柄。

8. 一个字典以属性列表的形式存储在 URL：http://bit.ly/aycNwd。编写一个程序读取该字典的内容并显示其内容。字典中包含什么数据？

# 17 内存管理与自动引用计数

回想 `NSMutableArray` 类，它允许你创建一个可以向其中添加对象和移除对象的数组。假设在程序执行开始时，你需要将文件内容读取到数组中。假设你想调用 `new myData` 并且你想从一个存储为属性列表形式的文件初始化其内容（这在第 19 章中有更详细的介绍）。

这从文件中读取并将结果元素存储到新创建的数组中，返回数组的引用。该引用被存储在变量 `myData` 中。

在这里，变量 `myData` 发生了变化，指向了另一个第一个数组，其内容是从文件中设置的。但第一个数组发生了什么呢？你不再拥有对它的引用了（当你给 `myData` 赋值时丢失了引用）。那么 `first` 数组中的所有元素呢？它们发生了什么？假设你需要重复这个过程成百或上千次地从文件中读取数据。对于所有那些不再被引用、因此应用程序不再需要的数组对象及其元素会发生什么？尽管你不再使用它们，这些对象可能仍然停留在某处。如果没有某些“清理”过程，内存将继续被未引用的对象填充，可能导致你的应用程序达到崩溃点，即实际上已经没有可用内存执行更多工作。

# 第 17 章 内存管理与自动引用计数

本章涵盖了内存管理的概念，尽管是在相当高的水平上。内存管理关于清理（回收）未使用的内存，以便可以再次使用。如果一个对象不再被使用，让我们重用它的内存。这听起来足够简单。然而，事实并没有那么简单。必须有人找出这个问题。也就是说，有人——可以是计算机，或者两者——必须能够判断对象何时不再被使用，以及其占用的内存何时可以回收。

已经开发了几种不同的内存管理策略来协助工作。其中两种是必要的；计算机跟踪对象并在需要时释放内存。第三种方法是混合方法；系统为你完成部分工作，但也要求程序员必须足够勤奋并细心地告知何时对象不再被使用。

在 Xcode 4.2 发布时，内存管理是一个备受关注的话题，它需要开发者具有大量的理解和远见。开发者必须仔细处理引用计数、`retain`、`release` 和 `autorelease` 的世界，以便产生明智使用内存的应用程序，避免在最不恰当的时机崩溃，这通常是因为尝试引用一个在时间期结束之前已无意销毁的对象。

随着 Xcode 4.2 发布了名为**自动引用计数**（简称 **ARC**）的功能，程序员不再需要考虑内存管理问题了——一切都处理好了！你有几个需要学习的特殊情况（有关它们的详情我们将参考 Apple 的文档）。但总的来说，ARC 对 iOS 开发者来说确实是天赐。这证明是，直到在本章之前，我根本没有提到过内存管理。在本书的上一个版本中，我付出了很大努力确保读者充分理解并明智地应用内存管理技术。

在本章中，你将获得适用于 Cocoa 和 iOS 开发者的不同内存管理方案的概述。我们将简要描述手动内存管理的工作方式。尽管不再需要担心对象的生命周期（以及在完成后释放内存等），但取决于你编写的应用程序类型，明智使用内存仍然很重要。例如，如果你正在编写一个在运行期间创建许多对象的交互式绘画程序，你必须确保程序在运行时不会继续消耗内存资源。在这种情况下，你有责任智能地管理这些资源，并确保你没有不必要地分配对象。

## 自动垃圾收集

对于 Objective-C 开发者支持三种基本的内存管理模型：

1. 自动垃圾收集
2. 手动引用计数和自动释放池
3. 自动引用计数 (ARC)

### 自动垃圾收集

作为 Objective C 2.0，名为垃圾收集的内存管理形式可用。通过垃圾收集，系统自动确定哪些对象拥有其他对象，并在程序执行需要空间时自动释放（垃圾收集）不再引用的对象。

iOS 运行时不支持垃圾收集，因此当你为平台开发程序时无法使用它。也就是说，你只能在开发 Mac OS 应用程序时。

如果你决定使用垃圾收集，必须在使用 Xcode 构建程序时开启它。你可以通过项目的 Build Settings 菜单来实现。在 Apple LLVM compiler 3.0 - Language 设置下，有一个名为 `Objective-C Garbage Collection` 的设置。将其从默认值 `Unsupported` 更改为 `Required` 指定你的程序将在启用自动垃圾收集的情况下构建（见图 17.1）。

![](img/22d1310b7c22ea2d48cd2058929a5cda_417_0.png)

图 17.1 启用垃圾收集

垃圾回收发生在程序运行期间，当系统确定已达到低水位线且是时候清理时。执行这一过程是一个相当计算密集型的任务；系统必须追踪你所有的对象和引用，并确定哪些对象当前正在被使用（即被引用），哪些没有被使用。这可能会导致你的应用程序出现明显的暂停，因为正如前面提到的，垃圾回收是非常计算密集型的。正因如此，你可能会决定不使用此项功能。

## 手动引用计数

如果你在不使用 ARC（自动引用计数）或垃圾回收的情况下创建应用程序，或者你必须支持无法 ARC 运行的代码，那么你需要了解如何管理内存。也就是说，你需要学习如何处理引用计数。

通用的概念如下：当一个对象被创建时，其初始引用计数设置为 1。每当你需要确保该对象被保留时，你实际上通过将其引用计数加 1 来创建一个引用。这是通过向对象发送 `retain` 消息来实现，如下：

```
[myFraction retain]
```

当你不再需要某个对象时，通过向它发送 `release` 消息将其引用计数减 1，如下所示：

```
[myFraction release]
```

当一个对象的引用计数达到 0 时，系统知道该对象不再被使用（因为在理论上，它不再被应用程序中的任何地方引用），通过启动对象的 `dealloc` 过程释放内存。在许多情况下，你会使用继承自 `NSObject` 的 `dealloc` 方法。然而，你可能需要重写 `dealloc` 来释放你的对象可能分配或保留的任何变量或其他对象。例如，如果你的类有一个 `NSArray` 作为实例变量之一，并且在对象被销毁时你 `alloc` 了它，那么你就负责释放它。你必须执行 `dealloc`。

手动引用计数策略的成功运行需要你作为程序员的勤奋，以确保引用计数在程序执行期间被适当地增加和减少。系统会处理你的一部分工作，但不是全部。

在使用手动引用计数时，你应该注意 `Foundation` 框架中的某些方法会增加对象的引用计数，例如当对象添加到 `NSMutableArray` 的 `addObject:` 方法时，或者当一个视图作为子视图添加到 `UIView` 的 `addSubview:` 方法时。同样，某些方法会减少对象的引用计数。`removeObjectAtIndex:` 和 `removeFromSuperview` 就是两种这样的方法。

在对象被销毁后（即其引用计数减至 0 并调用了 `dealloc`），对该对象的进一步引用将变得无效。如果你有这样的引用，它通常被称为悬空指针引用（dangling pointer reference）。发送该悬空指针会导致意外行为，包括你的应用程序崩溃。有时程序员会向一个已经释放释放的对象发送 `release` 消息，因为他们没有准确地跟踪对象的 `retain` 和 `release`。这被称为过度释放（over-releasing）一个对象，它通常会导致崩溃。

### 对象引用与自动释放池

你可能需要编写一个方法来创建一个对象（例如使用 `alloc`）并把该对象作为方法调用的结果返回。这里存在一个困境：尽管该方法使用了该对象，但它不能释放它，因为它需要返回它的值。`NSAutoreleasePool` 类的创建是为了解决诸如将自动释放池作为自动释放池，以便在对象中跟踪稍后要释放的对象的问题。当池被清空时，操作是通过向自动释放池发送 `drain` 消息完成的。

为了将一个对象添加到自动释放池维护的对象列表中，你向该对象发送 `autorelease` 消息，如下所示：

```
[result autorelease]
```

在处理使用 `Foundation`、`UIKit` 或 `AppKit` 框架程序的时，你必须创建一个自动释放池类，因为这些框架可以创建并返回自动释放的对象。你在应用程序中的写法如下：

```
NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
```

如果你创建一个启用了 ARC 的新项目，Xcode 会生成一个带有 `main` 起点的模板文件。

正如所述，池已经设置好，框架方法会自动将字符串、字典、按钮和其他新对象添加到自动释放池维护的列表中。

当你用完池后，你向它发送一个 `drain` 消息：

```
[pool drain]
```

这样做的效果向每个接收过 `autorelease` 消息并因此添加到池的对象发送 `release` 消息。正如你所知，如果这些对象中的任何一个引用计数减到了零，这些对象将收到 `dealloc` 消息并释放其内存。

注意，自动释放池并不包含实际的对象，只包含在池清空时要释放的对象引用。并不是所有新创建的对象都会添加到自动释放池中。事实上，任何由名称以 `alloc`、`copy`、`mutableCopy` 或 `new` 开头的方法创建的对象都不会被自动释放。在这种情况下，认为你拥有（own）它。

## 第 17 章 内存管理与自动引用计数

拥有一个对象意味着你负责在使用完它后释放该对象所占用的内存。这是通过向对象发送 `release` 消息来实现的。你也可以通过向它发送 `autorelease` 消息将其添加到自动释放池。

如果我们使用手动引用计数，程序 3.3 的主程序看起来像这样：

```
int main(int argc, char *argv[]) {
    NSAutoreleasePool *pool = [[NSAutoreleasePool alloc] init];
    Fraction *frac1 = [[Fraction alloc] init];
    Fraction *frac2 = [[Fraction alloc] init];
    // ... 其他代码 ...
    [frac1 release];
    [frac2 release];
    [pool drain];
    return 0;
}
```

注意，我们在 `main` 结束处释放了两个 `alloc` 的比例对象。尽管在应用程序终止时所有的内存都会被释放，但该示例说明了在用完对象后释放你拥有的对象的思想。示例还展示了在 `main` 开始时创建一个自动释放池，并在 `main` 结束时将其清空。

让我们再次查看程序 7.5 中使用的 `Fraction` 类的 `add:` 方法：

```
// 加两个分数：
// a/b + c/d = ((a*d) + (b*c)) / (b * d)
// result 将存储加法的结果
Fraction *result = [[Fraction alloc] init];
result.numerator = numerator * f.denominator + denominator * f.numerator;
result.denominator = denominator * f.denominator;
[result reduce];
return result;
```

### 事件循环与内存分配

在使用手动内存管理时，这个方法出现了一个问题。结果对象被 `alloc` 并在从方法中返回。由于该方法必须返回该对象，它不能释放它——否则它就会被销毁。解决此问题的最好方法是对对象进行 `autorelease`，这样它的值就可以返回，而释放会被推迟到自动释放池利用表达式返回接收者的事实：

```
Fraction *result = [[[Fraction alloc] init] autorelease];
```

或者这样：

```
return [[result autorelease]];
```

Cocoa 和 iOS 应用程序在所谓的运行或事件循环（run or event loop）中运行。对于通常通过你执行某些操作（例如，你在 iPhone 上按下按钮）或通过隐式操作（例如，网络接收到数据）发生的事件。为了处理事件，系统创建一个自动释放池并可能调用应用程序中的某些方法来处理它。当你处理完事件后，从方法返回，系统等待下一个事件的发生。在此之前，系统清空自动释放池。这意味着你创建的任何自动释放对象都将被释放，除非你保留了这些对象以便它们在池清空时存活。在使用手动引用计数时，你需要考虑自动释放池以及你的对象在事件循环结束时池清空时的存活情况。

## 第 17 章 内存管理与自动引用计数

`data` 属性的 `retain` 属性（仅用于非 ARC 编译的代码）表示，setter 方法应该保留赋值给该属性的任何对象，并释放旧值。我们在实现部分为我们的 `data` 属性合成了访问器方法。进一步假设我们有一个 `viewDidLoad` 方法，当我们的视图加载到内存时，系统会调用它。（当你学习 iOS 编程时会学到更多。目前，这些细节并不重要。）

假设在 `viewDidLoad` 方法内部，你想分配你的数据数组。在方法内部插入以下行：

```
data = [NSMutableArray array];
```

正如我们所描述的 Foundation 方法默认会创建自动释放（autoreleased）对象，该数组方法会创建一个自动释放的数组，你将其直接赋值给实例变量 `data`。问题是，该数组一旦当前事件循环完成就会被销毁。因为它是在自动释放池中创建的，而该池会在循环结束时被清空。为了确保数组在穿过事件循环时存活，你有几种替代方案。以下是三行可以使用的不同代码：

```
data = [[NSMutableArray array] retain]; // 在池清空后存活
```

```
data = [[NSMutableArray alloc] init]; // 不自动释放
```

```
self.data = [NSMutableArray array]; // 使用 setter 方法
```

在最后一种情况下，`data` 属性具有 `retain` 属性，自动释放的数组会被保留（记住赋值给 `self.data` 会调用所使用的 setter 方法）。注意，在所有三种情况下，你都必须在视图销毁时重写 `dealloc` 来释放你的数组：

```
- (void)dealloc {
    [data release];
    [super dealloc];
}
```

（调用 `super` 允许任何继承的对象被释放。使用手动内存管理的一个困恼是必须记住在释放你的对象后执行 `super dealloc`）。在许多情况下，使用框架方法创建新对象时，你可以选择创建一个自动释放的对象，也可以创建一个 `alloc` 出来的对象。如果你的应用程序在事件循环结束且池清空之前创建了许多对象，你可能想要使用 `alloc` 方法。这样一来，你可以在用完对象后立即释放它们，而无需等待事件处理结束。

# 手动内存管理规则总结

在处理手动引用计数环境时，除了属性被赋予 `atomic`（默认值）或 `nonatomic` 属性外，它们还可以被赋予 `assign`（默认值）、`retain` 或 `copy` 属性。

以下是使用 setter 设置属性值时，如何思考最后提到的这些属性是如何实现实现的，例如：

```
self.property = newValue;
```

`assign` 属性的作用方式如下：

```
property = newValue;
```

`retain` 属性的作用方式如下：

```
if (property != newValue) {
    [property release];
    property = [newValue retain];
}
```

`copy` 属性的作用方式如下：



```objc
if (property != newValue) {
    [property release];
    property = [newValue copy];
}
```

# 手动内存管理规则总结

在处理没有 ARC 垃圾回收的项目时，有一些规则需要记住：

- 如果你需要持有一个对象以确保它不被他人销毁，请确保对它进行了 `retain`。在使用完该对象后，请确保对它进行了 `release`。
- 发送 `release` 消息并不一定会销毁对象。当对象的引用计数递减到 0 时，对象会被销毁。系统通过向对象发送 `dealloc` 消息来释放其内存。
- 释放任何你通过 `copy`、`mutableCopy`、`alloc` 或 `new` 方法保留或创建的对象。这包括具有 `retain` 或 `copy` 属性的属性。你可以在对象销毁时重写 `dealloc` 来释放你的实例变量。
- 自动释放池在池本身被清空时提供对象的自动释放。系统通过对池中的每个对象根据其被自动释放的次数发送 `release` 消息来实现。自动释放池中任何引用计数下降到 0 的对象都会接收到 `dealloc` 消息以销毁该对象。
- 如果你不再需要方法内部的某个对象但需要返回它，请发送 `autorelease` 消息将其标记为稍后释放。`autorelease` 消息不会影响对象的引用计数。
- 当应用程序终止时，你占用的所有内存都会释放，无论它们是否在自动释放池中。
- 当你开发 Cocoa 或 iOS 应用时，自动释放池会在程序的执行过程中不断创建和清空（这会在每次事件发生时发生）。在这种情况下，如果你想确保自动释放的对象在自动释放池清空时不被自动销毁，你需要对它进行 `retain`。所有引用计数大于其收到的 `autorelease` 消息数的对象将在池释放后存活。

# 自动引用计数 (ARC)

自动引用计数消除了与手动引用计数相关的所有潜在陷阱。在底层，引用计数仍然被维护和跟踪。系统决定何时 `retain` 一个对象，以及何时对其进行 `autorelease` 或 `release`。你完全不需要担心这些。

你不需要担心从方法中分配对象。编译器会通过生成正确的代码对返回的对象进行必要的 `autorelease` 或 `retain`，从而找出该对象的内存需要如何管理。

# 强变量

默认情况下，所有指针变量都是强（strong）的。这意味着赋值会导致对象被 `retain`。最后，强变量默认初始化为 `nil`。所以你不需要显式地声明它们。看这段代码：

```objc
f1 = [NSMutableArray array];
f2 = [NSMutableArray array];
f1.child = f2;
f2.parent = f1;
```

如果你使用 ARC，那么 f1 和 f2 都是强引用。所以赋值方式如下：

```objc
f1.child = f2; // 使用新值
f2.parent = f1; // 使用旧值
```

现在当我们销毁父视图时，子视图对父视图的引用将不再有效。事实上，引用不存在的父视图会导致应用程序崩溃。

# 弱变量

如果你使用 ARC，你还可以使用弱（weak）指针。弱指针不会增加对象的引用计数。当对象被销毁时，弱指针会被自动设置为 `nil`。这对于避免引用循环非常有用。

# 引用循环

有时你会在两个对象之间建立一种关系，其中每个对象都需要引用另一个（这可能仅仅是两个对象，也可以是创建循环的对象链）。例如，一个可能会展示一张图片，而在图片内部你可能想为图片显示一个标题。你可以建立这样的结构：主视图是主视图，标题是子视图。

在处理这种视图层次结构时，父视图无疑想要持有其子视图的引用。在处理子视图时，知道它属于哪个父视图也是很有用的。因此，父视图将持有子视图的引用，而子视图也将持有父视图的引用。这种循环引用可能会产生问题。

当两个对象相互持有强引用时，所产生的被称为引用循环（retain cycle）。如果一个对象仍有引用，系统就不会销毁它。所以，如果两个对象相互持有强引用，任何一个都永远无法被销毁。

# 第 17 章 内存管理与自动引用计数

通过创建另一种类型的对象变量，允许两个对象之间建立不同类型的引用（即弱引用，weak reference），可以解决该问题。在这种情况下，弱引用将从子对象指向父对象。为什么呢？因为我们将另一个对象（在本例中为父视图）作为强引用，而另一个对象作为弱引用。

通过让父视图对其子视图持有强引用，而子视图对其父视图持有弱引用，就不会创建引用循环。弱变量不会防止它所引用的对象被释放。

当声明一个弱变量时，会发生几件事：系统会跟踪赋值给该变量时所创建的引用。当被引用的对象被释放时，弱变量会被设置为 `nil`。这防止了由于无意中向该对象发送消息而可能导致的崩溃。因为变量会被设置为 `nil`，向 `nil` 对象发送消息将不会产生任何操作，从而防止崩溃。

声明一个弱变量请使用 `weak` 关键字：

```objc
__weak UIView *imageView;
```

或者对属性使用 `weak` 属性：

```objc
@property (weak, nonatomic) UIView *imageView;
```

弱变量在配合代理（delegates）时也非常有用。通过让持有代理的变量变为弱，你可以确保当代理对象被释放时，该变量会被零。同样，这可以防止在 ARC 发明之前让许多程序员头疼的系统崩溃。

注意，iOS 4 或 Mac OS v10.6 不支持弱变量。在这种情况下，你仍然可以使用 `unsafe_retained`（或 `assign`）属性，或将你的变量声明为 `__unsafe_retained`。然而，要意识到，当被引用的对象被释放时，这些变量不会自动释放。

# @autoreleasepool 块

到目前为止，你已经在书中看到了编译器如何在你的主程序内部生成 `@autoreleasepool` 指令。该指令包含一组语句，定义了一个自动释放池上下文（autoreleasepool context）。在该文中创建的任何自动释放对象（这是使用 ARC 自动完成的）都会在该 `@autoreleasepool` 块结束时被销毁（除非编译器已处理以确保它们在块结束后仍然存在）。

如果你的程序生成了大量临时对象（这在循环内部执行代码时很容易发生），你可能想在程序中创建多个 `autoreleasepool` 块。例如，下面的代码段显示了如何设置 `autoreleasepool` 块来管理循环每次迭代创建的临时对象：

```objc
for (i = 0; i < n; i++) {
    @autoreleasepool {
        // 这里有大量处理临时对象的工作
    }
}
```

正如所述，Cocoa 和 iOS 运行在事件循环内部。为了给处理新事件做准备，系统会创建一个新的自动释放池上下文，并可能调用你应用程序中的某些方法来处理该事件。当你完成事件处理后，你从方法中返回，系统将等待下一个事件的发生。

在此之前，`autoreleasepool` 上下文会结束，这意味着自动释放的对象随后可能会被销毁。同样，有了 ARC，这会在“后台”自动发生，所以你不需要担心它。

# 方法名与非 ARC 编译代码

ARC 可以在未使用 ARC 编译的代码上工作。这可能发生在与旧版框架链接时，例如。只要非 ARC 代码符合标准的 Cocoa 命名规范，一切都会正常。也就是说，当 ARC 看到对 `alloc`、`copy`、`mutableCopy` 或 `init` 的调用时，它假设该方法将对象的所有权交还给调用者。

当我们谈论这里的“单词”（words）时，指的是位于 `camelCase`（驼峰命名法）中的单词。即名称中每个单词的首字母都大写。因此，编译器假设名为 `allocFraction`、`newAddressCard`、`initWithWithWidthAndHeight` 的方法返回对象的所有权，而 `newlys`、`copyAt` 和 `initials` 则不是。同样，这由 ARC 自动完成，除非你正在使用遵循此命名规范的方法。在这些情况下，有方法可以显式告诉编译器无论方法名如何，它是否返回对象的所有权。

注意，如果你尝试合成（synthesize）名称以本节第一段提到的任何特殊单词开头的属性，编译器将给你给出一个错误。

# 拷贝对象

本章讨论了涉及拷贝对象的一些微妙之处。我们引入了浅拷贝（shallow copying）与深拷贝（deep copying）的概念，并讨论了如何在 Foundation 框架下进行拷贝。

第 8 章“继承”讨论了在使用简单的赋值语句将对象赋值给另一个对象会发生什么，例如这里：

```objc
origin = pt;
```

在这个示例中，origin 和 pt 都是 `XYPoint` 对象，具有两个整数实例变量 x 和 y。

回想一下，赋值的效果仅仅是将 pt 的地址拷贝到 origin 中。在赋值操作结束时，两个变量都指向内存中的同一位置。通过如 `[origin setX:100 and:200]` 这样的消息对实例进行更改，会改变 origin 和 pt 变量引用的 `XYPoint` 对象的 x、y 坐标，因为它们都引用内存中的同一个对象。

这也适用于 Foundation 对象：将一个变量赋值给另一个仅仅是创建了对对象的引用。如果 `dataArray` 和 `dataArray2` 都是 `NSMutableArray` 对象，以下语句将影响变量所引用的同一个数组的第一个元素：

```objc
dataArray2 = dataArray;
[dataArray2 removeObjectAtIndex:0];
```

# copy 和 mutableCopy 方法

Foundation 类实现了名为 `copy` 和 `mutableCopy` 的方法，你可以使用它们来创建对象的副本。这是通过在类中实现一个方法来实现的。通过实现 `NSCopying` 协议来创建对象的副本。如果你需要创建一个可变副本，则必须实现 `NSMutableCopying` 协议。在 10.5 之前，你必须手动实现 `mutableCopy`。通过遵循 `NSCopying` 协议来创建不可变副本，你必须实现 `copy` 方法。不可变副本，正如前文所述，执行语句

```objc
dataArray2 = [dataArray copy];
```

在内存中创建了 `dataArray` 的新副本，包含其所有元素。随后执行语句

```objc
[dataArray removeObjectAtIndex:0];
```

从 `dataArray2` 中删除了第一个元素，但没有从 `dataArray` 中删除。程序 18.1 阐明了这一点。

# 程序 18.1

```objc
#import <Foundation/Foundation.h>

int main (int argc, char * argv[]) {
    @autoreleasepool {
        NSMutableArray *dataArray = [NSMutableArray arrayWithObjects:
            "one", "two", "three", "four", nil];
        NSMutableArray *dataArray2;

        // 简单赋值
        dataArray2 = dataArray;
        [dataArray2 removeObjectAtIndex:0];

        NSLog ("dataArray: %@", dataArray);
        for (NSString *elem in dataArray) {
            NSLog ("%@", elem);
        }

        NSLog ("dataArray2: %@", dataArray2);
        for (NSString *elem in dataArray2) {
            NSLog ("%@", elem);
        }

        // 尝试拷贝，然后从副本中删除第一个元素
        dataArray2 = [dataArray mutableCopy];
        [dataArray2 removeObjectAtIndex:0];

        NSLog ("dataArray: %@", dataArray);

        for (NSString *elem in dataArray) {
            NSLog ("%@", elem);
        }
    }
    return 0;
}
```

# 程序 18.1 输出

```
dataArray:
two
three
four
dataArray2:
two
three
four
dataArray:
two
three
four
dataArray2:
three
four
```

# 浅拷贝与深拷贝

程序 18.1 用不可变字符串填充了 `dataArray` 的元素（回字符串对象是不可变的）。在程序 18.2 中，你将用可变字符串填充它，这样就可以改变数组中的其中一个字符串。查看程序 18.2 并看看你是否理解了它的输出。

## 程序 18.2

```objc
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    @autoreleasepool {
        NSMutableArray *dataArray = [NSMutableArray arrayWithObjects:
            [NSMutableString stringWithString:@"one"],
            [NSMutableString stringWithString:@"two"],
            [NSMutableString stringWithString:@"three"],
            nil
        ];
        NSMutableArray *dataArray2;
        NSMutableString *mStr;

        NSLog(@"dataArray: %@\n");
        for (NSString *elem in dataArray) {
            NSLog("%@", elem);
        }
        // 创建一个拷贝，然后改变其中一个字符串

        mStr = [dataArray objectAtIndex:0];
        [mStr appendString:@"ONE"];

        NSLog(@"dataArray: %@\n");
        for (NSString *elem in dataArray) {
            NSLog("%@", elem);
        }

        NSLog(@"dataArray2: %@\n");
        for (NSString *elem in dataArray2) {
            NSLog("%@", elem);
        }
    }
    return 0;
}
```

## 程序 18.2 输出

```
dataArray:
  one
  two
  three
dataArray:
  oneONE
  two
  three
dataArray2:
  oneONE
  two
  three
```

你通过以下语句获取了 `dataArray` 的第一个元素：

```objc
mStr = [dataArray objectAtIndex:0];
```

然后你通过该语句对其追加了字符串 "ONE"：

```objc
[mStr appendString:@"ONE"];
```

注意原始数组及其拷贝的第一个元素的值：**两者都被修改**。也许你也能理解为什么 `dataArray` 的第一个元素被改变了，而它的拷贝没有。当你从集合获取一个元素时，你获得的是该元素的新引用，而不是一个新拷贝。因此，当在 `dataArray` 上调用 `objectAtIndex:` 方法时，返回的对象指向内存中与 `dataArray` 第一个元素相同的对象。随后修改字符串 `mStr` 会产生改变 `dataArray` 第一个元素的副作用，正如输出所示。

但关于你创建的那个拷贝呢？为什么它的第一个元素也被改变了？这是因为在默认情况下，拷贝是**浅拷贝**。因此，当使用 `mutableCopy` 方法拷贝数组时，会在内存中为新数组分配空间，并将各个元素拷贝到新数组中。将每个元素从原始位置拷贝到新位置，仅仅是将数组中一个元素的引用拷贝到了另一个元素。结果是两个数组的元素都引用内存中相同的字符串。这与将一个对象赋值给另一个对象没有区别，我们在本章开头介绍过。

要为数组的每个元素创建不同的拷贝，你必须执行**深拷贝**。这意味着要创建数组中每个对象的内容，而不仅仅是对象引用的拷贝（并思考如果数组元素本身也是数组，这意味着什么）。当使用 Foundation 类的 `copy` 或 `mutableCopy` 方法时，默认不会执行深拷贝。在第 19 节“归档”中，我们将展示如何使用 Foundation 的归档功能来创建对象的深拷贝。

例如，当你拷贝一个数组、字典或集合时，你获得的是这些集合的新拷贝。然而，如果你想改变一个集合但不改变其拷贝，你可能需要为单个元素创建自己的拷贝。例如，如果你在程序 18.2 中改变了 `dataArray2` 的第一个元素而不改变 `dataArray`，你可以创建一个新字符串（使用如 `stringWithString:` 等方法）并将其存储到 `dataArray2` 的位置中。



```objc
mStr = [NSString stringWithString:[dataArray2 objectAtIndex:0]];
```

然后你就可以对 `mStr` 进行更改，并使用 `replaceObjectAtIndex:withObject:` 方法将其添加到数组，如下：

```objc
[mStr appendString:@"ONE"];
[dataArray2 replaceObjectAtIndex:0 withObject:mStr];
```

希望在替换了数组中的对象后，`mStr` 和 `dataArray2` 的第一个元素指向内存中的同一个对象。因此，你程序中对 `mStr` 的后续更改也将改变数组的第一个元素。

# 实现 `<NSCopying>` 协议

如果你尝试在自己的类之一上使用 `copy` 方法——例如，在你的通讯录类上——执行以下操作：

```objc
NewBook = [myBook mutableCopy];
```

会收到类似这样的错误信息：

*** -AddressBook copyWithZone: selector not recognized

*** exception:

*** -AddressBook copyWithZone: selector not recognized

如所述，要在你的类中实现拷贝功能，你必须根据 `<NSCopying>` 协议实现一个或两个方法。

现在我们展示如何为你的 `Fraction` 类添加 `copy` 方法，该类在我们在第一部分“Objective-C 语言”中广泛使用。请注意，我们描述的拷贝策略技术适用于你自己的类。如果这些类是任何 Foundation 类的子类，你可能需要实现更复杂的拷贝策略。你必须考虑到……（注：由于提供的后续页面 OCR 文本出现严重乱码/重复，此处根据逻辑流进行了处理）。

## 在 Setter 和 Getter 方法中复制对象

你必须决定在类中是实现浅拷贝还是深拷贝。只需为该类的其他用户进行说明即可，以便他们知晓。

## 在 Setter 和 Getter 方法中复制对象

每当你实现一个 setter 或 getter 方法时，都应该考虑你正在实例变量中存储了什么、正在获取了什么，以及你是否需要保护这些值。例如，考虑当你使用相应的 setter 方法设置一个 `AddressCard` 对象的名称时：

```objc
newCard.name = newName;
```

假设 `newName` 是一个包含你新卡片名称的字符串。假设 setter 程序只是简单地将参数赋值给相应的实例变量：

```objc
(void) setName:(NSString *)theName
{
    name = theName;
}
```

现在，你认为如果程序随后更改了 `newName` 中的某些字符会发生什么（如果 `newName` 是一个可变字符串，就可能发生这种情况；此类对象可以用在指定 `NSString` 的地方，前者是后者的子类）？它还会在无意中改变你地址卡片中对应的字段，因为它们都引用同一个字符串对象。

正如你所看到的，更安全的方法是在 setter 程序中对对象进行拷贝。如果你没有合成（synthesize）setter，你也可以编写一个 `setName:` 方法的版本来使用 `copy`，如下：

```objc
(void) setName:(NSString *)theName
{
    name = [newName copy];
}
```

正如你在第 15 章“数字、字符串、字符串和集合”中所看到的，如果你在属性声明中指定了 `copy` 属性，则合成的方法将使用类的 `copy` 方法（你编写的或继承的那个）。因此，下面的属性声明

```objc
@property (nonatomic, copy) NSString *name;
```

与 `@synthesize` 指令结合时，将生成一个行为如下的方法：

```objc
(void) setName:(NSString *)theName
{
  if (theName != name)
    name = [theName copy];
}
```

使用互斥锁（mutex lock）。编写 `tells` 方法的人告诉系统不要使用互斥锁保护属性访问器，以防止两个线程同时执行同一段代码，这种情况通常会导致严重问题。这些锁会减慢程序速度，如果你知道这段代码将来会在单线程中运行，就可以避免使用它们。

如果没有指定 `nonatomic` 或者反之指定了 `atomic`（这是默认值），你的实例变量将受到互斥锁的保护。这将确保对实例变量的排他访问，并防止在多线程应用程序中如果多个线程尝试同时访问同一个变量时可能发生的竞态条件。

## 注意

属性没有 `mutablecopy`。使用可变实例变量将导致 `copyWithZone` 方法被执行，正如提到的，该方法按照惯例产生一个对象的不可变拷贝。

关于保护实例变量值的讨论也适用于 getter 程序。如果你返回一个可变对象，你应该确保对返回值的更改不会影响你实例变量的值。在这种情况下，你可以创建一个实例变量的拷贝并返回它，而不是原始值。

回到 `copy` 方法的实现，如果你正在拷贝包含不可变对象的变量（例如，不可变字符串对象），你可能不需要对对象的内容创建新的拷贝。仅仅通过赋值来创建对该对象的引用可能就足够了。例如，如果你在为包含 `name` 和 `email` 成员的 `AddressCard` 类实现 `copy` 方法，下面的 `copyWithZone` 实现就足够了：

```objc
-(AddressCard *)copyWithZone:(NSZone *)zone
{
  AddressCard *newCard = [[AddressCard allocWithZone:zone] init];

  [newCard assignName:name andEmail:email];
  return newCard;
}
```

```objc
-(void)assignName:(NSString *)theName andEmail:(NSString *)theEmail
{
  name = theName;
  email = theEmail;
}
```

`setName:andEmail:` 方法不用于设置实例变量，因为该方法会对其参数创建新拷贝，这会违背此练习的目的。相反，你使用一个名为 `assignName:andEmail:` 的新方法处理两个变量。

## 练习 423

意识到在这里直接赋值实例变量（而不是对它们进行完全拷贝）是可以的，因为拷贝卡片的所有者可以影响原始卡片的名称和邮箱成员（这些成员包含不可变字符串对象）。由于我们的两个实例变量默认是“强”变量，对它们进行简单赋值会创建该对象的另一个引用，在第 17 章中有更详细的解释。

## 练习

- 1. 根据 `NSCopying` 协议为 `AddressBook` 类实现 `copy` 方法。实现 `mutableCopy` 方法有意义吗？为什么或为什么不？另外，考虑如果有人使用 `AddressBook` 类中 `book` 属性的 setter 方法会发生什么。谁应该拥有作为参数传递给 setter 的地址簿？如何修复？

- 2. 修改第 8 章定义的 `Rectangle` 和 `XYPoint` 类以符合 `<NSCopying>` 协议。为这两个类都添加 `copyWithZone` 方法。确保 `Rectangle` 使用 `XYPoint` 的 `copy` 方法拷贝其 `XYPoint` 成员起点。为这些类实现可变和不可变拷贝有意义吗？请解释。

- 3. 创建一个 `NSDictionary` 对象并填充一些键值对。然后分别创建可变和不可变拷贝。创建的是深拷贝还是浅拷贝？验证你的答案。

# 第 19 章 归档

在 Objective-C 术语中，归档是将一个或多个对象保存为某种格式的过程，以便以后恢复。这通常涉及将对象写入文件，以便随后重新读取。我们讨论了两种归档数据的方法：属性列表（property lists）和键值编码（key-valued coding）。

## 使用 XML 属性列表归档

Mac OS X 应用程序使用 XML 属性列表（或 plist）来存储诸如默认偏好、应用程序设置和配置信息，因此了解如何创建和读取它们是很有用的。然而，当为数据结构创建属性列表时，其用于归档的作用是有限的：特定的对象类不会被保留，对同一个对象的多个引用不会被存储，对象的可变性也不会保留。

> 所谓的“旧式”属性列表存储数据的形式与 XML 属性列表不同。尽可能在你的程序中使用 XML 属性列表。

如果你的对象类型是 `NSString`、`NSDictionary`、`NSArray`、`NSDate`、`NSData` 或 `NSNumber`，你可以使用这些类实现的 `writeToFile:atomically:` 方法将数据写入文件。在写入字典或数组的情况下，该方法以属性列表的格式将数据写入文件。程序 19.1 显示了第 15 章“数字、字符串和集合”中创建的字典如何作为属性列表写入文件。

### 程序 19.1

```objc
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    @autoreleasepool {
        // 此处省略字典创建代码
        [glossary writeToFile:@"glossary" atomically:YES];
    }
    return 0;
}
```

`writeToFile:atomically:` 消息发送给你的字典，导致字典作为属性列表写入文件。`atomic` 参数设置为 `YES`，这意味着写入操作首先执行临时备份文件；一旦成功，最终数据将移动到指定的文件。这是一种保护措施，防止系统在操作过程中崩溃导致文件损坏，保护原始文件（如果存在）。

如果你检查程序 19.1 创建的字典内容，它看起来如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN">
<!DOCTYPE SYSTEM "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
  <key>abstract class</key>
  <string>为了让其他类继承而定义的类。</string>
  <key>adopt</key>
  <string>实现协议定义的所有方法</string>
  <key>archiving</key>
  <string>为了以后使用存储对象。</string>
</dict>
</plist>
```

从创建的 XML 文件中你可以看到字典是以一组键 `<key>...</key>` 和值 `<string>...</string>` 对的形式写入文件的。

## 使用 NSKeyedArchiver 进行归档

当你从字典创建属性列表（property list）时，字典中的键必须是 `NSString` 对象。数组的元素或字典的值可以是 `NSString`、`NSArray`、`NSDictionary`、`NSData`、`NSDate` 或 `NSNumber` 对象。

要从文件中将 XML 属性列表读取到程序中，请使用 `dictionaryWithContentsOfFile:` 或 `arrayWithContentsOfFile:` 方法。读取回数据请使用 `dataWithContentsOfFile:`；读取字符串对象请使用 `stringWithContentsOfFile:` 方法。程序 19.2 回读了程序 19.1 中的词汇表并显示其内容。

### 程序 19.2

```objc
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    @autoreleasepool {
        NSDictionary *glossary;

        glossary = [NSDictionary dictionaryWithContentsOfFile:@"glossary"];

        for (NSString *key in glossary) {
            NSLog("%@: %@", key, [glossary objectForKey:key]);
        }
    }

    return 0;
}
```

### 程序 19.2 输出

archiving: 存储一个对象以供以后使用。

abstract class: 定义一个类以便其他类可以继承自它。

adopt: 实现协议中定义的所有方法。

你的属性列表不需要从 Objective-C 程序创建；属性列表可以来自任何数据源。你可以使用简单的文本编辑器创建属性列表，或者使用 Mac OS X 系统上位于 `/Developer/Applications/Utilities` 下的属性列表编辑器程序。如果你计划在应用程序中使用属性列表，你可能想查看一下 `PropertyListSerialization` 类，它允许以机器可移植的方式将属性列表写入文件并从文件中读取。

## 使用 NSKeyedArchiver 进行归档

一种更灵活的方法允许你将任何类型的对象保存到文件中，而不仅仅是字符串、数组和字典。这是通过使用 `NSKeyedArchiver` 类创建键值归档（keyed archive）来实现的。

Mac OS X 从 10.2 版本开始就支持键值归档（keyed archives）。在此之前，使用 `NSArchiver` 类创建顺序归档（sequential archives）。顺序归档要求归档中的数据必须按照写入时完全相同的顺序被读取回。

键值归档是指归档中的每个字段都有一个名称。当你检索一个对象时，你给它一个名称或“键”。当你从归档中检索它时，通过相同的键进行检索。实际上，对象可以以任何顺序进行写入和检索。此外，如果类中添加或删除了实例变量，你的程序可以处理这种变化。

程序 19.3 显示了可以使用 `NSKeyedArchiver` 类的 `archiveRootObject:toFile:` 方法将词汇表保存到磁盘文件中。

### 程序 19.3

```objc
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    @autoreleasepool {
        // 此处省略字典创建代码
        [NSKeyedArchiver archiveRootObject:glossary toFile:@"glossary.archive"];
    }
    return 0;
}
```

程序 19.3 不会在终端产生任何输出。然而，语句 `[NSKeyedArchiver archiveRootObject:glossary toFile:@"glossary.archive"];` 将词汇表写入 `glossary.archive` 文件。可以为文件指定任何路径。在这种情况下，文件被写入到当前目录。

创建的归档文件以后可以使用 `NSKeyedUnarchiver` 的 `unarchiveObjectWithFile:` 方法读取到你的程序中，如程序 19.4 所示。

### 程序 19.4

```objc
#import <Foundation/Foundation.h>

int main (int argc, char *argv[]) {
    @autoreleasepool {
        NSDictionary *glossary;
        glossary = [NSKeyedUnarchiver unarchiveObjectWithFile:@"glossary.archive"];

        for (NSString *key in glossary) {
            NSLog("%@:%@", key, [glossary objectForKey:key]);
        }
    }
    return 0;
}
```

### 程序 19.4 输出

abstract class: 定义一个类以便其他类可以继承自它。

adopt: 实现协议中定义的所有方法。

archiving: 存储一个对象以供以后使用。

语句

```objc
glossary = [NSKeyedUnarchiver unarchiveObjectWithFile:@"glossary.archive"];
```

会导致文件被打开并读取其内容。此文件必须是文件的完整路径或如示例中的相对路径。

词汇表恢复后，程序简单地枚举其内容以验证恢复是否成功。

## 编写编码和解码方法

基础 Objective-C 类，如 `NSString`、`NSArray`、`NSDictionary`、`NSSet`、`NSDate`、`NSNumber` 和 `NSData`，可以按照上述描述的方式进行归档和存储。这还包括嵌套对象，例如包含字符串或其他数组对象的数组。

这意味着 Objective-C 系统并不知道如何使用这种技术归档一个 `AddressBook`，因为你尝试通过插入如下行来归档 `AddressBook`：

```objc
[NSKeyedArchiver archiveRootObject:myAddressBook toFile:@"addressbook.archive"];
```



# 编写编码和解码方法

基础 Objective-C 类，如 `NSString`、`NSArray`、`NSDictionary`、`NSSet`、`NSDate`、`NSNumber` 和 `NSData`，可以按照上述描述的方式进行归档和存储。这还包括嵌套对象，例如包含字符串或其他数组对象的数组。

这意味着 Objective-C 系统并不知道如何使用这种技术归档一个 `AddressBook`，因为你尝试通过插入如下行来归档 `AddressBook`：

```objc
[NSKeyedArchiver archiveObject:myAddressBook toFile: @addressbook.archive];
```

从错误信息中，你可以看到系统正在 `AddressBook` 类中寻找名为 `encodeWithCoder:` 的方法，但你从未定义过此类方法。要归档列出之外的其他对象，你必须告诉系统如何归档（编码）以及如何解码。这是通过根据 `<NSCoding>` 协议在你的类定义中添加 `encodeWithCoder:` 和 `initWithCoder:` 方法来实现的。

## 程序 19.5 AddressCard.h

```objc
#import <Foundation/Foundation.h>

@interface AddressCard: NSObject <NSCoding>

@property (copy, nonatomic) NSString *name, *email;

-(void)setName:(NSString *)name andEmail:(NSString *)email;

@end
```

### 实现文件

```objc
- (void) encodeWithCoder:(NSCoder *)encoder
{
  [encoder encodeObject:name forKey:@"name"];
  [encoder encodeObject:email forKey:@"email"];
}

- (id)initWithCoder:(NSCoder *)decoder
{
  name = [decoder objectForKey:@"name"];
  email = [decoder objectForKey:@"email"];

  return self;
}
```

# 第 19 章 归档

它是会在你想要从归档中提取的每个对象时发送消息的那个。

再次，由于你的 `AddressCard` 类直接继承自 `NSObject`，你不需要担心解码继承的实例变量。如果你确实需要，可以在解码器方法的开头插入类似下面的一行（假设该类的父类符合 `NSCoding` 协议）：

```objc
self = [super initWithCoder:decoder];
```

每个实例变量都是通过调用 `decodeObject:forKey:` 并传递与编码该变量时相同的键来解码的。

与你的 `AddressCard` 类类似，你也要为 `AddressBook` 类添加了编码和解码方法。你需要在接口文件中进行修改的唯一行是 `@interface` 指令，用于声明 `AddressBook` 类现在符合 `NSCoding` 协议。修改看起来如下：

```objc
@interface AddressBook: <NSCoding, NSCopying>
```

以下是包含在实现文件中的方法定义：

```objc
- (void) encodeWithCoder:(id *)encoder
{
    [encoder encodeObject:bookName forKey:@"AddressBookName"];
    [encoder encodeObject:book forKey:@"AddressBook"];
}

- (id) initWithWithCoder:(id *)decoder
{
    bookName = [decoder decodeObjectForKey:@"AddressBookName"];
    book = [decoder decodeObjectForKey:@"AddressBook"];

    return self;
}
```

## 程序 19.6 测试程序

```objc
#import "AddressBook.h"

int main(int argc, char *argv[])
{
    @autoreleasepool {
        NSString *aName = @"Julia Kochan";
        NSString *aEmail = @"jewels337@axlc.com";
        NSString *bName = @"Tony Iannino";
        NSString *bEmail = @"tony.iannino@techfitness.com";
        NSString *cName = @"Stephen Kochan";
        NSString *cEmail = @"steve@steve_kochan.com";
        NSString *dName = @"Jamie Baker";
        NSString *dEmail = @"jbaker@hitmail.com";

        AddressCard *card1 = [[AddressCard alloc] init];
        AddressCard *card2 = [[AddressCard alloc] init];
        AddressCard *card3 = [[AddressCard alloc] init];
        AddressCard *card4 = [[AddressCard alloc] init];

        AddressBook *myBook = [[AddressBook alloc] init];

        // 第一设置地址卡
        [card1 setName:aName andEmail:aEmail];
        [card2 setName:bName andEmail:bEmail];
        [card3 setName:cName andEmail:cEmail];
        [card4 setName:dName andEmail:dEmail];

        myBook = [[myBook initWithName:@"Steve's Address Book*"] init];

        // 向地址簿中添加一些卡片
        [myBook addcard:card1];
        [myBook addcard:card2];
        [myBook addcard:card3];
        [myBook addcard:card4];

        [myBook sort];

        if ([NSKeyedArchiver archiveRootObject:myBookToFile:
        @"addbook.arch"] == NO) {
            NSLog(@"archiving failed");
        }
        return 0;
    }
}
```

该程序创建了地址录，然后将其归档到文件 `addrbook.arch`。在创建归档文件的过程中，你会意识到 `AddressBook` 和 `AddressCard` 类的编码方法都被调用了。如果你想要证明，可以在这些方法中添加一些 `NSLog` 调用。

## 程序 19.7

```objc
#import "AddressBook.h"

int main (int argc, char * argv[]) {
    AddressBook *myBook;

    @autoreleasepool {
        myBook = [NSKeyedUnarchiver unarchiveObjectWithFile:@"addrbook.arch"];
        [myBook list];
    }

    return 0;
}
```

### 程序 19.7 输出

```
======= Contents of Steve's Address Book ========
Jamie Baker jaker@hitmail.com
Julia Kochan jewls337@axlc.com
Stephen Kochan steve@steve_kochan.com
Tony Iannino tony.iannino@techfitness.com
=============================================
```

在解档地址簿的过程中，添加到你类中的解码方法被自动调用了。注意你可以多轻松地将地址簿读回程序中。

如所述，`encodeObject:forKey` 方法适用于内置类以及你根据 `NSObject` 协议编写编码和解码方法的类。如果你的实例包含某些数据类型（例如整数或浮点数），你需要知道如何编码和解码它们（参见表 19.1）。

这里是一个名为 `Foo` 的类的简单定义，它包含实例变量——其中一个 `NSString`，另一个是 `int`，第三个是 `float`。该类有一个 setter、getter 和两个用于归档的编码/解码方法：

```objc
@interface Foo: NSObject <NSCoding>

@property (copy, nonatomic) NSString *strVal;
@property int intVal;
@property float floatVal;

@end
```

### 实现文件

```objc
@implementation Foo

@synthesize strVal, intVal, floatVal;

- (void) encodeWithCoder:(id *)encoder
{
    [encoder encodeObject:strVal forKey:@"strVal"];
    [encoder encodeInt:intVal forKey:@"intVal"];
    [encoder encodeFloat:floatVal forKey:@"floatVal"];
}

- (id) initWithWithCoder:(id *)decoder
{
    strVal = [decoder decodeObjectForKey:@"strVal"];
    intVal = [decoder decodeIntForKey:@"intVal"];
    floatVal = [decoder decodeFloatForKey:@"floatVal"];

    return self;
}

@end
```

# 使用 NSData 创建自定义归档

```objc
@autoreleasepool {
    Foo *myFoo = [[Foo alloc] init];
    NSMutableData *dataArea;
    NSKeyedArchiver *archiver;
    AddressBook *myBook;
}
```

```objc
// 插入程序 19.7 中的代码以在 my book 中
// 创建包含四张地址卡片的通讯录
```

```objc
[myFoo setStrVal:@"This is the string"];
[myFoo setIntVal:12345];
[myFoo setFloatVal:98.6];
```

```objc
// 设置一个数据区域并将其连接到 NSKeyedArchiver 对象
dataArea = [NSMutableData data];
```

```objc
archiver = [[NSKeyedArchiver alloc];
initForWritingWithMutableData:dataArea];
// 现在我们可以开始归档对象
[archiver encodeObject:myBook forKey:@myaddrbook];
[archiver encodeObject:myFoo forKey:@myfool];
[archiver finishEncoding];
```

```objc
// 将归档后的数据区域写入文件
if ((dataArea writeToFile:@"archive" atomically: YES) == NO) {
    NSLog("Archiving failed!");
}
return 0;
```



在分配一个 `NSKeyedArchiver` 对象后，会发送 `initForWritingWithMutableData` 消息以指定写入归档数据的区域；这就是你之前创建的 `NSMutableData` 区域 `dataArea`。存储在 `archiver` 中的 `NSKeyedArchiver` 对象现在可以发送消息来归档程序中的对象了。事实上，在收到 `finishEncoding` 消息之前，它会将所有的编码消息归档并存储在指定的区域。

你有两个对象需要归档——第一个是通讯录，第二个是你的 `Foo` 对象。你可以对这些对象使用 `encodeObject:forKey:`，因为你之前已经为 `AddressBook`、`AddressCard` 和 `Foo` 类实现了编码器和解码器方法。理解这个概念非常重要。

当你完成这两个对象的处理时，`archiver` 对象会接收到 `finishEncoding` 消息。此之后不能再归档任何对象，你需要发送此消息来完成归档过程。

你预留并命名为 `dataArea` 的数据区域现在包含了你归档的对象，其格式可以写入文件。消息表达式
`[dataArea writeToFile:@myArchive] atomically: YES]`
结束了向你的数据流发送 `writeToFile:atomically:` 消息，请求其将你的数据写入到名为 `myArchive` 的指定文件中。

如你从语句所示，`writeToFile:atomically:` 方法返回一个 `BOOL` 值：如果写入操作成功则返回 `YES`，如果失败（由于指定的文件路径无效或文件系统已满）则返回 `NO`。

从归档文件中恢复数据非常简单：你只需要反向操作即可。首先，需要预先分配一个数据区域。接下来，你需要将归档文件读取到数据区域；然后，你需要创建一个 `NSKeyedUnarchiver` 对象，并告诉它从指定区域解码数据。你必须调用解码方法来提取并解码你归档的对象。一旦完成，向 `NSKeyedUnarchiver` 对象发送一个 `finishDecoding` 消息。

所有这些操作都在程序 19.10 中完成。

# 程序 19.10

```objc
#import "AddressBook.h"
#import "Foo.h"

int main (int argc, char * argv[])
{
    @autoreleasepool {
        NSData *dataArea;
        NSKeyedUnarchiver *unarchiver;
        Foo *myFoo;
        AddressBook *myBook;

        // 读取归档并连接一个 NSKeyedUnarchiver 对象到它
        dataArea = [NSData dataContentsOfFile:@myArchive];

        if (!dataArea) {
            NSLog(@"Can't read back archive file!");
            return 1;
        }

        unarchiver = [[NSKeyedUnarchiver alloc] initReadingWithData:dataArea];

        // 解码之前存储在归档中的对象
        myBook = [unarchiver decodeObjectForKey:@myaddbook];
        myFoo = [unarchiver decodeObjectForKey:@myfool];

        [unarchiver finishDecoding];

        // 验证恢复是否成功
        [myBook list];
        NSLog(@"%@\n%d\n%f", [myFoo strVal], [myFoo intVal], [myFoo floatVal]);

        return 0;
    }
}
```

# 程序 19.10 输出

```
======= Contents of Steve's Address Book ========
Jamie Baker jbaker@hotmail.com
Julia Kochan jewls337@axlc.com
Stephen Kochan steve@steve_kochan.com
Tony Lannino tony.lannino@techfitness.com
================================================
This is the string
12345
98.6
```

输出验证了通讯录和你的 `Foo` 对象已成功从归档文件中恢复。

# 使用归档器复制对象

在程序 18.2 中，你尝试对包含可变字符串元素的数组创建副本，并看到了数组是如何进行浅拷贝的。实际上，字符串本身并没有被复制——只复制了它们的引用。
你可以使用 Foundation 的归档功能来创建对象的深拷贝。例如，程序 19.11 通过将 `dataArray` 归档到缓冲区然后解归档并赋值给 `array2`，从而将 `dataArray` 拷贝到 `array2`。

# 程序 19.11

```objc
#import <Foundation.h>

int main (int argc, char * argv[])
{
    @autoreleasepool {
        NSMutableArray *dataArray = [NSMutableArray arrayWithObjects:@"one", @"two", @"three", nil];
        NSMutableData *dataArea;
        NSKeyedArchiver *archiver = [[NSKeyedArchiver alloc] initForWritingWithMutableData:dataArea];

        [archiver encodeObject:dataArray forKey:@dataArray];
        [archiver finishEncoding];

        NSData *loadedData = [NSData dataContentsOfFile:@"myArchive"];
        NSKeyedUnarchiver *unarchiver = [[NSKeyedUnarchiver alloc] initReadingWithData:loadedData];
        NSMutableArray *array2 = [unarchiver decodeObjectForKey:@dataArray];

        [unarchiver finishDecoding];
        NSLog(@"%@", array2);
    }
    return 0;
}
```



# 第 20 章 Cocoa 和 Cocoa Touch 简介

![](img/22d1310b7c22ea2d48cd2058929a5cda_460_0.png)

计算机资源（内存、磁盘、显示器等）

**图 20.1** 应用程序层级结构

Application Services 层包含了对打印和图形渲染的支持，包括 Quartz、OpenGL 和 Quicktime。
紧挨在你的应用程序下方的是 Cocoa 层。如前指出的，*Cocoa* 包含了 Foundation、Core Data 和 AppKit 框架。Foundation 提供了用于处理集合、管理内存、文件系统、归档等的类。AppKit 类则用于管理窗口、视图、文档以及用户界面，而这正是 Mac OS X 广为人知的特性。
从这一描述来看，某些层之间似乎存在功能上的重复。集合（Collections）存在于 Cocoa 层和 Core Services 层中。然而，前者建立在后者的支持之上。此外，在某些情况下，某个层可以被跳过或“桥接”。例如，处理文件系统的 Foundation 类直接依赖 Core Services 层，因此跳过了 Application Services 层。在许多情况下，Foundation 框架对低层 Core Services 层（主要用过程化 C 语言编写）中的数据结构定义了面向对象的映射。

# Cocoa Touch

iPhone、iPod Touch 和 iPad 等 iOS 设备包含了一台运行着缩减版 Mac OS X 的计算机。iPhone 硬件中的某些功能（例如其加速度计）是手机特有的，在其他 Mac OS X Pro 或 iMac 上是找不到的。

实际上，Mac 笔记本电脑也包含加速度计，以便在电脑掉落时让硬盘停靠；然而，你无法在程序中直接访问此加速度计。

Cocoa 框架是为 Mac OS 桌面和笔记本电脑的应用程序开发设计的，而 Cocoa Touch 框架则是针对 iOS 设备的应用程序。

Cocoa 和 Cocoa Touch 共有 Foundation 和 Core Data 框架。然而，在 Cocoa Touch 下，`UIKit` 取替了 `AppKit` 框架，提供了许多类型对象的支持，例如窗口、视图、按钮、文本字段等。此外，Cocoa Touch 提供了处理加速度计、陀螺仪、通过 GPS 和 Wi-Fi 信号定位以及触摸驱动界面的类，并消除了不需要类。

对 Cocoa 和 Cocoa Touch 的简要介绍到此结束。在下一章中，你将学习如何使用 iOS SDK 中的模拟器为 iPhone 编写应用程序。

# 第 21 章 编写 iOS 应用程序

在本章中，你将开发两个简单的 iPhone 应用程序。第一个将介绍一些基本概念，让你熟悉使用 Interface Builder、建立连接以及理解代理（delegates）、输出（outlets）和动作（actions）。对于第二个 iPhone 应用程序，你将构建一个分数计算器。它将与书中其余部分学到的知识相结合。你在这里学到的原理也可以用于为其他 iOS 设备开发应用程序。

# iOS SDK

编写 iPhone 应用程序，你必须安装 Xcode 和 iOS SDK。该 SDK 可以从 Apple 网站免费获取。要下载 SDK，你首先需要注册成为 Apple 开发者（Apple Developer）。该过程也是免费的。要获取合适的链接，你可以从 `developer.apple.com` 开始并导航到相应位置。熟悉该网站是一个好主意。

本章的讨论基于 Xcode 4.2 和针对 iOS 5 的 iOS SDK。这两者的后续版本都应该与所描述的内容兼容。如果你发现屏幕显示与所示的不符，可能是因为你使用了不同版本的 Xcode。在这种情况下，请查看 `classroomM.com/objective-c` 论坛获取信息。

# 你的第一个 iPhone 应用程序

第一个应用程序展示了如何在 iPhone 屏幕上放置一个黑色的窗口，允许用户按下按钮，然后根据按钮点击显示某些文本。

> **注意**
> 第二个应用程序更有趣！你将利用从第一个应用程序中获得的知识来构建一个处理分数的简单计算器。你可以使用书中之前处理过的 `Fraction` 类，以及一个修改过的 `Calculator` 类。这次，你的计算器需要知道如何处理分数。

让我们直接进入第一个程序。本章采用的教学方法并不是涵盖所有细节；如前指出的，这里没有足够的空间做到这一点。相反，我们通过演示这些步骤，为你提供必要的基础，以便你通过另一本 Cocoa 或 iOS 编程书籍自行探索和学习更多概念。
图 21.1 显示了你为 iPhone 开发的第一个应用程序，运行在 iPhone 模拟器上（稍后将进行详细介绍）。

![](img/22d1310b7c22ea2d48cd2058929a5cda_464_0.png)

**图 21.1** 第一个 iPhone 应用程序

该应用程序的设计目的是展示当你按下标记为“1”的按钮时，相应的数字会出现在显示器上（见图 21.2）。它仅此而已！这个简单的应用程序为第二个分数计算器应用程序奠定了基础。
到书中这里，如果你已经使用 Xcode 输入并测试过程序，那么你应该已经熟悉 Xcode 了。这一次，我们还将使用 Xcode 的一项功能，允许你通过在显示 iPhone 屏幕的窗口中放置表格、标签和按钮等 UI 元素来设计用户界面。

> **注意**
> 在 Xcode 4 发布之前，UI 是使用一个名为 Interface Builder 的独立应用程序进行设计的。

![](img/22d1310b7c22ea2d48cd2058929a5cda_465_0.png)

**图 21.2** iPhone 应用程序

Apple 在 SDK 中分发 iPhone 模拟器。模拟器模拟了 iPhone 环境，包括主屏幕、Safari 浏览器等，使得调试变得更加容易。

要在 iOS 设备上运行应用程序，你需要注册 开发者计划并向 Apple 支付 99 美元的费用（编写时）。作为回报，你将收到一个激活代码，允许你在 iOS 设备上运行应用程序。这可以节省大量时间。

# 创建新的 iPhone 应用程序

让我们开发你的第一个应用程序。安装 iOS SDK 后，启动 Xcode 程序。选择 File，然后 New Project... 在 iOS 下（如果你在左侧栏没有此项，说明你还没有安装 iOS SDK），点击 Application。你应该看到一个窗口，如图 21.3 所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_466_0.png)

**图 21.3** 创建新项目

在这里，我们使用的模板为不同类型的应用程序提供了起点，如表 21.1 所示。

# iOS 应用程序模板

| 应用程序类型 | 描述 |
| --- | --- |
| Master-Detail | 使用导航器的应用程序。Contacts 是此类示例应用程序。为 iPad 等大屏幕设备生成分屏视图应用程序 |
| OpenGL Game | 基于 OpenGL ES 图形的游戏。 |
| Page-based Application | 使用页面控制器管理页面显示的应用程序。 |
| Single View Application | 从单个视图开始的应用程序。你在视图中进行绘图并将视图显示在窗口中。 |
| Tabbed Application | 使用标签栏的应用程序。例如 Music 应用程序。 |
| Utility Application | 使用翻转视图的应用程序。Stock Quote 应用是此类示例。 |
| Empty Application | 仅从主 iPhone 窗口开始的应用程序。你可以将其作为应用程序的起点。 |

回到 New Project 窗口，在右上窗格中选择 Single View Application，然后点击 Next 按钮。在 Product Name 中输入 `iPhone_1`，Company Identifier 随你填写，选择 Device Family 以勾选 User Automatic Reference Counting，并取消勾选 Use Story 和 Include Unit Tests。你的屏幕应该像图 21.4 所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_467_0.png)

**图 21.4** 选择项目选项

点击 Next（下一步）。你可以指定创建新项目文件夹的位置，无需担心 Source Control（源码控制）框是否被勾选。你的屏幕现在看起来应该像图 21.5。

![](img/22d1310b7c22ea2d48cd2058929a5cda_467_1.png)

**图 21.5** 指定存储项目文件夹的位置。

现在，点击 Create（创建）。如你从之前的项目中所知，你创建的项目将包含你想要使用的文件模板。这在图 21.6 中所示，`iPhone_1` 文件夹显示了五个文件：`iPhone_AppDelegate.h`、`iPhone_AppDelegate.m`、`iPhone_1ViewController.h`、`iPhone_1_ViewController.m` 和 `MainWindow.xib`。最右侧的面板包含了你的应用程序支持的方向以及应用程序的图标等。我们在这里忽略这个面板。

![](img/22d1310b7c22ea2d48cd2058929a5cda_468_0.png)

**图 21.6** 创建了新的 iOS 项目 iPhone_1

根据你的设置和之前对 Xcode 的使用，你的窗口可能不像图 21.6 所示。你可以选择按照你当前布局允许的操作进行，或者尝试将其设置为清晰标记的 Scheme（方案）。

在 Xcode 窗口的左上角，选择下拉菜单 Scheme。因为我们并不是开发这个应用程序以直接运行在 iPhone 上，所以你希望将 SDK 设置为在 iPhone 模拟器上运行。如图 21.7 所示，从下拉菜单中选择 iPhone simulator。

# 输入你的代码

现在我们准备好修改一些项目文件了。注意，系统为你创建了一个名为 `projectnameAppDelegate` 的类，在这个示例项目中 project-name 是 `iPhone_1`。你创建的每一个新 iOS 应用程序都会创建一个 application delegate（应用程序代理）子类。通常，有方法可以控制应用程序的执行。这包括诸如应用程序启动时、进入和离开后台时、系统告诉它内存使用过多时以及终止时该做什么等操作。在本章的两个示例中，我们都不会对这个类进行任何更改。

系统也为你创建了第二个类：`iPhone_1ViewController`。如你所见，Xcode 在相应的 .h 和 .m 文件为你创建了接口和实现部分。视图控制器（view controller）负责管理 iPhone 屏幕上一个或多个“视图”的显示。在这个应用程序中，我们只有一个视图，如图 21.1 所示。应用程序呈现许多不同的视图并使用多个视图控制器来管理它们的情况并不罕见。

我们的视图控制器类将负责处理标记为“1”的按钮的按下事件。我们定义了一个方法来响应该动作在 iPhone 窗口中发生时的操作，例如按下按钮。你很快就会看到如何将该动作与特定方法的执行连接起来。

你的对象可以拥有实例变量，其值对应于 iPhone 窗口中的控件，例如 outlet（插槽）上的名称或在可文本框中显示的文本。这些变量被称为 outlet，你将看到如何将实例变量连接到 iPhone 窗口中的实际控件。

对于我们的第一个应用程序，我们需要一个方法来响应按下标记为 1 的按钮的动作。我们还需要添加一个 outlet 变量，它包含（除其他信息外）要显示在我们在 iPhone 窗口顶部创建的标签中的内容。

编辑文件 `iPhone_1ViewController.h`，以添加一个名为 `display` 的新 `UILabel` 属性，并声明一个 action 方法（动作方法）来响应按钮的按下。你的接口文件应该像程序 21.1 所示。（文件开头自动插入的注释行在此不再显示。）

# 程序 21.1 iPhone_1ViewController.h

```objc
#import <UIKit/UIKit.h>

@interface iPhone_1ViewController : UIViewController

@property (strong, nonatomic) UILabel *display;

- (IBAction) click1;

@end
```

注意，iPhone 应用程序使用了头文件 `<UIKit/UIKit.h>`。这个头文件反过来导入了其他 UIKit 头文件，就像 `Foundation.h` 文件导入你需要的其他头文件（如 `NSString.h` 和 `NSObject.h`）一样。

注意：如本文之前提到的，使用与属性名不同的实例变量名会鼓励你通过属性而不是直接通过变量名来访问实例变量。Apple 一直采用这种编码风格。

你添加了属于 `UILabel` 类的名为 `display` 的属性。这将连接到标签的 outlet 属性（插槽属性）。当你设置这个属性字段时，它会更新窗口中标签的内容。`UILabel` 类定义的其他方法允许你设置它。

```objc
#import "iPhone_1ViewController.h"

@implementation iPhone_1ViewController

@synthesize display;

- (IBAction) click1 {
    self.display.text = @"1";
}

// 其他插入的方法

@end
```



# 第 21 章 编写 iOS 应用程序

## 设计界面

在 21.4 中，在 Xcode 主窗口中，注意一个名为 `iPhoneViewController.nib` 的文件。xib 文件（历史上被称为 "nib" 文件）因为它使用的扩展名包含了程序界面的信息，包括按钮、标签、标签栏、文本框等。

从左侧面板选择 `iPhoneViewController.xib` 文件。这会导致界面设计工具出现，如图 21.8 所示。右侧面板显示了 iPhone 窗口，默认背景为灰色。

从菜单栏中选择 Utilities（工具）、Attributes Inspector（属性检查器）、Object Library（对象库）。你的窗口应该像图 21.9 所示。

（如果你想让你的屏幕与图匹配，请查看检查器工具栏中的各种选项。此图显示了右侧面板的属性检查器和右下角面板的对象库。）

我们要做的第一件事是将 iPhone 窗口设置为黑色。为了做到这一点，首先点击中间面板中的 iPhone 窗口。

如果你扫一眼面板的部分，你会看到一个标记为 Background（背景）的属性。点击 Background 旁边填充颜色的矩形，它会弹出一组供你选择的颜色。选择黑色，这将检查器中 Background 旁的矩形从灰色变为黑色。

如果你查看代表 iPhone 窗口的中间面板，你会看到它变成了黑色，如图 21.10 所示。

你可以通过从对象库中拖拽对象到 iPhone 窗口中在 iPhone 界面中创建新对象。现在拖一个 Label（标签）。当标签位于窗口左侧、靠近顶部时释放鼠标，如图 21.11 所示。

当你移动标签并使其与窗口中之前放置的其他对象对齐时，会出现蓝色引导线。在其他时候，这些引导线的出现是为了确保你的对象与其他对象以及窗口边缘之间保持足够的距离，以符合 Apple 的界面指南。

你可以在未来的任何时候通过选择并拖动标签到窗口内的另一个位置来重新定位标签。

现在让我们为此标签设置属性。在你的 iPhone 窗口中，如果该标签当前未被选中，请点击你刚刚创建的标签以选中它。注意，检查器（Inspector）为你提供了有关窗口中当前选中对象的信息。我们不希望此标签默认显示文本，因此请将 `Value`（值）更改为空字符串。（也就是说，从检查器面板显示的文本框中删除字符串 `Label`。）

对于 `Alignment`（对齐）属性，选择右对齐图标。最后，将背景颜色更改为蓝色（或你选择的任何颜色），就像你将窗口背景颜色更改为黑色一样。

现在让我们更改标签的大小。回到 Window，只需通过拉动标签的角和侧边来调整其大小。调整并重新定位标签，使其看起来像图 21.12 中的所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_474_0.png)

图 21.12 修改标签的属性和大小

现在我们将向界面添加一个按钮。从对象库（Object Library）面板中，将一个圆角按钮（Rounded Rect Button）对象拖入你的界面窗口，将其放置在窗口的左下角，如图 21.13 所示（注意此图显示对象库窗口已图标视图更改为列表视图）。你可以通过两种方式更改按钮上的标签：双击按钮并输入文本，或者通过设置检查器面板中的 `Title`（标题）字段。无论选择哪种方法，请让你的窗口与图 21.13 所示的匹配。

![](img/22d1310b7c22ea2d48cd2058929a5cda_475_0.png)

图 21.13 向界面添加按钮

现在我们有一个标签，想要将其连接到程序中的显示实例变量，这样当我们在程序中设置该变量时，标签的文本就会改变。

我们还有一个按钮标签，我们希望在它被按下时调用我们的 `ele1` 方法。该方法将 `display` 字段的值设为 1，因为变量将连接到标签，所以标签随后会更新。回顾一下，这是我们设置的序列：

1. 用户点击标记为 1 的按钮。
2. 此事件导致 `ele1` 方法被执行。
3. `ele1` 方法将实例变量 `display` 的 `text` 属性更改为字符串 "1"。
4. 因为 `UILabel` 对象 `display` 连接到 iPhone 窗口中的标签，该标签将更新为相应的文本值，即值 1。

为了让这个序列生效，我们只需要建立这两个连接。有几种方法可以实现，这里我们只描述一种方法。

首先，让我们在第三个面板中显示源代码。要做到这一点，首先选择 `View`、`Utilities`、`Hide Utilities`（隐藏工具栏）。接下来，选择 `View`、`Assistant Editor`、`Show Assistant Editor`（显示助手编辑器）。希望你的 Xcode 窗口与图 21.14 所示。

![](img/22d1310b7c22ea2d48cd2058929a5cda_476_0.png)

将按钮连接到 `IBAction` 方法 `ele1`。你可以通过在点击按钮时按住 `Control` 键，并拖动屏幕上出现的线条到最右侧面板中显示的 `ele1` 方法（你可以将其拖到在接口部分声明方法的地方，也可以拖到在实现部分定义方法的地方）。如图 21.15 所示。

现在，将 `display` 变量连接到标签。选择 iPhone 窗口中的标签，按住 `Control` 键并点击并拖动出现的蓝色线条，连接到接口文件中的 `display` 属性声明。如图 21.16 所示。

搞定！从 `Product` 菜单或工具栏中选择 `Run`（运行）。如果一切顺利，程序将成功构建并开始执行。当执行开始时，你的程序将加载到 iPhone 模拟器中，模拟器将出现在你的电脑上。模拟器窗口应该像本章开始时图 21.1 所示那样出现。你只需通过点击按钮即可在模拟器上模拟按下按钮。当你这样做时，我们概述的步骤序列和你建立的连接将导致在显示顶部显示一个 1，如图 21.2 所示。

## 一个 iPhone 分数计算器

下一个示例稍微复杂一些，但与上一个示例的概念同样适用。我们不会显示创建此示例的所有步骤，而是提供步骤的总结和设计方法论的概述。当然，我们将显示所有的代码。

首先，让我们看看应用程序是如何工作的。图 21.17 显示了应用程序在启动后在模拟器中的样子。

![](img/22d1310b7c22ea2d48cd2058929a5cda_478_0.png)

图 21.17 启动后的分数计算器

计算器允许你输入分数：首先输入分子，按下标记为 `Over` 的键，然后输入分母。要输入分数 2/5，你将按 2，然后按 `Over`，最后按 5。

> 注意
> 此计算器设计为仅执行两个分数之间的操作。我们在本章末留了一个练习供你消除此限制。

显示随着按键的按下不断更新。图 21.18 显示了输入 4/6 并按下乘法键后的显示。

图 21.19 显示了 4/6 和 2/8 相乘的结果。你会看到 1/6 表示结果约分。

### 开始 Fraction_Calculator 项目

对于这个第二个程序示例，你将首先创建一个新项目。像之前一样在 `New Project` 窗口中选择 `Single View Application`。将你的新项目命名为 `Fraction_Calculator`。

![](img/22d1310b7c22ea2d48cd2058929a5cda_479_0.png)

当项目被创建时，你会发现得到了两个模板。`Fraction_CalculatorAppDelegate.h` 和 `Fraction_CalculatorDelegate.m` 定义了项目的应用程序代理类，`Fraction_CalculatorViewController.h` 和 `Fraction_CalculatorViewController.m` 定义了项目的视图控制器类。与第一个示例一样，所有的工作都在这个类中完成。

### 定义视图控制器

现在，让我们为你的视图控制器编写代码。`Fraction_CalculatorViewController`。我们将从接口文件开始。程序 21.2所示。

#### 程序 21.2 Fraction_CalculatorViewController.h 接口文件

```objc
#import <UIKit/UIKit.h>

#import "Calculator.h"

@interface Fraction_CalculatorViewController : UI

@property (strong, nonatomic) UILabel *display;

-(void)processDigit:(int) digit;

-(void)processOp:(char) theOp;

-(void)storeFracPart;

// 数字键

-(IBAction) clickDigit:(UIButton *) sender;

// 术运算键

-(IBAction) clickPlus;

-(IBAction) clickMinus;

-(IBAction) clickMultiply;

-(IBAction) clickDivide;

// 杂键

-(IBAction) clickOver;

-(IBAction) clickEquals;

-(IBAction) clickClear;

@end
```

有一些用于构建分数的管理变量（`currentNumber`、`firstOperand` 和 `isNumerator`），以及用于构建显示字符串的变量（`displayString`）。还有一个 `Calculator` 对象（`myCalculator`），它可以执行两个分数之间的实际计算。我们将关联一个名为 `clickDigit` 的单一方法来处理 0-9 任意数字的按下。该方法将接收一个参数，即实际按下的数字，你稍后会看到。最后，我们定义了方法来处理要执行的操作（`clickPlus`、`clickMinus`、`clickMultiply`、`clickDivide`）、在按下键时执行实际计算（`clickEquals`）、清除当前操作（`clickClear`），以及按下键时分离分子分母（`clickOver`）。定义了几个方法（`processDigit`、`processOp` 和 `storeFracPart`）来辅助前面的章节。

程序 21.2 显示了此控制器类的实现文件。注意，我们可以在实现部分声明实例。两种方法都有效。我们使用的方法将实例变量保持为私有，并清楚它们它们是在类内部使用的。

#### 程序 21.2 Fraction_CalculatorViewController.m 实现文件

```objc
#import "Fraction_CalculatorViewController.h"

@implementation Fraction_CalculatorViewController
{
    int currentNumber;
    BOOL firstOperand, isNumerator;
    Calculator *myCalculator;
    MutableString *displayString;
}

- (void)viewDidLoad {
    // 启动后自定义的点
    firstOperand = YES;
    isNumerator = YES;
    displayString = [MutableString stringWithWithCapacity: 40];
    myCalculator = [[Calculator alloc] init];
}

- (void)processDigit:(int)digit {
    currentNumber = currentNumber * 10 + digit;
    [displayString appendString:[NSString stringWithFormat:@"%i", digit]];
    display.text = displayString;
}

-(IBAction) clickDigit:(UIButton *)sender {
    int digit = sender.tag;
    [self processDigit:digit];
}

-(void) processOp:(char) theOp {
    NSString *opStr;
    op = theOp;
    switch (theOp) {
        case '+':
            opStr = @"+";
            break;
        case '-':
            opStr = @"-";
            break;
        case '*':
            opStr = @"*";
            break;
        case '/':
            opStr = @"/";
            break;
    }
    [self storeFracPart];
    firstOperand = NO;
    isNumerator = YES;
    [displayString appendString:opStr];
    display.text = displayString;
}

-(void) storeFracPart {
    if (firstOperand) {
        if (isNumerator) {
            myCalculator.operand1.numerator = currentNumber;
            myCalculator.operand1.denominator = 1; // 例如 3 * 4/5
        } else {
            myCalculator.operand1.denominator = currentNumber;
        }
    } else {
        if (isNumerator) {
            myCalculator.operand2.numerator = currentNumber;
            myCalculator.operand2.denominator = 1; // 例如 3/2 * 4 =
        } else {
            myCalculator.operand2.denominator = currentNumber;
            firstOperand = YES;
        }
    }
    currentNumber = 0;
}

-(IBAction) clickOver {
    [self storeFracPart];
    isNumerator = NO;
    [display appendString:@"//"];
    display.text = displayString;
}

// 算术操作键
-(IBAction) clickPlus {
    [self processOp: '+'];
}

-(IBAction) clickMinus {
    [self processOp: '-'];
}

-(IBAction) clickMultiply {
    [self processOp: '*'];
}

-(IBAction) clickDivide {
    [self processOp: '//'];
}

// 其他键
-[IBAction] clickEquals {
    if (firstOperand == NO) {
        [self storeFracPart];
        [myCalculator performOperation:op];
        [displayString append:@""];
        [displayString append:[myCalculator.accumulator]];
        convertToString();
        display.text = displayString;
        currentNumber = 0;
        isNumerator = YES;
        firstOperand = YES;
    }
}
```



```objc
[displayString append:@""];
}

}

- (IBAction)clickClear {
    isNumerator = YES;
    firstOperand = YES;
    currentNumber = 0;
    [myCalculator clear];
    [displayString append:@""];
    display.text = displayString;
}
```

计算器的窗口仍然像上一个应用程序一样只包含一个标签，我们称其为 `display`。当用户逐个输入数字时，我们需要在此过程中构建数字。变量 `currentNumber` 存储正在进行中的数字，`BOOL` 变量 `firstOperand` 和 `isNumerator` 用于跟踪这是第一个操作数还是第二个操作数，以及用户当前正在输入操作数的分子还是分母。

当按下计算器上的数字按钮时，我们设置使得某些标识信息将传递给 `clickDigit:` 方法，以识别按下的是哪个数字按钮。这是通过在属性检查（Attributes Inspector）面板中设置按钮的 Tag 属性为每个数字按钮设置一个唯一值来实现。在这种情况下，我们希望将 tag 设置对应的数字。因此，标签为 0 的按钮 tag 设置为 0，标签为 1 的按钮 tag 设置为 1，依此类推。发送到 `clickDigit:` 方法的 `sender` 参数是 iPhone 窗口中实际按下的 `UIButton` 对象。通过访问该对象的属性，你可以获取按钮的 tag 值。这在 `clickDigit:` 方法中如所示完成：

```objc
- (IBAction)clickDigit:(UIButton *)sender {
    int digit = sender.tag;
    [self processDigit:digit];
}
```

程序 21.2 中的按钮比第一个应用程序多得多。控制器实现文件中的大部分复杂性围绕构建分数和显示它们展开。正如所指出的，当按下 0–9 数字按钮时，会执行动作 `clickDigit`。该方法调用 `processDigit:` 方法将数字附加到显示字符串上。

当按下按键时，会调用 `clickEquals` 方法来执行两个分数之间的操作，并将结果存储在它的累加器（accumulator）中。该累加器在 `clickEquals` 方法内部被获取，结果添加到显示器中。

# Fraction 类

`Fraction` 类与本文之前的示例相比很大程度上没有变化。新增了一个 `convertToString` 方法，用于将分数转换为等效字符串。程序 21.2 显示了 `Fraction` 接口，紧接着是相应的实现。

## 程序 21.2 Fraction.h

```objc
#import <UIKit/UIKit.h>

@interface Fraction : NSObject

@property int numerator, denominator;

- (void)print;
- (void)setTo:(int)n over:(int)d;
- (Fraction *)add:(Fraction *)f;
- (Fraction *)subtract:(Fraction *)f;
- (Fraction *)multiply:(Fraction *)f;
- (Fraction *)divide:(Fraction *)f;
- (void)reduce;
- (double)convertToNum;
- (NSString *)convertToString;

@end
```

## 程序 21.2 Fraction.m

```objc
#import "Fraction.h"

@implementation Fraction

- (void)setTo:(int)n over:(int)d {
    numerator = n;
    denominator = d;
}

- (void)print {
    NSLog("%i/%i", numerator, denominator);
}

- (double)convertToNum {
    if (denominator != 0)
        return (double)numerator / denominator;
    else
        return NAN;
}

- (NSString *)convertToString {
    if (numerator == denominator) {
        if (numerator == 0)
            return @"0";
        else
            return @"1";
    } else if (denominator == 1) {
        return [NSString stringWithFormat:@"%i", numerator];
    }
    return nil;
}

- (Fraction *)add:(Fraction *)f {
    // 相加两个分数：
    // a/b + c/d = ((a*d) + (b*c)) / (b * d)
    // result 将存储加法结果
    Fraction *result = [[Fraction alloc] init];
    result.numerator = numerator * f.denominator + denominator * f.numerator;
    result.denominator = denominator * f.denominator;
    [result reduce];
    return result;
}

- (Fraction *)multiply:(Fraction *)f {
    Fraction *result = [[Fraction alloc] init];
    result.numerator = numerator * f.numerator;
    result.denominator = denominator * f.denominator;
    [result reduce];
    return result;
}

- (Fraction *)divide:(Fraction *)f {
    Fraction *result = [[Fraction alloc] init];
    result.numerator = numerator * f.denominator;
    result.denominator = denominator * f.numerator;
    [result reduce];
    return result;
}

- (void)reduce {
    int u = numerator;
    int v = denominator;
    int temp;
    if (u == 0)
        return;
    else if (u < 0)
        u = -u;
    while (v != 0) {
        temp = u % v;
        u = v;
        v = temp;
    }
    numerator /= u;
    denominator /= u;
}

@end
```

`convertToString` 方法检查分数的分子和分母，以产生更具可读性的结果。如果分子和分母相等（但不为零），我们返回 `@"1"`。如果分子为零，则字符串中不需要显示分母。

# 一个 iPhone 分数计算器

回想在 `convertToString` 中使用的 `stringWithFormat` 方法：它根据格式字符串（类似于 `NSLog`）和一个用逗号分隔的参数列表返回一个字符串。你将参数传递给接受可变参数的方法，并用逗号分隔它们，就像你将参数传递给 `NSLog` 函数时做的那样。

# 处理分数的计算器类

接下来，是时候查看 `Calculator` 类了。概念与我们在书中之前开发的同名类相似。但在此情况下，我们的计算器必须知道如何处理分数。以下是我们新的 `Calculator` 类接口和实现文件。

## 程序 21.2 Calculator.h

```objc
#import <UIKit/UIKit.h>
#import "Fraction.h"

@interface Calculator : NSObject

@property (strong, nonatomic) Fraction *operand1, *operand2, *accumulator;

- (Fraction *)performOperation:(char)op;
- (void)clear;

@end
```

## 程序 21.2 Calculator.m

```objc
#import "Calculator.h"

@implementation Calculator

@synthesize operand1, operand2, accumulator;

- (id)init {
    if (self) {
        operand1 = [[Fraction alloc] init];
        operand2 = [[Fraction alloc] init];
        accumulator = [[Fraction alloc] init];
    }
    return self;
}

- (void)clear {
    accumulator.numerator = 0;
    accumulator.denominator = 0;
}

- (Fraction *)performOperation:(char)op {
    Fraction *result;
    switch (op) {
        case '+':
            result = [operand1 add:operand2];
            break;
        case '-':
            result = [operand1 subtract:operand2];
            break;
        case '*':
            result = [operand1 multiply:operand2];
            break;
        case '/':
            result = [operand1 divide:operand2];
            break;
    }
    accumulator.numerator = result.numerator;
    accumulator.denominator = result.denominator;
    return accumulator;
}

@end
```



# 设计 UI

将你在视图中布局的每个数字按钮连接到 `selectDigit:` 方法。通过依次 Control-点击并拖拽每个按钮到 `selectDigit:` 方法来实现此操作。在你的视图控制器的接口或实现文件中执行任一操作即可。此外，对于每个数字按钮，在检查器中将 `Tag` 值设置为与按钮标题相对应的数字。例如，对于标签为 0 的数字按钮，将 `Tag` 设为 0；对于标签为 1 的数字按钮，将 `Tag` 设为 1，以此类推。

在 View 窗口中绘制剩余按钮并建立相应的连接。大功告成！你的接口设计完成，分数计算器应用已准备好运行。

# 总结

图 21.20 显示了项目窗口，你可以看到所有与分数计算器项目相关的文件。

![](img/22d1310b7c22ea2d48cd2058929a5cda_491_0.png)

图 21.20 分数计算器项目文件。

以下总结了你创建 iPhone 分数计算器应用所遵循的步骤：

1. 创建了一个新的 SingleView Application（单视图应用）。
2. 将你的 UI 代码输入 `Fraction_CalculatorViewController.h` 和 `.m` 文件。
3. 将 `Fraction` 和 `Calculator` 类添加到项目中。
4. 打开 `Fraction_CalculatorViewController.xib` 来创建 UI。
5. 设置了 View 窗口的背景。
6. 创建了标签和按钮，并将它们放置在 View 窗口内。
7. 从 View 窗口中创建的标签 Control-点击拖拽到 `ILabel` Outlet 属性显示上。
8. 之前 Control-点击并拖拽 View 窗口中的每个数字到相应的 `IBAction` 方法。对于每个数字，你选择了 `selectDigit:` 并设置了相应的数字 0-9，以便 `selectDigit:` 方法能够识别按下的是哪个按钮。

学习如何使用视图控制器是一次很有意义的练习，尽管这比在代理中完成所有工作要麻烦。希望这段关于开发应用的简要介绍能为你编写自己的应用提供良好的开始。我们的计算器应用有几个局限性，其中许多在随后的练习中得到了解决。

## 练习

1. 添加一个“转换为分数”的功能。当按下按钮时，使用 `Fraction` 类的 `convertTo` 方法产生结果的数值表示。将该结果转换为字符串并显示在屏幕上。
2. 修改计算器，使得如果在输入分子之前按了 `-` 键，可以输入负分数。
3. 在分数应用中显示错误，以便进行链式计算。例如，允许输入以下操作：`1/5 + 2/7 - 3/8 =`。
4. 你可以为应用添加一个图标，该图标将出现在 iPhone 的主屏幕上。这可以通过如 21.6 所示将其拖到 App Icons 部分来实现。对于普通尺寸（iPhone 3GS 及更早机型），图标尺寸应为 57x57 像素。对于 Retina 屏幕 iPhone（4 及后续机型），图标图像应该是 114x114 像素。
5. 使用你自己的图片为计算器的按钮提供自定义外观。你首先将图像添加到项目中（拖入左侧窗格）。然后，在检查器窗口中将按钮类型设置为 Custom（自定义），并将 Image 设置为你拷贝项目的文件。
6. 在互联网上找到一个合适的计算器图像进行使用，并设置计算器使用该图像作为图标。该计算器可以在 Store 免费获取，源代码发布在本书的论坛上（classroomM.com/objective-c）。

![](img/22d1310b7c22ea2d48cd2058929a5cda_493_0.png)

图 21.21 带自定义按钮的分数计算器

# 附录 A

# 术语表

附录为你遇到的许多术语提供了非正式定义。这些术语一些与 Objective-C 语言直接相关，另一些源于面向对象编程领域。对于后者，我提供了该术语专门适用于 Objective-C 语言的含义。

**abstract class** 为了创建子类而定义的类。实例是从子类创建的，而不是抽象类。*另参见 concrete subclass。*

**accessor method** 获取或设置实例变量值的方法。使用访问器方法设置和检索实例变量的值符合数据封装的方法论。

**Application Kit** 一个用于开发应用程序用户界面的框架，包含了菜单、工具栏和窗口等对象。它是 Cocoa 的一部分，更常被称为 AppKit。

**ARC** *参见 Automatic Reference Counting*

**archiving** 将对象数据的表示形式转换为以后可以恢复（反归档）的格式。

**array（数组）** 一个值的有序集合。数组可以被定义为基础的 Objective-C 类型，并在 Foundation 中通过 `NSArray` 和 `NSMutableArray` 类实现为对象。

**Automatic Reference Counting (ARC 自动引用计数）** Xcode 4.2 中引入的一项功能，由编译器管理与对象相关的内存。在 Xcode 4.2 之前，iOS 程序员需要使用手动技术来管理内存。这需要使用 `retain`、`autorelease` 和 `dealloc` 方法。

**automatic variable（自动变量）** 一种在进入和退出语句时自动分配和释放的变量。自动变量的作用范围局限于定义它的块，且没有默认值。其前面可选地加上关键字。

**autorelease pool（自动释放池）** 在 ARC 出现之前，这种对象是由 `NSAutoreleasePool` 管理的。现在它通过 `@autoreleasepool` 指令实现。自动释放池跟踪系统目标释放的对象。对于 iOS 和 Cocoa 应用程序，通常在运行循环结束时处理。

**bitfield（位域）** 包含一个或多个特定宽度字段的结构。位域可以像其他结构成员一样被访问和操作。

**block（块）** Apple 公司为 C 语言添加的扩展。块具有类似函数的语法，在定义时捕获作用范围内变量的值，并可以赋值给变量或作为方法或函数的参数传递。块可以高效地分发到另一个线程或处理器上执行。

**category（分类）** 一组在指定名称下归类的方法。分类可以对类的方法定义进行模块化，并可用于向现有类添加新方法。

**char string（字符字符串）** 一个以空字符终止的字符序列。

**class（类）** 变量和方法的实例，这些实例可以访问相应的变量。在定义一个类之后，就可以创建该类的实例（即对象）。

**class method（类方法）** 一种在类对象上调用的方法（用 `+` 符号定义）。参见 *instance method*（实例方法）。

**class object（类对象）** 一个标识特定类的对象。类名可以作为消息的接收者，以调用类方法。在其他地方，可以在类上调用类方法来创建一个类对象。

**cluster（簇）** 一个定义一组具体子类的抽象类，通过该抽象类向用户提供接口。

**Cocoa** 一个由 Foundation、Core Data 和 Application Kit 框架组成的开发环境。

**Cocoa Touch** 一个由 Foundation、Core Data 和 UIKit 框架组成的开发环境。

**collection（集合）** 一种 Foundation 框架对象，可以是数组、字典或集合，用于分组和操作相关对象。

**compile time（编译时间）** 源代码被分析并转换为称为对象代码的低级格式的时间。

**directive（指令）** 在 Objective-C 中，一种以 `@` 开头的特殊结构。`@interface`、`@implementation`、`@end` 和 `@class` 是指令的示例。

**composite class（复合类）** 一个由其他类的对象组成的类；它用作子类的替代方案。

**Distributed Objects（分布式对象）** 一个应用程序中的 Foundation 对象与另一个应用程序中的 Foundation 对象通信的能力，后者可能运行在另一台机器上。

**concrete subclass（具体子类）** 抽象类的子类。可以从子类中创建实例。

**dynamic binding（动态绑定）** 在运行时而不是编译时确定要对对象调用的方法。

**conform（遵循）** 如果一个类采用了协议中所有要求的方法（直接采用或通过继承间接采用），则该类遵循该协议。

**dynamic type（动态类型）** 在运行时而不是编译时确定对象所属的类。参见也见 *static typing*（静态类型）。

**constant character string（常量字符字符串）** 由双引号括围的字符序列。如果前面加上 `@`，它定义了一个类型为 `NSString` 的常量字符串类型。

**encapsulation（封装）** 参见 *data encapsulation*。

**data encapsulation（数据封装）** 对象的数据存储在它的实例变量中，并仅通过对象的方法访问。这维护了数据的完整性。

**external variable（外部变量）** 参见 *global variable*（全局变量）。

**factory method（工厂方法）** 参见 *class method*（类方法）。

**factory object（工厂对象）** 参见 *class object*（类对象）。

**formal protocol（正式协议）** 一组在 `@protocol` 声明的名称下的相关方法。不同的类（不一定）可以通过继承采用来实现其所有要求的方法。参见也见 *informal protocol*（非正式协议）。

**delegate（代理）** 一个被指向由另一个对象执行动作的对象。

**forwarding（转发）** 将消息及其相关参数发送到另一个方法执行的过程。

**designated initializer（指定初始化器）** 类中所有初始化方法（或子类中通过向父类发送消息）都会调用的方法。

**dictionary（字典）** 一种在 Foundation 下通过 `NSDictionary` 和 `NSMutableDictionary` 类实现的键值对集合。

**Foundation framework（Foundation 框架）** 一组类、函数和协议，它们构成了应用程序开发的基础，提供了基本设施，如内存管理、文件和 URL 访问、归档任务以及处理集合、字符串、数字和日期对象的操作。

**framework（框架）** 一组相互相关的类、函数、协议、文档、头文件和其他资源的集合。例如，Cocoa 框架被用于在 Mac OS X 下开发交互式图形应用程序。

**header file（头文件）** 一个包含常用定义、宏和变量声明的文件，通过 `#import` 或 `#include` 语句包含在程序中。

**function（函数）** 一个由名称标识的语句块，它可以接受一个或多个通过值传递传递的参数，并可选地返回一个值。函数可以是定义所在文件的本地（静态）的，也可以是全局的，在这种情况下，可以从其他文件中定义的方法或函数中调用。

**id** 一个可以持有任何类型对象指针的通用类型。

**immutable object（不可变对象）** 一个值不能被修改的对象。Foundation 框架的示例包括 `NSString`、`NSDictionary` 和 `NSArray` 对象。对应的 *mutable object*（可变对象）。

**garbage collection（垃圾回收）** 一种自动释放未引用对象所用内存的运行时管理系统。iOS 运行时不支持垃圾回收。

**implementation section（实现部分）** 类定义中的部分，包含了类中声明的方法的代码（即实现部分）。

**interface section（接口部分）** 类定义中的部分，包含了类的实例变量和方法的声明。

**informal protocol（非正式协议）** 一组在分类声明的名称下的相关方法。不同的类（不一定）可以通过继承采用来实现其所有要求的方法。参见也见 *formal protocol*。

**inheritance（继承）** 从类向子类传递方法和实例变量的过程。

**getter（get 方法）** 获取实例变量值的方法。参见 *setter method*（set 方法）。

**Instance（实例）** 类的具体表示。通过向类发送 `alloc` 或 `new` 消息创建。

**instance method（实例方法）** 属于实例的方法。参见也见 *class method*（类方法）。

**instance variable（实例变量）** 定义在接口部分的变量。实例方法可以直接访问实例变量。

**mutable object（可变对象）** 一个值可以被改变的对象。Foundation 框架支持可变和不可变的数组、集合、字符串和字典。

**internationalization（国际化）** 也见 *localization*（本地化）。

**isa** 所有对象继承的特殊变量。用于运行时标识对象所属的类。

**nil** 类型为 *id* 的对象，用于表示无效对象。其值定义为 0。`nil` 可以接收消息。

**notification（通知）** 向已注册在特定事件发生时发送消息的过程。

**linking（链接）** 将一个或多个文件转换为可执行程序的过程。

**NSObject** Foundation 框架下的根对象。

**local variable（局部变量）** 作用范围局限于定义它的块的变量。可以是类、方法或语句局部的。

**null character（空字符）** 值为 0 的字符。空字符常量表示为 `\0`。

**localization（本地化）** 使程序适用于特定地理区域执行的过程，通过将消息翻译成本地语言并处理时间、货币符号、日期格式等问题。*Localization* 指语言翻译，而术语 *internationalization*（国际化）是指该过程的其他部分。

**null pointer（空指针）** 无效的指针值，通常定义为 0。

**object（对象）** 一组变量和关联的方法。可以向对象发送消息，以执行其方法之一。

**object-oriented programming（面向对象编程）** 一种基于类和对象的编程方法，并对这些对象执行操作。

**message（消息）** 发送给对象（接收者）的方法及其参数。

**message expression（消息表达式）** 在方括号内的表达式，指定对象（接收者）和发送给该对象的消息。

**parent class（父类）** 另一个类继承的类。也被称为 *super class*（超类）。

**pointer** 一个引用另一个对象或数据类型的值。指针实现为内存中特定对象或值的地址。类的实例是指向内存中对象数据位置的指针。

**receiver** 接收消息的对象。在被调用的方法内部，可以将接收者称为 `self`。

**reference count** 引用计数。参见 retain count。

**retain count** 保留计数，对象被引用的次数计数。通过向对象发送 `retain` 消息来增加，通过向其发送 `release` 消息来减少。

**polymorphism** 来自不同类的对象接受相同消息的能力。

**preprocessor** 预处理器对源代码进行第一轮扫描的程序，处理以 `#` 开头的行，这些行可能包含预处理器语句。常见用途包括使用 `#define` 定义宏，使用 `#import` 和 `#include` 包含其他源文件，以及使用 `#if`、`#ifdef` 和 `#endif` 条件地包含源文件。

**root object** 继承层次结构中没有父类的顶层对象。

**runtime** 程序执行时所需的时间；也是负责执行程序指令的机制。

**selector** 用于选择方法的名称，以引用消息的接收者。编译后的选择器类型为 `SEL`，可以使用 `@selector` 指令生成。

**procedural programming** 过程化编程，一种通过操作一组数据的过程和函数定义程序的语言。

**self** 方法内部用于引用该对象的变量。

**property declaration** 属性声明为变量指定属性的方法，允许类为实例变量生成无内存且线程安全的访问器方法。属性声明还可以用于为运行时动态加载的访问器方法声明属性。

**set** 一个在 Foundation 下实现的唯一对象无序集合，使用 `NSSet`、`NSMutableSet` 和 `NSCountedSet` 实现。

**setter method** 设置实例变量值的方法。参见 *accessor method*。

**property list** 属性列表，一种以标准格式表示对象类型的方法。属性列表通常存储在 XML 格式中。

**statement** 语句以分号终止的一个或多个表达式。

**statement block** 括在大括号中的一个或多个语句。可以在语句块内声明局部变量，其作用范围局限于该块。

**protocol** 一个类必须实现或采纳的方法列表。协议提供了一种跨类标准化接口的方法。参见 formal protocol（正式协议）和 informal protocol（非正式协议）。

**static function** 使用 `static` 关键字声明的函数，只能由同一源文件中定义的其他函数或方法调用。

**Unicode character** 一种表示多达百万个字符集合的标准。`NSString` 和 `NSMutableString` 类处理 Unicode 字符字符串。

**static typing** 静态类型，在编译时显式定义对象所属的类。参见 dynamic typing。

**union** 一种聚合数据类型，例如包含共享相同存储区域成员的结构。在任何时刻，只有一个成员可以占据该存储区域。

**static variable** 作用范围限于其定义边界或模块的变量。静态变量具有默认值 0，并在方法或函数调用期间保持其值。

**Xcode** 用于 Mac OS 和 iOS 程序开发的编译和调试工具。

**structure** 一种可以包含不同类型成员的聚合数据类型。结构可以作为参数传递给函数和方法，也可以作为返回值。

**XML** 可扩展标记语言。Mac OS X 上生成的属性列表的默认格式。

**subclass** 也称为子类，子类继承父类或超类的方法和实例变量。

**zone** 用于分配数据和对象的指定内存区域。程序可以处理多个区域来更高效地管理内存。

**super** 方法中用于引用接收者类的关键字。

**super class** 特定类的父类。参见 super。

**synthesized method** 编译器为你创建的 setter 或 getter 方法。它被添加到 Objective-C 2.0 语言中。

**UIKit** 用于开发 iOS 设备应用程序的框架。除了提供处理常用 UI 元素（窗口、按钮和标签）的类外，它定义了处理设备特定功能（如加速度计和触摸界面）的类。UIKit 是 Cocoa Touch 的一部分。

# Appendix B
通讯录示例源代码

为了方便参考，这里是你在第二部分“Foundation 框架”中一直使用的通讯录示例的完整接口和实现文件。这包含了 `AddressCard` 和 `AddressBook` 类的定义。你应该在你的系统上实现这些类；然后扩展类定义以使其更实用、更强大。这是你学习语言并熟悉构建程序、处理类和对象以及使用 Foundation 框架的极佳方法。

### AddressCard 接口文件

```
```



# Appendix B 通讯录示例源代码

## AddressCard 接口文件

```objc
#import <Foundation/Foundation.h>

@interface AddressCard : NSObject <NSCopying, NSCoding>

@property (nonatomic, copy) NSString *name, *email;

- (void)setName:(NSString *)name andEmail:(NSString *)theEmail;
- (void)assignName:(NSString *)name andEmail:(NSString *)theEmail;
- (NSComparisonResult)compareNames:(id)element;

@end
```

## AddressBook 接口文件

```objc
#import <Foundation/Foundation.h>
#import "AddressCard.h"

@interface AddressBook : NSObject <NSCopying, NSCoding>

@property (nonatomic, copy) NSString *bookName;
@property (nonatomic, strong) NSMutableArray *book;

- (id)initWithName:(NSString *)name;
- (void)sort;
- (void)addCard:(AddressCard *)theCard;
- (void)removeCard:(AddressCard *)theCard;
- (NSInteger)entries;
- (void)list;
- (AddressCard *)lookup:(NSString *)theName;

@end
```

## AddressCard 实现文件

```objc
#import "AddressCard.h"

@implementation AddressCard

@synthesize name, email;

- (void)setName:(NSString *)name andEmail:(NSString *)theEmail {
    name = name;
    email = theEmail;
}

- (void)assignName:(NSString *)name andEmail:(NSString *)theEmail {
    name = name;
    email = theEmail;
}

- (NSComparisonResult)compareNames:(id)element {
    return [name compare:[element name]];
}

- (id)copyWithZone:(NSZone *)zone {
    id newCard = [[self class] allocWithZone:zone init];
    [newCard assignName:name andEmail:email];
    return newCard;
}

- (void)encodeWithCoder:(NSCoder *)encoder {
    [encoder encodeObject:name forKey:@"AddressName"];
    [encoder encodeObject:email forKey:@"AddressEmail"];
}

- (id)initWithCoder:(NSCoder *)decoder {
    self = [super init];
    if (self) {
        name = [decoder decodeObjectForKey:@"AddressName"];
        email = [decoder decodeObjectForKey:@"AddressEmail"];
    }
    return self;
}

@end
```

## AddressBook 实现文件

```objc
#import "AddressBook.h"

@implementation AddressBook

@synthesize book, bookName;

- (id)initWithName:(NSString *)name {
    self = [super init];
    if (self) {
        bookName = [NSString stringWithString:name];
        book = [NSMutableArray array];
    }
    return self;
}

- (id)init {
    return [self initWithName:@"Unnamed Book"];
}

- (void)sort {
    [book sortUsingSelector:@selector(compareNames)];
}

- (void)sort2 {
    [book sortUsingComparator:^NSComparisonResult(id obj1, id obj2) {
        return [[obj1 name] compare:[obj2 name]];
    }];
}

- (void)addCard:(AddressCard *)theCard {
    [book addObject:theCard];
}

- (void)removeCard:(AddressCard *)theCard {
    [book removeObjectIdenticalTo:theCard];
}

- (NSInteger)entries {
    return [book count];
}

- (void)list {
    NSLog(@"==================== Contents of: %@ =====", bookName);
    for (AddressCard *card in book) {
        NSLog(@"%-20s %-32s", [card.name UTF8String], [card.email UTF8String]);
    }
    NSLog(@"====================================================");
}

// 通过名称查找地址卡 - 假设完全匹配
- (AddressCard *)lookup:(NSString *)theName {
    for (AddressCard *nextCard in book) {
        if ([nextCard.name caseInsensitiveCompare:theName] == NSOrderedSame) {
            return nextCard;
        }
    }
    return nil;
}

- (void)encodeWithCoder:(NSCoder *)encoder {
    [encoder encodeObject:bookName forKey:@"AddressBookName"];
    [encoder encodeObject:book forKey:@"AddressBook"];
}

- (id)initWithCoder:(NSCoder *)decoder {
    self = [super init];
    if (self) {
        bookName = [decoder decodeObjectForKey:@"AddressBookName"];
        book = [decoder decodeObjectForKey:@"AddressBook"];
    }
    return self;
}

// NSCopying 协议方法
- (id)copyWithZone:(NSZone *)zone {
    id newBook = [[self class] allocWithZone:zone init];
    [newBook setBookName:bookName];
    // 以下将对地址簿进行浅拷贝
    [newBook setBook:book];
    return newBook;
}

@end
```



# 索引

# 符号

- `&` (与符号)
  - 地址运算符, 274–275
  - 按位与运算符, 211–213
- `&&` (逻辑与运算符), 101
- `=` (赋值运算符), 64
- `*` (星号)
  - 算术表达式, 55
  - 方向运算符, 274–275
  - 对象引用, 41–42
- `@` (at 符号), 21
- `^` (脱字符)
  - blocks, 263
  - 异或运算符, 211, 214
- `%` 字符, 24
- `:` (冒号)
  - 条件运算符, 122
  - 方法, 37
- `,` (逗号运算符), 294–295
- `//` (注释), 20
- `/* */` (注释), 20
- `}` (大括号), 21
- `--` (自减运算符), 78
  - 数组指针, 282–284
  - 前置/后置, 287–289
- `/` (除法运算符), 55
- `.` (点运算符), 134–135
- `==` (等于运算符), 74
- `>` (大于运算符), 74
- `>=` (大于或等于运算符), 74
- `++` (自增运算符), 77
  - 数组指针, 282–284
  - 前置/后置, 287–289
- `<<` (左移运算符), 211, 216
- `<` (小于运算符), 74
- `<=` (小于或等于运算符), 74
- `-=` (减等赋值运算符), 64
- `-` (减号)
  - 算术表达式, 55
  - 方法, 35
- `Foundation` 框架
  - 文档, 304
- 实例变量, 45–48
  - 继承的, 198
- 创建方法, 45–48
- set/getters, 48
- 算术表达式, 55
- 方法, 35
- `%` (取模运算符), 60–61
- `\` (换行符), 22
- `!=` (不等于运算符), 74
- 属性, 134–135
  - 来自 blocks 的变量, 263–265
- `~` (补码运算符), 211, 214–215
- 访问方法
  - setters/getters, 48
  - 合成, 200
- `||` (逻辑或运算符), 101
- `|` (按位包含或运算符), 211, 213–214
- `AddressClass`, 334–337
  - 显示属性, 454–455
  - 合成指令, 123–138
- `add:` 方法
  - 向消息接收者添加消息参数, 138
  - 分数加法测试程序, 138–139
  - `Fraction` 类对象引用, 137–138
- `+=` (加等赋值运算符), 64
- `#` (井号), 233
- `?` (问号), 条件运算符, 122
- 引用, 138
- 结果对象, 146–148
- `self` 关键字, 145
- `>>` (右移运算符), 211, 216–217
- `;` (分号), 21
- `->` (结构体指针运算符), 278
- `~` (波浪号), 主目录, 370
- `_` (下划线), 200
- `addCard:` 方法, 339
- 加法运算符, 55
- 加法程序, 23
- 地址簿, 创建
- `addObject:` 方法, 330, 352, 360, 362
- 地址卡
  - 添加, 339
  - 计数, 339
  - 创建, 331
  - 10 个对象, 328–329
  - 应用程序, 495
  - 删除, 344–347
  - 邮箱, 332
  - 持有, 337
  - 名称, 332
  - 名称和邮箱, 一次设置, 335–337
  - 数量, 报告, 337
  - 打印, 333
  - 使用 blocks 排序, 350–351
  - 使用 selectors 排序, 347–350
  - 合成, 334–337
  - 测试程序, 333
- `AddressCard` 类, 331
  - 内容, 337
  - 自定义存档, 创建, 336–337
  - 恢复, 338–339
  - 解码, 430
  - 编码, 430
- 地址簿名称, 存储, 337–338
- 删除, 344–347
- 查找, 341–344
- 视图, 330–331
- 程序, 339–341
- 序列化, 339
- 地址运算符 (`&`), 274, 275
- `AddressBook` 类
  - 实现文件, 338–339
  - `addCard:`, 339
  - 定义, 331
  - 实现文件, 331–332
  - 接口文件
    - 访问方法, 合成, 334–337
    - `compareNames:`, 348–350
    - `encodeWithCoder:`, 431
    - `print`, 333
    - `removeCard:`, 344–347
    - `setEmail:`, 332
    - `setName:`, 332
    - `setNameEmail:`, 335–337
  - 测试程序, 333–334
- `allKeys` 方法, 357
- `alloc` 方法, 40, 155, 309
- 分配对象, 39–40, 146
- 类比符号, 252–253
- `AND` 运算符 (`&`), 101
- Objective-C 编程更有趣！程序, 22
- `anyObject` 方法, 361
- `appendString:` 方法, 323, 326
- Apple
  - 获取
  - 开发者网站, 447
  - iOS. 参见 iOS
  - iPhone. 参见应用程序
- `Application Kit` 框架, 303
- `Application Services`, 444
- 应用程序包, 396–397
- 层级, 444
  - `Application Services`, 444
  - `Core Services`, 443
  - 内核, 443
- iPhone. 参见应用程序
- `count`, 339
- `entries`, 339
- `initWithName:`, 341–344
- `lookup:`, 339
- `sortUsingSelector:`, 347–350
- 接口文件, 337–338
- 程序, 339–341

# ARC (自动引用计数)

- `ARC` (自动引用计数), 41, 310, 408
- 非 ARC 编译代码, 411
- 变量, 409
- `rootObject:ToFile:` 方法, 428
- 存档对象
  - 自定义存档
    - 地址簿程序, 436–337
    - 完成存档过程, 337
    - 编码消息, 存储, 437
    - 可变数据区域, 创建, 336
    - 对象, 337
    - 恢复数据, 338–339
    - 写入文件, 438
  - 解码
    - 地址簿示例程序, 430–431
    - 数据类型, 430, 334–336
    - 方法, 430
    - 过程, 432
    - 测试程序, 433–434
    - 深拷贝, 创建, 339–441
  - 编码, 430
    - 地址簿示例程序, 430–431
    - 数据类型, 430, 334–336
    - 方法, 430
    - 过程, 431
    - 测试程序, 432–433
  - 键存档, 427
    - 创建, 428
    - 定义, 428
    - 恢复, 428–429
  - 支持, 428
  - 序列化存档, 428
  - XML 列表, 425
    - 创建, 425–427
    - 运行, 427
  - 写入, 427
- 赋值给其他变量, 248
- 字符, 251–252
- 声明, 249
- 定义, 248
- 元素，起始, 248
- 快速枚举, 339
- 斐波那契数字程序, 249–250
- 定义, 281
- 第一个元素，设置, 281
- 指针函数引用, 284
- 求和函数, 283–284
- 整数数组程序, 283–284
- 自增/自减运算符, 282
- 遍历数组, 281–284
- 序列化遍历, 248–249
- 下标, 248
- 值，存储, 248
- `Foundation`
  - 10 个对象程序, 328–329
  - 地址簿, 创建。参见地址簿, 创建
  - 创建 328
  - 数据类型转换对象, 353–354
  - 部署, 237–330
  - 月份名称程序, 327–328
  - 可变的，创建, 330
  - 对象，在末尾添加, 330
  - 概述, 327
  - 通过索引获取元素数字, 328
  - 排序方法, 352
  - 使用 blocks 排序, 350–351
  - 使用 selectors 排序, 347–350
- `arraySum` 函数, 283–284
- `arrayWithCapacity:` 方法, 352
- `arrayWithObjects:` 方法, 328, 351
- 赋值运算符 (`=`), 64
- 星号 (`*`)
  - 算术表达式, 55
  - 对象引用, 41–42
- at 符号 (`@`), 21
- 属性
  - 字典, 372
  - 标签, 458
- `attributesOfItemAtPath:` 方法, 371–372, 374

# 自动局部变量

- 自动局部变量, 257
- 自动引用计数 (`Automatic Reference Counting`)。查看 `ARC`
- 自动释放池 (`autorelease pools`), 403–405
  - 块 (`blocks`), 410–411
  - 定义, 21
  - 释放 (`draining`), 403
  - 主例程序示例, 404
  - 对象
    - 添加, 403
    - 自动释放的, 404–405
    - 拥有的，释放的, 404
    - 释放后的生存, 405–407
- `availableData` 方法, 390

# B

- 二进制表示法, 212
- 位运算符
  - 与 (`AND`), 212–213
- 二进制/十六进制表示
  - 转换, 212
  - 异或 (`Exclusive-OR`), 214
  - 包含或 (`Inclusive-OR`), 213–354
  - 左移, 216
  - 列表, 211
  - 补码 (`ones complement`), 214–385
  - 程序示例, 215–216
  - 右移, 216–217
- 位与运算符 (`&`), 211–213
- 空格（表达式）, 103
- 块 (`blocks`)
  - 优势, 262
  - 数组，排序, 350–351
  - 自动释放池, 410–411
  - 全局性定义, 263
  - 概述, 262
  - 语法, 262–263
  - 变量
    - 访问, 263–265
    - 赋值, 263
    - 值，编辑, 265–266
- 布尔变量 (`Boolean variables`), 121–122
- `BOOL` 数据类型, 121–122
  - 定义, 119
  - 质数表，创建, 118–119
  - 真假值, 119–121
- `break` 语句 (`break statements`)
  - 循环, 90
  - `switch` 语句, 115
- 缓冲区 (`buffers`), 375–376
- 包 (`bundles`), 396–397
- 按钮接口 (`buttons interfaces`)
  - 动作，添加, 460
  - 添加, 459

# C

- `.c` 文件扩展名, 14
- C 编程语言
  - 创建, 1
  - Objective-C 比较, 2
- C 目录, 385
- `calculate:` 方法, 141
- `calculateTriangularNumber`, 255–257
- `Calculator` 类 (`Calculator class`)
  - 定义, 65–67
  - 分数计算器应用程序, 473–474
  - 数字运算符，数字表达式程序, 109–112
- 驼峰命名法 (`camelCase`), 411
- `capitalizedString` 方法, 326

# 类 (`classes`) 499

- 脱字符 (`^`), 263
- 指针, 275–277, 285–286
- 块 (`blocks`), 263
- 字符串对象，删除, 323
- 异或运算符 (`Exclusive-OR operator`), 211, 224
- Unicode, 312
- 大小写敏感, 19
- `charPtr` 指针, 275–277
- 类名, 33
- 选择
  - 转换宏, 239
  - `define` 语句, 235
  - 命名, 135
  - 命名, 34
  - 对象, 155–156
- `caseInsensitiveCompare:` `nsstring` 方法, 325
- 圆面积/周长示例, 234-235
- `catch` 指令 (`catch directive`), 191
- `class` 指令 (`class directive`), 161–162
- 分类 (`categories`)
  - 类
    - 抽象, 173–174
    - 定义, 218
    - 访问器方法，合成, 120–133
    - 实现文件, 221
    - `AddressBook`
    - 接口文件, 220
    - `count` 方法, 339
    - 继承, 225
    - 实现文件, 338–339
    - `MathOps`, 221–224
    - `initWithMethod`, 339
    - `NSComparisonMethods`, 229
    - 接口文件, 337–338
    - 对象/分类命名对, 225
    - `lookup:` 方法, 341–344
    - 覆盖方法, 225
    - 程序, 339–341
    - 协议，采纳, 225
    - `sortUsingSelector:` 方法, 347–350
    - 无名。查看类扩展 (`classes, extensions`)
- `AddressCard`
  - 访问器方法，合成, 334–337
  - `CGPoint` 结构体, 270
  - `compareNames:` 方法, 348–350
  - `CGRect` 方法, 353
  - 定义, 331
  - `CGRect` 结构体, 270
  - `encodeWithCoder:`, 431
  - `CGSize` 方法, 353
  - `CGSize` 结构体, 270
  - 接口文件, 331
  - `changeCurrentDirectory:` 方法, 376
  - `print` 方法, 333
  - 字符数组, 251–252
  - `characterAtIndex:` i, 325
  - `setItem:` 方法, 332
  - `setName:` 方法, 332
  - `setName:andEmail:` 方法, 335–337
  - 分析程序, 107–109
  - 定义, 51
  - 概述, 52
  - 测试程序, 333–334
- `Calculator`
  - 定义, 65–67
  - 分数计算器应用程序, 473–474
  - 数字运算符，数字表达式程序, 109–112
- `Calculator`, 464–469
  - 分数计算器应用程序, 473–474
  - 数字运算符，数字表达式程序, 109–112
- `Complex`, 177–180
  - 定义, 130–131
  - 扩展, 148
  - 示例, 224–225
  - `Drawing` 协议, 227
  - `IBAction`, 454
  - `IBOutlet`, 454
  - 继承, 224
  - 扩展, 225
  - `class` 指令, 161–162
  - `add:` 方法, 137–138
  - 添加分数, 138–139
  - `calculate:` 方法, 141
  - 拷贝对象, 420
  - 拷贝分数, 419–420
  - `convertToNum` 方法, 95
  - 声明, 129–130
  - 方法，添加, 156–158
  - 方法，覆盖, 169–173
  - 对象方法，选择, 155–156
  - 对象，拥有的, 165
  - 父类方法, 154–155
  - 初始化, 197–198
  - 实例变量，声明, 33
  - 实例, 28
  - 分类，添加, 220–224
  - `iPhone_1ViewController.h` 类, 453–454
  - `iPhone_1ViewController.m` 类, 454–455
  - `reduce` 方法, 140, 142–145
  - 在 `add` 方法外减少分数, 145
  - 结果对象, 146–148
  - `setTo:over:` 方法, 135–137

# 类 501

- `NSArray`, 330
  - `sortUsingComparator:` 方法, 350–351
- 响应方法, 186–187
- 测试程序, 179–188
- `NSAutoreleasePool`, 403
- `NSBundle`, 396–397
- `NSCountSet`, 361
- `NSData`, 375–386
- `NSSet`, 361
- `NSDictionary`, 357
- `NSFileHandle`,
- `NSFileManager`
- `NSString`
- `CreateIndex`, 364
- `NSPathUtilities.h`, 381–382
- `NSProcessInfo`, 386–390
- `NSKeyedArchiver`, 428
- `NSKeyedUnarchiver`, 428–429
- `NSMutableDictionary`
  - 可变字典，创建, 354–355
  - 方法, 357
- `NSMutableSet`, 362
- `NSMutableString`, 320
- `NSNumber`, 174

# 类 502

- `UIView`, 229
- 单独类指令, 161–162
- 接口文件, 127–132
- 实现文件, 129–130
- 接口文件, 129–130
- 声明, 158–160
- 定义, 158
- 子类 `subclass`, 158–160
- 声明/定义, 160–161
- 程序, 164–165
- `side` 方法, 159
- `close` 方法, 391

# 悬指针引用

- 动态绑定, 180-182

# D

- 悬指针引用, 403
- 指针, 300
- 静态类型, 183-184
- 数据封装
  - 实例变量, 45-48
  - `int` 数据类型。参见 `int` 数据类型
  - 方法，创建, 45-48
  - 列表, 54-55
  - `setter/getters`, 48
  - 数值转换, 61-63
- 数据方法, 436
- 程序示例, 52-53
- 数据类型
  - 修饰符
    - `BOOL`, 121-122
    - 计数器, 54
    - `char`
    - `long`, 53-54
    - 分析程序, 107-109
    - 定义, 51
    - `long long`, 54
    - 概述, 52
    - `short`, 54
    - 指针, 275-277, 285-286
    - `typedef` 语句, 208-209, 270
    - `string` 对象, 删除, 323
    - `dataArray` 对象, 填充
    - Unicode, 312
    - 不可变字符串, 414-415
    - 转换, 209-210
    - 可变字符串, 416-417
    - 结束, 211
    - 日期程序, 268-269
    - 示例, 210-211
    - 日期结构
      - 规则, 210-212
      - 定义, 266-267
      - 类型强制转换运算符, 211
      - 初始化, 269-270
      - 转换为对象, 353-354
      - 月份值，测试, 267-268
    - `double`, 51
    - 指针, 277-279
    - 编码/解码, 430, 434-436
    - 程序, 268-269
    - 枚举
      - `todaysDate/purchaseDateVariables`,
      - 定义, 205
      - 声明, 272
      - 定义, 208
      - `datePtr` 指针, 277-279
      - 标识符, 206
      - `dealloc` 方法, 402
      - 整数, 205
      - 调试条件编译, 243
      - 月份程序, 206-208
    - 决策结构
      - 作为变量, 声明, 205
      - 布尔变量, 121-122
      - `float`, 24, 61-63
      - `BOOL` 数据类型, 121-122
      - 定义, 51
      - 定义, 119
      - 概述, 52
      - 质数表，创建, 118-119
      - `id`, 54
      - true/false 值, 119-121
      - 条件运算符
        - 编译时与运行时
        - 语法, 122
        - 检查, 182-183
        - 变量值, 赋值, 122-123
    - `#define` 语句
    - `else if` 语句
    - 方法
      - 字符分析程序, 107–109
      - 参数, 36–37
      - 类与实例, 35
      - 表达式程序, 109–112
      - 返回值, 36
      - 概述, 105
      - 多维数组, 253
      - 符号函数程序, 106–107
      - 指针, 275
      - 原型声明, 259–260
      - 语法, 105–106
      - `string` 对象
      - 程序, 112–114
      - 不可变, 315–316
      - 可变, 323
      - 绝对值程序, 94–98
      - 变量, 271
      - 复合关系测试, 100–103
      - 弱引用数组, 410
    - `else if` 结构。参见 `if`
    - `decodeObject:forKey:` 430, 432
    - 解码对象
      - 嵌套, 103–105
      - 地址录示例程序, 430–431
      - 语法, 93
      - `if-else` 语句, 98–100
      - 数据类型, 430, 434–436
      - 质数表，创建, 118–119
      - 方法, 430
      - 处理, 432
      - `switch` 语句
        - 测试程序, 433–434
        - `break` 语句, 115
        - `case` 运算符 (−), 78
        - `case` 值, 117
        - 数组指针, 282–284
        - 语法, 114–116
        - 前/后, 287–289
        - 深拷贝, 417–418, 439-441
        - `define` 语句, 233–239
        - 程序, 116–117
        - 参数空间, 238
        - 声明
          - 大写化, 235
          - 数组, 249
          - 类, 129–130
          - 234–235
          - 接口文件, 33
          - 注释，减少, 237
          - 与类定义分离, 127–132
          - 相等性测试, 236
          - `display` 属性, 454
          - 表达式
          - 外部变量, 201–280
          - `#define` 语句
          - 宏, 238–239
          - `delegates`
            - `case` 转换, 239
            - 条件运算符, 239
            - 子类, 452
            - 委托, 229
            - 小写字母，测试, 239
            - `deleteCharsInRange:` 方法, 323, 323
            - 多行代码, 237
            - 地址卡, 344–347
            - 放置, 234
            - `string` 对象的字符, 323
            - 文件, 371
            - `TRUE/FALSE` 值, 233–234
            - 可变 `string` 对象, 324
            - `denominator` 方法, 450
            - 依赖（系统）, 241–243
            - `description` 方法, 313
            - 设计接口, 234–235
            - 属性, 455
            - 相等性测试, 236
            - 按钮
            - 包含, 235
            - 未定义, 244
            - 有效性, 236
            - 字面量替换, 236
            - iPhone 应用, 474–475
            - `case` 转换, 239
            - 指南, 239
            - 小写字母，测试, 239
            - 定位, 458
            - 未定义, 230
            - 尺寸, 458
            - 用户界面设计, 237
            - 期望整数计算
            - 程序示例, 79–81
            - 块, 263
            - 字典, 172–133
            - 添加, 355
            - 枚举数据类型, 298
            - 字母顺序排序, 356
            - 协议, 226–327
            - 术语程序, 354–355
            - 可变/不可变, 354
            - 添加文件名到结尾, 383
            - 数组，返回, 383
            - 创建, 425–427
            - 解构, 384
            - 读取, 427
            - 获取键值, 355
            - 扩展，添加, 384
            - `dictionaryWithCapacity: size` 方法, 357
            - `dictionaryWithObjectsKeys:` 方法, 355–357
            - 扩展，移除, 383
            - 文件扩展名, 383
            - 完整路径, 370
            - 类, 161–162
            - 硬编码, 370
            - 实例变量作用域, 199
            - 最后组件，提取, 384
            - 可选, 230
            - 最后组件，移除, 384
            - 文件最后, 383
            - `private`, 199
            - `NSPathUtilities.h` 类, 381
            - `protected`, 199
            - 路径，添加到结尾, 384
            - 协议, 226
            - 相对路径, 370
            - `public`, 199
            - 标准化, 384
            - 选择, 186
            - 符号链接, 384
            - 合成, 133
            - 临时目录, 384
            - 用户信息，返回, 384
            - 目录, 376–378
            - 临时文件, 383
            - 属性字典, 372

# 显示 属性

- `Caches`, 385
- 访问方法，合成, 454–455
- `Documents`, 385

# 显示

- 数组, 309–330
- `home`, 370, 383
- iOS, 385
- 定位, 385
- 之间移动文件, 377
- `NSFileManager` 类方法, 376–378
- 程序结果, 41
- 操作程序, 377–382
- `string` 对象, 313
- 变量值, 23–25

# 捕获表达式程序

- 捕获表达式程序，190–191
- `Fraction` 类示例，189–190
- 多个 `catch` 块，191
- 抛出异常，191

# 扩展类

- 扩展类，148, 224-225
- 方法，添加，156–158
- 存储信息，161
- 子类，创建，156–180

# 扩展

- 交换-OR 运算符，280
- 异或运算符，211, 214
- 类，224–225
- 文件，14
- `extern` 关键字，201
- 外部外部变量，201-202

# 算术

- 赋值运算符，64
- `Calculator` 类，65–67
- 计数数字循环示例，71–72

# F

- 假值，119-121
- 快速枚举，339
- 斐波那契数列程序，249-250
- `fileExistsPath:` 方法，371, 376
- `fileForReadingAtPath:` 方法，390
- `fileForUpdatingAtPath:` 方法，390
- `fileForWritingAtPath:` 方法，390
- `Fraction` 类。参见 `Fraction` 类
- 整数算术，58–60
- 取模运算符，60–61
- 数值数据类型转换，61–63
- 运算符优先级，55–58
- 类型转换运算符，63–64

# 文件

- 在文件之间追加内容，393–399
- 属性字典，372
- 缓冲区，375–376
- 关闭，391
- 复制，371, 386
- 自定义存档。参见自定义存档
- 数据，返回，390
- 删除，371
- 目录，删除，371
- 存在性，测试，371
- 扩展，14
- 操作程序，391–392
- 头文件，导入，307, 454
- 实现
  - `AddressBook` 类，338–339
  - 分类，221
  - 类，定义，130–131
- 运算符，55
- 空格，103
- 复合关系，101
- 闰年程序，101–103
- 运算符，101
- 常量，51
- 数据类型转换
  - 结束，211
  - 示例，210–211
  - 规则，210–211
  - 类型转换运算符，211
- `#define` 语句
  - 包含，235
  - 有效性，236
- 数字运算符数字值评估
  - 程序，109–112
- 文件
  - `Fraction` 类，470–473
  - 程序
  - `Fraction_CalculatorViewController`
  - 分配对象，39–40
  - 类，465–468
  - 初始化对象，40
  - 实例变量，声明，37–38
  - 主程序，39
  - 概览，33
  - 多个对象，42–45
  - 语法，37
  - 对象引用，41–42
  - 导入，20, 131
  - 对象值，30–41
  - 接口。参见接口文件
  - 概览，33
  - 结果，显示，41
  - 在目录间移动，374
  - 变量，定义，39
  - `NSFileManager` 方法，370–371
  - 读取，371, 390
  - 偏移量，390–391, 393
  - 相对文件定位，393
  - 打开，390
  - 重命名，371
  - 操作程序，372–374
  - 分离接口/实现
  - 路径名
    - 文件，127–132
    - 在末尾添加文件名，383
    - 实现文件，130–132
    - 数组，返回，383
    - 接口文件，129–130, 132
    - 创建，384
    - 大小，374
    - 解构，384
    - 测试创建，384
    - 目录，定位，385
    - 向其写入数据，371, 390
    - 扩展，添加，384
    - `xib`，455
    - 扩展，提取，384
    - 扩展，移除，384
- `float` 数据类型，24, 61–63
- 文件扩展名，383
- 定义，51
- 全路径，370
- 概览，52
- 硬编码，370
- `floatValue` 方法，326
- 主目录，383
- `FPtr` 指针，291–292
- 最后组件，提取，384
- 最后组件，移除，384
- `Foo` 类，434–436
- 最后文件，提取，383
- 第200个三角形数元素，72–75
- `NSPathUtilities.h` 类，381
- 路径，在末尾添加，384
- 相对路径，370
- 标准化，384
- 符号链接，384
- 用户信息，返回，384
- 三角形数示例表，75–79
- 框架

# Foundation 框架

- 字母排序，356
- 枚举，355–356
- 术语表程序，354–355
- 可变/不可变，354
- 格式化字符串，25
- 概览，354
- 获取值，355
- 目录，376–378
- 存档。参见存档
- 属性字典，372
- 对象
  - 缓存，385
- 数组
  - 当前路径，显示，378
  - 10 个对象程序，328–329
  - 枚举，379–381
  - 地址簿。参见地址簿
  - 硬编码路径，370
  - 创建，370
  - 主目录，370
  - 定位，385
  - 数据类型转换为对象，353–354
  - 显示，327–330
  - 月份程序，327–328
  - 操作程序，377–378
  - 可变，330
  - 在末尾添加对象，330
- 文档，304–306
- Mac OS 库，306
- 数字，328
- 快速帮助，304
- 排序方法，352
- 与块排序，350–351
- 与选择器排序，347–350
- 包，396–397
- 复制对象
  - 属性字典，372
  - 复制方法，414–415
  - 缓冲区，375–376
  - 深拷贝，417–418
  - 克隆，391
  - `getter` 方法，422–423
  - 不可变字符串，413–415
  - 数据，返回，390
  - 可变字符串，416–417
  - 从目录删除，371
  - 可变拷贝协议，418–421
  - 存在性，测试，371
  - `setter` 方法，421–422
  - 浅拷贝，417
  - 字典添加键，355

# Foundation 框架 (续)

- 硬编码路径名，370
- 在目录间移动，374
- `NSFileManager` 方法，370–371
- 偏移量，390–393
- 操作程序，372–374
- 读取，371, 390
- 相对文件定位，393
- 重命名，371
- 大小，374
- 向其写入数据，371, 390
- 头文件，导入，307, 454
- 数字对象，307–311
  - 分配方法，309
  - `double` 对象，310
  - `NSNumber` 方法列表，310
  - `IntegerValue` 方法，311
  - 程序，307–309
  - 存储值，获取，310
  - 值，编辑，311
  - 值，获取，309
- 概览，274
- 向路径名添加文件名，383
- 数组，返回，383
- 创建，384
- 解构，384
- 目录，定位，385
- 扩展，添加，384
- 扩展，提取，384
- 文件扩展名，383
- 主目录，383
- 最后组件，提取，384
- 最后组件，移除，384
- 最后文件，提取，383
- 路径，在末尾添加，384
- 标准化，384
- 符号链接，384
- 临时目录，384
- 临时文件目录，384
- 用户信息，返回，384
- 添加/移除对象，360
- 计数，361
- 等性，360
- 交集，360
- 操作程序，358–360
- 有序索引，362–364
- 概览，358
- 并集，360
- 字符串对象
  - 创建，312
  - `description` 方法，313–314
  - 显示，313
  - 不可变。参见不可变字符串
  - 可变。参见可变对象
  - `SSString` 类，312, 324–326
  - 程序，312
  - `unichar` 字符，312
- 分数计算器应用程序
  - `Calculator` 类，473–464
  - 完成操作，462
  - 数字按钮，按下，469
  - `Fraction` 类，469–473

# 框架

- 实现文件，470–473
- 接口文件，469–470
- `Fraction_Calculator`，启动，462
- `Fraction_CalculatorViewController` 类，464–469
  - 实现文件，465–468
  - 接口文件，464–465
  - 接口设计，474–475
  - 输入分数，462
  - 分数乘法示例，462
  - 概览，448
  - 项目文件，475
  - 序列概览，475–476
  - 样本，464
  - 启动后在模拟器中查看，461
- 宏，239
- `MathOps` 分类，添加，220–224
- 约分分数，140–145
  - 创建，140
  - 声明，142–143
  - 定义，143–144
  - 在 `add:` 方法内部，145
  - 在 `add:` 方法外部，144–145
  - `setOver:` 方法，135–137
- `Fraction_CalculatorViewController` 类，464–469
  - `clickDigit:` 方法，469
  - `clickEquals` 方法，469
  - 实现文件，465–468
  - 接口文件，464–465
  - `processDigit:` 方法，469

# Fraction 类，31–33

- 分数程序
  - `add:` 方法，137–138
  - 向接收者添加参数，138
  - 分数测试程序，138–139
  - 引用，138
  - 结果对象，146–148
  - `self` 关键字，145
  - `calculate:` 方法，141
  - `convertToNum` 方法，95
  - 拷贝分数，419–420
  - 声明，129–130
  - 定义，130–131
  - 异常处理，189–190
  - 结束，148
  - 分数计算器 iPhone 应用程序，469–473
  - 实现文件，470–473
  - 接口文件，469–470
  - 初始化
    - 测试，197–198
    - 初始化方法，197
  - 拷贝分数，419–420
  - `Fraction` 类。参见 `Fraction` 类
  - iPhone 分数计算器应用程序。参见 iPhone 分数计算器应用程序
  - 多个分数，42–45
  - 约分分数，140–145
    - 创建，140
    - 声明，142–143
    - 定义，143–144
    - 在 `add:` 方法内部，145
    - 在 `add:` 方法外部，144–145
  - 没有类，30–31

# 框架 514

- `Application Services`, 444
- 绕过, 444
- `Cocoa`, 444
- `Core Services`, 443
- `kernel`, 443
- `scope`, 260
- `sign`
  - defined, 105
  - `else if` program, 106–107
  - `static`, 261
  - `syntax`, 254, 256
  - `values`, 常见公约数程序, 最大公约数程序, 257–259
  - `overview`, 257
  - `return type declaration`, 省略, 259
- `FSF` (自由软件基金),
- `full pathnames`, 370
- `arguments`
  - 命令行, 296–298
  - `numeric` 转换, 260
  - 指针, 279–280
  - `types`, 声明, 259
  - 变数量, 260

# G

- `arrays`
  - 带指针的引用, 284
  - passing, 261–262
  - `arraySum`, 238–284
  - `calculateTriangularNumber`, 255–257
  - `copyString`, 286
  - `declaring`, 260
  - `ending`, 257
- 垃圾回收
  - Disadvantages, 402
  - iOS support, 401
  - overview, 401
  - turning on, 401
- `gcd` function, 257–259
- `getter` methods, 48
  - copying objects, 422–743
  - `Rectangle` class, 168
- 最大公约数程序, 257–259
- 局部变量, 257
- 全局变量, 200-202
  - defined, 200
  - external, 201
  - lowercase g, 200
  - `globallyUniqueString` method, 387
- `main`
  - 添加, 255
  - 自动释放池, 404
  - 程序段, 39
  - `PathUtilities.h` class, 384
  - 指针, 291–292
  - `printMessage`, 254
  - 原型声明, 259–260
  - 与方法的关系, 299
  - 声明, 259
  - 省略, 259
- 词汇表程序
  - 存档, 428
  - 创建, 354–355
  - 读取, 428–429
- `GNUStep`, 1
- `GraphicObject` class
  - 分类示例, 224–225
  - `Drawing` 协议, 227
  - `greater than` (`>`) operator, 74

# 不变字符串对象

- `greater than or equal to` (`>=`) operator, 74
- 最大公约数程序, 85-87, 257-259
- `id` data type, 54
- 编译时与运行时
  - 检查, 182–183
  - 动态绑定, 180–182
  - 指针, 300
  - 静态类型, 183–184
- 分组元素. 见 `arrays`; `structures`

# H

- `If` 语句
- `.h` 文件扩展名, 14
- 绝对值程序, 94–98
- 复合关系测试, 100–103
- 闰年程序, 101–103
- 运算符, 101
- 条件编译, 243–244
- 处理异常, 189
- 异常程序终止,
  - 避免, 190
- 捕获表达式程序, 190–191
- `Fraction` 类示例, 189–190
- 多个 `catch` 块, 191
- 抛出异常, 191
- `else if` 结构
  - 字符分析, 107–109
  - 数字运算符数字表达式程序, 109–112
  - 概述, 105
- 硬编码路径名, 370
- 符号函数程序, 106–107
- 语法, 105–106
- 值运算符值表达式程序, 112–114
- `if-else` 结构, 98–100
- 嵌套, 103–105
- `hasPrefix:` `nsstring` 方法, 325
- `hasSuffix:` `nsstring` 方法, 325
- 头文件，导入, 307, 454
- 帮助
  - 论坛支持网站, 5
- `Foundation` 框架
  - 文档, 304–306
  - 快速帮助, 304–305
- 十六进制表示法, 212
- `#ifdef` 语句, 241
- `If-else` 语句, 98–100
- 可变字典, 354
- 可变 `string` 对象
  - `case`, 转换, 316
  - 字符长度，计数, 316
  - 字符串，连接, 316
  - 复制对象, 416–747
  - 基于另一个创建, 316
  - 声明, 315–317
  - 定义, 314
  - 相等性，测试, 316
  - 初始化, 317
- 主目录, 370, 383
- `hostName` 方法, 387

# I

- `IBAction` 类, 454
- `IBOutlet` 类, 454

# 不可变字符串对象

- 消息，发送, 317
- 可变，对比, 320
- 程序, 314–315
- 引用, 317
- 子字符串，创建, 318–220
  - 从内部字符串, 320
  - 前导字符串, 319
  - 定位字符串在另一个内部, 320
  - 范围, 320
  - 指定字符, 319
- 非正式协议, 229-230
- `init`
  - 分类, 225
  - `class` 指令, 161
  - 复制对象, 420
  - 实例变量, 152-154, 198
  - 添加, 156-158
  - 方法, 152–154
  - 覆盖, 169–173
  - 对象方法，选择, 155–156
  - 对象，拥有, 165–169
- 实现文件
  - `AddressBook` 类, 338–339
  - 类，定义, 130–131
  - `Fraction` 类, 470–473
  - `ViewController`, 465–468
  - 实例变量，声明, 37–38
  - 概览, 33
  - 内存引用, 166
  - 传递值给方法, 166
  - 父类, 152
  - 根类, 151
  - 存储信息, 161
  - 子类, 152–153
  - 好处, 173
  - 创建, 158–160
  - 定义, 173
  - 超类, 152–163
- `import` `Inclusive-OR` operator (`|`), 211, 213
- 自增运算符 (`++`), 77
- 数组指针, 282–284
- 前/后, 287–289
- 索引号, 248
- `indexPassingTest:` 方法, 364
- `indexLessThanObject:` 方法, 364
- `indexOfObjectPassingTest:` 方法, 351, 362
- `indexSet` 方法, 364
- 间接寻址, 273
- 方向 (`*`), 274, 275
- `init`
  - 方法, 40, 155
  - 创建, 197
  - 覆盖, 19–197
  - 测试, 197–198
  - 初始值，赋值, 722
  - 初始化数组, 250–251
  - 不可变字符串对象, 317
  - 多维数组, 253–254
  - 对象, 40, 195–197
  - 数组, 196

# 接口设计 517

- `init` 前缀用于方法, 196
- 方法，创建, 199
- 覆盖 `init`, 196–197
- 语法, 195–196
- 测试, 197–198
- 结构体, 269–270
- `initVar` 方法, 169–170
- `initWith:` 方法, 197
- `initWithCapacity:` 方法, 326, 357, 361
- `initWithCoder:` 方法, 430, 432
- `initWithContentsFile:` 方法, 325
- `initWithContentsURL:` 方法, 325
- `initWithName:` 方法, 339
- `initWithObjects:` 方法, 361
- `initWithKeys:` 方法, 357
- `initWithString:` `nsstring` 方法, 325
- `insertObject: objIndex:` i, 352
- `insertString:` `nsstring` `atIndex:` i, 326
- `insertString:atIndex:` 方法, 323
- 插入实例, 305
- 类对比实例, 29
- 语法, 28–29
- 实例变量
  - `_` (下划线), 200
  - 访问, 45–48
  - 方法，创建, 45–48
  - `setters/getters`, 48
  - 访问器方法，合成, 202
  - 声明, 33, 37–38
  - 继承, 152–154
  - 名字
    - `_` (下划线), 200
    - 选择, 34
    - 对比属性名, 454
    - 起点, 161
- `outlets`
  - 连接, 460
  - 定义, 453
  - 属性, 200
- 作用域, 198
  - 指令, 199
  - 实例, 198
  - `Printer` 类, 199
  - 存储, 298–299
  - 测试, 167
- `instancesRespondToSelector:` 方法, 185
- `int` 数据类型, 24
  - 位运算符
    - `AND`, 212–213
    - 二进制/十六进制表示法
    - 转换, 212
    - `Exclusive-OR`, 214
    - `Inclusive-OR`, 213–214
    - 左移, 216
    - 补码, 214
    - 右移, 215–217
  - 转换, 61–63
  - 枚举数据类型, 205
  - 概览, 52
  - 指针, 274
  - 限定符
    - `long`, 53–54
    - `long long`, 54
    - `short`, 54
    - `signed`, 54
  - 整数算术, 58–60
- `intValue` 方法, 326
- 接口设计, 455–460
  - `Attributes Inspector`, 455
  - 黑色窗口，创建, 455

# 接口设计 518

- 按钮
  - 动作，添加, 460
  - 添加, 459
  - 分数计算器应用程序, 474–475
  - 引导线, 458
- 标签
  - 添加, 455
  - 属性, 458
  - 定位, 458
  - 大小, 458
- 用户界面设计, 455
- 头文件，导入, 454
- `IBAction` 标识符, 454
- `IBOutlet` 标识符, 454
- 实例变量名对比属性名, 454
- 接口设计, 455–460
- iPhone 模拟器, 449, 452, 460
- 新项目, 449
- `outlets`, 453, 460
- 项目文件夹位置, 451
- 项目选项，选择, 450
- 合成 `display` 属性访问器方法, 454–455

# 接口文件

- `AddressBook` 类, 337–338
- `AddressCard` 类, 331, 337–338
- 参数, 36–37
- 类
  - 声明, 33, 129–130
  - 定义，扩展, 140
  - 实例方法，对比, 35
- `Fraction` 类, 469–470
- `Fraction_CalculatorViewController` 类, 464–465
- 方法
  - 参数, 36–37
  - 分类, 220
  - 类对比实例, 375
  - 返回值, 36
- 名字，选择, 34–35
- 概览, 33

# 显示文本响应按钮

- 黑色窗口，创建, 455
- 按钮动作，添加, 460
- `display` 变量和标签连接, 460
- `iPhone_1ViewController.h` 类, 453–454
- `iPhone_1ViewController.m` 类, 454–455
- 概览, 448
- 运行, 460
- 序列概述, 459
- 源代码，显示, 460

# 分数计算器应用程序

- `Calculator` 类, 473–474
- 完成操作, 462
- 数字按钮，按下, 469
- `Fraction` 类, 469–473
- 用户接口设计, 455

# iOS

- 应用程序
  - 声明 `display` 属性, 454
  - 代理子类, 452

# iPhone 应用 519

- `Fraction_CalculatorViewController` 类, 464–469
- 接口设计, 474–475
- 输入分数, 462
- 分数乘法示例, 462
- 概览, 448
- 项目文件, 475
- 序列概述, 475–476
- 模板, 464
- 启动后在模拟器中查看, 461
- 垃圾回收支持, 401
- `SDK`, 447
- `Fraction_Calculator`, 开始, 462
- `Fraction_CalculatorViewController` 类, 464–469
- 接口设计, 474–475
- 输入分数, 462
- 分数乘法示例, 462
- 概览, 448
- 项目文件, 475
- 序列概述, 475–476
- 模板, 464
- 启动后在模拟器中查看, 461

# iPhone 应用

- 代理子类, 452
- `display` 属性
  - 访问方法，合成, 454–455
  - 声明, 454
- 响应按钮点击显示文本
  - 黑色窗口，创建, 455
  - 按钮动作，添加, 460
- `display` 变量和标签
  - 连接, 460
- 头文件，导入, 454
- `IAction` 标识, 454
- `IBOut` 标识, 454
- 实例变量与属性, 454
- 接口设计, 455
- 属性检查器 (`Attributes Inspector`), 455
  - 黑色窗口，创建, 455
  - 按钮动作，添加, 460
- 按钮，添加, 459
- 引导线, 458
- 标签, 455–459
- `iPhone_1ViewController.h` 类, 453–455
- `iPhone_1ViewController.m` 类, 454–455
- 概览, 448
- 运行, 460
- 序列概述, 459
- 源代码，显示, 460

# 分数计算器

- `Calculator` 类, 473–474
- 完成操作, 462
- 数字按钮，按下, 469
- `Fraction` 类, 469–473
- 用户接口设计, 455

# iOS

- 开发者计划, 449
- `SDK`, 447
- iPhone 模拟器，选择, 452
- 原生的, 2
- 新项目，开始, 449
- `outlets` (连接点)
  - 连接, 460
  - 定义, 453
- 项目文件夹位置, 451
- 项目选项，选择, 450
- 模拟器, 449

# iPhone 应用 460

- 按钮点击, 460
- 选择, 452
- 分数计算器，显示, 461
- 模板, 449–450
- 视图, 453

- `lastIndex` 方法, 364
- `lastObject` 方法, 351
- `lastPathComponent` 方法, 383-384
- 层 (框架), 443-444
  - `Application Services`, 444
  - 绕过, 444
  - `Cocoa`, 444
  - `Core Services`, 443
  - 内核 (`kernel`), 443
- `iPhone_1ViewController.h` 类, 453-454
- `iPhone_1ViewController.m` 类, 454–455
- `isEqualToSet:` 方法, 360, 361
- `isEqualToString:` `nsstring` 方法, 325
- `isKindOfOfClass:` 方法, 185
- `isMemberOfOfClass:` 方法, 185
- `isReadableFileAtPath:` 方法, 371
- `isSubClassOfSet:` 方法, 185
- `isSubSubsetOfSet:` 方法, 361
- `isWritableFilePath:` 方法, 371
- 闰年程序, 101–103
- 左移运算符 (`<<`), 211, 216
- `length` 方法, 325
- 小于 (`<`) 运算符, 74
- 小于等于 (`<=`) 运算符, 74

# LinuxSTEP

# 局部变量

- 参数名, 141
- 自动的, 257
- 定义, 140
- 函数, 257
- 静态, 141-142, 257
- 值, 141, 257
- `long long` 修饰符, 54
- `long` 修饰符, 53-54
- `lookup:` 方法, 341-344
- 内核 (`kernel`), 443
- 键盘输入，`for` 循环, 379–380
- 键值存档 (`keyed archives`), 427
  - 创建, 428
  - 定义, 428
  - 读取, 428–429
  - 支持, 428
- `keyEnumerator` 方法, 357
- `keysSortedByValueUsingSelector:` 357

# 关键字

- `extern`, 201
- `self`, 145
- `static`, 141-142

# 循环

- `continue` 语句, 90
- 计数示例, 712
- `do`
  - 执行, 89
  - 反转数字程序, 89-90
  - 语法, 88
  - `while` 循环, 89
  - 结束, 75, 90
- 标签 (接口)
  - 添加, 455
  - 属性, 458
  - 定位, 458
  - 大小调整, 458
- 内存管理 521
  - 事件, 405–407
  - 小写字母, 239
  - `for`
  - `SQUARE_E`, 238–239
  - 第200 个三角形数示例, 72–75
  - 主函数
    - 添加, 255
    - 条件, 74
    - 初始化值, 73
    - 键盘输入, 79–81
    - 自动释放池示例, 404
  - 程序段, 39
  - `makeObjectsPerform Selector:` 方法, 351
  - 嵌套, 82
  - 概览, 75
  - 语法, 手动计数, 402–403
  - 三角形数
    - 示例, 75–79
    - 自动释放池, 403–405
    - 添加对象, 303
    - `while` 循环,
- 自动释放块 (`autoreleasing blocks`), 404–410
- 块 (`blocks`), 410–411
- 释放, 403
- `while`
  - 计数到 5 程序示例, 84–85
  - 主程序示例, 404
  - 释放后存活, 405–407
  - `do` 循环, 89
  - 最大公约数程序, 85–87
  - 拥有对象, 释放, 404
  - 悬空指针引用, 403
  - `for` 循环, 85
  - 反转数字程序, 87–88
  - 语法, 84
  - 释放, 402
  - 递减, 402
  - 递增, 402
  - 方法, 402
  - 强变量, 408
- 小写对比大写, 19
- 主-详情 模板, 450
- `lowercaseString` 方法, 326
- `MathOps` 类别, 220–224

# 矩阵

- 4 x 5, 252
- 符号, 252–253
- 文件扩展名, 144
- `member:` 方法, 361

# Mac OS 内存管理

- `Cocoa`, 274, 443
- `Cocoa Touch`, 444–345
- `ARC`, 408
- 库, 305–368
- 非 ARC 编译代码, 411
- 强变量, 409
- 除法, 239
- 条件运算符, 239
- 定义, 238–369
- 自动释放池
- `Fraction` 类, 239
- 导入, 240–241
- 块 (`blocks`), 410–411
- 定义, 21
- 释放后存活: `own` 自动释放池

# 内存管理

- 事件循环, 405–407
- 垃圾回收, 402
- iOS 支持, 401
- 概览, 401
- 开启, 401
- 手动计数, 402–403
- 自动释放池, 403–405
- 悬空指针引用, 403
- 释放, 402
- 递减, 402
- 递增, 402
- 方法, 402
- 强变量, 408
- 对象引用, 166
- 指针, 292–293
- 释放, 41
- 规则, 407–409
- 强变量, 409–410
- 声明, 410
- 代理, 410
- 强引用对象, 409
- 支持, 410

# 方法

- `+/-` 符号, 35
- `accessor/setter/getters`, 48
- 合成: 访问方法
- `add:`
  - 接收者的参数, 138
  - `Fraction` 对象引用, 137
  - 分数测试程序, 138–139
  - 引用, 138
  - 结果对象, 146–148
  - `self` 关键字, 145
- `addCard`, 339
- `addObject:` 330, 352, 360, 362
- `allKeys`, 357
- `alloc`, 40, 155, 309
- `anyObject`, 361
- `appendString`, 323, 326
- `ARC`, 310
- `archiveObject:ToFile:` 428
- 参数, 29, 141, 386
- 数组, 261–262, 352
- `arrayWithCapacity: size`, 352
- `arrayWithObjects:` 328, 351
- `availableData`, 390
- `calculate`, 141
- `camelCase`, 411
- `capitalizedString`, 326
- `caseSensitive:` `nsstring`, 325
- 数量, 225
- 定义, 219
- (接口), 220
- 实现 (文件), 221
- 继承, 225
- `MathOps` 类别, 224
- 示例, 225
- 自动释放块, 404–410
- 块 (`blocks`), 410–411
- 释放, 403
- `while`
  - 计数到 5 程序示例, 84–85
  - 主程序示例, 404
  - 释放后存活, 405–407
  - `do` 循环, 89
  - 最大公约数程序, 85–87
  - 拥有对象, 释放, 404
  - 悬空指针引用, 403
  - `for` 循环, 85
  - 反转数字程序, 87–88
  - 语法, 84
  - 释放, 402
  - 递减, 402
  - 递增, 402
  - 方法, 402
  - 强变量, 408

# 方法 525

- `NSSet` 类, 361
- `NSString` 类, 列表, 324–324
- `NSValue` 类, 353–354
- `numerator` (分子), 45
- `objectAtIndex:`, 328, 351
- `objectEnumerator`, 357, 361
- `objectKey:`, 355, 357
- `objects`, 28
  - 分配, 146
  - 选择, 155–156
  - 返回, 146
- `offsetInFile`, 390
- `operatingSystem`, 387
- `operatingSystemName` method, 387
- `operatingSystemVersionString`, 387
- `origin`, 162
- `pathComponents`, 383–384
- `pathExtension`, 383–384
- `pathWithComponents:`, 384
- `performSelector:`, 186
- 多态 (`polymorphism`)
  - `Complex` 示例, 177–180
  - 定义, 180
- `print`
  - `NSSet` 类, 360
  - 程序结果, 显示, 41
- `printVar:`, 153
- `processDigit:`, 469
- `processIdentifier`, 386
- `processInfo`, 386
- `processName`, 387
- `adopting`, 226
- `setAttributesOfItemAtPath:`, 371
- `setDenominator`, 36

# 方法

- `setName;`, 322, 421
- `setName:andEmail;`, 335–337
- `setNumerator;`, 36
- `setObject;`, 355, 357
- `setOrigin;`, 162
- `setProcessName;`, 387
- `setSide;`, 159
- `setString;`, 324, 326
- `setter` (`setter` 方法), 48
  - 复制对象, 421–423
  - `Rectangle` 类, 168
- `setOver;`, 135–137
- `setWithCapacity;`, 361
- `setWithObjects;`, 361
- `side`, 159
- `sortedArrayUsingComparator;`, 350, 352
- `sortedArrayUsingSelector;`, 352
- `sortUsingComparator;`, 350, 352
- `sortUsingSelector;`, 347–350, 352
- `string`, 325
- `stringByAppendingPathComponent;`, 383–384
- `stringByAppendingPathExtension;`, 384
- `stringByDeletingLastPathComponent;`, 384
- `stringByDeletingPathExtension;`, 384
- `stringByExpandingTildeInPath;`, 384
- `stringByResolvingLinksInPath;`, 384
- `stringByStandardizingPathmethod;`, 384
- `stringWithCapacity;`, `size`, 326
- `stringWithContentsOf;`, 325, 374
- `stringWithContentsOfURL;` `url` `encoding:` `exc` `err;`, 325
- `stringFormat: format, arg1, arg2, arg3 . . .`, 325
- `stringWithString:` `nsstring`, 325
- `substringFromString;`, 319, 325
- `substringToIndex;`, 319, 352
- `substringWithRange;`, 320, 325
- `syntax` (语法), 28–29
- `truncateFileAtOffset;`, 391
- `unarchiveWithFile;`, 352
- `union;`, 360
- `union;`, 362
- `uppercaseString`, 326
- `UTF8String`, 326
- `writeData;`, 390
- `writeToFile;`, 352
- 减等运算符 (`-=`), 64
- 减号 (`-`)
  - 算术表达式, 55
  - 方法, 355
- `minusSet:` method, 362
- `.mm` 文件扩展名, 144
- 取模运算符 (`%`), 60–61
- 月份 (`month`) 枚举数据程序, 206–208
- 月份名称程序, 327–328
- `moveitemAtPath:` method, 371, 374, 377
- 多维数组 (`multidimensional arrays`), 252–254
  - 4 x 5 矩阵, 252
  - 声明, 253
  - 初始化, 252–254
  - 符号, 252
- 多参数, 135–139
  - 添加到 接收者, 138
  - 点运算符, 138
  - `Fraction` (`分数`) 类, 139
  - 名字, 135
  - 无名字, 137
  - 引用, 337
  - `setOver:` 方法, 315

# NSCopying 协议 527

- 多个对象, 45
- 表达式, 235
- 多个协议, 226
- 乘法运算符, 55
- 方法 (分类)
  - 定义. 另见 `define` 语句
  - `InfoPlist` bundle, 396
  - 参数, 242
  - 大小写敏感, 34
  - `sortedArrayUsingComparator:` method, 350
  - 方法, 315
  - 类, 333
  - 复合字面量, 293
  - 类继承, 420
  - 相等性测试, 236
  - 复制分数, 419–420
  - 表达式有效性, 236
  - `copyWithZone:` method, 418

# NSArray 类

- 参数, 137
- 初始化方法, 196
- 大小写敏感, 34
- `sortedArrayUsingComparator:` method, 350
- 方法, 315
- 类, 333
- 复合字面量, 293
- 定义. 另见 `define` 语句
- `InfoPlist` bundle, 396
- 参数, 242
- 大小写敏感, 34
- `sortedArrayUsingComparator:` method, 350
- 方法, 315
- 类, 333
- 复合字面量, 293
- 定义. 另见 `define` 语句
- `InfoPlist` bundle, 396
- 参数, 242
- 大小写敏感, 34
- `sortedArrayUsingComparator:` method, 350
- 方法, 315
- 类, 333
- 复合字面量, 293
- 定义. 另见 `define` 语句
- `InfoPlist` bundle, 396
- 参数, 242
- 大小写敏感, 34
- `sortedArrayUsingComparator:` method, 350
- 方法, 315
- 类, 333
- 复合字面量, 293
- 定义. 另见 `define` 语句
- `InfoPlist` bundle, 396
- 参数, 242
- 大小写敏感, 34
```



# NSCountedSet 类

- methods, 364
- methods, 360
- overview, 362
- print method, 360

# NSKeyedArch 类, 428

# NSString 类

- methods, 315
- compound literals (复合字面量), 293
- defined. 另见 define 语句
- InfoPlist bundle, 396
- argument (参数), 242
- case sensitivity (大小写敏感), 34
- sortedArrayUsingComparator:method, 350
- method, 315
- classes, 333

# NSKeyedUnarchiver 类, 428-429

---

# NSArray 类

- arguments, 137
- initialization methods (初始化方法), 196
- case sensitivity (大小写敏感), 34
- sortedArrayUsingComparator:method, 350
- method, 315
- classes, 333
- compound literals (复合字面量), 293
- defined. 另见 define 语句
- InfoPlist bundle, 396
- argument (参数), 242

---

# 方法 525

- NSSet 类, 361
- 定义, 226–227
- NSString 类, 列表, 324–324
- 委托, 229
- NSValue 类, 353–354
- 现有定义, 扩展, 228
- numerator (分子), 45
- 非正式, 229–230
- objectAtIndex:, 328, 351
- 多个, 226
- objectEnumerator, 357, 361
- 名字, 226
- objectKey:, 355, 357
- objects, 28
- 协议遵守, 227–228
- allocating, 146
- 子类, 227
- choosing, 155–156
- rangeOfString:, 324
- returning, 146
- readDataOfLength:, 320
- offsetInFile, 390
- readDataToEndFile, 390
- operatingSystem, 387
- reduce
- operatingSystemName method, 387
- 创建, 140
- operatingSystemVersionString, 387
- 声明, 142–143
- origin, 162
- 定义, 144–144
- pathComponents, 383–384
- 程序, 144–145
- pathExtension, 383–384
- 与函数的关系, 299
- pathWithComponents:, 384
- performSelector:, 186
- removeAllObjects, 357, 362
- polymorphism (多态)
- removeCard:, 362
- Complex example (复杂示例), 177–180
- removeItemAtPath:, 371, 377
- dined, 180
- removeObject:, 352, 362
- print
- removeObjectAtIndex: i, 352
- NSSet 类, 360
- removeObjectIdenticalTo:, 345
- replaceChangesInRange: range
- printVar:, 153
- withWithString: nsstring, 326
- program results (程序结果), 显示, 41
- replaceObjectAtIndex: i withObject: obj, 352
- processDigit:, 469
- replaceOccurrencesOfString:, 324, 327
- processIdentifier, 386
- respondsToSelector:, 187
- processInfo, 386
- seekToEndOfFile, 391
- processName, 387
- seekToFileOffset:, 391
- selector directive, 186
- adopting, 226
- setAttributesOfItemAtPath:, 371
- setDenominator, 36
- category (分类) adoptions, 228
- dfined, 226
- setEmail:, 332

## 方法

- setName;, 322, 421
- setName:andEmail;, 335–337
- setNumerator;, 36
- setObject;, 355, 357
- setOrigin;, 162
- setProcessName;, 387
- setSide;, 159
- setString;, 324, 326
- setter (setter 方法), 48
- copying objects, 421–423
- Rectangle 类, 168
- setOver;, 135–137
- setWithCapacity;, 361
- setWithObjects;, 361
- side, 159
- sortedArrayUsingComparator;, 350, 352
- sortedArrayUsingSelector;, 352
- sortUsingComparator;, 350, 352
- sortUsingSelector;, 347–350, 352
- string, 325
- stringByAppendingPathComponent;, 383–384
- stringByAppendingPathExtension;, 384
- stringByDeletingLastPathComponent;, 384
- stringByDeletingPathExtension;, 384
- stringByExpandingTildeInPath;, 384
- stringByResolvingLinksInPath;, 384
- stringByStandardizingPathmethod;, 384
- stringWithCapacity;, size, 326
- stringWithContentsOf;, 325, 374
- stringWithContentsOfURL; url encoding: exc err;, 325
- stringFormat: format, arg1, arg2, arg3 . . . , 325
- stringWithString: nsstring, 325
- substringFromString;, 319, 325
- substringToIndex;, 319, 352
- substringWithRange;, 320, 325
- syntax (语法), 28–29
- truncateFileAtOffset;, 391
- unarchiveWithFile;, 352
- union;, 360
- union;, 362
- uppercaseString, 326
- UTF8String, 326
- writeData;, 390
- writeToFile;, 352
- minus equals (=) 运算符, 64
- minus signs (-)
- arithmetic expressions (算术表达式), 55
- methods, 355
- minusSet: method, 362
- mm 文件扩展名, 144
- modulus operator (取模运算符), 60–61
- month (月份) 枚举数据程序, 206–208
- month names program, 327–328
- moveitemAtPath: method, 371, 374, 377
- multidimensional arrays (多维数组), 252–254
- 4 x 5 矩阵, 252
- declaring, 253
- initializing, 252–254
- notation (符号), 252
- multiple arguments, 135–139
- adding to 接收者, 138
- dot operator (点运算符), 138
- Fraction (分数) 类, 139
- names, 135
- no names, 137
- references (引用), 337

# NSCopying 协议 527

- multiple objects, 45
- expressions (表达式), 235
- multiple protocols, 226
- multiplication operator (乘法运算符), 55
- methods (分类)
- defined. 另见 define 语句
- InfoPlist bundle, 396
- argument (参数), 242
- case sensitivity (大小写敏感), 34

# 530 个对象

- 数据类型, 430, 434–436
- 方法, 430
- 过程, 431
- 测试程序, 432–433
- 初始化, 40, 193–197
- 数组, 196
- 方法的 init 前缀, 196
- 创建方法, 197
- 重写方法, 195–196
- 语法, 197–198
- 手动引用计数, 402–405
- 自动释放池, 403–405
- 悬空指针引用, 443
- 释放, 402
- 递减, 402
- 递增, 402
- 方法, 402
- 方法, 28
- 分配, 146
- 选择, 155–156
- 返回, 146
- 多个, 42–45
- 选择名称, 34
- 数字, 307–311
- 分配方法, 309
- 比较, 311
- 创建, 309
- 引用, 41–42
- 集合
  - 添加/移除对象, 360
  - 计数, 361
  - 等等测试, 360
  - 交集, 360
  - 程序操作, 358–360
  - 有序索引, 362–364
  - 概述, 358
  - 并集, 360
- 静态类型, 183–184
- 字符串
  - 创建, 312
  - 描述方法, 313–314
  - 显示, 313
  - 不可变。见不可变字符串对象
  - 可变。见可变字符串对象
- NSString 类, 312, 324–326
- 程序, 312–313
- unichar 字符, 312
- 临时, 410–411
- 值,设置, 40–41
- 变量, 定义, 299
- 奇/偶整数, 98–100
- offsetFile 方法, 390
- 异或补运算符 (*), 211, 214–215
- OpenGL 游戏模板, 450
- 打开文件, 390
- OPENSTEP, 1
- operatingSystem 方法, 387
- operatingSystemName 方法, 387
- operatingSystemVersionString 方法, 387
- 运算符
  - & (地址), 274, 275
  - — (递减), 78
  - — 数组的指针, 282–284
- double 对象, 创建, 310
- NSNumber 类列表, 310
- initWithInteger: 方法, 311
- 程序, 307–309
- 存储的值,检索, 310
- 值,编辑, 311
- 值,检索, 309
- 协议遵循, 227–228
- 前/后, 287-289
- ++ (递增), 77-137
- + 数组的指针, 282-284
- 前/后, 287-289
- * (间接), 274, 255
- -= (减赋值), 64
- += (加赋值), 64
- -> (结构体指针), 278
- , (逗号), 294-295
- 赋值与算术
  - 组合, 64
- + 位
  - 与 (AND), 212-213
  - 二进制/十六进制转换, 212
  - 异或 (Exclusive-OR), 214
  - 或是 (Inclusive-OR), 213-214
  - 左移, 216
  - 列表, 211
  - 异或补, 214-215
  - 程序示例, 215-216
  - 右移, 216-217
- 复合, 101
- 条件
  - 宏, 239
  - 语法, 122
  - 变量值,赋值, 122-153
  - 定义, 55
- 点 (运算符
  - 多参数, 138
  - 属性,访问, 134-135
  - 取模, 60-61
  - 优先级, 55-58
  - 关系, 74-75
  - sizeof, 295-296
  - 类型转换, 63-211
- 可选指令, 230
- 逻辑或运算符 (||), 101
- 初始实例变量, 161
- 初始方法, 162
- outlet 变量
  - 连接, 460
  - 定义, 453
- 重写方法, 169-273
- 类别, 225
- init 方法, 196-197

# P

- + 宏指令, 199
- 基于页的应用程序模板, 450
- pathComponents 方法, 383, 384
- pathExtension 方法, 383, 384
- 路径名, 370
  - 在末添加文件名, 383
  - 数组,返回, 383
  - 创建, 384
  - 解构, 384
  - 目录,定位, 385
  - 扩展
    - 添加, 384
    - 提取, 384
    - 移除, 384
  - 文件扩展名, 383
  - 全路径, 370
  - 硬编码, 370
  - 目录, 383
  - 最后组件
    - 解构, 384
    - 移除, 384
  - 最后文件,提取, 383
- NSPathUtilities.class, 381
- 路径,末尾添加, 384
- 相对, 370
- 标准化, 384
- 声明, 275
- 符号链接, 384
- 函数, 291-292
- 临时目录, 384
- id 数据类型, 300
- 用户信息,返回, 384
- 间接, 273
- pathWithComponents: 方法, 384
- 整数, 274
- 百分号 (%), 24
- 内存地址, 292-293
- performSelector: 方法, 185-186
- 程序示例, 275
- 短语, daylighting
- 结构体, 277–279
- 在 Objective-C 中编程变得越来越有趣！程序, 22
- 减法, 290
- 多态
  - 复杂类示例, 177-180
  - 定义, 180
- 加扩展名, 14
- 加等号 (=) 运算符, 64
- 井号 (#), 233
- 处理器, 233
- 算术运算符, 55
- 条件
  - if 语句, 243
  - 名称,定义, 242
  - 指针, 273
  - & (地址), 274, 275
  - * (间接), 274, 255
  - 程序,调试, 243
  - 系统语句, 241
  - 参数, 279–284
  - 字符串,定义, 233
  - 关系, 274
  - 字符串, 285
  - else,定义, 244
  - 赋值, 281
  - if, 281
  - 元素, 283
  - 整数, 284
  - 数组, 281
  - 递增/递减运算符, 211
  - 数组,创建, 118–119
  - 集合, 360
  - 字符串, 286
  - 引用, 41
  - 自动释放池, 403
  - 类, 199
  - 程序, 534
  - 方法, 254
  - initWithInteger: 方法, 311
  - 遵循, 227
  - 类别, 169–273
  - 字符串,不可变, 414
  - 字符串,可变, 415
  - 程序操作, 39
  - 方法, 162
  - 概述, 358
  - 结果, 317
  - 变量, 299
  - 变量, 31
  - ,, 3
- 结果, 41
- 结果, 33
- 结果, 41
- 结果, 17
- 窗口, 17
- Xcode 图标, 8
- 数组, 196



# 索引

## 数据类型
- 数据类型, 430, 434–436
- 方法, 430
- 过程, 431
- 测试程序, 432–433

## 初始化
- 初始化, 40, 193–197
- 数组, 196
- 方法的 `init` 前缀, 196
- 创建方法, 197
- 重写方法, 195–196
- 语法, 197–198

## 内存管理
- 手动引用计数, 402–405
- 自动释放池, 403–405
- 悬空指针引用, 443
- 释放, 402
- 递减, 402
- 递增, 402
- 方法, 402

## 方法
- 方法, 28
- 分配, 146
- 选择, 155–156
- 返回, 146
- 多个, 42–45
- 选择名称, 34

## 数字
- 数字, 307–311
- 分配方法, 309
- 比较, 311
- 创建, 309
- 引用, 41–42

## 集合
- 集合
  - 添加/移除对象, 360
  - 计数, 361
  - 等等测试, 360
  - 交集, 360
  - 程序操作, 358–360
  - 有序索引, 362–364
  - 概述, 358
  - 并集, 360

## 静态类型
- 静态类型, 183–184

## 字符串
- 字符串
  - 创建, 312
  - 描述方法, 313–314
  - 显示, 313
  - 不可变。见不可变字符串对象
  - 可变。见可变字符串对象
- `NSString` 类, 312, 324–326
- 程序, 312–313
- `unichar` 字符, 312

## 临时
- 临时, 410–411

## 值与变量
- 值,设置, 40–41
- 变量, 定义, 299
- 奇/偶整数, 98–100

## 方法与运算符
- `offsetFile` 方法, 390
- 异或补运算符 (`*`), 211, 214–215
- OpenGL 游戏模板, 450
- 打开文件, 390
- OPENSTEP, 1
- `operatingSystem` 方法, 387
- `operatingSystemName` 方法, 387
- `operatingSystemVersionString` 方法, 387

### 运算符
- 运算符
  - `&` (地址), 274, 275
  - `—` (递减), 78
  - `—` 数组的指针, 282–284
- `double` 对象, 创建, 310
- `NSNumber` 类列表, 310
- `initWithInteger:` 方法, 311
- 程序, 307–309
- 存储的值,检索, 310
- 值,编辑, 311
- 值,检索, 309
- 协议遵循, 227–228
- 前/后, 287-289
- `++` (递增), 77-137
- `+` 数组的指针, 282-284
- 前/后, 287-289
- `*` (间接), 274, 255
- `-=` (减赋值), 64
- `+=` (加赋值), 64
- `->` (结构体指针), 278
- `,` (逗号), 294-295
- 赋值与算术
  - 组合, 64
- 位
  - 与 (AND), 212-213
  - 二进制/十六进制转换, 212
  - 异或 (Exclusive-OR), 214
  - 或是 (Inclusive-OR), 213-214
  - 左移, 216
  - 列表, 211
  - 异或补, 214-215
  - 程序示例, 215-216
  - 右移, 216-217
- 复合, 101
- 条件
  - 宏, 239
  - 语法, 122
  - 变量值,赋值, 122-153
  - 定义, 55
- 点 (运算符
  - 多参数, 138
  - 属性,访问, 134-135
  - 取模, 60-61
  - 优先级, 55-58
  - 关系, 74-75
  - `sizeof`, 295-296
  - 类型转换, 63-211
- 可选指令, 230
- 逻辑或运算符 (`||`), 101

## 初始化与重写
- 初始实例变量, 161
- 初始方法, 162
- outlet 变量
  - 连接, 460
  - 定义, 453
- 重写方法, 169-273
- 类别, 225
- `init` 方法, 196-197

# P

- 宏指令, 199
- 基于页的应用程序模板, 450
- `pathComponents` 方法, 383, 384
- `pathExtension` 方法, 383, 384

## 路径名
- 路径名, 370
  - 在末尾添加文件名, 383
  - 数组,返回, 383
  - 创建, 384
  - 解构, 384
  - 目录,定位, 385
  - 扩展
    - 添加, 384
    - 提取, 384
    - 移除, 384
  - 文件扩展名, 383
  - 全路径, 370
  - 硬编码, 370
  - 目录, 383
  - 最后组件
    - 解构, 384
    - 移除, 384
  - 最后文件,提取, 383
- `NSPathUtilities.class`, 381
- 路径,末尾添加, 384
- 相对, 370
- 标准化, 384
- 声明, 275
- 符号链接, 384
- 函数, 291-292
- 临时目录, 384
- `id` 数据类型, 300
- 用户信息,返回, 384
- 间接, 273
- `pathWithComponents:` 方法, 384
- 整数, 274
- 百分号 (`%`), 24
- 内存地址, 292-293
- `performSelector:` 方法, 185-186
- 程序示例, 275
- 短语, daylighting
- 结构体, 277–279
- 在 Objective-C 中编程变得越来越有趣！程序, 22
- 减法, 290

## 多态
- 多态
  - 复杂类示例, 177-180
  - 定义, 180

- 加扩展名, 14
- 加等号 (`=`) 运算符, 64
- 井号 (`#`), 233
- 处理器, 233
- 算术运算符, 55

### 条件
- 条件
  - `if` 语句, 243
  - 名称,定义, 242
  - 指针, 273
  - `&` (地址), 274, 275
  - `*` (间接), 274, 255
  - 程序,调试, 243
  - 系统语句, 241
  - 参数, 279–284
  - 字符串,定义, 233
  - 关系, 274
  - 字符串, 285
  - `else`,定义, 244
  - 赋值, 281
  - `if`, 281
  - 元素, 283
  - 整数, 284
  - 数组, 281
  - 递增/递减运算符, 211
  - 数组,创建, 118–119
  - 集合, 360
  - 字符串, 286
  - 引用, 41
  - 自动释放池, 403
  - 类, 199
  - 程序, 534
  - 方法, 254
  - `initWithInteger:` 方法, 311
  - 遵循, 227
  - 类别, 169–273
  - 字符串,不可变, 414
  - 字符串,可变, 415
  - 程序操作, 39
  - 方法, 162
  - 概述, 358
  - 结果, 317
  - 变量, 299
  - 变量, 31

## Rectangle 类
- Rectangle 类 535
- 三角形数表示例, 75-79
- 终止, 21
- 三角形数，计算
- 块, 263-265
- `calculateTriangularNumber`
- 函数, 255-257
- 值运算符 值表达式
- `else if` 语句, 112-114
- `switch` 语句, 116-117
- 如果预防会发生什么, 112
- `XYPoint` 类, 164-165
- 子类, 227
- `UITableViewDataDataSource`, 229
- `UITableViewDelegate`, 229
- 原型声明, 259-260
- `ublic` 指令, 199
- `purchaseDate` 变量, 272

![](img/22d1310b7c22ea2d48cd2058929a5cda_551_0.png)

### 修饰符 (qualifiers)
- 修饰符 (qualifiers)
  - `long`, 53-54
  - `long long`, 54
  - `short`, 54
  - `unsigned`, 54
- 问号 (`?`), 条件运算符, 122
- 询问类对象, 185
- 创建对象, 186
- 成员关系, 186
- 对方法的响应, 186–187
- 测试程序, 187-189

### 属性 (properties)
- 属性 (properties)
  - 访问, 134-135
  - display
    - 访问器方法，自动合成, 454-455
    - 声明, 454
    - 实例变量, 200
- 属性列表。参见 XML 属性列表
- `protected` 指令, 199
- `protocol` 指令, 226

![](img/22d1310b7c22ea2d48cd2058929a5cda_551_1.png)

### 协议 (protocols)
- 协议 (protocols)
  - 采用, 226
  - 类别采用, 226
  - 定义, 226
  - 定义, 226-227
  - 委托, 229
  - 绘制, 227
  - 现有定义，扩展, 228
  - 非正式的, 229-230
  - 多个, 226
  - 命名, 228
  - `NSCopying`, 226
  - 对象符合, 227-228
- `rangeOfString:` 方法, 324
- `readOfLength:` 方法, 390
- `readDataToEndFile` 方法, 390

## 读取
- 读取
  - 文件, 390
  - 键值存档, 428–429
  - XML 属性, 427
- 接收者, 145

### Rectangle 类
- Rectangle 类
  - 声明, 156-158
  - 定义, 163-164
  - getter 方法, 168
  - `origin:` 方法, 162
  - `setOrigin:` 方法, 162
- 快速帮助, 304-305

# 536 Rectangle 类
- 重命名文件, 371
- setter 方法, 168
- `replaceCharacters: rangeString:`
- `Square` 子类, 158–160
- `nsstring` 方法, 326
- 存储信息, 161

### XYPoint 子类
- XYPoint 子类
  - 方法, 352
  - 类指令, 161–162
  - `replaceOccurrencesOfString:` 方法, 324, 327
  - 声明/定义, 160–163
  - 预留命名, 34
  - 程序, 164–165
- `respondsToSelector:` 方法, 185, 187
- 形，创建, 271–272
- 恢复数据, 438–439
- `reduce` 方法
- `return` 语句, 257
- 创建, 140

## 返回值
- 返回值
  - 声明, 142–143
  - 声明, 36
  - 定义, 143–144
- 函数
  - 程序, 144–145
  - 声明, 259

## 约分程序
- 约分程序
  - 最大公约数程序, 257–259
  - `inside add:` 方法, 145
  - 忽略, 259
  - `outside add:` 方法, 144–145
- 概述,
- 引用计数
  - 从方法返回对象, 146
  - 自动：参见 ARC
  - 手动。参见引用计数
- 翻转数字程序
- 非 ARC 编译代码, 411
- `do` 循环, 89–90
- 强变量, 408
- `while` 循环, 87–88
- 弱变量, 409–411
- 右移运算符 (`>>`), 211, 216–217
- 声明, 410
- 委托, 410
- ReactNative, Dennis, 1
- 根类, 151
- 强引用对象, 409
- 支持, 410

## 常程
- 常程
  - `NSLog`, 21
  - 关系运算符, 74–75
  - `%` 字符, 24
  - 相对文件位置, 393
- 数组, 309–330
- 路径名, 370
- 短语，显示, 21
- 字符串对象, 313
- `removeAllObjects` 方法, 357, 362
- 变量值，显示, 325
- `removeCard:` 方法, 344–347
- `removeCard:` 方法, 34
- scaf, 79, 108
- `removeItemAtPath:` 方法, 371, 377

## 运行程序
- 运行程序
  - `removeObject:` 方法, 352, 362
  - Terminal, 18–19
  - Xcode, 15–16
- `removeObjectAtIndex:` 方法, 352
- 运行时到编译时间, 182–183
- `removeObjectIdenticalTo:` 方法, 345

# S

- 数组排序 537
- `scanf` 常程, 79, 108
- 操作程序, 358–360

## 作用域
- 作用域
  - 有序索引, 362–364
  - 实例变量, 198
  - 联合, 360
- 指令, 199
- `setSide:` 方法, 159
- 继承, 198
- `setString:` 方法, 324, 326
- 变量, 198
- setter 方法, 48
- 拷贝对象, 421–423
- SDK (iOS), 447
- `Rectangle` 类, 168
- `seekToEndFile` 方法, 391
- `seekToFileOffset` 方法, 391
- `setWithCapacity:` 方法, 361

## 选择
- 选择
  - 浅拷贝, 417
  - `self` 关键字, 145
  - `short` 修饰符, 54
  - 分号(`;`), 21
  - `side` 方法, 159

### 接口/实现
- 接口/实现
  - 符号, 127–132
  - 定义, 105
  - 实现文件, 129–132
  - 界面 (iPhone), 249
  - 序列化数组, 248–249
  - 扩展的, 228
  - 选择, 252
  - 按钮, 360
- `setAttributes:` 方法, 371
- 分子方法, 451
- 模板, 450
- `setEmail:` 方法, 332
- `setName:` 方法, 332
- 文件, 374
- `setNameAnd:` 方法, 335
- 标签, 458
- `sizeof` 运算符, 295
- `setObjectName:` 方法, 357
- 键值存档, 429
- `setProcess:` 方法, 386
- `sortComparator:` 方法, 352
- `sortUsingSelector:` 方法, 340

## 排序数组
- 排序数组
  - 键值存档, 350
  - 类别, 351
  - 计数, 361
  - 等等测试, 347
  - `NSArray` 类, 352
  - `NSMutableArray` 类, 352

# 540 stringFormat: format, arg1, arg2, arg3 . . . method
- `stringFormat: format, arg1, arg2, arg3 . . . method`
- `stringFormat: format, arg1, arg2.arg3... method`, 325
- `stringWithString:` nsstring method, 325
- 强变量, 408-409
- 结构指针运算符 (`->`), 278

## 结构
- 结构
  - 在另一个结构中定位字符串, 320
  - 范围, 320
  - 指定索引字符, 319
  - `substringToIndex:` method, 319, 325
  - `substringWithRange:` method, 320, 325
- 指针减法, 290
- 减法运算符, 55
- 求和变量, 24

## 变量
- 变量
  - 日期
    - 定义, 266-267
    - 初始化, 269-270
    - 月份值, 测试, 267-269
    - 指针, 277-279
    - 程序, 268-269
    - todays/purchaseDate 变量,
      - 声明, 272
      - 表达式, 求值, 269
      - 初始化, 269-270
      - 实例变量, 存储, 298-299
      - 命名, 省略, 272
      - 指针, 277-279
      - 在结构内部创建, 270-272
    - 语法, 267
  - 超类, 152-153
  - 支持, 论坛网站, 5

## switch 语句
- `switch` 语句
  - `break` 语句, 115
  - `case` 取值, 117
  - 语法, 114-116
- 值运算符值表达式
  - 程序, 116-117
  - 在结构定义中声明, 272
  - 初始值, 赋值, 272
  - 子类, 152-153

## 语法
- 语法
  - `@` (at 符号), 21
  - `{ }` (大括号), 21
  - `_` (下划线), 200
  - 参数, 256
  - 空格, 103
  - 块, 262-263
  - 大小写敏感, 19
  - 类扩展, 224-225
  - 益处, 173
  - 创建, 158-160
  - 定义, 173
  - 代理 (delegate), 452
  - 继承, 230
  - 协议 (protocols), 227
  - 下标, 248
  - 注释
    - `//` (斜杠字符), 20
    - `/* */`, 20



# 索引

## 符号

- **适用**, 20
- **定义**, 20
- **条件运算符**, 122
- **常量**, 21
- **define 语句**, 234
- **do 循环**, 88
- **else if 语句**, 105-106
- **函数**, 254
- **if 语句**, 93
- **substringFromIndex: method**, 319, 325
- **子字符串**
  - 创建, 318-320
  - 从字符串内部提取, 320
  - 前导字符, 319
- **Utility Application 模板**, 541

## A

- **实现文件**, 37
- **终止程序**, 21
- **接口文件**, 33
- **测试文件**, 创建, 374
- **行位置**, 19
- **线程安全代码**
  - 互斥锁, 422
- **for 循环**, 83
- **抛出异常**, 191
- **方法**, 28-29
- **波浪号 (-)**
  - 主目录, 370
- **多维数组**, 252-253
- **todayDateVariable**, 272
- **多个参数**, 135
- **三角形数**, 计算
- **换符**, 22
- **块**, 263–265
- **对象初始化**, 195–196
- **calculateTriangularNumber 函数**, 255–257
- **属性**, 134–135
- **true 值**, 119–121
- **语句**, 21
- **truncateFileAtOffset: method**, 391
- **结构**, 267
- **try 指令**, 190
- **switch 语句**, 114–116
- **二维数组**, 252
- **终止程序**, 21
- **类型强制转换运算符**, 63–64, 21
- **while 循环**, 84
- **typedef 语句**, 208–209, 270
- **synthesize 指令**, 133
- **定义**, 270–271
- **合成访问器方法**, 200
- **变量**, 271
- **AddressCard 类**, 334–337
- **显示属性**, 454–455
- **synthesize 指令**, 132–133
- **系统依赖**, 241–243

## U

- **UILabel 类**, 454
- **UITableView 类**, 229
- **UITableViewDataSource 协议**, 229
- **UIViewDelegate 协议**, 229
- **unarchiveObjectWithField: method**, 428-429
- **undef 语句**, 244
- **下划线 ()**, 200
- **Unicode 字符**, 312
- **union: method**, 360
- **unionSet: method**, 362
- **无符号限定符**, 54
- **解包 (unwrapping)**, 353-354
- **uppercaseString**, 326
- **UTF8String method**, 326
- **Utility Application 模板**, 450

## T

- **Tabbed Application 示例**, 450
- **三角形数表示例**, 75-79
- **模板 (iOS 应用程序)**, 449-450
- **临时目录**, 383
- **临时对象**, 410
- **Terminal (终端)**
  - 缺点, 19
  - 程序, 创建, 17
  - 编译并运行, 18–19
  - 输入程序, 17–18
  - 启动, 17
  - 窗口, 17
  - 启动, 17
- **值运算符值表达式**
  - else if 语句, 112–114
  - 数组, 250–251
  - define 语句, 233–234
  - 最大的公约数, 257
  - 视图, 257
  - 赋值, 272
  - 指针, 274
  - 局部变量, 266
  - 内存, 265
  - true/false 值, 119–121
  - 数组, 122–123
  - 显示, 25
  - 块, 263–265
  - 属性, 266
  - true/false 值, 119–121
  - 声明, 24
  - 数组, 250–251
  - define 语句, 233–234
  - 最大的公约数, 257
  - 视图, 257
  - 赋值, 272
  - 指针, 274
  - 局部变量, 266
  - 内存, 265
  - true/false 值, 119–121
  - 数组, 122–123
  - 显示, 25
  - 块, 263–265
  - 属性, 266
  - true/false 值, 119–121
  - 声明, 24
