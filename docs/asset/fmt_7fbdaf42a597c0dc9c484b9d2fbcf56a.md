
```
void test() {
string input = “aa as; asd ++e^asdf asdfg”;
regex pat {R"(\s+(\w+))"};
for (sregex_iterator p(input.begin(),input.end(),pat); p!=sregex_iterator{}; ++p) cout << (*p)[1] << ‘\n’;
}
```

输出：

```
as
asd
asdfg
```

注意我们漏掉了第一个单词 `aa`，因为它前面没有空白。如果我们将模式简化为 `R"((\w+))"`，我们会得到

```
aa
as
asd
e
asdf
asdfg
```

你不能通过 `regex_iterator` 进行写入，而且 `regex_iterator{}` 是唯一的序列结束方式。

# 37.4.2 regex_token_iterator

`regex_token_iterator` 是 `regex_iterator` 的适配器，它遍历所找到的 `match_results` 的 `sub_matches`：

```
template<class Bi,
class C = typename iterator_traits<Bi>::value_type ,
class Tr = typename regex_traits<C>::type>

class regex_token_iterator {
public:
using regex_type = basic_regex<C,Tr>;
using value_type = sub_match<Bi>;
using difference_type = ptrdiff_t;
using pointer = const value_type*;
using reference = const value_type&;
```

```
using iterator_category = forward_iterator_tag;
// ...
```

`regex_traits` 在 §37.5 中描述。提供了一组常用的别名：

```
using cregex_token_iterator = regex_token_iterator<const char *>;
using wcregex_token_iterator = regex_token_iterator<const wchar_t*>;
using sregex_token_iterator = regex_token_iterator<string::const_iterator>;
using wsregex_token_iterator = regex_token_iterator<wstring::const_iterator>;
```

`regex_token_iterator` 提供了一组最简的迭代器操作：

### 第 37.4.2 节 regex_token_iterator 1069

# regex_token_iterator（§iso.28.12.2）

```
regex_token_iterator p {};
 p is the end-of-sequence
```

```
regex_token_iterator p {b,e,pat,x,flags}; x lists the indices of the sub_matches to be included in the iteration or 0, meaning “the whole match,” or −1, meaning “represent each character sequence not matched as a sub_match”;
```

```
x can be an int, an initializer_list<int>, a const vector<int>&, or a const int (&sub_match)[N]
```

```
regex_token_iterator p {b,e,pat,x}; p is initialized with {b,e,pat,x,regex_constants::match_default}
```

```
regex_token_iterator p {b,e,pat}; p is initialized with {b,e,pat,0,regex_constants::match_default}
```

```
regex_token_iterator p {q};
p.~regex_token_iterator()
p=q
p==q
```

复制构造函数（无移动构造函数）析构函数：释放所有资源

复制赋值（无移动赋值）p 是否与 q 指向同一个 sub_match？

```
p!=q !(p==q)
c=*p c is the current sub_match x=p->m x=(*p).m
++p Make p point to the next occurrence of p ’s pattern
q=p++ q=p, then ++p
```

x 参数列出要包含在迭代中的 sub_matches。例如（迭代匹配 1 和 3）：

```
void test1()
{
string input {"aa::bb cc::dd ee::ff"};
regex pat {R"((\w+)([[:punct:]]+)(\w+)\s*)"};
sregex_token_iterator end {};
for (sregex_token_iterator p{input.begin(),input.end(),pat,{1,3}}; p!=end; ++p) cout << *p << '\n';
}
```

这将输出：

```
aa
bb
cc
dd
ee
ff
```

−1 选项基本上反转了报告匹配的策略，将每个不匹配的字符序列表示为一个 sub_match。这通常被称为“分词”（即把字符流拆分为记号），因为当你的模式匹配到记号分隔符时，选项 −1 会留下记号本身。例如：

```
void test2()
{
string s {"1,2 , 3 ,4,5, 6 7"}; // input
regex pat {R"(\s*,\s*)"}; // use comma as token separator copy(sregex_token_iterator{s.begin(),s.end(),pat,-1},
sregex_token_iterator{},
ostream_iterator<string>{cout,"\n"});
}
```

输出为：

```
1
2
3
4
5
67
```

这也可以等价地用一个显式循环来写：

```
void test3()
{
sregex_token_iterator end{};
for (sregex_token_iterator p {s.begin(),s.end(),pat,-1}; p!=end; ++p) cout << *p << '\n';
}
```

# 37.5 regex_traits

