
```cpp
explicit codec_byname(const char*, size_t refs = 0);

explicit codec_byname(const string&, size_t refs = 0);

protected:

  ~codec_byname();

};
```

# 22.4.2 数值分类 [category.numeric]

- `num_get<>` 和 `num_put<>` 类处理数值格式化和解析。为多种类型提供了虚函数。实现（可能不需要）将较小类型的提取委托给较大类型的提取器。
- 在 22.4.2 子类中 `num_put` 和 `num_get` 的所有成员规范仅适用于表 81 和 82 (2.3.1) 中要求的的特化版本，即 `num_get<char>`、`num_get<char, InputIterator>`、`num_put<char>`、`num_put<char, OutputIterator>`。这些特化版本引用 `ios_base` 参数用于格式规范，引用其浸入的 locale（imbued locale）来识别所有数值偏好，并引用 `ctype` 来执行字符提取。标准迭代器的成员函数使用 `num_get<>` 和 `num_put<>` 成员函数对数值值进行格式化和解析

## 22.4.2.1 模板类 num_get [locale.num

```cpp
namespace std {

template <class charT, class InputIterator = istream_iterator<charT>>

class num_get : public locale::facet {

public:

  typedef charT char_type;

  typedef InputIterator iterator_type;

  explicit num_get(size_t refs = 0);

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, bool& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, long& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, long long& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, unsigned short& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, unsigned& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, unsigned long& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, float& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, double& v) const;

  iterator_type get(iterator_type in, iterator_type end, ios_base& base,
      ios_base::iostate& err, long double& v) const;

245 正确解析 "-1" 到，例如 `unsigned short` 需要至少的

```cpp
iterator_type get(iterator_type in, iterator_type end, ios_base,
ios_base::iostate& err, void* v) const;

static locale::id id;
protected:
    ~num_get();
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, bool& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, long& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, long long& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, unsigned short& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, unsigned& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, unsigned long& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, float& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, double& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, long double& v) const;
    virtual iterator_type do_get(iterator_type in, iterator_type end, ios_base,
    ios_base::iostate& err, void* v) const;
    };
```

`facet` `num_get` 用于从输入序列中解析数值。

# 22.4.2.1 num_get 成员

`facet.num_get.members`

§ 22.4.2.1

715

# ISO/IEC N4296

`iter_type get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, void* val) const;`

返回：`get_do(in, end, str, err, val);`

## 22.4.2.1 num get 虚函数

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, long& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, long long& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, unsigned short& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, unsigned& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, int& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, long long& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, float& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, double& val) const;`

`iter_type_do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, void* val) const;`

`facet.num.get(virtuals)`

> 影响：从 `in` 中读取字符，并根据 `str.flags()` 和 `use_facet<ctype<char>>>(loc)` 进行解释，其中 `loc` 是 `str.getloc(loc)`。

该操作分为三个阶段的细节

- 阶段 1：确定转换规范

- 阶段 2：从 `in` 中提取字符，并根据阶段 1 确定的转换规范所需的格式确定相应的 `char` 值

- 阶段 3：存储结果

阶段 1：该函数通过以下方式初始化局部变量：

```cpp
ftmfags flags = str.flags();
ftmfags basefield = (flags & ios_base::basefield);
ftmfags uppercase = (flags & ios_base::uppercase);
ftmfags boolalpha = (flags & ios_base::boolalpha);
```

对于转换为整数类型，函数按照表 85 所示确定整数转换规范。按照顺序，应用第一个条件为真的行。

表 85 — 整数转换

| 状态 | stdio 等效于 |

| :--- | :--- |

| basefield == oct | %o |

| basefield == hex | %X |

| basefield == 0 | %i |

| 有符号整数类型 | %d |

| 无符号整数类型 | %u |

§ 22.4.2.1.2

对于转换为类型时，指示符为 `%g`。

对于转换为 `void`，指示符为 `%p`。

如果需要，则如表 86 所示向转换规范添加长度修饰符。

表 86 — 长度修饰符

| 类型 | 长度修饰符 |

