
```
if (num1 >= num2) {
  System.out.print(" red ");
  System.out.print(" orange ");
}
if ((num1 + 5) >= num2) {
  System.out.print(" white ");
} else {
  if ((num1 + 10) >= num2) {
    System.out.print(" black ");
    System.out.print(" blue ");
  } else {
    System.out.print(" yellow ");
  }
}
```

- a. 假设 `num1` 的值为 5，`num2` 的值为 4？

- b. 假设 `num1` 的值为 5，`num2` 的值为 12？

- c. 假设 `num1` 的值为 5，`num2` 的值为 27？

- SR 5.12 写一个表达式，根据 `int` 型变量 `temperature` 的值打印消息。如果 `temperature` 等于或小于 50，在一行打印 "It is cool."，在另一行打印 "Dress warmly."。如果 `temperature` 大于 80，在一行打印 "It is warm."，在另一行打印 "Dress coolly."。如果 `temperature` 在 50 到 80 之间，在一行打印 "It is pleasant."，在另一行打印 "Dress pleasantly."。

## 5.3 比较数据

在使用布尔表达式比较数据时，理解根据检查的数据类型而产生的某些细微差别很重要。让我们来看几种情况。

### 比较浮点数

在比较浮点数据时，会发生一种有趣的情况。根据 `==` 运算符，两个浮点值只有在它们底层表示的所有二进制位都匹配时才相等。如果所比较的值是计算结果，如果它们对于特定情况来说足够接近，那么它们不太可能是完全相等的。因此，在比较浮点数值时，你不应该经常使用相等运算符 `==`。

检查浮点数等性的更好方法是计算两个值之差的绝对值，并将结果与某些容差水平进行比较。例如，我们可以选择 0.00001 的容差水平。如果两个浮点值非常接近，使得它们的差小于容差，我们就愿意认为它们是相等的。比较两个浮点值 `f1` 和 `f2` 可以如下所示实现：

```
if (Math.abs(f1 - f2) < TOLERANCE)
    System.out.println("Essentially equal.");
```

常量 `TOLERANCE` 的值应该适用于这种情况。

### 比较字符

我们知道一个数字小于另一个数字意味着什么，但说一个字符小于另一个字符意味着什么？正如我们在第 2 章中讨论的，Java 中的字符基于 Unicode 字符集，它定义了所有可用字符的排序。字符 `'a'` 在字符集中位于字符 `'b'` 之前，因此我们可以说 `'a'` 小于 `'b'`。

我们可以在字符数据可以使用相等和关系运算符。例如，如果两个变量 `ch1` 和 `ch2` 持有两个字符，我们可以通过如下的 `if` 语句确定它们在 Unicode 字符集中的相对顺序：

> 核心概念
>
> Java 中字符的相对顺序由 Unicode 字符集定义。

```
if (ch1 < ch2)
    System.out.println(ch1 + " " is greater than " + ch2);
else
    System.out.println(ch1 + " is NOT greater than " + ch2);
```

## 5.3 比较数据

要确定两个字符串的相对顺序，请使用 `String` 类的 `compareTo` 方法。`compareTo` 方法比 `equals` 方法更通用。`compareTo` 方法不返回布尔值，而是返回一个整数。如果调用方法的 `String` 对象在作为参数传入的字符串之前（在……之前），则返回值为负。如果两个字符串包含相同的字符，则返回值为零。如果调用方法的 `String` 对象在作为参数传入的字符串之后（大于），则返回值为正。例如：

```java
int result = name1.compareTo(name2);
if (result < 0)
    System.out.println(name1 + " comes before " + name2);
if (result == 0)
    System.out.println("The names are equal.");
System.out.println(name1 + " follows " + name2);
```

请记住，字符比较是基于 Unicode 字符集的（参见附录 C）。这被称为字典序。如果字母字符的大小相同（全大写或全小写），则字典序也将是字母顺序。然而，在比较两个字符串（例如 "able" 和 "Baker"）时，`compareTo` 方法会认为 "Baker" 在前，因为所有大写字母都在所有小写字母之前。另一个较长字符串的前缀字符串被认为在较长字符串之前。例如，在比较两个字符串 "horse" 和 "horsefully" 时，`compareTo` 方法会认为 "horse" 在前。

## 自习题（答案见附录 N）

- SR 5.13 为什么在比较浮点数的相等性时我们必须小心？

