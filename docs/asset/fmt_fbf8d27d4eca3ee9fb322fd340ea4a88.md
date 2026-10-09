
```cpp
// 29.11.6.5.2, 赋值
path operator=(const path& p);
path operator=(const path& p) noexcept;
path operator=(const string_type& source);
path assign(const string_type& source);
template<class Source>
path operator=(const Source& source);
template<class Source>
path assign(const Source& source);
template<class InputIterator>
path assign(InputIterator first, InputIterator last);

// 29.11.6.5.3, 附加
path operator/=(const path& p);
template<class Source>
path operator/=(const Source& source);
template<class Source>
path append(const Source& source);
template<class InputIterator>
path append(InputIterator first, InputIterator last);

// 29.11.6.5.4, 拼接
path operator*=(const path& x);
path operator*=(const string_type& x);
path operator*=(const std::string_view<value_type>& x);
path operator*=(const value_type& x);
template<class Source>
path operator*=(const Source& x);
template<class charT>
path operator*=(const charT x);
template<class Source>
path concat(const Source& x);
template<class InputIterator>
path concat(InputIterator first, InputIterator last);

// 29.11.6.5.5, 修改器
void clear() noexcept;
path make_preferred();
path remove_filename();
path replace_filename(const path& replacement);
path replace_extension(const path& replacement = path());
void swap(path& lhs, path& rhs) noexcept;

// 29.11.6.5.8, 非成员运算符
friend bool operator==(const path& lhs, const path& rhs) noexcept;
friend bool operator<=(const path& lhs, const path& rhs) noexcept;
friend path operator/(const path& lhs, const path& rhs);

// 29.11.6.9, 原生观测器
const string_type& native() noexcept;
const value_type* c_str() noexcept;
operator string_type() const;

template<class charT, class traits = char_traits<charT>,
template<class Allocator = allocator<charT>>
basic_string<charT, traits, Allocator> string(const Allocator& a = Allocator()) const;
std::string string(const Allocator& a = Allocator()) const;

std::wstring wstring() const;
std::ustring ustring() const;
std::u32string u32string() const;

// 29.11.6.5.7, 通用格式化
template<class charT, class traits = char_traits<charT>,
template<class Allocator = allocator<charT>>
basic_string<charT, traits, Allocator> generic_string(const Allocator& a = Allocator()) const;
std::string generic_string() const;
std::wstring generic_string() const;
std::ustring generic_string() const;
std::u32string generic_string() const;

// 29.11.6.5.8, 比较
int compare(const char& p) const noexcept;
int compare(const string_type& s) const;
int compare(basic_string_view<value_type> s) const;
int compare(const value_type* s) const;

// 29.11.6.5.9, 分解
path name() const;
path directory() const;
path root() const;
path relative_path() const;
path parent_path() const;
path filename() const;
path stem() const;
path extension() const;

// 29.11.6.5.10, 查询
[[nodiscard]] bool empty() const noexcept;
bool has_root_name() const;
bool has_root_directory() const;
bool has_root_path() const;
bool has_relative_path() const;
bool has_parent_path() const;
bool has_filename() const;
bool has_stem() const;
bool has_extension() const;
bool is_absolute() const;
bool is_relative() const;

// 29.11.6.5.11, 生成
path lexically_normal() const;
path lexically_relative(const path& base) const;
path lexically_proximate(const path& base) const;

// 29.11.6.6, 迭代器
class iterator;
using const_iterator = iterator;

iterator begin() const;
iterator end() const;

// 29.11.6.7, path 插入器和提取器
template<class charT, class traits>
friend basic_ostream<charT, traits>&
operator<<(basic_ostream<charT, traits>& os, const path& p);

template<class charT, class traits>
friend basic_istream<charT, traits>&
operator>>=(basic_istream<charT, traits>& s, path& p);
};
```

3 点文件名（dot-filename）被视为对目录的引用。点点文件名（dot-dot filename）被视为父目录。点点指向实现定义的*根目录*（root-directory）。特定的文件名对于特定的操作系统具有特殊含义。

