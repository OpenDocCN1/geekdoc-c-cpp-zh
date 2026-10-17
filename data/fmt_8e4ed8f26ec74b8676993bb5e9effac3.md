
在典型的治疗中，患者躺下，操作人员调整身体的相应区域。操作人员在机器计算机控制台上设置治疗参数，并按下按钮释放辐射。患者被告知，典型的副作用是轻微的皮肤不适，类似于轻微灼伤的感觉。

在事故案例中，一些患者报告感到“巨大的热量感”或“电刺般的冲击”。在其中一个案例中，患者因辐射损伤失去了了肩膀和手臂的功能，并被迫切除了左乳房。另几个人死于放射性中毒。

释放的辐射量以`rad`（辐射吸收剂量）为单位测量。标准治疗量约为`200 rad`。据估计，这些事故导致了`20,000 rad`的剂量照射。

## 产生原因

操作人员告诉他们，`Therac-25`拥有如此多的安全措施，“几乎不可能”给患者造成过量辐射。但`Therac-25`使用的部分软件重用了之前更早版本的机器，而该版本包含了许多基于硬件的安全措施。因此，硬件特征

![](img/7f8e069c1898b741edc17dfeed34b0c1_294_0.png)

> 放射治疗设备投射精确的定向辐射。

掩盖了底层软件中的问题。`Therac-25`的安全功能主要是基于软件的，潜伏的问题随之浮现。

事实证明，操作员输错了参数并以特定的方式进行了纠正，结果软件允许机器在没有适当扩散的情况下释放最大剂量。这是一种非常奇怪的错误，导致技术人员无法重现该问题。在某一次，一台显然导致了过量辐射的机器在技术人员发现其没有问题后又被投入使用。

分析人士表示，软件问题只是发生事故的原因之一。虽然存在基础性的编程错误，但对整体安全问题也缺乏关注。而且由于某些机器的使用时间过长，导致报告并没有像应该的那样准确和彻底。

## 教训

软件安全是本案中的核心问题。当人类生命面临危险时，很难想象不去竭尽一切全力来确保你的软件尽可能健壮。这归结为风险分析。你愿意多大程度上承担你正在开发的特定部分软件仍包含错误的风险？对于许多应用来说，问题可能会给用户带来不便并可能产生业务影响，但其他应用则直接关乎人的生命。

来源：`computingcases.org`, `IEEE Computer`

## 更多条件语句和循环

### 章节目标

- 检查使用`switch`语句的条件处理。
- 讨论条件运算符。
- 检查替代的循环语句：`do`循环和`for`循环。
- 借助条件和循环绘制图形。
- 探索对话框的使用。

在第 5 章中，我们检查了用于决策的`if`语句和用于循环的`while`语句。本章将探索 Java 中用于执行类似任务的几条额外语句。特别在本章中，我们将探索`switch`语句，它允许我们根据特定值在几条执行路径之间进行选择。我们还将探索`do`和`for`循环，它们提供了区别于`while`循环的逻辑处理和/或语法。这些替代语句在细节上不同，任何特定情况都可能适合使用一种而非另一种。本章的“图形轨道”部分探索了如何使用条件和循环来控制图形，并检查了对话框的作用和用法。

![](img/7f8e069c1898b741edc17dfeed34b0c1_296_0.png)

### 6.1 switch语句

Java 中的另一种条件语句称为`switch`语句，它导致执行中的程序根据单个值遵循几条路径之一。可以使用多个`if`语句构建类似的逻辑，但在需要的情况下，`switch`语句通常使代码更易于阅读。

`switch`语句评估一个表达式以确定一个值，然后将该值与几个可能的`case`进行匹配。每个`case`都有关联的语句。评估表达式后，控制将跳转到与匹配值的第一个`case`相关的语句。考虑以下示例：

```
switch (idChar) {
    case 'A':
        aCount = aCount + 1;
        break;
    case 'B':
        bCount = bCount + 1;
        break;
    case 'C':
        cCount = cCount + 1;
        break;
    default:
        System.out.println("Error in Identification Character.");
}
```

首先，评估表达式。在这个示例中，表达式是一个简单的`char`。在这个示例中，表达式是一个简单的`char`。在这个示例中，表达式是一个简单的`char`。因此，如果`idChar`包含`'A'`，`aCount`加 1。如果`idChar`包含`'B'`，跳过`'A'`并`bCount`加 1。同样，如果`idChar`包含`'C'`，则处理`cCount`加 1。

