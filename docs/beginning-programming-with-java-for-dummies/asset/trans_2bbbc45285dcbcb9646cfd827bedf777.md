
我在图11-3中展示了这段代码的两次运行结果。第一次运行时，randomNumber为7。程序执行了case 7到case 10，以及default分支。第二次运行时，randomNumber为3。程序执行了case 3和case 4。然后，由于case 4中有break语句，程序跳出switch并显示Goodbye。

## 图11-3：请下定决心。

```
Type your question, my child: Do good things happen to good people?
Yes, but only if you're nice to me.
Yes (as if I care).
No, not until Cromwell seizes Dover.
No, not until Nell squeezes Rover.
You think you have problems? My random number generator is broken!
Goodbye
Type your question, my child: Is your switch statement missing some breaks?
Yessir, yessir! Three bags full.
What part of 'no' don't you understand?
Goodbye
```

![](img/f938eba5f15e231d828a6255e7ec5523_242_0.png)

清单11-2中的switch语句缺少一些break语句。即使没有这些break语句，代码也能无错误地编译。但是，当你运行清单11-2中的代码时，不会得到你想要的结果。

## 善用穿透

通常，在使用switch语句时，你并不希望发生穿透，因此会在switch中到处添加break语句。但有时候，穿透恰恰是你所需要的。

以一个月有多少天为例。这里面有简单的规则吗？包含字母"r"的月份有31天？“i”在“e”之前（除了在“c”之后）的月份有30天？

你可以随心所欲地调整if条件。但为了处理所有可能性，我更喜欢用switch语句。清单11-3演示了这一想法。

## 清单11-3：计算一个月有多少天

```
import java.util.Scanner;

class DaysInEachMonth {

    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        int month, numberOfDays = 0;
        boolean isLeapYear;
```

## 清单11-3（续）

```
System.out.print("Which month? ");
month = keyboard.nextInt();

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
    isLeapYear = keyboard.nextBoolean();
    if (isLeapYear) {
        numberOfDays = 29;
    } else {
        numberOfDays = 28;
    }
}

System.out.print(numberOfDays);
System.out.println(" days");

keyboard.close();
}
```

图11-4展示了清单11-3中程序的几次运行结果。对于月份6，计算机跳转到case 6。case 6子句中没有语句，所以程序运行的那一部分相当无聊。

## 图11-4
距离下一个重要截止日期还有多少天？

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

但由于case 6子句中没有break，计算机会直接走到case 9。同样，计算机发现没有语句也没有break，于是继续尝试下一个case，即case 11。到这时，计算机找到了有价值的内容。计算机将30赋给numberOfDays，并跳出整个switch语句（见图11-5）。

二月是所有月份中最棒的。首先，清单11-3中的二月case包含对Scanner类的nextBoolean方法的调用。该方法期望我输入true或false。代码用我输入的内容为布尔变量赋值。（在清单11-3中，我为isLeapYear变量赋值为true或false。）

## 图11-5
跟着弹跳球走。

![](img/f938eba5f15e231d828a6255e7ec5523_244_0.png)

二月还包含自己的if语句。在第10章中，我在其他if语句中嵌套if语句。但在二月的case中，我在switch语句中嵌套if语句。这很酷。

## 使用条件运算符

Java有一个精巧的特性，让我忍不住要写一写。使用这个特性，你可以以非常自然的方式思考各种选择。

那么我说“自然的方式”是什么意思呢？如果我一边模仿清单11-3末尾的if语句，一边大声思考，我会得出这样的结论：

```
//The thinking in Listing 11-3:
What should I do next?
If this is a leap year,
    I'll make the numberOfDays be 29;
Otherwise,
    I'll make the numberOfDays be 28.
```

我漫无目的地走进一个if语句，对自己接下来要做什么毫无头绪。这看起来很傻。现在是二月，每个人都知道二月要做什么。你要做的是问这个月有多少天。

在我看来，清单11-3中的代码并没有反映出思考二月问题的最自然方式。所以这里有一个更自然的方式：

```
//A more natural way to think about the problem:
The value of numberOfDays is...
Wait! Is this a leap year?
If yes, 29
If no, 28
```

在这种更自然的思考方式中，我一开始就知道我要选择一个天数。因此，当我走到岔路口时（这是闰年吗？），剩下的唯一任务就是在29和28之间做出选择。

我可以巧妙地做出选择：

```
case 2:
System.out.print("Leap year (true/false)? ");
isLeapYear = keyboard.nextBoolean();
numberOfDays = isLeapYear ? 29 : 28;
```

? : 组合被称为条件运算符。在图11-6中，我展示了我是如何将对二月的自然思考转变成条件运算符格式的。

## 图11-6：
从你的思维到计算机代码。

![](img/f938eba5f15e231d828a6255e7ec5523_246_0.png)

从整体上看，isLeapYear ? 29 : 28是一个带有值的表达式。那么这个表达式有什么值呢？isLeapYear ? 29 : 28的值要么是29，要么是28。这取决于isLeapYear是否为true。这就是条件运算符的工作方式：

- 如果问号前面的内容为true，整个表达式的值就是问号和冒号之间的内容。
- 如果问号前面的内容为false，整个表达式的值就是冒号后面的内容。

图11-7以一种有趣的方式帮你直观理解这些概念。

## 图11-7：
你见过表达式自言自语吗？

![](img/f938eba5f15e231d828a6255e7ec5523_246_1.png)

因此，条件运算符的整体效果就好像计算机在执行

```
numberOfDays = 29;
```

或

```
numberOfDays = 28;
```

不管怎样，numberOfDays都会得到一个值，而代码以一种优雅的方式解决了问题。

## 第12章

## 循环往复

## 本章内容

- 创建程序循环
- 使用循环制定问题解决方案
- 诊断循环问题

第8章中有代码用于反转用户输入的四字母单词。如果你还没有读过第8章，或者只是不想翻回去看，这里快速回顾一下代码：

```
c1 = keyboard.findWithinHorizon(".", 0).charAt(0);
c2 = keyboard.findWithinHorizon(".", 0).charAt(0);
c3 = keyboard.findWithinHorizon(".", 0).charAt(0);
c4 = keyboard.findWithinHorizon(".", 0).charAt(0);

System.out.print(c4);
System.out.print(c3);
System.out.print(c2);
System.out.print(c1);
```

这段代码对于恰好四个字母的单词来说非常合适，但如何反转一个五个字母的单词呢？就现有代码而言，你必须添加两条新语句：

```
c1 = keyboard.findWithinHorizon(".", 0).charAt(0);
c2 = keyboard.findWithinHorizon(".", 0).charAt(0);
c3 = keyboard.findWithinHorizon(".", 0).charAt(0);
c4 = keyboard.findWithinHorizon(".", 0).charAt(0);
c5 = keyboard.findWithinHorizon(".", 0).charAt(0);

System.out.print(c5);
System.out.print(c4);
System.out.print(c3);
System.out.print(c2);
System.out.print(c1);
```

真是麻烦！每当单词长度变化时，你都要向程序添加语句！输入变短时还要删除语句？这肯定不是解决问题的最佳方式。也许你可以命令计算机自动添加语句。（但话又说回来，也许你做不到。）
