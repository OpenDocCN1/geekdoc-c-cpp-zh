
你必须给通常的字面量追加一个后缀。对于 `Complex`，后缀是 `_i`；对于 `Puzzle`，后缀是 `_puzzle`。那么，4 如何变成 `Complex`，或者 `"oXoXoX"` 如何变成 `Puzzle` 呢？为此，将 `operator""s` 定义为自由函数，这些函数接收 `4` 或 `"oXoXoX"` 作为参数，并返回 `Complex` 或 `Puzzle`。

刚才只是快速浏览——现在进入慢动作版本。

### 23.7.1 什么是字面量？

在你可以自行定义它们的语境下，字面量包括

- 数字序列，其中混有少量用于逗号或指数的特殊字符，例如 `7`、`3.14`、`0xff` 或 `2.1e+4.8`；或
- 用引号括起来的字符串，例如 `"hello"` 和 `"octal\0123"`，可选地带有
  - 后缀，例如 `L` 或 `d`，用于指定确切的数据类型，和/或
  - 对于字符串，前缀 `L` 或用于 Unicode 或原始字符串字面量的字符串前缀之一——`u`、`U` 或 `R"(`。

还有一些预定义字面量是你不能更改或自行定义的。这些是 *布尔* 字面量 `true` 和 `false`，以及 *指针字面量* `nullptr`。

如果你能写 `™` 而不是用代码序列 `\u2122` 来表示商标符号，那岂不是很好？

```cpp
"Coca Cola[TRADE MARK SIGN]"_unicode
```

在 Unicode 标准中，每个字符也有一个唯一的名称。^2 在 Unicode 国际组件（ICU）库中，这是可行的，但人们不想用为此所需的大型表来使编译器膨胀。^3 然而，如果用户已经在使用 ICU，他们可能希望利用它来处理字符串字面量。

^2 Unicode 6.0 字符代码表，http://unicode.org/charts

^3 Unicode 国际组件，https://icu.unicode.org/

原则上，程序员现在可以自行定义字面量的后缀。而通过后缀，用户指定使用哪个 *自由函数* 来解释源代码中的字面量。

### 23.7.2 命名规则

标准在标识符的选择上对用户加以限制，因此对于可移植代码，你应当遵守以下标识符规则：

- 标识符必须以一个下划线 `_` 开头；所有其他字面量后缀都保留给未来的语言扩展。
- 特别地，它*不应*以两个下划线开头；标准将这种形式保留给编译器和标准库。尤其要注意，编译器或库定义的宏可能与此冲突。因此，最好避免这种潜在冲突。
- 出于同样的原因，标识符不应以下划线后跟大写字母开头——例如，不要以 `_A` 开头。
- 因此，第二个字符应当是小写字母或数字。
- 一个好的做法是在它们自己的命名空间中定义新的字面量运算符。这样，你可以通过 `using namespace` 指令精确控制哪些运算符可见。当你定义 `_x` 后缀时，`_x` 标识符并未被保留：只有与 `operator""` 一起使用时，它才成为标识符。因此，后缀 `_x` 和变量 `_x` 不会相互冲突。

> **提示**
>
> 用户定义字面量的运算符应定义在它们自己的命名空间中。它们的名称必须以一个下划线开头，后续字符应为小写字母。

### 23.7.3 字面量处理阶段

要理解为什么 `operator""` 会有不同的重载，你需要知道编译器会在不同阶段处理字面量。大致如下：

- 在 *词法单元* 拆分阶段，源代码的语言元素被归类为 *关键字*、*数字*、*符号*、*字符串* 等。此阶段得到的字面量可以作为 *原始字面量* 传递给 `operator""`。对于数字，这些字面量随后是 `const char*`（不带表示长度的 `size_t`）或模板变体；对于字符串字面量，它们是字符串变体（带表示长度的 `size_t`）。
- 数字字面量会被转换为其数值。此阶段之后，它们可以传递给带数值参数的 `operator""` 变体，然后被视为“已处理”（cooked，经过预处理——不再是“原始”的）。

### 23.7.4 重载变体

使用自定义后缀的所有可能性都有一个共同点：它们由 `operator""` 定义。接下来的差异如下：

- **类型**
  
  *返回类型* 始终是该字面量最终应具有的类型。内置类型和用户定义类型都可以。

