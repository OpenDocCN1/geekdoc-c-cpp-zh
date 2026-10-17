
在此示例中，正则表达式 `\W+` 匹配非单词字符，参数 `-1` 迭代器返回匹配项之间的序列（单词）。

# 594 | 第 18 章 字符串本地化与正则表达式

此示例中的每个单词。`regex_iterator` 遍历所有匹配项。通过对 `regex_iterator` 进行解引用，你可以得到一个匹配对象。通过访问此 `smatch` 对象的第一个元素 `[0]`，可以得到子字符串：

```cpp
regex reg("(\\w+)");

while (true) {
    cout << "Enter a string to split (q=quit): ";
    string str;
    if (getline(cin, str) || str == "q")
        break;
    const regex_iterator end;
    for (regex_iterator iter(cbegin(str), cend(str), reg); iter != end; ++iter) {
        cout << "*" << (*iter)[0] << "*" << endl;
    }
}
```

该程序的输出可能如下：

Enter a string to split (q=quit): This, is a test.
"This"
"is"
"a"
"test"

如此示例所示，即使是简单的正则表达式也能完成一些强大的字符串操作。

## regex_token_iterator

上一节描述了 `regex_iterator`，它遍历每个匹配的模式。在循环的每次迭代中，你会得到一个 `match_results` 对象，可以使用它来提取由捕获组捕获的子表达式。

`regex_token_iterator` 可用于遍历或选择所有匹配模式中的捕获组。它有四种格式的构造函数：

```cpp
regex_token_iterator(BidirectionalIterator a,
BidirectionalIterator b,
const regex_type& re,
[SubMatches matches, Flags]);
```

所有构造函数都需要一个开始和一个结束迭代器作为输入，以及正则表达式。可选的 `SubMatches` 参数用于指定应该遍历哪些捕获组。

- 单个整数，表示你想遍历的捕获组索引。
- 包含整数的向量，表示你想遍历的捕获组索引。
- 带有捕获组索引的 `initializer_list`。
- 带有捕获组索引的 C 风格数组。

当你省略 `SubMatches` 或将 `SubMatches` 指定为 0 时，你将获得一个遍历所有索引为 0 的捕获组的迭代器，这些是匹配完整正则表达式的子字符串。可选的 `Flags` 参数指定了匹配算法的选项。在大多数情况下，你可以保持默认值。更多细节请参阅标准库参考。

## regex_token_iterator 示例

之前的 `regex_iterator` 示例可以使用如下的 `regex_token_iterator` 重写。注意，在循环体中使用 `(*iter) [0]` 作为 `regex_token_iterator` 示例，是因为以 0 作为默认子匹配项的 token 迭代器会自动遍历索引为 0 的所有捕获组。该代码的输出与 `regex_iterator` 生成的输出完全一致：

```cpp
regex reg("\\w+");

while (true) {
    cout << "Enter a string to split (q=quit): ";
    string str;
    if (!getline(cin, str) || str == "q")
        break;
    const regex_token_iterator end;
    for (regex_token_iterator iter(cbegin(str), cend(str), reg); iter != end; ++iter)
        cout << "\"" << *iter << "\"" << endl;
}
```

接下来的示例要求用户输入日期，然后使用 `regex_token_iterator` 遍历第二和第三捕获组（月份和日期），它们被指定为一个整数向量。用于日期的正则表达式在本章前面已经解释过。唯一的区别是添加了 `^` 和锚点，这并不是必要的，因为该示例使用了 `regex_match()`。

```cpp
regex reg("\\d{4}/([0-9]|1[0-2])/([0-9]|1[0-9]|3[0-1]))");

while (true) {
    cout << "Enter a date (year/month/day) (q=quit): ";
    string str;
    if (!getline(cin, str) || str == "q")
        break;
    vector<int> indices{ 2, 3 };
    const regex_token_iterator end;
    for (regex_token_iterator iter(cbegin(str), cend(str), reg, indices); iter != end; ++iter)
        cout << "\"" << *iter << "\"" << endl;
}
```

此代码打印月份和日期值。该示例生成的输出如下：

```
Enter a date (year/month/day) (q=quit): 2011/1/13
"1"
"13"
Enter a date (year/month/day) (q=quit): 2011/11/32
Enter a date (year/month/day) (q=quit): 2011/12/5
"12"
"5"
```

