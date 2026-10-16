
Bi 必须是一个双向迭代器 (§33.1.2)。

与 `basic_string` 和 `basic_ostream` 一样，为最常见的 `match_results` 提供了一些标准别名：

```
using cmatch = match_results<const char *>; // C-style string
using wcmatch = match_results<const wchar_t *>; // wide C-style string
using smatch = match_results<string::const_iterator>; // string
using wsmatch = match_results<wstring::const_iterator>; // wstring
```

`match_results` 提供对其匹配字符串、其 `sub_matches` 以及匹配前后字符的访问：

```
m[0]
m.prefix() m[1] ... m[m.size()] m.suffix()
```

`match_results` 提供了一套常规操作：

## regex<C, Tr> 匹配和子匹配 (§iso.28.9, §iso.28.10)

| 表达式 | 描述 |

|---|---|

| `match_results m {};` | 默认构造函数：使用 `allocator_type{}` |

| `match_results m {a};` | 使用分配器 `a`；显式 |

| `match_results m {m2};` | 复制和移动构造函数 |

| `m2 = m` | 复制赋值 |

| `m2 = move(m)` | 移动赋值 |

| `m.~match_results()` | 析构函数：释放所有资源 |

| `m.ready()` | `m` 是否持有完整的匹配？ |

| `n = m.size()` | n 是子匹配的数量 |

| `n = m.max_size()` | n 是子匹配的最大数量 |

n-1 是 m 中子表达式的数量；如果没有匹配，n==0；n 是 m 中 `sub_matches` 的最大可能数量。

`m.empty()` `m.size()==0`？

`r=m[i]` r 是 m 的第 i 个 `sub_match` 的常量引用；`m[0]` 表示完整匹配。

如果 i>= size()，则 `m[i]` 表示一个代表未匹配子表达式的 `sub_match`。

`n=m.length(i)` `n=m[i].length()`；`m[i]` 中的字符数量 `n=m.length()`。

`n=m.length(0)`。

`pos=m.position(i)` `pos=m[i].first`；`m[i]` 的第一个字符。

`pos=m.position()` `pos=position(0)`。

`s=m.str(i)` `s=m[i].str()`；`m[i]` 的字符串表示。

`s=m.str()` `s=m.str(0)`。

`sm=m.prefix()` sm 是一个 `sub_match`，表示输入字符串中位于匹配项之前、未被 m 匹配的字符 `sm=m.suffix()` sm 是一个 `sub_match`，表示输入字符串中位于匹配项之后、未被 m 匹配的字符。

# regex<C,Tr> 匹配项和子匹配项（续）（§iso.28.9，§iso.28.10）

`p=m.begin()` p 指向 m 的第一个 `sub_match`。

`p=m.end()` p 指向 m 的最后一个 `sub_match` 之后的位置。

`p=m.cbegin()` p 指向 m 的第一个 `sub_match`（常量迭代器）。

`p=m.cend()` p 指向 m 的最后一个 `sub_match` 之后的位置（常量迭代器）。

`a=m.get_allocator()` a 是 m 的分配器。

`m.swap(m2)` 交换 m 和 m2 的状态。

`m==m2` m 和 m2 的 `sub_matches` 值是否相等？

`m!=m2` !(m==m2)。

我们可以使用下标运算符访问 `sub_match`，例如 `m[i]`。如果下标 i 指向不存在的 `sub_match`，则 `m[i]` 的结果表示一个未匹配的 `sub_match`。例如：

```
void test() {
regex pat "((AAAA)(BBB)?") ; string s = "AAAA";
smatch m;
regex_search(s,m,pat);

cout << boolalpha;
cout << m[0].matched << '\n'; cout << m[1].matched << '\n'; cout << m[2].matched << '\n'; cout << m[3].matched << '\n';
}
// true:wefound a match
// true:there was a first sub_match
// false: no second sub_match
// false: there couldn’t be a third sub_match for pat
```

- `match_not_eol`

- `match_not_bow`

- `match_not_eow`

- `match_any`

- `match_not_null`

- `match_continuous`

字符 ^ 不被视为表示“行首”。

字符 $ 不被视为表示“行尾”。

`\b` 不匹配子序列 [first,first)。

`\b` 不匹配子序列 [last,last)。

如果存在多个可能的匹配，则任意一个匹配均可接受。

不要匹配空序列。

仅匹配从 first 开始的子序列。

`match_prev_avail` --first 是一个有效的迭代器位置。