4 根名（root-name）标识路径解析的起始位置（29.11.6）。如果没有操作系统根名，则至少需要一个实现根名（implementation-root-name）。

> [注 2: 许多操作系统将带有两个目录分隔符字符的名字定义为驱动器分隔符；标识单个字母后跟冒号的根名称为驱动器；标识特定设备（如磁盘）的根名。注终]

5 如果根名存在歧义，则选择字符序列最长的那个。

> [注 3: 在类 POSIX 操作系统上，不可能在没有中间根目录元素的情况下同时拥有根名和相对路径。注终]

6 通用格式路径名的归一化处理意味着：

- 1. 如果路径名为空，

- 2. 将根名中的每个斜符字符替换为*首选分隔符*（preferred-separator）。

- 3. 将每个目录分隔符替换为*首选分隔符*。

> [注 4: 通用路径名定义目录分隔符为一个或多个斜符以及首选分隔符。注终]

- 4. 删除任何点文件名以及紧随其后的任何目录分隔符。

- 5. 只要适用，就删除紧随*目录分隔符*和点文件名之后的非点文件名，以及紧随其后的任何目录分隔符。

- 6. 如果存在*根目录*，删除所有点文件名以及紧随其后的任何目录分隔符。

> [注 5: 这些点点文件名无法指向非父目录。注终]

- 7. 如果最后一个文件名是点点，则删除末尾的目录分隔符。

- 8. 如果路径为空，则添加一个点。

归一化的结果是一个标准形式的路径，被称为已归一化的路径。

## 29.11.6 转换

### 29.11.6.3 参数格式转换

1 本节中描述的格式转换不适用于基于 POSIX 的操作系统，原因由于这些因素：

- (1.1) 通用格式可以作为路径名接受。

- (1.2) 参数中没有必要区分原生格式和通用格式。

- (1.3) 普通文件和目录的路径遵循相同的语法。

> 注终

2 定义了几个函数来接受*检测格式参数*（detected-format arguments），这些参数是字符序列。检测格式参数表示使用通用格式（29.11.6）的路径名，或者如果它匹配通用格式且被操作系统作为原生路径接受，则使用原生格式的路径名。

> [注 2: 某些操作系统没有无歧义的方法来区分原生格式和通用参数。这是为了简化不需要消除歧义的操作系统的使用。如果需要，操作系统的实现需要区分通用格式和原生格式。注终]

3 路径名根据操作系统的不同在通用格式和原生格式之间按需转换。在数学上，让 G(n) 和 N(g) 分别为实现中将原生到通用以及通用到原生格式转换的函数。如果对于某些 n 有 g=G(n)，则 N(G(n))=g；如果 n=N(g)

> [注 3: 不需要 N。]

5 如果原生格式要求文件路径的格式与目录路径不同，如果路径的最后一个元素是*目录分隔符*，则该路径应被视为目录路径，否则应被视为指向普通文件的路径。

> [注 4: 路径存储原生格式路径名（29.11.6.5），并在需要时表现得也存储了通用格式路径名。实现可以从原生路径名（以及可能的其他信息）生成通用格式路径名。注终]

7 当从通用表示构造路径时，另一种表示由适当的转换函数（G 或 N）选择。

8 当路径的一种表示的（新的）值 p 派自另一个表示时，如果该值（通过合适的 G 或 N）转换为 q；否则未指定。

> [注 5: 如果它是转换路径的结果，它是转换 p 的结果。注终]

## 29.11.6.3 类型和编码

1 普通字符字符串的原生编码是取决于操作系统的路径编码（29.11.6）。宽字符字符串的原生编码是实现的宽字符集（5.3）。

2 对于表示路径的字符序列的成员函数以及返回字符串的成员函数，如果参数或返回值于 `value_type`，则执行类型和编码转换。要转换的编码由其值决定：

- (2.1) char: 原生编码。如果有转换方法，由系统指定。[注 1: 对于基于 POSIX 的操作系统，从 char 值执行；对于基于 Windows 的操作系统，原生编码由调用 Windows API 定义。注终]

- (2.2) wchar_t: 原生编码是宽编码。转换方法未指定。[注 2: 对于使用普通字符串转换的 C++ 标准库函数，这种行为可能令人惊讶并返回错误。注终]

