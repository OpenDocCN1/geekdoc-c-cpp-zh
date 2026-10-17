
`(void)` 成员函数也读取空白字符，但它使用其返回值向程序通信。因此，你会这样使用它：

```cpp
int ct = 0;
char ch;
ch = cin.get();      // use return value
while (ch != '\n')
{
    cout << ch;
    ct++;
    ch = cin.get();
}
```

`cout << ct << endl;`

`(void)` 成员函数的返回类型为 `int`（或某种更大的整数整数类型，取决于字符集和本地区域）。这使得以下操作无效：

```cpp
char c1, c2, c3;
cin.get().get() >> c3;  // not valid
```

在此处 `cin.get()` 返回一个 `int` 值。由于返回值不是一个类对象，你不能对其应用成员运算符。因此，你会得到一个语法错误。然而，你可以在提取序列的末尾使用 `cin.get()`：

```cpp
char c1;
cin.get(c1).get();    // valid
```

`(void)` 返回类型为 `int` 意味着你不能在它后面跟随提取运算符。但因为 `cin.get(c1)` 返回 `cin`，它成为了 `get()` 合适的前缀。这段代码将返回第一个输入字符，将其赋值给 `c1`，然后返回第二个输入字符并将其丢弃。

到达真实的或模拟的文件结束时，`cin.get(void)` 返回值 `EOF`，这是由 `iostream` 头文件提供的符号常量。这种设计特性允许使用如下构造读取输入：

```cpp
int ch;
while ((ch = cin.get()) != EOF)
{
```

## 使用 cin 输入

```cpp
// process input
}
```

你应该使用 `int` 类型而不是 `char`，因为该值可能无法被表示。第 5 章“循环”更详细地描述了这些函数。

### 表格：get(ch) vs get()

| 属性 | `get(ch)` | `get()` |
| :--- | :--- | :--- |
| 输入类型 | `char &` | `int` |
| 返回值 | `cin` (对象) | `int` |
| 跳过空白 | 否 | 否 |
| 文件结束 | 设置 `failbit` | 返回 `EOF` |

## 你应该使用哪形式的 get()？

鉴于 `get(char &)` 和 `get(void)` 这两种方法，你应该用哪一个？如果你想跳过空白，应该使用 `(void)` 版本。例如：

```cpp
char ch;
cin.get(ch);
while (ch != '\n')
{
    // process input
}
```

如果你想包含换行符，应该使用 `(char &)` 版本。例如：

```cpp
char ch;
cin.get(ch);
while (ch != '\n')
{
    // process input
}
```

`get(char &)` 和 `get()` 的区别在于 `get(char &)` 将换行符留在输入流中，影响下一次输入操作的第一个字符，而 `get()` 则不会。

## 字符串输入：getline(), get() 和 ignore()

接下来，让我们回顾在第 4 章“自定义类型”中介绍的 `getline()` 成员函数。`getline()` 成员函数和读取字符串的 `get()` 版本，字符串具有相同的签名（从通用模板声明简化）：

```cpp
istream & get(char *, char);
istream & get(char *, int);
istream & getline(char *, int, char);
istream & getline(char *, int);
```

第一个参数（回顾）是放置输入字符串的位置。第二个参数是最大读取字符数加一。第三个参数指定一个字符作为输入的分隔符。仅带参数的版本使用换行符作为分隔符。

```cpp
char line[50];
cin.get(line, 50);
```

`cin.get()` 函数在遇到 49 个字符或遇到换行符（以先到者为准）后读取输入到数组中。`get()` 和 `getline()` 的区别在于 `get()` 将换行符留在输入流中，影响下一次操作，而 `getline()` 则不会。

列表 17.13 展示了 `getline()` 和 `get()` 如何工作。它还引入了 `ignore()` 成员函数。`ignore()` 接受两个参数：指定最大读取字符数的数字和一个作为输入分隔符的字符。

### 使用 cin 输入 (1107)

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

### 列表 17.13 get_fun.cpp

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

## 意外的字符串输入

`get(char *, int)` 和 `getline()` 的某些输入形式会影响流状态。与其他输入函数一样，遇到文件结束（end-of-file）会设置 `eofbit`，而任何损坏流的操作、设备故障或其他特殊情况会设置 `badbit`。另外两种特殊情况是无输入，以及输入达到或超过函数调用指定的最大字符数。让我们现在来看这些情况。

如果任一种方法未能提取到任何字符，该方法会在输入字符串中放入一个空字符（`null character`）并使用 `setState()` 设置 `failbit`。在什么情况下方法会无法提取任何字符呢？一种可能性是输入方法立即遇到文件结束。对于 `get(char *, int)`，另一种可能性是你输入了一个空行：

```cpp
char temp[80];
while (cin.get(temp,80)) // 在空行终止
```

