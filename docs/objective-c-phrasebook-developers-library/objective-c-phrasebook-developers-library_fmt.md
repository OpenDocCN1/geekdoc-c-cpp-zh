
# Objective-C 常用句手册（开发者库）

## 核心代码与命令

- 总编辑：Mark Taub
- 采买编辑：Mark Taber
- 开发编辑：Michael Thurston
- 执行编辑：Kristy Hart
- 项目编辑：Anne Goebel
- 文字编辑：Bart Reed
- 校对员：Charlotte Kughen
- 出版协调员：Vanessa Evans
- 封面设计：Gary Adair
- 排字员：Gloria Schurick

- 返回错误：222
- 消息转发：315

## 关于作者

David Chisnall 是一位自由职业作家和顾问。在攻读博士期间，他共同创立了 Étoilé 项目，该项目旨在基于 GNUstep（OpenStep 和 Cocoa API 的开源实现）开发一个开源桌面环境。他是 GNUstep 的活跃贡献者，也是 GNUstep Objective-C 2 运行时库以及 Clang 编译器中相关支持的原作者和维护者。

获得博士学位后，David 在学术界隐藏了一段时间，研究编程语言的历史。当他发现有些地方拥有同样优美的海景而且不需要处理那么多文书时，他最终离开了学术界。他偶尔会参与涉及动态语言语义的项目。

David 对 Objective-C 有深入了解，既参与过使用该语言的项目，也参与过该语言本身的实现。他还曾在 Objective-C 运行时之上实现过其他语言，包括 Smalltalk 和 JavaScript 的方言，允许在无需桥接的情况下混合使用这些语言的代码。

在不写作或编程时，David 喜欢跳阿根廷探戈和古巴萨萨舞、打羽毛球和极速飞盘，以及烹饪。

## 致谢

在写一本关于 Objective-C 的书时，我第一个应该感谢的人是 Nicolas Roard。在我开始读博士学位的同时，我买了第一台 Mac，并计划用它来写 Java 代码，因为不想学习一种私有语言。当我开始博士课程时，发现自己正和 Nicolas 一起工作，他是一个活跃的 GNUstep 贡献者。他说服了我 Objective-C 和 Cocoa 不仅适用于 Mac，而且它们都是值得学习的。他是完全正确的：Objective-C 是一门非常优雅的语言，而配套的框架让开发变得异常简单。

下一个要感谢的人是 Fred Kiefer。Fred 是 AppKit 框架的 GNUstep 实现的维护者。他对本书进行了极其详尽（读作：吹毛求疵）的技术审阅，发现了多处可以解释得不够理想的地方。如果你喜欢这本书，那么 Fred 应该享有很大一部分功劳。

最后，我需要感谢其他参与将这本书从我的文本编辑器送到你手中的每一个人，特别是最初向我提出这个想法的 Mark Taber。

## 我们希望听取你的意见

作为本书的读者，你是我们最重要的批评家和评论者。我们重视你的意见，并想知道我们做得好的地方、哪些可以做得更好、你希望我们出版哪些领域的内容，以及任何其他愿意分享给我们的智慧建议。

你可以直接发邮件或写信给我，告诉我你对这本书的喜欢或不喜欢之处——以及我们可以做什么来让我们的书籍更强大。

请注意，我无法帮助你解决与本书主题相关的技术问题，而且由于收到的邮件量很大，我可能无法回复每一条信息。

在你写信时，请务必写上书名、作者，以及你的姓名和电话或邮箱地址。我会仔细审查你的评论，并将它们与参与本书的作者和编辑分享。

**邮箱：**`mark.taber@pearson.com`

**邮件：**

Mark Taber  
Associate Publisher  
Addison Wesley Publishing  
800 East 96th Street  
Indianapolis, IN 46240 USA

## 读者服务

访问我们的网站并在`informit.com/aw`注册这本书，以便方便获取该书可能提供的更新、下载或勘误。

# 引言

Blaise Pascal 曾写道：“我没有时间写封短信，所以我写了一封长信。”这本书不到 350 页（小开本），是我写过最短的书，试图将我想说的所有内容挤进这么短的一卷书中是一项挑战。

当 Mark Taber 最初建议我写一本 Objective-C 短语手册时，我并不确定它会是什么样子的。自然语言的短语手册是一系列短习语，供那些发现自己需要快速一两句话的人使用。编程语言的短语手册应该承担类似的角色。

本书并不是语言参考书。Apple 在`http://developer.apple.com`网站上提供了关于 Objective-C 语言的熟练参考资料。这不是一份详尽的教程；与我的另一本 Objective-C 书籍《Cocoa Programming Developer’s Handbook》不同，你在这里找不到作为代码的完整程序。相反，你将看到非常短的 Objective-C 惯用法示例，希望你可以在广泛的场景中使用这些示例。

生活中最令人沮丧的事情之一是发现书中的代码示例实际上无法运行。书中了两类代码列表。白色背景上的代码旨在说明一个简单的点。这些代码可能依赖某些隐含的上下文，不应被视为可运行、可用的示例。你在书中看到的大部分代码都在灰色背景上。在每个示例的底部，你会找到该列表所在的文件名。你可以从 InformIT 网站上的书籍页面下载这些：`http://www.informit.com/title/0321743628`

## 关于排版的说明

本书使用 Vim 编写，并采用语义标记。从这里生成了三个不同的版本。其中两个是使用`pddfatex`创建的。如果你阅读的是纸质版或 PDF 版本，就能看到其中之一。两者唯一的区别是纸质版包含了裁切标记，以便打印机裁剪页面。

第三个版本是 XHTML，用于 ePub 版本。它是使用 EtoileText 框架创建的，该框架首先将 LaTeX 风格标记标记为树结构，然后执行一些转换以处理交叉引用和索引，最后生成 XHTML。执行这些操作的代码全部是用 Objective-C 编写的。

如果你两个版本都能访问，可能会发现 ePub 版中的代码列表看起来稍微好看。这是因为 EtoileText 使用了 SourceCodeKit（另一个 Étoilé 框架）来进行语法高亮。它使用了 Clang（一种现代的 Objective-C 编译器）的一部分对代码列表进行标记。这意味着代码范围被赋予了与编译器看到的完全相同的语义类型。例如，它可以区分函数调用和宏实例化。

你可以在 Étoilé 的 subversion 仓库中找到执行这些操作的代码：`http://svn.gna.org/viewcvs/etoile/trunk/Etoile/`

## Objective-C 哲学

要理解 Objective-C，你需要理解其创建背后的哲学。与设计为新的类语言的 C++、D 或 Java 不同，Objective-C 是一门混合语言。它是 C 的纯超集，意味着每一段 C 代码都是有效的 Objective-C 代码。

在我开始读博士学位的同时，我买了第一台 Mac，并计划用它来写 Java 代码，因为不想学习一种私有语言。当我开始博士课程时，我发现自己正和 Nicolas 一起工作，他是一个活跃的 GNUstep 贡献者。他说服了我 Objective-C 和 Cocoa 不仅适用于 Mac，而且它们都值得学习的。他是完全正确的：Objective-C 是一门非常优雅的语言，而配套的框架让开发变得异常简单。

下一个要感谢的人是 Fred Kiefer。Fred 是 AppKit 框架的 GNUstep 实现的维护者。他对本书进行了极其详尽（读作：吹毛求疵）的技术审阅，发现了多处可以解释得不够理想的地方。如果你喜欢这本书，那么 Fred 应该享有很大一部分功劳。

最后，我需要感谢其他参与将这本书从我的文本编辑器送到你手中的每一个人，特别是最初向我提出这个想法的 Mark Taber。

## 我们希望听取你的意见

作为本书的读者，你是我们最重要的批评家和评论者。我们重视你的意见，并想知道我们做得好的地方、哪些可以做得更好、你希望我们出版哪些领域的内容，以及任何其他愿意分享给我们的智慧建议。

你可以直接发邮件或写信给我，告诉我你对这本书的喜欢或不喜欢之处——以及我们可以做什么来让我们的书籍更强大。

请注意，我无法帮助你解决与本书主题相关的技术问题，而且由于收到的邮件量很大，我可能无法回复每一条信息。

在你写信时，请务必写上书名、作者，以及你的姓名和电话或邮箱地址。我会仔细审查你的评论，并将它们与参与本书的作者和编辑分享。

**邮箱：**`mark.taber@pearson.com`

**邮件：**

Mark Taber  
Associate Publisher  
Addison Wesley Publishing  
800 East 96th Street  
Indianapolis, IN 46240 USA

## 读者服务

访问我们的网站并在`informit.com/aw`注册这本书，以便方便获取该书可能提供的更新、下载或勘误。

# 引言

这本书不到 350 页（小开本），是我写过最短的书，试图将我想说的所有内容挤进这么短的一卷书中是一项挑战。

当 Mark Taber 最初建议我写一本 Objective-C 短语手册时，我并不确定它会是什么样子的。自然语言的短语手册是一系列短习语，供那些发现自己需要快速一两句话的人使用。编程语言的短语手册应该承担类似的角色。

本书并不是语言参考书。Apple 在`http://developer.apple.com`网站上提供了关于 Objective-C 语言的熟练参考资料。这不是一份详尽的教程；与我的另一本 Objective-C 书籍《Cocoa Programming Developer’s Handbook》不同，你在这里找不到作为代码的完整程序。相反，你将看到非常短的 Objective-C 惯用法示例，希望你可以在广泛的场景中使用这些示例。

生活中最令人沮丧的事情之一是发现书中的代码示例实际上无法运行。书中了两类代码列表。白色背景上的代码旨在说明一个简单的点。这些代码可能依赖某些隐含的上下文，不应被视为可运行、可用的示例。你在书中看到的大部分代码都在灰色背景上。在每个示例的底部，你会找到该列表所在的文件名。你可以从 InformIT 网站上的书籍页面下载这些：`http://www.informit.com/title/0321743628`

## 关于排版的说明

本书使用 Vim 编写，并采用语义标记。从这里生成了三个不同的版本。其中两个是使用`pddfatex`创建的。如果你阅读的是纸质版或 PDF 版本，就能看到其中之一。两者唯一的区别是纸质版包含了裁切标记，以便打印机裁剪页面。

第三个版本是 XHTML，用于 ePub 版本。它是使用 EtoileText 框架创建的，该框架首先将 LaTeX 风格标记标记为树结构，然后执行一些转换以处理交叉引用和索引，最后生成 XHTML。执行这些操作的代码全部是用 Objective-C 编写的。

如果你两个版本都能访问，可能会发现 ePub 版中的代码列表看起来稍微好看。这是因为 EtoileText 使用了 SourceCodeKit（另一个 Étoilé 框架）来进行语法高亮。它使用了 Clang（一种现代的 Objective-C 编译器）的一部分对代码列表进行标记。这意味着代码范围被赋予了与编译器看到的完全相同的语义类型。例如，它可以区分函数调用和宏实例化。

你可以在 Étoilé 的 subversion 仓库中找到执行这些操作的代码：`http://svn.gna.org/viewcvs/etoile/trunk/Etoile/`

## Objective-C 哲学

要理解 Objective-C，你需要理解其创建背后的哲学。与设计为新的类语言的 C++、D 或 Java 不同，Objective-C 是一门混合语言。它是 C 的纯超集，意味着每一段 C 代码都是有效的 Objective-C 代码。

在我开始读博士学位的同时，我买了第一台 Mac，并计划用它来写 Java 代码。当我开始读博士时，我发现自己正和 Nicolas 一起工作，他是一个活跃的 GNUstep 贡献者。他说服了我 Objective-C 和 Cocoa 不仅适用于 Mac，而且它们都值得学习的。他是完全正确的：Objective-C 是一门非常优雅的语言，而配套的框架让开发变得异常简单。

下一个要感谢的人是 Fred Kiefer。Fred 是 AppKit 框架的 GNUstep 实现的维护者。他对本书进行了极其详尽（读作：吹毛求疵）的技术审阅，发现了多处可以解释得不够理想的地方。如果你喜欢这本书，那么 Fred 应该享有很大一部分功劳。

最后，我需要感谢其他参与将这本书从我的文本编辑器送到你手中的每一个人，特别是最初向我提出这个想法的 Mark Taber。

## 我们希望听取你的意见

作为本书的读者，你是我们最重要的批评家和评论者。我们重视你的意见，并想知道我们做得好的地方、哪些可以做得更好、你希望我们出版哪些领域的内容，以及任何其他愿意分享给我们的智慧建议。

你可以直接发邮件或写信给我，告诉我你对这本书的喜欢或不喜欢之处——以及我们可以做什么来让我们的书籍更强大。

请注意，我无法帮助你解决与本书主题相关的技术问题，而且由于收到的邮件量很大，我可能无法回复每一条信息。

在你写信时，请务必写上书名、作者，以及你的姓名和电话或邮箱地址。我会仔细审查你的评论，并将它们与参与本书的作者和编辑分享。

**邮箱：**`mark.taber@pearson.com`

**邮件：**

Mark Taber  
Associate Publisher  
Addison Wesley Publishing  
800 East 96th Street  
Indianapolis, IN 46240 USA

## 读者服务

访问我们的网站并在`informit.com/aw`注册这本书，以便方便获取该书可能提供的更新、下载或勘误。

# 引言

这本书不到 350 页（小开本），是我写过最短的书，试图将我想说的所有内容挤进这么短的一卷书中是一项挑战。

当 Mark Taber 最初建议我写一本 Objective-C 短语手册时，我并不确定它会是什么样子的。自然语言的短语手册是一系列短习语，供那些发现自己需要快速一两句话的人使用。编程语言的短语手册应该承担类似的角色。

本书并不是语言参考书。Apple 在`http://developer.apple.com`网站上提供了关于 Objective-C 语言的熟练参考资料。这不是一份详尽的教程；与我的另一本 Objective-C 书籍《Cocoa Programming Developer’s Handbook》不同，你在这里找不到作为代码的完整程序。相反，你将看到非常短的 Objective-C 惯用法示例，希望你可以在广泛的场景中使用这些示例。

生活中最令人沮丧的事情之一是发现书中的代码示例实际上无法运行。书中了两类代码列表。白色背景上的代码旨在说明一个简单的点。这些代码可能依赖某些隐含的上下文，不应被视为可运行、可用的示例。你在书中看到的大部分代码都在灰色背景上。在每个示例的底部，你会找到该列表所在的文件名。你可以可以从 InformIT 网站上的书籍页面下载这些：`http://www.informit.com/title/0321743628`

## 关于排版的说明

本书使用 Vim 编写，并采用语义标记。从这里生成了三个不同的版本。其中两个是使用`pddfatex`创建的。如果你阅读的是纸质版或 PDF 版本，就能看到其中之一。两者唯一的区别是纸质版包含了裁切标记，以便打印机裁剪页面。

第三个版本是 XHTML，用于 ePub 版本。它是使用 EtoileText 框架创建的，该框架首先将 LaTeX 风格标记标记为树结构，然后执行一些转换以处理交叉引用和索引，最后生成 XHTML。执行这些操作的代码全部是用 Objective-C 编写的。

如果你两个版本都能访问，可能会发现 ePub 版中的代码列表看起来稍微好看。这是因为 EtoileText 使用了 SourceCodeKit（另一个 Étoilé 框架）来进行语法高亮。它使用了 Clang（一种现代的 Objective-C 编译器）的一部分对代码列表进行标记。这意味着代码范围被赋予了与编译器看到的完全相同的语义类型。例如，它可以区分函数调用和宏实例化。

你可以在 Étoilé 的 subversion 仓库中找到执行这些操作的代码：`http://svn.gna.org/viewcvs/etoile/trunk/Etoile/`

## Objective-C 哲学

要理解 Objective-C，你需要理解其创建背后的哲学。与设计为新的类语言的 C++、D 或 Java 不同，Objective-C 是一门混合语言。它是 C 的纯超集，意味着每一段 C 代码都是有效的 Objective-C 代码。

在我开始读博士学位的同时，我买了第一台 Mac，并计划用它来写 Java 代码，因为不想学习一种私有语言。当我开始博士课程时，我发现自己正和 Nicolas 一起工作，他是一个活跃的 GNUstep 贡献者。他说服了我 Objective-C 和 Cocoa 不仅适用于 Mac，而且它们都值得学习的。他是完全正确的：Objective-C 是一门非常优雅的语言，而配套的框架让开发变得异常简单。

这种差异的副作用之一是

# 第一章：Objective-C 哲学

Objective-C 和 C++ 中的指针转换具有截然不同的语义。在 Objective-C 中，当你将一个指针从一种对象类型转换到另一种对象类型时，不会生成任何代码。这种转换只是对编译器的类型检查器的一种提示。

然而，在 C++ 中，指针转换会执行某些指针算术，以便传递转换后指针的代码能够在正确的位置找到虚函数表（vtable）。这意味着在 Objective-C 中，你可以将任何对象类型转换为任何其他对象类型，而在 C++ 中，你需要使用一种特殊的转换方式。

这种区别非常重要。在 Objective-C 中，影响方法查找的唯一因素是对象的类型。在 C++ 和其他 Simula 家族语言中，查找还会受到编译器认为的对象类型的影响。

## 两个类型系统的故事



让初接触 Objective-C 的人感到困惑的点之一是，它拥有两套类型系统。如果你将原始实现视为一个预处理器，那么这就是有意义的。Objective-C 预处理器会执行类似 Strongtalk¹^ 的类型检查，而 C¹^StrongTalk 是 Smalltalk 的一种方言，添加了可选的静态类型检查。创建该语言的团队后来去开发了 Java。值得注意的是，尽管 StrongTalk 是运行最快的 Smalltalk 实现之一，但编译器并没有使用 C 类型检查。

C 拥有一种结构化类型系统。基本数据类型的等效性基于两个类型是否具有相同的表示。复杂类型永远不会被视为等效的。

Objective-C 增加了代数类型系统。对象的类型由其签名定义：即它声称将响应的消息。你可以隐式地将一个 Objective-C 对象转换为它的父类，因为它被定义为会响应父类所理解的所有消息。

你可以显式地将对象转换为其他类型。例如，你可以将一个字典对象转换为数组对象。只要你之后只向它发送字典和数组都能理解的消息，这种操作就是可行的。

## C 就是 Objective-C

Objective-C 最重要的特性之一是它是 C 的纯超集。你可以将 C 视为嵌入在 Objective-C 中用于低层任务的领域特定语言，而将 Smalltalk 的子集视为嵌入在 Objective-C 中用于高层任务的领域特定语言。使用纯 C 解决问题并没有任何错。许多人在学习 Objective-C 时犯的一个错误是，为了优化静态类型信息，假设他们必须停止使用 C。对于很多事情来说，C 的解决方案才是正确的。

**注意：**

Objective-C 还有一个姐妹语言 Objective-C++，它与 C++ 的关系就像 Objective-C 与 C 的关系一样。Objective-C++ 是 C++ 的纯超集，允许你从 Objective-C 对象调用 C++ 代码，反之亦然。由于它们拥有截然不同的对象模型，你不能用 C++ 派生一个 Objective-C 类，反之亦然；然而，你可以将 Objective-C 对象的指针作为 C++ 对象的字段，并将指向 C++ 对象的指针作为 Objective-C 对象的实例变量。

你可以在 Cocoa 框架中看到这一点。并不是所有内容都是对象。如果你请求字符串中的一段字符范围，你将使用 `NSRange` 结构。这是一个 C 结构——而不是 Objective-C 对象——包含一个位置和一个长度。点（Points）、矩形以及其他几种内容也以类似的方式表示。如果这些都是对象，那么你将消耗更多的内存，使操作变慢，并且并无法真正获得任何灵活性。

面向对象编程的 Ingalls 测试²^ 认为你应该能够创建一种新的整数，并将其用于在屏幕上定位窗口。Objective-C 未能通过这项测试，但该测试是以 Smalltalk 设计者之一提出该要求的 Dan Ingalls 命名的。这在现实世界中并不是一个非常实用的例子，因为大多数时候，设计新类型的整数会破坏许多预期整数具有标准行为的程序。

## 语言与库

在 Objective-C 中，在不需要动态行为的情况下，你不需要使用动态行为（例如延迟绑定和多态）。

对于非常动态的语言，很难在语言和库之间划清界限。在 Smalltalk 中，语言中没有语言的 `if` 语句。标准库定义了 `True` 和 `False` 单例类，它们响应 `-ifTrue:` 消息，并接受闭包作为参数。所有复杂的流控制结构（如循环或枚举）都是基于此实现的。

Objective-C 继承了 C 的流控制，但所有的动态行为都由运行时库（runtime library）提供。这与 C 或 C++ 不同。你可以编译一个不调用 `libc` 或 `libstdc++` 中任何函数的独立 C 或 C++ 二进制文件。每个 Objective-C 程序都必须链接到 `libobjc` 才能运行。该库传统上提供三个类：一个简单的根类、一个字符串类和一个协议类。其中第一个类提供了对象分配，这在 C++ 和 Java 中是语言的一部分。另外两个可能是编译器生成的类。在大多数情况下，你不会使用这些任何一个类。

OpenStep 定义了两个框架：Foundation 和 Application Kit，通常简称为 Foundation 和 AppKit。Foundation 提供了开发者所有应用程序所需的核心功能，例如集合类、运行循环（run loops）、通知传递、操作系统抽象等。Application Kit 构建在 Foundation 之上，为构建图形应用程序提供额外支持。Sun 的实现在最初发布后没有进行开发。Apple 在几年后收购了它，并将其命名为 Yellow Box，作为 Rhapsody 在 Windows 上发布。随着 OS X 的发布，它再次被命名，这次更名为 Cocoa。

## Objective-C 的历史

GNUstep 项目仍在活跃开发，但现在跟踪 Apple 对 OpenStep 规范的增强以及核心规范。这意味着 Foundation 框架几乎可以在任何地方使用，尽管 GNUstep 实现缺少了一些最新的类和方法。你可以将 Foundation 框架看作 Objective-C 的标准库。它为非复杂程序提供了许多所需的功能。若干 Objective-C 2 特性是专门为与 Foundation 协作设计的。你可以在没有 Foundation 的情况下使用它们，但前提是你实现了等的功能。

“面向对象”一词是由 Alan Kay 在 20 世纪 60 年代提出的，Smalltalk 是他和其他人用来演示这种编程风格的语言。Smalltalk 开发于 70 年代，最广泛的版本发布于 1980 年。然而，Smalltalk 运行非常慢。要正确运行它，你需要一台强大的计算机，例如 Xerox Alto，拥有 512KB 内存，且最好有一个 2MHz 的处理器。

Brad Cox 喜欢 Smalltalk 的想法，但他想要一种可以在人们负担得起的计算机上使用的语言。他的想法是将 Smalltalk 这种鼓励

# 第一章：Objective-C 哲学

封装、松耦合和代码复用，这是 C 语言的目标。而 C 处于光谱的另一端，几乎没有封装，没有动态分发，但有一个巨大的优势：它很快。

C 语言高度依赖 PDP-11 指令集。一个非常原始的 C 编译器就能产生相当快的代码。这在今天也是如此。诸如 LLVM、XLC 和 ICC 等编译器在优化上花费了大量精力，但几乎不作优化的 PCC 仍然能生成相当快的代码。

Brad Cox 和 Tom Love 在 1986 年创立了 StepStone，销售一种基于 Brad 早期对象对象预编译器的产品。该产品，即 Objective-C，是一个预处理器和一个较小的 Objective-C 运行时库。该预处理器生成 C 代码，你可以使用平台的 C 编译器对其进行编译。直到 2010 年，我仍遇到过在商业产品中继续使用 StepStone 编译器的公司。

1988 年，NeXT 购买了 StepStone 代码的许可，并直接购买了 Objective-C 的商标。随后，NeXT 将预处理器重写为 GNU 编译器集（GCC）的前端。在经过法律斗争后，自由软件基金强制他们发布了这些代码，但他们保留了运行时库的私有。GNU 项目随后编写了运行时库的替代品，但进行了一些更改。其中一个是 GNU 运行时选择器（selectors）关联了一个类型。在 NeXT（以及 Apple）平台上，选择器仅仅是字符串。这意味着 GNU 运行时可以捕捉由程序员错误导致的堆栈损坏，而这些错误在 NeXT 运行时是不可见的。

另一个变化在于消息传递机制。当你使用 NeXT 运行时发送消息时，编译器会将消息发送转换为对 `objc_msgSend()` 函数的调用。它查找该方法然后调用它。遗憾的是，在 C 中无法实现此函数。它必须为每个平台以及平台上的每种调用约定用汇语言编写。GNU 的解决方案是用 `objc_msg_lookup()` 函数替换它，该函数返回一个函数指针。这稍微慢一点，但意味着相同的代码可以在所有平台上运行。

从此以后 Objective-C 没有发生太大变化。NeXT 在 1997 年被 Apple 收购，Objective-C 被采纳为新操作系统 Rhapsody 上 Yellow Box 的主要开发语言。这些后来分别重命名为 Cocoa 和 OS X。2003 年，Apple 为语言添加了一些类似 Java 的异常处理原语。

下一组升级出现在 2007 年，当时 Apple 推出了 Objective-C 2。这让老 Objective-C 程序员感到有些困惑，因为之前的版本——NeXT 发布的版本——已经是 Objective-C 4。

幸运的是，“2 紧跟在 4 之后”的想法并没有进入 Cocoa 的任何排序代码中。

Objective-C 2 添加了一些语法糖。它提供了一种新的枚举方式、一种合成访问器方法的方法，并引入了垃圾回收。Objective-C 2 与其说是一个营销术语，不如说是一种真正的语言。你找不到用于选择它的编译器开关。某些功能（如非脆弱性实例变量）仅在某些运行时可用。而其他功能（如垃圾回收）在 iPhone 上不可用。声明属性（declared properties）和快速枚举是唯一在处处有效（包括非 Apple 平台）的 Objective-C 2 特性。

## 跨平台支持

迫使 NeXT 将 GCC 的 Objective-C 前端作为自由软件发布，对于自由软件基金会来说是一次公关上的胜利。遗憾的是，从长期跨平台支持的角度来看这并不理想。NeXT 发布的代码非常糟糕，在过去的十年里，很大程度上被 GCC 团队忽略了。

GCC 对 NeXT 时代的 Objective-C 有中等支持，也支持新的异常处理关键字。GNUstep 项目提供了 Foundation 和 AppKit 框架的实现，这些是 NeXT 和 Mac 开发的核心。

2007 年，Apple 开始开发一种新编译器。Clang 是面向 C 系语言（C、Objective-C 和 C++）的低级虚拟机（LLVM）的前端。它比 GCC 更具模块化，并被设计用于代码补全、语法高亮和静态分析，而不仅仅是编译。Clang 在不同层级使用的代码之间有清晰分离，并将运行时特定的代码隔离到单独的类中。

编译器只是 Objective-C 实现的一半。另一半是运行时库。GNU 运行时是用 GCC 开发的，并没有实现 Objective-C 2 所需的函数。为了解决这个问题，我作为 Étoilé 的一部分编写了一个框架，实现了大部分缺失的功能，并实现了 Apple 随 OS X 引入的公共运行时 API。

GNU 运行时是用 GCC 开发的，并没有实现 Objective-C 2 所需的函数。为了解决这个问题，我作为 Étoilé 的一部分编写了一个框架，实现了大部分缺失的功能，并实现了 Apple 随 OS X 引入的公共运行时 API。

GNU 运行时是用 GCC 开发的，并没有实现 Objective-C 2 所需的函数。为了解决这个问题，我作为 Étoilé 的一部分编写了一个框架，实现了大部分缺失的功能和变量……

## 编译 Objective-C 程序

如果你熟悉使用其中任一编译器编译 C 或 C++，你会发现编译 Objective-C 非常熟悉。

Clang 前端被设计为 GCC 的无缝替换品，因此在任何某些指令中看到 `gcc` 的地方，都可以将其替换为 `clang`。在 OS X 上，GCC 安装在 `/usr/bin/gcc`，因此它在你的路径中。在较旧版本的 Xcode 工具中，Clang 安装在 `/Developer/usr/clang`，因此你可能需要指定完整路径，或将此位置添加到你的路径中。在其他平台上，如果安装了它们，你通常可以在你的路径中找到它们。

从命令行运行编译器。

在 OS X 上，你可能会使用 XCode IDE。

这允许你创建具有多种不同模板类型的项目。如果你需要在其他平台上编译这些项目，你可以在 GNUstep 仓库中找到一个名为 `pbxbuild` 的工具，它可以完成编译工作。

如果你在其他平台上进行工作，可以使用 `GNUstep Make` 进行构建。这在 OS X 上同样适用，因此无论你选择哪种方案，都不应该因为构建系统导致可移植性问题。

# 第 2 章：Objective-C 入门

Objective-C 是对 C 语言的一组非常小的扩展。Smalltalk 的第一个版本的创建是基于一种赌注，认为在一张纸上规定出一个整个通用语言是可能的。Objective-C 对 C 的扩展比 Smalltalk 稍微复杂一点，但并没有复杂多少。

如果你已经熟悉 C 语言，那么学习 Objective-C 只需要一个下午——如果你已经理解了 Smalltalk 风格的面向对象，时间会更短。当然，这稍微有一点误导性。如果学习 Objective-C 真的那么简单，你买一本关于它的书时会觉得有点亏了。和 Smalltalk 一样，Objective-C 语言如此简单的很大程度上是因为它将许多工作委托给了库。

原始 StepStone 版本 Objective-C 的标准库非常小。它的设计目的是与 C 库一起使用，而不是作为一种独立的语言。现在，大多数 Objective-C 代码使用基于 NeXT Foundation 框架作为标准库——无论是 Apple 的 Foundation、GNUstep Base 库还是 `libFoundation`。这提供了诸如引用计数内存管理、标准数据结构、转发机制等功能。

你认为属于 Objective-C 语言的一部分的大部分内容实际上是由 Foundation 框架提供的。可以在不使用 Foundation 的情况下使用 Objective-C，但那是人们为了证明自己可以这样做，而不是因为这真的是件明智的事。

## 声明 Objective-C 类型

```objc
6 NSMutableArray *mutableArray = [NSMutableArray new];
7 NSArray *array = mutableArray;
8 NSObject *object = array;
9 id obj = mutableArray;
10 mutableArray = (NSMutableArray*)object;
11 mutableArray = obj;
```

*来源：cast.m*

Objective-C 正如其名，在 C 语言中添加了对象。具体来说，是遵循 Smalltalk 模型的对象，即类的实例。对象始终分配在堆上，因此始终通过指针进行引用。

在 Objective-C 的早期实现中（即从 Objective-C 生成纯 C 代码），类被转换成描述对象布局的结构体定义。你仍然可以在 GCC 的错误信息中看到这种设计的遗留，它偶尔会将对象称为“structures（结构体）”。

在 C 语言中，你需要显式的类型转换才能将任何结构体指针转换为其他类型的结构体指针。这个规则在 Objective-C 中稍微放宽。任何对象的布局都由根类中的实例变量（ivars）定义，然后由层级结构中后续的每个类中的实例变量定义。子类只能添加新的实例变量，而不能删除或重排父类中的实例变量。这意味着从内存布局的角度来看，将一个类实例的指针转换为另一个类实例的指针总是安全的。从面向对象类型系统的角度来看它也是安全的；任何子类始终能响应父类所响应的所有消息。

Objective-C 中的对象指针通过类名识别，类名后跟一个星号，就像 C 语言中的结构体指针一样，但不需要 `struct` 关键字。你始终可以将一个类实例的指针隐式地转换为其父类实例的指针。这对于间接父类同样有效。例如，`NSMutableArray` 是 `NSArray` 的子类，而 `NSArray` 是 `NSObject` 的子类。你可以将 `NSMutableArray` 转换为 `NSArray` 或 `NSObject`。然而，反转换需要显式转换。

Objective-C 还引入了一种新的指针类型：`id`。在转换规则方面，它大致相当于 `void*`。你可以隐式地将任何对象指针转换为 `id`，也可以将 `id` 转换为任何对象指针类型。

如果你习惯于无类型语言（如 Smalltalk、Ruby 或 Python），那么可能会想只使用 `id` 类型。这在大多数情况下是安全的，尽管有一个例外。Objective-C 使用消息名称进行查找，而不包含任何类型信息。这意味着你可以声明两个（在不同类中）名称相同但类型不同的方法。当编译器生成消息发送时，它使用接收者的类型来确定栈帧的布局。当在任何地方都只有一个该名称的方法时，就不需要类型信息。如果你想从对象外部访问实例变量，也需要静态类型，但这样做通常被认为是不良风格。虽然不需要指定静态类型信息，但通常是一个好主意。除了刚才提到的那种情况，它不会影响代码生成，但它会被编译器的语义分析阶段使用。这可以帮助在编译时捕捉一些错误。例如，如果你尝试将一个对象添加到 `NSArray` 实例中，编译器会警告你该对象不响应相关消息。这让你检查自己是否真的想用 `NSMutableArray`，或者是否需要为数组创建一个可变副本。

**注意：**

在 C++ 中，通常使用 `const` 关键字来描述对象为不可变。在 Objective-C 中，`const` 实际上是没用的。它指定对象的实例变量可能被直接修改，但这种操作很少执行。它不会改变可以给对象的消息，因此声明为 `const` 的对象仍然是可变的。

在大多数需要区分可变和不可变实例的情况下，Objective-C 程序员使用可变子类模式，即不可变类有一个可变子类。你可以隐式地将可变版本转换为不可变版本，但不能使不可变实例变为可用。

`Class` 类型与 `id` 类似，但它可以指向类。在 Objective-C 中，类是一个对象，所以你始终可以使用 `id` 代替 `Class`。



另外两个类型定义在标准的 Objective-C 头文件中。如果你使用 Clang 编译，这些类型中的大部分类型`SEL`用于选择器（selectors），我们将在本章稍后讨论。最后一个是`IMP`，代表“实例方法指针（Instance Method Pointer）”。这种类型指的是指向 Objective-C 方法的指针。大多数情况下，你根本不需要使用这种类型。它只用于 Objective-C 的某些非常动态的功能以及优化。我们将在第 19 章查看可能使用它的地方。

### 发送消息

```objc
9 [anObject autorelease];
10 [anObject addObject: anotherObject];
11 [anObject setObject: anotherObject
12 forKey: aThirdObject];
```

*来源：exampleMessages.m*

Objective-C 对 C 语言最重要的改进是增加了消息发送。正如我在上一章提到的，消息是一种高级控制结构。

这是 Objective-C 中往往让来自 C++ 和 Java 等语言的人感到畏的部分，因为其语法直接取自 Smalltalk，对于更熟悉 C 语法的人来说看起来非常陌生。这是刻意为之。在 C 语言中没有任何东西与 Objective-C 消息发送的行为相同，也没有内置定义，因此头文件是可选的。

### 发送消息

因此，新语法的出现强调了你同时也拥有了新的语义。记得 Tom Love 描述它为一种混合语言，在纯 C 部分与“对象领域（object land）”之间有清晰的语法分离，后者具有类 Smalltalk 的语法，并伴随着类 Smalltalk 的语义。

