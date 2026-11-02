
### 代码清单 10-7（续）

```java
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

代码清单 10-7 程序的三个运行结果如图 10-13 所示。

### 图 10-13：汉基维尔的喜悦？

```
Hankees and Socks scores? 9 4

The Hankees win :-)

Today's game is brought to you by SnitSoft, the number one software vendor in the Hankeeville area.
SnitSoft is featured proudly in Chapter 6. And remember, four out of five doctors recommend SnitSoft to their patients.

We beat 'em good. Didn't we?

Hankees and Socks scores? 3 8

The Socks win :-( 

Today's game is brought to you by SnitSoft, the number one software vendor in the Hankeeville area.
SnitSoft is featured proudly in Chapter 6. And remember, four out of five doctors recommend SnitSoft to their patients.

The umpire made an unfair call.

Hankees and Socks scores? 0 0

It's a tie :-|

Today's game is brought to you by SnitSoft, the number one software vendor in the Hankeeville area.
SnitSoft is featured proudly in Chapter 6. And remember, four out of five doctors recommend SnitSoft to their patients.

The game goes into overtime.
```

代码清单 10-7 中发生了什么：

- ✓ 我创建一个变量来存储 WhoWins 类型的值。
- 就像语句 `double amount;` 声明 amount 用于存储 double 值（例如 5.95 和 30.95）一样，语句 `WhoWins who;` 声明 who 用于存储 WhoWins 值（例如 home、visitor 和 neither）。
- ✓ 我为 who 变量赋值。我执行其中一条 `who = WhoWins.something;` 赋值语句。我执行的语句取决于 if 语句中 hankees > socks 比较的结果。

请注意，我在代码清单 10-7 中引用了 WhoWins 的每个值。我写的是 WhoWins.home、WhoWins.visitor 或 WhoWins.neither。如果我忘记 WhoWins 前缀并输入

```
who = home; //This assignment doesn't work!
```

编译器会给出 home cannot be resolved to a variable 错误信息。这就是枚举类型的工作方式。

- ✓ 我将该变量的值与每个 WhoWins 值进行比较。

在一个 if 语句中，我检查 who == WhoWins.home 条件。在其余两个 if 语句中，我检查其他 WhoWins 值。

在代码清单 10-7 的末尾，我本可以不使用枚举值。我本可以再次测试诸如 hankees > socks 之类的条件。

```
if (hankees > socks) {
    out.println("The Hankees win :-)");
}

// And later in the program...

if (hankees > socks) {
    out.println("We beat 'em good. Didn't we?");
}
```

但这种做法会很笨拙。在更复杂的程序中，我可能会检查 hankees > socks 多达十几次。这就像一遍又一遍地问同一个问题。

而不是反复检查 hankees > socks 条件，我将比赛结果存储为枚举值。然后我可以按需多次检查该枚举值。这是一种非常整洁的解决重复检查问题的方法。

## 第 11 章：如何拨动虚拟开关

### 本章内容

- 处理多种备选方案
- 从语句中间跳出
- 处理替代赋值

想象一下玩 Let's Make a Deal 有十扇不同的门。“选择 1 号门、2 号门、3 号门、4 号门……等等！我们先休息一下做广告。回来后我会说出另外六扇门的名字。”

蒙提·霍尔需要的就是 Java 的 switch 语句。

### 认识 switch 语句

第 9 章中的代码清单 9-2 模拟了一个算命玩具——电子神谕。向程序提问，程序会随机生成 yes 或 no 的答案。但就玩具而言，代码清单 9-2 的代码并不好玩。代码只有两种可能的答案。没有变化。甚至最早的会说话的娃娃也能说大约十种不同的句子。

假设你想增强代码清单 9-2 的代码。调用 myRandom.nextInt(10) + 1 会生成 1 到 10 的数字。因此也许你可以为十个数字中的每一个显示不同的句子。一大堆 if 语句应该可以解决问题：

```java
if (randomNumber == 1) {
    System.out.println("Yes. Isn't it obvious?");
}
if (randomNumber == 2) {
    System.out.println("No, and don't ask again.");
}
if (randomNumber == 3) {
    System.out.print("Yessir, yessir!");
    System.out.println(" Three bags full.");
}
if (randomNumber == 4)
  ...
if (randomNumber < 1 || randomNumber > 10) {
    System.out.print("Sorry, the electronic oracle");
    System.out.println(" is closed for repairs.");
}
```

但这种方法似乎很浪费。为什么不创建一个语句只检查 randomNumber 的值一次，然后根据找到的值采取行动呢？幸运的是，正好有这样的语句：switch 语句。代码清单 11-1 有一个 switch 语句的示例。

### 代码清单 11-1：应对各种场合的答案

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
            out.print("What part of 'no'");
            out.println(" don't you understand?");
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

![](img/6d9dcff12e52b997f3ad31445b712549_236_0.png)

### 图 11-2：一把有 11 个叉的叉子。

### switch 语句中的 default

如果在运行代码清单 11-1 程序时出现严重错误怎么办？假设表达式 `myRandom.nextInt(10) + 1` 生成的数字不在 1 到 10 范围内。那么计算机就会跳过所有 case 子句。计算机不会落在某个 case 子句上，而是跳转到 default 子句。在 default 子句中，计算机显示 `You think you have problems?...`，然后跳出 switch 语句。计算机离开 switch 语句后，会显示 Goodbye。

![](img/6d9dcff12e52b997f3ad31445b712549_236_1.png)

你其实不需要在 switch 语句的最后放置一个 break。在代码清单 11-1 中，最后一个 break（default 子句中的 break）只是为了整体整洁。

