
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

以下情况呢？
```
int y;
y = 1,024;
```

- `cin>>ch` 与 `cin.get(ch)` 以及 `ch=cin.get()` 在查看输入方面有什么不同？

（注：原文后续重复的 Daphne/Cleo 题目已根据指令要求去重，不再重复翻译。）

# 分支语句与逻辑运算符

在本章中，你将学习以下内容：

- `if` 语句
- `if else` 语句
- 逻辑运算符：`&&`、`||` 和 `!`
- `cctype` 库字符函数
- 条件运算符：`?:`
- `switch` 语句
- `continue` 和 `break` 语句
- 数字读取循环
- 基本文件输入输出

设计智能程序的关键在于赋予其决策的能力。第五章“循环与关系表达式”展示了一种决策类型——即程序决定是否继续循环。本章研究了 C++ 如何使用分支语句在替代方案之间做出决策。应该使用哪种吸血鬼防护方案（大蒜还是十字）？选择了哪个菜单？用户是否输入了零？`if` 和 `switch` 语句用于实现决策是本章的主题。本章还将介绍条件运算符（它提供了另一种选择方式）以及逻辑运算符（它们允许将两个测试合并为一个）。最后，本章将首次介绍文件输入输出。

# 第 6 章 分支语句与逻辑运算符

## if 语句

当 C++ 程序必须选择是否执行特定操作时，你通常使用 `if` 来实现这种选择。`if` 有两种形式：if 和 `if else`。让我们研究简单的 `if`。它模仿普通的英语，例如“如果你有钱，你就得到饼干。”`if` 语句引导程序在测试条件为真时执行语句或块，在条件为假时跳过语句块。因此，`if` 语句让程序决定是否应该执行特定的语句。

`if` 语句的语法与 `while` 相似：

```cpp
if (test-condition)
    statement
```

测试条件为真会导致程序执行语句，其可以是单个语句或一个块。测试条件为假会导致程序跳过语句（见图 6.1）。作为测试，`if` 条件被转换为 `bool` 值，零变为假，非零变为真。整个 `if` 结构被视为单个语句。大多数情况下，测试条件是一个关系表达式，类似于用于控制循环的表达式。例如，假设你想要程序能够统计输入中的空格以及字符的总数。你可以在 `while` 循环中使用 `cin.get(char)` 读取字符，然后使用 `if` 语句来识别并统计空格。列表 6.1 正是这样做的，使用句号 (.) 来识别句末。

### 列表 6.1 if.cpp

```cpp
// if.cpp 使用 if 语句
#include <iostream>
int main() {
    using std::cin;
    using std::cout;
    char ch;
    int spaces = 0;
    int total = 0;
    cin.get(ch);
    while (ch != '.') // 在句末处退出
    {
        if (ch == ' ') // 检查 ch 是否为空
            ++spaces;
        ++total; // 每次执行
        cin.get(ch);
    }
    cout << " " << spaces << " spaces, " << total << " characters in sentence" << "\n";
    return 0;
}
```

以下是列表 6.1 中程序的示例输出：
```
The balloon was an inflatable dog.
6 spaces, 46 characters in sentence
```
如列表 6.1 中的注释所示，`++spaces` 语句仅在 `ch` 为空格时执行。由于它在 `if` 语句之外，`++total` 语句在每次循环中执行。注意，换行字符是通过按 Enter 键生成的。

## if else 语句

`if` 语句让程序决定是否执行特定的语句块，而 `if else` 语句让程序决定执行两个语句或块中的哪一个。它是创建备选方案的非常有价值的语句。C++ 的 `if else` 语句模仿英语，例如“如果你有钱，你就得到饼干，否则你只能得到空气。”`if else` 语句具有以下通用形式：

```cpp
if (test-condition)
  statement1
else
  statement2
```

如果 `test-condition` 为真或非零，程序执行 `statement1` 并跳过 `statement2`。否则，当 `test-condition` 为假或零时，程序跳过 `statement1` 转而执行 `statement2`。

```cpp
if (answer == 192)
  cout << "That's right!"
else
  cout << "You'd better review Chapter 1 again.";
```

每个语句可以是单个语句，也可以是由大括号分隔的语句（见图 6.2）。整个 `else` 语句结构在语法上被构造为一个单个语句。

img/cd111a87c1db9aff4db4b18834327463_0.png
图 6.2 if else 语句的结构。

例如，假设你想通过打乱字母来更改传入的文本，同时保持换行字符不变。在这种情况下，输入的每行都将转换为等长度的输出行。这意味着你的程序对换行字符采取一种行动，而对所有其他字符采取另一种行动。如列表 6.2 所示，`if else` 使这项任务变得简单。该列表还演示了 `std::scope`，这是 `using` 指令的替代方案之一。

### 列表 6.2 ifelse.cpp