- (2.3) char_t: 编码为 UTF-8。转换方法未指定。

- (2.4) char16_t: 编码为 UTF-16。转换方法未指定。

- (2.5) char32_t: 编码为 UTF-32。转换方法未指定。

3 如果编码转换没有源，则产生的字符未指定。实现不应修改 `value_type` 类型的成员函数参数。

## 29.11.6.4 要求

1 除 (29.11.3) 外，名为 Source 的函数模板参数应该是之一：

- (1.1) basic_string<CharT, Allocator>。函数 const Source& 的有效范围为 [source.begin(), source.end())。

- (1.3) 匹配迭代 NCTCS 的 InputIterator 类型。值类型应该是编码字符类型。函数 const Source& 的有效范围为 [source, end)，其中 end 是元素值为 iterator_traits<decay<Source>>::value_type 的迭代器。

- (1.4) 字符数组到指针的结果指向 NCTCS 起始的指针。值类型应该是编码字符类型。函数 const Source& 的有效范围为 [source, end)，其中 end 是元素值为 iterator_traits<decay<Source>>::value_type 的迭代器。

2 除非 Source 表示 path 以外的类型，否则名为 Source 的函数模板参数不参与重载：

- (2.1) Source 是 `basic_string` 或 `basic_string_view` 的特化，

- (2.2) iterator_traits::decay_t<Source>::value_type 是有效的，且可能是 const 编码字符类型。

3 [注 1]: 查看路径（29.11.6）以了解上述值类型及其编码如何转换为 path::value_type 及其编码。

-4 Source 类型的参数不为空指针。

## 29.11.6.5 成员

### 29.11.6.5.1 构造函数

```
path() noexcept;
```

1 后置条件：empty() == true。

```
path(const path& p);
path(const path&& p) noexcept;
```

2 效果：构造一个 path 对象，其原生和通用格式分别为 p 的原始值。在第二种形式中，p 处于有效但未定义的状态。

```
path(string_type&& s, format fmt = auto_format);
```

3 效果：构造一个 path 对象，其源的检测格式的路径名为 source 的原始值（29.11.6.1），在需要时转换格式（29.11.6.3）。source 处于有效但未定义的状态。

```
template<class Source>
path(const Source& s, locale loc, format fmt = auto_format);
template<class Iterator>
path(Iterator first, Iterator last, locale loc, format fmt = auto_format);
```

4 强制：Source 和 InputIterator 的值类型为 char。

5 效果：让 s 为 source 的有效范围（29.11.6.4）或范围 [first, last)，并带有（29.11.6.3）所需的编码。找到 s 的检测格式（29.11.6.3.1），并构造一个格式为 s 的 path 对象。

5 强制：

6 效果：让有效范围或范围 [first, last)，按以下方式转换编码：

- (6.1) — 如果 value_type 是 wchar_t，使用 loc 的观念<wchar_t, char, mbstate_t> 转换为原生编码（29.11.6.2）。

- (6.2) — 否则使用 loc 的观念<wchar_t, char, mbstate_t> 进行转换，然后转换为当前原生编码。

- 7 从（29.11.6.1）找到解码后的路径，并构造一个格式为 s 的 ISO/IEC 8859-1 的 path 对象，并创建一个目录：

> [示例 1: 从以 ISO/IEC 8859-1 编码的数据库读取字符串，创建一个目录：

```
namespace fs=std::filesystem;
std::string latin1_string = read_latin1_data();
codecvt<wchar_t, char, mbstate_t> latin1_facet;
std::locale locale(std::locale(0), latin1_facet);
fs::create_directory(fs::path(latin1_string.c_str(), locale));
```

# ISO/IEC 14882:2020(E)

对于基于 Windows 的操作系统，路径的构造使用 latin_facet 将 ISO/IEC 8859-1 编码的 latin_string 转换为 UTF-16 编码的宽字符路径名字符串。ISO/IEC 8859-1 字符集中的所有字符将转换为 Unicode 表示法。— 结束

## 29.11.6.5 赋值
