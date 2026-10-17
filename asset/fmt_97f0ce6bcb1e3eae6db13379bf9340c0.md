
2 当 `none_base:space` 或 `none_base:one` 作为格式的最后一个元素出现时，会消耗空白；否则，当 `none_base:space` 出现在格式的初始元素中，至少需要一个空格。当 `none_base:none` 出现在格式的任何初始元素中时，允许但不强制空白。如果 `str.flag(show_currency)` 为 false，则货币符号是可选的，且仅当其字符添加到结果中时才会被消耗；否则，忽略货币符号。

3 如果 `mp_positive_sign()` 返回的字符串或 `mp_negative_sign()` 返回的字符串中的第一个字符（如果有）在格式的指示位置处被符号识别，则它会被消耗，字符串中的任何剩余字符在所有其他格式组件之后都是必须的。例如：如果 `show` 关闭或 `neg` 为空，则货币符号是可选的，如果没有检测到符号，则结果不为空。否则，如果符号存在，指示位置必须匹配 `neg` 或 `pos` 的第一个字符，并且如果结果中 `pos` 的第一个字符等于 `neg` 的第一个字符，或者两者都为空，则结果为正号。

4 货币组件中的数字被提取并按它们出现的顺序放入 `digits`，或放入字符缓冲区 `buf1` 以转换为单位的值，且仅当结果为负时由一个负号前。。值单位的产生方式类似于：

```cpp
for (int i = 0; i < n; ++)
buf1[i] = src.find(atoms,atoms+sizeof(src), buf1[i]) - atoms);
buf2[m] = 0;
sscanf(buf2,"LF");
```

其中 `n` 是放入 `buf1` 的字符数，`buf2` 是一个字符缓冲区，值 `src` 和 `atoms` 的定义如下：

```cpp
static const char src = "0123456789-";
char atoms[sizeof(src)];
```

返回一个指向有效货币格式最后一个识别字符之后的迭代器。

## 25.4.6.2 类 money_put

[locale.money]

```cpp
namespace std {
template <class charT, class OutputIterator = ostreambuf_iterator<char>>
class money_put : locale::facet {
public:
  using char_type = char;
  using iter_type = OutputIterator;
```

## ISO/IEC 14882:2017(E)

```cpp
using string_type = basic_string<charT>;

explicit money_put(size_t refs = 0);

iter_type put(iter_type s, bool intl, ios_base& f,
    char_type fill, long double units) const;
iter_type put(iter_type s, bool intl, ios_base& f,
    char_type fill, const string_type& type_q) const;

static locale_type::id id;

protected:
    -money_put();
    virtual iter_type do_put(iter_type, bool, ios_base&, char_type fill,
        long double units) const;
    virtual iter_type do_put(iter_type, bool, ios_base&, char_type fill,
        const string_type& type_q) const;
```

## 25.4.6.2.1 money_put [locale.money.put.members]

```cpp
iter_type put(iter_type s, bool intl, ios_base& f, char_type fill, long double count) const;
iter_type put(iter_type s, bool intl, ios_base& f, char_type fill, const string_type& type_q) const;
```

返回: `do_put(s, intl, f, loc)`.

## 25.4.6.2.2 money_put 虚函数 [locale.money.put.virtual]

```cpp
iter_type do_put(iter_type s, bool intl, ios_base& str,
    char_type fill, long double units) const;
iter_type do_put(iter_type s, bool intl, ios_base& str,
    char_type fill, const string_type& type_q) const;
```

> 影响：字符转换为由 `money_put<charT, Intl>` facet 引用指定的格式，以及通过从 `get_facet(str).flags()` 获取的 locale 提取的 `type<char>` facet 引用的字符映射。如果参数转换为字符序列，且具有 `ct.widen(bufi, bufi + sprint(buf, buf2))`（对于字符缓冲区，如果 `digits` 或 `buf2` 中的第一个字符等于 `ct.widen('-')`），则使用的模式是 `mp.neg_format()` 的结果；否则，模式为 `mp.pos_format()`。数字字符被写入，带有格式指定的千分位分隔符和小数点。它们出现在（可选的前导符号之后）数字或 `buf2`。在 `digits` 中，可选的前导符号（包括非数字字符）最后添加。

> 备注：当且仅当 `(str.flags() & str.showbase)` 为非零时，会生成货币符号。如果指定格式生成的字符数少于条目处 `str.width()` 返回的值，则需要 `fill` 的副本来填充指定宽度。对于等于 `(str.flags() & str.adjustfield)` 的值，如果 `(af == str.integral)` 为真，则 `fill` 字符放置在格式模式中出现无或空格的位置；否则，如果 `(af == str.left)` 为真，则它们被放置在其他字符之后。[注：通过格式模式和标志值的某些组合，可能会产生不使用 `money_get<>` 解析的输出]

