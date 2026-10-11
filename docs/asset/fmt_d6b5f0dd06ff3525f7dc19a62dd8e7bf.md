
参见 §11.3。

### B.7.2 错误处理

`iostream`可以处于四种状态之一：

**流状态**

| 状态 | 描述 |
| :--- | :--- |
| `good()` | 操作成功。 |
| `eof()` | 遇到了输入结束（“文件末尾”）。 |
| `fail()` | 发生了意外事件（例如，我们要查找数字但找到了 `'x'`）。 |
| `bad()` | 发生了意外且严重的事件（例如，磁盘读取错误）。 |

通过使用`s.exceptions()`，程序员可以请求`iostream`在从`good()`变为其他状态时抛出异常（参见 §10.6）。

在不处于`good()`状态的流上尝试的任何操作都没有效果；它是一个“无操作”（no op）。

`iostream`可以作为条件使用。在这种情况下，如果`iostream`的状态是`good()`，则条件为真（成功）。这是读取值流的常见惯用做法的基础：

```cpp
for (X buf; cin>>buf; ) {  // buf is an “input buffer” for holding one value of type X

  // ... do something with buf, ...

}

// we get here when >> couldn't read another X from cin
```

### B.7.3 输入操作

除了用于读取到字符串的操作外，其他输入操作都位于`<iostream>`中；读取到字符串的操作位于`<string>`中：

#### 格式化输入
| 操作 | 描述 |
| :--- | :--- |
| `in >> x` | 根据`x`的类型，从`in`读取到`x`。 |
| `getline(in,s)` | 从`in`读取一行到字符串`s`中。 |

除非另有说明，istream操作返回对其istream的引用，因此我们可以“链接”操作，例如`cin >> x >> y;`。

#### 非格式化输入
| 操作 | 描述 |
| :--- | :--- |
| `x=in.get()` | 从`in`读取一个字符并返回其整数值。 |
| `in.get(c)` | 从`in`读取一个字符到`c`中。 |
| `in.get(p,n)` | 从`in`读取最多`n`个字符到以`p`为起始的数组中。 |
| `in.get(p,n,t)` | 从`in`读取最多`n`个字符到以`p`为起始的数组中；将`t`视为终止符。 |
| `in.getline(p,n)` | 从`in`读取最多`n`个字符到以`p`为起始的数组中；从`in`中移除终止符。 |
| `in.getline(p,n,t)` | 从`in`读取最多`n`个字符到以`p`为起始的数组中；将`t`视为终止符；从`in`中移除终止符。 |
| `in.read(p,n)` | 从`in`读取最多`n`个字符到以`p`为起始的数组中。 |
| `x=in.gcount()` | `x`是最近一次对`in`执行的非格式化输入操作所读取的字符数。 |
| `in.unget()` | 回退流，使得下次读取的字符与上一次读取的字符相同。 |
| `in.putback(x)` | 将`x`“放回”流中，使其成为下次读取的字符。 |

`get()`和`getline()`函数会在写入到`p[0] ...`的字符末尾（如果有）放置一个0；`getline()`会移除终止符（`t`）（如果找到），而`get()`不会。`read(p,n)`不会在读取的字符之后向数组写入0。显然，格式化输入运算符比非格式化运算符更简单、更不易出错。

### B.7.4 输出操作

除了用于写出字符串的操作外，其他输出操作都位于`<ostream>`中；写出字符串的操作位于`<string>`中：

#### 输出操作
| 操作 | 描述 |
| :--- | :--- |
| `out << x` | 根据`x`的类型，将`x`写入`out`。 |
| `out.put(c)` | 将字符`c`写入`out`。 |
| `out.write(p,n)` | 将字符`p[0]..p[n–1]`写入`out`。 |

除非另有说明，ostream操作返回对其ostream的引用，因此我们可以“链接”操作，例如`cout << x << y;`。

### B.7.5 格式化

流I/O的格式由对象类型、流状态、区域设置信息（参见`<locale>`）和显式操作的组合控制。第10章和第11章解释了其中大部分内容。在这里，我们仅列出标准操纵器（修改流状态的操作），因为它们提供了修改格式的最直接方式。

区域设置超出了本书的范围。

### B.7.6 标准操纵器

标准库提供了与各种格式状态和状态更改相对应的操纵器。标准操纵器定义在`<ios>`、`<istream>`、`<ostream>`、`<iostream>`以及`<iomanip>`（用于接受参数的操纵器）中：

