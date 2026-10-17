
```
total += 5;
```

这与以下语句执行相同的操作：

```
total = total + 5;
```

赋值运算符的右侧可以是一个完整的表达式。运算符右侧的表达式会被求值，然后该结果会加到左侧变量的当前值上，并将该值存储在变量中。因此，以下语句：

```
total += (sum - 12) / count;
```

等价于：

```
total = total + ((sum - 12) / count);
```

Java 中定义了许多类似的赋值运算符，包括执行减法 (`-=`)、乘法 (`*=`)、除法 (`/=`) 和余数 (`%=`) 的运算符。完整的 Java 运算符集合在附录 D 中讨论。

所有赋值运算符都会先求值右侧的整个表达式，然后将结果用作另一个操作的右操作数。因此，以下语句：

```
result *= count1 + count2;
```

等价于：

```
result = result * (count1 + count2);
```

同样，以下语句：

```
result %= (highest - 40) / 2;
```

等价于：

```
result = result % ((highest - 40) / 2);
```

一些赋值运算符根据操作数的类型执行特定功能，就像它们对应的常规运算符一样。例如，如果 `+=` 运算符的操作数是字符串，则赋值运算符执行字符串连接。

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

- SR 2.21 What is the result of `19%5` when evaluated in a Java expression? Explain.

- SR 2.22 What is the result of `13/4` when evaluated in a Java expression? Explain.

- SR 2.23 If an integer variable `diameter` currently holds the value 5, what is its value after the following statement is executed? Explain.

  `diameter = diameter * 4;`

- SR 2.24 What is operator precedence?

- SR 2.25 What is the value of each of the following expressions?

  - a. `15 + 7 * 3`
  - b. `(15 + 7) * 3`
  - c. `3 * 6 + 10 / 5 + 5`
  - d. `27 % 5 + 7 % 3`
  - e. `100 / 2 / 2 / 2`
  - f. `100 / ( 2 / 2 ) / 2`

- SR 2.26 For each of the following expressions state whether they are valid or invalid. If invalid, explain why.

  - a. `result = ( 5 + 2 );`
  - b. `result = ( 5 + 2 * ( 15 - 3 );`
  - c. `result = ( 5 + 2 (;`
  - d. `result = ( 5 + 2 ( 4 ) );`

SR 2.27 执行以下语句序列后，整数变量 `result` 中包含什么值？

```
result = 27;
result = result + 3;
result = result / 7;
result = result * 2;
```

SR 2.28 执行以下语句序列后，整数变量 `result` 中包含什么值？

```
int base;
int result;
base = 5;
result = base + 3;
base = 7;
```

SR 2.29 什么是赋值运算符？

SR 2.30 如果整数变量 `weight` 当前持有值 100，执行以下语句后其值是多少？解释。

```
weight -= 17;
```

## 2.5 数据转换

由于 Java 是一种强类型语言，每个数据值都与特定类型相关联。有时将一种类型的数据值转换为另一种类型是有帮助或必要的，但在转换过程中我们必须小心不要丢失重要信息。例如，假设一个保存数字 1000 的 `short` 变量被转换为 `byte` 值。因为 `byte` 没有足够的位来表示值 1000，转换过程中会丢失一些位，`byte` 中表示的数字将不再保持其原始值。

从一种原始类型到另一种原始类型的转换分为两类：扩展转换和缩小转换。扩展转换更安全，因为它们通常不会丢失信息。它们被称为扩展转换，因为它们从一种数据类型转换到另一种使用相等或更大空间来存储值的类型。图 2.5 列出了 Java 的扩展转换。

例如，将 `byte` 转换为 `short` 是安全的，因为 `byte` 存储在 8 位中，而 `short` 存储在 16 位中。不会丢失信息。所有从一种整数类型到另一种整数类型的扩展转换，或从一种浮点类型到另一种浮点类型的扩展转换，都能精确地保留数值。

| From | To |
|---|---|
| `byte` | `short`, `int`, `long`, `float`, or `double` |
| `short` | `int`, `long`, `float`, or `double` |
| `char` | `int`, `long`, `float`, or `double` |
| `int` | `long`, `float`, or `double` |
| `long` | `float` or `double` |
| `float` | `double` |

### FIGURE 2.5 Java widening conversions

> KEY CONCEPT
>
> 应避免缩小转换，因为它们可能丢失信息。

尽管扩展转换不会丢失关于值大小的任何信息，但导致浮点值的扩展转换可能会丢失精度。在将 `int` 或 `long` 转换为 `float`，或将 `long` 转换为 `double` 时，最不显著的数字可能会丢失。在这种情况下，结果的浮点值将是整数值的舍入版本，遵循 IEEE 754 浮点标准中定义的舍入技术。

