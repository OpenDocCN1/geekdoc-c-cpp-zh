
- 13 返回：`this`。

```cpp
void swap(path& rhs) noexcept;
```

- 14 效果：交换两个路径所有格式的内容。

- 15 复杂度：常数时间。

# 30.10.8.4.6 path 本地格式访问 [fs.path.native_obs]

1. 所有本地格式访问返回的字符串均为本地格式（30.10.4）。

```cpp
const string_type& name() const noexcept;
```

- 2 返回：本地格式的路径名。

```cpp
const value_type* c_str() const noexcept;
```

- 3 返回：等于 `native().c_str()`。

```cpp
operator string_type() const;
```

- 4 返回：`native()`。

- 5 [注：提供到 `string_type` 的转换是为了让 `path` 类对象作为标准库文件构造函数和操作函数的参数传递。]

```cpp
template <class EChar, class traits = char_traits<EChar>,
class Allocator = allocator<EChar>>
basic_string<EChar, traits, Allocator>
    string(const Allocator& a = Allocator()) const;
```

- 6 返回：`native%`。

7 说明包括返回值在内的所有内存分配都应由 `a` 执行。转换（如果有）由 30.10.8.2 指定。

```cpp
std::string string() const;
std::wstring wstring() const;
std::ustring ustring() const;
std::u16string u16string() const;
std::u32string u32string() const;
```

- 8 返回：路径名。

- 9 说明：转换（如果有）由 30.10.8.2 指定。字符串的编码始终是 UTF-8。

# 30.10.8.4.7 path 通用格式访问 [fs.path.generic]

- 1 通用对象函数返回格式化为通用格式（30.10.8.1）的字符串。使用单斜杠 (`/`) 作为目录分隔符。

- 2 示例：在用反斜杠作为首选分隔符的操作系统上，`path("home\bar").generic_string()` 返回 `"home/bar"`。

```cpp
template <class EChar, class traits = char_traits<EChar>,
class Allocator = allocator<EChar>>
basic_string<EChar, traits, Allocator>
generic_string(const Allocator& a = Allocator()) const;
```

- 3 返回：通用格式的路径名。

- 4 说明：包括返回值在内的所有内存分配都应由 `a` 执行。转换（如果有）由 30.10.8.2 指定。

```cpp
std::string generic_string() const;
std::wstring generic_wstring() const;
std::ustring generic_ustring() const;
std::u16string generic_u16string() const;
std::u32string generic_u32string() const;
```

- 5 返回：通用格式的路径名。

- 6 说明：转换（如果有）由 30.10.8.2 指定。`generic_ustring()` 返回的字符串编码始终是 UTF-8。

# 30.10.8.4.8 path 比较 [fs.path.compare]

```cpp
int compare(const path& p) const noexcept;
```

- 1 返回：

- - 小于 0 的值，如果 `*this` 元素的 `native()` 字典排序小于 `p` 元素的 `native()`；否则，

- - 大于 0 的值，如果 `*this` 元素的 `native()` 字典排序大于 `p` 元素的 `native()`；否则，

# ISO/IEC 14882:2017(E)

(1.3) –.

备注：这些元素是通过对半开放范围 `["begin(), end)` 对于 `*this*` 和 `p` 进行迭代来确定的。

```
int compare(const string_type& s) const;
int compare(basic_string_view<value_type> s) const;
Returns: compare(s);
```

```
int compare(const value_type* s) const;
Returns: compare(s);
```

# 30.10.8.4.9 路径分解

[fs.path.decompose]

```
path_root() const;
Returns: root-name，如果通用格式下的 pathname 包含 root-name，否则返回 path()。
```

```
path_directory() const;
Returns: root-directory，如果通用格式下的 pathname 包含 root-directory，否则返回 path()。
```

```
root_path() const;
Returns: root_name() / root_directory();
```

```
path_relative() const;
Returns: 一个由通用格式下的 pathname 组成的路径，如果 empty() 为 false，则以 root-path 之后的第一个文件名开头。否则返回 path()。
```

