

获得各等级的学生人数：
A: 4
B: 1
C: 2
D: 1
F: 2

图5.10 | 创建GradeBook对象，输入成绩并显示成绩报告。(第2部分，共2部分。)

GradeBookTest类（图5.10）不会直接调用GradeBook的incrementLetterGradeCounter方法（图5.9的第69–95行）。该方法仅由GradeBook类的inputGrades方法使用，用于在用户输入每个新成绩时更新相应的字母等级计数器。方法incrementLetterGradeCounter的存在纯粹是为了支持GradeBook其他方法的操作，因此它被声明为private。

## 软件工程观察 5.2

> 回顾第3章，使用访问修饰符private声明的方法只能由声明这些private方法的类中的其他方法调用。这类方法通常被称为工具方法或辅助方法，因为它们通常用于支持类的其他方法的操作。

## switch语句的UML活动图

图5.11展示了通用switch语句的UML活动图。大多数switch语句在每个case中使用break，以便在处理完该case后终止switch语句。图5.11通过在活动图中包含break语句来强调这一点。

![](img/009e962758dcc71dbc43a493362e6dc0_207_0.png)

图5.11 | 带有break语句的switch多重选择语句UML活动图。

该图清楚地表明，case末尾的break语句会使控制立即退出switch语句。

对于switch的最后一个case（或可选的default case，当它位于最后时），break语句不是必需的，因为执行会继续到switch之后的下一语句。

## 软件工程观察 5.3

在switch语句中提供default case。包含default case会使你关注处理异常情况的需求。

## 良好编程实践 5.3

尽管switch中的每个case和default case可以按任意顺序出现，但请将default case放在最后。当default case列在最后时，该case的break不是必需的。

## 关于switch中每个case表达式的注意事项

使用switch语句时，请记住每个case必须包含一个常量整型表达式——即整数常量的任意组合，其计算结果为常量整数值（例如，−7、0或221）。整数常量就是整数值。此外，您还可以使用字符常量——单引号中的特定字符，如'A'、'7'或'$'——它们表示字符的整数值以及枚举常量（在第6.10节中介绍）。（附录B显示了ASCII字符集中字符的整数值，ASCII字符集是Java使用的Unicode字符集的子集。）

每个case中的表达式也可以是常量变量——一个包含在整个程序中都不改变的值的变量。这样的变量使用关键字final声明（在第6章中讨论）。Java有一个称为枚举的特性，我们也在第6章中介绍。枚举常量也可以用在case标签中。在第10章“面向对象编程：多态”中，我们介绍了一种更优雅的实现switch逻辑的方法——我们使用一种称为多态的技术来创建程序，这些程序通常比使用switch逻辑的程序更清晰、更易于维护、更易于扩展。

## 在switch语句中使用String（Java SE 7中的新特性）

从Java SE 7开始，您可以在switch语句的控制表达式和case标签中使用String。例如，您可能想使用城市名称来获取相应的邮政编码。假设city和zipCode是String变量，以下switch语句对三个城市执行此任务：

```
switch( city )
{
    case "Maynard":
        zipCode = "01754";
        break;
    case "Marlborough":
        zipCode = "01752";
        break;
    case "Framingham":
        zipCode = "01701";
        break;
} // end switch
```

## 5.7 break和continue语句

除了选择语句和重复语句之外，Java还提供了break和continue语句（本节和附录O中介绍）来改变控制流。上一节展示了如何使用break终止switch语句的执行。本节讨论如何在重复语句中使用break。

## break语句

break语句在while、for、do...while或switch中执行时，会导致立即退出该语句。执行继续到控制语句之后的第一条语句。break语句的常见用途是从循环中提前退出或跳过switch的其余部分（如图5.9所示）。图5.12演示了break语句退出for语句。

```
1 // Fig. 5.12: BreakTest.java
2 // break statement exiting a for statement.
3 public class BreakTest
4 {
5 public static void main( String[] args )
6 {
7 int count; // control variable also used after loop terminates
8
9 for ( count = 1; count <= 10; count++ ) // loop 10 times
10 {
11 if ( count == 5 ) // if count is 5,
12 break; // terminate loop
13
14 System.out.printf( "%d ", count );
15 } // end for
16
17 System.out.printf( "\nBroke out of loop at count = %d\n", count );
18 } // end main
19 } // end class BreakTest
```

1 2 3 4
Broke out of loop at count = 5

图5.12 | break语句退出for语句。

当for语句（第9–15行）中嵌套的if语句（第11–12行）检测到count为5时，第12行的break语句执行。这会终止for语句，程序继续执行第17行（紧接在for语句之后），该行显示一条消息，指示循环终止时控制变量的值。循环只完整执行了四次循环体，而不是十次。

## continue语句

continue语句在while、for或do...while中执行时，会跳过循环体中剩余的语句，并继续进行循环的下一次迭代。在while和do...while语句中，程序在continue语句执行后立即计算循环继续测试。在for语句中，先执行递增表达式，然后程序计算循环继续测试。

```
// Fig. 5.13: ContinueTest.java
// continue statement terminating an iteration of a for statement.
public class ContinueTest
{
    public static void main( String[] args )
    {
        for ( int count = 1; count <= 10; count++ ) // loop 10 times
        {
            if ( count == 5 ) // if count is 5,
                continue; // skip remaining code in loop

            System.out.printf( "%d ", count );
        } // end for

        System.out.println( "\nUsed continue to skip printing 5" );
    } // end main
} // end class ContinueTest
```

1 2 3 4 6 7 8 9 10
Used continue to skip printing 5

图5.13 | continue语句终止for语句的一次迭代。

图5.13使用continue在嵌套的if（第9行）确定count的值为5时跳过第12行的语句。当continue语句执行时，程序控制继续到for语句中控制变量的递增（第7行）。

在第5.3节中，我们指出在大多数情况下可以使用while代替for。但当while中的递增表达式在continue语句之后时，这就不成立了。在这种情况下，递增不会在程序计算重复继续条件之前执行，因此while不会像for那样执行。

## 软件工程观察 5.4

一些程序员认为break和continue违反了结构化编程。由于使用结构化编程技术可以达到相同的效果，这些程序员不使用break或continue。

## 软件工程观察 5.5

在实现高质量软件工程和实现最佳性能软件之间存在一种张力。有时这些目标中的一个是以牺牲另一个为代价来实现的。除了大多数性能密集型情况外，请应用以下经验法则：首先，使您的代码简单且正确；然后，使其快速且小巧，但仅在必要时这样做。

## 5.8 逻辑运算符

if、if...else、while、do...while和for语句都需要一个条件来确定如何继续程序的流程控制。到目前为止，我们只学习了简单的条件，例如count <= 10、number != sentinelValue和total > 1000。简单条件用关系运算符>、<、>=和<=以及相等运算符==和!=表示，每个表达式只测试一个条件。为了在做出决策的过程中测试多个条件，我们在单独的语句中执行这些测试

