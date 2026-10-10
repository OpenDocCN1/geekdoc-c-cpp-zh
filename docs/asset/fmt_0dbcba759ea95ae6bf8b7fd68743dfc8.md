
# C++ 终极指南（第5版）

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_4_0.png)

# Walter Savitch

加利福尼亚大学圣地亚分校

贡献者

# Kenrick Mock

阿拉斯加大学安克雷奇

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_4_1.png)

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_5_0.png)

# 前言

本书旨在设计作为 C++ 语言编程的教材和参考书。尽管它包含了编程技术，但它是围绕 C++ 语言的特征组织的，而不是围绕任何特定的技术课程。我设想的主要读者群是没有 C++ 语言广泛编程经验的本科生。因此，这本书是广泛用户的合适 C++ 教材或参考书。介绍性章节的编写水平初学者易于理解，这些章节中的框部分旨在向经验更丰富的程序员介绍基础的 C++ 语法。后面的章节初初来说也可以理解的，但其编写水平适合已进展到更高级主题的人。《绝对 C++》也适合任何自学 C++ 语言的人。（对于那些想要带有更多教学材料和非常基础编程的教材的人，请尝试我的《Problem Solving with C++, Eighth Edition》，Pearson Education 出）。

书中对 C++ 的涵盖远超初学者需要了解的内容。特别是，它对继承、多态、异常处理和标准模板库 (`STL`) 有广泛涵盖，以及对模式和统一建模语言 (`UML`) 有基础涵盖。

# 本版变化

第五版呈现了与第四版相同的编程哲学。对于讲师来说，你可以教授相同的课程，以相同的顺序介绍相同的主题，而涵盖的内容或分配的章节没有变化。变化包括：

- 第 1 章包含了对字符串类类的简要介绍，第 12 章包含了一个关于使用 `iostream` 将字符串和其他类型转换的章节。
- 新增了 25 道新的自测练习，第 13 章简要描述了递归。
- 修正了第四版中发现的几个错误。
- 书中新增了 15 个新的 VideoNotes (`www.pearsonhigher.com/savitch`)，总共 46 个。这些 VideoNotes 演示了解决问题和编码的过程以强化关键概念。当有视频时，书的页边缘会出现一个图标。

# ANSI/ISO C++ 标准

本版完全兼容最新 ANSI/ISO 标准的编译器。

# 标准模板库

标准模板库 (`STL`) 是预编程结构化类和算法的广泛集合。`STL` 也许是一个与核心语言一样大的课题，因此我包含了对 `STL` 的大量介绍。书中有一个关于模板通用主题的完整章节，和一个关于 `STL` 细节的章节，在文中其他地方还有其他相关的材料。

# 面向对象编程

本书围绕 C++ 的结构组织。因此，早期章节涵盖了 C++ 的某些高级编程语言共有的方面，但并非特别面向面向对象编程 (`OOP`)。对于一本参考书——以及一本学习第二语言的书来说，这是合理的。然而，我认为 C++ 是一种 `OOP` 语言。如果你在用 C++ 编程而不是 C，你必须正在使用 C++ 的 `OOP` 特性。这对 C++ 语言中实现的封装、继承和多态提供了广泛涵盖。第 20 章关于模式和 `UML` 提供了对 `OOP` 相关材料的额外涵盖。

# 主题顺序的灵活性

本书允许讲师在重新安排材料方面有很大的自由。这对于本书作为参考书是非常重要的。这也符合我迎合讲师风格的哲学，而不是将讲师束缚在我个人的主题顺序偏好。每个章节的介绍介绍了涵盖该章节每个节之前必须涵盖哪些内容。

# 利于学生理解

一本书以正确的顺序呈现主题是不够的。对于讲师来说，准确清晰也不够的。材料还需要以一种初学者易于理解的方式呈现。就像我的其他证明深受学生欢迎的教科书一样，这本书的编写旨在对学生友好且易于理解。

# 总结框

每个要点都在一个框部分进行了总结。这些框部分贯穿每个章节。它们作为材料的总结、快速参考源，以及快速学习你大致了解但不知道细节的 C++ 语法的方法。

### 自测练习

每个章节都包含大量的自测练习。所有自测练习的完整答案都在每个章节的最后。

# 前言

# 视频笔记 (VIDEO NOTES)

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_8_0.png)

视频笔记（VideoNotes）是逐步引导的视频，旨在引导读者解决章节末的习题或进一步阐述文中介绍的概念。文中的图标表示该主题有视频笔记提供强化支持。完全可导航的问题允许学生按照自己的进度进行学习。视频笔记位于 `www.pearsonhigher.com/savitch`。

# 其他功能

每章中都提供了“陷阱”（Pitfall）章节、“编程技巧”（programming technique）章节以及带有示例输入输出的完整程序示例。每章都以总结和编程项目合集结束。

# 通过 MyProgrammingLab 进行在线练习与评估

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_8_1.png)

