
- (2.2) 阶段 2：通过转换，将阶段 1 确定的每个 `char` 转换为一个 `char`，并使用 `use_facet<numpunct<charT>>(str.getloc())` 返回的值和转换来调整转换。

- (2.3) 阶段 3：确定是否需要放置位置。

- (2.4) 阶段 4：将序列插入到 `out` 中。

- 3 每个阶段的详细描述。

- 4 返回：

- 5 阶段 1：阶段 1 的第一步是确定转换说明符。使用局部变量描述此确定过程的表如下：

```cpp
mfflags flags = str.flags();
mfflags basefield = (flags & (ios_base::basefield));
mfflags uppercase = (flags & (ios_base::uppercase));
mfflags floatfield = (flags & (ios_base::floatfield));
mfflags showpoint = (flags & (ios_base::showpoint));
mfflags showbase = (flags & (ios_base::showbase));
```

用于描述阶段 i 的所有变量都是有序的。即，第一条条件为真的行将被应用。没有条件的行在较之前的所有行都不适用时作为默认行为。

对于从字符类型以外的整数类型的转换，函数按照第 87 所示确定整数转换说明符。

对于从浮点类型的转换，函数按照表 88 所示确定浮点转换说明符。

对于从整数类型或浮点类型的转换，按照表 89 所示为转换说明符确定一个长度修饰符。

转换说明符具有根据表 90 所示前置的可选附加限定符。

# 表 87 — 整数转换

| 状态 | stdio 等效于 |
|---|---|
| basefield == ios_base::oct | %o |
| (basefield == ios_base::hex) && !uppercase | %x |
| (basefield == ios_base::hex) | %X |
| 对于有符号整数类型 | %d |
| 对于无符号整数类型 | %u |

# 表 88 — 浮点转换

| 状态 | stdio 等效于 |
|---|---|
| floatfield == ios_base::fixed | %f |
| floatfield == ios_base::scientific && !uppercase | %e |
| floatfield == ios_base::scientific | %E |
| floatfield == (ios_base::fixed | ios_base::scientific) && !uppercase | %a |
| floatfield == (ios_base::fixed | ios_base::scientific) | %A |
| uppercase | %g |
| 其他 | %G |

# 表 89 — 长度修饰符

| 类型 | 长度修饰符 |
|---|---|
| long | 1 |
| long long | 11 |
| unsigned long | 1 |
| unsigned long long | 11 |
| long double | L |
| 其他 | 无 |

对于从浮点类型的转换，如果 `floatfield != (ios_base::fixed | ios_base::scientific)`，则 `str.precision()` 被指定精度。否则，不指定精度。从 `void*` 的转换修饰符是 `%p`。

阶段 1 的表示由调用 `printf(s, val)` 将打印的字符组成，其中 `s` 是上述说明符。**阶段 2**：小数点以外的任何字符都通过 `facet<char>(loc).widen()` 转换为 `char`。局部变量通过以下方式初始化：

```cpp
const numpunct<charT>& punct = use_facet<numpunct<charT>>(str.getloc());
```

对于类型，将 `punct.thousands_sep()` 字符插入到 `punct.grouping()` 返回的结果中，方法见 22.4.3.1。

# 表 90 — 数字转换

| 类型(s) | 状态 | stdio 等效于 |
|---|---|---|
| 整数类型 | flags & showpos | + |
| | flags & showbase | # |
| 浮点类型 | flags & showpos | + |
| | flags & showpoint | # |

小数点字符(.) 被 `punct.decimal_point()` 替换。

# 阶段 3 - 局部变量初始化为

```cpp
fmtflags adjustfield = (flags & (ios_base::adjustfield));
```

任何填充的位置由表 91 决定。

表 91 — 填充

| 状态 | 位置 |
|--- |--- |
| adjustfield == ios_base::left | 填充后 |
| adjustfield == ios_base::right | 填充前 |
| adjustfield == internal 且表示中出现符号 | 填充符号 |
| adjustfield == internal 且阶段 1 以 0x 或 0X 开始 | 填充 x 或 X 后 |
| 其他 | 填充前 |