# 37.3.1 regex_match()

若要查找与整个序列匹配的模式（例如长度已知的一行文本），请使用 `regex_match()`：

第 37.3.1 节 `regex_match()` 1063

- `regex_match(b,e ,m,pat,flags)`

- `regex_match(b,e ,m,pat)` `regex_match(b,e ,pat,flags)` `regex_match(b,e ,pat)`

- `regex_match(x,m,pat,flags)`

# 正则表达式匹配（§iso.28.11.2）

匹配由 `match_flag_type` 选项控制（§37.3）。

输入 [ b:e) 是否与正则表达式模式 pat 匹配？

将结果放入 `match_results` m 中；使用选项 flags。

`regex_match(b,e ,m,pat,regex_constants::match_default)` 输入 [b:e) 是否与正则表达式模式 pat 匹配？使用选项 flags。

`regex_match(b,e ,pat,regex_constants::match_default)` 输入 x 是否与正则表达式模式 pat 匹配？

x 可以是 `basic_string` 或 C 风格字符串；

将结果放入 `match_results` m 中；使用选项 flags。

- `regex_match(x,m,pat)` `regex_match(x,m,pat,regex_constants::match_default)`

- `regex_match(x,pat,flags)` 输入 x 是否与正则表达式模式 pat 匹配？

- x 可以是 `basic_string` 或 C 风格字符串；使用选项 flags `regex_match(x,pat)`

- `regex_match(x,pat,regex_constants::match_default)`

例如，考虑一个用于验证表格格式的简单程序。如果表格格式符合预期，程序会将“all is well”写入 cout；否则会将错误消息写入 cerr。表格由一系列行组成，每行包含四个以制表符分隔的字段，但第一行（标题行）可以只有三个字段。例如：

班级 男生 女生 总计

1a 12 15 27

1b 16 14 30

`regex_search(b,e ,m,pat)`

`regex_search(b,e ,pat,flags)`

`regex_search(b,e ,m,regex_constants::match_default)` 输入 [b:e) 是否包含与正则表达式模式 pat 匹配的内容？使用选项 flags。

`regex_search(b,e ,pat)`

`regex_search(x,m,pat,flags)`

`regex_search(b,e ,pat,regex_constants::match_default)` 输入 x 是否包含与正则表达式模式 pat 匹配的内容？x 可以是 `basic_string` 或 C 风格字符串；将结果放入 `match_results` m 中；使用选项 flags。

`regex_search(x,m,pat)` `regex_search(x,m,pat,regex_constants::match_default)`

`regex_search(x,pat,flags)` 输入 x 是否包含与正则表达式模式 pat 匹配的内容？x 可以是 `basic_string` 或 C 风格字符串；使用选项 flags。

`regex_search(x,pat)` `regex_search(x,pat,regex_constants::match_default)`

例如，我可以使用如下方式查找我的名字的一些常见拼写错误：

## 第 37.3.2 节 regex_search() 1065

```
regex pat "{[Ss]tro?u?v?p?stra?o?u?p?b?}";
smatch m;
for (string s; cin>>s; )
if (regex_search(s,m,pat))
if (m[0]!=“stroustrup” && m[0]!=“Stroustrup” )
cout << “Found: ” << m[0] << ‘\n’;
```

给定适当的输入后，该程序将输出 Stroustrup 的错误拼写，例如：

Found: strupstrup

Found: Strovstrup

Found: stroustrub

Found: Stroustrop

注意，`regex_search()` 即使在模式被其他字符“隐藏”时，也能找到该模式。例如，它会在 abstrustrubal 中找到 strustrub。如果希望将模式与输入字符串中的每个字符进行匹配，请使用 `regex_match`（§37.3.1）。

# 37.3.3 regex_replace()

若要对序列（例如文件）的一部分中的模式进行简单替换，请使用 `regex_replace()`：正则表达式替换（§iso.28.11.4）。

匹配由 `match_flag_type` 选项控制（§37.3）。

`out=regex_replace(out,b,e ,pat,fmt, flags)` 将 [b:e) 复制到 out，同时搜索正则表达式模式 pat；找到与 pat 的匹配项后，使用由 flags 控制的格式 fmt 将其复制到 out；fmt 可以是 `basic_string` 或 C 风格字符串。

`out=regex_replace(out,b,e ,pat,fmt)` `out=regex_replace(out,b,e ,pat,fmt, regex_constants::match_defaults)`。