最简单的消息发送不需要任何参数。这方面的例子可能是发送给数组的`-count`消息。注意消息名称前的减号。这是 Objective-C 文档中使用的约定，用于表示发送给实例的消息。加号则用于表示发送给类的消息，例如`+new`或`+arrayWithObject:`。

```objectivec
size = [anArray count];
```

这段代码获取数组中的元素数量并将其存储在变量`size`中。在 C++ 或 Java 等语言中，等效的操作类似于如下所示：

```cpp
size = anArray.size();
```

如果`anArray`是一个 C 结构体且`size`字段是一个函数指针，那么 Objective-C 中将使用相同的语法。由于这与向对象发送消息的意义完全不同，设计者认为使用相同的语法会引起混淆。

带有一个参数的消息看起来非常相似。如果你想向 Objective-C 数组中添加一个对象，你会使用类似下面的代码：

```objectivec
[anArray addObject: anObject];
```

当消息有多个参数时，情况开始变得有些不同。与 Smalltalk 一样，每个参数都有独立的名称，因此你会在特定索引处插入对象，如下：

```objectivec
[anArray insertObject: anObject atIndex: anIndex];
```

当你理解了基础语法后，这使得 Objective-C 代码非常易读，因为每条消息都会告诉你每个参数的用途。如果你在文档中遇到这条消息，它的写法将是：`-insertObject:atIndex:`。你可以从两个冒号看出它接收两个参数，并从两个冒号之前的文本看出这些参数应该是什么。和之前一样，减号表示这是发送给实例的消息。

如果你向一个没有实现该方法的对象发送消息，则会使用若干回退方法。在默认实现中，这些方法中的最后一个将抛出异常（你可以在运行时捕获并规避它）。在发送消息之前，你也可以询问对象它是否知道如何处理。我们将在第 19 章中查看如何实现。

在 Objective-C 中，像 Smalltalk 一样，类也是对象。你可以向它们发送消息，就像向对象发送消息一样。当你这样做时，使用类的名称作为接收者。

**注意：**

如果你向`nil`（一个定义为`(id)0`的常量）发送消息，不会得到错误。相反，你会得到一个返回值 0。这非常有用，因为你可以对之前消息发送的结果发送一串消息，如果其中一个在中间返回了`nil`，其余部分仍然可以工作。这消除了 Objective-C 代码中对`NULL`进行大量测试。

向`nil`发送返回结构体的消息的行为是未定义的。如果你在 SPARC 上使用 GCC 编译的代码中执行此操作，你的程序将因非法指令信号（illegal instruction signal）而崩溃。在 OS X 上，结构体将填充随机值，就像栈上未初始化的结构体一样。在发送返回结构体的消息之前，你应该始终小心检查对象是否为`nil`。

向类发送消息最常见的原因是创建该类的实例。在 Objective-C 中，类负责创建它们自己的实例。C++ 或 Java 中没有等效的`new`关键字。最接近等等物是`+new`消息，你可以将其发送给类。例如，你可能这样创建一个新的可变数组：

```objectivec
id anArray = [NSMutableArray new];
```

尽管这看起来非常相似，但语言对此消息将做什么不提供任何保证。某些类可能会创建子类的实例，而某些类可能会返回一个单例实例。仅仅根据约定，它才会给你返回一个接收者的新实例。

### 选择器（Selectors）

消息的名称被称为选择器（selector）。它是消息名称的抽象表示，具有`SEL`类型，这是一个不透明类型（opaque type）。你可以使用`@selector()`指令创建选择器。

在 C 语言中，你通过名称引用函数。函数名也可以用作指向该函数的指针。Objective-C 的流程控制更加动态。你可以获取方法的指针，但大多数情况下，你希望向对象发送特定的消息，而不是调用一个特定的方法。如果你调用一个方法，你必须完全确定接收者是你预期的那个类。一个常见的例子是标准库中的`qsort()`函数。它对数组进行排序，使用函数来定义项目之间的顺序。在 Objective-C 版本中，你可能通过向对象发送`-compare:`来比较对象，而不是使用函数指针。

你可以使用选择器通过名称调用方法，正如我们将在第 19 章中看到的。Foundation 框架中的许多方法接受选择器作为参数。它们的使用方式与接受函数指针作为参数的 C 函数非常相似，用于延迟执行、回调、集合排序等。

```objectivec
SEL new = @selector(new);
SEL set = @selector(setObject:forKey:);
```

### 类（Classes）

当你创建一个新类时，你需要做两件事：描述它的公共接口并编写它的私有实现。你需要三个 Objective-C 关键字：`@interface`、`@implementation`和`@end`。注意所有 Objective-C 关键字都以`@`符号开头。这是因为该符号在 C 标识符中是不允许的。相比之下，C++ 引入了`class`等标识符，这会破坏任何使用`class`作为变量名的 C 代码。

Objective-C 继承了 C 的编译模型，编译器期望单一文件，并通过预处理器合并文件来实现分离。根据约定，Objective-C 类的接口放在扩展名为`.h`的头文件中，实现放在`.m`文件中。没有人记得为什么选择`.m`。Objective-C 的设计者建议它可能代表“模块（module）”、“方法（methods）”或“消息（messages）”。由于头文件是在 Objective-C 编译器看到之前由预处理器插入编译单元的，这种分离并不是强制性的。C++ 和 C 中的不透明数据类型也是如此。

一个意外意外方面是实例变量（Java 和 C++ 称为“字段”）是定义在接口而不是实现中的。这是早期 Objective-C 实现方式的遗留。每个对象都被转换为 C 结构体，第一个字段是指向类的指针。为了生成这个结构体，编译器需要看到所有父类的所有实例变量。这种方法一个不幸的副作用是修改类的布局意味着你必须重新编译所有的子类。

现在，有了非脆弱性 ABI，你可以从子类中隐藏私有实例变量。对它们的每次引用都通过一个间接层进行。偏移量现在是一个变量，而不是编译时常量。默认情况下，Objective-C 实例变量是保护的（protected），这意味着它们只能由类或其子类访问。如果你在它们前面加上前缀……

```objectivec
@interface Integer : NSObject
{
    int integer;
}
@end
```

```objectivec
@implementation Integer

- (int)intValue {
    return integer;
}

- (void)setIntegerValue:(int)value {
    integer = value;
}

@end
```

30

第 2 章：Objective-C 入门

使用`@private`时，它们仅对类可见，而使用`@public`时，它们可以在任何地方被访问。这并不常见。对于访问权限，几乎没有进行运行时检查，并且有一些机制可以绕过访问控制，因此通常将所有内容设为保护状态，仅在私有类中将实例变量设置为公共。

**注意：**

Apple 非脆弱性 ABI 限制了偏移量变量的可见性，如果你尝试从不同的编译单元访问私有实例变量，将产生硬错误。仍然可以通过运行时内省（introspection）访问私有实例变量，这种保护在其他运行时环境中是不提供的。

类接口的基本结构包含三个部分。第一部分是定义新类在层次结构中的位置：

```objectivec
@interface ClassName : Superclass <protocols>
```

类名紧随`@interface`关键字之后。接下来是一个冒号，然后是父类的名称。可以设计新的根类，但要正确地做到非常复杂，因此大多数时候你将使用`NSObject`或`NSProxy`作为你的父类。

之后，你可以可选地在角括号中指定一个由逗号分隔的协议列表。Objective-C 中的协议类似于 Java 中的接口（interfaces）。它们定义了对象必须实现的方法列表。

### 声明类

31

接下来是实例变量列表。它的语法与 C 语言中定义结构体相同。一个只包含实例变量而没有方法的简单类定义如下：

```objectivec
@interface NoMethods : NSObject

{
    int integer;
    NSObject *object;
    float floatingPoint;
}

@end
```

在 C 结构体定义中有效的任何内容在这里都是有效的。如果你使用 Objective-C++，你还可以添加指向 C++ 对象的指针，以及具有简单构造函数的 C++ 实例。

最后，你列出类所实现的公共方法。与其为此凭造一些方法，让我们来看一些真实的方法声明：

```objectivec
+ (id)new;
- (void)appendString:(NSString *)aString;
```

第一个方法声明前的加号表示这是一个附加到类上的方法。你可以向类发送`+new`消息，它将给你返回一个对象指针。`id`类型是 Objective-C 引入的一种新类型，大致类似于 C 语言中的`void *`类型，但仅限于指向 Objective-C 对象。

32

第 2 章：Objective-C 入门

注意，返回类型和参数类型使用了与类型转换相同的语法。这突显了消息发送与 C 函数调用之间的另一个重要区别。该方法被编译为 C 函数，在调用它之前，指针会被强制转换为这些类型。

类定义的实现部分要简单得多。它以`@implementation`指令开始，包含了类所有方法的定义，如下所示：

```objectivec
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

需要注意的一个重要点是，你不需要声明类实现的所有方法。未在类接口中声明的方法被认为是私有的。调用它们将产生编译时警告，类的未来版本可能会完全停止对这些方法的响应。

### 使用协议

33

与类一样，Objective-C 中的协议也是对象。协议的行为是 Apple 在现代运行时更改的内容之一。在此之前，协议通过名称识别，如果两个协议具有相同的名称，则它们被认为是等价的。这意味着如果你在不同的库中声明了两个同名的协议，你就无法判断对象实现的是哪一个。更重要的是，你无法查找协议并查看它需要哪些方法。

在 Objective-C 2 中，协议现在是唯一的。你现在可以通过名称获取协议并对其进行检查。（注：原文此后存在大量重复段落，翻译已按要求去重处理）

### 为类添加方法

```objectivec
@protocol Collection

- (BOOL)isEmpty;

@end

@interface NSArray (Collection) <Collection>
@end

@interface NSSet (Collection) <Collection>
@end

@implementation NSArray (Collection)

- (BOOL)isEmpty
{
    return [self count] == 0;
}

@end

@implementation NSSet (Collection)

- (BOOL)isEmpty
{
    return [self count] == 0;
}

@end
```

*自：collection.m*

这被称为类扩展（class extension）。与其他分类（categories）不同，分类应该伴随一个指定了分类名称的独立`@implementation`指令，而类扩展中声明的方法预计会出现在类的主`@implementation`指令中。你可以用它来对私有方法进行前向声明。

在最新的 Objective-C 编译器中，你还可以在类扩展内部声明实例变量。为了让其生效，你需要在编译时指定`-fobjc-nonfragile-abi2`标记。

# 第 2 章：Objective-C 入门

### 使用非正式协议

```objectivec
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

通常情况下，你想定义一组希望类实现的方法，但这些方法是可选的。这在代理（delegates）中尤为常见，因为在发送消息之前，你需要测试代理是否实现了某个特定方法。

在 Objective-C 2 中，协议可以包含声明为可选的方法，但在那之前，使用分类来实现非正式协议是常见做法。如果你为 NSObject 的某个分类创建了接口，但没有为其提供接口定义，那么编译器将假设每个 NSObject 子类都响应接口中声明的消息，因此当你向对象发送其中任何一个消息时，它不会产生警告。

当然，并不是每个对象真的都会实现这些方法，所以你需要在发送消息之前，确保你使用`-respondsToSelector:`来测试对象是否真的实现了该方法。

### 通过声明属性合成方法

```objectivec
@interface Integer : NSObject

@property (nonatomic, assign) int integer;

@end

@implementation Integer

@synthesize integer;

@end
```

*自：synth.m*

Objective-C 2 的重大新增之一是声明属性（declared properties）。它们允许你定义访问器语义的某些方面，然后如果你不需要任何特殊处理，就可以合成相关方法。

属性还引入了一些新语法。它们是基于消息发送来实现的。本章开头的示例将同时创建`-integer`和`-setInteger:`方法。你可以像调用任何其他方法一样调用它们，但也可以使用点表示法，如下：

```objectivec
obj.integer = 12;

int i = obj.integer;

obj.integer += 42;
```

最后一种情况是最实用的。将其扩展为传统的 Objective-C 消息语法看起来如下：

```objectivec
[obj setInteger:[obj integer] + 42];
```

第 2 章：Objective-C 入门

值得注意的是，这两种方式生成的代码完全相同。第一种看起来效率更高，但实际上并非如此。在两种情况下，你都有两次消息发送和一次加法。如果`obj`是一个 C 结构体，这开销要大得多。

**注意：**

“属性”（property）一词在 Smalltalk 文档中用于指代任何可以通过访问器操作的实例变量。在稍旧的 Objective-C 文档中，也以相同的方式使用。指定声明属性（declared properties）而非仅仅是属性，有助于减少这种歧义。属性声明包含两个部分：接口和实现。接口定义了属性的名称和类型（正如你预期的那样），它还定义了一些高级语义。

属性默认是原子的（atomic）。这会产生一些开销，所以你可能想在你创建的大多数属性中指定非原子的（nonatomic）。访问方法的原子性并不能使对象线程安全，在线程之间共享对象时，几乎总是使用某些高级别的锁会更好。考虑`nonatomic.m`示例。它声明了一个原子属性。然后你在代码中使用单次自增操作。你可能认为这是一个原子自增，但事实并非如此。这行语句被展开为两次消息发送。

### 通过声明属性合成方法

```objectivec
@interface NotReallyAtomic : NSObject

@property int a;

@end

@implementation NotReallyAtomic
{
    obj.a += 1;
}

@end
```

*自：nonatomic.m*



在属性的语境下，原子性意味着对于非对象类型，非原子没有意义。属性可以是可读写（`readwrite`）或只读（`readonly`），表示是否支持对其赋值。类扩展提供了实现此操作的机制。如果你在主接口中声明属性为可读写，但在类扩展中将其设为只读，那么主 `@implementation` 中的 `@synthesize` 指令将创建 setter 和 getter。然而，在类扩展不可见的任何尝试使用 setter 的行为会导致编译器错误。

**注意：**

有时，你希望有一个可读写属性，但仅在公共接口中将其设为只读。类扩展提供了实现此操作的机制。如果你在接口中声明属性为只读，但在类扩展中重新声明为可读写，编译器可能看不到它们并产生警告。你可以通过为该属性提供一条 `@dynamic` 行来抑制这种警告。这告诉编译器这些方法确实存在，将在运行时进行解析。

或者，你可以使用 `@synthesize` 来告诉编译器会为你生成访问器方法。合成属性方法（Synthesized property methods）指向与属性同名的实例变量。这些方法会调用运行时库函数，传入实例变量的偏移量以及一些指示属性类型的标志位。

在旧的 Objective-C ABI 中，所有实例变量都需要在 `@interface` 描述中声明，以便编译器能将它们转换为 C 结构体。在非脆弱（non-fragile）ABI 中，情况并非如此。`@synthesized` 指令可以创建不属于类公共接口的新实例变量。

## 理解 `self`、`_cmd`、`super`

```objectivec
id method(id self, SEL _cmd, ...);
```

*自：object.m*

每个 Objective-C 方法都会被编译成函数。该函数有两个隐藏参数：`self` 和 `_cmd`。其中第一个非常显而易见：它是消息的接收者。如果是实例消息，`self` 将是该类的一个实例；如果是类消息，它将是类本身。

在 C++ 中，`this` 关键字几乎等同于 Objective-C 中的 `self`，但有一个关键区别：`self` 不是一个关键字。它只是参数的名字。在 C++ 中为 `this` 赋值会导致错误，而在 Objective-C 中为 `self` 赋值是被允许的。

第二个隐藏参数是消息的选择器（selector）。这对于消息转发等操作正常工作至关重要。当你向一个对象不知道如何处理的对象发送消息时，它会构造一个封装了消息的 `NSInvocation` 对象，然后将其传递给 `-forwardInvocation:`。

由于这两个隐藏参数都不是关键字，你可以在方法之外将它们都作标识符使用，尽管 C 规范保留了以下划线开头的标识符用于实现，因此最好不要使用 `_cmd`。普通的作用域规则依然适用，所以你也可以在方法内部声明一个名为 `self` 的变量，并隐藏掉作为参数传递进去的版本。如果你这样做，编译器会生成警告，因为这是件很愚蠢的事，但在语义上是有效的。

`super` 伪变量要复杂一些。它只在作为消息的接收者使用时才有效。它会生成一条消息发送，其中 `self` 是接收者，但方法会在父类而非当前类中查找。这就是你调用已重写方法的方法。

向 `super` 发送消息使用不同的方法查找函数，该函数接受指向 `objc_super` 结构体的指针作为参数。该结构体包含了目标类和目标对象。

父类在编译时就已经固定了。当你编译一个 Objective-C 类时，所有向 `super` 的消息都将在类接口中定义为父类的类上查找。对于大多数代码来说，这并不重要，但如果你正在使用运行时库函数为类添加方法，这是你需要记住的。如果你附加到新类上的方法向 `super` 发送消息，它将把消息发送到错误的类。

值得注意的是，在带有 GNU 运行时，分类（categories）中向父类发送消息的实现是不同的。类实现上下文与类结构位于同一个编译单元中，因为类结构是由编译器根据 `@implementation` 上下文中的代码生成的。只需通过查找并获取父类字段即可找到父类指针。

在分类中，类结构是不可用的。它必须在运行时查找。这导致从分类定义的方法中发送父类消息时速度较慢。Apple 运行时通过让链接器解析外部类引用来绕过这个问题。

动态查找的原因是为了支持类替换（class posing），这是一种一个类在运行时替换另一个类的定义的技术。在现代 Apple 运行时中，已不再支持类替换。每个类都将其它的结构导出为公共符号，因此链接器将在加载时解析类指针。

## 理解 `isa` 指针

```c
typedef struct objc_object *id;

struct objc_object
{
    id isa;
};
```

*自：object.m*

在 C++ 中，类就是结构体。你可以将一个 C 结构体子类化为一个 C++ 类。当你对一个 C++ 类调用方法时，你实际上是在调用一个带有修饰过名的 C 函数，并将结构体指针作为第一个（隐藏）参数。

在 Objective-C 中，结构体和类是完全不同的。在引入非脆弱 ABI 之前，你可以在结构体定义中使用 `@defs` 关键字来创建一个与类布局相同的结构体，但你不能在类和结构体之间互换使用。

对象与结构体的区别在于，你可以向类发送消息。这之所以有效，是因为结构体中的第一个实例变量指向类结构指针。按照惯例，这个实例变量被称为 `isa`，正如“这个对象是……”。如果你定义一个新的根类，必须记住这个实例变量。

与 `self` 和 `_cmd` 隐藏参数一样，`isa` 指针只是另一个实例变量；它不是关键字。对比 C++ 中的虚方法。C++ 对象包含一个虚函数表（vtable）。调用方法时，编译器会引用 vtable 并调用对应偏移处的函数。这是一个简单的指针数组。

在类布局是私有的运行时，你仍然可以找到实例变量的偏移量、方法的名称和签名、父类等。你可以查看其他对象的 `isa` 指针。`id` 类型被定义为包含类指针的 C 结构体，你可以像读取任何字段一样读取它。强烈建议这样做。

Objective-C 对象可能会转发消息，你拥有的对象指针可能是代理。如果你想获取另一个对象的类，应该发送 `-class` 消息。这样做更快，但在存在代理的情况下不会崩溃。你可以通过发送 `-isProxy` 消息来测试对象是否为代理，但如果你已经要发送消息，不如直接获取类。

## 类的初始化

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
    NSLog(@"-init called");
    return self;
}

@end

int main(void)
{
    [NSAutoreleasePool new];
    NSLog(@"main() entered");
    id init = [[Init alloc] init];
    init = [[Init alloc] init];
    return 0;
}
```

*自：classInit.m*

在 C++ 中，你可以通过将函数的结果赋值给全局或静态变量来执行静态初始化。在 C 中，你可以使用扩展（如 GCC 的 `__attribute__((constructor))`）来实现相同的结果。这些都会导致在 `main()` 函数之前调用特定的函数。正确使用这些特性非常困难。顺序在它们被称为是未定义的。

Objective-C 有一个等效的方法。类的 `+load` 方法在类与运行时注册时被调用，在 `main()` 函数执行之前。

从此方法中发送任意消息是不安全的。该类本身、其所有的父类以及常量字符串类都保证已经加载。其他类可能已经加载，但这不是保证的，而且即使在你的环境下可以运行，如果加载顺序发生细微变化，它也可能无法工作。

更安全的替代方案是 `+initialize` 方法。它在向类发送第一条消息时，由运行时自动调用。通常，第一条消息是类似于 `+alloc` 的内容，用于创建类的实例，但它也可能是请求类名或单例实例的消息。

`+initialize` 方法允许你对类所需的项进行延迟初始化。它不会在 `main()` 函数之前被调用，因此所有内容都已加载，进程处于一个定义良好的状态。

如果你实现了这两个方法，你就可以看到执行顺序。首先，在类一加载时，就会调用 `+load` 方法。当运行时加载器完成后，它会调用 `main()` 函数。当你向类发送消息时，会调用 `+initialize` 方法，然后是你实际调用的方法，接着你可以向返回的实例发送 `-init` 消息。

| 行数 | 输出 |
| :--- | :--- |
| 1 | `a.out[2690:903] +load called` |
| 2 | `a.out[2690:903] main() entered` |
| 3 | `a.out[2690:903] +initialize called` |
| 4 | `a.out[2690:903] -init called` |
| 5 | `a.out[2690:903] -init called` |

*输出来自：classInit.m*

注意 `+initialize` 方法只会被调用一次。当你第二次向类发送消息时，消息将直接被传递。`+initialize` 方法的调用也是线程安全的。如果你从不同的线程同时向同一个类发送两条消息，其中一个将阻塞，直到另一个运行完 `+initialize` 方法，然后两者都会继续。

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

*来自：type.m*

Objective-C 很大程度上依赖于运行时内省。Objective-C 对象可以通过发送消息进行内省，但 C 类型则不然。为了帮助这一点，Objective-C 定义了一种将 C 类型编码为字符串的方法。每种基本类型都被编码为一个单个字符。例如，`int` 编码为 "i"，而 `unsigned long long` 编码为 "Q"。大写字母表示无符号版本、小写字母表示有符号版本的约定适用于所有整数。

这些类型编码可以包含任意复杂的 C 类型，如从 `type.m` 示例的输出所示。

```text
Encoding: {_s=if@*[5S]}
```

*输出来自：type.m*

此示例给出了包含基本 C 类型、一个 Objective-C 对象和一个 C 数组的结构体的类型编码。类型编码是由编译器响应 `@encode()` 指令生成的，该指令用法与 `sizeof()` 类似，接收一个类型作为参数并返回一个类型编码。

结构本身由一对大括号表示。内部是结构的名称，后面是一个等号，然后是每个元素的类型编码。

接下来的四个字符显示前四个字段的类型编码。这里有两点注意：第一，Objective-C 对象都被编码为 "@"，无论其静态类型信息如何。第二，`char*` 被编码为 `*`。所有其他指针都被编码为 `^` 后跟指向的类型，但 C 字符串受到了特殊处理。

该编码的剩余部分是数组。它位于方括号中，后面是元素数量，然后是单个元素的类型。

你在 C 类型层面进行任何内省时，Objective-C 类型编码都会随处可见。

**注意：** Apple 和 GNU 的 Objective-C 实现之间的主要区别之一是它们使用选择器（selectors）来查找方法。在 Foundation 框架的最新版本中，你会发现许多接受 block 作为参数的方法。例如，你可以使用 block 作为参数遍历数组。

选择器是方法的名称。在示例中，`getCounter()` 函数返回一个实现 `a` 的新 block。

## 使用闭包（Closures）

`__block` 块上引用的栈上任何变量都会被复制到堆上并进行引用计数。当你调用 `_Block_copy()` 时，如果 block 在栈上，它本身会被复制到堆上；如果它不在栈上，则会增加其引用计数。`getCounter()` 函数返回的每个 block 都有计数器的副本，因为它是一个自动（栈）变量，因此对该函数的后续调用都会创建一个新版本。

```c
__block int counter = 0;
int (*getCounter())(void) = ^{
    counter++;
};

int main(void)
{
    int (*block)(void) = getCounter();
    block();
    assert(block() == 2, "Block didn't start");
    return 0;
}
```

*来自：block.m*

block 并没有给 C 语言增加任何表现力。一个 block 只是隐藏在单个结构中的函数指针和数据指针，编译器中包含一些额外的逻辑，在调用函数时将数据指针作为隐藏参数插入到函数中。

这并不意味着 block 是没用的。毕竟，Objective-C 的情况也是如此；它并没有让你做任何在 C 中做不到的事情，它只是添加了一些语法糖，让某些事情变得更容易。

像 Objective-C 对象一样，block 也有一个 `isa` 指针并且可以发送消息。它们是 `NSBlock` 私有抽象类的实例，该类实现了 `NSCopying` 协议。block 的多数对象行为是未文档的。你可以将它们存储在 Objective-C 集合中，但不要依赖它们理解特定消息的能力。在最新版本的 Clang 中，block 也支持内省，将其类型暴露为 Objective-C 类型编码。

我们将在第 15 章详细讨论 block。

## 内存管理

如果你有 C 或 C++ 背景，你可能习惯了跟踪对象的所有权并手动分配和销毁它们。如果你来自 Java 等语言，你可能已经习惯了让垃圾回收器为你处理这一切。

Objective-C 在语言层面上并没有提供任何用于分配或释放对象的机制。这被留给 C 代码来处理。你通常通过向其类发送 `+alloc` 消息来分配对象。这会调用类似 `malloc()` 的函数来为对象分配空间。向实例发送 `-dealloc` 消息将会清理它的实例变量并删除它。Foundation 框架在这种简单的人工内存管理基础上增加了引用计数。一旦你理解了它的工作原理，会让生活变得容易得多。

### 保留（Retaining）与释放（Releasing）

```objectivec
NSArray *anArray = [NSArray array];
anArray = [[NSArray alloc] init];
[anArray release];
```

*来自：retainRelease.m*

每个继承自 `NSObject` 的对象都有一个相关的引用计数。当引用计数达到 0 时，它会被销毁。通过 `+alloc` 或任何相关方法（如 `+new` 或 `+allocWithZone:`）创建的对象，其引用计数从 1 开始。

为了控制对象的引用计数，你向它发送 `-retain` 和 `-release` 消息。正如它们的名称所示，当你想要保留对对象的引用或当你想要释放现有的引用时，应该使用这些消息。`-retain` 消息增加对象的引用计数，而 `-release` 消息则减少它。

你也可以向对象发送 `-retainCount` 消息来确定其当前的引用计数。人们很想用它来进行优化，并在你确定一个对象只有一个引用时调用某些特殊情况。这是一个非常糟糕的主意。正如其名称所示，该方法告诉你对该对象被保留的引用的数量，而不是引用的总数。在栈上创建指向对象的指针时，不费力向它们发送 `-retain` 消息是常见的。这意味着一个对象可能在两个或更多地方被引用，尽管它的引用计数仅为 1。

### 赋值给实例变量

```objectivec
- (void)setStringValue:(NSString*)aString
{
    id tmp = [aString retain];
    [string release];
    string = tmp;
}
```

*来自：ivar.m*

在使用这种方式使用引用计数时，有几点需要注意。考虑以下简单的 setter 方法：



```objectivec
- (void)setStringValue:(NSString*)aString
{
    [string release];
    string = [aString retain];
}
```

来自：`ivar.m`

这看起来很合理。你释放了对旧值的引用，然后保留新值并将其赋值。在大多数情况下，这是有效的，但在少数情况下它不起，这可能导致调试变得困难。

如果 `aString` 和 `string` 的值相同会怎样？在这种情况下，你向同一个对象发送了一个 `-release` 消息，然后是一个 `-retain` 消息。如果其他某些代码持有该对象的引用，它仍然可以工作；但如果没有，第一条消息将导致对象被销毁，而第二条消息将发送给悬悬指针。

该方法的更佳实现是先保留新对象，正如本节开头所示。注意，你应该赋值 `-retain` 消息的结果，因为某些对象在被你保留时会返回另一个对象。这种情况非常罕见，但偶尔会发生。

最后，该方法不是线程安全的。如果你想要一个线程安全的 setter 方法，你需要保留新值，在结果和实例变量上执行原子交换操作，然后释放旧值。然而，通常情况下，几乎无法推理支持这种细粒度并发的代码，而且缓存抖动量将抵消任何性能收益，所以这是一个非常糟糕的主意。如果你真的需要它，使用属性（properties）比尝试手写它更好。

## 避免引用循环（Retain Cycles）

```objectivec
- (void)setDelegate:(id)aDelegate
{
    delegate = aDelegate;
}
```

来自：`ivar.m`

引用计数的问题在于它无法检测循环。如果你有两个相互保留的对象，它们都永远不会被释放。通常情况下，这不是一个主要问题，但在某些情况下循环是不可避免的。Objective-C 结构倾向于无环的，但最常见的是代理模式（delegation pattern）。在这种模式下，一个对象需要另一个对象的引用，但另一个不需要它的引用。如果你将对象作为参数传递，它会被过早地自动释放（autoreleased）。

## 自动释放池（Autorelease Pools）

```objectivec
int main(void)
{
    AutoreleasePool *pool = [NSAutoreleasePool new];
    id object = [Object autorelease];
    [pool drain];
    return 0;
}
```

来自：`autorelease.m`

除了循环外，引用计数最大的问题是存在某些时期，没有任何对象真正拥有引用。在 C 中，决定是由调用者还是被调用者负责释放它是一个问题。在 Objective-C 中，这个问题更为常见。许多方法可能会返回临时对象。如果你返回的是一个临时对象，它需要被释放；但如果你返回的是指向实例变量的指针，则不需要。你可以保留这样的指针，但那时你需要记得释放每个返回的对象。

解决这个问题的方案是自动释放池。当你向一个对象发送 `autorelease` 消息时，它会被添加到当前的 `AutoreleasePool` 实例中。当该实例销毁时，添加到其中的每个对象都会收到 `-release` 消息。`-autorelease` 消息是一种延迟释放。当你不再需要一个对象但其他地方可能需要时，向它发送。

如果你在使用 `NSRunLoop`，每次循环迭代开始都会创建一个自动释放池，并在结束时销毁。这意味着临时对象在当前迭代结束之前不会被销毁。如果你正在进行创建大量临时对象的操作，你可能想要创建一个新的自动释放池，如下：

```objectivec
id pool = [NSAutleasePool new];
[anObject doSomethingThatCreatesLotsOfObjects];
[pool drain];
```

注意，在销毁自动释放池时，向它发送 `-drain` 消息而不是 `-release` 消息。这是因为在垃圾收集模式下，Objective-C 运行时会忽略 `-release` 消息。在这种模式下，`-drain` 消息提供了提示，但不会销毁池。

## 使用自动释放的构造函数

```objectivec
+ (id)object
{
    return [[[self alloc] init] autorelease];
}
```

来自：`namedConstructor.m`

我在上一节中提到通过 `+alloc` 创建的对象引用计数为 1。事实上，所有对象创建时引用计数均为 1，但通过命名构造函数（如 `+stringWithFormat:` 或 `+array`）创建的对象也会自动释放。

如果你通过这些机制之一创建了对象，如果你想保留它，就必须向它发送 `-retain` 消息。如果你不，它将在稍后当自动释放池时被回收。

## 访问器中的自动释放对象

被销毁。

这是一个在你自己的类中需要遵守的重要约定。如果有人使用命名构造函数创建了你某个类的实例，他会期望自己不需要去手动释放它。一个典型的命名构造函数看起来就像本节开头的那个。

请注意，由于这是一个类方法，`self` 对象将是类本身。通过向 `self` 发送 `+alloc` 消息而不是向类名，该方法可以自动处理子类。

```objc
- (NSString*)stringValue
{
    return [[string retain] autorelease];
}
```

来自：`ivar.m`

在 Foundation 中实现的引用计数中，另一个常见问题是，你通常不会对那些仅在栈上引用的对象进行 retain（保留）。假设你有像下面这样的代码：

```objc
NSString *oldString = [anObject stringValue];
[anObject setStringValue:newString];
```

如果 `-setStringValue:` 方法正如我之前建议的那样实现，这段代码将会崩溃，因为当你设置新的字符串值时，`oldString` 引用的对象会被删除。这是一个问题。有两种解决方案，都涉及到自动释放池（autorelease pools）。一种是在设置新值时对旧值进行 autorelease（自动释放）。另一种是本节开头 `-stringValue` 方法的定义。

这确保了字符串不会因为该对象的任何操作而被意外销毁。另一个常见的惯用法是用 `-copy` 消息来代替 `-retain`。如果实例变量可能是可变的，那么这很有用。如果它是不可变的，`-copy` 将等同于 `-retain`。如果它是可变的，调用者将获得一个不会因为向该对象发送其他消息而发生改变的对象。

## 支持自动垃圾回收

```bash
$ gcc -c -framework Cocoa -fobjc-gc-only collected.m
$ gcc -c -framework Cocoa -fobjc-gc collected.m
```

从 OS X 10.5 开始，Apple 在 Objective-C 中引入了自动垃圾回收。这可以让程序员的生活变得更轻松，但在大多数情况下，它会带来性能开销。Apple 的回收器使用大量内存来跟踪活跃引用，因此在 iPhone 上是不可用的。它也不支持旧版本的 OS X，并且对 GNUstep 的支持有限，因此如果你想写出可移植的代码，应该避免使用垃圾回收。

如果你在垃圾回收模式下编译代码，所有的 `-retain`、`-release` 和 `-autorelease` 消息都将被忽略。编译器将为对堆内存的每一次赋值操作自动插入对运行时（runtime）函数的调用。

代码必须带有垃圾回收支持进行编译才能使用垃圾回收器。这会在对堆内存进行任何赋值时插入一组函数调用，在 Mac 运行时，这些函数声明在 `objc-auto.h` 中。这些函数确保垃圾回收器感知到写入操作。这些操作是必要的，因为回收器是并发的。它将在后台线程中运行，并在无法再次找到对对象的引用时删除它们。必须通知回收器更新的指针，否则它可能会意外删除你刚刚创建了引用的对象。

在为垃圾回收进行编译时，你有两个选项。如果你使用 `-fobjc-gc-only` 标志编译，你的代码将仅支持垃圾回收。如果你使用 `-fobjc-gc` 标志编译，代码将同时支持引用计数和自动垃圾回收。这在你编译框架（framework）时非常有用。你仍然必须在正确的位置添加 `-retain` 和 `-release` 调用，但你的框架的用户可以在开启或不开启回收的情况下使用它。

## 与 C 语言互操作

在垃圾回收模式下，并不是所有内存都会被扫描。通过 `malloc()` 分配的任何内容对垃圾回收器都是不可见的。如果你将对象指针作为 `void*` 参数传递给 C 函数，然后该函数将其存储在 `malloc()` 分配的内存中，那么它对回收器来说就是不可见的，即使仍有它的引用，它也可能被释放。

通常，你会在执行此操作之前向对象发送 `-retain` 消息，但这在垃圾回收模式下将不起作用。相反，你必须使用 `CFRetain()` 函数。这会增加对象的引用计数，无论回收器是否运行。回收器只有在对象的 retain 计数为零且在追踪的内存中找不到任何对它们的引用时，才会释放对象。

当你完成对一个回收器范围之外的引用使用后，你需要调用 `CFRelease()`。遗憾的是，这并不是你需要使用这些函数的唯一情况。在某些情况下，当你将对象作为回调函数的参数时，也需要使用它们。

## 使用弱引用

```objc
@interface WeakDelegate : NSObject
{
    __weak id delegate;
}
@property __weak id delegate;
@end