- **类型 operator "" _x(const char*)**
  
  不带长度参数的 const char* 形式处理原始字符串。像 1234_x 这样的数字序列会作为四个字符的序列加上终止字符 '\0' 传递给 operator "" _x(const char*)。注意，这并不指字符串字面量，即使参数是 const char*：这里的“原始”意味着数字序列不会经过预处理就传递给运算符。由于源代码中字面量周围没有引号，你只能用这种方式解析数字字面量。虽然你可以在源代码中写 234_x 或 9.87_x，但编译器会对不带引号的 hello_x 报错，因为此时它已将其归类为标识符词法单元，而不是字面量。

- **类型 operator "" _x(unsigned long long)** / **类型 operator "" _x(long double)**
  
  经过预处理（cooked）的数字字面量会使用参数 unsigned long long 和 long double 进行处理。因此，4847_x 会导致一次对 operator "" _x(unsigned long long) 的调用，参数为十进制数 4847。0x12ef_x 也会进行同样的调用；编译器会去掉 0x 前缀并转换数字。此外，10000.0_x 和 1e+4_x 会导致对 operator "" _x(long double) 的同一调用。

- **类型 operator "" _x(const char*, size_t)**
  
  其中 CHAR 可以代表 char、wchar_t、char16_t 或 char32_t。这些是由编译器预处理后的字符串，也是解析带引号字面量的唯一方式。这些运算符接收两个参数，第二个参数使用 size_t 指定长度。字符串不需要以 '\0' 字符终止。这里的“预处理”意味着编译器已经解释了字符串字面量之前的前缀，例如 u8、R"( 或 L，并且已经拼接了相邻字面量："mein" "text"_x 只会导致一次 operator "" _x(const char*,size_t) 调用。

- **template<char...> 类型 operator "" _x()**
  
  模板变体处理原始字面量，即不带引号的数字序列。与 const char* 形式不同，你也可以将其用于浮点数。字面量 2.17_x 会导致调用 operator "" _x<'2', '.', '1', '7'>()——不带终止字符 '\0'。通常，你会递归地定义这个运算符。

在实践中，当编译器决定使用这些重载中的哪一个时，情况如下面的清单所示。

```cpp
// https://godbolt.org/z/Mevoshb3o

namespace lits {
  long double operator"" _w(long double);
  string      operator"" _w(const char16_t*, size_t);
  unsigned    operator"" _w(const char*);
}

int main() {
    using namespace lits;
    1.2_w;       // operator"" _w(long double), with (1.2L)
    u"one"_w;   // operator"" _w(const char16_t*, size_t), with (u"one", 3)
    12_w;       // operator"" _w(const char*), with "12"
    "two"_w;    // ✗ operator"" _w(const char*, size_t) not defined
}
```

**清单 23.37** 哪个字面量导致哪个运算符调用？

对于字面量 "two"_w，编译器会查找 operator"" _w(const char*, size_t)。由于我们没有定义该运算符，编译器会在那里输出错误消息。

### 23.7.5 使用模板的用户定义字面量

如果你只需要处理一组定义明确的字面量，模板变体也很容易实现。

```cpp
// https://godbolt.org/z/5rdzn8YP4
namespace lits {
    // general template
    template<char...> int operator"" _bin2();
    // specializations
    template<> int operator"" _bin2<'0','0'>() { return 0; }
    template<> int operator"" _bin2<'0','1'>() { return 1; }
    template<> int operator"" _bin2<'1','0'>() { return 2; }
    template<> int operator"" _bin2<'1','1'>() { return 3; }
}
int main() {
    using namespace lits;
    int one = 01_bin2;
    int three = 11_bin2;
}
```

**清单 23.38** 用于长度恰好为二的字面量的模板。

首先声明通用模板，但不实现（“定义”）它。这里我们确实需要一个用于 operator"" 的、模板参数为 `char...` 的可变参数模板。然后，针对你希望使用的那些确切字面量，在模板特化列表中给出定义。

这里，`0_bin2` 和 `1111_bin2` 自然会导致错误，因为我们没有为它们定义任何特化。此外，这种枚举方式繁琐且容易出错——总而言之，不推荐。但它引出了 *递归地* 定义模板的概念。
