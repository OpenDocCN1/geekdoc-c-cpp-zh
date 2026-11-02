

## 图7-6 为1.38美元找零

```
How many cents do you have? 138
From 138 cents you get
5 quarters
1 dime
0 nickels
3 cents
```

你继续这样做，直到把所有5美分硬币都扣除完毕。此时，`whatsLeft`的值就只剩下3（表示3美分）。

![](img/f938eba5f15e231d828a6255e7ec5523_157_0.png)

清单7-3中的代码使用以下硬币面额来为美元找零：1美分、5美分（一个nickel）、10美分（一个dime）和25美分（一个quarter）。使用这些面额，MakeChange程序给你的不仅仅是一组加起来等于138美分的硬币。MakeChange类给你的是加起来等于138美分的最少硬币数。只要稍作修改，你就可以让这段代码适用于任何国家的硬币体系。你总能得到一组加起来等于某个总额的硬币。但对于某些国家的硬币面额，你并不总能得到加起来等于某个总额的最少硬币数。事实上，我正在寻找这样的例子。如果你国家的硬币体系导致MakeChange不能总是给出最佳答案，请给我发电子邮件（BeginProg@allmycode.com），在推特上@allmycode，或者在Facebook上发布到/allmycode。谢谢。

![](img/f938eba5f15e231d828a6255e7ec5523_157_1.png)

当两个或多个变量具有相似的类型时，你可以用组合声明来创建这些变量。例如，清单7-3中有两个组合声明——一个用于变量quarters、dimes、nickels和cents（均为int类型）；另一个用于变量whatsLeft和total（均为int类型）。但要创建不同类型的变量，你需要分开声明。例如，要创建名为total的int变量和名为amount的double变量，你需要一个声明`int total;`和另一个声明`double amount;`。

![](img/f938eba5f15e231d828a6255e7ec5523_157_2.png)

清单7-3中有一个对`System.out.println()`的调用，括号里什么都没有。当计算机执行这条语句时，光标会跳到屏幕上的新一行。（我经常用这条语句在程序输出中加入一个空行。）

## 如果你的int冒犯了你，就把它cast掉

图7-6中的运行看起来有点刻意。为什么从138美分开始？为什么不使用更熟悉的1.38美元？原因是数字1.38不是整数，而整数比其他类型的数字更精确。事实上，没有整数，取余运算符就不是很有用。例如，`1.38 % 0.25`的值是0.129999999999999。所有这些9都很难处理。想象一下，你看到信用卡账单上写着欠款$0.129999999999999。你可能会支付$0.13，然后让信用卡公司保留找零。但经过多年的四舍五入，信用卡公司会发大财！第8章会更详细地描述使用double值所导致的不精确性。

在本书中，我用与金钱相关的程序来说明Java的double类型。许多作者也这样做。但为了更高的精度，避免将double值用于金钱。相反，你应该使用int值，或者使用我在本章最后一节中描述的long值。更好的是，在Java API文档中查阅BigInteger和BigDecimal。

这些BigSomethingOrOther类型用起来很麻烦，但它们提供了工业级的数值范围和精度。

那么，如果你想要输入1.38，然后让程序把你输入的1.38变成138美分，该怎么办？你如何让程序做到这一点？

我的第一个想法是将1.38乘以100：

```
//This doesn't quite work.
double amount;
int total;
amount=keyboard.nextDouble();
total=amount*100;
```

在日常算术中，乘以100就能解决问题。但计算机很挑剔。在使用计算机时，当你混合使用int值和double值时，你必须非常小心。（见本边注中的第一张图。）

![](img/f938eba5f15e231d828a6255e7ec5523_158_0.png)

![](img/f938eba5f15e231d828a6255e7ec5523_158_1.png)

要把一个double值塞进一个int变量，你需要一种叫做“强制转换”（casting）的东西。当你转换一个值时，你实际上是在说：“我知道我正在试图把一个double值挤进一个int变量。这很紧，但我无论如何都要这么做。”

要进行强制转换，你把一个类型的名字放在括号中，如下所示：

```
 //This works!
 total = (int) (amount * 100);
```

这种强制转换表示法把double值138.0变成了int值138，于是皆大欢喜。（见本边注中的第二张图。）

## 自增和自减运算符

Java有一些很巧妙的小运算符，能让生活更轻松（对计算机的处理器、你的大脑和你的手指来说都是如此）。总共有四个这样的运算符——两个自增运算符和两个自减运算符。自增运算符加1，自减运算符减1。要了解它们是如何工作的，你需要一些例子。

