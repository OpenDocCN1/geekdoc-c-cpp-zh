
```cpp
int main() {
    auto const &[lone, ltwo] = Return{ 4, 5 };
    // 或者：
    auto &&[lone, ltwo] = Return{ 4, 5 };
}
```

该对象甚至不需要将其数据成员设为公共。在 TLES 节中涵盖了使用结构化绑定但不一定引用数据成员的情况。

另一个应用出现在嵌套的 `for` 语句或选择语句受益于使用各种类型的局部变量的情况下。这些变量可以使用从匿名结构体、对或元组初始化的结构化绑定声明轻松定义。这里的示例说明了这一点：

```cpp
// 定义一个结构体：
struct Three {
    size_t year;
    double firstName;
    double interest;
};
// 定义 Three 对象的数组，并逐处理每个对象：
Three array[10];
fill(array); // 此处未实现

for (auto &[year, amount, interest] : array) {
    cout << "Year " << year << ": amount = " << amount << "\n";
}
```

使用结构化绑定声明时，构造函数必须指定所有可用元素。如果结构体有四个数据成员，结构化绑定声明必须定义四个元素。为了避免未使用变量的警告，结构化绑定声明中的至少一个变量必须被使用。

### 3.3.8 定义类型和 `using` 声明

在 C++ 中，`typedef` 通常用于定义“指向函数的指针...”的简写符号。假设我们想为一个期望一个 `double` 和一个 `int` 并返回 `unsigned long int` 的函数定义一个简写。这样的函数可以是：

`unsigned long long int compute(double, int);`

指向此类函数的指针形式如下：

`unsigned long long int (*pf) (double, int);`

如果频繁使用这种指针，可以考虑使用 `typedef` 定义它；只需在它前面加上 `typedef`，指针名称就变成了一个类型的名称。可以将其大写以便更清晰地作为类型名称：

`typedef unsigned long long int (*PF) (double, int);`

在拥有该类型后，可以使用它来声明或定义此类指针：

```cpp
PF pf = compute; // 初始化指向此类函数的指针
// 'compute'
void fun(PF pf); // 期望指向此类函数的指针
// 'compute'
```

然而，将指针包含在 `typedef` 中可能不是一个好主意，因为掩盖了 `pf` 是指针的事实。毕竟，`PF` 看起来更像 `'int x'` 而不是指针。到底，`PF` 看起来比 `'int x'` 更像指针。为了让 `pf` 是一个指针，使用 `typedef`：

`typedef long long int (double, int);`

`typedef` 的作用域限制在编译单元。此外，C++ 提供了 `using` 关键字来关联类型。在实践中，`typedef` 和 `using` 可以互换。`using` 具有更好的可读性。考虑以下三种定义：

- 传统的、带标签的类型定义（将类型名放在前面）：

`typedef unsigned long int FUN (double, int);`

- `using` 提高可读性（将类型名放在后面）：

`using = long long int (double, int);`

- 另一种构造，使用 `using` 并在最后指定类型（参见 3.3.7）：

`using FUN = unsigned long int (double, int);`

## 3.3. C 语法的补充

### 3.3.9 范围循环

C++ 的 `for` 语句与 C 语言相同：

```cpp
for (init; cond; inc)
statement
```

通常初始化、条件和递增部分是显而易见的，例如在处理数组或 vector 的元素时。许多语言的 `foreach` 语句，C++ 提供了 `std::for_each` 通用算法（参见 22.6）。

此外，C++ 添加了范围循环的新语法：

- 普通数组；
- 初始化列表；
- 标准容器（参见 23）；

冒号左侧的部分被称为初始化。变量在 `for` 语句内部有效。这里有一个示例：

```cpp
for (size_t idx = 0; auto const &element: data)
    cout << idx << ": " << element << '\n';
```

范围循环也可以受益于结构化绑定。如果 `struct Element` 有一个键和一个双精度值，并且应该累加所有正键的值，那么以下代码实现了这一点：

```cpp
struct Element {
    int key;
    double last;
};

Element data[100]; // 某种初始化
double sum = 0;
for (auto const &[key, value] : data)
{
    if (key > 0)
        sum += value;
}
```

### 3.3.10 原始字符串字面量

标准 ASCII 字符（也称为 C 字符串）由双引号分隔，支持带有 `\u`、 `\\` 和 `\0` 的转义序列。某些 ASCII 字符通常被称为空终止字符串（单数：NTB，复数：NTBs）。C 的 NTB 是大量代码的基础

在某些情况下，避免使用转义序列是有吸引力的（例如在 XML 上文中）。C++ 允许这样做，使用 R，后面跟着一个双引号，可选跟随一个标签（任意非空白字符序列，紧跟 `)`）。原始字符串在右括号 `)` 处结束，后面跟着标签（如果在启动原始字符串字面量时指定），随后是双引号。这里是一些示例：

