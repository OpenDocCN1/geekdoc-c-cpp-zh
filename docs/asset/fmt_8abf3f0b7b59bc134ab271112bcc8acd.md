
```
result = (14 + 8) / 2;
```

任何括号内的表达式都会首先评估。在复杂的表达式中，即使不是严格需要，使用括号也是一种良好的习惯，以明确表达式是如何评估的。

括号中的表达式首先被评估。括号可以嵌套，且最内层的表达式将先执行。考虑以下表达式：

```
result = 3 * ((18 - 4) / 2);
```

在这个例子中，结果是 21。首先由于括号执行了减法。然后，乘法和除法处于同一优先级，将从左到右执行。最后，执行乘法。

特定表达式的评估可以使用表达式树来显示，如图 2.3 所示。运算符从底部向上执行，因此，树底部的运算符优先级高于上方的运算符。

![](img/7f8e069c1898b741edc17feed34b0c1_104_0.png)

图 2.3 表达式树

| 优先级 | 运算符 | 操作 | 结合性 |
|---|---|---|---|

| 1 | + | 一元加 | 从右到左 |
| | | 一元减 | |
| 2 | * | 乘法 | 从左到右 |
| | / | 除法 | |
| | % | 取余 | |
| 3 | + | 加法 | 从左到右 |
| | | 减法 | |
| | + | 字符串拼接 | |
| 4 | = | 赋值 | 从右到左 |

图 2.4 部分 Java 运算符优先级

表达式中的括号本身也是运算符。括号的优先级高于几乎任何其他运算符。图 2.4 显示了算术运算符、括号和赋值运算符之间的关系。附录 D 包含了所有运算符的完整优先级表。

为了使表达式语法正确，左括号的数量必须与右括号匹配，且它们必须正确嵌套。以下示例不是有效表达式：

```
result = (19 + 8) % 3 - 4); // 无效
result = ((19 + 8) ); // 无效
```

记住，当在表达式中引用变量时，其当前值被用于计算。在赋值语句中，变量 `count` 的当前值加上变量 `total` 的当前值，结果存储在变量 `sum` 中：

```
sum = count + total;
```

在赋值之前 `sum` 中包含的原始值会被计算值覆盖。`count` 和 `total` 中存储的值不会改变。

同一个变量可以出现在赋值语句的左侧和右侧。假设执行以下赋值语句时，变量 `count` 的当前值为 15：

```
count = count + 1;
```

## 第2章 数据与表达式

## 2.4 表达式

由于右侧表达式首先求值，获取 `count` 的原始值并对其加 1，产生结果 16。该结果随后存储在变量 `count` 中，覆盖了原始值 15。因此，赋值语句*递增*（或对变量 `count` 加 1）。

让我们看看表达式处理的另一个示例。列表 2.7 中的 `TempConverter` 程序将摄氏度转换为等值的华氏值，使用了公式：`fahrenheit = 9/5 + 32`

```
列表 2.7
****************************************************************
// TempConverter.java      作者: Loftus
// 展示了原始数据类型和算术
// 表达式的使用
****************************************************************
public class TempConverter {
    // 计算特定摄氏度的等值华氏值
    // 使用公式 (9/5) + 32。
    public static void main(String[] args) {
        final int BASE = 32;
        final double CONVERSION_FACTOR = 9.0 / 5.0;

        double fahrenheitTemp;
        int celsiusTemp = 24; // 要转换

        fahrenheitTemp = celsiusTemp * CONVERSION_FACTOR + BASE;
        System.out.println("Celsius Temperature: " + celsiusTemp);
        System.out.println("Fahrenheit Equivalent: " + fahrenheitTemp);
    }
}
```

```
输出：
Celsius Temperature: 24
Fahrenheit Equivalent: 75.2
```

注意在温度转换程序中，操作数是浮点字面量，以确保数字的小数部分被保留。优先级规则规定在最终加法计算之前进行乘法。`TempConverter` 程序非常有用，因为它每次执行程序时都会获取要转换的值并产生相同的结果。读取用户输入的交互式程序将在在本章稍后部分讨论。

### 递增和递减运算符

有两种用的算术运算符。递增运算符（`++`）对任何整数或浮点值加 1。递减运算符（`--`）类似，它从值中减 1。它们都是元运算符，因为它们只作用一个操作数。以下语句会导致 `count` 的值递增：

```
count++;
```

结果存储回变量 `count`。因此，它在功能上等于以下语句：

```
count = count + 1;
```

递增和递减运算符可以应用于变量之后（如 `count++` 或 `count--`），产生所谓的后置形式。它们也可以应用于变量之前（如 `++count` 或 `--count`），产生所谓的前缀形式。当单独作为语句时，前缀和后置形式在功能上是等价的。也就是说，写成

```
count++;
```

或者

```
++count;
```