```cpp
// ifelse.cpp 使用 if else 语句
#include <iostream>
int main()
{
    char ch;
    std::cout << "Type, and I shall repeat.\n";
    cin.get(ch);
    while (ch != '\n')
    {
        if (ch == '\n')
            std::cout << ch;    // 如果换行则执行
        else
            std::cout << ++ch;  // 否则执行
        cin.get(ch);
    }
    // 为了产生有趣的效果，尝试用 ch + 1 代替 ++ch
    std::cout << "\nPlease cause the slight confusion.\n";
    cin.get();
    cin.get();
    return 0;
}
```

以下是列表 6.2 中程序的示例输出：
```
Type, and I shall repeat.
An ineffable joy suffused me as beheld
An inflatable influence
The slight confusion
The of computing
```
注意列表 6.2 中的注释之一建议将 `++ch` 改为 `ch+1` 以产生有趣的效果。你能推断出会发生什么吗？如果不能，尝试运行并看看发生了什么。（提示：考虑如何处理类型）。

## if else 语句的格式

请记住，`if else` 语句中的两个备选方案必须是单个语句。如果你需要多个语句，则必须使用大括号将它们合并为一个语句块。与某些语言（如 BASIC 和 FORTRAN）不同，C++ 不会自动将 `if` 和 `else` 之间的内容视为一个块，因此你必须使用大括号来形成块。例如，以下代码会导致编译器错误：

```cpp
if (condition)
    statement1;
    statement2;
else
    statement3;
```
在这种情况下，`statement2` 被视为 `if` 块的一部分，而 `statement3` 是 `else` 语句。修复此问题请使用大括号：

```cpp
if (condition)
{
    statement1;
    statement2;
}
else
{
    statement3;
}
```

## else if else 结构

计算机程序就像生活，可能会提供两个以上的选择。你可以扩展 C++ `if else` 语句来满足这种需求。正如你所看到的，`else` 后面应该跟着一个语句，该语句可以是一个块。

```cpp
if (test-condition1)
    statement1
else if (test-condition2)
    statement2
else
    statement3
```

如果 `test-condition1` 为真，程序执行 `statement1` 并跳过其余部分。如果 `test-condition1` 为假，程序测试 `test-condition2`。如果 `test-condition2` 为真，它执行 `statement2`。如果两者为假，它执行 `statement3`。这种格式比嵌套 `if else` 语句要清晰得多：

```cpp
if (test-condition1)
    statement1
else
{
    if (test-condition2)
        statement2
    else
        statement3;
}
```

# 第 6 章 分支语句与逻辑运算符

这里是列表 6.3 中程序的示例输出：

输入一个 1-100 范围内的数字来找到我最喜爱的数字：50
太高了 -- 请再试：25
太低了 -- 请再试：37
太高了 -- 请再试：31
太高了 -- 请再试：28
太高了 -- 请再试：27
27 是正确的！

## 条件运算符与预防（Bug）

许多程序员会将更符合直觉的表达式 `variable == value` 反转为 `value == variable`，以捕获将相等运算符误写为赋值运算符的错误。例如，输入以下条件是有效的且可以正常工作的：

```cpp
if (3 == myNumber)
```
然而，如果你不小心写成下面的样子，编译器将生成错误信息，因为它认为你正尝试给字面量赋值（3 永远等于 3，不能被赋值为其他值）：

```cpp
if (3 = myNumber)
```

假设你在 `for` 循环中犯了类似的错误：

```cpp
if (myNumber = 3)
```

编译器只会地将值 3 赋值给 `myNumber`，并执行 `if` 块——这是一个非常常见的错误，而且很难发现。（不过，许多编译器会发出警告，听从警告是明智的。）作为一个一般规则，编写允许编译器发现错误的代码要比修复神秘故障的原因要容易得多。

## 逻辑表达式

通常你可能测试多一个条件。例如，要使一个字符成为小写字母，它的值必须大于等于 'a' 且小于等于 'z'。或者，如果你希望用户用 `y` 或 `n` 响应，你希望接受大写（Y 和 N）和小写。为了满足这种需求，C++ 提供了三个逻辑运算符来组合或修改现有表达式。这些运算符是逻辑或（写作 `||`）、逻辑与（写作 `&&`）和逻辑非（写作 `!`）。让我们检查一下它们：

### 逻辑或运算符：||

在英语中，“or”词可以表示一个或两个条件满足某项要求。例如，你可以去 MegaMicro 公司的野餐，或者你工作。C++ 的等效写法是逻辑或运算符，写作 `||`。该运算符将两个表达式合并为一个。如果原始表达式中的一个或两个都为真（非零），则结果表达式的值为 `true`。否则，表达式的值为 `false`。这里是一些示例：

