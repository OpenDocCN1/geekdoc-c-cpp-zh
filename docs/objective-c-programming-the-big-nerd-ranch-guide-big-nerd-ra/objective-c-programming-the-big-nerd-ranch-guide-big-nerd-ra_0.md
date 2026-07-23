# Objective-C 编程：Big Nerd Ranch 指南



![](img/cover.jpeg)










# 致谢

能与如此优秀的人合作是我的极大荣幸。其中几位投入了大量的时间和精力让这本书变得出色。我想借此机会感谢他们。

*   Mikey Ward 编写了本书的几个章节，包括`Your First iOS Application`、`Your First Cocoa Program` 和 `Blocks`。如果我是一个更好的老板，我会把他的名字印在封面上。
*   其他教授 Objective-C 课程的导师为我们提供了源源不断的建议和纠正。他们是 Scott Ritchie, Mark Fenoglio, Brian Hardy, Christian Keur 和 Alex Silverman。
*   我不知疲倦的编辑 Susan Loper 将我那段涵盖了程序员需要的所有知识的意识流独白，炼成了一本通俗易懂的入门教程。
*   几位技术评审员帮助我发现并修复了缺陷。他们是 James Majors, Mark Dalrymple, Scott Steinman, Bart Hoffman, Bolot Kerimbaev 和 Nate Chandler。
*   Ellie Volckhausen 设计了封面。
*   IntelligentEnglish.com 的 Chris Loper 设计并制作了 EPUB 和 Kindle 版本。
*   Pearson Technology Group 优秀团队耐心指导我们完成了书籍出版的业务流程。









#### 获取地址
#### 将地址存储在指针中
#### 获取地址的数据






#### 引用传递函数
#### 避免对 NULL 解引用

## 挑战

### 11. 堆



#### 嵌套消息发送
#### 多参数
#### 向 nil 发送消息

## 挑战


#### 参考页面
#### 快速帮助
#### 其他选项





#### 将 `NSString` 写入文件
#### `NSError`
#### 使用 `NSString` 读取文件
#### 从文件读取 `NSData`

### 24. 回调
## 辅助对象
## 通知
#### 该使用哪一个？
#### 回调与对象所有权



#### 开始 iTahDoodle





- [添加 C 语言辅助函数]
- [模型-视图-控制器 (MVC)]
- [应用程序代理]
- [设置视图]
    - [在 iOS 模拟器上运行]
- [连接表格视图]
    - [保存任务数据]
- [进阶好奇：：关于 `main()` 的问题？]
- [编辑 `BNRDocument.h`]
- [查看 Interface Builder]
- [建立连接]
- [重新审视 MVC]


- [属性特性]

### 32. Blocks
- [使用 blocks]
    - [赋值 block]
    - [传入一个 block]
- [返回值]
- [内存管理]
- [挑战]
    - [匿名 block]
    - [`NSNotificationCenter`]

### 33. 位运算
- [位与 (AND)]
- [其他位运算符]
    - [补码 (Complement)]
    - [左移]
    - [右移]
- [更多字节]
- [挑战]

- [`char`]
- [`char *`]
- [字符串字面量]
- [与 `NSString` 之间的转换]
- [挑战]


## 入门

## 你与这本书


虽然也有类似的书，但这一本是你应该读的。为什么？教人们如何为 iOS 和 Mac 编写应用程序已经多年，我已经确定了你在旅程现阶段需要了解的知识。我一直在努力捕捉这些知识，并摒弃了其他所有无关的内容。





汇编语言极其冗长繁琐且依赖于特定的 CPU（因为你最新的 iMac 的大脑可能与你那台心爱的、用旧了的 PowerBook 的大脑完全大不相同）。换句话说，如果你想在不同类型的计算机上运行程序，你就需要重写汇编代码。

为了编写出可以轻松从一种类型的计算机移动到另一种类型计算机的代码，我们开发了“高级语言”。通过高级语言，你不需要考虑特定的 CPU，而是可以用通用的方式表达指令，然后一个程序（称为编译器）会将该代码转换为高度优化的、特定于 CPU 的机器码。这些语言之一就是 C 语言。C 程序员用 C 语言编写代码，然后 C 编译器将 C 代码转换为机器码。


Objective-C 语言基于 C，但它增加了对面向对象编程的支持。Objective-C 是编写 Apple iOS 和 Mac OS 操作系统应用程序的编程语言。


在书中，你将学习足够的 C 和 Objective-C 编程语言知识，以学会为 Mac 或 iOS 设备开发应用程序。

为什么我要先教你 C 语言？每一个有效的 Objective-C 程序员都需要对 C 有相当深入的理解。此外，许多在 Objective-C 中看起来复杂的想法在 C 中都有非常简单的根源。我经常会用 C 引入一个概念，然后引导你并在 Objective-C 中掌握同一个概念。
本书的设计初衷是在 Mac 面前阅读。你将读到关于概念的解释，并进行说明这些概念的动手操作实验。这些实验不是可选的。如果你不完成它们，就无法真正理解这本书。学习编程最好的方法就是输入代码、犯错、修复错误，并从物理上熟悉语言的模式。仅仅阅读代码和在理论上理解概念对你和你的技能帮助不大。

为了进行更多练习，每章末都有名为 `Challenges`（挑战）的练习。这些练习提供了额外的练习，并将让你对刚刚学的内容更有信心。我强烈建议你尽可能完成所有的 `Challenges`。
你会在某些章节的结尾看到名为 `For the More Curious`（致好奇者）的部分。这些是对章节涵盖主题的更深入的解释。它们对于你的目标并不是绝对必要的，但我希望你会发现它们有趣且有用。


如果你学会盲打，你会发现这本书以及整个编程过程会愉快得多。盲打不仅速度快得多，还能让你看屏幕和书，而不是看键盘。这让你在错误发生时更容易捕捉到它们。这项技能将在你的整个职业生涯中受益匪浅。


通过开始本书，你决定成为一名程序员。你应该知道自己签署了什么。
程序员的生活大部分时候是一场无休止的斗争。在不断变化的技术格局中解决问题意味着程序员始终在学习新事物。在这种情况下，“学习新事物”是“与自己的无知作战”的委说法。即使程序员正在使用熟悉的技术，有时我们创建的软件也极其复杂，仅仅理解哪里出了问题往往就需要一整天的时间。

如果你写代码，你就会挣扎。大多数专业程序员学会了一小时又小时、日复一日地挣扎，而不会感到（太）沮丧。这是另一项让你受益的技能。如果你对程序员的生活和现代软件项目感兴趣，我强烈推荐 Scott Rosenberg 的著作《Dreaming in Code》（代码中的梦想）。

现在是时候投入并编写你的第一个程序了。

现在我们知道了本书的结构，是时候看看为 Mac 以及 iPhone 和 iPad 编程是如何运作的。为了做到，你将：

*   安装 Apple 开发工具
*   使用这些工具创建一个简单的项目
*   探索如何使用这些工具来确保我们的项目运行

在本章结束时，你将成功地为 Mac 编写你的第一个程序。


为了为 Mac OS（Macintosh）或 iOS（iPhone 和 iPad）编写应用程序，你将使用 Apple 的开发工具。你可以从 `http://developer.apple.com/` 下载这些工具，或从 Mac App Store 购买。

安装工具后，在硬盘的根目录下找到 `/Developer` 文件夹。该文件夹包含了为 Mac OS 桌面和 iOS 移动设备开发应用程序所需的内容。

我们在书中的工作几乎完全通过一个应用程序进行——Xcode，它位于 `/Developer/Applications`。（将 Xcode 图标拖到 Dock 栏是一个好主意，你会频繁使用它。）


Xcode 是 Apple 的集成开发环境（IDE）。这意味着编写、构建和运行新应用程序所需的所有内容都在 Xcode 中。


某些程序没有图形界面并在后台运行几天；我们称这些为守护进程（daemons）。守护进程听起来很可怕，但其实并不是。你现在 Mac 上可能有大约 60 个守护进程在运行。它们正等在那里，希望能够派上用场。例如，运行在你系统上的守护进程之一被称为 `pboard`。当你执行复制和粘贴时，`pboard` 守护进程会持有你正在复制的数据。

某些程序没有图形界面并在终端中运行一段时间；我们称这些为命令行工具（command-line tools）。在书中，你将主要编写命令行工具，以关注编程核心，而不受创建和管理用户界面的干扰。
现在我们将使用 Xcode 创建一个简单的命令行工具，以便你看到这一切是如何运作的。

当你编写程序时，你会创建并编辑一组文件。Xcode 在一个项目中跟踪这些文件。启动 Xcode。从 File 菜单选择 New，然后选择 New Project…。



![Choosing template](img/00001.jpg)

点击 Next 。





![选择选项](img/00002.jpg)

点击 `Next` 按钮。
现在选择你将创建项目目录的文件夹。你不需要用于版本控制的仓库，所以可以取消勾选该框。最后，点击 `Create` 按钮。

在接下来的几个章节中，你将反复创建这种类型的项目。在将来，我将直接说：“创建一个名为 `program-name-here` 的新 C 命令行工具”，以让你按照相同的顺序操作。



创建项目后，你将看到一个窗口，它显示了 `AGoodStart` 将是如何生成的。


![AGoodStart 项目首次视图](img/00003.jpg)

此窗口包含了许多细节，例如哪些版本的 Mac OS X 可以运行你的应用程序、编译你编写的代码时使用的配置，以及应用于你项目中的任何本地化设置。但让我们暂时忽略这些细节，找到一个简单的起点来开始工作。
在左侧面板的顶部，找到名为 `main.c` 的文件并点击它。（如果你没有看到 `main.c`，点击标记为 `AGoodStart` 文件夹旁边的三角形以展开其内容。）


![在 AGoodStart 组中寻找 main.c](img/00004.jpg)


```c
#include <stdio.h>
int main (int argc, const char * argv[]) {
    // 在此处插入代码...
    return 0;
}
```


* 注释会被计算机忽略，但程序员使用它们来记录我们编写的代码。你试图解决的编程问题越复杂，注释就越能帮助记录你是如何解决它的。当你在几个月后回到工作中，看着遗忘的代码，并心想：“我确定这个解决方案很棒，但我完全不记得它是如何运行的。”时，这种注释就变得尤为重要。

在 C 和 Objective-C 中，有两种方法区分注释和代码：
* 如果你在行代码的开头放置 `//`，那么从这些斜杠到该行结束的所有内容都被视为注释。你可以在“在此处插入代码...”中看到这种用法。
* 如果你有更详细的备注，可以使用 `/*` 和 `*/` 来标记跨越多行的注释的开始和结束。

这些标记注释的规则是 C 语法的一部分。语法是规定在特定语言中必须如何编写代码的规则集。这些规则非常具体，如果你未能遵守这些规则，你的程序将无法运行。


幸运的是，Xcode 有方法警告你这类错误。事实上，作为程序员，你面临的首要挑战之一就是解释当出现问题时 Xcode 告诉了你的信息，然后修复你的错误。随着本书的进行，你将看到 Xcode 对常见错误的一些响应。

让我们对 `main.c` 做一些更改。首先，我们需要腾出空间。找到标记 `main` 函数开始和结束的大括号 `{` 和 `}`。然后删除中间的所有内容。

现在更新 `main.c` 看起来像下面的代码。你将在 `main` 函数中添加一条注释、两行代码和另一条注释。现在，如果你你不理解输入的内容，请不要担心。想法是先开始。你还有整本书的时间来学习这一切的含义。

#include <stdio.h>
int main (int argc, const char * argv[]) {
    // 输出小说的开头
    printf("It was the best of times.\n");
    printf("It was the worst of times.\n");
    /* 那样真的好吗？
       也许它需要重写。 */
}
```

（注意，你需要输入的新代码以**粗字体**显示。未加粗的代码是已经存在的代码。这是我们在本书其余部分将使用的约定。）






（当你在使用这段代码或未来编写的任何代码遇到构建失败时，不要感到沮丧。犯错和纠错有助于你理解自己在做什么。事实上，这实际上比运气好第一次就成功要好得多。）

一旦构建成功，在日志导航器顶部找到标记为 `Debug` AGoodStart 的项。点击此项以显示程序最近运行的日志。


```
GNU gdb 6.3.50-20050815 (Apple version gdb-1705) (Tue Jul  5 07:36:45 UTC 2011)
Copyright 2004 Free Software Foundation, Inc.
GDB is free software, covered by the GNU General Public License, and you are
welcome to change it and/or distribute copies of it under certain conditions.
There is absolutely no warranty for GDB. Type "show warranty" for details.
This GDB was configured as "x86_64-apple-darwin".tty /dev/ttys001
[Switching to process 2723 thread 0x0]
It was the best of times.
It was the worst of times.
```
（在我写这些文字时，Apple 正在开发一种名为 `LLDB` 的新调试器。它最终将取代当前的调试器 `GDB`。如果你没有看到所有的 `GDB` 信息，这意味着 `LLDB` 现在是 `Xcode` 的标准调试器了。未来一定是一个极佳的地方；我羡慕你们。）


现在你已经构建并运行了程序，让我们来内部观察吧。程序是函数的集合。函数是处理器要执行的一系列操作列表。每个函数都有一个名称，你刚刚编写的函数名为 `main`。还有另一个函数——`printf`。你没有写这个函数，但你确实使用了它。（我们将在第 5 章中找出 `printf` 来自何。）

对于程序员来说，编写一个函数非常像写食谱：“慢慢搅拌一夸水直到它煮开。然后加入一杯面粉。趁热上菜。”


图 2.5 一张名为“烤鸡”的食谱卡

![一张名为“烤鸡”的食谱卡](img/00009.jpg)

Betty Crocker 的烹饪指令是英语。在本书的第一部分，你的函数将用 C 语言编写。然而，计算机处理器期望的是机器码指令。我们如何到达那里呢？
当你用 C 编写程序时（这对你来说相对愉快），编译器会将你的程序函数转换为机器码（这对处理器来说既愉快又高效）。编译器本身是一个程序，当你按下运行按钮时，由 `Xcode` 运行。编译程序等同于构建程序，我们将交替使用这些术。

当你运行程序时，编译后的函数会从硬盘拷贝到内存中，处理器执行名为 `main` 的函数。`main` 函数通常会调用其他函数。例如，你的 `main` 函数调用了 `printf` 函数。（关于函数如何相互作用的更多信息，我们将在第 5 章中看到。）


到此为止，你可能已经处理了几种挫败：安装问题、拼写错误以及大量的新词汇。也许你到目前为止做的一切都没有任何意义。这完全是正常。

在我写这些文字时，我的儿子 Otto 六岁了。Otto 每天都会感到好几次困惑。他不断尝试吸收那些不符合他现有心理支架的知识。困惑发生得如此频繁，以至于它并不真的困扰他。他从未停下来想：“为什么这这么难懂？我应该把这本书扔掉吗？”

随着年龄增长，我们感到困惑的情况少得多——不是因为我们无所不知，而是因为我们倾向于避开那些让我们迷茫的事情。例如，读一本历史书是非常愉快的，因为我们获得了一些可以挂在现有心理支架上的知识点。这是易学。


学习编写程序也是困难学习。你会时不时感到困惑。


在这些章节中，我们将探索编程的基础概念。我们将从程序的结构方式以及它如何处理数据开始。


继续上一章的食谱比喻，有时厨师会留一块黑板来存储数据。例如，在拆火鸡时，他注意到一个写着“14.2”的标签。在扔掉包装之前，他会在黑板上写下 `weight = 14.2`。然后，在把火鸡放入烤箱之前，他会参考重量计算烹饪时间（每磅 15 分钟）。


![使用黑板跟踪数据](img/00010.jpg)

在执行期间，程序经常需要存储将要使用的数据的地方。一个数据可以存放的地方被称为变量。每个变量都有一个名称（如 `cookingTime`）和一个类型（如数字）。此外，当程序执行时，变量将有一个值（如 228.0）。



```c
float weight;
```


在 C 中，你必须声明每个变量的类型有两个：

*   类型让编译器检查你的工作并提醒你可能的错误或问题。例如，假设你有一个存储文本的类型。如果你请求它的对数，编译器会告诉你类似“请求该变量的对数毫无意义”的内容。
*   告诉编译器为该变量留出内存空间（多少字节）。

以下是常用类型的概览。我们将在后面的章节中详细介绍每种类型。
| `short`, `int`, `long` |
| `float`, `double` |
| `char` |
| pointers（指针） |
| `struct` |
这些是 C 程序员每天使用的类型。仅仅这五个简单概念能捕捉如此复杂的想法，真是令人惊讶。





现在创建一个新项目（File` → `New` → `New Project...`）。此项目将是一个名为 `Turkey` 的 C 命令行工具（Command Line Tool）。

在项目导航器中，找到该项目的 `main.c` 文件并打开它。编辑 `main.c` 使与以下代码匹配。

#include <stdio.h>

int main (int argc, const char * argv[])
{
    // 声明一个类型为 float 的变量 'weight'
    float weight;
    // 给该变量赋一个数字
    // 打印给用户
    printf("The turkey weighs %f.\n", weight);
    // 声明另一个类型为 float 的变量
    float cookingTime;
    // 计算烹饪时间并存储变量中
    // 在此情况下，'*' 表示 '乘以'
    // 将结果打印给用户
    printf("Cook it for %f minutes.\n", cookingTime);
    // 结束函数并指示成功
    return 0;
}
```
编译并运行程序。你可以点击 Xcode 窗口左角的 Run 按钮，或者使用键盘快捷键 `Command-R`。然后点击 ![带有变量的程序](img/00006.jpg) 按钮进入日志导航器。选择标记为 `Debug Turkey` 的顶部项目以显示输出。它看起来应该是这样的：

```
Cook it for 228.000000 minutes.
```

现在点击 ![带有变量的程序](img/00005.jpg) 按钮返回项目导航器。然后选择 `main.c`，你就可以再次看到你的代码。让我们回顾一下你在这里所的工作。


```c
    float weight;
```
我们称你正在“声明变量 `weight`，其类型为 `float`”。

在接下来的一行中，你的变量获得了一个值：

    weight = 14.2;
```


在现代 C 中，你可以在一行内声明变量并为其赋初始值，如下所示：

    float weight = 14.2;
```

这里是另一个赋值：

    cookingTime = 15.0 + 15.0 * weight;
```


例如，在这一行中：

    weight = 14.2;
```


变量是任何程序的构建块。这只是对变量世界的介绍。随着我们的学习，你将学习更多关于变量如何工作以及如何使用它们。


创建一个名为 `TwoFloats` 的新 C 命令行工具。在 `main()` 函数中，声明两个类型为 `float` 的变量，并为它们中的每一个分配一个带有小数点的数字，例如 `3.14` 或 `42.0`。声明另一个类型为 `double` 的变量，并将其赋值这两个 `float` 变量的和。使用 `printf()` 打印结果。如果你需要检查语法，请参考本章中的代码。


## if/else

编程中一个重要的思想是根据情况采取不同的行动。订单中的所有计费字段都已填写了吗？如果是，启用提交（Submit）按钮。玩家还有剩余生命吗？如果是，继续游戏。如果没有，显示坟墓的图片并播放悲伤的音乐。

这种行为使用 `if` 和 `else` 实现，它们的语法如下：
```c
if (conditional) {
    // 如果条件为真，则执行此代码
} else {
}
```

在本章中你将不会创建一个项目。相反，请根据你在最后两章中学到的知识仔细考虑这些代码示例。


```c
float truckWeight = 34563.8;
// 它在限制之内吗？
if (truckWeight < 40000.0) {
} else {
    printf("It is a heavy truck\n");
}
```



```c
     printf("Truck weight is not within legal range.\n");
     printf("Impound truck.\n");
```

为什么？想象一下如果你删除了大括号。

```c
BOOL isNotLegal = !((truckWeight > 0.0) && (truckWeight <  40000.0));
     printf("Truck weight is not within legal range.\n");
     printf("Impound truck.\n");
