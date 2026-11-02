
## 随机性让我头晕

当你调用 myRandom.nextInt(10) + 1 时，你会得到一个 1 到 10 的数字。作为测试，我写了一个程序调用 myRandom.nextInt(10) + 1 20 次。

```
Random myRandom=new Random();
System.out.print (myRandom.nextInt(10) + 1);
System.out.print(" ");
System.out.print (myRandom.nextInt(10) + 1);
System.out.print(" ");
System.out.print (myRandom.nextInt(10) + 1);
//...And so on.
```

我多次运行程序并得到了下图所示的结果。（实际上，我是从 Eclipse 的 Console 视图复制结果到 Windows Notepad。） briefly 看一下图并注意两个趋势：

- 无法明显预测下一个数字是什么。
- 没有一个数字出现的频率明显高于其他数字。

![](img/6d9dcff12e52b997f3ad31445b712549_201_0.png)

Java 虚拟机费尽心机来维持这些趋势。这是因为以随机方式生成数字是一件非常棘手的事情。以下是该过程的一些有趣事实：

- 科学家和非科学家都使用随机数这个术语。但实际上，并不存在单一的随机数。毕竟，像 9 这样的数字有多随机呢？一个数字只有在它属于一个非常无序的数字集合中时才是随机的。更精确地说，如果用于生成该数字的过程遵循前述两个趋势，那么该数字就是随机的。当他们谨慎时，科学家会避免使用随机数这个术语，而改用随机生成数。

- 很难随机生成数字。计算机程序尽力而为，但最终，今天的计算机程序遵循一种模式，而这种模式并不是真正随机的。要以真正随机的方式生成数字，你需要一个装满乒乓球的大桶，就像州彩票抽奖中所使用的那种。问题是，大多数计算机的周边设备中并不附带装满乒乓球的大桶。因此严格来说，Java 的 Random 类生成的数字并不是随机的。相反，科学家称这些数字为伪随机。

- 这让我们所有人都感到惊讶，但知道一个随机生成的值对于预测下一个随机生成的值毫无帮助。例如，如果你抛硬币两次，两次都得到正面，第三次翻转是否更可能得到反面？不会。仍然是 50-50。如果你有三个儿子，并且你期待第四个孩子，第四个孩子是否更可能是一个女孩？不会。孩子的性别与年长孩子的性别无关。（我忽略了任何生物学效应，而我对这些一无所知。等等！我确实知道一些生物学 trivia：新生儿更可能是一个男孩而不是女孩。每 21 个新生男孩只有 20 个新生女孩。男孩更弱，所以我们死得更快。这就是为什么自然在出生时制造更多我们。）

![](img/6d9dcff12e52b997f3ad31445b712549_202_0.png)

TIP 你不必担心代码缩进，因为 Eclipse 可以自动缩进你的代码。详情请参阅第 4 章。

## 主题的变奏

我不喜欢剥猫皮。但我听说过，如果我真的需要剥一只，我有几种技术可供选择。下次我的猫 Histamine 把地毯误认为猫砂盆时，我会记住这一点。

无论你是在剥鲶鱼、剥小猫，还是编写计算机程序，相同的原则都适用。你总是有替代方案。Listing 9-2 向你展示了一种编写 `if` 语句的方法。本章的其余部分（以及第 10 章的全部内容）向你展示了一些创建 `if` 语句的其他方法。

## ... 否则呢？

你可以在没有 `else` 子句的情况下创建 `if` 语句。例如，想象一个网页，其中每十个随机选择的访客中有一个会收到特别优惠。为了让访客保持猜测，我调用 `Random` 类的 `nextInt` 方法，并向数字为幸运 7 的任何人提供优惠。

- 如果 `myRandom.nextInt(10) + 1` 生成数字 7，则显示特别优惠信息。
- 如果 `myRandom.nextInt(10) + 1` 生成除 7 以外的任何数字，则什么都不做。不要显示特别优惠信息，也不要显示令人沮丧的“对不起，没有优惠给你。”信息。

实现这种策略的代码如 Listing 9-3 所示。代码的几次运行如 Figure 9-5 所示。

Figure 9-5: Listing 9-3 中代码的三种运行。

![](img/6d9dcff12e52b997f3ad31445b712549_203_0.png)

Listing 9-3: 真是幸运？

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

Listing 9-3 中的 if 语句没有 else 子句。此 if 语句具有以下形式：

```
if (Condition) {
    SomeStatements
}
```

当 randomNumber 为 7 时，计算机显示 An offer just for you! 当 randomNumber 不是 7 时，计算机不显示 An offer just for you! 该操作如图 9-6 所示。

始终（我指的是始终）在 if 语句条件中比较两个数字或字符时使用双等号。永远（那就是永远、永远、永远）不要使用单个等号来比较两个值。单个等号执行赋值，而不是比较。

![](img/6d9dcff12e52b997f3ad31445b712549_204_0.png)

Figure 9-6: 如果你没有好话要说，那就不要说任何话。

在 Listing 9-3 中，我擅自添加了一个额外的 println。这个 println（在 main 方法的末尾）显示了我对 nextInt 的调用生成的随机数。在有特别优惠的网页上，你可能看不到随机生成的数字，但如果不知道代码生成的数字，我就无法测试我的 SpecialOffer 代码。

无论如何，请注意 randomNumber 的值在每次运行中都会显示。randomNumber 的 println 不在 if 语句内部。（这个 println 在 if 语句之后。）因此计算机总是执行这个 println。无论 randomNumber == 7 为真还是假，计算机都会采取适当的 if 操作，然后继续执行 System.out.println(randomNumber)。

## 在 if 语句中打包更多内容

这里有一个有趣的情况：你有两个棒球队——Hankees 和 Socks。你想在两行上显示球队的得分，并且获胜者的得分排在前面。（在计算机屏幕上，获胜者的得分显示在失败者的得分上方。在平局的情况下，你显示两个相同的得分，一个在另一个之上。）Listing 9-4 有代码。

Listing 9-4: 让最佳球队先显示

```
import java.util.Scanner;
import static java.lang.System.in;
import static java.lang.System.out;

class TwoTeams {
    public static void main(String args[]) {
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
}
```

Figure 9-7 显示了代码的几次运行。（为了在一张图中显示几次运行，我将结果从 Eclipse 的 Console 视图复制到 Windows Notepad。）

有了大括号，一堆 print 和 println 调用被安全地塞进 if 子句中。另一组 print 和 println 调用被挤进 else 子句中。这就创建了如图 9-8 所示的分叉情况。

Figure 9-7: 看吧？Listing 9-4 中的代码确实有效！

![](img/6d9dcff12e52b997f3ad31445b712549_205_0.png)

