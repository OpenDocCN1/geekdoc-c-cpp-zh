
## 你或我可以定义的标识符

我喜欢 Suzanne 这个名字，但如果你不喜欢传统名字，那就想一个全新的名字。你要生个新宝宝了。给她取名叫“Deneen”或“Chrisanta”。给他取名叫“Belton”或“Merk”。

名字是一个用来标识某事物的词，所以我不再称这些东西为名字，而是称它们为标识符。在计算机编程中，标识符是一种名词。标识符指的是一个值、程序的一部分、某种结构，或任何数量的东西。

清单 4-1 中有两个是你或我可以自行定义的标识符。它们是自创的词 ThingsILike 和 args。

```
class ThingsILike {
    public static void main(String args[]) {

```

正如名字 Suzanne 和 Chrisanta 在英语中没有特殊含义一样，名字 ThingsILike 和 args 在 Java 中也没有特殊含义。在清单 4-1 中，我用 ThingsILike 作为程序的名称，但我也可以使用像 GooseGrease、Enzyme 或 Kalamazoo 这样的名字。我必须在程序中写上 (String someName[])，但我也可以使用 (String args[])、(String commandLineArguments[]) 或 (String cheese[])。

![](img/bf4858233d2b2a32ff4e3991860526b3_98_0.png)

TIP
照我说的做，别照我做的做。为你的 Java 程序中的事物想出合理、信息丰富的名称。像 GooseGrease 这样的名字很可爱，但它们无助于你跟踪程序编写策略。

![](img/bf4858233d2b2a32ff4e3991860526b3_98_1.png)

REMEMBER
当我为 Java 程序命名时，我可以使用 ThingsILike 或 GooseGrease，但我不能使用 public 这个词。像 class、public、static 和 void 这样的词是 Java 中的关键字。

(String args[]) 中的 args 保存你在发出运行 Java 程序命令时输入的任何额外内容。例如，如果你通过输入 java ThingsILike won too 3 来运行程序，那么 args 就存储额外的值 won、too 和 3。作为一名初学者，你不需要考虑 Java 的这个特性。只需将 (String args[]) 粘贴到每个程序中即可。

## 有约定含义的标识符

很多人都叫 Suzanne，但只有一个国家叫 Canada。这是因为“Canada”这个词有一个标准、众所周知的含义。它就是国旗上有红色枫叶的国家。如果你要建立自己的国家，就应避免将其命名为 Canada，因为这样命名只会让每个人都困惑。（我知道，肯塔基州有一个镇叫 Canada，但这不算数。记住，你应该忽略这类例外。）

大多数编程语言都有约定含义的标识符。在 Java 中，几乎所有这些标识符都定义在 Java API 中。清单 4-1 中有五个这样的标识符。它们是单词 main、String、System、out 和 println：

```
public static void main(String args[]) {
    System.out.println("Chocolate, royalties, sleep");
}
```

以下是这些名称含义的简要说明（本书各处会有更详细的描述）：

- **main:** 每个 Java 程序中执行的起点。
- **String:** 一串文本；一连串的字符。
- **System:** Java API 中的一个现成程序。该程序访问一些超出 Java 虚拟机（JVM）直接控制的计算机功能。
- **out:** 文本程序显示其文本的位置。（对于在 Eclipse 中运行的程序，单词 out 代表 Console 视图。要了解更多关于基于文本的程序的信息，请查阅第 3 章的前几段。）
- **println:** 在计算机屏幕上显示文本。

![](img/bf4858233d2b2a32ff4e3991860526b3_99_0.png)

名称 println 来自“print a line”这个词组。如果你被允许用大写字母写这个名字，它会是 PRINTLN，词尾附近有一个字母 L。当计算机执行 println 时，计算机会在 Eclipse 的 Console 视图中放置一些文本，然后立即移动到下一行的开头，为 Console 视图中将要出现的其他内容做准备。

![](img/bf4858233d2b2a32ff4e3991860526b3_99_1.png)

