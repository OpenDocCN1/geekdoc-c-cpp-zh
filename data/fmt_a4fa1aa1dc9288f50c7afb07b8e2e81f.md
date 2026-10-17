
| `isspace(c, loc)` | Is `c` a space in `loc`? |

| `isblank(c, loc)` | Is `c` a blank in `loc`? |

| `isprint(c, loc)` | Is `c` printable? |

| `iscntrl(c, loc)` | Is `c` a control character? |

| `isupper(c, loc)` | Is `c` an uppercase letter? |

| `islower(c, loc)` | Is `c` a lowercase letter? |

| `isalpha(c, loc)` | Is `c` a letter? |

| `isdigit(c, loc)` | Is `c` a decimal digit? |

| `ispunct(c, loc)` | Is `c` not a letter, digit, whitespace, or invisible control character? |

| `isxdigit(c, loc)` | Is `c` a hexadecimal digit? |

| `isalnum(c, loc)` | `isalpha(c)` or `isdigit(c)` |

| `isgraph(c, loc)` | `isalpha(c)` or `isdigit(c)` or `ispunct(c)` (note: not space) |

These functions are trivially implemented using `use_facet`. For example:

```cpp
template<class C>
inline bool isspace(C c, const locale& loc)
{
    return use_facet<ctype<C>>(loc).is(space, c);
}
```

The one-argument versions of these functions (§36.2.1) use the current C global locale. Except for the rare cases in which the C global locale and the C++ global locale differ (§39.2.1), we can think of a one-argument version as the two-argument version applied to `locale()`. For example:

```cpp
inline int isspace(int i)
{
    return isspace(i, locale()); // almost
}
```

## 39.5.2 Character Conversions

Case conversions can be locale sensitive:

**Character Conversion (§iso.22.3.3.2.1)**

| Expression | Equivalent implementation |

| --- | --- |

| `c2 = toupper(c, loc)` | `use_facet<ctype<C>>(loc).toupper(c)` |

| `c2 = tolower(c, loc)` | `use_facet<ctype<C>>(loc).tolower(c)` |

## 39.5.3 String Conversions

Character code conversions can be locale sensitive. Class template `wstring_convert` performs conversions between a wide string and a byte string. It lets you specify a code conversion facet (such as `codecvt`) to perform the conversions, without affecting any streams or locales. For example, you might use a code conversion facet called `codecvt_utf8` directly to output a UTF-8 multibyte sequence to `cout` without altering `cout`’s locale:

```cpp
wstring_convert<codecvt_utf8<wchar_t>> myconv;
string s = myconv.to_bytes(L"Hello\n");
cout << s;
```

The definition of `wstring_convert` is fairly conventional:

```cpp
template<class Codecvt,
         class Wc = wchar_t,
         class Wa = std::allocator<Wc>,
         class Ba = std::allocator<char>>
class wstring_convert {
public:
    // wide-character allocator // byte allocator
    using byte_string = basic_string<char, char_traits<char>, Ba>;
    using wide_string = basic_string<Wc, char_traits<Wc>, Wa>;

    using state_type = typename Codecvt::state_type;
    using int_type = typename wide_string::traits_type::int_type;
    // ...
};
```

The `wstring_convert` constructors allow us to specify a character conversion facet, an initial conversion state, and values to be used in case of errors:

- `wstring_convert cvt {};`

- `wstring_convert cvt {pcvt, state};`

- `wstring_convert cvt {pcvt};`

- `wstring_convert cvt {b_err, w_err};`

- `wstring_convert cvt {b_err};`

- `cvt.~wstring_convert();`

`wstring_convert cvt {new Codecvt};` — `cvt` uses the conversion facet `*pcvt` and conversion state `state`.

`wstring_convert cvt {pcvt, state_type{}};` — `cvt` uses the conversion facet `*pcvt` and default conversion state.

`wstring_convert cvt {b_err, w_err};` — use `b_err` and `w_err` as error values.

`wstring_convert cvt {b_err};` — use `b_err` as error value.

If a conversion to a `wide_string` fails, functions on a `cvt` constructed with a non-default `w_err` string return that string (as an error message); otherwise, they throw `range_error`.

If a conversion to a `byte_string` fails, functions on a `cvt` constructed with a non-default `b_err` string return that string (as an error message); otherwise, they throw `range_error`.

An example:

```cpp
void test()
{
    wstring_convert<codecvt_utf8_utf16<wchar_t>> converter;
    string s8 = u8"This is a UTF-8 string";
    wstring s16 = converter.from_bytes(s8);
    string s88 = converter.to_bytes(s16);
    if (s8 != s88)
        cerr << "Insane!\n";
}
```