```

这段代码会让你在卡车司机中非常不受欢迎。在这种情况下，无论重量如何，每辆卡车都会被扣押。当编译器在条件后没有找到大括号时，只有下一条语句被视为 `if` 结构的一部分。因此，第二条语句始终会被执行。（第二条语句的缩进又是呢？虽然缩进对于人类阅读代码非常有帮助，但对编译器来说没有任何意义。）
## else if

如果你有两种以上的可能性怎么办？你可以使用 `else if` 逐个对它们进行测试。例如，想象一辆卡车属于三种重量类别之一：浮空型、轻型和重型。

```c
     printf("A floating truck\n");
} else if (truckWeight < 40000.0) {
     printf("A light truck\n");
} else {
     printf("A heavy truck\n");
```

你可以根据需要拥有任意数量 `else if` 子句。它们将按照出现的顺序逐一测试，直到其中一个评估为真。“按照它们出现的顺序”这一点非常重要。请务必排列你的条件顺序，以防止出现误报。例如，如果你交换了上面示例中的前两个测试，你将永远找不到浮空型卡车，因为浮空型卡车也是轻型卡车。最后的 `else` 子句是可选的，但当你想要捕获所有不满足之前条件的情况时，它是很有用的。


在实际开发中，你经常使用 `if` 和 `else` 来给实例变量赋值，这并并不罕见。例如，你可能会有以下代码：

```c
int minutesPerPound;
     minutesPerPound = 15;
else
     minutesPerPound = 20;
```


```c
int minutesPerPound = isBoneless ? 15 : 20;
```


如果你觉得这种写法很奇怪，继续使用 `if` 和 `else` 也没有什么问题。我怀疑，随着时间的推移，你会接受三元运算符，作为一种进行条件赋值的简洁方式。更重要的是，你将看到其他程序员使用它，而理解你所看到的内容是件好事！

## 挑战


```c
int i = 20;
int j = 25;
int k = ( i > j ) ? 10 : 5;
     printf("The first expression is true.");
} else if ( j > i ) { // 第二个表达式
     printf("The second expression is true.");
} else {
     printf("Neither expression is true.");
```

控制台会打印什么？

# 5
## 函数

在第 3 章 中，我引入了变量的概念：与数据块关联的名字。函数是一个与代码块关联的名字。你可以将信息传递给 `function`。你可以让 `function` 执行代码。你可以让 `function` 向你返回信息。

函数是编程的基础，所以本章有很多内容——三个新项目、新工具和许多新思想。让我们从一个演示函数用途的练习开始。
### 我应该何时使用函数？

假设你正在编写一个程序来祝贺学生完成 Big Nerd Ranch 的课程。在担心从数据库中检索学生列表或在精美的 Big Nerd Ranch 纸张上打印证书之前，你想先实验一下打印在证书上的信息。

为了进行这个实验，创建一个新项目：一个名为 `ClassCertificates` 的 C 命令行工具。
编写此程序时，你的第一个想法可能是：

```c
int main (int argc, const char * argv[])
{
     printf("Mark has done as much Cocoa Programming as I could fit into 5 days\n");
```

重复 `printf` 中的所有内容会让你感到苦吗？如果是这样，你就具备了优秀程序员的特质。

### 我如何编写和使用函数？
现在你已经意识到你需要一个 `function`，并且需要写一个。打开 `ClassCertificates` 项目中的 `main.c`，并在 `main` 之前添加新函数。将此函数命名为 `congratStudent`。

```c
#include <stdio.h>
void congratulateStudent(char *student, char *course, int numDays)
{
}
```

编辑 `main` 以使用你的新函数：

```c
{
     congratulateStudent("Mark", "Cocoa", 5);
     congratulateStudent("Bo", "Objective-C", 2);
     congratulateStudent("Mike", "Python", 5);
     congratulateStudent("Ted", "iOS", 5);
}
```

编译并运行程序。你可能会得到一个带有小黄色三角形和内部感叹号标记的警告。Xcode 中的警告不会阻止程序的运行；它只是引起了你对可能问题的注意。警告文本位于代码右侧。这个警告内容类似于 `No previous prototype for function 'congratStudent'`。暂时忽略这个警告，我们会在本节末尾回来讨论。


- `Mark has done as much Cocoa Programming as I could fit into 5 days.`
- `Bo has done as much Objective-C Programming as I could fit into 2 days.`
- `Mike has done as much Python Programming as I could fit into 5 days.`
- `Ted has done as much iOS Programming as I could fit into 5 days.`


函数名称左侧的 `void` 是什么？它是函数返回信息的类型。当你没有任何信息要返回时，使用 `void` 关键字。我们将在章稍些时候详细讨论返回。




你还在 `main` 中使用了或调用了你的新函数。当你调用 `congratulateStudent` 时，你向它传递了值。传递给函数的值被称为参数（arguments）。参数的值随后会被赋值给对应的参数名称（parameter name）。该参数名称可以在函数内部作为变量使用，包含传入的值。

让我们具体来看。在第一次调用 `congratulateStudent` 时，你传递了三个参数：`"Mark", "Cocoa", 5`。

congratulateStudent("Mark", "Cocoa", 5);
```

现在，我们重点关注第三个参数。当 `5` 被传递给 `congratulateStudent` 时，它会被赋值给第三个参数 `numDays`。参数和形参按照它们出现的顺序进行匹配。它们的类型也必须相同（或非常接近）。在这里，`5` 是一个整数值，而 `numDays` 的类型是 `int`。很好。

现在，当 `congratulateStudent` 在函数内部使用或引用 `numDays` 变量时，它的值将是 `5`。你可以看到 `numDays` 在分号之前被引用了。最后，你可以通过查看输出的第一行来证明这一切都正常工作，它正确地显示了天数。
回想我们最初提出的那个包含大量重复输入的 `ClassCertificates` 版本。使用函数的意义是什么？是为了节省输入量吗？是的，但这绝对不是全部。它还为了错误检查。你输入的越少，计算机处理得越多，出现拼写错误的机会就越少。此外，如果你写错了函数名，`Xcode` 会提醒你，但 `Xcode` 并不知道你是否写错了文本内容。

编写函数的另一个好处是可重用性。现在你已经写了这个实用的函数，你可以在另一个程序中使用它。修改起来也更简单了。你只需要在一个地方调整祝贺语句的措辞，它就会在所有地方生效。

函数的最后一个好处是，如果出现了“漏洞”（bug），你可以修复那一个函数，突然所有调用它的地方都会开始正常工作。将代码划分成函数使其更容易理解和维护。
现在回到你代码中的那个警告。在某处声明函数而在另一个地方定义它是非常常见的。声明函数只是警告编译器即将有一个特定名称的函数。定义函数才是你描述应该执行的步骤的地方。在这个练习中，你实际上在同一个地方声明并定义了函数。因为这并不常见，所以如果你的函数没有提前声明，`Xcode` 就会发出警告。

在本书中构建的任何项目中，忽略这个警告都是可以的。你也可以花时间禁用它。要这样做，请选择 `ClassCertificates` 目标（target），它是项目导航器顶部的项目。在编辑器窗格中，选择 `Build Settings` 选项卡下的 `All`。滚动查看不同的构建设置并找到 `Missing Function Prototypes` 设置。将此设置更改为 `No`。

 5.1 禁用 Missing Function Prototypes 警告
![Disabling Missing Function Prototypes warning](img/00011.jpg)

## 函数如何协同工作

程序是函数的集合。当你运行程序时，这些函数会从硬盘复制到内存中，处理器找到名为 `main` 的函数并执行它。


图 5.2 食谱卡片

![Recipe cards](img/00012.jpg)


当你准备调味面包屑时，停止执行“烤鸡肉”卡片。当面包屑准备好后，继续执行“烤鸡肉”卡片。

同样，`main` 函数会停止执行并“阻塞”，直到它调用的函数执行完毕。为了看到这种情况，我们将调用一个 `sleep` 函数，它的作用只是等待几秒。在你的 `main` 函数中，添加对 `sleep` 的调用。

int main (int argc, const char * argv[])
{
    congratulateStudent("Mark", "Cocoa", 5);
    sleep(2);
    congratulateStudent("Bo", "Objective-C", 2);
    congratulateStudent("Mike", "PHP and PostgreSQL", 5);
    sleep(2);
    congratulateStudent("Ted", "iOS", 5);
    return 0;
}

编译并运行程序。（现在忽略关于隐式声明的警告。）你应该能看到每条祝贺消息之间看到 2 秒的暂停。这是因为 `main` 函数会停止运行，直到 `sleep` 函数完成睡眠。

注意，当你调用一个函数时，你使用它的名称和一对用于参数的括号。因此，当我们谈论函数时，通常会包含一对空括号。从现在起，我们在谈论函数时将说 `main()`。



想象一下，你正在制作一份“烤鸡”的食谱。在你的厨房里，所有的食谱都有自己专属黑板，所以你已经准备好了一个用于“烤鸡”食谱的黑板。现在，当你调用“调味面包屑”食谱时，你需要一个新的黑板。你打算把它放在哪里呢？就放在“烤鸡”食黑板的正上方。毕竟，你为了制作“调味面包屑”而暂停了“烤鸡”的执行。在“调味面包屑”完成且帧被丢弃之前，你不需要“烤鸡”的帧。你现在拥有的是一栈帧。

图 5.3 栈中的两个黑板
![栈中的两个黑板](img/00013.jpg)

程序员们常说：“当一个函数被调用时，它的帧会在栈的顶端创建。当函数执行完毕时，它的帧会从栈中弹出并被销毁。”

让我们通过在一个假设的程序中加入 `showCookTimeForTurkey()`，来更仔细地观察栈的工作原理：
```c
void showCookTimeForTurkey(int pounds)
{
    int necessaryMinutes = 15 + 15 * pounds;
}

int main(int argc, const char * argv[])
{
    int totalWeight = 10;
    int turkeyWeight = totalWeight - gibletsWeight;
    showCookTimeForTurkey(turkeyWeight);
    return 0;
}

回想 `main()` 总是第一个执行的。`main()` 调用 `showCookTimeForTurkey()`，后者开始执行。那么，在 `pounds` 乘以 15 之后，这个程序的栈是什么样子的？

图 5.4 栈上的两个帧


栈始终是后进先出的（LIFO）。这意味着，`showCookTimeForTurkey()` 在 `main()` 从栈中弹出其帧之前，先将其帧从栈中弹出。

注意，`pounds` 作为 `showCookTimeForTurkey()` 的唯一参数，它是帧的一部分。记住，参数是一个局部变量，它被赋值了对应实参数的值。在这个例子中，值为 `9` 的变量 `turkeyWeight` 被作为参数传递给 `showCookTimeForTurkey()`。然后该值被赋值给参数 `pounds` 并复制到函数的帧中。


函数可以调用自己吗？你当然可以！我们称之为递归。有一首臭名无臭的歌曲叫《99 瓶啤酒》。创建一个名为 `BeerSong` 的新 C 命令行工具。打开 `main.c` 并添加一个函数来写出这首歌的词，然后在 `main()` 中启动它：

```c
void singTheSong(int numberOfBottles)
{
    if (numberOfBottles == 0) {
        printf("There are simply no more bottles of beer on the wall.\n");
        printf("%d bottles of beer on the wall. %d bottles of beer.\n",
               numberOfBottles, numberOfBottles);
        int oneFewer = numberOfBottles - 1;
        printf("Take one down, pass it around, %d bottles of beer on the wall.\n",
        singTheSong(oneFewer); // 这个函数调用了自己！
        printf("Put a bottle in the recycling, %d empty bottles in the bin.\n",
               numberOfBottles);
    }
} 
{
    singTheSong(99);
    return 0;
}

构建并运行程序。输出如下：

`99 bottles of beer on the wall. 99 bottles of beer.`
`Take one down, pass it around, 98 bottles of beer on the wall.`
`Take one down, pass it around, 97 bottles of beer on the wall.`
`97 bottles of beer on the wall. 97 bottles of beer.`
`…`
`1 bottles of beer on the wall. 1 bottles of beer.`
`Take one down, pass it around, 0 bottles of beer on the wall.`

（注：提供的文本末尾包含几处重复/碎片化的句子，这些似乎是源代码中的痕迹或错误。我保留了上述提供的递归示例的核心逻辑。）

## 理解栈与调试


注意，`pounds` 作为 `showCookTimeForTurkey()` 的唯一参数，它是帧的一部分。记住，参数是一个局部变量，它被赋值了对应实参数的值。在这个例子中，值为 `9` 的变量 `turkeyWeight` 被作为参数传递给 `showCookTimeForTurkey()`。然后该值被赋值给参数 `pounds` 并复制到函数的帧中。

（注：源文件中提供的剩余文本中包含了关于 Xcode UI 元素的大量重复和碎片化句子。根据保留核心内容和移除冗余行的指令，优先考虑了功能性解释。）


我们刚刚在这里快速查看了调试器，以演示栈帧（frames）是如何工作的。然而，当你的程序运行结果不符合预期，且你需要查看实际发生了什么时，使用调试器设置断点并浏览程序栈中的栈帧将将会非常有帮助。

## return
许多函数在完成执行时会返回一个值。你可以通过函数名之前的类型知道该函数将返回什么类型的数据。（如果函数不返回任何内容，它的返回类型为 `void`。）

创建一个名为 `Degrees` 的新 C 命令行工具。在 `main.c` 中，在 `main()` 之前添加一个将温度从摄氏转换为华氏的函数。然后更新 `main()` 来调用这个新函数。

```c

float fahrenheitFromCelsius(float cel)
{
    float fahr = cel * 1.8 + 32.0;
    printf("%f Celsius is %f Fahrenheit\n", cel, fahr);
    return fahr;
}
int main(int argc, const char * argv[])
{
    float freezeInC = 0;
    float freezeInF = fahrenheitFromCelsius(freezeInC);
    printf("Water freezes at %f degrees Fahrenheit\n", freezeInF);
}
```

看我们是如何获取 `fahrenheitFromCelsius()` 的返回值并将其赋值给类型为 `float` 的变量 `freezeInF` 的？很酷，对吧？


```c
float average(float a, float b)
{
    return (a + b)/2.0;
}
```

如果你调用了这个函数，`printf()` 的调用将永远不会执行。
那么，一个自然产生的问题是：“我们为什么要总是从 `main()` 返回 0？”当你向系统返回 `0` 时，你是在说“一切正常”。如果你是因为发生了某些错误而终止程序，你将返回 `1`。

这看起来可能与 `if` 语句中 `0` 和 `1` 的工作方式相矛盾；因为 `1` 是真，而 `0` 是假，人们自然地会认为 `1` 代表成功，`0` 代表失败。所以把 `main()` 想象成返回一个错误报告。在这种情况下，`0` 是好消息！成功就是没有错误。


```c
#include <stdio.h>
#include <stdlib.h>
float fahrenheitFromCelsius(float cel)
{
    float fahr = cel * 1.8 + 32.0;
    printf("%f Celsius is %f Fahrenheit\n", cel, fahr);
    return fahr;

int main(int argc, const char * argv[])
{
    float freezeInC = 0;
    printf("Water freezes at %f degrees Fahrenheit\n", freezeInF);
    return EXIT_SUCCESS;
}
```
在本书中，我们通常会使用 `0` 而不是 `EXIT_SUCCESS`。

## Global and static variables


```c
#include <stdio.h>
#include <stdlib.h>
// Declare a global variable
float lastTemperature;

{
    lastTemperature = cel;
    float fahr = cel * 1.8 + 32.0;
    printf("%f Celsius is %f Fahrenheit\n", cel, fahr);
}

int main(int argc, const char * argv[])
{
    float freezeInF = fahrenheitFromCelsius(freezeInC);
    printf("Water freezes at %f degrees Fahrenheit\n", freezeInF);
    printf("The last temperature converted was %f\n", lastTemperature);
}
```


# 6


我们已经使用过数字来测量和显示温度、重量以及煮火鸡的时间。现在，让我们仔细看看数字在 C 中是如何工作的。在计算机上，数字有两种口味：整数和浮点数。你已经用过这两种了。本章试图总结 C 程序员对这些数字需要了解的知识。


但在讨论数字之前，让我们仔细看一眼你一直在使用的 `printf()` 函数。`printf()` 向日志打印一个字符串。字符串是一串字符。基本上，它是文本。

重新打开你的 `Certificates` 项目。在 `main.c` 中，找到 `congratulateStudent()`。

void congratulateStudent(char *student, char *course, int numDays)
{
    printf("%s has done as much %s as I could fit into %d days.\n");
}
```
```

这个 `printf()` 调用做了什么？嗯，你已经见过它的输出；知道它是做什么的。现在让我们弄清楚它是如何实现的。

`printf()` 是一个接受字符串作为参数的函数。你可以通过双引号包裹文本来创建一个字面量字符串（而不是存储在变量中的字符串）。
`printf()` 接收的字符串被称为格式字符串，且格式字符串可以包含标记（tokens）。该字符串中的这三个标记是 `%s`、`%s` 和 `%d`。当程序运行时，标记会被变量的值替换。在这种情况下，这些变量是 `student`、`course` 和 `numDays`。注意它们在输出中是顺序替换的。如果你在列表中交换了 `student` 和 `course`，你会看到：

`Cocoa has done as much Mark Programming as I could fit into 5 days.`


三角形的内角和必须为 180。创建一个名为 `Triangle` 的新 C 命令行工具。在 `main.c` 中，写一个接受两个角并返回第三个角的函数。这是调用它时的样子：

```c

int main(int argc, const char * argv[])
{
    float angleA = 30.0;
    float angleB = 60.0;
    printf("The third angle is %.2f\n", angleC);
    return 0;
}
```
输出应该是：
`The third angle is 90.00`



注意 `student` 和 `course` 被声明为类型 `char *`。目前，只需将 `char *` 读作一种字符串类型即可。我们将在第 14 章 中回到字符串，并在第 34 章 中再次回到 `char *`。

最后，`\n` 是什么意思？在 `printf()` 语句中，你必须包含一个显式的换行符，否则所有的日志输出将挤在同一行。`\n` 代表换行符。
现在让我们回到数字。

## 整数


为了解决这些不同的问题，整数变量有不同的尺寸。整数变量具有特定位数的位可以在其中编码数字，变量位数越高，它能存储的数字就越大。典型尺寸有：8 位、16 位、32 位和 64 位。

同样，某些问题需要负数，而另一些则不需要。因此，整数类型有符号（signed）和无符号（unsigned）之。
无符号 8 位数可以存储 0 到 255 之间的任何整数。我是怎么得出的？`2⁸ = 256` 种可能的数字。我们选择从 0 开始。

有符号 64 位数可以存储 -9,223,372,036,854,775,807 到 9,223,372,036,854,775,807 之间的任何整数。`2⁶³ = 9,223,372,036,854,775,808` 减去一位用于符号（`+` 或 `-`）。


```c
UInt32 x; // 一个无符号 32 位整数
SInt16 y; // 一个有符号 16 位整数

然而，程序员更常用的是你在第 3 章中学的描述性类型。

```c
short b;     // 通常是 16 位（取决于平台）
int c;       // 通常是 32 位（取决于平台）
long d;      // 32 或 64 位   （取决于平台）
long long e; // 64 位

为什么 `char` 是一个数字？任何字符都可以被描述为一个 8 位数字，而计算机偏于用数字来思考。符号呢？`char`、`short`、`int`、`long` 和 `long long` 默认是有符号的，但你可以在前面加上 `unsigned` 来创建对应的无符号类型。

此外，整数的大小取决于平台。（平台是操作系统和特定计算机或移动设备的组合）。某些平台是 32 ，另一些是 64 。区别在于内存地址的大小，我们将在第 8 章 中详细讨论。
Apple 创建了两种整数类型，它们在 32 位平台上是 32 位，在 64 位平台上是 64 位：

```c
NSInteger g;
```

在 Apple 的大部分代码中，你会看到这些类型的使用。从意义上来说，它们与 `long` 和 `unsigned long` 相同。


创建一个新项目：名为 Numbers 的 C 命令行工具。在 `main.c` 中，创建一个整数并使用 `printf()` 以十进制（即十进制数字）将其打印出来：

```c
int main (int argc, const char * argv[])
{
    int x = 255;
    printf("x is %d.\n", x);
    return 0;
```

你应该看到类似的内容：
`x is 255.`
正如我们所看到的，`%d` 将整数打印为十进制数字。还有哪些标记有效？你可以以八进制（octal）或十六进制（hexadecimal）打印整数。在程序中添加几行：

```c
#include <stdio.h>
{
    int x = 255;
    printf("x is %d.\n", x);
    printf("In octal, x is %o.\n", x);
    return 0;
}
```

当你运行它时，你应该看到类似的内容：
`In octal, x is 377.`
`In hexadecimal, x is ff.`
（我们将在第 33 章 返回十六进制数字。）


```c
#include <stdio.h>
int main (int argc, const char * argv[])
    long x = 255;
    printf("x is %ld.\n", x);
    printf("In octal, x is %lo.\n", x);
    printf("In hexadecimal, x is %lx.\n", x);
    return 0;
```

如果你打印无符号数字，应该使用 `%u`：

#include <stdio.h>
int main (int argc, const char * argv[])
{
    unsigned long x = 255;
    printf("In octal, x is %lo.\n", x);
    printf("In hexadecimal, x is %lx.\n", x);
    return 0;
}

### 整数运算

算术运算符 `+`、`-` 和 `*` 的工作符合预期。它们也有符合你预期的优先级规则：`*` 在 `+` 或 `-` 之前求值。在 `main.c` 中，用计算替换之前的代码：

#include <stdio.h>
int main (int argc, const char * argv[])
{
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
}
```

你应该看到

#### 整数除法

大多数初学者对整数除法的工作方式感到惊讶。尝试一下：
```c
#include <stdio.h>
int main (int argc, const char * argv[])
{
    printf("3 * 3 + 5 * 2 = %d\n", 19);
    return 0;
}
```


如果你认为“11 除以 3 等于 3 余 2”，这其实是合理的。余数通常很有价值。取模运算符 `%` 类似于 `/`，但它返回余数而不是商：

```c
int main (int argc, const char * argv[])
{
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
    printf("11 / 3 = %d remainder of %d \n", 11 / 3, 11 % 3);
}
```

如果你想得到 `3.6667` 呢？使用强制转换运算符将 `int` 转换为 `float`。强制转换是你放在想要转换变量左侧的类型。在进行除法之前，将分母转换为 `float`：
```c
int main (int argc, const char * argv[])
{
    printf("3 * 3 + 5 * 2 = %d\n", 3 * 3 + 5 * 2);
    printf("11 / 3.0 = %f\n", 11 / (float)3);
    return 0;
}
```
现在，将执行浮点除法而不是整数除法，你会得到 `3.6667`。整数与浮点除法的规则如下：只有当分子和分母都是整数类型时才是整数除法。如果其中一个是浮点数，则执行浮点除法。

#### 运算符简写


```c
int x = 5;
x = x + 1; // x 现在是 6

C 程序员经常进行此类操作，因此创建了可以在不需要赋值的情况下改变变量值的运算符。例如，你可以使用递增运算符 `++` 将 `x` 中存储的值增加 1：

```c
x++; // x 现在是 6
```

还有一个递减运算符 `--`，它将值减 1：
```c
int x = 5;
x--; // x 现在是 4
```
如果你想让 `x` 增加 5 而不仅仅是 1 呢？你可以使用加法赋值：

```c
int x = 5;
x = x + 5; // x 现在是 10

但这个也有简写：

```c
x += 5; // x 现在是 10
```


你可以将第二行理解为“将 `x + 5` 的值赋值给 `x`”。除了 `+=` 外，还有 `-=`、`*=`、`/=` 和 `%=`。

要获取 `int` 的绝对值，你需要使用函数而不是运算符。该函数是 `abs()`。如果你想获取 `long` 的绝对值，请使用 `labs()`。这两个函数都声明在 `stdlib.h` 中中：

#include <stdio.h>
#include <stdlib.h>

int main (int argc, const char * argv[])
{
    printf("11 / 3 = %d remainder of %d \n", 11 / 3, 11 % 3);
    printf("11 / 3.0 = %f\n", 11 / (float)3);
    printf("The absolute value of -5 is %d\n", abs(-5));
    return 0;
```

## 浮点数


与整数一样，浮点数也有几种大小。与整数不同，浮点数总是有符号的：

```c
double h;      // 64 位
long double i; // 128 位
```

### 显示浮点数的标记
`printf()` 也可以显示浮点数，最常用的标记是 `%f` 和 `%e`。在 `main.c` 中，替换与整数相关的代码：

```c
int main (int argc, const char * argv[])
    double y = 12345.6789;
    printf("y is %f\n", y);
    printf("y is %e\n", y); 
    return 0;
}

当你编译并运行它时，你应该看到：

`y is 12345.678900`

因此 `%f` 使用普通的十进制计数法，而 `%e` 使用科学计数法。

注意 `%f` 目前显示小数点后 6 位。这通常有点多。通过修改标记将其限制为两位：
```c
int main (int argc, const char * argv[])
{
    double y = 12345.6789;
    printf("y is %.2f\n", y);
    return 0;
}
```


`y is 12345.68`
`y is 1.23e+04`


运算符 `+`、`-`、`*` 和 `/` 的行为完全如你预期的一样。如果你将进行大量的数学计算，你需要数学库。在 Mac 上打开终端（Terminal）应用并输入 `man math`。你将获得关于数学库中所有内容的精彩摘要：三角函数、舍入、幂、平方根和立方根等。

如果你在代码中使用了任何这些数学函数，请务必在该文件的顶部包含数学库头文件：
```c
#include <math.h>
```


## 挑战

使用数学库！在 `main.c` 中添加代码显示 1 弧度的正弦值。显示保留三小数位的数字。
# 7 循环

在 Xcode 中，再次创建一个新项目：名为 `Coolness` 的 C Command Line Tool。


```c
#include <stdio.h>
int main(int argc, const char * argv[])
{
    return 0;
}
```


假设一下，如果程序打印 12 次这种肯定，能让我 10 岁的自己感到更有信心。你会怎么做呢？

这里是笨拙的方法：
```c
#include <stdio.h>
int main(int argc, const char * argv[])
{
    printf("Aaron is Cool\n");
    // ... (重复很多次)
    return 0;
}

等等，原文显示的是：
```c
    printf("Aaron is Cool\n");
    printf("Aaron is Cool\n");
    // ... 依此类推
    return 0;}
```


### while 循环

我们将使用的第一个循环是 `while` 循环。`while` 循环的工作方式类似于 `if` 结构，但在条件成立时重复执行。修改代码使其看起来像这样：
```c
#include <stdio.h>
int main(int argc, const char * argv[])
{
    while (i < 12) {
        printf("%d. Aaron is Cool\n", i);
        i++;
    }
}
```


### for 循环

`while` 循环是一种通用的结构，但 C 程序员经常使用 `for` 循环：
```c
for (初始化; 条件; 步进) {
    代码
}

将程序使用 `for` 循环：

```c
int main(int argc, const char * argv[])
{
    for (int i = 0; i < 12; i++) {
        printf("%d. Aaron is Cool\n", i);
    return 0;
}
```


有时需要在循环内部停止循环执行。例如，假设你想遍历整数寻找数字 `x`，使得 `x + 90 = x²`。你的计划是遍历 0 到 11，找到解决方案时跳出循环。修改代码：

```c
int main(int argc, const char * argv[])
{
    int i;
    for (i = 0; i < 12; i++) {
        if (i + 90 == i * i) {
            break;
        }
    }
    return 0;
}
```


`Checking i = 0`
`Checking i = 1`
`Checking i = 2`
`Checking i = 3`
`Checking i = 5`
`Checking i = 6`
`Checking i = 7`
`Checking i = 8`
`Checking i = 10`
`The answer is 10.`

注意当调用 `break` 时，执行会直接跳转到代码块的结束。
### continue

有时你会发现自己在代码块的中间，需要说：“忘记这次循环执行的剩余部分，并开始下一次循环。”这是通过 `continue` 命令实现的。例如，如果你非常确定没有 3 的倍数满足该方程，你会如何避免浪费宝的时间去检查那些数字？




```c

int main(int argc, const char * argv[])
{
    int i;
        if (i % 3 == 0) {
            continue;
        }
        printf("Checking i = %d\n", i);
        if (i + 90 == i * i) {
        }
    }
    printf("The answer is %d.\n", i);
    return 0;
```

编译并运行它：

Checking i = 1
Checking i = 2
Checking i = 4
Checking i = 5
Checking i = 8
Checking i = 10
The answer is 10.
```
图 7.4 continue

![continue](img/00025.jpg)

## do-while 循环
酷的孩子们都不用 `do-while` 循环，但为了完整性，这里介绍一下它。`do-while` 循环在执行代码块之前不会检查表达式。因此，它确保代码块至少被执行一次。如果你重写原来的练习以使用 `do-while` 循环，它看起来像这样：

```c
int main(int argc, const char * argv[])
    int i = 0;
    do {
        printf("%d. Aaron is Cool\n", i);
        i++;
    return 0;
}
```

注意末尾的分号。这是因为与其他循环不同，`do-while` 循环实际上是一个很长的语句：
`do { 某些 } while ( 其他某些保持 true );`

这是这个 `do-while` 循环的流程图：


![do-while loop](img/00026.jpg)

## 挑战
编写一个程序，从 99 开始倒数 3 直到 0，并打印每个数字。但是，如果数字能被 5 整除，还应该打印单词“Found one!”。因此，输出应该像这样：

```
99
93
90
Found one!
87
0
Found one!
```

# 8 地址与指针
你的计算机的核心是一个处理器（中央处理单元或 `CPU`）和一片巨大的开关海洋（随机存取内存或 `RAM`），这些开关可以由处理器开启或关闭。我们说一个开关持有一个位（bit）的信息。你经常会看到 1 表示“开启”，0 表示“关闭”。

这八个开关组成一个字节（byte）信息。处理器可以获取这些开关的状态，对这些位进行操作，并将结果存储在另一组开关中。例如，处理器可能会从这里获取一个字节，从那里获取另一个字节，将它们相加，并将结果存储在其他地方的地方。


![Memory and the CPU](img/00027.jpg)

内存是有编号的，我们通常讨论特定数据字节的地址。当人们谈论 32 位 `CPU` 或 64 位 `CPU` 时，他们通常是在讨论地址有多大。64 位 `CPU` 处理的内存比 32 位 `CPU` 多得多。
## 获取地址

在 Xcode 中，创建一个新项目：一个名为 `Addresses` 的 C 命令行工具。

变量的地址是内存中存储该变量值的位置。要获取变量的地址，你使用 `&` 运算符：
```c
#include <stdio.h>

int main(int argc, const char * argv[])
    int i = 17;
    printf("i stores its value at %p\n", &i);
    return 0;
}

注意 `%p` 令牌。这是可以用内存地址替换的令牌。编译并运行程序。你会看到类似的内容：

`i stores its value at 0xbffff738`


在计算机中，一切都存储在内存中，因此一切都有地址。例如，一个函数开始于某个特定地址。要获取该地址，你只需要使用函数名：

```c
{
    int i = 17;
    printf("i stores its value at %p\n", &i);
    printf("this function starts at %p\n", main);
}
```

编译并运行程序。


如果你想在变量中存储一个地址怎么办？你可以把它放进一个大小合适的无符号整数中，但如果你在给该变量指定类型时更加具体，编译器将帮助你捕获错误。例如，如果你想要一个名为 `ptr` 的变量，它持有可以找到 `float` 的地址，你可以这样声明它：

```c
```

我们说 `ptr` 是一个指向 `float` 指针的变量。它不存储 `float` 的值；它指向一个可能存储 `float` 的地址。


```c
int main(int argc, const char * argv[])
{
    int i = 17;
    return 0;
}
```


如果你有一个地址，可以使用 `*` 运算符获取存储在那的数据。注意 `*` 的两种用法。第一种是在声明处：

```c
{
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at %p\n", addressOfI);
    printf("this function starts at %p\n", main);
}
```

第二种是在读取数据处：
```c
int main(int argc, const char * argv[])
{
    int i = 17;
    printf("i stores its value at %p\n", addressOfI);
    printf("this function starts at %p\n", main);
    printf("the value is %d\n", *addressOfI);
    return 0;
```

等等，让我们看看解引的示例：

int main(int argc, const char * argv[])
{
    int i = 17;
    int *addressOfI = &i;
    printf("this function starts at %p\n", main);
    printf("the value is %d\n", *addressOfI);
    return 0;
}

你也可以在赋值的左侧使用 `*` 运算符来在特定地址存储数据：

```c
int main(int argc, const char * argv[])
    int i = 17;
    int *addressOfI = &i;
    printf("i stores its value at %p\n", addressOfI);
    *addressOfI = 89;
    return 0;
}
```


既然一切都存在内存中，而且你现在知道如何找到数据开始的地址，下一个问题是“这个数据类型占用多少字节？”

使用 `sizeof()` 可以找到数据类型的大小。例如：

int main(int argc, const char * argv[])
{
    int i = 17;
    int *addressOfI = &i;
    *addressOfI = 89;
    printf("Now i is %d\n", i);
    printf("An int is %zu bytes\n", sizeof(int));
    printf("A pointer is %zu bytes\n", sizeof(int *));
}
```



编译并运行程序。如果你的指针长度为 4 字节，则你的程序正在 32 位模式下运行。如果你的指针长度为 8 字节，则你的程序正在 64 位模式下运行。

`sizeof()` 也可以接受变量作为参数，因此你可以像这样编写之前的程序：

int main(int argc, const char * argv[])
{
    int i = 17;
    int *addressOfI = &i;
    *addressOfI = 89;
    printf("Now i is %d\n", i);
    printf("An int is %zu bytes\n", sizeof(i));
    printf("A pointer is %zu bytes\n", sizeof(addressOfI));
    return 0;
```

## NULL


```c
float *myPointer;
// 现在将 myPointer 设置为 NULL，我稍后会在程序中存储一个指针
myPointer = NULL;

`NULL` 是什么？记住，地址只是一个数字。`NULL` 是 0。这在 `if` 语句中非常有用：

```c
...
// myPointer 是否已设置？
if (myPointer) {
    // myPointer 不是 NULL
    ...对 myPointer 指向的数据进行操作...
    // myPointer 是 NULL
}
```


## 有风格的指针声明

当你声明一个指向 `float` 的指针时，它看起来像这样：
```c
float *powerPtr;
```

由于该类型是指向 `float` 的指针，你可能想像这样写它：
```c
float* powerPtr;
```


为什么？你可以在同一行中声明多个变量。例如，如果我想声明变量 `x`、`y` 和 `z`，我可以这样做：

```c
```


你认为这些是什么？

```c
```

惊喜吧！`b` 是一个指向 `float` 的指针，但 `c` 只是一个 `float`。如果你想让它们都成为指针，你必须在每一个前面前面放一个 `*`：

```c
```

将 `*` 直接紧挨着变量名会让这更清晰。


编写一个程序，显示 `float` 消耗了多少内存。

在你的 Mac 上，`short` 是一个 2 字节的整数，使用一个位来存储符号（正或负）。它能存储的最小数字是多少？最大的数字是多少？`unsigned` `short` 只持有非负数。它能存储的最大的数字是多少？


有一个标准的 C 函数叫做 `modf()`。你给 `modf()` 一个 `double`，它会计算该数的整数部分和小数部分。例如，如果你给它 3.14，3 是整数部分，0.14 是小数部分。

你作为 `modf()` 的调用者，想要这两个部分。然而，一个 C 函数只能返回一个值。`modf()` 如何给你这两部分信息呢？
当你调用 `modf()` 时，你将提供一个地址，让它可以在那里存放一个数字。具体来说，它将返回小数部分，并将整数部分复制到你提供的地址。创建一个新项目：一个名为 `PBR` 的 C 命令行工具。

编辑 `main.c`：

```c
#include <math.h>

int main(int argc, const char * argv[])
{
    double integerPart;
    double fractionPart;
    // 将 integerPart 的地址作为参数传递
    fractionPart = modf(pi, &integerPart);
    printf("integerPart = %.0f, fractionPart = %.2f\n", integerPart, fractionPart);
    return 0;
}
```


图 9.1 `modf()` 返回时的栈
![modf() 返回时的栈](img/0028.jpg)


## 编写引用传递

描述二维空间中点的位置有两种常用方法：笛卡尔坐标系和极坐标系。在笛卡尔坐标系中，`(x, y)` 表示你应该先到 `x` 再到 `y`。在极坐标系中，`(theta, radius)` 表示你应该向左转 `theta` 弧度并移动 `radius` 。

![极坐标和笛卡尔坐标](img/0029.jpg)

如果你想写一个将笛卡尔坐标中的点转换为极坐标的函数怎么办？它需要读取两个浮点数并返回两个浮点数。函数的声明看起来如下：


也就是说，当函数被调用时，将会传递 `x` 和 `y` 的值。它还将提供可以存储 `radius` 和 `theta` 值的位置。现在在你的 `main.c` 顶部编写该函数，并在 `main()` 中调用它：

```c
#include <stdio.h>

void cartesianToPolar(float x, float y, double *rPtr, double *thetaPtr)
{
    // 待实现...

int main(int argc, const char * argv[])
{
    // 待实现...
}
```
*(注：根据上下文逻辑，此处应为具体的实现和调用，根据原文提供的代码块结构，完整逻辑如下：)*

```c
#include <math.h>

void cartesianToPolar(float x, float y, double *rPtr, double *thetaPtr)
{
    if (rPtr) {
        *rPtr = sqrt(x * x + y * y);
    }
    // 计算 theta
    if (x == 0.0) {
        if (y == 0.0) {
            theta = 0.0; // 未定义
        } else if (y > 0) {
        } else {
            theta = - M_PI_2;
        }
    } else {
        theta = atan(y/x);
    // 将 theta 存储在提供的地址
    if (thetaPtr) {
        *thetaPtr = theta;
    }

int main(int argc, const char * argv[])
{
    double pi = 3.14;
    double integerPart;
    // 将 integerPart 的地址作为参数传递
    fractionPart = modf(pi, &integerPart);
    // 找到存储在 integerPart 中的值
    printf("integerPart = %.0f, fractionPart = %.2f\n", integerPart, fractionPart);
    double y = 4.0;
    double radius;
    double angle;
    cartesianToPolar(x, y, &angle, &radius);
    return 0;
}
```

编译并运行程序。
图 9.3 `cartesianToPolar()` 返回时的栈
![cartesianToPolar() 返回时的栈](img/0030.jpg)

## 解引用 NULL
有时候可以通过引用提供许多值，但你可能只关心其中一部分。当你根本不使用这些值时，如何避免声明这些变量并传递它们的地址？通常，你传递 `NULL` 作为地址告诉函数“我不需要这个特定的值”。

这意味着在解引用指针之前，你应该始终检查它们是否为非 `NULL`。在 `cartesianToPolar()` 中添加这些检查：

```c
{
    // rPtr 是否非 NULL？
    if (rPtr) {
        // 将半径存储在提供的地址
    }
    // thetaPtr 是否为 NULL？
    if (!thetaPtr) {
        // 跳过函数的剩余部分
        return;
}
```



```c
// 计算 theta
float theta;
if (x == 0.0) {
        theta = 0.0;    // 技术上被认为未定义
    } else if (y > 0) {
        theta = M_PI_2;
    } else {
    }
} else {
    ...
}
```
# 10 结构体

有时你需要一个变量来存储几个相关的数块。例如，假设你正在编写一个计算人人体质量指数（BMI）的程序。（你的 BMI 是多少？它是你的体重（公斤）除以身高（米）的平方。BMI 低于 20 表示可能体重不足。BMI 超过 30 表示可能肥胖。这是一个衡量个人健身状况非常不精确的工具，但它是一个非常好的编程示例。）对于你的目的来说，一个人由一个表示身高（米）的 `float` 和一个表示体重（公斤）的 `int` 组成。


创建一个新项目：一个名为 `BMICalc` 的 C 命令行工具。编辑 `main.c` 来创建一个包含你所需数据的结构体：

```c

// 这里是 struct Person 的声明
struct Person {
    float heightInMeters;
};

int main(int argc, const char * argv[])
{
    struct Person person;
    person.heightInMeters = 1.8;
    printf("person weighs %i kilograms\n", person.weightInKilos);
    printf("person is %.2f meters tall\n", person.heightInMeters);
    return 0;
```

注意，你使用点（`.`）来访问结构体的成员。


图 10.1 成员赋值后的框架

![成员赋值后的框架](img/00031.jpg)
大多数时候，你会反复使用同一个结构体声明。因此，为结构体类型创建一个 `typedef` 是很常见的。`typedef` 为类型声明定义别名，允许我们更像使用普通数据类型一样使用它。修改 `main.c` 以为 `struct Person` 创建并使用 `typedef`：

```c
#include <stdio.h>

typedef struct {
    float heightInMeters;
    int weightInKilos;
} Person;
int main(int argc, const char * argv[])
{
    Person person;
    person.weightInKilos = 96;
    printf("person weighs %i kilograms\n", person.weightInKilos);
    printf("person is %.2f meters tall\n", person.heightInMeters);
    return 0;
}
```
现在你已经创建了 `typedef`，可以将 `Person` 结构体传递给另一个函数。添加一个名为 `bodyMassIndex()` 的函数，它接受一个 `Person` 作为参数并计算 BMI。然后更新 `main()` 来调用它：

```c
#include <stdio.h>
typedef struct _Person {
    float heightInMeters;
    int weightInKilos;
} Person;

{
  return p.weightInKilos / (p.heightInMeters * p.heightInMeters);
}

{
    Person person;
    person.weightInKilos = 96;
    person.heightInMeters = 1.8;
    float bmi = bodyMassIndex(person);
    return 0;
}
```


作为程序员，我处理的第一个结构体是 `struct tm`，标准 C 库用它来存储分解为各个部分的时间。结构体定义如下：

```c
struct tm {
    int    tm_min;     /* 小时后的分钟 [0-59] */
    int    tm_hour;    /* 自午夜起的小时 [0-23] */
    int    tm_mday;    /* 一个月的几 [1-31] */
    int    tm_mon;     /* 自 1 月起的月份 [0-11] */
    int    tm_wday;    /* 自周日起的几天 [0-6] */
    int    tm_yday;    /* 自 1 月 1 日起的几天 [0-365] */
    int    tm_isdst;   /* 夏令时标志 */
    long   tm_gmtoff;  /*  UTC 的偏移量（秒） */
    char   *tm_zone;    /* 时区 */
```

`time()` 函数返回自 1970 年格格威治第一时刻以来的秒数。`localtime_r()` 可以读取该时长并封装成 `struct tm`。




```c
// Allocate memory for one Person structure
     // Fill in two members of the structure
     x->weightInKilos = 81;
     x->heightInMeters = 2.0;
     // Print out the BMI of the original Person
     float xBMI = bodyMassIndex(x);
     // Let the memory be recycled
     free(x);
     // Forget where it was
     x = NULL;
}
```

注意运算符 `->`。`p->weightInKilos` 的意思是：“解引用结构指针 `p` 并获取名为 `weightInKilos` 的成员。”


# 第三部分

## Objective-C 与 Foundation
现在，你已经了解了程序、函数、变量和数据类型的基础知识，已经准备好学习 Objective-C 了。目前我们将继续使用命令行程序，以便将重点放在编程的核心要素上。

所有的 Objective-C 编程都是通过 Foundation 框架完成的。框架是你用于编写程序的类库。那么什么是类？这就是我们首先要讨论的……

# 12
## 对象

许多计算机语言都有“对象”的概念。对象类似于结构体，因为它持有数据。然而，与结构体不同，对象还包含一组作用于这些数据的函数。要触发其中一个函数，你需要向对象发送一条消息。用准确的术语来说，由消息触发的函数被称为“方法”。


对象本质上是非常“活跃”的。它们会工作，并发送和接收关于它们正在执行的工作的消息。一个复杂的 Objective-C 程序可能同时在内存中拥有数百个对象，它们互相发送消息。

类描述了一种特定类型的对象。这种描述包含了方法和实例变量，该类型的对象在其中存储数据。你请求一个类在堆上为你创建一个该类型的对象。我们称生成的对象为该类的“实例”。
例如，iPhone 自带了许多类，其中之一是 `CLLocation`。你可以请求 `CLLocation` 类创建一个 `CLLocation` 实例。在这个 `CLLocation` 对象内部有几个实例变量，用于保存位置数据，如经度、纬度和高度。该对象还有几个方法。例如，你可以询问一个 `CLLocation` 实例距离另一个 `CLLocation` 对象有多远。

#### 创建并使用你的第一个对象


图 12.1 创建一个 Foundation 命令行工具

![创建一个 Foundation 命令行工具](img/00033.jpg)


```objc
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSDate *now = [NSDate date];
    }
    return 0;
}
```
漂亮！这是你的第一次发送消息。你向 `NSDate` 类发送了 `date` 消息。`date` 方法请求 `NSDate` 类创建一个 `NSDate` 实例，将其初始化为当前日期/时间，并返回新对象的起始地址。然后你将返回的地址存储在变量 `now` 中。这个变量是一个指向 `NSDate` 对象的指针。

`NSLog()` 是一个 Objective-C 函数，与 `printf()` 相似；它接受一个格式字符串，将 `%` 标记替换为实际值，并将结果写入控制台。然而，它的格式字符串始终以 `@` 开头，且结尾不需要 `\n`。

构建并运行程序。你应该看到类似的内容：
`2011-08-05 11:53:54.366 TimeAfterTime[4862:707] The new date lives at 0x100114dc0`

与 `printf()` 不同，`NSLog()` 在输出前会加上日期、时间、程序名称和进程 ID。从现在起，当我显示 `NSLog()` 的输出时，我会跳过这些数据——页面太窄了。


```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
    @autoreleasepool {
        NSDate *now = [NSDate date];
        NSLog(@"@", now);
    }
}
```

你应该看到类似的内容：
`2011-08-05 11:53:54.366 TimeAfterTime[4862:707] 2011-08-05 11:53:54 +0000`
### 消息的剖析

消息发送总是被方括号包围，并且至少包含两个部分：

*   要触发的方法名称

消息发送（类似于函数调用）也可以带有参数。让我们来看一个例子：

#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"@", now);
        double seconds = [now timeIntervalSince1970];
        NSLog(@"It has %f seconds since the start of 1970.", seconds);
    }
}
```

`NSDate` 代表一个特定的日期时间。`NSDate` 的实例可以告诉你它与 1970 年 1 月 1 日凌晨 12:00 (GMT) 之间的差值（秒），通过向它发送 `timeIntervalSince1970` 消息来实现。
现在假设你需要一个新的对象——比你现有的对象晚 100,000 秒。`NSDate` 类有一个方法 `dateAddingInterval:`。你可以向它发送这个消息来获取新日期。使用代码：

```objc
#import <Foundation/Foundation.h>

{
    @autoreleasepool {
        NSDate *now = [NSDate date];
        NSLog(@"@", now);
        NSLog(@"In 100,000 seconds it will %@", later);
    }
    return 0;
}

在消息发送 `[now dateAddingInterval:100000]` 中，

*   `now` 是接收消息对象的指针（也称为“接收者”）
*   `dateAddingInterval:` 是方法名（也称为“选择器”）

图 12.2 消息发送

![消息发送](img/0034.jpg)
#### 内存中的对象

这是一个对象图。变量 `now` 和 `later` 是 `main()` 函数栈帧的一部分。它们指向 `NSDate` 对象，如箭头所示。

图 12.3 TimeAfterTime 的对象图
![TimeAfterTime 的对象图](img/0035.jpg)

你到为止只看到了一个类：`NSDate`。事实上，iOS 和 Mac OS X 附带了数百个类。我们将在后续章节中处理一些更常见的类。


在声明用于持有对象的指针时，大多数情况下你会指定指针所指向的对象的类：

`NSDate *expiration;`



然而，你通常需要一种方法创建一个指针，而不需要确切知道指针将指向什么种类型的对象。在这种情况下，我们使用类型 `id` 来表示“指向某种 Objective-C 对象的指针”。以下是使用它时的样子：

```objc
```

注意，在这个声明中没有星号。`id` 隐含了星号。


## 挑战

使用两个 `NSDate` 实例来计算你活了多少秒。提示：这里是如何从年、月、日等创建一个新的日期对象的：

NSDateComponents *comps = [[NSDateComponents alloc] init];
[comps setYear:1969];
[comps setMonth:4];
[comps setDay:30];
[comps setMinute:10];
[comps setSecond:0];
NSCalendar *g = [[NSCalendar alloc] initWithCalendarIdentifier:NSGregorianCalendar];
NSDate *dateOfBirth = [g dateFromComponents:comps];
```
要获取两个 `NSDate` 实例之间的秒数，请使用方法 `timeIntervalSinceDate:`。

```objc
double d = [laterDate timeIntervalSinceDate:earlierDate];

# 13

更多消息


```objc
NSDate *now = [NSDate date];
```


```objc
double seconds = [now timeIntervalSince1970];
```
我们说 `timeIntervalSince1970` 是一个**实例方法"。你通过向类的实例发送消息来导致该方法的执行。`timeIntervalSince1970` 方法返回一个 `double`。

```objc
NSDate *later = [now dateByAddingTimeInterval:100000];
```
`dateByAddingTimeInterval:` 是另一个实例方法。该方法接受一个参数。你可以通过方法名中的冒号判断出来。该方法也返回一个指向 `NSDate` 实例的指针。

## 嵌套消息发送

有一个类方法 `alloc`，它返回一个指向需要初始化的新对象的指针。该指针随后被用于向新对象发送消息 `init`。使用 `alloc` 和 `init` 是 Objective-C 中创建对象最常用的方法。一种良好的做法（也是 Apple 认可的方法）是通过嵌套消息发送，在一行代码中发送这两条消息：
```objc
[[NSDate alloc] init];
```


`init` 返回一个指向新对象的指针（这几乎总是来自 `alloc` 方法的指针），因此我们可以使用 `init` 的返回值进行赋值。通过更改以下行，在代码中尝试这些嵌套消息：

```objc
NSDate *now = [NSDate date];

改为

```objc
NSDate *now = [[NSDate alloc] init];

#### 多参数

某些方法接受多个参数。例如，`NSDate` 对象并不知道当前是月的第几天。如果你需要这些信息，将使用 `NSCalendar` 对象。可以告诉你每月第几日的 `NSCalendar` 方法接受三个参数。创建一个 `NSCalendar` 对象并在 `main.m` 中使用它：

#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
        NSDate *now = [[NSDate alloc] init];
        NSLog(@"The date is %@", now);
        double seconds = [now timeIntervalSince1970];
        NSLog(@"It has been %f seconds since the start of 1970.", seconds);
        NSDate *later = [now dateByAddingTimeInterval:100000];
        NSCalendar *cal = [NSCalendar currentCalendar];
        NSUInteger day = [cal ordinalityOfUnit:NSDayCalendarUnit
                                             inUnit:NSMonthCalendarUnit
                                            forDate:now];
        NSLog(@"This is day %lu of the month", day);
    return 0;
}
```





要获取字符串中的字符数，你可以使用 `length` 方法：
```objc
NSUInteger charCount = [x length];
```

你可以使用 `isEqual:` 方法来检查两个字符串是否相等：
```objc
if ([lament isEqual:x])
    NSLog(@"%@ and %@ are equal", lament, x);
```


```c
char *lament = "Why me!?";
char *x;
size_t charCount = strlen(x);
if (strcmp(lament, x) == 0)
    printf("%s and %s are equal\n", lament, x);
free(x);
```
我们将在第 34 章 中讨论 C 字符串。但每当你有选择时，请使用 `NSString` 对象 own 替 C 字符串。`NSString` 类有许多方法旨在让你的生活更轻松。此外，`NSString`（基于 UNICODE 标准）非常擅长存储地球上任何语言的文本。特殊字符？没问题。从右向左读的文本？不用。

## 挑战

有一个名为 `NSHost` 的类，它包含关于你计算机的信息。要获取 `NSHost` 实例，你可以使用 `NSHost` 类方法 `currentHost`。该方法返回一个指向 `NSHost` 对象的指针：
```objc
+ (NSHost *)currentHost
```


```objc
- (NSString *)localizedName
```


# 15 NSArray

和 `NSString` 类似，`NSArray` 是 Objective-C 程序员经常使用的另一个类。`NSArray` 的实例包含一个指向其他对象的指针列表。例如，假设你想创建一个包含三个 `NSDate` 对象的列表，然后遍历列表并打印每个日期。


```objc
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
{
        // 创建三个 NSDate 对象
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];
        // 创建包含所有三个对象的数组 (nil 结束列表)
        // 有几个日期？
        NSLog(@"There are %lu dates", [dateList count]);
        // 打印其中几个
        NSLog(@"The first date is %@", [dateList objectAtIndex:0]);
    }
    return 0;
}
```


- `count` 返回数组中的项数
- `objectAtIndex:` 返回数组在参数指定的索引处存储的指针。

数组是有序的，你通过索引访问数组中的项。数组是从 0 开始的：第一个项存储在索引 0，第二个项存储在索引 1，依此类推。因此，如果 `count` 方法说数组中有 100 个项目，你可以你可以使用 `objectAtIndex:` 请求索引从 0 到 99 的对象。
图 15.1 是你的程序的对象图。注意 `NSArray` 的实例有指向 `NSDate` 对象的指针。

图 15.1 DateList 的对象图
![DateList 的对象图](img/0036.jpg)
因此，如果你想通过循环来处理并处理数组中的每个项（或“遍历数组”），你可以创建一个 `for` 循环。编辑 `main.m`：

```objc
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
    @autoreleasepool {
        // 创建三个 NSDate 对象
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, nil];
        UInteger dateCount = [dateList count];
        for (int i = 0; i < dateCount; i++) {
            NSDate *d = [dateList objectAtIndex:i];
            NSLog(@"Here is a date: %@", d);
    }
    return 0;
}
```
程序员们这样做这样做，以至于他们为 `for` 循环增加了一个特殊的扩展用于遍历数组。修改代码以使用这种机制：

```objc
#import <Foundation/Foundation.h>
int main(int argc, const char * argv[])
    @autoreleasepool {
        // 创建三个 NSDate 对象
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0];
        NSDate *yesterday = [now dateByAddingTimeInterval:-24.0 * 60.0 * 60.0];
        NSArray *dateList = [NSArray arrayWithObjects:now, tomorrow, nil];
        for (NSDate *d in dateList) {
            NSLog(@"Here is a date: %@", d);
        }
    }
}
```

这种类型的循环被称为快速遍历，它是遍历数组项的一种极其高效的方式。有一个限制：你可以在遍历数组时不能添加或删除项。


数组有两种口味：

- `NSArray` 实例创建时带有指针列表。你永远无法从该数组中添加或移除指针。
- `NSMutableArray` 实例与 `NSArray` 类似，但你可以添加和移除指针。（`NSMutableArray` 是 `NSArray` 的子类。更多信息见第 18 章）
修改你的示例以使用 `NSMutableArray` 实例以及该类的方法：

```objc
#import <Foundation/Foundation.h>
{
    @autoreleasepool {
        // 创建三个 NSDate 对象
        NSDate *now = [NSDate date];
        NSDate *tomorrow = [now dateByAddingTimeInterval:24.0 * 60.0 * 60.0];
        // 创建一个空数组
        NSMutableArray *dateList = [NSMutableArray array];
        // 将日期添加到数组
        [dateList addObject:now];
        [dateList addObject:tomorrow];
        [dateList insertObject:yesterday atIndex:0];
        for (NSDate *d in dateList) {
            NSLog(@"Here is a date: %@", d);
        }
        // 移除昨天
        NSLog(@"Now the first date is %@", [dateList objectAtIndex:0]);
    }
    return 0;
}
```
## 挑战

创建一个名为 Groceries 的 Foundation 命令行工具。从创建一个空的 `NSMutableArray` 对象开始。然后向数组中添加几个杂货之类的物品（你也需要创建这些物品）。最后，使用快速遍历打印出你的购物列表。

下一个挑战确实，嗯，更具挑战性。请通读以下程序，它会寻找包含两个相邻 A 的常见专名。

```objc
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // 将一个文件读取为巨大的字符串（忽略错误的可能性）
        NSString *nameString = [NSString stringWithContentsOfFile:@"/usr/share/dict/propernames" encoding:NSUTF8StringEncoding];
    }
}
```




```objc
error:NULL];