```cpp
R"(Raw \"String"")
R"delimiter(Another \ Raw "(String))delimiter
```

## 3.3. C 语法的若干补充

在第一情况下，`{"` 和 `"}` 之间的所有内容都是字符串的一部分。不支持转义序列——第一个原始字符串字面量中的文本 `\"` 定义了三个字符：一个反斜杠、一个空白字符和一个双引号。第二个示例显示了在标记 `delimiter(` 和 `) delimiter` 之间定义的原始字符串。

原始字符串字面量在处理很长且复杂的 ASCII 序列字符（例如 `usage-info` 或长序列）时非常有用。归根结底，它们只是：长的 NTB。这些长原始字符串字面量应该与使用它们的代码分开，以保持代码运行的可靠性。

作为一个说明：bison++ 解析器生成器支持 `+NOTRANS(--{})` 提示。当指定该项时，在重新请求调试时，代码 bison++ 插入插入提示代码。直接将原始字符串字面量插入到处理提示代码的函数中非常难以阅读：

```cpp
void prompt(ostream &out)
{
    if (d_genDebug)
        out << (d_options.prompt()) ? R"(
            if (d_debug_)
n                s_out << "\n=============================\n"
                ?" << dflush_;
                std::string s;
                getline(std::cin
```

通过将原始字符串字面量定义为命名的 NTB 可以大大提高可读性，这些定义定义在源文件的匿名命名空间中（参见第 4 章）：

```cpp
namespace {
    char const noPrompt() = 
R"(
        if (d_debug_)
            s_out << '\n';
    )";

    char const doPrompt() = 
R"(
        if (d_debug_)
            s_out << "\n=============================\n"
            ?" << dflush_;
            std::string s;
            getline(std::cin, s);
    )";
```

```cpp
} // 匿名命名空间
void prompt(ostream &out)
{
    if (d_genDebug)prompt.prompt() <<
    out << (d_options.prompt ? doPrompt : noPrompt) << '\n';
}
```

### 3.3.11 二进制常量

除了十六进制整数常量（以 0x 开头）、八进制整数常量（以 0 开头）和十进制整数常量（以数字 1-9 中的任意一个开头）之外，二进制整数常量可以使用前缀 0b 或 0B 定义，也可以使用符号 `0b101` 来表示（十进制）值 5。

二进制常量在这里出现在例如位标志（bit-flags）的上下文中，因为它可以立即显示哪些位域被设置了，而其他表示法的信息量较少。

### 3.3.12 带有初始化器的选择语句

循环语句的标准以一个可选的初始化句开始。初始化句还允许我们将变量局部化到语句的作用范围内。初始化句也可以用于选择语句。

考虑以下情况：如果从标准输入流读取的下一行等于 `go!`，则执行某项操作。传统的，当在函数内部时，为了尽可能局部化包含下一行的字符串，必须使用如下构造：

```cpp
void function()
{
    // 任意一组语句
    {
        string line; // 局部化 line
        if (getline(cin, line))
            action();
    }
    // ... 任意一组语句
}
```

由于初始化句也可以用于选择语句（`if` 和 `switch` 语句）（注意，对于选择语句，分号是初始化句的一部分，这与 `for` 语句中可选的 init（无分号）句不同），我们可以将上述示例重表述为如下：

```cpp
void function()
{
    // ... 任意一组语句
    if (string line; getline(cin, line))
        action();
}
```

```cpp
// 任意一组语句
}
```

注意，变量仍然可以在实际的条件句中定义。这对于扩展的 `if` 和 `switch` 语句都是如此的。然而，在使用条件句之前，可以使用初始化句来定义额外的变量（复数，因为它可以包含一个用逗号分隔的变量列表，类似于 `for` 语句中可用的语法）。

### 3.3.13 属性

属性是插入到源文件中的编译器指令，用于告知编译器紧随指定属性之后的代码（变量或函数）的某些特殊之处。属性用于告知编译器某些情况是刻意的，从而防止编译器发出警告。

以下属性被识别：

- `[[caries_dependency]]`:

此属性目前尚未被 C++ 注释涵盖。在 C++ 注释的目前阶段，可以安全地忽略它。

- `[[deprecated]]`:

此属性（及其备用形式 `[[deprecated(`）：

```cc
demo.cc:12:24: warning: 'void deprecatedFunction()' is deprecated
    [-deprecated-declarations] deprecatedFunction();
```

```cc
demo.cc:5:21: note: declared here
    [[deprecated]] void deprecatedFunction()
```

当使用备用形式 `[[deprecated("do not use")]] void fun())` 时，编译器会生成警告，显示双引号之间的文本，例如：

```cc
demo.cc:12:24: warning: 'void deprecatedFunction()' is deprecated
    do not use [-deprecated-declarations]
    deprecatedFunction();
```

