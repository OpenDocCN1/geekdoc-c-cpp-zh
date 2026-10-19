

12 对于非 Unicode 编码中的字符串，字符串的宽度未指定。

13 在宽度字段前面的零（0）字符用前导零填充该字段（在符号或基数的指示之后），直到达到字段宽度，除非应用于无穷大或 NaN。此选项仅对除 charT 和 bool 之外的算术类型有效，或当指定了整数表示类型时有效。如果 0 字符和对齐选项同时出现，则 0 字符将被忽略。

[示例 3：

```
char c = 120;
string s1 = format("{:+06d}", c);    // value of s1 is "+00120"
string s2 = format("{:#06x}", 0xa);    // value of s2 is "0x000a"
string s3 = format("{:<06}", -42);    // value of s3 is "-42    " (0 is ignored because of < alignment)
```

— 示例结束]

14 精度中的非负整数是一个十进制整数，定义精度或最大字段大小。它只能与浮点类型和字符串类型一起使用。对于浮点类型，此字段指定格式化精度。对于字符串类型，此字段为复制到输出中的输入字符串前缀的估计宽度提供上限。对于 Unicode 编码中的字符串，格式化程序将复制到输出的最长前缀，该前缀由完整的扩展图形簇组成，其估计宽度不超过精度。

15 当使用 L 选项时，用于转换的形式称为特定于区域设置的形式。L 选项仅对算术类型有效，其效果取决于类型。

- (15.1) — 对于整数类型，特定于区域设置的形式会导致使用上下文的区域设置插入适当的数字分组分隔符字符。
- (15.2) — 对于浮点类型，特定于区域设置的形式会导致使用上下文的区域设置插入适当的数字分组和基数分隔符字符。
- (15.3) — 对于 bool 的文本表示，特定于区域设置的形式会导致使用上下文的区域设置插入适当的字符串，就像使用 numpunct::truename 或 numpunct::falsename 获得的一样。

16 类型决定数据应如何呈现。

17 字符串表示类型的可用选项在表 61 中指定。

### 表 61：字符串的类型选项的含义 [tab:format.type.string]

| Type | Meaning |
| --- | --- |
| none, s | Copies the string to the output. |

18 一些非字符串表示类型的含义是根据对 to_chars 的调用定义的。在这种情况下，让 [first, last) 为足以容纳 to_chars 输出的范围，value 为格式化参数值。格式化就像通过调用按指定方式调用 to_chars 并将输出复制通过格式上下文的输出迭代器一样进行。

[注意 7：根据格式说明符指定的方式，在将输出复制通过输出迭代器之前会执行额外的填充和调整。 — 注释结束]

19 除 bool 和 charT 之外的积分类型的可用整数表示类型在表 62 中指定。

[示例 4：

```
string s0 = format("{}", 42);    // value of s0 is "42"
string s1 = format("{0:b} {0:d} {0:o} {0:x}", 42);    // value of s1 is "101010 42 52 2a"
string s2 = format("{0:#x} {0:#X}", 42);    // value of s2 is "0x2a 0X2A"
string s3 = format("{:L}", 1234);    // value of s3 can be "1,234"    // (depending on the locale)
```

— 示例结束]

### 表 62：整数类型的类型选项的含义 [tab:format.type.int]

| Type | Meaning |
| --- | --- |
| b | `to_chars(first, last, value, 2)`; the base prefix is `0b`. |
| B | The same as `b`, except that the base prefix is `0B`. |
| c | Copies the character `static_cast<charT>(value)` to the output. Throws `format_error` if `value` is not in the range of representable values for `charT`. |
| d | `to_chars(first, last, value)`. |
| o | `to_chars(first, last, value, 8)`; the base prefix is `0` if `value` is nonzero and is empty otherwise. |
| x | `to_chars(first, last, value, 16)`; the base prefix is `0x`. |
| X | The same as `x`, except that it uses uppercase letters for digits above 9 and the base prefix is `0X`. |
| none | The same as `d`. [Note 8: If the formatting argument type is `charT` or `bool`, the default is instead `c` or `s`, respectively. — end note] |

20 charT 的可用表示类型在表 63 中指定。

### 表 63：charT 的类型选项的含义 [tab:format.type.char]

| Type | Meaning |
| --- | --- |
| none, c | Copies the character to the output. |
| b, B, d, o, x, X | As specified in Table 62. |

21 bool 的可用表示类型在表 64 中指定。

### 表 64：bool 的类型选项的含义 [tab:format.type.bool]