// Break it into an array of strings
NSArray *names = [nameString componentsSeparatedByString:@"\n"];

// Go through the array one string at a time
for (NSString *n in names) {
    // Look for the string "aa" in a case-insensitive manner
    NSRange r = [n rangeOfString:@"AA" options:NSCaseInsensitiveSearch];
    // Was it found?
    if (r.location != NSNotFound) {
        NSLog(@"%@", n);
    }
}
return 0;
}
```

`/usr/share/dict/propernames` 文件包含常见的专有名词。`/usr/share/dict/words` 文件包含普通单词（不是专有名词）。现在，根据上面的代码编写一个程序，找出既是专有名词又是普通单词的词。例如，“Glen”是一个男的名字，而“glen”狭狭的山谷。

当计算机对字符串进行排序时，通常会认为大写字母在小写字母之前。要进行不区分大小写的比较，请使用 `caseInsensitiveCompare:` 方法。

```objc
NSString *a = @"ABC";
NSString *b = @"abc";

if ([a caseInsensitiveCompare:b] == NSOrderedSame) {
    NSLog(@"a and b are equal");
}

if ([a caseInsensitiveCompare:b] == NSOrderedAscending) {
    NSLog(@"a comes before b");
}

if ([a caseInsensitiveCompare:b] == NSOrderedDescending) {
    NSLog(@"b comes before a");
}
```

在本次挑战中，使用 `caseInsensitiveCompare:` 来验证“Glen”和“glen”是等价的。

# 16 开发者文档

在上一章中，我为你提供了一些关于 `NSArray` 类的有用知识。当你开始在没有我的指导下编程时（包括完成本书中的`Challenges`时），你需要自己寻找这些知识。这正是 Apple 文档派用用场。

要在 Xcode 中查看文档，请打开 Organizer（点击 Xcode 窗口右上角的 !![开发者文档](img/00037.jpg) 按钮）并选择 Documentation 标签页。

图 16.1 Organizer 中的文档

![Organizer 中的文档](img/00038.jpg)

Apple 基本上提供了五种类型的文档：

*   **参考资料 (References)**：每个 Objective-C 类和每个 C 函数在这些页面中都有简要的说明。
*   **指南和快速入门 (Guides and Getting Starteds)**：指南没有那么简洁，并按概念对想法进行分组。例如，有一份《错误处理编程指南》，描述了 Mac 和 iOS 开发者告知发生错误的各种方式。
*   **示例代码 (Sample Code)**：这些是小型、完整的项目，展示了 Apple 如何期望使用其技术。例如，有一个 WeatherMap 项目展示了如何在 iOS 地图视图上创建自定义注释。
*   **发布说明 (Release Notes)**：每当 Mac OS 或 iOS 发布新版本时，都会附带一组发布说明。发布说明告诉开发者自上版本以来发生了什么。
*   **技术备注、文章、编码教程和技术问答 (Technical notes, Articles, Coding How-to’s, and Technical Q&As)**：这些是针对特定问题的短篇文档。

你可以浏览文档，但内容非常多。通常情况下，你会通过搜索访问文档。

## 参考页面 (Reference pages)

在 Organizer 左侧面板的顶部，点击 !![参考页面](img/00039.jpg) 按钮调出搜索面板。在搜索框中输入 `NSArray`，搜索结果将出现在搜索框下方。在 Reference 部分，点击 `NSArray` 查看 `NSArray` 的参考页面。

图 16.2 NSArray 参考页面

![NSArray 参考页面](img/00040.jpg)

很难过强调这些参考页面对你有多么重要，以及对所有水平的程序员有多么重要。Apple 为了方便付出了巨大努力创建了巨大的代码库。你将主要通过参考页面来学习这些库。当你阅读这本书时，请花一点时间……





![NSMutableArray 的声明](img/00047.jpg)

如果有多个匹配的声明，当你使用 Command-点击时会弹出一个窗口。尝试 Command-点击 `addObject:`。

Xcode 会不时向“母船”回调，以检查是否有更新的文档。它将下载更新并对它们进行重新索引，以便搜索。你可以在 Xcode 的偏好设置面板中触发立即检查。

Apple 在 `http://lists.apple.com/` 托管了一系列讨论邮件列表，其中有几个专门针对开发者主题。如果你在文档中没有找到答案，可以尝试搜索这些列表的存档。（为了考虑到每个列表中成千上万的成员，请在提问之前务必仔细搜索存档。）

还有另一个你理应该了解的资源：`stackoverflow.com`。这个网站是一个非常流行的地方，程序员在这里提问和回答。如果你能想出几个描述你所遇到的问题的关键词，可能可以在那里找到答案。

# 17 你的第一个类

到目前为止，你只使用过 Apple 创建的类。现在你可以编写自己的类了。请记住，类通过两种方式来描述对象：

- 类实现的方法（包括实例方法和类方法）
- 类中每个实例的实例变量

你将编写一个 `Person` 类，类似于你在第 10 章中编写的 `struct Person`。你的类将定义在两个文件中：`Person.h` 和 `Person.m`。`Person.h` 被称为头文件或接口文件，包含实例变量和方法的声明。`Person.m` 被称为实现文件。这是你编写每个方法的步骤或实现方法的地方。

创建一个新项目：名为 BMITime 的 Foundation 命令行工具。

要创建一个新类，选择 File → New → New File....。在左侧的 Mac OS X 部分，选择 Cocoa 并选择 Objective-C class 模板。将你的类命名为 `Person` 并将其设为 `NSObject` 的子类。最后，确保勾选了 BMITime target 并点击 Save。

注意，新类文件 `Person.h` 和 `Person.m` 现在出现在项目导航器中。打开 `Person.h`。声明两个实例变量和三个实例方法：

```
#import <Foundation/Foundation.h>

// Person 类继承了 NSObject 类定义的所有实例变量
// 和方法
@interface Person : NSObject
{
    // 它有两个实例变量
    float heightInMeters;
    int weightInKilos;
}
// 你可以使用这些方法设置那些实例变量
- (void)setHeightInMeters:(float)h;
- (void)setWeightInKilos:(int)w;
// 此方法计算体质指数
- (float)bodyMassIndex;
@end
```

注意你在大括号内部声明了实例变量，并在变量之后、大括号之外声明了方法。

对于编译器来说，这段代码表示：“我正在定义一个名为 `Person` 的新类，它拥有 `NSObject` 类的所有方法和实例变量。此外，我添加了两个新的实例变量：一个名为 `heightInMeters` 的 `float` 和一个名为 `weightInKilos` 的 `int`。我还将添加三个实例方法，它们将在 `Person.m` 中实现。”

注意 `setHeightInMeters:` 期望一个 `float` 参数且没有返回值，`setWeightInKilos:` 期望一个 `int` 参数且没有返回值，而 `bodyMassIndex` 不接受参数并返回一个 `float`。

现在打开 `Person.m`。删除任何现有方法并实现你声明的方法：

```
#import "Person.h"

@implementation Person

- (void)setHeightInMeters:(float)h
{
    heightInMeters = h;
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

注意 Xcode 为你导入了 `Person.h`。另请注意，你实现的方法名称必须与头文件中声明的名称完全匹配。在 Xcode 中，这很容易；当你开始在实现文件中输入方法名时，Xcode 会建议你已经声明的方法名称。

现在你已经实现了在 `Person.h` 中声明的所有方法，你的类已经完整了。编辑 `main.m` 来练练手：

```
#import <Foundation/Foundation.h>
#import "Person.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建 Person 的实例
        Person *person = [[Person alloc] init];
        // 给实例变量赋值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"person (%d, %f) has a BMI of %f", [person weightInKilos], [person heightInMeters], bmi);
    }
    return 0;
}
```

![NSMutableArray 的声明](img/00047.jpg)

*(注：源码中关于实现说明的部分存在重复/碎片化的文本；我已根据提供的代码块清理了逻辑流。）*




Objective-C 程序员经常调用访问器方法（accessor methods）。Apple 决定为调用访问器方法创建一个快捷方式。这个快捷方式让这两行代码变得完全相同：

```
p = [x fido];
```

```
p = x.fido;
```

它还让这两行代码变得完全相同：

```
[x setFido:3];
```

```
x.fido = 3;
```

这种使用点号（.）而不是方括号的形式被称为点表示法（dot notation）。

我避免使用点表示。我觉得它掩盖了正在发送消息（message）的事实，而且与我们在系统中发送其他任何消息的方式不一致。欢迎使用点表示法，但在本书的其他地方都不会出现。

## Properties（属性）

注意，我们在 `Person` 类中的大部分代码都用于编写访问器方法。Apple 创建了一种方便的方法来简化访问器方法的编写，称为 `properties`（属性）。通过属性，你可以在一行内同时声明 setter 和 getter 方法。

在 `Person.h` 中，用 `@property` 结构替换 setter 和 getter 方法的声明：

```objectivec
#import <Foundation/Foundation.h>

@interface Person : NSObject
{
    float heightInMeters;
    int weightInKilos;
}

@property float heightInMeters;
@property int weightInKilos;

- (float)bodyMassIndex;
@end
```

通过这次编辑，你并没有改变这个类。你只是使用了一种更简洁的语法。

现在，看看 `Person.m` 文件。它充满了简单且可预测的访问器方法。在你的访问器没有特殊功能的情况下，你只需要告诉编译器根据每个 `@property` 声明合成默认的访问器方法。删除访问器并用调用 `@synthesize` 来替换：

```objectivec
#import "Person.h"

@implementation Person
@synthesize heightInMeters, weightInKilos;
- (float)bodyMassIndex
{
    return weightInKilos / (heightInMeters * heightInMeters);
}
@end
```

编译并运行程序。一切运行起来应该和之前一样，但代码要简单得多且更容易维护。

## self

在任何方法内部，你都可以访问隐式局部变量 `self`。`self` 是指向正在运行方法的对象的指针。它用于对象向自己发送消息的场景。例如，许多 Objective-C 程序员对访问器方法非常“虔诚；除了使用访问器方法外，他们永远不会读取或写入实例变量。更新你的 `bodyMassIndex` 方法来取悦这些纯主义者：

```objectivec
- (float)bodyMassIndex
{
    float h = [self heightInMeters];
    return [self weightInKilos] / (h * h);
}
```

在这里，`Person` 的实例向自己发送了两个消息 `heightInMeters` 和 `weightInKilos`，以获取其实例变量的值。

你也可以将 `self` 作为参数传递，让其他对象知道当前对象在哪里。例如，你的 `Person` 类可能有一个方法 `addYourselfToArray:`，它看起来如下：

```objectivec
- (void)addYourselfToArray:(NSMutableArray *)theArray
{
    [theArray addObject:self];
}
```

在这里，你使用 `self` 告诉数组 `Person` 实例所在的位置。它字面意思就是它的地址。

## Multiple files（多文件）

注意，你的项目现在有两个文件中包含可执行代码：`main.m` 和 `Person.m`。（`Person.h` 是类的声明，但里面没有可执行代码）。当你构建项目时，这些文件会被分别编译，然后链接在一起。在现实项目中，一个项目由数百个 C 和 Objective-C 代码文件组成并不罕见。

你还可以链接代码库。例如，你可能会找到一个非常棒的库来解析来自数字望远镜的数据。如果你的程序需要此功能，你将编译该库并添加到项目中。当 Xcode 构建你的程序时，它会链接该库中定义的所有函数和类。

## Challenge（挑战）

创建一个新的 Foundation 命令行工具名为 `Stocks`。然后创建一个名为 `StockHolding` 的类来表示你购买的股票。它将是 `NSObject` 的子类。对于实例变量，它将有两个名为 `purchaseSharePrice` 和 `currentSharePrice` 的 `float` 以及一个名为 `numberOfShares` 的 `int`。为实例变量创建访问器方法。再创建两个实例方法：

```objectivec
- (float)costInDollars;  // purchaseSharePrice * numberOfShares
- (float)valueInDollars; // currentSharePrice * numberOfShares
```

在 `main()` 中，用三个 `StockHolding` 实例填充数组。然后遍历数组并打印每个实例的值。

图 17.2 一个 StockHolding 对象的数组

![An array of StockHolding objects](img/00049.jpg)

## Inheritance（继承）

当你创建 `Person` 类时，你将其声明为 `NSObject` 的子类。这意味着 `Person` 的每一个实例都将拥有在 `NSObject` 中定义的实例变量和方法，以及在 `Person` 中定义的实例变量和方法。我们说 `Person` 继承了 `NSObject` 的实例变量和方法。在这一节中，我们将深入探讨一下继承。

打开项目并创建一个新文件：`Employee`，它是 `Person` 的子类。

图 18.1 你认识的一些类的继承图

![Inheritance diagram of some you know](img/0050.jpg)

在 `Employee.h` 中，声明该类：

```objectivec
#import "Person.h"

@interface Employee : Person
{
    int employeeID;
}

@property int employeeID;
@end
```

在 `Employee.m` 中，合成访问器：

```objectivec
#import "Employee.h"

@implementation Employee
@synthesize employeeID;
@end
```

现在你有一个新的 `Employee` 类，它拥有 `Person` 的所有实例变量以及一个新的实例变量 `employeeID`。`Employee` 的实例将响应 `Person` 的所有消息。因为 `Person` 继承自 `NSObject`，`Employee` 也继承了 `NSObject` 的所有实例变量和方法。

图 18.2 BMI 对象图

![Object diagram for BMI](img/0051.jpg)

假设你向一个对象发送消息 `fido`。为了响应此消息，对象使用 `isa` 指针找到它的类并询问：“你有一个名为 `fido` 的实例方法吗？”如果类有一个名为 `fido` 的方法，它就会被执行。如果该类没有 `fido` 方法，它会询问父类：“你有一个名为 `fido` 的实例方法吗？”并沿着链向上寻找名为 `fido` 的方法。当找到该方法或到达链的顶端时，搜索停止。在链的顶端，`NSObject` 说：“不，没有 `fido`。”然后你会收到一条类似“此 `Employee` 实例不响应选择 `fido`”的错误消息。

尝试一下。打开 `main.m` 并向 `Person` 实例发送一个它无法理解的消息：

```objectivec
int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建 Person 的实例
        id person = [[Person alloc] init];
        // 给实例变量赋予有趣的值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"person (%d, %f) 的 BMI 为 %f", (int)[person weightInKilos], [person heightInMeters], bmi);
    }
}
```




```objc
            [person weightInKilos], [person heightInMeters], bmi);

[person count];
     }
return 0;
}
```

编译并运行程序。（忽略编译器的警告，因为这是你故意这么做的。在大多数情况下，如果你看到这个警告，你应该关注它！）你应该能在控制台中看到一个记录的运行时异常：

```
*** Terminating app due to uncaught exception 'NSInvalidArgumentException',
     reason: '-[Person count]: unrecognized selector sent to instance 0x100108de0'
```

在检查异常后，在继续操作之前删除有问题的那行代码。

你已经创建了这个新的 `Employee` 类，但还没有使用它。修改 `main.m` 以使用 `Employee`：

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建一个 Person 实例
        Person *person = [[Employee alloc] init];
        // 给实例变量赋予有趣的值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"person (%d, %f) has a BMI of %f",
              [person weightInKilos], [person heightInMeters], bmi);
    }
    return 0;
}
```

注意你的 `person` 变量仍然声明为指向 `Person` 的指针。认为这会导致问题吗？编译并运行程序，你会发现你的程序仍然运行良好。这是因为员工（employee）是人的一种——它可以做人能做的任何事情。也就是说，在程序期望 `Person` 实例的任何地方我们都可以使用 `Employee` 实例。

然而，现在你将使用一个 `Employee` 特有的方法，因此你必须更改指针变量的：

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建一个 Person 实例
        Employee *person = [[Employee alloc] init];
        // 给实例变量赋予有趣的值
        [person setWeightInKilos:96];
        [person setHeightInMeters:1.8];
        [person setEmployeeID:15];
        // 调用 bodyMassIndex 方法
        float bmi = [person bodyMassIndex];
        NSLog(@"Employee %d has a BMI of %f", [person employeeID], bmi);
    }
    return 0;
}
```

## 覆盖方法 (Overriding methods)

回顾一下，当发送消息时，对该名称方法的搜索从对象的类开始，并沿着继承层次向上进行。找到的第一个实现就是执行的实现。因此，你可以用自定义实现来覆盖继承的方法。例如，假设你决定员工的体质量指数始终为 19。在这种情况下，你可能会重写 `Employee` 中的 `bodyMassIndex` 方法。打开 `Employee.m` 并进行操作：

```objc
#import "Employee.h"
@implementation Employee
@synthesize employeeID;
- (float)bodyMassIndex
{
    return 19.0;
}
@end
```

编译并运行程序，注意你对 `bodyMassIndex` 的新实现是执行的那个——而不是来自 `Person` 的实现。

注意你在 `Employee.m` 中实现了 `bodyMassIndex`，但没有在 `Employee.h` 中声明它。在头文件中声明方法会发布该方法，以便其他类的实例可以调用它。然而，因为 `Employee` 继承自 `Person`，所有人已经知道 `Employee` 实例拥有 `bodyMassIndex` 方法了。没有必要再次发布它。

## super

如果你决定所有员工都自动获得 10% 的折扣会怎样呢？要做到这一点，你使用 `super`：

```objc
#import "Employee.h"
@implementation Employee
@synthesize employeeID;
- (float)bodyMassIndex
{
    float bmi = [super bodyMassIndex];
    return bmi * 0.9;
}
@end
```

## 挑战 (Challenge)

这个挑战基于上一章。创建一个名为 `ForeignHolding` 的 `Employee` 的子类。给 `ForeignHolding` 添加一个额外的实例变量：`conversionRate`，它的类型为 `float`。在 `main()` 中添加几个 `ForeignHolding` 的实例。

## 19 对象实例变量 (Object Instance Variables)

到目前为止，在类中声明的实例变量都是 `int` 或 `float` 等简单类型。实例变量指向其他对象的指针要常见得多。对象变量指向另一个对象并描述两者之间的关系。通常，实例变量分为三类：

- **对象类型属性 (Object-type attributes)**：指向一个类值对象（如 `NSString` 或 `NSNumber`）的指针。例如，员工的姓将是一个 `NSString`。因此，`Employee` 的实例将有一个指向 `NSString` 指针的实例变量。
- **一对一关系 (To-one relationships)**：指向单个复杂对象的指针。例如，一个员工可能有一个配偶。因此，`Employee` 的实例将有一个指向 `Person` 指针的实例变量。
- **一对多关系 (To-many relationships)**：指向集合类实例的指针，例如 `NSMutableArray`。（我们将在第 21 章看到其他集合的例子。）例如，一个员工可能有孩子。在这种情况下，`Employee` 的实例将有一个指向 `NSMutableArray` 指针的实例变量。该 `NSMutableArray` 将持有一个或多个 `Person` 对象的指针。

（注意，在上面的列表中，我提到“一个 `NSString`”。`NSString` 是类类，但“一个 `NSString`”是 `NSString` 实例的缩写。这种用法有点困惑，但非常常见，所以习惯它是好的。）

`Employee` 实例变量的声明如下：

```objc
@interface Employee : Person
{
    int employeeID;
    NSString *lastName;
    Person *spouse;
    NSMutableArray *children;
}
```





*   一个对象可以承担多个角色。例如，员工的配偶很可能也被列为孩子的紧急联系人：

    图 19.2 一个对象，多个角色
    ![一个对象，多个角色](img/00054.jpg)

*   你最终会产生许多不同的对象并占用程序的内存。你需要让正在使用的对象保持存在，但你希望那些必要的对象被释放（将它们的内存归还堆），以便它们的内存可以被重用。重用内存可以使你的程序内存占用尽可能小，这会让你的整个电脑运行起来更加敏捷。在移动设备（如 iPhone）上，如果你的程序内存占用过大，操作系统将杀掉你的程序。

## 对象所有权与 ARC

为了管理这些问题，我们引入了“对象所有权”的概念。当一个对象有一个对象实例变量时，拥有该指针的对象被认为拥有它所指向的对象。

从另一个角度来看，对象知道自己当前有多少个所有者。例如，在上面的图中，`Person` 的实例有三个所有者：`Employee` 对象和两个 `Child` 对象。当一个对象的所有者数量为零时，它认为再也没有人需要它了，并会释放自己。

每个对象的所有者计数由自动引用计数（Automatic Reference Counting）处理。`ARC` 是 Objective-C 的一项最新开发。在 Xcode 4.2 之前，我们手动管理所有权，并花费了大量精力。（关于手动引用计数及其工作原理的更多信息，请参见第 20 章的最后章节。不过，本书中的所有代码都假设你正在使用 `ARC`。）

让我们扩展 `BMITime` 项目来查看所有权在实践中是如何工作的。公司跟踪资产发放给了哪些员工并不是稀常的事。我们将创建一个 `Asset` 类，每个 `Employee` 将拥有一个包含他或她资产的数组。

    图 19.3 员工与资产
    ![员工与资产](img/00055.jpg)

这通常被称为“父子”关系：父对象（`Employee` 的实例）拥有一组子对象（一个包含 `Asset` 对象的 `NSMutableArray`）。

### 创建 Asset 类

创建一个新文件：NSObject 的 Objective-C 子类。将其命名为 `Asset`。打开 `Asset.h` 并声明两个实例变量和两个属性：

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

注意 `label` 属性声明中的 `strong` 修饰符。它表示：“这是一个指向对象的指针，我声称对该对象拥有所有权。”（我们将在第 20 章中讨论该属性属性的其他选项。）

记住，当一个对象没有任何所有者时，它会被销毁。当一个对象正在被释放时，它会收到 `dealloc` 消息。（每个对象都从 `NSObject` 继承 `dealloc` 方法。）你将重写 `dealloc`，以便你可以看到 `Asset` 实例何时被释放。

为了明确是哪一个特定的 `Asset` 实例被释放，你还将实现另一个 `NSObject` 方法 `description`。该方法返回一个字符串，作为该类实例的有用描述。对于 `Asset`，你将让 `description` 返回一个包含实例 `label` 和 `resaleValue` 的字符串。

打开 `Asset.m`。为你的实例变量合成访问器（accessors），然后重写 `description` 和 `dealloc`。

```objc
#import "Asset.h"

@implementation Asset
@synthesize label, resaleValue;
- (NSString *)description
{
    return [NSString stringWithFormat:@"<%@: $%d >",
              [self label], [self resaleValue]];
}
- (void)dealloc
{
    NSLog(@"deallocating %@", self);
} 
@end
```

注意上述代码中格式字符串中的 `%@` 令牌。该令牌会被向相应变量发送 `description` 消息的结果所替换（该变量必须是对象的指针，以便接收此消息）。

尝试构建你目前的内容，看看在输入时是否犯任何错误。你可以使用快捷键 `Command-B` 在不运行程序的情况下构建程序。这对于在不花时间运行程序的情况下测试代码，或者当你知道程序还没准备好运行时非常有用。此外，在做出更改后进行构建是一个好主意，这样如果你引入了语法错误，可以立即发现并修复它。如果你等待，就不会那么确定了。

### 为 Employee 添加一对多关系

为了在 `Employee` 中建立一对多关系（to-many relationship），你需要一个变量来存放集合。在 `Employee.h` 中，添加：

```objc
#import "Person.h"
@class Asset;

@interface Employee : Person
{
    int employeeID;
    NSMutableArray *assets;
}
@property int employeeID;
- (void)addAssets:(Asset *)a;
- (unsigned int)valueOfAssets;
@end
```

注意 `@class Asset` 编译器有一个名为 `Asset` 的类，而不需要完整的定义，这可以加快编译。

现在将注意力转向 `Employee.m`。对于一对多关系，你需要创建一个集合（一个数组）。

```objc
#import "Employee.h"
#import "Asset.h"

@implementation Employee
@synthesize employeeID;
- (void)addAssets:(Asset *)a
{
    if (!assets) {
        assets = [[NSMutableArray alloc] init];
    }
    [assets addObject:a];
}
- (unsigned int)valueOfAssets
{
    unsigned int sum = 0;
    for (Asset *a in assets) {
        sum += [a resaleValue];
    }
    return sum;
}

- (float)bodyMassIndex
{
    float normalBMI = [super bodyMassIndex];
    return normalBMI * 0.9;
}

- (NSString *)description
{
    return [NSString stringWithFormat:@"<Employee %d: $%d in assets>",
              [self employeeID], [self valueOfAssets]];
}

- (void)dealloc
{
    NSLog(@"deallocating %@", self);
} 

@end
```



现在，你需要创建一些资产并将它们分配给员工。编辑 `main.m`：

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"
#import "Asset.h"

int main(int argc, const char * argv[])
{
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
        // 创建 10 个资产
        for (int i = 0; i < 10; i++) {
            // 创建一个资产
            Asset *asset = [[Asset alloc] init];
            // 给它起一个有趣的标签
            NSString *currentLabel = [NSString stringWithFormat:@"Laptop %d", i];
            [asset setLabel:currentLabel];
            [asset setResaleValue:i * 17];
            // 获取 0 到 9 之间的随机数
            NSUInteger randomIndex = random() % [employees count];
            // 找到该员工
            Employee *randomEmployee = [employees objectAtIndex:randomIndex];
            // 将资产分配给该员工
            [randomEmployee addAssetsObject:asset];
        }
        NSLog(@"Employees: %@", employees);
        NSLog(@"放弃一个员工的所有权");
        [employees removeObjectAtIndex:5];
        NSLog(@"放弃数组的所有权");
        employees = nil;
    }
    return 0;
}
```

编译并运行程序。你将看到类似下面的内容：

```
Employees: (
  "<Employee 0: $0 in assets>",
  "<Employee 1: $153 in assets>",
  "<Employee 2: $119 in assets>",
  "<Employee 3: $68 in assets>",
  "<Employee 4: $0 in assets>",
  "<Employee 5: $136 in assets>",
  "<Employee 6: $119 in assets>",
  "<Employee 7: $34 in assets>",
  "<Employee 8: $0 in assets>",
  "<Employee 9: $136 in assets>"
)
Giving up ownership of one employee
deallocating <Employee 5: $136 in assets>
deallocating <Laptop 3: $51 >
deallocating <Laptop 5: $85  >
Giving up ownership of array
deallocating <Employee 0: $0 in assets>
deallocating <Employee 1: $153 in assets>
deallocating <Laptop 9: $153 >
…
deallocating <Employee 9: $136 in assets>
deallocing <Laptop 8: $136 >
```

当员工 `#5` 从数组中移除时，它会被释放（deallocated），因为它没有所有者。。，它的资产也会被释放，因为它们没有所有者。（你必须相信我：被释放的资产的标签（`NSString` 实例）在没有所有者后也会被释放。）

当 `employees` 被置为 `nil` 时，数组不再拥有所有者。因此它被释放，这会引发更大规模的内存清理和释放链反应，突然间，没有任何一个……都消失了。

## 内存泄漏
当我们一起使用 `Asset` 和 `Employee` 类时，如何确保这两种关系是一致的呢？例如，一个 `Asset` 应该知道是哪个 `Employee` 持有它。

在 `Asset.h` 中，添加一个指向 `Employee` 的指针：

```objc
#import <Foundation/Foundation.h>

class Employee;

@interface Asset : NSObject
@property (nonatomic, retain) NSString *label;
@property (nonatomic, assign) int resaleValue;
@property (nonatomic, retain) Employee *employee;
@end
```

在 `Asset.m` 中，扩展 `description` 方法：

```objc
#import "Asset.h"
#import "Employee.h"

@implementation Asset

- (NSString *)description {
    return [NSString stringWithFormat:@"%@: $%d in assets", self.label, self.resaleValue];
}

@end
```

等等，如果我们在 `Asset` 中对 `employee` 指针使用 `retain`，而 `Employee` 对 `assets` 数组使用 `retain`，就会导致循环引用（retain cycle）。为了修复这个问题，我们应该在 `Asset` 中对 `employee` 指针使用 `weak`。

在 `Employee.h` 中：

```objc
#import <Foundation/Foundation.h>

class Asset;

@interface Employee : NSObject
@property (nonatomic, assign) int weightInKilos;
@property (nonatomic, assign) double heightInMeters;
@property (nonatomic, assign) int employeeID;
@property (nonatomic, retain) NSMutableArray *assets;
@end
```

在 `Employee.m` 中，扩展 `addAssetsObject:` 方法：

```objc
#import "Employee.h"
#import "Asset.h"

@implementation Employee

- (instancetype)init {
    self = [super init];
    if (self) {
        _assets = [[NSMutableArray alloc] init];
    }
    return self;
}

- (void)addAssetsObject:(Asset *)asset {
    if (!_assets) {
        _assets = [[NSMutableArray alloc] init];
    }
    [_assets addObject:asset];
    [asset setEmployee:self];
}

- (void)setWeightInKilos:(int)weight { _weightInKilos = weight; }
- (void)setHeightInMeters:(double)height { _heightInMeters = height; }
- (void)setEmployeeID:(int)id { _employeeID = id; }

@end
```

我最喜欢的 Bug 之一：让两个访问器自动调用对方。这会导致无限循环：`addAssetsObject:` 调用 `setHolder:`，后者调用 `addAssetsObject:`，以此……




资产（Asset）拥有员工（Employee），员工拥有资产数组，而资产数组又拥有资产。这种所有权循环创建了一个垃圾孤岛。这些对象本应该被释放以释放内存，但它们并没有被释放。这被称为引用循环（retain cycle）。引用循环是内存泄漏的非常常见来源。

要在你的程序中找到引用循环，可以使用 Apple 的性能分析工具 `Instruments`。当你对程序进行性能分析时，会在程序运行时对其进行监控，以查看代码和系统在后台发生了什么。然而，你的程序运行和退出的速度非常快。为了给你留出性能分析的时间，请在 `main()` 函数的末尾添加一百秒的 `sleep()`：

```objc
     ...
     }
sleep(100);
     return 0;
}
```

在 Xcode 中，选择菜单栏中的 `Product` → `Profile`。`Instruments` 将启动。当出现可能的性能分析工具列表时，选择 `Leaks`：

图 20.2 选择性能分析器
![选择性能分析器](img/00057.jpg)

随着程序的运行，你可以浏览各项状态。在窗口左侧你有两个工具可以选择（图 20.3）。点击 `Allocations` 工具将让你看到堆中已分配的所有内容的条形图：

图 20.3 Allocations 工具
![Allocations 工具](img/00058.jpg)

例如，你可以看到有 10 个 `Asset` 实例仍然存在于你的堆中。

要寻找引用循环，请切换到 `Leaks` 工具并从表格上方菜单栏选择 `Cycles` 视图。选择一个特定的循环来查看其对象图：

图 20.4 Leaks 工具
![Leaks 工具](img/00059.jpg)

## 弱引用 (Weak references)

如何修复引用循环？使用弱引用（weak reference）。弱引用是一个不隐式表示所有权的指针。为了修复我们的引用循环，资产不应该拥有它的持有者。编辑 `Asset.h` 使 `holder` 成为一个弱引用：

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

编译并运行程序。注意，所有对象现在都被正确地释放了。

在父子关系中，防止此类引用循环的通用规则是父对象拥有孩子，但孩子应该拥有父对象。

## 弱引用置零（Zeroing of weak references）

为了看到弱引用的作用，让我们添加另一个数组。如果我们想要一个所有资产的数组——即使是尚未分配给特定员工的资产？我们可以在创建资产时将它们添加到数组中。在 `main.m` 中添加几行代码：

```objc
#import <Foundation/Foundation.h>
#import "Employee.h"
#import "Asset.h"

int main(int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建 Employee 对象数组
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
            // 给它一个标签
            NSString *currentLabel = [NSString stringWithFormat:@"Laptop %d", i];
            [asset setLabel:currentLabel];
            [asset setResaleValue:i * 17];
            // 获取一个 0 到 9 之间的随机数
            NSUInteger randomIndex = random() % [employees count];
            // 找到该员工
            Employee *randomEmployee = [employees objectAtIndex:randomIndex];
            // 将资产分配给员工
            [randomEmployee addAssets:asset];
            [allAssets addObject:asset];
        }
        NSLog(@"Employees: %@", employees);
        NSLog(@"Giving up ownership of one employee");
        [employees removeObjectAtIndex:5];
        NSLog(@"allAssets: %@", allAssets);
        NSLog(@"Giving up ownership of arrays");
        allAssets = nil;
        employees = nil;
    }
    sleep(100);
    return 0;
}
```

在编译和运行程序之前，思考一下你期望输出是什么样子。你会看到 `allAssets` 数组的内容——在 Employee #5 被释放之后。此时，Employee #5 的资产状态将会是什么？这些资产失去了一个所有者（Employee #5），但它们仍然被 `allAssets` 拥有，因此它们不会被释放。

之前由 Employee #5 拥有的资产的 `holder` 又是怎样的呢？当弱引用指向的对象被释放时，指针变量将被置零（或设置为 `nil`）。因此，Employee #5 的资产不会被释放，它们的 `holder` 变量将自动被设置为 `nil`。

现在编译并运行程序并检查你的输出：

```
Employees: (
    "Employee 0: $0 in assets",
    ...
    "Employee 9: $136 in assets"
)
Giving up ownership of one employee
deallocating <Employee 5: $136 in assets>
allAssets: (
    "Laptop 0: $0, assigned to <Employee 3: $68 in assets>",
    "Laptop 1: $17, assigned to <Employee 6: $119 in assets>",
    "Laptop 2: $34, assigned to <Employee 7: $34 in assets>",
    "Laptop 3: $51 unassigned>",
    "Laptop 4: $68, assigned to <Employee 3: $68 in assets>",
    "Laptop 5: $85 unassigned>",
    "Laptop 6: $102, assigned to <Employee 6: $119 in assets>",
    "Laptop 7: $119, assigned to <Employee 2: $119 in assets>",
    "Laptop 8: $136, assigned to <Employee 9: $136 in assets>",
    "Laptop 9: $153, assigned to <Employee 1: $153 in assets>"
)
Giving up ownership of arrays
deallocing <Laptop 3: $51 unassigned>
...
deallocing <Laptop 8: $136 unassigned>
```

## 给好奇的读者：手动引用计数与 ARC

正如在第 19 章开头提到的，在自动引用计数（ARC）引入 Objective-C 之前，我们使用手动引用计数来计数。在手动引用计数中，所有权的变化发生在你向对象发送递减或增加引用计数的消息时。

`[anObject release]; // anObject 失去一个所有者`

`[anObject retain]; // anObject 获得一个所有者`

你主要会在访问器方法中（新值被保留，旧值被释放）以及 `dealloc` 方法中（之前保留的对象被释放）看到这类调用。`Asset` 的 `setHolder:` 方法看起来应该是这样的：

```objc
- (void)setHolder:(Employee *)newEmp
{
    [newEmp retain];
    [holder release];
    holder = newEmp;
}
```

`dealloc` 方法看起来如下：

```objc
- (void)dealloc
{
    [label release];
    [holder release];
    [super dealloc];
}
```

`description` 方法又是怎样的？它创建并返回一个字符串。`Asset` 应该拥有它的所有权吗？这并不合理；资产正在交付它创建的字符串。当你 `autorelease` 一个对象时，你是在将其标记为未来将发送 `release`。在 ARC 之前，`Asset` 的 `description` 方法看起来如下：

```objc
- (NSString *)description
{
```




```objc
NSString *result = [[NSString alloc] initWithFormat:@"<%@: $%d >",
                                               [self label], [self resaleValue]];
[result autorelease];
return result;
}
```

它何时会被发送 `release` 消息？当当前的 autorelease 池被清空时：

```objc
// 创建 autorelease 池
NSAutoreleasePool *arp = [[NSAutoreleasePool alloc] init];
Asset *asset = [[Asset alloc] init];
NSString *d = [asset description];
// d 指向的字符串在 autorelease 池中
[arp drain]; // 字符串被发送 release 消息
```

