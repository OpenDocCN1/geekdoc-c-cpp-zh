

**注意**

当输出语句输出 `char` 值时，它只输出字符本身，而不输出单引号（除非单引号是输出语句的一部分）。

例如，假设 `ch` 是一个 `char` 变量，且 `ch = 'A';`。语句：

```cpp
cout << ch;
```

或

```cpp
cout << 'A';
```

输出：

```text
A
```

类似地，当输出语句输出字符串的值时，它只输出字符串本身，而不输出双引号（除非你将双引号作为输出的一部分）。

## 示例 2-21

考虑以下语句。每条语句右侧显示了输出。

| 语句 | 输出 |
|---|---|
| `cout << 29 / 4 << endl;` | `7` |
| `cout << "Hello there." << endl;` | `Hello there.` |
| `cout << 12 << endl;` | `12` |
| `cout << "4 + 7" << endl;` | `4 + 7` |
| `cout << 4 + 7 << endl;` | `11` |
| `cout << 'A' << endl;` | `A` |
| `cout << "4 + 7 = " << 4 + 7 << endl;` | `4 + 7 = 11` |
| `cout << 2 + 3 * 5 << endl;` | `17` |
| `cout << "Hello \nthere." << endl;` | `Hello<br>there.` |

看看第 9 条语句的输出。回想一下，在 C++ 中，换行字符是 `\n`；它会使插入点在打印之前移动到下一行的开头。因此，当 `\n` 出现在输出语句的字符串中时，它会使插入点在输出设备上移动到下一行的开头。这一事实解释了为什么 Hello 和 there. 会打印在不同行上。

**注意**

在 C++ 中，`\` 称为转义字符，`\n` 称为换行转义序列。

回想一下，所有变量都必须正确初始化；否则，存储在其中的值可能没有太大意义。还要记住，C++ 不会自动初始化变量。

如果 num 是一个 int 变量，那么以下 C++ 语句的输出：

```cpp
cout << num << endl;
```

是有意义的，前提是 num 已被赋值。例如，以下 C++ 语句序列：

```cpp
num = 45;
cout << num << endl;
```

将产生输出 45。

## 示例 2-22

考虑以下 C++ 程序：

```cpp
// This program illustrates how output statements work.

#include <iostream>

using namespace std;

int main()
{
    int a, b;

    a = 65;                    //Line 1
    b = 78;                    //Line 2

    cout << 29 / 4 << endl;    //Line 3
    cout << 3.0 / 2 << endl;   //Line 4
    cout << "Hello there.\n";  //Line 5
    cout << 7 << endl;         //Line 6
    cout << 3 + 5 << endl;     //Line 7
    cout << "3 + 5";           //Line 8
    cout << " **";             //Line 9
    cout << endl;              //Line 10
    cout << 2 + 3 * 6 << endl; //Line 11
    cout << "a" << endl;       //Line 12
    cout << a << endl;         //Line 13
    cout << b << endl;         //Line 14

    return 0;
}
```

在下面的输出中，标有“语句所在行”的列和行号不属于输出的一部分。此列中显示行号是为了便于看出哪个输出对应哪条语句。

| 输出 | 语句所在行 |
|---|---|
| 7 | 第 3 行 |
| 1.5 | 第 4 行 |
| Hello there. | 第 5 行 |
| 7 | 第 6 行 |
| 8 | 第 7 行 |
| 3 + 5 ** | 第 8 行和第 9 行 |
| 20 | 第 11 行 |
| a | 第 12 行 |
| 65 | 第 13 行 |
| 78 | 第 14 行 |

大部分情况下，输出很直接。看看第 7、8、9 和 10 行语句的输出。第 7 行的语句输出 3 + 5 的结果，即 8，并将插入点移动到下一行的开头。第 8 行的语句输出字符串 3 + 5。注意，第 8 行的语句仅由字符串 3 + 5 组成。因此，在打印 3 + 5 之后，插入点仍停留在 5 之后；它不会移动到下一行的开头。接下来，第 9 行语句的输出会在插入点（此前位于 5 之后）输出一个空格和 **。

第 10 行的输出语句只包含操纵符 endl，它将插入点移动到下一行的开头。因此，当第 11 行的语句执行时，输出从该行开头开始。注意，在此输出中，“语句所在行”列不包含第 10 行。这是因为第 10 行的语句不产生任何可打印输出。它只是将插入点移动到下一行的开头。接下来，第 11 行的语句输出 2 + 3 * 6 的值，即 20。然后，操纵符 endl 将插入点移动到下一行的开头。

**注意**

在表达式中输出或访问变量的值不会销毁或修改变量的内容。

现在让我们仔细看看换行字符 `'\n'`。考虑以下 C++ 语句：

```cpp
cout << "Hello there.";
cout << "My name is James.";
```

如果这些语句按顺序执行，则输出为：

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

当在字符串中遇到 `\n` 时，插入点会定位到下一行的开头。另请注意，`\n` 可以出现在字符串中的任何位置。例如，以下语句的输出：

```cpp
cout << "Hello \nthere. \nMy name is James.";
```

为：

```text
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