`regex_traits<T>` 表示字符类型、字符串类型和 locale（区域设置）之间的对应关系，这正是正则表达式实现者所需要的：

```
template<class C>
struct regex_traits {
public:
using char_type = C;
```

```
using string_type = basic_string<char_type>;
using locale_type = locale;
using char_class_type = /* implementation-defined bitmask type*/;
// ...

};
```

标准库提供了特化 `regex_traits<char>` 和 `regex_traits<wchar_t>`。

### 第 37.5 节 `regex_traits` 1071

| 操作 | 描述 |

|---|---|

| `regex_traits<C>` | 操作（§iso.28.7） |

| `regex_traits tr {}` | 构造一个默认的 `regex_trait<C>` |

| `n=length(p) n` | n 是 C 风格字符串 `p` 中的字符数； |

| `n=char_traits<C>::length();` | 静态（static） |

| `c2=tr.translate(c)` | c2=c，即空操作 |

| `c2=tr.translate_nocase(c)` | 使用 `facet<ctype<C>>(getloc()).tolower(c)`；§39.4.5 |

| `s=tr.transform(b,e)` | s 是一个字符串，可用于将 [`b:e`) 与其他字符串进行比较；§39.4.1 |

| `s=tr.transform_primary(b,e)` | s 是一个字符串，可用于将 [`b:e`) 与其他字符串进行比较；忽略大小写；§39.4.1 |

| `s=tr.lookup_collatename(b,e)` | s 是名为 [`b:e`) 的排序元素的 `string` 名称，或空字符串 |

| `m=tr.lookup_classname(b,e,ign)` | m 是名为 [`b:e`) 的字符分类的分类掩码的字符串名称；如果 `ign==true` 则忽略大小写 |