`MyProgrammingLab` 帮助学生全面掌握编程的逻辑、语义和语法。通过练习题和即时的个性化反馈，`MyLabLab` 提高了那些对主流高级编程语言的基础概念和范式感到困难的初学者的能力。

作为一个自学和作业工具，`MyProgrammingLab` 由数百个根据本书书结构组织的小型练习题组成。对于学生来说，系统会自动检测其提交代码中的逻辑和语法错误，并提供针对性的提示，使学生能够弄清楚错误在哪里以及为什么。对于教师来说，全面的成绩本可以记录正确和错误的答案，并存储学生输入的代码。

`MyProgrammingLab` 与 Turing’s Craft（CodeLab 交互式编程练习系统的开发者）合作向本书的用户提供服务。如需查看完整演示、查看教师和学生的反馈，或在您的课程中使用 `MyProgrammingLab`，请访问 `www.myprogramming.com`。

# 支持材料

所有本书的用户都可以在 `www.pearsonhigher.com/support` 获取以下支持材料：

- 本书源代码

仅限合规教师在 `www.pearsonhigher.com/irc` 获取以下资源（请联系您的当地销售代表）：

- 教师讲义
- PowerPoint® 幻灯片

前言

# 致谢

许多个人对本书的出版提供了无私帮助和支持。我非常感谢 Addison-Wesley 出版公司的 Frank Rugg 和 Susan Hartman，他们构思了第一、第二、第三和第四版。特别感谢 Matt Goldstein、Chelsea Kharakon、M Lloyd 以及 Pearson Education 的其他人，他们的支持对项目的成功至关重要。

我感谢所有审稿人的辛勤工作：

- Richard Albright
- Jerry K. Bilbey, Jr
- Albert M. Cheng
- David Cherba
- Frederick H. Colch
- Stephen Corbesero
- Christopher E. Cramer
- Ron DiNapoli
- Martin Dulberg
- Evan Golub
- Terry Harvey
- Joanna Klukowska
- Lawrence S. Kroll
- Alvin Sim
- Tim H. Lin
- R. M. Lowe
- Jeffrey Popyack
- Amar Raheja
- Victoria Rayskin
- Loren Rhodes
- Francis Marion
- University of Delaware
- University of Houston
- Michigan State University
- Colorado Technical University
- Moravian College
- Cornell University
- Pennsylvania State University
- North Carolina State University
- University of Maryland
- Hunter College (CUNY)
- San Francisco State University
- Florida State University
- Auburn University
- Cal Poly Pomona
- Drexel University
- University of Central Angeles
- Juniata College
- University of Michigan
- Victor Shtern
- University of Notre Dame
- Chrysafis Vogiatzis
- Joel Weinstein
- Northeastern University
- Dick Whalen
- Southern Maryland

特别感谢 Kenrick Mock（阿拉斯加安科奇大学），他执行了本版本的更新。我再次感谢他付出了非常出色的工作。

Walter Savitch

# 文中视频笔记位置

`www.pearsonhighered.com/savitch`

此页特意留白

xxiv 目录

- 节点 733
- 在列表头插入节点 740

### 17.4 树 800

- 自测题答案 809
- C++ 与面向对象编程 3
- C++ 术语 4
- 赋值兼容性 15
- 整数与浮点数除法 21

`#include <iostream>`

```
int main()
```
下一行表示 `main` 是一个没有参数并返回 `int`（整数）值的函数：

```
某些编译器允许你省略 int 或将其替换为 void，表示一个不返回值的函数。然而，之前的形式是启动 C++ 程序主函数最广泛接受的形式。程序以执行以下语句结束：
return 0;
```

```
该语句结束 main 函数的调用并返回 0 作为函数的值。根据 ANSI/ISO C++ 标准，这不是要求的，但许多编译器会要求。第 3 章将涵盖所有关于 C++ 函数的细节。
C++ 基础
你在 C++ 中进行 C 风格的内存管理。但是 C++ 也有它自己的内存管理语法。大多数编译器将允许他的或她的垃圾回收。
```

## 显示 1.1 示例 C++ 程序

```cpp
#include <iostream>

using namespace std;

int main() {
    int numberOfLanguages;
    cout << "Hello reader.\n";
    cout << "Welcome to C++.\n";
    cout << "How many programming languages have you used? ";
    cin >> numberOfLanguages;
    if (numberOfLanguages < 1) {
        cout << "Read the preface. You may prefer\na more elementary book by the same author.\n";
    } else {
        cout << "Enjoy the book.\n";
    }
    return 0;
}
```

### 示例对话 1

你好。
欢迎来到 C++。
你用过多少种编程语言？
请阅读序言。你可能更喜欢同一作者写的更入门的书。

> 用户在键盘上输入了 0。
用户输入以**粗体**显示。

### 示例对话 2

你好。
欢迎来到 C++。
你用过多少种编程语言？
好好看书。

> 用户在键盘上输入了 1。
用户输入以**粗体**显示。