缩小转换比扩展转换更可能丢失信息。它们通常从一种类型转换到一种用于存储值所需空间更少的类型，因此某些信息可能会受损。缩小转换可能同时丢失数值大小和精度。因此，通常应避免它们。图 2.6 列出了 Java 的缩小转换。

缩小转换中空间缩小情况的一个例外是当我们将 `byte`（8 位）或 `short`（16 位）转换为 `char`（16 位）时。这些仍然

| From | To |
|---|---|
| `byte` | `char` |
| `short` | `byte` or `char` |
| `char` | `byte` or `short` |
| `int` | `byte`, `short`, or `char` |
| `long` | `byte`, `short`, `char`, or `int` |
| `float` | `byte`, `short`, `char`, `int`, or `long` |
| `double` | `byte`, `short`, `char`, `int`, `long`, or `float` |

### FIGURE 2.6 Java narrowing conversions

被视为缩小转换，因为符号位被合并到新的字符值中。由于字符值是无符号的，负整数将被转换为与原始整数的数值没有特定关系的字符。

请注意，`boolean` 值在扩展转换或缩小转换中均未提及。`boolean` 值不能转换为任何其他原始类型，反之亦然。

## Conversion Techniques

在 Java 中，转换可以通过三种方式发生：

- assignment conversion
- promotion
- casting

赋值转换发生在一种类型的值被赋给另一种类型的变量时，在此过程中值被转换为新类型。只能通过赋值实现扩展转换。例如，如果 `money` 是一个 `float` 变量而 `dollars` 是一个 `int` 变量，则以下赋值语句会自动将 `dollars` 中的值转换为 `float`：

```
money = dollars;
```

因此，如果 `dollars` 包含值 25，则赋值后，`money` 包含值 25.0。但是，如果我们尝试将 `money` 赋给 `dollars`，编译器会发出错误消息，提醒我们正在尝试可能丢失信息的缩小转换。如果我们真的想执行此赋值，就必须通过使用强制转换使转换显式化。

通过提升进行的转换在某些运算符需要修改其操作数以执行操作时自动发生。例如，当一个名为 `sum` 的浮点值除以一个名为 `count` 的整数值时，`count` 的值会在除法进行之前自动提升为浮点值，从而产生浮点结果：

```
result = sum / count;
```

当一个数字与字符串连接时也会发生类似的转换。数字首先被转换为字符串，然后两个字符串被连接。

强制转换是 Java 中最一般的转换形式。如果 Java 程序中可以完成某种转换，就可以使用强制转换来完成。强制转换是 Java 的一种运算符，以类型名在括号中指定。它放在要转换的值前面。例如，要将 `money` 转换为整数值，我们可以在其前面加上强制转换：

```
dollars = (int) money;
```

强制转换返回 `money` 中的值，截断任何小数部分。如果 `money` 包含值 84.69，则赋值后 `dollars` 将包含值 84。请注意，强制转换不会改变 `money` 中的值。赋值操作完成后，`money` 仍包含值 84.69。

强制转换在我们需要暂时将值视为另一种类型时在许多情况下很有帮助。例如，如果我们想用整数值 `total` 除以整数值 `count` 并得到浮点结果，可以这样做：

```
result = (float) total / count;
```

首先，强制转换运算符返回 `total` 中的值的浮点版本。此操作不会改变 `total` 中的值。然后，`count` 通过算术提升被视为浮点值。现在除法运算符将执行浮点除法并产生预期结果。如果没有包含强制转换，操作将执行整数除法并在将其赋给 `result` 之前截断答案。此外请注意，由于强制转换运算符的优先级高于除法运算符，强制转换作用于 `total` 的值，而不是除法的结果。

## SELF-REVIEW QUESTIONS (see answers in Appendix N)

SR 2.31 为什么扩展转换比缩小转换更安全？

SR 2.32 将以下每个转换识别为扩展转换或缩小转换。

- a. `int` to `long`
- b. `int` to `byte`
- c. `byte` to `short`
- d. `byte` to `char`
- e. `short` to `double`

SR 2.33 假设 `result` 是一个 `float` 变量而 `value` 是一个 `int` 变量，执行以下赋值语句后 `value` 将是什么类型的变量？解释。

```
result = value;
```

SR 2.34 假设 `result` 是一个包含值 27.32 的 `float` 变量而 `value` 是一个包含值 15 的 `int` 变量，执行以下赋值语句后每个变量的值是多少？解释。

`value = (int) result;`

SR 2.35 给定以下声明，以下每个赋值语句存储什么结果。

`int iResult, num1 = 17, num2 = 5;`

`double fResult, val1 = 12.0, val2 = 2.34;`

