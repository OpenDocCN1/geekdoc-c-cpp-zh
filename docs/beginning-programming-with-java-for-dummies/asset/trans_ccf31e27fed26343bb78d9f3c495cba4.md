
## 第8章：数字？谁需要数字？

### 本章内容

- 使用字符
- 处理“真”或“假”值
- 完善你对 Java 基本类型的知识

我不太喜欢传真机。它们效率太低。发送一份简短的传真，你得到什么？你得到两片树——一端在发送端，另一端在接收端。你还有数百万个点——点在打印页上扫描细小的线条。点区分亮区和暗区。太浪费了！

把传真和电子邮件相比。用电子邮件，我可以用 2,500 个零和一发送一份 25 字的比赛参赛作品，而且不用浪费任何纸张。最重要的是，电子邮件并不描述亮点和暗点。电子邮件包含每个字母的代码——字母 A 的零和一的短序列，字母 B 的零和一的不同序列，等等。还能更简单吗？

现在想象发送一份一词传真。那个词是“true”，其含义被理解为，“true，我接受你撰写 *《用 Java 进行初级编程傻瓜书，第 4 版》* 的提议。” 带有此消息的传真会发送 t-r-u-e 四个字母的图片，纸上有污渍的地方线条模糊，墨粉用完的地方有小白点。

但说真的，“true”消息的本质是什么？可能性只有两种，对吧？消息可能是“true”或“false”，要表示这些可能性，我不需要太多铺张。0 代表“false”，1 代表“true”怎么样？

他们问：“你是否接受我们让你撰写 *《用 Java 进行初级编程傻瓜书，第 4 版》* 的提议？”

“我回复：”1“。

可惜我几个月前没想到这一点。无论如何，本章涉及字母、真、假以及其他类似的东西。

### 字符

在第 6 章和第 7 章中，你在所有变量中存储数字。这没问题，但生活不止有数字。例如，我用电脑写了这本书，这本书包含成千上万个非数字的东西，叫做字符。

用于存储字符的 Java 类型是 `char`。清单 8-1 有一个使用 `char` 类型的简单程序，图 8-1 显示了清单 8-1 程序的运行结果。

**清单 8-1：使用 char 类型**

```java
class LowerToUpper {
    public static void main(String args[]) {
        char smallLetter, bigLetter;

        smallLetter = 'b';
        bigLetter = Character.toUpperCase(smallLetter);
        System.out.println(bigLetter);
    }
}
```

![](img/f938eba5f15e231d828a6255e7ec5523_169_0.png)

在清单 8-1 中，第一个赋值语句将字母 `b` 存储在 `smallLetter` 变量中。在该语句中，注意 `b` 如何被单引号包围。在 Java 程序中，每个 `char` 字面量都以单引号开头和结尾。

当你用引号包围一个字母时，你告诉计算机该字母不是变量名。例如，在清单 8-1 中，不正确的语句 `smallLetter = b` 会告诉计算机查找名为 `b` 的变量。因为没有名为 `b` 的变量，你会得到一个 `b cannot be resolved to a variable` 消息。

在清单 8-1 的第二个赋值语句中，程序调用了一个名为 `Character.toUpperCase` 的 API 方法。方法 `Character.toUpperCase` 做了其名称所暗示的事情——该方法生成小写字母的大写等价物。在清单 8-1 中，这个大写等价物（字母 `B`）被赋给变量 `bigLetter`，并且 `bigLetter` 中的 `B` 被打印到屏幕上，如图 8-2 所示。

![](img/f938eba5f15e231d828a6255e7ec5523_170_0.png)

**图 8-2：** 清单 8-1 中的操作。

当计算机在屏幕上显示一个 `char` 值时，计算机不会用单引号包围该字符。

### 我离题了……

一段时间前，我想知道如果我调用 `Character.toUpperCase` 方法并向该方法提供一个一开始就不是小写的字符会发生什么。我翻出了 Java API 文档，但找不到有用的信息。文档说 `toUpperCase` “使用 UnicodeData 文件中的大小写映射信息将字符参数转换为大写。” 谢谢，但这对我没用。

