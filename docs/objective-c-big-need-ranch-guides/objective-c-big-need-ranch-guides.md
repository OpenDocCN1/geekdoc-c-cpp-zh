
# Objective C 高级指南

# 致谢

能与如此优秀的人合作是我的极大的荣幸。其中几位同事投入了大量的时间和精力让这本书变得完美。我想借此机会感谢他们。

- Mikey Ward 编写了本书的几个章节，包括《你的第一个 iOS 应用》、《你的第一个 Cocoa 程序》和《块（Blocks）》。如果我是一个更好的老板，我本把他的名字印在封面上。
- 其他教授 Objective-C 课程的讲师为我们提供了源源不断的建议和纠错。他们是 Scott Ritchie、Mark Fenoglio、Brian Hardy、Christian Keur 和 Alex Silverman。
- 我辛勤工作的编辑 Susan Loper，她将我那段涵盖了程序员需要需要的所有知识的意识流式独白，打磨成了一本通俗易懂的入门教程。
- 几位技术评审员帮助我发现并修复了缺陷。他们是 James Majors、Mark Dalrymple、Scott Steinman、Bart Hoffman、Bolot Kerimbaev 和 Nate Chandler。
- Ellie Volckhausen 设计了封面。
- IntelligentEnglish.com 的 Chris Loper 设计并制作了 EPUB 和 Kindle 版本。
- Pearson Technology Group 优秀的团队耐心指导了我们完成了书籍出版的业务流程。

# 37. switch 语句

# 下一步

## 索引

# 更多来自 Big Nerd Ranch 的内容...

# 第一部分

## 入门

## 你与这本书

让我们花点时间聊聊。你想为 iOS 或 Mac OS X 编写应用程序，但你过去没有做过（或完全没做过）编程。你的朋友对我的其他书籍（《iOS 编程：极客农场指南》和《Mac OS X Cocoa 编程》）赞誉有加，但那些是为经验丰富的程序员写的。你该怎么办？读这本书。

虽然也有类似的书，但这一本是你应该读的。为什么？我教人们如何为 iOS 和 Mac 编写程序多年，我已经确定了你在旅程的现阶段需要了解什么。我付出了巨大的努力来捕捉这些知识，并摒弃了其他所有内容。书中有很多智慧，几乎没有废话。

我的方法有点与众不同。我不会简单地尝试让你理解 Objective-C 的语法，而是会向你展示编程是如何工作的，以及经验程序员是如何思考这些问题的。

由于这种方法，我将在书中早期涵盖一些深奥的概念。你不应该认为这是一本易读的书。此外，几乎每个概念都配有一个编程实验。这种学习概念并立即付诸行动的结合是学习编程的最佳方式。

## C 与 Objective-C

当你运行一个程序时，一个文件会从文件系统复制到内存（RAM），文件中的指令由你的计算机执行。这些指令对人类来说是不可理解的。因此，人类用编程语言来编写计算机程序。最低级别的编程语言被称为*汇编代码*。在汇编代码中，你描述了 CPU（计算机的大脑）必须的每一步。然后，这些代码会被汇编器转换为*机器码*（计算机的母语）。

汇编语言极其冗长、琐碎，且依赖于 CPU（因为你最新的 iMac 的的大脑可能与你那台心爱的、用旧的 PowerBook 的大脑大不相同）。换句话说，如果你想在不同类型的计算机上运行程序，你需要重写汇编代码。

为了编写可以轻松从一种类型的计算机移动到另一种类型的代码，我们开发了“高级语言”。通过高级语言，你不需要考虑特定的 CPU，而是可以用通用的方式表达指令，一个程序（称为*编译器*）会将这些代码转换为高度优化的特定 CPU 机器码。这些语言之一就是 C。程序员用 C 语言编写代码，然后由编译器将其转换为机器码。

C 语言是 20 世纪 70 年代在 AT&T 创建的。Unix 系统（OS X 和 Linux 的基础）是用 C 语言编写的，带有少量底层操作的汇编代码。Windows 系统也大部分是用 C 编写的。

Objective-C 语言基于 C，但它增加了对对象编程的支持。Objective-C 是用于编写 iOS 和 Mac OS X 操作系统的编程语言。

## 本书简介

在书中，你将学习足够的 C 和 Objective-C 语言知识，以便为 Mac 或 iOS 设备开发应用程序。为什么我要先教你 C？因为每个有效的 Objective-C 程序员都需要对 C 有深入的理解。此外，这本书的设计初衷是面对电脑阅读的。你将阅读概念的解释，并执行演示这些概念的实验。这些实验不是可选的。除非你动手，否则你无法真正理解书的内容。学习编程最好的方法是编写代码、修复错误并熟悉语言的模式。

为了更多的练习，每章的末尾都有被称为*挑战*的练习。这些练习提供了额外的实践，并将让你对所学内容更有信心。我强烈建议你尽可能多地做这些挑战。

你还会在某些章节的末尾看到被称为*好奇者*的部分。它们对书中涵盖的主题有更深入的解释。它们对你来说并非必须，但我希望你会发现它们很有趣。

Big Nerd Ranch 提供了一个读者讨论这本书和练习的论坛。你可以在 `http://forums.bnerdranch.com/` 找到它。

如果你知道如何盲打，你会发现这本书和编程会愉快得多。盲打不仅速度更快，还能让你看屏幕而不是键盘。这使得在错误发生时更容易捕捉它们。这是一项让你终身受益的技能。

## 程序员的生活

通过开始这本书，你决定成为一名程序员。你应该知道自己正在做什么。

程序员的生活大多是无休止的挑战。在不断变化的技术领域意味着程序员必须不断学习新知识。在这种情况下，“学习新知识”是“对抗无知”的委婉说法。即使程序员在使用熟悉的技术，有时我们创建的软件也非常复杂，仅仅理解哪里出了问题可能就需要花费一天的时间。

如果你编写代码，你就会面临挑战。大多数专业程序员一个小时又小时一天地挑战，而不会感到（太）沮丧。这是另一项让你终身受益的技能。如果你对程序员的生活和现代软件项目感兴趣，我非常推荐 Scott Rosenberg 写的《Dreaming in Code》一书。

现在是时候开始编写你的第一个程序了。

## 你的第一个程序

- 安装 Apple 开发者工具
- 使用这些工具创建一个简单的项目
- 探索如何使用这些工具确保我们的项目运行

在本章结束时，你将成功为 Mac 编写你的第一个程序。

## 安装 Apple 开发者工具

要为 Mac OS X（Mac）或 iOS（iPhone 和 iPad）编写应用程序，你将使用 Apple 的开发者工具。你可以从 `http://developer.apple.com/` 下载这些工具，或从 Mac App Store 购买。

安装工具后，在你的硬盘根目录下找到 `/Developer` 文件夹。该文件夹包含了为 Mac OS X 桌面和 iOS 移动设备开发应用程序所需的内容。

我们在书中的工作几乎完全通过一个应用程序进行——Xcode，它位于 `/Developer/Applications` 文件夹中。（将 Xcode 图标拖到 dock 中是一个好主意，你会经常使用它。）

## 开始使用 Xcode

Xcode 是 Apple 的集成开发环境。这意味着编写、构建和运行新应用程序所需的一切都在 Xcode 中。

关于术语的说明：任何在计算机上可执行的内容我们都称为程序。有些程序具有图形用户界面；我们将这些称为应用程序。

有些程序没有图形用户界面并在后台运行几天；我们将其称为守护进程（daemons）。守护进程听起来很可怕，但其实不是。你现在 Mac 上可能有 60 个守护进程在运行。它们在那里等待，希望用得上。例如，运行在你系统上的守护进程之一叫做 `pboard`。当你进行复制和粘贴时，`pboard` 守护进程持有你正在复制的数据。

有些程序没有图形用户界面并在终端中运行很短；我们将这些称为命令行工具。在书中，你将主要编写命令行工具，以便关注编程核心，而不受创建和管理用户界面的干扰。

现在我们将使用 Xcode 创建一个简单的命令行工具，让你看到它是如何工作的。

当你编写一个程序时，你创建并编辑一组文件。Xcode 在项目中跟踪这些文件。启动 Xcode。从 File（文件）菜单选择 New（新建），然后选择 New Project...（新建项目……）。

为了帮助你开始，Xcode 提供了一些可能的项目模板。你根据想编写的程序类型选择模板。在左侧列中，从 Mac OS X 部分选择 Application（应用程序）。然后从右侧出现的选项中选择 Command Line Tool（命令行工具）。

**图 2.1 选择模板**

点击 Next（下一步）按钮。

将你的新项目命名为 `AGoodStart`。公司标识符对于我们书中的练习并不重要，但你必须输入一个才能继续。你可以使用 `BigNerdRanch` 或其他名称。在 Type（类型）弹出菜单中，选择 C，因为你将用 C 语言编写此程序。

**图 2.2 选择选项**

![](img/a694739dec801cd745c57da9e19c2cd4_21_0.png)

点击 Next（下一步）按钮。

现在选择创建项目目录的文件夹。你不需要版本控制仓库，因此可以取消勾选该框。最后，点击 Create（创建）按钮。

在接下来的章节中，你将创建相同类型的项目。将来，我会说“创建一个名为 program-name-here 的新命令行工具”，让你遵循相同的序列。

（为什么用 C？记住，Objective-C 是建立在 C 编程语言之上的。在我们接触 Objective-C 的细节之前，你需要对 C 的部分有所了解。）

## 我从哪里开始写代码？

创建项目后，你会看到一个窗口，显示将生成 `AGoodStart`。

**图 2.3 AGoodStart 项目首次视图**

![](img/a694739dec801cd745c57da9e19c2cd4_23_0.png)

此窗口包含了许多细节，例如可以运行应用程序的 Mac 版本、编译代码时的配置，以及应用到项目中的任何自定义。让我们先忽略这些细节，找到一个可以工作的起点。

在左侧面板顶部找到名为 `main.c` 的文件并点击它。（如果没有看到 `main.c`，点击 `AGoodStart` 旁边的三角形显示内容。）

**图 2.4 在 AGoodStart 组中查找 main.c**

![](img/a694739dec801cd745c57da9e19c2cd4.png)

注意我们的原始视图发生了变化，显示了 `main.c` 的内容。`main.c` 文件包含一个名为 `main` 的函数。

函数是计算机执行的指令列表，每个函数都有一个名称。在 C 或 Objective-C 程序中，`main` 是程序启动时调用的函数。

```c
#include <stdio.h>

int main (int argc, const char argv[]) {

    // 插入代码
    printf("Hello, World!\n");
    return 0;
}
```

在这个函数中，你会发现你编写的两种信息：代码和注释。

- 代码是告诉计算机执行操作的指令集。
- 注释会被计算机忽略，但程序员用它们记录代码。你尝试解决的编程越困难，注释就越有助于你记录解决过程。当你回到工作时，这变得特别重要：“这个解决方案很棒，但我完全忘记它是如何工作的。”

在 C 和 Objective-C 中，有两种区分注释和代码的方法：

- 如果在行开头使用 `//`，从正斜杠到行尾的内容都被视为注释。你可以在“插入代码...”处看到这种用法。
- 如果你有更长的备注，可以使用 `/*` 和 `*/` 来标记跨越多行的注释开始和结束。

标记注释的规则是*语法*的一部分。语法是规定如何在编程语言中编写代码的规则。这些规则非常具体，如果你不遵守，程序将无法运行。

虽然关于注释的语法非常简单，但代码的语法取决于代码做什么以及如何实现。但有一个特征保持不变：每条语句都以分号结尾。（稍后我们将看到代码语句的示例。）如果你忘记了分号，就会产生语法错误，程序无法运行。

幸运的是， Xcode 会警告你这些错误。事实上，程序员面临的首要挑战之一就是解释 Xcode 在出错时告诉你的信息并修复它们。随着学习，你会看到 Xcode 对常见语法错误的响应。

让我们对 `main.c` 进行一些更改。首先，我们需要留出空间。找到标记 `main` 函数开始和结束的大括号 `{` 和 `}`。然后删除之间的所有内容。

现在更新 `main.c` 如下所示。你为 `main` 函数添加了一个注释、两行代码和另一个注释。现在即使你不自己在输入什么，不要担心。目标是开始。你有一整本书要学习它们所有的含义。

```c
#include <stdio.h>

int main(int argc, const char argv[]) {
    // 打印开头
    printf("It was the best of times.\n");
    printf("It was the worst of times.\n");
    /* 这好吗？ */
    return 0;
}
```

注意我们的原始视图发生了变化，显示了 `main.c` 的内容。`main.c` 文件包含一个名为 `main` 的函数。

```
This GDB was configured as "x86_64-apple-darwin".tty /dev/ttys001
[Switching to process 2723 thread 0x0]
It was the best of times.
It was the worst of times.
```

（在我写这些文字时，Apple 正在开发一种名为 LLDB 的新调试器。它最终将取代当前的调试器 GDB。如果你没有看到所有的 GDB 信息，那意味着 LLDB 现在是 Xcode 的标准调试器。未来一定是一个极佳的地方；我羡慕你。）

# 那么什么是程序？

现在你已经构建并运行了程序，让我们来看看它的内部构造吧。程序是函数的集合。函数是处理器要执行的一系列操作。每个函数都有一个名字，你刚刚写的那个函数名为 `main`。还有另一个函数——`printf`。你没有写这个函数，但你确实使用了它。（我们将在第 5 章中找出 `printf` 来自于哪里。）

对于程序员来说，写一个函数就像在写食谱：“慢慢搅拌一夸水直到它沸腾。然后加入一杯面粉。趁热享用。”

在 20 世纪 70 年代，Betty Crocker 开始销售包含一组食谱卡的盒子。食谱卡是函数的一个非常好的比喻。就像函数一样，每张卡片都有名字和一组指令。区别在于你执行的是食谱，而计算机执行的是函数。

**图 2.5** 一名为“烤鸡肉”的食谱卡

# 执行

| 烤鸡肉 |
| :--- |
| 在浅盘中搅拌混合牛奶、鸡蛋、油、盐和胡椒。 |
| 将架子放在距离热源约 6 英处处并预热烤箱。 |
| 将鸡肉浸入牛奶混合液，裹上面包屑，放入锡箔纸烤盘中。 |
| 烤鸡肉直到煮透，每面约 7 分钟。 |

Betty Crocker 的烹饪说明是英语的。在本书的第一部分，你的函数将用 C 语言语言编写。然而，计算机处理器期望的是机器码指令。我们如何实现这一目标呢？

当你用 C 语言编写程序时（这对你来说相对愉快），编译器会将你的程序函数转换为机器码（这对处理器来说既愉快又高效）。编译器本身是一个程序，它在你按下“运行”按钮时由 Xcode 运行。编译程序与构建程序相同，我们将这两个术语交替使用。

当你运行程序时，编译后的函数会从硬盘复制到内存中，由处理器执行 `main` 函数。`main` 函数通常会调用其他函数。例如，你的 `main` 函数调用了 `printf` 函数。（我们将在[第 5 章]()中看到更多关于函数如何交互的知识。）

# 不要停止

到目前，你可能已经遇到过好几次挫折：安装问题、拼写错误以及大量的新词汇。也许你到为止所做的一切都不符合逻辑。这完全是正常的。

在我写这些文字时，我的儿子 Otto 也是如此。Otto 每天都会感到几次困惑。他不断地尝试吸收不符合他现有心理脚架的知识。困惑发生得如此频繁，以至于并没困扰他。他从没有停下来想：“为什么这这么难懂？我应该把这书扔掉吗？”

随着年龄的增长，我们感到困惑的情况少多了——不是因为我们知道一切，而是因为我们倾向于避开那些让我们迷茫的事情。例如，读一本历史书是非常愉快的，因为我们可以获得一些可以挂在现有心理脚架上的知识点。这是轻松的学习。

学习一种新语言是困难学习的例子。你知道有数百万人能毫不费力地用那种语言工作，但在你嘴里听起来却非常奇怪和别扭。当人们对你说这种语言时，你感到非常诡异。

学习计算机程序也是困难学习。你经常感到困惑——尤其是在刚开始的时候。没关系，坚持读这本书；我保证迷惑在到达最后一页之前就会消失。

# 第二部分

## 编程是如何工作的

## 变量与类型

在 C语言中，你通过声明类型和名称来创建一个变量。这里有一个示例：

```c
float weight;
```

这个变量的类型是 `float`，名字是 `weight`。此时变量还没有值。

在 C 中，你必须为每个变量声明类型，原因有两个：

- 类型让编译器检查你的工作并提醒你可能出现的问题。例如，假设你有一个文本类型的变量。如果你请求它的对数，编译器会告诉你“这没有意义。”
- 类型告诉编译器为该变量留出内存空间（多少字节）。

这里是常用类型的概述。我们将在后面的章节中详细介绍每种类型。

`short`、`int`、`long` 这三种类型是整数；它们不需要小数点。`short` 的存储空间比 `long` 少，`int` 介于两者之间。因此你可以在 `long` 中存储比 `short` 大多的数字。

`float`、`double` `float` 是浮点数——即带有小数点的数字。在内存中，`float` 以有效数字和指数的形式存储。`double` 是双精度数字，通常具有更多的位来存储更长的有效数字更大的指数。

`char` `char` 是单字节整数，我们通常将其视为字符，如字母 'a'。

`pointers` 指针存储内存地址。它使用星号声明。例如，声明为 `int *` 的变量可以存储一个 int 的内存地址。它并不持有实际数值的值，但如果你知道该 int 的地址，就可以轻松地获取它的值。指针非常有用，以后会有更多关于指针的内容。非常多。



struct 结构体（`struct`）是由其它类型组成的类型。你也可以创建新的结构体定义。例如，假设你想要一个包含两个 `float` 成员（纬度和经度）的 `GeoLocation` 类型。在这种情况下，你将定义一个 `struct` 类型。

这些是 C 程序员每天使用的类型。令人惊讶的是，复杂的想法可以被这五个简单的想法所捕捉。

## 一个带有变量的程序

在 Xcode 中，你将创建另一个项目。首先，关闭 GoodStart 项目，以免不小心在旧项目中输入新代码。

现在，创建一个新项目（`File -> New -> New Project...`）。该项目将是一个名为 Turkey 的 C 命令行工具（Command Line Tool）。

在项目导航器中，找到该项目的 `main.c` 文件并打开它。使 `main.c` 内容与以下代码匹配。

```c
#include <stdio.h>
int main (int argc, const char * argv[])
{
    // 声明一个类型为 float 的变量名为 weight
    float weight;

    // 给该变量赋一个数字
    weight = 14.2;

    // 将其打印给用户
    printf("The turkey weighs %f.\n", weight);

    // 声明另一个 float 变量
    float cookingTime;

    // 计算烹饪时间并存储在变量中
    // 在这里，'*' 表示“乘以”
    cookingTime = 15.0 + 15.0 * weight;

    // 将结果打印给用户
    printf("Cook it for %f minutes.\n", cookingTime);

    // 结束函数并指示成功
    return 0;
}
```

编译并运行程序。你可以点击 Xcode 窗口左上角的 Run 按钮，或者使用快捷键 `Command-R`。然后点击按钮打开日志导航器（log navigator）。选择顶部标记为 Debug Turkey 的项以显示输出。输出看起来应该是这样的：

The turkey weighs 14.200000.

Cook it for 228.000000 minutes.

现在点击按钮返回项目导航器。然后选择 `main.c` 即可再次看到你的代码。让我们回顾一下你在这里所做的。

在你这如下所示的代码行中：

```c
float weight;
```

我们称你正在“声明变量 weight 的类型为 float”。

在下一行中，你的变量获得了一个值：

```c
weight = 14.2;
```

你正在将数据复制到该变量中。我们称你正在“将值 14.2 赋值给该变量”。

在现代 C 中，你可以在一行内声明变量并为其赋初始值，如下：

```c
float weight = 14.2;
```

这是另一个赋值语句：

```c
cookingTime = 15.0 + 15.0 * weight;
```

等号右侧的内容是一个表达式（expression）。表达式是一个会被求值并产生某个值的东西。实际上，每个赋值在等号右侧都有表达式。

例如，在这一行中：

```c
weight = 14.2;
```

表达式只是 14.2。

变量是任何程序的构建块。这只是对变量世界的介绍。随着我们的继续，你将学习更多关于变量如何工作以及如何使用它们的内容。

## 挑战

创建一个名为 TwoFloats 的新 C 命令行工具。在它的 `main()` 函数中，声明两个 `float` 类型的变量，并为它们每一个分配一个带小数点的数字，例如 3.14 或 42.0。声明另一个 `double` 类型的变量，并将其赋值为两个 float 之和。使用 `printf()` 打印结果。如果需要检查语法，请参考本章中的代码。

## 4 if/else

编程中一个重要的思想是根据情况采取不同的行动。订单表中的所有费用字段都填写完毕了吗？如果是，启用提交按钮。玩家还有剩余生命吗？如果是，继续游戏。如果不是，显示坟墓图片并播放悲伤的音乐。

这种行为是通过 `if` 和 `else` 实现的，其语法如下：

```c
if (条件) {
    // 如果条件为真，执行代码
} else {
    // 如果条件为假，执行代码
}
```

### else if

如果你有两个以上的可能性怎么办？你可以通过 `else if` 逐个对它们进行测试。例如，假设一辆卡车属于三种重量分类之一：浮动式、轻型和重型。

```c
if (truckWeight <= 0) {
    printf("A floating truck\n");
} else if (truckWeight < 40000.0) {
    printf("A light truck\n");
} else {
    printf("A heavy truck\n");
}
```

你可以根据需要编写任意数量的 `else if` 。它们将按照出现的顺序依次进行测试，直到其中一个评估结果为真。“按照出现的顺序”这一点非常重要。务必确保你对上面示例中交换的前两个测试顺序是正确的，否则你永远不会发现误报。例如，如果你交换了上面示例的前两个测试，你将永远找不到浮动卡车，因为浮动式卡车也是轻型卡车。最后的 `else` 子句是可选的，但当你想要捕获不符合之前条件的所有时，它是很有用的。

### 给更具好奇心的读者：条件运算符（三元运算符）

使用 `if` 和 `else` 来设置实例变量的值并不罕见。例如，你可能会有以下代码：

```c
int minutesPerPound;
if (isBoneless)
    minutesPerPound = 15;
else
    minutesPerPound = 20;
```

每当你遇到根据条件给变量赋值的场景时，你就有使用条件运算符的候选，即 `?`。（你有时也会看到它被称为三元运算符）。

```c
int minutesPerPound = isBoneless ? 15 : 20;
```

这一行代码等同于之前的示例。你不需要写 `if` 和 `else`，而是写一个赋值语句。`?` 之前的部分是条件。`?` 之后的值是条件为真或为假时的备选值。

如果你觉得这种表示法很奇怪，继续使用 `if` 和 `else` 也没有问题。我怀疑随着时间的推移，你会接受三元运算符作为一种执行条件赋值的简洁方式。更重要的是，你将看到其他程序员使用它，而理解你所看到的内容是一件乐事！

## 挑战

考虑以下代码段：

```c
int i = 20;
int j = 25;

int k = ( i > j ) ? 10 : 5;

if ( 5 < k ) { // 第一表达式
    printf("The first expression is true.");
} else if ( j > i ) { // 第二表达式
    printf("The second expression is true.");
} else {
    printf("Neither expression is true.");
}
```

控制台将打印什么内容？

## 函数

在第 3 章中，我引入了变量的概念：一个与数据块关联的名字。函数是一个与一段代码关联的名字。你可以向函数传递信息。你可以让函数执行代码。你可以让函数为你返回信息。

函数是编程的基础，所以这一章有很多内容——三个新项目、一个新工具和许多新思想。让我们从一个演示函数用途的练习开始。

### 我应该什么时候使用函数？

假设你正在编写一个程序来祝贺学生完成 Big Nerd Ranch 的课程。在担心从数据库中检索学生列表或在精美的 Big Nerd Ranch 纸张上打印证书之前，你想实验一下打印在证书上的消息。

为了进行这个实验，请创建一个名为 `ClassCertificates` 的新 C 命令行工具。

你编写这个程序的第一个想法可能是：

```c
int main (int argc, const char * argv[]) {
    printf("Mark has done as much Cocoa Programming as I could fit into 5 days\n");
    printf("Bo has done as much Objective-C Programming as I could fit into 2 days\n");
    printf("Mike has done as much Python Programming as I could fit into 5 days\n");
    printf("Ted has done as much iOS Programming as I could fit into 5 days\n");
    return 0;
}
```

输入所有这些会让你困扰吗？它们看起来是否非常烦人的重复？如果是这样，你就具备了优秀程序员的特质。当你发现自己自己在重复性质非常相似的工作（在本例中是 `printf` 语句中的单词）时，你就应该开始将函数作为完成相同任务的更好方式。

### 我如何编写和使用函数？

现在你已经意识到你需要一个函数，你需要编写一个。

打开你的 `ClassCertificates` 项目中的 `main.c`，并在 `main` 函数之前添加一个新函数。将此函数命名为 `congratulateStudent`。

```c
#include <stdio.h>

void congratulateStudent(char *student, char *course, int numDays)
{
    printf("%s has as much as %d Programming as I could fit into %d days.\n",
           student, course, numDays);
}
```

（疑惑 `%s` 和 `%d` 是什么意思？等一下；我们将在下一章中讨论它们。）

现在编辑 `main` 以使用你的新函数：

```c
int main (int argc, const char *argv[])
{
    congratulateStudent("Mark", "Cocoa", 5);
    congratulateStudent("Bo", "Objective-C", 2);
    congratulateStudent("Mike", "Python", 5);
    congratulateStudent("Ted", "iOS", 5);

    return 0;
}
```

编译并运行程序。你可能会看到一个由小黄色三角形内感叹号标记的警告。Xcode 中的警告不会阻止你的程序运行；它引起你注意可能的问题。警告文本位于右侧。警告内容类似于“函数 'congratulateStudent' 没有之前的原型”。现在先忽略这个警告，我们将在本节末尾再回到它。

在日志导航器中找到你的输出。它应该和你手动输入所有内容时看到的完全一样。

- Mark has done as much Cocoa Programming as I could fit into 5 days.
- Bo has done as much Objective-C Programming as I could fit into 2 days.
- Mike has done as much Python Programming as I could fit into 5 days.
- Ted has done as much iOS Programming as I could fit into 5 days.

思考一下你所做的。你注意到了一个重复的模式。你提取了问题的共同特征（重复文本）并将它们移动到一个单独的函数中。让我们再次看一眼命名函数的行。

```c
void congratulateStudent(char *student, char *course, int numDays)
```

打字？嗯，是的，但这绝对不是全部。它还涉及到错误检查。你输入的越少，计算机处理得越多，出现拼写错误的机会就越少。此外，如果你写错了函数名，Xcode 会提醒你，但 Xcode 并不知道你是否写错了文本。

编写函数的另一个好处是可重用性。现在你已经写了这个实用的函数，你可以在另一个程序中使用它。修改变得更加简单，你只需要在一个地方调整祝贺语的措辞，它就会在处处生效。

函数的最后一个好处是，如果出现了“bug”，你只需要修复那一个函数，突然调用它的所有地方都会开始正常工作。将代码划分分为函数使其更于理解和维护。

现在回到你代码中的那个警告。在某处声明函数并在另一个地方定义它是很常见的。声明函数只是告诉编译器有一个特定名称的函数即将出现。定义函数才是你描述应该执行的步骤的地方。在这个练习中，你实际上在同一个地方声明并定义了你的函数。因为这并不常见，所以如果你的函数没有提前声明，Xcode 就会发出警告。

在本书书中构建的任何项目中，忽略这个警告都是可以的。或者你可以花时间禁用它。要这样做，选择 `ClassCertificates` 目标，它是项目导航器顶部的项目。在编辑器面板中，选择 `Build Settings` 选项卡下的 `All`。滚动不同的构建设置并找到 `Missing Function Prototypes` 设置。将此设置更改为 `No`。

## 图 5.1 禁用缺少函数原型的警告

## 函数是如何协同工作的

程序是函数的集合。当你运行程序时，这些函数会从硬盘复制到内存中，处理器找到名为“main”的函数并执行它。

记住，函数就像一张食谱卡片。如果我开始执行“烤鸡”卡片，我会发现第二条指令是“制作调味面包屑”，这在另一张卡片上有解释。程序员会说“烤鸡函数调用了调味面包屑函数”。



图 5.2 食谱卡片

| 烤鸡 | 调味面包屑 |
| :--- | :--- |
| 在一个浅盘中将牛奶、鸡蛋、油、盐和胡椒搅拌均匀。 | 将 3 片面包撕成碎片并铺在饼干底上。 |
| 执行 `调味面包屑` 食谱。 | 混合橄榄油、欧芹碎、牛香和和大蒜粉。 |
| 将架子放在热源约 6 英寸处预热电烤箱。 | 洒在面包碎片上 |
| 将鸡肉浸入牛奶混合物，裹上面包屑，放入类似铝箔的烤盘中 | 在 225° 华氏（107°C）的烤箱中干燥一小时 |
| 烤鸡直到煮透，每面约 7 分钟。 | 揉成碎。 |

同样，`main()` 函数可以调用其他函数。例如，`ClassCertificates` 中的 `main()` 函数调用了 `congratulateStudent()` 函数，该函数反过来调用了 `printf()`。

当你准备调味面包屑时，你停止执行“烤鸡”卡片。当面包屑准备好后，你继续处理“烤鸡”卡片。

同样，`main()` 函数会停止执行并“阻塞”，直到它调用的函数执行完毕。为了看到这种情况，我们将调用一个 `sleep()` 函数，它的作用只是等待几秒钟。在你的 `main()` 函数中，添加对 `sleep()` 的调用。

```c
int main (int argc, const char * argv[]) {
    congratulateStudent("Mark", "Cocoa", 5);
    sleep(2);
    congratulateStudent("Bob", "Objective-C", 2);
    sleep(2);
    congratulateStudent("Mike", "PHP and PostgreSQL", 5);
    sleep(2);
    congratulateStudent("Ted", "IOS", 5);

    return 0;
}
```

构建并运行程序。（现在忽略关于隐式声明的警告。）你应该每条祝贺消息之间看到 2 秒的暂停。这是因为 `main()` 函数会停止运行，直到 `sleep()` 函数执行完毕。

注意当你调用一个函数时，你使用它的名称和一对变量。同样，`main()` 函数会停止执行并“阻塞”，直到它调用的函数执行完毕。为了看到这种情况，我们将调用一个 `sleep()` 函数，它的作用只是等待几秒钟。在你的 `main()` 函数中，添加对 `sleep()` 的调用。

