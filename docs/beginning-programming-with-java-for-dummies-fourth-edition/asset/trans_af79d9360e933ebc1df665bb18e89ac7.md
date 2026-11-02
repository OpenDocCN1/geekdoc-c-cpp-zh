

## 图11-4：距离下一个重大截止日期还有多少天？

```
Which month? 1
31 days

Which month? 6
30 days

Which month? 2
Leap year (true/false)? false
28 days

Which month? 2
Leap year (true/false)? true
29 days
```

但在 `case 6` 子句中没有 `break`，计算机会直接继续执行到 `case 9`。同样，计算机没有找到任何语句，也没有 `break`，于是计算机又继续前进到下一个 `case`，即 `case 11`。这时，计算机终于找到了它想要的东西。计算机将 30 赋给 `numberOfDays`，然后跳出整个 `switch` 语句（见图11-5）。

二月是所有月份中最好的。首先，清单11-3中的二月 `case` 包含对 `Scanner` 类 `nextBoolean` 方法的调用。该方法要求我输入 `true` 或 `false`。代码使用我输入的内容为一个布尔变量赋值。（在清单11-3中，我将 `true` 或 `false` 赋给 `isLeapYear` 变量。）

### 图11-5：跟着弹跳的球走。

```
switch (month) {
case 1:
case 3:
case 5:
case 7:
case 8:
case 10:
case 12:
    numberOfDays = 31;
    break;
case 4:
case 6:
case 9:
case 11:
    numberOfDays = 30;
    break;
case 2:
    System.out.print("Leap year (true/false)? ");
    isLeapYear = myScanner.nextBoolean();
    if (isLeapYear)
        numberOfDays = 29;
    else
        numberOfDays = 28;
}
System.out.print(numberOfDays);
System.out.println(" days");
```

二月还包含它自己的 `if` 语句。在第10章中，我在其他 `if` 语句中嵌套 `if` 语句。但在二月，我在 `switch` 语句中嵌套了一个 `if` 语句。这很酷。

### 使用条件运算符

Java 有一个我忍不住要写一写的好特性。使用这个特性，你可以用一种非常自然的方式来思考各种选择。

“自然的方式”是什么意思？如果我一边模仿清单11-3末尾的 `if` 语句一边大声思考，我会得出这样的结论：

```
//清单11-3中的思考过程：
我接下来该怎么办？
如果是闰年，
    我就把numberOfDays设为29；
否则，
    我就把numberOfDays设为28。
```

我稀里糊涂地进入了一个 `if` 语句，却完全不知道下一步该做什么。这看起来很傻。现在是二月，每个人都知道二月该做什么。你要问这个月有多少天。

在我看来，清单11-3中的代码并没有反映出思考二月问题的最自然方式。所以这里有一个更自然的方式：

```
//一种更自然的思考问题的方式：
numberOfDays的值是……
等等！这是闰年吗？
    如果是，29
    如果不是，28
```

在第二种更自然的思考方式中，我从一开始就知道我要选择一个天数。所以当我走到岔路口时（这是闰年吗？），剩下的任务只是在29和28之间做出选择。

我可以优雅地做出选择：

```
case 2:
System.out.print("Leap year (true/false)? ");
isLeapYear = keyboard.nextBoolean();
numberOfDays = isLeapYear ? 29 : 28;
```

`? :` 组合被称为条件运算符。在图11-6中，我向你展示了我对二月的自然思考如何演变成条件运算符的格式。

### 图11-6：从你的思维到计算机的代码。

![](img/6d9dcff12e52b997f3ad31445b712549_246_0.png)

整体来看，`isLeapYear ? 29 : 28` 是一个带有值的表达式。那么这个表达式有什么值呢？嗯，`isLeapYear ? 29 : 28` 的值要么是29，要么是28。这取决于 `isLeapYear` 是否为真。这就是条件运算符的工作方式：

-   如果问号前面的内容为真，整个表达式的值就是问号和冒号之间的内容。
-   如果问号前面的内容为假，整个表达式的值就是冒号后面的内容。

### 图11-7：你见过表达式自言自语吗？

![](img/6d9dcff12e52b997f3ad31445b712549_246_1.png)

所以条件运算符的整体效果就像是计算机在执行

```
numberOfDays = 29;
```

