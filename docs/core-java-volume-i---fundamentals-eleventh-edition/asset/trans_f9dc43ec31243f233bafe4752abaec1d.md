
数字。程序清单 9.8 用 Java 编程语言列出了这个程序，而程序清单 9.9 是 C++ 代码。

![](img/127bccebb2cfadea3f02579edaad63c3_587_0.png)

> **注意：** 即使筛法并不是一个很好的基准测试，我们还是忍不住对算法的两种实现进行了计时。以下是使用 i7-8550U 处理器和 16 GB 内存、运行 Ubuntu 17.10 的计时结果：
>
> - C++（g++ 7.2.0）：173 毫秒
> - Java（Java 11.0.1）：41 毫秒

我们已在 *Java 核心技术* 的十个版本中运行过这项测试，而在最近六个版本中，Java 轻松胜过 C++。平心而论，如果把 C++ 编译器的优化级别调高，它能以 34 毫秒的成绩胜过 Java。只有当程序运行时间足够长，从而触发 HotSpot 即时编译器时，Java 才能与之匹敌。

### 程序清单 9.8 `sieve/Sieve.java`

```java
package sieve;

import java.util.*;

/**
 * This program runs the Sieve of Eratosthenes benchmark. It computes all primes
 * up to 2,000,000.
 * @version 1.21 2004-08-03
 * @author Cay Horstmann
 */
public class Sieve
{
   public static void main(String[] s)
   {
      int n = 2000000;
      long start = System.currentTimeMillis();
      var bitSet = new BitSet(n + 1);
      int count = 0;
      int i;
      for (i = 2; i <= n; i++)
         bitSet.set(i);
      i = 2;
      while (i * i <= n)
      {
         if (bitSet.get(i))
         {
            count++;
            int k = 2 * i;
            while (k <= n)
            {
               bitSet.clear(k);
               k += i;
            }
         }
         i++;
      }
      while (i <= n)
      {
         if (bitSet.get(i)) count++;
         i++;
      }
      long end = System.currentTimeMillis();
      System.out.println(count + " primes");
      System.out.println((end - start) + " milliseconds");
   }
}
```

### 程序清单 9.9 `sieve/sieve.cpp`

```cpp
/**
   @version 1.21 2004-08-03
   @author Cay Horstmann
*/

#include <bitset>
#include <iostream>
#include <ctime>

using namespace std;

int main()
{
    const int N = 2000000;
    clock_t cstart = clock();

    bitset<N + 1> b;
    int count = 0;
    int i;
    for (i = 2; i <= N; i++)
        b.set(i);
    i = 2;
    while (i * i <= N)
    {
        if (b.test(i))
        {
            count++;
            int k = 2 * i;
            while (k <= N)
            {
                b.reset(k);
                k += i;
            }
        }
        i++;
    }
    while (i <= N)
    {
        if (b.test(i))
            count++;
        i++;
    }

    clock_t cend = clock();
    double millis = 1000.0 * (cend - cstart) / CLOCKS_PER_SEC;

    cout << count << " primes\n" << millis << " milliseconds\n";

    return 0;
}
```

至此，我们对 Java 集合框架的巡览就结束了。如你所见，Java 类库提供了种类繁多的集合类，以满足你的编程需求。在下一章中，你将学习如何编写图形用户界面。

## 图形用户界面编程

### 本章内容

- 10.1 Java 用户界面工具包的历史，第 565 页
- 10.2 显示框架，第 567 页
- 10.3 在组件中显示信息，第 574 页
- 10.4 事件处理，第 598 页
- 10.5 Preferences API，第 624 页

Java 诞生之时，大多数计算机用户还在与图形桌面应用程序交互。如今，基于浏览器的应用程序和移动应用程序要常见得多，但仍有一些时候，提供桌面应用程序会很有用。在本章和下一章中，我们将讨论使用 Swing 工具包进行用户界面编程的基础知识。另一方面，如果你打算只将 Java 用于服务器端编程，并且对编写 GUI 程序不感兴趣，那么完全可以放心跳过这两章。

### 10.1 Java 用户界面工具包的历史

Java 1.0 问世时，包含一个用于基本 GUI 编程的类库，称为抽象窗口工具包（AWT）。基本的 AWT 库通过将用户界面元素的创建和行为委托给每个目标平台（Windows、Linux、Macintosh 等）上的原生 GUI 工具包来处理这些元素。例如，如果你使用最初的 AWT 在 Java 窗口中放置一个文本框，实际处理文本输入的是底层的一个“对等”文本框。由此得到的程序理论上可以运行在任何这些平台上，并具有目标平台的“外观与感觉”。