ARC 会自动使用 autorelease 池，但你必须手动创建并清空该池。在 ARC 出现时，我们还获得了一种创建 autorelease 池的新语法。上面的代码现在看起来像是这样：

```objc
// 创建 autorelease 池
@autoreleasepool {
    Asset *asset = [[Asset alloc] init];
    NSString *d = [asset description];
    // d 指向的字符串在 autorelease 池中
} // 池被清空了
```

### 引用计数规则

有一组所有 Objective-C 程序员都遵循的内存管理约定。如果你使用 ARC，它会在后台为你遵循这些约定。

在这些规则中，我使用“你”来表示“你当前正在处理的某个类的实例”。这是一种很有同理心的形式：你想象你自己就是正在编写的那个对象。因此，“如果你保留（retain）了这个字符串，它将不会被释放”实际上意味着“如果你当前正在处理的类的实例保留了该字符串，它将不会被释放”。

以下是这些规则。（实现细节在括号中。）

*   如果你使用名称以 `alloc` 或 `new` 开头或包含 `copy` 的方法创建对象，那么你就拥有了它的所有权。（也就是说，假设新对象的引用计数为 1 且不在 autorelease 池中）。当你不再需要该对象时，你有责任释放（release）它。这里列了一些传达所有权的常用方法：`alloc`（其后通常会紧跟一个 `init` 方法）、`copy` 和 `mutableCopy`。
*   通过任何其他方式创建的对象都不属于你。（也就是说，假设它的引用计数为 1 已经在 autorelease 池中，因此在 autorelease 池被清空之前，除非被保留（retain），否则注定会被释放。）
*   如果你没有一个对象并想确保它的持续存在，通过向它发送 `retain` 消息来获取所有权。（这会增加引用计数。）
*   当你拥有一个对象并且不再需要它时，向它发送 `release` 或 `autorelease` 消息。（`release` 会立即减少引用计数。`autorelease` 会导致在 autorelease 池被清空时发送 `release` 消息。）
*   只要一个对象至少有一个所有者，它就会继续存在。（当它的引用计数变为零时，它会被接收到 `dealloc` 消息。）

理解内存管理的技巧之一是**局部思考（think locally）**。`Asset` 类不需要知道任何其他同样关心其 `label` 的对象的信息。只要 `Asset` 实例保留了它想要保留的对象，你就不会遇到任何问题。初学这种语言的程序员有时会犯尝试跟踪整个应用程序中对象的错误。不要这样做。如果你遵循这些规则并始终从类的局部角度进行思考，你永远不需要担心应用程序的其他部分对某个对象做了什么。

遵循所有权的思想，现在就很清楚为什么你需要在 `description` 方法中对字符串进行 autorelease 了：员工对象创建了这个字符串，但它不想拥有它。它想把它送出去。

# 21

## 集合类

你已经使用了两个集合类：`NSArray` 及其子类 `NSMutableArray`。正如你所知，数组包含一个指向其他对象的指针集合。指针是有序的，因此你使用索引（整数）来访问集合中的对象。在本章中，我们将深入研究数组，并查看其他集合类：`NSSet`/`NSMutableSet` 以及 `NSDictionary`/`NSMutableDictionary`。

## NSArray/NSMutableArray

当你向数组添加对象时，数组声称拥有该对象的所有权。当你从数组中移除对象时，数组会放弃所有权。打开 BMITime，看看你是如何使用 `employees` 数组的。忽略所有其他内容，你会看到这样的代码：

```objc
// 创建一个 Employee 对象数组
NSMutableArray *employees = [[NSMutableArray alloc] init];
for (int i = 0; i < 10; i++) {
    // 创建 Employee 实例
    Employee *person = [[Employee alloc] init];
    // 将员工放入数组
    [employees addObject:person];
}
[employees removeObject:5];
```

你通常使用 `alloc`/`init` 创建可变数组。例如，你可以这样写：

```objc
NSMutableArray *employees = [NSMutableArray array];
```

注意，`addObject:` 方法将对象添加到末尾。`NSMutableArray` 会根据需要进行增长。

### 不变对象

当你创建一个 `NSArray` 实例时，你将所有对象分配给它。这通常看起来像：

```objc
NSArray *colors = [NSArray array:@"Orange", "Yellow", nil];
```

末尾的 `nil` 是你告诉方法停止的方式。大多数初学者对 `NSArray` 的存在感到惊讶。为什么会有人想要一个不可变的列表呢？原因有两个：

*   你不信任与你合作的人。也就是说，你想让他们看一个数组，但不想让他们改变它。一种更温和的方法是给他们 `NSMutableArray`，但告诉他们它是 `NSArray`。例如，想象以下这个方法：

```objc
// 返回一个包含 30 个奇数的数组
- (NSArray *)odds {
    NSMutableArray *odds = [[NSMutableArray alloc] init];
    int i = 1;
    while ([odds count] < 30) {
        [odds addObject:[NSNumber numberWithInt:i]];
        i += 2;
    }
    return odds;
}
```

任何调用此方法的人都假设它返回一个不可变的 `NSArray`。如果调用者尝试从返回的对象添加或删除项目，编译器将发出严厉的警告——尽管它实际上是一个 `NSMutableArray` 实例。

*   另一个原因是性能：不变对象永远不需要复制。对于可变对象，你可能会创建一个私有副本，以便你知道系统中的其他代码不会在你的脚下更改它。这对于不变对象来说是不必要的。事实上，虽然 `NSMutableArray` 的 `copy` 方法会创建自己的新副本并返回新数组的指针，但 `NSArray` 的 `copy` 方法什么都不做——它只是返回指向自身的指针。

结果是，不变对象在 Objective-C 编程中非常常见。在 Foundation 中，许多类都会创建不可变实例：`NSArray`、`NSString`、`NSAttributedString`、`NSData`、`NSCharacterSet`、`NSDictionary`、`NSSet`、`NSIndexSet` 和 `NSURLRequest`。所有这些类都有可变子类：`NSMutableArray`、`NSMutableString`、`NSMutableAttributedString` 等。`NSDate` 和 `NSNumber` 则是不变的，并且没有可变子类。

### 排序

排序数组有多种方法，但最常见的方法是使用排序描述符数组。`NSMutableArray` 有以下方法：

`- (void)sortUsingDescriptors:(NSArray *)sortDescriptors;`




该参数是一个 `NSSortDescriptor` 对象的数组。排序描述符（sort descriptor）包含了数组中所包含对象的属性名称，以及该属性应该按升序还是降序排序。我们为什么要传递一个排序描述符数组呢？想象一下，你说：“按姓氏升序排序这个医生列表。”如果两个医生的姓氏相同怎么办？你可以指定：“按姓氏升序排序，如果姓氏相同，则按名字升序排序，如果姓和名都相同，则按邮政编码排序。”

图 21.1 按 lastName 排序，然后是 firstName，最后是 zipCode

![按 lastName 排序，然后是 firstName，最后是 zipCode](img/00060.jpg)

排序的属性可以是任何实例变量，可以是对象任何方法的返回值。

让我们回到 BMITime 项目查看实际中的排序。在 `main()` 中，在记录 `employees` 数组之前，按 `valueOfAssets` 对其进行排序。如果两个员工持有价值相同的资产，则按 `employeeID` 对它们排序。编辑 `main.m`：

```objective-c
      }      NSSortDescriptor *voa = [NSSortDescriptor sortDescriptorWithKey:@"valueOfAssets"
                                                           ascending:YES];
      NSSortDescriptor *ei = [NSSortDescriptor sortDescriptorWithKey:@"employeeID"
                                                            ascending:YES];
      [employees sortUsingDescriptors:[NSArray arrayWithObjects:voa, ei, nil]];
      NSLog(@"Employees: %@", employees);
```

编译并运行程序。你应该能看到员工列表顺序正确：

```
Employees: (
  "<Employee 0: $0 in assets>",
  "<Employee 4: $0 in assets>",
  "<Employee 8: $0 in assets>",
  "<Employee 7: $34 in assets>",
  "<Employee 3: $68 in assets>",
  "<Employee 2: $119 in assets>",
  "<Employee 6: $119 in assets>",
  "<Employee 5: $136 in assets>",
  "<Employee 9: $136 in assets>",
  "<Employee 1: $153 in assets>")
```

### 过滤 (Filtering)

有一个名为 `NSPredicate` 的类。谓词（predicate）包含一个可能为真的陈述，例如“`employeeID` 大于 75。” `NSMutableArray` 有一个方便的方法可以丢弃所有不符合谓词的对象：

```objective-c
- (void)filterUsingPredicate:(NSPredicate *)predicate;
```

`NSArray` 有一个方法可以创建一个新数组，其中包含所有符合谓词的对象

```objective-c
- (NSArray *)filteredArrayUsingPredicate:(NSPredicate *)predicate;
```

假设你正准备收回给所有目前持有总价值超过 $70 资产的员工的资产。在 `main.m` 附近添加代码：

```objective-c
          [employees removeObjectAtIndex:5];
          NSLog(@"allAssets: %@", allAssets);
NSPredicate *predicate = [NSPredicate predicateWithFormat:
                                                   @"holder.valueOfAssets > 70"];
          NSArray *toBeReclaimed = [allAssets filteredArrayUsingPredicate:predicate];
          NSLog(@"toBeReclaimed: %@", toBeReclaimed);
          toBeReclaimed = nil;
          NSLog(@"Giving up ownership of arrays");
          allAssets = nil;
          employees = nil;
      }
  return 0;
}
```

编译并运行程序。你应该看到一个资产列表：

```
toBeReclaimed: (
  "<Laptop 1: $17, assigned to <Employee 6: $119>",
  "<Laptop 3: $51, assigned to <Employee 5: $136>",
  "<Laptop 5: $85, assigned to <Employee 5: $136>",
  "<Laptop 6: $102, assigned to <Employee 6: $119>",
  "<Laptop 8: $136, assigned to <Employee 9: $136>",
  "<Laptop 9: $153, assigned to <Employee 1: $153>")
```

用于创建谓词的格式字符串可以非常复杂。如果你进行了大量的过滤操作，请确保阅读 Apple 的 `Predicate Guide`（谓词指南）。

### NSSet/NSMutableSet

`set`（集合）是一个没有顺序概念的集合，特定的对象在集合中只能出现一次。集合主要用于回答“它是否存在？”这个问题。例如，你可能有一组不适当的 URL。在向孩子显示任何页面之前，你想快速检查该 URL 是否在集合中。集合处理此操作极快。员工的资产没有固有的顺序，而且资产不应该在同一个 `assets` 集合中出现两次。修改你的程序，对 `assets` 关系使用 `NSMutableSet` 代替 `NSMutableArray`。

图 21.2 使用 NSMutableSet 处理 assets

![使用 NSMutableSet 处理 assets](img/0061.jpg)

在 `Employee.h` 中，更改变量的声明：

```objective-c
#import "Person.h"
@class Asset;
@interface Employee : Person
{
    int employeeID;
    NSMutableSet *assets;
}
@property int employeeID;
- (void)addAssetsObject:(Asset *)a;
- (unsigned int)valueOfAssets;
@end
```

在 `Employee.m` 中，创建正确类的实例：

```objective-c
- (void)addAssetsObject:(Asset *)a
{
    if (!assets) {
        assets = [[NSMutableSet alloc] init];
    }
    [assets addObject:a];
    [a setHolder:self];
}
```

编译并运行程序。它的功能应该相同。你不能通过索引访问集合中的对象，因为集合没有顺序概念。相反，你所做的只能问“这里有其中之一吗？” `NSSet` 有一个方法：

```objective-c
- (BOOL)containsObject:(id)x;
```

当你向集合发送此消息时，它会遍历它的对象集合，寻找与 `x` 相等的对象。如果找到了，它返回 `YES`；否则返回 `NO`。这引出了一个相当深奥的问题：相等意味着什么？`NSObject` 类定义了一个名为 `isEqual:` 的方法。要检查两个对象是否相等，你使用 `isEqual:` 方法：

```objective-c
if ([myDoctor isEqual:yourTennisPartner]) {
    NSLog(@"my doctor is equal to your tennis partner");
}
```

`NSObject` 的 `isEqual:` 定义如下：

```objective-c
- (BOOL)isEqual:(id)other
{
    return (self == other);
}
```

因此，如果你没有重写 `isEqual:`，代码段等同于：

```objective-c
if (myDoctor == yourTennisPartner) {
    NSLog(@"my doctor is equal to your tennis partner");
}
```

有些类重写了 `isEqual:`。例如，在 `NSString` 中，重写了 `isEqual:` 来比较字符。对于这些类，相等和相同是有区别的。假设我们有两个字符串指针：

```objective-c
NSString *x = ...
NSString *y = ...
```

`x` 和 `y` 如果它们指向完全相同的地址，则是相同的。`x` 和 `y` 如果它们指向的字符串包含相同的字母，则是相等的。因此，相同的对象总是相等的。相同的对象并不总是相同的。这种差异重要吗？是的。例如 `NSMutableArray` 有两个方法：

```objective-c
- (NSUInteger)indexOfObject:(id)anObject;
- (NSUInteger)indexOfObjectIdenticalTo:(id)anObject;
```

第一个方法询问每个对象“`isEqual:anObject`?”第二个方法询问每个对象“`== anObject`?”

### NSDictionary/NSMutableDictionary

如你所知，数组通过数字索引；很容易问“给我第 10 个对象。”字典通过字符串索引；很容易问“给我存储在 `favoriteColor` 键下的对象。”更准确地说，字典是键值对的集合。键通常是字符串，而值可以是任何类型的对象。这些键值对不按特定顺序保持。

让我们创建一个高管字典。键将是高管职位，值将是 `Employee` 的实例。第一个员工将放在 `@"CEO"` 键下；第二个放在 `@"CTO"` 键下。修改你的 `main.m` 创建并填充 `NSMutableDictionary`。然后，打印出高管字典。最后，将字典的指针设置为 `nil`，这样你就可以看到字典被释放了。





```objectivec
// 创建一个 Employee 对象数组
NSMutableArray *employees = [[NSMutableArray alloc] init];

// 创建一个高管字典
NSMutableDictionary *executives = [[NSMutableDictionary alloc] init];
for (int i = 0; i < 10; i++) {
    // 创建 Employee 实例
    Employee *person = [[Employee alloc] init];
    // 给实例变量赋予有趣的值
    [person setWeightInKilos:90 + i];
    [person setHeightInMeters:1.8 - i/10.0];
    [person setEmployeeID:i];
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
…
NSLog(@"allAssets: %@", allAssets);
NSLog(@"executives: %@", executives);
executives = nil;
NSPredicate *predicate = [NSPredicate predicateWithFormat:@"holder.valueOfAssets > 70"];
NSArray *toBeReclaimed = [allAssets filteredArrayUsingPredicate:predicate];
NSLog(@"toBeReclaimed: %@", toBeReclaimed);
toBeReclaimed = nil;
NSLog(@"释放数组的所有权");
allAssets = nil;
employees = nil;
}
return 0;
}
```

编译并运行程序。高管字典应该将其打印出来：

```objectivec
executives = {
    CEO = "<Employee 0: $0 in assets>";
    CTO = "<Employee 1: $153 in assets>";
}
```

图 21.3  NSMutableDictionary 中的两个 Employee 实例

![NSMutableDictionary 中的两个 Employee 实例](img/00062.jpg)

## C 原始类型

本章涵盖的集合只持有对象。如果你想要一个 `float`、`int` 或结构体指针的集合怎么办？你可以将常见的 C 原始类型封装在对象中。有两个类专门为此目的设计的。`NSNumber` 持有 C 数字类型。`NSValue` 可以持有指针和某些类型的 `struct`（结构体）。

例如，如果你想将数字 4 和 5.6 放入数组中，你会使用 `NSNumber`：

```objectivec
NSMutableArray *numList = [[NSMutableArray alloc] init];
[numList addObject:[NSNumber numberWithInt:4]];
[numList addObject:[NSNumber numberWithFloat:5.6]];
```

## 集合与 nil

你不允许向我们介绍过的任何集合类中添加 `nil`。如果你需要将“空无”的概念（`nil`）放入集合中怎么办？有一个叫做 `NSNull` 的类。`NSNull` 只有一个实例，它是一个代表“空无”的对象。这里有一个例子。

```objectivec
NSMutableArray *hotel = [[NSMutableArray alloc] init];
// 一层是大堂
[hotel addObject:lobby];
// 二层是泳池
[hotel addObject:pool];
// 三层尚未建成
[hotel addObject:[NSNull null]];
// 四层是卧室
[hotel addObject:bedrooms];
```

## 挑战

探索 `NSArray`、`NSMutableArray`、`NSDictionary` 和 `NSMutableDictionary` 的参考页面。你每天都会用到这些类。

## 常量

我们花费了很多时间讨论变量，正如其名所示，它们在程序运行过程中会改变值。然而，有些信息是不改变的。我们称这些为常量，Objective-C 程序员定义常量有两种常用的常用方法：`#define` 和全局变量。

在 Xcode 中，创建一个名为 Constants 的新行内工具（Line Tool）。在标准 C 库中，常量使用 `#define` 预处理器指令定义。标准库的数学部分声明在 `math.h` 文件中。那里定义的常量之一是 `M_PI`。在 `main.m` 中使用它：

```objectivec
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // 在字面量中使用，用于任意字符
        NSLog("%f", M_PI);
    }
    return 0;
}
```

当你编译并运行它时，你应该会看到：`π is 3.14159`

要查看定义，在编辑器中 Command-点击 `M_PI`。它将带你跳转到 `math.h` 中的以下行：

```c
#define M_PI 3.1415926535897932384626433832795028
```

## 预处理器指令

编译 C、C++ 或 Objective-C 代码文件分两个阶段完成。首先，预处理器会处理该文件。预处理器的输出然后进入编译器。预处理器指令以 `#` 开头，最流行的三个是 `#include`、`#import` 和 `#define`。

## #include 和 #import

`#include` 和 `#import` 本质上做的是相同的事情：请求预处理器读取一个文件并将其添加到输出中。通常，你包含的是一个声明文件（`.h` 文件），这些声明被编译器用来理解它正在编译的代码。

`#include` 和 `#import` 之间有什么区别？`#import` 确保预处理器只包含文件一次。`#include` 则允许你多次包含同一个文件。C 程序员倾向于使用 `#include`。

当指定要包含的文件名时，可以使用引号或角括号。引号表示文件在项目目录。角括号表示文件在预处理器知道的标准位置中。这里有两个 `#import` 的示例：

```objectivec
// 包含我写的头文件
#import "PetStore.h"

// 包含 LDAP 库
#import <ldap.h>
```

在项目中，以前会在每个文件中包含一组头文件。这会导致文件开头变得杂乱并使编译变慢。为了让更方便且编译更快，大多数 Xcode 项目都有一个预编译并包含的所有文件。在你的 Constants 项目中，这个文件被称为 `Constants-pch`。

那么，`math.h` 中的常量是如何被引入 `main.m` 的？你的 `main.m` 文件有这一行：

```objectivec
#import <Foundation/Foundation.h>
```

`Foundation.h` 文件有这一行：

```objectivec
#include <CoreFoundation/CoreFoundation.h>
```

`CoreFoundation.h` 文件有这一行：

```objectivec
#include <math.h>
```

## #define

`#define` 告诉预处理器，“每当你遇到 A，就将其替换为 B”。再次查看来自 `math.h` 的那行：

```c
#define M_PI 3.1415926535897932384626433832795028
```

在 `#define` 指令中，你只需用空格分隔两个部分（标记和它的替换内容）。

`#define` 实际上可以用来制作类似函数。在 `main.m` 中，打印两个数字中较大的：

```objectivec
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog("%d is larger", MAX(10, 12));
    }
    return 0;
}
```

`MAX` 不是函数；它是一个 `#define`。`MAX` 最基础的 C 版本是：

```c
#define MAX(A,B) ((A) > (B) ? (A) : (B))
```

所以，当编译器看到你刚刚添加的行时，它看起来像这样：

```objectivec
NSLog("%d is larger", ((10) > (12) ? (10) : (12)));
```




让我们向程序中添加一些内容来解释。首先，有一个名为 `NSLocale` 的类，它存储了关于不同地理位置的信息。你可以获取用户当前区域（locale）的实例，然后向它提问。例如，如果你想知道用户所在地区使用的货币是什么，你可以这样询问：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"\u03c0 is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));
        NSLocale *here = [NSLocale currentLocale];
        NSString *currency = [here objectForKey:@"currency"];
        NSLog(@"Money is %@", currency);
    }
    return 0;
}
```

编译并运行它。根据你所在的位置，你应该能看到类似的内容：

`Money is USD`

但是，如果你将键名误写为 `@"Kuruncy"`，你将得不到任何返回。为了防止这个问题，Foundation 框架定义了一个名为 `NSLocaleCurrencyCode` 的全局变量。它写起来并不更简单，但如果你真的写错了，编译器会报错。此外，Xcode 中的代码补全对全局变量有效，但对字符串常量 `@"currency"` 则无效。将你的代码改为使用该常量：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSLog(@"\u03c0 is %f", M_PI);
        NSLog(@"%d is larger", MAX(10, 12));
        NSLocale *here = [NSLocale currentLocale];
        NSString *currency = [here objectForKey:@"NSLocaleCurrencyCode"];
        NSLog(@"Money is %@", currency);
    }
    return 0;
}
```

在编写 `NSLocale` 类时，这个全局变量出现在两个地方。在 `NSLocale.h` 中，该变量的声明大致如下：

```objectivec
extern NSString const *NSLocaleCurrencyCode;
```

`const` 意味着该指针在程序的整个生命周期内不会改变。`extern` 意味着“我保证它存在，但它将在另一个文件中定义”。果然，在 `NSLocale.m` 文件中，有这样的一行：

```objectivec
NSString const *NSLocaleCurrencyCode = @"currency";
```

### enum

你通常需要定义一组常量。例如，假设你正在开发一个有五档的搅拌机：搅拌（Stir）、切碎（Chop）、乳化（Liquefy）、脉冲（Pulse）和碎冰（Ice Crush）。你的 `Blender` 类有一个名为 `setSpeed:` 的方法。如果类型指示只允许这五种速度中的一种，那是最好的。为了做到，你会定义一个枚举：

```objectivec
enum BlenderSpeed {
    BlenderSpeedStir = 1,
    BlenderSpeedChop = 2,
    BlenderSpeedLiquify = 5,
    BlenderSpeedPulse = 9,
    BlenderSpeedIceCrush = 15
};

@interface Blender : NSObject
{
    // speed 必须是五种速度之一
    enum BlenderSpeed speed;
}

// setSpeed: 期望五种速度中的之一
- (void)setSpeed:(enum BlenderSpeed)x;
@end
```

开发者厌倦了输入 `enum BlenderSpeed`，因此他们经常使用 `typedef` 为其创建一个简写形式：

```objectivec
typedef enum  {
    BlenderSpeedStir = 1,
    BlenderSpeedChop = 2,
    BlenderSpeedLiquify = 5,
    BlenderSpeedPulse = 9,
    BlenderSpeedIceCrush = 15
} BlenderSpeed;

@interface Blender : NSObject
{
    // speed 必须是五种速度之一
    BlenderSpeed speed;
}

// setSpeed: 期望五种速度中的之一
- (void)setSpeed:(BlenderSpeed)x;
@end
```

通常你并不在乎这五种速度代表什么数字——只在乎它们彼此是不相同的。你可以省略这些值，编译器会为你生成值：

```objectivec
typedef enum {
    BlenderSpeedStir,
    BlenderSpeedChop,
    BlenderSpeedLiquify,
    BlenderSpeedPulse,
    BlenderSpeedIceCrush
} BlenderSpeed;
```

### #define vs 全局变量

既然你可以使用 `#define` 或全局变量（包括 `enum`）来定义常量，为什么 Objective-C 程序员倾向于使用全局变量呢？在某些情况下，全局变量具有性能优势。例如，如果你始终使用全局变量，可以使用 `==` 代替 `isEqual:` 来比较字符串（且算术运算更快）。此外，当你在调试器中时，全局变量更容易处理。你应该使用全局变量和 `enum` 来定义常量，而不是使用 `#define`。

# 23 使用 NSString 和 NSData 写入文件

Foundation 框架为开发者提供了几种读取文件和写入文件的方法。在本章中，你将尝试其中几种。

## 将 NSString 写入文件

首先，让我们看看如何将 `NSString` 的内容放入文件中。当你将字符串写入文件时，需要指定你正在使用的编码格式。字符串编码描述了每个字符如何被存储为字节数组。`ASCII` 是一种字符串编码，它将字母‘A’定义为存储为 `01000001`。在 `UTF16` 中，字母‘A’存储为 `0000000001000001`。Foundation 框架支持大约 20 种不同的字符串编码。`UTF` 有两种形式：`UTF16`（每个字符使用两个或多个字节）和 `UTF8`（前 128 个字符使用一个字节，其他字符使用两个或更多字节）。对于大多数用途，UTF-8 是一个很好的选择。

创建一个新项目：名为 `Stringz` 的 Foundation 工具。在 `main()` 中，使用 `NSString` 类的方法创建一个字符串并将其写入文件系统：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSMutableString *str = [[NSMutableString alloc] init];
        for (int i = 0; i < 10; i++) {
            [str appendString:@"Aaron is cool!\n"];
        }
        [str writeToFile:@"/tmp/cool.txt"
               atomically:YES
               encoding:NSUTF8StringEncoding
                  error:NULL];
        NSLog(@"done writing /tmp/cool.txt");
    }
    return 0;
}
```

该程序创建一个可以使用任何文本编辑器读取和编辑的文件。`/tmp/cool.txt` 字符串被称为文件路径。文件路径可以是绝对的或相对的：绝对路径以代表根目录的 `/` 开头，而相对路径从程序的工作目录开始。相对路径不以 `/` 开头。在 Objective-C 编程中，你会发现我们几乎使用绝对路径，因为我们通常不知道程序的工作目录在哪里。

## NSError

可以想象，将字符串写入文件时可能会发生各种问题。例如，用户可能对文件所在的目录没有写入权限。或者目录根本不存在。或者磁盘满了。对于这些可能无法完成的情况，方法除了返回成功或失败的布尔值外，还需要一种方式来返回错误的描述。

回想一下第 9 章，当你需要函数返回返回值之外的其他内容时，可以使用引用传递。你向函数（或方法）传递变量的引用，其可以在其中直接存储或操作该值。引用就是该变量的内存地址。

对于错误处理，许多方法通过引用接收 `NSError` 指针。为上面的示例添加错误处理：

```objectivec
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSMutableString *str = [[NSMutableString alloc] init];
        for (int i = 0; i < 10; i++) {
            [str appendString:@"Aaron is cool!\n"];
        }
        // 声明一个 NSError 对象的指针，但不要实例化它。
        // 只有在确实发生错误时，才会创建 NSError 实例。
        NSError *error;
    }
}
```




```objc
NSError *error = nil;
// 通过引用传递 NSError 指针给 NSString 方法
BOOL success = [str writeToFile:@"/tmp/cool.txt"
                          atomically:YES
                              encoding:NSUTF8StringEncoding
                              error:&error];
// 测试返回的 BOOL，如果写入失败则查询 NSError
if (success) {
    NSLog(@"done writing /tmp/cool.txt");
} else {
    NSLog(@"writing /tmp/cool.txt failed: %@", [error localizedDescription]);
}
}
return 0;
}
```

编译并运行它。现在修改代码，为 `write` 方法传递一个不存在的文件路径，例如 `@"/too/darned/bad.txt"`。你应该会得到一个友好的错误信息。

请注意，在这段代码中声明了一个指向 `NSError` 实例的指针，但你并没有创建或实例化一个 `NSError` 对象并赋值给该指针。

为什么呢？你希望在没有错误时避免创建一个不必要的错误对象。如果发生错误，`writeToFile:atomically:encoding:error:` 将负责创建一个新的 `NSError` 实例，然后修改你声明的 `error` 指针以使其指向新的错误对象。然后你就可以通过你的 `error` 指针询问该对象发生了什么问题。

这种对 `NSError` 的条件性创建要求你传递 `error` 的引用（`&error`），因为此时还没有对象可以传递。然而，与你在 第 9 章 中传递基础 C 变量的引用不同，在这里你传递的是一个指针变量的地址。本质上，你传递的是另一个地址的地址（该地址可能会变成一个 `NSError` 对象的地址）。

为了回顾我们在 第 9 章 中关于国际间谍战的类比，你可能会告诉你的间谍：“如果发生任何问题，请写一份完整的报告（体积太大，无法放入钢管中），并把它藏在图书馆的一本书里。我需要知道你把它藏在哪里了，所以请把书的索书号放在钢管里。”也就是说，你正在给间谍一个位置，让她可以在那里存放她创建的错误报告的地址。

以下是 `NSString` 类中 `writeToFile:atomically:encoding:error:` 的声明：

```objc
- (BOOL)writeToFile:(NSString *)path
         atomically:(BOOL)useAuxiliaryFile
             encoding:(NSStringEncoding)enc
             error:(NSError **)error
```

注意这个双星号。当你调用此方法时，你提供的是一个指向 `NSError` 实例的指针的指针。

通过引用传递 `NSError` 的方法总是返回一个指示是否发生错误的值。例如，此方法在发生错误时会返回 `NO`。在返回结果指示发生错误之前，切不要尝试访问 `NSError`；如果 `NSError` 对象实际上不存在，尝试访问它将导致你的程序崩溃。

## 使用 NSString 读取文件

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

`NSData` 对象表示字节缓冲区。例如，如果你从一个 `URL` 获取某些数据，你就会得到一个 `NSData` 实例。你可以请求 `NSData` 将自己写入文件。创建一个名为 `ImageFetch` 的新命令行工具，从网站获取图像并存到 `NSData` 实例中。然后请求 `NSData` 将它的字节缓冲区写入文件：

```objc
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSURL *url = [NSURL URLWithString:@"http://www.google.com/images/logos/ps_logo2.png"];
        NSURLRequest *request = [NSURLRequest requestWithURL:url];
        NSError *error = nil;
        NSData *data = [NSURLConnection sendSynchronousRequest:request
                               returningResponse:NULL
                                               error:&error];
        if (!data) {
            NSLog(@"fetch failed: %@", [error localizedDescription]);
            return 1;
        }
        NSLog(@"The file is %lu bytes", [data length]);
        BOOL written = [data writeToFile:@"tmp/google.png"
                                options:0
                                error:&error];
        if (!written) {
            NSLog(@"write failed: %@", [error localizedDescription]);
            return 1;
        }
        NSLog(@"Success!");
    }
    return 0;
}
```

编译并运行该程序。在“预览”（Preview）中打开生成的图像。

注意 `writeToFile:options:error:` 方法接收一个表示保存过程中使用的选项数字。最常用的选项是 `NSDataWritingAtomic`。假设你已经获取了一张图像，正在用新版本替换它。在写入新图像时，断电了。半写的文件没用的。在半写的文件比没有文件更糟的情况下，你可以让写入变为原子性的。添加此选项：

```objc
NSLog(@"The file is %lu bytes", [data length]);
BOOL written = [data writeToFile:@"tmp/google.png"
                          options:NSDataWritingAtomic
                          error:&error];
if (!written) {
    NSLog(@"write failed: %@", [error localizedDescription]);
    return 1;
}
```

现在，数据将写入一个临时文件，并在写入完成后该文件将被重命名。这样，你要么得到完整的文件，要么什么都没有。

## 从文件读取 NSData

你也可以从文件内容创建 `NSData` 实例。为你的程序添加两行代码：

```objc
#import <Foundation/Foundation.h>
int main (int argc, const char * argv[]) {
    @autoreleasepool {
        NSURL *url = [NSURL URLWithString:@"http://www.google.com/images/logos/ps_logo2.png"];
        NSURLRequest *request = [NSURLRequest requestWithURL:url];
        NSError *error = nil;
        // 这将阻塞直到获取到数据
        NSData *data = [NSURLConnection sendSynchronousRequest:request
                               returningResponse:NULL
                                               error:&error];
        if (!data) {
            NSLog(@"fetch failed: %@", [error localizedDescription]);
            return 1;
        }
        NSLog(@"The file is %lu bytes", [data length]);
        BOOL written = [data writeToFile:@"tmp/google.png"
                              options:NSDataWritingAtomic
                              error:&error];
        if (!written) {
            NSLog(@"write failed: %@", [error localizedDescription]);
            return 1;
        }
        NSLog(@"Success!");
        NSData *readData = [NSData dataWithContentsOfFile:@"tmp/google.png"];
        NSLog(@"The file read from the disk has %lu bytes", [readData length]);
    }
    return 0;
}
```




到目前为止，你的代码一直是老大。它向标准的 Foundation 对象（如 `NSString` 和 `NSArray` 的实例）发送消息，并告诉它们要做什么。到目前为止，你的程序都在几毫秒内运行并退出。

你一直过着一种甜蜜而简单的生活。在现实世界中，应用程序会运行几个小时，你的对象则是是从用户、时钟、网络等涌入的事件流的奴隶。

在真实的应用程序中，需要一个对象来等待鼠标移动、触摸事件、定时器和网络活动等事件。在 Mac OS 和 iOS 上，这个对象是 `NSRunLoop` 的实例。运行循环停在那里等待，当某些事情发生时，它会向另一个对象发送消息。

我们说，当某些事情发生时，运行循环会触发一个回调（callback）。对于 Objective-C 程序员来说，回调有三种表现形式。（由于这些是非常通用的概念，我将使用 `x` 来代表发生的“某个特定事情”。我将在接后的章节中补充细节。）

*   **目标-动作（Target-action）**：在等待开始之前，你说：“当 `x` 发生时，向那个特定对象发送这条特定的消息。”接收消息的对象是目标（target）。消息的选择器（selector）是动作（action）。
*   **辅助对象（Helper objects）**：在等待开始之前，你说：“这里有一个符合你协议的辅助对象。当事情发生时，向它发送消息。”（关于协议的更多信息，请参见第 25 章。）辅助对象通常被称为代理（delegates）或数据源（data sources）。
*   **通知（Notifications）**：有一个名为通知中心的对象。在等待开始之前，你说通知中心：“这个对象正在等待这类通知。当其中一个通知到达时，向该对象发送这条消息。”当 `x` 发生时，一个对象向通知中心发布通知，中心再将其转发给你的对象。

在本章中，你将实现所有类型的回调，并学习在什么情况下应该使用哪种。

## 目标-动作 (Target-action)

定时器（Timers）使用目标-动作机制。你创建一个带有延迟、目标和动作的定时器。在延迟结束后后，定时器会向其目标发送动作消息。

你将创建一个带有运行循环和定时器的程序。每隔两秒，定时器就会向其目标发送动作消息。你将创建一个类，该类的实例将作为目标。

图 24.1 `Logger` 是 `NSTimer` 的目标

![Logger is the target of the NSTimer](img/00063.jpg)

在 Xcode 中，创建一个新项目：一个名为 `Callbacks` 的 Foundation 命令行工具（Command Line Tool）。为了玩玩，首先只需获取一个运行循环并让它运行起来。编辑 `main.m`：

```objc
#import <Foundation/Foundation.h>

int main (int argc, const char * argv[])
{
  @autoreleasepool {
    [[NSRunLoop currentRunLoop] run];
  }
  return 0;
}
```

编译并运行程序。注意 `run` 方法永远不会返回。运行循环处于无限循环中，等待某些事情发生。你需要终止程序。（选择 Product → Stop。）

现在，你将创建一个自定义类来作为定时器的目标。创建一个新文件：一个名为 `Logger` 的派自 `NSObject` 的 Objective-C 类。（记得，要进入类模板，选择 File → New → New File....）在 `Logger.h` 中，声明动作方法：

```objc
#import <Foundation/Foundation.h>
@interface Logger : NSObject
- (void)sayOuch:(NSTimer *)t;
@end
```

注意，动作方法接收一个参数 ——发送动作消息的对象。在这种情况下，它是定时器对象。

在 `Logger.m` 中实现一个简单的 `sayOuch:` 方法：

```objc
#import "Logger.h"
@implementation Logger
- (void)sayOuch:(NSTimer *)t
{
  NSLog(@"Ouch!");
}
@end
```

此时，我们需要简短地转个弯讨论一下选择器（selectors）。记住，当你向一个对象发送消息时，会询问该对象的类是否有一个具有同名的方法。搜索会沿着继承层级向上进行，直到某个类回答“是的，我有同名的方法”为止。

图 24.2 查找具有正确名称的方法

![The search for a method with the right name](img/00064.jpg)

你可以想象，这种搜索必须非常、非常地完成。如果我们使用方法的实际名称（可能很长），方法查找将非常缓慢。为了加快速度，编译器会为它遇到的每个方法名分配一个唯一的数字。在运行时，我们使用该数字而不是方法名。

图 24.3 它的真实工作原理

![How it really works](img/00065.jpg)

这个代表特定方法名称的唯一数字被称为选择器（selector）。要创建一个向我们的 `Logger` 发送 `sayOuch:` 消息的定时器，你必须要求编译器查找它的选择器。这是通过 `@selector` 指令完成的。在 `main.m` 中，创建 `Logger` 的实例并将其设为 `NSTimer` 实例的目标。将动作设置为 `sayOuch:` 的选择器。

```objc
#import <Foundation/Foundation.h>
#import "Logger.h"
int main (int argc, const char * argv[])
{
  @autoreleasepool {
    Logger *logger = [[Logger alloc] init];
    NSTimer *timer = [NSTimer scheduledTimerWithInterval:2.0
                                     target:logger
                                   selector:@selector(sayOuch:)
                                    userInfo:nil
                                     repeats:YES];
    [[NSRunLoop currentRunLoop] run];
  }
  return 0;
}
```

编译并运行程序。（你会得到未使用变量的警告。）你应该每两秒在控制台上看到一次 `Ouch!`。注意冒号是选择器的一部分。

再次查看编译警告。它在说：“嘿，你创建了变量 `timer` 但没有使用它。”在某些情况下，如此处，你需要标记变量为未使用。现在加上它。

```objc
__unused NSTimer *timer = [NSTimer scheduledTimerWithInterval:2.0
                                                            target:logger
                                                           selector:@selector(sayOuch:)
                                                            userInfo:nil
                                                             repeats:YES];