```cpp
5 == 5 || 5 == 9 // true，因为第一个表达式为真
5 > 3 || 5 > 10 // true，因为第一个表达式为真
5 > 8 || 5 < 10 // true，因为第二个表达式为真
5 < 8 || 5 > 2 // true，因为两个表达式都为真
5 > 8 || 5 < 2 // false，因为两个表达式都为假
```

由于 `||` 的优先级低于关系运算符，你不需要在这些表达式中使用括号。表 6.1 总结了 `||` 运算符的工作方式。

表 6.1 || 运算符

| expr1 || expr2 的值 | 结果 |
|---|---|
| expr1 == true | expr1 == false | true |
| expr2 == false | true | false |

C++ 规定 `||` 是一个序列点（sequence point）。也就是说，在评估右侧之前，左侧指示的任何值都会改变。（在 C++11 较新的部分，运算符左侧的子表达式在右侧的子表达式之前排序。）例如，考虑以下表达式：

```cpp
i < 6 || i == j
```

假设 `i` 原值为 10。在与 `j` 进行比较时，`i` 的值变为 11。此外，如果左侧表达式为真，C++ 不会去评估右侧表达式，只需要一个表达式就能让整个逻辑为真。（记住，分号和逗号运算符也是序列点。）

列表 6.4 在 `if` 语句中使用 `||` 运算符来检查字符的大写和小写版本。它还使用了 C++ 的字符串拼接功能（见第 4 章，“复合类型”）将单个字符串跨三行显示。

列表 6.4 or.cpp

```cpp
// or.cpp -- 使用逻辑或运算符
#include <iostream>
int main() {
    using namespace std;
    cout << "此程序将重新格式化您的硬盘\n"
         "并删除您的所有数据。\n"
         "您想继续吗？y/n";
    char ch;
    cin >> ch;
    if (ch == 'y' || ch == 'Y') // y 或 Y
        cout << "你已被警告！\a\a\n";
    else if (ch == 'n' || ch == 'N') // n 或 N
        cout << "明智的选择 ... 再见\n";
    else
        cout << "那不是 y 或 n！显然你\n"
             << "不听指令，所以 \n"
             << "我还是会毁你的硬盘。\a\a\a\n";
    return 0;
}
```

（程序并没有真的执行任何威胁。）这里是列表 6.4 中程序的示例运行。

此程序可能会重新格式化您的硬盘并删除您的所有数据。
您想继续吗？</y> N
明智的选择 ... 再见

### 逻辑与运算符：&&

逻辑与运算符写作 `&&`，同样将两个表达式合并为一个。只有当两个原始表达式都为真时，结果表达式的值才为 `true`。这里是一些示例：

```cpp
5 == 5 && 5 == 9 // false，因为第二个表达式为假
5 > 3 && 5 > 10 // true，因为第二个表达式为假
5 > 8 && 5 < 10 // true，因为两个表达式都为真
5 < 8 && 5 > 2 // true，因为两个表达式都为真
5 > 8 && 5 < 2 // false，因为第一个表达式为假
```

由于 `&&` 的优先级也低于关系运算符，你不需要在这些表达式中使用括号。像 `||` 运算符一样，`&&` 是一个序列点。但有一个关键区别：如果左侧表达式为假，右侧表达式不会被评估。这被称为短路求值（short-circuit evaluation）。

表 6.2 && 运算符

| expr1 && expr2 的值 | 结果 |
|---|---|
| expr1 == false | false |
| expr1 == true | expr2 == false | false |
| expr1 == true | expr2 == true | true |

列表 6.5 在 `if` 语句中使用 `&&` 运算符检查字符是否在范围内。

列表 6.5 and.cpp

```cpp
// and.cpp -- 使用逻辑与运算符
#include <iostream>
int main() {
    using namespace std;
    char ch;
    cout << "输入一个字符：";
    cin >> ch;
    if (ch >= 'a' && ch <= 'z')
        cout << "你输入了一个小写字母。\n";
    else if (ch >= 'A' && ch <= 'Z')
        cout << "你输入了一个大写字母。\n";
    else
        cout << "你输入的不是字母。\n";
    return 0;
}
```

`&&` 运算符在检查多个条件时特别有用，例如在解引用指针之前检查指针是否为空：

```cpp
if (ptr != nullptr && *ptr == 5) {
    // 执行某些操作
}
```

在这种情况下，短路求值确保了表达式的第二个部分不会被评估，从而防止在 `ptr` 为空时发生崩溃。

## 程序笔记

以下是列表 6.5 中程序的输入部分：

```cpp
cin >> temp;
while (i < ArSize && temp >= 0) // 2 个退出条件
{
    array[i] = temp;
    ++i;
    if (i < ArSize)             // 数组剩余空间
    {
        cout << "Next value: ";
        cin >> temp; // 获取下一个值
    }
}
```