说起来似乎很傻，我问自己如果我是 `toUpperCase` 方法会怎么做。如果有人递给我一个大写字母 `R` 并告诉我把该字母大写，我会说：“把你那该死的资本 R 拿回去。” 用计算的术语来说，我会向那个人发送一条错误消息。所以我想知道如果我对字母 `R` 应用 `Character.toUpperCase` 是否会得到错误消息。

我试过了。我在清单 8-2 中设计了这个实验。

**清单 8-2：探究 toUpperCase 的行为**

```java
class MyExperiment {
    public static void main(String args[]) {
        char smallLetter, bigLetter;
        smallLetter = 'R';
        bigLetter = Character.toUpperCase(smallLetter);
        System.out.println(bigLetter);
        smallLetter = '3';
        bigLetter = Character.toUpperCase(smallLetter);
        System.out.println(bigLetter);
    }
}
```

在我的实验中，我没有混合化学品并引爆东西。我做的是：

-   我将 `'R'` 赋给 `smallLetter`。

    `toUpperCase` 方法取了大写字母 `R` 并给了我另一个大写字母 `R`。（见图 8-3。）我没有得到错误消息。这告诉我 `toUpperCase` 方法对已经是大写的字母做什么。方法什么都不做。

-   我将 `'3'` 赋给 `smallLetter`。

    `toUpperCase` 方法取了数字 `3` 并给了我相同的数字 `3`（见图 8-3）。我没有得到错误消息。这告诉我 `toUpperCase` 方法对非字母字符做什么。它什么都不做，什么都没有，零， zilch，bupkis。

**图 8-3：** 运行清单 8-2 中的代码。

![](img/f938eba5f15e231d828a6255e7ec5523_171_0.png)

我写下这个实验是为了说明一个重要观点。当你不了解计算机编程的某些内容时，写一个测试程序往往会有所帮助。设计一个实验，看看计算机如何响应。

我猜把大写字母 `R` 交给 `toUpperCase` 方法会给我一个错误消息，但我错了。看？问题的答案不是从天上掉下来的。创建 Java API 的人们做出了决定。他们做出了一些显而易见的选择，也做出了一些出人意料的选择。没有人知道 Java 功能的一切，所以不要指望把所有答案都塞进你的脑袋。

Java 文档很棒，但对于文档回答的每一个问题，它忽略了另外三个问题。所以要大胆。不要害怕动手。写很多简短的实验性程序。你不会弄坏计算机，所以尽情地玩吧。你好奇的精神总会得到回报。

阅读和理解 Java 的 API 文档是一门艺术，而不是一门科学。有关如何充分利用这些文档的建议，请阅读我的文章“理解 Java 的 API 文档”，网址为 http://www.dummies.com/extras/beginningprogrammingwithjava。

### 一次只能一个字符，请

一个 `char` 变量只存储一个字符。所以如果你想写下面的语句

```java
char smallLetters;
smallLetters = 'barry'; //Don't do this
```

请抵制这种诱惑。你不能一次在一个 `char` 变量中存储多个字母，也不能把多个字母放在一对单引号之间。如果你想存储单词或句子（不仅仅是单个字母），那么你需要使用一种叫做 `String` 的东西。有关 Java 的 `String` 类型的介绍，请参阅第 18 章。

### 变量与回收

在清单 8-2 中，我两次使用了 `smallLetter`，两次使用了 `bigLetter`。这就是为什么它们被称为变量。首先，`smallLetter` 的值是 `R`。后来，我改变了 `smallLetter` 的值，使得 `smallLetter` 的值变为 `3`。

当我给 `smallLetter` 分配一个新值时，`smallLetter` 的旧值会被抹掉。例如，在图 8-4 中，第二个 `smallLetter` 赋值将 `3` 放入 `smallLetter`。当计算机执行这个第二个赋值语句时，旧值 `R` 就消失了。

