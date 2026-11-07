

```cpp
    sum += input;
}
cout << "Last value entered = " << input << endl;
cout << "Sum = " << sum << endl;
cout << "Now enter a new number: ";
cin >> input;    // won't work
```

如果你希望程序在流状态位被设置后继续读取后续输入，就必须把流状态重置为良好状态。这可以通过调用 `clear()` 方法完成：

```cpp
while (cin >> input)
{
    sum += input;
}
cout << "Last value entered = " << input << endl;
cout << "Sum = " << sum << endl;
cout << "Now enter a new number: ";
cin.clear();          // reset stream state
while (!isspace(cin.get()))
    continue;         // get rid of bad input
cin >> input;         // will work now
```

注意，仅重置流状态还不够。导致输入循环终止的不匹配输入仍然留在输入队列中，程序必须越过它。一种方法是不断读取字符，直到遇到空白字符。`isspace()` 函数（见第 6 章“分支语句和逻辑运算符”）是一个 ctype 函数，如果其参数是空白字符，则返回 true。或者，你可以丢弃该行剩余内容，而不只是下一个单词：

```cpp
while (cin.get() != '\n')
    continue;         // get rid of rest of line
```

这个示例假设循环因不适当的输入而终止。相反，假设循环因文件结束或硬件故障而终止，那么处理坏输入的新代码就毫无意义。你可以使用 `fail()` 方法测试该假设是否正确，从而解决问题。由于历史原因，只要设置了 `failbit` 或 `eofbit`，`fail()` 就会返回 true，因此代码必须排除后一种情况。以下代码展示了这种排除的示例：

```cpp
if (cin.fail() && !cin.eof() )  // failed because of mismatched input
{
    cin.clear();      // reset stream state
    while (!isspace(cin.get()))
        continue;  // get rid of bad input
}
else // bail out
{
    cout << "I cannot go on!\n";
    exit(1);
}
cout << "Now enter a new number: ";
cin >> input;  // will work now
```

## 其他 iostream 类方法

第 3 章到第 5 章讨论了 `get()` 和 `getline()` 方法。你可能还记得，它们提供以下额外的输入能力：

- `get(char &)` 和 `get(void)` 方法提供不跳过空白字符的单字符输入。
- `get(char *, int, char)` 和 `getline(char *, int, char)` 函数默认读取整行，而不是单个单词。

这些函数被称为*无格式输入函数*，因为它们只是按原样读取字符输入，不跳过空白字符，也不执行数据转换。

下面我们来看这两组 iostream 类成员函数。

### 单字符输入

当带一个 char 参数或不带参数使用时，`get()` 方法会获取下一个输入字符，即使它是空格、制表符或换行字符。`get(char & ch)` 版本将输入字符赋给其参数，而 `get(void)` 版本将输入字符转换为整数类型（通常是 int）后作为返回值。

### get(char &) 成员函数

我们先试试 `get(char &)`。假设程序中有以下循环：

```cpp
int ct = 0;
char ch;
cin.get(ch);
while (ch != '\n')
{
    cout << ch;
    ct++;
    cin.get(ch);
}
cout << ct << endl;
```

接下来，假设你键入以下乐观输入：

```text
    1 C++ clearly.<Enter>
```

按下 Enter 键会把这行输入发送给程序。该程序片段读取字符 1，用 cout 显示它，并将 ct 递增到 1。接下来，它读取 1 后面的空格字符，显示它，并将 ct 递增到 2。如此继续，直到程序将 Enter 键处理为换行字符并终止循环。这里的要点是，通过使用 `get(ch)`，代码会读取、显示并统计空格以及可打印字符。

相反，假设程序尝试使用 `>>`：

```cpp
int ct = 0;
char ch;
cin >> ch;
while (ch != '\n')    // FAILS
{
    cout << ch;
    ct++;
    cin >> ch;
}
cout << ct << endl;
```

首先，代码会跳过空格，因此不会统计它们，并把相应输出压缩成下面这样：

```text
1C++clearly.
```

更糟的是，循环将永远不会终止！因为提取运算符会跳过换行符，代码永远不会把换行字符赋给 ch，所以 while 循环测试永远不会终止循环。

`get(char &)` 成员函数返回一个对调用它的 istream 对象的引用。这意味着你可以在 `get(char &)` 后面连接其他提取操作：

```cpp
char c1, c2, c3;
cin.get(c1).get(c2) >> c3;
```

