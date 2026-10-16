
# 第2章 主要编程语言的演变

```
02 RL-ITEM-NO              PICTURE IS Z(5).
02 FILLER                  PICTURE IS X(5).
02 RL-ITEM-DESC            PICTURE IS X(20).
02 FILLER                  PICTURE IS X(5).
02 RL-UNIT-PRICE           PICTURE IS ZZZ.99.
02 FILLER                  PICTURE IS X(5).
02 RL-AVAILABLE-STOCK      PICTURE IS Z(5).
02 FILLER                  PICTURE IS X(5).
02 RL-REORDER-POINT        PICTURE IS Z(5).
02 FILLER                  PICTURE IS X(5).
02 FILLER                  PICTURE IS X(71).

WORKING-STORAGE SECTION.
01  SWITCHES.
    02 CARD-EOF-SWITCH      PICTURE IS X.
01  WORK-FIELDS.
    02 AVAILABLE-STOCK      PICTURE IS 9(5).

PROCEDURE DIVISION.
000-PRODUCE-REORDER-LISTING.
    OPEN INPUT BAL-FWD-FILE.
    OPEN OUTPUT REORDER-LISTING.
    MOVE "N" TO CARD-EOF-SWITCH.
    PERFORM 100-PRODUCE-REORDER-LINE
        UNTIL CARD-EOF-SWITCH IS EQUAL TO "Y".
    CLOSE BAL-FWD-FILE.
    CLOSE REORDER-LISTING.
    STOP RUN.

100-PRODUCE-REORDER-LINE.
    PERFORM 110-READ-INVENTORY-RECORD.
    IF CARD-EOF-SWITCH IS NOT EQUAL TO "Y"
        PERFORM 120-CALCULATE-AVAILABLE-STOCK
        IF AVAILABLE-STOCK IS LESS THAN BAL-REORDER-POINT
            PERFORM 130-PRINT-REORDER-LINE.

110-READ-INVENTORY-RECORD.
    READ BAL-FWD-FILE RECORD
        AT END
            MOVE "Y" TO CARD-EOF-SWITCH.

120-CALCULATE-AVAILABLE-STOCK.
    ADD BAL-ON-HAND BAL-ON-ORDER
        GIVING AVAILABLE-STOCK.

130-PRINT-REORDER-LINE.
    MOVE SPACE             TO REORDER-LINE.
    MOVE BAL-ITEM-NO        TO RL-ITEM-NO.
    MOVE BAL-ITEM-DESC      TO RL-ITEM-DESC.
    MOVE BAL-UNIT-PRICE     TO RL-UNIT-PRICE.
```

## 2.7 分时的开端：Basic

Basic（Mather 和 Waite，1971）是另一种被广泛使用但很少得到尊重的编程语言。和 COBOL 一样，它在很大程度上被计算机科学家忽视。同样与 COBOL 类似，它在最初版本中并不优雅，只包含很少的一组控制语句。

Basic 在 20 世纪 70 年代末和 80 年代初的微型计算机上非常流行。这直接源于早期版本 Basic 的两个主要特点：它对于初学者（尤其是那些非理科导向的人）来说容易学习，而且较小的方言可以在内存很小的计算机上实现。⁶ 随着微型计算机能力的增强和其他语言的实现，Basic 的使用逐渐减少。20 世纪 90 年代初，随着 Visual Basic（微软公司，1991）的出现，Basic 的使用开始强劲复苏。

### 2.7.1 设计过程

Basic（初学者通用符号指令代码）最初由两位数学家 John Kemeny 和 Thomas Kurtz 在新罕布什尔州的达特茅斯学院（现达特茅斯大学）设计。他们在 20 世纪 60 年代初为 Fortran 和 ALGOL 60 的各种方言开发了编译器。他们的理科学生在学习或使用这些语言时通常几乎没有困难。然而，达特茅斯主要是一所文理学院，理工科学生仅占学生总数的约 25%。1963 年春天，他们决定专门为文科学生设计一种新语言。这种新语言将使用终端作为计算机访问的方法。该系统的目标如下：