严格来说，Java API 中标识符的含义并非一成不变。虽然你可以为 System 或 println 这样的词自创含义，但这样做不是个好主意——因为你会让其他程序员感到困惑，他们习惯了这些熟悉标识符名称的标准 API 含义。

## 字面量

字面量是一段看起来像其所代表的值的文本。在 Suzanne 的句子中（参见图 4-2），“eh”是一个字面量，因为“eh”指的是单词“eh”。

编程语言也有字面量。例如，在清单 4-1 中，引号中的内容就是字面量：

```
System.out.println("Chocolate, royalties, sleep");
```

当你运行 ThingsILike 程序时，你会在屏幕上看到单词 Chocolate、royalties、sleep。在清单 4-1 中，文本“Chocolate, royalties, sleep”指的是这些词，正如它们在屏幕上出现的那样（不包括引号）。

你在计算机程序中使用的数字大多是字面量。如果你把语句

```
mySalary = 1000000.00;
```

放在计算机程序中，那么 1000000.00 就是一个字面量。它代表数字 1000000.00（一百万）。

如果你不喜欢数位数，你可以在 Java 7 程序中放入以下语句：

```
mySalary = 1_000_000.00;
```

从 Java 7 开始，带下划线的数字可以用作字面量。

在 Java 7 之前的版本中，你不能在代码中使用像 1_000_000.00 这样的数字。

![](img/bf4858233d2b2a32ff4e3991860526b3_100_0.png)

![](img/bf4858233d2b2a32ff4e3991860526b3_100_1.png)

不同国家使用不同的数字分隔符和不同的数字格式。例如，在美国，你写 1,234,567,890.55。在法国，你写 1234567890,55。在印度，你将数字按两三位一组分组。你不能在 Java 程序中写类似 mySalary = 1,000,000.00 的语句。Java 的数字字面量中没有逗号。但你可以用 mySalary = 10_00_000.00 来方便印度人阅读的编程。而且对于程序的输出，你可以使用 Java 的 Locale 和 NumberFormat 类来显示像 1234567890,55 这样的数字。（有关 Locale 和 NumberFormat 的更多信息，请查阅第 18 章。）

## 标点符号

典型的计算机程序有很多标点符号。例如，考虑清单 4-1 中的程序：

```
class ThingsILike {
    public static void main(String args[]) {
        System.out.println("Chocolate, royalties, sleep");
    }
}
```

每个方括号、每个大括号、任何形式的波浪线都在使程序有意义方面发挥作用。

在英语中，你一直写到一行末尾然后将文本换到下一行开头。在编程中，你很少这样做。相反，代码的标点符号指导某些行的缩进。缩进显示程序的哪些部分从属于哪些其他部分。就好像在英语中，你这样写 Suzanne 的句子：

Suzanne says "eh" because
'
    as you know
'
she lives in Canada.

图 4-3 和图 4-4 中的图表向你展示了 ThingsILike 程序的各部分是如何包含在其他部分之内的。注意一对花括号如何像一个盒子一样起作用。为了让程序的结构一目了然，你要缩进每个盒子内部的所有内容。

图 4-3：一对花括号像一个盒子一样起作用。

![](img/bf4858233d2b2a32ff4e3991860526b3_101_0.png)

图 4-4：计算机程序中的思想彼此嵌套。

![](img/bf4858233d2b2a32ff4e3991860526b3_101_1.png)

REMEMBER
我不能再强调这一点了。如果你不缩进代码，或者缩进但不够仔细，那么你的代码仍然可以正确编译和运行。但这种成功的运行会给你一种虚假的自信。一旦你尝试更新一些缩进不良的代码，你就会完全迷惑。所以听我的建议：在整个过程中始终仔细缩进你的代码。无论是草拟一个快速测试程序还是为亿万富翁客户编写代码，都要使你的缩进精确。

TIP
Eclipse 可以自动为你缩进代码。选择你想要缩进代码的 .java 文件。然后，在 Eclipse 的主菜单中选择 Source→Format。Eclipse 会重新排列编辑器中的行，缩进应该缩进的内容，并通常使你的代码看起来不错。