```
parent_path() const;
Returns: 如果 has_relative_path() 为 false，返回 *this；否则返回一个其通用格式为通用 pathname *this 的最大前缀的路径，该路径在其迭代中产生一个元素。
```

```
filename() const;
Returns: relative_path().empty() ? path() : --end().
```

```
path_stem() const;
Returns: 设 f 为 filename 的通用 pathname 格式。返回一个 pathname 为
```

- - + f，如果它不包含除最后一个点以外的点，或者仅由一个或两个点组成；否则返回 f 中结束于其最后一个点之前的前缀。

- [示例：

```
std::cout << path("foo/bar.txt").stem(); // 输出 "bar"
path p = "foo.bar.tar";
for ( : ; !p.extension().empty(); p = p.stem()) {
    std::cout << p.extension() << '\n';
    // .tar
    // .bar
}
// 示例结束 [ ]
```

`path extension() const;`

- + 返回：一个其通用格式下的 pathname 为 `filename()` 中不包含在 `stem` 中的后缀的路径。

```
[示例]:
path("foo/bar.txt").extension(); // 生成 "txt" 且 stem() 为 "bar"
path("foo/bar.tar").extension(); // 生成 "tar" 且 stem() 为 "bar"
path("foo/profile").extension(); // 生成 ".profile" 且 stem() 为 "profile"
path(".bar").extension(); // 生成 "bar" 且 stem() 为 ""
path("").extension(); // 生成 ""
 示例结束
```

> 注意：返回值包含了点，以便区分没有扩展名和有扩展名。 — 备注结束

> 注意：在非 POSIX 操作系统上，对于路径 p，即使通用格式路径是相同的，`p.stem() + p.extension()` 也可能不等于 `p.filename()` — 备注结束

# 30.10.8.4.10 路径查询

```
[fs.path.query]
bool empty() const noexcept {
    Returns: 如果通用格式下的 pathname 为空，返回 true，否则返回 false。
}
bool root_path() const {
    Returns: .root_path().empty();
}
bool root_name() const {
    Returns: .root_name().empty();
}
bool root_directory() const {
    Returns: .root_directory().empty();
}
bool has_relative_path() const {
    Returns: .relative_path().empty();
}
bool has_parent_path() const {
    Returns: .parent_path().empty();
}
bool has_filename() const {
    Returns: .filename().empty();
}
bool has_stem() const {
    Returns: !stem().empty();
}
```

# ISO/IEC 14882:2017(E)

```cpp
bool has_extension() const;
Returns: !extension().empty();

bool is_absolute() const;
Returns: 如果通用形式下的 pathname 包含绝对路径，则返回 true。
> [示例：对于基于 POSIX 的操作系统，path("/").is_absolute() 为 true，对于基于 Windows 的操作系统则为 false。 — 示例结束]

bool is_relative() const;
Returns: !is_absolute();

path lexically_normal() const;
Returns: 通用形式下的路径是 *this 的通用 pathname 的规范形式。

path lexically_relative() const;
Returns: 较于 base 的此。不解析符号链接。
影响：如果 root_name() == base.name() 为 true 或 has_relative_path() && root_directory() 为 true，则返回路径和 base 中第一个匹配的元素如下：
```

`auto {a, b} = match(begin(), end(), base.end());`

```
然后：
- 如果 a == end() 且 b == end()，返回 path()；否则
- n 为 [b, end()) 中不是点的 filename 元素个数。如果 n != 0，返回 path()；否则
- 返回一个默认构造的 path 类对象，随后连续应用 operator() n 次，并对 {a, end) 中的中的每个元素执行该操作。上述断言均成功。在 Windows 上，返回的路径的目录分隔符字符将是反斜杠而非正斜杠，但这不影响路径相等性。 — 示例结束

> 注意：如果需要链接语义，请使用操作函数 relative()。

> 注意：如果需要规范化 (30.10.8.4) 以确保元素的一致匹配，请对 *this 应用 lexically_normal()，或者两者都应用 — 备注结束

path lexically_proximate(const path& base) const;
Returns: 如果 lexically_relative(base) 的值不是空路径，则返回它。否则返回 *this；
> 注意：如果需要链接语义，请使用操作函数 proximate() — 备注结束
> 注意：如果需要规范化 (30.10.8.4) 以确保元素的一致匹配，请对 *this 应用 lexically_normal()，或者两者都应用 — 备注结束

# 30.10.8 迭代器 [fs.path.iter]

- 1 迭代器遍历通用格式下的 pathname (30.10.8.1)。
- 2 `path::iterator` 满足双向迭代器 (27.2.6)的所有要求，除了可解引用迭代器和类型为 `path::iterator` 的 b 之外，没有要求 a 和 b 绑定到同一个对象。其 `value_type` 是 `path`。
- 3 调用 `path` 的任何非 const 方法都会使迭代器失效。4 对于通用格式的元素，其正向遍历顺序如下：
    - root-name，如果存在。
    - root-directory，如果存在。[注意：通用格式需要确保比较工作。 — 注意]
    - filename，如果存在。
    - 空元素，如果存在。
- 5 反向遍历是正向遍历的逆序。

```

iterator begin() const;

Returns: 第元素的迭代器。如果没有元素，则返回结束迭代器。

iterator end() const;

Returns: 结束迭代器。

```

# 30.10.8.6.1 路径插入器和提取器

[fs.path.io]

```

template <class charT, traits>

basic_ostream<<charT, traits>&

operator<<=(basic_ostream<charT, traits>& os, const path& p);

```

```

1 等同于：os << quoted(p.string<charT, traits>()); [注意：quoted 函数在 30.7.8 中有描述。 — 注意]

```

```

2 返回 os;

```

```

template <class charT, traits>

basic_istream<<charT, traits>&

operator>>=(basic_istream<charT, traits>& is, const path& p);

```

```

3 等同于：

basic_string<charT, traits> tmp;

is >> quoted(tmp);

p = tmp;

```

```

4 返回 is;

```

# 30.10.8.6.2 路径工厂函数

[fs.path.factory]

```

template <class Source>

path upath(const Source source);

```





# ISO/IEC 14882:2017(E)

template <class Iterator, Iterator last>
path u8path(Iterator first, Iterator last);

- 1 要求：源序列和 `[first, last]` 序列均为 UTF-8 编码。`Source` 和 `Iterator` 的值类型为 `char`。
- (2.1) 如果 `value_type` 为 `char` 且当前窄字符编码 (30.10.4) 为 UTF-8，返回 `path(source)` 或 `path(first)`；否则；
- (2.2) 如果 `value_type` 为 `wchar` 且原生宽编码为 UTF-16，或者 `value_type` 为 `char6_t` 或 `char32_t`，则将 `source` 从 `[first, last)` 转换为类型 `string_type` 的临时变量 `tmp` 并返回 `path(tmp)`；
- (2.3) 将 `source` 从 `[first, last)` 转换为类型 `u32string` 的临时变量 `tmp` 并返回 `path(tmp)`。

备注：参数格式 (30.10.8.2) 适用于这些函数的参数。未规定 Unicode 编码转换。

示例：从 UTF-8 编码的数据库读取一个字符串，并使用文件名的原生编码创建一个目录：
```cpp

namespace fs = std::filesystem;

std::string utf8_string = read_utf8_data();

fs::create_directory(fs::u8path(utf8_string));

```

对于原生窄字符编码设置为 UTF-8 的基于 POSIX 的操作系统，不会发生编码或类型转换。
对于原生窄字符编码未设置为 UTF-8 的基于 POSIX 的操作系统，会发生到 UTF-32 的转换，然后转换为当前的窄字符编码。某些 Unicode 字符没有原生字符表示。
对于基于 Windows 的操作系统，会发生从 UTF-8 到 UTF-16 的转换。 — 示例结束

# 30.10.9 filesystem_error [fs.filesystem_error]

```cpp

namespace std:: {

class filesystem_error : public system_error {

public:

    filesystem_error(const string& what_arg, error_code ec);

    filesystem_error(const string& what_arg,

                      const path& p1, error_code ec);

    filesystem_error(const string& what_arg,