1. 必须让非理科学生易于学习和使用。
2. 必须“令人愉快且友好”。
3. 必须为作业提供快速周转。
4. 必须允许自由且私密的访问。
5. 必须认为用户时间比计算机时间更重要。

> 6. 一些早期微型计算机包含驻留在 4096 字节 ROM 中的 Basic 解释器。

最后一个目标确实是一个革命性的概念。它至少部分基于这样一种信念：随着时间的推移，计算机会变得明显更便宜，事实也确实如此。

第二个、第三个和第四个目标的结合促成了 Basic 的分时特性。在 20 世纪 60 年代初，只有通过终端为大量同时使用的用户提供单独访问，才能实现这些目标。

1963 年夏天，Kemeny 开始着手第一个 Basic 版本的编译器，通过远程访问 GE 225 计算机。Basic 操作系统的设计和编码始于 1963 年秋天。1964 年 5 月 1 日凌晨 4 点，第一个使用分时 Basic 的程序被输入并运行。到 6 月，系统上的终端数量增加到 11 个，到秋天已激增至 20 个。

### 2.7.2 语言概述

最初的 Basic 版本非常小，而且奇怪的是，它不是交互式的：执行中的程序无法从用户那里获取输入数据。程序以某种批处理方式输入、编译和运行。最初的 Basic 只有 14 种不同的语句类型和一种数据类型——浮点型。由于人们认为目标用户中很少会有人理解整数类型和浮点类型之间的区别，所以该类型被称为“数字”。总体而言，它是一种非常受限的语言，尽管相当容易学习。

### 2.7.3 评价

原始 Basic 最重要的方面在于，它是第一个通过连接远程计算机的终端来使用的广泛使用的语言。⁷ 终端在当时刚刚开始可用。在那之前，大多数程序是通过穿孔卡片或纸带输入计算机的。

Basic 的许多设计来自 Fortran，并受到 ALGOL 60 语法的一些次要影响。后来，它以多种方式发展，几乎没有对其标准化做出任何努力。美国国家标准协会（ANSI，1978b）发布了 Minimal Basic 标准（ANSI，1978b），但这只代表了语言特性的最低限度。事实上，最初的 Basic 与 Minimal Basic 非常相似。

尽管可能令人惊讶，但数字设备公司（DEC）在 20 世纪 70 年代使用了一个相当精致的 Basic 版本，名为 Basic-PLUS，来编写其为 PDP-11 小型计算机开发的最大的操作系统 RSTS 的重要部分。

> 7. Lisp 最初也通过终端使用，但在 20 世纪 60 年代初并未被广泛使用。

Basic 一直因其编写的程序结构不佳而受到批评，以及其他方面。根据第1章讨论的评价标准，特别是可读性和可靠性，该语言确实表现得很差。显然，该语言的早期版本并非旨在用于任何重要规模的严肃程序，也不应该被这样使用。后来的版本更适合这类任务。

20 世纪 90 年代 Basic 的复兴是由 Visual Basic（VB）的出现推动的。VB 被广泛使用，很大程度上是因为它提供了一种构建图形用户界面（GUI）的简单方法，因此得名 Visual Basic。当 .NET 出现时，一个新的 VB 版本也随之而来，即 VB.NET。虽然它与早期 VB 版本有显著不同，但它迅速取代了旧语言。也许 VB 与 .NET 版本之间最重要的区别在于，后者完全支持面向对象的编程。

下面是 Basic 程序示例：

```
REM  Basic Example Program
REM  Input:  An integer, listen, where listen is less
REM          than 100, followed by listen-integer values
REM  Output: The number of input values that are greater
REM          than the average of all input values

DIM intlist(99)
result = 0
sum = 0
INPUT listen
IF listen > 0 AND listen < 100 THEN
    REM Read input into an array and compute the sum
        FOR counter = 1 TO listen
            INPUT intlist(counter)
            sum = sum + intlist(counter)
        NEXT counter
    REM Compute the average
        average = sum / listen
    REM Count the number of input values that are > average
        FOR counter = 1 TO listen
            IF intlist(counter) > average
                THEN result = result + 1
        NEXT counter
    REM Print the result
        PRINT "The number of values that are > average is:";
              result
ELSE
    PRINT "Error-input list length is not legal"
END IF
END
```

