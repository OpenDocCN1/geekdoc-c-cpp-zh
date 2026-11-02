
那么当你自己输入程序时会有什么大不了的呢？嗯，当你把手指放到键盘上时，会发生很多有趣的事情。这就是为什么本章的后半部分专门用于故障排除。

## EchoLine 程序的工作原理

当你还是个小婴儿，舒适地躺在母亲怀里时，她告诉你如何向计算机屏幕发送字符：

```
System.out.println(whatever text you want displayed);
```

她没有告诉你的是如何从计算机键盘获取字符。有很多种方法可以做到这一点，但本章我推荐的是

```
keyboard.nextLine()
```

现在，有趣的部分来了。调用 nextLine 方法不仅仅是从键盘获取字符。当计算机运行你的程序时，计算机会用你在键盘上输入的内容替换文本 keyboard.nextLine()。

要理解这一点，请看清单 5-1 中的语句：

```
System.out.println(keyboard.nextLine());
```

运行程序时，计算机看到你对 nextLine 的调用并立即停下来。（参见图 5-2。）计算机等待你输入一行文本。所以（参见图 5-3）你输入这一行：

```
Hey, there's an echo in here.
```

计算机用这一整行 Hey 替换程序中 keyboard.nextLine() 的调用。该过程如图 5-5 所示。

keyboard.nextLine() 的调用嵌套在 System.out.println 调用内部。所以最终，计算机的行为就像清单 5-1 中的语句是这样：

```
System.out.println("Hey, there's an echo in here.");
```

计算机在屏幕上显示另一份文本 Hey, there's an echo in here. 这就是为什么你在图 5-4 中看到两份 Hey 行。

![](img/f938eba5f15e231d828a6255e7ec5523_119_0.png)

Figure 5-5:
计算机用文本替换 nextLine 调用处的内容。

## 获取数字、单词和其他内容

在清单 5-1 中，单词 keyboard.nextLine() 从计算机键盘获取整行文本。所以如果你输入

```
Testing 1 2 3
```

清单 5-1 中的程序会回显你整行 Testing 1 2 3 文本。

有时你并不希望程序获取整行文本。相反，你希望程序获取一行中的一部分。例如，当你输入 1 2 3 时，你可能希望计算机获取数字 1。（也许数字 1 代表一个客户之类的。）在这种情况下，你不要在程序中放入 keyboard.nextLine()。相反，你使用 keyboard.nextInt()。

表 5-1 向你展示了 keyboard.next 用法的一些变体。不幸的是，表格的条目并不十分可预测。要读取输入行，你调用 nextLine。但要读取输入单词，你不会调用 nextWord。（Java API 没有 nextWord 方法。）相反，要读取单词，你调用 next。

| 表 5-1 | 一些 Scanner 方法 |
|---|---|
| 读取此内容 ... | ... 调用此方法 |
| 没有小数点的数字 | nextInt() |
| 带小数点的数字 | nextDouble() |
| 单词（例如以空格结尾） | next() |
| 行（或在已从行中读取一些数据后剩余的部分） | nextLine() |
| 单个字符（例如字母、数字或标点字符） | findWithinHorizon(" ",0).charAt(0) |

此外，表格的故事有一个出人意料的结局。要读取单个字符，你不会调用 nextSomething。相反，你可以调用奇怪的 findWithinHorizon(" ",0).charAt(0) 方法组合。（你得原谅创建 Scanner 类的人。他们是从一个专门的角度创建 Scanner 的。）

要查看表格中一些方法的使用情况，请查看本书中的其他程序清单。第 6、7 和 8 章有一些特别好的示例。

## 输入三行代码然后不再回头

清单 5-1 中隐藏着三行额外的代码。这些行帮助计算机从键盘读取输入。这三行是

```java
import java.util.Scanner;
Scanner keyboard = new Scanner(System.in);
keyboard.close();
```

关于这三行，我有坏消息和好消息。

- **坏消息是，这些行的推理很难理解。** 这在第 5 章尤其如此，在这里我介绍 Java 最基本的概念。
- **好消息是，你不必理解这三行的推理。** 你可以将这些行复制并粘贴到任何从键盘获取输入的程序中。你不需要以任何方式更改这些行。这些行在各种 Java 程序中无需任何修改即可工作。

## 快速浏览 Scanner

在本章中，我建议你忽略 import java.util.Scanner 和 Scanner keyboard 等行的任何含义。只需无脑地将这两行粘贴到你的代码中，然后继续前进。

当然，你可能不想听我的建议。你可能不喜欢在代码中忽略东西。如果你恰好是这样固执的人，我有一些快速事实告诉你。