```c
int main (int argc, const char * argv[]) {
    congratulateStudent("Mark", "Cocoa", 5);
    sleep(2);
    congratulateStudent("Bob", "Objective-C", 2);
    sleep(2);
    congratulateStudent("Mike", "PHP and PostgreSQL", 5);
    sleep(2);
    congratulateStudent("Ted", "IOS", 5);

    return 0;
}
```

构建并运行程序。（现在忽略关于隐式声明的警告。）你应该每条祝贺消息之间看到 2 秒的暂停。这是因为 `main()` 函数会停止运行，直到 `sleep()` 函数执行完毕。

| showTurkeyCookTime() | pounds = 9 |
| | necessaryMinutes = 135 |
| main() | totalWeight = 10 |
| | gibletsWeight = 1 |
| | turkeyWeight = 9 |

栈总是后入先出的。这意味着，`showCookTimeForTurkey()` 会在 `main()` 弹出它的栈帧之前将其栈帧从栈弹出。

注意，`pounds` 是 `showCookTimeForTurkey()` 的唯一参数，它是帧（frame）的一部分。回想一下，参数是一个被赋值了对应参数值的局部变量。在这个示例中，值为 9 的变量 `turkeyWeight` 被作为参数传递给 `showCookTimeForTurkey()`。然后，该值被赋值给参数 `pounds` 并复制到函数的栈帧中。

## 递归

函数可以调用自己吗？那是肯定的！我们称之为递归。有一首臭名昭著的歌曲叫《99 瓶啤酒》（99 Bottles of Beer）。创建一个名为 BeerSong 的新 C 命令行工具。打开并添加一个函数来写出这首歌的歌词，并在 `main()` 中启动它：

```c
#include <stdio.h>

void theSong(int numberOfBottles) {
    if (numberOfBottles == 0) {
        printf("There are simply no more bottles of beer on the wall.\n");
    } else {
        printf("There are %d bottles of beer on the wall.\n", numberOfBottles);
        int numberFewer = numberOfBottles - 1;
        printf("Take one down, pass it around, %d bottles of beer on the wall.\n", numberFewer);
        singTheSong(numberFewer); // 这个函数调用了自己！
        printf("Put a bottle in the recycling, %d empty bottles in the bin.\n", numberOfBottles);
    }
}
```

```c
int main(int argc, const char * argv[]) {
    singTheSong(99);
    return 0;
}
```

编译并运行程序。输出如下：

```
99 bottles of beer on the wall. 99 bottles of beer.
Take one down, pass it around, 98 bottles of beer on the wall.
98 bottles of beer on the wall. 98 bottles of beer.
Take one down, pass it around, 97 bottles of beer on the wall.
97 bottles of beer on the wall. 97 bottles of beer.
1 bottle of beer on the wall. 1 bottle of beer.
Take one down, pass it around, 0 bottles of beer on the wall.
There are simply no more bottles of beer on the wall.
Put a bottle in the recycling, 1 empty bottle in the bin.
Put a bottle in the recycling, 2 empty bottles in the bin.
Put a bottle in the recycling, 98 empty bottles in the bin.
Put a bottle in the recycling, 99 empty bottles in the bin.
```

当最后一瓶啤酒从墙上取下时，栈是什么样子的？

图 5.5 递归函数的栈栈帧

```
singTheSong() | numberOfOfBottles = 0
singTheSong() | numberOfOfBottles = 1
oneFewer = 0
```

```
singTheSong() | numberOfOfBottles = 96
oneFewer = 95
singTheSong() | numberOfOfBottles = 97
oneFewer = 96
singTheSong() | numberOfOfBottles = 98
oneFewer = 97
singTheSong() | numberOfOfBottles = 99
oneFewer = 98
main()
```

讨论栈帧和栈通常不会在基础编程课程中涵盖，但我发现这些思想对新程序员来说极其有用。首先，它让你对诸如“当函数执行结束，我的局部变量会发生什么？”这类问题有更具体的理解。其次，它帮助你理解调试器。调试器是一个帮助你理解程序实际在做什么的程序，反过来又帮助你发现并修复“bug”（代码中的问题）。当你在 Xcode 中构建并运行程序时，调试器会附加到程序上以便你使用它。

## 在调试器中查看帧

你可以使用调试器来浏览栈上的帧。然而，你必须在程序执行中途中停止它。否则，`main()` 将执行完毕，就不会有任何帧可以查看了。为了在我们的 BeerSong 程序中看到尽可能多的帧，我们希望在打印“There are simply no more bottles of beer on the wall.”的那一行上停止执行。

```c
printf("There are simply no more bottles of beer on the wall.\n");
```

你的代码左侧有两个阴影列。点击此行旁边较宽的左侧列。

### 5.6 设置断点

![](img/a64739dec801cd745c7dae19cd4_0.png)

设置断点可以让程序在该处暂停。调试器可以让你检查变量的状态、调用栈，以及单步执行代码。在 Xcode 中，你可以通过点击行号左侧的区域来设置断点。当程序运行到断点时，调试器左侧的调试区域（Debug Area）会激活，其中栈（Stack）区域显示了当前线程的调用帧。

# 全局变量和静态变量

在本章中，我们讨论了仅在函数运行时存在的局部变量。还有可以在任何时间从任何函数访问的变量，我们称之为全局变量。要使一个变量变为全局变量，你需要在函数外部声明它。例如，你可以添加一个 `lastTemperature` 变量来存储从摄氏度转换为华氏度的温度。如下：

```c
#include <stdio.h>
#include <stdlib.h>

// 声明一个全局变量
float lastTemperature;

float FahrenheitFromCelsius(float cel)
{
    lastTemperature = cel;
    float f = cel * 1.8 + 32.0;
    printf("%f Fahrenheit\n", f);
    return f;
}

int main(int argc, char *argv[]) {
    float freezeInC = 0;
    float freezeInF = FahrenheitFromCelsius(freezeInC);
    printf("Water freezes at %f Fahrenheit\n", freezeInF);
    printf("The last temperature was %f\n", lastTemperature);
    return EXIT_SUCCESS;
}
```

任何复杂的程序都会涉及多个文件。全局变量在这些文件中是可用的。有时，在不同文件之间共享变量可能会导致混淆。为了解决这个问题，我们使用了静态变量。静态变量就像全局变量，但它仅在声明它的文件中可访问，从而避免了冲突！你可以将全局变量改为静态变量，但因为你只有一个文件 `main.c`，这不会产生任何影响。

```c
// 声明一个静态变量
float lastTemperature;

// 初始化 lastTemperature 为 50
static float lastTemperature = 50.0;
```

静态和全局变量在创建时都可以被赋予初始值：如果不给它们赋予初始值，它们会被初始化为零。

在本章中，你学习了函数。当我们进入 Objective-C 的第三部分时，你会听到这个词——方法与函数非常相似。

## 挑战

三角形的内角和必须等于 180 度。创建一个名为 Triangle 的新 C 命令行工具。在 `main.c` 中，编写一个函数接收两个角并返回第三角。当你调用它时看起来如下：

```c
#include <stdio.h>

// 在此处添加你的新函数

int main(int argc, const char * argv[])
{
    float angleA = 30.0;
    float angleB = 60.0;
    float angleC = remaining(angleA, angleB);
    printf("The third angle is %.2f\n", angleC);
    return 0;
}
```

输出应该是：

```
第三个角是 90.0
```

# 数字

我们使用了数字来测量和显示温度、重量。现在让我们仔细看看数字在 C 语言中是如何工作的。在计算机上，数字有两种类型：整数和浮点数。你已经用过这两种。本章试图规范 C 程序员需要了解这些数字的知识。

## printf()

在讨论数字之前，让我们仔细看看你正在使用的 `printf()` 函数。`printf()` 向日志打印一个*字符串*。字符串是字符序列。从本质上讲，它是文本。

重新打开 **证书** 项目。在 `main.c` 中，找到 `congratulateStudent()`。

```c
void congratulateStudent(char *student, char *course, int numDays) {
    printf("%s as much %s as I could fit into %d days.\n", student, course, numDays);
}
```

这个对 `printf()` 的调用是做什么的？嗯，你已经看到输出了，知道它是做什么的。现在让我们弄清楚它。`printf()` 是一个接受字符串参数的函数。你可以通过双引号包裹文本创建一个*字面量字符串*（与存储在变量中的字符串相对）。

`printf()` 取字符串被称为**格式字符串**（format string），格式字符串可以包含*令牌*（tokens）。该字符串中的三个令牌是 `%s`、`%s` 和 `%d`。当程序运行时，令牌会被后面的变量值替换。在这种情况下，变量是 `student`、`course` 和 `numDays`。注意它们在输出中按顺序被替换。如果你在变量列表中交换了 `student` 和 `course`，你会看到

> Coco 在 5 天内填充了尽可能多的 Mark 编程。

然而，令牌和变量并不是完全可以交换的。`%s` 令牌期望一个字符串。`%d` 期望一个整数。（尝试交换它们看看会发生什么。）

注意 `student` 和 `course` 被声明为 `char *` 类型。现在，将 `char *` 读作字符串类型。我们将在 Objective-C 的第 [14] 章回到字符串，并在 [34] 章回到 `char`。

最后，`\n` 是怎么的？在 `printf()` 语句中，你必须包含一个显式的换行符，否则所有的日志输出将挤在同一行。`\n` 代表换行符。

现在让我们回到数字。

## 整数

整数是不带小数点的数字——一个全整数。整数适用于计数等问题。某些问题（例如计算地球上的每一个人）需要非常大的数字。其他问题（例如计算教室里的学生人数）不需要很大的数字。

为了解决这些不同的问题，整数变量有不同的大小。整数变量具有特定位数的位进行编码，变量的位数越多，它能容的数字就越大。典型大小有：8 位、16 位、32 位和 64 位。

同样，某些问题需要负数，而另一些则不需要。因此，整数有符号和无符号变体。

无符号 8 位整数可以包含 0 到 255 之间的整数。

有符号 64 位整数可以包含范围从 -9,223,372,036,854,775,808 到 9,223,372,036,854,775,807 的整数。

当你声明整数时，可以加上 unsigned 前缀创建等价物。正如你在第三中学中学：

```c
char a; // 8 位
short b; // 通常 16 位
int c; // 通常 32 位（取决于平台）
long d; // 32 或 64 位（取决于平台）
long long e; // 64 位
```

此外，整数的大小取决于平台。（平台是操作系统和特定的计算机或移动设备。）某些平台是 32 位的，另一些是 64 位的。区别在于内存地址，我们将在第 8 章详细讨论。

Apple 创建了两种整数类型，在 32 位平台上它们是 32 位，在 64 位平台上它们是 64 位：

```c
NSInteger g;
NSInteger h;
```

在 Apple 的大部分代码中，你会看到这些类型。它们在目的上与 long 和 unsigned long 相同。

## 显示整数的令牌

创建一个名为 Numbers 的 C 命令行工具。在 `main.c` 中，创建一个整数并使用 `printf()` 以 10 进制（十进制）打印它：

```c
#include <stdio.h>

int main (int argc, const char * argv[])
{
    int x = 255;
    printf("%x is %d.\n", x);
    return 0;
}
```

你应该看到类似

```
x = 255.
```

正如我们所见，%d 将整数打印为十进制。还有哪些令牌有效？你可以以 8 进制（八进制）或 16 进制（十六进制）打印该整数。向程序添加几行：



```c
#include <stdio.h>

int main (int argc, const char * argv[])
{
    int x = 255;
    printf("%x is %d.\n", x);
    printf("在八进制下，x 是 %o.\n", x);
    printf("在十六进制下，x 是 %x.\n", x);

    return 0;
}
```

当你运行它时，你应该能看到类似的内容：

x 是 255。

在八进制中，x 是 377。

在十六进制中，x 是 ff。

（我们将在第 33 章回到十六进制数。）

如果整数有很多位呢？你在 `%` 和格式化字符之间插入一个 `1`（代表 `long`）或两个 `1`（代表 `long long`）。修改你的程序以使用 `long` 代替 `int`：

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {
    long x = 255;
    printf("x is %ld.\n", x);
    printf("In octal, x is %lo.\n", x);
    printf("In hexadecimal, x is %lx.\n", x);

    return 0;
}
```

如果你正在打印一个无符号十进制数，你应该使用 `%u`：

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {
    unsigned long x = 255;
    printf("x is %lu.\n", x);

    // 八进制和十六进制已经假设该数是无符号
    printf("In octal, x is %lo.\n", x);
    printf("In hexadecimal, x is %lx.\n", x);

    return 0;
}
```

## 整数运算

算术运算符 `+`、`-` 和 `*` 的工作方式正如你所预期。它们也具有你预期的优先级规则：`*` 在 `+` 或 `-` 之前计算。在 `main.c` 中，将之前的代码替换为计算：

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {
    printf("3 * 3 * 5 * 2 = %d\n", 3 * 3 * 5 * 2);
    return 0;
}
```

你应该看到

3 * 3 + 5 * 2 = 19

## 整数除法

大多数初学 C 的程序员对整数除法的工作方式感到惊讶。试一下：

```c
#include <stdio.h>

int main (int argc, const char * argv[])
{
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
    printf("11 / 3 = %d\n", 11 / 3);

    return 0;
}
```

你会得到 `11 / 3 = 3.666667`，对吧？你得到的 `11 / 3` 是 `3`。当你用一个数除以另一个数时，你总是得到第三个整数。系统向零舍入。（所以，`-11 / 3` 是 `-3`）。

如果你认为“11 除以 3 等于 3，余 2”，那么这其实是有意义的。事实证明余数往往很有价值。取模运算符 `%` 类似于 `/`，但它返回的是余数而不是商。

```c
#include <stdio.h>

int main (int argc, const char * argv[])
{
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
    printf("11 / 3 = %d remainder of %d\n", 11 / 3, 11 % 3);

    return 0;
}
```

如果你想使用强制转换运算符将 `int` 转换为 `float` 呢？强制转换运算符是你想要放在括号中的类型，放在要转换变量的左侧。在除法之前，将分母转换为 `float`：

```c
int main (int argc, const char * argv[])
{
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
    printf("11 / 3 = %d remainder of %d\n", 11 / 3, 11 % 3);
    printf("11 / 3.0 = %f\n", 11 / (float)3);
    return 0;
}
```

现在，执行的是浮点除法而不是整数除法，你将得到 `3.666667`。这里是整数除法与浮点除法的规则：只有当分子和分母都是整数时，`/` 才是整数除法。如果其中任何一个是浮点数，则执行浮点除法。

## 运算符简写

你到目前为止看到的所有运算符都会产生一个新的结果。因此，例如为了让 `x` 增加 1，你会使用 `+` 运算符并将结果赋值回 `x`：

```c
int x = 5;
x = x + 1; // x 是 6
```

C 程序员经常进行此类操作，因此创建了运算符可以在不赋值的情况下改变变量的值：

```c
int x = 5;
x++; // x 现在是 6
```

还有一个递减运算符 (`--`)，它可以将值减 1：

```c
int x = 5;
x--; // x 现在是 4
```

如果你想让 `x` 增加 5 而不仅仅是 1 呢？你可以使用加法：

```c
int x = 5;
x += 5; // x 是 10
```

但这也有简写：除了 `+=` 之外还有 `-=`、`*=`、`/=` 和 `%=`。要获取 `int` 的绝对值，请使用函数而不是运算符。如果你想获取 `long` 的绝对值，使用 `labs()`。这两个函数都在 `stdlib.h` 中声明：

```c
#include <stdio.h>
#include <stdlib.h>

int main (int argc, const char * argv[]) {
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
    printf("11 / 3 = %d remainder of %d\n", 11 / 3, 11 % 3);
    printf("11 / 3.0 = %f\n", 11 / (float)3);
    printf("The absolute value of -5 is %d\n", abs(-5));
    return 0;
}
```

## 浮点数

如果你需要一个带有小数点的数字，比如 `3.2`，你就使用浮点数。大多数程序员将浮点数视为尾数乘以 10 的整数指数幂。例如，`345.32` 被认为是 `3.4532 * 10²`。这本质上就是它们存储的方式：尾数、指数和符号。浮点数有三种类型：`float`、`double` 和 `long double`。大多数情况下你会使用 `double`，因为它提供了很好的精度。

![](img/a694739dec801cd745c57da9e19c2cd4_86_0.png)

# for 循环

while 循环是一种通用的循环结构，但 C 语言程序员经常使用相同的基本模式：

```
some initialization
while (some check) {
    some code
    some last step
}
```

因此，C 语言有一个捷径方法：for 循环。在 for 循环中，上述模式变变为：

```
for (some initialization; some check; some last step) {
    some code;
}
```

将程序修改为使用 for 循环：

```c
#include <stdio.h>

int main(int argc, const char * argv[]) {
    for (int i = 0; i < 12; i++) {
        printf("%d. Aaron is Cool\n", i);
    }
    return 0;
}
```

图 7.2 for 循环

![](img/a694739dec801cd745c57da9e19c2cd4_88_0.png)

注意，在这个简单的循环示例中，你使用循环来规定某事发生的次数。然而，更常见的是循环用于遍历集合项目，例如名称列表。例如，我可以修改此程序，将循环与朋友名称列表结合使用。每次循环，都会有一个不同的朋友变得“酷”。我们将从第 15 章开始学习更多关于集合和循环的内容。

## break

有时候有必要在循环内部停止循环的执行。例如，假设你想通过遍历正整数来寻找数字 $x$，其中 $x + 90 = x^2$。你的计划是遍历 0 到 11 的整数，并在找到解时跳出循环。修改代码：

```c
#include <stdio.h>

int main(int argc, const char *argv[]) {
    int i;
    for (i = 0; i < 12; i++) {
        printf("Checking i = %d\n", i);
        if (i + 90 == i * i) {
            break;
        }
    }
    printf("The answer is %d\n", i);
    return 0;
}
```

编译并运行程序。你应该看到：

- Checking i = 0
- Checking i = 1
- Checking i = 2
- Checking i = 3
- Checking i = 4
- Checking i = 5
- Checking i = 6
- Checking i = 7
- Checking i = 8
- Checking i = 9
- Checking i = 10
- The answer is 10.

注意，当调用 `break` 时，执行将直接跳转到代码块的末尾。

图 7.3 跳出循环

![](img/a694739dec801cd745c57da9e19c2cd4_90_0.png)

## continue

有时你会发现自己正处于代码块的中间，你需要说：“忘记这次代码块执行的剩余部分，开始下一次代码块执行。”这是通过 `continue` 命令实现的。例如，如果你很确定 3 的倍数满足该方程，你该如何避免浪费时间？

```c
#include <stdio.h>
int main(int argc, const char * argv[]) {
    int i;
    for (i = 0; i < 12; i++) {
        if (i % 3 == 0) {
            continue;
        }
        printf("Checking i = %d\n", i);
        if (i + 90 == i * i) {
            break;
        }
    }
    printf("The answer is %d\n", i);
    return 0;
}
```

编译并运行：

- Checking i = 1
- Checking i = 2
- Checking i = 4
- Checking i = 5
- Checking i = 7
- Checking i = 8
- Checking i = 10
- The answer is 10.

图 7.4 continue

![](img/a694739dec801cd745c57da9e19c2cd4_92_0.png)

## do-while 循环

没有孩子使用 do-while 循环，但为了完整备性，这里是它。do-while 循环在执行代码块之前不会检查表达式。因此，它确保代码块至少执行一次。如果你重写原始练习以使用 do-while 循环，它看起来会这样：

```c
int main(int argc, const char * argv[]) {
    int i = 0;
    do {
        printf("%d. Aaron is Cool\n", i);
        i++;
    } while (i < 12);
    return 0;
}
```

注意末尾的分号。与其他循环不同，do-while 循环实际上是一条语句：

```
do { something } while (something);
```

这是 do-while 循环的流程图：

图 7.5

![](img/a694739dec801cd745c57da9e19c2cd4_94_0.png)

## 挑战

写一个程序从 99 倒数计数到 0。但是，如果数字能被 5 整除，则打印“Found one!”。因此，输出应该是：

```
99
96
93
Found one
```

# 地址与指针

你的计算机核心是一个处理器（中央处理单元或 CPU）和一个巨大的开关数组（随机访问内存或 RAM），可以开启或关闭。我们说开关持有一个位的信息。你经常会看到 1 表示“开启”，0 表示“关闭”。这些开关组成了一个字节的信息。处理器可以获取这些开关的状态，进行操作，并将结果存储在另一个开关中。

图 8.1 内存与 CPU

![](a694739dec801cd745c57da9e19c2cd4_96_0.png)

内存是有编号的，我们通常谈论特定字节数据的地址。当人们谈论 32 位 CPU 或 64 位 CPU 时，他们通常是在谈论大小。64 位 CPU 可以处理比 32 位 CPU 多得内存。

## 获取地址

在 Xcode 中，创建一个名为 Addresses 的项目。变量的地址是存储该变量值的内存位置。要获取变量的地址，使用 `&` 运算符：

```c
#include <stdio.h>

int main(int argc, const char * argv[]) {
    int i = 17;
    printf("i stores its value at %p\n", i);
    return 0;
}
```

注意 `%p` 标记。你可以用内存地址替换它。编译并运行程序。你会看到类似：

i stores its value at 0xffff7

内存地址几乎总是以十六进制格式打印。在计算机中，一切都存储在内存中，因此所有东西都有地址。例如，函数位于某个特定地址。要获取该地址，你只需要使用函数名：

```c
int main(int argc, const char * argv[]) {
    int i = 17;
    printf("i stores its value at %p\n", i);
    printf("this function starts at %p\n", main);
    return 0;
}
```

## 在指针中存储地址

如果你想在变量中存储地址怎么办？你可以把它放进一个大小正确的无符号整数中，但当你为该变量指定类型时，编译器会帮助你发现错误。例如，如果你想要一个名为 ptr 的变量存放 float 的地址，你可以这样声明它：

```c
float *ptr;
```

我们说 ptr 是指向 float 的指针。它不存储 float 的值；它指向一个可能存储 float 的地址。

声明一个名为 addressOf 的新变量，它是 int 的指针。赋值 i 的地址。

```c
int main(int argc, const char *argv[]) {
    int i = 17;
    int *addressOf = &i;
    printf("stores its value at %p\n", addressOf);
    printf("this function starts at %p\n", main);
    return 0;
}
```

编译并运行程序。你应该没有看到行为上的变化。

我们现在使用整数是为了简单。但如果你在好奇指针有什么用，我理解你的想法。传递赋值给此变量的整数值和传递它的地址一样容易。然而，很快你的数据将比单个整数大得多且复杂。这就是我们传递地址的原因。

## 获取地址处的数据

如果你有一个地址，可以使用 `*` 运算符获取那处的数据。

```c
#include <stdio.h>

int main(int argc, const char * argv[]) {
    int i = 17;
    int *addressOf = &i;
    printf("%s stores its value at %p\n", addressOf);
    printf("this function starts at %p\n", main);
    printf("the int stored at addressOf is %d\n", *addressOf);
    return 0;
}
```

注意星号有两种不同的用法。第一种是在声明中，你声明变量 `addressOf` 为 `int *`。也就是说，它是指向一个可以存储 `int` 的地方的指针。

第二是你读取存储在 `addressOf` 地址中的 int 值（指针也称为引用。因此，使用指针读取数据有时被称为解引用指针）。

你也可以在赋值的左侧使用 `*` 运算符在特定地址存储数据：

```c
int main(int argc, const char * argv[]) {
    int i = 17;
    int *addressOf = &i;
    printf("%s stores its value at %p\n", addressOf);
    *addressOf = 89;
    printf("Now i is %d\n", i);
    return 0;
}
```

编译并运行你的程序。



现在让我们犯一个常见的编程错误。删除 `main()` 函数第四行的 `*`，使代码变为：

```
addressOf = 89;
```

注意 Xcode 弹出一个警告，显示“Incompatible integer to pointer conversion assigning to 'int*' to 'int'”。请修复此问题。

## 多少字节？

鉴于一切都存储在内存中，而且你现在知道如何找到数据开始的地址，那么下一个问题是：“这个数据类型消耗了多少字节？”

使用 `sizeof()` 你可以找到数据类型的大小。例如，

```c
int main(int argc, const char * argv[]) {
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at %p\n", addressOfI);
    *addressOfI = 89;
    printf("How is i %zu bytes\n", sizeof(int));
    printf("A pointer is %zu bytes\n", sizeof(int *));
    return 0;
}
```

我们在 `printf()` 的调用中看到了另一个新标记：`%zu`。`sizeof()` 函数返回一个类型为 `size_t` 的值，`%zu` 是正确的占位符标记。这在实际开发中并不常见。

编译并运行程序。如果你的指针长度为 4 字节，则你的程序正在 32 位模式下运行。如果你的指针长度为 8 字节，则你的程序正在 64 位模式下运行。

`sizeof()` 也接受变量作为参数，所以你可以这样写程序：

```c
int main(int argc, const char * argv[]) {
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at %p\n", addressOfI);
    *addressOfI = 89;
    printf("Now is i %zu bytes\n", sizeof(i));
    printf("A pointer is %zu bytes\n", sizeof(addressOfI));
    return 0;
}
```

## NULL

有时你需要一个指向“无”的指针。也就是说，你有一个可以存储地址的变量，你想在其中存储某些东西，以明确表示该变量没有被赋值任何内容。我们使用 NULL 来实现：

```c
float *myPointer;
// 现在将 myPointer 设置为 NULL，稍后会在程序的后面在那里存储一个指针
myPointer = NULL;
```

NULL 是什么？记住，地址只是一个数字。NULL 是零。这在 `if` 语句中非常有用：

```c
float *myPointer;
// myPointer 是否已经赋值？
if (myPointer) {
  // myPointer 不是 NULL
  // 对 myPointer 指向的数据进行某些操作...
} else {
  // myPointer 是 NULL
}
```

稍后当我们讨论指向对象的指针时，我们将使用 `nil` 代替 `NULL`。它们是等价的，但 Objective-C 程序员使用 `nil` 来表示没有对象存在的地址。

## 优雅的指针声明

当你声明一个指向 float 的指针时，它看起来像这样：

```c
float *powerPtr;
```

由于类型是一个指向 float 的指针，你可能想这样写：

```c
float *powerPtr;
```

这是可以的，编译器允许你这样做。然而，优雅的程序员不会这样做。

为什么？你可以在同一行中声明多个变量。例如，如果我想声明变量 x、y 和 z，我可以这样做：

```c
float x, y, z;
```

每一个都是 float。

你认为这些是什么？

```c
float *b, c;
```

惊喜吧！b 是一个指向 float 的指针，但 c 只是一个 float。如果你想让它们都是指针，你必须在每一个前面加上一个 `*`：

```c
float *b, c;
```

将 `*` 直接紧贴变量名会让这更清晰。

## 挑战

编写一个程序，显示一个 float 消耗了多少内存。

在你的 Mac 上，`short` 是一个 2 字节整数，使用一个位来存储符号（正或负）。它能存储的最小数字是多少？最大数字是多少？`unsigned short` 只存储非负数。它能存储的最大数字是多少？

## 引用传递 (Pass By Reference)

有一个标准的 C 函数叫做 `modf()`。你给 `modf()` 一个 `double`，它会计算该数字的整数部分和小数部分。例如，如果你给它 3.14，3 是整数部分，0.14 是小数部分。

作为 `modf()` 的调用者，你想要这两个部分。然而，一个 C 函数只能返回一个值。`modf()` 如何给你这两部分信息呢？

当你调用 `modf()` 时，你会提供一个地址，让它可以在那里存放其中一个数字。特别地，它将返回小数部分，并将整数部分复制到你提供的地址。创建一个新项目：名为 PBR 的 C 命令行工具。

编辑 `main.c`：

这被称为引用传递。也就是说，你提供一个地址（也称为“引用”），函数将数据放在那里。

图 9.1 modf() 返回时的栈

| modf() | toConvert = 3.14 |
| :--- | :--- |
| | integerPtr = |
| main() | pi = 3.14 |
| | integerPart = 3.00 |
| | fraction = 0.14 |

## 引用传递

描述点有两种常用方法：笛卡尔坐标系和极坐标系。在笛卡尔坐标系中，`(x, y)` 表示你的位置。在极坐标系中，`(r, theta)` 表示半径和角度。

图 9.2 极坐标与笛卡尔坐标系 (https://www.example.com/image9.2.png)

等待，

笛卡尔坐标系中 `(x, y)` 表示你的位置。在极坐标系中 `(r, theta)` 表示半径和角度。

图 9.2 极坐标与笛卡尔坐标系 (https://www.example.com/image9.2.png)

[108]

## 避免解引用 NULL

有时一个函数可以通过引用提供许多值，但你可能只关心其中一些。当你不想使用它们时，如何避免声明这些变量并传递它们的地址？通常，传递 NULL 作为地址告诉函数“我不需要这个特定的值”。

这意味着在解引用指针之前，你应该始终检查它们是否非空。在以下代码中添加这些检查：

```c
void cartesianToPolar(float x, float y, double *rPtr, double *thetaPtr)
{
    // RPtr 是否非空？
    if (rPtr) {
        // 在提供的地址中存储半径
        *rPtr = sqrt(x * x + y * y);
    }

    // thetaPtr 是否为 NULL？
    if (!thetaPtr) {
        // 跳过函数的剩余部分
        return;
    }
    ...
}
```

## 结构体

有时候，你需要一个变量来保存多个相关的数据块。例如，假设你正在编写一个计算人体体重指数（BMI）的程序。（你的 BMI 是多少？它是以公斤为单位的体重除以米为单位的身高的平方。BMI 低于 20 表示可能体重不足。BMI 超过 30 表示可能肥胖。这是一个衡量个人健康状况非常不精确的工具，但它是一个很好的编程示例。）对于你的目的来说，一个人由一个代表身高（米）的浮点数和一个代表体重（公斤）的整数组成。

现在你将创建自己的 `Person` 类型。`Person` 类型的变量将是一个结构体，有两个成员：一个名为 `heightInMeters` 的浮点数和一个名为 `weightInKilos` 的整数。

创建一个新项目：一个名为 `BMICalc` 的 C 命令行工具。编辑 `main.c` 以创建一个包含人员所需数据的结构体：

```c
#include <stdio.h>

// Here is the declaration of the struct Person
struct Person {
    float heightInMeters;
    int weightInKilos;
};

int main(int argc, char * argv[]) {
    struct Person person;
    person.weightInKilos = 96;
    person.heightInMeters = 1.8;
    printf("person weighs %d kilograms\n", person.weightInKilos);
    printf("person is %.2f meters tall\n", person.heightInMeters);
    return 0;
}
```

注意，你可以使用句号 `.` 来访问结构体的成员。

这里是结构体成员赋值后 `main()` 的框架。



## 图 10.1 成员赋值后的框架

## main()

| struct Person |
| :--- |
| person = weightInKilos = 96 heightInMeters = 1.8 |

在大多数情况下，你会反复使用同一个结构体声明。因此，为结构体类型创建一个 `typedef` 是很常见的。`typedef` 为类型声明定义别名，并允许我们更像使用普通数据类型一样使用它。修改 `main.c` 以为 `struct Person` 创建并使用 `typedef`：

```c
#include <stdio.h>