## 用户设计与语言设计

畅销书 *《About Face：用户界面设计精髓》* 的作者艾伦·库珀，在可以被称得上是最关心用户界面设计的语言——Visual Basic 的设计中也发挥了重要作用。对他来说，这一切归结为一种使技术人性化的愿景。

![](img/e382387aad0004c80a0dd0a70be9a623_87_0.png)

## 关于 Basic 的一些信息

**你是怎么开始这一切的？** 我高中辍学，在加州的一所社区大学获得了编程专业的副学士学位。我的第一份工作是在旧金山的美洲总统轮船公司（美国历史最悠久的海运公司之一）担任程序员。除了零零散散的几个月外，我一直都是自雇人士。

**你目前的工作是什么？** Cooper 公司的创始人和董事长，这家公司致力于使技术人性化（www.cooper.com）。

**你最喜欢的工作是什么？** 交互设计顾问。

**你在语言设计和用户界面设计领域非常知名。对于设计语言与设计软件，或者设计其他任何东西，有什么想法吗？** 在软件领域几乎是一样的：了解你的用户。

## 关于早期的 Windows 版本

**在 20 世纪 80 年代，你开始使用 Windows，并谈到被它的优点所吸引：图形用户界面支持和动态链接库，后者让你能够创建自我配置的工具。你最终帮助塑造了 Windows 的哪些部分？** 微软在 Windows 中对实用多任务处理的支持给我留下了深刻印象。这包括动态重定位和进程间通信。

`MSDOS.exe` 是 Windows 最初几个版本的 shell 程序。它是一个很糟糕的程序，我相信它可以大幅改进，而我就是做这件事的人。在业余时间，我立刻开始编写一个比 Windows 自带 shell 更好的 shell 程序。我把它叫做 Tripod。微软最初的 shell `MSDOS.exe` 是 Windows 初期成功的主要绊脚石之一。Tripod 试图通过更易于使用和配置来解决这个问题。

**那个“啊哈！”时刻是什么时候？** 直到 1987 年底，当我在采访一位企业客户时，Tripod 的关键设计策略突然出现在我的脑海中。当这位 IS 经理向我解释他需要为不同的用户群创建和发布各种各样的 shell 解决方案时，我意识到一个难题：并不存在理想的 shell。每个用户都需要他们自己的个人 shell，根据他们自己的需求和技能水平进行配置。一瞬间，我找到了 shell 设计问题的解决方案：它将是一个 shell 构造套件；一种工具，每个用户都能精确地构建出适合自己独特应用和培训组合所需的 shell。

**个性化的 shell 这个想法有什么吸引人之处？** 不是我告诉用户理想的 shell 是什么，而是他们可以设计自己的、个性化的理想 shell。通过可定制的 shell，程序员可以创建一个功能强大且范围广泛但也有些危险的 shell；而 IT 经理可以创建一个可以交给前台文员的 shell，只暴露该文员使用的少数几个特定应用工具。

你是如何从一个外壳程序写到与微软合作的？Tripod 和 Ruby 是同一个东西。在我与比尔·盖茨签下协议后，我把原型的名字从 Tripod 改成了 Ruby。然后，我按照原型应有的用法使用了 Ruby 原型：作为构建发布级代码的一次性模型。我就是这么做的。微软拿走了 Ruby 的发布版本，并向其中加入了 QuickBasic，从而创造了 VB。所有这些最初的创新都来自 Tripod/Ruby。

> `MSDOS.exe` 是 Windows 最初几个版本的外壳程序。它是一个糟糕的程序，而我相信它可以被大幅改进，而且我就是那个能做到的人。在业余时间，我立刻开始编写一个比 Windows 自带的更好的外壳程序。

## Ruby：Visual Basic 的孵化器