@implementation WeakDelegate
@synthesize delegate;
@end
```

来自：`gc.m`

Apple 垃圾回收实现中最棒的特性之一是置零弱引用（zeroing weak references）。在垃圾回收出现之前的 Objective-C 文档中，未保留的指针通常被称为“弱引用”。如果你在垃圾回收模式下声明一个对象指针 `__weak`，你就得到了一个置零弱引用。垃圾回收器在判断一个对象是否活跃时不会计算它。如果对对象的所有引用都是弱引用，它就可以被销毁。此后，读取弱引用将返回 `nil`。

在引用计数环境中（例如引用 `delegate` 的情况），弱引用通常用于消除引用循环（retain cycles）。在追踪环境中不需要这些，因此你可以对 `delegate` 以及任何其他可能出现引用循环的地方使用强引用。弱引用最常与通知等内容结合用。你会保留对一个对象的弱引用，只要它在别处被引用，你就一直向它发送消息，然后让它可以自动清理。

## 分配扫描内存

Cocoa 现在提供了一些允许你存储弱引用的集合。旧版本的 Foundation 框架提供了 `NSMapTable` 和 `NHashTable` 作为不透明的 C 类型，并有一组用于使用它们的 C 函数。这些接口仍然可用，但从 10.5 版本开始，Apple 将这两个 C 类型变成了类。

`NSMapTable` 类型是 `NSDictionary` 的通用形式，可以将任何指针大小的类型作为值和键。在垃圾回收的情况下，你可以使用此类来存储与强或弱对象指针的双向映射。这对于像 `NotificationCenter` 之类的东西有用，这样对象在仍在注册接收通知时可以被回收，并在发生这种情况时可以自动从通知中心中移除。

```objc
id *buffer = NSAllocateCollectable(10 * sizeof(id), NSScannedOption);
```

来自：`gc.m`

如果你使用 `malloc()` 分配内存，它对垃圾回收器是不可见的。如果你想要一个类似包含对象的 C 数组，这就是问题。我们已经看过了解决此问题的方法。你可以对正要存储的对象调用 `CFRetain()`。

# 第 3 章：内存管理

对旧值调用 `CFRelease()`，然后将它们交换。

这种方法并不理想，尽管它可以工作。另一种选择是从垃圾回收器中分配一块内存区域。`NSAllocateCollectable()` 函数与 `malloc()` 类似，但有两个重要的区别。首先，它返回的内存是被垃圾回收的。目前没有对应的 `NSFreeCollectable()` 函数。当指向缓冲区的最后一个指针消失时，该缓冲区会被回收。

**注意：**

Apple 垃圾回收器不支持内部引用（interior references），因此你必须确保保留一个指向该区域起始部分的指针。指向缓冲区中间位置的指针无法阻止它被释放。

第二个区别是，该函数的第二个参数定义了你想要的内存类型。如果你将使用缓冲区来存储 C 类型，只需在此处传递 0 即可。如果你传递 `NSScannedOption`，返回的缓冲区将被扫描为可能包含对象指针的位置，以及由 `NSAllocateCollectable()` 返回的其他内存区域的指针。

# 第 4 章：常见的 Objective-C 模式

## 支持两阶段创建

```objc
NSMutableString *buffer = [[NSMutableString alloc] init];
NSMutableArray *array = [[NSMutableArray alloc] initWithObject: buffer];
```

来自：`allocInit.m`

你可能已经见过的模式之一是两阶段创建模式。在传统的、NeXT 出现之前的 Objective-C 中，你通过向类发送 `+new` 消息来创建一个对象。当你实现一个新类时，你会重写 `+new` 来调用父类的实现，然后执行该类的初始化。NeXT 改变了这一点，将对象的创建和对象的初始化分为两个不同的方法。`+new` 方法仍然有效，但它现在向类发送 `+alloc` 消息，并向返回的对象发送 `-init` 消息。

`+alloc` 方法本身默认会调用 `+allocWithZone:`。它接受一个 `NSZone` 作为参数。这是一个封装了分配区域的不透明类型。这在 NeXT 系统上被大量使用，为了高效利用这些机器配备的极小内存。它在 OS X 上运行效果并不理想，而且并不是所有类都恰好支持，因此在许多现代 Objective-C 代码中，它是一个遗留特性。

当你创建一个新类时，你会重写 `-init` 方法，或者提供一个新的指定初始化器。

**注意：**

你仍然可以在 GCC 中找到一些旧式创建方式的痕迹。当使用 `+new` 创建对象时，通常做法是创建新实例，然后将其赋值给类方法中的 `self`。GCC 中有一段代码来支持这一点，允许从类方法访问实例变量。该功能在很久以前就被弃用了，所以现在你尝试这样做时会得到一个警告。

重写 `+alloc` 非常罕见。偶尔，人们这样做是为了实现类级池或强制单例，但这非常不寻常。如果你正在实现一个单例类，你可以重写 `+alloc` 在存在现有实例时返回它。我们将在本章稍后部分讨论。

## 拷贝对象

```objc
@interface Pair : NSObject <NSCopying>
@property (nonatomic, retain) id first, second;
@end

@implementation Pair
@synthesize first, second;
- (id)copyWithZone: (NSZone*)aZone {
    Pair *new = [self->isa allocWithZone: aZone];
    new.first = first;
    new.second = second;
    return new;
}
@end
```

来自：`copy.m`

Foundation 框架包含一个名为 `NSCopyObject()` 的函数。逻辑上你可能会认为这会拷贝一个对象，你几乎是对的。它创建一个与原始对象相同类的新对象，然后使用类似 `memcpy()` 的方法将实例变量拷贝过去。

这对于仅有原始 C 类型作为实例变量的对象非常有效，但对其他对象效果不佳。对象指针在拷贝时需要被发送 `-retain` 消息。C 指针可能需要对其进行某些其他处理，特别是当它们是从某些其他库返回的不透明类型时。

在没有关于对象之间具体关系信息的情况下，拷贝函数无法自动创建真正的拷贝。某些对象甚至不应该支持拷贝。例如，你认为封装了套接字（socket）对象的拷贝语义是什么？你会得到两个封装了同一个套接字的对象吗？

真正知道如何拷贝对象的是对象本身。如果对象实现了 `NSCopying` 协议，你可以向它发送 `-copyWithZone:` 消息来获取拷贝。该方法接受一个 `NSZone` 作为参数。如今大多数代码不再理会 `NSZone` 了。`NSObject` 提供了一个 `-copy` 方法，它只是使用默认区域作为参数调用 `-copyWithZone:`。尽管你可能总是调用 `-copy`，但你应该实现 `-copyWithZone:`。

该方法通常通过向接收者的 `isa` 指针发送 `+allocWithZone:` 消息开始，这将创建一个新实例。然后可能会调用初始化方法，也可能会填充实例变量。

**注意：**

如果你继承自实现了 `NSCopying` 的父类，你应该在你的实现中调用 `[super copyZone:]`。

## 常见的 Objective-C 模式

每种编程语言都鼓励不同的设计模式。理解贯穿 Foundation 框架的常用模式，会让理解整个框架以及编写 Objective-C 代码变得容易得多。

本章提供了 Objective-C 中一些常见模式的概述。如果你想阅读更多，可以在 Erik M. Buck 和 Donald A. Yacktman 编写的 *Cocoa Design Patterns* 中找到更详细的概述（Addison-Wesley，2009）。

## 归档对象

通常，你需要程序的某些状态比单次调用更持久。你可以在属性列表中存储一些纯数据类型，正如我们在第 7 章看到的，但任意对象呢？你可以以自定义（或公开）格式写入数据，然后从这些数据重新创建对象。然而，仅仅为了让几个对象持久化就定义新的文件格式对大多数程序员来说精力投入太大。



幸运的是，Foundation 在`NSCoding`协议中提供了答案。它定义了两个方法：`-initWithCoder:`和`-encodeWithCoder:`。许多标准类实现了这个协议，你自己实现也相对容易。

作为参数传递给方法的对象编码器。这是一个封装了某些数据表示的类。在旧系统中，这通常是`NSArchiver`，但在新的系统上它通常是`NSKeyedArchiver`。旧的`NSArchiver`接口仅允许写入值流。然而，键存档支持存储类似字典的内容。它们允许你存储键值对并以不同的顺序读回。

支持归档有两个部分。你的对象必须能够将自己写入归档，并且能够将自己读回。

在`-encodeWithCoder:`方法中，你必须将对象的状态写入编码器。这并不意味着对象的所有实例变量。某些对象的实例变量仅用于缓存可以从其他地方重构的信息。通常在唤醒后重构这些信息比存储它们要好。

# 第 4 章：常见的 Objective-C 模式

## 归档对象

```objc
- (void)encodeWithCoder:(NSCoder*)aCoder
{
    if ([aCoder allowsKeyedCoding])
    {
        [aCoder encodeInt:integer forKey:@"integer"];
        [aCoder encodeObject:string forKey:@"string"];
    }
    else
    {
        [aCoder encodeValueOfObjCType:@encode(int) at:&integer];
        [aCoder encodeObject:string];
    }
}
```

*自：archive.m*

用于瞬态编码（例如，通过网络传输），而键值编码器（keyed coders）用于持久化数据。

键值归档器（keyed archivers）为存档原始 C 类型提供了更方便的方法。你可以发送诸如`-encodeInt:forKey:`等消息。旧式的归档器只有一个方法用于存储原始 C 类型，该方法接收 Objective-C 类型编码和变量的指针。

相应的加载方法可能会稍微复杂一些。归档器会为它存储的每个对象存储*类版本*（class version）。你应该在`+initialize`中通过发送一个`+setVersion:message-to-self`。

```objc
- (id)initWithCoder:(NSCoder*)aCoder
{
    if ([aCoder versionForClassName:[self className]] != 0)
    {
        [self release];
        return nil;
    }

    if ([aCoder allowsKeyedCoding])
    {
        integer = [aCoder decodeIntForKey:@"integer"];
        string = [aCoder decodeObjectForKey:@"string"];
    }
    else
    {
        [aCoder decodeValueOfObjCType:@encode(int) at:&integer];
        string = [aCoder decodeObject];
    }

    string = [string retain];
    return self;
}
```

当你更改对象的实例变量布局时，发送`+setVersion:message-to-self`。

`-initWithCoder:`方法可能需要从你程序的旧版本加载归档文件，因此它应该检查版本，如果对应于旧版本，则以不同的方式处理归档文件。

同样重要的是记住，如果且仅当父类遵循`NSCoding`协议时，要调用这两个方法的父类实现。如果它没有遵循该协议，但具有某些你希望持久化的状态，则由你负责归档这些状态以及你子类的实例变量。

## 创建指定初始化器

```objc
- (id)initWithSelectorName:(NSString*)aSel arguments:(NSArray*)args
{
    if (nil == (self = [super init]))
    {
        return nil;
    }

    selector = [aSel copy];
    arguments = [args mutableCopy];
    return self;
}

- (id)initWithSelectorName:(NSString*)aSel
{
    return [self initWithSelectorName:aSel arguments:nil];
}

- (id)init
{
    return [self initWithSelectorName:nil];
}
```

*自：designatedInit.m*

到为止看到的大多数类都是使用`-init`方法初始化的。该方法是`NSObject`中的*指定初始化器*（designated initializer）。如果你为`NSObject`创建子类，通常会重写此方法。

当创建一个新的`NSObject`子类时，它所有的实例变量都会被设置为零。你的初始化器随后可以将其中一些变量设置为其他值，并获取对象所需的任何其他资源。

> **注意：**
>
> `NSObject`中的`-init`方法什么都不做，它只是返回`self`。这意味着在直接子类中，避免向`super`发送`-init`消息是很有诱惑力的。一个对`NSObject`的分类可能会替换这个方法。

并不是所有类都以`-init`作为指定初始化器。按照约定，带参数的初始化方法是指定初始化器。

瞬态归档器（transient archivers）归档时会存储它存储的每个对象的*类版本*。键值归档器提供了更方便化的便利方法。如果父类使用指定初始化器模式，所有其他带参数的初始化方法都会调用它。

这种方法使得子类化变得更加容易。许多类提供了初始化的便利方法。

本节的示例取自 MessageSend。这是一个只允许实例的类。

## 强制单例模式

```objc
@implementation Singleton

static Singleton *sharedInstance;

+initialize
{
    if (!sharedInstance)
    {
        sharedInstance = [self new];
    }
}

+ (id)sharedInstance
{
    if (!sharedInstance)
    {
        sharedInstance = [self new];
    }

    return sharedInstance;
}

+ (id)alloc
{
    if (sharedInstance && [self self])
    {
        [NSException raise:format:@"May create more than instance."];
    }

    return [super alloc];
}

+ (id)allocWithZone:(NSZone*)aZone
{
    if (sharedInstance && [self self])
    {
        [NSException raise:format:@"May create more than instance."];
    }

    return [super allocWithZone:aZone];
}

@end
```

*自：singleton.m*

单例最常见的错误是在创建时引入竞态条件。这个特定的单例将自己存储在一个私有变量中。这对于单线程应用程序运行良好，但多线程应用程序呢？如果你从两个线程同时发送`+sharedInstance`消息，会发生什么？两者测试变量，发现它尚未被创建，然后创建它。为了避免这个问题，你可以使用锁。一个更简单的解决方案是在`+initialize`方法中创建实例。该方法在运行时第一次向类发送消息时被调用。运行时负责确保该方法在向类传递任何消息之前完成。例如，在 AppKit 中获取应用程序对象，你将向`NSApplication`发送`sharedApplication`消息。这个类是单例的一个特例，因为它将其实例存储在全局`NSApp`变量中。如果应用程序已经启动，你可以直接使用这个变量，避免获取应用程序的消息发送。

> **注意：**
>
> Apple 文档建议在创建单例的`+sharedInstance`方法中使用`@synchronized(self)`。这种方法方法比本节提出的方法要慢得多，而且需要更多代码，因此没什么理由推荐它。

GCC 运行时中存在一个长期错误会导致其无法正常工作，但在 GNUstep 运行时中已修复。

# 第 4 章：常见的 Objective-C 模式

嗯，尽管存在某些问题，它似乎是自然的解决方案。

*委托模式*（delegation pattern）背后的思想与继承和原型的原理相似：你允许一个对象定义另一个对象行为的一个子集。

你不会在 Foundation 框架中经常看到这种模式，但在 AppKit 或 UIKit 代码中非常常见。每个用户界面对象都使用委托来允许你定义在响应用户界面事件时发生什么。

有几种模式与委托有关，它们都与一个通用规则相关：你应该倾向于使用对象组合而非继承。这对于松耦合至关重要，因为它使得代码复用变得容易得多。

如果你有一个 C++ 类，它有三个父类提供了其行为的某些方面，那么修改它要比修改一个将其功能某些方面委托给另外三个类的 Objective-C 类要困难得多。

## 提供外观（Providing Façades）

```objc
@interface Control : View
{
    id cell;
}
@end

@implementation Control

- (id)selectedCell
{
    return cell;
}

- (BOOL)isEnabled
{
    return [[self selectedCell] isEnabled];
}

- (void)setEnabled:(BOOL)flag
{
    [[self selectedCell] setEnabled:flag];
    [self setNeedsDisplay:YES];
}

@end
```

*自：facade.m*

委托的一个非常常见的用法是*外观模式*（façade pattern）。它将一个或多个私有或半私有对象封装在一个公共接口中。这在 Objective-C 中非常常用，用于提供类似多继承的功能，即一个对象结合了几个不同对象的行为，并将将其某些功能委托给每个对象。

AppKit 中的`NSControl`层次结构是这种方法的很好的例子。该层次结构中的类继承自`NSView`的行为，并将行为委托给`NSCell`的子类。`NSView`提供了如图形上下文、事件处理以及与视图层次结构交互等功能。cell 则提供了如绘图等功能。本节顶部的示例是`NSControl`的（非常）简化版本。

当你在 OS X 上点击按钮时，你通常是在点击一个`NSButton`实例，它是一个`NSControl`子类，使用`NSButtonCell`进行其实现。作为程序员，你几乎可以互换使用这些控件，也可以复用它们包含的 cell。例如，如果你在表格或大纲视图中看到按钮，它是用`NSButtonCell`绘制的，而不是`NSButton`。

在第 19 章中，我们将使用 Objective 消息转发（Objective-forwarding）机制来快速方便地实现这种外观。通过直接调用包装的对象或多个对象的方法来实现它们也是可能的，也是常见的。

这种方法比多重继承灵活得多，因为它允许同一个类与许多不同的委托一起使用。在 C++ 中，你会使用模板类来实现相同的效果。它们有不同的优势。Objective-C 版本生成的代码少得多，这这意味着更好的指令缓存利用率。而 C++ 版本则在编译时让某些类别的优化（主要是内联）变得更容易。

## 创建类簇（Creating Class Clusters）

```objc
static Pair *placeHolder;

+ (void)initialize
{
    if ([Pair class] == self)
    {
        placeHolder = [self alloc];
    }
}

+ (id)allocWithZone:(NSZone*)aZone
{
    if ([Pair class] == self)
    {
        if (nil == placeHolder)
        {
            placeHolder = [super allocWithZone:aZone];
        }

        return placeHolder;
    }

    return [super allocWithZone:aZone];
}

- (Pair*)initWithFloat:(float)aFloat:(float)b
{
    return [[FloatPair alloc] initWithFloat:aFloat:b];
}

- (Pair*)initWithInt:(int)aInt:(int)b
{
    return [[IntPair alloc] initWithInt:aInt:b];
}
```

*自：classCluster.m*

类簇在 Objective-C 中非常常见。很多 Foundation 类都是类簇，你可能会发现实现一些你自己的类簇是有用的。

类簇是一个抽象的父类，它隐藏了具体的子类。这在 Objective-C 中比许多语言更容易实现，因为没有创建对象的关键字。大多数类簇都提供命名的构造函数，例如`numberWithFloat:`，它们创建正确子类的新实例。如果你向此类发送`+alloc`消息，你会得到一个占位实例。示例是 Pair 类。它没有声明任何变量。

```objc
@implementation IntPair

- (Pair*)initWithInt:(int)aInt:(int)b
{
    first = aInt;
    second = bInt;
    return self;
}

- (NSString*)description
{
    return [NSString stringWithFormat:@"%d, %d",
        first, second];
}

- (float)firstFloat { return first; }
- (float)secondFloat { return second; }
- (int)firstInt { return first; }
- (int)secondInt { return second; }

@end
```

*自：classCluster.m*

这些具体子类中的每一个都很简单。它们都声明了两个实例变量：一个是 int 类型，另一个 float 类型。它们都提供一个单一的初始化方法，该方法仅从父类调用，然后它们重写了方法。这个示例没有在父类中提供任何有用方法。在实际实现中，你可能会看到父类中实现了比较或算术方法。或者，它们可能在单独的分类中提供。

类簇隐藏了实现细节。你可以更改私有子类的任何方面，而无需修改甚至重新编译使用它们的代码。这就是为什么 Objective-C 中的代码复用比 C++ 等语言常见得多的原因之一。在 Objective-C 中产生具有公共接口和私有实现的代码是非常容易的，且使用的代码不依赖实现的任何方面。

子类类簇通常需要实现少数*原始方法*。父类中的其他方法都是基于这些核心功能实现的。我们将在第 7 章的“集合子类化”部分详细讨论这一点。

例如，如果你想创建一个`NSString`的子类，你必须实现`-length`和`-characterAtIndex:`。该类中的所有其他方法都调用这两个方法。一个更高效的实现还会实现`-getCharacters:range:`。

## 使用运行循环（Using Run Loops）

```objc
[[NSRunLoop currentRunLoop] run];
```

*自：timer.m*

定义结构的设计模式

大多数非复杂的 Objective-C 程序的核心都是*运行循环*（run loop）。通常情况下，运行循环等待来自一个或多个事件源的数据，然后响应这些数据执行代码，从而提供了一种*事件驱动编程*模型。

Foundation 框架在`NSRunLoop`类中提供了运行循环的实现。如果你正在编写应用程序，通常系统会自动为你创建一个该实例。你也可以在命令行工具中显式地创建一个。

应用程序中的主运行循环监听来自窗口服务器的事件，对应于按按下、鼠标移动、触摸事件等。其他各种类会隐式地向运行循环添加事件源。例如，`NSTimer`类（我们第 8 章介绍）会向运行循环添加一个定时器事件源，允许你在特定时间执行某些操作。

第 16 章介绍的通知机制允许你通过运行循环传递程序内任意事件的通知，你还可以通过`NSFileHandle`注册文件描述符活动的通知。

运行循环本身与内存管理有关。每次运行循环迭代都有自己的自动释放池（autorelease pool）。这意味着在运行循环迭代期间发送了`-autorelease`消息的对象将在迭代结束时被销毁（除非在其他地方被保留）。



正因如此，加上运行循环用于传递来自用户输入的事件，最好将单次运行循环迭代中完成的工作量保持尽可能小。在大多数程序中，你不需要直接与运行循环交互。它在后台运行，而其他类提供了更方便的接口。

## 数字

Objective-C 和 Smalltalk 之间的主要区别之一是 Objective-C 继承了全范围的原始（非对象）C 类型。按大小从小到大排列分别是 `char`、`short`、`int`、`long` 和 `long long` 整数，包含有符号（`signed`）和无符号（`unsigned`）变体，以及两种浮点类型：`float` 和 `double`。它们的行为与 C 语言完全相同，并带有类型提升规则。你还会发现 Objective-C 编译器支持 `long double` 类型，这取决于架构。

注意，这与 Java 非常相似，Java 也只有少量非对象类型，但存在一些非常重要的区别。在 Java 中，内建类型（intrinsic types）被定义为固定大小。而在 C 中，它们被定义为具有最小精度。例如，规范规定 `int` 具有“执行环境架构建议的自然大小”，而在 Java 中，它被明确定义为“32 位有符号补码整数”。

除了原始类型外，C 还支持通过 `typedef` 关键字为现有类型定义新名称。最常见的原因是规范没有要求任何标准类型具有特定大小，只需确保每个类型至少与前一个类型一样大。特别是目前部署的一些平台上，`int` 可能是 16 位、32 位或 64 位，因此你不能依赖这些类型的任何特定大小。

OS X 支持 ILP32 和 LP64 模式。这种缩写用于描述哪些 C 类型具有多大的位宽。ILP32 意味着 `int`、`long` 和指针都是 32 位。LP64 意味着 `long` 和指针是 64 位数值，并且隐含地其他值较小。

相比之下，Microsoft Windows 在 64 位架构上是 LLP64 平台；`int` 和 `long` 保持为 32 位，只有指针和 `long long` 是 64 位。如果你假设可以安全地将指针转换为 `long`，就会产生问题——这种操作在世界上几乎所有平台（包括 Win32）上都可行，但在 Win64 上无效。

将指针转换为整数是一个严重的问题。`long long` 类型至少有 64 位，因此在任何当前平台上，它保证足够存储任何指针，但在任何 32 位或 16 位平台上，它可能太大了。

### 在集合中存储数字

C99 引入了 `intptr_t` 定义，其大小与指针完全相同。Apple 引入了等效类型：`NSInteger`。它贯穿 Cocoa 框架，且大小始终与指针相同。还有一个无符号版本 `NSUInteger`。

在 GUI 代码中，你经常会遇到 `CGFloat` 或 `NSFloat`。它们是等价的。它们的大小与指针相同，使得它们在 32 位平台上是 `float`，在 64 位平台上是 `double`。

# 第 5 章：数字

`numberArray.m` 示例将一组 `NSNumber` 实例存储在数组中，然后使用 `-compare:` 选择器对它们进行排序。从输出可以看出，无论数字是如何创建的，排序顺序都会强制执行。

```text
1 2010-03-15 14:50:48.166 a.out[51465:903] (
2 "-9223372036854775808",
3 "-2",
4 1,
5 "200.0123",
6 "300.057",
7 18446744073709551615
)
```

*输出来自：`numberArray.m`*

### 执行小数算术

```objc
NSDecimalNumber *one = [NSDecimalNumber one];
NSDecimalNumber *fortyTwo = [NSDecimalNumber decimalNumberWithString:@"42"];
NSDecimalNumber *sum = [one decimalNumberByAdding: fortyTwo];
NSDecimal accumulator = [sum decimalValue];
NSDecimal temp = [fortyTwo decimalValue];
NSDecimalMultiply(&accumulator, &accumulator, &temp, NSRoundPlain);
temp = [one decimalValue];
NSDecimalAdd(&accumulator, &accumulator, &temp, NSRoundPlain);
NSDecimalNumber *result = [NSDecimalNumber decimalNumberWithDecimal:accumulator];
```

*来自：`decimal.m`*

C 语言提供了两种处理数字的选项：整数和浮点值。浮点值由两个部分组成：尾数和指数。它们的值是 2 的指数次方乘以尾数。

浮点值的问题在于它们是二进制的。这意味着它们的精度是根据二进制位定义的，而这并不总是你想要的。例如，对于财务应用程序，你可能需要精确存储到四位小数的金额。这通过浮点值是无法实现的；像 0.1 这样的值无法用任何有限的二进制浮点表示，就像三进制的 0.1（三分之一）无法用任何有限的小进制序列一样。

二进制数是 2 的幂次和，就像十进制数是 10 的幂次和一样。对于小数，基点后的数字表示二分之一、四分之一、八分之一等。如果你尝试通过相加 2 的幂来创建一个 0.1 的值，你永远无法成功，尽管你会越来越接近。当你尝试通过相加 10 的幂来创建一个三分之一（三十分之一，加上百分之一，再加上千分之一，等等）时，也会发生同样的情况。

一种解决方案是使用固定点算术。与其存储美元，你可能存储分的百分分之一。你必须记得归一化你的值，并且你受到整数类型的范围限制。Objective-C 提供了另一种选择：十进制浮点类型。

`NSDecimal` 类型是一个表示小数值的 C 结构体。有点奇怪的是，没有用于创建这些值的 C API。你必须创建一个 `NSDecimalNumber` 实例，然后向它发送一个 `-decimalValue` 消息。

你对算术运算有两种选择。`NSDecimalNumber` 实例是不可变的。你可以根据算术结果创建新的实例——例如，通过向一个发送 `decimalNumberByAdding:` 消息。

或者，你可以使用 C API，它会直接修改结构体的值。如果你只执行一次算术运算并将结果存储在对象中，第一种方案更简单。如果你正在执行多个步骤，那么使用 C API 会更快。因为它们直接修改结构体，所以你不需要为每个中间步骤创建一个新对象。

**注意：**

CX 包含了十进制数字类型，某些编译器作为扩展支持这些类型。`NSDecimal` 类型与这些类型不兼容。在大多数平台上，这并不重要。如果你的目标是类似 IBM 的 POWER6 这种具有十进制算术硬件的设备，那么直接使用十进制类型会更好。

这两种方法都不特别快。十进制数被表示为数字数组，在两个数字归一化后，会成对地进行操作。你可以预期获得与软件浮点实现相似的性能——可能稍微略差，因为 `NSDecimal` 没有被广泛使用，因此没有成为许多优化工作的重点。`NSDecimalNumber` 是 `NSNumber` 的子类，所以我们在下一节中将看到的所有将 `NSNumber` 转换为字符串的方法都能按预期工作。你也可以将它们转换为

### 字符串与数字的转换

```objc
int answer = [@"42" intValue];
NSString *answerString = [NSString stringWithFormat:@"%d", answer];
NSNumber *boxedAnswer = [NSNumber numberWith:answer];
assert([answerString isEqualToString:[boxedAnswer stringValue]]);
```

*来自：`strtonum.m`*

有多种方法可以在数字和字符串之间转换。许多表示简单数据的对象都有如 `intValue` 这样的方法，返回整数。如果你有一个包含数值的字符串，可以向它发送 `-doubleValue`、`-floatValue`、`-intValue` 来将其转换为这些类型。在 Foundation 的安全版本中，你也可以发送 `-intValue`。

有多种反向操作的方法，获取字符串。方法可能会截断或近似该值。如果你已经在 `NSNumber` 实例中拥有了一个数字，有两种获取字符串的方法，其中一种是另一种方法的封装。`descriptionWithLocale:` 方法根据指定的区域对数字进行格式化并返回字符串。

实际上，它并没有执行翻译。它向一个新的 `NSString` 发送 `initWithFormat:locale:` 消息。格式字符串取决于数字类型：例如，`double` 将使用 `%0.16g` 格式字符串转换。这使用最多 16 位有效数字，并在需要时使用指数。

小数点分隔符取决于区域设置。如果你向 `NSNumber` 发送 `-stringValue` 消息，这等同于将 nil 作为参数发送 `-descriptionLocale:`。这使用标准区域设置，因此在任何平台上结果都是相同的。

如何，给定一个字符串，我们如何从中解析值？

答案在于 `NSScanner` 类。

### 从字符串读取数字

```objc
NSScanner *parser = [NSScanner scannerWithString:@"1 plus 2"];
int operands[2];
NSString *operation;
[parser setCharactersToBeSkipped:[NSCharacterSet whitespaceCharacterSet]];
[parser scanInt:operands];
[parser scanCharactersFromSet:[NSCharacterSet letterCharacterSet] intoString:&operation];
[parser scanInt:operands+1];
```

*来自：`scanner.m`*

任何 C 程序员首先学会使用的两个函数是 `printf()` 和 `scanf()`。这两个函数非常相似——一个几乎是另一个的反过来——它们让你能够构造格式化字符串并从中解析数据。我们已经见过 `NSString` 有一个 `sprintf()` 的粗略模拟，所以你可以从格式字符串和变量构造字符串，但 Objective-C 中 `sscanf()` 的等价物是什么？如何，给定一个字符串，我们如何从中解析值？

答案在于 `NSScanner` 类。这个类是一个非常强大的分词器类。你创建一个附加到字符串的 `NSScanner` 实例，然后一次一次地从中扫描值。

你发送给扫描器的所有消息都具有相同的格式。它们接收一个变量的指针并返回一个 `BOOL`，表示操作是否成功。扫描器将当前的扫描索引存储在字符串中，只有在扫描成功时才会对其递增，因此你可以尝试以不同的方式解析后续字符。你也可以非常方便地使用 `NSScanner` 实现预读和回溯。若你向它发送一个 `-scanLocation` 消息，它会返回字符串中的当前索引。然后你可以尝试扫描一些内容，遇到错误后，通过发送一个 `-setScanLocation:` 消息来回溯，从而重置旧索引。

`NSScanner` 最强大的方法之一是 `-scanCharactersFromSet:intoString:`。它从当前扫描点开始读取字符串，直到遇到一个不在指定集合中的字符为止。正如我们在第 6 章中看到的，你可以使用任何任意字符集构造 `NSCharacterSet` 实例，也可以使用标准集合中的一个。

本节开头的示例从字符串中读取了一个数字、一个单词，然后是另一个数字。数字是使用内置的 `-scanInt:` 方法读取的，但单词的部分要复杂一些。它使用了一个 `NSCharacterSet`，在本例中是所有字母的集合。

这并不是示例中使用的唯一 `NSCharacterSet`。该扫描器还配置为跳过空白字符。发送给扫描器的 `setCharactersToBeSkipped:` 消息会告诉它忽略作为参数传递的集合中的任何字符。传递空白字符集会告诉它跳过调用之间发生的任何空白字符。当你发送扫描消息时，如果扫描器开始读取的位置存在该集合中的字符，它将跳过这些字符。在解析标记（token）时，它不会跳过这些字符，因此在字符串中放入“1 2”会被读取为两个独立的数字，而不是 12。

### 字符串操作

Objective-C 提供两种字符串：C 字符串和 Objective-C 字符串（也称为字符串对象）。作为编译器扩展，GCC 也允许你使用 Pascal 字符串，但这些字符串非常罕见，且仅为了与 Pascal 库兼容而提供支持。

C 字符串是一种非常原始的数据类型。它是一个字符数组，以 NULL 字节终止。它没有字符编码的概念，可以存储任何不包含零字节的字节序列。UTF-8 专门为与 C 字符串配合而设计：它是一种变长度编码，即使在多字节序列中也不使用零字节。

Objective-C 字符串是一种高级抽象。它被用作 UTF-16 字符序列进行访问，但其内部表示是私有的。如果你为 GNU 运行时编译 Objective-C，常量字符串将由具有三个实例变量的类实例表示：`isa` 指针、一个指向 C 字符串的指针以及一个包含 C 字符串长度的整数。当模块加载时，运行时（runtime）会将 `isa` 指针设置为正确的类。

当你访问 Objective-C 字符串中的单个字符时，你使用 `unichar` 类型。它代表单个 UTF-16 字符。注意，UTF-16 也是一种变长度编码，单个 Unicode 字符可能多于一个 UTF-16 字符。让事情更复杂的是，像重音之类的组合标记可能意味着使用多个 Unicode 字符来表示单个字形（glyph）。

### 创建常量字符串

```objc
const char* cstring = "C string";
NSString *objcstring = @"Objective-C string";
CFStringRef cfstring = CFSTR("Core Foundation string");
```

*源自 `constantStrings.m`*

在 OS X 上，Objective-C 字符串与 Core Foundation (CF) 字符串无缝桥接（toll-free bridged）。常量 CF 字符串的表示方式与 GNU runtime Objective-C 字符串类似，但有几点不同。它们的 `isa` 指针设置为 Core Foundation 框架中存在的外部引用，因此不需要链接 Objective-C runtime 或 Foundation 框架即可工作。它们还有一个 `flags` 字段，允许其内部表示可以是 UTF-8 或 UTF-16，取决于哪种对其内容更高效。

常量 Objective-C 字符串通过在常量 C 字符串字面量前加上 `@` 符号创建，例如 `@"string"`。你也可以在 C 和 Objective-C 代码中使用 `CFSTR()` 宏来创建常量 Core Foundation 字符串。该宏调用编译器内置函数，以生成一个常量字符串对象。

### 比较字符串

```objc
NSString *twelve = @"12";
NSString *twelveFromInt = [NSString stringWithFormat:@"%d", 12];
NSNumber *numberTwelve = [NSNumber numberWithInt:12];

if ([twelve isEqualToString:twelveFromInt])
    NSLog(@"Both strings are equal");

if (twelve == twelveFromInt)
    NSLog(@"Both strings are equal");

if (twelve == @"12")
    NSLog(@"Constant strings are equal");

if ([twelve isEqual:numberTwelve])
    NSLog(@"String is equal");