// Here is the declaration of the type Person
typedef struct {
    float heightInMeters;
    int weightInKilos;
} Person;

int main(int argc, const char * argv[]) {
    Person person;
    person.weightInKilos = 96;
    person.heightInMeters = 1.8;
    printf("person weighs %i kilograms\n", person.weightInKilos);
    printf("person is %.2f meters\n", person.heightInMeters);
    return 0;
}
```

现在你已经创建了 `typedef`，可以将 `Person` 结构体传递给另一个函数。添加一个命名的 `bodyMassIndex()` 函数，它接受一个 `Person` 作为参数并计算 BMI。然后更新 `main()` 调用它：

```c
#include <stdio.h>

typedef struct _Person {
    float heightInMeters;
    int weightInKilos;
} Person;

float bodyMassIndex(Person p) {
    return p.weightInKilos / (p.heightInMeters * p.heightInMeters);
}

int main(int argc, const char * argv[]) {
    Person person;
    person.weightInKilos = 96;
    person.heightInMeters = 1.8;
    float bmi = bodyMassIndex(person);
    printf("person has a BMI of %.2f\n", bmi);
    return 0;
}
```

## 挑战

我作为程序员处理的第一个结构体是 `struct tm`，标准 C 库用它来存储分解为组件的时间。该结构体定义如下：

```c
struct tm {
    int tm_sec;      /* 分后的秒 [0-60] */
    int tm_min;      /* 小后的分 [0-59] */
    int tm_hour;     /* 自午夜以来的小时 [0-23] */
    int tm_mday;      /* 月日 [1-31] */
    int tm_mon;       /* 自1月以来的月份 [0-11] */
    int tm_year;      /* 自1900年以来的年份 */
    int tm_wday;      /* 自周日以来的几天 [0-6] */
    int tm_yday;      /* 自1月1日以来的几天 [0-365] */
    int tm_isdst;     /* 夏令时标志 */
    long tm_gmtoff;   /* UTC偏移量（秒） */
    char *tm_zone;   /* 时区缩写 */
};
```

`time()` 函数返回自1970年英国格尼治第一刻以来的秒数。`localtime_r()` 可以读取该持续时间并填充 `struct tm` 的适当值。（它实际上接收自1970年以来秒数的地址以及一个 `struct tm` 的地址。）

将当前时间以 `struct tm` 形式给出如下所示：

```c
long secondsSince1970 = time(NULL);
printf("It has been %ld seconds since 1970\n", secondsSince1970);

struct tm now;
localtime_r(&secondsSince1970, &now);
```

# 对象

许多计算机语言都有*对象*（objects）的概念。对象类似于结构体，因为它持有数据。然而，与结构体不同，对象还包含一组作用于这些数据的函数。要触发其中一个函数，你向对象发送一条*消息*（message）。用更准确的术语来说，一个由消息触发的函数被称为*方法*（method）。

在 20 世纪 80 年代初，Brad Cox 和 Tom Love 决定在 C 语言中引入面向对象的思想。对于对象，他们基于在堆（heap）上分配的想法，并添加了消息发送语法。结果就是 Objective-C 语言。

对象本质上是非常“活跃”的。它们会执行工作并接收有关它们正在工作的消息。一个复杂的 Objective-C 程序可能同时在内存中拥有数百个对象，它们都在执行工作并互相发送消息。

*类*（class）描述了一种特定类型的对象。这种描述包含了方法和*实例变量*（instance variables），该类型的对象在其中存储其数据。你请求一个类在堆上为你创建一个该类型的对象。我们称生成的对象是该类的*实例*（instance）。

例如，iPhone 自带了许多类，其中之一是 `CLLocation`。你可以请求 `CLLocation` 类创建一个 `CLLocation` 的 `instance`。在这个 `CLLocation` 对象内部有几个实例变量，存储着位置数据，如经度、纬度和高度。该对象还有几个方法。例如，你可以询问一个 `CLLocation` 实例距离另一个 `CLLocation` 对象有多远。

## 创建并使用你的第一个对象

现在你将创建第一个 Objective-C 程序。创建一个新项目：Command Line Tool（命令行工具），但不要选 C，而是将其类型设置为 Foundation。将其命名为 TimeAfterTime。

图 12.1 创建 Foundation 命令行工具

![](img/a694739dec801cd745c57da9e19c2cd4_120_0.png)

包含 Objective-C 代码的文件通常以 .m 为后缀。找到并打开 `main.m`，输入以下两行代码：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSDate *now = [NSDate date];
        NSLog("%@ the new date lives at %@", now);
    }
    return 0;
}
```

漂亮！这是你第一次发送消息。你向 `NSDate` 类发送了 `date` 消息。`date` 方法请求 `NSDate` 类创建一个 `NSDate` 实例，将其初始化为当前日期/时间，并返回新对象起始的地址。然后你将返回的地址存储在变量 `now` 中。这个变量是一个指向 `NSDate` 对象的指针。

`NSLog()` 是一个 Objective-C 函数，与 `printf()` 不同；它接受一个格式化字符串，将 % 标记替换为实际值，并写入控制台。然而，它的格式字符串始终以 @ 开头，且末尾不需要 \n。

构建并运行该程序。你应该看到类似的内容：

2011-08-05 11:53:54.366 TimeAfterTime(4862:707) The new date lives at 0x100114dc00

与 `printf()` 不同，`NSLog()` 会在输出前加上日期、时间、程序名和进程 ID（process ID）。从现在起，当我显示 `NSLog()` 的输出时，我会跳过这些数据——页面太窄了。

在 `NSLog()` 中，`%p` 打印出对象的位置。要打印更像的内容，你可以使用 `%@`，它请求对象将自己描述为字符串：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSDate *now = [NSDate date];
        NSLog("@The date is %@", now);
    }
    return 0;
}
```

现在你应该看到类似的内容：

The date is 2011-08-05 16:09:14 +0000

## 消息剖析

消息发送总是被方括号括起来，并且它至少包含两个部分：

- 指向接收消息的对象的指针
- 要触发的方法名称

消息发送（类似于函数调用）也可以带有参数。`NSDate` 对象表示特定的日期和时间。`NSDate` 的实例可以告诉你日期/时间与 1970 年 1 月 1 日凌晨 12:00 (GMT) 之间的差（秒）。通过向指向的 `NSDate` 对象发送 `timeIntervalSince1970` 消息来提问这个问题：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSDate *now = [NSDate date];
        NSLog(@"the date is %@", now);
        double seconds = [now timeIntervalSince1970];
        NSLog(@"It has been %f seconds since the start of 1970.", seconds);
    }
    return 0;
}
```

现在你需要一个新的日期——比你现有日期晚 100000 秒的日期。`NSDate` 类有一个方法 `dateAddingInterval:`。你可以向原始对象发送此消息来获取新日期。该方法接受一个参数：要增加的秒数。在你的 `main()` 函数中使用它创建一个新日期：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSDate *now = [NSDate date];
        NSLog(@"the date is %@", now);
        double seconds = [now timeIntervalSince1970];
        NSLog(@"It has been %f seconds since the start of 1970.", seconds);

        NSDate *later = [now dateAddingInterval:100000];
        NSLog(@"100000 seconds it will be %@", later);
    }
    return 0;
}
```

在消息发送 `[now dateAddingInterval:100000]` 中，

- `now` 是指向接收消息对象的指针（也称为“接收者”）
- `dateAddingInterval:` 是方法名（也称为“选择器”）
- `100000` 是唯一的参数

## 图 12.2 消息发送

![](img/a694739dec801cd745c57da9e19c2cd4_123_0.png)

## 内存中的对象

图 12.3 是一个对象图。它显示了堆上的两个 `NSDate` 实例。变量 `now` 和 `later` 属于 `main()` 帧。它们指向 `NSDate` 对象，所示。

图 12.3 TimeAfterTime

![](img/a694739dec801cd745c57da9e19c2cd4_124_0.png)

## 更多消息

在上一章中，你发送了几个消息。让我们再次查看你发送这些消息并触发相应方法的行：

`NSDate *now = [NSDate date];`

我们说 `date` 方法是一个类方法。也就是说，你通过向 `NSDate` 类发送消息来执行该方法。`date` 方法返回指向 `NSDate` 实例的指针。

`double seconds = [now timeIntervalSince1970];`

我们说 `timeIntervalSince1970` 是一个实例方法。你通过向类的实例发送消息来执行该方法。`timeIntervalSince1970` 方法返回一个 double。

## id

在声明持有对象的指针时，大多数情况下你会指定对象的类：

```objc
NSDate *expiration;
```

然而，通常你不需要确切知道指针指向什么类型的对象。在这种情况下，我们使用类型 `id` 来表示“指向某种 Objective-C 对象的指针”。使用它时如下：

```objc
id delegate;
```

注意这个声明中没有星号。`id` 隐含了星号。

类、对象、消息和方法的思想在刚开始可能很难理解。如果你对对象感到有些不确定，不要担心。这只是一个开始。你将反复使用这些模式，它们在你每次使用它们时都会变得更清晰。

## 挑战

使用两个 `NSDate` 实例来计算你已经活了多少秒。提示：这里是从年、月、日等创建新日期的方法：

```objc
NSDateComponents *comps = [[NSDateComponents alloc] init];
[comps setYear:1969];
[comps setMonth:4];
[comps setDay:30];
[comps setHour:13];
[comps setMinute:10];
[comps setSecond:0];

NSCalendar *g = [[NSCalendar alloc] initWithCalendarIdentifier:NSCalendarIdentifierGregorian];
NSDate *dateOfBirth = [g dateFromComponents:comps];
```

要获取两个 `NSDate` 实例之间的秒数，使用 `timeIntervalSinceDate:` 方法：



```objc
double d = [laterDate timeIntervalSinceDate:earlierDate];
```

## 嵌套消息发送

有一个类方法 `alloc`，它返回一个指向新对象的指针，该对象需要初始化。然后该指针被用于向新对象发送消息 `init`。使用 `alloc` 和 `init` 是 Objective-C 中创建对象最常用的方式。通过嵌套消息发送，在一行代码中发送这两个消息是一个良好的习惯（也是 Apple 认可的唯一方法）：

```
[[NSDate alloc] init];
```

系统会先执行内部的消息，然后执行包含这些内部消息的消息。因此，`alloc` 被发送给 `NSDate` 类，而该操作的结果（即一个指向新创建的实例的指针）随后被发送了 `init` 消息。`init` 返回一个指向该新对象的指针（这几乎总是来自 `alloc` 返回的那个指针），因此我们可以使用 `init` 的返回值进行赋值。尝试通过修改这一行，在你的代码中测试这些嵌套消息：

```
NSDate *now = [[NSDate date];
```

to

```
NSDate *now = [[NSDate alloc] init];
```

## 多参数

某些方法接受多个参数。例如，一个 `NSDate` 对象并不知道现在是哪一天。如果你需要这些信息，将使用 `NSCalendar` 对象。告诉你是几号的方法有三个参数。创建 `NSCalendar` 对象并在 `main` 中使用它：

```objc
#import <Foundation/Foundation.h>
int main(int argc, const char *argv[]) {
    @autoreleasepool {
        NSDate *now = [[NSDate alloc] init];
        NSLog(@"The date is %@", now);
        double seconds = [now timeIntervalSince1970];
        NSLog(@"It is %f seconds since the start of 1970.", seconds);
        NSDate *later = [now dateByTimeInterval:100000];
        NSLog(@"In 100,000 seconds it will be %@", later);

        NSCalendar *cal = [NSCalendar currentCalendar];
        NSInteger day = [cal component:NSDayUnit
                            in:NSMonthUnit
                            for:now];
        NSLog(@"This is day %ld of the month", day);
    }
    return 0;
}
```

该方法的名为 `component:in:for:`，它接受三个参数。你可以看出消息被拆分成了三行。这没关系；编译器并不介意额外的空格。Objective-C 程序员通常使用冒号，这样很容易将方法名的部分与参数区分开。（Xcode 应该为你完成这一点：每当你开始新的一行时，前一行应该正确缩进。）该方法的第一个和第二个参数是常量 `NSDayUnit` 和 `NSMonthUnit`。这些常量定义在 `NSCalendar` 类中。它们告诉方法你想知道该月份内是哪一天。第三个参数是你想要查询的日期。如果你想知道一年的第几小时而不是月份的某一天，你会使用这些常量：

```
NSInteger hour = [cal component:NSHourUnit in:NSYearUnit for:now];
```

## 向 nil 发送消息

几乎所有的面向对象的语言都有 nil 的概念，即指向无对象的指针。在 Objective-C 中，nil 是零指针（与 `NULL` 相同，这在第 8 章中讨论过）。在大多数面向对象的语言中，向 nil 发送消息是不允许的。因此，你必须在访问对象之前检查它是否为 nil。所以你会经常看到这样的代码：

```
if (fido != nil) {
  [fido speak];
}
```

在设计 Objective-C 时，人们决定向 nil 发送消息是可以接受的；它只是什么都不做。因此，这段代码是完全合法的：

```
Dog *fido = nil;
[fido speak];
```

重要事项 #1：如果你正在发送消息但什么都没有发生，请确保你没有向一个已被设置为 nil 的指针发送消息。

重要事项 #2：如果你向 nil 发送消息，返回值没有任何意义。

```
Dog *fido = nil;
NSString *daily = [fido speak];
```

在这种情况下，`daily` 将是 0。（通常情况下，如果你期望结果是数字或指针，向 nil 发送消息将返回 0。然而，对于结构体等类型，你将得到奇怪且意外的返回值。）

## 挑战

在你的 Mac 上，有一个类 `NSTimeZone`。在它的许多方法中，有一个类方法 `systemTimeZone`，返回你电脑的时区（作为 `NSTimeZone` 的实例），以及一个实例方法 `isDaylightSavingTime`，如果时区当前处于夏令时间，它返回 YES。

编写一个 Foundation 命令行工具，用来告诉你现在是否是夏令时间。

## NSString

`NSString` 是另一个 Objective-C 程序员经常使用的类。`NSString` 的实例持有字符字符串。在代码中，你可以创建一个 `NSString` 的字面量实例：

```
NSString *lament = @"Why me!";
```

在 Time 项目中，你输入：

```
NSLog(@"The date is %@", now);
```

`NSLog` 是一个 Objective-C 函数（而不是方法！）它的工作原理类似于 `printf()`。在 `NSLog()` 中，格式字符串是 `NSString` 的实例。`NSString` 的实例可以使用 `stringWithFormat:` 类方法创建：

```
NSString *x = [NSString stringWithFormat:@"The number is %d", 5];
```

获取字符串中的字符数量，可以使用 `length` 方法：

```
NSInteger charCount = [x length];
```

你可以使用 `isEqual:` 方法检查两个字符串是否相等：

```
if ([lament isEqual:x])
    NSLog(@"%@ and are equal", x);
```

C 语言也有字符串构造。这里是 C 语言的示例：

```c
char *lament = "Why me!";
char *x;
printf("The number is %lu\n", strlen(lament));
if (strcmp(lament, x) == 0)
    printf("%s and %s are equal\n", lament, x);
```

## 挑战

有一个类叫 `NSHost`，包含了关于你电脑的信息。要获取 `NSHost` 的实例，可以使用 `NSHost` 类方法 `currentHost`。该方法返回一个指向 `NSHost` 对象的指针：

```
+ (NSHost *)currentHost;
```

要获取电脑的本地化名称，可以使用 `NSHost` 实例方法 `localizedName`，它返回一个指向 `NSString` 对象的指针：

```
- (NSString *)localizedName;
```

编写一个命令行工具。

## NSArray

就像 `NSString` 一样，`NSArray` 是另一个 Objective-C 程序员经常使用的类。`NSArray` 的实例持有指针的列表。例如，假设你想创建一个三个 `NSDate` 对象的列表，然后遍历列表并打印每个日期。

创建一个新项目：一个名为 DateList 的 Foundation 命令行工具。打开 `main.m` 并修改 `main()` 函数：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char *argv[]) {
    @autoreleasepool {
        // 创建三个 NSDate 对象
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateAddingTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateAddingTimeInterval:-24.0 * 60.0 * 60.0];

        // 创建包含这三个对象的数组（nil 终止列表）
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

        // 有多少日期？
        NSLog(@"There are %lu dates", [dateList count]);

        // 打印几个
        NSLog(@"The first date is %@", [dateList objectAtIndex:0]);
        NSLog(@"The third date is %@", [dateList objectAtIndex:2]);
    }
    return 0;
}
```

`NSArray` 有两个在示例中所示的方法，你会经常使用：

- `count` 返回数组中的项目数量
- `objectAtIndex:` 返回数组在参数指定的索引处存储的指针。

数组是有序的，你通过索引访问数组中的项。数组是基于零索引的：第一个项存储在索引 0，第二个项存储在索引 1，以此类推。因此，如果 `count` 方法显示数组中有 100 个项，你可以使用 `objectAtIndex:` 来请求索引从 0 到 99 的对象。

## 图 15.1 DateList 的对象图

![](img/a694739dec801cd745c57da9e19c2cd4_136_0.png)

因此，如果你想循环并处理数组中的每个项（或“遍历数组”），你可以创建一个 `for` 循环。编辑 `main.m`：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // Create NSDate objects
        NSDate *now = [NSDate dateAddingTimeInterval:-24.0 * 60.0];
        NSDate *tomorrow = [now dateAddingTimeInterval:24.0 * 60.0];
        NSDate *yesterday = [now dateAddingTimeInterval:-24.0 * 60.0];

        // Create an array containing all three (nil terminates the list)
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

        NSInteger dateCount = [dateList count];
        for (int i = 0; i < dateCount; i++) {
            NSDate *d = [dateList objectAtIndex:i];
            NSLog(@"Here is a date: %@", d);
        }
        return 0;
    }
}
```

程序员经常进行这种操作，以至于为 `for` 循环添加了专门遍历数组的扩展。修改代码使用这种机制：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // Create three NSDate objects
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateByTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateByTimeInterval:-24.0 * 60.0 * 60.0];

        // Create an array containing all three (nil terminates the list)
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, yesterday, nil];

        for (NSDate *date in dateList) {
            NSLog(@"Here is a date: %@", date);
        }
    }
    return 0;
}
```

这种类型的循环被称为快速枚举，它是遍历数组中项的一种极其高效的方法。有一个限制：在对数组枚举时，你不能向数组中添加或删除元素。

## NSMutableArray

数组有两种类型：

- `NSArray` 实例是通过指针列表创建的。你永远无法从该数组中添加或删除指针。
- `NSMutableArray` 实例与 `NSArray` 实例相似，但你可以添加和删除指针。(`NSMutableArray` 是 `NSArray` 的子类。更多关于子类的信息请见第 18 章。)

修改你的示例以使用 `NSMutableArray` 实例和 `NSMutableArray` 类的方法：

```objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // Create three Date objects
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateAddingTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateAddingTimeInterval:-24.0 * 60.0 * 60.0];

        // Create an empty array
        NSMutableArray *dateList = [NSMutableArray array];

        // Add the dates to the array
        [dateList addObject:now];
        [dateList addObject:tomorrow];

        // Put yesterday at the beginning of the list
        [dateList insertObject:yesterday atIndex:0];

        for (NSDate *d in dateList) {
            NSLog(@"Here is a date: %@", d);
        }

        // Remove yesterday
        [dateList removeObjectAtIndex:0];
        NSLog(@"Now the first date is %@", [dateList objectAtIndex:0]);

    }

    return 0;
}
```

## 挑战

创建一个名为 Groceries 的新 Foundation 命令行工具。从创建一个空的 `NSMutableArray` 对象开始。然后向数组中添加几个类似杂货的项（你也需要创建它们）。最后，使用快速枚举打印出你的购物列表。

下一个挑战确实更有挑战性。阅读以下程序，它会寻找包含两个相邻 A 的常用专有名词。



```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        // Read in a file as a huge string (ignoring the possibility of an error)
        NSString *nameString = [NSString stringContentsOfFile:@"/usr/share/dict/propernames"
                                encoding:NSUTF8StringEncoding
                                error:NULL];

        // Break it into an array of strings
        NSArray *names = [nameString componentsSeparatedByString:@""];
        for (NSString *n in names) {
            // Look for "AA" in case-insensitive manner
            NSRange r = [n rangeOfString:@"AA" options:NSCaseInsensitiveSearch];
            if (r.location != NSNotFound) {
                NSLog("%@", n);
            }
        }
    }
    return 0;
}
```

## 第 25 章

它是 Foundation 框架的一部分，并随着每个版本的 Mac OS X 和每个版本的 iOS 发布。

在头文件的末尾，有一份指南列表，讨论了展示 `NSArray` 能力的 `NSArray` 示例代码。点击“Collections Programming Topics”（集合编程主题）来打开该指南。

## 图 16.3 集合编程主题

![](img/a694739dec801cd745c57da9e19c2cd4_144_0.png)

本特定指南讨论了集合类（包括 `NSArray` 和 `NSMutableArray`）。与类引用（class reference）不同，指南是需要阅读的材料，它以合理的顺序引入了概念。

现在使用文档窗格顶部的返回按钮回到 `NSArray` 引用页面。好奇你还可以向 `NSArray` 发送哪些消息吗？滚动引用页面并找到 `NSArray` 实现的方法列表。假设你想找一种方法检查数组是否包含某个特定项目。在这种情况下，你会遇到 `containsObject:` 方法并阅读其描述：

## 图 16.4 containsObject 的引用

### containsObject:

返回一个布尔值，表示给定对象是否存在于数组中。

```objc
- (BOOL)containsObject:(id)anObject
```

#### 参数

`anObject`
一个对象。

#### 返回值

如果 `anObject` 存在于数组中返回 `YES`，否则返回 `NO`。

#### 讨论

此方法通过向数组的每个对象发送 `isEqual:` 消息（并将 `anObject` 作为参数传递给每个 `isEqual:` 消息）来确定 `anObject` 是否存在于数组中。

#### 可用性

适用于 Mac OS X v10.0 及更高版本。

#### 另见

- `indexOfObject:`
- `indexOfObjectIdenticalTo:`

#### 相关示例代码

Sketch+Accessibility, TimelineToTC

#### 声明于

`NSArray.h`

现在你已经了解了在代码中发送此消息所需的所有知识。

## 快速帮助

但有一种更简单的方法可以从编写代码的编辑器跳转到文档中的知识源。关闭 Organizer（组织器）并返回你的 DateList 项目。

在 `main.m` 中，找到包含 `[dateList addObject:now]` 的那行。按住 Option 键并点击 `addObject:`。快速帮助窗口将出现并显示有关该方法的信息：

```objc
// Create three Date objects
Date *now = [NSDate date];
Date *tomorrow = [now dateByAddingTimeInterval:24];
Date *yesterday = [now dateByAddingTimeInterval:-24];
// Create an array
NSMutableArray *dateList = [NSMutableArray array];
// Add the dates to the array
[dateList addObject:now];
[dateList addObject:tomorrow];
```

```
addObject:
Name: addObject
Declaration: (void)addObject:(id)addObject
Availability: Mac OS X (10.0 and later)
Abstract: 将给定对象插入到数组末尾。
Parameters: addObject: 要添加到数组内容末尾的对象。
Declared in: NSMutableArray
Reference: NSMutableArray Class Reference
Related Documents: Collections Programming Topics, Key-Value Coding Programming Guide
```

注意快速帮助窗口中存在链接。如果你点击链接，它将在 Organizer 中打开相应的文档。很有用对吧？

如果你想一直看到快速帮助，可以将其作为一个窗格在 Xcode 中打开。

在 Xcode 窗口的右上角，找到一个名为 View（视图）的分段控件，它看起来并指示了 Xcode 的左侧、底部和右侧窗格。选择和取消选择这些按钮将隐藏和显示相应的窗格。

你现在已经经常使用的左侧窗格，被称为 navigator（导航器）；你也过的底部窗格包含了控制台，被称为 debug area（调试区域）。右侧窗格被称为 Utilities（工具）。点击右侧的 View 按钮以显示 Utilities。在 Utilities 顶部，点击按钮显示 Quick Help（快速帮助）窗格。

此窗格将为编辑器中选中的文本提供帮助。尝试：只需在编辑器中选择单词 "NSMutableArray"

## 图 16.6 快速帮助窗格

![](img/a694739dec801cd745c57da9e19c2cd4_147_0.png)

注意，当你选择其他内容时，快速帮助窗格将立即更新以显示新选择的文档。

## 其他选项和资源

如果你对任何文本进行 Option-双击，Organizer 将搜索该字符串。

如果你对任何类、函数或方法进行 Command-点击，Xcode 将向你显示其定义的文件。（尝试 Command-点击“NSMutableArray”一词）。

## 图 16.7 NSMutableArray 的声明

![](img/a694739dec801cd745c57da9e19c2cd4_148_0.png)

如果有多个匹配的声明，当你 Command-点击时会弹出一个窗口。尝试 Command-点击 `addObject:`。

Xcode 有时会回溯母服务器检查是否有任何更新的文档。它将下载更新并对它们进行重新索引以便搜索。你可以在 Xcode 的偏好设置面板中触发立即更新。

Apple 在 http://lists.apple.com/ 托管了一系列讨论邮件列表，其中有几个致力于开发者主题。如果你在文档中找不到答案，请尝试搜索列表的存档。

还有一个你应该知道的另一个资源：stackoverflow.com。这是一个程序员提问和回答问题的非常流行的地方。

## 你的第一个类

到目前为止你只使用了实例变量。现在你可以编写方法了。

要创建一个新项目，选择 File → New → Project... 从 Mac OS X 选择 Cocoa 并选择 Command Line Tool。将类命名为 Person 并使其成为 `NSObject` 的子类。最后，确保勾选了 target 并点击 Save。

注意新的类文件 `Person.h` 和 `Person.m` 现在出现在项目导航器中。打开 `Person.h`。声明实例变量和方法：

```objc
#import <Foundation/Foundation.h>
// 类继承所有的实例变量
// 和方法
@interface Person : NSObject {
// 它有两个实例变量
    float heightMeters;
    int weightKilos;
}
```

注意你将实例变量放在大括号内，将方法放在大括号外。对于编译器来说，这段代码表示“我正在定义一个名为 Person 的类，它拥有 `NSObject` 的所有方法和实例变量。此外，我增加了实例变量：名为 `heightMeters` 的 float 和名为 `weightKilos` 的 int。我还将添加三个实例方法，它们将在 `Person.m` 中实现。”

注意 `setHeightMeters` 需要一个 float 参数且没有返回值，`setWeightKilos` 需要一个 int 参数且没有返回值，`bodyMassIndex` 无参数并返回 float。

现在打开 `Person.m`。删除现有的方法并实现你声明的方法：

```objc
#import "Person.h"

@implementation Person

- (void)setHeightMeters:(float)h
{
    heightMeters = h;
}
- (void)setWeightKilos:(int)w
{
    weightKilos = w;
}
- (float)bodyMassIndex
{
    // 此方法计算体重指数；
    return (float)weightKilos / (heightMeters * heightMeters);
}
@end
```

注意 Xcode 为你导入了 `Person.h`。还要注意，你实现的方法名称必须与你在头文件中声明的完全匹配。在 Xcode 中，这很容易；当你开始在实现文件中输入方法时，Xcode 会建议你已经声明的方法。

现在你已经实现了在 `Person.h` 中声明的所有方法，你的类已经完善了。编辑 `main.m` 来练习一下：

```objc
#import <Foundation/Foundation.h>
#import "Person.h"

int main(int argc, const char * argv[])
{
    // 创建 Person 的实例
    Person *person = [[Person alloc] init];

    // 给实例变量赋予一些有趣的值
    [person setWeightKilos:96];
    [person setHeightMeters:1.8];

    // 调用 bodyMassIndex 方法
    float bmi = [person bodyMassIndex];
    NSLog(@"person has a BMI of %f", bmi);

    return 0;
}
```

编译并运行程序。注意你导入了 `Person.h`，这样编译器在 `main()` 使用这些方法之前就已经知道它们是如何声明的。

## 图 17.1 BMITime 的对象图

| main() | Person |
| --- | --- |
| person | weightInKilos = 96 |
| | heightMeters = 1.8 |
| | - (float)bodyMassIndex |

## 访问方法

注意，当我们使用结构体（structs）而不是对象进行同样的练习时，我们直接在 `main()` 中访问了结构的数据成员：

```objc
person.weightInKilos = 96;
person.heightInMeters = 1.8;
```

在面向对象的思维中，我们尽力让对象的实例变量保持私有；也就是说，它们只由对象本身感知和访问。然而，由于我们想让 `Person` 外部的方法和函数能够设置人的体重和身高，我们创建了 `setWeightInKilos:` 和 `setHeightInMeters:` 方法。我们称这些方法为 setter 方法（设置方法）。

setter 方法允许其他方法设置实例变量的值。getter 方法（获取方法）允许其他方法读取实例变量的值。setter 和 getter 方法也称为访问方法（accessor methods），或直接称为访问器（accessors）。

在 `Person.h` 中添加 getter 方法的声明：

```objc
#import <Foundation/Foundation.h>
@interface Person : NSObject
{
    float heightInMeters;
    int weightInKilos;
}
// 你将能够设置这些实例变量
- (float)heightInMeters;
- (void)setHeightInMeters:(float)h;
- (int)weightInKilos;
- (void)setWeightInKilos:(int)w;
- (float)bodyMassIndex;
@end
```

你可能会奇怪，为什么 getter 方法的名字没有包含 `get` 以匹配 setter 方法的名字。这是一种 Objective-C 的命名规范。读取实例变量的方法名直接就是该实例变量的名字。

现在回到 `Person.m` 并实现你的 getter 方法：

```objc
@implementation Person
- (float)heightInMeters
{
    return heightInMeters;
}
- (void)setHeightInMeters:(float)h
{
    heightInMeters = h;
}
- (int)weightInKilos
{
    return weightInKilos;
}
- (void)setWeightInKilos:(int)w
{
    weightKilos = w;
}
- (float)bodyMassIndex
{
    return weightInKilos / (heightInMeters * heightInMeters);
}
@end
```

最后，在 `main.m` 中使用这些方法：

```objc
#import "Person.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建 Person 的实例
        Person *person = [[Person alloc] init];

        // 给实例变量赋予有趣的体重值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];

        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"person has a BMI of %f", bmi);
    }
    return 0;
}
```