| `m=tr.lookup_classname(b,e)` | m=tr.lookup_classname(b,e |

| `tr.isctype(c,m)` | c 是否被归类为 `m`？ |

| `m` | m 是一个 `class_type` |

| `i=tr.value(c,b)` | i 是 c 在基数 b 下表示的整数值；b 必须是 `8`、`10` 或 `16` |

| `loc2=tr.imbue(loc)` |  |

| `loc=tr.getloc()` | 将 `tr` 的 locale 设置为 `loc`；`loc2` 是 `tr` 先前的 locale；`loc` 是 `tr` 的 locale |

transform（转换）用于在模式匹配实现中生成字符串以进行快速比较。分类名称是 §37.1.1 中列出的字符分类之一，例如 `alpha`、`s` 和 `xdigit`。

# 37.6 建议

- [1] 在大多数常规正则表达式用途中，使用 `regex`；§37.1。

- [2] 可以调整正则表达式记号法以匹配各种标准；§37.1.1、§37.2。

- [3] 默认的正则表达式记号法是 ECMAScript 的记号法；§37.1.1。

- [4] 为了可移植性，请使用字符类记号法，避免非标准缩写；§37.1.1。

- [5] 要有所节制；正则表达式很容易变成一种只写（write-only）语言；§37.1.1。

- [6] 除了最简单的模式之外，优先使用原始字符串字面量来表达模式；§37.1.1。

- [7] 注意，`\i` 允许你用一个先前的子模式来表达某个子模式；§37.1.1。

- [8] 使用 `?` 使模式变为“懒惰”模式；§37.1.1、§37.2.1。

- [9] `regex` 可以使用 ECMAScript、POSIX、awk、grep 和 egrep 记号法；§37.2。

- [10] 保留一份模式字符串的副本，以防你需要输出它；§37.2。

- [11] 使用 `regex_search()` 来查看字符流，使用 `regex_match()` 来查找固定布局；§37.3.2、§37.3.1。

# 此页有意留白

- 引言

- I/O 流层次结构 文件流；字符串流

- 错误处理

- I/O 操作

- 流迭代器

- 缓冲

- 建议

输入操作；输出操作；操作器；流状态；格式化

输出流和缓冲区；输入流和缓冲区；缓冲区迭代器

# 38

# I/O 流

> 你看到的就是你得到的。

> ——布赖恩·克尼汉

## 38.1 引言

I/O 流库提供文本和数值的格式化与无格式缓冲 I/O。I/O 流设施的定义位于 `<istream>`、`<ostream>` 等头文件中；参见 §30.2。`ostream` 将类型化对象转换为字符（字节）流：

类型化值：字节序列：‘c’ 123 `ostream` “Somewhere” (123,45) 流缓冲区

`istream` 将字符（字节）流转换为类型化对象：

类型化值：字节序列：‘c’

123 `istream` “Somewhere”

(123,45) 流缓冲区

`iostream` 是一种既能充当 `istream` 又能充当 `ostream` 的流。图中的缓冲区是流缓冲区（`streambuf`；§38.6）。你需要它们来定义从 `iostream` 到新型设备、文件或内存的映射。`istream` 和 `ostream` 上的操作在 §38.4.1 和 §38.4.2 中描述。

使用流库并不需要了解实现流库所使用的技术。因此，我只介绍理解和运用 `iostream` 所需的一般概念。如果你需要实现标准流、提供新型流或提供新的 locale，除了这里介绍的内容之外，你还需要标准的一份副本、一本好的系统手册以及可工作代码的示例。

流 I/O 系统的关键组件可以图形化地表示如下：

`ios_base`:

与 locale 无关的格式状态

`basic_streambuf<>` : 缓冲

`basic_ios<>` :

依赖 locale 的格式状态

流状态

真实目标/来源

字符缓冲区

`basic_iostream<>` : 格式化（<<、>> 等） 设置/清理

`locale`:

格式信息

实线箭头表示“派生自”。虚线箭头表示“指向”。

用 <> 标记的类是模板，由字符类型参数化并包含一个区域设置。I/O 流操作：

- 是类型安全且类型敏感的

- 可扩展（当有人设计新类型时，可以在不修改现有代码的情况下添加匹配的 I/O 流运算符）

### 第 38.1 节 引言

- 是区域设置敏感的（第 39 章）

- 是高效的（尽管其潜力并不总是得到充分发挥）

- 与 C 风格的 `stdio` 互操作（§43.3）

- 包含格式化、无格式和字符级操作

`basic_iostream` 基于 `basic_istream` (§38.6.2) 和 `basic_ostream` (§38.6.1) 定义：

```
template<typename C, typename Tr = char_traits<C>>
class basic_iostream :
public basic_istream<C,Tr>, public basic_ostream<C,Tr> {
public:
using char_type = C;
using int_type = typename Tr::int_type;
using pos_type = typename Tr::pos_type;
using off_type = typename Tr::off_type;
using traits_type = Tr;

explicit basic_iostream(basic_streambuf<C,Tr>* sb); virtual ~basic_iostream();
protected:
basic_iostream(const basic_iostream& rhs) = delete;
basic_iostream(basic_iostream&& rhs);

basic_iostream& operator=(const basic_iostream& rhs) = delete;
basic_iostream& operator=(basic_iostream&& rhs);
void swap(basic_iostream& rhs);
};
```

模板参数分别指定字符类型和用于操作字符的 traits (§36.2.2)。

请注意，没有提供复制操作：共享或克隆流相当复杂的内部状态将难以实现且使用成本高昂。移动操作 intended for use by derived classes，因此为受保护。移动一个 `iostream` 而不移动其定义派生类（如 `fstream`）的状态将导致错误。

有三个标准流：

# 标准 I/O 流

`cout` 标准字符输出（通常默认为屏幕） `cin` 标准字符输入（通常默认为键盘） `cerr` 标准字符错误输出（无缓冲） `clog` 标准字符错误输出（有缓冲）

`wcin` `cin` 的 `wistream` 版本

`wcout` `cout` 的 `wostream` 版本

`wcerr` `cerr` 的 `wostream` 版本

`wclog` `clog` 的 `wostream` 版本

在 `<iosfwd>` 中提供了流类型和流对象的转发声明。

# 38.2 I/O 流层次结构

`istream` 可以连接到输入设备（如键盘）、文件或字符串。同样，`ostream` 可以连接到输出设备（如文本窗口或 HTML 引擎）、文件或字符串。I/O 流设施在类层次结构中组织：

`ios_base`

`basic_ios<>`

`basic_istream<>` `basic_ostream<>`

`basic_istringstream<>` `basic_iostream<>` `basic_ostringstream<>`

`basic_ifstream<>` `basic_ofstream<>`

`basic_fstream<>` `basic_stringstream<>`

后缀为 `<>` 的类是按字符类型参数化的模板。点线表示虚基类 (§21.3.5)。

关键类是 `basic_ios`，其中定义了大部分实现和许多操作。然而，大多数普通（甚至不那么普通）的用户从未见过它：它主要是流的实现细节。它在 §38.4.4 中描述。其大部分设施在按其功能描述的上下文中描述（例如，格式化；§38.4.5）。

## 38.2.1 文件流