### 使用 cin 输入 (1109)

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

### 表 17.6 输入

| 方法 | 行为 |
| :--- | :--- |
| `getline(char *, int)` | 如果没有读取到字符则设置 `failbit`（换行符除外） |
| `get(char *, int)` | 没有读取到字符则设置 `failbit` |

## 其他 istream 方法

我们目前讨论的其他 istream 方法包括 `peek()`、`count()` 和 `putback()`。`read()` 函数读取指定数量的字节并存储在指定的位置。例如，假设你使用 `cin.get(my, 80)` 读取一行到数组，并想知道读取了多少字符。你可以使用 `strlen()` 函数统计数组中的字符，但使用 `cin.count()` 报告从流中读取了多少字符会更快。

`count()` 方法返回上一次非格式提取方法读取的字符数。这意味着它是通过 `get()`、`getline()`、`ignore()` 或 `read()` 方法读取的，而不是通过格式化输入以适应特定类型的提取运算符 `>`。例如，假设你使用 `cin.get(my, 80)` 读取一行到数组，并想知道读取了多少字符。你可以使用 `strlen()` 函数统计数组中的字符，但使用 `cin.count()` 报告从流中读取了多少字符会更快。

列表 17.14 使用两种方法来读取并回显输入，直到但不包含 # 字符。第一种方法读取通过 # 字符，然后使用 `putback()` 将该字符重新插入输入流。第二种方法使用 `peek()` 进行前瞻。

### 列表 17.14 peeker.cpp

```cpp
// peeker.cpp -- some istream methods
#include <iostream>

int main()
{
    using std::cout;
    using std::cin;
    using std::endl;

    // 读取并回显输入直到 # 字符
    char ch;

    while (cin.get(ch)) // 在 EOF 时终止
    {
        if (ch != '#')
            cout << ch;
        else
        {
            cin.putback(ch); // 重新插入字符
            break;
        }
    }

    if (!cin.eof())
    {
        cin.get(ch);
        cout << endl << ch << " is next input character.\n";
    }
    else
    {
        cout << "End of file reached.\n";
        std::exit(0);
    }

    while (cin.peek() != '#') // 前瞻
    {
        cin.get(ch);
        cout << ch;
    }
    if (!cin.eof())
    {
        cin.get(ch);
        cout << endl << ch << " is next input character.\n";
    } else
        cout << "End of file reached.\n";

    return 0;
}
```

这里是列表 17.14 中程序的运行示例。

我用了一个 #3 号铅笔，但我本该用 #2 号的。

我用了一个

# is next input character.

3 号铅笔，但我本该用一个

# is next input character.

## 程序说明

让我们更仔细地观察一下列表 17.14 中的一些代码。第一种方法使用 while 循环读取输入：

```cpp
while(cin.get(ch)) // 在 EOF 时终止

if (ch != '#')
    cout << ch;
else
{
    cin.putback(ch); // 重新插入字符
    break;
}
```

表达式 `cin.get(ch)` 在达到文件末尾条件时返回 `false`，从键盘模拟文件末尾会终止循环。如果 # 字符首先出现，程序会将该字符放入输入流并使用 `break` 语句终止循环。

第二种方法在外观上更简单：

```cpp
while(cin.peek() != '#') // 前瞻
{
    cin.get(ch);
    cout << ch;
}
```

### 使用 cin 的输入 1113

程序前瞻下一个字符。如果它不是 # 字符，程序读取下一个字符，回显它，然后前瞻下一个字符。这个过程一直持续到终止字符出现。

现在让我们正如所承诺的，来看一个示例——列表 17.15——它使用 `peek()` 来判断整行是否已经读取。如果只有行的一部分能放入输入数组，程序将丢弃该行的剩余部分。

### 列表 17.15 truncate.cpp

```cpp
// truncate.cpp -- 如果需要使用 get() 截断输入行
#include <iostream>
const int SLEN = 10;
inline void eatline() { while (std::cin.get() != '\n') continue; }
int main() {
    std::cin;
    std::cout;
    std::endl;

    char name[SLEN];
    char title[SLEN];
    cout << "Enter your name: ";
    cin.get(name,SLEN);
    if (cin.peek() != '\n')
        cout << "Sorry, we only have enough room for \n"
        << name << endl;

    eatline();
    cout << "Dear " << name << endl;
}
```

这里是列表 17.15 中程序的运行示例：

Enter your name: Ella Fishniffer

Sorry, we only have enough room for Ella Fish

Dear Ella Fish, enter your title:

Executive Adjunct

We were forced to truncate your title.

Name: Ella Fish

Title: Executive

注意无论第一个输入语句是否读取了整行，以下代码都有意义：

```cpp
while (cin.get() != '\n') continue;
```