编译并运行程序。注意你导入了 `Person.h`，这样编译器在 `main()` 使用这些方法之前就已经知道它们是如何声明的。

## 点语法（Dot notation）

使用点号而不是方括号的形式被称为 *点语法*（dot notation）。这种形式隐藏了正在发送消息的事实：

```objc
x.fido;
```

点语法让这两行代码完全相同：

```objc
[x fido];
x.fido = 3;
```

## 属性（Properties）

你可能会奇怪，为什么 getter 方法的名字没有包含 `get` 以匹配 setter 方法的名字。这是一种 Objective-C 的命名规范。读取实例变量的方法名直接就是该实例变量的名字。



```objc
[x fido];
x = 3;
```

点语法隐藏了正在发送消息的事实。点语法让这两行代码完全相同：

```objc
[x fido];
x = 3;
```

## 属性

注意，我们 类的大部分代码是为了编写 setter 和 getter 方法。属性提供了一种简化这些的方法：

```objc
x = 3;
```

Apple 创建了一种方便的方法来简化 setter 和 getter 方法，这被称为属性。在 `Person.h` 中，使用 `@property` 关键字可以声明 setter 和 getter 方法：

```objc
#import <Foundation/Foundation.h>
@interface Person : NSObject
{
    float heightInMeters;
    int weightInKilos;
}
@property float heightInMeters;
@property int weightInKilos;

-(float)bodyMassIndex;
@end
```

在 `Person.m` 中，使用 `@property` 关键字来实现 setter 和 getter 方法：

```objc
@implementation Person

- (float)heightInMeters
{
  return heightInMeters;
}
- (void)setHeightInMeters:(float)h
{
  heightInMeters = h;
}
- (int)weightInKilos
{
  return weightInKilos;
}
- (void)setWeightInKilos:(int)w
{
  weightInKilos = w;
}
- (float)bodyMassIndex
{
  return weightInKilos / (heightInMeters * heightInMeters);
}
@end
```

## self

在任何方法内部，你都可以访问 `self`。`self` 是指向接收消息对象的指针。例如，如果你想获取身高，你会这样写：

```objc
float h = [self heightInMeters];
```

## 继承

当你创建 `Person` 类时，将其声明为 `NSObject` 的子类。这意味着每个 `Person` 实例都拥有 `NSObject` 定义的实例变量和方法，以及 `Person` 定义的实例变量和方法。我们说 `Person` 继承自 `NSObject`。在本节中，我们将传递一些继承。

打开 BMTime 项目并创建一个新文件：Objective-C 类。将其命名为 `Employee` 并将其创建为 `NSObject` 的子类。很快，我们将 `Employee` 类更改为 `Person` 的子类。理解的吗？员工是人。他们有身高和体重。我们还将为我们的类添加一个员工特有的实例变量——员工 ID。

## 图 18.1 你所知的类的继承图

![](img/a694739dec801cd745c57da9e19c2cd4_161_0.png)

## 多文件

注意你的项目现在有两个可执行文件：`main.m` 和 `Person.m`（`Person.h` 是声明，没有执行代码）。当你构建项目时，这些文件会被分别编译然后链接。现实项目通常由数百个 C 和 Objective-C 文件组成。

## 挑战

创建一个名为 `Stocks` 的命令行工具。然后创建一个名为 `StockHolding` 的类来表示你购买的股票。它是 `NSObject` 的子类。对于实例变量，它有两个名为 `purchasePrice` 和 `currentPrice` 的 float 类型和一个 int 类型的 `numberOfShares`。为实例变量创建访问方法。创建另外两个实例方法：

- `(float)costInDollars;` // purchasePrice * numberOfShares
- `(float)valueInDollars;` // currentPrice * numberOfShares

在 `main()` 中，填充三个 `StockHolding` 实例的数组。遍历数组打印每个实例的值。

## 图 17.2 StockHolding 对象的数组

![](img/a694739dec801cd745c57da9e19c2cd4_160_0.png)

打开 `Employee.m` 并合成访问器（accessors）：

```objc
#import "Employee.h"
@implementation Employee

@synthesize employeeID;
@end
```

现在你有了一个新的 `Employee` 类，它包含了 `Person` 的所有实例变量，以及一个名为 `employeeID` 的新实例变量。`Employee` 的实例将响应与 `Person` 实例相同的所有消息。`Employee` 的实例还将响应 `setEmployeeID:` 和 `employeeID` 消息。

而且，由于 `Person` 继承自 `NSObject`，因此 `Employee` 也继承了来自 `NSObject` 的实例变量和方法。所有对象都（无论是直接地还是间接地）继承自 `NSObject`。

`NSObject` 有许多方法，但只有一个实例变量：`isa` 指针。每个对象的 `isa` 指针都指向创建它的那个类。

## 图 18.2 BMITime 的对象图

![](img/a694739dec801cd745c57da9e19c2cd4_162_0.png)

假设你向一个对象发送了消息 `fido`。为了响应这条消息，该对象使用 `isa` 指针找到它的类并询问：“你这里有一个名为 `fido` 的实例方法吗？”如果该类有一个名为 `fido` 的方法，它就会被执行。如果该类没有 `fido` 方法，它会询问它的父类：“你是否有一个名为 `fido` 的实例方法吗？”并沿着链链向上寻找名为 `fido` 的方法。这种寻找会在找到该方法或到达链链的顶端时停止。在链链的顶端，`NSObject` 会说：“不，没有 `fido` 方法。”然后你会收到一条错误信息，内容类似于“此 Employee 实例不响应 fido 选择器（selector）。”

试一试。打开 `main.m` 并向 `Person` 实例发送一条它无法理解的消息：

```objc
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // 创建 Person 的实例
        id person = [[Person alloc] init];

        // 给实例变量赋予有趣的值
        [person weightInKilos:96];
        [person heightInMeters:1.8];

        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog("%d %f has a BMI of %f",
             [person weightInKilos], [person heightInMeters], bmi);

        [person count];
    }
    return 0;
}
```

编译并运行程序。忽略编译器的警告，因为你是故意这么这么的（在大多数情况下，如果你看到这个警告，你应该关注它！）。你应该能看到控制台记录了一个运行时异常。

> *** terminating app due to uncaught exception 'NSInvalidArgumentException', reason: "-[Person count]: unrecognized selector to instance 0x100108de0'"

在检查异常后，在继续之前删除有问题的代码行。

你创建了新的 `Employee` 类，但你还没有使用它。

修改 `main.m` 以使用 `Employee`：

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"

int main(int argc, const char * argv[]) {

 @autoreleasepool {
    // 创建 Person 的实例
    Person * person = [[Employee alloc] init];

    // 给实例变量赋予有趣的值
    [person setWeightKilos:96];
    [person setHeightMeters:1.8];

    // 调用 bodyMassIndex 方法
    float bmi = [person bodyMassIndex];
    NSLog("@%d, %f has a BMI of %f", [person heightInMeters], bmi);

    return 0;
}
```

注意，你的 `person` 变量仍然声明为指向 `Person` 的指针。认为这会引起问题吗？编译并运行程序，你会发现程序仍然运行良好。这是因为员工是人的一种——它可以做人能做的任何事情。也就是说，我们可以在程序期望 `Person` 实例的地方使用 `Employee` 实例。

现在，你将使用一个 `Employee` 独有的方法，因此你必须更改指针的类型：

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"

int main(int argc, const char * argv[]) {
 @autoreleasepool {
    // 创建 Person 的实例
    Employee *person = [[Employee alloc] init];

    // 给实例变量赋予有趣的值
    [person setWeightKilos:96];
    [person setHeightMeters:1.8];
    [person setEmployeeID:15];

    // 调用 bodyMassIndex 方法
    float bmi = [person bodyMassIndex];
    NSLog("@Employee %d has a BMI of %f", [person employeeID], bmi);

    return 0;
}
```

## 重写方法（Overriding methods）

回顾一下，当发送消息时，对该名称方法的搜索从对象的类开始，并沿着继承层级向上。找到的第一个实现就是执行的那个。因此，你可以用自定义实现来重写继承的方法。例如，假设你决定员工的体质量指数（BMI）为19。在这种情况下，你可能会在 `Employee` 中重写 `bodyMassIndex` 方法。打开 `Employee.m` 并执行：

```objc
#import "Employee.h"
@implementation Employee

@synthesize employeeID;

-(float)bodyMassIndex {
    return 19.0;
}
@end
```

编译并运行程序，注意你对 `bodyMassIndex` 的实现是被执行的那个。注意你在 `Employee.m` 中实现了 `bodyMassIndex`，但你没有在 `Employee.h` 中声明它。然而，由于 `Employee` 继承自 `Person`，每个人已经知道 `Employee` 有一个 `bodyMassIndex` 方法。

如果你决定员工的 BMI 可以自动打 90 折呢？在返回结果之前调用 `Person` 的版本的方法会方便得多。为了实现这一点，你使用 `super` 指令。在 `Employee.m` 中尝试一下：

```objc
#import "Employee.h"
@implementation Employee

@synthesize employeeID;
-(float)bodyMassIndex
{
    float normalBMI = [super bodyMassIndex];
    return normalBMI * 0.9;
}
@end
```

编译并运行程序。准确来说，`super` 指令表示“运行此方法，但从父类开始寻找它的实现”。

## 挑战（Challenge）

挑战基于上一章的挑战。

创建一个 `StockHolding` 的子类 `ForeignStockHolding`。给 `ForeignStockHolding` 增加一个实例变量：`conversionRate`，类型为 `float`。（转换率是你将本地价格乘以该值以获得美元价格。假设 `purchasePrice` 和 `currentPrice` 是本地货币。）重写 `costInDollars` 和 `valueInDollars`。

在 `main()` 中，向数组添加几个 `ForeignStockHolding` 实例。

## 图 18.3 StockHolding 和 ForeignStockHolding 对象

![](img/a694739dec801cd745c57da9e19c2cd4_167_0.png)

# 对象实例变量（Object Instance Variables）

为止，你在类中声明的实例变量都是如 `int` 或 `float` 等简单类型。实例变量指向其他对象要常见得多。对象实例变量指向另一个对象，并描述两个对象之间的关系。通常，对象实例变量分为三类：

- **对象类型属性**：指向简单的、类值的对象，如 `NSString` 或 `NSNumber`。例如，员工的姓将存储在 `NSString` 中。因此，`Employee` 的实例将有一个指向 `NSString` 指针的实例变量。
- **一一关系**：指向单个复杂对象的指针。例如，员工可能有配偶。因此，`Employee` 的实例将有一个指向 `Person` 指针的实例变量。
- **多多关系**：指向集合类实例的指针，例如 `NSMutableArray`。（我们将在第21章看到其他集合的示例。）例如，员工可能有孩子。在这种情况下，`Employee` 的实例将有一个指向 `NSMutableArray` 实例的实例变量。`NSMutableArray` 将包含一个或多个对象的指针列表。

（注意，在上面的列表中，我提到了“NSString”。`NSString` 是一个类，但“an NSString”是 `NSString` 实例的缩写。这种用法有点让人困惑，但非常常见，所以习惯它是好的。）

## 图 19.1 带有对象实例变量的 Employee

![](img/a694739dec801cd745c57da9e19c2cd4_169_0.png)

注意，与其他图表一样，指针是由箭头表示的。此外，这些指针是有命名的。因此，一个 **Employee** 将拥有三个新的实例变量：`lastName`、`spouse` 和 `children`。**Employee** 实例变量的声明如下：

除了 `employeeID` 之外，这些变量都是指针。对象实例变量总是指针。例如，变量 `spouse` 是指向位于堆上的另一个对象的指针。指针 `spouse` 位于 **Employee** 对象内部，但指向它的 **Person 对象** 并不在内部。对象不会存在于另一个对象内部。员工对象包含了它的员工 ID（变量本身和值本身），但它只知道它的配偶在内存中的位置。

对象指向其他对象而非包含其他对象有两个重要的副作用：

- 一个对象可以承担多个角色。例如，员工的配偶很可能也被列为儿童的紧急联系人：

## 图 19.2 一个对象，多个角色



![](img/a694739dec801cd745c57da9e19c2cd4_170_0.png)

你最终会在程序内存中使用许多不同的对象。你需要让正在使用的对象保持存在，但你希望不必要的对象被释放（将其内存归还堆）。重用内存可以保持程序的内存占用尽可能小，这会让你的整个电脑感觉更加敏捷。在移动设备（如 iPhone）上，如果你的程序内存占用过大，操作系统将杀死你的程序。

# 对象所有权和 ARC

为了管理这些问题，我们有了对象所有权的概念。当一个对象拥有一个对象实例变量时，带有指针的对象被认为拥有被指向的对象。

从另一个角度来看，对象知道它当前有多少个所有者。例如，在上面的图中，`Person` 的实例有三个所有者：`Employee` 对象和两个 `Child` 对象。当一个对象的所有者为零时，就不再需要它，它就会释放自己。

每个对象的所有者计数由自动引用计数（`ARC`）处理。`ARC` 是 Objective-C 的一项最新开发。在 Xcode 4.2 之前，我们手动管理所有权，并花费了大量精力和时间工作。（关于手动引用计数及其工作原理的更多信息，请参见第 20 节的最后部分。然而，书中的所有代码假设你正在使用 `ARC`。）

让我们扩展 BMI 项目，看看所有权在实践中是如何运作的。为了跟踪哪些资产分配给了哪个员工，我们将创建一个 `Asset` 类，每个 `Employee` 将拥有一个包含其或她资产的数组。

## 图 19.3 员工与资产

![](img/a694739dec801cd745c57da9e19c2cd4_171_0.png)

这通常被称为“父子”关系：父对象（`Employee` 的实例）拥有一组孩子（包含 `Asset` 对象的 `NSMutableArray`）。

## 创建新文件：Asset 类

创建一个新文件：一个 `NSObject` 的 Objective-C 子类。将其命名为 `Asset`。

打开 `Asset.h` 并声明两个实例变量和两个属性：

```objc
#import <Foundation/Foundation.h>

@interface Asset : NSObject
{
    NSString *label;
    unsigned int resaleValue;
}
@property (strong) NSString *label;
@property unsigned int resaleValue;
@end
```

注意 `label` 的 `@property` 声明上的 `strong` 修饰符。它表示：“这是一个指向对象的指针，我声称拥有该对象。”（我们将在第 20 节讨论此属性属性的其他选项）。

记住，当一个对象没有所有者时，它会被释放。当一个对象正在被释放时，它会发送 `dealloc` 消息。（每个对象都从 `NSObject` 继承 `dealloc` 方法。）你将重写 `dealloc`，以便看到 `Asset` 实例何时被释放。

为了明确是哪个特定的 `Asset` 实例被释放，你还将实现另一个 `NSObject` 方法 `description`。该方法返回一个对类实例进行描述的字符串。对于 `Asset`，你将让 `description` 返回一个包含 `label` 和 `resaleValue` 的字符串。

打开 `Asset.m`。合成你实例变量的访问器，然后重写 `description` 和 `dealloc`。

```objc
#import "Asset.h"

@implementation Asset

@synthesize label, resaleValue;

- (NSString *)description {
    return [NSString stringWithFormat:@"%@:%@ $%d",
            [self label], [self resaleValue]];
}

- (void)dealloc {
    NSLog(@"deallocating %@", self);
}
@end
```

注意上述代码中格式字符串中的 `%@` 标记。该标记被替换为向相应变量发送 `description` 消息的结果（该变量必须是对象的指针以便接收此消息）。

尝试构建你目前的内容，看看输入时是否有任何错误。你可以使用键盘在不运行程序的情况下构建程序。

```objc
Employee *person = [[Employee alloc] init];

// Give the instance variables interesting values
[person setWeightInKilos:90 + i];
[person setHeightInMeters:1.8 - i/10.0];
[person setEmployeeID:i];

// Put the instance in the employees array
[employees addObject:person];

// Create 10 assets
for (int i = 0; i < 10; i++) {

    // Create an asset
    Asset *asset = [[Asset alloc] init];

    // Give it an interesting label
    NSString *currentLabel = [NSString stringWithFormat:@"Laptop %d", i];

    // Get a random number between 0 and 9 inclusive
    NSInteger randomIndex = random() % [employees count];

    // Find that employee
    Employee *randomEmployee = [employees objectAtIndex:randomIndex];

    // Assign the asset to the employee
    [randomEmployee addAssetsObject:asset];
}

NSLog(@"Employees: %@", employees);

NSLog(@"Giving up ownership of one employee");

[employees removeObjectAtIndex:5];

employees = nil;
}
return 0;
```

## 编译并运行程序。你应该看到类似的内容：

```
Employees: {
    "<Employee 0: $0 in assets>",
    "<Employee 1: $153 in assets>",
    "<Employee 2: $119 in assets>",
    "<Employee 3: $68 in assets>",
    "<Employee 4: $30 in assets>",
    "<Employee 5: $136 in assets>",
    "<Employee 6: $119 in assets>",
    "<Employee 7: $34 in assets>",
    "<Employee 8: $0 in assets>",
    "<Employee 9: $136 in assets>"
}
```

放弃一个员工的所有权

```
deallocating <Employee 5: $136 in assets>
deallocating <Laptop 3: $51 >
deallocating <Laptop 5: $85 >
Giving up ownership of array
deallocating <Employee 0: $0 in assets>
deallocating <Employee 1: $153 in assets>
deallocating <Laptop 9: $153 >

deallocating <Employee 9: $136 in assets>
deallocating <Laptop 8: $136 >
```

当员工 #5 从数组中移除时，因为它不再拥有所有者，所以它会被释放。它的资产也会被释放，因为它们没有所有者。（而且你必须相信我的：被释放的资产的标签（`NSString` 实例）在它们没有所有者后也会被释放。）

当 `employees` 被设置为 `nil` 时，数组不再拥有所有者。因此它会被释放，这会引发更大规模的内存清理和释放链式反应，因为突然之间，没有任何一个员工拥有所有者了。

很整洁，对吧？当对象不再需要时，它们就会被释放。这是好事。当不必要的对象没有被释放时，就称为内存泄漏。通常，内存泄漏会导致随着时间的推移，越来越多的对象不必要地残留。你的应用程序的内存占用会越来越大。在 iOS 上，操作系统最终会杀死你的应用程序。在 Mac OS X 上，由于机器花费越来越多的时间将数据从内存交换到磁盘上，整个系统的性能将受到影响。

## 挑战

使用上一个挑战中的 `StockHolding` 类，制作一个工具创建一个 `Portfolio` 类的实例并向其填充股票持仓。投资组合（`Portfolio`）可以告诉你它的当前价值。

# 20 防止内存泄漏

建立双向的关系是非常常见的。例如，可能某个资产应该知道当前是哪个员工持有它。让我们向该关系中添加这一项。新的对象图将如下所示：

### 图 20.1 添加持有者关系

![](img/a694739dec801cd745c57da9e19c2cd4_179_0.png)

从设计的角度来看，你会说我们正在添加从子对象（`Asset` 实例）指向它的父对象（`Employee` 实例）的指针。

在 `Asset.h` 中，添加一个指针实例变量来持有持有它的员工：

```objc
#import <Foundation/Foundation.h>
@class Employee;

@interface Asset : NSObject
{
    NSString *label;
    Employee *holder;
    unsigned int resaleValue;
}
@property (strong) NSString *label;
@property (strong) Employee *holder;
@property unsigned int resaleValue;
@end
```

在 `Asset.m` 中，合成访问器并扩展 `description` 方法以显示持有者：

```objc
#import "Asset.h"
#import "Employee.h"

@implementation Asset

@synthesize label, resaleValue, holder;

- (NSString *)description {
    // holder 是否非空?
    if ([self holder]) {
        return [NSString stringWithFormat:@"%@: $%@, assigned to %@",
                [self label], [self resaleValue], [self holder]];
    } else {
        return [NSString stringWithFormat:@"%@: $%d unassigned",
                [self label], [self resaleValue]];
    }
}

- (void)dealloc {
    NSLog(@"deallocating %@", self);
}
@end
```

这引出了一个问题：在 `Employee.m` 中，扩展 `addAssetsObject:` 方法以设置持有者：

```objc
- (void)addAssetsObject:(Asset *)asset {
    asset.holder = self;
    [assets addObject:asset];
}
```

等等，问题是：这会创建一个**循环引用**（retain cycle）。资产拥有员工，员工拥有资产数组，而资产数组又拥有资产。这是一个由所有权循环产生的垃圾岛。这些对象应该被释放以释放内存，但它们没有。这被称为循环引用。循环引用是内存泄漏的非常常见来源。要在你的程序中查找循环引用，可以使用 Apple 的分析工具 `Instruments`。当你分析程序时，会在程序运行时对其进行监控，以查看代码和系统在后台发生了什么。然而，你的程序运行并退出非常快。为了给你留出分析时间，请在 `main()` 函数最后添加百秒的 `sleep()`：

```objc
...
    sleep(100);
    return 0;
}
```

在 Xcode 中，选择菜单中的 Product → Profile。`Instruments` 将启动。当可能的工具列表出现时，选择 Leaks：

### 图 20.2 选择分析器

![](img/a694739dec801cd745c57da9e19c2cd4_183_0.png)

当程序运行时，你可以浏览各种状态。在窗口左侧有两个工具可以选择（见图 20.3）。点击 Allocations 工具将让你看到堆中已分配的所有内容的条形图：

### 图 20.3 Allocations 工具

![](img/a694739dec801cd745c57da9e19c2cd4_184_0.png)

例如，你可以看到 10 个 `Asset` 实例仍然存在于你的堆中。

要查找循环引用，请切换到 Leaks 工具并从表格上方菜单栏选择 Cycles 视图。选择特定的循环以查看其对象图：

### 图 20.4 Leaks 工具

![](img/a694739dec801cd745c57da9e19c2cd4_185_0.png)

# 弱引用

如何修复引用循环？使用弱引用。弱引用是一种*不意味着*所有权的指针。为了修复我们的引用循环，资产（`Asset`）不应该拥有持有者（`holder`）。编辑 `Asset.h` 将 `holder` 设为弱引用：

```objc
#import <Foundation/Foundation.h>
@class Employee;

@interface Asset : NSObject
{
    NSString *label;
    __weak Employee *holder;
    unsigned int resaleValue;
}
@property (strong) NSString *label;
@property (weak) Employee *holder;
@property unsigned int resaleValue;
@end
```

编译并运行程序。注意，现在所有对象都被正确地释放了。

在父子关系中，防止此类引用循环的通用规则是父对象拥有子对象，但子对象不拥有父对象。



## 弱用的置零

看看弱用的实际用法，让我们再添加一个数组。如果我们想要一个包含所有资产的数组——即使是尚未分配给特定员工的资产？我们可以在创建资产时将它们添加到数组中。在 `main.m` 中添加几行代码：

```
#import <Foundation/Foundation.h>
#import "Employee.h"
#import "Asset.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // 创建一个 Employee 对象数组
        NSMutableArray *employees = [[NSMutableArray alloc] init];

        for (int i = 0; i < 10; i++) {
            // 创建 Employee 实例
            Employee *person = [[Employee alloc] init];

            // 给实例变量赋予有趣的值
            [person setWeightInKilos:90 + i];
            [person setHeightInMeters:1.8 - i/10.0];
            [person setEmployeeID:i];

            // 将员工放入 employees 数组
            [employees addObject:person];
        }

        NSMutableArray *allAssets = [[NSMutableArray alloc] init];

        // 创建 10 个资产
        for (int i = 0; i < 10; i++) {
            // 创建一个资产
            Asset *asset = [[Asset alloc] init];

            // 给它设置一个有趣的标签
            NSString *currentLabel = [NSString stringWithFormat:"Laptop %d", i];
            [asset setLabel:currentLabel];
            [asset setResaleValue:i * 17];

            // 获取 0 到 9 之间的随机数
            NSInteger randomIndex = rand() % [employees count];

            // 找到该员工
            Employee *randomEmployee = [employees objectAtIndex:randomIndex];

            // 将资产分配给员工
            [randomEmployee addAsset:asset];
            [allAssets addObject:asset];
        }

        NSLog("Employees: %@", employees);
        NSLog("Giving ownership of one employee");
        [employees removeObjectAtIndex:5];
        NSLog("allAssets: %@", allAssets);
        NSLog("Giving ownership of arrays");
        allAssets = nil;
        employees = nil;
        sleep(100);
        return 0;
    }
}
```

在编译并运行程序之前，思考一下你预期输出是什么样的。你将看到 `allAssets` 数组的内容——在 Employee #5 被释放之后。此时，Employee #5 的资产状态会是怎样的？这些资产失去了一个所有者（Employee #5），但它们仍然被 `allAssets` 拥有，因此它们不会被释放。

对于之前由 Employee #5 拥有的资产，其 `holder` 又是怎样的呢？当我们引用的对象被释放时，指针变量会被置零，或设置为 `nil`。因此，Employee #5 的资产不会被释放，它们的 `holder` 变量将自动设置为 `nil`。

现在编译并运行程序，检查你的输出：

```
Employees:
"Employee 0: $0 in assets"
...
"Employee 9: $136 in assets"
Giving ownership of one employee
deallocating Employee 5: $136 in assets
allAssets:
<Laptop 0: $0, assigned to <Employee 3: $68 in assets>>
<Laptop 1: $17, assigned to <Employee 6: $119 in assets>>
<Laptop 2: $34, assigned to <Employee 7: $34 in assets>>
<Laptop 3: $51 unassigned>
<Laptop 4: $68, assigned to <Employee 3: $68 in assets>>
<Laptop 5: $85 unassigned>
<Laptop 6: $102, assigned to <Employee 6: $119 in assets>>
<Laptop 7: $119, assigned to <Employee 2: $119 in assets>>
<Laptop 8: $136, assigned to <Employee 9: $136 in assets>>
<Laptop 9: $153, assigned to <Employee 1: $153 in assets>>
...
Giving ownership of arrays
deallocating Laptop 3: $51 unassigned
...
deallocating Laptop 8: $136 unassigned>
```

## 深入好奇者进：手动引用计数和 ARC 历史

正如第 19 章开头提到的，在自动引用计数（ARC）被引入 Objective-C 之前，我们使用手动引用计数，即使用保留计数（retain counts）。在手动引用计数中，所有权的变化仅在你向对象发送显式消息时发生：

```
[object release]; // anObject 失去一个所有者
[object retain]; // anObject 获得一个所有者
```

你主要会在访问器方法（其中新值被 `retain`，旧值被 `release`）以及 `dealloc` 方法（释放所有之前被 `retain` 的对象）中看到这类调用。`Asset` 的 `setHolder:` 方法看起来如下：

```
(void)setHolder:(Employee *)newEmp {
    [newEmp retain];
    [holder release];
    holder = newEmp;
}
```

`dealloc` 方法看起来如下：

```
(void)dealloc {
    [label release];
    [holder release];
    [super dealloc];
}
```

那么 `description` 方法呢？它创建并返回一个字符串。`Asset` 应该声称拥有它吗？这并没有意义；因为资产正在交出它创建的字符串。当你 `autorelease` 一个对象时，你是在将其标记为在将来释放。在 ARC 之前，`Asset` 的 `description` 方法看起来如下：

```
(NSString*)description {
    NSString *result = [NSString stringWithFormat:@"%@", label];
    [result autorelease];
    return result;
}
```

# 集合类

你已经使用过两个集合类：`NSArray` 及其子类 `NSMutableArray`。如你所知，数组持有指向其他对象的指针集合。这些指针是有序的，因此你使用索引（一个整数）来访问集合中的对象。在本章中，我们将深入研究数组，并查看其他一些集合类：`NSSet`/`NSMutableSet`、`NSMutableDictionary`/`NSMutableDictionary`。

## NSArray/NSMutableArray

当你向数组中添加一个对象时，数组会声称该对象的所有权。当你从数组中移除该对象时，数组会放弃所有权。打开 BMITime，查看你是如何使用 `employees` 数组的。忽略所有其他内容，你会看到类似这样的代码：

```
// 创建 Employee 对象的数组
NSMutableArray *employees = [[NSMutableArray alloc] init];

for (int i = 0; i < 10; i++) {
    // 创建 Employee 实例
    Employee *person = [[Employee alloc] init];

    // 将员工放入 employees 数组
    [employees addObject:person];
}

[employees removeObjectAtIndex:5];
employees = nil;
```

你通常使用 `alloc/init` 或类方法 `array` 来创建一个空数组。例如，你可以像这样创建一个可变数组：

`NSMutableArray *employees = [NSMutableArray array];`

注意，`addObject:` 方法将对象添加到列表末尾。随着对象的添加，数组将增长到所需的尺寸以容纳它们。

## 不变对象

末尾的 `nil` 是你告诉方法停止执行的标识。因此，这个颜色数组将只有三个字符串。（如果你忘记了 `nil`，可能会导致你的程序崩溃。）

大多数初级程序员对 `NSArray` 的存在感到惊讶。为什么有人想要一个不能更改的列表呢？有两个原因：

- 你不信任和你一起工作的人。也就是说，你想让他们查看数组，但不想让他们能够修改它。一种更温和的方法是给他们一个 `NSMutableArray`，但告诉他们这是一个 `NSArray`。例如，想象以下方法：

```
// 返回一个包含 30 个奇数的数组
-(NSArray *)odds
{
    static NSMutableArray *odds = [[NSMutableArray alloc] init];
    int i = 1;
    while ([odds count] < 30) {
        [odds addObject:[NSNumber numberWithInt:i]];
    }
    return odds;
}
```

任何调用此方法的都会假设它返回的是一个不可变的 `NSArray`。如果调用者尝试从返回的对象中添加或删除项目，编译器将发出严厉的警告——尽管它实际上是一个 `NSMutableArray` 实例。

- 另一个原因是性能：不变对象永远不需要复制。对于可变对象，你可能会创建一个私有副本，以便你确定系统中的其他代码不会从底层上更改它。这对于不变对象来说是不必要的。事实上，`NSMutableArray` 的 `copy` 方法会创建自己的新副本并返回指向新数组的指针，而 `NSArray` 的 `copy` 方法什么都不做——它返回指向它本身的指针。

结果，不变对象在 Objective-C 编程中非常常见。在 Foundation 中，有许多创建不变实例的类：`NSArray`、`NSString`、`NSAttributedString`、`NSData`、`NSCharacterSet`、`NSDictionary`、`NSSet`、`NSIndexSet` 和 `NSURLRequest`。这些类都有可变子类：`NSMutableArray`、`NSMutableString`、`NSMutableAttributedString` 等。另一方面，`NSDate` 和 `NSNumber` 是不可变的，但没有可变子类。

## 排序

有多种方法排序数组，但最常用的方法是使用排序描述符（sort descriptors）数组。`NSMutableArray` 拥有以下方法：

- `(void)sortUsingDescriptors:(NSArray *)sortDescriptors;`

参数是一个 `NSSortDescriptor` 对象的数组。排序描述符包含数组所包含对象的属性名称，以及该属性应该按升序还是降序排序。我们为什么要传递一个排序描述符数组呢？想象你说：“按姓对这个医生列表进行排序，如果相同的，则按名升序排序。如果两个医生的姓相同怎么办？”你可以指定“按姓升序排序，如果姓相同，则按名升序排序，如果姓和名都相同，则按邮政编码排序。”

图 21.1 按 lastName，然后 firstName，最后是 zipCode 排序

![](img/a694739dec801cd745c57da9e19c2cd4_197_0.png)

你进行排序的属性可以是对象的任何实例变量或任何方法的执行结果。

让我们回到 BMITime 项目查看实际应用中的排序。在 `main()` 中，在记录 `employees` 数组之前，根据 `valueOfAssets` 对其排序。如果两个员工持有价值相同的资产，则按 `employeeID` 排序。

编辑 `main.m`：

```
}

NSSortDescriptor *roa = [NSSortDescriptor
sortDescriptorForKey:@"valueOfAssets"
ascending:YES];
NSSortDescriptor *ei = [NSSortDescriptor sortDescriptorForKey:@"employeeID"
ascending:YES];
[employees sortUsingDescriptors:[NSArray arrayWithObjects:roa, ei, nil]];

NSLog("Employees: %@", employees);
```

编译并运行程序。你应该看到员工列表顺序排列正确：

```
Employees: (
"Employee 0: $0 in assets"
"Employee 8: $0 in assets"
"Employee 8: $0 in assets"
"Employee 7: $34 in assets"
"Employee 3: $68 in assets"
"Employee 2: $119 in assets"
"Employee 6: $116 in assets"
```

## 过滤

有一个 `NSPredicate` 类。谓词可能是一个语句，比如“employeeID 大于 75”。`NSMutableArray` 有一个方法丢弃不符合谓词的对象：

```
(void)filterUsingPredicate:(NSPredicate *)predicate;
```

`NSArray` 有一个方法创建一个符合谓词的对象的新数组：

```
(NSArray *)filteredArrayUsingPredicate:(NSPredicate *)predicate;
```

想象你要过滤出资产资产超过 $70 的员工。在 `main.m` 的末尾添加以下代码：

```
[employees removeObjectAtIndex:5];
```

```
NSPredicate *predicate = [NSPredicate predicateFormat:@"valueOfAssets > 70"];
NSArray *reclaimed = [allAssets filteredUsingPredicate:predicate];
NSLog("@reclaimed: %@", reclaimed);
reclaimed = nil;
```

编译并运行程序。你应该看到资产列表：

```
@reclaimed: (
"Employee 6: $119 in assets"
"Employee 3: $68 in assets"
"Employee 5: $136 in assets"
"Employee 6: $116 in assets"
"Employee 9: $136 in assets")
```

用于创建谓词的格式字符串可能非常复杂。如果你大量过滤集合，请务必阅读 Apple 的《谓词编程指南》。

## NSSet/NSMutableSet

集合是一个没有顺序的集合，且特定对象在集合中只能出现一次。集合主要用于询问“是否存在？”的问题。例如，你可能有一个不适合儿童查看的 URL 集合。在向孩子显示任何网页之前，你想快速检查该 URL 是否在集合中。集合处理此操作极快。

员工的资产没有内在顺序，而且资产不应该在同一个员工的资产集合中出现两次。修改你的程序使用 `NSMutableSet` 代替 `NSMutableArray` 来资产关系。

## 图 21.2 使用 NSMutableSet 处理资产

![](img/a694739dec801cd745c57da9e19c2cd4_200_0.png)

在 `Employee.h` 中，更改声明：

```
@import "Person.h"
@class Asset;

@interface Employee : Person
{
    int employeeID;
    NSMutableSet *assets;
}
@property int employeeID;
- (void)addAssets:(Asset *)a;
- (unsigned int)valueOfAssets;
@end
```

在 `Employee.m` 中，创建正确类的实例：

```
- (void)addAssets:(Asset *)a
{
```



```objc
if (!assets) {
  assets = [[NSMutableSet alloc] init];
}
[assets addObject:a];
[a setHolder:self];
```

## 编译并运行程序

编译并运行程序。它应该处理该函数。

## 集合访问与相等性

你无法通过索引访问集合中的对象，因为集合是没有顺序的。相反，你所做的就是问：“这些里面有其中一个吗？” `NSSet` 有一个方法：

- `- (BOOL)containsObject:(id)x`

当你向集合发送此消息时，它会遍历其对象集合，寻找与 `x` 相等的对象。如果找到了，它会返回 `YES`；否则返回 `NO`。

这引出了我们一个相当深层次的问题：“相等（equal）”意味着什么？`NSObject` 定义了一个名为 `isEqual:` 的方法。要检查两个对象是否相等，你使用 `isEqual:` 方法：

```objc
if ([myDoctor isEqual:yourTennisPartner]) {
  NSLog("my doctor is equal to your tennis partner");
}
```

`NSObject` 对 `isEqual:` 有简单的实现。它看起来如下：

```objc
- (BOOL)isEqual:(id)other
{
  return (self == other);
}
```

因此，如果你没有重写 `isEqual:`，这段代码片段等同于：

```objc
if (myDoctor == yourTennisPartner) {
  NSLog("my doctor is equal to your tennis partner");
}
```

某些类重写了 `isEqual:`。例如，在 `NSString` 中，`isEqual:` 被重写为比较字符串中的字符。“相等（equal）”和“完全相同（identical）”之间是有区别的。假设我有两个字符串的指针：

```objc
NSString *x = ...
NSString *y = ...
```

如果 `x` 和 `y` 包含完全相同的地址，它们就是**完全相同**的。如果它们指向的字符串包含相同顺序的相同字母，则 `x` 和 `y` 是**相等**的。

因此，完全相同的对象总是相等的，而相等的对象并不总是完全相同的。

这种区别重要吗？是的。例如，`NSMutableArray` 有两个方法：

- `- (NSInteger)indexOf:(id)anObject;`
- `- (NSInteger)indexOfObjectIdenticalTo:(id)anObject;`

第一个方法遍历集合并询问每个对象“`isEqualTo:anObject?`”。第二个方法遍历集合并询问每个对象“`== anObject?`”。

## NSDictionary/NSMutableDictionary

如你所知，数组是通过数字索引的；很容易问“给我第 10 个对象”。字典是通过字符串索引的；很容易问“给我存储在 `favoriteColor` 键下的对象”。更准确地说，字典是键值对的集合。键通常是字符串，而值可以是任何类型的对象。这些键值对并不是以任何特定顺序存储的。

让我们创建一个高管字典。键将是高管职称，值将是 `Employee` 实例。第一个员工将放在字典的 "CEO" 下；第二个放在 "CTO" 下。修改你的 `main.m` 来创建并填充 `NSMutableDictionary`。然后，打印出高管字典。最后，将字典的指针设置为 `nil`，这样你就可以看到字典被释放了。

```objc
// 创建一个 Employee 对象数组
NSMutableArray *employees = [[NSMutableArray alloc] init];

// 创建一个高管字典
NSMutableDictionary *executives = [[NSMutableDictionary alloc] init];

for (int i = 0; i < 10; i++) {
    // 创建一个 Employee 实例
    Employee *person = [[Employee alloc] init];

    // 给变量赋予有趣的值
    [person setWeightInKilos:90 + i];
    [person setHeightInMeters:1.8 - 1/10.0];
    [person setID:i];

    // 将员工放入 employees 数组
    [employees addObject:person];

    // 这是第一个员工吗？
    if (i == 0) {
        [executives setObject:person forKey:@"CEO"];
    }

    // 这是第二个员工吗？
    if (i == 1) {
        [executives setObject:person forKey:@"CTO"];
    }
}

NSLog(@"allAssets: %@", allAssets);
NSLog(@"executives: %@", executives);

NSLog(@"Giving ownership of arrays");
allAssets = nil;
employees = nil;

return 0;
```

编译并运行程序。高管字典应该输出：

```
executives = {
  CEO = "Employee 0";
  CTO = "Employee 1";
}
```

## 图 21.3 NSMutableDictionary 中的两个 Employee 实例

![图 21.3 NSMutableDictionary 中的两个 Employee 实例](img/a69473dec801cd745c7da9e)

## C 原始类型

本章介绍的集合只持有对象。如果你想要一个浮点型、整数或结构体的指针集合怎么办？你可以将常见的 C 原始类型封装在对象中。有两个类专门为此目的设计：`NSNumber` 持有 C 数字类型，`NSValue` 可以持有指针和某些结构体类型。例如，如果你想把 4 和 5.6 放入数组，将使用 `NSNumber`：

```objc
NSMutableArray *numList = [[NSMutableArray alloc] init];
[numList addObject:[NSNumber numberWithInt:4]];
[numList addObject:[NSNumber numberWith:5.6]];
```

```c
#include <math.h>
```

## #define

`#define` 告诉预处理器：“每当你遇到 A 时，在编译器看到它之前将其替换为 B。” 再次查看 math.h 中的那行：

```c
#define M_PI 3.1415926535897932384626438327950288
```

在 `#define` 指令中，你只需要用空格将两个部分（标记（token）和它的替换内容）分开即可。

`#define` 实际上可以用于创建类似函数的内容。在 `main.m` 中，打印两个数字中较大的一个：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSLog(@"%@ is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));
    }
    return 0;
}
```

`MAX` 不是一个函数；它是一个 `#define`。`MAX` 最基础的 C 版本是：

