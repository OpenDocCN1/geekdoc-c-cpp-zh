
```
out.println(hankees);
out.print("Socks:  ");
out.println(socks);
} else if (gameCancelled) {
    out.println("Sorry, sports fans.");
} else {
    out.println("The game isn't over yet.");
}
```

级联 if 语句没有什么特别之处。这并非一种新的编程语言特性。级联 if 语句利用的是 Java 中的一个“漏洞”——在某些情况下可以省略花括号的漏洞。除此之外，级联 if 语句只是为你提供了一种在代码中思考决策的新方式。

注意：清单 10-6 使用了一个静态导入（static import）声明，以避免不必要地重复 System.out 这几个字。想稍微了解一下静态导入声明（同时我也为没有更详细地解释这个概念而道歉），请看第 9 章。然后，想真正弄懂静态导入声明，请看第 18 章。

## 枚举各种可能性

第 8 章描述了 Java 的 boolean 类型——一种只有两个值（true 和 false）的类型。boolean 类型非常方便，但有时你需要更多的值。毕竟，交通灯的值可以是绿色、黄色或红色。扑克牌的花色可以是黑桃、梅花、红心或方块。工作日可以是周一、周二、周三、周四或周五。

生活中充满了各种小的可能性集合，而 Java 有一个可以反映这些可能性的特性。这个特性称为枚举（enum）类型。它从 Java 5.0 版本起可用。

## 创建枚举类型

清单 10-6 中的故事有三种可能的结局——Hankees 队获胜、Socks 队获胜，或者比赛打平。你可以用下面这一行 Java 代码来表示这些可能性：

```
enum WhoWins {home, visitor, neither}
```

本周的比赛在 Hankeeville 的 SnitSoft 体育场举行，因此值 home 代表 Hankees 队获胜，值 visitor 代表 Socks 队获胜。

计算机编程的目标之一是让每个程序的结构都映射（mirror）它要解决的问题。当一个程序能让你联想到其背后的实际问题时，这个程序就容易理解，维护成本也低。例如，一个为客户账户制表的程序应该使用像 customer 和 account 这样的名称。而一个处理三种可能结果（主队胜、客队胜、平局）的程序，应该有一个具有三个可能值的变量。enum WhoWins {home, visitor, neither} 这一行创建了一个用于存储三个值的类型。

WhoWins 类型被称为枚举类型。你可以把新的 WhoWins 类型看作一个打了类固醇的 boolean。WhoWins 类型不是两个值（true 和 false），而是三个值（home、visitor 和 neither）。你可以创建一个 WhoWins 类型的变量：

```
WhoWins who;
```

然后给这个新变量赋值：

```
who = WhoWins.home;
```

在下一节中，我会好好利用 WhoWins 类型。

## 使用枚举类型

清单 10-7 向你展示了如何使用全新的 WhoWins 类型。

### 清单 10-7：得意的赢家和输不起的输家

```
import java.util.Scanner;
import static java.lang.System.out;

class Scoreboard {

    enum WhoWins {home, visitor, neither}

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int hankees, socks;
        WhoWins who;
        out.print("Hankees and Socks scores? ");
        hankees = keyboard.nextInt();
        socks = keyboard.nextInt();
        out.println();
    }
```

### 清单 10-7（续）

```
if (hankees > socks) {
    who = WhoWins.home;
    out.println("The Hankees win :-)");
} else if (socks > hankees) {
    who = WhoWins.visitor;
    out.println("The Socks win :-(");
} else {
    who = WhoWins.neither;
    out.println("It's a tie :-|");
}

out.println();
out.println("Today's game is brought to you by");
out.println("SnitSoft, the number one software");
out.println("vendor in the Hankeeville area.");
out.println("SnitSoft is featured proudly in");
out.println("Chapter 6. And remember, four out");
out.println("of five doctors recommend");
out.println("SnitSoft to their patients.");
out.println();

if (who == WhoWins.home) {
    out.println("We beat 'em good. Didn't we?");
}

if (who == WhoWins.visitor) {
    out.println("The umpire made an unfair");
    out.println("call.");
}

if (who == WhoWins.neither) {
    out.println("The game goes into overtime.");
}

keyboard.close();
}
```

清单 10-7 中程序的 3 次运行情况如图 10-13 所示。

## 📈 量化交易全攻略

从入门到精通，掌握系统化投资策略

![](img/f938eba5f15e231d828a6255e7ec5523_230_0.png)