如果没有匹配匹配表达式，将执行`default`情况。

遇到`break`语句时，处理跳转到`switch`语句之后的语句。`break`语句通常用于跳出每个`case`。如果没有`break`语句，处理将继续进入下一个`case`。

核心概念：`switch`语句匹配字符或整数值到多个`case`之一。

你可能记得`break`语句在第 S 章中简要提到过，因为它可以用于其他循环和条件语句。我们当时警告过这种处理通常是不必要的，并且被许多开发者认为是不习惯。`switch`语句是这一准则的例外。使用`break`语句是确保只执行一个`case`代码的唯一方法。

> 核心概念`break`语句通常位于`switch`语句每个`case`的结尾。

## switch语句

![](img/7f8e069c1898b741edc17dfeed34b0c1_298_0.png)

`switch`语句评估初始表达式并将其与多个`case`之一匹配。在相应的`case`中继续处理。如果没有其他`case`匹配，将执行选项`default`情况。

示例：

```
switch (numValues)
  case 0:
    System.out.println("No values were entered.");
    break;
  case 1:
    System.out.println("One value was entered.");
    break;
  case 2:
    System.out.println("Two values were entered.");
    break;
  default:
    System.out.println("Too many values were entered.");
```

在`switch`语句开头评估的表达式类型必须是`char`、`byte`、`short`或`int`。特别地，它不能是`boolean`或浮点数或`String`。此外，每个`case`的值必须是常量；它不能是变量或其他表达式。这限制了`switch`语句适用的场景。但在适用时，它通常使代码更易于阅读和理解。

# 第 6 章 更多条件与循环

同样注意，`switch`语句的隐式布尔条件基于相等性。语句开头的表达式与每个`case`值进行比较，以确定它与哪一个相等。`switch`语句不能用于确定其他关系操作（例如小于），除非先进行初步处理。例如，列表 6.1 中的`GestureDetector`程序根据用户输入的数字分数打印注释。

```
LISTING 6.1
********************************************************************
// GradeReport.java           Author: Lewis/Loftus
// 演示 switch 语句的使用。
********************************************************************

import java.util.Scanner;
public class GradeReport {
    //----------------------------------------------------------------------
    // 从用户处读取分数并相应地打印注释。
    //----------------------------------------------------------------------
    public static void main(String[] args) {
        int grade, category;

        Scanner scan = new Scanner(System.in);
        System.out.print("Enter a numeric grade (0 to 100): ");
        grade = scan.nextInt();

        category = grade / 10;
        System.out.print("That grade is ");
        switch (category) {
            case 10:
                System.out.println("a perfect score. Well done.");
                break;
            case 9:
                System.out.println("well above average. Excellent.");
                break;
            case 8:
                System.out.println("above average. Nice job.");
                break;
```

```
LISTING 6.1 续
case 7:
System.out.println("average.");
break;
case 6:
System.out.println("below average. You should see the");
System.out.println("instructor to clarify the material " + "presented in class.");
break;
default:
System.out.println("not passing.");
}
}
```

OUTPUT

Enter a numeric grade (0 to 100): 86

That grade is above average. Nice job.

在`GradeReport`中，分数的类别是通过将分数除以 10（整数除法）得到的，产生一个 0 到 10 之间的整数值（假设输入了有效分数）。该结果被用作`switch`的表达式，为 60 分及以上的分数打印各种消息，对所有其他分数打印默认句子。

注意，任何`switch`语句都可以实现为一组嵌套的`if`语句。然而，嵌套的`if`语句会让读者很快变得难以理解，并且在实现和调试时容易出错。由于`switch`经常评估相等性，有时嵌套的`if`语句是必要的。这取决于具体情况。

## 自测习题（答案见附录 N）

- SR 6.1 当 Java 程序运行时，如果用于`switch`语句评估的表达式不与该语句关联的任何`case`值匹配，会发生什么？
- SR 6.2 如果`switch`语句中的`case`不以`break`语句结尾会发生什么？
- SR 6.3 如果用户输入“72”，`GradeReport`程序的输出是什么？如果用户输入“46”呢？如果用户输入“123”呢？

将以下嵌套的`if`语句转换为等价的`switch`语句。

## 6.2 条件运算符

