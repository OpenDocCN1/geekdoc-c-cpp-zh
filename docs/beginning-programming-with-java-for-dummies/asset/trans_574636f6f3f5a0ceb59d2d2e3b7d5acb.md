

## 看！一个程序！

在清单4-1中，你会看到一段Java代码。和所有新手程序员一样，你应当谦逊地敬畏这段代码。但别被吓到。一旦你掌握了窍门，编程其实很简单。是的，也很有趣。

### 清单4-1：一个简单的Java程序

```java
/*
 * A program to list the good things in life
 * Author: Barry Burd, BeginProg@allmycode.com
 * February 13, 2014
 */

class ThingsILike {
    public static void main(String args[]) {
        System.out.println("Chocolate, royalties, sleep");
    }
}
```

当我运行清单4-1中的程序时，我得到了图4-1所示的结果：计算机在屏幕上显示“Chocolate, royalties, sleep”这些单词。我承认，仅仅为了让“Chocolate, royalties, sleep”出现在某人电脑屏幕上而编写并运行一个Java程序，工作量很大，但任何事业都得有个起点。

图4-1：运行清单4-1中的程序。

![](img/f938eba5f15e231d828a6255e7ec5523_93_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_93_1.png)

本书中的大多数程序都是基于文本的程序。这些程序几乎只在Eclipse的控制台视图中进行输入和输出。相比之下，GUI（图形用户界面）程序会显示窗口、按钮、文本框和其他小部件来与用户交互。你可以在本书网站（http://allmycode.com/BeginProg）上看到清单4-1中程序的GUI版本，以及本书其他许多示例的GUI版本。

你可以自己在电脑上运行清单4-1中的代码。步骤如下：

1. 按照第2章的说明安装Eclipse。
2. 接着，按照第3章前半部分的说明操作。

这些说明告诉你如何运行名为03-01的项目，该项目可以从本书网站（http://allmycode.com/BeginProg）下载。要运行清单4-1中的代码，请对04-01项目按照相同的说明操作，该项目也在同一下载中。

### 程序各行的含义

如果清单4-1中的程序有朝一日出名了，会有人写一本CliffsNotes式的书来总结这个程序。这本书会非常短，因为你只需一句话就能概括清单4-1的行为。这句话是：

```
Display Chocolate, royalties, sleep
on the computer screen.
```

现在将前面这句话与清单4-1中的主体内容进行比较。由于清单4-1有更多的行，你可能会猜到清单4-1包含大量样板代码。好吧，你猜对了。不写样板代码，你就无法编写Java程序，但幸运的是，样板文本在不同的Java程序之间变化不大。我尽力用不超过66个词总结清单4-1的全部文本：

```
This program lists the good things in life.
Barry Burd wrote this program on February 13, 2014.
Barry realizes that you may have questions about this code, so you can reach him at BeginProg@allmycode.com, on Twitter at @allmycode, or on Facebook at /allmycode.

This code defines a Java class named ThingsILike.
Here's the main starting point for the instructions:
    Display Chocolate, royalties, sleep
    on the screen.
```

本章其余部分（还有约4500个词）将更详细地解释清单4-1中的代码。

### Java程序中的元素

英语和Java都被称为语言，这并非巧合。你用语言来表达思想。英语向人们表达思想，Java向计算机表达思想。而且，英语和Java都有词语、名称和标点符号之类的东西。实际上，两种语言最大的区别在于Java比英语更容易学。（如果英语容易，那么计算机就能理解英语了。可惜，它们不能。）

取一个普通的英语句子，与清单4-1中的代码进行比较。这个句子是：

Suzanne says "eh" because, as you know, she lives in Canada.

在高中语法课上，你为动词、形容词和诸如此类的东西而烦恼。但在本书中，你将按照关键字和标识符来思考，如图4-2所示。

![](img/f938eba5f15e231d828a6255e7ec5523_95_0.png)

Suzanne的句子中包含各种各样的东西。它们和你在计算机程序中发现的东西是同类。所以计划是这样的：将图4-2中的元素与清单4-1中的类似元素进行比较。你已经理解英语了，所以你用这种理解来弄清楚关于Java的一些新东西。