如果 `str.width()` 非零且阶段 2 之后的 `charT` 数量小于 `str.width()`，则在填充指示的位置添加 `fill` 字符，使序列长度达到 `str.width()`。

# 阶段 4: 将序列插入到 `out` 中。

返回：如果 `str.width()` 非零且阶段 2 之后的 `charT` 数量小于 `str.width()`，则在填充指示的位置添加 `fill` 字符，使序列长度达到 `str.width()`。

阶段 4: 将序列插入到 `out` 中。

返回：如果 `str.width()` 非零且阶段 2 之后的 `charT` 数量小于 `str.width()`，则在填充指示的位置添加 `fill` 字符到

```cpp
string_type s = use_facet<numpunct<charT>>(loc).truename();
```

然后将 `s` 的每个字符插入到

```cpp
*out++ = c
```

```cpp
do_put(iter_type out, ios_base& str, char_type fill,
bool val) {
```
# 22.4.3.1 类 numpunct

```cpp
namespace std {
template <class charT>
class numpunct : public locale::facet {
public:
    explicit numpunct(size_t refs = 0);
char_type decimal_point();
char_type thousands_sep();
string_type grouping()
;
protected:
    ~numpunct();
    virtual char_type do_decimal_point();
    virtual char_type do_thousands_sep();
    virtual string_type do_grouping();
    virtual string_type do_truename();
    virtual string_type do_falsename();
};
```
1 `numpunct<charT>` 指定数字标点。表 81 (22.3.1.1) 中的特化为 `numpunct<charT, charT>` 提供了 "C" 数字格式，即它们包含了等于 "C" locale 信息或通过调用 `widen` 的宽字符对应项。

2 数字格式的语法如下，其中 `digit` 代表由 `intflags` 指定的进制，`thousands-sep` 和 `decimal-point` 是相应 `numpunct<charT>` 成员的结果。整数具有如下：

```cpp
integer      = [sign units]
sign         = '+' | '-'
pyminus      = '\'' | units [thousands-sep units]
digits       = digits [digits]
```

而浮点值具有：
```cpp
floatall     = [sign units [decimal-point [digits]]] [e [sign] digits] |
sign         = 'e' | 'E'
decimal-point = digits
```

其中千分位分隔符之间的数字数量由 `do_grouping()` 指定。对于解析，`digits` 部分不包含千分位分隔符，不应用分组约束。

# 22.4.3.1. numpunct 成员 [facet.numpunct.members]

- `char_type do_decimal_point() const;`
返回: `do_decimal_point()`

- `char_type do_thousands_sep() const;`
返回: `do_thousands_sep()`

- `string_type do_grouping() const;`
返回: `do_grouping()`

- `string_type truename() const;`
`string_type falsename() const;`
返回: 分别返回 `do_truename()` 或 `do_falsename()`。

## ISO/IEC numpunct 虚函数

### 22.4.3.1.2 [facet.numpunct.virtuals]

`char_type do_decimal_point() const;`

- 1 返回：一个用于小数点基数分隔符的字符。所需的特化版本返回 ' ' 或 'L'。

`char_type do_thousands_sep() const;`

- 2 返回：一个用于数字分组分隔符的字符。所需的特化版本返回 ' ' 或 'L'。

`string do_grouping() const;`

- 3 返回：作为整数值向量的 `basic_string<char> vec`，其中每个元素 `vec[i]` 代表位置 `i` 的数字位数，从 0 开始是最右侧组。如果 `vec.size() <= 1`，则该数字与分组 (i-1) 相同：如果 `(i<0 || vec[i]<=0 || vec[1]<CHAR_MAX)`，则数字分组的大小不受限制。 47 因此，字符串 "003" 指定每组 3 位数字，而 "3" 可能表示每组 51 (!) 位，因为 51 是 "03" 的 ASCII 值。

