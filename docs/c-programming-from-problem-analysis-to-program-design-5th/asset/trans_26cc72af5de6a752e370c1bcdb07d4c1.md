
> **注意**  
> 在表达式中输出或访问变量的值不会销毁或修改变量的内容。

现在让我们仔细看看换行字符 `\n`。考虑以下 C++ 语句：

```cpp
cout << "Hello there.";
cout << "My name is James.";
```

如果按顺序执行这些语句，输出为：

```text
Hello there.My name is James.
```

现在考虑以下 C++ 语句：

```cpp
cout << "Hello there.\n";
cout << "My name is James.";
```

这些 C++ 语句的输出为：

```text
Hello there.
My name is James.
```

当在字符串中遇到 `\n` 时，插入点会定位到下一行开头。另请注意，`\n` 可以出现在字符串中的任何位置。例如，以下语句的输出：

```cpp
cout << "Hello \nthere. \nMy name is James.";
```

为：

```text
Hello
there.
My name is James.
```

另请注意，以下语句的输出：

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

或

```cpp
cout << "Hello there.";
cout << "\nMy name is James.";
```

或

```cpp
cout << "Hello there.";
cout << endl << "My name is James.";
```

每种情况下，这些语句的输出都是：

```text
Hello there.
My name is James.
```

### 示例 2-24

以下 C++ 语句的输出：

```cpp
cout << "Count...\n....1\n......2\n.......3";
```

或

```cpp
cout << "Count..." << endl << "....1" << endl
     << "......2" << endl << ".......3";
```

为：

```text
Count...
....1
......2
.......3
```

### 示例 2-25

假设你想将以下句子作为消息的一部分输出在一行中：

今天阳光明媚、温暖，而且没有风。我们可以去打高尔夫球。

显然，你会使用一条输出语句来产生这个输出。然而，在编程代码中，这条语句作为输出语句的一部分可能无法放在一行内。当然，你可以像下面这样使用多条输出语句：

```cpp
cout << "It is sunny, warm, and not a windy day. ";
cout << "We can go golfing." << endl;
```

注意第一条语句末尾的分号，以及第二条语句开头的标识符 `cout`。另请注意，第一条语句末尾没有操纵符 `endl`。这里使用两条输出语句将这句话输出在一行中。等价地，你也可以使用以下输出语句输出这句话：

```cpp
cout << "It is sunny, warm, and not a windy day. "
     << "We can go golfing." << endl;
```

在这条语句中，请注意第一行末尾没有分号，并且第二行开头没有出现标识符 `cout`。由于第一行末尾没有分号，这条输出语句会延续到第二行。另请注意每一行句子开头和结尾的双引号。该字符串被拆分成两个字符串，但这两个字符串都属于同一条输出语句。

如果输出语句中出现的字符串很长，而你想将该字符串输出在一行中，可以使用前面两种方法中的任意一种来拆分该字符串。但是，以下语句是不正确的：

```cpp
cout << "It is sunny, warm, and not a windy day.
          We can go golfing." << endl;        //illegal
```

换句话说，键盘上的回车（或 Enter）键不能成为字符串的一部分。也就是说，在编程代码中，*不能*使用键盘上的回车（或 Enter）键将字符串拆分成多行。

回顾一下，换行字符是 `\n`，它会使插入点移动到下一行开头。C++ 中有许多转义序列，可用于控制输出。表 2-4 列出了一些常用的转义序列。

### 表 2-4 常用转义序列

|  | 转义序列 | 描述 |
|---|---|---|
| `\n` | 换行 | 光标移动到下一行开头 |
| `\t` | 制表符 | 光标移动到下一个制表位 |
| `\b` | 退格 | 光标向左移动一个空格 |
| `\r` | 回车 | 光标移动到当前行开头（不是下一行） |
| `\\` | 反斜杠 | 打印反斜杠 |
| `\'` | 单引号 | 打印单引号 |
| `\"` | 双引号 | 打印双引号 |

以下示例展示了其中一些转义序列的效果。

### 示例 2-26

以下语句的输出：

```cpp
cout << "The newline escape sequence is \\n" << endl;
```

为：

```text
The newline escape sequence is \n
```

以下语句的输出：

```cpp
cout << "The tab character is represented as '\\t'" << endl;
```

为：

```text
The tab character is represented as '\t'
```

请注意，单引号也可以不使用转义序列来打印。因此，前面的语句等价于以下输出语句：

```cpp
cout << "The tab character is represented as '\\t'" << endl;
```

以下语句的输出：

```cpp
cout << "The string \"Sunny\" contains five characters." << endl;
```

为：

```text
The string "Sunny" contains five characters.
```

> **注意**  
> 本书配套网站包含一个 C++ 程序，用于展示示例 2-26 中各语句的效果。该程序名为 `Example2_26.cpp`。

要在程序中使用 `cin` 和 `cout`，必须包含某个头文件。下一节将解释这个头文件是什么、如何在程序中包含头文件，以及为什么程序中需要头文件。第 3 章将全面解释 `cin` 和 `cout`。

## 预处理指令

C++ 中显式定义的操作只有少数，例如算术运算和赋值运算。运行 C++ 程序所需的许多函数和符号以库的集合形式提供。每个库都有一个名称，并通过头文件来引用。例如，执行输入/输出（I/O）所需函数的描述包含在头文件 `iostream` 中。类似地，一些非常有用的数学函数（如幂、绝对值和正弦）的描述包含在头文件 `cmath` 中。如果你想使用 I/O 或数学函数，就需要告诉计算机在哪里找到必要的代码。你使用预处理指令和头文件名来告诉计算机库中提供的代码所在的位置。预处理指令由一个称为预处理器的程序处理。

预处理指令是提供给预处理器的命令，这些命令使预处理器在编译 C++ 程序之前修改其文本。所有预处理命令都以 `#` 开头。预处理命令末尾没有分号，因为它们不是 C++ 语句。要在 C++ 程序中使用头文件，请使用预处理指令 `include`。

在 C++ 程序中包含头文件（由 IDE 提供）的一般语法是：

```cpp
#include <headerFileName>
```

例如，以下语句在 C++ 程序中包含头文件 `iostream`：

```cpp
#include <iostream>
```

用于包含头文件的预处理指令放在程序的第一行，以便这些头文件中声明的标识符可以在整个程序中使用。（回顾一下，在 C++ 中，标识符必须先声明才能使用。）

C++ 要求提供某些头文件作为其组成部分。附录 F 描述了一些常用头文件。程序员个人也可以创建自己的头文件，本书后面的“类与数据抽象”一章将对此进行讨论。

请注意，预处理命令在程序经过编译器之前由预处理器处理。

从图 1-3（第 1 章）可以得出结论：C++ 系统有三个基本组成部分：程序开发环境、C++ 语言和 C++ 库。这三个组成部分都是 C++ 系统不可或缺的部分。程序开发环境由图 1-3 所示的六个步骤组成。在你通读本书学习 C++ 语言的过程中，我们将根据需要讨论 C++ 库的组成部分。

