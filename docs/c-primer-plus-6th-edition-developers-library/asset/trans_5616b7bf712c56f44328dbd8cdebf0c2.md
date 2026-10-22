

以下是示例输出：

```
Some number limits for this system:
Biggest int: 2147483647
Smallest long long: -9223372036854775808
One byte = 8 bits on this system.
Largest double: 1.797693e+308
Smallest normal float: 1.175494e-38
float precision = 6 digits
float epsilon = 1.192093e-07
```

C 预处理器是一个有用且有帮助的工具，因此在你能使用时请充分利用它。随着你在本书中继续学习，我们会向你展示更多应用。

## 探索和利用 printf() 和 scanf()

函数 printf() 和 scanf() 使你能够与程序进行通信。它们被称为输入/输出函数，或简称为 I/O 函数。它们不是你可以用 C 使用的唯一 I/O 函数，但它们是最通用的。历史上，这些函数与 C 库中的所有其他函数一样，并不是 C 定义的一部分。C 最初将 I/O 的实现留给编译器编写者；这使得 I/O 能够更好地匹配特定机器。出于兼容性的考虑，各种实现都附带了 scanf() 和 printf() 的版本。然而，不同实现之间偶尔会出现差异。C90 和 C99 标准描述了这些函数的标准版本，我们将遵循该标准。

虽然 printf() 是输出函数而 scanf() 是输入函数，但两者工作方式非常相似，各自使用一个控制字符串和一个参数列表。我们将首先介绍 printf()，然后介绍 scanf()，向你展示它们的工作方式。

## printf() 函数

当你要求 printf() 打印一个变量时，你给出的指令取决于变量类型。例如，我们在打印整数时使用过 %d 记法，在打印字符时使用过 %c 记法。这些记法称为转换说明，因为它们指定了数据如何转换为可显示形式。我们将列出 ANSI C 标准为 printf() 提供的转换说明，然后展示如何使用其中最常见的说明。表 4.3 展示了转换说明符以及它们导致打印的输出类型。

表 4.3 转换说明符及 resulting 打印输出

| Conversion | Output Specification |
|------------|----------------------|
| %a | Floating-point number, hexadecimal digits and p-notation (C99/C11). |
| %A | Floating-point number, hexadecimal digits and P-notation (C99/C11). |

```
printf("Farewell! thou art too dear for my possessing,\n");
printf("%c%d\n", '$', 2 * cost);

return 0;
}
```

输出，当然是

```
The 7 contestants ate 12.750000 berry pies.
The value of pi is 3.141593.
Farewell! thou art too dear for my possessing,
$15600
```

这是使用 printf() 的格式：

```
printf(Control-string, item1, item2,...);
```

Item1、item2 等是要打印的项目。它们可以是变量或常量，甚至是先求值后再打印值的表达式。Control-string 是一个字符字符串，描述项目如何打印。如第 3 章所述，控制字符串应包含与每个要打印的项目对应的转换说明符。例如，考虑以下语句：

```
printf("The %d contestants ate %f berry pies.\n", number,
    pies);
```

Control-string 是用双引号括起来的短语。此特定控制字符串包含两个转换说明符，对应于 number 和 pies——两个要显示的项目。图 4.6 显示了另一个 printf() 语句的示例。

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_142_0.png)

图 4.6 Arguments for printf().

以下是示例中的另一行：

```
printf("The value of pi is %f.\n", PI);
```

这次，项目列表只有一个成员——符号常量 PI。

正如你在图 4.7 中看到的，Control-string 包含两种不同的信息形式：

- 实际打印的字符
- 转换说明

## Caution

不要忘记为 Control-string 之后列表中的每个项目使用一个转换说明。如果你忘记了这个基本要求，后果不堪设想！不要这样做：

```
printf("The score was Squids %d, Slugs %d.\n", score1);
```

这里，第二个 %d 没有值。这种失误的结果取决于你的系统，但最好的情况你也会得到部分无意义的内容。

![](img/c84b77d4534c72b32b9d7ca8ee81bf4c_143_0.png)

图 4.7 Anatomy of a control string.

如果你只想打印一个短语，就不需要任何转换说明。如果你只想打印数据，可以省略运行中的评论。以下来自清单 4.6 的每个语句都是完全可以接受的：

```
printf("Farewell! thou art too dear for my possessing,\n");
```

```
printf("%c%d\n", '$', 2 * cost);
```

在第二个语句中，注意打印列表中的第一个项目是字符常量而不是变量，第二个项目是乘法。这说明 printf() 使用的是值，无论是变量、常量还是表达式。

由于 printf() 函数使用 % 符号来标识转换说明，如果你想打印 % 符号本身，就会有一个小问题。如果你只使用一个 % 符号，编译器会认为你搞砸了转换说明。解决方法很简单——只需使用两个 % 符号，如下所示：

```
pc = 2*6;
```

```
printf("Only %d%% of Sally's gribbles were edible.\n", pc);
```

以下输出会产生：

```
Only 12% of Sally's gribbles were edible.
```

## printf() 的转换说明符修饰符

你可以通过在 % 和定义转换字符之间插入修饰符来修改基本的转换说明。表 4.4 和 4.5 列出了你可以在那里合法放置的字符。如果你使用多个修饰符，它们应按表中的顺序排列

| Modifier | Meaning |
|---|---|
| t | 与整数转换说明符一起使用，表示 `ptrdiff_t` 值。这是对应于两个指针之间差值的类型。 (C99)。 |
|  | Examples: `"%td"` and `"%12ti"`. |
| z | 与整数转换说明符一起使用，表示 `size_t` 值。这是 `sizeof` 返回的类型。 (C99)。 |
|  | Examples: `"%zd"` and `"%12zx"`. |

## Note Type Portability

`sizeof` 运算符，回顾一下，返回类型或值的大小，以字节为单位。这应该是某种形式的整数，但标准只规定它应为无符号整数。因此它可能是 `unsigned int`、`unsigned long`，甚至是 `unsigned long long`。因此，如果你要使用 `printf()` 显示一个 `sizeof` 表达式，你可能在一个系统上使用 `%u`，在另一个系统上使用 `%lu`，在第三个系统上使用 `%llu`。这意味着你需要研究适用于你的系统的正确用法，并且如果你将程序移动到不同的系统，可能需要更改你的程序。好吧，本来是这样的，除了 C 提供了帮助以使类型更具可移植性。首先，`stddef.h` 头文件（在包含 `stdio.h` 时包含）将 `size_t` 定义为你的系统用于 `sizeof` 的类型；这称为底层类型。其次，`printf()` 使用 `z` 修饰符来指示用于打印的相应类型。类似地，C 定义了 `ptrdiff_t` 类型和 `t` 修饰符，以指示系统用于两个地址之间差值的底层有符号整数类型。

## Note Conversion of float Arguments

有转换说明符用于打印浮点类型 `double` 和 `long double`。然而，没有用于 `float` 的说明符。原因是在 K&R C 中，`float` 值在用于表达式或作为参数之前会自动转换为 `double` 类型。ANSI C（或更晚版本）通常不会自动将 `float` 转换为 `double`。为了保护大量假设 `float` 参数会被转换为 `double` 的现有程序，所有传递给 `printf()` 的 `float` 参数——以及任何其他不使用显式原型的 C 函数——仍然会自动转换为 `double`。因此，在 K&R C 或 ANSI C 下，显示 `float` 类型不需要特殊的转换说明符。

## Table 4.5 The printf() Flags

| Flag | Meaning |
|---|---|
| - | 项目左对齐；即它从字段左侧开始打印。 |
|  | Example: `"%-20s"`. |