```

*源自 `CompareStrings.m`*

比较字符串相等性最简单、直接的方法是使用比较运算符 `==`。不幸的是，这可能会导致微妙的 bug。如果你想测试两个字符串是否相等，应该使用 `isEqual:` 方法。注意，该方法期望参数是 Objective-C 字符串。在本节开头，编译器通常会合并常量字符串，使得 `twelve` 和字面量 `@"12"` 成为同一个对象。这并不是保证的，但没有正理由编译器不这样做。字符串与 `Number` 实例之间的比较更有意思。你可能认为这会将字符串与向该数字发送 `-stringValue` 的结果进行比较，但事实并非如此。

这一点很重要，因为相等性必须满足交换律。如果 `[a isEqual:b]` 为真，很多代码会假设 `[b isEqual:a]`。这在集合类中尤为如此。例如，如果你向 `NSMutableSet` 插入两个对象，而相等性仅在一个方向上成立，那么结果是未定义的。

通常，当你想要比较字符串（或者说，是任何对象）时，你不仅想知道它们是否相等，还想知道它们的顺序。这让字符串的比较开始变得复杂。对于两个数字，它们之间有一个唯一的规范排序。而对于字符串，有几种定义良好的排序方式。“etoile”、“Étoilé”和“Etoile”应该按什么顺序排列？如果你进行的是不区分大小的比较，第一个和最后一个将具有相同的排名。带重音的字母紧跟在不带重音变体之后，还是在所有不带重音字母之后，取决于你的区域设置（locale）。



当你有一个文件列表时，如果你将`file10`排在`file2`之前，用户可能会感到恼火，尽管这是这两个文件名的字典顺序。对于仅基于字符值的简单比较，你可以使用`-compare:`方法。这，就像所有其他比较

## 第 6 章：字符串操作

`results`返回一个`NSComparisonResult`，这是一个带有三个可能值的枚举类型：`NSOrderedAscending`（升序）、`NSOrderedSame`（相同）和`NSOrderedDescending`（降序）。如果你正在向用户展示数据，应该使用`-localizedCompare:`。这将根据用户所选语言的定义规则返回两个字符串的排序结果。这两者都是此通用比较方法的封装：

```objectivec
- (NSComparisonResult)
compare: (NSString*)aString
options: (NSStringCompareOptions)mask
range: (NSRange)range
locale: (**id**)locale;
```

这允许你指定一组选项，例如，`NSNumericSearch`用于让`10`排在`9`之后，以及`NSCaseInsensitiveSearch`用于忽略大小写。将范围作为第三参数传递允许你将比较限制在接收者的子字符串中，传递`locale`则允许你指定非 ASCII 字符的排序规则。注意的是，通常将`nil`作为`locale`意味着使用当前区域设置或*规范区域（canonical locale）*。在这种情况下，传递`nil`意味着使用规范区域并对字符值进行数值比较。

### 逐字符处理字符串

```objectivec
for (NSUInteger i=0 ; i<[aString length] ; i++)
{
    unichar c = [aString characterAtIndex: i];
    // Process c
}
```

*源自：stringIterateSlow.m*

`NSString`类是一个*类簇（class cluster）*。它是一个抽象类，当你创建一个它时，你得到的是某个私有子类的实例。任何`NSString`子类都必须实现两个原始方法：`-length`和`-characterAtIndex:`。其中第一个返回长度，第二个返回字符串中特定索引处的字符。

如果你需要对字符串中的每个字符进行操作，可以在简单的循环中对其进行迭代，并反复调用此方法。这种方式非常低效，因为每个字符都需要进行一次消息发送（message send）。这比访问 C 字符串中的字符要贵得多。此版本还会为每个字符发送一个`-length`消息，只有在长度在迭代过程中可能会变化时才需要这样做。

另一种方法是获取一个 C 字符串并对其进行操作。例如，你可以向字符串发送`-UTF8String`消息，然后处理返回的 C 字符串。尽管这听起来合理，但请记住字符串可能很大，并且可能不是以 UTF-8 格式存储，因此对象可能需要将其内部表示转换为 UTF-8，分配内存来存储它，稍后由自动释放池（或垃圾回收器）清理该内存。

访问字符串中字符最高效的方法是`-getCharacters:range:`。Objective-C 中以`get`开头的方法通常接收一个指向调用者分配的空间的指针，并返回其中的数据。在这种情况下，第一个参数是一个指向`unichar`缓冲区的指针，该缓冲区必须足够大以存储请求的字符。

下一个示例使用此机制来计算源文件中分号的数量。首先，它将源代码加载到字符串中，然后一次获取十个字符。注意双重循环结构。外层循环获取字符块，内层循环遍历该块。当你使用*快速枚举（fast enumeration）*来遍历集合时，编译器也会生成相同的结构。

每十个字符需要发送一次消息。你可以通过增加缓冲区的大小，用额外的空间换取更快的速度。注意这个缓冲区是分配在栈上的。这是很快的，但你应该

```objectivec
int semicolons = 0;
NSUInteger length = [str length];
NSRange range = { 0, 10 };
while (range.location < length)
{
    unichar buffer[10];
    if (range.location + range.length > length)
    {
        range.length = length - range.location;
    }
    [str getCharacters:buffer range:range];
    range.location += 10;
    for (unsigned i=0 ; i<range.length; i++)
    {
        unichar c = buffer[i];
        if (c == ';')
        {
            semicolons++;
        }
    }
}
printf("Source file contained %d semicolons\n", semicolons);
```

*源自：StringIterate.m*

`NSString`类是一个*类簇（class cluster）*。它是一个抽象类，当你创建一个它时，你得到的是某个私有子类的实例。任何`NSString`子类都必须实现两个原始方法：`-length`和`-characterAtIndex:`。其中第一个返回长度，第二个返回字符串中特定索引处的字符。

如果你需要对字符串中的每个字符进行操作，可以在简单的循环中对其进行迭代，并反复调用此方法。这种方式非常低效，因为每个字符都需要进行一次消息发送。这比访问 C 字符串中的字符要贵得多。此版本还会为每个字符发送一个`-length`消息，只有在长度在迭代过程中可能会变化时才需要这样做。

另一种方法是获取一个 C 字符串并对其进行操作。例如，你可以向字符串发送`-UTF8String`消息，然后处理返回的 C 字符串。尽管这听起来合理，但请记住字符串可能很大，并且可能不是以 UTF-8 格式存储，因此对象可能需要将其内部表示转换为 UTF-8，分配内存来存储它，稍后由自动释放池（或垃圾回收器）清理该内存。

访问字符串中字符最高效的方法是`-getCharacters:range:`。Objective-C 中以`get`开头的方法通常接收一个指向调用者分配的空间的指针，并返回其中的数据。在这种情况下，第一个参数是一个指向`unichar`缓冲区的指针，该缓冲区必须足够大以存储请求的字符。

下一个示例使用此机制来计算源文件中分号的数量。首先，它将源代码加载到字符串中，然后一次获取十个字符。注意双重循环结构。外层循环获取字符块，内层循环遍历该块。当你使用*快速枚举（fast enumeration）*来遍历集合时，编译器也会生成相同的结构。

每十个字符需要发送一次消息。你可以通过增加缓冲区的大小，用额外的空间换取更快的速度。注意这个缓冲区是分配在栈上的。这是很快的，但你应该

### 编码转换

要从某种其他编码的 C 字符串创建字符串对象，使用`+stringCString:encoding:`方法。该方法的第一个参数是 C 字符串，第二个参数是表示编码的枚举类型成员。如果数据来自旧版 Mac，你可能想使用`NSMacOSRomanStringEncoding`，这是在 Mac OS 支持 Unicode 之前的默认编码。如果你需要与旧 Windows 系统交互，`NSWindowsCP1252StringEncoding`是你在大多数地区需要的编码。较新的 Windows 系统将使用 UTF-16，但它们更偏好小端版本`NSUTF16LittleEndianStringEncoding`。

如果你以特定编码存储字符串数据，通常会使用`NSData`实例而不是指针。这是一个非常简单的类，它封装了一个内存区域：一个指针和一个大小。因为它是一个对象，你可以对其进行内省，使用引用计数处理销毁，并将其存储在集合中。在许多情况下，这比直接使用指针更方便。

在使用某种拉丁字母变体的国家，最常见的文本编码是 UTF-8。它允许你用单字节表示任何 ASCII 字符，并用两个字节表示大多数其他字符。`NSString`提供了获取和设置 UTF-8 数据的便利方法：`-UTF8String`和`+stringWithUTF8String:`。在大多数中，每当你从 C 字符串转换时，可以使用这些方法。如果你使用表意文字，UTF-8 是相当低效的。

### 修剪字符串

```objc
NSString *str = @"* String with leading spaces*";
str = [str stringByTrimmingCharactersInSet:[NSCharacterSet whitespaceCharacterSet]];
str = [str substringFromIndex:2];
NSAssert([str isEqualToString:@"String with leading spaces*"], @"Trimming failed");
```

*源自 trim.m*

通常，当你有一个字符串时，你想要修剪它的末端，即移除固定数量的字符或来自特定集合的字符。第二种情况的一个常见例子是移除字符串开头和结尾的空白。

Objective-C 字符串对象提供了许多方法来实现这一操作。如果你只是想移除字符串的尾部或开头字符，`NSString`上的`-substringWithRange:`方法是最有用的。它会创建一个新的字符串对象，其中包含另一个字符串中某个范围的字符。对于不可变字符串来说，这是一个非常廉价的操作；它只是返回一个引用原始字符串数据的字符串对象，而不会复制字符串。然而，当你对可变字符串调用该方法时，它必须复制字符。

要从特定集合集中移除字符，你需要了解`NSCharacterSet`对象。正如其名称所示，该类封装了一个字符集。你可以从字符串创建这些集合，也有许多预定义的集合代表了特定的、定义良好的字符集。

该类的用法与 C 语言中的`ctype.h`函数类似。你可以向它发送`-characterIsMember:`消息，以测试单个字符是否为集合的成员。例如，调用 C 库函数`ispunct()`等同于向通过发送`+punctuationCharacterSet`消息获取的对象发送`-characterIsMember:`消息。

Objective-C 的版本更冗长，但更具通用性。字符集对象可以很容易地在代码中传递。`NSString`类在许多地方使用了它们。例如，你可以请求字符串中给定集合的字符范围，或者使用字符集定义分隔符来拆分字符串。

### 拆分字符串

```objc
NSString *str = @"A String with\twords and spaces";
NSArray *wordsWithTab = [str componentsSeparatedByString:@" "];
NSArray *words = [str componentsSeparatedByCharactersInSet:[NSCharacterSet whitespaceCharacterSet]];
```

*源自 split.m*

在 Objective-C 中拆分字符串有三种方法。第一是显而易见的：只需遍历字符，直到找到一个合适的拆分位置，然后使用`-substringWithRange:`创建新的标记（token）。这在通用情况下可行，但对于这种本该轻而易举的事情来说太费精力了。

在 C 语言中，你可以使用`strsep()`函数或已弃用的`strtok()`函数，在特定集合中字符出现的任何地方拆分字符串。`NSString`上的`-componentsSeparatedByCharactersInSet:`方法的工作原理几乎完全相同，尽管它接受一个`NSCharacterSet`作为参数而不是字符串。

你可以通过使用`+characterSetWithCharactersInString:`构建字符集，使该方法的行为得像`strtok_r()`。`NSString`方法返回一个包含子字符串的`NSArray`。这与 C 语言函数的工作完全相同；每当有两个相邻的分隔符字符时，你会得到空字符串。

此外，你也可以根据特定子字符串的出现来拆分字符串。当分隔符由多个字符组成时，这种方法非常有用。

### 拷贝字符串

```objc
NSString *staticString = @"a string";
NSString *constantString = [staticString copy];
NSString *stringAlias = [constantString retain];
NSMutableString *mutableString = [stringAlias mutableCopy];
NSMutableString *mutableStringAlias = [mutableString retain];
```

*源自 stringcopy.m*

C++ 往往比它应有的慢很多的地方之一就是在处理字符串时。在任何你有纯手动内存管理的环境中，人们倾向于对对象进行防御性拷贝，以维护清晰的所有权规则。

在 Objective-C 中，这种情况较少见，更多代码面临的是相反的问题：在应该使用拷贝的地方保留了对可变对象的引用（retaining references）。当你向`NSString`发送`-copy`消息时，它的效果与发送`-retain`相同。

你可能会想问，为什么我们有两个执行相同功能的方法？答案很简单：`NSMutableString`是`NSString`的子类。如果你向`NSMutableString`发送`-retain`消息，你会增加引用计数。如果你发送`-copy`消息，你将得到一个新对象。情况可能比这更复杂，因为某些`NSMutableString`的具体子类支持“写时拷贝”（copy-on-write），因此`NSMutableString`实例在其中一个被修改之前会共享相同的数据。

### 从模板创建字符串

```objc
int a = 12;
float b = 42.0;
const char *cString = "words";
id object = [NSObject new];
NSString *string = [NSString stringWithFormat:@"%d, %f, %s, %@", a, b, cString, object];
```

*源自 formatstring.m*

如果你有 C 语言背景，学到的第一个函数之一可能是`printf()`。这是一个变参函数，接受格式化字符串作为第一个参数。格式化字符串的内容定义了其他参数的类型。

Objective-C 作为 C 语言的后代，继承了格式化字符串的概念。Objective-C 的格式化字符串与 C 字符串几乎一样，但多了一个特性：`%@`说明符表示匹配的参数是一个对象。

对象应该知道如何描述自己。每个对象都应该响应`-description`消息，该消息返回一个描述对象的`NSString`。许多类从`NSObject`继承了这一点，它只返回类名和对象在内存中的地址。其他类提供了更方便的方法。例如，集合类以 NeXT 风格的属性列表输出其内容。

注意：GNU 调试器（gdb）对`-description`方法有一些内置支持。当你对对象使用`print-object`命令（可以缩为`po`）时，它会调用对象的描述方法。这样做时要小心，因为它会在被调试进程中运行某些代码，这些代码可能也包含 Bug。然而，当它有效时，非常有帮助。我们将在第 18 章详细讨论调试。

你可以使用类似于`asprintf()`的变参方法从格式化字符串创建 Objective-C 字符串对象。第一个参数是包含某些格式说明符的 Objective-C 字符串，其余参数是用于替换说明符的变量。`formatstring.m`示例展示了如何将格式化字符串用于`NSString`。该示例根据给可执行文件的参数构造了一个字符串，然后将其写入标准错误输出。注意我们需要在处创建一个`NSAutoreleasePool`。

# 第 6 章：操作字符串

```objc
int main(int argc, char **argv)
{
    [NSAutoreleasePool new];
    NSMutableString *str = [NSMutableString stringWithFormat:@"%d arguments: ", argc];
    for (int i=0 ; i<argc ; i++)
    {
        [str appendFormat:@"%s ", argv[i]];
    }
    NSLog(@"%@", str);
    return 0;
}
```

*源自 formatstring.m*

该程序的开始。使用格式化字符串会创建一些临时对象，这些对象是自动释放的。如果你没有自动释放池，你将收到一个警告，提示这些对象发生了内存泄漏。在这个微小的程序中，它们反正是泄漏了；告诉自动释放池去回收它们并没有意义，因为操作系统会在进程退出时自动回收内存。

这个示例首先创建一个可变字符串，包含传递给程序的参数数量。然后它遍历剩余的参数，将每个参数（作为 C 字符串）附加到可变字符串。最后，它将结果传递给`NSLog()`。

`NSLog()`函数也使用了格式化字符串。直接将`str`作为第一个参数传递是很诱惑力的。在有人使用带有`%`符号的字符串作为该程序的参数之前，这将运行良好。这时，函数将查看第二个参数并尝试解释它。不幸的是，并没有第二个参数，所以它将从寄存器中读取一个随机值。如果它将其解释为某种数字，那就不是大问题。如果它将其解释为指针（指向 C 字符串或 Objective-C 对象），它几乎肯定会崩溃。通过传递`@"%@"`，我们告诉`NSLog()`只有一个真实的参数，并且该参数是一个对象。



### 存储富文本

```objc
NSDictionary *keyword = [[NSDictionary dictionaryWithObject: @"keyword" forKey: @"type"] retain];
NSMutableAttributedString *program = [NSMutableAttributedString new];

NSAttributedString *fragment = [[NSAttributedString alloc] initWithString: @"int" attributes: keyword];
[program appendAttributedString: fragment];
```

*源自 `richText.m`*

字符串仅仅是字符列表。在显示字符串之前，你通常需要其他属性。这些属性描述了字体、大小、对齐方式和下划线样式等。

如果你正在编写处理结构化文本的内容——例如 HTML 或另一种形式的语义标记（如 DocBook），那么这些属性可能是一级标题或有序列表。

Foundation 提供了一个类，用于为字符串分配任意属性。`NSAttributedString` 类允许你将字典附加到富属性字符串的范围上。这些字典可以包含你想要的任何任意信息，包括语义标记。

AppKit 使用了该类，并为字典定义了几个用于提供显示标记的键。你可以使用它将一个 `NSFont` 实例附加到文本范围，并让 AppKit 的文本系统以指定的字体显示该范围的文本。

示例将程序片段作为富属性字符串进行构建，为定义关键字定义了属性。你随后可能会有一个转换器，它取这个富属性字符串并生成一个使用显示属性以便在文本视图中显示的字符串，或者生成另一个从该标记生成 HTML 的字符串。

记住，`NSAttributedString` 是通用的。你可以用它将任何你想要定义的属性附加到字符串的范围上。

## 第 7 章：使用集合

与我们过的其他内容一样，Objective-C 中有两种集合：面向对象的版本和原始 C 类型。后者如往常一样，是构建在前者之上的。

在 C 中，有两种复合数据类型：数组和结构体。数组只是包含相同类型数据的内存块。结构体具有固定的布局，并可能包含不同类型的元素。C 复合类型是指针算术上非常薄的一层语法糖。当你访问数组中的元素时，编译器会将数组索引乘以一个元素的大小，并将此结果加到数组的起始指针上。当你访问结构体中的元素时，编译器会在结构体的起始指针上加上一个固定的偏移量。

Objective-C 集合是更高级的构造。每个 Objective-C 集合与 Objective-C 添加的大多数其他功能一样，都是对象。你通过向它们发送消息来与之通信。Foundation 框架包含了许多集合类，用于存储有序和无序数据，以及映射或索引集。Objective-C 中的大多数集合类都存储对象。与异构的 C++ STL 不同，Objective-C 集合存储的是对象。

与异构的 C++ STL 不同，Objective-C 集合是对象。

如果你想创建一个新的子类，并且你想让父类中的其他方法工作，那么你必须实现这两个方法。

### 使用数组

```objc
NSArray *array = [NSArray arrayWithObjects:@"array", @"containing", @"string", @"objects", nil];
NSMutableArray *mutable = [array mutableCopy];
[mutable sortUsing:@selector(compare:)];
[mutable addObject:];
[mutable removeAllObjects];
```

*源自 `nsarray.m`*

除了 C 数组外，Foundation 还提供了 `NSArray` 类及其可变子类 `NSMutableArray`。它们实现了一种抽象数据类型，将从零开始的整数映射到对象。在内部，它可能由 C 数组、跳表列表或其他数据结构实现，取决于它是如何创建的。例如，如果你通过合并两个不可变数组创建一个数组，你可能会得到一个不存储任何内容仅访问另外两个数组的复合数组。

创建 Objective-C 数组简单的方法是使用 `+arrayWithObjects:` 方法，该方法由 `NSArray` 和 `NSMutableArray` 同时实现。这是另一个可变方法的示例，它接收一系列对象作为参数，并使用 `nil` 表示列表的结束。当你使用变量作为此方法的参数时，必须确保没有一个变量是 `nil`，否则数组将将其视为列表的结束并忽略后面的值。

**注意：** 大多数 Objective-C 集合不允许你将 `nil` 作为值存储。如果你需要表示空值而非值的缺失，可以使用 `NSNull` 类。它提供了一个单例对象，可以通过 `[NSNull null]` 访问。

子类化 `NSMutableArray` 稍微困难一点；它又增加了六个原始方法。然而，大多数情况下，你是在使用数组而不是对其进行子类化。你可以通过两种方式向可变数组插入对象：`-addObject:`（将其添加到末尾）或 `-insertObject:atIndex:`（将其插入指定位置）。

### 操作索引

指定的索引。后一种方法会将数组中的所有后续对象后移一位以腾出空间。要替换对象，请使用 `-replaceObject:withObject:`。

数组通过整数索引。通常，你想对数组中的一组值进行某些操作。一种名为 `NSIndexSet` 的特殊类用于存储索引组。在内部，它存储的是一个范围集合，因此可能非常密集。索引集的一个非常常见的用途是在枚举数组时收集索引，然后在最后将它们删除。在枚举集合的同时从中删除对象是一个坏主意，在大多数情况下它会抛出异常。如果你将想要删除的每个索引添加到索引集中，就可以一次性删除所有它们。

涉及索引集的操作通常比涉及索引的相关操作更高效。即使在相对原始的实现中也是如此，因为你需要的消息发送（message sends）更少。数组上的每个操作都会都会进行边界检查，以确保它不会引用超出数组末尾的索引。使用索引集，接收者只需要将 `-lastIndex` 的结果与数组的最后一个索引进行比较，就可以对索引集中的每个元素进行操作而无需进行范围检查。

与其他集合一样，索引集也有可变和不可变版本。大多数情况下，你会使用可变版本。你通过添加和删除单个索引或范围来操作它。你可以使用索引集存储对任何内容的索引，但它们与 `NSArray` 结合使用时最有用，`NSArray` 有几个方法设计为接受索引集作为参数。如果你只是想处理数组中的某些子元素，通常可以将它们作为创建子数组的替代方案。

### 存储无序对象组

```objc
NSArray *array = [NSArray arrayWithObjects:@"seven","eight",nil];
NSSet *set = [NSSet setWithArray:array];
NSMutableSet *mSet = [set mutableCopy];
NSCountedSet *cSet = [NSCountedSet setWithArray:array];
```

如果你想存储一个没有顺序的对象集合，可以使用 `NSSet` 及其可变子类。这模拟了数学中的集合，因此插入两次同一个对象只会存储它的一个副本。`NSSet` 如何确定对象之间的等效性是非常复杂的。等效性不等于同一性（identity）；它不会存储两个相同对象的副本，但也不会存储两个具有相同的对象。它通过向其中一个对象发送 `-isEqual:` 消息并将另一个对象作为参数来确定两个对象是否相等。

实现 `NSSet` 最简单的方法是将每个新对象与每个现有对象进行比较。然而，这会非常缓慢，幸运的是 `NSSet` 并不是这样工作的。相反，它使用 `-hash` 方法。每个对象都应该实现此方法并返回一个整数哈希值。如果两个对象相等，它们必须具有相同的哈希值。像 `NSSet` 这样的集合根据哈希值将对象放入桶（buckets）中。在测试一个对象是否已经在集合中时，它只需要测试具有相同哈希值的对象。因此，良好的哈希函数对于这些集合类的良好性能至关重要。幸运的是，作为此类集合中最常用的对象，`NSString` 已经有了良好的哈希实现。这种方法的一个微小问题是，对象在集合中时不能改变其哈希值。对于可变对象，在不破坏某些其他规则的情况下是不可能强制执行点的。因此，在对象存储在集合中时不要修改它们是很重要的。

另一种类型的集合是 `NSCountedSet`，它是 `NSMutableSet` 的子类，支持多次添加同一个对象。这为 `NSMutableSet` 增加了一个方法 `-countForObject:`，它返回特定对象被添加到集合的次数。

**注意：** 在 Java 和其他一些语言中，计数集合被称为 *bag*（袋）。值得注意的是，由于 `NSCountedSet` 是 `NSSet` 的子类，它的某些方法设计用于允许 `NSCountedSet` 实例替代 `NSSet` 实例。如果你对本节开始创建的任何集合发送 `-count` 消息，将得到相同的值。如果你遍历任何集合，将得到七个对象。可以通过 `-countForObject:` 消息判断一个对象是否在计数集合中出现多次。

### 创建字典

```objc
NSMutableDictionary *dict = [NSMutableDictionary dictionaryWithObjectsAndKeys:@"one","1","two","2",nil];
[dict setObject:@"three" forKey:@"3"];
```

字典（通常称为 *map* 或 *关联数组*）提供了由其他对象索引的对象集合。通常，字典通过字符串进行索引。这并不是唯一的选择，但对可以作为键的类有一些限制。字典与集合相似，相同的限制也适用。用作键的对象必须实现 `-hash` 和 `-isEqual:` 方法，在比较时返回 `YES` 并在相等时返回相同的哈希值。只要它们在集合中，哈希值就不能改变。此外，键必须实现 `NSCopying` 协议。当你向字典添加键值对时，值会被保留，但键会被复制。如果你传递的是不可变对象（如 `NSString`），则其效果与保留它相同。

### 遍历集合

```objc
NSLog(@"Objective-C 1 的方式:");
NSEnumerator *e=[a objectEnumerator];
for (id obj=[e nextObject]; nil!=obj; obj=[e nextObject])
{
    [obj print];
}

NSLog(@"快速枚举:");
for (id obj in a)
{
    [obj print];
}

NSLog(@"使用 block:");
[a enumerateObjectsUsingBlock^(id obj, NSUInteger idx, BOOL *stop)
{
    [obj print];
}];

NSLog(@"避免枚举:");
[a makeObjectsPerformSelector:@selector(print)];
```

*来自：`enum.m`*

对集合执行的最常见任务之一是遍历集合中的每个元素并进行某些处理。在 Objective-C 中有很多方法可以实现这一点。由于这是一个非常常见的任务，新的实现方法不断被添加。

对于数组，你可以从 `0` 到 `[array count]` 遍历每一个索引并发送 `-objectAtIndex:` 消息。这非常低效。传统的遍历集合的方法是使用枚举器；一个 `NSEnumerator` 子类的实例。

## 第 7 章：集合的操作

**注意：**

如果你来自 Java 语言，请在脑海中将 *iterator*（迭代器）替换为 enumerator（枚举器），你会发现你所熟悉的多数模式仍然有效。

你可以通过向集合发送 `-objectEnumerator` 消息来获取集合的枚举器。这个对象非常简单。它只响应两个消息，而你很可能只会使用其中一个：`-nextObject`。它返回集合中的下一个对象，如果你已经枚举了集合中包含的所有对象，则返回 `nil`。

在 Objective-C 2 中，Apple 引入了*快速枚举*（fast enumeration）。你可以对任何实现了 `NSFastEnumeration` 协议的集合使用它。该协议定义了一个方法，可以通过单次消息发送获取多个对象。具体数量由调用者和接收者定义。编译器分配一个缓冲区并将其指针传递给接收者。接收者随后可以将一些对象拷贝到此缓冲区中，或者如果它在内部将数据存储为 C 数组（或一组数组），则返回指向其内部存储区域的指针。

该协议中的方法被一个新的流程控制结构 `for..in` 循环使用。当你使用这种循环时，编译器将产生两个嵌套循环。在外部循环中，它将调用快速枚举方法，从集合获取接几个对象。在内部循环中，它将遍历这个 C 数组。

你可以在没有编译器支持的情况下使用快速枚举。GNUstep 中的 `GSFastEnumeration.h` 头文件提供了 `FOR_IN` 和 `END_FOR_IN` 宏，它们展开后的代码与编译器用于 `for..in` 循环的代码相同。这些宏非常复杂，因此最好不要尝试自己调用快速枚举方法。

从 OS X 10.6，Apple 引入了另一种遍历集合的新方法：使用*blocks*（块）。Blocks 是 C 语言的一种新扩展，但设计用于与 Objective-C 紧密协作。像 Objective-C 对象一样，blocks 也有一个 `isa` 指针。它指向一个实现了 `NSObject` 协议的私有类，因此可以将 blocks 存储在集合中。它们还支持使用 Objective-C 类型编码进行内省，尽管这种支持在 OS X 上尚未成为其公共接口的一部分。

绝大多数集合类现在都实现了使用 blocks 进行枚举的方法。使用这些方法可能很方便，尽管这会限制你代码的可移植性。你可以通过将 `NSEnumerationConcurrent` 作为第一个参数传递给如 `-enumerateObjectsWithOptions:usingBlock:` 这样的方法来执行并发枚举。通常只有当 block 在每个元素上的执行需要很长时间时，这种方法才可能带来性能提升。

每个集合都有不同的通过 blocks 进行枚举的方法。数组的版本接收对象的索引作为参数，字典的版本同时接收键和值，依此类推。这些方法会比其他替代方案慢一些，因为它们需要为每个对象都调用一次 block（这与调用函数的开销相同），但它们可以会更加方便。

在某些情况下，你可以完全避免枚举。例如，`NSArray` 实现了一个 `-makeObjectsPerformSelector` 方法，以及另一个接受对象作为第二个参数的版本。如果你在枚举时执行的操作只是向每个对象发送消息，你可以使用这些方法来代替创建循环。

### 在集合中查找对象

```objc
NSArray *array = [NSArray arrayWithObjects:
    @"a", @"group", @"of",
    @"string", @"objects", nil];
NSSet *set = [NSSet setWithArray: array];
NSUInteger i = [array indexOfObjectIdenticalTo: @"group"];
if (NSNotFound == i)
    i = [array indexOfObject: @"group"];
NSString *original = [set member: @"string"];
```

*来自：`getObject.m`*

`NSArray` 和 `NSSet` 都实现了 `-containsObject:` 方法，如果集合包含一个与参数相等的对象，该方法返回 `YES`。这使用了我们之前在讨论集合类时介绍过的等性概念：如果向其中一个对象发送另一个对象作为参数的 `-isEqual:` 消息并返回 `YES`，则这两个对象是相等的。

在数组中，你可能想确切知道对象所在的位置，而不仅仅是知道它是否存在。有两个方法可以告诉你这一点：`-indexOfObject:` 和 `-indexOfObjectIdenticalTo:`。后者使用指针比较来判断等性。

所有这些方法在数组中都是缓慢的。它们都需要进行线性搜索，并且大多数方法需要向每个对象发送消息。通常，你只应该在小数组或不频繁调用的代码路径中使用它们。如果你需要频繁执行这种反向映射，使用字典或类似的结构来存储这种关系会更好。

对于集合，性能情况有所不同。因为集合根据哈希值将对象存储在桶中，所以集合可以快速识别出对象是不同的。显然，因为集合是无序的，所以没有集合方法可以查找对象的索引。然而，有一个方法可以查找与参数相等的存储对象。`NSSet` 上的 `-member:` 方法返回与参数相等的存储对象。这对于确保对象的唯一性非常有用。`unique.m` 示例显示了一个从 C 字符串构造唯一对象的方法（注：原文 `unique.m` 应为 `unique.m`）。如果你传递两次相同的 C 字符串，你每次都将得到相同的实例。注意，此函数不是线程安全的。在测试字符串是否在集合中和添加新字符串之间存在潜在的竞态。该函数的线程安全版本需要你在调用 `-member:` 后获取锁，再次发送此消息，然后在添加新对象后释放锁。如果你正在创建一个新的不可变类，你可能希望在构造函数中实现类似的内容。这会用内存换取部分速度，但意味着你可以始终使用指针比较来判断等性，这在某些情况下可以是一个巨大的性能胜利。

### 集合子类



所有的标准集合都是类簇（class clusters）。这意味着为它们创建新的子类并非易事。父类是抽象的，而具体的子类是私有的（所以你不能对它们进行子类）。每个集合都说明了子类中必须实现的方法。实现此点的简单方法是通过委托：只需将与你正在子类的集合相同类型的对象作为实例变量。`typedArray.m` 示例使用了这种方法。`TypedArray` 类是 `NSMutableArray` 的子类。该类中的 `realArray` 实例变量是一个 `NSMutableArray`。它在类的指定初始化器中创建，就像任何其他创建 `NSMutableArray` 的代码一样，实际上会获得该类某一个具体子类的实例。另一个实例变量是 `Class` 类型，用于检查插入的对象的类型。

```objc
- (NSUInteger)count {
    return [realArray count];
}

- (id)objectAtIndex:(NSUInteger)anIndex {
    return [realArray objectAtIndex:anIndex];
}
```

来自：`checkedArray.m`

### 集合子类化

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

来自：`checkedArray.m`

与异构的标准数组类不同，此版本要求插入的每个对象都必须传递给初始化器的类的实例（或其子类）。如果你尝试插入其他对象，此版本将静默失败，但你可以轻松地将其修改为抛出异常。

该类中的许多方法都是简单直接的。例如，`-removeObjectAtIndex:` 方法只是向被封装的数组传递相同的消息。其他方法，例如 `-insertObject:atIndex:`，则会进行类型检查然后调用真实数组。

此示例实现了 `NSMutableArray` 中的所有七个原始方法。

```objc
- (void)insertObject:(id)anObject atIndex:(NSUInteger)anIndex
{
    if (![anObject isKindOfClass:type])
    {
        return;
    }
    [realArray insertObject:anObject atIndex:anIndex];
}

