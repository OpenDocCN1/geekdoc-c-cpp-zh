
# ISO/IEC 14882:2020(E)

+   - 第1阶段：确定转换说明符
+   - 第2阶段：从 in 中提取字符，并为第1阶段确定的转换规范所期望的格式确定相应的 char 值。
+   - 第3阶段：存储结果

下面介绍各个阶段的细节。

# 第1阶段：函数通过以下代码初始化局部变量

```
fmtflags flags = str.flags();
fmtflags basefield = (flags & ios_base::basefield);
fmtflags uppercase = (flags & ios_base::uppercase);
fmtflags boolalpha = (flags & ios_base::boolalpha);
```

对于整型的转换，该函数按表106所示确定整型转换说明符。表中按顺序排列，即第一个条件为真的行适用。

# 表106：整型转换 [tab:facet.num.get.int]

| 状态 | stdio 等价表示 |
|---|---|
| basefield == oct | %o |
| basefield == hex | %X |
| basefield == 0 | %i |
| 有符号整型 | %d |
| 无符号整型 | %u |

对于浮点类型的转换，说明符为 %g。

对于 void* 的转换，说明符为 %p。

如果需要，按表107所示，在转换规范中添加长度修饰符。

# 表107：长度修饰符 [tab:facet.num.get.length]

| 类型 | 长度修饰符 |
|---|---|
| short | h |
| unsigned short | h |
| long | l |
| unsigned long | l |
| long long | ll |
| unsigned long long | ll |
| double | l |
| long double | L |

# 第2阶段：如果 in == end，则第2阶段终止。否则从 in 中取出一个 charT，并按如下方式初始化局部变量

```
char_type ct = *in;
char c = src[find(atoms, atoms + sizeof(src) - 1, ct) - atoms];
if (ct == use_facet<num punct<charT>>(loc).decimal_point())
c = '.';
bool discard =
  ct == use_facet<num punct<charT>>(loc).thousands_sep()
  && use_facet<num punct<charT>>(loc).grouping().length() != 0;
```

其中 src 和 atoms 的值定义如下：

```
static const char src[] = "0123456789abcdefxABCDEFx+-";
char_type atoms[sizeof(src)];
use_facet<ctype<charT>>(loc).widen(src, src + sizeof(src), atoms);
```

对于这个 loc 值。

如果 discard 为 true，那么如果尚未累积 '.'，则记住该字符的位置，但该字符将被忽略。否则，如果已经累积了 '.'，则丢弃该字符并终止第2阶段。如果没有被丢弃，则执行检查，以确定 c 是否允许作为第1阶段返回的转换说明符的输入字段的下一个字符。如果是，则累积该字符。
如果该字符被丢弃或累积，则通过 ++in 推进 in，并返回到第2阶段的开头继续处理。

# 第3阶段：在第2阶段累积的字符序列（字段）按照 <cstdlib> 头文件中声明的某个函数的规则转换为数值：

+   - 对于有符号整数值，使用函数 strtoll。
+   - 对于无符号整数值，使用函数 strtoull。
+   - 对于浮点值，使用函数 strtof。
+   - 对于双精度值，使用函数 strtod。
+   - 对于长双精度值，使用函数 strtold。

要存储的数值可以是以下之一：

+   - 零，如果转换函数没有转换整个字段。
+   - 最大正（或负）可表示值，如果要转换为有符号整数类型的字段表示的值太大，无法在 val 中表示为正（或负）。
+   - 最大正可表示值，如果要转换为无符号整数类型的字段表示的值无法在 val 中表示。
+   - 已转换的值，否则。

结果数值存储在 val 中。如果转换函数没有转换整个字段，或者该字段表示的值超出可表示范围，则将 ios_base::failbit 赋给 err。

检查数字分组。即检查被丢弃的分隔符的位置是否与 use_facet<num punct<charT>>(loc).grouping() 一致。如果不一致，则将 ios_base::failbit 赋给 err。

在任何情况下，如果第2阶段处理因测试 in == end 而终止，则执行 err |= ios_base::eofbit。

```
iter_type do_get(iter_type in, iter_type end, ios_base& str,
    ios_base::iostate& err, bool& val) const;
```

