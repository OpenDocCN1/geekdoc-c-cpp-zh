

## 5.4 while 语句

正如本章引言中所讨论的，重复语句（或循环）允许我们多次执行另一条语句。while 语句是一种循环，它像 if 语句一样评估布尔条件，并在条件为真时执行一条语句（称为循环体）。然而，与 if 语句不同，执行完体之后，条件会被再次评估。如果条件仍然为真，则再次执行体。这种重复会一直持续到条件变为假为止；然后处理会继续执行 while 循环体之后的语句。图 5.7 显示了这种处理。

### While Statement

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_257_0.png)

while 循环只要布尔表达式为真，就会重复执行指定的语句。表达式首先被评估；因此语句可能根本不会被执行。每次执行语句后，表达式都会被再次评估，直到表达式变为假。

示例：

```
while (total > max)
{
    total = total / 2;
    System.out.println ("Current total: " + total);
}
```

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_257_1.png)

图 5.7 while 循环的逻辑

下面的循环打印从 1 到 5 的值。每次循环迭代打印一个值，然后递增计数器。

```
int count = 1;
while (count <= 5)
{
    System.out.println (count);
    count++;
}
```

KEY CONCEPT
while 语句在条件变为假之前一直执行相同的语句。

请注意，while 循环的体是一个包含两个语句的块。整个块在每次循环迭代时都会重复。

让我们再看一个使用 while 循环的程序。列表 5.7 中显示的 Average 程序从用户读取一系列整数值，将它们求和并计算平均值。

我们不知道用户可能输入多少个值，因此我们需要一种方法来指示用户已完成输入数字。在此程序中，我们指定零为哨兵值，表示输入结束。while 循环会一直处理输入值，直到用户输入零为止。这假设零

### LISTING 5.7

```
//****************************************************************
// Average.java        Author: Lewis/Loftus
//
// Demonstrates the use of a while loop, a sentinel value, and a
// running sum.
//****************************************************************

import java.text.DecimalFormat;
import java.util.Scanner;

public class Average
{
    //-------------------------------------------------------------
    // Computes the average of a set of values entered by the user.
    // The running sum is printed as the numbers are entered.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        int sum = 0, value, count = 0;
        double average;

        Scanner scan = new Scanner (System.in);
```

### LISTING 5.7 continued

```
System.out.print ("Enter an integer (0 to quit): ");
value = scan.nextInt();

while (value != 0) // sentinel value of 0 to terminate loop
{
    count++;

    sum += value;
    System.out.println ("The sum so far is " + sum);

    System.out.print ("Enter an integer (0 to quit): ");
    value = scan.nextInt();
}

System.out.println ();

if (count == 0)
    System.out.println ("No values were entered.");
else
{
    average = (double)sum / count;

    DecimalFormat fmt = new DecimalFormat ("0.###");
    System.out.println ("The average is " + fmt.format(average));
}
}
```

### OUTPUT

```
Enter an integer (0 to quit): 25
The sum so far is 25
Enter an integer (0 to quit): 164
The sum so far is 189
Enter an integer (0 to quit): -14
The sum so far is 175
Enter an integer (0 to quit): 84
The sum so far is 259
Enter an integer (0 to quit): 12
The sum so far is 271
Enter an integer (0 to quit): -35
The sum so far is 236
Enter an integer (0 to quit): 0

The average is 39.333
```

不是应计入平均值的有效数字之一。哨兵值必须始终在输入值的正常范围之外。

请注意，在 Average 程序中，一个名为 sum 的变量用于维护一个运行总和，这意味着它是迄今为止输入值的总和。变量 sum 初始化为零，并且每次读取的值都会被加到 sum 上并存储回 sum。

我们还必须计算输入值的数量，以便在循环结束后可以除以适当的值来计算平均值。请注意，哨兵值不计入计数。考虑用户在输入任何有效值之前立即输入哨兵值的特殊情况。程序末尾的 if 语句避免了除零错误。

让我们再检查一个使用 while 循环的程序。列表 5.8 中显示的 WinPercentage 程序根据获胜场次计算体育队的胜率。

我们在 WinPercentage 程序中使用 while 循环来验证输入，这意味着我们保证用户输入的值是我们认为有效的值。在此示例中，这意味着获胜场次必须大于或等于零且小于或等于比赛总数。while 循环会继续执行，反复提示用户输入有效输入，直到输入的数字确实有效为止。

```
//******************************
// WinPercentage.java Author: Lewis/Loftus
// Demonstrates the use of a while loop for input validation.
//******************************
import java.text.NumberFormat;
import java.util.Scanner;

public class WinPercentage
{
//----------------------
// Computes the percentage of games won by a team.
//----------------------
public static void main (String[] args)
{
final int NUM_GAMES = 12;
int won;
double ratio;
```

### LISTING 5.8 continued

```
Scanner scan = new Scanner (System.in);

System.out.print ("Enter the number of games won (0 to "
    + NUM_GAMES + "):");
won = scan.nextInt();

while (won < 0 || won > NUM_GAMES)
{
    System.out.print ("Invalid input. Please reenter: ");
    won = scan.nextInt();
}

ratio = (double)won / NUM_GAMES;

NumberFormat fmt = NumberFormat.getPercentInstance();

System.out.println ();
System.out.println ("Winning percentage: " + fmt.format(ratio));
}
```

### OUTPUT

```
Enter the number of games won (0 to 12): -5
Invalid input. Please reenter: 13
Invalid input. Please reenter: 7

Winning percentage: 58%
```

我们通常希望我们的程序具有健壮性，这意味着它们尽可能优雅地处理潜在问题。验证输入数据和避免诸如除零之类的错误是我们在设计程序时应有意识解决的情况。循环和条件有助于我们识别和处理此类情况。

### Infinite Loops

程序员有责任确保循环的条件最终会变为假。如果不会，循环体将永远执行，或者至少直到程序被中断为止。这种情况被称为无限循环，是一个常见的错误。

下面是无限循环的一个示例：

```
int count = 1;
while (count <= 25)  // Warning: this is an infinite loop!
{
    System.out.println (count);
    count = count - 1;
}
```

如果执行此循环，您应准备好中断它。在大多数系统上，按下 Control-C 键盘组合键（按住 Control 键并按 C）会终止正在运行的程序。

在此示例中，count 的初始值为 1，并在循环体中递减。只要 count 小于或等于 25，while 循环就会继续。因为 count 每次迭代都会变小，所以条件将始终为真，或者至少直到 count 的值变得如此之小以至于发生下溢错误。关键是代码的逻辑明显是错误的。

> KEY CONCEPT
> 我们必须仔细设计程序以避免无限循环。

让我们再看一些无限循环的其他示例：

```
int count = 1;
while (count != 50)  // infinite loop
    count += 2;
```

在此代码片段中，变量 count 初始化为 1 并朝正方向移动。然而，请注意它每次递增 2。此循环永远不会终止，因为 count 永远不会等于 50。它从 1 开始，然后变为 3，然后是 5，依此类推。最终它达到 49，然后变为 51，然后是 53，并永远继续下去。

现在考虑以下情况：

```
double num = 1.0;
while (num != 0.0)  // infinite loop
    num = num - 0.1;
```

再次，循环控制变量的值似乎朝正确的方向移动。而且，事实上，看起来 num 最终会取值为 0.0。然而，此循环是无限的（至少在大多数系统上是如此），因为 num 永远不会恰好等于 0.0。这种情况与本章前面讨论过的在 if 语句条件中比较浮点值的情况类似。由于值在二进制中的表示方式，内部会发生微小的计算误差，使得比较两个浮点值是否相等变得有问题。