```

再次编译，警告应该消失了。

## 辅助对象

定时器非常简单。它们只只一件事：：触发。因此，目标-动作是一个很好的选择。许多简单的用户界面控件（如按钮和滑块）也使用目标-动作机制。那么更复杂的情况呢？

在第 23 章中，你使用 `NSURLConnection` 方法从服务器获取数据。它运行良好，但该方法有两个问题：

*   它在等待所有数据到达时阻塞主线程。如果你在真实的应用程序中使用此方法，在获取数据期间用户界面将变得无响应。
*   如果服务器要求用户名和密码，它没有办法进行回调。

由于这些原因，我们通常异步使用 `NSURLConnection`。也就是说，我们启动获取，然后在数据到达、服务器要求凭据或获取失败时等待回调。

你如何获取这些回调？你为 `NSURLConnection` 提供一个辅助对象。当事情发生时，连接向辅助对象发送消息。什么消息？编写 `NSURLConnection` 的人编写了一个协议 —— 一个方法方法列表，辅助对象可以实现。这里是该协议中的一些方法：




```objc
- (NSURLRequest *)connection:(NSURLConnection *)c
             willSendRequest:(NSURLRequest *)req
             redirectResponse:(NSURLResponse *)res;

- (void)connection:(NSURLConnection *)sender
  didReceiveAuthenticationChallenge:(NSAuthenticationChallenge *)ch;

- (void)connection:(NSURLConnection *)sender
  didReceiveData:(NSData *)data;

- (void)connectionDidFinishLoading:(NSURLConnection *)sender;

- (void)connection:(NSURLConnection *)sender didFailWithError:(NSError *)error;

- (NSCachedURLResponse *)connection:(NSURLConnection *)sender
                   willCacheResponse:(NSCachedURLResponse *)cachedResponse;
```

如你所见，`NSURLConnection` 的功能比 `NSTimer` 要丰富得多。现在，你将创建一个实现了这些方法部分或全部的对象，然后将该对象作为它的辅助对象引入 `NSURLConnection`。特别是，`NSURLConnection` 有一个名为 `delegate` 的指针。

图 24.4 Logger 是 NSURLConnection 的代理

![Logger 是 NSURLConnection 的代理](img/00066.jpg)

在 `main()` 中，创建一个 `NSURLConnection` 并将 `Logger` 实例设为它的代理：

```objc
#import <Foundation/Foundation.h>
#import "Logger.h"

int main (int argc, const char * argv[])
{
  @autoreleasepool {
    Logger *logger = [[Logger alloc] init];
    NSURL *url = [NSURL URLWithString:
@"http://www.gutenberg.org/cache/epub/205/pg205.txt"];
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
    __unused NSURLConnection *fetchConn
                                    = [[NSURLConnection alloc] initWithRequest:request
                                                                        delegate:logger
                                                                startImmediately:YES];
    __unused NSTimer *timer
                                    = [NSTimer scheduledTimerWithTimeInterval:2.0
                                                                          target:logger
                                                                    selector:@selector(sayOuch:)
                                                                   userInfo:nil
                                                                repeats:YES];
    [[NSRLoop currentRunLoop] run];
  }
  return 0;
}
```

`Logger` 实例需要一个 `NSMutableData` 实例来存储到达的字节。在 `Logger.h` 中添加一个实例变量：

```objc
#import <Foundation/Foundation.h>
@interface Logger : NSObject {
  NSMutableData *incomingData;
}
- (void)sayOuch:(NSTimer *)t;
@end
```

现在在 `Logger.m` 中实现一些代理方法：

```objc
#import "Logger.h"
@implementation Logger

- (void)sayOuch:(NSTimer *)t
{
  NSLog(@"Ouch!");
}
// 每当有一块数据到达时调用
- (void)connection:(NSURLConnection *)connection
  didReceiveData:(NSData *)data
{
  NSLog(@"received %lu", [data length]);
  // 如果不存在，则创建一个可变数据对象
  if (!incomingData) {
    incomingData = [[NSMutableData alloc] init];
  }
  [incomingData appendData:data];
}
// 当最后块数据处理完毕时调用
- (void)connectionDidFinishLoading:(NSURLConnection *)connection
{
  NSLog(@"Got it!");
  NSString *string = [[NSString alloc] initWithData:incomingData
                                           encoding:NSUTFStringEncoding];
  incomingData = nil;
  NSLog(@"string has %lu characters", [string length]);
  // 取消下一行的注释以查看整个文件
  // NSLog(@"The whole string is %@", string);
}
// 如果获取失败调用
- (void)connection:(NSURLConnection *)connection
  didFailWithError:(NSError *)error
{
  NSLog(@"connection failed: %@", error localizedDescription]);
  incomingData = nil;
}
@end
```

注意，你并没有实现协议中的所有方法——只需你关心的那些。构建并运行程序。你应该看到数据以合理的分块从 Web 服务器传。最终，代理会收到获取完成的通知。到目前为止，回调的规则如下：向一个对象发送一个回调时，Apple 使用目标-动作（target-action）机制。向一个对象发送一组回调时，Apple 使用带有协议的辅助对象。（我们将在下一节中详细讨论协议。）这些辅助对象通常被称为 `delegate`（代理）或 `data source`（数据源）。

如果回调需要发送到多个对象怎么办？

## 通知

当用户在 Mac 上更改时区时，程序中的许多对象可能都想知道更改已经发生。它们每一个都可以注册通知中心（notification center）的观察者。当时区更改时，通知 `NSSystemTimeZoneDidChangeNotification` 将发布到中心，中心将将其转发给所有相关的观察者。

在 `main.m` 中，注册 `Logger` 实例以便在区更改时接收通知：

```objc
#import <Foundation/Foundation.h>
#import "Logger.h"

int main (int argc, const char * argv[])
{
  @autoreleasepool {
    Logger *logger = [[Logger alloc] init];
    [[NSNotificationCenter defaultCenter]
                     addObserver:logger
                        selector:@selector(zoneChange:)
                          name:NSSystemTimeZoneDidChangeNotification
                          object:nil];
    NSURL *url = [NSURL URLWithString:
@"http://www.gutenberg.org/cache/epub/205/pg205.txt"];
    NSURLRequest *request = [NSURLRequest requestWithURL:url];
    __unused NSURLConnection *fetchConn
                                    = [[NSURLConnection alloc] initWithRequest:request
                                                                        delegate:logger
                                                                startImmediately:YES];
    __unused NSTimer *timer
                                    = [NSTimer scheduledTimerWithTimeInterval:2.0
                                                                          target:logger
                                                                    selector:@selector(sayOuch:)
                                                                   userInfo:nil
                                                                repeats:YES];
    [[NSRLoop currentRunLoop] run];
  }
  return 0;
}
```




```objective-c
[[NSNotificationCenter defaultCenter] removeObserver:self];
}
```

* 对象不拥有它们的代理（delegate）或数据源（data sources）。如果你创建了一个作为代理或数据源的对象，你的对象应该在它的 `dealloc` 方法中“辞职”：

```objective-c
- (void)dealloc
{
    [windowThatBossesMeAround setDelegate:nil];
    [tableViewThatBegsForData setDataSource:nil];
}
```

* 对象不拥有其目标（targets）。如果你创建了一个作为目标的对象，你的对象应该在它的 `dealloc` 方法中将目标指针置零：

```objective-c
- (void)dealloc
{
    [buttonThatKeepsSendingMeMessages setTarget:nil];
}
```

这些问题在当前程序中都不存在，因为你的 `Logger` 对象在程序结束之前不会被释放。（另外，纯属巧合的是，在这个练习中，我使用了两个记录详尽的规则例外：`NSURLConnection` 拥有它的代理，而 `NSTimer` 拥有它的目标。）

# 25 协议 (Protocols)

此时，我需要谈论一个稍微抽象的概念。曾有人说过：“记住‘你是谁’和‘你做什么’的区别是非常重要的。”对象也是如此：对象的类与它在工作系统中的角色是不同的。例如，一个对象可以是 `NSMutableArray` 的实例，但它在应用程序中的角色可能是待运行的打印任务队列。

就像“数组作为打印队列”的例子一样，非常棒的类比它们在任何特定应用程序中可能的角色要通用得多。因此，该类的实例可以用多种不同的方式使用。

我们讨论过如何指定一个类。可以指定一个角色吗？在某种程度上，我们可以使用 `@protocol` 结构来指定一个角色。

例如，在一个 iOS 应用程序中，你经常在 `UITableView` 实例中显示数据。然而，`UITableView` 对象并不包含它所显示的数据；它必须从另一个源获取数据。你必须告诉它：“这里有一个满足你数据源角色的对象。”

图 25.1 UITableView 数据源

![UITableView datasource](img/00067.jpg)

创建 `UITableView` 类的开发者是如何指定 `UITableView` 数据源角色的？他创建了一个协议（protocol）。协议是一个方法声明列表。有些方法是强制要求的（required），有些是可选的（optional）。如果你的对象要履行该角色，它必须实现强制要求的方法，并可以选择实现可选的方法。

`UITableView` 的数据源协议名为 `UITableViewDataSource`，这里是它的定义（注释是我写的）：

```objective-c
// 就像类一样，协议可以继承其他协议。
// 此协议继承自 NSObject 协议
@protocol UITableViewDataSource <NSObject>
// 任何表视图数据源必须实现以下方法
@required
// 表视图有多个节(sections)，每个节可以有若干行(rows)
- (NSInteger)tableView:(UITableView *)tv numberOfRowsInSection:(NSInteger)section;
// 这个索引路径包含两个整数（一个节和一个行号）
// 表视图的 cell 是用户在该节/行中看到的内容
- (UITableViewCell *)tableView:(UITableView *)tv
      cellForRowAtIndexPath:(NSIndexPath *)ip;
// 这些方法由表视图数据源实现（也可以不实现）
@optional
// 如果数据源没有实现此方法，表视图将只有一个节
- (NSInteger)numberOfSectionsInTableView:(UITableView *)tv;
// 行可以被删除和移动
- (BOOL)tableView:(UITableView *)tv canEditRowAtIndexPath:(NSIndexPath *)ip;
- (BOOL)tableView:(UITableView *)tv canMoveRowAtIndexPath:(NSIndexPath *)ip;
- (void)tableView:(UITableView *)tv
  commitEditingStyle:(UITableViewCellEditingStyle)editingStyle
  forRowAtIndexPath:(NSIndexPath *)ip;
- (void)tableView:(UITableView *)tv
  moveRowAtIndexPath:(NSIndexPath *)sourceIndexPath
        toIndexPath:(NSIndexPath *)destinationIndexPath;
// 为了节省墨水纸，我省略了一些可选方法的声明。
@end
```

（与类一样，协议在 Apple 的开发者文档中也有参考页面，你可以搜索并浏览它们以查看协议包含的方法。）

当你创建一个类来履行 `UITableView` 数据源的角色时，你需要在头文件中显式地写道：“此类遵循 `UITableViewDataSource` 协议”。它看起来像这样：

```objective-c
@interface TerrificViewController : UIViewController <UITableViewDataSource>
...
@end
```

也就是说，“`TerrificViewController` 是 `UIViewController` 的子类，并遵循 `UITableViewDataSource` 协议。”

如果你的类遵循多个协议，请在角括号内列出它们：

```objective-c
@interface TerrificViewController : UIViewController
       <UITableViewDataSource, UITableViewDelegate, UITextFieldDelegate>
```

然后，在 `TerrificController.m` 文件中，你需要实现每个协议中的强制要求方法。如果你忘记实现其中一个强制要求的方法，你将收到编译器的严厉警告。

你还将浏览可选方法，并挑选出你想要实现的方法。如果你实现了它们，它们将在适当的时间被自动调用。

最后注一点：在[第 24 章]的 Callbacks 程序中，你将 `Logger` 实例设为了 `NSURLConnection` 对象的代理。但你没有在 `Logger.h` 中声明 `Logger` 遵循某个协议。在编写本文时，`NSURLConnection` 代理还没有正式的协议。如果这种情况发生了变化，我将不会感到意外。（如果在构建 Callbacks 时收到了类似“此对象未遵循 NSURLConnectionDelegate 协议”的警告，说明这种情况发生了。）

# 26 属性列表 (Property Lists)

有时你需要计算机和人类都能读取的文件格式。例如，假设你想在一个文件中保留你的股票组合的描述。当你添加新股票时，如果能够手动编辑该文件将是极好的。但对于你的程序来说，能够读取它可能很有用。面对这个问题，Objective-C 程序员使用了属性列表。

属性列表是以下任何内容的组合：

* `NSArray`
* `NSDictionary`
* `NSString`
* `NSData`
* `NSDate`
* `NSNumber`（整数、浮点数或布尔值）

例如，字典数组就是一个属性列表（或简称“P-list”）。

读取和将属性列表写入文件非常简单。在 Xcode 中，创建一个名为 `stock` 的命令行工具项目并添加以下代码：

```objective-c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[])
{
    @autorepool {
        NSMutableArray *stocks = [[NSMutableArray alloc] init];
        NSMutableDictionary *stock;
        stock = [NSMutableDictionary dictionary];
        [stock setObject:@"AAPL" forKey:@"symbol"];
        [stock setObject:[NSNumber numberWithInt:200] forKey:@"shares"];
        [stocks addObject:stock];
        stock = [NSMutableDictionary dictionary];
        [stock setObject:@"GOOG" forKey:@"symbol"];
        [stock setObject:[NSNumber numberWithInt:160] forKey:@"shares"];
        [stocks addObject:stock];
        [stocks writeToFile:@"/tmp/stocks.plist" atomically:YES];
    }
    return 0;
}
```

（注意我重用了了 `stock` 指针。我用它指向第一个字典，然后又指向第二个。）

图 26.1 字典数组

![An array of dictionaries](img/00068.jpg)

当你运行程序时，你会得到一个 `stocks.plist` 文件。如果你用文本编辑器打开它，它看起来像这样：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC
```





```xml
<!DOCTYPE plist PUBLIC "-////Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
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

不错，对吧？人类可读。XML。一行代码。

如果你发现自己正在手动创建属性列表（property lists），你应该知道 `Xcode` 有一个专门用于属性列表的内置编辑器。

现在加上读取该文件的代码：

```objc
int main(int argc, const char * argv[])
{
    @autoreleasepool {
        NSMutableArray *stocks = [[NSMutableArray alloc] init];
        NSMutableDictionary *stock;
        stock = [NSMutableDictionary dictionary];
        [stock setObject:@"AAPL"
                   forKey:@"symbol"];
        [stock setObject:[NSNumber numberWithInt:200]
                   forKey:@"shares"];
        [stocks addObject:stock];
        stock = [NSMutableDictionary dictionary];
        [stock setObject:@"GOOG"
                   forKey:@"symbol"];
        [stock setObject:[NSNumber numberWithInt:160]
                   forKey:@"shares"];
        [stocks addObject:stock];
        [stocks writeToFile:@"/tmp/stocks.plist"
                  atomically:YES];
        NSArray *stockList = [NSArray arrayWithContentsOfFile:@"/tmp/stocks.plist"];
        for (NSDictionary *d in stockList) {
            NSLog(@"I have %@ shares of %@",
                  [d objectForKey:@"shares"], [d objectForKey:@"symbol"]);
        }
    }
    return 0;
}
```

编译并运行程序。

## 挑战

编写一个工具创建一个包含所有 8 类型的属性列表：数组、字典、字符串、数据、日期、整数、浮点数、布尔值。

# 第四部分

## 事件驱动型应用程序

这就是我们一直追求的目标，也是你阅读这本书的原因——编写 iOS 和 Cocoa 应用程序。在接下来的章节中，你将体验到应用程序开发。你的应用程序将拥有 GUI（图形用户界面），并且它们是事件驱动的。

在命令行程序中，你执行程序，然后它会运行自己的逻辑直到完成。事件驱动型应用程序则不同。它启动后开始一个运行循环来等待事件。当事件发生时，应用程序会立即行动，执行方法、发送消息等。

首先，你将编写一个 iOS 应用程序，然后是一个类似的 Cocoa 应用程序。Cocoa 是 Apple 编写系列框架，你用它在 Mac 上编写应用程序。你已经熟悉了这些框架之一——`Foundation`。

要编写 iOS 应用，你需要使用另一组名为 `Cocoa Touch` 的框架。Cocoa 和 Cocoa Touch 有一些共同的框架，如 `Foundation`。其他的则特定于某个平台。

# 27

## 你的第一个 iOS 应用程序

在本章中，你将创建一个 iOS 应用程序：一个名为 `iTahDoodle` 的简单待办事项列表应用，它将数据存储在属性列表中。完成后，`iTahDoodle` 看起来如下所示。

图 27.1 完整的 iTahDoodle 

![Complete iTahDoodle application](img/00069.jpg)

所有的 iOS 应用程序都是事件驱动的应用程序。运行循环等待事件。等待中的应用程序随后会对用户（如点击按钮）或系统（如低内存警告）生成的事件做出响应。

#### 开始使用 iTahDoodle

在 `Xcode` 中，选择 File → New → New Project....。在 iOS 栏目下（而不是 Mac OS X 栏目），点击 `Application`。在出现的模板选项中，选择 `Empty Application`。

图 27.2 创建一个新的 iOS 应用程序

![Creating a new iOS Application](img/00070.jpg)

`Xcode` 的项目模板是为了让你的工作更轻松。它们包含了可以加速开发的样板代码。然而，在这里我们特意选择了 `Empty Application` 模板，这是你可以获得的最接近空白的模板。在此时允许 `Xcode` 生成过多的样板代码会产生干扰。

在 `Xcode` 中，选择 File → New → New Project....。在 iOS 栏目下（而不是 Mac OS X 栏目），点击 `Application`。在出现的模板选项中，选择 `Empty Application`。

`Xcode` 的项目模板是为了让你的工作更轻松。它们包含了可以加速开发的样板代码。然而，在这里我们特意选择了 `Empty Application` 模板，这是你可以获得的最接近空白的模板。在此时允许 `Xcode` 生成过多的样板代码会产生干扰。

在 `Xcode` 中，选择 File → New → New Project....。在 iOS 栏目下（而不是 Mac OS X 栏目），点击 `Application`。在出现的模板选项中，选择 `Empty Application`。

`Xcode` 的项目模板是为了让你的工作更轻松。它们包含了可以加速开发的样板代码。然而，在这里我们特意选择了 `Empty Application` 模板，这是你可以获得的最接近空白的模板。在此时允许 `Xcode` 生成过多的样板代码会产生干扰。

（注：原文中存在大量重复段落，译文已按要求去重，仅保留一次。）




从实例变量的声明中看出，`iTahDoodle`应用程序将包含至少四个额外的对象。然而，在处理这些对象之前，你将编写一个 C 函数。在 Objective-C 中，我们通常通过方法（methods）而不是函数完成工作。因此，当我们在 Objective-C 应用程序中使用 C 函数时，通常将其称为“辅助”（helper）函数。

`iTahDoodle` 将用户的任务存储为属性列表（property list）——即一个 XML 文件。因此，你需要一种方法在应用程序运行时获取该文件的位置。你将编写一个 C 函数，以 `NSString` 的形式返回该文件路径。

要向你的应用程序添加辅助函数，你首先需要在 `BNRAppDelegate.h` 中声明它。

```objc
#import <UIKit/UIKit.h>

// 声明一个辅助函数，我们将用它来获取
// 磁盘上保存待办事项列表的位置路径
NSString *docPath(void);

@interface BNRAppDelegate : UIResponder <UIApplicationDelegate>
{
    UITableView *taskTable;
    UITextField *taskField;
    UIButton *insertButton;
    NSMutableArray *tasks;
}

- (void)addTask:(id)sender;
@property (strong, nonatomic) UIWindow *window;
@end
```

注意你在类声明上方声明了 `docPath()`。这是因为尽管 `docPath()` 是在 `BNRAppDelegate.h` 文件中定义的，但它并不是 `BNRAppDelegate` 类的一部分。事实上，这个函数可以在 `iTahDoodle` 项目中拥有自己的一对文件。然而，由于 `iTahDoodle` 中只有一个这样的辅助函数，为了保持简单，我们将其放在 app delegate 的类文件中。

现在打开 `BNRAppDelegate.m` 并实现你的辅助函数。同样，由于 `docPath()` 并不是类的一部分，请在 `#import` 之后、`@implementation` 行之前（即类实现开始的地方）实现它。

```objc
#import "BNRAppDelegate.h"

// 获取存储在磁盘上的待办事项数据的路径辅助函数
NSString *docPath()
{
    NSArray *pathList = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES);
    return [[pathList objectAtIndex:0] stringByAppendingPathComponent:@"data.td"];
}

@implementation
```

`docPath()` 函数调用了另一个 C 函数 `NSSearchPathForDirectoriesInDomains()`。该函数搜索匹配特定标准的目录并返回这些目录数组。不用担心这些参数是什么；在你编写的几乎所有 iOS 应用程序中，你将传入完全相同的三个参数，并返回一个恰好包含一个元素的数组。（如果你对它的工作原理感兴趣，你可以在开发者文档的“基础函数参考”（Foundation Functions Reference）中找到 `NSSearchPathForDirectoriesInDomains()`。）

## iTahDoodle 中的对象

现在我们可以回到对象上了。你已经了解构成 `iTahDoodle` 应用程序的五个对象。这里有一个 `BNRAppDelegate` 实例，该对象指向其他四个对象的指针：`UITableView`、`UITextField`、`UIButton` 和 `NSMutableArray` 的实例。

图 27.4 iTahDoodle 的对象图

![iTahDoodle 的对象图](img/00072.jpg)

在我们继续配置和连接这些对象之前，让我们先来了解一些关于对象及其之间关系的理论知识。

## 模型-视图-控制器 (Model-View-Controller)

模型-视图-控制器，或 MVC，是一种设计模式，其核心思想是：你创建的任何类都应该属于三个工作类别之一：模型、视图或控制器。以下是分工的详解：

*   **模型（Models）** 负责存储数据并让其他对象可以使用。模型不了解用户界面，也不了解如何在屏幕上绘制自己；它们的唯一目的是持有和管理数据。`NSString`、`NSDate` 和 `NSArray` 都是传统的模型对象。在 `iTahDoodle` 中，到目前为止你的唯一模型对象是存储任务的 `NSMutableArray`。然而，每个单独的任务将由 `NSString` 实例来描述，这些也是模型对象。
*   **视图（Views）** 是应用程序的视觉元素。视图知道如何在屏幕上绘制自己以及如何响应用户输入。视图不知道它们所显示的实际数据，也不知道数据是如何结构和存储的。`UIView` 及其各种子类（包括 `UIWindow`）是视图对象的示例。在 `iTahDoodle` 中，你的视图对象是 `UITableView`、`UITextView` 和 `UIButton` 的实例。一个简单的规则是：如果你能看到它，它就是视图。
*   **控制器（Controllers）** 执行连接和驱动应用程序不同部分所需的逻辑逻辑。它们处理事件并协调应用程序中的其他对象。控制器是任何应用程序的主力军。虽然 `BNRAppDelegate` 是 `iTahDoodle` 中唯一的控制器，但复杂的应用程序将有许多控制器来协调模型和视图对象。图 27.5 显示了响应用户事件（如点击按钮）时对象之间的控制流。注意，模型和视图之间互不通信；控制器稳稳地坐在中间，接收来自某些对象的消息并分发给其他对象。

不要低估 MVC 模式所代表的职责分工至关重要。大多数 Cocoa 和 Touch API 都是用 MVC 编写的，你自己的代码也应该是。现在，让我们回到我们的控制器——`BNRAppDelegate` 实例。

## 应用程序代理 (The application delegate)

当 iOS 应用程序首次启动时，会有大量的后台设置工作。在这个阶段，会创建一个 `UIApplication` 实例来控制应用程序的状态并作为与操作系统的桥梁。`BNRAppDelegate` 的实例也会被创建并设置为 `UIApplication` 实例的 `delegate`（这解释了“app delegate”名称的由来）。

在应用程序启动期间，它尚未准备好处理工作或输入。当这种情况发生变化时，`UIApplication` 实例会向代理发送 `application:didFinishLaunching:` 消息。这个方法非常重要。你需要将所有在用户交互应用程序之前需要发生或到位的操作放在这里。

在 `iTahDoodle` 中，我们在该方法要做之一是找到属性列表并将其加载到数组中。在 `BNRAppDelegate.m` 中，已经有一个 `application:didFinishLaunching:` 方法的存根。找到它并将括号之间的代码替换为以下内容：

```objc
#pragma mark - Application delegate callbacks

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // 尝试从存储在磁盘上的数组加载现有的待办事项数据集。
    NSArray *plist = [NSArray arrayWithContentsOfFile:docPath()];
    if (plist) {
        // 如果可用数据集，将其拷贝到我们的实例变量。
        tasks = [plist mutableCopy];
    } else {
        // 否则，创建一个空的来开始。
        tasks = [[NSMutableArray alloc] init];
    }
    return YES;
}
```





你是否对代码开头的 `#pragma mark` 感到好奇？Objective-C 程序员经常使用此构造在类内部对方法进行分组。`Xcode` 也能识别它。在编辑器顶部的导航栏上，找到 `BNRAppDelegate.m` 右侧的项。（目前，该项可能显示为 `@implementation AppDelegate`，这取决于你的光标在代码中的位置。）点击此项，`Xcode` 将向你显示该文件中的位置列表。你可以点击列表中的任何位置以跳转到代码的对应位置。注意，你新添加的 `pragma mark` 会出现在此列表中。当一个类中有很多很多方法时，这非常有用。

## 设置视图

在应用程序准备就绪之前，我们还需要需要做的另一件事是设置我们的视图对象。这包括创建它们、配置它们以及将它们放置在屏幕上。听起来很有道理，对吧？用户无法点击不存在或不在屏幕上的按钮。

在 `iTahDoodle` 中，你将在 `application:didFinishLaunchingWithOptions:` 中通过编程的方式来设置视图。还有一种用于设置视图的可视化“拖放”工具，我们将在下一章中使用它。

我应该提醒你，这里是代码开始变得密集的地方。在屏幕上创建和显示视图的详细语法是专门关于 iOS 应用程序编程书籍的主题。在输入代码时，尝试理解其发生的大致过程。你创建每个对象，然后通过设置它的某些属性来配置它。接下来，将配置好的视图对象作为窗口对象的子视图添加进去，最后，将窗口放置在屏幕上。

```objc
#pragma mark - Application delegate callbacks

- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
     // 尝试从存储在磁盘的数组加载现有的待事项数据集。
     NSArray *plist = [NSArray arrayWithContentsOfFile:docPath()];
     if (plist) {
         // 如果可用，将其拷贝到我们的实例变量中。
         tasks = [plist mutableCopy];
     } else {
         // 否则，仅创建一个空的以便我们开始。
         tasks = [[NSMutableArray alloc] init];
     }
     // 创建并配置 UIWindow 实例
     // CGRect 是一个包含起点 (x,y) 和大小 (width,height) 的结构体
     CGRect windowFrame = [[UIScreen mainScreen] bounds];
     UIWindow *theWindow = [[UIWindow alloc] initWithFrame:windowFrame];
     [self setWindow:theWindow];
     // 定义三个 UI 元素的矩形框
     // CGRectMake() 从 (x, y, width, height) 创建一个 CGRect
     CGRect tableFrame = CGRectMake(0, 80, 320, 380);
     CGRect fieldFrame = CGRectMake(20, 40, 200, 31);
     CGRect buttonFrame = CGRectMake(228, 40, 72, 31);
     // 创建并配置表格视图
     taskTable = [[UITableView alloc] initWithFrame:tableFrame
                                             style:UITableViewStylePlain];
     [taskTable setSeparatorStyle:UITableViewCellSeparatorStyleNone];
     // 创建并配置用于输入新任务的文本字段
     taskField = [[UITextField alloc] initWithFrame:fieldFrame];
     [taskField setBorderStyle:UITextBorderStyleRoundedRect];
     [taskField setPlaceholder:@"Type a task, tap Insert"];
     // 创建并配置圆矩形 Insert 按钮
     insertButton = [UIButton buttonWithType:UIButtonTypeRoundedRect];
     [insertButton setFrame:buttonFrame];
     // 按钮使用目标/动作回调进行工作
     // 配置 Insert 按钮的动作以调用此对象的 -addTask: 方法
     [insertButton addTarget:self
                       action:@selector(addTask:)
             forControlEvents:UIControlTouchUpInside];
     // 给按钮设置标题
     [insertButton setTitle:@"Insert"
                forState:UIControlState];
     // 将我们的 UI 元素添加到窗口
     [self window] addSubview:taskTable];
     [self window] addSubview:taskField];
     [self window] addSubview:insertButton];
     // 完成窗口并将其显示在屏幕上
     [self window] setBackgroundColor:[UIColor whiteColor]];
     [self window] makeKeyAndVisible;
     return YES;
}
```

### 在模拟器上运行

现在你已经设置好了视图，我们可以编译应用程序来查看它们的外观。在 `Xcode` 中，找到 Run 按钮附近的 `Scheme` 下拉菜单。选择 `iPhone 5` 作为最新版本的 iOS 模拟器：

图 27.6 Scheme 选择器

编译并运行应用程序。你会收到来自编译器的警告，说你还没有实现 `addTask:`。暂时忽略它；稍后你会实现 `addTask:`。

模拟器允许你在桌面上运行 Cocoa Touch 应用程序。这是一种查看你的程序在设备上运行时应该什么样以及如何运行的快速方便的方法。你可以看到在 `application:didFinishLaunching:` 中设置并布局的视图，但它们现在还不能做任何事情。事实上，点击 Insert 按钮会导致应用程序崩溃，因为按钮的动作方法 `addTask:` 尚未实现。（这就是编译器警告你的原因之一。）

图 27.7 iTahDoodle 对象图

## 连接表格视图

你在屏幕上有了一个表格视图，但它完全不知道应该显示什么。作为一个视图对象，表格视图本身不包含任何实际数据。它需要一个对象作为其数据源。在 `iTahDoodle` 中，表格视图的数据源将是 `BNRAppDelegate` 实例。

在 `BNRAppDelegate.m` 中，更新 `application:didFinishLaunchingWithOptions:` 向表格视图发送消息，使 `BNRAppDelegate` 成为其数据源：

```objc
// 创建并配置表格视图
taskTable = [[UITableView alloc] initWithFrame:tableFrame
                                             style:UITableViewStylePlain];
[taskTable setSeparatorStyle:UITableViewCellSeparatorStyleNone];
// 将此对象设置为数据源
[taskTable setDataSource:self];
// 创建并配置用于输入新任务的文本字段
taskField = [[UITextField alloc] initWithFrame:fieldFrame];
```

为了让表格视图的数据源工作，它必须实现 `UITableViewDataSource` 协议中的方法。首先，更新 `BNRAppDelegate.h` 以声明 `BNRAppDelegate` 遵循该协议：

```objc
@interface BNRAppDelegate : UIResponder
<UIApplicationDelegate, UITableViewDataSource>
{
    UITableView *taskTable;
    UITextField *taskField;
    UIButton *insertButton;
    NSMutableArray *tasks;
}
- (void)addTask:(id)sender;
```

`UITableViewDataSource` 协议有两个 `BNRAppDelegate` 现在必须实现的方法。至少，表格视图的数据源必须准备好告诉表格视图给定分区中有多少行，以及给定行中的单元格应该是什么样的。

相应实现回调：

```objc
#pragma mark - 表格视图管理

- (NSInteger)tableView:(UITableView *)tableView
numberOfRowsInSection:(NSInteger)section
{
   // 因为此表格视图只有一个分区，
   // 它的行数等于我们 tasks 数组中的项数
   return [tasks count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView
       cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
   // 为了提高性能，我们会重新配置内存中已滑出屏幕的单元格
   // 并带有新内容交回，而不是总是创建新单元格。
   // 首先，我们检查是否有可供复用的单元格。
```




```objc
UITableViewCell *c = [taskTable dequeueReusableCellWithIdentifier:@"Cell"];

if (!c) {
    // ...并且在没有可用单元格时才分配一个新的
    c = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault
                                    reuseIdentifier:@"Cell"];
}
// 然后我们根据模型对象（重）配置单元格，
// 在此例中我们的 todoItems 数组
NSString *item = [tasks objectAtIndex:[indexPath row]];
[[c textLabel] setText:item];
//并将配置好的单元格返回给表视图
return c;
}
```

要测试该应用程序，请直接在 `application:didFinishLaunchingWithOptions:` 顶部的数组中添加一些数据。

```objc
- (BOOL)application:(UIApplication *)application
didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    // 尝试从存储在磁盘的数组加载现有的待办事项数据集。
    NSArray *plist = [NSArray arrayWithContentsOfFile:docPath()];
    if (plist) {
        // 如果可用数据集，则将其拷贝到我们的实例变量中。
        tasks = [plist mutableCopy];
    } else {
        // 否则，创建一个空数组开始。
        tasks = [[NSMutableArray alloc] init];
    }
    // tasks 是否为空？
    if ([tasks count] == 0) {
        // 在其中放入一些字符串
        [tasks addObject:@"Walk the dogs"];
        [tasks addObject:@"Feed the hogs"];
        [tasks addObject:@"Chop the logs"];
    }
    // 创建并配置 UIWindow 实例
    CGRect windowFrame = [[UIScreen mainScreen] bounds];
    UIWindow *theWindow = [[UIWindow alloc] initWithFrame:windowFrame];
    [self setWindow:theWindow];
    ...
}
```

图 27.8 iTahDoodle 的完整对象图

![iTahDoodle 的完整对象图](img/00076.jpg)

编译并运行应用程序。表视图应该显示你的测试数据。尽管如此，你仍然无法添加新任务。再次冲锋！

## 添加新任务

当你在 `application:didFinishLaunchingWithOptions:` 中创建 `UIButton` 实例时，你为它提供了一个目标/动作对：

```objc
[insertButton addTarget:self
                 action:@selector(addTask:)
             forControlEvents:UIControlEventTouchUpInside];
```

目标是 `self`，动作是 `addTask:`。因此，插入按钮向 `BNRAppDelegate` 发送 `addTask:` 消息。因此，我们需要在 `BNRAppDelegate.m` 中实现 `addTask:` 方法。

```objc
- (void)addTask:(id)sender
{
    // 获取待办事项
    NSString *t = [taskField text];
    // 如果 taskField 为空，则在此退出
    if ([t isEqualToString:@""]) {
        return;
    }
    // 将其添加到我们的工作数组
    [tasks addObject:t];
    // 刷新表视图以便新项目显示
    [taskTable reloadData];
    // 并清空文本字段
    [taskField setText:@""];
    // 隐藏键盘
    [taskField resignFirstResponder];
}
```

什么是 `UITableViewCell`？它是一个代表 `UITableView` 中单行的视图。什么是 `UITableView`？它是一个显示数据列表的视图。什么是 `dataSource`？它是为 `UITableView` 提供数据的对象。什么是 `delegate`？它是处理来自 `UITableView` 事件的对象。什么是 `dequeueReusableCellWithIdentifier:`？它是一个用于重用已滑出屏幕的单元格的方法。什么是 `identifier`？它是一个用于标识单元格类型的字符串。什么是 `textLabel`？它是一个在 `UITableViewCell` 中显示文本的标签。什么是 `setText:`？它是一个用于设置 `UILabel` 文本的方法。什么是 `indexPath`？它是一个表示项目在 `UITableView` 中位置的对象。什么是 `row`？它是一个返回行索引的属性。什么是 `tasks` ？它是一个包含待办事项的数组。




打开 `BNRDocument.h` 并添加一个方法和两个实例变量：`todoItems` 将是一个可变的字符串数组，而 `itemTableView` 将是一个指向 `NSTableView` 对象的指针，该对象将显示 `todoItems` 中的字符串。此外，声明 `BNRDocument` 遵循 `NSTableViewDataSource` 协议。

```
#import <Cocoa/Cocoa.h>

@interface BNRDocument : NSDocument <NSTableViewDataSource>

{
   NSMutableArray *todoItems;
  IBOutletIBOutlet NSTableView *itemTableView;
}

- (IBAction)createNewItem:(id)sender;

@end
```

注意，没有为“插入”（Insert）按钮设置实例变量。但是，该按钮有一个动作——`createNewItem:` 方法。

