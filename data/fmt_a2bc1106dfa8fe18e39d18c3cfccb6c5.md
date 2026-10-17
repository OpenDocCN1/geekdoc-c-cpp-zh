
`adjustment = MAX - height;`

### 关键概念
`if-else` 语句允许程序在条件为真时做一件事，在条件为假时做另一件事。

如果条件为真，执行第一条赋值语句；如果条件为假，执行第二条赋值语句。二者只能执行其一，因为布尔条件的计算结果要么为 `true` 要么为 `false`。注意，这里再次使用了恰当的缩进，以表明这些语句属于主导的 `if` 语句的一部分。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_243_0.png)

`if` 语句测试布尔表达式 `Expression`，如果为真，则执行第一条 `Statement`。可选的 `else` 子句指定当 `Expression` 为假时应执行的 `Statement`。

示例：

```
if (tal < 7)
    System.out.println ("Total is less than 7.");
```

```
if (firstCh != 'a')
    count++;
else
    count = count / 2;
```

代码清单 5.2 中的 `Wages` 程序使用 `if-else` 语句来计算员工应得的工资。

在 `Wages` 程序中，如果员工一周工作超过 40 小时，工资金额会考虑加班时间。程序使用 `if-else` 语句来判断用户输入的小时数是否大于 40。如果是，额外的小时数按正常工资的 1.5 倍支付。如果没有加班时间，则总工资仅根据工作小时数和标准工资率计算。

我们再来看一个 `if-else` 语句的示例：

```
if (roster.getSize() == FULL)
    roster.expand();
else
    roster.addName (name);
```

### 代码清单 5.2

```java
//****************************************************************
// Wages.java        Author: Lewis/Loftus
//
// Demonstrates the use of an if-else statement.
//****************************************************************
import java.text.NumberFormat;
import java.util.Scanner;
public class Wages
{
    //-------------------------------------------------------------
    // Reads the number of hours worked and calculates wages.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final double RATE = 8.25;  // regular pay rate
        final int STANDARD = 40;   // standard hours in a work week
        Scanner scan = new Scanner (System.in);
        double pay = 0.0;
        System.out.print ("Enter the number of hours worked: ");
        int hours = scan.nextInt();
        System.out.println ();
        // Pay overtime at "time and a half"
        if (hours > STANDARD)
            pay = STANDARD * RATE + (hours-STANDARD) * (RATE * 1.5);
        else
            pay = hours * RATE;
        NumberFormat fmt = NumberFormat.getCurrencyInstance();
        System.out.println ("Gross earnings: " + fmt.format(pay));
    }
}
```

### 输出

```
Enter the number of hours worked: 46
Gross earnings: $404.25
```

该示例使用了一个名为 `roster` 的对象。即使不知道 `roster` 代表什么，或者它是由哪个类创建的，我们也能看出它至少有三个方法：`getSize`、`expand` 和 `addName`。`if` 语句的条件调用 `getSize`，并将结果与常量 `FULL` 进行比较。如果条件为真，则调用 `expand` 方法（显然是为了扩展 `roster` 的大小）。如果 `roster` 尚未满，则将变量 `name` 作为参数传递给 `addName` 方法。

代码清单 5.3 中的程序实例化了一个 `Coin` 对象，通过调用 `flip` 方法抛掷硬币，然后使用 `if-else` 语句根据结果决定打印两句话中的哪一句。

### 代码清单 5.3

```java
//****************************************************************
// CoinFlip.java      Author: Lewis/Loftus
//
// Demonstrates the use of an if-else statement.
//****************************************************************
public class CoinFlip
{
    //------------------------------------------------------------
    // Creates a Coin object, flips it, and prints the results.
    //------------------------------------------------------------
    public static void main (String[] args)
    {
        Coin myCoin = new Coin();
        myCoin.flip();
        System.out.println (myCoin);
        if (myCoin.isHeads())
            System.out.println ("You win.");
        else
            System.out.println ("Better luck next time.");
    }
}
```

### 输出

```
Tails
Better luck next time.
```

`Coin` 类如代码清单 5.4 所示。它存储两个整数常量（`HEADS` 和 `TAILS`），代表硬币的两种可能状态，以及一个名为 `face` 的实例变量，代表硬币的当前状态。`Coin` 构造函数首先通过调用 `flip` 方法抛掷硬币，该方法通过随机选择一个数字（0 或 1）来确定硬币的新状态。`isHeads` 方法根据硬币当前的 `face` 值返回一个布尔值。`toString` 方法使用 `if-else` 语句来决定返回哪个字符串来描述硬币。当 `myCoin` 对象在 `main` 方法中传递给 `println` 时，`toString` 方法会被自动调用。

## 使用块语句

我们可能希望在布尔条件求值后执行多件事。在 Java 中，我们可以用块语句替换任意单条语句。

## 第 5 章 条件语句和循环

### 代码清单 5.4