- The word Scanner is defined in the Java API.

A Scanner is something you can use for getting input.

This Scanner class belongs to Java versions 5.0 and higher. If you use version Java 1.4.2, you don't have access to the Scanner class. (You see an error marker when you type Listing 5-1.)

- 单词 Scanner 在 Java API 中有定义。

Scanner 是你可以用来自获取输入的东西。

这个 Scanner 类属于 Java 5.0 及更高版本。如果使用 Java 1.4.2 版本，你无法访问 Scanner 类。（当你输入清单 5-1 时，你会看到错误标记。）

- The words System and in are defined in the Java API.

Taken together, the words System.in stand for the computer keyboard.

In later chapters, you see things like new Scanner(new File("myData.txt")). In these chapters, I replace System.in with the words new File("myData.txt") because I'm not getting input from the keyboard. Instead, I'm getting input from a file on the computer's hard drive.

- 单词 System 和 in 在 Java API 中有定义。

合在一起，单词 System.in 代表计算机键盘。

在后面的章节中，你会看到类似 new Scanner(new File("myData.txt")) 的内容。在这些章节中，我用单词 new File("myData.txt") 替换 System.in，因为我不是从键盘获取输入。相反，我是从计算机硬盘上的文件获取输入。

- The word keyboard doesn't come from the Java API.

The word keyboard is a Barry Burd creation. Instead of keyboard, you can

use readingThingie (or any other name you want to use as long as you use the name consistently). So, if you want to be creative, you can write

- 单词 keyboard 不来自 Java API。

单词 keyboard 是 Barry Burd 的创作。代替 keyboard，你可以使用

readingThingie（或任何你想要使用的名称，只要你一致使用该名称）。所以，如果你想发挥创意，可以写

```
Scanner readingThingie =
    new Scanner(System.in);

System.out.println
    (readingThingie.nextLine());
```

修订后的清单 5-1（使用 readingThingie 代替 keyboard）可以顺利编译和运行。

- The line import java.util.Scanner is an example of an import declaration.

An optional import declaration allows you to abbreviate names in the rest of your program. You can remove the import declaration from Listing 5-1. But if you do, you must use the Scanner class's fully qualified name throughout your code. Here's how:

- 行 import java.util.Scanner 是 import 声明的一个例子。

可选的 import 声明允许你在程序其余部分中缩写名称。你可以从清单 5-1 中删除 import 声明。但如果你这样做，你必须在整个代码中使用 Scanner 类的完全限定名称。方法如下：

```
class EchoLine {

    public static void main
        (String args[]) {

        java.util.Scanner keyboard
            = new java.util.Scanner
                (System.in);

        System.out.println
            (keyboard.nextLine());

        keyboard.close();
    }
}
```

请确保将这些行放在正确的位置：

- 将 `import java.util.Scanner` 行作为程序的第一行。
- 将 `Scanner keyboard = new Scanner(System.in)` 行放在 main 方法内部，紧跟在 `public static void main(String args[]) {` 行之后。
- 将 `keyboard.close()` 行作为程序的最后一行。

在未来的某个时候，你可能需要更小心地处理这三行的位置。但就目前而言，我给出的规则对你很有帮助。

## 预期意外

不久前，我遇到了一位有有趣政策的讲师。他说，“有时候我在讲课时，会在电脑上从头开始编写程序。我就在学生面前做。如果程序第一次编译和运行就正确，我希望学生给我热烈鼓掌。”

起初，你可能会认为这个家伙自负极大，但你必须将事情放在适当的背景下。程序第一次编译和运行就正确的情况并不常见。几乎总是有拼写错误或其他某种错误。

所以本节讨论的是你在第一次编译和运行程序时看到的正常、预期错误。每个人都会犯这些错误，即使是最有经验的人。关键是保持冷静。以下是我的一般建议：

- **不要期望你输入的程序第一次就能编译成功。**
  准备好返回编辑器修复一些错误。
- **不要期望编译完美的程序就能正确运行。**
  即使在 Eclipse 编辑器中没有错误标记，你的程序仍可能包含缺陷。在 Eclipse 编译你的程序后，你仍需要成功运行程序。也就是说，你的程序应该完成运行并显示正确的输出。
  你先编译然后运行。让程序在没有错误的情况下编译是这两个任务中较容易的。
- **阅读 Eclipse 编辑器中的内容，而不是你假设 Eclipse 编辑器中的内容。**
  不要假设你已正确输入单词，已正确大写单词，或已正确匹配大括号或括号。比较你输入的代码与任何示例代码。确保每个细节都正确无误。