这种基于对等机制的方法对于简单应用程序来说效果很好，但很快就发现，编写一个依赖于原生用户界面元素的高质量可移植图形库是极其困难的。菜单、滚动条和文本字段等用户界面元素在不同平台上的行为可能会有细微差异。因此，用这种方法很难为用户提供一致且可预测的体验。此外，一些图形环境（例如 X11/Motif）没有 Windows 或 Macintosh 那样丰富的用户界面组件集合。这进一步限制了基于“最低共同标准”方法的可移植库。结果，用 AWT 构建的 GUI 应用程序根本不如原生 Windows 或 Macintosh 应用程序好看，也不具备这些平台的用户所期待的那种功能。更令人沮丧的是，AWT 用户界面库在不同平台上存在*不同的*缺陷。开发人员抱怨不得不在每个平台上测试自己的应用程序——这种做法被嘲讽地称为“一次编写，到处调试”。

1996 年，Netscape 创建了一个名为 IFC（Internet Foundation Classes）的 GUI 库，它采用了一种完全不同的方法。按钮、菜单等用户界面元素被*绘制*到空白窗口上。底层窗口系统唯一需要的功能就是能够创建一个窗口并在其上绘制。因此，无论程序在哪个平台上运行，Netscape 的 IFC 部件的外观和行为都相同。Sun Microsystems 与 Netscape 合作完善了这种方法，创建了一个代号为“Swing”的用户界面库。Swing 曾作为 Java 1.1 的扩展提供，并在 Java 1.2 中成为标准库的一部分。

Swing 现在是这种非对等机制 GUI 工具包的正式名称。

> **注意：** Swing 并不是 AWT 的完全替代品——它构建在 AWT 架构之上。Swing 只是为你提供了功能更强大的用户界面组件。每当你编写 Swing 程序时，都会用到 AWT 的基础——特别是事件处理。从现在起，当我们说“Swing”时，指的是“绘制型”用户界面类；当我们说“AWT”时，指的是窗口工具包的底层机制，例如事件处理。

Swing 必须费力地绘制用户界面的每一个像素。Swing 最初发布时，用户抱怨它很慢。（如果你在树莓派等硬件上运行 Swing 应用程序，仍然可以体会到这个问题。）过了一段时间，台式计算机变快了，用户又抱怨 Swing 很丑——确实，它已经落后于那些通过动画和花哨效果美化过的原生部件。更糟糕的是，Adobe Flash 越来越多地被用来创建具有更炫目效果的用户界面，而这些界面根本不使用原生控件。

2007 年，Sun Microsystems 推出了一个完全不同的用户界面工具包，称为 JavaFX，作为 Flash 的竞争者。它运行在 Java 虚拟机上，但有自己的编程语言，称为 JavaFX Script。该语言针对编写动画和花哨效果进行了优化。程序员抱怨需要学习一门新语言，于是纷纷避而远之。2011 年，Oracle 发布了新版本 JavaFX 2.0，它提供了 Java API，不再需要单独的编程语言。从 Java 7 更新 6 开始，JavaFX 已与 JDK 和 JRE 捆绑在一起。然而，在本书编写之时，Oracle 已宣布从版本 11 开始，JavaFX 将不再与 Java 捆绑。

由于本书介绍核心 Java 语言和 API，我们将重点讨论用于用户界面编程的 Swing。

> **提示：** 我们为你提供了一章介绍 JavaFX 的附赠章节。如果你拥有本书的印刷版，请从 http://horstmann.com/corejava 下载免费的 PDF。电子书将该章放在末尾。

### 10.2 显示框架

顶层窗口（即不包含在另一个窗口内部的窗口）在 Java 中称为*框架*。AWT 库有一个用于这种顶层窗口的类，称为 *Frame*。这个类的 Swing 版本称为 *JFrame*，它扩展了 *Frame* 类。*JFrame* 是少数不绘制在画布上的 Swing 组件之一。因此，装饰元素（按钮、标题栏、图标等）由用户的窗口系统绘制，而不是由 Swing 绘制。

> **警告：** 大多数 Swing 组件类都以“J”开头：JButton、JFrame 等。也有 Button 和 Frame 这样的类，但它们是 AWT 组件。如果你不小心漏掉了“J”，程序可能仍能编译和运行，但 Swing 和 AWT 组件的混用可能导致外观和行为不一致。