## § 25.4.6.2 ISO/IEC 14882:2017(E)

识别出有效序列，不改变 `err`；否则将 `err` 设置为 `err|str.failbit`，如果没有更多可用字符，则设置为 `err|str.failbit|str.eofbit`，且不改变单位或数字。`units` 返回的模式或可能由负号（或数字）开头的数字序列。例如：在美国区域设置中，序列 `$1,056.23` 对于 `units` 将产生 `105623`，对于 `digits` 将产生 `"105623"`—这是 `digits` 中的一个示例。如果 `mp.grouping()` 表示不允许出现空格，则此类分组是可选的；如果存在，则在读取所有格式组件后检查其位置是否正确。

# ISO/IEC 14882:2017(E)

`string_type_do_curr_symbol()` const;

返回：一个作为货币标识符使用的字符串。253

`string_type_do_positive_sign()` const;

`string_type_do_negative_sign()` const;

返回：`do_positive_sign()` 返回用于表示正货币价值的字符串：254

`do_negative_sign()` 返回用于表示负值的字符串。

`int do_frac_digits()` const;

返回：十进制基数分隔的数字个数（如果有的话）。255

`pattern do_pos_format()` const;

`pattern do_neg_format()` const;

返回：表 70 (25.3.1.1) 中的特化版本，许多 `moneypunct<char>, moneypunct<char_t, true>` 返回一个类型为 `<char_t, true>` 的对象，该对象由 `{symbol, sign, name, value}` 初始化。256

## 25.4.6 类模板 moneypunct_bname

```cpp
namespace std {
    template<class charT, bool Int = false>
    class moneypunct_bname : public moneypunct<charT, Int> {
    public:
        using pattern = money_base::pattern;
        using string_type = basic_string<charT>;

        explicit moneypunct_bname(const char* s, size_t refs = 0);
        explicit moneypunct_bname(const string& s, size_t refs = 0);

    protected:
        moneypunct_bname();

    };
}
```

## 25.4.7 消息检索分类

类 `messages<charT>` 实现了从消息目录中检索字符串。

### 25.4.7.1 类模板 messages

```cpp
namespace std {
    class messages_base {
    public:
        using catalog = unsigned signed integer type;
    };

    template<class charT>
    class messages : public locale::facet, messages_base {
    public:
        using char_type = charT;
        using string_type = basic_string<charT>;
    };
```

> 253 对于国际特化（第二个参数为 true），这通常是四个字符，通常是三个字母和一个空格。

> 254 这是一个空字符串。

> 255 在常见的美国区域设置中，此值是 2。

> 256 注意，`do_curr_sym()` 返回的国际符号通常包含一个空格本身；例如 `"USD *"`。

§ 25.4.7.1

```cpp
explicit messages(size_t refs = 0);

catalog open(const basic_string<char>& fn, const locale& loc) const;
string_type get(catalog c, int set, int msgid,
    const string_type& default) const;
void close(catalog c) const;

static locale::id id;
```

```cpp
protected:
    messages();
    virtual catalog do_open(const basic_string<char>&, const locale& loc) const;
    virtual string_type do_get(catalog int, int set, int msgid,
        const string_type& default) const;
    virtual void do_close(catalog c) const;
```

- 1 可作为 `get` 和 `close` 参数的 `messages_base::catalog` 类型的值，可以通过调用成员函数 `open` 来获取。

## 25.4.7.1 messages 成员 [locale.messages.members]

```cpp
catalog open(const basic_string<char>&, const locale& loc) const;
```

- 1 返回：`do_open(name, loc)`.

```cpp
string_type get(catalog cat, int set, int msgid, string_type& default) const;
```

- 2 返回：`do_get(cat, set, msgid, default)`.

```cpp
void close(catalog cat) const;
```

- 3 影响：调用 `do_close(cat)`。

## 25.4.7.2 messages 虚函数 [locale.messages.virtual]

```cpp
catalog do_open(const basic_string<char>&, const locale& loc) const;
```

- 1 返回：根据实现定义的映射由字符串标识的消息目录，可传递给 `get()`。该结果可以使用直到 `close()`。

- 2 返回：如果无法打开目录，返回一个小于 0 的值。

- 3 备注：在检索消息时，`locale` 参数用于转换。

```cpp
string_type do_get(catalog cat, int set, int msgid, const string_type& default) const;
```