在上一章中，按钮动作的目标是应用程序代理类的实例 `BNRAppDelegate`。基于文档的应用程序没有应用程序代理对象，相反，它是围绕 `NSDocument` 的子类构建的。对于 TahDoodle 来说，该类就是 `BNRDocument`。

在基于文档的应用程序中，用户可以同时打开多个文档对象的实例。因此，当 TahDoodle 运行时，你可以有多个 `BNRDocument` 实例（多个待办事项列表）。每个实例将有自己的表格视图、按钮、任务数组和窗口。每个实例将独立于其他实例来响应消息，并且每个实例都将是自己的按钮的目标。

在你输入的声明中，还有两个新术语：`IBOutlet` 和 `IBAction`。这些告诉 Xcode：“这是一个指针（`IBOutlet`）或动作方法（`IBAction`），开发者将使用 Interface Builder（接口生成器）来连接它们，而不是通过代码连接。”

## 预览 Interface Builder

在项目导航器中，找到并选择一个名为 `BNRDocument.xib` 的文件。当你从项目导航器中选择以 `.xib`（XML Interface 生成器文档）结尾的文件时，Interface Builder 会出现在编辑器窗格中，显示一个布局网格。

现在，布局网格上只有一个视图对象——一个窗口对象。它是 `NSWindow` 的实例，稍后我们将向它添加其他视图对象。

现在，在 Xcode 窗口的右上角，点击右侧的“View”（视图）按钮以显示“Utilities”（工具箱）。在 Utilities 的顶部，点击 ![A look at Interface Builder](img/00079.jpg) 按钮显示检查器。

检查器被细分为不同的检查器。在本章中，你将使用属性（attributes）、尺寸（size）和连接（connections）检查器。

图 28.3 属性、尺寸和连接检查器

![Attributes, size, and connections inspectors](img/00080.jpg)

在 Utilities 窗格的底部，检查器下方是库（library），它也被分为多个标签页。选择 ![Attributes, size, and connections inspectors](img/00081.jpg) 按钮显示对象库。此库列出了 Interface Builder 识别的所有不同对象类型列表，你可以在这里获取界面元素，并将它们拖放到窗口对象上。

库的底部是一个搜索字段。输入 `table` 来过滤对象列表。第一项 `Table View`（表格视图）代表 `NSTableView` 类的实例。你可以点击它来查看详情。

## 编辑 BNRDocument.xib

从对象库中拖一个 `NSTableView` 实例到窗口对象上。调整表格的大小以填充窗口的大部分，但在底部为按钮留出空间。

图 28.4 添加一个 NSTableView

![Adding an NSTableView](img/00082.jpg)

注意，当对象的边缘靠近窗口或其他对象的边缘时，它们会自动对齐到指南线（guides）。这些指南线根据 Apple 的《人机交互指南》（HIG）对齐视图对象。这些是任何开发者在为 Mac 设计用户界面时应该遵循的规则。iPhone 和 iPad 也有相应的 HIG。你可以在开发者文档中找到所有的 HIG。

现在，你将在属性检查器中设置表格视图的一些属性。通常情况下，你点击布局网格上的一个对象，检查器就会切换上下文向你显示该对象的属性。获取 `NSTableView` 实例的属性要棘手一些。你拖到窗口上的表格视图对象实际上是一个嵌套对象的集合：一个 `NSScrollView`、一个 `NSTableView` 以及一个或多个 `NSTableColumn` 实例。要获取此集合中的特定对象，请在按住 Control 和 Shift 键的同时点击表格视图。你将看到光标下的对象列表，从那里你可以选择你真正感兴趣的对象。选择 `NSTableView`。

图 28.5 从堆栈中选择视图

![Selecting a view from a stack](img/00083.jpg)

在属性检查器中，将表格视图设置为一列。然后，回到编辑器，选择表格视图的头部，并将单独的一列调整大小以充满整个表格视图的宽度。

图 28.6 调整列宽

![Resizing columns](img/00084.jpg)

你已经很好地调整了视图的大小，但当用户调整应用程序窗口大会发生什么？你可以让表格视图随窗口缩放。实际上，你将让包含表格视图的滚动视图随窗口缩放。在表格视图上 Control-Shift-点击，并从列表中选择 `NSScrollView`。在检查器窗格的顶部，点击 ![Resizing columns](img/00085.jpg) 按钮显示尺寸检查器。找到名为“Autizing”（自动布局）部分。

Autizing 部分包含自动布局掩——它让你配置所选视图在其父视图缩放时如何反应。视图像类一样存在层级结构中。`NSScrollView` 的父视图是 `NSWindow` 的实例。

开启一个 ![Resizing columns](img/00085.jpg) 弹簧（spring）允许所选视图在其父视图扩展时沿指定方向扩展。开启一个支撑（strut）会将所选视图固定在其父视图的指定边缘上。幸运的是，自动布局掩码旁边有一个方便的动画，可以让你预览弹簧和支撑组合对所选视图产生的影响。

在自动布局掩码中设置四个支撑和两个弹簧。这将滚动视图的四边固定在窗口相应的边缘，并允许滚动视图（以及表格视图）在水平和垂直方向扩展。

图 28.7 设置自动布局掩码

![Setting the autosizing mask](img/00086.jpg)

现在离开表格转向按钮。回到对象库。找到并拖一个 `NSButton` 实例到窗口对象上。你可以选择库列出的任何按钮样式；圆角按钮（Rounded Rect Button）是经典的。一旦将按钮拖到窗口上，你可以双击按钮文本并输入来更改标签。将其设置为“Insert”（插入）按钮。

最后，在尺寸检查器中，使用自动布局掩码将按钮固定在窗口的左下角并保持当前大小。

图 28.8 插入按钮的自动布局掩码

![Autosize mask for Insert button](img/00087.jpg)

所以你已经创建了 TahDoodle 需要的两个视图对象：一个 `NSTableView` 和一个 `NSButton`。你还配置了这些对象。你设置了表格的列数并设置了按钮标题。你还确保了它们在窗口缩放时能够相应调整大小和位置。

图 28.9 已配置的 BNRDocument.xib

![BNRDocument.xib with views configured](img/00088.jpg)

当你双击 `NSButton` 并输入标题时，你所做的与上一章中添加这行代码的操作是相同的：

```
   [insertButton setTitle:@"Insert"]
```





```objectivec
forState:UIControlStateNormal];
```

那么，你什么时候该使用 Interface Builder，什么时候该通过代码设置视图呢？在简单的情况下，两种方法都可行。我们本可以使用 XIB 来构建 iTahDoodle 的界面。但总的来说，用户界面越复杂，使用 Interface Builder 就越有意义。

（现在你对 Xcode 有了更多了解，请看看书末尾的抽出的卡片。这张卡片包含了在 Xcode 之间进行导航的键盘快捷键。它们有很多呢！当你继续学习 Xcode 时，请使用这张卡片寻找可以节省你时间和点击次数的快捷键。）

## 创建连接

创建和配置视图并不是你在 Interface Builder 中能做的所有事情。你还可以将这些视图对象连接（或“接线”）到你的应用程序代码中。特别是，你可以设置目标-动作对（target-action pairs）并分配指针。

布局网格左侧是“占位符”（placeholders）和对象的列表。这被称为文档大纲（document outline）。（如果你只看到一堆没有标签的图标，点击 `![建立连接](img/00089.jpg)` 按钮显示展开后的列表。）

图 28.10 最小化和展开的文档大纲

![最小化和展开的文档大纲](img/00090.jpg)

在文档大纲的占位符部分下找到 `File's Owner`。占位符代表一个特定的对象，该对象在运行时才能指定。`File's Owner` 代表将加载此 XIB 作为其用户界面的任何对象。在你的情况下，`File's Owner` 代表 `BNRDocument` 的实例。

现在选择编辑器中的 `Insert` 按钮，并按 Control 键拖动到 `File's Owner`。

图 28.11 建立连接

![建立连接](img/00091.jpg)

当你释放鼠标按钮时，会弹出一个小窗口，显示你可以建立的可用连接。选择 `createNewItem:` 作为按钮触发的动作。

图 28.12 选择动作

![选择动作](img/00092.jpg)

你现在已经配置好了目标-动作对。这等同于 iTahDoodle 中的以下代码。

```objectivec
[insertButton addTarget:self
                 action:@selector(addTask:)
   forControlEvents:UIControlEventTouchUpInside];
```

接下来，连接 `BNRDocument` 的 `itemTableView` 输出口。从 `File's Owner`（代表 `BNRDocument`）按 Control 键拖动到 `NSTableView` 并释放。为此出口选择唯一的选项：`itemTableView`。

图 28.13 建立更多连接

![建立更多连接](img/00093.jpg)

最后，在表格视图上 Control-Shift-点击，并从列表中选择 `NSTableView`。然后从表格视图 Control 键拖动到 `File's Owner`，并在连接中选择 `dataSource`。

图 28.14 连接表格视图的数据源

![连接表格视图的数据源](img/0094.jpg)

所以，你到底做了什么？你分配了指针。`BNRDocument` 类声明了一个指向 `NSTableView` 的指针。你指示 Interface Builder，你希望这个指针指向你拖入窗口的特定 `NSTableView` 实例。同样，表格视图也有自己的几个指针，比如 `dataSource`。你指示 Interface Builder 将表格视图的 `dataSource` 指针指向 `BNRDocument`。这等同于你在 iTahDoodle 中通过代码设置表格视图的数据源：

```objectivec
[taskTable setDataSource:self];
```

当你输入 `IBOutlet` 和 `IBAction` 关键字时，你是在为 Interface Builder 标记这些输出（outlets）和动作（actions），告诉它：“嘿！当我尝试连接指针时，请确保把它放进列表里！”当你编写代码时，Interface Builder 会扫描 `IBOutlet` 和 `IBAction` 关键字，以便它知道你可能想要建立哪些连接。

以下是实际定义：

```
#define Action void
#define IBOutlet
```

从 `#define` 中知道，`IBAction` 在编译器看到它之前会被替换为 `void`，而 `IBOutlet` 会消失。因此，在编译时，所有的 `IBOutlet` 关键字都会被移除（留下的输出）。`IBAction` 关键字被替换为 `void`，因为用户界面的动作预计不会有返回值。

注意，你不需要像创建界面时那样分配基于 XIB 的用户界面元素。它们在 XIB 加载时会自动分配内存。

最后，记住按钮没有指针。这是因为一个对象需要它需要发送消息的对象的实例变量。按钮需要向 `BNRDocument` 发送消息，这就是为什么我们连接了它的动作。然而，`BNRDocument` 不需要向按钮发送消息，所以它不需要指向按钮的指针。

## 回顾 MVC

现在你已经布局了用户界面，让我们来看这个项目的对象图：

图 28.15 TahDoodle 的对象图

![TahDoodle 的对象图](img/095.jpg)

`NSDocument` 是 `BNRDocument` 继承的父类，是一个有趣的家伙。初看之下，它似乎像是一个模型对象。但如果你查询 `NSDocument` 的类引用，你会发现它更像是一个控制器而不是其他任何。`NSDocument` 协调各种与磁盘相关的活动，并直接连接到负责输入的视图。当你创建 `NSDocument` 子类 `BNRDocument` 时，你添加了指向真实对象的指针（一个 `NSMutableArray`）。

## 编辑 BNRDocument.m

现在你已经创建、配置并连接了应用程序的用户界面，是时候回到代码编写了。点击项目导航中的 `BNRDocument.m` 重新打开它，并实现 `createNewItem:`。

```objectivec
#import "BNRDocument.h"

@implementation BNRDocument

#pragma mark - NSDocument Overrides
- (NSString *)windowNibName
{
  return @"BNRDocument";
}

#pragma mark - Actions
- (IBAction)createNewItem:(id)sender
{
  // 如果还没有数组，创建一个来存储新任务
  if (!todoItems) {
      todoItems = [NSMutableArray array];
  }
  [todoItems addObject:@"New Item"];
  // -reloadData 告诉表格视图刷新并询问其数据源
  // （在本例中就是这个 BNRDocument 对象）要显示的数据
  [itemTableView reloadData];
  // -updateChangeCount: 告诉应用程序是否有未保存的更改。NSChangeDone 标记为已保存
  [self updateChangeCount:NSChangeDone];
}

现在实现表格视图数据源方法（由 `NSTableViewDataSource` 协议定义）：

#pragma mark Data Source Methods
- (NSInteger)numberOfRowsInTableView:(NSTableView *)tv
{
  // 此表格视图用于显示 todoItems，
  // 所以表格视图中的条目数量将与数组中的对象数量相同。
  return [todoItems count];
}

- (id)tableView:(NSTableView *)tableView
      objectValueForTableColumn:(NSTableColumn *)tableColumn
                        row:(NSInteger)row
{
  // 从 todoItems 中返回与表格视图想要显示的单元格对应的项
  return [todoItems objectAtIndex:row];
}

- (void)tableView:(NSTableView *)tableView
      setObjectValue:(id)object
      forTableColumn:(NSTableColumn *)tableColumn
                   row:(NSInteger)row
{
  // 当用户在表格视图上更改待办事项时，
  // 更新 todoItems 数组
  [todoItems replaceObjectAtIndex:row withObject:object];
  // 然后标记文档为有未保存的更改。
  [self updateChangeCount:NSChangeDone];
}

@end
```





编译并运行程序。`TahDoodle` 将显示在屏幕上，你可以在其上添加和更改待办事项。然而，目前缺失的一个重大功能是无法保存和重新打开待办列表。为了实现这一功能，你需要重写继承自 `BNRDocument` 超类 `NSDocument` 的以下方法：

```objectivec
- (NSData *)dataOfType:(NSString *)typeName
                  error:(NSError **)outError
{
  // 当文档正在保存时，会调用此方法
  // 我们预期向调用者交付一个封装了我们数据的 NSData 对象
  // 这样就可以将其写入磁盘
  // 如果数组为空，我们现在写入一个空数组
  if (!todoItems) {
      todoItems = [NSMutableArray array];
  }
  // 将 todoItems 数组打包成 NSData 对象
  NSData *data = [NSPropertyListSerialization
                                    dataWithPropertyList:todoItems
                                            format:NSPropertyListXMLFormat_v1_0
                                          options:NSPropertyListMutableContainers
                                               error:outError];
  // 返回我们新打包的 NSData 对象
  return data;
}

- (BOOL)readFromData:(NSData *)data
               ofType:(NSString *)typeName
                error:(NSError **)outError
{
  // 当文档正在加载时，会调用此方法
  // 我们接收一个 NSData 对象，并预期从中提取我们的数据
  // 提取我们的 todoItems
  todoItems = [NSPropertyListSerialization propertyListWithData:data
                                                   options:0
                                            format:NULL
                                               error:outError];
  // 根据上述调用的成功与否返回成功结果
  return (todoItems != nil);
}
```

注意，这是你第一次实现一个接收 `NSError**` 参数的方法。在这种情况下，我们仅仅是返回了由 `propertyListWithData:options:format:error:` 生成的 `NSError`，但根据失败的性质，你也可以创建并返回一个新的 `NSError`。

再次构建编译并运行应用程序。现在你就可以保存和加载任务列表了。

## 挑战

- 添加一个“删除已选项目”按钮。
- 在开发者文档中查找 `NSError` 类引用，并按照章节末尾提到的，在保存和加载时创建返回新的 `NSError` 实例。

# 第五部分 高级 Objective-C

你现在已经拥有足够的 Objective-C 知识来开始 iOS 或 Cocoa 开发。但不要急着离开。接下来的章节将对你作为 Objective-C 程序员第一年将非常有用的技术和概念进行温和讨论。

# 29

在 `NSObject` 类中，有一个名为 `init` 的方法。在对象分配内存后，你向新实例发送 `init` 消息，以便它可以初始化实例变量。因此，`alloc` 为对象创建空间，而 `init` 让对象准备好工作。使用 `init` 的写法如下：

```objectivec
NSMutableArray *things = [[NSMutableArray alloc] init];
```

注意，`init` 是一个返回已初始化对象地址的实例方法。它是 `NSObject` 的初始化器。本章介绍如何编写初始化器。

## init 方法

创建一个新项目：名为 `Appliances` 的 Foundation 命令行工具。在这个程序中，你将两个类：`Appliance` 和 `OwnedAppliance`（`Appliance` 的子类）。`Appliance` 的实例将有一个 `productName` 和 `voltage`。`OwnedAppliance` 的实例还将拥有其所有者的名称。

图 29.1 Appliance 及其子类 OwnedAppliance

创建一个新文件：名为 `Appliance` 的 `NSObject` 子类。在 `Appliance.h` 中，为 `productName` 和 `voltage` 创建实例变量和属性声明：

```objectivec
#import <Foundation/Foundation.h>

@interface Appliance : NSObject {
NSString *productName;
int voltage;

@property (copy) NSString *productName;
@property int voltage;

@end
```
（我们将在第 30 章讨论 `copy` 属性限定。）

在 `Appliance.m` 中，对化属性以为实例变量创建访问器方法：

```objectivec
#import "Appliance.h"

@implementation Appliance
@synthesize productName, voltage;
...
```

你可以这样创建一个 `Appliance` 实例：

```objectivec
Appliance *a = [[Appliance alloc] init];
```

注意，由于 `Appliance` 没有实现 `init` 方法，它将执行在 `NSObject` 中定义的 `init` 方法。当这种情况发生时，所有特定于 `Appliance` 的实例变量都将被清零。因此，`Appliance` 新实例的 `productName` 将为 `nil`，`voltage` 将为 0。

## 基础 init 方法

在某些情况下，为实例变量设置初始值为零可能运行良好。但在其他情况下，你需要你的类实例在诞生时，其实例变量已初始化为非零值。

假设每个 `Appliance` 实例在开始生命时电压应为 120。在 `Appliance.m` 中，通过添加新的 `init` 实现来重写 `NSObject` 的 `init` 方法：

```objectivec
- (id)init
{
  // 调用 NSObject 的 init 方法
  self = [super init];
  // 给 voltage 一个初始值
  voltage = 120;
  // 返回指向该对象的指针
  return self;
}
```





```objc
// Give voltage a starting value
[self setVoltage:120];
}
return self;
}
```

在大多数情况下，并没有理由非要选择其中一种方法而非方法，但这确实是一个很好的争论点。这种论点是这样的：支持直接赋值的人说：“你不能在 `init` 方法中使用访问器方法！访问器假设对象已经准备好工作了，而对象在 `init` 方法完成之前是没准备就绪的。”然后支持访问器方法的人会说：“噢，得了。在现实世界中，这几乎不是问题。我的访问器方法可能在为我处理其他事情。当我设置该变量时，我都会使用访问器方法。”实际上，在大多数情况下，这两种方法都是有效的。

## 带参数的 init 方法

有时，如果没有调用它的方法提供的信息，对象就无法正确初始化。例如，想象一个电器如果没有名称就无法工作（`nil` 是不算数的）。在这种情况下，你需要能够向初始化器传递一个名称以便使用。

你无法通过 `init` 做到这一点，因为现在到将来，`init` 都没有参数。因此，你必须创建一个新的初始化方法。然后，当另一个方法创建 `Appliance` 实例时，它看起来如下：

```objc
Appliance *a = [[Appliance alloc] initWithProductName:@"Toaster"];
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

在 `Appliance.m` 中，找到 `init` 的实现。将方法重改为 `initWithProductName:` 并使用传入的值设置 `productName`。

```objc
- (id)initWithProductName:(NSString *)pn
{
    // 调用 NSObject 的 init 方法
    self = [super init];
    // 是否返回了非 nil 对象？
    if (self) {
        // 设置产品名称
        [self setProductName:pn];
        // 给电压一个初始值
        [self setVoltage:120];
    }
    return self;
}
```

在继续之前，构建项目以确保语法正确。

现在你可以使用给定的名称创建 `Appliance` 实例了。然而，如果你将 `Appliance.h` 和 `Appliance.m` 交给另一个程序员，她可能没有意识到她需要调用 `initWithProductName:`。如果她用最常见的方式创建 `Appliance` 实例怎么办？

```objc
Appliance *a = [[Appliance alloc] init];
```

这并不是不合理的行为。作为 `NSObject` 的子类，`Appliance` 实例被认为可以执行 `NSObject` 实例可以做的任何事情。而 `NSObject` 的实例会响应 `init` 消息。然而，这在这里产生了一个问题，因为上面的代码创建的 `Appliance` 实例的产品名称为 `nil`，电压为 0。而我们之前决定，每个 `Appliance` 实例都需要 120 的电压和一个实际名称才能正常工作。你该如何防止这种情况的发生呢？

解决方案很简单。在 `Appliance.m` 中，添加一个 `init` 方法，使用默认名称调用 `initWithProductName:`。

```objc
- (id)init
{
    return [self initWithProductName:@"Unknown"];
}
```

注意，这个新重写的 `init` 并没有做什么——它只是调用了 `initWithProductName:` 方法，该方法完成了大部分工作。

为了测试你的两个初始化器，你需要一个 `description` 方法。在 `Appliance.m` 中实现 `description`：

```objc
- (NSString *)description
{
    return [NSString stringWithFormat:@"<%@: %d volts>", productName, voltage];
}
```

现在，在 `main.m` 中，运行一下这个类：

```objc
#import <Foundation/Foundation.h>
#import "Appliance.h"

int main (int argc, const char * argv[])
{
    @autoreleasepool {
        Appliance *a = [[Appliance alloc] init];
        NSLog(@"a is %@", a);
        [a setProductName:@"Washing Machine"];
        [a setVoltage:120];
        NSLog(@"a is %@", a);
    }
    return 0;
}
```




注意图 29.3 显示每个类都有一个指定的初始化器。该初始化器是该类的指定初始化器。`init` 是 `NSObject` 的指定初始化器，`initWithProductName:` 是 `Appliance` 的指定初始化器，而 `initWithProductName:firstOwnerName:` 是 `OwnedAppliance` 的指定初始化器。一个类只有一个指定初始化方法。如果类有其他初始化器，那么这些初始化器的实现必须调用（直接或间接地）指定初始化器。因此，指定初始化器起到漏斗的作用。

当你创建一个指定初始化器名称与其父类指定初始化器不同的类时（正如你在 `Appliance` 和 `OwnedAppliance` 中做的那样），你有责任在头文件中对其进行说明。在 `Appliance.h` 中添加相应的注释：

```objc
#import <Foundation/Foundation.h>

@interface Appliance : NSObject {
    NSString *productName;
    int voltage;
}

@property (copy) NSString *productName;
@property int voltage;

// 指定初始化器
- (id)initWithProductName:(NSString *)pn;
@end
```

在 `OwnedAppliance.h` 中：

```objc
#import "Appliance.h"

@interface OwnedAppliance : Appliance {
    NSMutableSet *ownerNames;
}

// 指定初始化器
- (id)initWithProductName:(NSString *)pn
        firstOwnerName:(NSString *)n;
- (void)addOwnerNamesObject:(NSString *)n;
- (void)removeOwnerNamesObject:(NSString *)n;
@end
```

因此，Objective-C 程序员在编写初始化器时遵循以下规则：

- 如果一个类有多个初始化器，只有一个执行实际工作。该方法被称为指定初始化器。所有其他初始化器应该直接或间接地调用指定初始化器。
- 如果你的类的指定初始化器名称与父类的指定初始化器不同，你必须重写父类的指定初始化器，以便初始化实例变量。
- 如果你有多个初始化器，请在头文件中明确说明哪一个是指定初始化器。

## 致命方法

偶尔，你可以重写父类的指定初始化器。假设你正在创建一个名为 `WallSafe` 的 `NSObject` 子类，它的指定初始化器是 `initWithCode:`。然而，为 `initWithCode` 设置默认值对于你的应用程序来说是可以接受的。

那么怎么办？`WallSafe` 的实例仍然响应 `init` 消息。有人这样做：

```objc
WallSafe *ws = [[WallSafe alloc]
```

最好的做法是重写指定初始化器，告知开发者他们犯错了以及如何修复：

```objc
- (id)init
{
```

## 属性 属性

在上一节中，你创建了一个名为 `Appliance` 的类，它有两个属性：`productName` 和 `voltage`。让我们看看这些属性是如何工作的。

在 `Appliance.h` 中，你声明了两个实例变量来存储数据：

```objc
{
    NSString *productName;
    int voltage;
}
```

你还声明了访问器方法。你使用了 `@property` 构造：

```objc
@property (copy) NSString *productName;
@property int voltage;
```

在 `Appliance.m` 中，你可以显式地实现访问器方法：

```objc
- (void)setProductName:(NSString *)s
{
    productName = [s copy];
}

- (NSString *)productName
{
    return productName;
}

- (void)setVoltage:(int)x
{
    voltage = x;
}

- (int)voltage
{
    return voltage;
}
```

## 属性属性

现在让我们详细查看你可以用于控制访问器创建方式的不同属性。

### 可变性

属性可以声明为 `readwrite` 或 `readonly`。默认值是 `readwrite`，这意味着会同时创建 setter 和 getter。如果你不需要 setter 方法，可以将属性标记为 `readonly`：

```objc
@property (readonly) int voltage;
```

### 周期修饰符

属性可以声明为 `unsafe_retained`、`strong`、`weak` 或 `copy`。此选项决定了 setter 如何处理内存管理。

`unsafe_retained` 是默认且最简单的：它只是将传入的值赋值给属性。想象这个声明：

```objc
@property (unsafe_retained) int averageScore;
```

这将产生一个几乎等同于以下内容的 setter 方法：

```objc
- (void)setAverageScore:(int)d
{
    averageScore = d;
}
```

在 `Appliance` 中，`voltage` 是一个不安全的未保留的属性。对于持有非对象的属性，你将始终使用 `unsafe_retained`。`strong` 正如你在第 20 节中所学的，它会确保对传入的对象保留一个强引用。它还会放弃对旧对象的所有权（如果它还有其他所有者，则会被销毁）。对于持有对象的属性，你通常会使用 `strong`。

`weak` 并不意味着对指向的对象拥有所有权。它会合成一个 setter，将属性设置为传入的对象。如果该对象被销毁，属性将设置为 `nil`。（请注意，如果指针是 `unsafe_retained` 且它指向的对象被销毁，你将拥有一个“悬空指针”。向悬空指针发送消息通常会导致程序崩溃。）

`copy` 会对传入对象的副本创建一个强引用。但这里有一个细节大多数人都误解了：

#### copy

`copy` 选项会创建对象的副本，然后将指针指向该副本。想象你有一个如下的属性声明和定义：

```objc
@property (copy) NSString *lastName;
@synthesize lastName;
```

生成的 setter 方法看起来大致如下：

```objc
- (void)setLastName:(NSString *)d
{
    lastName = [d copy];
}
```

`copy` 属性的使用适用于具有可变子类的对象类型。例如，`NSString` 有一个名为 `NSMutableString` 的子类。你可以想象 `setLastName:` 方法可能会接收到一个可变字符串：

```objc
// 创建一个可变字符串
NSMutableString *x = [[NSMutableString alloc] initWithString:"Ono"];
// 将其传递给 setLastName:
[myObj setLastName:x];
```




```objc
// 'copy' prevents this from changing the lastName
[x appendString:@" Lennon"];
```

如果传入的对象是不可变的，`copy` 会怎样？为一个不可变对象创建副本似乎是浪费的。`copy` 方法只是调用 `copyWithZone:` 并传递 `nil` 作为参数。例如，在 `NSString` 中，`copyWithZone:` 方法被重写为如下：

```objc
- (id)copyWithZone:(NSZone *)z
{
    return self;
}
```

也就是说，它根本没有创建副本。（注意，`NSZone` 和通用的内存区域已是 Cocoa 编程中几乎被废弃的遗留特征，因此我们在这里不会深入探讨它们。不过，`copyWithZone:` 仍然具有一些用途，并且尚未被完全淘汰。）

对于那些提供可变和不可变两个版本的对象，`copy` 方法返回一个不可变的副本。例如，`NSMutableString` 有一个 `copy` 方法，它返回一个 `NSString` 实例。如果你希望副本是一个可变对象，请使用 `mutableCopy` 方法。

并没有名为 `mutableCopy` 的属性生命周期限定符。如果你希望你的 setter 方法将属性设置为对象的可变副本，你必须自己实现该 setter，以便对传入的对象调用 `mutableCopy` 方法。例如，在 `OwnedAppliance` 中，你可能会创建一个 `setOwnerNames:` 方法：

```objc
- (void)setOwnerNames:(NSSet *)newNames
{
    ownerNames = [newNames mutableCopy];
}
```

## 关于拷贝的更多信息

大多数 Objective-C 类根本没有 `copyWithZone:` 方法。Objective-C 程序员创建的次数比你想象的要少。

奇的是，`copy` 和 `mutableCopy` 方法在 `NSObject` 中的定义如下：

```objc
- (id)copy
{
    return [self copyWithZone:NULL];
}

- (id)mutableCopy
{
    return [self mutableCopyWithZone:NULL];
}
```

因此，如果你有像下面这样的代码：

```objc
Appliance *b = [[Appliance alloc] init];
Appliance *c = [b copy];
```

你将得到如下错误信息：

```
-[Appliance copyWithZone:]: unrecognized selector sent to instance 0x100110130
```

## 关于 atomic 与 nonatomic 的建议

这是一本编程入门书籍，`atomic`/`nonatomic` 选项涉及一个相对高级的主题，即多线程。以下是你需要的：`nonatomic` 选项会让你的 setter 方法运行得稍微快一点。如果你查看 Apple UIKit 的头文件，每个属性都被标记为 `nonatomic`。你也应该将你的属性设为 `nonatomic`。

（我向每个人提供这个建议。然而，在每个群体中，总有人知道恰好多到让人讨厌。那个人会说：“但是当我让我的 App 使用多线程时，我需要 atomic setter 方法提供的保护。”而我应该说：“我不认为你很快就会写多线程代码。即使你写了，我认为 atomic setter 方法也不会起上什么帮助。”但我真正想说的是：“好吧，那么你就让你的 setter 保持 atomic 吧。”因为你不能告诉别人他们还没准备好听的话。）

在 `Appliance.h` 中，将你的访问器设为非原子：

```objc
@property (copy, nonatomic) NSString *productName;
@property (nonatomic) int voltage;
```

遗憾的是，此时属性的默认值是 `atomic`，所以你必须进行此更改。

## 键值编码 (Key-value coding)

键值编码是使用名称来读取和设置属性的能力。键值编码方法定义在 `NSObject` 中，因此每个对象都具有这种能力。

打开 `main.m` 并找到这一行：

```objc
[a setProductName:@"Washing Machine"];
```

重写该行以使用键值编码：

```objc
[a setValue:@"Washing Machine" forKey:@"productName"];
```

在这种情况下，在 `NSObject` 中定义的 `setValue:forKey:` 方法将寻找名为 `setProductName:` 的 setter 方法。如果该对象没有 `setProductName:` 方法，它将直接访问实例变量。

你也可以使用键值编码读取变量的值。在 `main.m` 中添加一行打印产品名称：

```objc
int main (int argc, const char * argv[])
{
    @autorelease {
        Appliance *a = [[Appliance alloc] init];
        NSLog(@"a is %@", a);
        [a setValue:@"Washing Machine" forKey:@"productName"];
        [a setVoltage:240];
        NSLog(@"a is %@", a);
        NSLog(@"the product name is %@", [a valueForKey:@"productName"]);
    }
    return 0;
}
```




创建一个名为 `VowelCounter` 的新 Foundation 命令行工具。然后创建一个新的 Objective-C 分类（category）文件。将分类命名为 `VowelCounting` 并将其成为 `NSString` 的一个分类。

现在打开 `NSString+VowelCounting.h` 并声明你想要添加到 `NSString` 类中的方法：

```objc
#import <Foundation/Foundation.h>

@interface NSString (VowelCounting)

- (int)vowelCount;

@end
```

现在在 `NSString+VowelCount.m` 中实现该方法：

```objc
#import "NSString+VowelCounting.h"

@implementation NSString (VowelCounting)

- (int)vowelCount
{
    NSCharacterSet *charSet =
             [NSCharacterSet characterSetWithCharactersInString:@"aeiouyAEIOUY"];
    NSUInteger count = [self length];
    int sum = 0;
    for (int i = 0; i < count; i++) {
        unichar c = [self characterAtIndex:i];
        if ([charSet characterIsMember:c]) {
            sum++;
        }
    }
    return sum;
}

@end
```

现在在 `main.m` 中使用新方法：

```objc
#import <Foundation/Foundation.h>
#import "NSString+VowelCounting.h"

int main (int argc, const char * argv[])
{
    @autorelease {
        NSString *string = @"Hello, World!";
        NSLog(@"%@ has %d vowels", string, [string vowelCount]);
    }
    return 0;
}
```

编译并运行程序。很不错，对吧？事实证明分类是非常有用的。

需要注意的是，只有这个程序拥有该分类。如果你想在另一个程序中使用该方法，必须将该文件添加到你的项目中，并在构建该程序时编译该分类。

# 32 块（Blocks）

在第 24 章 中，你学习了回调机制、委托（delegation）和通知（notifications）。回调允许其他对象响应事件并调用你对象中的方法。虽然这些方法完全可行，但它们会打乱代码的结构。你为了清晰而希望靠在一起的程序部分，通常并不会靠在一起。

例如，在第 24 章的回调程序中，你添加了代码，在用户时区更改时注册你的对象以接收通知，并在接收到此通知时触发 `zoneChange:`。但现在我正在读你的代码，对这个 `zoneChange:` 方法在被触发时做了什么感到好奇，所以我去寻找该方法的实现。在回调示例中，注册对象接收通知的代码和被触发的方法实现是紧挨着的，但你可以想象，在一个更大、更复杂的应用程序中，这两部分代码可能相隔数百行。

Mac OS X 10.6 和 iOS 4 引入了一种名为“块”（blocks）的新功能。Objective-C block 就像一段 C 函数那样的代码块，但它可以像数据一样被传递。我们很快就会看到它是如何让相关代码保持在一起的。

Blocks 和 block 语法绝对是高级 Objective-C 主题，起初可能会让人困惑。然而，Apple 的 API 越来越多地使用 block。在本章中，我们将逐步几个简单的示例，以便你在实际工作中遇到 block 时做好准备。

如果你有其他编程语言的背景，你可能知道 block 称为匿名函数、闭包（closures）或 lambdas。如果你熟悉函数指针，block 看起来可能很相似，但你很快就会发现，正确使用 block 可以写出比函数指针更优雅的代码。

## 定义 blocks

这是一个 block：

```objc
^{
    NSLog(@"I'm a log statement within a block!");
}
```

它看起来像一个函数，但它使用的是脱字符符号（`^`）而不是函数名。脱字符符号将这段代码标识为 block。同样，像函数一样，block 可以接受参数：

```objc
^(double dividend, double divisor) {
    double quotient = dividend / divisor;
    return quotient;
}
```

这个 block 接受两个 double 作为参数。block 也可以有，但我们稍后会回到这个问题。

这些 block 有名字吗？还没有。这些 block 是值，就像数字 5 是一个值一样。为了通过名字访问 block，我们必须将其赋值给一个 block 变量。

## 使用 blocks

为了看到它是如何工作的，我们将直接进入代码环节。在这次练习中，你将使用一个 block 来移除数组中每个字符串的所有元音字母。

创建一个名为 `VowelMovement` 的新 Foundation 命令行工具。在这个程序中，你将使用一个 block 来遍历字符串数组并转换每一个。首先，你将创建三个数组：一个用于存储原始字符串，一个用于存储“去元音后”的字符串，第三个用于存储从字符串中删除的字符。在 `main.m` 中，替换 `@autoreleasepool` 大括号内部的代码：

```objc
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // 此处待替换
    }
}
```
注，此处原文代码块为：
```objc
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSString *string = @"Hello, World!";
        NSLog(@"%@ has %d vowels", string, [string vowelCount]);
    }
    return 0;
}
```
（注：根据上下文逻辑，此处应为 `main.m` 的基础结构，请参考下方提供的占位符逻辑）

```objc
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        NSString *string = @"Hello, World!";
        NSLog(@"%@ has %d vowels", string, [string vowelCount]);
    }
    return 0;
}
```
（更正：原文提供的 `main.m` 示例代码如下，翻译时需保持逻辑，原文中 `main.m` 的替换是针对 `VowelMovement` 逻辑描述的）

*重新对齐原文翻译：*

现在在 `NSString+VowelCount.m` 中实现该方法：

```objc
#import "NSString+VowelCounting.h"

@implementation NSString (VowelCounting)

- (int)vowelCount
{
    NSCharacterSet *charSet =
             [NSCharacterSet characterSetWithCharactersInString:@"aeiouyAEIOUY"];
    NSUInteger count = [self length];
    int sum = 0;
    for (int i = 0; i < count; i++) {
        unichar c = [self characterAtIndex:i];
        if ([charSet characterIsMember:c]) {
            sum++;
        }
    }
    return sum;
}

@end
```

现在在 `main.m` 中使用新方法：

```objc
#import <Foundation/Foundation.h>
#import "NSString+VowelCounting.h"

