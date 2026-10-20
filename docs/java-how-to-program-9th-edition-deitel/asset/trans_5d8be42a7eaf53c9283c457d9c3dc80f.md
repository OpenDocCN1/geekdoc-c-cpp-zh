

![](img/009e962758dcc71dbc43a493362e6dc0_237_0.png)

图 6.1 | 层级式的“老板方法/工人方法”关系。

## 6.3 static 方法、static 字段与 Math 类

尽管大多数方法是通过对特定对象的方法调用来执行的，但情况并非总是如此。有时某个方法执行的任务不依赖于任何对象的内容。这样的方法适用于其声明的整个类，称为静态方法或类方法。类中通常包含便捷的静态方法来执行常见任务。例如，回顾我们在图 5.6 中曾使用 Math 类的静态方法 pow 来计算一个值的幂。要将方法声明为 static，只需在方法声明的返回类型前放置关键字 static。对于程序中导入的任何类，你可以通过指定声明该方法的类名，后跟一个点（.）和方法名来调用该类的静态方法，如下所示：

```
ClassName.methodName( arguments )
```

我们在此使用各种 Math 类方法来介绍静态方法的概念。Math 类提供了一系列方法，使你能够执行常见的数学计算。例如，你可以通过静态方法调用 `Math.sqrt( 900.0 )` 计算 900.0 的平方根。

上述表达式求值为 30.0。sqrt 方法接受一个 double 类型的参数，并返回一个 double 类型的结果。要在命令窗口中输出上述方法调用的值，你可以编写如下语句：

```
System.out.println( Math.sqrt( 900.0 ) );
```

在此语句中，sqrt 返回的值成为 println 方法的参数。在调用 sqrt 方法之前无需创建 Math 对象。此外，Math 类的所有方法都是 static 的——因此，每个方法都是通过在方法名前加上类名 Math 和点（.）分隔符来调用的。

> 软件工程观察 6.4
> Math 类是 java.lang 包的一部分，该包由编译器隐式导入，因此使用 Math 类的方法时无需显式导入 Math 类。

方法参数可以是常量、变量或表达式。如果 c = 13.0, d = 3.0, f = 4.0，则语句

```
System.out.println( Math.sqrt( c + d * f ) );
```

计算并打印 13.0 + 3.0 * 4.0 = 25.0 的平方根，即 5.0。图 6.2 总结了若干 Math 类方法。在图中，x 和 y 均为 double 类型。

| 方法 | 描述 | 示例 |
|---|---|---|
| abs(x) | x 的绝对值 | abs(23.7) 为 23.7<br>abs(0.0) 为 0.0<br>abs(-23.7) 为 23.7 |
| ceil(x) | 将 x 舍入为不小于 x 的最小整数 | ceil(9.2) 为 10.0<br>ceil(-9.8) 为 -9.0 |
| cos(x) | x 的三角余弦（x 以弧度为单位） | cos(0.0) 为 1.0 |
| exp(x) | 指数方法 e^x | exp(1.0) 为 2.71828<br>exp(2.0) 为 7.38906 |
| floor(x) | 将 x 舍入为不大于 x 的最大整数 | floor(9.2) 为 9.0<br>floor(-9.8) 为 -10.0 |
| log(x) | x 的自然对数（以 e 为底） | log(Math.E) 为 1.0<br>log(Math.E * Math.E) 为 2.0 |
| max(x, y) | x 和 y 中的较大值 | max(2.3, 12.7) 为 12.7<br>max(-2.3, -12.7) 为 -2.3 |
| min(x, y) | x 和 y 中的较小值 | min(2.3, 12.7) 为 2.3<br>min(-2.3, -12.7) 为 -12.7 |
| pow(x, y) | x 的 y 次幂（即 x^y） | pow(2.0, 7.0) 为 128.0<br>pow(9.0, 0.5) 为 3.0 |
| sin(x) | x 的三角正弦（x 以弧度为单位） | sin(0.0) 为 0.0 |
| sqrt(x) | x 的平方根 | sqrt(900.0) 为 30.0 |
| tan(x) | x 的三角正切（x 以弧度为单位） | tan(0.0) 为 0.0 |

图 6.2 | Math 类方法。

## Math 类常量 PI 和 E