- (void)removeObjectAtIndex:(NSUInteger)idx
{
    [realArray removeObjectAtIndex:idx];
}
```

来自：`checkedArray.m`

`NSArray` 或 `NSMutableArray` 将能够正常工作。

**注意：**

在 C++ 中，原始方法将父类中的纯虚方法，编译器将阻止你直接实例化父类，或实例化任何没有实现这些方法的子类。Objective-C 中没有相应的机制。

子类化的另一个更常见原因是你想为底层表示实现一个不同的数据结构。例如，如果你打算在数组的一端插入对象，然后从另一端删除它们，你可能希望使用可调整大小的环形缓冲区（ring buffer）作为你的数组实现。

如果是此类情况，你仍然应该重写相同的方法，但这次要用你自己的存储机制的实现来替换它们。你仍然可以在任何可以使用父类的地方使用你的子类——包括将其传递给其他库——但将使用你自己的存储。

# 日期与时间

在 Objective-C 中，有两个概念包含在时间的泛畴内。一个是绝对时间，另一个是时间间隔。时间间隔很容易处理。它们是简单的标量，通常以秒为单位。`NSTimeInterval` 类型用于存储时间间隔。它通常被定义为双精度浮点值，这为大多数用例提供了足够的精度。

你会在各种框架中找到表示时间间隔的其他方法。例如 OS X 上的 QTKit，它将时间间隔存储为有理数。这允许你重复相加它们，而不会遇到由于浮点舍入误差导致的漂移，这在处理媒体时非常重要。在整部电影的长度范围内，复合浮点误差可能会导致视频和音频轨道明显不同步。

时间间隔给出两个绝对时间之间的差值。绝对时间的定义相当困难。时区甚至不同的日历都使得定义绝对时间变得相对困难。Foundation 框架中许多与日期和日期相关的代码都是为了解决这个问题设计的。

## 查找当前日期

```objc
NSDate *now = [NSDate date];
now = [NSDate dateWithTimeIntervalSince1970:time(NULL)];
```

来自：`date.m`

`NSDate` 类封装了一个绝对时间值。它以两个组件的形式存储。一个是一个定义良好的固定点：纪元（epoch date）。另一个是自该纪元以来的时间间隔。`NSDate` 支持两个标准的纪元，它们都是根据格列日历定义的。一个是 UNIX 纪元，1970 年 1 月 1 日。这个纪元是随第一批 UNIX 系统定义的，后来被纳入 ISO C 标准。C 语言的 `time()` 函数将返回自该日期以来的秒数。

另一个纪元是作为 OpenStep 规范定义的，被称为参考日期（reference date）。

如果你需要获取特定日历中日期的各个分量，你需要使用 `NSCalendar` 类。如果你想生成一个字符串值，应该使用 `NSDateFormatter`。

## 计算经过的时间

第二个和三个参数分别描述了日期和时间组件所需的详细程度。其范围可以从不显示任何内容到非常简短的数字描述，再到写出月份和日期全名的详细描述。

```objc
NSDate *start = [NSDate date];
sleep(1);
NSTimeInterval elapsed = 0 - [start timeIntervalSinceNow];
```

来自：`elapsed.m`

你可以通过向其中一个日期对象发送 `-timeIntervalSinceDate:` 消息，并将另一个对象作为参数，来获取两个日期对象之间的差异。或者，若要找到某个日期是多久之前的，你可以向它发送一个 `-timeIntervalSinceNow:` 消息。如果该日期在过去，这将得到一个负数，因此若要找出自通过 `+date` 或 `+new` 创建日期以来经过了多少时间，你应该从零中减去这个值。

这不是计算经过时间最快的方法。`gettimeofday()` 系统调用会在结构体中返回系统时间。这避免了创建对象和发送消息的开销，但工作量稍大，因为你需要自己处理该结构体。该结构体在不同的字段中存储秒和微秒，因此减法操作比仅比较两个标量值要费力。

## 从字符串解析日期

```objc
NSDate *isoDate = [NSDate dateWithString:@"1982-06-15 06:10:00 +0000"];
NSLocale *gb = [[NSLocale alloc] initWithLocaleIdentifier:@"en_GB"];
NSDateFormatter *formatter = [NSDateFormatter new];
[formatter setLocale:gb];
[formatter setDateStyle:NSDateFormatterShortStyle];
[formatter setTimeStyle:NSDateFormatterNoStyle];
NSDate *britishDate = [formatter dateFromString:@"15/06/1982"];
```

来自：`stringdate.m`

`NSDate` 类有一个构造函数，允许从 ISO 8601 格式的字符串构建日期。这在你解析用于交换的文件日期时非常有用，但在处理用户提供的数据时并不那么有用。如果你想从本地化字符串创建日期，你需要回到 `NSDateFormatter` 类。该类封装了某些日期格式的描述，并可以在日期和字符串对象之间进行双向转换。

当你创建一个日期格式化器时，可以将区域（locale）设置为显式区域，或者保持设置为用户当前的区域。然后，你可以使用该区域的标准时间和日期格式之一，或者通过 `-setDateFormat:` 方法显式指定一个。该方法接受一个模板字符串作为参数，但在大多数代码中不建议使用它，因为它没有考虑到区域设置。

读取日期的你还有一个最后的选项。如果你想从某些自定义格式读取日期，可以使用 `NSScanner` 从字符串中读取组件，然后构造一个 `NSDateComponents` 对象并将其传递给 `NSC` 以创建日期。`NSScanner` 在第 5 章中有所介绍。

## 接收定时器事件

```objc
- (void)periodic:(NSTimer *)theTimer {
    NSLog(@"Timer fired");
}

- (void)start {
    SEL sel = @selector(periodic:);
    [NSTimer scheduledTimerWithInterval:1.0
                                 target:self
                               selector:sel
                               userInfo:nil
                                repeats:YES];
    [[NSRunLoop currentLoop] run];
}
```

来自：`timer.m`

`NSTimer` 类封装了一个在特定时间产生事件的事件源。这在原理上与 `alarm()` 系统调用类似，尽管你可以同时调度多个定时器。你几乎总是使用本节开头介绍的方法来构造定时器。该方法会在同一个操作中创建并调度一个新的定时器。当时间间隔过去后，定时器将向对象发送消息。定义这种方式的最简单方法是将选择器（selector）、目标（target）和一个字典传递给定时器，它接受一个参数：一个 `NSTimer` 实例。

还有另一个接受 `NSInvocation` 作为参数的构造函数。这种方法更难使用，但更强大，因为它可以使用任何消息。当你这样创建定时器对象时，它会被自动释放（autoreleased），但会被运行循环（run loop）对象保留（retain）。你只有在使用 `NSRunLoop` 时才能使用定时器。运行循环对象等待来自内核的事件——例如，定时器或文件描述符上的数据变得可用——然后向这些事件发送消息。如果你正在使用 AppKit 或 UIKit，`NSApplication` 和 `UIApplication` 类都会在内部创建一个运行循环实例。这些类在运行循环中注册，以接收来自显示服务器的单元界面事件的通知，然后将它们传递下去。如果你在编写命令行应用程序或服务器，你仍然可以使用 `NSRunLoop`。它是 Foundation 框架的一部分，但你必须手动创建它并告诉它运行。这非常简单，并在上一个示例的 `-start` 方法的最后一行完成。

# 使用属性列表（Property Lists）

属性列表是存储结构化数据的一种。你可以在属性列表中存储两个标准集合类（数组和字典），以及大多数数据类型，如字符串、数字、日期等。属性列表旨在设计为抽象的。它们没有绑定到特定的语言或特定的表示形式。目前有三种定义的属性列表序列化格式。旧的是 OpenStep 属性列表格式。这是一种非常密集且人类可读的格式。遗憾的是，OS X 不能写入旧式的属性列表。它可以读取它们，但规范没有定义存储日期或其他少数其他东西，因此向其写入是无效的。GNUstep 扩展了 OpenStep 属性列表格式以允许存储新格式支持的内容。

带有 OS X，苹果引入了 XML 和二进制属性列表格式。XML 格式非常冗长，但优点是可以被兼容 XML 的工具解析并嵌入其他 XML 文档。二进制表示解析非常快且非常紧凑，但由于是二进制格式，人类不可读。其他语言的库可以处理属性列表。WindowMaker 中的 WINGS 库可以读写它们，NetBSD 包含的库也是如此。苹果 Core Foundation 框架及其开源 CFL 库也可以从 C 代码使用它们。

## 在属性列表中存储集合

```objc
NSArray *array = [NSArray arrayWithObjects:@"array", @"containing", @"string", @"objects", nil];
[array writeToFile:@"example.plist" atomically:NO];
NSMutableArray *cycle = [array mutableCopy];
[cycle addObject:cycle];
[cycle writeToFile:@"failure.plist" atomically:NO];
```

来自：`writeplist.m`

数组和字典类实现了 `-writeToFile:atomically:` 方法。这些可以通过属性列表格式将集合的内容写入文件。这些方法并不是魔法。只有当集合不包含无法存储在属性列表中的类型时，它们才有效。如果你传递 `YES` 作为第二个参数，该方法将确保磁盘上的表示始终是一致的。它会将属性列表写入临时文件，并在写入完成后重命名该文件。运行本节开头的代码将生成一个 `example.plist` 文件，其中包含一个数组作为根元素，并在其中四个字符串。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
<string>array</string>
<string>containing</string>
<string>string</string>
<string>objects</string>
</array>
</plist>
```

来自：`example.plist`

在当前版本的 OS X 中，这种方法将使用 XML 属性列表格式。如你所见，这非常冗长。旧的 OpenStep 属性列表格式使用括号。

## 第 9 章：使用属性列表（Property Lists）

对于数组和字符串的双引号，其大小会减小不到一半。将其转换为二进制格式可以将文件大小从 294 字节减少到 82 字节。

对于如此小的属性列表，这种空间的缩小是无关紧要的。这两种格式可能都能放入磁盘上的单个分配单元，因此它们将占据相同的磁盘空间。两者的解析时间都微乎其微。

然而，对于较大的属性列表，并非如此。例如，Safari 将你的历史记录存储在二进制属性列表中。目前，我的记录是 15MB。如果将其转换为 XML 格式，它会变成 34MB。解析开销也会增加，无论是在 CPU 时间还是内存占用方面。

遗憾的是，集合类不会以默认（XML）以外的格式写入自身的属性列表版本。相反，你必须使用 `NSPropertyListSerialization` 类，我们将在接下来的章节中介绍它。

属性列表格式都是分级化的。它们不支持写入循环数据结构。此示例中的第二个数组包含一个指向自身的指针。将此内容写入属性列表时的行为是未定义的。在 OS X 上，只有递归指针之前的元素会被存储在文件中。其之后出现的任何对象都会被忽略。

## 从属性列表中读取数据

```objectivec
NSArray *array = [NSArray arrayWithContentsOfFile:@"example.plist"];
NSData *data = [NSData dataWithContentsOfFile:@"example.plist"];
NSMutableArray *mutable = [NSPropertyListSerialization propertyListFromData:data
                                            mutabilityOption:NSPropertyListMutableContainersAndLeaves
                                                      format:NULL
                                               errorDescription:NULL];
NSAssert([mutable isKindOfClass:[NSMutableArray class]], @"Should have read a mutable array");
[[mutable objectAtIndex:0] appendString:@""suffix"];
```

来自：`readplist.m`

读取属性列表有两种方法。第一种是使用我们刚刚查看的写入方法的反向方法。支持属性列表序列化的两个集合类都有一个 `-initWithContentsOfFile:` 初始化器，以及相应的构造函数。

这听起来很容易，但存在一些复杂性。最重要的一点是属性列表不存储任何关于可变性的信息。例如，`NSString` 和 `NSMutableString` 的存储方式完全相同。

当你读回属性列表时，你应该得到哪一个？如果你通过向 `NSArray` 类发送 `+arrayWithContentsOfFile:` 消息来读回数组，你会得到一个不可变数组。如果你向 `NSMutableArray` 发送相同的消息，你将得到一个可变数组。

对于属性列表的外部元素来说这没问题，但数组内部的对象呢？在这两种情况下，你得到的都都是填充了不可变对象的数组。这可能不是你想要的。



如果你想读回可变对象，你需要使用`NSPropertyListSerialization`。该类处理属性列表的读取和写入，并提供了比各种集合类更精细粒度的控制。

**注意：**

如果你阅读 Apple 的最新版本文档，你会发现我们在`NSPropertyListSerialization`上使用的方法被标记为未来将弃用。这是因为该方法是在 Apple 开始使用`error:`参数的时期引入的，但在他们引入`NSError`类之前。遗憾的是，推荐用来替代它的方法尚未提供等等的功能。

当你使用该类读取属性列表时，可以传传递一个可变性选项作为参数。共有三个可能的选项。默认选项是所有对象都是不可变的。本章开头示例使用的选项走向了另一个极端，使所有内容都变成可变。在数组中的一个字符串后面添加后缀就演示了这一点。

第三种选项处于中间位置。它让容器对象变为可变，但其他对象（字符串、数字、日期等）保持不可变。当你只想修改属性列表的结构而不想修改任何叶元素时，这非常有用。

当你用这样读取属性列表时，属性列表序列化类会告诉你该属性列表的格式。

## 转换属性列表格式

```objectivec
NSString *file = [NSString stringWithUTF8String: argv[1]];
NSData *data = [NSData dataWithContentsOfFile:file];
NSPropertyListFormat fmt;
id plist = [NSPropertyListSerialization propertyListWithData:data
                                                         options:0
                                                            format:&fmt
                                                       errorDescription:NULL];
if (fmt == NSPropertyListBinaryFormat) {
    return 0;
}
data = [NSPropertyListSerialization dataWithPropertyList:plist
                                                   options:0
                                                     format:NSPropertyListBinaryFormat
                                               errorDescription:NULL];
[data writeToFile:file atomically:NO];
```

*自：`makebinary.m`*

在 OS X 上，你不能以 OpenStep 格式写入属性列表，但你仍然可以使用其他形式。通常，你应该对私有数据使用二进制格式，对用户可能想要编辑的内容使用 XML 格式。属性列表的意义在于你可以在不同表示之间进行转换。当然，它们随后会忘记将其转换回来，所以你的程序下次读取它们时会很慢。

如果你不是在每次程序运行时都修改属性列表，那么在加载时检查格式是否仍为二进制格式，如果不是，则以这种格式重写。

## 存储用户默认 (User Defaults)

```objectivec
NSUserDefaults *def = [NSUserDefaults standardUserDefaults];
id persistentString = [def stringForKey: @"example"];
NSLog(@"Old value: %@", persistentString);
if (argc > 1) {
    NSString *new = [NSString stringWithUTF8String:argv[1]];
    [def setObject:new forKey: @"example"];
    [def synchronize];
}
```

*自：`defaults.m`*

用户默认系统是属性列表最大的用户之一。如果你查看`~/Library/Preferences`目录，你会看到很多属性列表文件。这些文件存储了当前用户的偏好设置。在`/Library/Preferences`有对应的全局目录。每个应用程序都有自己的默认域，通常是一个反向 DNS 符号字符串（例如`com.apple.TextEdit`）。`NSUserDefaults`类可以访问该域的数据。

用户默认系统会从多种来源读取数据。最实用的之一是命令行。你可以将键值对作为命令行参数传递给任何 OS X 应用程序，这非常有用，当

## 存储用户默认值

默认系统以单个字典的形式暴露出来，并带有一些方便方法。通常情况下，你可以假装用户默认对象实际上是一个持久化的字典。

**注意：**

默认系统可以与 Windows 注册表相比，但有几点重要的区别。两者都支持多层级的键（用户、系统和网络），但默认系统向程序员隐藏了所有这些。尽管两者看起来都像树形结构，但注册表是一个单一数据库，而默认系统则将每个作用域的数据存储在独立的文件。这使得使用第三方工具修改默认值变得容易，并且意味着它的扩展性更好，因为你永远不需要一次将这些一个或两个文件读取到内存中。缺点是对默认值的操作不是事务性的。同时从两个程序修改同一个作用域是未定义的。

与字典不同，默认对象具有一些方便方法，用于访问非对象类型以及对对象类型进行类型检查。在当前的示例中，我们向它发送了一个`-stringForKey:`消息。该消息封装了`-objectForKey:`方法，但确保了返回值为字符串。

还有其他方便方法，例如`-floatForKey:`和`-setFloatForKey:`，它们接收原始 C 类型，并在存储到默认系统之前将其封装在`NSNumber`实例中。

此示例中的代码在最后向默认对象发送了一个`-synchronize`消息。这通常不是必要的。默认对象会定期与磁盘上的存储进行同步。然而，在这个示例中，我们没有使用运行循环（因此计时器将无法工作），并且在修改默认值后立即退出，因此如果没有此操作，我们的更改将永远不会提交到磁盘。

运行此示例，你可以看到初始值为`nil`，因为默认值中没有存储任何内容。作为参数传递给短时间程序的值被存储在默认值中，并在下次运行时自动检索到。

这还演示了对`NSArgumentDomain`的使用。默认值有多个来源，它们按顺序加载并覆盖之前的值。最后一个（因此优先级最高）默认值是命令行参数。指定`-example`命令行选项会将默认值中的`"example"`键设置为传递给参数的任何内容。这不会替换持久化值，它只是在程序的本次运行中覆盖了它。你可以看到，当我们再次运行程序而不带命令行参数时，将使用两次调用之前的旧值。这在第三次运行时提交到了磁盘。

1. `$ ./a.out persistent`

2. `a.out[72216:903] Old value: (nil)`

3. `$ ./a.out new`

4. `a.out[72216:903] Old value: persistent`

5. `$ ./a.out -example arg store`

6. `a.out[72362:903] Old value: arg`

7. `$ ./a.out -example arg`

8. `a.out[72363:903] Old value: arg`

9. `$ ./a.out new`

10. `a.out[72363:903] Old value: store`

11. `$ plutil -convert xml1`

12. `~/Library/Preferences/a.out.plist`

13. `$ cat ~/Library/Preferences/a.out.plist`

14. `<?xml version="1.0" encoding="UTF-8"?>`

15. `<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">`

16. `<plist version="1.0">`

17. `<dict>`

18. `<key>example</key>`

19. `<string>new</string>`

20. `</dict>`

21. `</plist>`

*来自：`defaults.m`* 程序的输出，但在第四次运行时没有被使用，因为在没有此操作的情况下，更改将不会提交到磁盘。由于没有使用运行循环（所以计时器将无法工作），并且在修改默认值后立即退出，因此我们的更改将永远不会提交到磁盘。运行此示例，你可以看到初始值为`nil`，因为默认值中没有存储任何内容。这还演示了对`NSArgumentDomain`的使用。默认值有多个来源，它们按顺序加载并覆盖之前的值。最后一个（因此优先级最高）默认值是命令行参数。指定`-example`命令行选项会将默认值中的`"example"`键设置为传递给参数的任何内容。这不会替换持久化值，它只是在程序的本次运行中覆盖了它。你可以看到，当我们再次运行程序而不带命令行参数时，将使用两次调用之前的旧值。这在第三次运行时提交到了磁盘。

# 与环境交互

Objective-C 通常用于类 Unix 平台，并从那里继承了环境的概念。这包括工作目录、环境变量等概念。在传统的 Objective-C 环境中，你被期望以与 C 程序完全相同的方式获取这些值。通过 OpenStep，Sun 和 NeXT 引入了`NSProcessInfo`类，它提供了更高层次的抽象。这种动机之一是 OpenStep 程序预计会在 OPENSTEP、Solaris 和 Windows NT 上运行。所有这些在环境方面都有细微差异，需要一些抽象来隐藏它们。

## 获取环境变量



```c
int main(int argc, char **argv, char **envp)
{
    // C 方式
    while (*envp)
    {
        printf("%s\n", *envp);
        envp++;
    }
    printf("Working Directory: %s\n", getenv("PWD"));

    // Objective-C 方式
    [NSAutleasePool new];
    NSDictionary *env = [[NSProcessInfo processInfo] environment];
    for (NSString *key in env)
    {
        NSLog("%@ = %@", key, [env objectForKey: key]);
    }
    NSLog("Working Directory: %@\n", [env objectForKey:@"PWD"]);
    return 0;
}
```

## 存储用户默认值

默认系统以单个字典的形式暴露出来，并带有一些方便方法。通常情况下，你可以假装用户默认对象实际上是一个持久化的字典。

**注意：**

默认系统可以与 Windows 注册表相比，但有几点重要的区别。两者都支持多层级的键（用户、系统和网络），但默认系统向程序员隐藏了所有这些。尽管两者看起来都像树形结构，但注册表是一个单一数据库，而默认系统则将每个作用域的数据存储在独立的文件。这使得使用第三方工具修改默认值变得容易，并且意味着它的扩展性更好，因为你永远不需要一次将一个或两个文件读取到内存中。缺点是对默认值的操作不是事务性的。同时从两个程序修改同一个作用域是未定义的。

与字典不同，默认对象具有一些方便方法，用于访问非对象类型以及对对象类型进行类型检查。在当前的示例中，我们向它发送了一个`-stringForKey:`消息。该消息封装了`-objectForKey:`方法，但确保了返回值为字符串。

还有其他方便方法，例如`-floatForKey:`和`-setFloatForKey:`，它们接收原始 C 类型，并在存储到默认系统之前将其封装在`NSNumber`实例中。

此示例中的代码在最后向默认对象发送了一个`-synchronize`消息。这通常不是必要的。默认对象会定期与磁盘上的存储进行同步。然而，在这个示例中，我们没有使用运行循环（所以计时器将无法工作），并且在修改默认值后立即退出，所以如果没有此操作，我们的更改将永远不会提交到磁盘。

运行此示例，你可以看到初始值为`nil`，因为默认值中没有存储任何内容。作为参数传递给短时间程序的值被存储在默认值中，并在下次运行时自动检索到。

这还演示了对`NSArgumentDomain`的使用。默认值有多个来源，它们按顺序加载并覆盖之前的值。最后一个（因此优先级最高）默认值是命令行参数。指定`-example`命令行选项会将默认值中的`"example"`键设置为传递给参数的任何内容。这不会替换持久化值，它只是在程序的本次运行中覆盖了它。你可以看到，当我们再次运行程序而不带命令行参数时，将使用两次调用之前的旧值。这在第三次运行时提交到了磁盘。

```
1. $ ./a.out persistent
2. a.out[72216:903] Old value: (nil)
3. $ ./a.out new
4. a.out[72216:903] Old value: persistent
5. $ ./a.out -example arg store
6. a.out[72362:903] Old value: arg
7. $ ./a.out -example arg
8. a.out[72363:903] Old value: arg
9. $ ./a.out new
10. a.out[72363:903] Old value: store
11. $ plutil -convert xml1
12. ~/Library/Preferences/a.out.plist
13. $ cat ~/Library/Preferences/a.out.plist
14. <?xml version="1.0" encoding="UTF-8"?>
15. <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
16. <plist version="1.0">
17. <dict>
18. <key>example</key>
19. <string>new</string>
20. </dict>
21. </plist>
```

*来自：`defaults.m`* 程序的输出，但在第四次运行时没有被使用，因为在没有此操作的情况下，更改将永远不会提交到磁盘。

# 与环境交互

Objective-C 通常用于类 Unix 平台，并从那里继承了环境的概念。这包括工作目录、环境变量等概念。在传统的 Objective-C 环境中，你被期望以与 C 程序完全相同的方式获取这些值。通过 OpenStep，Sun 和 NeXT 引入了`NSProcessInfo`类，它提供了更高层次的抽象。这种动机之一是 OpenStep 程序预计会在 OPENSTEP、Solaris 和 Windows NT 上运行。所有这些在环境方面都有细微差异，需要一些抽象来隐藏它们。

## 获取环境变量

```c
int main(int argc, char **argv, char **envp)
{
    // C 方式
    while (*envp)
    {
        printf("%s\n", *envp);
        envp++;
    }
    printf("Working Directory: %s\n", getenv("PWD"));

    // Objective-C 方式
    [NSAutoreleasePool new];
    NSDictionary *env = [[NSProcessInfo processInfo] environment];
    for (NSString *key in env)
    {
        NSLog("%@ = %@", key, [env objectForKey: key]);
    }
    NSLog("Working Directory: %@\n", [env objectForKey:@"PWD"]);
    return 0;
}
```

POSIX 标准并不要求第三参数即可工作，因此在可移植代码中依赖它并不是一个好主意。

当程序启动时，运行时加载器会加载所有需要的共享库，然后跳转到 C 标准库中的一个特殊函数，该函数通常称为`_start_`。然后它会调用`main()`，但在调用之前，它会存储指向环境变量的指针。

你可以通过调用`getenv()` C 标准函数来访问此存储器。或者，你也可以通过向单例进程信息对象发送`-environment`消息来访问环境变量。这会返回一个包含环境的字典。

**注意：**

没有办法使用 Objective-C 代码设置环境变量。修改环境通常是在 C 代码中完成的，并作为调用`exec()`系列函数之一的预备工作。这仅在 UNIX 类平台上有效，例如在 Windows 或 Symbian 系统上则无效。因此，不建议这样做。你可以通过向`NSTask`发送`-setEnvironment:`消息来设置一个新的字典，该字典将作为新子进程的环境。

## 解析命令行参数

```c
int main(int argc, char **argv)
{
    [NSAutoreleasePool new];
    NSUserDefaults *d = [NSUserDefaults standardUserDefaults];
    NSString *file = [d stringForKey: @"file"];
    if (nil == file)
    {
        fprintf(stderr, *"USAGE: %s -file {filename}", argv[0]);
        return 1;
    }
    NSLog(@"Using file %@", file);
    return 0;
}
```

*源自：`args.m`*

标准 C 不提供在`main()`函数之外获取程序参数的方法。GNU C 标准库提供了一些扩展，以便在程序启动后访问它们，并且在大多数 UNIX 类平台上，你可以从`/proc`文件系统读取它们，但没有一种简单的方法可以从 C 代码中以可移植的方式获取它们。

使用 Objective-C，你始终可以通过向`NSProcessInfo`发送`-arguments`消息来获取参数。这会返回一个包含所有选项 Objective-C 字符串的`NSArray`。然后你可以以你喜欢的任何方式处理这些参数。

这种访问参数的方式是非常寻常的。正如我们在上一章看到的，解析命令行参数最简单的方法是使用`NSUserDefaults`中的`NSArgumentDomain`。当一个 Objective-C 程序启动时，所有的命令行参数都会读取并插入到字典中，该字典由默认系统使用。

这使得提供一组命令行参数以及（可配置的）默认值变得非常容易。当你使用这种方法时，你永远不会直接与参数交互。相反，你向默认系统请求某个键的值，它会返回一个可能来自持久化存储位置或命令行环境的值。

在`EtoileFoundation`框架中，我们提供了一个`ETGetOptionsDictionary()`函数，它封装了标准的`getopt()`函数。这提供了一种使用 Objective-C 使用 UNIX 风格命令行参数的方法。如果你用 Objective-C 编写 UNIX 风格的工具，可以使用它。否则，最好使用默认系统。

## 用户区域

```objectivec
NSLocale *l = [NSLocale autoupdatingCurrentLocale];
NSString *language = [l objectForKey: NSLocaleIdentifier];
NSString *humanReadableLanguage = [l displayNameForKey: NSLocaleIdentifier value: language];
```

*源自：`locale.m`*

如果你的程序以任何方式与用户直接交互，你可能会在某个时刻想要对其进行本地化。Objective-C 提供了很多丰富的设施来实现这一点。

`NSLocale`对象封装了一个区域。有几种方法可以获取该类的实例。如果你向它发送`+systemLocale`消息，你将获得系统区域。然而，这通常不是你应该使用的。它是当用户区域无法正常工作时的备用区域。你可以通过两种方式获取用户的当前区域：发送`+currentLocale`消息会返回一个封装了当前区域的`locale`对象。如果用户选择了新区域，将发布`NSCurrentLocaleDidChangeNotification`，你可以为新区域获取一个新的`locale`对象。

或者，你可以向该类发送`+autoupdatingCurrentLocale`消息。这会返回一个始终代表当前区域的`locale`对象，即使发生了变化也是如此。这可能会导致稍微困惑，因为在该对象上对同一个方法的两次连续调用可能会返回不同的值。

如果你想支持在程序运行时更改区域设置，那么避免缓存从`locale`对象返回的数据是非常重要的。如果你正在显示通知并更新它们，即使你使用的是自动更新的区域对象也是如此。

## 支持突然终止

```objectivec
NSProcessInfo *p = [NSProcessInfo processInfo];
[p enableSuddenTermination];
// 执行一些事情
[p disableSuddenTermination];
// 执行不能被中断的事情
[p enableSuddenTermination];
```

*源自：`sudden.m`*

传统上，进程终止有两种选项。进程可以通过到达`main()`函数中的`return`语句来优雅地退出。或者，它也可以通过接收未处理的信号（如段错误）来突如其地退出。

在这两种情况下，内核都会回收它的所有资源，但在突然终止的情况下，这些资源中的某些可能被留在了不一致的状态。这的一个典型例子过去一直是复杂应用程序（如文字处理器）中的一个大问题。它们会打开文件进行写入，然后崩溃，导致文件处于非常难以恢复的状态。你可以通过使用 Foundation 对象的原子写入功能来避免这个问题，它会写入临时文件然后重命名，因此写入要么完全成功，要么完全失败。

从 OS X 10.6 开始，Apple 引入了突然终止机制。这种机制背后的理论是，许多程序在退出时花费大量时间运行操作系统本会回收对象的析构函数。通过突然终止，进程可以宣称它没有任何保存的数据。这样操作系统就可以自由地杀死它，而不是请求它优雅退出。这对于长时间空闲的长运行后台任务特别有用。它们通常会被内核交换到磁盘。当你要求它们优雅退出时，大量的代码和数据需要调入内存来处理退出。通过突然终止，交换文件中的页面将只需标记为可重用。

在你的应用程序中支持突然终止非常简单。你在`NSProcessInfo`上调用两个方法，分别在某些不能中断的操作的两侧调用。

**注意：**

如果你在带有`NSDocument`基础设施的项目中使用 AppKit，你什么都不需要做。当任何文档有未保存的数据时，你的应用程序将被标记为不支持突然终止。

这些方法被称为`-disableSuddenTermination`和`-enableSuddenTermination`，但名称稍微有些误导性。它们并没有实际上启用或禁用突然终止，而是修改一个计数器。当计数器达到 0 时，应用程序被标记为可杀死。计数器的初始值为 1，因此你必须显式地向进程信息对象发送`-enableSuddenTermination`消息来启用它。如果你正在创建一个应用程序，可以通过在应用程序包的属性列表文件中设置键来避免这一点。

Cocoa 应用程序与命令行工具不同，通常以包（bundle）的形式分发。这些目录被图形化文件管理器视为文件。NeXT 曾非常有效地利用这些目录在同一个应用程序中存储不同操作系统的二进制文件，这使得文件服务器可以包含一个适用于 OPENSTEP、Solaris 甚至 Windows 的应用程序。该包（bundle）包含的内容之一是一个属性列表，称为`info.plist`，它描述了关于应用程序的一些属性，例如其主类的名称、启动时加载的资源等。初始终止状态就是这些属性之一。

# 第 11 章：键值编码（Key-Value Coding）

典型程序中的大量代码都涉及到访问和修改对象的状态。

*键值编码 (KVC)* 机制旨在为设置和获取对象的属性提供一个抽象接口。它与*键值观察 (KVO)* 机制结合使用，后者提供了一种观察另一个对象特定属性变化的抽象方式。



KVC 允许你像操作字典一样与每个对象进行交互。无论属性是如何存储的，你都使用相同的机制来读取和写入属性。主要优势是它消除了大量编写自定义控制器类来将模型对象适配视图的需求。视图类通常需要从模型对象上获取和设置属性。通过 KVC，有一种通用的参数化机制可以完成操作。你只需要为视图对象提供一个键或键路径，让它自动从模型中检索数据，而无需知道模型实现的任何细节，甚至无需知道除支持 KVC 之外的接口。

### 通过键访问值

```objective-c
[object setValue:@"42" forKey:@"integer"];
int value = [[object valueForKey:@"integer"] intValue];
NSAssert(value == 42, @"Value set and retrieved");
```

*来自：kvc.m*

通过 KVC 操作的对象看起来非常像字典。`NSDictionary` 类本身符合 KVC 规范，尽管在使用它时通常不会使用 KVC 方法。与符合 KVC 规范的对象交互的两个最常用方法是 `-valueForKey:` 和 `-setValue:forKey:`。`NSDictionary` 的 `-objectForKey:` 方法在检索值方面的行为几乎相同。`NSDictionary` 的两个设置方法的工作略有不同。

你会注意到的第一点是，如果你在不可变字典上使用 `-setObject:forKey:`，你会得到编译时警告。但如果你使用 `-setValue:forKey:`，则不会。该方法由 `NSObject` 实现。当你在不可变字典上调用它时，它会在运行时失败，但在编译时没有任何提示。

另一个大区别是对 `nil` 的使用。如果你用 `-setValue:forKey:` 使用 `nil` 作为值，它将删除该键。如果你对 `-setObject:forKey:` 执行相同操作，则会抛出异常。

### 确保符合 KVC 规范

```objective-c
@interface KeyPublic : NSObject
@end

@implementation KeyPublic
@end

@interface KeyIVar : KeyPublic
{
    int integer;
}
@end

@implementation KeyIVar
@end
```

*来自：kvc.m*

当你使用 KVC 方法时，几乎总是会调用 `NSObject` 中的实现。这些实现会尝试确定如何真正访问属性。它们首先查找的地方是访问器方法（accessor methods）。按照惯例，Objective-C 类提供 `-property` 和 `-setProperty:` 方法来读取和设置“属性”。如果你的类提供了这些方法，它们将被调用。KVC 还会查找其他几个方法，包括用于布尔属性的 `-isProperty` 等。

```objective-c
@interface KeyAccessor : KeyIVar
@end

@implementation KeyAccessor
- (int)integer
{
    return integer;
}
- (void)setInteger:(int)aValue
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

*来自：kvc.m*

如果失败，该类将收到一个 `+accessInstanceVariablesDirectly` 消息。如果返回 `YES`，KVC 方法将查找与属性名称匹配的实例变量并使用它。`NSObject` 中此方法的实现确实返回 `YES`，因此只有在你想要防止 KVC 检查变量时才需要重写它。最后，如果仍然失败，KVC 代码将调用两个回退方法之一，取决于你是在设置还是获取属性。这些是 `-valueForUndefinedKey:` 和 `-setValue:forUndefinedKey:`。

```objective-c
@interface KeyFallback : KeyPublic
{
    NSMutableDictionary *dict;
}
@end

@implementation KeyFallback
- (id)valueForUndefinedKey:(NSString *)key
{
    return [dict valueForKey:key];
}
- (void)setValue:(id)aValue forUndefinedKey:(NSString *)key
{
    [dict setValue:aValue forKey:key];
}
@end
```

*来自：kvc.m*

这些方法是支持 KVC 的最后机会。如果你实现了它们，对于你不直接支持的键，你应该调用父类的实现。如果在根类上调用它，它会抛出异常。如果你使用声明属性来合成访问器方法，你将免费获得 KVC 兼容性。此示例使用了一个公共类和若干个支持该属性的私有子类。你可以交叉使用所有这些类的实例，至少在存储该键时是。更重要的是，你可以使用 `KeyIVar` 或 `KeyFallback` 进行原型设计，然后切换到其他方案。

回退方法在原型设计时特别有用。当你开始工作时，创建一个私有字典实例变量，并通过 KVC 访问对象上的所有属性。一旦你确定了类真正需要的属性，你就可以用一组访问器替换回退实现，并作为一个独立步骤，将 KVC 调用替换为直接发送。

### 键路径（Key Paths）

注意，KVC 仅访问运行时类型信息，并且所有对象类型在类型编码中都被编码为 `*`。这意味着你可以使用 KVC 将一个 `NSString` 实例设置为声明为 `NSArray` 的实例变量的值。当你尝试这样做时，KVC 不会产生任何错误，编译器也是如此。然而，接收者在下一次向字符串发送如 `-objectAtIndex` 之类的消息时，将会得到一个异常。如果你正在为对象类型编写 KVC 访问器，你可能想要添加一个断言语句来检查对象是否具有兼容的类。

202

## 第 11 章：键值编码（Key-Value Coding）

通过 KVC，你可以使用*键路径（key paths）*。这些是包含点分隔的键名的简单字符串。如果你想访问对象的属性的属性，可以通过键路径在单次操作中完成。

**注意：**

访问声明属性的点符号表示法与 KVC 表示法非常相似，两者很容易混淆。这很遗憾，因为它们之间完全没有关系。点符号表示法直接向访问器方法发送消息。而接收键路径的 KVC 方法是更高级层次的抽象。这就是为什么点符号表示法广泛不受欢迎的原因之一。

遗憾的是，这种相似性是刻意的。在公开发布之前，Apple 员工使用 KVC 术语来引用声明属性，这两者原本可能旨在有更紧密的关系。

键路径的巨大优势在于，例如，通用视图对象只需要存储一个指向模型对象的指针。它不需要指向模型内部各种组件的指针，可以通过键路径访问这些组件。

例如，如果你有一个用于显示人物信息的视图，你可以使用`father`和`mother`键路径连接家谱树中的成员。然后你可以使用`father.mother`键路径将同一个视图用于显示祖父母关系的场景中，以此类推。

### 观察键

键路径经常用于*Cocoa 绑定（bindings）*。这些是连接模型和视图的通用控制器类。

### 观察键

```objc
+ (void)observeValueForKeyPath:(NSString*)keyPath
ofObject:(id)object
change:(NSDictionary*)change
context:(void*)context
{
    NSLog(@"%@.%@ is now %@", object, keyPath,
          [change objectForKey: NSKeyValueChangeNewKey]);
}

