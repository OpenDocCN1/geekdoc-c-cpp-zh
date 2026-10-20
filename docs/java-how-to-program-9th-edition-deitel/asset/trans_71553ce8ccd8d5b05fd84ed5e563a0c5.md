
如示例输出所示，对 nextInt 生成的值进行缩放和平移，使程序能够模拟掷一个六面骰子。应用程序使用嵌套控制语句（switch 嵌套在 for 内）来确定骰子每一面出现的次数。for 语句（第21–47行）迭代 6,000,000 次。在每次迭代中，第23行生成一个 1 到 6 的随机值。该值随后用作 switch 语句（第26–46行）的控制表达式（第26行）。根据骰子的面值，switch 语句在每次循环迭代中递增六个计数器变量之一。当我们在第7章学习数组时，将展示一种优雅的方法，用一条语句替换该程序中的整个 switch 语句！这个 switch 语句没有 default 情况，因为我们针对第23行表达式可能产生的每个骰子值都有一个 case。运行程序，观察结果。你会看到，每次运行该程序，它都会产生不同的结果。

## 6.9.1 随机数的通用缩放与平移

之前，我们使用以下语句模拟掷一个六面骰子：

```
face = 1 + randomNumbers.nextInt( 6 );
```

该语句始终将 1 ≤ face ≤ 6 范围内的整数赋给变量 face。此范围的宽度（即该范围内连续整数的个数）为 6，且范围起始数为 1。在前面的语句中，范围的宽度由作为参数传给 Random 方法 nextInt 的数字 6 决定，范围的起始数则是加到 randomNumberGenerator.nextInt(6) 上的数字 1。我们可以将这一结果概括为：

```
number = shiftingValue + randomNumbers.nextInt( scalingFactor );
```

其中 shiftingValue 指定所需连续整数范围内的第一个数，scalingFactor 指定该范围内有多少个数。

还可以从连续整数范围以外的值集合中随机选择整数。例如，要从序列 2、5、8、11 和 14 中获得一个随机值，可以使用以下语句：

```
number = 2 + 3 * randomNumbers.nextInt( 5 );
```

在这种情况下，randomNumberGenerator.nextInt(5) 产生 0–4 范围内的值。每个产生的值都乘以 3，得到序列 0、3、6、9 和 12 中的一个数。我们将 2 加到该值上，以平移值范围，从而从序列 2、5、8、11 和 14 中获得一个值。我们可以将这一结果概括为：

```
number = shiftingValue +
    differenceBetweenValues * randomNumbers.nextInt( scalingFactor );
```

其中 shiftingValue 指定所需值范围内的第一个数，differenceBetweenValues 表示序列中连续数字之间的恒定差值，scalingFactor 指定该范围内有多少个数。

## 6.9.2 随机数的可重复性用于测试与调试

Random 类的方法实际上基于复杂的数学计算生成伪随机数——这组数字看起来是随机的。生成这些数字的计算使用一天中的时间作为种子值来改变序列的起始点。每个新的 Random 对象在创建时都会基于计算机系统的时钟值来设置自身的种子，从而使程序的每次执行都会产生不同的随机数序列。

在调试应用程序时，通常需要在每次程序执行时重复完全相同的伪随机数序列。这种可重复性使您能够在用不同的随机数序列进行测试之前，证明您的应用程序对某个特定的随机数序列是有效的。当可重复性很重要时，您可以按如下方式创建 Random 对象：

```
Random randomNumbers = new Random( seedValue );
```

seedValue 参数（类型为 long）为随机数计算提供种子。如果每次都使用相同的 seedValue，Random 对象将产生相同的数字序列。您可以在程序执行期间随时通过调用对象的 set 方法来设置 Random 对象的种子，例如：

```
randomNumbers.set( seedValue );
```

错误预防提示 6.2

在开发程序时，使用特定的种子值创建 Random 对象，以便每次程序执行时产生可重复的数字序列。如果出现逻辑错误，请修复错误并使用相同的种子值再次测试程序——这样可以重建导致错误的那一相同数字序列。一旦逻辑错误被移除，在不使用种子值的情况下创建 Random 对象，使 Random 对象在每次程序执行时生成新的随机数序列。

## 6.10 案例研究：机会游戏；引入枚举

一种流行的机会游戏是掷骰子游戏，称为 craps（双骰子），在世界各地的赌场和后巷中都有玩耍。游戏规则很简单：

> 你掷两颗骰子。每颗骰子有六个面，分别包含一、二、三、四、五和六个点。骰子停下后，计算两个朝上的面上的点数之和。如果第一次掷出的和为 7 或 11，你就赢了。如果第一次掷出的和为 2、3 或 12（称为“craps”），你就输了（即“庄家”赢）。如果第一次掷出的和为 4、5、6、8、9 或 10，那么该和数就成为你的“点数”。要获胜，你必须继续掷骰子，直到“掷出你的点数”（即掷出相同的点数）。如果在掷出点数之前掷出 7，你就输了。