但首先，有个友好的提醒：在接下来的几段中，我会在英语和Java之间进行对比。当你阅读这些段落时，保持开放的心态很重要。例如，在比较Java和英语时，我可能会写道“事物的名称与字典中的单词不同”。当然，你可以争辩说某些字典列出了专有名词，有些人的名字叫Hope、Prudence和Spike，但请不要这样。如果你不吹毛求疵，你会从阅读中获得更多。好吗？我们还是朋友吗？

### 关键字

关键字是字典中的词——一个内置于语言中的词。

在图4-2中，像“says”这样的词是关键字，因为“says”在英语句子中使用时总是扮演相同的角色。Suzanne句子中的其他关键字是“because”、“as”、“you”、“know”、“she”、“lives”和“in”。

计算机程序也有关键字。事实上，清单4-1中的程序使用了Java的四个关键字（以粗体显示）：

```
class ThingsILike {
    public static void main(String args[]) {
```

每个Java关键字都有特定的含义——这个含义在不同程序之间保持不变。例如，每当我编写Java程序时，public这个词总是表示程序中任何其他代码都可以访问的那部分。

![](img/f938eba5f15e231d828a6255e7ec5523_96_0.png)

Java编程语言区分大小写。这意味着如果你把单词中的小写字母改成大写字母，就会改变单词的含义。改变大小写可能使整个单词从有意义变成无意义。在清单4-1中，你不能把public替换成Public。如果这样做，整个程序就会停止运行。

本章对关键字class、public、static和void的含义几乎没有详细介绍。你可以提前看看其他章节的内容，但也可以通过“作弊”来应付。编写程序时，只需以

```
class SomethingOrOther {
```

开头，然后将文本

```
public static void main(String args[]) {
```

粘贴到你的代码中。在你最初的几个程序中，这种策略会很好地为你服务。

表4-1列出了完整的Java关键字列表。

**表4-1 Java关键字**

| abstract | continue | for | new | switch |
| --- | --- | --- | --- | --- |
| assert | default | goto | package | synchronized |
| boolean | do | if | private | this |
| break | double | implements | protected | throw |
| byte | else | import | public | throws |
| case | enum | instanceof | return | transient |
| catch | extends | int | short | try |
| char | final | interface | static | void |
| class | finally | long | strictfp | volatile |
| const | float | native | super | while |

![](img/f938eba5f15e231d828a6255e7ec5523_97_0.png)

在Java中，单词true、false和null具有特定含义。与表4-1中的关键字一样，你不能把true、false和null用来表示Java程序中它们通常含义之外的任何东西。但由于某些只与最挑剔的Java专家有关的原因，true、false和null不被称作Java关键字。无论如何，如果你把true、false和null这几个词涂写在表4-1中，也没问题。

关于关键字，要记住一点：在Java中，每个关键字都有官方的、预定的含义。甲骨文公司的人对Java程序的构成有最终决定权，他们创建了Java的所有关键字。你不能为任何Java关键字编造自己的含义。例如，你不能在计算中使用public这个词：

```java
//This is BAD, BAD CODE:
public = 6;
```

如果你试图这样使用关键字，编译器将显示错误消息，并拒绝翻译你的源代码。这在英语中也是如此。生个孩子并给他取名“Because”。

> “让我们为今晚的主持人——Because O. Borel——献上热烈的掌声。”

你可以这样做，但这个孩子永远不会过上正常的生活。

![](img/f938eba5f15e231d828a6255e7ec5523_97_1.png)

尽管我在这节中热切地声称，但Java中有两个关键字在Java程序中没有含义。这两个关键字——const和goto——被保留在Java中不用于。如果你试图创建一个名为goto的变量，Eclipse会显示“Invalid VariableDeclaratorId”错误消息。Java的创造者认为，如果你在代码中使用了const或goto这两个词中的任何一个，你应该被礼貌地请到C++程序员的桌上。

