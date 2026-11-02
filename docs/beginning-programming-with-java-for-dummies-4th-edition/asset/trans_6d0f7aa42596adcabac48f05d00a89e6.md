
```
out.println(hankees);
out.print("Socks: ");
out.println(socks);
} else if (gameCancelled) {
    out.println("Sorry, sports fans.");
} else {
    out.println("The game isn't over yet.");
}
```

级联 if 语句并没有什么特别之处。这并不是一种新的编程语言特性。级联 if 语句利用了 Java 中的一个漏洞——在某些情况下省略大括号的漏洞。除此之外，级联 if 语句只是为你在代码中思考决策提供了一种新的方式。

注：列表 10-6 使用了静态导入声明，以避免不必要地重复 System.out 这几个词。要想稍微了解一下静态导入声明（以及我没有更彻底地解释这一概念的道歉），请参阅第 9 章。然后要了解静态导入声明的真正内容，请参阅第 18 章。

## 枚举可能性

第 8 章描述了 Java 的 boolean 类型——只有两个值（true 和 false）的类型。boolean 类型非常方便，但有时你需要更多的值。毕竟，交通灯的值可以是绿色、黄色或红色。扑克牌的花色可以是黑桃、梅花、红心或方块。而一周中的某一天可以是星期一、星期二、星期三、星期四或星期五。

生活充满了各种小的可能性集合，而 Java 有一个特性可以反映这些可能性。该特性称为枚举类型。它从 Java 5.0 版本开始可用。

### 创建枚举类型

列表 10-6 中的故事有三个可能的结局——Hankees 获胜、Socks 获胜，或比赛平局。你可以用下面这行 Java 代码表示这些可能性：

```java
enum WhoWins {home, visitor, neither}
```

本周的比赛在 Hankeeville 的 SnitSoft 球场举行，因此值 home 代表 Hankees 获胜，而值 visitor 代表 Socks 获胜。

计算机编程的一个目标是使每个程序的结构反映程序所解决的问题。当程序提醒你其底层问题时，程序易于理解且维护成本低。例如，用于汇总客户账户的程序应使用 names like customer 和 account 之类的名称。而处理三种可能结果（home wins、visitor wins 和 tie）的程序应该有一个具有三种可能值的变量。行 `enum WhoWins {home, visitor, neither}` 创建了一个用于存储三个值的类型。

WhoWins 类型称为枚举类型。把新的 WhoWins 类型想象成增强版的 boolean。不是两个值（true 和 false），WhoWins 类型有三个值（home、visitor 和 neither）。你可以创建一个 WhoWins 类型的变量：

```java
WhoWins who;
```

然后为新变量赋值：

```java
who = WhoWins.home;
```

在下一节中，我将 WhoWins 类型派上用场。

### 使用枚举类型

列表 10-7 向你展示如何使用全新的 WhoWins 类型。

**列表 10-7：自豪的赢家和沮丧的输家**

```java
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
}
```

**图 10-13：Hankeeville 的喜悦？**

```text
Hankees and Socks scores? 9 4

The Hankees win :-)

Today's game is brought to you by
SnitSoft, the number one software
vendor in the Hankeeville area.
SnitSoft is featured proudly in
Chapter 6. And remember, four out
of five doctors recommend
SnitSoft to their patients.

We beat 'em good. Didn't we?

Hankees and Socks scores? 3 8

The Socks win :-( 

Today's game is brought to you by
SnitSoft, the number one software
vendor in the Hankeeville area.
SnitSoft is featured proudly in
Chapter 6. And remember, four out
of five doctors recommend
SnitSoft to their patients.

The umpire made an unfair call.

Hankees and Socks scores? 0 0

It's a tie :-|

Today's game is brought to you by
SnitSoft, the number one software
vendor in the Hankeeville area.
SnitSoft is featured proudly in
Chapter 6. And remember, four out
of five doctors recommend
SnitSoft to their patients.

The game goes into overtime.
```

列表 10-7 中发生了什么：

- ✔ 我创建一个变量来存储 `WhoWins` 类型的值。就像行 `double amount;` 声明 amount 用于存储 double 值（例如 5.95 和 30.95）一样，行 `WhoWins who;` 声明 who 用于存储 `WhoWins` 值（例如 home、visitor 和 neither）。
- ✔ 我为 `who` 变量赋值。我执行其中一个 `who = WhoWins.something;` 赋值语句。我执行的语句取决于 if 语句中 `hankees > socks` 比较的结果。
- ✔ 我将变量的值与每个 `WhoWins` 值进行比较。在一个 if 语句中，我检查 `who == WhoWins.home` 条件。在剩下的两个 if 语句中，我检查其他 `WhoWins` 值。

请注意，我在列表 10-7 中引用了每个 WhoWins 值。我写 `WhoWins.home`、`WhoWins.visitor` 或 `WhoWins.neither`。如果我忘记 `WhoWins` 前缀并输入 `who = home; //This assignment doesn't work!`，编译器会给出 `home cannot be resolved to a variable` 错误信息。这就是枚举类型的工作方式。

在列表 10-7 的接近末尾，我本可以不用枚举值。我本可以再次测试诸如 `hankees > socks` 之类的条件。

```java
if (hankees > socks) {
    out.println("The Hankees win :-)");
}

// And later in the program...

if (hankees > socks) {
    out.println("We beat 'em good. Didn't we?");
}
```

但这种做法会很笨拙。在更复杂的程序中，我可能会检查 `hankees > socks` 十几次。这就像一遍又一遍地问同一个问题。

而不是反复检查 `hankees > socks` 条件，我将比赛结果存储为枚举值。然后我可以按需多次检查枚举值。这是一种非常整洁的解决重复检查问题的方法。

## 第 11 章：如何拨动虚拟开关

### 本章内容

- 处理多种选择
- 从语句中间跳出
- 处理替代赋值

想象一下用十扇不同的门玩 *Let's Make a Deal*。“选择 1 号门、2 号门、3 号门、4 号门……等等！让我们休息一下做广告。回来后，我会说出另外六扇门的名字。”

Monty Hall 需要的是 Java 的 `switch` 语句。

### 认识 switch 语句

第 9 章中的列表 9-2 中的代码模拟了一个算命玩具——电子神谕。向程序提问，程序会随机生成一个 yes 或 no 的答案。但，就玩具而言，列表 9-2 中的代码并不好玩。该代码只有两种可能的答案。没有变化。甚至最早的会说话的娃娃也能说大约十种不同的句子。

假设你想增强列表 9-2 的代码。调用 `myRandom.nextInt(10) + 1` 生成 1 到 10 的数字。所以也许你可以为十个数字中的每一个显示不同的句子。一大堆 if 语句应该可以解决问题：

```java
if (randomNumber == 1) {
    System.out.println("Yes. Isn't it obvious?");
}
if (randomNumber == 2) {
    System.out.println("No, and don't ask again.");
}
if (randomNumber == 3) {
    System.out.println("Yessir, yessir!");
    System.out.println(" Three bags full.");
}
```