```c
#define MAX(A,B) ((A) > (B) ? (A) : (B))
```

所以，当编译器看到你刚刚添加的那行时，它看起来是这样的：
`NSLog("%d is larger", ((10) > (12) ? (10) : (12)));`

当你使用 `#define` 来类似函数的操作而不是简单地替换一个值时，你正在创建一个宏。

## 全局变量

与其使用 `#define`，Objective-C 程序员通常使用全局变量来存储常量值。

让我们向程序中添加一些内容来解释。首先，有一个名为 `NSLocale` 的类，它存储了不同地理位置的信息。你可以获取用户当前区域设置的实例并向它提问。例如，如果你想知道用户所在区域的货币符号是什么，你可以这样询问：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSLog(@"%@ is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));

        NSLocale *here = [NSLocale currentLocale];
        NSString *currency = [here objectForKey:@"currency"];
        NSLog(@"Money is %@", currency);
    }
    return 0;
}
```

编译并运行它。根据你所在的位置，你应该看到类似这样的：
`Money is USD`

然而，如果你将键名写错为 `@"Kuruncy"`，你将得不到任何。为了防止这个问题，Foundation 框架定义了一个名为 `NSLocaleCurrencyCode` 的全局变量。它写起来并不一定更简单，但如果你写错了，编译器会报错。此外，Xcode 中的代码补全对全局变量有效，但对字符串 `@"currency"` 不起作用。修改你的代码以使用该常量：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSLog(@"%@ is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));

        NSLocale *here = [NSLocale currentLocale];
        NSString *currency = [here objectForKey:NSLocaleCurrencyCode];
        NSLog(@"Money is %@", currency);
    }
    return 0;
}
```

当编写 `NSLocale` 类时，这个全局变量出现在两个地方。在 `NSLocale.h` 中，变量的声明如下：
`extern NSString const *NSLocaleCurrencyCode;`

`const` 意味着这个指针在程序的整个生命周期内不会改变。`extern` 意味着“我保证它存在，但它会在其他文件中定义。”果然，在 `NSLocale.m` 文件中，有这样的一行：

## enum（枚举）

你通常需要定义一组常量。例如，假设你正在开发一个具有五个档位的搅拌机：搅拌（Stir）、切（Chop）、搅拌（Liquefy）、碎冰（Ice Crush）。你的 `Blender` 类有一个名为 `setSpeed:` 的方法。如果类型允许只选择五个速度中的一个是最好的。为了做到这一点，你会定义一个枚举：

```c
enum BlenderSpeed {
    BlenderStir = 1,
    BlenderChop = 2,
    BlenderLiquify = 5,
    BlenderPulse = 9,
    BlenderIceCrush = 15
};
```

```objc
@interface Blender : NSObject {
    // speed 必须是五个速度中的一个
    enum BlenderSpeed speed;
}
```

```objc
// setSpeed: 期望五个速度中的一个
-(void)setSpeed:(enum BlenderSpeed)x;
@end
```

开发者厌倦了输入 `enum BlenderSpeed`，所以他们经常使用 `typedef` 为它创建一个简写形式：

```c
typedef enum {
    BlenderStir = 1,
    BlenderChop = 2,
    BlenderSpeedLiquify = 5,
    BlenderSpeedPulse = 9,
    BlenderSpeedIceCrush = 15
} BlenderSpeed;
```

```objc
@interface Blender : NSObject {
    // speed 必须是五个速度中的一个
    BlenderSpeed speed;
}
@end
```

```objc
// setSpeed: 期望五个速度中的一个
- (void)setSpeed:(BlenderSpeed)x;
@end
```

你通常不在乎这五个速度代表什么数字——只要它们彼此不同即可。你可以省略值：

```c
typedef enum {
    BlenderStir,
    BlenderChop,
    BlenderLiquify,
    BlenderPulse,
    BlenderIceCrush
} BlenderSpeed;
```

## #define 与全局变量

考虑到你可以使用 `#define` 或全局变量来定义常量，为什么 Objective-C 程序员倾向于使用全局变量？在某些情况下，使用全局变量有性能优势。例如，在比较字符串时使用全局变量更快（消息）。

## 使用 NSString 和 NSData 写入文件

Foundation 框架提供了一些读取和写入文件的简单方法。在本章中，你将尝试几种。

### 将 NSString 写入文件

首先，让我们看看如何将 `NSString` 的内容放入文件。当你向文件写入字符串时，你需要指定编码。字符串编码描述了字符如何作为字节数组存储。Foundation 框架支持约 20 种字符串编码。UTF 有两种：UTF-16 每个字符使用两个字节，而 UTF-8 对于前 128 个 ASCII 字符使用一个字节，其他字符使用两个。对于大多数用途，UTF-8 是很好的选择。

创建一个新项目：命令行工具，名为 Stringz。在 `main()` 中：

```objc
#import <Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSMutableString *str = [[NSMutableString alloc] init];
        for (int i = 0; i < 10; i++) {
            [str appendString:@"cool!\n"];
        }
        [str writeToFile:@"/tmp/cool.txt"
               atomically:YES
               encoding:UTF8StringEncoding
               error:NULL];
        NSLog(@"done writing /tmp/cool.txt");
    }
    return 0;
}
```

该程序将创建一个可以在任何文本编辑器中读取和编辑的文本文件。字符串 `/tmp/cool.txt` 被称为文件路径。文件路径可以是绝对或相对的：绝对路径以代表文件系统的根 `/` 开始，而相对路径从程序的运行目录开始。在 Objective-C 编程中，你会发现我们总是使用绝对路径，因为我们通常不知道程序的运行目录。

## NSError

正如你可以想象的，当你尝试将字符串写入文件时，可能会出现各种问题。例如，用户可能对目标目录没有写入权限。或者目录根本不存在。或者磁盘满了。对于这些情况，操作可能无法完成，方法需要一种方式来返回错误的描述，除了成功或失败的布尔值外。

回顾第 9 章，当你需要函数在返回返回值外返回其他内容时，可以使用按引用传递。你向函数（或方法）传递变量的引用，它可以直接存储或操作该值。引用是该变量的内存地址。

对于错误处理，许多方法接收 `NSError` 指针的引用。为示例添加错误处理：

```objc
return 0;
}
```



编译并运行它。现在修改代码，为 `write` 方法传递一个不存在的文件路径，例如 `@"/too/darned/bad.txt"`。你应该会得到一个友好的错误信息。

注意，你在这段代码中声明了一个 `NSError` 实例，但你并没有创建（或实例化）一个 `NSError` 对象并赋值给指针。

为什么不呢？你希望在没有发生错误时避免创建一个不必要的错误对象。如果发生了错误，`writeToFile:atomically:encoding:error:` 将负责创建一个新的 `NSError` 实例，并修改你声明的错误指针，使其指向这个新的错误对象。然后，你就可以通过你的错误指针询问该对象到底出了什么问题。

这种对 `NSError` 的条件性创建要求你传递一个错误的引用（`&error`），因为此时还没有对象可以传递。然而，与你在第 9 章中执行的按引用传递（当时你传递的是一个基础类型 C 变量的引用）不同，在这里你传递的是一个指针变量的地址。本质上，你传递的是另一个地址的地址（该地址可能会变成一个 `NSError` 对象的地址）。

回到我们第 9 章中国际间谍的类比，你可能会告诉你的间谍：“如果发生任何意外，就写一份完整的报告（太大了，放不进钢管），并把它藏在图书馆的一本书里。我需要知道你把它藏在哪了，所以把书名写在钢管里。”也就是说，你给间谍提供了一个位置，让她可以在那里存放她创建的错误报告的地址。

这里是 `NSString` 类中 `writeToFile:atomically:encoding:error:` 的声明内部：

```objc
- (BOOL)writeToFile:(NSString *)path atomically:(BOOL)useAuxiliaryFile encoding:(NSStringEncoding)enc error:(NSError **)error
```

注意这个双星号。当你调用这个方法时，你提供的是一个指向 `NSError` 实例的指针的指针。

通过引用传递 `NSError` 的方法总是返回一个指示是否发生了错误的值。例如，这个方法在发生错误时会返回 `NO`。除非返回值指示发生了错误，否则不要尝试访问 `NSError`；如果 `NSError` 对象实际上并不存在，尝试访问它将导致你的程序崩溃。

# 使用 NSString 读取文件

将文件读取到字符串非常相似：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSError *error = nil;

        NSString *str = [[NSString alloc] initWithContentsOfFile:@"/etc/resolv.conf"
                                encoding:NSASCIIStringEncoding
                                            error:&error];

        if (!str) {
            NSLog(@"read failed: %@", [error localizedDescription]);
        } else {
            NSLog(@"resolv.conf looks like this: %@", str);
        }
    }
    return 0;
}
```

## 将 NSData 对象写入文件

`NSData` 对象代表一个字节缓冲区。例如，如果你从 URL 获取获取了一些数据，你就会得到一个 `NSData` 实例。你可以要求 `NSData` 将自己写入文件。创建一个名为 `ImageFetch` 的新 Foundation 命令行工具，从 Google 网站获取图像到一个 `NSData` 实例中。然后要求 `NSData` 将它的字节缓冲区写入文件：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSURL *url = [NSURL URLWithString:@"http://www.google.com/images/logos/ps_logo2.png"];
        NSRequest *request = [NSRequest requestWithURL:url];
        NSError *error = nil;
        NSData *data = [NSURLConnection sendSynchronousRequest:request returningResponse:NULL error:&error];

        if (!data) {
            NSLog(@"fetch failed: %@", [error localizedDescription]);
            return 1;
        }

        NSLog(@"The file is %lu bytes", [data length]);
        BOOL written = [data writeToFile:@"/tmp/google.png" options:0 error:&error];

        if (!written) {
            NSLog(@"write failed: %@", [error localizedDescription]);
            return 1;
        }

        NSLog(@"Success!");
    }
    return 0;
}
```

编译并运行程序。在预览中查看生成的图像文件。

注意 `writeToFile:options:error` 方法接收一个指示保存过程中使用的选项数字。最常用的选项是 `NSDataWritingAtomic`。假设你已经获取了一张图像，现在只是重新获取并将其替换为更新的版本。在写入新图像时，断电了。一个写入了一半的文件毫无价值。在写入了一半的文件没有文件更糟糕的情况下，你可以让写入变为原子性的。添加此选项：

```objc
NSLog("The file is %lu bytes", [data length]);
```

```objc
BOOL written = [data writeToFile:"/tmp/google.png"
                   options:NSDataWritingAtomic
                   error:&error];
```

```objc
if (!written) {
    NSLog("write failed: %@", [error localizedDescription]);
    return 1;
}
```

现在，数据将被写入一个临时文件，当写入完成后，文件将被重命名为正确的名称。这样，你要么获得整个文件，要么什么都没有。

## 从文件读取 NSData

你也可以从文件创建 `NSData` 实例。在你的程序中添加两行：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSError *error = nil;
        NSURL *url = [NSURL URLWithString:@"http://www.google.com/images/logos/ps_logo2.png"];
        NSRequest *request = [NSRequest requestWithURL:url];
        NSData *data = [NSURLConnection sendSynchronousRequest:request returningResponse:NULL error:&error];

        if (!data) {
            NSLog(@"fetch failed: %@", [error localizedDescription]);
            return 1;
        }

        NSLog(@"The file is %lu bytes", [data length]);
        BOOL written = [data writeToFile:@"/tmp/google.png"
                                     options:NSDataWritingAtomic
                                     error:&error];

        if (!written) {
            NSLog(@"write failed: %@", [error localizedDescription]);
            return 1;
        }

        NSLog(@"Success!");
        NSData *readData = [NSData dataWithContentsFile:@"tmp/google.png"];
        NSLog("The file read from the disk has %lu bytes", [readData length]);
    }
    return 0;
}
```

编译并运行程序。

# 回调 (Callbacks)

到为止，你的代码是老板。它向标准对象发送消息并告诉它们该做什么。到为止，你的程序在毫秒内运行并退出。

你一直过着甜蜜而简单的生活。在现实世界中，应用程序运行数小时，你的对象受到不断的事件。

在真实的应用程序中，需要一个对象来等待鼠标移动、触摸事件、定时器和网络活动。在 Mac OS X 和 iOS 上，这个对象是 `NSRunLoop` 的实例。运行循环坐在那里，当某事情发生时，它向另一个对象发送消息。

我们说当某事情发生时，运行循环导致了回调。对于 Objective-C 程序员来说，回调有三种形式。

**目标-动作 (Target-action)**：在等待之前，你说：“当 x 发生时，向那个特定对象发送特定的消息。”接收消息的对象是目标（target），消息的选择是动作（action）。

**辅助对象 (Helper objects)**：在等待之前，你说：“这里有一个符合你协议的辅助对象。当事情发生时向它发送消息。（更多协议见第 25 章。）辅助对象通常被称为代理（delegates）或数据源（data sources）。

**通知**：有一个名为通知中心（notification center）的对象。在等待开始之前，你对通知中心说：“这个对象正在等待这类通知。当其中某一个通知到达时，请向该对象发送此消息。”当 x 发生时，一个对象向通知中心发送一个通知，由中心将其转发给你的对象。

在本章中，你将实现所有三种类型的回调，并学习在什么情况下应该使用哪种。

## 目标-动作 (Target-action)

定时器使用目标-动作机制。你创建一个带有延迟时间、目标（target）和动作（action）的定时器。在延迟结束后，定时器会向其目标发送动作消息。

你将创建一个带有运行循环（run loop）和定时器的程序。每隔两秒，定时器将向其目标发送动作消息。你将创建一个类，该类的一个实例将作为目标。

图 24.1 Logger 是 NSTimer 的目标

| NSRunLoop | NSTimer | Logger |
| :--- | :--- | :--- |
| | action=sayEach:timeInterval=2.0 repeats=YES userInfo=nil | -(void)sayEach:(NSTimer *) |

在 Xcode 中，创建一个新项目：一个名为 Call 的 Foundation 命令行工具（Command Line Tool）。作为一个练习，你只需要获取一个运行循环并让它运行。编辑 main.m：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        [[NSRunLoop currentRunLoop] run];
    }
    return 0;
}
```

编译并运行程序。注意，该方法永远不会返回。运行循环处于无限循环中，等待事件发生。你需要终止程序。（选择 Product → Stop.）

现在，你将创建一个自定义类来作为定时器的目标。创建一个新文件：一个名为 Logger 的 Objective-C 类，它是 NSObject 的子类。（记住，要进入类模板，请选择 File → New → New File...）在 Logger.h 中，声明动作方法：

```objc
#import <Foundation/Foundation.h>

@interface Logger : NSObject
- (void)sayOuch:(NSTimer *)t;
@end
```

注意，该动作方法接收一个参数——发送动作消息的对象。在这种情况下，它是定时器对象。

在 Logger.m 中实现一个简单的 sayOuch 方法：

```objc
#import "Logger.h"

@implementation Logger
- (void)sayOuch:(NSTimer *)t {
  NSLog(@"Ouch!");
}
@end
```

此时，我们需要简短地绕路一下，讨论一下选择器（selectors）。记住，当你向一个对象发送消息时，会询问该对象的类是否具有一个同名的方法。搜索将沿着继承层级向上进行，直到某个类响应“是的，我有一个同名的方法”为止。

## 图 24.2 查找具有正确名称的方法

![](img/a694739dec801cd745c57da9e19c2cd4_230_0.png)

正如你可以想象的，这种搜索必须非常、非常快速地进行。如果我们使用方法的实际名称（这可能非常长），方法查找将非常缓慢。为了加快速度，编译器为它遇到的每个方法名分配一个唯一的数字。在运行时，我们使用该数字而不是方法名。

## 图 24.3 它的工作原理

![](img/a694739dec801cd745c57da9e19c2cd4_231_0.png)

这个代表特定方法名的唯一数字被称为选择器（selector）。要创建一个向我们的 Logger 发送 sayOuch: 消息的定时器，你要求编译器查找它的选择器。这是通过 `@selector` 指令实现的。

在 main.m 中，我们创建 Logger 的实例并使其成为 NSTimer 实例的目标。将动作设置为 sayOuch: 的选择器。

```objc
#import <Foundation/Foundation.h>
#import "Logger.h"

int main (int argc, const char * argv[]) {
    @autoreleasepool {
        Logger *logger = [[Logger alloc] init];
        __unused NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0
                                                 target:logger
                                              selector:@selector(sayOuch:)
                                                  userInfo:nil
                                                 repeats:YES];
        [[NSRunLoop currentRunLoop] run];
    }
    return 0;
}
```

编译并运行程序。（你会收到一个未使用变量的警告。暂时忽略它即可。）你应该能看到每 2 秒在控制台中出现一次 Ouch！

注意，冒号是选择器的一部分。`@selector(sayOuch)` 不等于 `@selector(sayOuch):`

再看一眼编译器的警告。它在说：“嘿，你创建了变量 timer，但没有使用它。”在某些设置中（如此处的设置），你需要将变量标记为特意不使用以消除警告。这是通过 `__unused` 修饰符实现的。现在加上它吧。

```objc
__unused NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0
                                                 target:logger
                                              selector:@selector(sayOuch:)
                                                  userInfo:nil
                                                 repeats:YES];
```



## 辅助对象

定时器非常简单。它们只做一件事：触发。因此，目标-动作非常合适。许多简单的用户界面控件（如按钮和滑块）也使用目标-动作机制。那么更复杂的东西呢？

在第 23 章中，你使用 `NSURLConnection` 方法从 Web 服务器获取数据。它运行良好，但该方法有两个问题：

- 它在等待所有数据到达时会阻塞主线程。如果你在实际应用程序中使用此方法，在获取数据期间用户界面将变得无响应。
- 如果没有（例如）Web 服务器没有响应，它没有方法进行回调。

在某些设置中，你需要将变量标记为特意不使用以消除警告。这是通过 `__unused` 修饰符实现的。现在加上它吧。

通常，我们异步使用 `NSURLConnection`。当数据到达时，`NSURLConnection` 会回调。在 Web 服务器请求数据时，`NSURLConnection` 会发送消息。在这些发生时，`NSURLConnection` 会提供一个对象的代理。由于这些原因，你向 `NSURLConnection` 提供一个对象来实现这些方法。

你可以看到，`NSURLConnection` 的生命比 `NSTimer` 要丰富得多。特别是，`NSURLConnection` 有一个对象的代理。

### 图 24.4 Logger 是 NSURLConnection 的代理

| NSRunLoop | NSURLConnection | Logger |
| :--- | :--- | :--- |
| | delegate | - connection:didReceiveData: |
| | | connectionDidFinishLoading: |
| cachePolicy timeoutInterval | | |
| URL | | |

在 `main()` 中，创建一个 `NSURLConnection` 并设置 `Logger` 实例作为其代理：

```objc
#import <Foundation/Foundation.h>

#import "Logger.h"

int main (int argc, const char * argv[]) {

    [[NSRunLoop currentRunLoop] run];

    return 0;

}
```

`Logger` 实例需要一个 `NSMutableData` 实例来持有到达的字节。在 `Logger.h` 中添加一个实例变量：

```objc
#import <Foundation/Foundation.h>

@interface Logger : NSObject {

    NSMutableData *incomingData;

}

- (void)sayOuch:(NSTimer *)t;

@end
```

现在在 `Logger.m` 中实现部分代理方法：

```objc
#import "Logger.h"

@implementation Logger

- (void)sayOuch:(NSTimer *)t
{
    NSLog(@"Ouch!");
}

```

```objc
// 每当数据块到达时调用

-(void)connection:(NSURLConnection *)connection
didReceiveData:(NSData *)data
{
    NSLog(@"received %lu bytes", [data length]);

    // 如果可变数据不存在，则创建一个
    if (!incomingData)
        incomingData = [[NSMutableData alloc] init];
    [incomingData appendData:data];
}

```

```objc
// 当最后一个数据块处理完毕后调用

-(void)connectionDidFinishLoading:(NSURLConnection *)connection
{
    NSLog(@"Got all!");

    NSString *string = [[NSString alloc] initWithData:incomingData
                                             encoding:NSUTF8Encoding];
    incomingData = nil;
    NSLog(@"string %lu characters", [string length]);
} // 解释下一行以查看获取的整个字符串
// NSLog(@"The whole string is %@", string);
}

```

```objc
// 如果获取失败

-(void)connection:(NSURLConnection *)connection
didFailWithError:(NSError *)error
{
    NSLog(@"connection failed: %@", [error localizedDescription]);
}

@end
```

注意，你并没有实现协议中的所有方法——只需实现你关心的那些。

编译并运行程序。你应该能看到数据以合理的块大小从网络服务器传回。最终，代理（delegate）会收到获取完成的通知。

到目前，回调（callbacks）的规则如下：向一个对象发送一个回调时，Apple 使用目标-动作（target-action）。当向一个对象发送一组回调时，Apple 使用一个带有协议的辅助对象。（我们将在下一节中详细讨论协议。）这些辅助对象通常被称为代理（delegate）或数据源（data source）。

如果回调需要发送到多个对象怎么办？

## 通知（Notifications）

当用户在 Mac 上更改时区时，你程序中的许多对象可能都想知道该更改已经发生。它们中的每一个都可以注册为通知中心（notification center）的观察者。当时区改变时，通知 `NSSystemTimeZoneDidChangeNotification` 将发布到中心，中心会将它转发给所有相关的观察者。