+ (void)watchChange
{
    NSMutableDictionary *dict = [NSMutableDictionary new];
    [dict addObserver:self
             forKeyPath:@"aKey"
               options:NSKeyValueObservingOptionNew
               context:NULL];

    [dict setObject:@"set as object"
             forKey:@"aKey"];

    [dict removeObserver:self
             forKeyPath:@"aKey"];
}
```

*来源：kvo.m*

拥有统一的设置和获取键机制是有用的，但它并不特殊。KVC 的真正力量来自于 KVO（键值观察），它让你监控键的变化。绑定机制在许多情况下利用 KVC 和 KVO 消除了对控制器的需求。当视图想要修改模型时，它使用 KVC。当模型变化时，视图接收来自 KVO 的通知并更新自身以反映变化。这两种紧密相关的技术的结合，允许你在对象之间建立紧密的连接，而不会导致设计上的紧耦合。

注册为 KVO 观察者非常类似于注册接收通知（见第 16 章），但有几处不同。最重要的点之一是，KVO 通知始终发送到同一个方法。本节开头示例代码中的第一个方法展示了它应该是什么样子。

在这个示例中，它是一个类方法。大多数时候，你会使用实例方法，但重要的是记住，在 Objective-C 中类也是对象，因此你可以在任何通常使用对象的地方使用它们。这种实现非常简单；它只是记录了键的新值。第二个方法显示了如何注册通知。通知方法中的 `change` 参数是一个字典，在这个版本中，它包含了键的新值。它只包含新值，因为这是我们唯一要求的。

### 确保 KVO 兼容性

添加观察者方法中的 `options:` 参数是一个位域。你可以只请求新值、只请求旧值或两者都请求。你还可以请求变化前后的通知。

这让你能够轻松执行诸如记录对对象进行的更改等任务，这对于实现撤销（undo）支持非常有帮助。如果你的模型对象兼容 KVO，你可以获取每次变化的通知，保存旧值，然后在以后（使用 KVC）将其还原。这种实现撤销的逻辑可以与你模型对象的实现细节完全解耦。

```objc
[self setValue:@"42" forKey:@"aKey"];
self.aKey = 12;
[self willChangeValueForKey:@"aKey"];
aKey = 47;
[self didChangeValueForKey:@"aKey"];
```

*来源：kvo.m*

拥有统一的设置和获取键机制是有用的，但它并不特殊。KVC 的真正力量来自于 KVO，它让你监控键的变化。绑定机制在许多情况下利用 KVC 和 KVO 消除了对控制器的需求。当视图想要修改模型时，它使用 KVC。当模型变化时，视图接收来自 KVO 的通知并更新自身以反映变化。这两种紧密相关的技术的结合，允许你在对象之间建立紧密的连接，而不会导致设计上的紧耦合。

注册为 KVO 观察者非常类似于注册接收通知（见第 16 章），但有几处不同。最重要的点之一是，KVO 通知始终发送到同一个方法。本节开头示例代码中的第一个方法展示了它应该是什么样子。

在这个示例中，它是一个类方法。大多数时候，你会使用实例方法，但重要的是记住，在 Objective-C 中类也是对象，因此你可以在任何通常使用对象的地方使用它们。这种实现非常简单；它只是记录了键的新值。第二个方法显示了如何注册通知。通知方法中的 `change` 参数是一个字典，在这个版本中，它包含了键的新值。它只包含新值，因为这是我们唯一要求的。

### 确保 KVO 兼容性

添加观察者方法中的 `options:` 参数是一个位域。你可以只请求新值、只请求旧值或两者都请求。你还可以请求变化前后的通知。

这让你能够轻松执行诸如记录对对象进行的更改等任务，这对于实现撤销（undo）支持非常有帮助。如果你的模型对象兼容 KVO，你可以获取每次变化的通知，保存旧值，然后在以后（使用 KVC）将其还原。这种实现撤销的逻辑可以与你模型对象的实现细节完全解耦。

如果直接设置实例变量会发生什么？遗憾的是，答案很简单：什么也没有。直接设置实例变量只是内存存储。没有简单的方法自动检测内存中的单个值何时被修改。这意味着你必须用……包裹直接访问。

KVO 可能是框架中看起来像魔法的部分。值得记住，KVO 没有任何你自己的代码做不到的事情。它不依赖于任何未公开的接口、编译器修改或类似的技巧。如果你愿意，你可以在自己的代码中实现类似的功能。你可以查看 GNUstep 的实现来看看如何这样做。

在 GNUstep 和 OS X 上，KVO 机制都是使用 `isa-swizzling` 实现的。这是一种技巧，在对象创建后，将对象的 `isa` 指针切换到指向不同的类。

幸运的是，KVO 等系统作为框架一部分的目的是让你无需知道它们如何工作，除非你特别感兴趣。然而，KVO（以及其他内容）使用 `isa-swizzling` 实现有一个重要的副作用。这意味着你不应该依赖于对象的 `isa` 指针指向特定类或未被修改过。如果你想测试一个对象是否是特定类的实例，请使用 `-isMemberOfClass:` 或 `-isKind:`。向对象发送一个类消息来获取它的类，不要只检查 `isa` 指针。

### 错误处理

大多数代码都包含 bug。良好的代码意识到这一点并优雅地处理它们。真正好的代码使用形式方法来证明没有 bug，但大多数人负担不起真正好的代码。

书中的大多数示例代码假装错误从未发生过。这本书的页面很小，任何示例的适当错误处理代码都会迅速填满这些与示例要点大部分无关的内容。

大多数在运行时检测到的错误源于一个函数或方法使用无效输入调用另一个。处理这种问题的方法很大程度上取决于语言。例如，Erlang 不建议在模块级别进行防御性编程；如果你的模块处于未定义状态，你应该杀死它并创建一个新版本。在 C 中，鼓励你验证每个输入并检查每个返回值。

# 第 12 章：处理错误

在 Java 中，你可以通过使用异常来推迟错误处理。Lisp 和 Smalltalk 允许你在错误发生时检查堆栈，并动态修复产生错误输入的代码。

在这方面，Objective-C 介于 C 和 Java 之间。某些错误最好在靠近产生原因的地方进行处理，而另一些错误只能通过报告原因并退出来处理。

Objective-C 自 NeXT 时代起就有所谓的*异常（exceptions）*，但直到过去几年，它们的行为才变得像其他语言中的异常。然而，作为 C 的超集，Objective-C 支持你在 C 中找到的所有形式的错误报告。

### 异常的运行时差异

异常处理的实现相当困难。当你抛出一个异常时，你需要回溯抛出异常处与捕获处之间的每一个栈帧。实现这一点有方法。在像 Smalltalk 这样具有栈内省功能的语言中，这相对容易。异常可以查看每个栈帧并执行回溯。

在 Java 和类似的语言中，通常通过返回两个值来实现。在典型的 Java VM 中，一个寄存器被保留用于返回异常对象。在每次调用后，JVM 都会检查该寄存器是否为零，如果不是，则跳转到异常处理代码。

这在 Objective-C 中是不可能的，因为你需要能够与 C 交互操作。在抛出异常处与捕获处之间的某些栈帧可能是 C，你不能期望系统上所有的 C 代码在抛出异常时都修改为返回另一个值。



另一个选项类似于微软的`结构化异常处理（SEH）`，在进入和离开异常处理块时，会推入和弹出一个清理代码地址的链表。当抛出异常时，使用此栈来找到要运行的清理代码，并跳转到栈中的正确位置。这本可以是 Objective-C 的一个选项，但开销很大。它要求你在每次进入和退出异常处理块时运行某些代码，然后在抛出异常时再运行一些代码。

不过，C 确实包含一对调用可以让你执行类似栈回溯的操作。`setjmp()`调用存储当前的 CPU 寄存器，包括栈指针和帧指针。`longjmp()`调用重新加载它们。这样做的效果是将栈重置为调用`setjmp()`时的状态。这就是 Objective-C 异常传统的实现方式。

正如你可以想象的，这远非理想。它不支持在中间栈帧中执行清理操作。如果你的 Objective-C 代码调用了一些 C++ 代码，而 C++ 代码再次调用了 Objective-C 代码，你可以`longjmp()`跳过 C++ 代码，防止其运行析构函数。

GNU 运行时在 2004 年获得了兼容 C++ 的异常处理支持。在该模式下编译的每个函数（无论源语言是什么）都会导出一些 DWARF 调试数据，描述栈帧的布局以及如何回溯它。这通常被称为`零成本异常处理`，因为它对不使用异常处理的代码不会产生任何运行时开销。如果你在此模式下编译 C 代码，二进制文件会由于额外的回溯信息而变大一点，但除非通过 C 代码抛出异常，否则这些额外数据甚至不会被换入内存。

有了这种支持，当 Objective-C 异常穿过 C++ 栈帧时，可以在 C++ 中运行清理代码，反之亦然。你还可以在使用`__attribute__((cleanup))` GCC 扩展在 C 中注册清理代码。

Apple 在 64 位运行时时代了这一变化。这显著地改变了异常的性能特性。使用`setjmp()`/`longjmp()`异常时，进入异常处理区域开销很大（它需要保存所有寄存器），但抛出异常非常快。然而，它也不安全，因此文档建议捕获异常后通常应该终止程序。异常应被用于半优雅的异常终止，除非它们在离抛出处非常近被捕获。

使用零成本异常，进入异常处理块没有任何成本。抛出异常非常昂贵，但是安全的。这意味着你可以在代码中放置`@try`块而不会减慢任何速度，并在发生任何异常情况时抛出异常。

如果你需要与 Apple 的 32 位运行时兼容，那么避免异常仍然是一个好主意；如果你频繁使用`@try`块，它们将增加大量的开销。

**注意：**

使用旧式异常时，你必须小心地为捕获异常后需要访问的任何局部变量指定`volatile`。如果你不这样做，它们可能会被恢复到调用`setjmp()`时所持的值。

### 抛出和捕获异常

Objective-C 代码看起来非常像 Java 或 C++。有一些局限性。首先，它们只允许捕获 NSException 实例。其次，它们没有等同于`@finally`的机制（`@finally`运行清理代码后继续执行）。抛出异常的最佳方法仍然向 NSException 实例发送`-raise`消息。你也可以使用`@throw`关键字来抛出任意对象，但如果它不起作用，不要太惊讶。如果你正在使用 GNU 运行时或现代运行时，它可能会生效，但你正在做一件未经过良好测试的操作。

### 使用异常对象

NSException 类曾用于实现一个`longjmp()`缓冲区栈，并在需要时跳转到栈顶部的缓冲区。现在，回溯完全由运行时和回溯库完成，但 NSException 仍用于封装异常。

异常包含三个部分：名称（name）、原因（reason）和用户信息字典（user info dictionary）。名称是此类异常的唯一标识符。这只是一个字符串，但通常使用符号常量（例如`NSRangeException`），以便在捕获异常时对异常名称进行指针比较。描述（description）是人类可读的描述。这通常只用于调试，因此本地化并不重要。你理解发生了什么比你的用户理解发生了什么更重要。最后，用户信息字典是一个包含一些键值对的 NSDictionary。由抛出异常的代码完全决定在这里放入什么，尽管大多数异常抛出方法都会记录它们将在用户信息字典中放入的内容。你可以利用它将任意信息传递到任何捕获异常的地方。

### 使用异常对象

#### 捕获

因为它是一个字典，你可以决定稍后添加一些额外的键，而不会破坏现有代码的二进制兼容性。在这些情况下，通常会使用不可变字典——即`NSDictionary`而不是`NSMutableDictionary`——因为捕获异常的代码并不期望能够修改它。如果你要为异常附加字典，通常会使用`NSDictionary`的`+dictionaryWithValuesAndKeys:`构造器来创建一个一次性的不可变字典并抛出。

在最近的 OS X 版本中，异常对象还包含一些对调试有额外信息。向它发送`-callStackReturnAddresses`消息将给你一个包含`NSNumber`的`NSArray`，这些数字指向栈上所有函数的返回地址。这并不是特别有用，但 OS X 10.6 引入的`-callStackSymbols`方法就很有用。它能提供异常创建时栈上所有函数或方法的名称。

这种后一种方法由未处理异常的处理器使用，每当回溯异常未被捕获时，该处理器就会被调用，在程序中止前打印栈跟踪。你可能想使用`NSSetUncaughtExceptionHandler()`函数将此处理器替换为你自己的实现。如果你有一个错误报告机制，那么拥有未处理异常的后向跟踪是非常有用的。

### 使用异常管理内存

```objc
12 id pool = [NSAutoreleasePool new];
13 id array = [NSArray new];
14 @try
15 {
16 throw(array);
17 }
18 @catch (id e)
19 {
20 NSLog(@"Caught exception %@", e);
21 e = [e retain];
22 [pool drain];
23 [e autorelease];
24 pool = nil;
25 @throw;
26 }
27 @finally
28 {
29 [array release];
30 [pool drain];
```

*来自：`releaseexcept.m`*

异常处理使得内存管理变得稍微困难。如果你在方法中创建了一个新对象并在结束释放它，你必须考虑到事实：异常本质上是伪装的非局部 goto，并且突然有很多方法可以从你的方法返回。每一个函数调用或消息发送都变成了一个潜在的返回路径。你可以通过在`@try`块末尾添加一个`@finally`块来轻松地解决这个问题。此块中的代码始终会被执行，无论是通过到达结尾退出`@try`块，还是通过抛出异常退出。

**注意：** 在 Java 中，你也可以将异常作为局部 goto，通过在同一个方法中抛出异常并捕获它，向虚拟机宣告某条代码路径是非常的。这在 Objective-C 中也是可能的，但效率极低。`@throw()`语句将调用`objc_exception_throw()`函数，该函数将调用一个回溯库函数。该函数将读取栈帧的 DWARF 数据并调用 Objective-C 的个性函数（personality function）。该函数随后会读取更多 DWARF 数据，将异常的类与 catch 块的类进行比较，然后将指令指针设置为 catch 语句的地址。

在 Java 中，虚拟机将直接将此翻译为跳转到 catch 块的无条件跳转。如果你必须使用这种模式，请在 Objective-C 中使用 C`goto`语句。然而，通常最好完全避免它，并找到一个不忽略结构化编程思想的解决方案。

你在处理异常时可能遇到的另一个问题是在重新抛异常对象。异常对象通常是自动释放的（autoreleased）。这意味着，在手动内存管理下，它们会在当前自动释放池被删除时被删除。

这在大多数代码中并不是问题。你最常用的自动释放池在整个运行循环期间一直存在。然而，有时你会创建自己的自动释放池。

如果你在`@finally`块中释放了你的自动释放池（这似乎是显而易见的解决方案），你将会遇到一个问题。异常对象会在回溯你的栈帧时被删除，上一个栈帧可能会崩溃，因为它在查找异常类型时引用了一个孤立的指针。

为了避免这种情况，你需要确保在删除自动释放池之前保留（retain）异常对象，并在之后再次自动释放（autorelease）。这就是为什么抛出`NSException`对象以外的任何东西是坏主意之一。任何遵循 Apple 文档中此类建议的人，最终都将得到只能正确处理`NSException`对象的代码，并且过早破坏任何其他对象类型。

要正确实现这一点，你需要一个全捕获子句：一个带有`id`类型的`@catch`子句。这将捕获所有的 Objective-C 异常。记住，C++ 异常仍然不会在此块中被捕获，如果你在使用外部异常进行回溯，仍然需要一个`@finally`块来处理清理。你可以在`@catch`子句中将自动释放池的指针设置为`nil`，以防止它被释放两次。

### 传递错误代理

```objc
23 NSFileManager *fm = [NSFileManager defaultManager];
24 [fm copyPath: source
25 toPath: destination
26 handler: [ErrorHandler new]];
```

*来自：`errordelegate.m`*

在 Common Lisp 中，你有*可恢复*（resumable）*异常*的概念。这些与 Objective-C、Java、C++ 等中发现的回溯型异常形成对比。可恢复异常不会回溯栈；它运行异常处理代码然后继续。

在 Objective-C 中没有直接的对应物，但你可以通过通过方法传递一个*错误代理*（error delegate）来实现结果。`FileHandle`的旧版 API 就是这样工作的。它们的最后一个参数是在操作遇到问题时发送的对象。该方法返回一个`BOOL`，表示操作是否继续。

我在 LanguageKit 中使用这种模式来报告编译错误和警告。当编译器遇到错误时，它调用错误代理中的方法。该默认实现是将消息打印到控制台，但其他实现会转换语法树。如果它返回`YES`，编译器回溯并再次尝试。如果返回`NO`，编译器会抛出异常，由调用编译的代码捕获。通常，你应该在操作过程中可能遇到可以修复的问题使用这种模式。例如，你可以在加载引用其他文件时使用它。如果引用的文件之一缺失，默认选项是中止。然而，错误代理可以通过翻译或提示用户来提供新路径。

### 返回错误值

```objc
4 (-BOOL)trySomething;
5 (-id)tryToDoSomethingWithObject:(id)anObject
6 error:(NSError **)e;
```

*来自：`errorReturn.m`*

在 C 中，一种常见的模式是成功时返回零，返回非零值表示错误条件。这在 Objective-C 中不那么流行，但返回一个表示操作成功的`BOOL`值是相对常见的。大多数情况下，这是通过以某种方式变异接收者的方法来实现的。当你调用这类方法时，是为了影响对象的某种变化，而不是为了获取值，因此返回值没有被用于其他地方。这种模式的例子是`NSStream`的`-setProperty:forKey:`方法。它尝试设置流的属性，如果成功则返回`YES`。注意，这与 C 的模式相反，C 模式在失败时返回真。

### 使用 NSError

```objc
6 NSError *error = nil;
7 NSStringEncoding enc;
8 NSString *str = [NSString stringWithContentsOfFile:@"DoesNotExist"
9 usedEncoding:&enc
10 error:&error];
11 if (nil != error)
12 {
13 NSLog(@"Error: %@",
14 [error localizedDescription]);
15 }
```

*来自：`nserror.m`*

# 第 12 章：处理错误

Apple 在 OS X 10.2 中引入的几个方法接受一个`NSString**`作为参数。这被用于返回一个报告错误的第二个值。如果调用后该指针指向的变量为 nil，则表示操作成功。如果不是，它将包含一个描述错误的字符串。

这有一些显而易见的局限性。对于向用户报告字符串是可以的，但对于从错误中恢复并不特别有用。如果你想在代码中处理错误，你需要以某种方式解析字符串。

当 Apple 发布 Safari（10.2.7 版本）时，他们添加了一个新类：`NSError`。它几乎总是通过作为方法最后一个参数传递的指针返回。错误对象看起来与异常对象非常相似。它有一个名称（称为*domain*，域）和一个与之关联的字典。

与异常对象不同，字典有几个预定义的键。这些包括本地化的错误描述。你可以无需经过任何额外处理就将其展示给用户。

错误对象有时还包含一种恢复策略。*recovery attempter*（恢复尝试者）对象可以尝试自动从错误中恢复。对于某些错误，这是不可能的，但通常当你尝试执行某些可行但不安全的操作时，你会得到错误。当这种情况发生时，你应该将错误展示给用户，然后调用恢复尝试者。

### 使用 NSError

如果你用过 Common Lisp，这种模式看起来会很熟悉，它是一种即时的可重启异常形式。

# 第 13 章：访问目录和文件

如果你正在使用 AppKit，对于大多数与文件系统相关的任务，你有两个选择。Foundation 框架的`NSFileManager`类提供了许多操作文件和目录的低级方法。Application Kit 中的`NSWorkspace`类提供了更抽象的形式。

`NSWorkspace`的许多功能被委托给了*workspace process*（工作区进程）。在旧的 NeXT 系统上，这是一个单一程序，而在 OS X 上，其功能的各个部分由窗口服务器和 Finder 实现。

正因如此，当无法保证工作区进程存在时，使用高层次版本是没有意义的——例如，在可能通过远程连接运行的命令行工具中或在服务器代码中。

UIKit 框架没有`NSWorkspace`的等效物。如果你目标是 Cocoa Touch，则必须使用低级 API。

### 读取文件

```objc
NSData *copy = [NSData dataWithContentsOfFile: file];
NSData *mapped = [NSData dataWithContentsOfMappedFile: file];
NSData *read = [[NSFileHandle fileHandleForReadingAtPath: file] readDataToEndOfFile];
```

*来自：`readFile.m`*

UNIX 系统通常提供两种访问文件的方法：`read()`和`mmap()`系统调用。大多数其他系统——至少是运行在具有*内存管理单元（MMU）*硬件的系统——都有这些等效实现。前者将字节流从文件复制到缓冲区中。后者将文件数据映射到内存区域。

Foundation 提供了两个大致对应于这些操作的类。`NSData`类封装了一个包含未类型数据的内存区域。你可以通过各种选项从文件创建该类的实例。

对于小文件，你可以直接使用封装了`read()`调用并把文件数据副本读取到内存中的版本。对于较大的文件，你可能希望使用`+dataWithContentsOfMappedFile:`。

后一种方法的优势是它与操作系统的虚拟内存子系统交互得非常好。如果你耗尽了物理内存，你不需要为驱逐包含映射文件数据的页分配交换空间；你只需要丢弃它们，并在下次访问时将它们读回。

如果你在一个内存非常少且没有虚拟内存的平台上，这非常有用。例如，3GS 之前的 iPhone 只有 128MB RAM，且没有任何一个具有交换空间。如果你将一个 4MB 的文件读取到内存中，你就用完了应用程序可用的大部分空间。

相比之下，如果你创建一个代表文件的映射数据对象，系统将会在需要时以 4KB 为块读取数据，并在不再需要时将其驱逐。例如，当创建新对象时耗尽了内存，内核将从内存中驱逐映射文件以腾出空间。如果你已经读取了文件，它就无法做到这一点，因此会导致内存耗尽并杀死你的应用程序。

如果你只想读取文件的一部分，应该使用`NSFileHandle`。

UIKit 框架没有`NSWorkspace`的等效物。如果你目标是 Cocoa Touch，则必须使用低级 API。

`NSData`类封装了一个包含未类型数据的内存区域。你可以通过各种选项从文件创建该类的实例。

对于小文件，你可以直接使用封装了`read()`调用并把文件数据副本读取到内存中的版本。对于较大的文件，你可能希望使用`+dataWithContentsOfMappedFile:`。

后一种方法的优势是它与操作系统的虚拟内存子系统交互得非常好。如果你耗尽了物理内存，你不需要为驱逐包含映射文件数据的页分配交换空间；你只需要丢弃它们，并在下次访问时将它们读回。

如果你在一个内存非常少且没有虚拟内存的平台上，这非常有用。例如，3GS 之前的 iPhone 只有 128MB RAM，且没有任何一个具有交换空间。如果你将一个 4MB 的文件读取到内存中，你就用完了应用程序可用的大部分空间。

相比之下，如果你创建一个代表文件的映射数据对象，系统将会在需要时以 4KB 为块读取数据，并在不再需要时将其驱逐。例如，当创建新对象时耗尽了内存，内核将从内存中驱逐映射文件以腾出空间。如果你已经读取了文件，它就无法做到这一点，因此会导致内存耗尽并杀死你的应用程序。

如果你只想读取文件的一部分，应该使用`NSFileHandle`。

`NSData`类封装了一个包含未类型数据的内存区域。你可以通过各种选项从文件创建该类的实例。

`NSFileManager`类封装了文件系统作为一个整体并让你进行操作。

### 移动和复制文件



```objc
NSFileManager *fm = [NSFileManager new];
if (shouldMove) {
    [fm copyItemAtPath:source to:destination error:nil];
} else {
    [fm moveItemAtPath:source to:destination error:nil];
}
```

*来自：`fileCopy.m`*

`NSFileManager` 类封装了文件系统作为一个整体并让你进行操作。

### 获取文件属性

```objc
NSFileManager *fm = [NSFileManager defaultManager];
NSDictionary *attrs = [fm attributesOfItemAtPath:@"fileAttributes.m" error:NULL];
NSString *fileType = [attrs fileType];
NSNumber *creator = [attrs objectForKey:NSFileHFSCreatorCode];
```

*来自：`fileAttributes.m`*

`NSFileManager` 类封装了大多数标准的 POSIX 文件系统操作函数。在 C 语言中，你通常使用`stat()`函数来获取文件信息。该函数接受一个结构体指针作为参数，并填充该文件的相关信息。

这种做法的局限性显而易见：你无法在破坏所有使用该结构体的现有代码的情况下为其添加新字段。`NSFileManager`的版本要灵活得多。`attributesOfItemAtPath:error:`方法返回一个`NSDictionary`，向字典中添加额外条目非常简单，且不会破坏二进制兼容性。

从这个示例中你会注意到一点是，我们可以向字典发送`-fileType`消息来获取值。该方法是`NSDictionary`的一部分，返回与`NSFileType`键对应的字典条目。还有其他几个类似的字典方法。

在 OS X 上，你比其他 POSIX 平台拥有更多的文件元数据。HFS+ 为每个文件存储了创建者代码（creator code）和类型代码（type code）。这些现在不再频繁使用，但在经典的 MacOS 上，它们被用来代替文件扩展来确定打开文件的正确应用程序。

# 第 13 章：访问目录和文件

### 操作路径

```objc
NSString *home = @"~"*;
NSString *full = [home stringByExpandingTildeInPath];
NSString *users = [full stringByDeletingLastPathComponent];
NSString *file = [users stringByAppendingPathComponent: @"users"];
NSString *fileWithExtension = [file stringByAppendingPathExtension: @"db"*];
```

*来自：`path.m`*

许多 UNIX 代码通过`sscanf()`和`sprintf()`函数来操作路径。当你将代码移植到 Windows 或 Symbian 时，这会导致很多问题，例如它们的文件系统布局和路径分隔符是不同的。

OpenStep 从一开始就被设计为跨不同的操作系统家族的。`NSString`类提供了几个用于操作路径的方法。尽管这些方法操作的是字符串，但它们暴露了一个更抽象的接口。你可以添加或删除路径组件（路径中的单个条目，文件或目录）。你还可以修改文件扩展名。

在 OS X 上，像任何 UNIX 系统一样，有一个由斜杠表示根文件夹。子目录由斜杠分隔，文件扩展名由点分隔。在 Windows 上，有多个根目录，路径组件由反斜杠分隔，但文件扩展名仍由点分隔。

如果你在`NSString`上使用路径操作方法，你的代码无论文件系统约定如何都能正常工作。遗憾的是，`NSMutableString`没有相应的操作set。你可以通过使用`+pathWithComponents:`和`-pathComponents`方法来避免创建大量临时对象的开销，这两个方法分别从路径组件数组构造字符串以及创建一个路径组件数组。

在处理路径的代码中，没必要过于担心效率。文件系统上的几乎任何操作的开销都比创建几个临时对象要贵得多。

# 第 13 章：访问目录和文件

### 判断文件或目录是否存在

```objc
NSFileManager *fm = [NSFileManager defaultManager];
BOOL isDir;
if ([fm fileExistsAtPath: path isDirectory: &isDir])
{
    if (isDir)
        printf(@"Folder exists\n");
    else
        printf(@"File exists\n");
}
else
    printf(@"File does not exist\n");
```

*来自：`fileExists.m`*

确定文件是否存在的最简单方法是尝试访问它然后检查错误。这并不特别优雅，尽管这通常是安全的方法。如果你想在尝试操作之前向用户提供有关操作是否预期成功的反馈，你需要一个显式的测试。

`-fileExistsAtPath:isDirectory:`方法正是此意。该方法的命名有点误导。它测试指定路径上是否存在文件或目录，并告诉你它是否是一个目录。

第二个参数是一个指向`BOOL`的指针。如果你是从 C 或 C++ 转过来的，这看起来非常熟悉，但对于来自 Java 等语言的人来说，这可能看起来有点奇怪。C 以及扩展 Objective-C 只支持返回单个值，但此方法需要返回两个东西：东西是否存在以及它是否是目录。实现这一点几种方法。一种是定义一个枚举类型，包含不存在、文件存在和目录存在的元素。这会让所有使用该方法的代码变得更简单，因此无法立即看出为什么没有这样做。当你意识到可以传递`NULL`作为第二个参数时，答案变得明显了。如果你这样做，方法将不会费力测试该路径上的对象是否为目录。这是一个相对小的节省，因此并不清楚这是否是一个明智的设计。

**注意：**

不要使用这种机制创建临时文件。如果你这样做，在测试文件是否存在和创建文件之间存在潜在的竞态条件。请使用 C 库`mkstemp()`函数。EtoileFoundation 框架有一个该方法的封装，如果你想留在对象领域可以使用它。

# 第 13 章：访问目录和文件

### 使用包（Bundles）

```objc
NSBundle *mainBundle = [NSBundle mainBundle];
NSLog(@"%@ links against: %@", [mainBundle executablePath], [NSBundle allFrameworks]);
```

*来自：`bundles.m`*

在 Apple System 7 及更早版本中，文件系统支持两个分支：代码分支（code fork）和数据分支（data fork）。数据分支用于存储任意资源。从 Mac OS 8.1 开始，Apple 引入了 HFS+，它支持任意数量的分，使得文件在包含内容的能力上实际上等于目录。NTFS 有相同的功能。OS X 仍然支持资源分支，并在不支持它们的文件系统（如 UFS 和 FAT）上存储在隐藏文件中，但不建议这样做。将包含分支的文件拷贝到其他文件系统是一个问题。如果你用 OS X 将文件拷贝到 FAT 磁盘，然后用 Windows 从该磁盘拷贝，你将不会拷贝隐藏文件，因此分支中的数据将会丢失。

与此同时，NeXT 采取了不同的方向。如果分支让文件像目录，为什么不使用目录呢？NeSTEP 在标准 UNIX 文件系统之上提供了类似分支的功能，只是用目录代替了文件。应该被视为文件的目录被称为*包（bundles）*。

框架和应用程序。这些都包含一些可执行代码（程序或共享库）和一组资源。

具体的布局取决于系统。GNUstep 使用较旧的 NeXT 风格包布局，而 OS X 使用一个稍微简单的一个。你可以很容易地产生同时具有 GNUstep 和 Cocoa 布局的包，允许同一个`.app`包在不同系统间切换无需重新编译。

# 第 13 章：访问目录和文件

**注意：**

命令行工具通常不存储在包（bundles）中。然而，它们仍然有一个主包对象。该对象的路径包含主可执行文件的目录。

在 bundle 的资源目录中，查找具有指定扩展名的命名资源的本地化版本。

你可以在代码中使用此方法来获取存储在应用程序 bundle 或任何已加载的 bundle 中的资源文件的本地化版本。如果你的代码在一个框架（framework）中，你可能想从框架 bundle 中获取资源。这比从主 bundle 获取代码要稍微复杂一些。

`+bundleForClass:`方法将为你提供包含指定类代码的 bundle。如果你认为未来可能会将某个类移动到框架中，那么在加载资源时使用此方法是一个好主意。

### 在系统位置查找文件

```objectivec
11 NSArray *dirs =
12 NSSearchPathForDirectoriesInDomains(
13 NSDLibraryDirectory,
14 NSAllDomainsMask,
15 *YES);
```

**在系统位置查找文件**

*来自：`frameworkLoader.m`*

在 OS X 上，文件系统的布局是非常明确的。你可能可以硬编码路径并期望它们能够正常工作。如果你将代码移植到其他平台，你会发现事情会发生严重的破坏。

这是 OpenStep 程序员经常遇到的问题之一。例如，在 Solaris、OPENSTEP 和 Windows NT 之间迁移代码，需要为每个平台更改许多硬编码路径。

在 Apple 购买 NeXT 之后，他们发布了新版本的 OPENSTEP，它包含一个 MacOS 兼容层和一个名为 Rhapsody 的新用户界面。它使用了与 OPENSTEP 相同的 NeXT 文件系统层次结构，并在根目录下包含一个`/NeXT`文件夹，其中包含层次结构中非 UNIX 风格的部分。

通过 Rhapsody DR2，Apple 对目录布局进行了一些重大更改，并引入了现在 OS X 用户熟悉的布局。为了方便起，并支持 Windows 上的 YellowBox (Cocoa)（该产品很快就停产了），他们引入了`NSSearchPathForDirectoriesInDomains()`函数。

该函数返回一个用于特定用途的目录数组。当你调用此函数时，第一个参数描述你想要的目录类型。这可能是一个应用程序目录、库目录等。第二个参数是*文件系统域*（filesystem domain）。

OS X 像 OPENSTEP 一样，将文件系统层次结构划分为若干域，这些域的内容大致相同，但用途不同。这些域是有序的，因此你应该优先使用高优先级域中的文件。四个域如下：

- **User（用户）**：该域位于用户主目录下。这里的文件对用户是私有的，完全由用户控制。

- **Local（本地）**：包含机器本地文件的域。在 OS X 上，这包括`/Library`目录等，本地系统管理员可能会修改该目录。

- **Network（网络）**：在这个域中很少看到任何东西。你在独立机器或属于异构网络的机器上看不到它。它用于由网络管理员控制的目录。

- **System（系统）**：最后一个域包含系统文件。通常情况下，你不应该向该域中的任何位置写入内容，尽管你可以从中读取。你所做的任何修改可能会在用户下次更新系统时被撤销。

并不是每个域中都存在每个类型的目录。例如，系统域中没有文档目录，如果有的话将毫无意义。

最后一个参数告诉函数是否要展开路径中的波号（tildes）。你几乎总是在这里传递 **YES**。

`frameworkLoader.m`示例展示了我们在本章中过的几个内容。此示例加载了一个命名的框架。由于框架是包，你可以使用`NSBundle`来加载它们。

该示例首先获取系统中所有的 Library 目录列表。然后按顺序检查它们，以测试每个目录中是否存在名称与框架相同且具有`.framework`扩展名的目录。如果存在名称正确的内容，示例程序告诉`NSBundle`加载它。你可以使用这段代码在运行时懒加载加载框架，而不是显式地链接到它们。

或者，你可以修改它，在库目录中查找应用程序的插件目录（plugins directory），在这种情况下，你应该查找`NSApplicationSupportDirectory`。如果你将插件作为包进行构建，你将以完全相同的方式加载它们。

```objectivec
11 NSArray *dirs =
12 NSSearchPathForDirectoriesInDomains(
13 NSDLibraryDirectory,
14 NSAllDomainsMask,
15 *YES);
16 for (NSString *dir in dirs)
{
17 NSString *f = [dir stringByAppendingPathComponent:@"framework"];
18 BOOL isDir = NO;
19 if ([fm fileExistsAtPath:f isDirectory:&isDir] && isDir)
{
20 NSBundle *bundle = [NSBundle bundleWithPath:f];
21 if ([bundle load])
{
22 NSLog(@"Loaded %@", f);
23 return YES;
24 }
25 }
```

# 第 14 章：线程

原始的 NeXT 操作系统构建在 Mach 之上，正如 OS X 一样。Mach 从一开始就支持线程，是最早实现该特系统之一。最近，POSIX 线程 API 提供了一种跨平台的创建线程的方法方式。在 OS X 上，POSIX 线程实现在 Mach 之上，而 Objective-C 线程则实现在 POSIX 之上。

Objective-C 中的线程被封装在`NSThread`对象中。这些对象封装了 POSIX 线程并提供了一些便利方法。从 10.5 版本开始，有两种创建线程的方法。传统的方法类似于标准的 POSIX 线程创建方式，而另一种旨在更符合 Java 习惯。

当你创建一个 POSIX 线程时，你在新线程中调用一个带有 void 参数的函数。当你使用`NSThread`创建新线程时，你执行类似的操作，向对象发送消息并将另一个对象作为参数。更像 Java 的创建新线程的方法是继承`NSThread`并重写`main`方法。你可以创建该线程的实例并向它发送`-start`消息来启动。

```objectivec
10 (void)processInNewThread
{
11 SEL sel = @selector(process:);
12 [NSThread detachNewThreadSelector:sel target:self object:nil];
}
```

```objectivec
6 double oldPriority = [NSThread threadPriority];
7 [NSThread setThreadPriority:0];
8 [[NSThread mainThread] setThreadPriority:1];
```

当你创建一个线程时，它没有释放池（autorelease pool），因此最常见的做法是先创建一个释放池，或者为线程创建一个运行循环。在 Objective-C 中，创建线程是一个相对昂贵的操作，就像在 C 中一样。进程必须从内核为新线程的栈获取新内存，创建调度它的所有用户空间和内核数据结构，并为线程本地存储映射额外的空间。因此一旦一旦了线程，让它们运行一段时间是一个好主意。

在线程中创建一个新的运行循环是实现这一点的好方法。你可以注册定时器触发，监控文件描述符以获取新数据，并在新线程中使用事件驱动的编程风格。

`NSThread`实现了`threadPriority`和`setThreadPriority`方法，并作为类方法和实例方法存在。当发送给类时，它们

# 第 14 章：线程

控制当前线程的优先级。当发送到一个实例时，它们会控制该对象封装的线程的优先级。

线程的优先级决定了它将获得多少 CPU 时间，以及在获得 CPU 访问权限之间等待多久。

通过用于控制线程优先级的低级 POSIX API，你还可以设置调度策略。执行这些操作的函数都是 POSIX 实时扩展的一部分，这些扩展还提供了信号队列等功能。Objective-C API 目前（尚未）暴露这些功能。

使用此 API 设置的优先级是 0 到 1 之间的双精度浮点值。这些值将被缩放为调度器理解的某些整数范围，因此你应该记住，微小的差异会被舍入。

POSIX 规范为线程定义了两种*竞争*范围*（contention scopes）。线程的优先级定义了是否允许其获得 CPU 时间的基值，该值会根据它已经拥有的时间以及距离上次拥有时间经过了多长时间进行缩放。竞争范围决定了哪些线程在竞争 CPU 时间。在系统竞争范围下，线程与系统中所有其他线程竞争；在进程竞争范围下，它只与属于同一个进程的线程竞争。

OS X 仅实现了系统范围，这意味着高优先级线程将从其他进程的低优先级线程中抢夺处理器时间。如果你设置大于 0.5 的线程优先级，请记住这会对系统的其他部分产生不利影响。这仍然不会导致完全的饥饿。在 OS X 10.6 中，在纯 CPU 密集型任务中，最高线程优先级获得的 CPU 时间比最低优先级授予的略多一倍以上。大多数任务将涉及某些等待磁盘数据的时间。处于阻塞状态的线程无论其优先级如何，都不会消耗任何 CPU 时间。

OS X 上的调度策略与传统的 UNIX 模型相反，在传统模型中，只有超级用户才能提高进程的优先级。相当有趣的是，在 OS X 最新版本中，线程优先级对线程获取 CPU 时间数量的影响实际上比拥有它的线程的进程优先级的影响更大。这意味着，虽然你不能提高进程的优先级，但可以通过提高你进程中所有线程的优先级来实现相同的效果。



# 线程

控制当前线程的优先级。当发送到一个实例时，它们会控制该对象封装的线程的优先级。

线程的优先级决定了它将获得多少 CPU 时间，以及在获得 CPU 访问权限之间等待多久。

通过用于控制线程优先级的低级 POSIX API，你还可以设置调度策略。执行这些操作的函数都是 POSIX 实时扩展的一部分，这些扩展还提供了信号队列等功能。Objective-C API 目前（尚未）暴露这些功能。

使用此 API 设置的优先级是 0 到 1 之间的双精度浮点值。这些值将被缩放为调度器理解的某些整数范围，因此你应该记住，微小的差异会被舍入。

POSIX 规范为线程定义了两种竞争范围（contention scopes）。线程的优先级定义了是否允许其获得 CPU 时间的基值，该值会根据它已经拥有的时间以及距离上次拥有时间经过了多长时间进行缩放。竞争范围决定了哪些线程在竞争 CPU 时间。在系统竞争范围下，线程与系统中所有其他线程竞争；在进程竞争范围下，它只与属于同一个进程的线程竞争。

OS X 仅实现了系统范围，这意味着高优先级线程将从其他进程的低优先级线程中抢夺处理器时间。如果你设置大于 0.5 的线程优先级，请记住这会对系统的其他部分产生不利影响。这仍然不会导致完全的饥饿。在 OS X 10.6 中，在纯 CPU 密集型任务中，最高线程优先级获得的 CPU 时间比最低优先级授予的略多一倍以上。大多数任务将涉及某些等待磁盘数据的时间。处于阻塞状态的线程无论其优先级如何，都不会消耗任何 CPU 时间。

OS X 上的调度策略与传统的 UNIX 模型相反，在传统模型中，只有超级用户才能提高进程的优先级。相当有趣的是，在 OS X 最新版本中，线程优先级对线程获取 CPU 时间数量的影响实际上比拥有它的线程的进程优先级的影响更大。这意味着，虽然你不能提高进程的优先级，但你可以通过提高你进程中所有线程的优先级来实现相同的效果。

防止普通用户增加进程优先级的原始设计是为了防止一个用户获得不公平的 CPU 时间。OS X 系统倾向于单用户机器，因此这个问题并不大，但你仍然可以从同一用户拥有的更重要任务中抢夺处理器时间。例如，实时视频捕获对性能非常敏感，如果你的程序决定将其优先级调得足够高导致捕获应用程序丢帧，用户可能会非常恼怒。

设置线程优先级时要考虑他人。通常情况下，你应该只使用 0 到 0.5 之间的范围。只有在绝对没有其他选择时，才将线程设置为高于默认水平。不要仅仅因为你正在进行 CPU 密集型操作并希望它运行得快就这样做。

## 线程同步

```objc
static NSLock *lock;
static NSMutableArray *messages;

void recordLogMessage(NSString *msg)
{
    [lock lock];
    @try
    {
        [messages addObject: msg];
        NSLog(@"%@", msg);
    }
    @finally
    {
        [lock unlock];
    }
}
```

*来自：`lock.m`*

你可以通过多种方式同步两个线程。执行此类同步的类都遵循 `NSLocking` 协议。该协议定义了两个方法：`lock` 和 `-unlock`。

简单的锁类是 `NSLock`，它实现了一个互斥锁（mutex）。一次只能有一个线程锁定它，因此向它发送 `-lock` 消息会导致任何其他向同一对象发送 `-lock` 消息的线程阻塞，直到你发送了相应的 `-unlock` 消息。

这对于保护较短的临界区非常有用。对于较长的临界区，通常使用 `NSRecursiveLock`。`NSRecursiveLock` 允许同一个线程多次锁定同一个锁而不会死锁。

## 等待条件

```objc
- (void)addToQueue
{
    [condition lock];
    queueSize++;
    [condition signal];
    [condition unlock];
}

- (void)main
{
    while (1)
    {
        id pool = [NSAutoreleasePool new];

        [condition lock];

        while (queueSize == 0)
        {
            [condition wait];
        }

        queueSize--;
        [condition unlock];

        NSLog(@"Processed data from queue");
        [pool release];
    }
}
```

*来自：`condition.m`*

很多时候，你希望一个线程睡眠，并在另一个线程执行某些操作时唤醒它。POSIX 线程 API 使用条件变量（condition variables）来实现。

条件变量与互斥锁（mutex）配对使用。当你在条件变量上等待时，首先获取互斥锁，然后原子地释放它并在条件变量上睡眠。当条件变量被信号触发时，你会唤醒并原子地重新获取互斥锁。你可以将条件变量视为在线程之间传递互斥锁的一种。

OpenStep 规范包含一个封装了这种低级机制的类：`NSConditionLock`。与 POSIX 版本不同（POSIX 版本每次调用都需要与互斥锁关联），该类包含自己的互斥锁并实现了 `NSLocking` 协议。

这意味着你可以将条件锁作为锁，尽管这样做很浪费。除了锁之外，条件锁还关联了一个整数变量，表示条件。当你在条件锁上睡眠时，可以指定一个值。只有当条件锁用该值触发时，你的线程才会被唤醒。

当你等待的条件是一个整数值时，条件锁非常方便，但在其他情况下则不那么方便。通常，你希望线程在对象进入特定状态时被唤醒。使用低级 POSIX 函数来实现这非常容易，因为它们要求你自己测试条件，但使用 `NSConditionLock` 就没那么容易。

为了解决这个问题，Apple 引入了 `NSCondition` 类。它是对 POSIX 互斥锁和条件变量的简单封装。你可以锁定它，在释放锁的同时在其上睡眠，然后从另一个线程对其发送信号来唤醒它。

当在 `NSCondition` 上睡眠后唤醒时，条件对象将处于锁定状态。你必须测试你的条件，然后要么解锁条件对象，要么回去睡眠。

在几乎所有使用条件变量的场景中，都会使用相同的模式。通常，它们允许你在线程之间建立生产者—消费者关系。消费者线程需要一直睡眠，直到有数据等待它。生产者线程在有数据供其时需要唤醒消费者线程。

本节开头的示例展示了类中的两个方法。`addToQueue` 方法预计从生产者线程调用，而 `-main` 方法实现了消费者线程。

消费者线程代码展示了线程化对象的几个重要特性。它没有使用 `NSRunLoop`，而是实现了自己的运行循环（一个无限循环），并在每次迭代中显式地创建和销毁一个自动释放池。在每次迭代中，它首先锁定条件，如果没有数据在等待，则释放锁并睡眠。

生产者线程可以获取锁并触发条件。当这种情况发生时，消费者线程将在锁可用时立即准备好唤醒。生产者通过释放锁允许这一点。

消费者线程随后获取下一段要处理的数据并释放锁。在这个示例中，增加和减少共享变量被用作向共享数据结构添加某些数据的代理。

**注意：**

从条件变量唤醒线程所需的操作序列开销很大，因此如果可能应尽量避免。对于两个线程之间的通信，我通常倾向于使用无锁环形缓冲区（lockless ring buffer），它在空闲一段时间切换到锁定模式。Apple 的 Grand Central Dispatch（GCD）内部实现了这种模型，因此你可以直接使用，而无需自己编写环形缓冲区代码。

# Blocks 与 Grand Central

Objective-C 最近添加的特性之一是对 `blocks` 的支持，也称为 `closures`（闭包）。Blocks 是 Smalltalk 的一部分，但由于几个原因在 Objective-C 中被省略了。Smalltalk 将它们用于流控制，而 Objective-C 继承了 C 的流控制语句，因此不需要它们。编译器和运行时库的额外复杂性加上速度损失，意味着它们最初对 Objective-C 来说并不是高优先级。

闭包是一个可以在其他作用域内部创建的函数，并且引用该作用域内的变量。通常，一个函数可能会引用三个内容：全局变量、参数和局部变量。相比之下，block 可以在函数内部声明，甚至可以在另一个 block 内部声明。它可以引用在声明处可见的任何变量。

## 将变量绑定到 Blocks

```objc
int (^add)(int a, int b) = ^{
    return a + b;
};
```

*来自：`blockScope.m`*

你可以将函数视为 block 的一种特例。从概念上讲，函数是一个声明在全局作用域内的 block。虽然它们的实现方式略有不同，但差异很小。因此，block 最简单的情况等同于函数。它接受一些参数，产生一些输出，并且不引用自身作用域之外的任何内容。本节开头的片段展示了这种 block 的示例。该声明位于全局作用域，看起来像是一个非常冗长的函数声明。

下一种类型的 block 引用其声明处函数的内容。你可以在 `blockScope.m` 的其余部分看到这种 block。

**注意：**

尽管对程序员暴露只有一种 block 类型，但实际上有两种实现。你可以通过检查 `isa` 指针来确定是哪种类型，尽管这不受公共 API 保证且可能会发生。如果你创建的 block 没有引用参数或全局变量以外，那么它是静态分配的，每次创建它时都会获得指向同一个对象的指针。

另一个变量 `c` 是局部变量。它在 `getCounter()` 中分配在栈上。当该函数返回时，该变量被销毁。block 仍然存在，但它引用的是变量的副本。这意味着 block 内部的 `c` 始终包含 block 创建时的 `c` 值。你可以从输出看到它是工作的。每个 block 打印创建时的计数器值和当前值。

```objc
void (^getCounter())(void) {
    static int counter;
    int c = counter;

    void (*block)(void) = ^(void) {
        printf("current: %d ", counter);
        printf("old: %d\n", c);
    };

    counter++;
    return _Block_copy(block);
}

int main(void) {
    void (*block)(void) = getCounter();
    block();
    block();

    void (*block2)(void) = getCounter();
    block2();
    block2();

    block();
    block();

    return 0;
}
```

*来自：`blockScope.m`*

```text
1 current: 1 old: 0
2 current: 1 old: 0
3 current: 2 old: 1
4 current: 2 old: 1
5 current: 2 old: 0
6 current: 2 old: 0
```

*来自 `blockScope.m` 的输出*

传统的闭包引用的是闭包作用域中的真实变量，而不是副本。你可以通过使用 `__block` 修饰符声明变量来实现这种行为。其实现非常复杂。变量会从栈上移动到堆内存中一个引用计数的块中。这意味着对它的每一个引用都指向同一个变量。

`blockCapture.m` 示例演示了这一点，该函数创建了两个关联的计数器。

```c
typedef int (*counter_t)(void);

void linkedCounters(counter_t *a, counter_t *b)
{
    __block int *c = 0;

    *a = ^(void)^() { return c++; };
    *b = ^(void)^() { return ++c; };

    *a = _Block_copy()*(*a);
    *b = _Block_copy()*(*b);

    c++;
}

int main(void)
{
    counter_t pre, post;

    linkedCounters(&post, &pre);
    printf("%d %d, %d, %d\n", pre(), post(), pre(), post());

    return 0;
}
```

*来自：`blockCapture.m`*

这两个计数器都引用内存中的同一个变量：一个返回它后递增；另一个先递增后返回它。当你运行此程序时，你会发现调用其中一个 block 会影响下一次调用另一个 block 的返回值。

```text
2, 4, 4
```

*输出来自：`blockCapture.m`*



当你下次调用`linkedCounters()`函数时，你将获得一组新的`block`，它们引用一个新的计数器变量。注意`static`和`__block`存储修饰符之间的区别。它们都有相似的效果，即将变量从栈上移出并使其持续时间比函数更长，但它们的工作方式非常不同。

当你将变量声明为`static`时，对它的每一个引用都指向同一块内存。当你将变量声明为`__block`时，来自同一作用域的每个引用都指向同一块内存，但每当你进入声明该变量的作用域时，你都会获得一个新副本。

### 使用 Block 管理内存

```c
__block int counter;
int (*block)(void) = ^(void) { return counter++; };
block = [block retain];
_Block_release(block);
```

*来自：blockMemory.m*

Cocoa 的内存管理传统上使用引用计数。Block 的工作方式相同。有两个函数控制 block 的引用计数：`_Block_copy()`函数增加其引用计数，而`_Block_release()`函数减少引用计数。

第一个函数没有命名为`_Block_retain()`，是为了显式表示返回的 block 可能不是作为参数传递的那个。在某些情况下，block 可能会分配在栈上，然后在被复制时复制到堆上。

在 Objective-C 中，你也可以像对待其他对象一样向 block 的`-retain`、`-release`和`-autorelease`消息。事实上，你可以向 block 发送任何想要的消息，但它们只对少数消息有响应。如果你向 block 发送任何消息，编译器不会报错，但你会收到运行时异常。

block 引用的变量内存管理可能更难理解。`blockRetain.m`示例显示了两个都引用对象的 block。第一个获取对象指针的拷贝，第二个由于使用了`__block`存储修饰符而获取共享引用。

当你 retain 持有对象指针拷贝的 block 时，该对象也会隐式地、自动地被 retain。注意，这只发生一次。当你第二次 retain 该 block 时，并不会发生。当 block 被销毁时，对象会被 release。

```objc
id a = [@"a" mutable];
__block id b = [@"b" mutable];
unsigned long (*refCountA)() = ^() { return [a retain]; };
unsigned long (*refCountB)() = ^() { return [b retain]; };
printf("%ld %ld\n", refCountA(), refCountB());
refCountA = _Block_copy(refCountA);
refCountB = _Block_copy(refCountB);
printf("%ld %ld\n", refCountA(), refCountB());
[a release]; [b release];
printf("%ld %ld\n", [a retain], [b retain]);
```

*来自：blockRetain.m*

1

2

3

4

5

6

7

8

9

10

11*输出来自：blockRetain.m*

在这次特定的运行中，它可能会崩溃。要正确地做到这一点非常困难，因为 block 与对象不同，它们没有注册清理代码的方法。当 block 引用其他指针时这也是一个问题。即使指针没有`__block`存储修饰符，它引用的内存也不会被复制。这意味着你必须像跟踪 C 中的其他内存一样跟踪它，增加的复杂性在于包含该引用的 block 可能会持续很长时间。

### 在后台执行操作

```objc
dispatch_queue_t q = dispatch_get_global_queue(0,0);
__block int count;
dispatch_async(q, ^(void){ count++; });
sleep(1);
assert(count == 1);
```

如果你在 OS X 10.6 上使用 Cocoa 或在 FreeBSD 上使用 GNUstep，那么你可以选择使用`libdispatch`（Apple 命名为 Grand Central Dispatch）进行并发处理。该库由 Apple 编写并根据 Apache 2 许可证发布。如果你使用`libdispatch`，你不需要手动管理线程，而是管理工作队列。

### 创建自定义工作队列

```objc
dispatch_queue_t q = dispatch_queue_create("Example",0);
__block int count;
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ count++; });
dispatch_async(q, ^(void){ printf("%ld\n", count); });
```

*来自：libdispatchFIFO.m*

Grand Central 并不依赖 block，但结合 block 使用要容易得多。在最简单的情况下，你只需将 block 推入工作队列并在后台执行它们。这就是本节开头的示例所所的。它获取默认队列的句柄并将 block 推入其中。该队列将一旦有空闲的 CPU 时间就会在后台执行它。

Grand Central 默认创建三个并发队列。这些队列被注册在三个优先级级别：低、默认和高。在每个队列上并发运行任务的数量取决于系统负载和 CPU 的数量。

# 第 15 章：Blocks 与全局调度

可用的核心。你可以通过我们在上一节中看到的`dispatch_get_global_queue()`函数获取这些核心的一个句柄。

创建一个新的并发队列是没有意义的。推入并发队列的 Blocks 将按照它们推入的顺序开始执行，但可能会以任意顺序完成，并且可能有多个 Block 同时运行。

还有一个特殊的队列，它用于在主线程上运行。你可以通过`dispatch_get_main_queue()`获取它的引用。该队列在 OS X 10.6 上用于实现运行循环（run loop）。这是一个 FIFO（先进先出）队列，你可能希望创建类似的队列。FIFO 队列类似于轻量级线程。它按顺序执行，一次执行一个 Block。线程与队列之间的关系是变化的。取决于各种因素，你所有的队列最终可以在不同的线程上并发运行，或者都在在单个 OS 线程上执行。

你通过调用`dispatch_queue_create()`创建一个新的 FIFO 队列。当你有一组需要按定义顺序执行、但在很大程度上独立于程序其他部分时，这种方法非常有用。这有助于减少对显式同步的需求。

本章开始的示例向新队列推入了三个增加计数器的 Block 以及一个打印其最终值的 Block。

### 创建自定义工作队列

这些 Block 之间都是相关的；以错误的顺序执行它们是一个非常糟糕的主意。通过这种方法，它们彼此之间将以保证的顺序执行，但与程序的其他部分无关。这意味着你不需要在计数器变量周围放置任何锁，除非你计划从队列外部访问它。

# 第 16 章：通知

Objective-C 鼓励松散耦合，Foundation 框架中没有比通知机制更能体现这一点的。通知是为任意数量监听器实现回调的简单方法。你可以监听特定名称、特定对象或两者的通知。通知本身包含一个发送者、一个名称以及与之关联的字典，因此对象可以向监听通知的对象传递任意信息。

如果你使用通知，复用类将变得非常容易。你不需要要求每个想要监听你的类事件的类都实现特定的接口，你只需要发布通知即可。

```objc
- (void)notify:(NSNotification*)note
{
    NSLog(@"Received %@", note);
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

*来自：notify.m*

为了监听通知，你需要为你的线程向`NSNotificationCenter`对象注册感兴趣的通知。这是通知的路由点。当通知被发布时，它会被发送到通知中心，然后通知中心将其转发给所有感兴趣的方。大多数情况下，你将使用默认通知中心。可以为不同的用途创建不同的通知中心，但最常见的是使用标准的那个。这通过向`NSNotificationCenter`发送`+defaultCenter`消息获得。

要注册通知，你随后向中心发送`-addObserver:selector:name:object:`消息。注意此消息中的`selector`参数。单个对象可以在不同的方法上接收不同的通知。这非常有用，因为这意味着你不需要测试收到了什么种的通知，可以将不同的事件处理器整洁地分离到不同的方法中。

在注册观察者时，对象或通知名称可以为`nil`。这让你能够注册接收从特定对象发送的所有消息，或者接收特定类型的所有通知（无论其发送者是谁）。这些比任何其他东西都更有调试。例如，你可以写一个日志切面，监听特定类型的所有通知并记录发送者。

监听通知时需要记住的一点是，通知中心不会保留（retain）你的对象。如果你的对象在销毁时仍注册接收通知，那么当下次发送这些通知之一时，你的程序将会崩溃。为了避免这种情况，请确保向通知中心发送`-removeObserver:`消息。

### 发送通知

```objc
NSNotificationCenter *nc = [NSNotificationCenter defaultCenter];
[nc postNotification:@"Example" object:@"sender" userInfo:nil];
```

*来自：notify.m*

发布通知比注册监听要简单得多。发布通知的标准方法是构造一个`NSNotification`对象然后发送它。发送通知最常用的方法是`-postNotification:object:userInfo:`方法。还有一个该方法的简化版本，它省略了`userInfo`参数。注意`object`——通知的发送者——被指定为一个参数。这意味着例如，代码可以代表其他对象发送通知。

### 入队通知

在实践中，如果你使用较长的方法来队列通知，参数之一是`coalesceMask:`，它决定了如何合并通知。你可以合并相同名称的通知、相同发送者的通知或两者兼有。合并在`NSPostWhenIdle`发布样式下最有用。当你的代码很忙时，你可以多次发送相同的通知，然后当没有其他事件需要处理时，通知队列将只发布一次该通知。这对于触发低优先级计数工作的代码片段非常理想。

```objc
NSNotificationQueue *nq = [NSNotificationQueue defaultQueue];
NSNotification *note = [NSNotification initWith:@"Example" object:@"sender" userInfo:nil];
[nq enqueueNotification:note postingStyle:NSPostWhenIdle [[NSRunLoop currentLoop] run]];
```

*来自：notify.m*

在实践中，你的代码可能会产生大量的通知，或者产生一些不需要立即处理的通知。`NotificationQueue`类解决了这两个问题。通知队列既可以推迟通知的交付，也可以合并它们。与`NSNotificationCenter`不同，队列没有构造通知的便利方法，你必须自己完成。然后使用三种发布样式之一发布通知。在这个示例中，通知的交付被推迟到运行循环中没有其他事件时。定时器和文件描述符上的数据就绪具有优先级。或者，你可以在下一次运行循环迭代中或立即发布。

如果你发送大量相同类型的通知，那么缓存通知对象是一个好主意。反复将同一个对象传递给通知队列开销很小，而且它可以自动只发送一次通知。

### 在应用程序之间发送通知

```objc
[c addObserver:self
         selector:@selector(newCopyStarted:)
             name:ProcessDidStart
           object:nil
suspensionBehavior:NSNotificationSuspensionBehaviorHold];
```

*来自：distributedNotify.m*

通知提供的松散耦合是如此

## 应用间发送通知

在 Foundation 框架内进行扩展以为应用程序之间的通信提供一种（简单的）机制是非常用的。`NSDistributedNotificationCenter`类是`NSNotificationCenter`的子类，它可以向其他应用程序广播通知。这种扩展需要一些更改。普通的通知带有一个发送者（sender），该发送者是指向某个对象的指针。在具有另一个地址空间的进程中，指向对象的指针并不特别有用，因此分布式通知使用字符串作为发送者。你可以使用任何你喜欢的字符串，但通常是应用程序的名称。

通知可以关联字典（dictionaries）。在应用程序内部，这些字典可以包含任何对象，但对于广播，它们被限制为存储在属性列表（property lists）中的对象（参见第 9 章）。

**注意：**

在 OS X 上，只有一种类型的分布式通知中心，向与发送者具有相同用户 ID 的应用程序发送通知。GNUstep 提供了另外两种：一个用于与计算机上的所有应用程序通信（无论用户是谁），另一个用于在局域网内广播通知。

分布式通知的传递语义也略有不同。当你发布一个（普通）通知时，它是同步传递的。发送对象已经控制了 CPU。其方法的栈帧位于栈的顶端，它可以自由地将程序流委托给通知中心，然后由通知中心将其委托给通知监听器。

对于分布式通知，情况并非如此。你不能直接在函数的中间中断另一个进程正在执行的任何操作¹其实，你可以；信号（signals）正是那样做的，但你从信号处理程序能执行的操作是非常有限的，因此你必须等到合适的点。分布式通知通过与运行循环（run loop）交互来实现这一点。要接收分布式通知，你必须使用`NSRunLoop`。`distributedNotify.m`示例是一个简单的程序，每当它的新实例启动时都会写入日志消息。该类的`-init`方法执行了所有的实际工作。首先，它为分布式通知注册了一个观察者。该对象为`nil`，因此它将从任何发送者处接收此通知。然后它构建通知。user info 字典包含一个键值对，存储了进程 ID（PID）。

发布通知后，它启动了运行循环。程序将处于阻塞状态，直到某些运行循环事件发生。该程序中只有一个事件定义了处理程序，因此它所做的就是每当`ProcessDidStart`通知发布时，接收一个`-newCopyStarted:`消息，这只会在运行该程序的另一个副本时发生。

```objectivec
- (id)init
{
    NSDistributedNotificationCenter *c = [NSDistributedNotificationCenter defaultCenter];

    [c addObserver:self
             selector:@selector(newCopyStarted:)
                 name:ProcessDidStart
               object:nil
    suspensionBehavior:NSNotificationSuspensionBehaviorHold];

    NSProcessInfo *pinfo = [NSProcessInfo processInfo];
    NSNumber *pid = [NSNumber numberWithInt:[pinfo processIdentifier]];
    NSDictionary *userInfo = [NSDictionary dictionaryWithObject:pid
                                 forKey:@"pid"];

    [c postNotificationName:ProcessDidStart
                          object:[pinfo processName]
                       userInfo:userInfo
                         options:0];

    [[NSRunLoop currentRunLoop] run];
}
```

*来自：distributedNotify.m*

如果你编译并运行这个示例，你将发现它接收了自己的通知，因此它会 true你它已经启动。如果你运行另一个副本，你将从每个运行实例收到一条日志消息，告诉你关于新实例的信息。这是一个非常简单的示例，但很容易将分布式通知用于更复杂的事件。例如，我在 XMPKit 中使用它们，在用户更改在线状态时通知所有运行的应用程序。其他程序会监听此。

# 网络访问



编写网络感知应用程序的标准跨平台方法是 Berkeley Sockets API。它是作为开发 TCP/IP 的一部分编写的，并设计为与协议无关。大多数语言都有此 API 的实现。在 Objective-C 中，你一如既往地可以自由使用 C 版本，它提供了低级接口的所有功能。然而，大多数情况下，这花费了大量精力却收益极小。Foundation 框架提供了几个类，使得编写网络应用程序变得更加容易。使用这些抽象有时会丢失一些低级 API 的功能，但并并不多。

### 封装 C Sockets

我们在第 13 章中简要查看了 `NSFileHandle` 类，我提到过它封装了一个文件描述符（file descriptor）。socket API 也是文件描述符。你可以对 socket 进行读和写操作，使用与对任何其他文件描述符相同的相同的函数调用。你还可以使用 `NSFileHandle` 来封装 socket。这允许你使用低级 API 创建 socket，然后使用更抽象的方式与创建的 socket 交互。如果你需要使用低级 socket API 中任何未被高级 API 方便暴露的部分，这是你可以使用的唯一解决方案。在其他情况下，它仍然是最方便的。

将 socket 封装在文件描述符对象中的最大优势是，你可以轻松地与运行循环（run loop）集成。这允许你轻松编写事件驱动的 socket 代码。

**注意：**

记住 Objective-C 的目标是让 C 程序员的生活变得更轻松。不要为了使用而使用 Objective-C API；只有当它们作为你特定问题的解决方案，比 C API 更有意义时才使用它们。使用仅仅是 C API 简单微封装的 Objective-C API 会增加开销和复杂性，但不会让你的代码更易维护。巨大的优势是，你可以对 socket 使用 Objective-C 的引用计数。如果你在创建 `NSFileHandle` 时将 `YES` 作为 `closeDealloc:` 的参数，那么文件描述将在对象销毁时关闭。

如果你向你的对象发送 `-waitForDataInBackgroundNotify:`，它会被添加到运行循环轮询的文件描述列表中。在下一次运行循环迭代中，如果有数据等待，`NSFileHandle` 对象将发布一个通知。如果你为此通知注册了处理程序，那么你就可以读取新数据。

该方法的文档具有误导性。它声称该方法将创建另一个线程。实际上，在 OS X 上，运行循环使用 `kqueue()` API；GNUstep 可能会使用 `poll()` 或 `select()`；方法将另一个文件描述符添加到等待列表中。在 OS X 10.6 上，这是使用 Grand Central Dispatch 发布通知的，但核心功能是相同的。

最后一个优势是，你不再需要考虑缓冲区。当你从 socket 读取数据时，通常需要分配一个缓冲区并将指针传递给 `read()` 或 `recv()` 系统调用。使用文件描述符对象，你读取的是 `NSData` 实例。如果你编写大量字符串，可能可能考虑为 `NSFileHandle` 添加一个分类，提供 `-writeUTF8String:` 和 `-readUTF8String:` 方法，或者你的协议使用的编码的等效方法，允许直接获取和发送字符串。

### 连接服务器

```objectivec
NSInputStream *in;
NSOutputStream *out;
NSHost *host = [NSHost hostWithName:@"example.com"];
[NSStream getStreamsToHost:host
                     port:80
               inputStream:&in
             outputStream:&out];
[in open];
```

*来自：nsstream.m*

### 连接到服务器

Objective-C 提供了一组类似于 Java 的流类用于网络通信，以及底层的 UNIX 接口。遗憾的是，这些流版本并没有特别有用。它们没有提供一种简洁的方式来添加如压缩之类的过滤器，或者在连接过程中进行加密协商，而许多现代协议都需要这些功能。

然而，最令人遗憾的局限性是它们并不容易支持 SRV 记录。这些是 DNS 记录，用于发布服务到端口的映射，以及主机到 IP 地址的映射。它们被 DNS-SD 使用，但由于 IP 地址的短缺，它们在公互联网的分层 DNS 中已变得越来越常见。

如果你在 OS X 上使用 POSIX 的 `getaddrinfo()` 函数查询服务器地址，你需要提供主机名和服务名。系统随后会将这些名称映射到任何支持的协议上的网络地址和端口号。

当你构造一个 `NSStream` 时，你必须将端口号指定为整数。这意味着对于任何使用 DNS SRV 记录的服务，它都将失败。但是，如果你使用 `getaddrinfo()` 然后将生成的 socket 封装在 `NSFileHandle` 中，它就能正常工作。在 EtoileFoundation 中，我们为 `NSFileHandle` 提供了一个分类，允许你直接从主机名和协议名创建文件句柄，并封装了这一调用。

```objc
16 hints.ai_family = PF_UNSPEC;
17 hints.ai_socktype = SOCK_STREAM;
18 // 请求一个流地址。
19 error = getaddrinfo(server, service, &hints, &res0);
20 if (error) { return nil; }
21
22 int s = -1;
23 for (struct addrinfo *res = res0;
24 res != NULL && s < 0 ;
25 res = res->ai_next)
26 {
27 s = socket(res->ai_family, res->ai_socktype, res->ai_protocol);
28 // 如果 socket 失败，尝试下一个地址
29 if (s < 0) { continue; }
30
31 // 如果连接失败，尝试下一个地址
32 if (connect(s, res->ai_addr, res->ai_addrlen) < 0)
33 {
34 close(s);
35 s = -1;
36 continue;
37 }
38 }
39 freeaddrinfo(res0);
```

*来自: NSFileHandle+Socket.m*

该分类在 `NSFileHandle+Socket.m` 示例中显示。当你调用 `getaddrinfo()` 时，你以 C 字符串的形式提供服务器和服务类型，以及一组指示你想要的 socket 类型的提示。然后你将得到一个 `addrinfo` 结构体数组，其中包含构造连接 socket 所的信息。

这些结构按照解析器认为最佳的顺序排列，因此你通常依次尝试每一个，直到找到一个可用的。如果你同时拥有 IPv6 和 v4 连接，只要有 DNS 条目指向这两者，这段代码就会尝试两者。

### 在网络上共享对象

```objc
6 NSMutableDictionary *object = [NSMutableDictionary new];
7 NSConnection *conn = [NSConnection new];
8 [conn setRootObject: object];
9 if ([conn registerName: @"sharedDict"])
10 {
11 [[NSRunLoop currentRunLoop] run];
12 }
```

*来自: doPublish.m*

Objective-C 最强大且最未充分使用的部分之一是*分布式对象*distributed objects）系统。如果你向一个对象发送消息，而该对象不知道如何处理它，它将接收到 `-forwardInvocation:` 消息，其中一个对象封装消息作为参数。

就像 Objective-C 中的其他一切一样，你可以对这个对象进行内省。它会告诉你选择器（selector）、参数数量以及所有参数的类型和值。

Foundation 框架包含一个 `NSDistantObject` 类，它利用了这一点。远程对象是一个代理，将消息转发到远程对象。远程对象可能在不同的进程中，甚至在不同的计算机上。

如果你将对象作为参数传递给发送远程对象的消息，它们可能会被复制，或者在远端创建一个远程代理来回传消息。

使用分布式对象非常简单。任何使用它们的程序都有两个部分：客户端和服务器。服务器向其他进程提供对象，而客户端连接到服务器并访问它们。

默认情况下，对象仅在本地机器上共享。要跨网络共享它们，你必须在注册时使用 `use NSSocketPortNameServer`。

```objc
6 NSMutableDictionary *object = [NSMutableDictionary new];
7 NSConnection *conn = [NSConnection new];
8 [conn setRootObject: object];
9 if ([conn registerName: @"sharedDict"])
10 {
11 [[NSRunLoop currentRunLoop] run];
12 }
```

（注：上面的代码片段在 OCR 源中似乎重复或碎片化）。

（此处省略后续重复的段落，其内容与上文一致）

### 查找网络对等

多年来，许多协议被用于在本地网络上查找服务。NetBIOS 和 AppleTalk 在 90 年代中期以前在本地网络上很常见，直到它们开始被 TCP/IP 取代。TCP/IP 协议栈并不包含任何执行此操作的内容。最接近的是广播地址。IETF 的 ZeroConf 工作组提出了这一方案。

DNS 是一种可扩展的映射发布方式。它通常用于主机名到 IP 地址的映射，但也可以用于电话号码、地理位置以及许多其他。

通过 mDNS，单个计算机可以在 .local 域发布 DNS 记录。这被用作*DNS 服务发现* *(DNS-SD)* 的基础，它描述了通过 DNS 发布任意服务的方法。你也可以在传统的分层 DNS 中使用此标准，但它在 mDNS 中最有用。

这两个标准的结合通常被称为 *Bonjour*，并通过 `NSNetService` 类暴露给 Objective-C。这允许应用程序发布 DNS-SD 记录并找到特定服务的所有记录。

许多应用程序在 OS X 上使用此功能。Safari 使用它共享书签；iChat 使用它查找无服务器消息的联系人；iTunes 使用它共享音乐；系统使用它查找共享文件夹和打印机。如果你正在编写任何种网络应用程序，可能会发现使用 `NSNetService` 向对等节点发布会有帮助。

```objc
12 NSProcessInfo *pi = [NSProcessInfo processInfo];
13 NSString *name = [NSString stringWithFormat:@"%@@", [pi hostName]];
14 NSNetService *service = [[NSNetService alloc] initWithDomain:@"" 
15 type:type
16 name:name 
17 port:123];
18 [service publish];
19 NSNetServiceBrowser *sb = [NSNetServiceBrowser new];
20 [sb setDelegate:self];
21 [sb searchForOfType:type inDomain:@""];
```

*来自: netservice.m*

## 第 17 章：网络访问

对象（我们将在本章末尾查看对象），然后你可以将此作为你正在服务的对象的名称，并忽略 Bonjour 系统的 DNS 相关底层。对于其他内容，你发布的端口通常更有用，而名称将是你向用户展示的名称。

你使用 `NSNetServiceBrowser` 类来搜索对等节点（peers）。这个类的正确用法稍微有点棘手。发布服务是同步的；你向 `NSNetService` 实例发送一个 `-publish` 消息，服务就会发布。搜索是异步的，并且需要一个活跃的*run loop*（运行循环）。

当你向选择器发送搜索消息时，它会传输一个 DNS 请求。可能需要一段时间才能获得响应，而你可能不希望在搜索时停止用户的操作，因此该方法会立即返回。

当接收到响应时，该类将向其代理（delegate）发送消息，并带一个新的 `NSNetService` 实例描述它找到的每个服务器。它将继续监听，直到你向它发送一个 `-stop` 消息。

在很多情况下，你永远不会发送这条消息。你可以让浏览器在进程的生命周期内一直在后台运行，并在局域网上出现新对等节点时获取通知。然后你可以触发用户界面的更新以显示新的对等节点。这就是像 iTunes 的程序所做的，当新的共享列表在网络上出现时将其添加到库中。

### 寻找网络对等节点

# 第 18 章：Objective-C 调试

程序员分为两种：一类是总是第一次就写出完美代码的人，另一类是真实存在的。如果你属于第一类，可以跳过这一章。如果你属于第二类，那么总会有你尝试运行代码并发现它运行得并不如预期那样完美。

这是一个令人烦恼的体验，但如果你能快速修复问题，这种烦恼就会减少很多。在本章中，我们将查看一些定位 Objective-C 程序中 产生原因的技术。

### 检查对象

```objective-c
@interface DebugObject : NSObject
@end

@implementation DebugObject

- (NSString*)description
{
    return @"Not a very helpful message";
}

@end

void debug(id anObject) {}
```

*自：description.m*

在大多数时候，当你调试 Objective-C 程序时，你将使用*GNU 调试器**(GDB)*，它对 Objective-C 有一些内置支持。如果你正在使用 Xcode，那么你正在通过图形前端使用 GDB。你可以从“运行”（Run）菜单访问命令行界面。这通常很有用，因为 Xcode 仅为调试器的最常用功能提供了 GUI 界面，而不是针对所有功能。

GDB 中有两个功能使其非常适合 Objective-C。第一个是它附带了简单的 Objective-C 解析器和解释器，因此你可以在调试器中编写 Objective-C 表达式并以此方式检查变量。第二个是 `print-object` 命令。

此命令打印一个对象。它通过向对象发送 `-description` 消息来实现这一点，该消息会返回一个描述对象的 `NSString`。这意味着它只对有效对象有效。如果你尝试对过早释放或内存已损坏的对象使用此命令，调试器要么崩溃，要么会捕获到段错误信号。

```gdb
$ gdb ./a.out
(gdb) break debug
Breakpoint 1 at 0x100000e4d: file description.m, line 10.
(gdb) r
Starting program: a.out
Breakpoint 1, debug (anObject=0x100111bc0) at description.m:10
10
void debug(id anObject) {}
(gdb) print anObject
$1 = (id) 0x100111bc0
(gdb) print-object anObject
Not a very helpful message
(gdb) print-object [NSObject new]
<NSObject: 0x100111c30>
(gdb) print-object [anObject class]
DebugObject
(gdb) print-object [anObject className]
DebugObject
(gdb) print-object anObject->isa
DebugObject
```

*输出自：description.m*

该方法在 `NSObject` 中的默认实现只是打印类名和地址。其他各种标准对象以不同的方式实现了它。例如，集合类以属性列表（property list）格式打印其内容。这个示例返回了一个非常没用的信息，但在你的代码中，你应该尝试提供一些帮助的信息。

### 识别内存问题

Objective-C 中最常见的问题之一是过早释放（premature deallocation）。如果你在某处遗漏了 `-retain`，你就持有一个指针。如果它是自动释放的（autoreleased），那么这个指针在失效之前可以保持很长时间的有效。当指针失效时，你通常会在 Mac 运行时的 `objc_send` 内部或 GNU 运行时的 `objc_lookup` 内部得到崩溃。这是因为运行时尝试查找该消息，但指针现在已经无效了。

找到对象当然只是问题的一部。你还需要弄清楚它为什么被过早释放。通常，你可以通过查看相关的源文件并检查所有的 `-retain` 和 `-release` 消息来快速做到这一点。clang 的静态分析部分（希望）可以自动完成此操作。如果无效，尝试重写类的 `-retain` 和 `-release` 方法，在调试器中为它们设置断点，并查看它们到底在哪里被保留和释放的。

当设置了 `NSZombie` 环境时，对象不会被释放。相反，它们的类会被设置为 `NSZombie`，每当它接收到消息时都会记录日志。



```gdb
$ gcc -framework -g dealloc.m && ./a.out
Segmentation fault
$ gdb ./a.out
(gdb) r
Starting program: a.out
Program received signal EXC_BAD_ACCESS, not access memory.
Reason: KERN_INVALID_ADDRESS at address: 0x00007a000010
0x0007fff82961c in objc_send()
(gdb) up 6
#6
*0x000000010000eef in main () at prematuredealloc.m:9*
...
(gdb) quit
$ NSZombieEnabled=YES ./a.out
a.out*** -hash: message sent to deallocated instance
```

```objc
id pool = [NSoreleasePool new];
NSMutableString *str = [NSMutableString stringWithString:@"example"];
[pool drain];
```

输出自：`alloc.m`

### 观察异常

```objective-c
int throw(void)
{
    [NSException raise:@"ExampleException" format:@"Watch this"];
}
```

自：`throw.m`

如果你阅读 `NSException` 的文档，你会在 `-raise` 方法中看到这段：“所有其他抛出异常的方法都会调用此方法，因此如果你在调试异常，请在这里设置断点。这在 OS X 10.5 之前是正确的，在 GNUstep 上仍然如此。遗憾的是，在较版本的 OS X 上这不再成立，如果你想编写一个更改异常抛出行为的分类（category），也会更加费力。现在，各种抛出异常的

## 异常异常

OS X Foundation 直接使用 `@throw`。这是一种简单的语法糖，它调用 `objc_exception_throw()` 函数。该函数随后调用回溯库代码来运行 `@finally` 块中的所有代码，并为该异常找到正确的处理程序。

```text
1 (gdb) break [NSException raise]
2 Breakpoint 1 at 0x51eb851eb14a14
3 (gdb) r
4 Starting program: a.out
5 2010-03-11 14:52:54.519 a.out[39782:a0f] *** Terminating app due to uncaught exception ’ExampleException’, reason: ’Watch this’
6 terminate called after throwing an instance of ’NSException’
7 Program received signal SIGABRT, Aborted.
8 0x00007fff81c3afe6 in __kill ()
9 (gdb) break objc_exception_throw
10 Breakpoint 2 at 0x7fff829660da
11 (gdb) r
12 Starting program: a.out
13 Breakpoint 2, 0x7fff829660da in objc_exception_throw ()
14 (gdb) bt
15 #0 0x00007fff829660da in objc_exception_throw ()
16 #1 0x00007fff81fd0267 in +[NSException raise:format:arguments:] ()
17 #2 0x00007fff81fd01f4 in +[NSException raise:format:] ()
18 #3 0x0000000100000ea9 in throw () at throw.m:5
19 #4 0x0000000100000eca in main () at throw.m:12
```

输出自：`throw.m`

如果你在 `objc_exception_throw()` 上设置了断点，那么你将捕获所有异常，无论它们是如何抛出的。这还会捕获像 `@throw @"string"` 这样的内容，这些在 OS X 上并没有被正式支持，但仍然有效。

### 断言预期

```objective-c
@interface IgnoreAsserts : NSAssertionHandler

@end

@implementation IgnoreAsserts

- (void)handleFailureInFunction: (NSString*)functionName file: (NSString*)fileName lineNumber: (NSInteger)line description: (NSString *)format, ...

{

    NSLog(@"Ignoring assert on line %d of %@() in %@", line, functionName, fileName);

}

@end

int main(void)

{

    [NSAutoreleasePool new];

    [[[NSThread currentThread] threadDictionary] setObject: [[IgnoreAsserts new] autorelease] forKey: NSAssertionHandlerKey];

    NSCAssert(1 == 2, @"This might not be true");

    return 0;

}
```

来自：`assert.m`

在 C 代码中，标准库提供了一个 `assert()` 宏，当谓词参数评估为假时，它会记录消息并调用 `abort()`。Objective-C 版本稍微好用一些。

Foundation 提供了两个宏：`NSAssert()` 和 `NSCAssert()`。如果你在使用 C99（你应该这样做），那么这些是可变参数的；否则你需要使用变体，例如 `NSAssert1()`，它接受固定数量的参数。`NSAssert()` 引用 `self`，因此只能在 Objective-C 方法体中使用。`NSCAssert()` 可以在 C 函数中使用。与 C 变体不同，当断言为假时，它们不会中止程序。相反，它们会向每个线程的断言处理对象发送消息。该对象默认是 `NSAssertionHandler` 的实例，并且当你触发断言时，它会抛出一个 `NSInternalConsistencyException`。你可以捕获它并恢复，但大多数情况下，它会到达栈顶并导致程序中止。

你可以创建 `NSAssertionHandler` 的你自己的子类，并重写其中一个或两个断言处理方法，以实现某些其他行为。这个示例忽略了 C 函数中的断言，在遇到它们时仅记录一条消息。

```text
1 $ ./a.out
2 a.out[40031:903] Ignoring assert on line 21 of main in $@
```

输出自：`assert.m`

想要重写这一点相当不寻常，但你可能有一些正当的理由。最明显的理由之一是错误报告。当遇到断言时，意味着你的程序发生了严重的错误。你可能想要收集一些导致此情况的情况的信息并将其上传到错误跟踪系统中，而不仅仅是崩溃。

你可以通过定义 `NS_BLOCK_ASSERTS` 宏来禁用断言。这通常只在性能关键型代码中值得这样做。通常，浪费一点 CPU 时间比在未定义状态下继续运行要好。

### 记录调试消息

```objective-c
- (void)log
{

    NSLog(@"%s:%d:%s (%@) Log message", __FILE__, __LINE__, __PRETTY_FUNCTION__, self);

}
```

来自：`nslog.m`

我们已经在很多代码中使用 `NSLog()` 函数。当你在终端中运行应用程序时，传递给 `NSLog()` 的消息将发送到标准错误流。在 OS X 上，图形应用程序中的 `NSLog()` 将消息发送到系统控制台。在 Microsoft Windows 上，使用 GNUstep，它们将发送到系统事件监视器。`NSLog()` 函数写入一个格式字符串，前面带有日期、时间、进程名称和进程 ID。当你在格式字符串中放入 `%@` 时，它使用调试器的对象的字符串表示。

**注意：**

GNUstep 框架提供了一系列日志宏，`NSDebugLog()` 家族。它们封装了 `NSLog()`，但只有在设置了特定值时才会记录。

你也可以使用编译器定义的特殊宏来构造格式字符串。`__FILE__` 宏是当前文件名的 C 字符串。`__LINE__` 宏是当前行号的整数。最后，`__PRETTY_FUNCTION__` 宏展开为包含当前方法的 C 字符串。

```text
1 ./a.out
2 2010-03-11 15:57:43.200 a.out[40861:903] nslog.m:9:[log] (<0x10012b70>) Log message
```

# Objective-C Runtime（Runtime）

正如我在书开头提到的，Objective-C 的实现由两部分组成：编译器和运行时库。编译器获取源代码并将动态转换为运行时库。运行时库是用 C 编写的，这意味着是用 Objective-C 的子集编写的。运行时库的所有接口（包括编译器调用的接口）对 Objective-C 代码都是可见的。

Objective-C 中所有动态部分都由运行时库实现。最明显的例子就是消息发送。当你发送一条消息时，运行时负责决定由谁来处理。这并不是运行时库的唯一职责。它还处理该语言所有的反射功能。它跟踪所有的类和协议元数据，并将其暴露给程序员。当你使用键值编码时，你正在（间接地）使用 Objective-C 运行时函数查找接收者的方法和实例变量。

### 通过名称发送消息

```objective-c
id obj = [NSObject new];

SEL sel = NSFromString(@"release");

IMP release = [obj methodForSelector:sel];

release(obj, sel);
```

来自：`methodByName.m`

Objective-C 方法是通过间接层调用的 C 函数。具体实现在不同的运行时之间有所不同。在 NeXT 和 Apple 运行时中，简单的消息发送是通过 `objc_msgSend()` 函数实现的。不幸的是，这并不是你需要的唯一函数。该函数声明为返回 `id`，并适用于任何具有相同调用约定的类型的方法。例如，在 Darwin/x86 上，对象指针在 eax 寄存器中返回。如果你返回一个浮点值，它返回在浮点寄存器中。如果你返回一个结构体，空间

### 通过名称发送消息

因为它是在调用者中分配的，并且一个指针作为隐藏参数传递进来。

你必须记得调用 `objc_msgSend_sret()` 或 `objc_msgSend_fpret()`。这相当麻烦，因为这意味着你必须了解目标平台上的调用约定。

对于 GNU 运行时（runtimes），这要简单得多。它没有 `objc_msgSend()` 函数。相反，你调用 `objc_msg_lookup()`，然后在将返回的函数指针强制转换为正确的类型后进行调用。

实现这种操作在不同运行时之间具有可移植性的最简单方法是使用 NSObject 的 `-methodForSelector:` 方法。它返回一个指向用于实现该方法的函数的指针，然后你可以调用它。该方法接收两个隐藏参数：接收者（receiver）和选择器（selector）。

这几乎足够通过名称调用方法了。缺失的部分是某种将字符串转换为选择器的机制。`NSSelectorFromString()` 函数正是起此作用的。它接受一个 `NSString` 作为参数并返回一个选择器。然后你可以将此选择器传递给 `-methodForSelector:`，并作为返回函数的第二个参数。

### 通过名称查找类

```objective-c
Class nsview = NSClassFromString(@"NSView");

if (Nil == nsview)
{
    NSLog(@"未链接到 AppKit");
}
else
{
    id view = [nsview new];
    NSLog(@"View: %@", view);
}
```

来自：`weakClass.m`

运行时的职责之一是存储所有已加载类的表。你可以遍历此表，逐个查看每个类，或者使用它通过名称查找类。后者对于实现弱类类引用（weak class references）特别有用。现代 Apple 运行时直接支持这种功能，但由于支持尚未通过语言暴露出来，因此并不特别实用。弱类引用的核心思想是，你可以可选地使用某个类。

例如，你可能会在某个框架中编写一些使用 Foundation 类的代码，如果你链接了 AppKit，它就可以使用 AppKit 类。这样该框架就可以任何拥有 Foundation 实现的地方工作，但如果可用 AppKit 特性，它就会利用这些特性。你也可以使用这种机制来避免对第三方框架的依赖。

```text
1 $ gcc -framework Foundation -g -std=c99 weakClass.m && ./a.out
2 a.out[53194:903] 未链接到 AppKit
3 $ gcc -framework Cocoa -g -std=c99 weakClass.m && ./a.out
4 a.out[53184:903] View: <NSView: 0x1001163b0>
```

输出来自：`weakClass.m`

注意此示例链接到 Cocoa（链接了 AppKit 和 Foundation）与仅链接 Foundation 时输出的区别。如果存在 `NSView` 类，它就会创建一个实例。如果不存在，它只记录一条消息。你也可以将此用在必须与框架旧版本向后兼容的代码中。如果你使用这种机制查找新类，你会得到一个 `Nil` 值，当类不存在时可以处理该值。

### 测试对象是否理解某个方法

```objective-c
SEL sel = @selector(delegateMethod:);

if ([delegate respondsToSelector:sel])
{
    [delegate delegateMethod:self];
}
```

来自：`respondsToSelector.m`

Objective-C 代码倾向于使用非正式的协议（protocols）。这些是代理（delegate）可以可选实现的消息组。当你编写使用这些协议的代码时，需要在发送消息之前测试该类是否真的实现了该方法。

**注意：**

这并不完全正确。你可以直接在 `@try` 块中发送消息，并在它不理解该方法时捕获抛出的异常。然而，考虑到抛出异常的代价，这并不是推荐的方法。

幸运的是，这操作非常简单。NSObject 实现了一个 `-respondsToSelector:` 方法，用于测试接收者是否可以处理带有给定选择器的消息。

该方法不仅由 NSObject 实现，它还是 NSObject 协议的一部分。其他根类也会实现它。这对于消息转发（forwarding）来说非常重要。在 NSObject 中，此方法调用了 `class_respondsToSelector()` 运行时函数。在其他类中，实现方式是不同的。如果你直接使用运行时函数，你的代码将非常脆弱。

大多数时候，你想知道的是要发送消息的对象是否能处理该消息，而不是它是否有一个处理该消息的方法。在某些语言（如 C++）中这些是相同的，但在 Objective-C 中它们是不同的。

### 转发消息

当你向一个没有对应方法的对象发送消息时，对象仍有一些方法可以处理它。这些方法在 Objective-C 的发展过程中演变了很多。

在旧的 Objective-C 中，会调用对象的 `forward::` 方法。这是一个变长方法，要求接收者知道栈帧结构。NeXT 用 `-forwardInvocation:` 替换了它。该方法传递一个封装了消息的对象。`-forwardInvocation:` 机制非常灵活，但性能并不良好。创建对象和解构栈帧的开销比普通消息发送高出数百倍，这意味着你不应该在任何性能敏感的地方使用这种机制。

如果你使用这种转发机制，你必须实现 `-methodSignatureForSelector:` 方法。它返回一个代表与消息相关的调用结构的对象。`NSInvocation` 类在创建封装的消息时会使用它。

从 10.5 开始，Apple 引入了一种新的、更快的转发机制。如果你的对象实现了 `-forwardingTargetForSelector:` 方法，该方法将带有缺失方法的选择器被调用。它可以返回一个对象，然后消息将传递给该对象。

**注意：** GNU 运行时使用的双阶段消息发送机制不支持这种新机制，旧版本的 Apple 运行时也是如此。如果你使用它，最好使用 `-forwardInvocation:` 提供回退代码。如果你使用的是较新的 Apple 运行时或带有非脆弱 ABI 的 GNUstep 运行时，你将获得速度上的优势。如果不是，你的代码仍然运行，只是速度很慢。

```objective-c
@interface Facade : NSObject
{
    id delegate;
}
@end

@implementation Facade

- (id)forwardingTargetForSelector:(SEL)sel
{
    return delegate;
}
```



```objc
- (void)forwardInvocation:(NSInvocation *)anInv
{
    [delegate invoke:anInv];
}
@end
```

这让外观模式等变得非常简单。你可以快速将任何你不理解的方法交给代理。如果你在调用代理方法之前或之后需要进行额外的处理，只需实现该方法并调用代理即可。

# 第 19 章：Objective-C Runtime

## 查找类

```objc
int classCount = objc_getClassList(NULL, 0);
Class *classList = calloc(classCount, sizeof(Class));
objc_getClassList(classList, classCount);
for (int i=0 ; i<classCount ; i++)
{
    [classes addObject:NSStringFromClass(classList[i])];
}
free(classList);
[classes sortUsingSelector:@selector(compare:)];
```

*来源：`classTree.m`*

查找 Objective-C 类有两种方法。如果你知道类的名称，可以直接使用 `NSClassFromString()` 函数。该函数接受一个字符串对象作为参数，并返回该类；如果没有注册名为该字符串的类，则返回 `Nil`。

如果你不知道类的名称，那么你就需要采取不同的方法。在某些情况下，你可能想要知道某个类，但此时并不知道它的名称。例如，如果你有一个插件架构，你可能允许用户指定要加载的包（bundles），然后想要收集某个特定类的子类，或者收集所有符合给定协议的类。

**注意：**

在测试类是否符合协议（protocol conformance）时，使用运行时函数（比向类发送 `+conformsToProtocol:` 消息要好得多。许多类使用 `+initialize` 进行懒性初始化，如果你向它们发送消息，即使你并没有实际使用该类，也会导致这段代码运行。

`objc_getClassList()` 函数将给你返回一个类数组。它接受两个指针作为参数：一个是一个用于返回类的数组，另一个是缓冲区（buffer）的大小。如果你用 `NULL` 作为第一个参数调用它，它不会返回任何类，但会告诉你共有多少个类。

一旦你获取了这个数组，你就可以遍历它并检查这些类。在这个示例中，我只是将类名存储在一个数组中然后进行排序。在下一节中，你将看到如何获取类名并打印每个类的实例变量和方法。

如果你正在搜索符合特定协议的类，那么你应该使用 `class_conformsToProtocol()` 函数。这会告诉你该类是否符合指定的协议。如果符合，你就可以将其加入到已加载的插件列表中。

## 检查类

```objc
const char *name = [className UTF8String];
printf("%s\n\tIvars:\n", name);
Class cls = NSClassFromString(className);
unsigned int ivarCount;
Ivar *ivars = class_copyIvarList(cls, &ivarCount);
for (unsigned int i=0 ; i<ivarCount ; i++)
{
    printf("\t\t%s\n", ivar_getName(ivars[i]));
}
free(ivars);
unsigned int methodCount;
Method *methods = class_copyMethodList(cls, &methodCount);
printf("%s\n\tMethods:\n", name);
for (unsigned int i=0 ; i<methodCount ; i++)
{
    printf("\t\t%s\n", sel_getName(method_getName(methods[i])));
}
```

*来源：`classTree.m`*

一旦你获取了类的指针（通过枚举所有类、向对象发送 `-class` 消息或使用 `NSClassFromString()`），你就可以对它进行检查。类结构包含了大量关于 Objective-C 类的信息，所有这些信息对程序员都是可用的。

在较旧的运行时，`Class` 是 `struct objc_class` 的一个类型定义，后者定义在头文件中。在更现代的系统中，`Class` 是一个不透明类型（opaque type），你需要通过一组公共函数与其进行交互。这使得随着时间演进 ABI（二进制应用接口）变得更容易。类结构的布局可以通过修改编译器和运行时更改，而不需要修改任何其他代码。

`classTree.m` 示例打印了系统中所有类的实例变量和方法。还有更多元数据可以供访问。例如，实例变量存储了它们的类型以及距离对象起始位置的偏移量。

这些信息被用于 KVC 的实现。当你为一个键（key）设置值且 KVC 允许访问实例变量时，它会首先找到匹配的名称。然后它会将偏移量添加到对象中。最后，它会将方法指针添加到对象中。

类结构可以通过修改编译器和运行时更改，而不需要修改任何其他代码。`classTree.m` 示例打印了系统中所有类的实例变量和方法。还有更多元数据可以供访问。例如，实例变量存储了它们的类型以及距离对象起始位置的偏移量。

这些信息被用于 KVC 的实现。当你为一个键（key）设置值且 KVC 允许访问实例变量时，它会首先找到匹配的名称。然后它会将偏移量添加到对象中。最后，它会将方法指针添加到对象中。

在较新的运行时，还有关于声明属性（declared properties）的元数据。关于类的任何信息都可以通过调用运行时函数进行检查。

## 创建类

```objc
#include <objc/runtime.h>

void makeIndestruct(id obj) {
    Class new = objc_allocateClassPair([obj class], "Fake", 0);
    addMethod(new, @selector(dealloc), (id)(imp),0);
    objc_registerClass(new);
    obj->isa = new;
}
```

*来源：`newClass.m`*

在运行时创建类是非常罕见的，但它确实为动态行为提供了许多机会。运行时创建类最重要的一点是，编译器生成的任何都不是魔法。创建一个新类涉及三个步骤：首先分配类对（class pair），然后添加方法、实例变量和协议，最后注册类对。

**注意：**

当分配类对时，你必须提供父类、新类的名称以及在类结构末尾添加的空间大小。新类的名称必须是唯一的。如果调用两次本节的示例代码将无法工作。绕过此问题的简单方法是在静态变量中保持一个计数器，每次创建新类时原子地递增它，并将其附加到类名字符串。

类对（class pair）这个术语可能令人困惑。源代码中的每个 Objective-C 类在运行时都被编译为两个类。对象是类的实例，类是元类的实例。实例方法附加到类，类方法附加到元类。当你向类发送消息时，使用元类来查找对应的方法。

类末尾的额外空间在将类创建与 `isa` 交换（isa-swizzling）结合时非常有用。更改现有类的 `isa` 指针可以让你添加方法，但不能添加实例变量。然而，你可以在类结构的末尾创建一些空间，并在那里存储额外数据。用类作为参数调用 `object_getIndexedIvars()` 将给你该数据起始位置的地址。

你可以利用此功能实现其他对象模型。例如，我曾用它为 Objective-C 添加了基于原型的面向对象功能，允许闭包作为方法并添加到单个对象中。

# 索引

## A

- 抽象基类, 94
- 关联数组, 143
- 自动装箱, 200
- 自动释放池, 65

## B

- 容器 (bag), 142
- 块 (blocks), 56, 147, 259
- Bonjour, 293
- 装箱, 101
- 束 (bundles), 239

## C

- C 语言整数, 100
- 标准本地区域设置, 109, 118
- 类别 (category), 35, 183
- CF, 见 Core Foundation
- Clang, 13
- 类簇 (class cluster), 93, 101, 119, 136, 138, 152
- 类扩展, 37
- 类版本, 82
- 闭包 (closures), 56, 259
- Cocoa 绑定, 203
- 条件变量, 255
- 竞争范围, 248
- Core Foundation, 114

## D

- 声明属性, 39
- 默认域, 178
- 委托模式, 63, 90
- 指定初始化器, 84
- 分布式对象, 289
- DNS 服务发现, 293
- DNS-SD, 见 DNS 服务发现

## E

- 错误代理, 221
- 错误域, 224
- 错误恢复尝试者, 224
- 事件驱动编程, 97
- 异常, 210

## F

- 快速枚举, 120, 146
- 外观模式 (façade pattern), 91
- 文件系统域, 242
- 格式化字符串, 130
- 转发, 316

## G

- 垃圾回收, 12
- GCC, 见 GNU Compiler
- 集合 (Collection)
- GDB, 见 GNU debugger
- gdb, 见 GNU debugger
- GNU 编译器集合, 10
- GNU 调试器, 131, 298
- GNUstep runtime, 13, 89, 317
- `gnustep-config` 工具, 15
- Grand Central Dispatch, 286

## I

- ILP32, 100
- IMP 类型, 22
- 非正式协议, 313
- 实例方法指针
- 实例变量, 19
- 内生类型, 99
- `isa` 动态替换 (isa-swizzling), 206, 324
- 迭代器, 146
- ivars, 见 实例变量

## K

- 键路径 (key paths), 202
- 键值编码 (key-value coding), 144, 195
- 键值观测 (key-value observing), 195
- KVC, 见 键值编码
- KVO, 见 键值观测

## L

- libdispatch, 267
- libobjc2, 见 GNUstep runtime
- LLVM, 见 Low Level Virtual Machine
- 低级虚拟虚拟机, 13
- LP64, 100

## M

- 映射 (map), 143
- mDNS, 见 多播 DNS
- 内存管理单元, 228
- 消息转发, 316
- 元类 (metaclass), 323
- MMU, 见 内存管理单元
- 多播 DNS, 293
- 可变子类模式, 21, 136
- 互斥锁 (mutex), 见 互斥锁
- 互斥锁, 251

## N

- 非原子 (nonatomic), 41
- 通知, 273
- `NSApplication` 类, 167
- `NSArchiver` 类, 81
- `NSArray` 类, 20, 137
- `NSAssert()` 宏, 305
- `NSAssertionHandler` 类, 305
- `NSAttributedString` 类, 134
- `NSAutoreleasePool` 类, 65, 131
- `NSBundle` 类, 239, 243
- `NSC` 类, 161, 166
- `NSCert()` 宏, 305
- `NSCharacterSet` 类, 111, 125
- `NSCoder` 协议, 81, 183
- `NSConditionLock`, 256
- `NSCCopying` 协议, 79, 143
- `NSCountedSet` 类, 142, 228
- `NSData` 类, 124, 228
- `NSDate` 类, 158, 162, 166
- `NSDateFormatter`, 161, 165
- `NSDecimal` 类型, 106
- `NSNumber` 类, 106
- `NSDictionary` 类, 196, 217, 233
- `NSDObject` 类, 290
- `NSNotificationCenter` 类, 279
- `NSDocument` 类, 193
- `NSError` 类, 174, 224
- `NSException` 类, 214, 302
- `NSFastEnumeration` 协议, 146
- `NSFileHandle` 类, 97, 221, 229, 284
- `FileManager` 类, 227, 230, 233
- `NSFont` 类, 134
- `NSIndexSet` 类, 139
- `NSInteger` 类型, 100
- `NSInvocation` 类, 45, 167, 291, 317
- `NSLocale` 类, 190
- `NSLog()` 函数, 132, 306
- `NSMutableArray` 类, 19, 137
- `NSMutableCopying` 协议, 129, 136
- `NSMutableString` 类, 128
- `NSNetService`, 293
- `NSNetServiceBrowser` 类, 294
- `NSNotification` 类, 276
- `NSNotificationQueue` 类, 277
- `NSNull` 类, 138
- `NSNumber` 类, 94, 102, 200
- `NSObject` 类, 20, 30, 34, 84, 131, 197
- `NSObject` 调试支持, 299
- `NSObject` 协议, 314
- `NSProcessInfo` 类, 185
- `NSPropertyListSerialization` 类, 172, 174, 177
- `NSProxy` 类, 30
- `NSRecursiveLock` 类, 251
- `NSRunLoop` 类, 65, 167, 180, 294
- `NSScanner` 类, 110, 166
- `NSSet` 类, 141
- `NSStream` 类, 223, 287
- `NSString` 类, 119, 142, 234
- `NSTask` 类, 187
- `NSThread` 类, 246
- `NSTimeInterval` 类型, 157
- `NSTimer` 类, 97, 166
- `NSUserDefaults` 类, 178, 189
- `NSValue` 类, 101
- `NSView` 类, 91
- `NSWorkspace` 类, 227
- `NSZombie` 类, 300
- `NSZone` 类型, 76

## O

- Objective-C 库, 10, 309
- Objective-C 类型编码, 102

## P

- `plutil` 工具, 177
- 过早优化, 116
- 原生方法, 96
- 属性列表, 80, 131, 279
- 纯虚方法, 154

## R

- 引用日期, 158
- 替换方法, 36
- 可恢复异常, 221
- 运行循环, 97, 167, 180, 294

## S

- SEL 类型, 21, 27
- 选择器 (selector), 27, 45, 311, 316
- 单例模式, 87, 94, 231
- 字符串对象, 113
- 意外终止, 192

## T

- 线程字典, 232
- 无缝桥接, 114
- 两阶段创建模式, 76
- 有类型选择器, 55

## U

- `UIApplication` 类, 167
- `unichar` 类型, 114

## V

- 可变参数函数, 130
- 可变参数方法, 131, 138
- 虚函数表, 3

## W

- 弱类引用, 312
- 工作空间进程, 227

## X

- XCode, 16, 298

## Z

- 无成本异常处理, 212
- 置零弱引用, 72