或者

```
numberOfDays = 28;
```

无论如何，`numberOfDays` 都会得到一个值，并且代码优雅地解决了问题。

## 第12章：转了一圈又一圈

### 本章内容

-   创建程序循环
-   用循环解决问题
-   诊断循环问题

第8章中的代码可以反转用户输入的四个字母单词中的字母。如果你没有读过第8章，或者只是不想翻回去看，这里快速回顾一下代码：

```
c1 = keyboard.findWithinHorizon("",0).charAt(0);
c2 = keyboard.findWithinHorizon("",0).charAt(0);
c3 = keyboard.findWithinHorizon("",0).charAt(0);
c4 = keyboard.findWithinHorizon("",0).charAt(0);

System.out.print(c4);
System.out.print(c3);
System.out.print(c2);
System.out.print(c1);
```

这段代码对于恰好有四个字母的单词来说非常好用，但是如何反转一个五个字母的单词呢？按照目前代码的写法，你必须添加两个新语句：

```
c1 = keyboard.findWithinHorizon("",0).charAt(0);
c2 = keyboard.findWithinHorizon("",0).charAt(0);
c3 = keyboard.findWithinHorizon("",0).charAt(0);
c4 = keyboard.findWithinHorizon("",0).charAt(0);
c5 = keyboard.findWithinHorizon("",0).charAt(0);

System.out.print(c5);
System.out.print(c4);
System.out.print(c3);
System.out.print(c2);
System.out.print(c1);
```

真麻烦！每当单词长度变化时，你就要在程序中添加语句！当输入变短时，你就要删除语句！这不可能是解决问题的最佳方式。也许你可以命令计算机自动添加语句。（但话又说回来，也许你不能。）

幸运的是，你可以做一些更好的事情。你可以编写一次语句，然后告诉计算机多次执行该语句。多少次？你可以告诉计算机根据需要的次数来执行一条语句。

这就是核心思想。本章其余部分将详细介绍。

### 一遍又一遍地重复指令（Java while 语句）

这里有一个简单的骰子游戏：不断掷两个骰子，直到掷出 7 或 11 为止。清单12-1有一个模拟该游戏动作的程序，图12-1显示了该程序的两次运行。

### 图12-1：妈妈需要一双新鞋。

![](img/6d9dcff12e52b997f3ad31445b712549_249_0.png)

### 清单12-1：掷出7或11

```java
import java.util.Random;
import static java.lang.System.out;

class SimpleDiceGame {
    public static void main(String args[]) {
        Random myRandom = new Random();
        int die1 = 0, die2 = 0;
        while (die1 + die2 != 7 && die1 + die2 != 11) {
            die1 = myRandom.nextInt(6) + 1;
            die2 = myRandom.nextInt(6) + 1;
            out.print(die1);
            out.print(" ");
            out.println(die2);
        }

        out.print("Rolled ");
        out.println(die1 + die2);
    }
}
```

清单12-1的核心是一种叫做 *while 语句*（也称为 *while 循环*）的东西。*while* 语句具有以下形式：

```
while (Condition) {
    Statements
}
```

用英语重新表述，清单12-1中的 *while* 语句会这样说：

```
while 两个骰子的和不是7并且不是11
持续执行花括号里的所有内容：{
}
```

花括号里的内容（一遍又一遍重复的内容）是获取两个新的随机数并显示这些随机数值的代码。只要 `die1 + die2 != 7 && die1 + die2 != 11` 保持为真，花括号中的语句就会重复执行。

循环中每次重复执行的语句被称为循环的一次*迭代*。在图12-1中，第一次运行有2次迭代，第二次运行有12次迭代。

当 `die1 + die2 != 7 && die1 + die2 != 11` 不再为真时（也就是说，当和为7或11时），语句的重复就会立即停止。计算机继续执行循环之后的语句。

### 跟踪循环中的执行过程

为了追踪清单12-1中代码的执行过程，我借用图12-1中第一次运行的数字：

-   ✓ 开始时，`die1` 和 `die2` 的值都是 0。
-   ✓ 计算机到达 `while` 语句的顶部，检查 `die1 + die2 != 7 && die1 + die2 != 11` 是否为真（见图12-2）。
-   ✓ 条件为真，因此计算机在图12-3中走真路径。