首先，`cin.get(c1)` 将第一个输入字符赋给 c1，并返回调用对象，即 cin。这使代码化简为 `cin.get(c2) >> c3`，它把第二个输入字符赋给 c2。该函数调用返回 cin，使代码化简为 `cin >> c3`。这反过来会把下一个非空白字符赋给 c3。注意，c1 和 c2 最终可能被赋为空白字符，但 c3 不会。

如果 `cin.get(char &)` 遇到文件结尾（无论是真实的文件结尾，还是从键盘模拟的文件结尾：DOS 和 Windows 命令提示符模式下按 Ctrl+Z，Unix 下行首按 Ctrl+D），它不会给其参数赋值。这很正确，因为如果程序已到达文件末尾，就没有值可赋值。此外，该方法会调用 `setstate(failbit)`，这会使 cin 的测试结果为假：

```cpp
char ch;
while (cin.get(ch))
{
    // process input
}
```

只要有有效输入，`cin.get(ch)` 的返回值就是 `cin`，其求值为真，因此循环继续。到达文件结尾时，返回值求值为假，从而终止循环。

### get(void) 成员函数

`get(void)` 成员函数也会读取空白字符，但它使用返回值将输入传达给程序。因此你会这样使用它：

```cpp
int ct = 0;
char ch;
ch = cin.get();       // use return value
while (ch != '\n')
{
    cout << ch;
    ct++;
    ch = cin.get();
}
cout << ct << endl;
```

`get(void)` 成员函数返回 int 类型（或某种更大的整数类型，具体取决于字符集和区域设置）。这使得下面这样写无效：

```cpp
char c1, c2, c3;
cin.get().get() >> c3;  // not valid
```

这里 `cin.get()` 返回一个 int 类型的值。由于该返回值不是类对象，你不能对其应用成员运算符。因此会出现语法错误。不过，你可以在提取序列末尾使用 `get()`：

```cpp
char c1;
cin.get(c1).get();  // valid
```

`get(void)` 返回 int 类型这一事实意味着你不能在它后面接提取运算符。但由于 `cin.get(c1)` 返回 cin，这使它适合作为 `get()` 的前缀。这段特定代码会读取第一个输入字符，将其赋给 c1，然后读取第二个输入字符并将其丢弃。

到达文件结尾时（无论是真实还是模拟的），`cin.get(void)` 返回 `EOF` 值，这是 `iostream` 头文件提供的一个符号常量。这一设计特性允许使用以下结构来读取输入：

```cpp
int ch;
while ((ch = cin.get()) != EOF)
{
    // process input
}
```

这里你应该为 ch 使用 `int` 类型，而不是 `char` 类型，因为 `EOF` 值可能无法用 `char` 类型表示。

第 5 章“循环和关系表达式”更详细地描述了这些函数，表 17.5 总结了单字符输入函数的特性。

**表 17.5**  `cin.get(ch)` 与 `cin.get()` 对比

| 属性 | `cin.get(ch)` | `ch = cin.get()` |
| --- | --- | --- |
| 传递输入字符的方法 | 赋给参数 `ch` | 使用函数返回值赋给 `ch` |
| 字符输入时的函数返回值 | 对类 `istream` 对象的引用 | 字符编码，作为 `int` 类型的值 |
| 文件结束时的函数返回值 | 转换为 `false` | 文件结束时返回 `EOF` |

### 应使用哪种形式的单字符输入？

在 `>>`、`get(char &)` 和 `get(void)` 之间选择时，应该使用哪一种？首先，你需要决定是否希望输入跳过空白字符。如果跳过空白字符比较方便，就应该使用提取运算符 `>>`。例如，在提供菜单选项时，跳过空白字符很方便：

```cpp
cout << "a. annoy client        b. bill client\n"
     << "c. calm client        d. deceive client\n"
     << "q.\n";
cout << "Enter a, b, c, d, or q: ";
char ch;
cin >> ch;
while (ch != 'q')
{
    switch(ch)
    {
        ...
    }
    cout << "Enter a, b, c, d, or q: ";
    cin >> ch;
}
```

例如，要输入 `b` 响应，你键入 `b` 并按 Enter，生成两个字符的响应 `b\n`。如果使用任意一种形式的 `get()`，你就必须添加代码，在每个循环周期处理那个 `\n` 字符，而提取运算符会方便地跳过它。（如果你用 C 编过程，可能遇到过换行符在程序看来像无效响应的情况。这个问题容易修复，但很烦人。）

