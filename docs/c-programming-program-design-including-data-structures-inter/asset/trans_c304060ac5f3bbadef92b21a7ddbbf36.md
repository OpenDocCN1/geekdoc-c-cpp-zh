
| 输出 | 语句所在行 |
|---|---|
| 7 | 第3行 |
| 1.5 | 第4行 |
| Hello there. | 第5行 |
| 7 | 第6行 |
| 8 | 第7行 |
| 3 + 5 ** | 第8行和第9行 |
| 20 | 第11行 |
| a | 第12行 |
| 65 | 第13行 |
| 78 | 第14行 |

大部分情况下，输出很直接。看看第7、8、9和10行语句的输出。第7行的语句输出 3 + 5 的结果，即 8，并将插入点移到下一行开头。第8行的语句输出字符串 3 + 5。注意，第8行的语句仅由字符串 3 + 5 组成。因此，在打印 3 + 5 之后，插入点仍位于 5 之后；它不会移到下一行开头。第9行语句的下一个输出会在插入点输出一个空格和 `**`，该插入点此前位于 5 之后。

第10行的输出语句只包含操纵符 endl，它将插入点移到下一行开头。因此，当第11行的语句执行时，输出从该行开头开始。注意，在此输出中，列“语句所在行”不包含第10行。这是因为第10行的语句不产生任何可打印输出。它只是将插入点移到下一行开头。接下来，第11行的语句输出 2 + 3 * 6 的值，即 20。然后，操纵符 endl 将插入点移到下一行开头。

> 在表达式中输出或访问变量的值不会破坏或修改变量的内容。

现在让我们仔细看看换行符 '\n'。考虑以下 C++ 语句：

```cpp
cout << "Hello there.";
cout << "My name is James.";
```

如果这些语句依次执行，输出为：

```
Hello there.My name is James.
```

现在考虑以下 C++ 语句：

```cpp
cout << "Hello there.\n";
cout << "My name is James.";
```

这些 C++ 语句的输出为：

```
Hello there.
My name is James.
```

当在字符串中遇到 `\n` 时，插入点会定位到下一行开头。还要注意，`\n` 可以出现在字符串中的任何位置。例如，以下语句的输出：

```cpp
cout << "Hello \nthere. \nMy name is James.";
```

为：

```
Hello
there.
My name is James.
```

另外，请注意以下语句的输出：

```cpp
cout << '\n';
```

与以下语句的输出相同：

```cpp
cout << "\n";
```

这等价于以下语句的输出：

```cpp
cout << endl;
```

因此，以下语句序列的输出：

```cpp
cout << "Hello there.\n";
cout << "My name is James.";
```

等价于以下语句序列的输出：

```cpp
cout << "Hello there." << endl;
cout << "My name is James.";
```

### 示例 2-23

考虑以下 C++ 语句：

```cpp
cout << "Hello there.\nMy name is James.";
```

或者：

```cpp
cout << "Hello there.";
cout << "\nMy name is James.";
```

或者：

```cpp
cout << "Hello there.";
cout << endl << "My name is James.";
```

在每种情况下，这些语句的输出为：

```
Hello there.
My name is James.
```

### 示例 2-24

以下 C++ 语句的输出：

```cpp
cout << "Count...\n....1\n.....2\n.....3";
```

或者：

```cpp
cout << "Count..." << endl << ".....1" << endl
     << ".....2" << endl << ".....3";
```

为：

```
Count...
.....1
.....2
.....3
```

### 示例 2-25

假设你想将以下句子作为一条消息的一部分输出在一行中：

It is sunny, warm, and not a windy day. We can go golfing.

显然，你会使用一条输出语句来产生这个输出。然而，在编程代码中，作为输出语句的一部分，这条语句可能无法放在一行中。当然，你可以像下面这样使用多条输出语句：

```cpp
cout << "It is sunny, warm, and not a windy day. ";
cout << "We can go golfing." << endl;
```

注意第一条语句末尾的分号，以及第二条语句开头的标识符 cout。另外，注意第一条语句末尾没有操纵符 endl。这里使用了两条输出语句来在一行中输出该句子。

等价地，你可以使用以下输出语句来输出这个句子：

```cpp
cout << "It is sunny, warm, and not a windy day. "
     << "We can go golfing." << endl;
```

在这条语句中，注意第一行末尾没有分号，并且标识符 cout 没有出现在第二行开头。由于第一行末尾没有分号，这条输出语句会延续到第二行。另外，注意每一行句子开头和结尾的双引号。该字符串被分成两个字符串，但这两个字符串都是同一条输出语句的一部分。

如果输出语句中出现的字符串很长，而你想在一行中输出该字符串，可以使用前面两种方法中的任意一种来拆分字符串。然而，以下语句将是非法的：

```cpp
cout << "It is sunny, warm, and not a windy day.
       We can go golfing." << endl; //illegal
```

换句话说，键盘上的回车（Enter）键不能成为字符串的一部分。也就是说，在编程代码中，不能通过按键盘上的回车（Enter）键将字符串拆分成多行。

回想一下，换行符是 \n，它会使插入点移到下一行开头。C++ 中有许多转义序列，可让你控制输出。表 2-4 列出了一些常用转义序列。

### 表 2-4 常用转义序列

| 转义序列 | 描述 |
|---|---|
| `\n` | 换行——光标移到下一行开头 |
| `\t` | 制表符——光标移到下一个制表位 |
| `\b` | 退格——光标向左移动一个空格 |
| `\r` | 回车——光标移到当前行开头（而不是下一行） |
| `\\` | 反斜杠——打印反斜杠 |
| `\'` | 单引号——打印单引号 |
| `\"` | 双引号——打印双引号 |

以下示例展示其中一些转义序列的效果。

### 示例 2-26

以下语句的输出：

```cpp
cout << "The newline escape sequence is \\n" << endl;
```

为：

```
The newline escape sequence is \n
```

以下语句的输出：

```cpp
cout << "The tab character is represented as \'\\t\'" << endl;
```

为：

The tab character is represented as `'\t'`

注意，单引号也可以在不使用转义序列的情况下打印。因此，前面的语句等价于以下输出语句：

```cpp
cout << "The tab character is represented as '\\t'" << endl;
```

以下语句的输出：

```cpp
cout << "The string \"Sunny\" contains five characters." << endl;
```

为：

The string "Sunny" contains five characters.

> **注意：** 与本文配套的网站包含一个 C++ 程序，用于展示示例 2-26 中语句的效果。该程序名为 `Example2_26.cpp`。

要在程序中使用 `cin` 和 `cout`，必须包含某个头文件。下一节将解释这个头文件是什么、如何在程序中包含头文件，以及为什么程序中需要头文件。第3章将详细解释 `cin` 和 `cout`。

## 预处理指令

C++ 中只明确定义了少量操作，例如算术和赋值操作。运行 C++ 程序所需的许多函数和符号都以库的集合形式提供。每个库都有一个名称，并通过头文件来引用。例如，执行输入/输出（I/O）所需函数的描述包含在头文件 `iostream` 中。类似地，一些非常有用的数学函数（如幂、绝对值和正弦）的描述包含在头文件 `cmath` 中。如果你想使用 I/O 或数学函数，就需要告诉计算机在哪里找到必要的代码。你使用预处理指令和头文件名来告诉计算机库中提供的代码的位置。预处理指令由称为**预处理器**的程序处理。