Java 条件运算符在某些方面与`if-else`语句相似。它是一个三元运算符，因为它需要三个操作数。条件运算符的符号通常是`?;:`，但它与其他运算符的不同之处在于，组成它的两个符号总是被隔开的。以下是一个包含条件运算符的表达式示例：

```
(total > MAX) ? total + 1 : total * 2;
```

在`?`之前是一个布尔条件。`?`之后是两个由符号隔开的表达式。整个条件表达式在条件为真时返回第一个表达式的值，在条件为假时返回第二个表达式的值。

### 核心概念

条件运算符根据布尔条件将结果求值为两个可能值之一。

记住，这个示例是一个返回值的表达式。条件运算符本质上是一个运算符，而不是一个孤立的语句。通常我们就是对该值做些处理，例如将其赋值给变量：

```
total = (total > MAX) ? total + 1 : total * 2;
```

条件运算符与条件语句之间的区别可能是细微的。在许多方面，`?`运算符允许我们形成简洁的逻辑，作为简写的`if-else`语句。之前的语句在功能上与其等效，有时甚至优于以下内容：

```
if (total > MAX)
  total = total + 1;
else
  total = total * 2;
```

让我们再看几个例子。考虑以下声明：

```
int larger = (num1 > num2) ? num1 : num2;
```

如果`num1`大于`num2`，则返回`num1`的值并用于初始化变量`larger`。否则，返回`num2`的值并初始化`larger`。同样，以下语句打印两个值中较小的：

```
System.out.println("Smaller: " + ((num1 < num2) ? num1 : num2));
```

条件运算符偶尔有助于评估简短条件并返回结果。然而，它不是`if-else`语句的替代品，`?:`的操作数是表达式而不一定是语句。请谨慎使用。

## 自测习题（答案见附录 N）

- SR 6.5 条件运算符与条件语句之间的区别是什么？
- SR 6.6 写一个声明，如果布尔变量为真，则初始化字符为`'A'`，否则为`'B'`。
- SR 6.7 使用条件运算符表示以下逻辑。

## 6.3 do 语句

回顾第 5 章，`while`语句首先检查条件，如果为真则执行体。`do`语句与`while`语句相似，不同在于终止条件位于体尾。与`while`循环一样，`do`循环执行体直到条件变为假。条件写在循环末尾，表示在执行循环体之前不进行评估。注意，`do`循环的体始终至少执行一次。

```
if (val <= 10)
    System.out.println("The value is not greater than 10.")
else
    System.out.println("The value is greater than 10.")
```

以下代码使用`do`循环打印 1 到 5。将此代码与第 5 章中使用`while`循环完成任务的类似示例进行比较。

```
int count = 0;
do {
  count++;
  System.out.println(count);
} while (count < 5);
```

注意`do`循环简单地以关键字`do`开始。`do`循环的体持续到`while`子句包含决定是否再次执行体的布尔条件为止。有时很难判断以关键字`while`开头的代码行是`while`循环的开始还是`do`循环的结束。

> 核心概念

`do`循环至少执行一次循环体。

`do`循环只要布尔表达式为真，就会重复执行指定的语句。语句至少执行一次，然后评估表达式以决定是否再次执行该语句。

示例：

```java
{
  System.out.print("Enter a word:");
  word = scan.next();
  System.out.println(word);
} while (word.equals("quit"));
```

# 列表 6.2 **********************************************************************

```java
// ReverseNumber.java      Author: Lewis/Loftus
// 展示了 do 循环的用法。
// *****************************************************
import java.util.Scanner;

public class ReverseNumber {
  // 使用数学方法反转整数的数字。
  //----------------
  public static void main(String[] args) {
    int number, lastDigit, reverse = 0;

    Scanner scan = new Scanner(System.in);

    System.out.print("Enter a positive integer: ");
    number = scan.nextInt();

    do {
      lastDigit = number % 10;
      reverse = (reverse * 10) + lastDigit;
      number = number / 10;
    } while (number > 0);

    System.out.println("That number reversed is " + reverse);
  }
}
```

# 第 6 章 更多条件判断和循环

列表 6.2 继续输出

```
Enter a positive integer: 2896
That number reversed is 6982
```

`ReverseNumber`程序中的 do 循环使用取模运算来确定个位上的数字，将其加到反转数字中，并使用整数除法从原始数字中去掉该数字。当我们用完数字时，do 循环终止，这对应于变量`number`达到零值的点。通过几个示例仔细地跟踪程序的逻辑，看看它是如何工作的。
