

#include <string>

为什么会这样呢？因为string类型，就像我们将在第7章学习的其他几种类型一样，并不是C++内建的基本类型之一，而是在string库中定义的类。#include指令使该类型可用于程序。

与字符字面量有些类似，字符串字面量是由双引号括起来的一系列字符。⁶ 例如，

```
"Ohm's Law"
"Enter project id on one line\n\tand its name on the next.\n"
"\nThe project cost = $"
"Einstein said, \"God is subtle but he is not malicious\""
```

都是字符串字面量。正如最后三个示例所示，可以在字符串字面量中使用转义序列。还要注意，包含单个字符的字符串字面量不是char字面量；例如，"X"是字符串字面量，而'X'是char字面量。它们不能互换使用。

如果两个字符串字面量相邻，或者仅由空白字符（空格、制表符和换行符）分隔，则它们将连接成一个字面量。例如，对于

```
"square " "feet"
```

或

```
"square "
"feet"
```

这两个字符串字面量将合并为

```
"square feet"
```

输出的可读性通常可以通过在行之间加空行来改善。使用两个换行符可以实现这一点。例如，如果我们输出字符串字面量

```
"First row\n\nSecond row"
```

第一个换行符（在下面的输出中显示为↲）将结束出现First row的那一行，第二个换行符使下一行为空行，之后出现Second row：

```
First row↲
↲
Second row
```

### 3.2.2 标识符

示例3.1程序为一些软件对象使用了名称：`element`代表放射性元素，`halfLife`代表其半衰期，`time`代表一段时间，`initialAmount`和`amountRemaining`代表该元素的数量。这些名称称为**标识符**。它们应以字母开头，后面可以跟任意多个字母、数字或下划线。它们不能是C++**关键字**（例如`int`、`const`、`double`等），这些关键字是为特殊对象保留的。C++关键字的完整列表见附录B。

*使用能暗示其含义的有意义的标识符是一种良好的编程实践，因为这样的名称使程序更易于阅读和理解。因此，它们充当程序文档的一部分，并有助于程序维护。* 例如，标识符`feetPerSecond`比任何缩写标识符`f`、`ft`或`FPS`都更有意义，因为这些缩写可能表示包含这些字母的任何其他内容。你应该抵制为了少敲几下键盘而使用短标识符的诱惑。*完整的单词比缩写更可取。*

重要的是要记住，C++是*区分大小写*的——也就是说，它区分大写和小写。例如，`length`和`Length`是不同的标识符。类似地，main函数的名称必须是`main`，而不是`Main`。

命名约定因程序员而异，但最常见的约定之一如下：

- *变量：* 使用小写名称，但在第一个单词之后的每个组成单词首字母大写。一些示例是`length`、`halfLife`和`feetPerSecond`。
- *常量：* 使用全大写字符的名称，并用下划线（`_`）字符分隔各个组成单词。一些示例是`PI`、`TWO_PI`和`SPEED_OF_LIGHT`。

在程序中可以使用标识符之前，必须*声明*它以告知编译器其含义。我们现在先看变量的声明，然后再看常量的声明。

### 3.2.3 变量

在分析问题时，我们经常发现问题中的对象之间存在可以用*公式*表示的关系。例如，示例3.1程序中使用的放射性衰变定律公式可以表示如下：

$$a = a_0 \times 0.5^{-t/h}$$

在这个公式中，a、a₀、t和h是变量，可以代入数值来计算a的值。

在计算中，变量（variable）一词指的是一个内存位置，可以在其中存储值并在以后检索。编译器的任务之一是将这样的内存位置与程序中为变量命名的每个标识符相关联。为此，它必须知道变量的名称以及它可能拥有的值的类型，以便分配适当大小和形式的内存位置。这就是变量声明的目的，其形式如下：

变量声明

形式：

```
type variable_name;
type variable_name = initializer_expression;
```

其中type是基本数据类型之一（或后面讨论的数据类型之一），variable_name是有效的C++标识符。

目的：

指示C++编译器为指定类型的值保留内存，并将该内存位置与名称variable_name相关联。在第二种形式中，initializer_expression的值将存储在该内存位置；对于第一种形式，variable_name的值是未定义的（或不确定的）。

示例3.1程序中的声明

```
string element;
double halflife;
double initialAmount, time;
```

展示了变量声明的第一种形式。这些变量的值被认为是未定义的，因为与它们关联的内存位置的内容是未知的。如果我们希望它们有特定的初始值，可以使用声明的第二种形式，例如，

```
string element = " ";
double halfLife = 0;
double initialAmount = 0, time = 0;
```

指定element的初始值是一个包含空格的字符串，halfLife、initialAmount和time的初始值都是0。对于像element这样类型为string的变量，请记住必须像示例3.1那样#include string库。

适当大小的内存位置将与这些变量中的每一个相关联。例如，对于double变量time，将分配一个适合double类型（通常为8字节）的内存位置。我们可以这样设想：

time ?

这里，问号表示该变量是未定义的。尽管某些版本的C++会将数值变量初始化为0，但其他版本只是让它们的初始值成为垃圾值——即分配给它的内存位置中的位串所对应的任何值。你不应该假设未初始化的变量会有特定的值。

如果time的声明改为

```
double time = 0;
```

0将被用作初始值：

time 0

对于上述time的任一声明，如果随后输入180作为time的值，则存储在该内存位置中的值将变为180.0：

time 180.0

类似地，声明

```
string element = "polonium";
```

将使用“polonium”作为element的初始值：

element polonium

变量声明的放置位置在很大程度上是编程风格的问题，因为C++允许将声明放在变量首次使用之前的（几乎）任何位置。在本书中，变量通常会在首次使用之前声明，因为这更容易确保变量的使用方式与其类型一致。

### 3.2.4 常量

除了变量之外，我们还可以为常量使用名称。当程序使用通用常量（如几何常量π或光速）时，这尤其有用，

```
const double PI = 3.14159265359,
    SPEED_OF_LIGHT = 2.997925e8; // meters/sec
```

但也可以用于将名称与程序中使用的其他常量关联起来：

```
const int UPPER_LIMIT = 1000;
const char
    PERCENT_SIGN = '%',      // using a normal character
    SPACE = ' ',             // using a white space char
    TAB = '\t',             // using an escape sequence
    BELL = '\007';          // using an octal (ASCII) code
```

通常，常量声明具有以下形式：

常量声明

形式：

```
const type CONSTANT_NAME = constant-expression;
```

其中const是C++关键字；type是基本数据类型之一（或后面讨论的数据类型之一）；CONSTANT_NAME是有效的C++标识符；constant-expression是任何有效表达式（如后面章节所述），其值是一个类型为type的常量。

目的：

将名称与常量关联。任何在程序中更改此值的尝试都是错误。

为常量使用名称有两个主要原因。一个是让程序更易于理解。为了说明，考虑以下语句：

```
populationChange = (0.1853 - 0.1175) * population;
```

0.1853和0.1175是“魔法数字”，因为它们似乎毫无解释地神奇出现。然而，如果我们定义常量BIRTH_RATE和DEATH_RATE：

```
const double
    BIRTH_RATE = 0.1853, // rate at which people are born
    DEATH_RATE = 0.1175; // rate at which people die
```

我们可以将语句重写为更易理解的形式：

```
populationChange = (BIRTH_RATE - DEATH_RATE) * population;
```

使用常量的第二个好处是使程序更易于修改。为了说明，假设我们在程序中的多个地方使用了π的值3.1416，并且发现这个值不能提供所需的精度。为了修正程序，我们将不得不