让我们重新回顾你对早期 Windows 以及那个 DLL 特性的兴趣。DLL 不是一种实物，而是操作系统的一种机制。它允许程序员构建可在运行时链接的代码对象，而不仅仅是在编译时链接。正是这一点让我发明了 VB 中可动态扩展的部分，第三方供应商可以添加控件。

Ruby 产品体现了软件设计中的许多重大进步，但其中有两点尤为成功。如前所述，Windows 的动态链接能力一直让我着迷，但拥有工具和知道如何利用它们是两回事。凭借 Ruby，我最终找到了动态链接的两个实际用途，而最初的程序就包含了这两者。第一，这种语言既可安装，又可以被动态扩展。第二，控件面板可以被动态添加。

你的 Ruby 语言是第一个拥有动态链接库并链接到可视化前端的语言吗？据我所知，是的。

用一个简单的例子来说，这能让程序员对其程序做些什么？从第三方供应商那里购买一个控件，例如网格控件，将其安装到自己的电脑上，然后让这个网格控件作为语言的一个组成部分出现，包括在可视化编程前端中。

为什么人们称你为“Visual Basic 之父”？Ruby 自带一种小巧的语言，只适合执行外壳程序所需的十来个简单命令。然而，这种语言是以一系列 DLL 的形式实现的，任意数量的 DLL 都可以在运行时安装。内部解析器会识别一个动词，然后沿着 DLL 链传递它，直到其中一个 DLL 确认自己知道如何处理该动词。如果所有 DLL 都无法处理，就会产生语法错误。从我们最早的讨论开始，微软和我本人都考虑过扩展这种语言，甚至有可能完全用一门“真正的”语言来替换它。C 语言是最常被提及的候选者，但最终，微软利用这个动态接口拔掉了我们的小型外壳语言，并用 QuickBasic 完全替换了它。这种语言与可视化前端的新结合是静态且永久的，尽管最初的动态接口使这种耦合成为可能，但它在这个过程中丢失了。

## 对新想法的一些最终评论

在编程和编程工具（包括语言和环境）领域，哪些项目最让你感兴趣？我有兴趣创建旨在帮助用户而非程序员的编程工具。

最需要牢记的关键规则、名言或设计理念是什么？桥梁不是工程师建造的，而是铁工建造的。同样，软件程序不是工程师建造的，而是程序员建造的。

## 2.8 面向所有人的一切：PL/I

PL/I 代表了首次大规模尝试设计一种可用于广泛应用程序领域的语言。此前所有语言以及后来大多数语言都专注于某一特定应用领域，例如科学、人工智能或商业。

### 2.8.1 历史背景

与 Fortran 类似，PL/I 也是作为 IBM 的产品开发的。到 20 世纪 60 年代初，工业界计算机用户已分为两个截然不同的阵营：科学计算和商业应用。从 IBM 的角度来看，科学计算程序员可以使用大型 IBM 7090 或小型 IBM 1620 计算机。这一群体广泛使用浮点数据和数组。Fortran 是主要语言，但也使用了一些汇编语言。他们有自己的用户组 SHARE，并且与从事商业应用的人几乎没有接触。

对于商业应用，人们使用大型 IBM 7080 或小型 IBM 1401 计算机。他们需要十进制和字符串数据类型，以及精细且高效的输入输出设施。他们使用 COBOL，尽管在 1963 年初 PL/I 的故事开始时，从汇编语言到 COBOL 的转换还远未完成。这类用户也有自己的用户组 GUIDE，并且很少与科学计算用户接触。

1963 年初，IBM 的规划者们觉察到这种情况开始发生变化。这两个此前彼此疏远的计算机用户群体正朝着彼此靠拢，而这种方式被认为必然会产生问题。科学家们开始收集大量待处理的数据文件。这些数据需要更复杂、更高效的输入输出设施。商业应用人员开始使用回归分析来构建管理信息系统，这需要浮点数据和数组。局面开始变得明朗：计算设施很快将需要两台独立的计算机和两组技术人员，以支持两种截然不同的编程语言。