int main (int argc, const char * argv[])
{
    @autorelease {
        NSString *string = @"Hello, World!";
        NSLog(@"%@ has %d vowels", string, [string vowelCount]);
    }
    return 0;
}
```

编译并运行程序。很不错，对吧？事实证明分类是非常有用的。

需要注意的是，只有这个程序拥有该分类。如果你想在另一个程序中使用该方法，必须将该文件添加到你的项目中，并在构建该程序时编译该分类。

# 32 块（Blocks）

在第 24 章 中，你学习了回调机制、委托（delegation）和通知（notifications）。回调允许其他对象响应事件并调用你对象中的方法。虽然这些方法完全可行，但它们会打乱代码的结构。你为了清晰而希望靠在一起的程序部分，通常并不会靠在一起。

例如，在第 24 章的回调程序中，你添加了代码，在用户时区更改时注册你的对象以接收通知，并在接收到此通知时触发 `zoneChange:`。但现在我正在读你的代码，对这个 `zoneChange:` 方法在被触发时做了什么感到好奇，所以我去寻找该方法的实现。在回调示例中，注册对象接收通知的代码和被触发的方法实现是紧挨着的，但你可以想象，在一个更大、更复杂的应用程序中，这两部分代码可能相隔数百行。

Mac OS X 10.6 和 iOS 4 引入了一种名为“块”（blocks）的新功能。Objective-C block 就像一段 C 函数那样的代码块，但它可以像数据一样被传递。我们很快就会看到它是如何让相关代码保持在一起的。

Blocks 和 block 语法绝对是高级 Objective-C 主题，起初可能会让人困惑。然而，Apple 的 API 越来越多地使用 block。在本章中，我们将逐步几个简单的示例，以便你在实际工作中遇到 block 时做好准备。

如果你有其他编程语言的背景，你可能知道 block 称为匿名函数、闭包（closures）或 lambdas。如果你熟悉函数指针，block 看起来可能很相似，但你很快就会发现，正确使用 block 可以写出比函数指针更优雅的代码。

## 定义 blocks

这是一个 block：

```objc
^{
    NSLog(@"I'm a log statement within a block!");
}
```

它看起来像一个函数，但它使用的是脱字符符号（`^`）而不是函数名。脱字符符号将这段代码标识为 block。同样，像函数一样，block 可以接受参数：

```objc
^(double dividend, double divisor) {
    double quotient = dividend / divisor;
    return quotient;
}
```

这个 block 接受两个 double 作为参数。block 也可以有返回值，但我们稍后会回到这个问题。

这些 block 有名字吗？还没有。这些 block 是值，就像数字 5 是一个值一样。为了通过名字访问 block，我们必须将其赋值给一个 block 变量。

## 使用 blocks

为了看到它是如何工作的，我们将直接进入代码环节。在这次练习中，你将使用一个 block 来移除数组中每个字符串的所有元音字母。

创建一个名为 `VowelMovement` 的新 Foundation 命令行工具。在这个程序中，你将使用一个 block 来遍历字符串数组并转换每一个。首先，你将创建三个数组：一个用于存储原始字符串，一个用于存储“去元音后”的字符串，第三个用于存储从字符串中删除的字符。在 `main.m` 中，替换 `@autoreleasepool` 大括号内部的代码：

```objc
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // 此处待替换
    }
}
```
（注：原文此处为 `main.m` 结构描述，翻译时保留语境）

### 声明 block

现在是 block 的代码。虽然 block 看起来像函数，但它们可以存储在变量中。与其他变量一样，block 变量先声明后赋值。将以下代码添加到 `main.m` 以声明你的变量。

```objc
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // ... 之前的代码 ...
        
        // 声明 block
        void (^devowelizer)(id, BOOL *);
    }
    return 0;
}
```
（注：根据原文逻辑，此处翻译时需保持代码结构）

让我们拆解这个声明来看看发生了什么。

图 32.1 Block 声明

在声明基本类型变量时，你给出类型然后是名字，例如 `int` `i`。然而，对于 block 变量，名字在声明的中间，位于脱字符之后。block 变量的类型取决于 block 是如何构造的。在这种情况下，`devowelizer` 的类型是“一个接受一个对象、一个整数和一个 `BOOL` 指针且不返回任何值的块”。

### 赋值 block

现在让我们为我们的新变量赋值。对于 block 变量，值始终是大括号内部的一组指令。在 `main.m` 中，添加以下赋值：





```objc
@"a", @"e", @"i", @"o", @"u", nil];

// 声明 block 变量
void (^devowelizer)(id, NSUInteger, BOOL *);

// 将 block 赋值给变量
devowelizer = ^(id string, NSUInteger i, BOOL *stop) {
    NSMutableString *newString = [NSMutableString stringWithString:string];
    // 遍历元音数组，将每个元音出现的次数
    // 替换为空字符串。
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                    withString:@""
                                     options:NSCaseInsensitiveSearch
                                     range:fullRange];
    }
    [newStrings addObject:newString];
}; // block 赋值结束
}
return 0;
}
```

重新编译你的程序以检查输入错误。关于未使用变量的警告将会消失。

现在你已经编写了一个 block——一组指令——并将其赋值给 block 变量 `devowelizer`。注意，block 的赋值以分号结尾，就像任何变量赋值一样。

和处理任何变量一样，你可以同时完成 `devowelizer` 的声明和赋值：

```objc
void (^devowelizer)(id, NSUInteger, BOOL *) = ^(id string, NSUInteger i, BOOL *stop) {
    NSMutableString *newString = [NSMutableString stringWithString:string];
    // 遍历元音数组，将每个元音出现的次数
    // 替换为空字符串。
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                    withString:@""
                                     options:NSCaseInsensitiveSearch
                                     range:fullRange];
    }
    [newStrings addObject:newString];
};
```

和之前一样，在这里我们声明了一个接受三个参数、没有返回值且名为 `devowelizer` 的 block 变量。然后我们编写了一个具体的 block 并将其存储在 `devowelizer` 中。

### 传递 block

由于 `devowelizer` 是一个变量，你可以将其作为参数传递。`NSArray` 有一个名为 `enumerateObjectsUsingBlock:` 的方法。该方法期望将 block 作为其唯一参数。它会为数组中的每个对象执行一次该 block。

在 `main.m` 中，添加以下代码使用 `devowelizer` 调用 `enumerateObjectsUsingBlock:`，然后打印出去元音后的字符串。

```objc
int main (int argc, const char * argv[])
{
    @autoreleasepool {
        // 创建要去元音的字符串数组和一个新字符串容器
        NSArray *oldStrings = [NSArray arrayWithObjects:
                                @"Sauerkraut", @"Raygun", @"Big Nerd Ranch", @"Mississippi", nil];
        NSLog(@"old strings: %@", oldStrings);
        NSMutableArray *newStrings = [NSMutableArray array];
        // 创建一个我们要从字符串中删除的字符列表
        NSArray *vowels = [NSArray arrayWithObjects:
                              @"a", @"e", @"i", @"o", @"u", nil];
        // 声明 block 变量
        void (^devowelizer)(id, NSUInteger, BOOL *);
        // 将 block 赋值给变量
        devowelizer = ^(id string, NSUInteger i, BOOL *stop) {
            NSMutableString *newString = [NSMutableString stringWithString:string];
            // 遍历元音数组，将每个元音出现的次数
            // 替换为空字符串。
            for (NSString *s in vowels) {
                NSRange fullRange = NSMakeRange(0, [newString length]);
                [newString replaceOccurrencesOfString:s
                                            withString:@""
                                             options:NSCaseInsensitiveSearch
                                             range:fullRange];
            }
            [newStrings addObject:newString];
        }; // block 赋值结束
        // 使用我们的 block 遍历数组
        [oldStrings enumerateObjectsUsingBlock:devowelizer];
        NSLog(@"new strings: %@", newStrings); 
    }
    return 0;
}
```

编译并运行你的程序。你会在控制台看到两个数组。第二个数组应该与第一个匹配——只是去掉了所有的元音。

```
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

需要注意的是，`enumerateObjectsUsingBlock:` 不接受任何 block 作为其参数。该方法要求“一个接受一个对象、一个整数和一个 `BOOL` 指针且没有返回值的 block”。这就是为什么我们按照特定的方式构造了赋值给 `devowelizer` 的 block。它的三个参数是专门为遍历数组而设计的。

第一个参数是指向当前对象的指针。注意该指针的类型是 `id`，这样无论数组包含什么种类型的对象都能工作。第二个参数是一个 `NSUInteger` 类型，是当前对象的索引。第三个对象是一个指向 `BOOL` 的指针，默认值为 `NO`。如果我们想在当前迭代后停止，可以将其改为 `YES`。

在 block 赋值的开头添加一个检查：

```objc
devowelizer = ^(id string, NSUInteger i, BOOL *stop){
    NSRange yRange = [string rangeOfString:@"y"
                                options:NSCaseInsensitiveSearch];
    // 我找到 y 吗？
    if (yRange.location != NSNotFound) {
        *stop = YES; // 防止进一步迭代
        return;     // 停止当前迭代
    }
    NSMutableString *newString = [NSMutableString stringWithString:string];
    // 遍历元音数组，将每个元音出现的次数
    // 替换为空字符串。
    for (NSString *s in vowels) {
        NSRange fullRange = NSMakeRange(0, [newString length]);
        [newString replaceOccurrencesOfString:s
                                    withString:@""
                                     options:NSCaseInsensitiveSearch
                                     range:fullRange];
    }
    [newStrings addObject:newString];
}; // block 赋值结束
```

这将检查当前字符串是否包含大写或小写的 ‘y’。如果是，则会将指针设置为 `YES`（阻止执行更多迭代）并停止当前迭代。





你可以使用 `NSNotificationCenter` 方法 `addObserverForName:object:queue:usingBlock:` 并改传递一个 block。通过这种方法，你直接将指令交给 `NSNotificationCenter`，这样你就不需要将回调代码写在其他地方了。任何阅读你代码的人都将在同一块代码中看到这些指令以及发送给 `NSNotificationCenter` 的消息。（在章节末尾的挑战中，你将对你的 Callbacks 程序进行完全相同的更改。）

## typedef

Block 的语法可能会让人困惑，但你可以使用在第 10 章中中学过的 `typedef` 关键字让它变得更容易用。记住 `typedef` 应该放在文件顶部或头文件中，且位于任何方法实现之外。在 `main.m` 中，添加以下行代码：

```objectivec
#import <Foundation/Foundation.h>

typedef void (^ArrayEnumerationBlock)(id, NSUInteger, BOOL *);

int main (int argc, const char * argv[])
{
```

注意，这看起来和 block 变量声明完全相同。然而，在这里我们定义的是一个类型而不是变量，因此我们在插入符号 `^` 旁边放置了合适的类型名称。这允许我们简化相似 block 的声明。与其通过这种方式声明 `devowelizer`：

```objectivec
void (^devowelizer)(id, NSUInteger, BOOL *);
```

你可以将该行替换为以下声明：

```objectivec
ArrayEnumerationBlock devowelizer;
```

这让你的 block 变量声明看起来更加熟悉。注意，block 类型本身只定义了 block 的参数和返回类型；它对该类型 block 内部的指令集没有影响。

## 返回值

最后，当 block 返回一个值时，你可以像调用函数一样调用它的 block 变量。

```objectivec
double (^divBlock)(double,double) = ^(double k, double j) {
    return k/j;
}
```

在这段代码中，你将 `divBlock` 声明为一个返回 `double` 并期望两个 `double` 作为参数的 block 变量。然后你给它分配了一个值，该值包含了返回两个参数结果的指令。

你可以像这样使用这个 block：

```objectivec
double quotient = divBlock(42.0, 12.5);
```

## 内存管理

和原始变量一样，block 是创建并存储在栈（stack）上的。这意味着当创建 block 的函数或方法返回时，block 会随栈帧一起被销毁。然而，有时你的 block 需要存得比那更久。例如，它可以变成对象的实例变量。在这种情况下，你必须将 block 从栈拷贝到堆（heap）。

要将 block 从栈拷贝到堆，你向它发送 `copy` 消息：

```objectivec
ArrayEnumerationBlock iVarDevowelizer = [devowelizer copy];
```

现在，你的 block 在堆上存在了一个副本。它现在是堆上的 block 而不是栈上的 block，而新的 block 变量是指向该 block 的指针。

接收 block 作为参数的方法，例如 `NSArray` 的 `enumerateObjectsUsingBlock:` 或 `NSNotificationCenter` 的 `addObserverForName:object:queue:usingBlock:`，被预期会拷贝传递给它们的 block 以留留它们。通过这样做，它们为这些 block 创建了指针——以及强引用。

所以我们已经看到 block 如何被声明、赋值并像变量一样被传递。我们还看到它们看起来像函数。现在，我们正在像对待对象一样向 block 发送消息。

像对象一样行为的堆上 block 会带来一些内存管理问题：

那些与 block 一起使用的变量怎么办？

block 通常会在其代码内部使用在它外部创建的其他变量（包括原始变量和指向对象的指针）。为了确保这些外部变量在 block 需要它们的使用任何时候都可用，这些变量在进行拷贝时会被 block 捕获（captured）。

对于原始变量，这意味着值被拷贝并存储为 block 内部的局部变量。对于指针，block 本身将对它所引用的任何对象保持强引用。这意味着被 block 引用的任何对象都保证了其存活时间至少与 block 本身一样长。（如果你一直在好奇 block 和函数指针之间的区别，答案就在这里。让我们看看函数指针怎么做！）

举个例子，看看我们的 `VowelMovement` 程序。`devowelizer` block 提到了两个在 block 外部创建的对象：`newStrings`（一个用于存储修改后字符串的数组）和 `string`（当前用于修改拷贝的字符串）。`devowelizer` 将对这两个对象都保持强引用，只要 block 本身存在，它们就会保持存活。

这些强引用会导致引用循环/循环引用吗？

当然会。修复方法是一样的：其中一个引用需要变成弱引用（weak reference）。要这样做，在 block 外部声明一个 `__weak` 指针，然后在 block 内部引用这个指针而不是。

我可以修改 block 捕获的变量吗？

默认情况下，block 捕获的变量在 block 内部是常量，你不能改变它们的值。例如，对象指针变量在 block 的作用域内是常量。（尽管你仍然可以向对象发送更改其内容的消息，但你不能修改指针本身。）

然而，有时你希望能够在 block 内部修改外部变量。要实现这一点，你必须使用 `__block` 关键字声明外部变量。例如，在下面的代码中，增加 `counter` 的值。

```objectivec
__block int counter = 0;
void (^counterBlock)() = ^{ counter++; };
counterBlock(); // counter 加到 1
counterBlock(); // counter 加到 2
```

如果没有 `__block` 关键字，你会在 block 定义处得到编译错误。

## 基于 block 的未来

Block 可能很难理解和使用。然而，它们在事件驱动的应用程序中非常有用且强大。Apple 的 API 正在越来越多使用 block。例如，`AssetLibrary` 和 `GameKit` 框架使用了许多基于 block 的方法。在可能的情况下使用 Apple 基于 block 的方法是一个很好的主意。

## 挑战

### 匿名 block

本章的示例将 block 的声明、赋值和使用分成了三行，以提高可读性。

当你需要向方法传递一个整数时，例如 `NSNumber` 的 `numberWithInt:`，你可以匿名地传递 `int`：

```objectivec
// 选项 1：完全拆解
int i;
i = 5;
NSNumber *num = [NSNumber numberWithInt:i];

// 选项 2：跳过变量
NSNumber *num = [NSNumber numberWithInt:5];
```

由于 block 是变量，你也可以 block 这样做。事实上，这是使用 block 最常见的方式。你很少为了传递它而声明 block 变量；你通常是匿名使用它们。

修改本章的练习，将 block 匿名作为参数传递给 `enumerateObjectsUsingBlock:`。也就是说，保留 block，但去掉 block 变量。

### NSNotificationCenter

在第 24 章中，你使用了 `NSNotificationCenter` 的 `addObserver:selector:name:object:` 方法通过你的 `zoneChange:` 方法注册回调。更新该练习，改用 `addObserverForName:object:queue:usingBlock:` 方法。在开发者文档中查找其详情。





传入的块（block）应该接收一个参数（一个 `NSNotification *`）并且不返回任何，就像 `zoneChange:` 方法一样。

你可以将 `nil` 作为 `queue:` 的参数；该参数用于并发，这是一个我们在书中不会涵盖的主题。

# 第六部分：高级 C 

要成为一名胜任的 Objective-C 程序员，你还必须成为一名胜任的 C 程序员。关于 C，你还有几件事是真的需要了解。这些主题并不是你每天都会用的概念，但你偶尔会遇到，因此我想在这里向你介绍它们。

# 33: 位运算

在本书的第一部分，我将计算机的内存描述为一片广阔的开关草原（数十亿计的开关），这些开关可以打开或关闭。每个开关代表一个位（bit），我们通常用 `1` 表示“开启”，用 `0` 表示“关闭”。

然而，你永远不会对单个位进行寻址。相反，你处理的是字节大小的位块。如果你把一个字节看作一个 8 位无符号整数，那么每个位就代表另一个 2 的幂：

图 33.1 一个字节代表十进制数字 60

![一个字节代表十进制数字 60](img/00100.jpg)

由于有 10 根手指的副作用，人们喜欢使用十进制（基 10）。然而，计算机喜欢 2 的幂。程序员经常使用 16 进制系统（16 = 2⁴），被称为十六进制或简称为“hex”。当我们处理整数的单个位时，这一点尤为如此。

我们使用字母 `a`、`b`、`c`、`d`、`e` 和 `f` 作为额外的数字。因此，十六进制的计数如下：`0, 1, 2, 3, 4, 5, 6, 7, 8, 9, a, b, c, d, e, f, 10, 11,` …

为了在编写十六进制时清晰起见，我们在数字前加上前缀 `0x`。以下是使用十六进制的相同数字和字节：

图 33.2 一个字节代表十六进制数 0x3c

![一个字节代表十六进制数 0x3c](img/00101.jpg)

注意，一个字节始终可以描述为两个位的十六进制数（如 `3c`）。这使得十六进制成为查看二进制数据的一种合理方式。一个硬汉程序员会说的话是：“我通过研究十六进制编辑器中的文档文件，反向工程了该文件格式。”想将文件显示为十六进制编码字节的列表吗？在 Terminal 中，对文件运行 `hexdump`：

```
$ hexdump myfile.txt
0000000 3c 3f 78 6d 6c 20 76 65 72 73 69 6f 6e 3d 22 31
0000010 2e 30 22 3f 3e 0a 3c 62 6f 6f 6b 20 78 6d 6c 6e
0000020 73 3d 22 68 74 74 70 3a 2f 2f 64 6f 63 62 6f 6f
0000030 6b 2e 6f 72 67 2f 6e 73 2f 64 6f 63 62 6f 6f 6b
0000040 22
0000041
```

第一列是第二列列出的字节相对于文件开头的偏移量（十六进制）。每两个位数字代表一个字节。

## 位或运算 (Bitwise-OR)

如果你有两个字节，可以对它们进行位或运算以创建一个第三个字节。如果前两个字节中对应的位中至少有一个为 `1`，那么第三个字节上的该位将将为 `1`。

图 33.3 两个字节进行位或运算的结果

![两个字节进行位或运算的结果](img/00102.jpg)

这是通过 `|` 运算符完成的。要尝试操作位，请创建一个项目：一个名为 `bitwize` 的 C 命令行工具（不是 Foundation）。

编辑 `main.c`：

```c
#include <stdio.h>
int main (int argc, const char * argv[])
{
    unsigned char a = 0x3c;
    unsigned char b = 0xa9;
    unsigned char c = a | b;
    printf("Hex: %x | %x = %x\n", a, b, c);
    printf("Decimal: %d | %d = %d\n", a, b, c);
    return 0;
}
```

当你运行此程序时，你会看到两个字节进行位或运算的结果：

`Hex: 3c | a9 = bd`
`Decimal: 60 | 169 = 189`

这有什么用？在 Objective-C 中，我们经常使用整数来指定某个设置。整数始终是一个位序列，每个位都用于表示设置中可以开启或关闭的一个方面。我们创建了这种表示。

## 位与运算 (Bitwise-AND)

如果你有两个字节，可以对它们进行位与运算以创建一个第三个字节。如果前两个字节中对应的位都为 `1`，那么第三个字节上的该位将为 `1`。

图 33.4 两个字节进行位与运算的结果

![两个字节进行位与运算的结果](img/00103.jpg)

这是通过 `&` 运算符完成的。在 `main.c` 中添加：

```c
#include <stdio.h>
int main (int argc, const char * argv[])
{
    unsigned char a = 0x3c;
    unsigned char b = 0xa9;
    unsigned char c = a & b;
    printf("Hex: %x | %x = %x\n", a, b, c);
    printf("Decimal: %d | %d = %d\n", a, b, c);
    return 0;
}
```

当你运行此程序时，你会看到两个字节进行位与运算的结果：

`Hex: 3c & a9 = 28`
`Decimal: 60 & 169 = 40`

## 其他位运算符

为了完整起见，这里是其他的位运算符。这些在 Objective-C 中不常用，但了解一下是有好处的。

### 异或运算 (Exclusive OR)

你可以对两个字节进行异或运算以创建一个第三个字节。如果两个字节中对应的位中恰好有一个为 `1`，那么第三个字节上的该位将为 `1`。

图 33.5 两个字节进行异或运算的结果

![两个字节进行异或运算的结果](img/00104.jpg)

这是通过 `^` 运算符完成的。在 `main.c` 中添加：

```c
unsigned char e = a ^ b;
printf("Hex: %x ^ %x = %x\n", a, b, e);
printf("Decimal: %d ^ %d = %d\n", a, b, e);
return 0;
```

当你运行它时，你会看到：

`Hex: 3c ^ a9 = 95`
`Decimal: 60 ^ 169 = 149`





这个运算符有时会让初学者感到困惑。在大多数表格程序中，`^` 运算符表示幂运算：`2³` 表示 `2³`。在 C 语言中，我们使用 `pow()` 函数进行幂运算：

```c
double r = pow(2.0, 3.0); // 计算 2 的三次方
```

### 补码 (Complement)

如果你有一个字节（byte），它的补码就是完全相反的字节：每个 0 变成 1，每个 1 变成 0。

图 33.6 补码

![补码](img/00105.jpg)

这是通过 `~` 运算符实现的。在 `main.c` 中添加几行代码：

```c
unsigned char f = ~b;
    printf("Hex: The complement of %x is %x\n", b, f);
    printf("Decimal: The complement of %d is %d\n", b, f);
    return 0;
}
```

你应该能看到：

`Hex: The complement of a9 is 56`
`Decimal: The complement of 169 is 86`

### 左移 (Left-shift)

如果你对位进行左移，你会取每个位并将其向最高位移动。数字左侧的位会被丢弃，右侧留出的空位用 0 填充。

图 33.7 左移 2 位

![左移 2 位](img/00106.jpg)

左移通过 `<<` 运算符完成。在 `main.c` 中添加移动两位的操作：

```c
unsigned char g = a << 2;
    printf("Hex: %x shifted left two places is %x\n", a, g);
    printf("Decimal: %d shifted left two places is %d\n", a, g);
    return 0;
}
```

当这段代码运行时，你将看到：

`Hex: 3c shifted left two places is f0`
`Decimal: 60 shifted left two places is 240`

每当你将一个数字左移一位，它的值就会翻倍。

### 右移 (Right-shift)

右移运算符应该并不意外。在 `main.m` 中添加代码：

```c
unsigned char h = a >> 1;
    printf("Hex: %x shifted right one place is %x\n", a, h);
    printf("Decimal: %d shifted right one place is %d\n", a, h);
    return 0;
}
```

运行时：

`Hex: 3c shifted right one places is 1e`
`Decimal: 60 shifted right two places is 30`

图 33.8 右移 1 位

![右移 1 位](img/00107.jpg)

每当你将一个数字右移一位，它的值就会减半。（如果是奇数，则向下取整。）

## 使用 enum 定义位掩码 (bit masks) 

你通常会想要定义一个常量列表，每个常量代表一个有一个位为 1 的整数。然后，这些整数可以通过位或（bitwise-OR）组合在一起，并如上所述使用位与（bitwise-AND）进行测试。

实现此点的优雅方法是定义一个 `enum`，并使用左移运算符来定义这些值。以下是 `UIDataDetector` 常量的定义方式：

```c
enum {
    UIDataDetectorTypePhoneNumber   = 1 << 0,
    UIDataDetectorTypeLink          = 1 << 1,
    UIDataDetectorTypeAddress       = 1 << 2,
    UIDataDetectorTypeCalendarEvent = 1 << 3,
    UIDataDetectorTypeNone          = 0,
    UIDataDetectorTypeAll           = NSUIntegerMax
};
```

## 更多字节

在本章中，我们使用了 `unsigned char`，它是 8 位字节。任何无符号整数类型的工作都相同。例如，`NSTextCheckingTypePhoneNumber` 实际上声明为 `uint64_t`，一个 64 位的无符号数。

## 挑战

编写一个程序创建一个无符号 64 位整数，使得每隔一个位就为 1。（实际上有两个可能的数字：一个是偶数，另一个是奇数。创建奇数那个。）显示该数字。

# 34

## C 字符串 (C Strings)

在有选择的情况下，Objective-C 程序员总是会选择处理 `NSString` 对象而不是 C 字符串。然而，有时我们别无选择。我们最终使用 C 字符串的最常见原因是什么？当我们在 Objective-C 代码内部访问 C 库时。例如，有一个 C 函数库可以让你的程序与 PostgreSQL 数据库服务器通信。该库中的函数使用 C 字符串。

## char

在上一节中，我们讨论了字节如何被视为一个数字。我们也可以将字节视为一个字符。正如之前提到的，有很多字符串编码。最老且最著名的是 ASCII（美国标准交换代码），它为每个字节定义了不同的字符。例如，`0x4b` 是字符 `K`。

创建一个新的命令行工具（Command Line Tool）并命名为 `yostring`。在这个程序中，你将列出一些 ASCII 字符。编辑 `main.c`：

```c
#include <stdio.h>
int main (int argc, const char * argv[])
{
    char x = 0x21; // 字符 '!'
    while (x <= 0x7e) { // 字符 '~'
        printf("%x is %c\n", x, x);
        x++;
    }
    return 0;
}
```

你可能在想：“嘿，一个字节可以包含 256 个数字中的任何一个。你只打印了 94 个字符。剩下的去哪了？”重要的是意识到 ASCII 是为了驱动旧的打字机式终端设计的，这些终端打印在纸上而不是屏幕上。例如，数字 `7` 会让终端响铃。事实上，字符 `0-31` 是不可打印的控制代码。数字 `32` 是空格字符。数字 `127` 是删除——它导致之前的字符消失。`128–255` 呢？ASCII 使用 7 位。数字 `128` 没有 ASCII 字符。

你可以将 ASCII 字符作为字面量使用。只需将它们放在单引号内。修改你的代码以使用这些：

```c
int main (int argc, const char * argv[])
{
    char x = '!'; // 字符 '!'
    while (x <= '~') { // 字符 '~'
        printf("%x is %c\n", x, x);
        x++;
    }
    return 0;
}
```

编译并运行。不可打印字符可以使用以 `\` 开头的转义序列来表示。你已经用过 `\n` 作为换行符。这里有几个：

表 34.1 常见转义序列
| | |
|---|---|
| `\n` | 换行 |
| `\t` | 制表符 |
| `\'` | 单引号 |
| `\"` | 双引号 |
| `\0` | 空字节 (0x00) |
| `\\` | 反斜杠 |

## char *

C 字符串只是内存中紧挨的一组字符。当遇到字符 `0x00` 时，字符串结束。

图 34.1 作为 C 字符串的单词 “Love”

![作为 C 字符串的单词 “Love”](img/00108.jpg)

接收 C 字符串的函数期望字符串第一个字符地址。例如，`strlen()` 会统计字符串中的字符数。尝试构建一个字符串并使用 `strlen()` 计数：

```c
#include <stdio.h> // 用于 printf
#include <stdlib.h> // 用于 malloc/free
#include <string.h> // 用于 strlen
int main (int argc, const char * argv[])
{
    char x = 0x21; // 字符 '!'
    while (x <= 0x7e) { // 字符 '~'
        printf("%x is %c\n", x, x);
        x++;
    }
    return 0;
    // 获取堆上 5 字节内存的指针
    char *start = malloc(5);
    // 在第一个字节放入 'L'
    *start = 'L';
    // 在第二个字节放入 'o'
    *(start + 1) = 'o';
    // 在第三个字节放入 'v'
    *(start + 2) = 'v';
    // 在第四个字节放入 'e'
    *(start + 3) = 'e';
    // 在第五个字节放入零作为结束符
    *(start + 4) = '\0';
    // 打印字符串及其长度
    printf("%s has %zu characters\n", start, strlen(start));
    // 打印第三个字母
    printf("The third letter is %c\n", *(start + 2));
    // 释放内存以便重用
    free(start);
    start = NULL;
    return 0;
}
```

编译并运行。注意你将指针和数字相加的地方。`start` 被声明为 `char *`。`char` 是一个字节。所以 `start + 1` 是比 `start` 多一个字节的指针。`start + 2` 是比 `start` 多两个字节。

图 34.2 每个字符的地址

![每个字符的地址](img/00109.jpg)

这种对指针赋值并引用结果的操作非常常见，因此有一个简写形式：`start[2]` 等同于 `*(start + 2)`。修改你的代码来使用它：

```c
char *start = malloc(5);
start[0] = 'L';
start[1] = 'o';
```




```c
start[2] = 'v';
start[3] = 'e';
start[4] = '\0';
printf("%s has %zu characters\n", start, strlen(start));
printf("The third letter is %c\n", start[2]);
free(start);
start = NULL;
return 0;
}
```

编译并运行它。需要注意的是，这种方法适用于任何数据类型。在这里，例如，我可以创建一个我喜欢的 3 个浮点数的列表并打印它们：

```c
int main (int argc, const char * argv[])
{
    // 申请一块足够容纳三个 float 内存块
    float *favorites = malloc(3 * sizeof(float));
    // 将值推入缓冲区中的对应位置
    favorites[0] = 3.14158;
    favorites[1] = 2.71828;
    favorites[2] = 1.41421;
    // 打印列表中的每个数字
    for (int i = 0; i < 3; i++) {
        printf("%.4f is favorite %d\n", favorites[i], i);
    }
    // 释放内存以便可以重用
    free(favorites);
    favorites = NULL;
    return 0;
}
```

这里唯一的有趣区别是 `favorites` 的类型类型为 `float *`。一个 `float` 占用 4 字节。因此 `favorites + 1` 在内存中比 `favorites` 远 4 个字节。

## 字符串字面量

如果你经常处理 C 字符串，使用 `malloc()` 内存并逐个填充字符将非常痛苦。相反，你可以通过将字符串放在引号中来创建一个指向字符字符串（以零字符终止）的指针。修改你的代码以使用字符串字面量：

```c
int main (int argc, const char * argv[])
{
    char x = '!'; // 字符 '!'
    while (x <= '~') { // 字符 '~'
        printf("%x is %c\n", x, x);
        x++;
    }
    char *start = "Love";
    printf("%s has %zu characters\n", start, strlen(start));
    printf("The third letter is %c\n", start[2]);
    return 0;
}
```

编译并运行它。

注意，你不需要为字符串字面量 `malloc` 和 `free` 内存。它是一个常量，并且在内存中只出现一次，因此编译器会处理它的内存使用。作为其常量性的副作用，如果你尝试更改字符串中的字符，就会发生糟糕的事情。添加一行应该导致你的程序崩溃的代码：

```c
char *start = "Love";
start[2] = 'z';
printf("%s has %zu characters\n", start, strlen(start));
```

当你编译并运行它时，你应该得到一个 `EXC_BAD_ACCESS` 信号。你尝试写入无权写入的内存。

为了让编译器警告你向内存的常量部分写入，你可以使用 `const` 修饰符来指定指针指向不可更改的数据。尝试一下：

```c
const char *start = "Love";
start[2] = 'z';
printf("%s has %zu characters\n", start, strlen(start));
```

现在当你编译时，你应该会收到来自编译器的错误。在继续之前，删除有问题的行（`start[2] = 'z';`）。

你可以在字符串字面量上述转义序列。使用几个吧：

```c
const char *start = "两个换行符和一个制表符后的反斜杠:\n\n\t\\";
printf("%s has %zu characters\n", start, strlen(start));
printf("The third letter is '%c\n", start[2]);
return 0;
}
```

编译并运行它。

## 与 NSString 之间的转换

如果你在 Objective-C 程序中使用 C 字符串，你需要知道如何从 C 字符串创建一个 `NSString`。`NSString` 类有一个方法可以实现这一点：

```objc
char *greeting = "Hello!";
NSString *x = [NSString stringWithCString:greeting encoding:NSUTF8StringEncoding];
```

你也可以从 `NSString` 获取 C 字符串。这稍微复杂一点，因为 `NSString` 可以处理某些编码无法处理的字符。检查转换是否可以发生是一个好主意：

```objc
NSString *greeting = "Hello!";
const char *x = NULL;
if ([greeting canBeConvertedToEncoding:NSUTF8StringEncoding]) {
    x = [greeting cStringUsingEncoding:NSUTF8StringEncoding];
}
```

你不拥有生成的 C 字符串；系统最终会为你释放它。你可以保证它的寿命至少与当前的自动释放池（autorelease pool）一样长，但如果你需要 C 字符串存在很长时间，你应该将其拷贝到你用 `malloc()` 创建的缓冲区。

## 挑战

编写一个名为 `spaceCount()` 的函数，用于统计 C 字符串中的空格字符（ASCII 0x20）。像这样测试它：

```c
#include <stdio.h>
int main (int argc, const char * argv[])
{
    const char *sentence = "He was not there.";
    printf("\"s\" has %d spaces\n", sentence, spaceCount(sentence));
    return 0;
}
```




你知道我一直刻意避免讨论的 `main()` 函数的参数吗？

```c
int main (int argc, const char * argv[])
{
  ...
}
```

现在你准备好学习它们了。`argv` 是一个 C 字符串数组。`argc` 告诉你有数组中有个字符串。这些字符串代表什么？命令行参数。

你一直在创建的命令行工具可以在 Terminal（终端）中运行。Terminal App 只是被称为 shell（壳）的一个精美界面。有几种不同的 shell，名字很好听，如 `csh`、`sh`、`zsh` 和 `ksh`，但几乎所有的 Mac 用户都使用 `bash`。当你从 `bash` 运行程序时，在输入程序名后，你可以提供任意数量由空格分隔的参数。这些参数在调用 `main()` 之前会被封装进 `argv`。

说实话，Cocoa 和 iOS 程序员很少使用 `argv` 和 `argc`。然而，如果你编写编写一个实用的命令行工具，你几乎肯定需要知道如何利用它们。

在 Xcode 中，创建一个名为 `Affirmation` 的新 C Command Line Tool（命令行工具）项目。`Affirmation` 将接受两个参数：一个人的名字和一个数字 `n`。当你运行它时，那个人会被宣布 `n` 次很酷。

```
$ Affirmation Mikey 3
Mikey is cool.
Mikey is cool.
Mikey is cool.
```

在我们在此之前，将 `main()` 修改为仅打印 `argv` 中的每个参数：

```c
#include <stdio.h>

int main (int argc, const char * argv[])
{
  for (int i = 0; i < argc; i++) {
    printf("arg %d = %s\n", i, argv[i]);
  }
  return 0;
}
```

如果你在 `bash` 中运行此代码，只需要在命令行中输入参数即可。

```
$ Affirmation Aaron 4
```

然而，要在 Xcode 中运行带参数的程序，你必须先编辑 Scheme（方案）。在 Product 菜单下，选择 Edit Scheme....当表单出现时，在左侧的表格视图中选择 `Run Affirmation`。然后从表单顶部的选项中选择 `Arguments` 标签。找到标题为 `Arguments Passed On Launch` 的列表，并使用 `+` 按钮添加项目：一个名字和一个数字。

图 36.1 添加参数

![Adding arguments](img/00111.jpg)

点击 OK 关闭表单。

当你运行程序时，你将得到 `argv` 中的字符串列表。让大多数人感到惊讶的是 `argv[0]`：

```
arg 0 = /Users/aaron/Library/Developer/Xcode/DerivedData/
     Affirmation-enkfqsgavfsproeggoxwbrmcowvn/Build/Products/Debug/Affirmation
arg 1 = Aaron
arg 2 = 4
```

`argv[0]` 是可执行文件的路径。

图 36.2 Affirmation 中的 argv 和 argc

![argv and argc in Affirmation](img/00112.jpg)

如果你的程序接收参数，你应该做的第一件事是确保参数数量正确。编辑 `main.m`：

```c
#include <stdio.h>
#include <stdio.h> // atoi()

int main (int argc, const char * argv[])
{
  if (argc != 3) {
    fprintf(stderr, "Usage: Affirmation <name> <number>\n");
    return 1;
  }
  int count = atoi(argv[2]);
  for (int j = 0; j < count; j++) {
    printf("%s is cool.\n", argv[1]);
  }
  return 0;
}
```

`atoi()` 是一个标准 C 函数，用于读取一个 C 字符串并尝试将其转换为 `int`。

编译并运行程序。

# 37

## Switch 语句

检查一个变量是否属于一组值中的某并不罕见。使用 `if-else` 语句，它看起来如下：

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

为了让这种操作变得更容易，C 语言提供了 `switch` 语句。上面的代码可以改为：

