

## 2.8 决策：相等运算符和关系运算符

| 标准代数相等或关系运算符 | Java 相等或关系运算符 | 示例 Java 条件 | Java 条件含义 |
|----------------------------------------------------|---------------------------------------|------------------------|-------------------------------------|
| = | == | x == y | x 等于 y |
| != | != | x != y | x 不等于 y |
| > | > | x > y | x 大于 y |
| < | < | x < y | x 小于 y |
| >= | >= | x >= y | x 大于或等于 y |
| <= | <= | x <= y | x 小于或等于 y |

图 2.14 | 相等运算符和关系运算符。

// Fig. 2.15: Comparison.java
// 使用 if 语句、关系运算符和相等运算符比较整数。
// import java.util.Scanner; // 程序使用类 Scanner

public class Comparison
{
// main 方法开始执行 Java 应用程序
public static void main( String[] args )
{
// 创建 Scanner 从命令行获取输入
Scanner input = new Scanner( System.in );

int number1; // 要比较的第一个数字
int number2; // 要比较的第二个数字

System.out.print( "Enter first integer: " ); // 提示
number1 = input.nextInt(); // 从用户读取第一个数字

System.out.print( "Enter second integer: " ); // 提示
number2 = input.nextInt(); // 从用户读取第二个数字

if ( number1 == number2 )
System.out.printf( "%d == %d\n", number1, number2 );

if ( number1 != number2 )
System.out.printf( "%d != %d\n", number1, number2 );

if ( number1 < number2 )
System.out.printf( "%d < %d\n", number1, number2 );

}

```
32      if ( number1 > number2 )
33          System.out.printf( "%d > %d\n", number1, number2 );
34
35      if ( number1 <= number2 )
36          System.out.printf( "%d <= %d\n", number1, number2 );
37
38      if ( number1 >= number2 )
39          System.out.printf( "%d >= %d\n", number1, number2 );
40  } // end method main
41  } // end class Comparison
```

```
Enter first integer: 777
Enter second integer: 777
777 == 777
777 <= 777
777 >= 777
```

```
Enter first integer: 1000
Enter second integer: 2000
1000 != 2000
1000 < 2000
1000 <= 2000
```

```
Enter first integer: 2000
Enter second integer: 1000
2000 != 1000
2000 > 1000
2000 >= 1000
```

图 2.15 | 使用 if 语句、关系运算符和相等运算符比较整数。 （第 2 部分，共 2 部分。）

类 Comparison 的声明从第 6 行开始

```
public class Comparison
```

该类的 main 方法（第 9–40 行）开始执行程序。第 12 行

```
Scanner input = new Scanner( System.in );
```

声明 Scanner 变量 input 并为其分配一个从标准输入（即键盘）输入数据的 Scanner。

第 14–15 行

```
int number1; // first number to compare
int number2; // second number to compare
```

声明用于存储从用户输入的值的 int 变量。

第 17–18 行

```
System.out.print( "Enter first integer: " ); // prompt
number1 = input.nextInt(); // read first number from user
```

分别提示用户输入第一个整数并输入该值。输入值存储在变量 number1 中。

第 20–21 行

```
System.out.print( "Enter second integer: " ); // prompt
number2 = input.nextInt(); // read second number from user
```

分别提示用户输入第二个整数并输入该值。输入值存储在变量 number2 中。

第 23–24 行

```
if ( number1 == number2 )
    System.out.printf( "%d == %d\n", number1, number2 );
```

比较 number1 和 number2 的值以确定它们是否相等。 if 语句始终以关键字 if 开始，后跟括号中的条件。 if 语句期望其主体中有一个语句，但如果它们被一对大括号 ({}) 括起来，则可以包含多个语句。此处显示的主体语句的缩进不是必需的，但它通过强调第 24 行的语句是第 23 行开始的 if 语句的一部分来提高程序的可读性。仅当存储在变量 number1 和 number2 中的数字相等（即条件为真）时，第 24 行才会执行。第 26–27、29–30、32–33、35–36 和 38–39 行中的 if 语句分别使用运算符 !=、<、>、<= 和 >= 比较 number1 和 number2。如果一个或多个 if 语句中的条件为真，则相应的主体语句执行。

## 常见编程错误 2.6

将相等运算符 == 与赋值运算符 = 混淆可能会导致逻辑错误或语法错误。相等运算符应读作“等于”，赋值运算符读作“得到”或“得到值”。为了避免混淆，有些人将相等运算符读作“双等号”或“等于等于”。

## 良好编程实践 2.11

在程序中每行放置一条语句可以增强程序的可读性。

每个 if 语句的第一行末尾没有分号（;）。这样的分号会在执行时导致逻辑错误。例如，

```
if ( number1 == number2 ); // logic error
    System.out.printf( "%d == %d\n", number1, number2 );
```

实际上会被 Java 解释为

```
if ( number1 == number2 )
    ; // empty statement
    System.out.printf( "%d == %d\n", number1, number2 );
```

其中单独一行上的分号——称为空语句——是在 if 语句中的条件为真时要执行的语句。当空语句执行时，不会执行任何任务。然后程序继续执行输出语句，无论条件为真还是为假，输出语句都会始终执行，因为输出语句不是 if 语句的一部分。

## 常见编程错误 2.7

在 if 语句的条件右括号后放置分号通常是逻辑错误。

注意图 2.15 中空白的使用。回想一下，编译器通常会忽略空白。因此，语句可以根据您的喜好拆分到多行并进行间隔，而不会影响程序的含义。拆分标识符和字符串是不正确的。理想情况下，语句应保持简短，但这并不总是可能的。

> **错误预防提示 2.9**
> 一个冗长的语句可以分布在几行上。如果必须将单个语句拆分到多行，请选择有意义的断点，例如逗号分隔列表中的逗号之后，或冗长表达式中的运算符之后。如果语句跨两行或多行，则缩进所有后续行直到语句结束。

图 2.16 按优先级递减的顺序显示了迄今为止讨论的运算符。除了赋值运算符 = 之外，所有运算符都从左到右关联。赋值运算符 = 从右到左关联，因此像 x = y = 0 这样的表达式被求值，就像它写成 x = (y = 0) 一样，这首先将值 0 分配给变量 y，然后将该赋值的結果 0 分配给 x。

> **良好编程实践 2.12**
> 在编写包含许多运算符的表达式时，请参考运算符优先级图表（附录 A）。确认表达式中的运算按您期望的顺序执行。如果在复杂表达式中不确定求值顺序，请使用括号强制顺序，就像在代数表达式中一样。

| 运算符 | 结合性 | 类型 |
|---|---|---|
| * / % | 从左到右 | 乘法 |
| + - | 从左到右 | 加法 |
| < <= > >= | 从左到右 | 关系 |
| == != | 从左到右 | 相等 |
| = | 从右到左 | 赋值 |

图 2.16 | 讨论的运算符的优先级和结合性。

## 2.9 总结

在本章中，您学习了 Java 的许多重要特性，包括在命令提示符上显示屏幕数据、从键盘输入数据、执行计算和做出决策。这里介绍的应用程序向您介绍了基本的编程概念。正如您将在第 3 章中看到的那样，Java 应用程序通常在 main 方法中只包含几行代码——这些语句通常创建执行应用程序工作的对象。在第 3 章中，您将学习如何实现自己的类并在应用程序中使用这些类的对象。

## 摘要

+   *第 2.2 节 Java 中的第一个程序：打印一行文本*
+   - Java 应用程序（p. 38）在您使用 java 命令启动 JVM 时执行。