C++ 中的变量声明与其他许多通用编程语言中的的。显示 1.1 中的下面这一行声明了变量 `numberOfLanguages`：

```cpp
int numberOfLanguages;
```

`int` 类型是 C++ 中整数（integers）类型之一。

如果你以前没有写过 C++ 程序，那么使用 `cin` 和 `cout` 进行控制台输入/输出对你来说可能是新鲜的。这个主题在本章的稍后部分会有介绍，但从这个示例程序可以观察到基本思想。例如，考虑显示 1.1 中的两行：

```cpp
cout << "How many programming languages have you used? ";
cin >> numberOfLanguages;
```

第一行将引号内的文本输出到屏幕上。引号内的文本被称为字符串，或者更准确地说，是 C 字符串。第二行读取用户在键盘上输入的数字，并将变量 `numberOfLanguages` 的值设置为该数字。

```cpp
cout << "Read the preface. You may prefer\n"
 << "a more elementary book by the same author.\n";
```

输出多个字符串而不仅仅是一个。详细将在在本章后的第 1.3 节中解释，但这段简短的介绍将使能够理解 1.3 节之前示例中 `cin` 和 `cout` 的简单用法。符号 `\n` 是换行符，指示计算机开始新行输出。

尽管你可能不确定编写语句的具体细节，但你可能可以猜测 `if-else` 语句的意思。你需要的细节应该阅读序言，看看你是否更喜欢更入门的书。

（顺便说一下，如果你还没有至少一些编程语言的经验，你应该阅读序言，看看你是否更喜欢更入门的书。阅读这本书不需要具有过任何 C++ 经验，但强烈建议具备一些基础的编程经验。）

## 1.2 变量、表达式和赋值语句

一旦人们理解了变量在编程中的用法，他们就理解了编程的精髓。

> E. W. DIJKSTRA, 《结构化编程笔记》

C++ 中的变量、表达式和赋值与许多其他通用语言中的相似。

### 标识符

变量的名称（或你在程序中定义的其他项目）被称为标识符。C++ 标识符必须以字母或下划线符号开头，其余部分必须是字母、数字或下划线符号。例如，以下都是合法的：

```
x x1 x1 _abc ABC123z7 sum RATE count2 bigBonus
```

所有名称都是合法的，并将被编译器接受，但前五个是标识符的糟糕选择，因为它们不符合标识符的使用习惯。以下任何一个都是不合法的，并将被编译器拒绝：

```
12 3X %change data-1 myfirst.c PROG_CPP
```

前三个是不允许的，因为它们不是以字母或下划线开头。其余三个不是标识符，因为它们包含了字母、数字和下划线符号以外的符号。

虽然以下划线开头是法的，但你应该避免这样做，因为以下划线开头的标识符通常被保留给系统标识符和标准库。

C++ 是一种大小敏感的语言：也就是说，它在标识符拼写中区分大写字母和小写字母。因此，以下三个不同的标识符可以用于命名三个不同的变量：

```
rate RATE Rate
```

然而，在同一个程序中使用这样的变体并不是好主意，因为这可能会引起混乱。虽然 C++ 没有强制要求，但变量通常用小写字母拼写。预定义的标识符，如 `main`、`cin` 和 `cout`，必须全小写字母拼写。现在在面向对象编程中正变得通用的惯例是使用大小写字母（以及数字）混合拼写变量名，始终以小写字母开始变量名，并用大写字母指示“单词”边界，如下例变量名所示：

```
topSpeed, bankRate1, bankRate2, timeOfArrival
```

这种习惯在 C++ 中不像在其他一些面向对象的语言那样常见，但正在被更广泛的使用并且是一种值得遵循的习惯。

C++ 标识符可以是任何长度，尽管某些编译器会忽略某些指定的（长度）初始字符之后的字符。

### 标识符

C++ 标识符必须以字母或下划线符号开头，剩余字符必须是字母、数字或下划线符号。C++ 标识符区分大小写，且长度没有限制。

# 第1章 C++ 基础

### 关键字或保留字

有一类特殊的标识符，被称为**关键字**（keywords）或**保留字**（reserved words），它们在 C++ 中有预定义的含义且不能用作变量或其他任何内容的名称。在代码显示中，这些关键字以不同的颜色显示。关键字的完整列表见附录 1。
如 `in` 和 `cout` 等单词不是关键字。这些预定义的单词不是 C++ 核心语言的一部分，你允许重新定义它们。虽然这些预定义的单词不是关键字，但它们定义在 C++ 语言标准要求的库中。不说说，将预定义标识符用于其标准含义之外的任何用途都可能导致混乱和危险，因此应该避免。最安全、最简单的方法是将预定义标识符视为关键字对待。

### 变量

C++ 程序中的每个变量在使用之前都必须被**声明**（declared）。当你**声明**一个变量时，你是在告诉编译器——以及计算机——你将在变量中存储什么类型的数据。例如，以下是可能出现在 C++ 程序中的两种定义：

```cpp
int numberOfLanguages;
double oneWeight, totalWeight;
```