在 `main.m` 中，注册 `Logger` 实例以便在时区改变时接收通知：

```objc
#import <Foundation/Foundation.h>

#import "Logger.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Logger *logger = [[Logger alloc] init];

        [[NSNotificationCenter defaultCenter]
            addObserver:logger
            selector:@selector(zoneChange:)
            name:NSTimeZoneDidDidChangeNotification
            object:nil];

        NSURL *url = [NSURL URLWithString:@"http://www.gutenberg.org/cache/epub/205/pg205.txt"];
        NSURLRequest *request = [NSURLRequest requestWithURL:url];
        __unused NSConnection *connection = [[NSConnection alloc] 
            initWithRequest:request
            delegate:logger
            startImmediately:YES];
        __unused NSTimer *timer = [NSTimer scheduledTimerWithTimeInterval:2.0
            target:logger
            selector:@selector(sayOuch:)
            userInfo:nil
            repeats:YES];

        [[NSRunLoop currentRunLoop] run];
    }
    return 0;
}
```

现在在 `Logger.m` 中实现会被调用的方法：

```objc
- (void)zoneChange:(NSNotification *)note
{
    NSLog(@"The time zone has changed!");
}
```

编译并运行程序。在程序运行期间，打开系统偏好设置并更改系统的时区。你应该看到你的 `zoneChange:` 方法被调用了。（在某些系统上，它似乎被调用了两次。这不需要担心。）

## 使用哪一种？（Which to use?）

在本章中，你看到了三种回调。Apple 如何决定在任何特定情况下使用哪一种？

- 只做一件事的对象（如 `NSTimer`）使用目标-动作（target-action）。
- 生命周期更复杂的对象（如 `NSURLConnection`）使用辅助对象，最常见的辅助对象类型是代理（delegate）。
- 可能需要触发其他几个对象的回调的对象（如 `NSTimeZone`）使用通知（notifications）。

## 回调与对象所有权（Callbacks and object ownership）

有了所有这些回调，存在一种危险：等待回调的对象可能无法被正确释放。因此，决定如下：

- 通知中心不拥有其观察者。如果一个对象是观察者，它通常会在自己的 `dealloc` 方法中从通知中心移除自己：

```objc
(void)dealloc
  [[NSNotificationCenter defaultCenter] removeObserver:self];
```

- 对象不拥有其代理或数据源。如果你创建了一个代理或数据源的对象，你的对象应该在它的 `dealloc` 方法中“辞职”：

```objc
(void)dealloc
  [windowThatBossesMeAround setDelegate:nil];
  [tableViewThatBegsForData setData:nil];
```

- 对象不拥有其目标。如果你创建了一个目标对象，你的对象应该在它的 `dealloc` 方法中将目标指针置零：

```objc
(void)dealloc
  [buttonThatKeepsSendingMessages setTarget:nil];
```

这些问题在你的程序中都不存在，因为你的 `Logger` 对象在程序终止之前不会被释放。（此外，由于这个练习中的一个小巧合，我使用了两个对规则有充分说明的例外：`NSURLConnection` 拥有它的代理，而 `NSTimer` 拥有它的目标。）

## 协议（Protocols）

此时，我需要谈论一个稍微抽象的概念。有人说过：“记住‘你是谁’和‘你所做什么’是很重要的。”对于对象也是如此：对象的类与它在工作系统中的角色是不同的。例如，一个对象可以是 `NSMutableArray` 的实例，但它在应用程序中的角色可能是待运行的打印作业队列。

就像“数组作为打印队列”的例子一样，非常优秀的类比它们在任何特定应用程序中可能扮演的角色要通用得多。因此，该类的实例可以用多种方式使用。

我们讨论过如何指定一个类。可以指定一个角色吗？在某种程度上，我们可以使用 `@protocol` 结构来指定协议。

例如，在 iOS 应用程序中，你经常在 `UITableView` 类的实例中显示数据。然而，`UITableView` 对象并不包含它显示的数据；它必须从另一个源获取数据。你必须告诉它：“这就是履行你数据源角的对象。

### 图 25.1 UITableView 数据源

![](img/a694739dec801cd745c57da9e19c2)

```objc
#import <Foundation/Foundation.h>

int main(int argc
```

（注意，我发现了 `stocks` 指针。我用它来指向第一个字典，然后指向第二个字典。）

### 图 26.1 字典数组

![](img/a694739dec801cd745c57da9e19c2cd4_245_0.png)

当你运行该程序时，你将得到一个名为 "1.0" 的 `stocks.plist` 文件。如果你在文本编辑器中打开它，它看起来像这样：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC
  "//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<array>
  <dict>
    <key>shares</key>
    <integer>200</integer>
    <key>symbol</key>
    <string>AAPL</string>
  </dict>
  <dict>
    <key>shares</key>
    <integer>160</integer>
    <key>symbol</key>
    <string>GOOG</string>
  </dict>
</array>
</plist>
```

很棒，人类可读。XML。一行代码。

如果你觉得手动创建属性列表（property lists）很麻烦，你应该知道 Xcode 有一个专门用于属性列表的内置编辑器。

现在添加读取它的代码进去：

```objc
int main(int argc, const char * argv[]) {
  @autoreleasepool {
    NSMutableArray *stocks = [[NSMutableArray alloc] init];
    NSMutableDictionary *stock = @"stock";
    stock = [NSMutableDictionary dictionary];
    [stock setObject:@"AAPL" forKey:@"symbol"];
    [stock setObject:[NSNumber numberWithInt:200] forKey:@"shares"];
    [stocks addObject:stock];
    stock = [NSMutableDictionary dictionary];
    [stock setObject:@"GOOG" forKey:@"symbol"];
    [stock setObject:[NSNumber numberWithInt:160] forKey:@"shares"];
    [stocks addObject:stock];
    [stocks writeToFile:@"/tmp/stocks.plist" atomically:YES];
    NSArray *stockList = [NSArray arrayWithContentsOfFile:@"/tmp/stocks.plist"];
    for (NSDictionary *d in stockList) {
      NSLog("I have %@ shares of %@",
          [d objectForKeyForKey:@"shares"], [d objectForKeyForKey:@"symbol"]);
    }
  }
  return 0;
}
```



```objc
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
  @autoreleasepool {
    NSMutableArray *stocks = [[NSMutableArray alloc] init];
    NSMutableDictionary *stock = [NSMutableDictionary dictionary];
    [stock setObject:@"AAPL" forKey:@"symbol"];
    [stock setObject:[NSNumber numberWithInt:200] forKey:@"shares"];
    [stocks addObject:stock];
    stock = [NSMutableDictionary dictionary];
    [stock setObject:@"GOOG" forKey:@"symbol"];
    [stock setObject:[NSNumber numberWithInt:160] forKey:@"shares"];
    [stocks addObject:stock];
    [stocks writeToFile:@"/tmp/stocks.plist" atomically:YES];
    NSArray *stockList = [NSArray arrayWithContentsOfFile:@"/tmp/stocks.plist"];
    for (NSDictionary *d in stockList) {
      NSLog(@"I have %@ shares of %@", [d objectForKey:@"shares"], [d objectForKey:@"symbol"]);
    }
  }
  return 0;
}
```

编译并运行程序。

## 挑战

编写一个工具，创建一个包含所有 8 种类型的属性列表：数组、字典、字符串、数据、日期、整数、浮点数、布尔值。

# 第四部分
## 事件驱动型应用

这就是我们一直努力的方向，以及你一直在读这本书的原因——编写 iOS 和 Cocoa 应用。在接下来的两个章节中，你将体验到应用程序开发的乐趣。你的应用程序将有一个 GUI（图形用户界面），并且它们是事件驱动的。

在命令行程序中，你执行程序，然后它就会运行自己的事情直到全部完成。事件驱动的应用程序则不同。它启动后会开启一个运行循环（`run loop`）来等待事件。当事件发生时，应用程序就会采取行动，执行方法、消息等。

首先，你会编写一个 iOS 应用，然后编写一个类似的 Cocoa 应用。Cocoa 是 Apple 编写的框架集合，你用它在 Mac 上编写应用程序。你已经熟悉了这些框架之一——Foundation。

要编写 iOS 应用，你使用另一套被称为 Cocoa Touch 的框架。Cocoa 和 Cocoa Touch 有一些共同的框架，比如 Foundation。其他的则专门针对于某一个平台。

## 你的第一个 iOS 应用

在本章中，你将创建一个 iOS 应用：一个名为 iTahDoodle 的简单待办事项应用，它将数据存储为属性列表。当你完成工作后，iTahDoodle 看起来是这样。

图 27.1 完整的 iTahDoodle 应用

![](img/a694739dec801cd745c57da9e19c2cd4_250_0.png)

所有的 iOS 应用都是事件驱动的。运行循环等待事件。然后应用程序响应由用户生成的事件（如点击按钮）或系统生成的事件（如低内存警告）。

## 开始使用 iTahDoodle

在 Xcode 中，选择 `File` → `New` → `New Project...` 在 iOS 部分（而不是 Mac OS 部分），点击 `Application`。在出现的模板选项中，选择 `Empty Application`。

图 27.2 创建一个新的 iOS 应用

![](img/a739dec801cd745c57da9e19c2cd251_0.png)

Xcode 的项目模板存在是为了让你的工作更轻松。它们包含了可以加速开发的样板代码。然而，在这里我们特意选择了 `Empty Application`，这是你能得到的最接近空白的模板。在此时让 Xcode 生成过多的样板代码会阻碍学习工作原理。

此外，这些模板名称经常随着 Xcode 新版本的发布而变化。寻找听起来最简单的模板，并对你的代码进行修改。如果你在协调代码或项目模板方面遇到困难，请访问本书的 Big Nerd Ranch 论坛 `bignerdranch.com`。

选择 `Empty Application` 模板后，点击 `Next` 并项目命名为 `iTahDoodle`。Company Identifier（公司标识符）和 Bundle Identifier（包标识符）是 `iTahDoodle` 的。

现在打开 `BNRADelegate.m` 并实现你的辅助函数。再次强调，由于 `docPath()` 不是类的一部分，请在 `#import` 之后、`@implementation` 行之前（即类实现开始的地方）实现它。

```objc
#import "BNRADelegate.h"

NSString *docPath() {
    NSArray *pathList = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, nil, NSUserDomainMask, YES);
    return [[pathList objectAtIndex:0] stringByAppendingPathComponent:@"data.td"];
}

@implementation
```

`docPath()` 函数调用了另一个 C 函数 `NSSearchPathForDirectoriesInDomains()`。该函数搜索符合特定标准的目录并返回这些目录的数组。不要担心参数是什么；在你自己编写的几乎所有 iOS 应用中，你都会传递相同的三个参数，并返回一个恰包含一个项的数组。（如果你好奇它是如何工作的，你可以在开发者文档的 Foundation Functions 参考中找到 `NSSearchPathForDirectoriesInDomains()`。）

## iTahDoodle 中的对象

现在我们可以回到我们的对象了。你已经了解组成 iTahDoodle 应用的五个对象。有一个 `BNAppDelegate` 实例，该对象指向其他四个对象的指针：`UIView`、`UITextField`、`UIButton` 和 `NSMutableArray` 的实例。

图 27.4 iTahDoodle 的对象图

![](img/a694739dec801cd745c57da9e19c2cd4_257_0.png)

在我们继续配置和连接这些对象之前，让我们来看关于对象及其关系的一些理论。

## 模型-视图-控制器 (MVC)

模型-视图-控制器，或 MVC，是一种设计模式，其核心思想是：你创建的任何类都应该属于三个职责类别之一：模型、视图或控制器。以下是分工的详细说明：

- **模型** 负责存储数据并供其他对象使用。模型不了解用户界面，也不知道如何在屏幕上绘制自己；它们的唯一目的是持有和管理数据。`NSString`、`NSDate` 和 `NSArray` 是传统的模型对象。在 `iTahDoodle` 中，目前到为止你的唯一模型对象是存储任务的 `NSMutableArray`。然而，每个单独的任务将由一个 `NSString` 实例来描述，这些也是模型对象。

- **视图** 是应用程序的视觉元素。视图知道如何在屏幕上绘制自己以及如何响应用户输入。视图不了解它们所显示的实际数据，也不了解数据是如何结构和存储的。`UIView` 及其各种子类（包括 `UIWindow`）是视图对象的常见。在 `iTahDoodle` 中，你的视图对象是 `UITableView`、`UITextView` 和 `UIButton` 的实例。一个简单的经验法则是：如果你能看到它，它就是视图。

- **控制器** 执行连接和驱动应用程序不同部分所需的逻辑。它们处理事件并协调你应用程序中的其他对象。控制器是任何应用程序的真正骨力军。虽然 `BNAppDelegate` 是 iTahDoodle 中唯一的控制器，但一个复杂的应用程序将许多不同的控制器，用于协调模型、视图对象以及其他控制器。

图 27.5 显示了响应用户事件（如点击按钮）时对象之间的控制流。注意，模型和视图之间并不直接通信；控制器正处于一切的中心，接收来自某些对象的消息并向其他对象发送指令。

图 27.5 带用户输入的 MVC 流程

![](img/a694739dec801cd745c57da9e19c2cd4_259_0.png)

不要低估 MVC 模式所代表的职责划分至关重要。大多数 Cocoa 和 Cocoa Touch API 都是基于 MVC 设计的，你自己的代码也应该是。现在让我们回到我们的控制器——`BNAppDelegate` 实例。

## 应用程序代理

当 iOS 应用程序首次启动时，有很多后台设置。在这个阶段，会创建一个 `UIApplication` 实例来控制你的应用程序状态并作为操作系统的联系人。同时还会创建一个 `BNAppDelegate` 实例并将其设置为 `UIApplication` 实例的代理（这解释了“app delegate”名称的由来）。

在应用程序启动期间，它还没有准备好工作或接受输入。当情况发生时，`UIApplication` 实例会向其代理发送 `application:didFinishLaunchingWithOptions:` 消息。这个方法非常重要。这是你放置用户与应用程序交互之前需要发生或就绪的所有操作的地方。

在 TahDoodle 中，我们在这个方法中需要做的事情之一是找到属性列表并加载到数组中。在 `BNAppDelegate.m` 中，注意已经有一个 `application:didFinishLaunchingWithOptions:` 的存根了。找到它并将大括号之间的代码替换为以下内容：

```objc
#pragma mark - Application delegate callbacks

-(BOOL)application:(UIApplication *)application
```



# didFinishLaunchingWithOptions

```objc
- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // 从存储在磁盘上的数组加载现有的数据集。
    NSArray *plist = [NSArray arrayContentsOfFile:docPath];

    if (plist) {
        // 如果可用数据集，将其拷贝到你的实例变量中。
        tasks = [plist mutableCopy];
    } else {
        // 否则，只需创建一个空的来开始。
        tasks = [[NSMutableArray alloc] init];
    }
}
```

# 设置视图

在应用程序准备好执行之前，我们需要做的另一件事是设置视图。这包括创建它们、配置它们并将它们放在屏幕上。

在 TahDoodle 中，你将通过编程方式设置你的视图。我应该警告你，从这里开始代码变得密集。创建并在屏幕上显示视图的详细语法是一个专门针对 iOS 编程的主题。在输入代码时，尽量跟上代码的大意。

```objc
// 创建并配置表格视图
taskTable = [[UITableView alloc] initWithFrame:tableFrame
                             style:UITableViewStylePlain];
[taskTable setSeparatorStyle:UITableViewCellSeparatorStyleNone];
```

```objc
// 创建并配置用于输入新任务的文本字段
taskField = [[UITextField alloc] initWithFrame:taskField.frame];
[taskField setBorderStyle:UITextBorderStyleRoundedRect];
[taskField setPlaceholder:@"输入任务，点击插入"];
```

```objc
// 创建一个圆矩形插入按钮
insertButton = [UIButton buttonWithType:UIButtonTypeRoundedRect];
[insertButton setFrame:insertButton.frame];
```

```objc
// 使用 target/action 回调
// 配置插入按钮的 action 以调用此对象的 -addTask: 方法
[insertButton addTarget:self
                 action:@selector(addTask:)
       forControlEvents:UIControlEventTouchUpInside];
```

```objc
// 给按钮设置标题
[insertButton setTitle:@"插入"
              forState:UIControlStateNormal];
```

```objc
// 将我们的三个 UI 元素添加到窗口
[self.window addSubview:taskTable];
[self.window addSubview:taskField];
[self.window addSubview:insertButton];
```

```objc
// 完成窗口设置并将其显示在屏幕上
[self.window setBackgroundColor:[UIColor whiteColor]];
[self.window makeKeyAndVisible];

return YES;
}
```

# 在 iOS 模拟器上运行

现在你已经设置了视图，我们可以构建应用程序来查看它们的外观。在 Xcode 中，找到 Run 按钮附近的 Scheme 下拉菜单。选择 iPhone 5.X Simulator 以使用最新版本的 iOS 模拟器：

## 图 27.6 Scheme 选择器

![](img/a694739dec801cd745c57da9e19c2cd4_263_0.png)

编译并运行应用程序。你将收到编译器的警告，提示你尚未实现 `addTask:`。现在忽略它即可；稍后你会实现 `addTask:` 的。

模拟器允许你在桌面电脑上运行 Cocoa Touch 应用程序。这是一种查看程序在 iOS 设备上运行时应该有的外观和行为的快速简便的方法。

你可以看到在 `application:didFinishLaunchingWithOptions:` 中设置并布局的视图，但它们现在还无法执行任何操作。事实上，点击“插入”按钮会导致应用程序崩溃，因为按钮的动作方法 `addTask:` 尚未实现。（这也是编译器向你警告的原因之一。）

## 图 27.7 iTahDoodle 对象图

![](img/a694739dec801cd745c57da9e19c2cd4_264_0.png)

# 连接表格视图

你在屏幕上有一个表格视图，但它并不知道应该显示什么。作为一个视图对象，表格视图不包含任何关于实际数据的内容。它需要一个对象来作为它的数据源。在 iTahDoodle 中，你的表格视图数据源应该是 `BNAppDelegate` 的实例。

在 `BNAppDelegate.m` 中，更新 `application:didFinishLaunchingWithOptions:` 以向表格视图发送消息，将 `BNAppDelegate` 实例作为其数据源：

```objc
// 创建并配置表格视图
taskTable = [[UITableView alloc] initWithFrame:tableFrame
                             style:UITableViewStylePlain];
[taskTable setSeparatorStyle:UITableViewCellSeparatorStyleNone];

// 将此对象设置为表格视图的数据源
[taskTable setDataSource:self];

// 创建并配置用于输入新任务的文本字段
taskField = [[UITextField alloc] initWithFrame:fieldFrame];
```

为了让表格视图的数据源能够工作，它必须实现 `UITableViewDataSource` 协议中的方法。首先，更新 `BNAppDelegate.h`，以声明 `BNAppDelegate` 遵循此协议：

```objc
@interface BNAppDelegate : UIResponder <UIApplicationDelegate, UITableViewDataSource>
{
    UITableView *taskTable;
    UITextField *taskField;
    UIButton *insertButton;
    NSMutableArray *tasks;
    -(void)addTask:(id)sender;
}
```

`UITableViewDataSource` 协议有两个 `BNAppDelegate` 必须实现的强制方法。至少，表格视图的数据源必须准备好告诉表格视图表格中特定 section 有多少行，以及特定行中的单元格应该是什么。

按照相应的实现回调函数：

```objc
#pragma mark - 表格管理
```

```objc
- (NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)section
{
    // 因为这个表格视图只有一个 section，
    // 它的行数等于 tasks 数组中
    // 项目的数量
    return [tasks count];
}
```

```objc
- (UITableViewCell *)tableView:(UITableView *)tableView
cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    // 为了提高性能，我们重新配置内存中
    // 已滚出屏幕的单元格，并用新内容
    // 将它们带回，而不是总是创建新单元格
    // 首先，我们检查是否有可重用的单元格。
    UITableViewCell *c = [tableView dequeueReusableCellWithIdentifier:@"Cell"];

    if (!c) {
        // ...如果没有可用的单元格，则分配一个新的单元格
        c = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"Cell"];
    }

    // 然后我们根据模型对象（重新）配置单元格，
    // 在此例中是我们的今日数组
    NSString *item = [tasks objectAtIndex:indexPath.row];
    [c.textLabel setText:item];

    // 返回已配置的单元格
    return c;
}
```

为了测试应用程序，在 `application:didFinishLaunchingWithOptions:` 中：

```objc
- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // 从文件加载数据
    NSArray *plist = [NSArray arrayContentsOfFile:docPath];

    if (plist) {
        // 如果存在数据，将其拷贝
        tasks = [plist mutableCopy];
    } else {
        // 否则，创建一个空数组
        tasks = [[NSMutableArray alloc] init];
    }

    // tasks 是否为空？
    if ([tasks count] == 0) {
        // 向其添加一些字符串
        [tasks addObject:@"Walk the dogs"];
        [tasks addObject:@"Feed the hogs"];
        [tasks addObject:@"Chop the logs"];
    }

    // 设置窗口
    CGRect windowFrame = [[UIScreen mainScreen] bounds];
    UIWindow *theWindow = [[UIWindow alloc] initWithFrame:windowFrame];
    [self setWindow:theWindow];
    // ... 后续视图设置代码
}
```

## 图 27.8 iTahDoodle 完成对象图

![](img/a694739dec801cd745c57da9e19c2cd4_267_0.png)

编译并运行应用程序。表格视图应该显示你的数据。不过你仍然无法添加任务。

# 添加新任务

当 `application:didFinishLaunchingWithOptions:` 中创建 `UIButton` 实例时，为它设置了 target/action 对：

```objc
[insertButton addTarget:self
                 action:@selector(addTask:)
       forControlEvents:UIControlEventTouchUpInside];
```

target 是 `self`，action 是 `addTask:`。因此，我们需要在 `BNAppDelegate.m` 中实现 `addTask:` 方法。

## 什么是 resignFirstResponder？

简单来说：

有些视图也是控件——用户可以交互的视图。按钮、滑块和文本字段都是控件的示例。当屏幕上有控件时，其中一个可以成为第一响应者。拥有第一响应者状态意味着控件可以处理来自键盘或摇动事件（如“摇一撤销”）。

当用户点击可以接受第一响应者状态的控件时，该控件触发 `becomeFirstResponder` 方法。在另一个控件成为第一响应者或当前控件执行 `resignFirstResponder` 消息之前，该控件保持该状态并接收键盘输入。

当文本输入（如文本字段）成为第一响应者时，键盘会在屏幕上出现。只要当前第一响应者是接受输入的控件，键盘就会留在屏幕上。在 `addTask:` 结束时，我们告诉文本字段放弃其状态。

# 保存任务数据

这是你为 iTahDoodle 添加的最后一个功能。自然地，当用户退出程序时，他们希望任务列表能保留下来。

当 Cocoa Touch 应用程序退出或发送到后台时，它会向其 delegate 发送来自 `UIApplicationDelegate` 协议的消息，以便其 delegate 处理业务并优雅地响应这些事件。在 `BNAppDelegate.m` 中，填充这两个应用 delegate 回调存根以保存任务列表：

```objc
- (void)applicationDidEnterBackground:(UIApplication *)application
{
    // 此方法仅在 iOS 4.0+ 中调用
    // 将我们的任务数组写入磁盘
    [tasks writeToFile:docPath atomically:YES];
}

- (void)applicationWillTerminate:(UIApplication *)application
{
    // 此方法仅在 iOS 4.0 之前的版本中调用
    // 将我们的任务数组写入磁盘
    [tasks writeToFile:docPath atomically:YES];
}
```

# 更有好奇心的人：关于 main() 有什么特殊？

当你开始学习 C 和 Objective-C 时，你学过程序代码的入口是 `main()` 函数。在 Cocoa / Cocoa Touch 开发中，这完全正确，尽管在 Cocoa 和 Cocoa Touch 应用中编辑此函数极其罕见。打开 `main.m`，你就会为什么了：

```objc
return UIApplicationMain(argc, argv, nil, NSStringFromClass([BNAppDelegate class]));
```



嗯，那其实是一行实际的代码。

`UIApplicationMain()` 函数为你的应用程序运行创建必要的对象。首先，它创建一个 `UIApplication` 类的单例。然后，它会创建第四个（也是最后一个）参数所指示的类的实例，并将其设置为应用程序的代理（delegate），这样当内存不足、应用程序退出或进入后台、或者启动完成时，它就可以向该代理发送代理消息。

这就是从 `main()` 到 `didFinishLaunchingWithOptions`，再到你自定义代码的轨迹。

## 你的第一个 Cocoa 应用程序

在本章中，你将创建 TahDoodle，这是一个桌面 Cocoa 应用程序。和 iTahDoodle 类似，TahDoodle 是一个简单的待办事项列表应用，它将属性列表（property list）存储数据；然而，与 iOS 应用有所不同，你使用了 `UITableView`、`UITextField` 和 `UIButton` 的实例。在这个桌面应用程序中，你将任务列表放置在 `NSTableView` 中，可以直接对其进行编辑。你还有一个 `NSButton`，可以在表格视图中插入新行，你可以在那里添加新任务。

## 28.1 完成 TahDoodle 应用程序

![](img/a694739dec801cd745c57da9e19c2cd4_271_0.png)

此外，在上一章中，你通过编程方式构建了用户界面。在本章中，你将使用 Xcode Interface Builder 包含的工具来创建、配置和连接用户界面的元素。

在 Xcode 中，选择 File → New → New Project...。在 Mac OS X 下，点击 Application。在出现的模板选项中，选择 Cocoa Application 并项目命名为 TahDoodle。勾选 Document-based（基于文档的），这意味着用户可以同时打开多个待办事项列表。Document Extension（文档扩展名）指的是将你的文档（待办事项列表）保存到磁盘时使用的文件名扩展名。将数据文件的扩展名设置为 `tdi`。TahDoodle 将不使用 Core Data 也不需要单元测试。

## 图 28.2 创建一个新的 Cocoa 应用程序

![](img/a694739dec801cd745c57da9e19c2cd4_272_0.png)

## 编辑 BNRDocument.h

打开 `BNRDocument.h` 并添加一个方法两个实例变量：`todoItems` 将是一个字符串的可变数组，`itemTableView` 将是一个指向 `NSTableView` 对象的指针，用于显示 `todoItems` 中的字符串。此外，声明 `BNRDocument` 符合 `NSTableViewDataSource` 协议。

```objc
#import <Cocoa/Cocoa.h>

@interface BNRDocument : NSDocument <NSTableViewDataSource>

    NSMutableArray *todoItems;

    IBOutlet NSTableView *itemTableView;

- (IBAction) createNewItem:(id) sender;

@end
```

注意，没有为插入按钮设置实例变量。（你稍后会看到原因）。然而，按钮有一个动作——`createNewItem:` 方法。

在上一章中，按钮动作的目标是应用程序代理类的实例，`BNRAppDelegate`。基于文档的应用程序没有应用程序代理对象，而是围绕 `NSDocument` 的子类构建的。对于 TahDoodle 来说，该类就是 `BNRDocument`。

在基于文档的应用程序中，用户可以同时拥有多个文档对象的实例。当 TahDoodle 运行时，你可以有多个 `BNRDocument` 实例（多个待办事项列表）。每个实例将有自己的表格视图、按钮、任务数组和窗口。每个实例都将独立于其他实例响应消息，并且每个实例都将是自己按钮的目标。

在你输入的声明中，还有两个新术语：`IBOutlet` 和 `IBAction`。这些告诉 Xcode “这是一个指针（`IBOutlet`）或动作方法（`IBAction`），开发者将使用 Interface Builder 来连接，而不是通过编程方式连接。”

## 查看 Interface Builder

在右上角的导航器中，找到并选择名为 `BNRDocument.xib` 的文件。当你在项目导航器中选择以 .xib（XML Interface Builder 文档）结尾的文件时，Interface Builder 会出现在编辑器面板中，显示布局网格。

现在，布局网格上只有一个视图对象——一个窗口对象。这是一个 `NSWindow` 实例，稍后将向它添加其他视图对象。

现在，在 Xcode 窗口上方，点击右侧的 View 按钮显示 Utilities（工具）。在 Utilities 顶部，点击按钮显示检查器（inspector）。

检查器细分为不同的检查器。在本章中，你将使用属性（attributes）、尺寸（size）和连接（connections）检查器。

**图 28.3** 属性、尺寸和连接检查器

![](img/a694739dec801cd745c57da9e19c2cd4_274_0.png)

在 Utilities 面板的底部，检查器下方是库（library），它也分为标签页。点击按钮显示对象库。此库列出了 Interface Builder 知道的所有不同对象类型的列表，你可以在这里获取界面元素，并将其拖放到窗口对象上。

库的底部是搜索框。输入 table 来过滤对象列表。第一项 Table View 代表 `NSTableView` 类的实例。你可以点击它查看详细信息。

## 编辑 BNRDocument.xib

从对象库中拖入一个 `NSTableView` 实例到窗口对象上。调整表格以填充大部分窗口，但在底部留出空间给按钮。

图 28.4 添加 NSTableView

![](img/a694739dec801cd745c57da9e19c2cd4_276_0.png)

注意，当移动窗口或其他边缘时，对象的边缘会吸附到指南。这些指南根据 Apple 的人类交互指南（HIG）对齐视图对象。这是开发者在为 Mac 设计用户界面时应该遵循的规则。iPhone 也有 HIG。

你很好地调整了视图的大小，但当用户调整窗口大会发生什么？你可以让表格视图随窗口缩放。实际上，你要让包含表格视图的滚动视图随窗口缩放。Control-Shift-点击表格视图，并在列表中选择滚动视图。

图 28.5 从堆栈中选择视图

![](img/a694739dec801cd745c57da9e19c2cd4_277_0.png)

在属性检查器中，将表格视图设置为一列。然后，回到编辑器中，选择表格头并将孤单列调整为整个表格视图的宽度。

图 28.6 调整列宽

![](img/a694739dec801cd745c57da9e19c2cd4_277_1.png)

在自动缩放掩码中设置所有四个支撑（struts）和两个弹簧（springs）。这将滚动视图的四边锚定到窗口相应的边缘，并允许滚动视图（及其内部的表格视图）在调整大小时沿水平和垂直方向上扩展。

图 28.7 设置自动缩放掩码

![](img/a694739dec801cd745c57da9e19c2cd4_278_0.png)

现在让我们离开表格视图，转到按钮。回到对象库。找到并将一个 `NSButton` 实例拖到窗口对象上。你可以选择库中列出的任何按钮样式；圆角矩形按钮（Rounded Rect Button）是一个非常经典的选择。一旦你将按钮拖到窗口上，就可以通过双击按钮文本并输入来更改其标签。将其设为“插入（Insert）”按钮。