```c
int yeastType = ...;
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

等等，让我们看看正确的版本：

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

注意 `break` 语句。如果没有 `case` 结尾的 `break`，系统将执行所有后续的 `case` 子句。例如，如果我有：

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

程序将运行 `makeBeer()`、`makeWine()` 和 `makeFuel()`。这主要是因为忘记在 `case` 结尾放置 `break` 是一个常见的错误，而且它只有在程序运行异常时才会被发现：因为 `case` 只能是一个常量整数。因此，在大多数 Objective-C 程序中你看不到很多 `switch` 语句。这就是为什么我在书快结束时悄悄地插入了它。





## 符号

- `!` (逻辑非)运算符，`if/else`
- `!=` (不等于)运算符，`if/else`
- `\"` 转义序列，`char`
- `#define`，`常量`
- `#define` 与全局变量
- `#import`, `#include` 和 `#import`
- `#include`, `#include` 和 `#import`
- `%` (取模运算符)，`整数除法`（另参见 `tokens`）
- `%=` 运算符，`运算符简写`
- `%@`,`创建 Asset 类`
- `%d`，`printf()`
- `%e`，用于显示浮点数的令牌
- `%p`,`获取地址`
- `%s`，`printf()`
- `%u`，用于显示整数的令牌
- `%zu`，`多少字节？`
- `&` 运算符，获取地址，`获取地址`
- `&&` (逻辑与)运算符，`if/else`
- `()` (括号) 转换运算符，使用 `整数除法`
- `()` 函数，`我如何编写和使用函数？`
- `**` 函数，`函数如何协同工作`
- `*` (星号) 算术运算符，`整数运算`
- `*` 指针运算符，`获取地址处的数据`
- `*=` 运算符，`运算符简写`
- `+` (加号)，`整数运算`
- `++` (自增运算符)，`运算符简写`
- `+=` 运算符，`运算符简写`
- `-` (减号)，`整数运算`
- `--` (自减运算符)，`运算符简写`
- `-=` 运算符，`运算符简写`
- `->` (解引用)运算符，`堆`
- `.pch` (预编译头文件)，`#include` 和 `#import`
- `/` (除法运算符)，`整数除法`
- `/* ... */` (注释)，`我从哪里开始写代码？`
- `//` (注释)，`我从哪里开始写代码？`
- `/=` 运算符，`运算符简写`
- 8 位无符号数字，`整数`
- `;` (分号)，`我从哪里开始写代码？`
- `{}` 块和，`赋值块`
- `do-while` 循环和，`do-while 循环`
- `<` (小于) 运算符，`if/else`
- `< >` (尖括号)，导入头文件，`#include` 和 `#import`
- `<<` 运算符，`左移`
- `<=` 运算符，`if/else`
- `=` 运算符，`变量`
- `==` 运算符，`if/else`
- `>` (大于) 运算符，`if/else`
- `>>` 运算符，`右移`
- `?` (三元运算符)，`好奇者：三元运算符`
- `@property`，`属性`
- `@selector()`，`目标-动作`
- `@synthesize`，`属性`
- `\` (反斜杠)，`char`
- `\n`，`printf()`
- `\\` 转义序列，`char`
- `^` (脱字符/异或运算符)，`异或`
- 标识块，`定义块`
- `{}` (大括号)，`我从哪里开始写代码？`
- `||` (逻辑或) 运算符，`if/else`





`~` (波浪号), 补

### A

`abs()`, 运算符简写

accessor methods, 访问器方法

> properties and, 属性

actions (target), 回调

`addObject:`, NSArray/NSMutableArray

addresses, 地址与指针

> pointers and, 类型

`alloc`, 嵌套消息发送, `init`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_150.html_filepos611323)

ampersand (`&`), retrieving addresses, 获取地址

`AND` (`&&`) 逻辑运算符, if/else

`AND` (位运算), 按位与

angle brackets (`< >`), importing header files, #include and #import

anonymous

> blocks, 匿名块

> functions, 块

Apple Developer Tools, installing, 你的第一个程序

`application:didFinishLaunchingWithOptions:`, 应用代理, 添加新任务, 致更奇心好奇的人：`main()` 是怎么的？

applications

> (另另参见 程序, Xcode)

> Cocoa, 你的第一个 Cocoa 应用

> Cocoa Touch, 你的第一个 iOS 应用

> desktop, 你的第一个 Cocoa 应用

> document-based, 编辑 BNRDocument.h

> event-driven, 事件驱动应用

> iOS, 你的第一个 iOS 应用

> vs. programs, 开始使用 Xcode

`ARC` (自动引用计数), 对象所有权

> command-line, 命令行参数

> functions, 如何编写和使用函数？

> `init`, 带参数的 `init` 方法

> methods, 多个参数

> arrays, `NSArray`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_075.html_filepos275171)

> in C, `C`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_182.html_filepos754392)

> filtering, 过滤

> sorting, 排序

> ASCII characters, 向文件写入一个 `NSString`, `char`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_177.html_filepos737436)

> assembly code, C and Objective-C

`asterisk` (`*`) arithmetic operator, 整数运算

> pointer operator, 获取地址处的数据

`AT&T`, C and Objective-C

`atoi()`, 命令行参数

`atomic` option, atomic vs. nonatomic

`attributes` inspector, 编辑 BNRDocument.xib

Automatic Reference Counting (ARC), 对象所有权

automatic variables, 堆

`autosizing mask`, 编辑 BNRDocument.xib

### B

backslash (`\`), `char`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_177.html_filepos737436)

base-16 (十六进制)

> integers, 显示整数的令牌

> number system, 位运算

base-8 (八进制) integers, 显示整数的令牌

> bits, 地址与指针

bitwise AND, 按位与

bitwise operations, 位运算

bitwise OR, 按位或

`block` keyword, 内存管理

`blocking` (functions), 如何工作

> blocks, 块

> anonymous, 匿名块

> defining, 定义块

> return values of, 返回值

> variables, 定义块

BOOL (type), 布尔变量

boolean variables, 布尔变量

`break` statement, 断点

`breakpoint navigator, 在调试器中查看调用帧

`breakpoints, 在调试器中查看调用帧

`buffers, 堆

`bugs, 递归

`building programs, 如何运行我的程序?

`bytes, 地址与指针





-   原始类型，C 原始类型
-   字符串，C 字符串
-   回调，回调, 块
-   内存管理和，回调与对象所有权
-   调用函数，如何编写和使用函数？
-   捕获变量，内存管理
-   脱位符 (`^`)
-   异或运算符，异或
-   识别块，定义块
-   强制转换运算符，整数除法
-   中央处理器单元 (CPU),地址与指针
-   char (类型)，类型, char
-   作为 8 位数字，整数
-   `char *` (类型)，printf()
-   类方法，更多消息
-   类前缀，开始学习 iTahDoodle
-   类，对象, 你的第一个类
-   （另参见 objects
-   Cocoa，事件驱动应用, 你的第一个 Cocoa 应用
-   Cocoa Touch，事件驱动应用
-   代码补全，我该从哪里开始写代码？
-   集合类，集合类)
-   命令行参数，命令行参数
-   C 中的命令行工具，开始学习 Xcode
-   定义的，开始学习 Xcode
-   Foundation，创建第一个对象
-   编译器，C 和 Objective-C, 什么是程序？
-   补数，补数
-   条件表达式，if/else, 深入感兴趣的：三元运算符
-   常量，常量
-   continue 语句，continue
-   控制器对象 (MVC)，Model-View-Controller
-   控制，添加新任务
-   便捷方法，Retain 计数规则
-   copy (方法)，copy, 关于拷贝的更多信息
-   copy (属性标记)，copy
-   copyWithZone:，copy
-   count (NSArray)，NSArray
-   Cox, Brad，对象
-   CPU (中央处理器单元),地址与指针
-   大括号 (`{ }`),我该从哪里开始写代码？

### D
-   守护进程，开始学习 Xcode
-   数据源，回调
-   数据类型，类型
-   dateByTime:，间隔
-   dealloc，创建 Asset 类
-   debug 导航器，在调试器中查看栈帧
-   调试器，递归
-   栈帧，在调试器中查看栈帧
-   GDB/LLDB，我如何运行我的程序？
-   声明变量，你的第一个类
-   方法，你的第一个类
-   变量，类型
-   递减运算符 (`--`),运算符简写
-   #define，常量
-   #define vs. 全局变量，#define 与 全局变量
-   代理，回调
-   引用运算符 (`->`)，堆
-   指针引用，获取地址处的数据
-   description 方法，创建 Asset 类
-   指定初始化器，带参数的 init 方法
-   开发者文档，开发者文档
-   字典，NSDictionary/NSMutableDictionary
-   目录，写入文件到，NSError
-   除法（整数），整数除法
-   do-while 循环，do-while 循环
-   文档大纲，建立连接
-   基于文档的应用程序，编辑 BNRDocument.h
-   文档，开发者文档
-   点符号表示法，点符号表示法





`double` (类型), [类型]

双引号转义序列 (`\"`), [char]

《代码之梦》(Rosenberg), [程序员的生活是如何工作的]

### E

else, [if/else]

else if, [else if]

编码 (字符串), [向文件写入 NSString]

enum, [enum]

> 位掩码，定义, [使用 enum 定义位掩码]

`enumerateObjectsUsingBlock:`, [传入一个块 (block)]

相等的对象, [NSSet/NSMutableSet]

错误对象, [NSError]

错误，语法, [我该从哪里开始写代码？]

转义序列, [char]

事件驱动应用, [事件驱动应用]

事件, [回调], [我的第一个 iOS 应用程序]

异或 (XOR), [异或逻辑]

EXC_BAD_ACCESS 信号, [字符串字面量]

EXIT_FAILURE, [return]

EXIT_SUCCESS, [return]

指数, [浮点数]

表达式, [带有变量的程序]

> 条件的, [if/else], [给好奇好奇者：条件（三元）运算符]

外部变量, [内存管理]

### F

%f, [显示浮点数的标记符]

快速枚举, [NSArray]

> NSData 和, [向文件写入 NSData 对象]

> NSError 和, [NSError]

> 读取, [使用 NSString 读取文件]

> 写入, [使用 NSString 和 NSData 写入文件]

过滤, [过滤]

第一响应者, [添加新任务]

标志 (位运算符), [位与 Bitwise-AND]

`float` (类型), [类型]

> 类型转换和, [整数除法]

浮点数, [浮点数]

for 循环, [for 循环]

> NSArray 和, [NSArray]

格式化字符串 `printf()`, [显示整数的标记符], [显示浮点数的标记符], [创建 Asset 类]

Foundation (框架), [Objective-C 和 Foundation], [参考页面], [事件驱动应用]

Foundation.h 头文件, [BNRAppDelegate]

帧 (frames), [局部变量、帧和栈], [在调试器中查看帧]

框架, [Objective-C 和 Foundation], [事件驱动应用]

`free()`, [堆]

函数, [函数]

> (另见方法)

> 参数和, [我如何编写和使用函数？]

> 使用的益处, [我什么时候应该使用？], [我如何编写和使用函数？]

> 阻塞, [函数如何协作]

> 调用, [我如何编写和使用函数？], [函数如何协作]

> 声明, [我如何编写和使用函数？]

> 定义, [我该从哪里开始写代码？]

> 定义, [我如何编写和使用函数？]

> 解释, [什么是程序？]

> 的帧, [局部变量、帧和栈]

> 局部变量, [局部变量、帧和栈]

> 在 math.h 中的, [用于浮点数的函数]

> 名称的, [我该从哪里开始写代码？], [函数如何协作]

> 参数的, [我如何编写和使用函数？], [局部变量、帧和栈]

> 引用传递, [编写引用传递函数]

> 在程序中, [函数如何协作]

> 菜谱的隐喻, [什么是程序？]

> 递归的, [递归]

> 返回值, [return]

> 写入, [我如何编写和使用函数？]




# GDB 调试器，我如何运行我的程序？

# getter 方法，访问方法

# 属性属性和，可变性

# 全局变量，全局和静态变量, 全局变量

# vs. `#define`，#define` 与全局变量

# 图形用户界面（参见 用户界面 ）

# GUI（参见 用户界面 ）

# 指南，在开发者文档中的，参考页面

## H

### `.h` (头文件),你的第一个类

### 头文件，#include` 和 `#import`

### 头文件 (`.h`),你的第一个类

### 堆，堆

### 基于堆的块，内存管理

### 辅助函数，添加一个 C 辅助函数

### 辅助对象，回调, 辅助对象

### 十六进制（16 进制）整数，显示整数的标记符

### 数制系统，位运算

### 高级语言，C 和 Objective-C

### 人机交互指南 (HIG),编辑 `NR.xib`

## I

### `id` (类型),id

### 相同对象，NSSet/NSMutableSet

### `if` 构造语句，`if/else`

### 不变对象，不可变对象

### 实现文件 (`.m`),你的第一个类

### `#import`,`include` 和 `#import`

### `#include`,`include` 和 `#import`

### 增运算符 (`++`),简写运算符

### 继承，继承

### 继承和，继承

### 对象，实例变量

### 实例，[对象]](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_062.html_filepos239808)

### 实例化 (对象)，NSError

### `int` (类型),类型, 布尔变量, 整数

### 转换和，整数除法

### 整数，整数

### 集成开发环境，开始使用 Xcode

### Interface Builder，了解 Interface Builder

### 接口文件 (`.h`),你的第一个类

### 接口，在 Interface Builder 中设置，了解 Interface Builder

### 编程化接口，设置视图

### iOS 应用，你的第一个 iOS

### Cocoa Touch 和，事件驱动应用

### 内存管理在，向 Employee 添加对多关系

### Objective-C 和，C 和 Objective-C

### 模拟器，在 iOS 模拟器上运行

### `isEqual`,NSString, 相同对象，NSSet/NSMutableSet

### 迭代，数组

### Key 值对，字典

### Key 值对，字典





爱，Tom，对象

## M

- `.m` 文件，创建并使用你的第一个对象, 你的第一个类
- 机器码，C 和 Objective-C
- 宏，`#define`](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_111.html_filepos442105)
- Mac OS X，C 和 Objective-C
  - > (另参 Cocoa)
- `main()`，我该从哪里开始写代码？, 我该如何编写和使用函数？, 查看调试器中的帧, 给更有好奇心的人：main() 是怎么的？
- `malloc()`，堆, 字符串字面量, C 数组
- 手动引用计数，给更有好奇心的人：手动引用计数和 ARC 历史
- `math.h` 头文件，浮点数函数

## memory

- > 堆，堆
- > 内存中的对象,内存中的对象
- > 栈，局部变量、帧和栈](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_029.html_filepos129632)
- 内存地址，地址和指针
- 内存泄漏，为 Employee 添加对多关系, 防止内存泄漏, 强留循环

## memory management

- > 自动引用计数 (ARC)，对象所有权和 ARC
- > blocks，内存管理](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_165.html_filepos70554)
- > C 中的堆,堆
- > 回调，回调与对象所有权
- > 释放对象,对象实例
- > 局部变量,堆
- > 手动引用计数，给更有好奇心的人：手动引用计数和 ARC](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_100.html_filepos392371)
- > 属性，属性修饰符](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_157.html_filepos650918)
- > 强留循环,强留循环
- > 弱引用，弱引用](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_098.html_filepos384227)
- > 消息，更多消息](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_068.html_filepos256664)
- > 消息剖析，消息剖析](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_064.html_filepos247366)
- > 嵌套，嵌套消息发送](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_069.html_filepos259014)
- > 对象，对象](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_062.html_filepos239808)
- > 向 nil 发送消息,向 nil 发送消息
- > 方法，对象](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_062.html_filepos239808)
  - > (另参 函数)
  - > 访问器，访问器方法](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_083.html_filepos313200)
  - > 便利性，引用计数规则](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_100.html_filepos397084)
  - > 声明，你的第一个类](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_082.html_filepos304223)
  - > 覆写，重写方法](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_090.html_filepos339612)
- 减号 (`-`)，整数运算](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_037.html_filepos168255)
- 模型对象 (MVC)，模型-视图-控制器](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_135.html_filepos541913)
- 模型-视图-控制器 (MVC)，模型-视图-控制器](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_135.html_filepos541913), 重温 MVC
- > `modf()`，引用传递](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_055.html_filepos213189)
- > 取模 (`%`)，整数除](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_037.html_filepos169185)
- > `mutableCopy``拷贝`, 更多拷贝
- > MVC (模型-视图-控制器)，模型-视图-控制器](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_135.html_filepos541913), 重温 MVC
- > `M_PI` 常量，常量](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_108.html_filepos434559)

## N

- > 嵌套，嵌套消息发送](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_069.html_filepos259014)
- > 换行符 (`\n`)，`printf()`](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_036.html_filepos155423), `char` (CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_177.html_filepos737436)
- > NS (NEXT)，获取 ioodle](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_131.html_filepos527790)
- > `nil`，向 nil 发送消息](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_071.html_filepos265556), 不可变对象, 集合和 nil
- > `nonatomic` 选项，atomic vs. nonatomic](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_157.html_filepos660269)
- > NOT (`!`) 逻辑运算符，if/else](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_020.html_filepos94817)
- > 通知 (回调)，回调](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_120.html_filepos474225), 通知
- > NS (NEXT)，获取 ioodle](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_131.html_filepos527790)
- > `NSArray`,NSArray](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_075.html_filepos275171), `NSArray/NSMutableArray`](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_102.html_filepos403530)
  - > 过滤，过滤](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_102.html_filepos415265)
  - > 不可变对象和，不可变对象](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_102.html_filepos405753)
  - > 属性列表和，属性列表](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_127.html_filepos515962)
  - > 排序，排序](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_102.html_filepos411041)
- `NSAttributedString`,不可变字符串对象](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_102.html_filepos405753)
- `NSCharacterSet`,不可变字符集](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_102.html_filepos405753)
- `NSData`,不可变对象](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_102.html_filepos405753)
  - > 属性列表，属性列表](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_127.html_filepos515962)
  - > 从文件读取，从文件读取 NSData](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_119.html_filepos471155)
  - > 写入文件，将 NSData 对象写入到文件](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_118.html_filepos465991)





- `NSDataWritingAtomic` 选项 (`NSData`)，将 NSData 对象写入文件
- `NSDate`，消息剖析
- > 属性列表和，属性列表
- `NSDictionary`，不可变对象, `NSDictionary/NSMutableDictionary`
- > 属性列表和，属性列表
- `NSError`，NSError
- `NSIndexSet`，不可变对象
- `NSInteger` (类型),整数
- `NSLocale`，全局变量
- `NSLog()`，创建并使用你的第一个对象
- > vs. `printf()`, `NSString`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_073.html_filepos269191)
- `NSMutableArray`，NSMutableArray, 对象所有权和 ARC, `NSArray/NSMutableArray`, 不可变对象
- > 排序，排序
- > `UIKit.h` 和，BNRAppDelegate
- `NSMutableAttributedString`，不可变对象
- `NSMutableDictionary`，`NSDictionary/NSMutableDictionary`
- `NSMutableSet`，`NSSet/NSMutableSet`
- `NSMutableString`，不可变对象
- `NSNull`，集合与 nil
- `NSNumber`，不可变对象, C 原生类型
- > 属性列表和，属性列表
- `NSObject`，继承, 创建 Asset
- > `init` 和 `init`](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_150.html_filepos61123)
- > 键值编码，键值编码
- `NSPredicate`，过滤
- `NSRunLoop`，回调
- `NSScrollView`，编辑 BNRDocument.xib
- `NSSearchPathForDirectories()`，添加 C 辅助函数
- `NSSet`，不可变对象, `NSSet/NSMutableSet`
- `NSString`，NSString, 不可变对象
- > (另参 strings)
- > 属性，属性列表
- > 读取文件，使用 NSString 读取文件
- > 写入文件，将 NSString 写入文件
- `NSTableView`，你的第一个 Cocoa 应用, 编辑 BNRDocument.xib
- `NSUInteger` (类型),整数
- `NSURLConnection`，辅助对象
- `NSURLRequest`，不可变对象
- `NSValue`，C 原生类型
- `NULL`，NULL, 避免引用
- > 数字 (另参 浮点数,整数)
- > 十进制，显示整数的 Token, 位运算
- > 八进制，显示整数的 Token
- `object` 封装，键值编码
- > `object` 库，编辑 BNRDocument.xib
- > `object` 所有权，对象所有权和 ARC
- `object-type`，实例变量
- `objectAtIndex: (NSArray)``NSArray
- `Objective-C`，C 和 Objective-C
- `objects`，对象
- > deallocating，实例变量
- > 不变的，不可变对象
- > 继承和，继承
- > 作为实例变量，实例变量
- > 实例变量之间的关系，实例变量
- 八进制 (base-8) 整数，显示整数的 Token
- 运算符（比较/逻辑），if/else
- OR (位运算)，位或
- OR (||) 逻辑运算符，if/else
- 重写方法，重写方法

## P
- 参数，我该如何编写和使用函数？, 局部变量、栈帧和栈
- 父子级关系（对象），对象所有权和 ARC
- > 内存泄漏和，防止内存泄漏
- 括号 (())
- > 转换运算符，整数除法
- > 函数和，我该如何编写和使用函数？, 函数如何协同工作





- 引用传递，引用传递](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_055.html_filepos213189), NSError
- 加号 (`+`), 整数运算
- 指针，类型, 地址与指针
- `function`，Blocks
- `NSMutableArray` 和，NSMutableArray
- 对象和，消息机制剖析
- 在指针中存储地址，在指针中存储地址
- PostgreSQL 数据库，C 字符串
- 预编译头文件，#include 和 #import
- 优先级，用于算术运算符，整数运算
- 谓词，过滤
- 预处理器，预处理器指令
- 预处理器指令，预处理器指令
- 基本类型 (C)，C 基础类型
- `printf()`，什么是程序？, 函数是如何协同工作的, `printf(), 用于显示浮点数的令牌
- `vs.` vs. `NSLog()`，NSString
- 程序性能分析，强引用循环
- 编程语言，C 和 Objective-C

## 程序
- `building`，我该如何运行我的程序？
- `compiling`，什么是程序？
- `defined`，什么是程序？
- `profiling`，强引用循环
- `running`，我该如何运行我的程序？, 带有变量的程序
- `vs.` 应用程序，使用 Xcode
- `project` navigator，我该如何运行我的程序？
- `projects`，使用 Xcode
- `properties`，属性, 属性
- `attributes`，属性属性
- `@property`，属性
- `property lists`，属性列表
- `protocols`，辅助对象, 协议

## Q
- 快速帮助，快速帮助

## R
- RAM (随机访问存储器)，地址与指针
- `readonly` (属性属性)，可变性
- `readwrite` (属性属性)，可变性
- `receivers` (对象)，消息机制剖析
- 食谱比喻 (函数)，什么是程序？
- 递归，递归

## references
- `NSError` 和，NSError
- `pass by`，引用传递](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_055.html_filepos213189)
- `resignFirstResponder`，添加任务
- `retain` 计数，了解：手动引用计数与 ARC, retain 计数
- `retain` 循环，强引用循环
- `return`，返回
- `in` blocks，返回值
- `right-shifting` 位，右移

## S
- `@selector()`，目标-动作
- `selectors`，目标-动作
- `self`，self, 添加新任务
- `semicolon` (`;`)，我从哪里开始代码？
- `blocks` 和，赋值一个 block
- `do-while` 循环，do-while 循环
- `setter methods`，访问器方法
- `property attributes` 和，可变性
- `setValue:forKey:`，键值编码 (KVC)
- `shell`，命令行参数
- `short` (类型)，类型
- `shortcuts`，`keyboard`，带有变量的程序, 创建 Asset 类, 编辑 BNRDocument.xib
- `simulator` (iOS)，在 iOS 模拟器上运行
- `sizeof()`，多少个字节？
- `sleep()`，函数是如何协同工作的, 强引用循环
- `sorting`，排序
- `springs` (自动调整掩码)，编辑 BNRDocument.xib
- `stack`，局部变量、栈帧与栈
- `stack-based blocks`，内存管理
- `standard libraries`，函数是如何协同工作的





# 静态变量
- 静态变量，全局变量和静态变量
- `stdio.h` 头文件，函数如何协同工作
- `stdlib.h` 头文件，函数如何协同工作

# 字符串
- `string encodings`，将 `NSString` 写入文件
- 字符串，`NSString`
- 在 C 语言中，`C 字符串`
- 定义，`printf()`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_036.html_filepos155423)
- 字面量，`字符串字面量`
- `printf()` 和 `printf()`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_036.html_filepos155423)
- `stringWithFormat:`，`NSString`
- `strlen()`，`char`

# 结构体
- `strong` 属性属性，生命周期限定符
- `struct` 类型，`类型`, `结构体`
- 结构体，`类型`, `结构体`
- `struts` (自动调整掩码)，编辑 `BNRDocument.xib`

# 子类
- 子类，`NSMutableArray`
- 子视图，设置视图
- `super` 指令，`super`

# 语法
- 语法错误，我从哪里开始写代码？
- 语法，代码，我从哪里开始写代码？
- `synthesize` (等等，原文写的是 `@synthesize`，但通常是一个关键字，我将其视为代码类表达式)，`@synthesize`，`属性`
- 合成访问器方法，`属性`
- T `\t` 转义序列，`char`
- 表格视图，连接表格视图, 编辑 `BNRDocument.xib`
- target-action 回调，`回调`
- 模板，从 Xcode 开始, 从 i 开始
- 终端`命令行参数`
- `ternary` 运算符 (?) 更多好奇的三元运算符
- `tilde` (`~`)，`符号`
- 定时器，使用 target-action`Target-action`
- 多对多关系，`实例变量`
- 一对一关系，`实例变量`, 防止内存泄漏
- 标记
- `description`，创建 `Asset` 类
- `explained`，`printf()`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_036.html_filepos155423)
- 浮点数，显示浮点数的标记
- 整数，显示整数的标记
- 指针，获取地址
- `string`，`printf()`(CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_036.html_filepos155423)
- `typedef` 关键字，`结构体`, `typedef`
- 类型，`类型`

### U
- `UIButton`，添加任务
- `UIKit.h` 头文件，`BNRAppDelegate`
- `UITableView`，`协议`
- `UITableViewDataSource` 连接表格视图
- `UNICODE` 标准，`NSString`
- `UnixC and Objective-C
- `unsafe_retained` (属性)生命周期限定符
- `unsigned 8-bit` 数字，`整数`
- `unsigned` 关键字，`整数`
- `__unused` 修饰符，`Target-action`
- `user interface`，设置 `Interface Builder`查看 Interface Builder
- `programmatically`，设置视图
- `UTF` 字符串，将 `NSString` 写入文件

### V
- `valueForKey`，键值编码
- `variables`，`变量与类型`
- `assigning`，带有变量的程序
- `automatic`，`堆`
- `block`，定义 blocks
- `boolean`，`布尔变量`
- `captured`，内存管理
- `declaring`，`类型`, 带有变量的程序, 你的第一个类
- `external`，内存管理
- `global`，全局变量和静态变量, 全局变量`
- `instance`，`对象`, `实例变量`
- `local`，局部变量、帧和栈
- `self`，`self`
- `static`，全局变量和静态变量





> 编程方式，设置视图

`void`, 如何编写和使用函数？, 返回

### W

警告 (Xcode), 如何编写和使用函数？

`weak` (属性修饰), 生命周期修符

`weak` 引用, 弱引用

> blocks 和，内存管理

while 循环, while 循环

`writeToFile:atomically:encoding:error:`, NSError

### X

Xcode

> 属性检查器, 编辑 BNRDocument.xib

> 断点导航器, 在调试器中查看帧

> 在...中编写程序，如何运行我的程序？

> 代码补全, 我从哪里开始写代码？

> 在...中颜色编码，我从哪里开始写代码？

> 在...中创建类，你的第一个类

> 调试导航器, 在调试器中查看帧

> 在...中查看开发者文档，开发者文档

> 安装,安装 Apple 开发者工具

> 键盘快捷键,带有变量的程序, 创建 Asset 类, 编辑 BNRDocument.xib

> 日志导航器,如何运行我的程序？

> 偏好,我从哪里开始写代码？

> 项目导航器,如何运行我的程序？

> 快速帮助,快速帮助

> 运行程序,带有变量的程序

> 在...中运行程序,如何运行我的程序？

> 模板,开始使用 Xcode

> ...中的警告,如何编写和使用函数？

> `.xib` 文件,查看 Interface Builder

`XOR` (异或),异或

### Z

`zero` (false)

> `nil`,向 nil 发送消息](CR%2105JTP5FAEH75ZCBEQMM1XBY4QNJ7_split_071.html_filepos26556)

> `NULL` 和,NULL

# 来自 Big Nerd 的更多...

Big Nerd Ranch 的存在是为了开阔学生和客户的眼界。无论我们是在培训人才还是为公司开发移动战略，我们的核心理念贯穿于一切之中。

## Big Nerd 的故事

Big Nerd Ranch 是 CEO Aaron Hillegass 的创意，自 2001 年成立以来，该园区已接待了 2000 多名学生。在过去的十年里，我们有机会与苹果、三星、诺基亚、谷歌、洛斯阿拉莫实验室和 Adobe 等顶级公司合作，帮助他们实现编程目标。我们的软件工程师团队是行业内顶尖的，这体现在我们的工作中。我们为客户开发了数十种灵活解决方案。

## 帽子背后的故事

2001 年，Big Nerd Ranch 创始人 Aaron Hillegass 在 WWDC（开发者大会）推广 Big Nerd 品牌。由于没有钱买昂贵的展位，Aaron 戴了一顶大牛仔帽在向潜在学生和客户发放 Big Nerd 材料时吸引注意力。一周后，我们获得了第一个大客户，从那时牛仔帽就成了 Big Nerd 品牌的代名词。

## 新园区 - 2012 年开放

为了不断完善学生体验，Big Nerd Ranch 正在建立自己的设施。新园区距离亚特兰大机场仅 20 分钟车程，将成为一个学习中心，包含了 Aaron Hillegass 对技术教育的愿景，拥有先进教室、精致餐饮和健身设施。

## 培训：达到 Nerd 境界

自 2001 年以来，Big Nerd Ranch 一直在静修环境中提供由专家导师教授的密集计算机编程课程。我们认为学生在我们的园区里蓬勃成长。课程、住宿和用餐都在同一栋建筑内进行，让你自由地与编程伙伴和导师学习、编码和讨论。在 Big Nerd Ranch，我们负责细节；你唯一的工作就是学习。

### 我们的老师

我们的老师是各自领域的领袖。他们对所教的技术有深入的理解，并拥有丰富的开发经验，使他们能够解决你作为开发者会遇到的问题。Big Nerd Ranch 的导师提供了必要的知识结合和卓越的教学技能，使我们的学生离开园区时技能大大提升。

### Big Nerd 方式

我们开发了“Big Nerd Ranch 方法”。这种方法论指导着我们课程的开发和呈现。风格轻松但专注，简短的讲座后是实操练习，旨在让你对所学习的每项技术都有即时、相关的理解。

### 你的园区之旅

一次费用涵盖学费、餐饮、住宿以及往返机场的交通。在 Big Nerd Ranch，我们通过在佐治亚亚特兰大和德国法兰克福的安静舒适环境中提供课程，消除了标准企业培训固有的干扰。

### 可用课程

*   高级 Mac OS X
*   Android
*   入门 Cocoa
*   入门 iOS (iPhone/iPad)
*   入门 Ruby on Rails
*   西班牙语 Cocoa 跨境班
*   Cocoa I
*   Cocoa II
*   iOS 跨境班
*   Django
*   iOS (iPhone/iPad)
*   OpenGL
*   Python 掌握 精通
*   Ruby on Rails I
*   Ruby on Rails II

## 上门培训：我们的 Nerd，你的地点

通过我们的上门培训计划，你可以以经济且方便的方式让我们著名的课程来到你那里。我们的专家导师将通过新鲜、参与感强且无障碍的实教学支持帮助你的团队进步。





*   课后导师指导可以为您的团队在处理极具挑战性的项目时提供支持。

### 价格负担能力

*   无需为所有员工安排飞机、火车和汽车行程；我们的技术专家（Nerds）会直接上门服务。
*   可培训多达 22 名学生，价格比公开注册培训相比有大幅折扣。

### Nerd 专业知识

*   我们的讲师在教学和编程方面都拥有丰富经验。他们通过将实战经验引入您的团队，超越了理论层面。
*   现场培训包括课后联系我们的技术专家、访问我们广阔的校友网络以及我们的 Big Nerd Ranch 论坛。学习支持不会因为课程的结束而停止。

对于您的现场培训，我们提供一名讲师、所有 Big Nerd Ranch 版权课程材料、礼品、结证书以及访问我们广泛校友网络的权限。您则需要提供教室布置、所有学生使用的电脑及相关设备、一台投影仪和一个投影幕。

## 咨询：在公司内部及现场实现 Nerdvana

当您与 Big Nerd Ranch 签署合同时，我们将与您直接合作，将您的需求转化为全面的桌面和/或移动解决方案。我们的开发者和设计师一直创造着 iPhone App Store 中最引人注目的应用程序。

### 管理哲学

Big Nerd Ranch 全方位地管理每位客户的关系。我们的目标是从项目启动到完成全过程中对客户进行沟通和教育，并最终帮助他们在其利基市场中获得竞争优势。

### 项目策略

我们对所有项目估算都采取注重细节的方法。我们将与您合作定义策略、指明产品供应，然后将它们构建成独立的软件。

### 我们的流程

我们的咨询流程分为三个不同的阶段：需求、执行和监控/控制。将您的业务案例带给我们，我们将为您制定用户界面和数据库设计制定一份计划。从那里开始，我们将制定报价单并开始设计和实施过程。我们的技术专家将进行许多测试，包括调试和性能优化，确保应用程序运行符合您的预期。最后，我们将对您的应用程序进行 Beta 测试，并准备好将其在 iTunes 商店和/或 Android 市场进行提交和部署。一旦您的应用程序完成，技术专家将与您一起进行后续版本更新，甚至可以帮助您的应用程序进行营销。

### 客户证言

| | |
| :--- | :--- |
| | tops 已与 Big Nerd Ranch 密切合作了八多年。他们一直为我们的项目交付高质量的代码；整洁且富有诗意。得益于他们的贡献，我们已成为该领域的领导者。 |
| | -- Mark Sanchez 博士，总裁/创始人 |
| tops Software | |
| topsortho.com | || 从最简单的 GUI 设计任务到深入操作系统最深层角落的工作，Big Nerd Ranch 应该是您在 Mac/iPhone 咨询领域虚拟通讯录的首选联系人。毫不夸张地说，Aaron Hillegass 简直是 Cocoa 编程的教科书级（字面意思是写了这本书），将他及其团队的专业知识应用到您的应用程序中，您再没有更更好的选择了。我还没有合作过任何像 Big Nerd Ranch 这样能力出众且沟通畅的咨询公司。简单来说，这些家伙非常靠谱。 |
| | -- Glenn Zelniker，首席执行官 |
| Z-Systems Audio Engineering | |
| www.z-sys.com | |
| 我们寻求 Big Nerd Ranch 将 Teavana 的理念转化为 iPhone 应用程序。他们不仅是开发者，更是我们的合作伙伴，让应用程序比我们单方面想象的更好。最终的应用程序没有任何 Bug，且运行完全符合预期。我绝对推荐 Big Nerd Ranch，并对他们的工作赞不绝口。 |
| | -- Jay Allen，电子商务副总裁 |
| Teavana Corporation | |
| www.teavana.com | |

## 软件：精雕细琢的应用程序

Big Nerd Ranch 是领先的可下载移动端和桌面 Mac 应用程序开发商。我们最引人注目的 iPhone 和桌面应用程序可以在 iTunes 商店购买。

### 移动应用程序

智能手机已开始接管手机市场。自 iPhone 诞生以来，我们已为客户创建了数十个应用程序，现在拥有一自己的应用程序阵容，包括游戏、工具、音乐和教育类应用。作为不断发展的技术前沿，Big Nerd Ranch 致力于保持领先地位。

### 移动应用

世界已进入移动时代。如果您的公司没有移动应用程序，您就落后了。截至 2011 年初，iTunes 应用商店已增长到近 400,000 个应用程序，Android 市场已攀升至 250,000 个应用程序。Google 发布了其 Android 平台及其自带的应用商店，数十家手机制造商已宣布了搭载 Android 系统的设备。RIM 推出了 App World，Palm 有自己的 Palm Store，诺基亚推出了 Ovi（其在线商店），微软发布了 Windows Marketplace。

虽然 iOS 市场仍处于领先地位，但它给出了一些惊人的数据：

*   iOS 应用商店总下载量：103 亿。
*   iPhone 应用程序以每天 3000 万的速度被下载。
*   截至 2011 年初，当应用商店达到 100 亿下载量时，其花费的时间仅为 iTunes 商店歌曲达到相同目标的一半（31 个月对比 67 个月）。
*   目前 iPhone/iPad/iPod touch 的平均下载应用数量超过了 60 个。

## 书籍：Big Nerd 指南系列

在 Big Nerd Ranch，我们的哲学和对教育的热爱延伸到了我们的书中。访问 `www.bignerdranch.com/books` 查看目前出售的 Big Nerd Ranch 书籍。

## 联系 Big Nerd Ranch

访问我们的网站 `www.bignerdranch.com/`。

如需获取 Big Nerd Ranch 现场培训方案，请致电我们：404.478.9005。

![Contact the Big Nerd Ranch](img/00113.jpg)