#### I/O 操纵器
| 操纵器 | 效果 |
| :--- | :--- |
| `s << boolalpha` | 使用`true`和`false`的符号表示（输入和输出）。 |
| `s << noboolalpha` | `s.unsetf(ios_base::boolalpha)`。 |
| `s << showbase` | 输出时，在`oct`前加`0`，在`hex`前加`0x`。 |
| `s << noshowbase` | `s.unsetf(ios_base::showbase)`。 |
| `s << showpoint` | 始终显示小数点。 |
| `s << noshowpoint` | `s.unsetf(ios_base::showpoint)`。 |
| `s << showpos` | 为正数显示`+`。 |
| `s << noshowpos` | `s.unsetf(ios_base::showpos)`。 |
| `s << skipws` | 跳过空白字符。 |
| `s << noskipws` | `s.unsetf(ios_base::skipws)`。 |
| `s << uppercase` | 在数值输出中使用大写字母，例如1.2E10和0X1A2，而不是1.2e10和0x1a2。 |
| `s << nouppercase` | 使用`x`和`e`而不是`X`和`E`。 |
| `s << internal` | 在格式化模式中标记的位置进行填充。 |
| `s << left` | 在值之后填充。 |
| `s << right` | 在值之前填充。 |
| `s << dec` | 整数基数为10。 |
| `s << hex` | 整数基数为16。 |
| `s << oct` | 整数基数为8。 |
| `s << fixed` | 浮点格式dddd.dd。 |
| `s << scientific` | 科学计数法格式d.ddddEdd。 |
| `s << defaultfloat` | 任何能提供最精确浮点输出的格式。 |
| `s << endl` | 放入`'\n'`并刷新缓冲区。 |
| `s << ends` | 放入`'\0'`。 |
| `s << flush` | 刷新流。 |
| `s >> wv` | 吃掉空白字符。 |
| `s << resetiosflags(f)` | 清除标志`f`。 |
| `s << setiosflags(f)` | 设置标志`f`。 |
| `s << setbase(b)` | 以基数`b`输出整数。 |
| `s << setfill(c)` | 使`c`成为填充字符。 |
| `s << setprecision(n)` | 精度为`n`位数字。 |
| `s << setw(n)` | 下一个字段宽度为`n`个字符。 |

这些操作中的每一个都返回对其第一个（流）操作数`s`的引用。例如：

```cpp
cout << 1234 << ',' << hex << 1234 << ',' << oct << 1234 << endl;
```

产生

```cpp
1234,4d2,2322
```

以及

```cpp
cout << '(' << setw(4) << setfill('#') << 12 << ")" << 12 << ")\n";
```

产生

```
(##12) (12)
```

要显式设置浮点数的一般输出格式，请使用

```cpp
b.set(ios_base::fmtflags(0), ios_base::floatfield)
```

参见第11章。

## B.8 字符串操作

标准库在`<cctype>`中提供字符分类操作，在`<string>`中提供字符串及相关操作，在`<regex>`中提供正则表达式匹配，并在`<cstring>`中提供对C风格字符串的支持。

### B.8.1 字符分类

基本执行字符集中的字符可以这样分类：

| 函数 | 描述 |
| :--- | :--- |
| `isspace(c)` | `c`是空白字符（`' '`, `'\t'`, `'\n'`等）吗？ |
| `isalpha(c)` | `c`是字母（`'a'..'z'`, `'A'..'Z'`）吗？（注意：不包括`'_'`。） |
| `isdigit(c)` | `c`是十进制数字（`'0'..'9'`）吗？ |
| `isxdigit(c)` | `c`是十六进制数字（十进制数字或`'a'..'f'`或`'A'..'F'`）吗？ |
| `isupper(c)` | `c`是大写字母吗？ |
| `islower(c)` | `c`是小写字母吗？ |
| `isalnum(c)` | `c`是字母或十进制数字吗？ |
| `iscntrl(c)` | `c`是控制字符（ASCII 0..31和127）吗？ |
| `ispunct(c)` | `c`不是字母、数字、空白字符或不可见控制字符吗？ |
| `isprint(c)` | `c`是可打印的（ASCII`' '..'~'`）吗？ |
| `isgraph(c)` | 是`isalpha(c)`或`isdigit(c)`或`ispunct(c)`吗？（注意：不包括空格。） |

此外，标准库提供了两个消除大小写差异的有用函数：

| 函数 | 描述 |
| :--- | :--- |
| `toupper(c)` | `c`或`c`的大写等效字符 |
| `tolower(c)` | `c`或`c`的小写等效字符 |

扩展字符集，如Unicode，得到支持但超出了本书的范围。

### B.8.2 字符串

标准库字符串类`string`是通用字符串模板`basic_string`针对字符类型`char`的特化；也就是说，`string`是一个`char`序列：

