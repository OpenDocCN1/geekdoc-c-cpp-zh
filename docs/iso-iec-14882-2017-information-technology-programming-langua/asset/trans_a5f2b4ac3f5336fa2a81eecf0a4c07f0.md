

# ISO/IEC 14882:2017(E)

格式字符，由 `time_put<>::put` 用于产生由"%H:%M:%S"` 指定的格式，直到遇到错误或序列结束。

返回：一个迭代器，指向最后一个识别为可能作为有效时间部分的字符之后的后续位置。

```cpp
iter_type_get_date(iter_type s, iter_type end, ios_base& str,
    ios_base::iostate& err, tm t) const;
```

影响：从 s 开始的字符，直到提取出 `struct tm` 结构体以及剩余的 `time_put<>::put` 用于产生以下格式之一的格式字符，或者直到遇到错误。格式取决于 `date_order()` 返回的值，如表 80 所示。

表 80 - do_get_date 影响

| date_order() | 格式 |
|--- | --- |
| no_order | "%%m%d%Y" |
| dmy | "%%d%m%Y" |
| mdy | "%%m%d%Y" |
| ymd | "%%Y%m%d" |
| ydm | "%%Y%d%m" |

实现还可能包含实现定义的格式。

返回：一个迭代器，指向最后一个识别为可能作为有效名称部分的字符之后的后续位置。

```cpp
iter_type_get_weekday(iter_type s, iter_type end, ios_base& str,
    ios_base::iostate& err, tm t) const;
```

```cpp
iter_type_get_month(iter_type s, iter_type end, ios_base& str,
    ios_base::iostate& err, tm t) const;
```

影响：从 s 开始的字符，直到提取出（可能是缩写的）星期或月份名称。如果它发现一个缩写，且其后跟着可能匹配全称的字符，它将继续匹配，直到匹配到全称或失败为止。它设置了相应的 `struct tm` 成员。

返回：一个迭代器，指向最后一个识别为有效名称部分的字符之后的后续位置。

```cpp
iter_type_get_year(iter_type s, iter_type end, ios_base& str,
    ios_base::iostate& err, tm t) const;
```

影响：从 s 开始的字符，直到提取出一个无歧的标识符。是否接受两位数取决于实现，并且（如果接受）它们假设为哪个世纪也取决于实现。`tm->year` 成员据此设置。

返回：一个迭代器，指向最后一个识别为年份标识部分的字符之后的后续位置。

```cpp
iter_type_get_date(iter_type s, iter_type end, ios_base& f,
    ios_base::iostate& err, tm t, char modifier) const;
```

要求：t 指向一个对象。

影响：函数首先评估 `err = ios_base::goodbit`。它从 s 开始读取字符，直到遇到错误，或者它已经提取并分配了这些 `struct tm` 成员，以及任何剩余的格式字符（对应适用于 ISO/IEC 9945 格式日期的转换指令，这些指令通过拼接 `'%'`、当非空时的 `modifier` 字符以及格式字符来实现的）。当拼接未能产生完整的有效指令时，函数保持 t 指向的对象不变并评估 `err |= ios_base::failbit`。当在读取一个字符后 `s == end` 为真时，函数评估 `err |= ios_base::eofbit`。

对于像 `%`、`X` 或调用 `E` 或 `0` 修饰符的 `X` 等复杂转换，当函数无法从输入序列 `[s, end]` 中确定一个或所有 `tm` 成员时，它评估 `err |= ios_base::failbit`。在这种情况下，输出 `tm` 成员的值可能在它们的有效范围之外。

备注：未指定调用 `do_get()` 使用同一个 `struct tm` 对象的地址是更新对象的当前内容还是简单覆盖其内容。可移植程序在调用该函数之前应将对象置零。

返回：一个迭代器，指向对于给定格式和修饰符的有效序列的最后一个字符之后的位置。

## 25.4.5.2 类模板 time_get_byname [locale.time.get.byname]

```cpp
namespace std {
template <class char, class InputIterator = istambuf_iterator<char>>
class time_get_byname : public facet<char, InputIterator> {
public:
    using deorder = time_base::deorder;
    using iter_type = InputIterator;

    explicit time_get_byname(const char*, size_t refs = 0);
    explicit time_get_byname(const string&, size_t refs = 0);

protected:
    time_get_byname();
};
```

## 25.4.5.3 类模板 time_put [locale.time.put]

```cpp
namespace std {
template <class char, class OutputIterator = ostambuf_iterator<char>>
class time_put : public facet {
public:
    using char_type = char;
    using iter_type = OutputIterator;

    explicit time_put(size_t refs = 0);

    // 下面通过其他成员函数实现。
    iter_put(iter_type s, ios_base f, char_type fill, const tm* tmb,
             const char* pattern, const char* pat_end);
    iter_put(iter_type s, ios_base f, char_type fill, const tm* t,
             const char* format, char modifier = 0);

    static const id id;

protected:
    time_put();
    virtual iter_type do_put(iter_type s, ios_base f, char_type type, const tm* t,
                             char format, char modifier) const;
};
```

### 25.4.5.3.1 time_put 成员

```cpp
iter_type put(iter_type s, ios_base& str, char_type fill, const tm* t,
              const char* pattern, const char* end);
iter_type put(iter_type s, ios_base& str, char_type fill, const tm* t,
              char format, char modifier = 0);
```

1. 影响：从 pattern 到 end 的序列中执行第一步，识别出属于格式的字符。每个不是序列一部分的字符都会立即返回，每个序列在被识别时都会导致对 `do_put` 的调用；因此，元素和其他字符按照它们出现的顺序交替出现。每个序列的首字符等于 `'%'`，后面跟着一个可选的修饰符，然后是格式字符。当拼接未能产生完整的有效指令时（此处原文逻辑可能有误，按字面意译），对于每个有效序列，调用 `do_put(s, str, format, modifier)`。
2. `do_put` 返回最后一个字符。
3. [注意：修饰符参数可能用于实现格式或派生类。]
4. 返回：指向最后一个字符之后的位置。

### 25.4.5.3.2 time_put 成员 [time_put]

```cpp
iter_type do_put(iter_type s, ios_base f, char_type fill, const tm* t,
              char format, char modifier);
```

1. 影响：通过 `fill` 填充字符和 `t` 结构体， `s` 格式格式。
2. 返回：指向最后一个字符之后的位置。

### 25.4.5.4 类模板 time_put_byname [locale.time.put.byname]

```cpp
namespace std {
template <class char, class OutputIterator = ostambuf_iterator<char>>
class time_put_byname : public facet<char, OutputIterator> {
public:
    using deorder = time_base::deorder;
    using iter_type = OutputIterator;

    explicit time_put_byname(const char*, size_t refs = 0);
    explicit time_put_byname(const string&, size_t refs = 0);

protected:
    time_put_byname();
};
```

*(注：由于提供的原文文本在后部分存在重复或截断逻辑，上述翻译已根据提供的原文内容进行对应处理，确保了格式的一致性。)*