- SR 5.14 我们如何比较字符串的相等性？

- SR 5.15 为 4.2 节中的 `Die` 类编写一个 `equals` 方法。如果调用方法的 `Die` 对象与作为参数传入的 `Die` 对象具有相同的 `facevalue`，则方法返回 true，否则返回 false。

- SR 5.16 假设字符串变量 `s1` 和 `s2` 已初始化。编写一个表达式，按字典序分行打印这两个字符串。

## 5.4 while 语句

正如我们在在本章引言中所讨论的，重复语句（或循环）允许我们多次执行另一个语句。`while` 语句是一种循环，它评估布尔条件的方式与 `if` 语句相同，如果条件为真，则执行语句（称为循环体）。然而，与 `if` 语句不同，在执行循环体后，会再次评估条件。如果条件仍为真，则再次执行循环体。这种重复一直持续到 `while` 的条件变为假；然后继续处理 `while` 循环体之后的语句。图 5.7 显示了这种处理过程。

![](img/7f8e069c1898b741edc17dfeed34b0c1_257_0.png)

只要布尔表达式为真，`while` 循环就会重复执行指定的 `Statement`。首先评估表达式；因此，语句可能完全不执行。在每次执行 `Statement` 之后都会评估表达式，直到表达式变为假。

示例：

```java
while (total > max)
{
    total = total / 2;
    System.out.println("Current total: " + total);
}
```

图 5.7 `while` 循环的逻辑

## 5.4 while 语句

以下循环打印从 1 到 5 的值。循环的每次迭代打印一个值，然后增加计数器。

> 核心概念
>
> `while` 语句不断执行同一语句，直到其条件变为假。

```java
int count = 1;
while (count <= 5) {
    System.out.println(count);
    count++;
}
```

注意，`while` 循环的体是一个包含两个语句的块。整个块在循环的每次迭代中重复。

让我们另一个使用 `while` 循环的程序。列表 5.7 显示的 `Average` 程序从用户处读取一系列整数值，对其求和并计算平均值。

我们不知道用户可能会输入多少个值，因此我们需要一种方法来指示用户已完成数字输入。在这个程序中，我们将零指定为哨兵值，表示输入的结束。`while` 循环继续处理输入值，直到用户输入零。这假设零不是应该计入平均值的有效数字。注意在 `Average` 程序中，使用了一个名为 `sum` 的变量来维护累加和，这意味着它是到目前为止输入的值之和。该变量初始化为零，每个值都加回 `sum` 中。

## 列表 5.7

```java
********************************************************************************
// Average.java               Author: Lewis/Loftus
// 展示了 while 循环、哨兵值和
//     累加和的使用。
********************************************************************************

import java.text.DecimalFormat;
import java.util.Scanner;

public class Average {
    // 计算用户输入的一组值的平均值。
    // 随着数字的输入，打印累加和。
    //--------------------------------------------------------------------------------------
    public static void main(String[] args) {
        int sum = 0, count = 0;
        double average;

        Scanner scan = new Scanner(System.in);
```

## 列表 5.7 续

```java
System.out.print("Enter an integer (0 to quit): ");
value = scan.nextInt();

while (value != 0) // 0 为终止哨兵值
{
    count++;

    sum += value;
    System.out.println("The sum so far is " + sum);
}

System.out.println();

if (count == 0) {
    System.out.println("No values were entered.");
} else {
    average = (double)sum / count;
    DecimalFormat fmt = new DecimalFormat("0.###");
    System.out.println("The average is " + fmt.format(average));
}
```

### 输出

Enter an integer (0 to quit): 25

The sum so far is 25

Enter an integer (0 to quit): 164

The sum so far is 189

Enter an integer (0 to quit): 14

The sum so far is 175

Enter an integer (0 to quit): 84

The sum so far is 259

Enter an integer (0 to quit): 12

The sum so far is 271

Enter an integer (0 to quit): -35

The sum so far is 236

Enter an integer (0 to quit): 0

The average is 39.333

## 列表 5.8

```java
// *************************************************
// WinPercentage.java             Author: Lewis/Loft
// 展示了使用 while 循环进行输入验证。
// *************************************************

import java.text.NumberFormat;
import java.util.Scanner;

public class WinPercentage
{
    // 计算队伍获胜比赛的百分比。
    // -------------------------------------
    public static void main(String[] args)
    {
        final int NUM_GAMES = 12;
        int won;
        double ratio;
        Scanner scan = new Scanner(System.in);
```