### 使用前置自增

第一个例子如图7-7所示。

```
class AddMoreGumballs {
    public static void main(String args[]) {
        int gumballs=27;

        ++gumballs;
        System.out.println(gumballs);
        System.out.println(++gumballs);
        System.out.println(gumballs);
    }
}
```

图7-7中的程序的一次运行如图7-8所示。在这次平淡无奇的运行中，gumballs的计数被显示了三次。

图7-8：前置自增代码（图7-7中的代码）的一次运行。

![](img/f938eba5f15e231d828a6255e7ec5523_160_0.png)

双加号根据你放置的位置有两个不同的名称。当你把`++`放在变量前面时，这个`++`被称为前置自增运算符。在“preincrement”这个词中，pre代表“之前”。在这种情境下，“之前”有两个不同的含义：

-   你把`++`放在变量之前。
-   计算机在变量用于语句中任何其他部分之前，先给变量的值加1。

图7-9展示了前置自增运算符动作的慢动作回放。在图7-9中，计算机遇到了`System.out.println(++gumballs)`这条语句。首先，计算机给gumballs加1（把gumballs的值提高到29）。然后，计算机使用gumballs的新值（29）执行`System.out.println`。

图7-9：前置自增运算符在动作中。

![](img/f938eba5f15e231d828a6255e7ec5523_160_1.png)

### 使用后置自增

前置自增的一个替代是后置自增。在后置自增中，post代表“之后”。“之后”这个词有两个不同的含义：

-   你把`++`放在变量之后。
-   计算机在变量用于语句中任何其他部分之后，才给变量的值加1。

图7-10展示了后置自增运算符动作的特写视图。在图7-10中，计算机遇到了`System.out.println(gumballs++)`这条语句。首先，计算机使用gumballs的旧值（28）执行`System.out.println`。然后，计算机给gumballs加1（把gumballs的值提高到29）。

图7-10：后置自增运算符在动作中。

![](img/f938eba5f15e231d828a6255e7ec5523_161_0.png)

看一下图7-11中的粗体代码行。计算机在屏幕上打印gumballs的旧值（28）。只有在打印了这个旧值之后，计算机才给gumballs加1（把gumballs的值从28提高到29）。

图7-11 使用后置自增。

```java
class AddEvenMoreGumballs {
    public static void main(String args[]) {
        int gumballs=27;
        gumballs++;
        System.out.println(gumballs);
        System.out.println(gumballs++);
        System.out.println(gumballs);
    }
}
```

![](img/f938eba5f15e231d828a6255e7ec5523_161_1.png)

![](img/f938eba5f15e231d828a6255e7ec5523_161_2.png)

使用`System.out.println(gumballs++)`时，计算机在打印gumballs已有的旧值之后，才给gumballs加1。

图7-11中的代码的一次运行如图7-12所示。将图7-12与图7-8中的运行进行比较。

图7-12：后置自增代码（图7-11中的代码）的一次运行。

![](img/f938eba5f15e231d828a6255e7ec5523_162_0.png)

-   在图7-8的前置自增中，显示的第二个数字是29。
-   在图7-12的后置自增中，显示的第二个数字是28。

在图7-12中，数字29直到运行结束才出现在屏幕上，那时计算机执行了最后一个`System.out.println(gumballs)`。

![](img/f938eba5f15e231d828a6255e7ec5523_162_1.png)

你是不是在纠结使用前置自增还是后置自增？不用再想了。大多数程序员使用后置自增。在典型的Java程序中，你经常看到像`gumballs++`这样的写法。你很少看到像`++gumballs`这样的写法。

除了前置自增和后置自增之外，Java还有两个使用`--`的运算符。这两个运算符被称为前置自减和后置自减：

-   使用前置自减（`--gumballs`）时，计算机在变量用于语句其余部分之前，先给变量的值减1。
-   使用后置自减（`gumballs--`）时，计算机在变量用于语句其余部分之后，才给变量的值减1。

## 赋值运算符

如果你读过上一节——关于加1运算符的那一节——你可能会想，你是否能够操纵这些运算符来实现加2、加5或加1000000。你能写出`gumballs+++`并且仍然称自己为Java程序员吗？嗯，你不能。如果你尝试这样做，Eclipse会给你一条错误消息：

```
Invalid argument to operation ++/--
```