- 4 所需特化版本返回空字符串，表示无分组。

`string_type do_true() const;`
`string_type do_falsename() const;`

- 5 返回：一个分别代表布尔值 true 或 false 名称的字符串。分别为 L"true" 和 L"false"。

- 6 在类实现中，这些名称为 "true" 和 "false"，或者 L"true" 和 L"false"。

## 22.4.3.2 类模板 numpunct_byname [locale.numpunct.byname]

```cpp
namespace std {
  template <char T>
  class numpunct_byname : public numpunct<char> {
    // 此类针对 char 和 wchar_t 进行了特化。
  public:
    typedef charT char_type;
    typedef basic_string<char> string_type;
    explicit numpunct_byname(const char*, size_t refs = 0);
    explicit numpunct_byname(const string&, size_t refs = 0);
  protected:
    ~numpunct_byname();
  };
};
```

## 22.4.4 排序范类 [category.collate]

### 22.4.4.1 类模板 collate [locale.collate]

```cpp
namespace std {
  template <char T>
  class collate : public locale::facet {
  public:
    typedef charT char_type;
    typedef basic_string<char> string_type;
    explicit collate(size_t refs = 0);
  };
```
```cpp
int compare(const charT* low1, const charT* high1,
const charT* low2, const charT* high2) const;
string_type transform(const charT* low, const charT* high) const;
long hash(const charT* low, const charT* high) const;
```
```cpp
static locale::id id;
protected:
-collate();
virtual int do_compare(const charT* low1, const charT* high1,
const charT* low2, const charT* high2) const;
virtual string_type do_transform(const charT* low, const charT* high) const;
virtual long do_hash(const charT* low, const charT* high) const;
};
```

- 1. 类 `collate<char, wchar_t>` 提供了用于字符串排序（比较）和哈希的功能。本地区域函数模板 `operator()` 使用 `collate` 变畴（facet），允许本地区域直接作为标准算法的谓词（第 25 节），并包含对字符串的操作。表 81 ((22.3.1.1.1)) 中需的特化版本，即 `collate<char>` 和 `collate<wchar_t>`，应用了字典排序 (25.4.8)。

- 2. 每个函数比较范围在 `[low,high)` 内的字符字符串。

### 22.4.4.1.1 成员

> [locale.collate.members]

```cpp
int compare(const charT* low1, const charT* high1,
const charT* low2, const charT* high2) const;
```

- 1 返回：`do_compare(low1, low2, high2)`

```cpp
string_type transform(const charT* low, const charT* high) const;
```

- 2 返回：`do_transform(low, high)`

```cpp
long hash(const charT* low, const charT* high) const;
```

- 3 返回：`do_hash(low, high)`

### 22.4.4.1.2 collate 虚函数

> [locale.collate.virtual]

```cpp
int do_compare(const charT* low1, const charT* high1,
const charT* low2, const charT* high2) const;
```

- 1 如果第一个字符串大于第二个，则返回；较小则返回 -1，否则如此。表 81 ((22.3.1.1.1)) 中需的特化版本，即 `collate<char>` 和 `collate<wchar_t>`，实现了字典排序 (25.4.8)。

```cpp
string_type transform(const charT* low, const charT* high) const;
```

- 2 返回：一个 `string<char>` 值，其在字典顺序上与另一个字符串调用 `transform()` 的结果比较，与对两个字符串调用 `do_compare()` 的结果相同。

```cpp
long hash(const charT* low, const charT* high) const;
```

- 3 返回一个整数，当 `do_compare()` 传入字符串时返回 0（相等）。注意：结果等于另一个字符串的概率应该非常小，接近 `numeric_limits<unsigned long>::max()`。

```cpp
namespace std {
  template <char T>
  class collate_byname : public collate<char> {
    public:
      typedef basic_string<char> string_type;
      explicit collate_byname(const charT*, size_t refs = 0);
```