```java
//*****************************
// Coin.java Author: Lewis/Loftus
// Represents a coin with two sides that can be flipped.
//*****************************
public class Coin
{
    private final int HEADS = 0;
    private final int TAILS = 1;
    private int face;
    /**
     * Sets up the coin by flipping it initially.
     */
    public Coin()
    {
        flip();
    }
    /**
     * Flips the coin by randomly choosing a face value.
     */
    public void flip()
    {
        face = (int) (Math.random() * 2);
    }
    /**
     * Returns true if the current face of the coin is heads.
     */
    public boolean isHeads()
    {
        return (face == HEADS);
    }
    /**
     * Returns the current face of the coin as a string.
     */
    public String toString()
    {
        String faceName;
        if (face == HEADS)
            faceName = "Heads";
        else
            faceName = "Tails";
        return faceName;
    }
}
```

块语句是一组用大括号括起来的语句集合。我们在之前的示例中多次使用这些大括号来包含方法和类的定义。

程序 `Guessing` 在代码清单 5.5 中展示，使用了一个 `if-else` 语句，其中 `else` 子句的语句是一个块语句。

如果用户输入的猜测等于随机选择的答案，就会打印出适当的确认信息。然而，如果答案不正确，则会打印两条语句，一条说明猜测错误，另一条打印实际答案。本章末尾的一个编程项目将此示例的概念扩展为 Hi-Lo 游戏。

请注意，如果没有使用块大括号，说明答案不正确的句子会在答案错误时打印，但揭示正确答案的句子会在所有情况下都打印。也就是说，只有第一条语句才会被视为 `else` 子句的一部分。

请记住，除对人类阅读者之外，缩进没有任何意义。语句如果没有正确分组，可能会导致程序员对代码的执行方式产生错误的假设。例如，以下代码具有误导性：

```java
if (depth >= UPPER_LIMIT)
    delta = 100;
else
    System.out.println ("WARNING: Delta is being reset to ZERO");
    delta = 0;  // not part of the else clause!
```

缩进（更不用说代码的逻辑）暗示变量 `delta` 仅在 `depth` 小于 `UPPER_LIMIT` 时才被重置为零。然而，如果不使用块，重置 `delta` 为零的赋值语句根本不受 `if-else` 语句的控制。它在任何情况下都会执行，这显然不是预期的结果。

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_248_0.png)

### 代码清单 5.5

```java
//***************************************************************************
// Guessing.java      Author: Lewis/Loftus
//
// Demonstrates the use of a block statement in an if-else.
//***************************************************************************
import java.util.*;
public class Guessing
{
    //-------------------------------------------------------------
    // Plays a simple guessing game with the user.
    //-------------------------------------------------------------
    public static void main (String[] args)
    {
        final int MAX = 10;
        int answer, guess;
        Scanner scan = new Scanner (System.in);
        Random generator = new Random();
        answer = generator.nextInt(MAX) + 1;
        System.out.print ("I'm thinking of a number between 1 and "
                         + MAX + ". Guess what it is: ");
        guess = scan.nextInt();
        if (guess == answer)
            System.out.println ("You got it! Good guessing!");
        else
        {
            System.out.println ("That is not correct, sorry.");
            System.out.println ("The number was " + answer);
        }
    }
}
```

### 输出结果

```text
I'm thinking of a number between 1 and 10. Guess what it is: 7
That is not correct, sorry.
The number was 5
```

块语句可以在 Java 语法要求单个语句的任何地方使用。例如，`if-else` 语句的 `if` 部分可以是一个块，或者 `else` 部分可以是一个块（如我们在 `Guessing` 程序中看到的），或者两部分都可以是块语句。例如：

```java
if (boxes != warehouse.getCount())
{
    System.out.println ("Inventory and warehouse do NOT match.");
    System.out.println ("Beginning inventory process again!");
    boxes = 0;
}
else
{
    System.out.println ("Inventory and warehouse MATCH.");
    warehouse.ship();
}
```

在此 `if-else` 语句中，`boxes` 的值与通过调用 `warehouse` 对象的 `getCount` 方法获得的值进行比较（无论那是什么）。如果它们不完全匹配，则执行两个 `println` 语句和一个赋值语句。如果它们匹配，则打印不同的消息并调用 `warehouse` 的 `ship` 方法。

### 嵌套 if 语句

作为 `if` 语句结果而执行的语句可能又是另一个 `if` 语句。这种情况称为 *嵌套 if*。它允许我们在确定之前决策的结果后做出另一个决策。代码清单 5.6 中的程序 `MinOfThree` 使用嵌套 `if` 语句来确定用户输入的三个整数值中的最小值。

仔细追踪 `MinOfThree` 程序的逻辑，使用最小值位于三个位置中的各种输入集，以了解它如何确定最低值。

嵌套 `if` 语句会出现一个重要情况。看起来在嵌套 `if` 之后出现的 `else` 子句可能适用于任一 `if` 语句。例如：

```java
if (code == 'R')
    if (height <= 20)
        System.out.println ("Situation Normal");
    else
        System.out.println ("Bravo!");
```

### 代码清单 5.6

```java
//********************************************************************
// MinOfThree.java      Author: Lewis/Loftus
//
// Demonstrates the use of nested if statements.
//********************************************************************
import java.util.Scanner;
public class MinOfThree
{