`s=regex_replace(x,pat,fmt,flags)` 将 x 复制到 s，同时搜索正则表达式模式 pat；找到与 pat 的匹配项后，使用以下格式将其复制到 s。

格式 `fmt` 由 `flags` 控制；

`x` 可以是 `basic_string` 或 C 风格字符串；`fmt` 可以是 `basic_string` 或 C 风格字符串。

`s=regex_replace(x,pat,fmt)` `s=regex_replace(x,pat,fmt, regex_constants::match_defaults)`。

格式复制使用正则表达式的 `format()`（§37.2.2）完成，并采用 `$` 前缀表示法，例如，$& 表示匹配项，$2 表示第二个子匹配项。下面是一个小型测试程序，它接受由单词和数字组成的字符串对，并将其按每行一个 `{word,number}` 的形式输出：

```
void test1() {
string input {"x 1 y2 22 zaq 34567"};
regex pat {"(\w+)\s(\d+)"}; // word space number string format {"{$1,$2}\n"};
cout << regex_replace(input,pat,format);
}
```

输出为：

```
{x,1}
{y2,22}
{zaq,34567}
```

注意行首令人恼火的“多余”空格。默认情况下，`regex_match()` 会将未匹配的字符复制到其输出中，因此 pat 未匹配的两个空格也会被打印出来。

若要消除这些空格，可以使用 `format_no_copy` 选项（§37.2.2）：

```
cout << regex_replace(input,pat,format,regex_constants::format_no_copy); Now we get:
```

```
{x,1}
{y2,22}
{zaq,34567}
```

子匹配项不必按顺序输出：

```
void test2()
{
string input {"x 1 y 2 z 3"};
regex pat {"(\w)\s(\d+)"}; // word space number string format {"$2: $1\n"};
cout << regex_replace(input,pat,format,regex_constants::format_no_copy); }
```

现在输出为：

```
1: x
22: y2
34567: zeq
```

# 37.4 正则表达式迭代器

`regex_search()` 函数允许我们在数据流中查找模式的一次出现。如果我们想查找所有此类出现并对它们执行某些操作，该怎么办？如果数据被组织为一系列易于识别的行或记录，我们可以遍历这些行或记录，并对每一个使用 `regex_match()`。如果我们要对模式的每次出现执行的操作只是简单替换，则可以使用 `regex_replace()`。如果我们希望遍历一个字符序列，并对模式的每次出现执行某些操作，则可以使用 `regex_iterator`。

### 第 37.4 节 正则表达式迭代器 1067

# 37.4.1 regex_iterator

`regex_iterator` 是一种双向迭代器；每次递增时，它都会在序列中搜索模式的下一次匹配：

```
template<class Bi,
class C = typename iterator_traits<Bi>::value_type ,
class Tr = typename regex_traits<C>::type>
class regex_iterator {
public:
using regex_type = basic_regex<C,Tr>;
using value_type = match_results<Bi>;
using difference_type = ptrdiff_t;
using pointer = const value_type*;
using reference = const value_type&;
using iterator_category = forward_iterator_tag;
// ...
}
```

`regex_traits` 的相关内容见 §37.5。

系统提供了通常的一组别名：

```
using cregex_iterator = regex_iterator<const char *>;
using wcregex_iterator = regex_iterator<const wchar_t*>;
using sregex_iterator = regex_iterator<string::const_iterator>;
using wsregex_iterator = regex_iterator<wstring::const_iterator>;
```

`regex_iterator` 提供一组最基本的迭代器操作：

```
regex_iterator p {};
regex_iterator p {b,e,pat,flags); regex_iterator p {b,e,pat); regex_iterator p {q);
p=q
p==q
regex_iterator<Bi,C,Tr> (§iso.28.12.1)
```

p 是序列末尾。

遍历 [b:e)，使用选项 flags 查找 pat 的匹配项。

p 使用 {b,e,pat,regex_constants::match_default} 初始化。

复制构造函数（无移动构造函数）。

复制赋值（无移动赋值）。

`p` 是否与 `q` 指向同一个 `sub_match`？

```
p!=q !(p==q)
c=*p c is the current sub_match
x=p->m x=(*p).m
++p Make p point to the next occurrence of p’s pattern q=p++ q=p, then ++p
```

`regex_iterator` 是双向迭代器，因此我们不能直接迭代 `istream`。例如，我们可以输出 `string` 中所有以空白分隔的单词：
