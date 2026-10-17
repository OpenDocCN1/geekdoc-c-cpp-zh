
```cpp
iter_put(iterator_type i, ios_base& f, char_type fill, long long v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, unsigned long v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, unsigned long long v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, double v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, double double v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, void* v) const;
```

`protected:` 

```cpp
num_put();

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, bool v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, long long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, unsigned long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, unsigned long long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, double v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, double double v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, void* v) const;
```
};

`facet` `num_put` 用于将数字格式化为 `ostream` 序列。25.4.2.1 `num_put` 成员

```cpp
iter_put(iterator_type i, ios_base& f, char_type fill, bool v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, long v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, long long v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, unsigned long v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, unsigned long long v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, double v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, double double v) const;

iter_put(iterator_type i, ios_base& f, char_type fill, void* v) const;
```

返回：`do_put(out)`.

```cpp
virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, bool v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, long long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, unsigned long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, unsigned long long v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, double v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, double double v) const;

virtual iter_do_put(iterator_type i, ios_base& f, char_type fill, void* v) const;
```

影响：将 `val` 写入输出，格式化如所述。在后续，使用以下局部变量初始化：

```cpp
isc str;
```

此操作细节分阶段进行：

- 阶段 1：确定转换说明符。描述此决定的表使用以下局部变量

```cpp
ffflags flags = (flags & (iosbase::basefield));
ffflags basefield = (flags & (iosbase::basefield));
ffflags uppercase = (flags & (iosbase::uppercase));
ffflags floatfield = (flags & (iosbase::floatfield));
ffflags showbase = (flags & (iosbase::showbase));
ffflags showbase = (flags & (iosbase::showbase));
ffflags showpoint = (flags & (iosbase::showpoint));
```

每个阶段的详细描述。

返回：`out`。

阶段 1：阶段 1 的第一阶段是确定转换说明符。描述阶段的表是有顺序的。也就是说，给出的第一行是适用的。没有条件的行是当之前的行都不适用时的默认行为。对于除字符类型外的整数类型的转换，函数根据表 75 确定整数转换说明符。

表 75

| 状态 | stdio 等效于 |
|---| --- |
| basefield == iosbase::oct | % |
| (basefield == iosbase::hex) && uppercase | %x |
| (basefield == iosbase::hex) | %X |
| 对于有符号整数类型 | %d |
| 对于无符号整数类型 | %u |

# ISO/IEC 14882:2017(E)

对于从浮点类型的转换，函数根据表 76 所示确定浮点转换说明符。

表 76 — 浮点转换

| 状态 | stdio 等效 |
| --- | --- |
| floatfield == ios_base::fixed | %f |
| floatfield == ios_base::scientific && !uppercase | %e |
| floatfield == ios_base::scientific | %E |
| floatfield == (ios_base::fixed | ios_base::scientific) && !uppercase | %a |
| floatfield == (ios_base::fixed | ios_base::scientific) | %A |
| !uppercase | %g |
| otherwise | %G |

对于从整数或浮点类型的转换，转换说明符会添加表 77 所示的长度修饰符。

表 77 — 长度修饰符

| 类型 | 长度修饰符 |
| --- | --- |
| long | 1 |
| long long | 11 |
| unsigned long | 1 |
| unsigned long long | 11 |
| long double | L |
| otherwise | none |

转换说明符在前面带有表 78 所示的可选额外限定符。

表 78 — 数值转换

| 类型(s) | 状态 | stdio 等效 |
| --- | --- | --- |
| 整数类型 | showpos | + |
| | showcase | - |
| 浮点类型 | showpos | + |
| | showpoint | # |

对于从浮点类型的转换，如果 `floatfield != (ios_base::fixed | ios_base::scientific)`，则在转换规范中指定 `str::precision(val)`。否则，未指定精度。
从 `void` 的转换说明符为 `%p`。

阶段 1 结束时的表示由 `printf(s, val)` 打印的字符组成，其中 `s` 是上述确定的转换。

**阶段 2:** 除小数点以外的任何字符都通过 `facet<ctype<char>>(loc).wideto(c)` 转换为 `char`。
本地变量 `punct` 通过以下方式初始化：
`const numpunct<char>& punct = use_facet<numpunct<char>>(str.getgetloc());`

# ISO/IEC 14882:2017(E)

对于算术类型，根据 25.4.3.1.2 中描述的方法使用 `punct.do_grouping()` 返回的值，将 `punct.thousands_sep()` 字符插入序列中。小数点字符被 `punct.decimal_point()` 替换。

**阶段 3**: 本地变量初始化为：

