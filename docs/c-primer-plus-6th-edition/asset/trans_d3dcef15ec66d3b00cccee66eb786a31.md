

# 使用 cin 输入 (1107)

输入。例如，下面的函数调用将读取并丢弃后续 255 个字符，或者遇到第一个换行符，以先者为准：

```
cin.ignore(255, '\n');
```

该函数的两个参数的默认值分别为 1 和 `EOF`，函数的返回类型为 `istream &`

```cpp
istream & ignore(int = 1, int = EOF);
```

（`EOF` 默认值会导致 `ignore` 读取指定的数量字符——直到文件结束，以先者为准）。该函数返回调用它的对象。这允许你像下面这样串联函数调用：

```
cin.ignore(255, '\n').ignore(255, '\n');
```

在这里，第一个 `ignore()` 方法读取并丢弃了一行，第二个调用读取或丢弃第二行。这两个函数共同读取了列表 17.13 内容。

# 列表 17.13 get_fun.cpp

```cpp
// get_fun.cpp
// 使用 get() 和 getline()
#include <iostream>
const int Limit = 255;

int main()
{
    using std::cout;
    using std::cin;
    using std::endl;

    char input[Limit];

    cout << "Enter a string for getline() processing:\n";
    cin.getline(input, Limit, '#');
    cout << "Here is your input:\n";
    cout << input << "\nDone with phase 1\n";

    char ch;
    cin.get(ch);
    cout << "The next input character is " << ch << endl;

    if (ch != '\n')
        cin.ignore(Limit, '\n'); // 丢弃行剩余部分

    cout << "Enter a string for get() processing:\n";
    cin.getline(input, Limit, '#');
    cout << "Here is your input:\n";
    cout << input << "\nDone with phase 2\n";

    cin.get(ch);

    cout << "The next input character is " << ch << endl;

    return 0;

}
```

这里是列表 17.13 中程序的示例运行结果。

Enter a string for getline() processing:
Please pass
me a #3 melon!:

Here is your input:
Please pass
me a

Done with phase 1

The next input character is 3

Enter a string for get() processing:
I still
want my #3 melon!

Here is your input:
I still
want my

Done with phase 2

The next input character is #

> 注意：`getline()` 函数丢弃了输入中的 `#` 终止字符，而 `get()` 函数则不会。

# 意外的字符串输入

`get(char *, int)` 和 `getline()` 的某些输入形式会影响流状态。与其他输入函数一样，遇到文件结束（end-of-file）会设置 `eofbit`，而任何损坏流的操作、设备故障或其他特殊情况会设置 `badbit`。另外两种特殊情况是无输入，以及输入达到或超过函数调用指定的最大字符数。让我们现在来看这些情况。

如果任一种方法未能提取到任何字符，该方法会在输入字符串中放入一个空字符（`null character`）并使用 `setState()` 设置 `failbit`。在什么情况下方法会无法提取任何字符呢？一种可能性是输入方法立即遇到文件结束。对于 `get(char *, int)`，另一种可能性是你输入了一个空行：

```cpp
char temp[80];
while (cin.get(temp,80)) // 在空行终止
```

# 使用 cin 输入 (1109)

有趣的是，空行不会导致 `getline()` 设置 `failbit`。这是因为即使 `getline()` 不存储换行符，它仍然会提取。如果你让 `getline()` 循环在空行终止，可以这样写：

```cpp
char temp[80];
while (cin.getline(temp, 80) && temp[0] != '\0') // 在空行终止
```

现在假设输入队列中的字符数超过了输入方法指定的最大值。首先考虑 `getline()` 和以下代码：

```cpp
char temp[30];
while (cin.getline(temp, 30))
```

`getline()` 将从输入队列读取连续字符，并将它们放入 `temp` 数组的连续元素中，直到（按测试顺序）遇到文件结束、要读取的下一个字符是换行符，或者存储了 29 个字符。如果设置了文件结束，则设置 `failbit`。如果下一个读取的字符是换行符，该字符将被读取并丢弃。如果读取了 29 个字符，除非下一个字符是换行符，否则设置 `failbit`。因此，30 个或更多字符的输入行将终止。

现在考虑 `get(char *, int)` 方法。它先检查字符数量，检查文件结束，最后检查下一个字符是否为换行符。如果读取了最大数量的字符，它不会设置 `failbit`。尽管如此，你可以使用 `peek`（下一节）查看下一个字符来判断输入方法是否提取了太多字符。如果是换行符，那么 `get()` 一定读取了整行。如果不是换行符，那么 `get()` 一定在到达结尾之前停止了。这种技术并不一定适用于 `getline()`，因为 `getline()` 会读取并丢弃换行符，即下一个字符。表 17.6 总结了这些行为。

表 17.6 输入

| 方法 | 行为 |
| :--- | :--- |
| getline(char *, int) | 如果没有读取到字符则设置 `failbit`（换行符除外） |
| get(char *, int) | 没有读取到字符则设置 `failbit` |

# 其他 istream 方法

我们目前讨论的其他 istream 方法包括 `peek()`、`count()` 和 `putback()`。`read()` 函数读取指定数量的字节并存储在指定的位置。例如，假设你使用 `cin.get(my, 80)` 读取一行到数组，并想知道读取了多少字符。你可以使用 `strlen()` 函数统计数组中的字符，但使用 `cin.count()` 报告从流中读取了多少字符会更快。

`count()` 方法返回上一次非格式提取方法读取的字符数。这意味着它是通过 `get()`、`getline()`、`ignore()` 或 `read()` 方法读取的，而不是通过格式化输入以适应特定类型的提取运算符 `>`。例如，假设你使用 `cin.get(my, 80)` 读取一行到数组，并想知道读取了多少字符。你可以使用 `strlen()` 函数统计数组中的字符，但使用 `cin.count()` 报告从流中读取了多少字符会更快。