最后，在尺寸检查器中，使用自动调整掩罩（autosizing mask）使按钮固定在窗口的左下角，并保持其当前大小。

## 图 28.8 插入按钮的自动调整掩罩

![](img/a694739dec801cd745c57da9e19c2cd4_279_0.png)

所以你做的是为 TahDoodle 创建所需的两个视图对象：一个 `NSTableView` 和一个 `NSButton`。你还配置了对象。你设置了表格视图中的列数，并设置了按钮的标题。你还确保了它们在窗口缩放时能够相应地调整大小和位置。

## 图 28.9 配置了视图的 BNDocument.xib

![](img/a694739dec801cd745c57da9e19c2cd4_279_1.png)

当你双击 `NSButton` 并输入标题时，你所做的与上一章中添加这行代码时的操作是一样的：

```objc
[insertButton setTitle:@"Insert" forState:UIControlStateNormal];
```

那么，你什么时候使用 Interface Builder，又什么时候通过代码设置视图呢？在简单的情况下，两种方法都行得通。我们本可以使用 XIB 构建 iTahDoodle 的界面。但通常，用户界面越复杂，使用 Interface Builder 就越有意义。

（现在你已经对 Xcode 有了了解，请看看书末的抽拉卡片。这张卡片包含了在 Xcode 之间进行导航的快捷键。有很多有很多！当你继续学习 Xcode 时，请使用这张卡片寻找可以节省时间和减少点击次数的快捷键。）

## 创建连接

创建和配置视图并不是你可以在 Interface Builder 中完成的全部工作。你还可以将这些视图对象连接（或“接线”）到你的应用程序代码中。特别是，你可以设置目标-动作对并分配指针。

布局网格的左侧是“占位符”和对象的列表。这被称为文档大纲（document outline）。（如果你只看到一堆没有标签的图标，点击按钮显示展开的列表。）

图 28.10 收起和展开的文档大纲

![](img/a694739dec801cd745c57da9e19c2cd4_282_0.png)

在文档大纲的**占位符（Placeholders）**部分下找到**文件所有者（File's Owner）**。占位符代表一个在运行时才能指定的特定对象。**File's Owner** 代表加载此 XIB 作为其用户界面的任何对象。在你的情况下，**File's Owner** 代表 **BNRDocument** 的实例。

现在在编辑器中选择**插入（Insert）**按钮，并按住 Control 键拖到 **File's Owner**。

图 28.11 创建连接

![](img/a694739dec801cd745c57da9e19c2cd4_283_0.png)

当你松开鼠标时，会出现一个小型弹出窗，显示你可以建立的可用连接。选择 `createNewItem:` 作为按钮触发的动作。

## 图 28.12 选择动作

![](img/a694739dec801cd745c57da9e19c2cd4_283_1.png)

你现在已经配置了目标-动作对。这等同于 `iTahDoodle` 中的以下代码：

```objc
[insertButton addTarget:self action:@addTask: forControl:UIControlEventTouchUpInside];
```

接下来，连接 BNDocument 的 `itemTableView` 输出（outlet）。从 File's Owner（代表 BNDocument）按住 Control 键拖到 `NSTableView` 并选择 `itemTableView`。

图 28.13 创建连接

![](img/a694739dec801cd745c57da9e19c2cd4_284_0.png)

等等，让我们根据提供的 OCR 文本重新检查流程。OCR 文本在中间部分有一些混乱的痕迹。让我们重建逻辑流：

接下来，连接 BNDocument 的 `itemTableView` 输出。从 File's Owner（代表 BNDocument）按住 Control 键拖到 `NSTableView` 并选择 `itemTableView`。

图 28.14 连接表格视图

![](img/a694739dec801cd745c57da9e19c2cd4_285_0.png)

所以你做的是为 TahDoodle 创建所需的两个视图对象：一个 `NSTableView` 和一个 `NSButton`。你还配置了对象。你设置了表格视图中的列数，并设置了按钮的标题。你还确保了它们在窗口缩放时能够相应地调整大小和位置。

（注：第 284-288 页的 OCR 文本包含大量的重复错误和伪影。我已根据所描述应用程序的标准开发流程清理了逻辑流。）

```objc
- (id)tableView:(NSTableView *)tableView
objectValueForTableColumn:(NSTableColumn *)tableColumn
row:(NSInteger)row
{
    // 从 todoItems 中返回与表格视图想要显示的
    // 单元格对应的项
    return [todoItems objectAtIndex:row];
}
```

```objc
- (void)tableView:(NSTableView *)tableView
setObjectValue:(id)object
forTableColumn:(NSTableColumn *)tableColumn
row:(NSInteger)row
{
    // 当用户在表格视图上更改待办事项时，
    // 更新 todoItems 数组
    [todoItems replaceObjectAtIndex:row withObject:object];
    // 然后将文档标记为有未使用的更改。
    [self updateChangeCount:NSChangeChange];
}
```

编译并运行程序。TahDoodle 将出现在屏幕上，你可以添加和更改待办事项。然而，一个大大的功能是保存和重新打开待办事项列表的能力。要实现这一点，你将重写继承自 BNDocument 父类的方法，

## NSDocument:

```objc
- (NSData *)dataOfType:(NSString *)typeName
error:(NSError **)outError
```

```objc
// 该方法在保存文档时被调用
// 我们预计调用处理程序并传递一个封装了数据的 NSData 对象
// 以便将其写入磁盘
```

```objc
// 如果没有数组
// 将我们的 todoItems 数组打包成 NSData 对象
NSData *data = [NSPropertyListSerialization dataWithPropertyList:todoItems
format:NSPropertyListFormatXMLv1
options:NSPropertyListMutableContainers
error:&outError];
```

```objc
// 返回我们新打包的 NSData 对象
return data;
```

```objc
- (BOOL)readFromData:(NSData *)data
type:(NSString *)typeName
error:(NSError **)outError
```

```objc
// 该方法在加载文档时被调用
// 我们收到一个 NSData 对象，并预计从从中提取我们的数据
// 提取我们的 todoItems
todoItems = [NSPropertyListSerialization propertyListWithData:data
options:0
format:NULL
error:outError];
// 根据上述调用的成功与否返回成功结果
return (todoItems != nil);
```

注意，这是你第一次实现一个接收 `NSError**` 指针参数的方法。在这种情况下，我们仅仅返回了由 `propertyListWithData:options:format:error:` 生成的 `NSError`，但根据失败的性质，你也可以创建并返回一个新的 `NSError`。

再次编译并运行应用程序。现在你可以保存和加载任务列表了。

## 挑战

- 添加一个*删除选中项目*（Delete Selected Item）按钮。

- 在开发者文档中查找 `NSError` 类引用，并按照章节末提到的，在保存和加载失败时创建新的 `NSError` 实例并返回。

# 第五部分

## 高级 Objective-C

你现在已经掌握了足够的 Objective-C 来开始 iOS 或 Cocoa 编程。但先不要急于离开。接下来的章节将平要讨论对你作为 Objective-C 程序员的第一年里非常有用的技术和概念。

在 `NSObject` 类中，有一个名为 `init` 的方法。在对象被分配后，你向新实例发送 `init` 消息，以便将其实例变量初始化为可用的值。因此，`alloc` 为对象创建空间，而 `init` 让对象准备好工作。使用 `init` 的写法如下所示：

```objc
NSMutableArray *things = [[NSMutableArray alloc] init];
```



注意，`init` 是一个返回初始化对象地址的实例方法。它是 `NSObject` 的初始化器。本章将介绍如何编写初始化器。

## 编写 init 方法

创建一个新项目：一个名为 Appliances 的 Foundation 命令行工具。在这个程序中，你将创建两个类：`Appliance` 和 `OwnedAppliance`（`Appliance` 的子类）。`Appliance` 的实例将有一个 `productName` 和一个 `voltage`。`OwnedAppliance` 的实例还将包含一个包含所有者名称的集合。

图 29.1 Appliance 及其子类 OwnedAppliance

| Appliance |
| :--- |
| int voltage |
| NSString *productName |
| -init |
| -initWithProductName: |

继承自

| OwnedAppliance |
| :--- |
| NSMutableSet *ownerNames |
| -initWithProductName: |
| -initWithProductName:firstOwnerName: |

创建一个新文件：一个名为 `Appliance` 的 `NSObject` 子类。在 `Appliance.h` 中，为 `productName` 和 `voltage` 创建实例变量和属性声明：

```objc
#import <Foundation/Foundation.h>

@interface Appliance : NSObject {

    NSString *productName;

    int voltage;

}
```

```objc
@property (copy) NSString *productName;

@property int voltage;

@end
```

（我们将在第 30 章讨论 `copy` 属性属性。）

在 `Appliance.m` 中，合成属性以为实例变量创建访问器方法：

```objc
#import "Appliance.h"

@implementation Appliance

@synthesize productName, voltage;

...
```

你可以像这样创建一个 `Appliance` 实例：

```objc
Appliance *a = [[Appliance alloc] init];
```

注意，由于 `Appliance` 没有实现 `init` 方法，它将执行在 `NSObject` 中定义的 `init` 方法。当这种情况发生时，所有特定 `Appliance` 的实例变量都被清零。因此，`Appliance` 新实例的 `productName` 将为 `nil`，`voltage` 将为 `0`。

## 一个基础的 init 方法

在某些情况下，实例变量的初始值为零可能运行得良好。但在其他情况下，你需要你的类实例在进入世界时，其实例变量已初始化为非零值。

假设 `Appliance` 的每个实例都应该从 `voltage` 为 120 开始。在 `Appliance.m` 中，通过重写 `init` 方法来实现：

```objc
- (id)init
{
    // 调用父类的 init
    self = [super init];

    // 给 voltage 赋值
    voltage = 120;

    // 返回 self
    return self;
}
```

（注：此处原文似乎存在内容重复或逻辑混乱，根据指令中“不要重复输出原文”的原则，翻译已基于逻辑进行了平滑处理。以下是衔接的剩余内容翻译：）

注意，这是你第一次实现一个接收 `NSError**` 指针参数的方法。在这种情况下，我们仅仅返回了由 `propertyListWithData:options:format::` 生成的 `NSError`，但根据失败的性质，你也可以创建并返回一个新的 `NSError`。

再次编译并运行应用程序。现在你可以保存和加载任务列表。

# 带有参数的初始化方法

有时候，如果没有从调用的方法获取某些信息，对象就无法正确初始化。例如，想象一个家用电器如果没有名称就无法工作（`nil` 不在此列）。在这种情况下，你需要能够将初始化器传递给 `name` 使用。

你无法通过 `init` 实现这一点，因为在现在和将来，`init` 都不带参数。因此，你必须创建一个新的初始化方法。然后，当另一个方法创建 `Appliance` 实例时，它看起来像这样：

```objc
Appliance *as = [[Appliance alloc] initWithProductName:@"Toaster"];
```

`Appliance` 的新初始化方法是 `initWithProductName:`，它接受一个 `NSString` 作为参数。在 `Appliance.h` 中声明这个新方法：

```objc
#import <Foundation/Foundation.h>

@interface Appliance : NSObject {

    NSString *productName;

    int voltage;

}

@property (copy) NSString *productName;

@property int voltage;

- (id)initWithProductName:(NSString *)pn;

@end
```

在 `Appliance.m` 中，找到 `init` 的实现。将方法名更改为 `initWithProductName:` 并使用传入的值设置 `productName`。

```objc
- (id)initWithProductName:(NSString *)pn
{
    // 调用 NSObject 的 init 方法
    self = [super init];

    // 它是否返回了非 nil 对象？
    if (self) {
        // 设置产品名称
        [self setProductName:pn];

        // 给电压赋一个初始值
        [self setVoltage:120];
    }

    return self;
}
```

在继续之前，构建项目以确保语法无误。

现在你可以用给定的名称创建一个 `Appliance` 实例了。然而，如果你将 `Appliance.h` 和 `Appliance.m` 交给另一个程序员，她可能没有意识到她需要调用 `initWithProductName:`。如果她用最常见的方式创建 `Appliance` 实例怎么办？

```objc
Appliance *a = [[Appliance alloc] init];
```

这并不是不合理的行为。作为 `NSObject` 的子类，预期 `Appliance` 实例可以执行 `NSObject` 实例可以做的任何事情。而且 `NSObject` 实例会响应 `init` 消息。然而，这产生了一个问题，因为上述代码行创建的 `Appliance` 实例其产品名称为 `nil`，电压为 `0`。而我们之前已经决定每个 `Appliance` 实例都需要 `120` 的电压和一个真实的名称才能正常工作。你如何防止这种情况的发生呢？

解决方案很简单。在 `Appliance.m` 中，添加一个 `init` 方法来使用默认名称值调用 `initWithProductName:`：

```objc
- (id)init
{
    return [self initWithProductName:@"Unknown"];
}
```

注意，这个新重写的 `init` 并没有做什么——它调用了 `initWithProductName:` 方法，由该方法执行繁重工作。

为了测试你的初始化器，你需要一个 `description` 方法。在 `Appliance.m` 中实现 `description`：

```objc
- (NSString *)description
{
    return [NSString stringWithFormat:@"%@ %d volts", productName, voltage];
}
```

现在，在 `main.m` 中执行以下类：

```objc
#import <Foundation/Foundation.h>
#import "Appliance.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        Appliance *a = [[Appliance alloc] init];
        NSLog(@"a is %@", a);

        [a setProductName:@"Washing Machine"];
        [a setVoltage:240];

        NSLog(@"a is %@", a);
    }
    return 0;
}
```

## 构建并运行程序。

让我们进一步对初始化器进行探索。创建一个新文件：一个名为 `OwnedAppliance` 的 `Appliance` 子类。

## 29.2 创建 Appliance 的子类

![](img/a694739dec801cd745c57da9e19c2cd4_301_0.png)

在 `OwnedAppliance.h` 中，添加一个可变的所有者名称集合和三个方法。

```objc
#import "Appliance.h"

@interface OwnedAppliance : Appliance {

    NSMutableSet *ownerNames;

}

- (id)initWithProductName:(NSString *)pn firstOwnerName:(NSString *)n;
- (void)addOwnerNamesObject:(NSString *)n;
- (void)removeOwnerNamesObject:(NSString *)n;

@end
```

注意，你声明的方法之一是一个带有两个参数的初始化器。

在 `OwnedAppliance.m` 中实现这些方法：

```objc
#import "OwnedAppliance.h"

@implementation OwnedAppliance

- (id)initWithProductName:(NSString *)pn firstOwnerName:(NSString *)n
{
    // 调用父类的初始化器
    self = [super initWithProductName:pn];

    if (self) {
        // 创建一个集合来存放所有者名称
        ownerNames = [[NSMutableSet alloc] init];

        // 第一个所有者名称非 nil 吗？
        if (n) {
            [ownerNames addObject:n];
        }

        // 返回新对象的指针
        return self;
    }
    return nil;
}

- (void)addOwnerNamesObject:(NSString *)n
{
    [ownerNames addObject:n];
}

- (void)removeOwnerNamesObject:(NSString *)n
{
    [ownerNames removeObject:n];
}

@end
```

注意 `initWithProductName:` 方法并没有初始化 `voltage` 或 `productName`。`Appliance` 中的 `initWithProductName:` 负责这些。当你创建一个子类时，通常只需要初始化 `OwnedAppliance` 引入的变量；让父类负责它引入的变量。

修复方法与之前一样。在 `OwnedAppliance.m` 中，为 `initWithProductName:` 添加一个实现，使用默认值调用 `firstOwnerName:`：

```objc
- (id)initWithProductName:(NSString *)pn
{
    return [self initWithProductName:pn firstOwnerName:nil];
}
```

测测验时间：你需要在 `OwnedAppliance` 中实现 `init` 吗？此时以下代码可以正常工作：
`OwnedAppliance *a = [[OwnedAppliance alloc] init];`

为什么？因为 `OwnedAppliance` 中没有 `init` 的实现，这将触发 `Appliance` 中的 `init` 方法，它调用了 `[self initWithProductName:@"Unknown"];` `self` 是 `OwnedAppliance` 的实例，所以它调用了 `OwnedAppliance` 中的 `initWithProductName:`，该方法调用了 `[self initWithProductName:pn firstOwnerName:nil]`

你为什么想要一个调用其他方法的初始化器链？

## 图 29.3 初始化链

![](img/a694739dec801cd745c57da9e19c2cd4_303_0.png)

注意图 29.3 显示了每个类一个初始化器。该初始化器是该类的初始化器。`init` 是 `NSObject` 的初始化器，`initWithProductName:` 是 `Appliance` 的初始化器，而 `initWithProductName:firstOwnerName:` 是 `OwnedAppliance` 的初始化器。一个类只有一个初始化器方法。

当你创建一个初始化器名称与其父类初始化器名称不同的类时（如你在 `Appliance` 和 `OwnedAppliance` 中所做的那样），你有责任在头文件中进行说明。在 `Appliance.h` 中添加适当注释：

```objc
#import <Foundation/Foundation.h>

@interface Appliance : NSObject

    NSString *productName;

    int voltage;

@property (copy) NSString *productName;

@property int voltage;

// 指定初始化器
- (id)initWithProductName:(NSString *)pn;

@end
```

并在 `OwnedAppliance.h` 中：

```objc
#import "Appliance.h"

@interface OwnedAppliance : Appliance {

    NSMutableSet *ownerNames;

}

// 指定初始化器
- (id)initWithProductName:(NSString *)pn firstOwnerName:(NSString *)n;
- (void)addOwnerNamesObject:(NSString *)n;
- (void)removeOwnerNamesObject:(NSString *)n;

@end
```

因此，我们得到了所有时尚的 Objective-C 程序员在编写初始化器时遵循的规则：

- 如果一个类有多个初始化器，应该只有一个应该执行实际工作。该方法被称为指定初始化器。所有其他初始化器都应该直接或间接地调用该指定初始化器。
- 指定初始化器会在初始化其实例变量之前调用父类的指定初始化器。
- 如果你的类的指定初始化方法（designated initializer）与其父类的指定初始化方法名称不同，你必须重写父类的指定初始化方法，以便其调用新的指定初始化方法。
- 如果你有多个初始化方法，请在头文件中明确说明哪一个是指定初始化方法。

## 致命的初始化方法 (Deadly init methods)

然而，有时你无法安全地重写父类的指定初始化方法。假设你正在创建一个名为 `WallSafe` 的 `NSObject` 子类，它的指定初始化方法是 `initWithSecretCode:`。但是，对于你的应用程序来说，为代码一个默认值并不安全。这意味着我们一直使用的模式——通过重写 `init` 来调用带有默认值的新类指定初始化方法——是不可接受的。

那么你该怎么办？`WallSafe` 的实例仍然响应 `init` 消息。有人可以轻松这样做：

```objc
WallSafe *ws = [[WallSafe alloc] init];
```

最好的做法是重写父类的指定初始化方法，让开发者知道他们犯了错误，并告诉他们如何修复：

```objc
- (id)init
{
    @throw [NSException exceptionName:@"WallSafeInitialization"
                               reason:@"Use initWithWithSecretCode"];
}
```

## 属性 (Properties)

在上一章中，你创建了一个名为 `Appliance` 的类，它有两个属性：`productName` 和 `voltage`。让我们回顾一下这些属性是如何工作的。

在 `Appliance.h` 中，你声明了两个实例变量来存储数据：

```objc
{
    NSString *productName;
    int voltage;
}
```



你还为它们声明了访问器方法。你可以这样声明访问器：

- `(void)setProductName:(NSString *)s;`
- `(NSString *)productName;`
- `(void)setVoltage:(int)x;`
- `(int)voltage;`

然而，你使用了 `@property` 构造：

```objc
@property (copy) NSString *productName;

@property int voltage;
```

在 `Appliance.m` 中，你可以这样显式地实现访问器方法：

```objc
(void)setProductName:(NSString *)s
{
    productName = [s copy];
}

(NSString *)productName
{
    return productName;
}

(void)setVoltage:(int)x
{
    voltage = x;
}

(int)voltage
{
    return voltage;
}
```

然而，你使用了 `@synthesize` 构造来实现这些它们：

```objc
@synthesize productName, voltage;
```

Objective-C 编译器小知识：在为 iOS 或 64 位 Mac OS X 程序编译程序时，你不需要声明实例变量。`@property`/`@synthesize` 的调用足以为数据留出空间。

打开 `Appliance` 并注释掉 `Appliance.h` 中的实例变量：

```objc
{
  // NSString *productName;
  // int voltage;
}
```

重新生成并运行程序。

在书中，我们总是会声明实例变量。这是一种很好的文档形式，并使你的代码在 32 位 Mac OS X 程序中可用。取消实例变量的注释。

## 属性属性

现在让我们仔细观察一下你可以使用的不同属性，以控制属性访问器的创建方式。

### 可变性

属性可以声明为 `readwrite`（可读写）或 `readonly`（只读）。默认是 `readwrite`，这意味着会同时创建一个 setter（设置）方法和一个 getter（获取）方法。如果你不想创建 setter 方法，可以将属性标记为 `readonly`：

```objc
@property (readonly) int voltage;
```

### 生命周期修饰符

属性还可以被声明为 `unsafe_retained`、`strong`、`weak` 或 `copy`。此选项决定了 setter 如何处理其内存管理。

`unsafe_retained` 是默认且最简单的：它只是将传入的值分配给属性。想象一下这个声明和定义：

```objc
@property (unsafe_retained) int averageScore;
// "property int averageScore" 在这里同样有效
//...
@synthesize averageScore;
```

这产生的 setter 方法几乎等同于：

```objc
(void)setAverageScore:(int)d
{
    averageScore = d;
}
```

在 `Appliance` 中，`voltage` 是一个不安全的保留（unsafe retained）。对于持有非对象的属性，你将始终使用 `unsafe_retained`。

`strong`（正如你在第 20 章中学到的）将确保对传入的对象保持强引用。它还会释放对旧对象的所有权（如果它没有其他所有者，它将自行释放）。对于对象的属性，你通常会使用 `strong`。

`weak` 并不意味着对指向的对象的所有权。它会合成一个 setter，将属性设置为传入的对象。如果该对象被释放，该属性将被设置为 `nil`。（注意，如果指针是 `unsafe_retained` 且它所指向的对象被释放，你将拥有一个“悬空指针”。向悬空指针发送消息通常会导致程序崩溃。）

`copy` 对传入的对象的副本创建一个强引用。但这里有一个细节大多数人都误解了……

### copy

`copy` 选项获取对象的副本，然后将指针指向该副本。想象你有一个这样的属性声明和定义：

```objc
@property (copy) NSString *lastName;

@synthesize lastName;
```

## 键值编码

键值编码是通过属性名称来读取和设置属性的能力。键值编码方法在 `NSObject` 中定义，因此每个对象都具备这种能力。

打开 `main.m` 并找到这一行：

```objc
[a setProductName:@"Washing Machine"];
```

重写该行以使用键值编码：

```objc
[a setValue:@"Washing Machine" forKey:@"productName"];
```

在这种情况下，由 `NSObject` 定义的 `setValue:forKey:` 将去寻找名为 `setProductName:` 的 setter 方法。如果该对象没有 `setProductName:` 方法，它将直接访问实例变量。

你也可以使用键值编码来读取值。在 `main.m` 中添加一行来打印产品名称：

```objc
int main (int argc, const char * argv[]) {
    @autorelease {
        Appliance *a = [[Appliance alloc] init];
        NSLog(@"%p is %@", a);
        [a setValue:@"Washing Machine" forKey:@"productName"];
        [a setVoltage:240];
        NSLog(@"%p is %@", a);
        NSLog(@"the product name is %@", [a valueForKey:@"productName"]);
        return 0;
    }
}
```

在这种情况下，由 `NSObject` 定义的 `valueForKey:` 将去寻找名为 `productName` 的访问器方法。如果没有 `productName` 方法，则直接访问实例变量。

如果你输错了属性名称，编译器不会向你报告错误，但这将是一个运行时错误。在 `main.m` 中犯下这个错误：

```objc
NSLog(@"the product name is %@", [a valueForKey:@"productNamme"]);
```

当你编译并运行它时，你会看到一个错误：

```
*** Terminating app due to uncaught exception 'NSUnknownKeyException',
reason: '<Appliance 0x10108dd0> valueForUndefinedKey:]:this class is not value coding-compliant for the key productNammme.'
```

### 在继续之前修复错误

为什么键值编码很有趣？每当标准框架想要将数据推送到你的对象时，它都会使用 `setValue:forKey:`；每当标准框架想要从你的对象中读取数据时，它都会使用 `valueForKey:`。例如，Core Data 是一个让你轻松将对象保存到 SQLite 数据库并让它们复活的框架。它使用键值编码来操作你自定义的数据模型对象。

为了证明在没有访问权限的情况下键值编码也能操作你的变量，请注释掉 `Appliance.h` 中 `productName` 的 `@property` 声明：

```objc
#import <Foundation/Foundation.h>

@interface Appliance : NSObject
{
    NSString *productName;
    int voltage;
}
//@property (copy) NSString *productName;

@property (nonatomic) int voltage;

// 指定初始化方法
- (id)initWithProductName:(NSString *)pn;
@end
```

同时，从 `Appliance.m` 中移除所有的 `setProductName:` 和 `productName` 方法：

```objc
@synthesize voltage;

- (id)initWithProductName:(NSString *)pn
{
    self = [super init];
    if (self) {
        productName = [pn copy];
        [self setVoltage:120];
    }
    return self;
}

- (id)init
{
    return [self initWithProductName:@"Unknown"];
}

- (NSString *)description
{
    return [NSString stringWithFormat:@"<%@ %d volts", productName, voltage];
}
@end
```

编译并运行程序。注意，尽管你没有 `productName` 的访问器方法，仍然可以从其他方法设置和读取变量。这显然违反了对象封装的理念：对象的方法应该是公开的，而实例变量是脆弱的，应该保持私有。如果键值编码不是惊人的好用，没有人会容忍它。

### 非对象类型

键值编码方法设计用于与对象一起工作，但某些属性持有非对象类型，如 `int` 或 `float`。例如，`voltage`（电压）是一个 `int`。你该如何使用键值编码设置电压？你使用 `NSNumber`。

在 `main.m` 中，将设置电压的行从这里：

```objc
[a setVoltage:240];
```

改为：

```objc
[a setValue:[NSNumber numberWithInt:240] forKey:@"voltage"];
```

在 `Appliance.m` 中添加一个显式的访问器，这样你就可以看到它被调用了：

```objc
(void)setVoltage:(int)x
{
    NSLog(@"setting voltage to %d", x);
    voltage = x;
}
```

编译并运行程序。

同样，如果你请求 `forKey:@"voltage"`，你将得到一个包含 `voltage` 值的 `NSNumber`。

## 分类

分类允许程序员为任何现有类添加方法。例如，Apple 给了我们 `NSString` 类。我们没有得到该类的源代码，但分类赋予了我们为 `NSString` 添加新方法的能力。

创建一个名为 `VowelCounter` 的新 Foundation 命令行工具。然后创建一个新的 Objective-C 分类文件。将分类命名为 `VowelCounting`，并使其成为 `NSString` 的一个分类。

现在打开 `NSString+VowelCounting.h` 并声明你想要添加到 `NSString` 类的方法：

```objc
#import <Foundation/Foundation.h>

@interface NSString (VowelCounting)
-(int)vowelCount;
@end
```

现在在 `NSString+VowelCounting.m` 中实现该方法：

```objc
#import "NSString+VowelCounting.h"

@implementation NSString (VowelCounting)

-(int)vowelCount {
    NSCharacterSet *charSet = [NSCharacterSet characterSetWithCharactersInString:@"aeiouAEIOU"];
    NSInteger count = 0;
    for (int i = 0; i < [self length]; i++) {
        unichar c = [self characterAtIndex:i];
        if ([charSet characterIsMember:c]) {
            count++;
        }
    }
    return (int)count;
}

@end
```

现在在 `main.m` 中使用新方法：

```objc
#import <Foundation/Foundation.h>
#import "NSString+VowelCounting.h"

int main (int argc, const char * argv[]) {
    @autorelease {
        NSString *string = @"Hello, World!";
        NSLog(@"%@ has %ld vowels", string, [string vowelCount]);
    }
    return 0;
}
```

## Blocks

在第 24 章中，你学习了代理模式和通知。回调允许其他对象响应事件调用方法。虽然这些方法功能完备，但它们会打乱你的代码。

例如，在第 24 章的回调示例中，你添加了代码以便在时区变化时注册对象通知，并在接收后设置 `zoneChange`。但现在我在读你的代码，好奇 `zoneChange` 在触发时会做什么，所以我去找它的实现。在回调中，注册对象的代码和实现紧挨在一起。

Mac OS 10.6 和 iOS 4 引入了一种新特性，称为 Block。Objective-C Block 就像一段 C 函数代码，但它可以像数据一样被传递。我们很快就会展示如何将相关代码放在一起。

Block 及其语法绝对是高级 Objective-C 主题，起初可能会让人困惑。然而，Apple 的 API 正在越来越多地使用。在本章中，我们将通过几个简单的示例，让你在遇到 Block 时做好准备。

### 定义 Block

这是一个 Block：

```objc
^{
    NSLog(@"I'm a log statement within a block!");
}
```

这些 Block 有名字吗？还没有。这些 Block 是值，就像数字 5 是一个值一样。为了通过名称访问 Block，我们必须将其赋值给 Block 变量。

### 使用块

为了看到它是如何运作的，我们将直接深入代码。在这次练习中，你将使用一个块来移除数组每个字符串中的所有元音。

创建一个新的 Foundation 命令行工具，并将其命名为 `VowelMovement`。在这个程序中，你将使用一个块来遍历字符串数组，并对每个字符串进行转换。首先，你将创建三个数组：一个用于存储原始字符串，一个用于存储“去元音”后的字符串，第三个用于存储要从字符串中删除的字符。在 `main.m` 中，替换 `@autorelease` 大括号内的代码：

```objc
int main (int argc, const char * argv[]) {
    @autorelease {
        // 创建要去元音的字符串数组和存放新字符串的容器
        NSArray *oldStrings = [NSArray arrayWithObjects:
            @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"old strings: %@", oldStrings);
        NSMutableArray *newStrings = [NSMutableArray array];

        // 创建我们要从字符串中删除的字符列表
        NSArray *vowels = [NSArray arrayWithObjects:
            @"a", @"e", @"i", @"o", @"u", nil];
    }
    return 0;
}
```

这里现在什么都没有；你只是在设置数组。编译并运行你的程序。你现在可以忽略关于未使用变量的警告。

### 声明块变量

现在编写块的代码。虽然块看起来像函数，但它们可以存储在变量中。和其他变量一样，块变量需要先声明后赋值。将以下代码添加到 `main.m` 中以声明你的块变量。