然而，在较大的表达式中使用递增或递减运算符可能会产生不同的结果。例如，如果变量 `count` 当前值为 15，以下语句将 15 赋值给 `total`，将 16 赋值给 `count`：

```
total = count++;
```

然而，以下语句将 16 同时赋值给 total 和 `count`：

```
total = ++count;
```

在两种情况下 `count` 的值都会递增，但在较大的表达式中的值取决于使用的是递增运算符的前缀还是后置形式。由于递增和递减运算符的前缀形式和后置形式之间存在细微差异，应该谨慎使用。始终优先考虑可读性。

### 赋值运算符

为了方便，Java 定义了几个赋值运算符，将基本操作与赋值结合。例如，`+=` 运算符用法如下：

```
total += 5;
```

这与以下语句执行相同的操作：

```
total = total + 5;
```

赋值运算符的右侧可以是完整的表达式。运算符右侧的表达式被求值，然后将结果加到左侧变量的当前值，并将该值存储在变量中。因此，以下语句：

```
total += (sum - 12) / count;
```

等于：

```
total = total + ((sum - 12) / count;
```

Java 中定义了许多类似的赋值运算符，包括执行减法（`-=`）、乘法（`*=`）、除法（`/=`）和取余（`%=`）的运算符。所有的赋值运算符都首先求值右侧的整个表达式，然后将结果作为另一个操作的右操作数。因此，以下语句：

```
result *= count1 + count2;
```

等于：

```
result = result * (count1 + count2);
```

同样，以下语句：

```
result %= highest - 40;
```

等于：

```
result = result % (highest - 40);
```

某些赋值运算符根据操作数的类型执行字符串连接。例如，`+=` 运算符用于字符串。

### 自测

- 2.21 19 在表达式中求值时的结果是什么？
- 2.22 13 在表达式中求值时的结果是什么？
- 2.23 如果整数 `diameter` 当前持有值 5，在执行以下语句后值是多少？`diameter = diameter;`
- 2.24 什么是运算符优先级？
- 2.25 下列各项的值是多少？
  - a. 15 + 7
  - b. (15 + 7)
  - c. 3 * 7
  - d. 17 % 5
  - e. 100 / 2
  - f. 100 % 2
- 2.26 对于以下每一项，说明它们有效还是无效。如果无效，解释原因。
  - a. result = (5 + 2);
  - b. result = (15 + 2);
  - c. result = 5 + 2;
  - d. result = (5 + 2);
- 2.27 在执行以下序列后，整数变量 `result` 包含什么值？
```
result = 27;
result = result + 3;
result = result / 7;
result = result * 2;
```
- 2.28 在执行以下序列后，整数变量 `result` 包含什么值？
```
int base;
int result;
base = 5;
result = base + 3;
base = 7;
```
- 2.29 什么是赋值运算符？
- 2.30 如果整数变量 `weight` 当前持有值 100，在执行以下语句后其值是多少？解释。`weight = 17;`

# 第 2 章 数据与表达式

| 源 | 目标 |
|---|--|
| byte | short, int, long, float, or double |
| short | int, long, float, or double |
| char | int, long, float, or double |
| int | long, float, or double |
| long | float or double |
| float | double |

图 2.5 Java 宽转换

![](img/7f8e069c1898b741edc17dfeed34b0c1_111_0.png)

宽转换不会丢失任何关于数值大小的数；但导致浮点值产生的宽转换可能会丢失精度。当将 `int` 或 `long` 转换为 `float`，或将 `long` 转换为 `double` 时，某些低有效位可能会丢失。在这种情况下，生成的浮点值将是整数值的舍入版本，遵循 IEEE 754 浮点标准中的舍入技术。

窄转换比宽转换更有可能丢失信息。它们通常是从一个类型转换为另一个存储值所需的空间较小的类型，因此某些信息可能会受到损害。窄转换会丢失数值大小和精度。因此，通常情况下，应该避免它们。图 2.6 列出了 Java 窄转换。

窄转换中空间缩小情况的一个例外是将 `byte`（8 位）或 `short`（16 位）转换为 `char`（16 位）。这些仍然被视为窄转换，因为符号位被并到了新的字符值中。由于字符值（char）是无符号的，负整数将转换为一个与原始整数数值值没有特定关系的字符。

| 源 | 目标 |
|---|--|
| byte | char |
| short | byte or char |
| char | byte or short |
| int | byte, short, char, or int |
| long | byte, short, char, or int |
| float | byte, short, char, int, or long |
| double | byte, short, char, int, long, or float |

图 2.6 Java 窄转换

## 2.5 数据转换

注意，在宽转换或窄转换中均未提到布尔值。`boolean` 值不能转换为任何其他基本类型，反之亦然。

### 转换技术

在 Java 中，转换可以通过三种方式发生：

- 赋值转换
- 提升（promotion）
- 强制类型转换（casting）