| :--- | :--- |

| short | h |

| unsigned short | h |

| long | 1 |

| unsigned long | 1 |

| long long | 1 |

| unsigned long long | 11 |

| double | 1 |

| long double | L |

**阶段 2：** 如果 `in=end` 则阶段 2 终止。否则，从 `in` 取一个 `charT` 并在满足以下时初始化局部变量：

```cpp
char char_type = *in;
char c = src[find(atoms, sizeof(src) - 1, ct); atoms];
if (ct == use_facet<nump<charT>>(loc).decimal_point()) {
  c = ',';
bool discard = use_facet<nump<charT>>(loc).thousands_sep(src) && use_facet<nump<charT>>(loc).grouping(src).length() != 0;
```

其中 `src` 和 `atoms` 的定义如下：

```cpp
static const char[src] = "0123456789abcdefdefXX--";
char_atoms[sizeof(src)];
use_facet<ctype<charT>>(loc).wididen(src, src + sizeof(src), atoms);
```

对于 `loc` 的每个值：

如果 `discard` 为 true，则 `','` 已经累积，否则 `','` 被忽略。否则，如果 `','` 已经累积，则该字符被丢弃且阶段 2 终止。如果没有被丢弃，则检查 `c` 是否允许作为阶段 1 指定的转换规范的输入字段的下一个字符。如果是，则将其累积。

如果字符被丢弃或累积，则 `in` 通过 `++in` 移动，处理返回阶段 2 的开头。

**阶段 3：** 在阶段 2 中累积的字符序列（字段）根据头文件 `<ctype>` 中声明的 `one` 函数的规则转换为数值。

- 对于有符号整数值，使用函数 `strtol`。

- 对于无符号整数值，使用函数 `strtou`。

- 对于浮点数值，使用函数 `strtod`。

要存储的数值可以是：

- 0，如果转换未能转换整个字段。设置 `ios_base::failbit`。

- 最大正表示值，如果字段表示的值大于 `val` 的表示范围。设置 `ios_base::failbit`。

(3.6) — 最大负表示值（对于无符号整数为 0），如果字段表示的值小于 `val` 的表示范围。设置 `ios_base::failbit`。

(3.7) — 否则为转换的值。

结果存储在 `val` 中。

- 4 检查数字分组。如果是，则检查丢弃的分隔符的位置是否与 `use<nump<char>>(loc)` 一致。

- 5 在任何情况下，阶段 2 终止。

```cpp
iter_type do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, void* val) const;
```

- 6 影响：从 `in` 中读取字符，并根据 `str.flags()` 和 `use_facet<ctype<char>>>(loc)` 进行解释，其中 `loc` 是 `str.getloc(loc)`。

- 7 在任何情况下，阶段 2 终止。

```cpp
iter_type do_get(iter_type in, iter_type end, ios_base& str, ios_base::iostate& err, void* val) const;
```

- 8 如果字符被丢弃或累积，则 `in` 通过 `++in` 移动，处理返回阶段 2 的开头。

- 9 数值存储在 `val` 中。

# ISO/IEC N4296

```cpp
iter_do_put(iter_type out, ios_base& str, char_type fill,
long long val) const;
iter_do_put(iter_type out, ios_base& str, char_type fill,
unsigned long val) const;
iter_do_put(iter_type out, ios_base& str, char_type fill,
unsigned long val) const;
iter_do_put(iter_type out, ios_base& str, char_type fill,
double val) const;
iter_do_put(iter_type out, ios_base& str, char_type fill,
long double val) const;
iter_do_put(iter_type out, ios_base& str, char_type fill,
void* val) const;
```

- 1 效果：将字符写入序列 `out`，并按需格式化 `val`。在接后的描述中，通过以下代码初始化局部变量：

```cpp
local loc = str.getloc();
```

- 2 该操作分为几个阶段的细节：

    - (2.1) 阶段 1：确定一个原始说明符，并假设当前 `loc` 为 "C"，根据该说明符确定 `printf(spec, val)` 将打印的字符（见 27.9.2)。
