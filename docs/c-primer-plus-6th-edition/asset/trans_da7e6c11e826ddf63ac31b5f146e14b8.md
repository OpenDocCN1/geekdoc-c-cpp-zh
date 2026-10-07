

```cpp
cin.clear(); // reset stream state
while (!isspace(cin.get()))
    continue; // get rid of bad input
}
else // bail out
{
    cout << "I cannot go on!\n";
    exit(1);
}
cout << "Now enter a new number: ";
cin >> input; // will work now
```

# 其他 istream 类方法

第 3 到 5 章讨论了 `get()` 和 `getline()` 方法。如你可能还记得，它们提供了以下额外的输入功能：

- `get(char &)` 和 `get(void)` 方法提供单字符输入，且不会跳过空白。
- `get(char *, int, char)` 和 `getline(char *, int, char)` 函数默认读取整行而不是单个单词。

这些是非格式化输入函数，因为它们简单地按原样读取字符，不会跳过空白字符，也不会进行数据转换。
让我们来看这两组 istream 类成员函数。

## 单字符输入

当与 `char` 参数或不带参数使用时，`get()` 方法会获取下一个输入字符，即使它是空格、制表符或换行符。`get(char & ch)` 版本将其输入字符赋值给其参数，而 `get(void)` 版本将输入字符转换为整数（通常是 `int`）作为其返回值。

## get(char &) 成员函数

让我们先尝试 `get(char &)`。假设你的程序中有如下循环：

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
```

cout << ct << endl;
```

如果 `cin.get(char &)` 遇到文件结束（无论是真实的还是从键盘模拟的，DOS 和 Windows 命令行提示符使用 Ctrl+Z ，Unix 在行首使用 Ctrl+D ），它不会给其参数赋值。如果程序已经到达文件末尾，没有值可供赋值，这是正确的。此外，该方法调用了 `setstate(failbit)`，导致 `cin` 测试为 `false`：

```cpp
char ch;
while (cin.get(ch))
{
    // process input
}
```

只要有有效输入，`cin.get(ch)` 的返回值就是 `cin`，其评估为 `true`，循环继续。当到达文件结束时，返回值评估为 `false`，循环终止。

## getchar() 成员函数

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

cout << ct << endl;

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

## 表格：get(ch) vs get()

| 属性 | get(ch) | get() |
| :--- | :--- | :--- |
| 输入类型 | char & | int |
| 返回值 | cin (对象) | int |
| 跳过空白 | 否 | 否 |
| 文件结束 | 设置 failbit | 返回 EOF |

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