```cc
demo.cc:5:38: note: declared here
    [[deprecated("do not use")]] void deprecatedFunction()
```

- `[[fallthrough]]`

当语句嵌套在 `switch` 语句的 case 下时使用：

```cpp
switch (selector) {
    case 1:
        // 某些操作
        fallthrough; // 显式穿透
    case 2:
        // 某些操作
        break;
}
```

# 第 3 章：C++ 的初印象

- * E 或 e: 浮点数字面量中的指数字符。例如：1.23E+3。在这里，E 应该读作（并解释为）：乘以 10 的几次方。因此，1.23E+3 代表值 1230。
- * F 可以作为非整数数值常量的后缀，用于表示值类型为 `float`，而不是默认的 `double`。例如：12.F（将 `double` 将 12 转换为浮点值）；1.23E+3F（上一个示例）。1.23E+3 是一个 `double` 值，而 1.23E+3F 是一个 `float`。
- * L 可以作为前缀，表示元素为 `wchar_type` 字符的字符字符串。例如：L"hello world"。
- * L 可以作为整值的后缀，用于表示值类型为 `long`，而不是默认的 `int`。注意，没有表示 `short` 类型的字母。对于该类型，必须使用 `static_cast<short>()`。
- * p 用于指定十六进制浮点数中的前缀。例如 0x1p4。它的指数被读取为十进制常量，因此不能以 0x 开头。指数被解释为 2 的幂。所以 0x1p2 等（十进制）等于 64：16 * 2^2。
- * U 可以作为整值的后缀，用于表示无符号值（unsigned），而不是有符号值。它可以与后缀 L 结合，产生一个 `unsigned long int` 值。

当然，还有：x 和 a 字符可以用来表示无符号字符（可选使用大写字母）。

## 3.4. 新语言定义的数据类型

使用 `bool` 类型通常比使用 `int` 类型更清晰。考虑以下原型：

```cpp
bool exists(char const *fileName); // (1)
int  exists(char const *fileName); // (2)
```

对于第一个原型，读者期望如果给定的文件名是一个存在的文件名，函数将返回 `true`。然而，对于第二个原型存在一些歧义：从直觉上，返回值 1 是很有吸引力的，因为它允许如下构造：

另一方面，许多系统函数（如 `access`、`stat` 以及许多其他）返回 0 表示操作成功，保留其他值来表示各种类型的错误。

根据经验，我建议：如果一个函数应该通知调用者任务的成功或失败，让函数返回枚举值，并通过各种符号常量来记录情况。只有当函数返回一个具有概念意义的整数值（例如两个 `int` 值的和）时，才让函数返回 `int`。

### 3.4.1 'bool' 数据类型

`bool` 类型表示布尔（逻辑）值，可以使用（现已保留的）常量 `true` 和 `false`。除了这些保留值外，整值也可以赋值给 `bool` 类型的变量，它们会根据转换规则隐式转换为 `true` 和 `false`（假设 `intValue` 是一个 `int` 变量，`boolValue` 是一个 `bool` 变量）：

```cpp
// 从 int 到 bool:
boolValue = intValue ? true : false;

// 从 bool 到 int:
intValue = boolValue ? 1 : 0;
```

此外，当 `bool` 值被插入字符串时，`true` 被表示为 1，`false` 表示为 0。考虑以下示例：

```cpp
cout << "A true value: " << true << "\n"
     << "A false value: " << false << "\n";
```

`bool` 数据类型在许多编程语言中也存在。Pascal 有自己的类型 `Boolean`；Java 有 `boolean` 类型。与这些语言不同，C++ 的 `bool` 类型行为类似于一种 `int` 类型，只有 `true` 和 `false` 两个值。

实际上，这些值可以被解释为 1 和 0 的枚举值。所以可以想象 `bool` 类型背后的哲学，尽管如此，将 `true` 赋值给 `int` 变量也不会产生错误。

### 3.4.2 'wchar_t' 数据类型

`wchar_t` 类型是 `char` 类型的扩展，用于容纳宽字符值（详见下一节）。g++ 编译器保留 `sizeof(wchar_t)` 为 4，可以容纳 65536 个字符值。注意 Java 的 `char` 类型与 C++ 的 `char` 类型类似，宽度为 2 字节。另一方面，Java 的 `byte` 类型与 C++ 的 `char` 类型类似：1。

### 3.4.3 Unicode 编码

在 C++ 中，可以通过在字符串字面量前加上 L（例如 L"hello world"）来定义 `wchar_t` 字面量。C++ 还支持 8、16 和 32 Unicode 编码。此外，引入了两个新类型：分别存储 Unicode 值的 `char16_t` 和 `char32_t`。

各种 Unicode 编码的字符串字面量可以定义为：