`regex_token_iterator` 还可以用于执行字段分割或分词（tokenization）。它是使用 C 语言旧的 `strtok()` 函数更安全、更灵活的替代方案。通过 `regex_token_iterator` 构造函数指定遍历组索引为 -1 来触发分词。在分词模式下，迭代器遍历输入序列中不匹配正则表达式的所有子字符串。以下代码通过对逗号 `,` 和任意数量的空白字符进行字符串分词来演示：

```cpp
regex reg(",");

while (true) {
    cout << "Enter a string to split (q=quit): ";
    string str;
    if (!getline(cin, str) || str == "q")
        break;
    const regex_token_iterator end;
    for (regex_token_iterator iter(cbegin(str), cend(str), reg, -1); iter != end; ++iter)
        cout << "\"" << *iter << "\"" << endl;
}
```

以下代码演示了 `regex_replace()` 的用法：

```cpp
const string str("<h1></h1><p>Some text</p></body>");
regex r("<h1>(.*?)</h1><p>(.*?)</p>");
const string format("$1 and P=$2");
const string result = regex_replace(str, r, format);
cout << "Original string: " << str << "" << endl;
cout << "New string: " << result << "" << endl;
```

该程序的输出如下：

Original string: <h1></h1><p>Some text</p></body>
New string: <body>Header and P=Some text</body>

`regex_replace()` 算法接受多个标志，用于修改其工作方式。最重要的标志见下表：

| 标志 | 描述 |
| --- | --- |
| format_default | 默认替换所有匹配模式的项，并将所有不匹配模式的内容复制到结果字符串中。 |
| format_no_copy | 替换所有匹配模式的项，但不将不匹配模式的内容复制到结果字符串中。 |
| format_first_only | 仅替换第一次出现的模式项。 |

以下示例修改了代码以使用 `format_no_copy` 标志：

```cpp
const string str("<h1></h1><p>Some text</p></body>");
regex r("<h1>(.*?)</h1><p>(.*?)</p>");
const string format("$1 and P=$2");
string result = regex_replace(str, r, format,
      regex_constants::format_no_copy);
cout << "Original string: " << str << "" << endl;
cout << "New string: " << result << "" << endl;
```

输出与上一个的结果所示：

Original string: <h1></h1><p>Some text</p></body>
New string: Header and P=Some text

另一个示例是拆分输入字符串并将每个单词替换为换行符，使目标字符串每行仅一个单词。以下演示了如何在不使用任何循环处理字符串的情况下实现。第一个代码创建一个匹配单个单词的正则表达式。当找到匹配项时，它会被替换为 `$1n`，其中 `$1` 被替换为匹配到的单词。还要注意使用 `format_no_copy` 标志，以防止将源字符串中的空格和其他非单词字符复制到结果字符串：

```cpp
regex reg("(\\w+)");
const string format("$1\n");

while (true) {
  cout << "Enter a string to split over multiple lines (q=quit): *";
  string str;
  if (!getline(cin, str) || str == "q")
    break;
  cout << regex_replace(str, reg, format,
        regex_constants::format_no_copy) << endl;
}
```

该程序的输出如下：

Enter a string to split over multiple lines (q=quit): This is a test.
This
is
a
test

## 总结

本章让你体会了在考虑本地化时进行编码的意义。正如任何经历过本地化工作的人所说的那样，如果你提前做了计划，添加对新语言或区域的支持将容易得多；例如，使用 Unicode 字符并注意区域设置。

本章的第二部分解释了正则表达式库。一旦你熟悉了正则表达式的语法，处理字符串就会变得简单得多。正则表达式允许你验证字符串、在输入序列中搜索子字符串、执行查找和替换操作等。强烈建议你了解它们并开始使用它们，而不是编写自己的字符串处理程序。它们会让你的生活变得更轻松。

# 19 额外的库实用程序

本章包含内容？

- 如何使用 `std::function` 作为函数指针
- 如何处理编译时有分数
- 如何处理时间
- 如何生成随机数
- 什么是元（tuples）以及如何使用它们

WROX.COM 本章下载
请注意，本章的所有代码示例都可以作为本章代码，在书籍网站 www.wrox.com/go/proc+3e 的 "Download Code"（下载代码）选项卡中下载。