本课程专为希望系统学习量化交易的投资者设计，涵盖策略编写、回测、风控与实盘部署，助你构建属于自己的量化交易体系。

立即购买，开启你的量化之旅！

| 课程版本 | 价格 | 原价 | 说明 |
| --- | --- | --- | --- |
| 体验版 | ¥9.9 | ¥99 | 基础入门视频 + 电子书 |
| 专业版 | ¥199 | ¥399 | 完整课程 + 源码 + 社群答疑 |
| 企业版 | ¥999 | ¥1999 | 团队学习 + 定制策略 + 1V1 辅导 |

- ✅ 录播课程，随时学习
- ✅ 专属社群，交流答疑
- ✅ 源码级教学，实战演练
- ✅ 手机/电脑/平板随时随地学

## 适合人群

- 对量化交易感兴趣的投资者
- 有一定编程基础的程序员
- 希望提升投资效率的金融从业者

## 常见问题

- Q：课程有效期多久？
- A：课程购买后永久有效，可反复观看。
- Q：购买后如何学习？
- A：下载课程 App 或用网页版登录即可观看。
- Q：支持退款吗？
- A：虚拟产品暂不支持退款，请试看后再购买。

赋值语句。我要执行的语句取决于 if 语句中 hankees > socks 比较的结果。

注意，在清单 10-7 中，我引用了每一个 WhoWins 值。我会写 WhoWins.home、WhoWins.visitor 或 WhoWins.neither。如果我忘了 WhoWins 前缀并输入：

```
who = home; //This assignment doesn't work!
```

编译器就会给我一条“home cannot be resolved to a variable”错误消息。枚举类型就是这样工作的。

## 将变量值与各个 WhoWins 值进行比较

在一条 if 语句中，我检查 who == WhoWins.home 条件。在另外两条 if 语句中，我检查其他 WhoWins 值。

在清单 10-7 的末尾，我本可以不使用枚举值。我可以再测试一次像 hankees > socks 这样的条件。

```
if (hankees > socks) {
    out.println("The Hankees win :-)");
}

// And later in the program...

if (hankees > socks) {
    out.println("We beat 'em good. Didn't we?");
}
```

但这种做法会很笨拙。在更复杂的程序中，我可能会反复检查 hankees > socks 十几次。那就像一遍又一遍地问同一个问题。

与其反复检查 hankees > socks 条件，不如把比赛结果存储为一个枚举值。然后，我想检查多少次就检查多少次。这是解决“反复检查”问题的一个非常简洁的方法。

```
if (randomNumber == 4)
  .
  .
if (randomNumber < 1 || randomNumber > 10) {
    System.out.print("Sorry, the electronic oracle");
    System.out.println(" is closed for repairs.");
}
```

但这种方法似乎很浪费。为什么不创建一条只检查一次 randomNumber 的值、然后根据找到的值采取行动的语句呢？幸运的是，确实存在这样的语句：switch 语句。清单 11-1 中有一个 switch 语句的例子。

## 清单 11-1：应对各种场合的答案

```java
import java.util.Scanner;
import java.util.Random;
import static java.lang.System.out;

class TheOldSwitcheroo {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        Random myRandom = new Random();
        int randomNumber;

        out.print("Type your question, my child: ");
        keyboard.nextLine();

        randomNumber = myRandom.nextInt(10) + 1;

        switch (randomNumber) {
        case 1:
            out.println("Yes. Isn't it obvious?");
            break;

        case 2:
            out.println("No, and don't ask again.");
            break;

        case 3:
            out.print("Yessir, yessir!");
            out.println(" Three bags full.");
            break;

        case 4:
            out.print("What part of \"no\"!");
            out.println("I don't understand?");
            break;

        case 5:
            out.println("No chance, Lance.");
            break;

        case 6:
            out.println("Sure, whatever.");
            break;

        case 7:
            out.print("Yes, but only if");
            out.println(" you're nice to me.");
            break;

        case 8:
            out.println("Yes (as if I care).");
            break;

        case 9:
            out.print("No, not until");
            out.println(" Cromwell seizes Dover.");
            break;

        case 10:
            out.print("No, not until");
            out.println(" Nell squeezes Rover.");
            break;

        default:
            out.print("You think you have");
            out.print(" problems?");
            out.print(" My random number");
            out.println(" generator is broken!");
            break;
        }

        out.println("Goodbye");

        keyboard.close();
    }
}
```