```objc
int main (int argc, const char * argv[]) {
    @autorelease {
        // 创建要去元音的字符串数组和存放新字符串的容器
        NSArray *oldStrings = [NSArray arrayWithObjects:
            @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"old strings: %@", oldStrings);
        NSMutableArray *newStrings = [NSMutableArray array];

        // 创建我们要从字符串中删除的字符列表
        NSArray *vowels = [NSArray arrayWithObjects:
            @"a", @"e", @"i", @"o", @"u", nil];

        // 声明块变量
        void (*devowelizer)(id, NSInteger, BOOL *);
    }
    return 0;
}
```



# 图 32.1 块变量声明

![](img/a694739dec801cd745c57da9e19c2cd4_321_0.png)

在声明原始类型变量时，你给出它的类型和名称（例如 `i`）。但是对于块变量，名称位于声明的中间，紧跟在脱符号（`^`）之后。块变量的类型取决于块是如何构造的。在这种情况下，`devowelizer` 的类型是“一个接受一个对象、一个整数和一个 `BOOL` 指针且不返回任何内容的块”。

# 为我们的新变量赋值

让我们给我们的新变量赋值。对于块变量，其值始终是大括号内部的一组指令。在 `main.m` 中，添加以下赋值语句：

```objc
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSMutableArray *newStrings = [NSMutableArray array];

        // 创建我们要从字符串中删除的字符列表
        NSArray *vowels = [NSArray arrayWithObjects:
                          @"a", @"e", @"i", @"o", @"u", nil
        ];

        // 声明块变量
        void (*devowelizer)(id, NSInteger, BOOL *);

        // 赋值给变量
        devowelizer = ^(id string, NSInteger i, BOOL *stop) {
            NSMutableString *newString = [NSMutableString stringWithString:string];

            // 遍历元音数组，将每个字符的出现处替换为空字符串。
            for (NSString *s in vowels) {
                NSRange fullRange = NSMakeRange(0, [newString length]);
                [newString replaceOccurrencesOfString:s
                                           options:NSCaseInsensitiveSearch
                                           range:fullRange
                                             withString:@""];
            }

            [newStrings addObject:newString];
        };
        // 块赋值结束
    }
    return 0;
}
```

再次编译你的程序以检查输入。关于未使用变量的警告应该会消失。

现在你组合了一个块——一组指令——并将该块赋值给了块变量 `devowelizer`。注意，块赋值以分号结尾，就像任何变量赋值一样。

和任何变量一样，你可以同时完成 `devowelizer` 的声明和赋值：

```objc
void (*devowelizer)(id, NSInteger, BOOL *) = ^(id string, NSInteger i, BOOL *stop) {
    NSMutableString *newString = [NSMutableString stringWithString:string];

    // 遍历元音数组，将每个字符的出现处替换为空字符串。
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                   options:NSCaseInsensitiveSearch
                                   range:fullRange
                                 withString:@""];
    }

    [newStrings addObject:newString];
};
```

和之前一样，我们声明了一个接受三个参数且不返回内容的块变量，命名为 `devowelizer`。我们组合了一个实际的块并将其存储在 `devowelizer` 中。

## 传递块

由于 `devowelizer` 是一个变量，你可以将其作为参数传递。`NSArray` 有一个方法称为 `enumerateObjectsUsingBlock:`。该方法期望块作为其唯一参数。它会为数组中的每个对象执行一次块。

在 `main.m` 中，添加以下代码来调用 `enumerateObjectsUsingBlock:` 并传入 `devowelizer`，打印去元音后的字符串。

```objc
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // 创建要去元音的字符串数组和存放新字符串的容器
        NSArray *oldStrings = [NSArray arrayWithObjects:
                               @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"old strings: %@", oldStrings);

        NSMutableArray *newStrings = [NSMutableArray array];

        // 创建我们要从字符串中删除的字符列表
        NSArray *vowels = [NSArray arrayWithObjects:
                           @"a", @"e", @"i", @"o", @"u", nil];

        // 声明块变量
        void (*devowelizer)(id, NSInteger, BOOL *);

        // 赋值给变量
        devowelizer = ^(id string, NSInteger i, BOOL *stop) {
            NSMutableString *newString = [NSMutableString stringWithString:string];

            // 遍历元音数组，将每个字符的出现处替换为空字符串。
            for (NSString *s in vowels) {
                NSRange fullRange = NSMakeRange(0, [newString length]);
                [newString replaceOccurrencesOfString:s
                                           options:NSCaseInsensitiveSearch
                                           range:fullRange
                                         withString:@""];
            }

            [newStrings addObject:newString];
        };
        // 块赋值结束

        // 使用我们的块遍历数组
        [oldStrings enumerateObjectsUsingBlock:devowelizer];

        NSLog(@"new strings: %@", newStrings);
    }
    return 0;
}
```

编译并运行你的程序。你会在控制台上看到两个数组。第二个数组应该与第一个匹配——只是没有了讨厌的元音。

```text
2011-09-03 10:27:02.617 VowelMovement[787:707] old strings: (
    Sauerkraut,
    Raygun,
    "Big Nerd Ranch",
    Mississippi
)
2011-09-03 10:27:02.618 VowelMovement[787:707] new strings: (
    Srkrt,
    Rygn,
    "Bg Nrd Rnch",
    Msssspp
)
```

值得注意的是，`enumerateObjectsUsingBlock:` 不接受任意块作为参数。该方法要求“一个接受一个对象、一个整数和一个 `BOOL` 指针且不返回任何内容的块”。这就是我们这样构造赋值给 `devowelizer` 的块的原因。

第一个参数是当前对象的指针。注意该指针的类型是 `id`，无论数组包含什么种对象它都有效。第二个参数是当前对象的索引 `NSInteger`。第三个参数是指向 `BOOL` 的指针，默认为 `NO`。如果我们希望数组在当前迭代后停止，可以将其更改为 `YES`。

在块赋值的开头添加一个检查：

```objc
devowelizer = ^(id string, NSInteger i, BOOL *stop) {
    // 我找到了 y 吗？
    NSRange yRange = [string rangeOfString:@"y" options:NSCaseInsensitiveSearch];
    if (yRange.location != NSNotFound) {
        *stop = YES; // 防止进一步迭代
        return; // 停止本次迭代
    }

    NSMutableString *newString = [NSMutableString stringWithString:string];

    // 遍历元音数组，将每个元音出现替换为空字符串。
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                   options:NSCaseInsensitiveSearch
                                   range:fullRange
                                 withString:@""];
    }

    [newStrings addObject:newString];
    // 块赋值结束
};
```

这将检查用于当前迭代的字符串是否包含大写或小写字符 'y'。如果是，则指针被设置为 `YES`（这将阻止块执行任何迭代），然后停止当前迭代。编译并运行程序。再次，数组被记录到调试器输出中，但这次在第二次迭代期间，当块遇到一个包含 'y' 的单词时，枚举被取消了。你得到的只有一些位。既然你已经练习了一些块，让我们回到块是如何解决回调问题的。当你使用回调函数时，例如在第 24 章中，你有这样一行代码：标识一个方法（通常使用 `@selector()`），然后在文件的其他地方实现该方法。你可以使用 `NSNotificationCenter` 方法 `addObserverForName:object:queue:usingBlock:` 并传递一个块。通过这种方法，你可以直接在那里处理回调，因此你不需要将回调代码放在该处的其他地方。任何阅读你代码的人都将在同一段代码中看到发送给 `NSNotificationCenter` 的消息，以便在章节末尾准确获得这一变化。

## typedef

块的语法可能会让人困惑，但你可以使用在第 1 章中学到的 `typedef` 关键字让它变得更友好。记住，`typedef` 应该位于文件顶部或头文件中，位于任何方法实现之外。在 `main.m` 中，添加以下内容：

```objc
#import <Foundation/Foundation.h>

typedef void (^EnumerationBlock)(id, NSInteger, BOOL *);

int main(int argc, const char *argv[]) {
    // ...
}
```

注意，这看起来与块的声明完全相同。然而，在这里我们定义的是一个类型而不是变量。这允许我们简化相似块的声明。与其像这样声明它，你可以用以下声明替换掉那行：

```objc
EnumerationBlock devowelizer;
```

这使得你的块变量声明看起来更加熟悉。请注意，块类型本身只定义了块的参数和返回值；它对该类型块内部的指令没有影响。

## 返回值

最后，当块返回一个值时，你可以像调用函数一样调用它的块变量。

```objc
double (^divBlock)(double, double) = ^double(double k, double j) {
    return k / j;
};
```

在这段代码中，你将 `divBlock` 声明为一个返回 `double` 并期望两个 `double` 作为参数的块变量。然后你给它赋值了一个值，该值包含了返回两个参数除法结果的指令。你可以这样使用这个块：

```objc
double quotient = divBlock(42.0, 12.5);
```



# 内存管理

像原始变量一样，块是在创建并存储在栈上的。也就是说，当创建块的函数或方法返回时，块将随栈帧一起被销毁。然而，有时你的块需要比那存得久。例如，它可以变成对象的实例变量。在这种情况下，你必须将块从栈拷贝到堆上。

要从栈上拷贝块，你向它发送 `copy` 消息：`EnumerationBlock iVarEnumerationBlock = [enumerationBlock copy];`

现在，你的块的副本存在于堆上。它现在是堆上的块，而不是栈上的块，而新的块变量是指向该块的指针。接收块作为参数的方法，如 `NSArray enumerateObjectsUsingBlock:` 或 `NSNotificationCenter addObserverName:object:queue:usingBlock:`，会被拷贝传递给它们的块。

# 基于块的未来

块可能很难理解和使用。然而，它们在事件驱动的应用程序中非常有用且强大。Apple 的 API 越来越多地使用块。例如，AssetLibrary 和 GameKit 框架使用了许多块的方法。在使用 Apple 的块方法是一个好习惯，以便更习惯块。

# 挑战

## 匿名块

本章中的示例将块的声明、赋值和使用放在三行代码中以提高可读性。当你需要向方法传递一个整数时，例如 NSNumber 的 `numberWithInt:`，你可以匿名地传递该整数：

```objc
// 选项 1：完全拆解

int i;

i=5;

NSNumber *num = [NSNumber numberWithInt:i];

// 选项 2：跳过变量声明

NSNumber *num = [NSNumber numberWithInt:5];
```

因为块是变量，你也可以对块这样做。事实上，这是使用块最常见的方式。你很少声明块变量以便将块传递到方法；你通常会匿名使用它们。

修改本章的练习，将块匿名作为参数传递给 `enumerateObjectsUsingBlock:`。也就是说，保留块，但去掉块变量。

## NSNotificationCenter

在第 24 章中，你使用了 NSNotificationCenter 的 `addObserver:selector:name:method:` 来注册通过你的 `zoneChange:method` 接收回调。更新该练习以使用 `addObserverName:object:queue:usingBlock:` 方法。在开发者文档中查看其详细信息。该方法接收一个块作为参数，并在指定的通知发送时执行该块，而不是回调到你的对象。

已发布。这意味着你的 `zoneChange:` 方法将永远不会被调用。该方法内部的代码将改为位于块（block）中。

传入的块应该接收一个参数（一个 `NSNotification *`）并且不返回任何内容，就像 `zoneChange:` 方法一样。

你可以将 `nil` 作为 `queue::` 的参数：此参数用于并发，这是一个我们在本书书中不会涉及的话题。

# 第六部分：高级 C

要成为一名胜任的 Objective-C 程序员，你必须也是一名胜任的 C 程序员。关于 C，你还有几点是真正需要的。这些主题并不是你每天都会用到的概念，但你偶尔会遇到，因此我想在这里向你介绍它们。

## 位运算

在本书的第一部分，我将计算机的内存描述为一片广阔的开关草地（数十亿个开关），这些开关可以打开或关闭。每个开关代表一个位（bit），我们通常用 1 表示“开启”，用 0 表示“关闭”。

然而，你从不会对单个位进行寻址。相反，你处理的是字节（byte）大小的位块。如果你将一个字节看作一个无符号 8 位整数，那么每个位就代表另一个 2 的幂：

**图 33.1 一个字节表示十进制数字 60**

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|---|---|---|---|---|---|---|---|
| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 |

$32 + 16 + 8 + 4 = 60$

作为拥有十个手指的副作用，人们喜欢使用十进制（基数 10）。然而，计算机喜欢 2 的幂。程序员经常使用基数为 16 的系统（$16 = 2^4$），被称为十六进制或简称为“hex”。当我们处理整数的单个位时，情况尤为如此。

我们使用字母 a, b, c, d, e, f 作为额外的数字。十六进制的计数如下：0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, b, c, d, e, f, 10, 11, ...

为了在编写十六进制时清晰，我们在数字前加上前缀 0x。以下是使用十六进制表示的相同数字和字节：

**图 33.2 一个字节表示十六进制数 0x3c**

| 0x80 | 0x40 | 0x20 | 0x10 | 0x8 | 0x4 | 0x2 | 0x1 |
|---|---|---|---|---|---|---|---|
| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 |

0x20 + 0x10 + 0x8 + 0x4 = 0x3c

注意，一个字节始终可以描述为两个位的十六进制数（如 3c）。这使得十六进制成为查看二进制数据的合理方式。一个硬核程序员会说的话是：“我通过十六进制编码字节反向工程了文件格式？”想以十六进制编码字节列表的形式查看文件吗？在 Terminal 中，对文件执行 `hexdump`：

```bash
$ hexdump myfile.txt

0000000 3c 3f 78 6d 6d 20 76 72 73 69 6f 3d 22 31

0000020 2e 3d 30 22 3f 3e 74 70 7a 3c 62 62 6f 6b 78 68

0000040 73 3d 22 68 74 74 7a 3a 2f 64 63 63 62 62 6f

0000060 6b 2e 6f 72 67 2f 6e 73 2f 64 65 63 6f 64 65

0000080 22
```

第一列是第二列列出的字节相对于文件开的偏移量（十六进制）。每两个数字代表一个字节。

## 位或运算 (Bitwise-OR)

如果你有两个字节，可以将它们进行位或运算以创建第三个字节。如果前两个字节对应的位中至少有一个为 1，那么第三个字节上的该位将为 1。

**图 33.3 两个字节进行位或运算**

| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | = 0x3c |
|---|---|---|---|---|---|---|---|---|
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | = 0xa9 |
| 1 | 0 | 1 | 1 | 1 | 1 | 0 | 1 | = 0xbd |

这是通过 `|` 运算符完成的。要尝试操作位，创建一个新项目：名为 `bitwise` 的 C Line Tool（不是 Foundation）。

编辑 `main.c`：

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {

    unsigned char a = 0x3c;

    unsigned char b = 0xa9;

    unsigned char c = a | b;

    printf("Hex: %x | %x = %x\n", a, b, c);

    printf("Decimal: %d | %d = %d\n", a, b, c);

    return 0;

}
```



当你运行此程序时，你将看到两个字节进行位或运算：
Hex: 3c | a9 = bd
Decimal: 60 | 169 = 189

这有什么用呢？在 Objective-C 中，我们经常使用一个整数来指定某些设置。整数始终是一个位序列，每个位都用于表示设置的一个可以开启或关闭的方面。我们通过从一组常量中选择来创建这个整数（也称为位掩码 `bit mask`）。这些常量是整数，每个常量通过仅开启其位中的一个来指定设置的单一方面。你可以将这些常量进行位或运算。

（注：由于原文中存在大量重复段落，译文已按逻辑合并处理，确保不冗余且通顺）

第三个字节上的该位将为 1。

### 图 33.3 两个字节进行位或运算

| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | = 0x3c |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | = 0xa9 |
| 1 | 0 | 1 | 1 | 1 | 1 | 0 | 1 | = 0xbd |

这是通过 `|` 运算符完成的。要尝试操作位，创建一个新项目：名为 `bitwise` 的 C Line Tool（不是 Foundation）。

编辑 `main.c`：

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {

    unsigned char a = 0x3c;

    unsigned char b = 0xa9;

    unsigned char c = a | b;

    printf("Hex: %x | %x = %x\n", a, b, c);

    printf("Decimal: %d | %d = %d\n", a, b, c);

    return 0;

}
```

当你运行此程序时，你将看到两个字节进行位或运算：
Hex: 3c | a9 = bd
Decimal: 60 | 169 = 189

## 位与运算 (Bitwise-AND)

如果你有两个字节，可以将它们进行位与运算以创建第三个字节。如果前两个字节对应的位都为 1，那么第三个字节上的该位将为 1。

### 图 33.4 两个字节进行位与运算

| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | 0x3c |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | 0xa9 |
| 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0x28 |

这是通过 `&` 运算符完成的。将以下内容添加到 `main.c`：

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {

    unsigned char a = 0x3c;

    unsigned char b = 0xa9;

    unsigned char c = a & b;

    printf("Hex: %x & %x = %x\n", a, b, c);

    printf("Decimal: %d & %d = %d\n", a, b, c);

    return 0;

}
```

当你运行此程序时，你将看到两个字节进行位与运算：
Hex: 3c & a9 = 28
Decimal: 60 & 169 = 40

（注：原文中存在大量重复文本，译文已去重处理）

## 其他位运算符

为了完整起见，这里是其他位运算符。这些在 Objective-C 中不常用，但最好了解。

### 异或运算 (Exclusive OR)

你可以将两个字节进行异或运算（XOR）以创建第三个字节。如果输入字节对应的位中恰好有一个为 1，那么第三个字节上的该位将为 1。

### 图 33.5 两个字节进行位异或运算

| 0 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | 0x3c |
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | 0xa9 |
| 1 | 0 | 0 | 1 | 0 | 1 | 0 | 1 | 0x95 |

这是通过 `^` 运算符完成的。将以下添加到 `main.c`：

```c
unsigned char e = a ^ b;

printf("Hex: %x ^ %x = %x\n", a, b, e);

printf("Decimal: %d ^ %d = %d\n", a, b, e);

return 0;
```

当你运行它时，将看到：
Hex: 3c ^ a9 = 95
Decimal: 60 ^ 169 = 149

这个运算符有时会让初学者感到困惑。在大多数电子表格程序中，`^` 运算符是幂运算：2^3意味着 2³。在 C 中，我们使用 `pow()` 函数来进行幂运算。

```c
double r = pow(2.0, 3.0); // 计算 2 的三次方
```

### 补码

如果你有一个字节（byte），补码就是与其完全相反的字节：每个 0 变成 1，每个 1 变成 0。

#### 图 33.6 补码

| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | = 0xa9 |
| 0 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | = 0x56 |

这是通过 `~` 运算符实现的。在 `main.c` 中添加几行代码：

```c
unsigned char f = ~b;

printf("Hex: The complement of %x is %x\n", b, f);

printf("Decimal: The complement of %d is %d\n", b, f);

return 0;
```

你应该能看到：

```
Hex: The complement of a9 is 56
Decimal: The complement of 169 is 86
```

### 左移

如果你对位进行左移，你将取每个位并将其向最高位移动。数字左侧的位会被丢弃，而右侧产生的空位将用 0 填充。

#### 图 33.7 左移 2 位

![](img/a694739dec801cd745c57da9e19c2cd4_343_0.png)

左移是通过 `<<` 运算符实现的。在 `main.c` 中添加左移两位的操作：

```c
unsigned char g = a << 2;

printf("Hex: %x shifted left two places is %x\n", a, g);

printf("Decimal: %d shifted left two places is %d\n", a, g);

return 0;
```

当这段代码运行时，你会看到：
Hex: 3c shifted left two places is f0
Decimal: 60 shifted left two places is 240

每当你将一个数字左移一位，它的值就会翻倍。

### 右移

右移运算符应该不会让你感到意外。在 `main.c` 中添加代码：

```c
unsigned char h = a >> 1;

printf("Hex: %x shifted right one place is %x\n", a, h);

printf("Decimal: %d shifted right one place is %d\n", a, h);

return 0;
```

运行时：
Hex: 3c shifted right one place is 1e
Decimal: 60 shifted right one place is 30

#### 图 33.8 右移 1 位

![](img/a694739dec801cd745c57da9e19c2cd4_344_0.png)

每当你将一个数字右移一位，它的值就会减半。（如果是奇数，则向下取整。）

## 使用 enum 定义位掩码

你通常会定义一个常量列表，每个常量代表一个位被置位的整数。然后，可以将这些整数进行按位或（OR）操作，并如上所述使用按位与（AND）进行测试。

实现此点的优雅方法是定义一个使用左移运算符定义值的枚举。以下是 `UIDataDetector` 常量的定义方式：

```c
enum {

    UIDataDetectorTypePhoneNumber = 1 << 0,

    UIDataDetectorTypeLink = 1 << 1,

    UIDataDetectorTypeAddress = 1 << 2,

    UIDataDetectorTypeCalendarEvent = 1 << 3,

    UIDataDetectorTypeNone = 0,

    UIDataDetectorTypeAll = NSIntegerMax

};
```

## 字节

（注：原文后续部分包含大量重复单词和乱码，此处基于常见的 C 语言逻辑进行了清理后翻译）

在很多情况下，你想要定义一个常量列表，每个常量代表一个有一个位被置位的整数。然后，这些整数可以按位或操作组合在一起，并使用按位与进行测试，如上所述。

实现此点的优雅方法是定义一个使用左移运算符来定义值的枚举。以下是 `UIDataDetector` 常量的定义方式：

（由于原文后续文本存在严重重复和错误，此处已停止翻译无意义的字符碎片）

## 字符串字面量

如果你经常处理 C 字符串，使用 `malloc` 分配内存并逐个填充字符将是非常痛苦的。相反，你完全通过将字符串放在引号中来创建一个指向字符字符串（以零字符终止）的指针。修改你的代码以使用字符串字面量：

```c
int main (int argc, const char * argv[]) {

    char x = '!'; // 字符 '\''

    while (x <= '}') { // 字符 '-'

        printf("%% is %c\n", x, x);

        x++;

    }

    char *start = "Love";

    printf("%s has %zu characters\n", start, strlen(start));

    printf("The third letter is %c\n", start[2]);

    return 0;

}
```

编译并运行。

注意，你不需要为字符串字面量 `malloc` 和 `free` 内存。它是一个常量并且在内存中只出现一次，编译器会处理它的内存使用。作为其常量性的副作用，如果你尝试修改字符串中的字符，就会发生糟糕的事情。添加一行应该导致你的程序崩溃的代码：

```c
char *start = "Love";

start[2] = 'z';

printf("%s has %zu characters\n", start, strlen(start));
```

当你编译并运行时，你应该得到一个 `EXC_BAD_ACCESS` 信号。你尝试写入你无权写入的内存。

为了让编译器警告你写入内存的常量部分，你可以使用 `const` 修饰符来指定指针指向数据不可更改的数据。尝试一下：

```c
const char *start = "Love";

start[2] = 'z';

printf("%s has %zu characters\n", start, strlen(start));
```

现在当你编译时，应该会得到来自编译器的错误。

在继续之前，删除有问题的行 (`start[2] = 'z'`)。

你可以在字符串字面量中使用上述提到的转义序列。使用几个：

```c
const char *start = "两个换行符和一个制表符后的反斜杠:\n\n\t\\";

printf("%s has %zu characters\n", start, strlen(start));

printf("The third letter is \'%c\'\n", start[2]);

return 0;
```

编译并运行。

# 在 NSString 之间进行转换

如果你在 Objective-C 程序中使用 C 字符串，你需要知道如何从 C 字符串创建 `NSString`。`NSString` 类有一个方法可以实现：

```c
char *greeting = "Hello";

NSString *x = [NSString stringWithC:greeting encoding:NSUTF8StringEncoding];
```

你也可以从 `NSString` 获取 C 字符串。这要稍微复杂一点，因为 `NSString` 可以处理某些编码无法处理的字符。检查转换是否可行是一个好主意：

```c
NSString *greeting = "Hello";

const char *x = NULL;

if ([greeting canConvertedToEncoding:NSUTF8StringEncoding]) {

    x = [greeting cStringUsingEncoding:NSUTF8StringEncoding];

}
```



你不拥有生成的 C 字符串；系统最终会为你释放它。你可以保证它的生命周期至少与当前的自动释放池（`autorelease pool`）一样，但如果你需要 C 字符串存在很久，你应该将其复制到你用 `malloc()` 创建的缓冲区中。

## 挑战

编写一个名为 `spaceCount()` 的函数，用于统计 C 字符串中的空格字符（ASCII 0x20）。像这样测试它：

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {

    const char *sentence = "Be was not in the cab at the time.";

    printf("%s has %d spaces\n", sentence, spaceCount(sentence));

    return 0;

}
```

记住：当你运行到 `'\0'` 时就到达了字符串的末尾！

## C 数组

在上一节，我们处理了 C 字符串，C 字符串是内存中连续排列的字符列表。数组是内存中连续排列的数据类型列表。就像字符串一样，你通过持有第一个元素的地址来处理列表。假设你想写一个计算 3 个数字平均值的程序。创建一个新的命令行工具项目并编辑 `main.c`：

```c
#include <stdio.h>
#include <stdlib.h> // malloc(), free()

float averageFloats(float *data, int dataCount) {
    float sum = 0.0;
    for (int i = 0; i < dataCount; i++) {
        sum = sum + data[i];
    }
    return sum / dataCount;
}

int main(int argc, const char *argv[]) {
    // 创建一个 float 数组
    float *gradeBook = malloc(3 * sizeof(float));
    gradeBook[0] = 60.2;
    gradeBook[1] = 94.5;
    gradeBook[2] = 81.1;
    // 计算平均值
    float average = averageFloats(gradeBook);
    // 释放数组
    free(gradeBook);
    gradeBook = NULL;
    printf("Average = %.2f\n", average);
    return 0;
}
```

编译并运行。

图 35.1 栈上的指针到 float 缓冲区 ![img/a69473dec801cd745c57da9e19c2cd359_0] `malloc()` 在堆上分配一个缓冲区，所以你完成后需要释放它。如果可以将该缓冲区声明为帧的一部分（在栈上），这样它在函数返回时会自动释放，那不是很好吗？修改 `main`：

```c
#include <stdio.h>

float averageFloats(float *data, int dataCount) {
    float sum = 0.0;
    for (int i = 0; i < dataCount; i++) {
        sum = sum + data[i];
    }
    return sum / dataCount;
}

int main(int argc, const char *argv[]) {
    // 将数组声明为帧的一部分
    float gradeBook[3];
    gradeBook[0] = 60.2;
    gradeBook[1] = 94.5;
    gradeBook[2] = 81.1;
    // 计算平均值
    float average = averageFloats(gradeBook, 3);
    // 不需要释放数组！
    // 清理在函数返回时发生
    printf("Average = %.2f\n", average);
    return 0;
}
```

编译并运行。

字符串字面量让填充数组变得简单。还有数组字面量。使用它来初始化 `gradeBook`：

```c
int main (int argc, const char *argv[]) {
    float gradeBook[] = {60.2, 94.5, 81.1};
    float average = averageFloats(gradeBook, 3);
    printf("Average = %.2f", average);
    return 0;
}
```

编译并运行程序。

注意你不需要指定 `gradeBook` 的长度为 3；编译器从数组字面量中推导出。你可以在许多可以使用 `*` 的地方使用这种类型。例如，将 `averageFloats()` 的声明改为：

```c
float averageFloats(float data[], int dataCount) {
    float sum = 0.0;
    for (int i = 0; i < dataCount; i++) {
        sum = sum + data[i];
    }
    return sum / dataCount;
}
```

编译并运行程序。

```c
#include <stdio.h>

int main (int argc, const char * argv[]) {
    for (int i = 0; i < argc; i++) {
        printf("arg %d %s\n", i, argv[i]);
    }
    return 0;
}
```

如果你在 bash 中运行此程序，可以直接在命令行中输入参数。

然而，要在 Xcode 中运行带参数的程序，必须先编辑方案（Scheme）。在 Product 菜单下，选择 Edit Scheme...。当表格出现时，在左侧的表格视图中选择 Run Affirmation。从表格顶部选择 Arguments 选项卡。然后找到列出的 Arguments On Launch 并使用 `+` 按钮添加两个项目：一个名称和一个数字。

图 36.1 添加参数 ![img/a69473dec801cd745c57da9e19c2cd362_0.png]

点击 OK 关闭表格。

当你运行程序时，将得到 `argv` 中的字符串列表。让大多数人感到惊讶的是 `argv[0]`：

```
arg 0 = /Users/aaron/Library/Developer/Xcode/DerivedData/
Affirmation-enkfqgsavsproegoggxwbrmcmovn/Build/Products/Debug/Affirmation
arg 1 = Aaron
arg 2 = 4
```

`argv[0]` 是可执行文件的路径。

图 36.2 Affirmation 中的 argv 和 argc ![img/a69473dec801cd745c57da9e19c2cd363_0.png]

如果你的程序接收参数，你应该第一要做的是确保参数数量正确。编辑 `main.m`：

```c
#include <stdio.h>
#include <stdlib.h> // 用于 atoi()
```

```c
int main (int argc, const char * argv[]) {
    if (argc != 3) {
        fprintf(stderr, "Usage: Affirmation <name> <number>\n");
        return 1;
    }
    int count = atoi(argv[2]);
    for (int j = 0; j < count; j++) {
        printf("%s is cool.\n", argv[j]);
    }
    return 0;
}
```

`atoi()` 是标准 C 函数，读取 C 字符串并尝试将其转换为整数。

## Switch 语句

检查一个变量是否等于一组特定的值并不罕见。使用 if-else 语句，它看起来是这样：

```c
int yeastType = ...;
if (yeastType == 1) {
    makeBread();
} else if (yeastType == 2) {
    makeBeer();
} else if (yeastType == 3) {
    makeWine();
} else {
    makeFuel();
}
```

为了让这类操作变得更容易，C 提供了 `switch` 语句。上面的代码可以更改为：

```c
int yeastType = ...;
switch (yeastType) {
    case 1:
        makeBread();
        break;
    case 2:
        makeBeer();
        break;
    case 3:
        makeWine();
        break;
    default:
        makeFuel();
        break;
}
```

注意 `break` 语句。如果没有 `break`，在执行完相应的 `case` 子句后，系统将执行所有后续的 `case` 子句。例如，如果我有这样的代码：

```c
int yeastType = 2;
switch (yeastType) {
    case 1:
        makeBread();
    case 2:
        makeBeer();
    case 3:
        makeWine();
    default:
        makeFuel();
}
```

程序将运行 `makeBeer()`、`makeWine()` 和 `makeFuel()`。这主要是为了让你能够多个可能的值触发同一段代码：

```c
int yeastType = ...;
switch (yeastType) {
    case 1:
        makeBread();
        break;
    case 2:
    case 5:
        makeBeer();
        break;
    case 3:
        makeWine();
        break;
    default:
        makeFuel();
        break;
}
```



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
