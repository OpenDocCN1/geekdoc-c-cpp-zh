
## 图 8-4：
smallLetter 值的变化。

![](img/f938eba5f15e231d828a6255e7ec5523_173_0.png)

可以吗？你能承受忘记 smallLetter 曾经的值吗？是的，在清单 8-2 中，这样是可以的。在用以下语句为 bigLetter 分配值之后

```
bigLetter = Character.toUpperCase(smallLetter);
```

你可以完全忘记现有的 smallLetter 值。你不需要这样做：

// This code is cumbersome.
// The extra variables are unnecessary.
char smallLetter1, bigLetter1;
char smallLetter2, bigLetter2;

smallLetter1 = 'R';
bigLetter1 = Character.toUpperCase(smallLetter1);
System.out.println(bigLetter1);

smallLetter2 = '3';
bigLetter2 = Character.toUpperCase(smallLetter2);
System.out.println(bigLetter2);
```

你不需要将旧值和新值存储在单独的变量中。相反，你可以像清单 8-2 中那样重用变量 smallLetter 和 bigLetter。

这种变量重用并不会为你节省大量额外的输入。它也不会节省太多内存空间。但重用变量可以使程序更简洁。当你查看清单 8-2 时，你一眼就能看出代码有两个部分，并且你会看到这两个部分大致做着相同的事情。

清单 8-2 中的代码简单且易于管理。在这样一个小的程序中，简单性和可管理性并不很重要。但在大型程序中，仔细思考每个变量的使用是有帮助的。

## 何时不重用变量

上一节讨论了重用变量以使程序更简洁易读。本节展示了另一面。在本节中，手头的问题迫使你创建新的变量。

假设你正在编写代码来反转一个四字母单词中的字母。你将每个字母存储在其自己的单独变量中。清单 8-3 显示了代码，图 8-5 显示了代码的运行情况。

## 清单 8-3：让单词倒过来

```
import java.util.Scanner;

class ReverseWord {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        char c1, c2, c3, c4;

        c1 = keyboard.findWithinHorizon(".", 0).charAt(0);
        c2 = keyboard.findWithinHorizon(".", 0).charAt(0);
        c3 = keyboard.findWithinHorizon(".", 0).charAt(0);
        c4 = keyboard.findWithinHorizon(".", 0).charAt(0);

        System.out.print(c4);
        System.out.print(c3);
        System.out.print(c2);
        System.out.print(c1);
        System.out.println();