a. `iResult = num1 / num2;`
b. `fResult = num1 / num2;`
c. `fResult = val1 / num2;`
d. `fResult = (double) num1 / num2;`
e. `iResult = (int) val1 / num2;`

## 2.6 Interactive Programs

在执行期间设计程序以交互方式从用户读取数据通常很有用。这样，每次运行程序时都可以根据输入的数据计算新的结果。

### The Scanner Class

`Scanner` 类是标准 Java 类库的一部分，提供了读取各种类型输入值的便捷方法。输入可以来自各种来源，包括用户交互式输入的数据或存储在文件中的数据。`Scanner` 类也可以用于将字符字符串解析为单独的片段。图 2.7 列出了 `Scanner` 类提供的一些方法。

> KEY CONCEPT
>
> `Scanner` 类提供了从各种来源读取各种类型输入的方法。

我们必须首先创建一个 `Scanner` 对象才能调用其方法。Java 中的对象使用 `new` 运算符创建。以下声明创建一个从键盘读取输入的 `Scanner` 对象：

```
Scanner scan = new Scanner (System.in);
```

此声明创建了一个名为 `scan` 的变量，表示一个 `Scanner` 对象。对象本身由 `new` 运算符和对特殊方法

`Scanner (InputStream source)`

`Scanner (File source)`

`Scanner (String source)`

构造方法：设置新的扫描器以从指定的源扫描值。

`String next()`

返回下一个输入标记作为字符字符串。

`String nextLine()`

返回当前行剩余的所有输入作为字符字符串。

`boolean nextBoolean()`

`byte nextByte()`

`double nextDouble()`

`float nextFloat()`

`int nextInt()`

`long nextLong()`

`short nextShort()`

返回下一个输入标记作为指定类型。 如果下一个标记与类型不一致，则抛出 `InputMismatchException`。

`boolean hasNext()`

如果扫描器在其输入中还有另一个标记，则返回 true。

`Scanner useDelimiter (String pattern)`

`Scanner useDelimiter (Pattern pattern)`

设置扫描器的分隔模式。

`Pattern delimiter()`

返回扫描器当前用于匹配分隔符的模式。

`String findInLine (String pattern)`

`String findInLine (Pattern pattern)`

尝试查找指定模式的下一个出现位置，忽略分隔符。

### FIGURE 2.7 Some methods of the Scanner class

调用构造方法来设置对象。 `Scanner` 构造方法接受一个参数，指示输入的来源。 `System.in` 对象表示标准输入流，默认情况下为键盘。 使用 `new` 操作符创建对象将在下一章进一步讨论。

除非另有说明，否则 `Scanner` 对象假定使用空白字符（空格字符、制表符和换行符）来分隔输入的元素，称为标记。 这些字符称为输入分隔符。 如果输入标记由除空白以外的字符分隔，则分隔符集可以更改。

`Scanner` 类的 `next` 方法读取下一个输入标记作为字符串并返回它。 因此，如果输入由空格分隔的一系列单词组成，则每次调用 `next` 都会返回下一个单词。 `nextLine` 方法读取输入直到找到行尾，并将其作为一个字符串返回。

程序 `Echo`，如清单 2.8 所示，只是读取用户输入的一行文本，将其存储在保存字符字符串的变量中，然后将其回显到屏幕上。

`Echo` 类定义上方 `import` 语句告诉程序我们将在此程序中使用 `Scanner` 类。 `Scanner` 类是 `java.util` 类库的一部分。 `import` 语句的使用将在第 3 章中进一步讨论。

提供了各种 `Scanner` 方法，例如 `nextInt` 和 `nextDouble`，用于读取特定类型的数据。 `GasMileage` 程序，如清单 2.9 所示，读取行驶英里数作为整数，并读取消耗的燃油量作为 `double`，然后计算燃油里程。

### LISTING 2.8

```
//****************************************************************
// Echo.java      Author: Lewis/Loftus
//
// Demonstrates the use of the nextLine method of the Scanner class
// to read a string from the user.
//****************************************************************

import java.util.Scanner;

public class Echo
{
    //-------------------------------------------------------------
    // Reads a character string from the user and prints it.
    //-------------------------------------------------------------
    public static void main (String[] args)
```

### LISTING 2.9 continued

```
{
    int miles;
    double gallons, mpg;

    Scanner scan = new Scanner (System.in);

    System.out.print ("Enter the number of miles: ");
    miles = scan.nextInt();

    System.out.print ("Enter the gallons of fuel used: ");
    gallons = scan.nextDouble();

    mpg = miles / gallons;

    System.out.println ("Miles Per Gallon: " + mpg);
}
```

### OUTPUT

Enter the number of miles: 328
