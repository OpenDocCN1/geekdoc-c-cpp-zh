

# EOF 结束输入

记住当 `cin` 方法检测到 EOF（文件结束）时，它会在 `cin` 对象中设置一个标志，指示 EOF 条件。当此标志被设置时，`cin` 将不再读取任何输入，对 `cin` 的进一步调用将没有任何影响。对于文件输入，这是合理的，因为你确实想这样做。然而，对于键盘输入，你可能使用模拟的 EOF 来终止循环，稍后再读取更多输入。`cin.clear()` 方法可以清除 EOF 标志并允许输入继续。第 17 章“输入、输出与文件”将进一步讨论此。但是，请记住，在某些系统中，Ctrl+Z 有效地终止了输入和输出，其能力超出了 `cin.clear()` 恢复它们的范畴。

# 字符输入的常用习语

以下是每次读取一个文本字符直到 EOF 的循环的基本设计：

```
cin.get(ch); // 尝试读取一个字符
while (cin.fail() == false) // 测试是否为 EOF
{
    // 执行某些操作
    cin.get(ch); // 尝试读取另一个字符
}
```

这段代码你可以采用一些快捷方式。第 6 章引入了运算符，它可以在 true 和 false 之间进行切换。你可以将 `while` 循环重写成像这样：

```
while (!cin.fail()) // 只要输入未失败
```

`cin.get(char)` 方法的返回值是 `cin`，这是一个对象。然而，`istream` 类提供了一个函数，可以将 `cin` 等 `istream` 对象转换为 `bool` 值；当 `cin` 出现在需要 `bool` 值的循环中时，就会调用此转换函数，例如在 `while` 循环的测试条件中。此外，如果上一次尝试读取成功，则转换后的 `bool` 值为 `true`，否则为 `false`。这意味着你可以像下面这样重写 `while` 循环：

```
while (cin) // 只要输入成功
```

这比使用 `cin.fail()` 或 `!cin.eof()` 更通用，因为它还能检测其他可能的失败原因，例如磁盘故障。

最后，由于 `cin.get(char)` 的返回值是 `cin`，你可以将循环压缩为这种格式：

```
while (cin.get(ch)) // 只要输入成功
{
    // 执行某些操作
}
```

在这里，`cin.get(char)` 在测试条件的缩进中被调用两次——一次在循环之前，一次在循环结束。为了评估循环测试，程序

# 循环与文本输入

首先必须执行 `cin.get(ch)` 的调用，如果成功，它会将一个值放入 `ch`。然后程序获取函数调用的返回值，即 `cin`。接着它对 `cin` 应用 `bool` 转换，如果输入正常则产生 `true`，否则产生 `false`。这三条准则（识别终止条件、初始化条件和更新条件）都被压缩到了一个循环测试条件中。

### cin.get() 的另一个版本

怀旧的 C 用户可能渴望 C 语言 I/O 函数 `getchar()` 和 `putchar()`。如果你愿意，它们在 C++ 中也可用。你可以像在 C 中一样使用 `stdio.h` 头文件（或更现代的 `cstdio`）。你可以使用 `istream` 和 `ostream` 类中的成员函数，它们的工作方式相同。让我们看看那种方法。

不带参数的 `cin.get()` 成员函数返回输入中的下一个字符。也就是说，这样使用它：

```
ch = cin.get();
```

（记住 `cin.get(ch)` 返回的是一个对象，而不是读取的字符。）此函数的工作方式与 C 的 `getchar()` 非常相似，返回类型为 `int` 的字符代码。同样，你可以使用 `cout.put()` 函数（见第 3 章“处理数据”）来显示字符：

```
cout.put(ch);
```

它的工作方式与 C 的 `putchar()` 类似，只是它的参数应该是 `char` 类型而不是 `int` 类型。

注意

最初，`put()` 成员只有一个单一原型 `put(char)`。你可以向它传递一个 `int` 参数，然后它会被类型转换为 `char`。标准要求使用单一原型；然而，某些 C++ 实现提供了：`put(char)`、`put(signed char)` 和 `put(unsigned char)`。在这些实现中，使用带有 `int` 参数的 `put()` 会产生错误信息，因为转换 `int` 有多个选择。一个显式类型，如 `cin.put(char(ch))`，对 `int` 类型是有效的。

要成功使用 `cin.get()`，你需要知道如何处理 EOF 条件。当函数返回 EOF 时，没有更多的字符可以返回了。`cin.get()` 返回一个特殊值，由符号常量 `EOF` 表示。该常量定义在 `istream` 头文件中。EOF 值必须与任何有效字符值不同，以便程序不会将 EOF 与普通字符混淆。通常，EOF 被定义为值 -1，没有任何字符的 ASCII 码为 -1，但你不需要知道它的实际值。你可以在程序中使用 `EOF`。例如，列表 5.18 的核心部分看起来所示：

# 第 5 章 循环与关系表达式

```
char ch;
cin.get(ch);
while (cin.fail() == false) // 测试是否为 EOF
{
    cout << ch;
    ++count;
    cin.get(ch);
}
```

你可以使用 `int ch`，将 `cin.get(char)` 替换为 `cin.get()`，将 `cout` 替换为 `cout.put()`，并将 `cin.fail()` 测试替换为 EOF 测试：

```cpp
int ch;
// 为了兼容 EOF 值
while (ch != EOF)
{
    cout.put(ch); // 对于某些实现使用 cout.put(char(ch))
    ++count;
    ch = cin.get();
}
```

注意

某些系统不支持模拟的 EOF，或者支持得不完美，可能会导致列表 5.19 中的示例无法运行。如果你使用 `cin.get()` 来冻结屏幕，在这里将不起作用，因为检测 EOF 在尝试读取后关闭了。然而，你可以使用列表 5.14 那样的循环来清除屏幕。或者你可以使用 `cin.get()` 重置输入流。

这是列表 5.19 的运行情况：

+   The sullen mackerel sulks in the shadowy shall.<ENTER>
The sullen mackerel sulks in the shadowy shall.
Yes, but the bird of happiness harbors secrets.<ENTER>
Yes, but the bird of happiness harbors secrets.
<CTRL+Z><ENTER>
10 characters read

让我们分析条件：

while (ch = cin.get()) != EOF

`!` 的优先级高于 `=`，但这里是 `ch = cin.get()`，所以首先将 `cin.get()` 的返回值与 EOF 比较。` != EOF` 比较产生一个假或真的结果；该布尔值转换为 0 或 1，这就是赋值给 `ch` 的值。

如果你漏掉了一些括号：

while (ch = cin.get()) != EOF

括号包裹了子表达式 `ch = cin.get()`，导致程序评估该表达式。为了进行评估，程序首先必须调用 `cin.get()` 函数。接下来，它将返回值赋值给 `ch`。由于赋值语句的值是左操作数的值，子表达式减少了 `ch` 的值。如果这个值是 EOF，循环终止；否则继续。测试条件需要所有的括号。

另一方面，使用 `cin.get(ch)`（带参数）进行输入不会产生任何类型问题。记住，`cin.get(char)` 函数在 EOF 处不会为 `ch` 赋值特殊值。事实上，在这种情况下，`ch` 永远不会被用来持有非字符值。表 5.3 总结了 `cin.get(char)` 和 `cin.get()` 之间的区别。

