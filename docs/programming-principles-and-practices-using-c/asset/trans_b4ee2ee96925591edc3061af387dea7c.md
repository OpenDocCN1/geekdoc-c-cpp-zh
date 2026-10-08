
### B.8.3 正则表达式匹配

正则表达式设施位于 `<regex>` 中。主要功能包括：

- 在任意长度的数据流中搜索匹配正则表达式的字符串 – 由 **regex_search()** 支持
- 将正则表达式与已知大小的字符串进行匹配 – 由 **regex_match()** 支持
- 替换匹配项 – 由 **regex_replace()** 支持；本书未对此进行描述；请参阅专家级文本或手册

**regex_search()** 或 **regex_match()** 的结果是一组匹配项，通常表示为 **smatch** 对象：

```cpp
regex row("^\\w+(	|\\d+)|(\\d+)$(\\d+)\\$" );   // data line

while (getline(in,line)) {                // check data line
    smatch matches;
    if (!regex_match(line, matches, row))
        error("bad line", lineno);
    // check row:
    int field1 = from_string<int>(matches[1]);
    int field2 = from_string<int>(matches[2]);
    int field3 = from_string<int>(matches[3]);
    // ...
}
```

正则表达法的语法基于具有特殊含义的字符（第 23 章）：

| **正则表达式特殊字符** | |
| :--- | :--- |
| . | 任意单个字符（“通配符”） |
| [ | 字符类 |
| { | 计数 |
| ( | 开始分组 |
| ) | 结束分组 |
| \ | 下一个字符具有特殊含义 |
| * | 零次或多次 |
| + | 一次或多次 |
| ? | 可选（零次或一次） |
| \| | 替代（或） |
| ^ | 行首；取反 |
| $ | 行尾 |

| **重复** | |
| :--- | :--- |
| {n} | 恰好 n 次 |
| {n,} | n 次或更多 |
| {n,m} | 至少 n 次且至多 m 次 |
| * | 零次或多次，即 {0,} |
| + | 一次或多次，即 {1,} |
| ? | 可选（零次或一次），即 {0,1} |

| **字符类** | |
| :--- | :--- |
| alnum | 任意字母数字字符或下划线 |
| alpha | 任意字母字符 |
| blank | 任意非换行分隔符的空白字符 |
| cntrl | 任意控制字符 |
| d | 任意十进制数字 |
| digit | 任意十进制数字 |
| graph | 任意图形字符 |
| lower | 任意小写字符 |
| print | 任意可打印字符 |
| punct | 任意标点字符 |
| s | 任意空白字符 |
| space | 任意空白字符 |
| upper | 任意大写字符 |
| w | 任意单词字符（字母数字字符） |
| xdigit | 任意十六进制数字字符 |

几个字符类由简写表示支持：

| **字符类简写** | | |
| :--- | :--- | :--- |
| \d | 十进制数字 | [[:digit:]] |
| \l | 小写字符 | [[:lower:]] |
| \s | 空格（空格、制表符等） | [[:space:]] |
| \u | 大写字符 | [[:upper:]] |
| \w | 字母、十进制数字或下划线 (\_) | [[:alnum:]] |
| \D | 非 \d | [^[:digit:]] |
| \L | 非 \l | [^[:lower:]] |
| \S | 非 \s | [^[:space:]] |
| \U | 非 \u | [^[:upper:]] |
| \W | 非 \w | [^[:alnum:]] |

## B.9 数值

C++ 标准库提供了数学（科学、工程等）计算的最基本构建块。

### B.9.1 数值限制

每个 C++ 实现都指定了内置类型的属性，以便程序员可以使用这些属性来检查限制、设置哨兵值等。

从 `<limits>` 中，我们获得每个内置或库类型 **T** 的 `numeric_limits<T>`。此外，程序员可以为用户定义的数值类型 **X** 定义 `numeric_limits<X>`。例如：

```cpp
class numeric_limits<float> {
public:
    static const bool is_specialized = true;

    static constexpr int radix = 2;       // base of exponent (in this case, binary)
    static constexpr int digits = 24;     // number of radix digits in mantissa
    static constexpr int digits10 = 6;    // number of base-10 digits in mantissa

    static constexpr bool is_signed = true;
    static constexpr bool is_integer = false;
    static constexpr bool is_exact = false;

    static constexpr float min() { return 1.17549435E-38F; }  // example value
    static constexpr float max() { return 3.40282347E+38F; }  // example value
    static constexpr float lowest() { return -3.40282347E+38F; } // example value

    static constexpr float epsilon() { return 1.19209290E-07F; } // example value
    static constexpr float round_error() { return 0.5F; }        // example value

    static constexpr float infinity() { return /* some value */; }
    static constexpr float quiet_NaN() { return /* some value */; }
    static constexpr float signaling_NaN() { return /* some value */; }
    static constexpr float denorm_min() { return min(); }

    static constexpr int min_exponent = -125;      // example value
    static constexpr int min_exponent10 = -37;     // example value
    static constexpr int max_exponent = +128;      // example value
    static constexpr int max_exponent10 = +38;     // example value

    static constexpr bool has_infinity = true;
    static constexpr bool has_quiet_NaN = true;
    static constexpr bool has_signaling_NaN = true;
    static constexpr float_denorm_style has_denorm = denorm_absent;
    static constexpr bool has_denorm_loss = false;

    static constexpr bool is_iec559 = true;              // conforms to IEC-559
    static constexpr bool is_bounded = true;
    static constexpr bool is_modulo = false;
    static constexpr bool traps = true;
    static constexpr bool tininess_before = true;

    static constexpr float_round_style round_style = round_to_nearest;
};
```

从 `<limits.h>` 和 `<float.h>` 中，我们获得指定整数和浮点数关键属性的宏，包括：

| **限制宏** | |
| :--- | :--- |
| `CHAR_BIT` | `char` 中的位数（通常为 8） |
| `CHAR_MIN` | 最小 `char` 值 |
| `CHAR_MAX` | 最大 `char` 值（如果 `char` 是有符号则为 127，如果是无符号则为 255） |

### B.9.2 标准数学函数

标准库提供了最常见的数学函数（定义在 `<cmath>` 和 `<complex>` 中）：

| **标准数学函数** | |
| :--- | :--- |
| `abs(x)` | 绝对值 |
| `ceil(x)` | 大于等于 `x` 的最小整数 |
| `floor(x)` | 小于等于 `x` 的最大整数 |
| `round(x)` | 四舍五入到最近的整数（.5 向远离零的方向舍入） |
| `sqrt(x)` | 平方根；`x` 必须为非负数 |
| `cos(x)` | 余弦 |
| `sin(x)` | 正弦 |
| `tan(x)` | 正切 |
| `acosh(x)` | 反余弦；结果为非负数 |
| `asinh(x)` | 反正弦；返回最接近 0 的结果 |
| `atanh(x)` | 反正切 |
| `sinh(x)` | 双曲正弦 |
| `cosh(x)` | 双曲余弦 |
| `tanh(x)` | 双曲正切 |
| `exp(x)` | 以 e 为底的指数 |
| `log(x)` | 自然对数，以 e 为底；x 必须为正数 |
| `log10(x)` | 以 10 为底的对数 |

有接受 **float, double, long double,** 和 **complex** 参数的版本。对于每个函数，返回类型与参数类型相同。如果标准数学函数无法产生数学上有效的结果，它会设置变量 **errno**。

### B.9.3 复数

标准库提供了复数类型 **complex<float>, complex<double>,** 和 **complex<long double>**。当 **Scalar** 是支持常规算术运算的其他类型时，**complex<Scalar>** 通常可以工作，但不保证可移植性。

```cpp
template<class Scalar> class complex {  // a complex is a pair of scalar values, basically a coordinate pair
  Scalar re, im;
public:
  constexpr complex(const Scalar &r, const Scalar &i) :re(r), im(i) { }
  constexpr complex(const Scalar &r):re(r), im(Scalar{}) { }
  constexpr complex() :re(Scalar{}), im(Scalar{}) { }
  Scalar real() { return re; }  // real part
  Scalar imag() { return im; }  // imaginary part
  // operators: += -= *= /=
};
```