## 39.5.4 Buffer Conversions

We can use a code conversion facet (§39.4.6) to write directly into or to read directly from

- 而不是在内置类型值之间进行转换); §39.4.3.

- [17] `time_put` facet 可用于 `<chrono>` 风格和 `<ctime>` 风格的时间；§39.4.4.

- [18] 优先使用 `locale` 显式的字符分类函数；§39.4.5, §39.5.

本页有意留空。

- 引言

- 数值极限

  - 极限宏

- 标准数学函数

- **复数**

- 数值数组：**valarray**

  - 构造函数与赋值；下标访问；操作；切片；**slice_array**；广义切片

- 广义数值算法

  - **accumulate()**；**inner_product()**；**partial_sum()** 与 **adjacent_difference()**；**iota()**

- 随机数

  - 引擎；随机设备；分布；C 风格随机数

- 建议

# 数值

> 计算的目的是洞察，而非数字。

> — R. W. Hamming

> ……但对于学生而言，数字往往是通往洞察的最佳途径。

> — A. Ralston

# 40.1 引言

C++ 在设计时并非主要着眼于数值计算。然而，数值计算通常发生在其他工作的上下文中——例如数据库访问、网络、仪器控制、图形、仿真和金融分析——因此，对于作为更大系统一部分的计算任务，C++ 成了一种颇具吸引力的载体。此外，数值方法早已超越了“对浮点数向量进行简单循环”的阶段。当计算需要更复杂的数据结构时，C++ 的优势便体现出来。最终结果是，C++ 被广泛用于涉及复杂数值计算的科学、工程、金融及其他计算领域。因此，支持此类计算的手段和技术应运而生。本章介绍标准库中支持数值计算的部分。我无意教授数值方法。数值计算本身就是一个引人入胜的话题。要理解它，你需要一门优秀的数值方法课程，或者至少一本优秀的教科书——而不仅仅是语言手册和教程。

除此处描述的标准库设施外，第 29 章还给出了数值编程的一个扩展示例：N 维矩阵。

# 40.2 数值极限

要想用数字做一些有意义的事情，我们通常需要了解内置数值类型的一般属性。为了让程序员能够充分利用硬件，这些属性是由实现定义的，而不是由语言本身的规则确定的（§6.2.8）。例如，最大的 int 是多少？最小的正 float 是多少？double 赋给 float 时是舍入还是截断？char 有多少位？

`<limits>` 中提供的 `numeric_limits` 模板特化给出了这些问题的答案。例如：

```cpp
void f(double d, int i)
{
    char classification[numeric_limits<unsigned char>::max()];
    if (numeric_limits<unsigned char>::digits == numeric_limits<char>::digits) {
        // chars are unsigned
    }
    if (i < numeric_limits<short>::min() || numeric_limits<short>::max() < i) { // i cannot be stored in a short without loss of digits
    }

    if (0 < d && d < numeric_limits<double>::epsilon()) d = 0;

    if (numeric_limits<Quad>::is_specialized) {
        // limits information is available for type Quad
    }
}
```

每个特化都为其参数类型提供相关信息。因此，通用 `numeric_limits` 模板只是一组常量和 `constexpr` 函数的记号句柄：

```cpp
template<typename T>
class numeric_limits {
public:

    static const bool is_specialized = false; // is information available for numeric_limits<T>?
    // ... uninteresting defaults ...
};
```

真正的信息位于特化中。标准库的每个实现都为每个基本数值类型（字符类型、整数类型、浮点类型和 `bool`）提供 `numeric_limits` 的特化，但不为任何其他可能的候选类型提供，例如 `void`、枚举或库类型（如 `complex<double>`）。

对于 `char` 这样的整数类型，只有少数信息是有意义的。下面是一个 `numeric_limits<char>` 的示例，该实现中 `char` 有 8 位且为有符号类型：

```cpp
template<>
class numeric_limits<char> {
public:

    static const bool is_specialized = true; // yes, we have information
    static const int digits = 7; // number of bits (“binary digits”) excluding sign
    static const bool is_signed = true; // this implementation has char signed
    static const bool is_integer = true; // char is an integral type
    static constexpr char min() noexcept { return -128; } // smallest value
    static constexpr char max() noexcept { return 127; } // largest value
    // lots of declarations not relevant to a char
};
```

`numeric_limits` 的大多数成员旨在描述浮点数。例如，下面描述一种可能的 `float` 实现：
