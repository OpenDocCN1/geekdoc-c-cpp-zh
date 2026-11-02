

![](img/f938eba5f15e231d828a6255e7ec5523_202_0.png)

你不必担心代码的缩进，因为 Eclipse 可以自动为你的代码缩进。详情请参阅第 4 章。

## 主题的变奏

我不喜欢剥猫皮。但我听说过，如果我真的需要剥一只猫皮，我有几种技术可选。下次我的猫组胺把地毯当成猫砂盆时，我会记住这一点。*

无论你是在剥鲶鱼皮、剥小猫皮，还是在编写计算机程序，同一个原则都适用。你总是有替代方案。第 9-2 节向你展示了一种编写 if 语句的方法。本章的其余部分（以及第 10 章的全部内容）向你展示了创建 if 语句的其他方法。

## ... 否则呢？

你可以创建一个没有 else 子句的 if 语句。例如，想象一个网页，其中每十个随机选择的访客中有一个会收到特别优惠。为了让访客保持猜测，我调用 Random 类的 nextInt 方法，并向幸运数字为 7 的任何人提供优惠。

- 如果 myRandom.nextInt(10) + 1 生成的数字是 7，则显示特别优惠信息。
- 如果 myRandom.nextInt(10) + 1 生成的数字不是 7，则什么也不做。不要显示特别优惠信息，也不要显示令人沮丧的“对不起，没有为你准备的优惠”信息。

* Rick Ross 在我另一本书中读到关于剥猫皮的内容，通过电子邮件向我发送了这些信息：“……你提到‘剥猫皮’然后继续讨论猫砂盆之类的东西。请注意，短语‘剥猫皮的方法不止一种’指的是从鲶鱼身上去除不可食用的皮肤的困难，并且有不止一种方法可以做到这一点。这些方法从把动物的尾巴钉在木板上并用钳子剥下来，到让毛茸茸的那种猫去处理这东西然后就不管它了不等。我在河上长大（那条从美国南北流经、名字以‘M’开头且有很多重复字母的大河），所以这对我们的经历至关重要。”另一位读者 Alan Wilson 对此讨论补充了他的看法：“……短语‘剥猫皮’……实际上有一个更古老且同样有趣的英国海军起源。它指的是将九根绳子系到鞭子上的活动，该鞭子在几百年前被用来惩罚顽固的水手。‘九尾猫’是那根鞭子的名字，而系绳子‘剥’鞭子的方法不止一种。”无论如何，是时候让我向我的小宠物道歉了。

实现这种策略的代码如第 9-3 节所示。该代码的几次运行结果如第 9-5 图所示。

### 图 9-5:
三次运行
的代码
在清单
9-3 中。

![](img/f938eba5f15e231d828a6255e7ec5523_203_0.png)

### 清单 9-3：你真幸运？

```
import java.util.Random;

class SpecialOffer {
    public static void main(String args[]) {
        Random myRandom = new Random();
        int randomNumber = myRandom.nextInt(10) + 1;

        if (randomNumber == 7) {
            System.out.println("An offer just for you!");
        }

        System.out.println(randomNumber);
    }
}
```

第 9-3 节中的 if 语句没有 else 子句。这个 if 语句的形式如下：

```
if (Condition) {
    SomeStatements
}
```

当 randomNumber 为 7 时，计算机显示 An offer just for you! 当 randomNumber 不是 7 时，计算机不显示 An offer just for you! 该操作如第 9-6 图所示。

![](img/f938eba5f15e231d828a6255e7ec5523_203_1.png)

> 总是（我是说总是）在 if 语句条件中比较两个数字或字符时使用双等号。永远（就是永远、永远、永远）不要使用单个等号来比较两个值。单个等号执行赋值，而不是比较。

图 9-6：
如果你没有什么好说的，那就不要说任何话。

![](img/f938eba5f15e231d828a6255e7ec5523_204_0.png)

在第 9-3 节中，我擅自添加了一个额外的 println。这个 println（在 main 方法的末尾）显示了我调用 nextInt 生成的随机数。在带有特别优惠的网页上，你可能看不到随机生成的数字，但如果不知道代码生成了什么数字，我就无法测试我的 SpecialOffer 代码。

无论如何，请注意 randomNumber 的值在每次运行中都会显示。randomNumber 的 println 不在 if 语句内部。（这个 println 在 if 语句之后。）因此计算机总是执行这个 println。无论 randomNumber == 7 为真还是假，计算机都会采取适当的 if 操作，然后继续执行 System.out.println(randomNumber)。

## 将更多内容打包到 if 语句中

这里有一个有趣的情况：你有两个棒球队——Hankees 和 Socks。你想在两行上分别显示球队的得分，并且获胜者的得分排在前面。（在计算机屏幕上，获胜者的得分显示在失败者得分之上。在平局的情况下，你将两个相同的得分一个显示在另一个之上。）第 9-4 节有代码。

```
Listing 9-4: May the Best Team Be Displayed First

import java.util.Scanner;
import static java.lang.System.in;
import static java.lang.System.out;

class TwoTeams {
    public static void main(String args[]) {
```

### 清单 9-4（续）

```java
Scanner keyboard = new Scanner(in);
int hankees, socks;

out.print("Hankees and Socks scores? ");
hankees = keyboard.nextInt();
socks = keyboard.nextInt();
out.println();

if (hankees > socks) {
    out.print("Hankees: ");
    out.println(hankees);
    out.print("Socks: ");
    out.println(socks);
} else {
    out.print("Socks: ");
    out.println(socks);
    out.print("Hankees: ");
    out.println(hankees);
}

keyboard.close();
}
```

第 9-7 图展示了代码的几次运行。（为了在一张图中展示几次运行，我将结果从 Eclipse 的 Console 视图复制到 Windows Notepad。）

有了大括号，一堆 print 和 println 调用被安全地隐藏在 if 子句内部。另一组 print 和 println 调用被挤在 else 子句内部。这就造成了第 9-8 图所示的分叉情况。

图 9-7：看？第 9-4 节中的代码真的有效！

![](img/f938eba5f15e231d828a6255e7ec5523_205_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_206_0.png)

图 9-8：
为你最喜欢的
队伍加油。

## 语句和块

思考 if 语句的一个优雅方式是认识到你只能在 if 语句的每个子句中放入一个语句。

在你第一次阅读这条单语句规则时，你可能会对这些问题感到不感兴趣。事实上，直到第 18 章我才能解释这些问题。在我解释静态导入声明之前，我需要介绍一些概念。我需要描述类、包和静态成员。

因此在你读到第 18 章之前，请耐心等待。只需将三个导入声明粘贴到你的 Java 程序顶部，并相信一切都会正常工作。

![](img/f938eba5f15e231d828a6255e7ec5523_207_0.png)

你可以用单个单词 out 来缩写 System.out。你也可以用单个单词 in 来缩写 System.in。只要确保将导入声明完全按照第 9-4 节中的显示复制即可。只要与第 9-4 节中的行有任何偏差，你可能会收到编译器错误。