图 6.8 模拟了 craps 游戏，使用方法来实现游戏逻辑。main 方法（第21–65行）在必要时调用 rollDice 方法（第68–81行）来掷骰子并计算它们的和。示例输出显示了首轮掷骰即赢或输，以及后续轮次赢或输的情况。

```
1  // Fig. 6.8: Craps.java
2  // Craps class simulates the dice game craps.
3  import java.util.Random;
```

```
55        else
56        if ( sumOfDice == SEVEN ) // lose by rolling 7 before point
57        gameStatus = Status.LOST;
58    } // end while
59
60    // display won or lost message
61    if ( gameStatus == Status.WON )
62        System.out.println( "Player wins" );
63    else
64        System.out.println( "Player loses" );
65    } // end main
66
67    // roll dice, calculate sum and display results
68    public static int rollDice()
69    {
70        // pick random die values
71        int die1 = 1 + randomNumbers.nextInt( 6 ); // first die roll
72        int die2 = 1 + randomNumbers.nextInt( 6 ); // second die roll
73
74        int sum = die1 + die2; // sum of die values
75
76        // display results of this roll
77        System.out.printf( "Player rolled %d + %d = %d\n",
78            die1, die2, sum );
79
80        return sum; // return sum of dice
81    } // end method rollDice
82 } // end class Craps
```

```
Player rolled 5 + 6 = 11
Player wins
```

```
Player rolled 5 + 4 = 9
Point is 9
Player rolled 4 + 2 = 6
Player rolled 3 + 6 = 9
Player wins
```

```
Player rolled 1 + 2 = 3
Player loses
```

```
Player rolled 2 + 6 = 8
Point is 8
Player rolled 5 + 1 = 6
Player rolled 2 + 1 = 3
Player rolled 1 + 6 = 7
Player loses
```

图 6.8 | Craps 类模拟掷骰子游戏 craps。（第 3 部分，共 3 部分。）

## rollDice 方法

在游戏规则中，玩家第一次掷骰子时必须掷两颗骰子，并且之后每次掷骰子时也必须如此。我们声明 rollDice 方法（图 6.8，第68–81行）来掷骰子并计算和打印它们的和。rollDice 方法只声明一次，但从 main 中的两处（第26行和第50行）调用，其中 main 包含了一局完整的 craps 游戏逻辑。rollDice 方法不接受任何参数，所以它的参数列表为空。每次调用时，rollDice 返回骰子之和，因此方法头（第68行）中指明返回类型为 int。虽然第71行和第72行看起来相同（除了骰子变量名），但它们不一定产生相同的结果。这两条语句都会产生一个 1–6 范围内的随机值。变量 randomNumbers（在第71–72行使用）不是在方法中声明的，而是作为类的 private static final 变量在第8行声明并初始化。这使我们能够创建一个 Random 对象，并在每次调用 rollDice 时复用。如果某个程序包含多个 Craps 类实例，它们都会共享这一个 Random 对象。

## main 方法的局部变量

这个游戏相当复杂。玩家可能在第一次掷骰时赢或输，也可能在后续任意一次掷骰时赢或输。main 方法（第21–65行）使用局部变量 myPoint（第23行）来存储玩家在第一次掷骰未赢未输时的“点数”，使用局部变量 gameStatus（第24行）来跟踪整体游戏状态，并使用局部变量 sumOfDice（第26行）来保存最近一次掷骰的点数和。变量 myPoint 被初始化为 0 以确保应用程序能够编译。如果不初始化 myPoint，编译器会报错，因为 myPoint 在 switch 语句的每一种情况中并不都被赋值，因此程序可能会在 myPoint 被赋值之前就试图使用它。相比之下，gameStatus 在 switch 语句的每一种情况中都会被赋值，因此它在使用前保证已被初始化，无需初始化。

## enum 类型 Status

局部变量 gameStatus（第24行）被声明为一种名为 Status 的新类型（在第11行声明）。Status 类型是类 Craps 的 private 成员，因为 Status 只会在该类中使用。Status 是一种称为枚举的类型，其最简单的形式是声明一组由标识符表示的常量。枚举是一种特殊的类，由关键字 enum 和类型名（这里为 Status）引入。与类一样，花括号分隔枚举声明的主体。花括号内是一个逗号分隔的枚举常量列表，每个常量代表一个唯一的值。枚举中的标识符必须唯一。你将在第8章中了解更多关于枚举的内容。

![](img/009e962758dcc71dbc43a493362e6dc0_255_0.png)

## 良好编程实践 6.1

> 惯例是枚举常量的名称中只使用大写字母。这使它们更加突出，并提醒您它们不是变量。

Status 类型的变量只能赋值为枚举中声明的三个常量之一（第11行），否则会发生编译错误。当游戏获胜时，程序将局部变量 gameStatus 设置为 Status.WON（第33行和第54行）。当游戏失败时，程序将局部变量 gameStatus 设置为 Status.LOST（第38行和第57行）。否则，程序将局部变量 gameStatus 设置为 Status.CONTINUE（第41行），表示游戏尚未结束，必须再次掷骰子。

