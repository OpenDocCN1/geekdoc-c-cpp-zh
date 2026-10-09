
```cpp
namespace std {
template<class charT, class Iterator = istream_iterator<charT>>
class num_get : public locale::facet {
public:
    using char_type = charT;
    using iter_type = Iterator;

    explicit num_get(size_t ref = 0);

    iter_type get(iter_type in_in, iter_type in_end, ios_base, bool& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, long& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, long long& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, unsigned short& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, unsigned int& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, long long& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, float& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, double& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, long double& v) const,
                  ios_base::iostate& err);
    iter_type get(iter_type in_in, iter_type in_end, ios_base, void* v) const,
                  ios_base::iostate& err);

    static locale::id id;

protected:
    num_get();
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, bool& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, long& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, long long& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, unsigned short& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, unsigned int& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, long long& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, float& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, double& v) const,
                              ios_base::iostate& err);
    virtual iter_type do_get(iter_type in_in, iter_type in_end, ios_base, long double& v) const,
                              ios_base::iostate& err);
};
```

### 28.4.3.2 成员

- 单元 facet 用于从输入序列（如流）中解析值。

- 返回：`do_get(in, end, str, err)`。

### 28.4.3.3 虚函数

- 影响：从 `in` 中读取字符，根据 `flags()`、`ctype<charT>(loc)` 对进行解释，其中 `loc` 是 ISO/IEC 14882:2020 标准。

- 各阶段的详细信息如下。

#### 阶段 1：确定转换说明符

该函数通过以下方式初始化局部变量：

```cpp
fmtflags flags = str_flags();
fmtflags basefield = (flags & ios_base::basefield);
fmtflags uppercase = (flags & ios_base::uppercase);
fmtflags boolalpha = (flags & ios_base::boolalpha);
```

对于转换为整数类型，函数确定表 106 所示的整数规范。即条件为真的第一行。

对于转换为浮点数类型，说明符为 `%g`。

对于转换为 `void*`，说明符为 `%p`。

如果需要，则如表 107 所示向转换规范中添加长度修饰符。

表 106：整数转换器

| 状态 | stdio 等效于 |

|---|---|

| basefield == oct | %o |

| basefield == hex | %X |

| basefield == 0 | %i |

| 有符号整数类型 | %d |

| 无符号整数类型 | %u |

表 107：长度修饰符

| 类型 | 长度修饰符 |

|---|---|

| short | h |

| unsigned short | h |

| long | 1 |

| unsigned long | 1 |

| long long | 11 |

| unsigned long long | 11 |

| double | 1 |

| long double | L |

#### 阶段 2：从 in 中提取字符

如果 == end，阶段 2 终止。否则从 `in` 取一个 `charT` 并通过以下方式初始化局部变量：

```cpp
char_type c = *in;
if (src = use_find(atoms, sizeof(src) - 1, c); atoms);
if (c != use_facet(numpcount<charT>(loc).decimal_point())
c = ',';
bool discard = false;
ct = use_facet(numpcount<charT>(loc).thousands_sep();
&& c != use_facet(numpcount<charT>(loc).length() != 0;
```

其中值 `src` 和 `atoms` 的定义为：

```cpp
static const char src[] = "0123456789abcdefABCDEF-";
char_type atoms[] = sizeof(src);
use_facet<charT>(loc).width(src, src + sizeof(src), atoms);
```

对于此值 `c`。

如果 `discard`，则 ' ' 尚未积累，记录了字符的位置，但该字符被忽略。否则，如果 '.' 已经积累，则该字符被丢弃且阶段 2 终止。

# ISO/IEC 14882:2020(E)

进行检查以确定 `c` 是否为阶段 1 返回的转换的输入的下一个字符。如果是，则对其进行累积。

如果字符被丢弃或累积，则处理指针递增 `++` 并返回阶段 2 的开始。

阶段 3：在阶段 2 中遇到的字符序列（字段）根据头文件 `<cstdlib>` 中声明的函数规则转换为数值值：

- (3.1) 对于有符号整数值，使用函数 `strtol`

- (3.2) 对于无符号整数值，使用函数 `strtoull`

- (3.3) 对于浮点数值，使用函数 `strtof`

- (3.4) 对于 double 值，使用函数 `strtod`

- (3.5) 对于 long double 值，使用函数 `strtold`

要存储的数值可以是以下值之一：

- (3.6) 零，如果转换函数没有转换整个字段