        keyboard.close();
    }
}
```

图 8-5：阻止那些 pots！

![](img/f938eba5f15e231d828a6255e7ec5523_174_0.png)

清单 8-3 中的技巧如下：

-   按顺序为变量 c1、c2、c3 和 c4 分配值。
-   以相反的顺序在屏幕上显示这些变量的值：c4、c3、c2，然后是 c1，如图 8-6 所示。

图 8-6：
使用四个变量。

![](img/f938eba5f15e231d828a6255e7ec5523_175_0.png)

如果你不使用四个单独的变量，那么你就得不到想要的结果。例如，想象一下你只用一个变量存储字符。你运行程序并输入单词 pots。当需要反向显示单词时，计算机记得单词 pots 中的最后一个 s。但计算机不记得 p、o 或 t，如图 8-7 所示。

图 8-7：
因为你只使用了一个变量而出错。

![](img/f938eba5f15e231d828a6255e7ec5523_175_1.png)

## 这所有 findWithinHorizon 乱七八糟的东西背后是什么？

不用陷入太多细节，这里就是 findWithinHorizon(".", 0).charAt(0) 技术的工作原理：

Java 的 findWithinHorizon 方法会在输入中查找内容。该方法找到的内容取决于你在括号中放入的内容。例如，对 findWithinHorizon("\\d\\d\\d", 0) 的调用会查找由三个数字组成的组。以下代码行

```
System.out.println(keyboard.
findWithinHorizon("\\d\\d\\d", 0));
```

我可以输入

Testing 123 Testing

计算机回应并显示

123

在调用 findWithinHorizon("\\d\\d\\d", 0) 中，每个 \\d 代表一个单独的数字。这种 \\d 业务是称为正则表达式的特殊代码中的众多缩写之一。

现在这里有一个奇怪的事情。在正则表达式的世界里，点代表任何字符。（也就是说，点代表“任何字符，不一定是点”。）因此 findWithinHorizon(".", 0) 告诉计算机找到用户在键盘上输入的任何种类的下一个字符。当你试图输入单个字符时，findWithinHorizon(".", 0) 非常有用。

在调用 findWithinHorizon("\\d\\d\\d", 0) 中，0 告诉 findWithinHorizon一直搜索到输入结束。这个值 0 是一个特殊情况，因为除 0 之外的任何值都会将搜索限制为特定数量的字符。（这就是方法名中包含 horizon 这个词的原因。horizon 是方法所能看到的最远距离。）这里有几个例子：

-   使用相同的输入 Testing 123 Testing Testing，调用 findWithinHorizon("\\d\\d\\d", 9) 返回 null。它返回 null，因为输入的前九个字符（字符 Testing 1 — 七个字母、一个空格和一个数字）不包含三个连续的数字。这九个字符与模式 \\d\\d\\d 不匹配。
-   使用相同的输入，调用 findWithinHorizon("\\d\\d\\d", 10) 也返回 null。它返回 null，因为输入的前十个字符（字符 Testing 12）不包含三个连续的数字。
-   使用相同的输入，调用 findWithinHorizon("\\d\\d\\d", 11) 返回 123。它返回 123，因为输入的前 11 个字符（字符 Testing 123）包含这 3 个连续的数字。
-   使用输入 A57B842123 Testing，调用 findWithinHorizon("\\d\\d\\d", 12) 返回 442。它返回 442，因为在输入的前 12 个字符（字符 A57B842123 Test）中，由 3 个连续数字组成的第一个序列是序列 442。

但是等等！要从键盘抓取单个字符，我调用 `findWithinHorizon(".", 0).charAt(0)`。在读取单个字符时，`charAt(0)` 的作用是什么？不幸的是，任何 `findWithinHorizon` 调用都表现得好像它在查找一堆字符，而不仅仅是单个字符。即使你调用 `findWithinHorizon(".", 0)`，并且计算机从键盘获取一个字母，Java 程序也会将该字母视为可能存在的多个输入字符之一。

对 `charAt(0)` 的调用解决了多字符问题。此 `charAt(0)` 调用告诉 Java 从 `findWithinHorizon` 获取的任何字符中挑选初始字符。

是的，这很复杂。是的，我不喜欢解释它。但不，你不必理解这个边栏中的任何细节。想读就读细节，不在乎就跳过细节。

我希望能给你 12 条简单的规则来帮助你决定何时重用变量、何时不重用变量。问题是，我做不到。这完全取决于你想要完成什么。那么你如何自己弄清楚何时重用变量、何时不重用变量呢？就像那个人对问如何到达卡内基音乐厅的人说的那样，“练习，练习，再练习。”

## 读取字符

创建 Java Scanner 类的人并没有为读取单个字符创建 next 方法。因此，要输入单个字符，我将两个 Java API 方法粘合在一起。我使用 `findWithinHorizon` 和 `charAt` 方法。

第 5 章中的表 5-1 介绍了此 `findWithinHorizon(".", 0).charAt(0)` 用于读取单个输入字符的技术，并且清单 8-3 使用该技术一次读取一个字符。（事实上，清单 8-3 使用该技术四次来读取四个单独的字符。）

注意图 8-5 中输入的格式。要输入单词 pots 中的字符，我一次输入四个字母，彼此之间没有空格，也没有引号。`findWithinHorizon(".", 0).charAt(0)` 技术就是这样工作的，但不要怪我或我的技术。其他开发人员的字符读取方法也以相同的方式工作。不管你使用谁的方法，读取字符与读取数字都不同。方法如下：

**使用像 nextDouble 和 nextInt 这样的方法时，你在数字之间输入空格。**

如果我输入 80 6，则两次对 nextInt 的调用会读取数字 80，然后是数字 6。如果我输入 806，则一次对 nextInt 的调用会读取数字 806（八百零六），如图 8-8 所示。