| Type | Meaning |
| --- | --- |
| none, s | Copies textual representation, either true or false, to the output. |
| b, B, c, d, o, x, X | As specified in Table 62 for the value `static_cast<unsigned char>(value)`. |

[Note 9: In either case, a sign is included if indicated by the sign option. — end note]

22 表 65 指定了浮点表示类型的可用选项及其对除无穷大和 NaN 之外的值的含义。对于小写表示类型，无穷大和 NaN 分别格式化为 `inf` 和 `nan`。对于大写表示类型，无穷大和 NaN 分别格式化为 `INF` 和 `NAN`。

### 表 65：浮点类型的类型选项的含义 [tab:format.type.float]

| Type | Meaning |
| --- | --- |
| a | If precision is specified, equivalent to `to_chars(first, last, value, chars_format::hex, precision)` where `precision` is the specified formatting precision; equivalent to `to_chars(first, last, value, chars_format::hex)` otherwise. |
| A | The same as `a`, except that it uses uppercase letters for digits above 9 and `P` to indicate the exponent. |
| e | Equivalent to `to_chars(first, last, value, chars_format::scientific, precision)` where `precision` is the specified formatting precision, or `6` if precision is not specified. |
| E | The same as `e`, except that it uses `E` to indicate exponent. |
| f, F | Equivalent to `to_chars(first, last, value, chars_format::fixed, precision)` where `precision` is the specified formatting precision, or `6` if precision is not specified. |
| g | Equivalent to `to_chars(first, last, value, chars_format::general, precision)` where `precision` is the specified formatting precision, or `6` if precision is not specified. |
| G | The same as `g`, except that it uses `E` to indicate exponent. |
| none | If precision is specified, equivalent to `to_chars(first, last, value, chars_format::general, precision)` where `precision` is the specified formatting precision; equivalent to `to_chars(first, last, value)` otherwise. |

23 表 66 指定了指针表示类型的可用选项及其到 to_chars 的映射。

### 表 66：指针类型的类型选项的含义 [tab:format.type.ptr]

| Type | Meaning |
| --- | --- |
| none, p | If `uintptr_t` is defined, `to_chars(first, last, reinterpret_cast<uintptr_t>(value), 16)` with the prefix `0x` added to the output; otherwise, implementation-defined. |

[Note 10: Pointer presentation types also apply to `nullptr_t`. — end note]

## 20.20.3 错误报告 [format.err.report]

1 格式化函数如果传递的参数 `fmt` 不是 `args` 的格式字符串，则抛出 `format_error`。它们传播由格式化程序特化和迭代器的操作抛出的异常。存储分配失败通过抛出 16.4.6.13 中描述的异常来报告。

## 20.20.4 格式化函数 [format.functions]

1 在函数的描述中，运算符 + 用于某些迭代器类别，而对于这些类别它不必定义。在这些情况下，`a + n` 的语义与 25.2 中相同。

```
template<class... Args>
  string format(string_view fmt, const Args&... args);
```

2 效果：等价于：

```
return vformat(fmt, make_format_args(args...));
```

```
template<class... Args>
  wstring format(wstring_view fmt, const Args&... args);
```

3 效果：等价于：

```
return vformat(fmt, make_wformat_args(args...));
```

```
template<class... Args>
  string format(const locale& loc, string_view fmt, const Args&... args);
```

4 效果：等价于：

```
return vformat(loc, fmt, make_format_args(args...));
```

```
template<class... Args>
wstring format(const locale& loc, wstring_view fmt, const Args&... args);
```

效果：等价于：

```
return vformat(loc, fmt, make_wformat_args(args...));
```

```
string vformat(string_view fmt, format_args args);
wstring vformat(wstring_view fmt, wformat_args args);
string vformat(const locale& loc, string_view fmt, format_args args);
wstring vformat(const locale& loc, wstring_view fmt, wformat_args args);
```

返回：一个字符串对象，保存由 `args` 提供的格式化参数的字符表示，按 `fmt` 中给出的规范格式化。如果存在，`loc` 用于特定于区域设置的格式化。

抛出：如 20.20.3 中指定。

```
template<class Out, class... Args>
Out format_to(Out out, string_view fmt, const Args&... args);
template<class Out, class... Args>
Out format_to(Out out, wstring_view fmt, const Args&... args);
```

效果：等价于：

```
using context = basic_format_context<Out, decltype(fmt)::value_type>;
return vformat_to(out, fmt, make_format_args<context>(args...));
```