- (3.7) 最大的（或最小的）代表值，如果字段转换为有符号整数类型时表示的值太大（正或负），无法在 `val` 中表示。

- (3.8) 最大的可表示值，如果字段转换为无符号整数时表示的值无法在 `val` 中表示。

- (3.9) 转换后的值，其他。

结果存储在 `val` 中。如果转换函数没有转换整个字段，或者字段范围超出代表值的范围，则将 `ios_base::fail` 赋值给 `err`。

4 检查数字分组。即分隔符的位置与 `use_facet<nump<char>>(10).group()` 保持一致。如果不一致，则将 `ios_base::fail` 赋值给 `err`。

5 在任何情况下，如果阶段 2 处理因测试 -- 而结束，则 `err == ios_base::eof`。

```cpp
iter_type do_get(iter_type in, iter_type end, ios_base base, ios::oststate& err, bool val) {
```

6 影响：如果 `(str.fail() || ios_base::badalpha)`，则输入将像处理 `long` 一样继续；如果 `val` 存储为 `true`，则值的确定如下：如果要存储的值为 `0`，则为 `false`；如果值为 `1`，则为 `true`；其他情况存储 `true` 且 `ios_base::eofbit == err`。

7 其他序列通过调用由 `use_facet<nump<char>>(str.get())` 获取的 facet 的成员 `fasename()` 和 `truename()` 被定义为“如果”。获取范围 `(in, end)` 内的连续字符，并且仅在识别唯一匹配的需要时才与序列中的相应位置进行匹配。仅在需要匹配时才比较输入 `end`。如果匹配到目标序列，则将 `val` 设置为相应的值。如果存储 `false` 并将 `ios_base::failbit` 赋值给 `err`，则 `val` 被设置并设置为 `false`。

迭代器指向最后一个成功匹配的字符的后一个点。如果没有找到目标，则将其设置为 `str.end()` 或 `err`；如果匹配到另一个目标，则将其设置为该目标 `(in end)`。如果没有匹配到任何目标，则将其设置为 `str::failbit`；如果失败原因是 `(in == end)`，则设置为 `str::eofbit`。

[示例 1：对于目标："a" 和 `false`："abb"，输入序列 "a" 的 `val == true` 且 `err == ''` 元素；输入序列 "abb" 产生 `err == str.failbit`，并在 'c' 元素处结束。对于目标 "1" 和 `false`："0"，输入序列 "1" 产生 `val == true` 且 `err == str.goodbit`。对于空序列 ("")，任何输入序列都会产生 `err == str.goodbit`。]

返回值：in

# 28.4.3.3 类模板 `numput`

# 28.4.3.1 通用

```cpp evennamespace std {
template<class charT, class OutputIterator = istambuf_iterator<charT>> class num_put : public locale::facet {
public:
using char_type = charT;
```

[locale.num.put] [locale.num.put.general]

§ 28.4.3.1 ISO/IEC 2020 – 所有权利保留 1357

ISO/IEC 14882:2020(E)

using iter_type = OutputIterator;

explicit num_put(iter_type s, int refs = 0);

```cpp
iter_type type_put(iter_type s, ios_base& f, char_type fill, bool v) const;
iter_type type_put(iter_type s, ios_base& f, char_type fill, long v) const;
iter_type type_put(iter_type s, ios_base& f, char_type fill, long long v) const;
iter_type type_put(iter_type s, ios_base& f, char_type fill, unsigned long v) const;
iter_type type_put(iter_type s, ios_base& f, char_type fill, unsigned long long v) const;
iter_type type_put(iter_type s, ios_base& f, char_type fill, double v) const;
iter_type type_put(iter_type s, ios_base& f, char_type fill, long double v) const;
iter_type type_put(iter_type s, ios_base& f, char_type fill, void* v) const;

static locale _id;

-num_put();

```cpp

virtual iter_type do_put(iter_type, ios_base&, char_type fill, bool v) const;

virtual iter_type do_put(iter_type, ios_base&, char_type fill, long v) const;

virtual iter_type do_put(iter_type, ios_base&, char_type fill, long long v) const;

virtual iter_type do_put(iter_type, ios_base&, char_type fill, unsigned long v) const;

virtual iter_type do_put(iter_type, ios_base&, char_type fill, unsigned long long v) const;

virtual iter_type do_put(iter_type, ios_base&, char_type fill, double v) const;

virtual iter_type do_put(iter_type, ios_base&, char_type fill, long double v) const;

virtual iter_type do_put(iter_type, ios_base&, char_type fill, void* v) const;