效果：如果 (str.flags()&ios_base::boolalpha) == 0，则输入过程与 long 类型相同，但如果将值存储到 val 中，则按照以下方式确定该值：如果要存储的值为 0，则存储 false。如果值为 1，则存储 true。否则存储 true，并将 ios_base::failbit 赋给 err。

否则，目标序列由调用 use_facet<num punct<charT>>(str.getloc()) 获得的facet的成员 false name() 和 true name() “按照”确定。范围 [in, end)（见 22.2.3）内的连续字符仅在识别唯一匹配所必要时被获取并与目标序列中的对应位置匹配。输入迭代器 in 仅在需要获取字符时才与 end 比较。如果目标序列唯一匹配，则将 val 设置为相应的值。否则存储 false，并将 ios_base::failbit 赋给 err。

in 迭代器始终指向最后一个成功匹配字符之后的一个位置。如果 val 被设置，则将 err 设置为 str.goodbit；如果在寻找另一个要匹配的字符时发现 (in == end)，则设置为 str.eofbit。如果 val 未被设置，则将 err 设置为 str.failbit；如果失败的原因是在 (in == end)，则设置为 (str.failbit|str.eofbit)。

[示例1：对于目标 true: "a" 和 false: "abb"，输入序列 "a" 产生 val == true 和 err == str.eofbit；输入序列 "abc" 产生 err = str.failbit，in 在 'c' 元素处结束。对于目标 true: "1" 和 false: "0"，输入序列 "1" 产生 val == true 和 err == str.goodbit。对于空目标 ("")，任何输入序列都产生 err == str.failbit。— 示例结束]

返回：in。

# 28.4.3.3 num_put 类模板 [locale.nm.put]

# 28.4.3.3.1 概述 [locale.nm.put.general]

```
namespace std {
  template<class charT, class OutputIterator = ostreambuf_iterator<charT>>
  class num_put : public locale::facet {
  public:
    using char_type = charT;
```

| 类型 | 状态 | stdio 等价表示 |
|---|---|---|
| 整型 | showpos | + |
|  | showbase | # |
| 浮点型 | showpos | + |
|  | showpoint | # |

对于浮点类型的转换，如果 floatfield != (ios_base::fixed | ios_base::scientific)，则在转换规范中将 str.precision() 指定为 precision。否则，不指定精度。

对于 void* 的转换，说明符为 %p。

第1阶段末尾的表示由调用 printf(s, val) 时打印出的 char 组成，其中 s 是上面确定的转换说明符。

**第2阶段：** 除小数点(.)以外的任何字符 c 都通过以下代码转换为 charT

```cpp
use_facet<ctype<charT>>(loc).widen(c)
```

局部变量 punct 通过以下代码初始化

```cpp
const numpunct<charT>& punct = use_facet<numpunct<charT>>(loc);
```

对于算术类型，punct.thousands_sep() 字符被插入序列，插入方式由 punct.do_grouping() 返回的值决定，采用 28.24.4.1.3 中描述的方法。小数点字符(.)被 punct.decimal_point() 替换

**第3阶段：** 局部变量初始化为

```cpp
fmtflags adjustfield = (flags & (ios_base::adjustfield));
```

根据表112确定任何填充的位置。

| 状态 | 位置 |
|---|---|
| adjustfield == ios_base::left | 后面填充 |
| adjustfield == ios_base::right | 前面填充 |
| adjustfield == internal 且表示中出现符号 | 符号后填充 |
| adjustfield == internal 且第1阶段后的表示以 0x 或 0X 开头 | x 或 X 后填充 |
| *其他情况* | 前面填充 |

如果 str.width() 非零且第2阶段后序列中的 charT 数量小于 str.width()，则在指定的填充位置添加足够的填充字符，使序列长度达到 str.width()。

调用 str.width(0)。

**第4阶段：** 第3阶段末尾的 charT 序列通过以下代码输出

```cpp
*out++ = c
```

```
iter_type do_put(iter_type out, ios_base& str, char_type fill, bool val) const;
```

返回：如果 (str.flags() & ios_base::boolalpha) == 0，则返回 do_put(out, str, fill, (int)val)，否则按如下方式获取字符串 s

string_type s =
    val ? use_facet<numpunct<charT>>(loc).truename()
        : use_facet<numpunct<charT>>(loc).falsename();

然后将 s 的每个字符 c 通过 *out++ = c 插入到 out 中，并返回 out。