也与以下语句的输出相同：

```cpp
cout << endl;
```

因此，以下语句序列的输出：

```cpp
cout << "Hello there.\n";
cout << "My name is James.";
```

与以下语句序列的输出相同：

```cpp
cout << "Hello there." << endl;
cout << "My name is James.";
```

## 示例 2-23

考虑以下 C++ 语句：

```cpp
cout << "Hello there.\nMy name is James.";
```

或：

```cpp
cout << "Hello there.";
cout << "\nMy name is James.";
```

或：

```cpp
cout << "Hello there.";
cout << endl << "My name is James.";
```

在每种情况下，这些语句的输出都是：

```text
Hello there.
My name is James.
```

## 示例 2-24

以下 C++ 语句的输出：

```cpp
cout << "Count...\n....1\n......2\n......3";
```

或：

```cpp
cout << "Count..." << endl << ".....1" << endl
     << "......2" << endl << "......3";
```

为：

```text
Count...
.....1
......2
......3
```

## 示例 2-25

假设你想将以下句子作为消息的一部分在一行中输出：

今天阳光明媚、温暖，而且没有刮风。我们可以去打高尔夫球。

显然，你会使用一条输出语句来产生这个输出。然而，在编程代码中，作为输出语句的一部分，这条语句可能无法放在一行中。当然，你可以像下面这样使用多条输出语句：

```cpp
cout << "It is sunny, warm, and not a windy day. "
cout << "We can go golfing." << endl;
```

注意第一条语句末尾的分号，以及第二条语句开头的标识符 cout。另请注意，第一条语句末尾没有操纵符 endl。这里使用两条输出语句将句子输出在一行中。等价地，你可以使用以下输出语句来输出这个句子：

```cpp
cout << "It is sunny, warm, and not a windy day. "
     << "We can go golfing." << endl;
```

在这条语句中，请注意第一行末尾没有分号，并且标识符 cout 没有出现在第二行开头。由于第一行末尾没有分号，这条输出语句会在第二行继续。另请注意每一行句子开头和结尾的双引号。该字符串被分成两个字符串，但两个字符串都是同一条输出语句的一部分。

如果输出语句中出现的字符串很长，而你想将该字符串输出在一行中，你可以使用前面两种方法中的任意一种来拆分字符串。然而，以下语句是不正确的：

```cpp
cout << "It is sunny, warm, and not a windy day.
          We can go golfing." << endl;                 //illegal
```

换句话说，键盘上的 Return（或 Enter）键不能成为字符串的一部分。也就是说，在编程代码中，不能通过按键盘上的 Return（Enter）键将字符串分成多行。

回想一下，换行字符是 `\n`，它会使插入点移动到下一行的开头。C++ 中有许多转义序列，可让你控制输出。表 2-4 列出了一些常用的转义序列。

## 表 2-4  常用转义序列

|  | 转义序列 | 描述 |
|---|---|---|
| `\n` | 换行符 | 光标移动到下一行的开头 |
| `\t` | 制表符 | 光标移动到下一个制表位 |
| `\b` | 退格 | 光标向左移动一个空格 |
| `\r` | 回车 | 光标移动到当前行的开头（不是下一行） |
| `\\` | 反斜杠 | 打印反斜杠 |
| `\'` | 单引号 | 打印单引号 |
| `\"` | 双引号 | 打印双引号 |

以下示例展示了其中一些转义序列的效果。

## 示例 2-26

以下语句的输出：

```cpp
cout << "The newline escape sequence is \\n" << endl;
```

为：

```text
The newline escape sequence is \n
```