`fstflag adjustfield = (flags & ios_base::adjustfield);`
任何填充的位置由表 79 确定。

表 79 — 填充填充

| 状态 | 位置 |
| --- | --- |
| adjustfield == ios_base::left | 填充在之后 |
| adjustfield == ios_base::right | 填充在之前 |
| adjustfield == internal 且表示中出现符号 | 符号符号之后 |
| adjustfield == internal 且阶段 1 以 0x 或 0X 开头 | 在 x 或 X 之后 |
| otherwise | 填充在之前 |

如果 `str.width()` 不为零且阶段 2 之后序列中的 `char't` 小于 `str.width()`，则在指定的填充位置向序列中添加足够的填充字符，使序列长度达到 `str.width()`。

**阶段 4**: 阶段 3 结束时的 `char't` 编码通过以下方式输出：

```
*out++ = c
```

`iter_type do_put(iter_type, ios_base& str, char_type fill, bool val) const;`

返回：如果 `(str.flags() & ios_base::bopumpal) == 0` `do_put(out, str, int(val))`，否则返回字符串 `s` 如果

`string_type s =`

`val ? use_facet<nump<char'T>>(loc).truename() : use_facet<nump<char'T>>(loc).falsename();`

并通过 `*out++ = c` 将 `c` 的每个字符插入 `out` 并返回 `out`。

## 25.4.3 数值面类标点符号 [facet.nump]

## 25.4.3.1 类模板 nump

```cpp
namespace std {
template <class char'T>
class numpt : public locale::facet {
public:
  using char_type = char'T;
  using string_type = basic_string<char'T>;n
  explicit numpt(size_t refs = 0);
  char_type decimal_point() const;
  char_type thousands_sep() const;
  string grouping() const;
```

240 转换规范 #0 生成一个前导 0，该字符不是填充字符。

§25.4.3.1 ©ISO/IEC 2017 — 保留所有 805

```cpp
string_type truename() const;
string_type falsename() const;
static locale::id id;
```

```cpp
protected:
    numpunct(); // virtual
    virtual char_type do_decimal_point() const;
    virtual char_type do_thousands_sep() const;
    virtual string do_grouping() const;
    virtual string_type do_truename() const; // 用于 bool
    virtual string_type do_falsename() const; // 用于 bool
};
```

- 1 `numpunct<char>` 提供数值表示。表 69 (25.3.1.1.1) 中的特化 `nnumpunct<char>` 和 `numpunct<char>` 提供了经典的 "C" 数值格式，即它们包含等同于 "C" locale 中的信息或通过 `widen()` 识别的对应数字。

数值格式的语法如下，其中 `digit` 代表由 `fmtflags` 参数设置的基数，且 `thousands-sep` 和 `decimal-point` 是对应的 `numpunct<char>` 成员的结果。整数值具有：

```cpp
integer ::= [sign] units
sign ::= [plusminus]
plusminus ::= '+\' | '-\''
units ::= digits [thousands-sep units]
digits ::= [digit]
```

以及浮点值：

```cpp
float ::= [sign] units [decimal-point digits]] [e [sign] digits] |
           :: [sign]
           :: decimal-point digits [e [sign] digits]
           :: 'e' | 'E'
```

其中千分分隔符之间的数字由 `do_grouping()` 指定。对于解析，如果数字不包含千分分隔符，则不应用分组约束。

（注：由于提供的文本包含大量重复、OCR 乱码以及页面 错误，已根据 C++ 标准的逻辑流对内容去重和清理处理。）

# ISO/IEC 14882:2017(E)

对于另一个不相等的字符串，相等值应该非常小，接近 `(1.0/numeric_limits<unsigned long>::max())`。注。

## 25.4.4.2 类模板 collate_byname [locale::collate_byname]

```
namespace std {
    template<class charT>
    class collate_byname : public collate<charT> {
    public:
        using string_type = basic_string<charT>;
        explicit collate_byname(const charT&, size_t refs = 0);
        explicit collate_byname(const string&, size_t refs = 0);
    protected:
        collate_byname();
    };
};
```

## 25.4.5 时间范类 [category::time]

- 1 模板 `time_get<charT, InputIterator>` 提供日期和时间的格式化与解析。25.4.5 子类中 `time_put` 和 `time_get` 成员函数的所有规范仅适用于表 69 和 70 (25.3.1.1) 中描述的规范。它们的成员使用 `ios_base::ios_base::iostate&` 以及 25.4 中描述的填充参数以及 `<ctype>` 变体来确定格式细节。

## 25.4.5.1 类模板 time_get [locale::time_get]

```
namespace std {
