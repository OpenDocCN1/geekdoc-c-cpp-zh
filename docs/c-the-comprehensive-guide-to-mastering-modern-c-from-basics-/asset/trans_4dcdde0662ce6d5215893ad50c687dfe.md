
不想为了满足这些需求所需的巨大表格而让编译器变得臃肿。[ 55 ]。然而，如果用户已经在使用 ICU，他们可能想利用它来处理字符串字面量。

从原则上说，程序员现在可以为字面量本身定义后缀了。通过该后缀，用户可以指定使用哪个自由函数来解释源码中的该字面量。

## 23.7.2 命名规则

标准限制了此标识符的选择，因此对于可移植代码，你应该遵循以下标识符命名规则：

- 标识符必须以下划线 `_` 开头；所有其他字面量后缀都留给未来的语言扩展。

- 特尤其是它不应该以两个下划线开头；标准将此留给编译器和标准库。特别是由编译器或库定义的宏可能会与此发生冲突。因此，最好避免这种潜在的冲突。

- 出于的原因，标识符不应以下划线跟随大写字母开头——例如，不要以 `_A` 开头。

- 所以第二个字符应该是小写字母或数字。

- 将新的字面量操作符定义在它们自己的命名空间是一个良好的习惯。这样，你可以使用命名空间指令精确地控制哪些操作符可见的。当你定义 `_x` 后缀时，`_x` 标识符并没有被保留：只有当配合 `operator""` 时，它才成为一个标识符。因此，后缀 `_x` 和变量 `_x` 之间不会冲突。

> 提示
用户定义字面量的操作符应该定义在它们自己的命名空间中。它们的名称必须以下划线开头，后面接小写字母。

## 23.7.3 字面量处理阶段

为了理解为什么会有不同的 `operator""` 重载，你需要知道编译器在不同的阶段处理字面量。这些大致如下：

- 在标记拆分阶段，源码的语言元素被分类为关键字、数字、符号、字符串等。此阶段的字面量可以作为原始字面量传递给 `operator""`。对于数字，它们将是 `const char*`（长度使用 `size_t`）或模板变体；对于字符串字面量，它们是字符字符串变体（长度使用 `size_t`）。

- 然后，数字字面量被转换为它们的数值。在此阶段之后，它们可以带有数值参数传递给 `operator""` 变体，并被视为“已加工”（经过预处理——不再是“原始的”）。

## 23.7.4 重载变体

使用自定义后缀的所有共同点是它们都是通过 `operator""` 定义的。区别如下：

- 类型：返回类型始终是该字面量最终应该拥有的类型。内置类型和用户定义类型都是可能的。

- `Type operator ""_x(const char*)`: 不带长度参数的 `const char*` 形式是原始字符串。像 `1234_x` 这样的数字序列作为四个字符序列和终止字符 `'\0'` 传递给 `operator""_x(const char*)`。注意，即使参数是 `const char*`，它也不指的是字符串字面量：“原始”意味着数字序列在没有经过预处理的情况下传递给操作符。由于源码中的字面量周围没有引号，所以你只能通过这种方式解析数字字面量。虽然你可以在源码中写 `234_x` 或 `9.87_x`，但编译器会对没有加引号的 `hello_x` 报错，因为此时它已将其分类为标识符标记，而不是字面量。

- `Type operator ""_x(unsigned long long)` 和 `Type operator ""_x(long double)`：预处理的（已加工的）数字字面量使用 `unsigned long long` 和 `long double` 参数进行处理。因此，`4847_x` 将导致对 `operator""_x (unsigned long long)` 的单次调用，小数 4847。

`0x12ef_x` 也会进行相同的调用；编译器会处理掉 `0x` 前缀并转换数字。此外，`10000.0_x` 和 `1+e4_x` 会导致对 `operator "_x(long double)` 的调用。

- `Type operator "_x(const CHAR*, size_t)`
其中 `CHAR` 可以代表 `char`、`wchar_t`、`char16_t` 或 `char32_t`。这些是编译器预处理过的字符串，是解析带引号字面量的唯一方法，操作符接收两个参数，第二个使用 `size_t` 指定长度。字符串不需要以 `'\0'` 字符终止。
这里的预处理意味着编译器已经解释了字符串字面量之前的前缀（例如 `u8 R(` 或 `L(`），并且已经拼接了相邻的字面量：`"mein" "text"_x` 只导致一个 `operator "_x(const char*, size_t)`。

- `template<char...> Type operator "_x()`
该变体处理原始字面量，即不带引号的数字序列。与 `const char*` 形式不同，你也可以将其用于浮点数。字面量 `2.17_x` 将导致对 `operator "_x<'2', '.', '1', '7'>()` 的调用——不带终止的 `'\0'` 字符。通常，你会递归地定义这个操作符。

在实践中，当编译器决定使用这些重载之一时，如下所示。

```
// https://godbolt.org/z/Mevoshb3o
namespace lits {
    long double operator"_w(long double);
    string      operator"_w(const char16_t*, size_t);
};

unsigned operator""_w(const char*);
int main() {
    using namespace lits;
    1.2_w; // operator""_w(long double), with (1.2L)
    u'one'_w; // operator""_w(char16_t, size_t), with (u'one', 3)
    12_w; // operator""_w(const char*), with "12"
    "two"w; // operator""_w(const char*, size_t) 未定义
}
```
**列表 23.37** 哪个字面量会导致哪个操作符调用？

对于字面量 `"two"w`，编译器寻找 `operator""_w(const char*, size_t)`。由于我们没有定义它，编译器在此处输出错误信息。

## 23.7.5 使用模板的用户定义字面量

如果你只需要处理一组定义良好的字面量，`template variant` 变体也容易实现。

```
// https://godbolt.org/z5rdzn8YP4
namespace lits {
    // 通用模板
    template<char... > int operator""_bin2();
    // 特殊化
    template<> int operator""_bin2<'0'>() { return 0; }
    template<> int operator""_bin2<'1'>() { return 1; }
    template<> int operator""_bin2<'0','1'>() { return 2; }
    template<> int operator""_bin2<'1','1'>() { return 3; }
}
int main() {
    using namespace lits;
    int b = 11_bin2;
}
```