当一个类型的值赋值给另一个类型的变量时，会发生赋值转换，期间值会被转换为新类型。只有宽转换可以通过赋值完成。例如，如果 `money` 是一个 `float` 变量而 `dollars` 是一个 `int` 变量，那么赋值语句会自动将 `dollars` 中的值转换为 `float`：

```
money = dollars;
```

因此，如果 `dollars` 包含值 25，赋值后，`money` 包含值 25.0。然而，如果我们尝试将 `money` 赋值给 `dollars`，编译器将发出错误，提醒我们正在尝试进行可能丢失信息的窄转换。如果我们真的想这样做，我们必须使用强制类型转换来显式进行转换。

当某些运算符为了执行操作而修改其操作数时，通过提升进行的转换会自动发生。例如，当浮点值除以一个整数计数 `count` 时，`count` 的值在除法发生之前会自动提升为浮点值，产生一个浮点结果：

```
result = sum / count;
```

当数字与字符串拼接时，也会发生类似的转换。第一个会被转换为（提升为）字符串，然后将两个字符串拼接在一起。

强制类型转换是 Java 中最通用的转换形式。如果转换在 Java 程序中可以完成，就可以使用强制类型转换完成。强制类型转换是一个 Java 运算符，由括号中的类型名称指定。它放置在要转换的值前面。例如，要将 `money` 转换为整数值，我们可以在它前面加上强制类型转换：

```
dollars = (int) money;
```

强制类型转换返回 `money` 中的值，并截断任何小数部分。如果 `money` 包含值 84.69，那么赋值后 `dollars` 将包含值 84。注意，强制类型转换不会改变 `money` 中的值。赋值操作完成后，`money` 仍然包含值 84.69。

在许多需要将一个值视为其他类型的情况下，强制类型转换是有帮助的。例如，如果我们想将整数值除以整数计数 `count` 并得到浮点结果，我们可以这样做：

```
result = (float) total / count;
```

首先，强制转换运算符返回 `total` 中值的浮点版本。此操作不会改变 `total` 中的值。然后，`count` 通过算术提升被视为浮点值。现在，除法运算符执行浮点除法并产生预期的结果。如果没有包含强制类型转换，该操作将执行整数除法并在赋值给 `result` 之前截断答案。注意，由于强制类型转换运算符的优先级高于除法运算符，强制类型转换作用于 `total` 的值，而不是除法的结果。

### 自测习题

SR 2.31 为什么宽转换比窄转换更安全？
SR 2.32 识别以下每个转换是宽转换还是窄转换。
- a. int 到 long
- b. int 到 byte
- c. byte 到 short
- d. byte 到 char
- e. short 到 double
SR 2.33 假设 `result` 是 `float` 变量而 `value` 是 `int` 变量，执行以下语句后 `result` 将是什么类型？
```
result = value;
```
SR 2.34 假设 `result` 是 `float` 变量而 `value` 是 `int` 变量，执行以下语句后其值是多少？
```
value = (int) result;
```
SR 2.35 给以下声明，每个变量存储了什么值？
```
int result = 12;
double val1 = 5;
```
- a. result = num1
- b. result = val2
- c. result
- d. result = (double) num1
- e. val1

### 2.6 交互式程序

设计一个从用户读取数据的程序通常有用。这样，每次程序运行时都可以根据输入的数据计算新结果。

#### Scanner 类

`Scanner` 类是标准库的一部分，提供了读取各种类型的方便方法。输入可以来自各种来源，包括用户输入的数据或存储在文件中的数据。`Scanner` 类还可以用于将字符串拆分为部分。2.7 列出了 `Scanner` 提供的一些方法。

> 核心概念
> `Scanner` 类提供了读取各种类型的方法。

我们必须先创建一个 `Scanner` 才能调用它的方法。Java 对象使用 `new` 运算符创建。以下声明创建了一个从键盘读取输入的 `Scanner` 对象：

```java
Scanner scan = new Scanner(System.in);
```

此声明创建了一个名为 `scan` 的变量，代表一个 `Scanner` 对象。对象本身是通过 `new` 运算符和对特殊的调用创建的。

```
Scanner (InputStream source)
Scanner (File source)
Scanner (String source)
```

构造函数：设置新扫描器从指定的源扫描。

String next() 返回下一个输入标记作为字符字符串。

String nextLine() 返回当前行的剩余输入作为字符字符串。

```
boolean nextBoolean()
byte nextByte()
double nextDouble()
float nextFloat()
int nextInt()
long nextLong()
short nextShort()
```

以指示类型返回下一个输入标记。如果下一个标记与类型不一致，则抛出 `InputMismatchException`。

boolean hasNext() 如果扫描器输入中有另一个标记，则返回 true。

Scanner useDelimiter (String pattern)

Scanner useDelimiter (Pattern pattern) 设置扫描器的分隔符模式。

Pattern delimiter() 返回扫描器当前用于匹配分隔符的模式。

String findInLine (String pattern)