本章讨论了 C++ 标准库中可用的一些额外库功能，这些功能并不直接适用于其他章节。

# std::function

`std::function` 定义在 `<functional>` 头文件中，可以用于创建一个指向函数、函数对象或 lambda 表达式的类型；基本上，任何可调用对象都可以。它被称为多态函数包装器。它可以用作函数指针或作为函数的参数以实现回调。`std::function` 模板的模板参数看起来与大多数模板参数略有不同。其语法如下：

```cpp
std::function<R(ArgTypes...)>
```

R 是函数的返回值，ArgTypes 是函数参数类型的逗号分隔列表。

以下示例演示了如何使用 `std::function` 实现函数指针。它创建了一个指向函数 `func()` 的函数指针 `f1`。一旦定义了 `f1`，你就可以使用 `func` 或 `f1` 调用函数：

```cpp
void func(int num, const string& str)
{
    cout << num << ": " << str << endl;
}
int main() {
    std::function<void(int, const string&)> f1 = func;
    f1(42, "hello");
    return 0;
}
```

请记住 `ratio` 是一个编译时常量，这意味着分子和分母需要在编译时就已经确定。以下代码将产生编译器错误：

```cpp
intmax_t n = 1;
intmax_t d = 60;
ratio<n, d> r1;    // Error
```

将 `n` 和 `d` 设为常量可以消除错误：

```cpp
const intmax_t n = 1;
const intmax_t d = 60;
typedef ratio<n, d> r1;    // Ok
```

有理数总是归一化的。对于有理 `ratio<n, d>`，会计算最大公约数 `gcd`，分子 `num` 和分母 `den` 定义如下：

- num = sign(n)*sign(d)*abs(n)/gcd
- den = abs(d)/gcd

该库支持有理数的加、减、除。由于这些操作也是在编译时完成的，因此你不能使用标准的算术运算符。相反，你需要结合 `typedef` 使用特定的模板。以下是算术模板：`ratio_add`、`ratio_subtract`、`ratio_multiply` 和 `ratio_divide`。这些模板将结果计算为一个新的 `ratio` 类型。可以通过嵌入的 `typedef` 类型来访问它。以下代码定义了两个比例，分别代表 1/60 和 1/30。`ratio_add` 模板将这两个数字相加产生结果有理数，即 1/20：

```cpp
typedef ratio<1, 60> r1;
typedef ratio<1, 30> r2;
typedef ratio_add<r1, r2> r3; // type result;
```

标准库还定义了若干比较模板：`ratio_equal`、`ratio_less_equal`、`ratio_greater` 和 `ratio_greater_equal`。与算术模板一样，`ratio` 比较模板全在编译时求值。这些比较模板创建了一个新类型 `integral_constant`：一个持有值和编译时常量值的结构体。例如，`integral_constant<bool> true` 存储一个布尔真，而 `integral_constant<int>` 存储一个值为 15 的整数。比例比较模板的结果是 `integral_constant<bool> true` 或 `integral_constant<bool> false`。与 `integral_constant` 关联的值可以通过 `value` 数据成员访问。以下示例演示了 `ratio_less` 的用法。第 12 章讨论了使用 `boolalpha` 输出布尔值的 true 或 false：

```cpp
typedef ratio<1, 60> r1;
typedef ratio<1, 30> r2;
typedef ratio_add<r1, r2> r1 res;
cout << boolalpha << res::value << endl;
```

以下示例结合了所有内容。注意，由于 `ratio` 是编译时常量，你不能执行像 `cout << ri` 这样的操作，你需要获取分子和分母并打印它们：

```cpp
// 定义一个编译时有理数
typedef ratio<1
```

输出应当如下：

- 1) 1/60
- 2) 1/60
- 3) 1/30
- 4) 1/20
- 5) false

为了方便起见，该库提供了若干 SI（国际单位制）`typedef` 定义。它们如下：

```cpp
typedef ratio<1, 10000000000000000000000> yocto; // *
typedef ratio<1, 100000000000000000000> zepto; // *
typedef ratio<1, 10000000000000000000> ato;
typedef ratio<1, 10000000000000000000> femto;
typedef ratio<1, 100000000000000000000> pico;
typedef ratio<1, 100000000000000000> nano;
typedef ratio<1, 10000000000000> micro;
typedef ratio<1, 1000> milli;
```