| 操作 | 描述 |
| :--- | :--- |
| `s=s2` | 将`s2`赋值给`s`；`s2`可以是字符串或C风格字符串。 |
| `s+=x` | 将`x`附加到`s`的末尾；`x`可以是字符、字符串或C风格字符串。 |
| `s[i]` | 下标访问。 |
| `s+s2` | 连接；结果是一个新字符串，包含`s`的字符后跟`s2`的字符。 |
| `s==s2` | 字符串值比较；`s`或`s2`（但不能同时两者）可以是C风格字符串。 |
| `s!=s2` | 字符串值比较；`s`或`s2`（但不能同时两者）可以是C风格字符串。 |
| `s<s2` | 字符串值的字典序比较；`s`或`s2`（但不能同时两者）可以是C风格字符串。 |
| `s<=s2` | 字符串值的字典序比较；`s`或`s2`（但不能同时两者）可以是C风格字符串。 |
| `s>s2` | 字符串值的字典序比较；`s`或`s2`（但不能同时两者）可以是C风格字符串。 |
| `s>=s2` | 字符串值的字典序比较；`s`或`s2`（但不能同时两者）可以是C风格字符串。 |
| `s.size()` | `s`中的字符数。 |
| `s.length()` | `s`中的字符数。 |

### B.8.3 正则表达式匹配

正则表达式设施位于`<regex>`中。主要功能包括：

- 在任意长度的数据流中搜索匹配正则表达式的字符串 – 由`regex_search()`支持
- 将正则表达式与已知大小的字符串进行匹配 – 由`regex_match()`支持
- 替换匹配项 – 由`regex_replace()`支持；本书未对此进行描述；请参阅专家级文本或手册

`regex_search()`或`regex_match()`的结果是一组匹配项，通常表示为`smatch`对象：

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

正则表达法的语法基于具有特殊含义的字符（第23章）：

| `正则表达式特殊字符` | |
| :--- | :--- |
| `.` | 任意单个字符（“通配符”） |
| `[` | 字符类 |
| `{` | 计数 |
| `(` | 开始分组 |
| `)` | 结束分组 |
| `\` | 下一个字符具有特殊含义 |
| `*` | 零次或多次 |
| `+` | 一次或多次 |
| `?` | 可选（零次或一次） |
| `\|` | 替代（或） |
| `^` | 行首；取反 |
| `$` | 行尾 |

| `重复` | |
| :--- | :--- |
| `{n}` | 恰好n次 |
| `{n,}` | n次或更多 |
| `{n,m}` | 至少n次且至多m次 |
| `*` | 零次或多次，即{0,} |
| `+` | 一次或多次，即{1,} |
| `?` | 可选（零次或一次），即{0,1} |

| `字符类` | |
| :--- | :--- |
| `alnum` | 任意字母数字字符或下划线 |
| `alpha` | 任意字母字符 |
| `blank` | 任意非换行分隔符的空白字符 |
| `cntrl` | 任意控制字符 |
| `d` | 任意十进制数字 |
| `digit` | 任意十进制数字 |
| `graph` | 任意图形字符 |
| `lower` | 任意小写字符 |
| `print` | 任意可打印字符 |
| `punct` | 任意标点字符 |
| `s` | 任意空白字符 |
| `space` | 任意空白字符 |
| `upper` | 任意大写字符 |
| `w` | 任意单词字符（字母数字字符） |
| `xdigit` | 任意十六进制数字字符 |

几个字符类由简写表示支持：

| `字符类简写` | | |
| :--- | :--- | :--- |
| `\d` | 十进制数字 | `[[:digit:]]` |
| `\l` | 小写字符 | `[[:lower:]]` |
| `\s` | 空格（空格、制表符等） | `[[:space:]]` |
| `\u` | 大写字符 | `[[:upper:]]` |
| `\w` | 字母、十进制数字或下划线 (\_) | `[[:alnum:]]` |
| `\D` | 非 `\d` | `[^[:digit:]]` |
| `\L` | 非 `\l` | `[^[:lower:]]` |
| `\S` | 非 `\s` | `[^[:space:]]` |
| `\U` | 非 `\u` | `[^[:upper:]]` |
| `\W` | 非 `\w` | `[^[:alnum:]]` |

## B.9 数值

C++标准库提供了数学（科学、工程等）计算的最基本构建块。

### B.9.1 数值限制

每个C++实现都指定了内置类型的属性，以便程序员可以使用这些属性来检查限制、设置哨兵值等。

从`<limits>`中，我们获得每个内置或库类型`T`的`numeric_limits<T>`。此外，程序员可以为用户定义的数值类型`X`定义`numeric_limits<X>`。例如：

```cpp
class numeric_limits<float> {

public:

    static const bool is_specialized = true;

    static constexpr int radix = 2;       // base of exponent (in this case, binary)

    static constexpr int digits = 24;     // number of radix digits in mantissa

    static constexpr int digits10 = 6;    // number of base-10 digits in mantissa

    static constexpr bool is_signed = true;
```