Math 类声明了两个表示常用数学常量的字段——Math.PI 和 Math.E。Math.PI（3.141592653589793）是圆的周长与其直径的比值。Math.E（2.718281828459045）是自然对数的底数（通过静态 Math 方法 log 计算）。这些字段在 Math 类中使用修饰符 public、final 和 static 声明。将它们声明为 public 允许你在自己的类中使用这些字段。任何用关键字 final 声明的字段都是常量——其值在字段初始化后不能更改。PI 和 E 被声明为 final，因为它们的值从不改变。将这些字段声明为 static 使它们可以通过类名 Math 和点（.）分隔符访问，就像 Math 类的方法一样。回顾第 3.4 节，当类的每个对象维护其自身的一份属性副本时，表示该属性的字段也称为实例变量——类的每个对象（实例）在内存中都有该变量的独立实例。有些字段对于类的每个对象并没有单独的实例。static 字段就是这种情况，它们也被称为类变量。当创建包含 static 字段的类的对象时，该类的所有对象共享该类 static 字段的一份副本。类变量（即 static 变量）和实例变量共同构成了类的字段。你将在第 8.11 节了解更多关于 static 字段的内容。

## 为什么 main 方法要声明为 static？

当你使用 java 命令执行 Java 虚拟机（JVM）时，JVM 会尝试调用你指定类的 main 方法——此时尚未创建该类的任何对象。将 main 声明为 static 允许 JVM 在不创建类实例的情况下调用 main。当你执行应用程序时，你需要将类名作为参数传递给 java 命令，如下所示：

```
java ClassName argument1 argument2 ...
```

JVM 加载由 ClassName 指定的类，并使用该类名来调用 main 方法。在上述命令中，ClassName 是传递给 JVM 的一个命令行参数，用于告诉它执行哪个类。在 ClassName 之后，你还可以指定一个字符串列表（以空格分隔）作为命令行参数，JVM 会将这些参数传递给应用程序。这些参数可能用于指定运行应用程序的选项（例如文件名）。正如你将在第 7 章“数组与 ArrayList”中学到的，你的应用程序可以访问这些命令行参数并使用它们来定制应用程序。

## 6.4 声明具有多个参数的方法

方法通常需要多条信息来执行其任务。我们现在来考虑如何编写具有多个参数的自定义方法。

图 6.3 使用名为 maximum 的方法来确定并返回三个 double 值中的最大值。在 main 中，第 14–18 行提示用户输入三个 double 值，然后从用户处读取这些值。第 21 行调用方法 maximum（在第 28–41 行声明）来确定作为参数接收的三个值中的最大值。当 maximum 方法将结果返回给第 21 行时，程序将 maximum 的返回值赋给局部变量 result。然后第 24 行输出最大值。在本节末尾，我们将讨论第 24 行中运算符 + 的使用。

```
1 // Fig. 6.3: MaximumFinder.java
2 // Programmer-declared method maximum with three double parameters.
3 import java.util.Scanner;
4 
5 public class MaximumFinder
6 {
7    // obtain three floating-point values and locate the maximum value
8    public static void main( String[] args )
9    {
10    // create Scanner for input from command window
11    Scanner input = new Scanner( System.in );
12    
13    // prompt for and input three floating-point values
14    System.out.print(
15        "Enter three floating-point values separated by spaces: " );
16      double number1 = input.nextDouble(); // read first double
17      double number2 = input.nextDouble(); // read second double
18      double number3 = input.nextDouble(); // read third double
19
20      // determine the maximum value
21      double result = maximum( number1, number2, number3 );
22
23      // display maximum value
24      System.out.println( "Maximum is: " + result );
25  } // end main
26
27  // returns the maximum of its three double parameters
28  public static double maximum( double x, double y, double z )
29  {
30      double maximumValue = x; // assume x is the largest to start
31
32      // determine whether y is greater than maximumValue
33      if ( y > maximumValue )
34          maximumValue = y;
35
36      // determine whether z is greater than maximumValue
37      if ( z > maximumValue )
38          maximumValue = z;
39
40      return maximumValue;
41  } // end method maximum
42  } // end class MaximumFinder
```

```
Enter three floating-point values separated by spaces: 9.35 2.74 5.1
Maximum is: 9.35
```

```
Enter three floating-point values separated by spaces: 5.8 12.45 8.32
Maximum is: 12.45
```

```
Enter three floating-point values separated by spaces: 6.46 4.12 10.54
Maximum is: 10.54
```

图 6.3 | 程序员声明的具有三个 double 参数的方法 maximum。（第 2 部分，共 2 部分。）

## public 和 static 关键字

方法 maximum 的声明以关键字 public 开头，表示该方法是“对公众可用的”——它可以被其他类的方法调用。关键字 static 使 main 方法（另一个静态方法）能够如第 21 行所示那样调用 maximum，而无需用类名 MaximumFinder 限定方法名——同一类中的静态方法可以直接相互调用。任何其他使用 maximum 的类都必须用类名完全限定方法名。

## 方法 maximum

考虑 maximum 的声明（第 28–41 行）。第 28 行表明它返回一个 double 值，方法名为 maximum，并且该方法需要三个 double 参数。