# 第 5 章 条件判断与循环

# 列表 5.8 继续

```
Scanner scan = new Scanner (System.in);
```

```
System.out.print("Enter the number of games won (0 to "
+ NUM_GAMES + ");");
won = scan.nextInt();
```

```
while (won < 0 || won > NUM_GAMES)
{
  System.out.print("Invalid input. Please reenter: ");
  won = scan.nextInt();
}
```

```
ratio = (double)won / NUM_GAMES;
```

```
NumberFormat fmt = NumberFormat.getPercentInstance();
```

```
System.out.println();
System.out.println("Winning percentage: " + fmt.format(ratio));
```

### 输出

Enter the number of games won (0 to 12): -5

Invalid input. Please reenter: 13

Invalid input. Please reenter: 37

Winning percentage: 58%

我们希望程序是健壮的，这意味着它们能够以尽可能优雅的方式处理潜在问题。在设计程序时，验证输入数据并避免诸如除以零等错误是我们应该有意识地处理的情况。循环和条件判断帮助我们识别并处理此类情况。

# 无限循环

确保循环条件最终会变为假是程序员的责任。如果不是这样，循环体将永远执行下去，或者至少持续到程序被中断。这种情况被称为死循环，是一种常见的错误。

以下是一个死循环的示例：

```
int count = 1;
while (count <= 25) // 警告：这是一个死循环！
{
    System.out.println(count);
    count = count - 1;
}
```

如果你执行了这个循环，应该准备好中断它。在大多数系统上，按下 Control-C 组合键（按住 Control 键并按 C）可以终止正在运行的程序。

在这个示例中，`count` 的初始值为 1，并在循环体中递减。只要 `count` 小于或等于 25，`while` 循环就会继续。因为 `count` 将始终为真，或者至少 `count` 的值会小到发生溢出错误。关键点在于代码的逻辑显然是错误的。

> 核心概念
>
> 我们仔细地设计程序以避免死循环。

让我们来看其他死循环的示例：

```
int count = 1;
while (count != 50) // 死循环
count += 2;
```

在这段代码中，变量 `count` 被初始化为 1，并向正方向移动。然而，请注意，它每次增加 2。这个循环永远不会终止，因为 `count` 永远不会等于 50。它从 1 开始，然后变为 3、5 等。最终它会达到 49，然后变为 51、53，并永远地持续下去。

现在考虑以下情况：

```
double num = 1.0;
while (num != 0.0) // 死循环
num = num - 0.1;
```

同样，循环变量的值似乎似乎在朝着正确的方向移动。事实上，`num` 似乎最终会取到 0.0 的值。然而，这个循环是无限的（至少在某些系统上是如此），`num` 的值永远不会恰好等于 0.0。这与我们之前在本章中探索在 `if` 语句条件中比较浮点数时遇到的情况类似。由于二进制表示这些值的方式，内部会发生微小的计算误差，使得比较两个浮点数是否相等变得很有问题。

# 嵌套循环

循环的体可以包含另一个循环。这种情况被称为嵌套循环。请记住，对于外层循环的每一次迭代，内层循环都会完全执行。考虑以下代码片段。字符串 "Here again" 被打印了多少次？

```
int count1, count2;
count1 = 1;
while (count1 <= 10)
{
    count2 = 1;
    while (count2 <= 50)
    {
        System.out.println("Here again");
        count2++;
    }
    count1++;
```

`println` 语句位于内层循环内部。外层循环执行 10 次，因为 `count1` 在 1 到 10 之间迭代。内层循环执行 50 次，因为 `count2` 在 1 到 50 之间迭代。对于外层循环的每一次迭代，`println` 语句被执行了 500 次。

与任何循环情况一样，我们必须仔细检查循环的条件和变量的初始化。让我们考虑如果外层循环是 `(count1 < 10)` 而不是 `count1 <= 10` 会怎样？这如何改变打印的总行数？外层循环将执行 9 次而不是 10 次，所以 `println` 语句将执行 450 次。如果外层循环保持原始定义，但在内层循环之前将 `count2` 初始化为 11 而不是 1 呢？内层循环将执行 40 次而不是 50 次，因此打印的总行数将 400 行。

让我们来看另一个使用嵌套循环的示例。回文（palindrome）是一个正读和反读都相同的字符字符串。例如，以下字符串是回文：
