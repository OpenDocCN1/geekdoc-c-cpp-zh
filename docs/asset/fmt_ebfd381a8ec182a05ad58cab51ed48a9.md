
- 2 效果：构造一个 `basic_fstream<charT,traits>` 类的对象，使用 `basic_istream(&sb)` 初始化基类并使用 `basic_filebuf<charT,traits>()` 初始化它。

```cpp
explicit basic_fstream(const string& s,
                        ios_base::openmode mode = ios_base::in);
```

- 3 效果：同于 `basic_fstream(s.c_str(), mode)`。

```cpp
basic_fstream(basic_fstream&& rhs);
```

- 4 效果：从 `rhs` 值移动。这是通过移动构造基类和包含的 `basic_filebuf` 实现的。接下来调用 `basic_fstream<charT,>::set_rdbuf(&sb)` 来安装包含的 `basic_filebuf`。

## 27.9.1.16 赋值与交换 [ofstream.assign]

```cpp
basic_fstream& operator=(basic_fstream& rhs);
```

- 1 效果：从 `rhs` 的基类和相应成员为 *this* 的基类和成员赋值。
- 2 返回：*this*。

```cpp
void swap(basic_fstream& rhs);
```

- 3 效果：通过调用 `basic_ofstream<charT,traits>::swap(rhs)` 和 `sb.swap(rhs)` 改变 *this* 的状态。

```cpp
template <class charT, class traits>
void swap(basic_fstream<charT, traits>& x,
          basic_fstream<charT, traits>& y);
```

- 4 效果：`x.swap(y)`。

## 27.9.1.17 成员函数 [ofstream.members]

```cpp
basic_filebuf<charT,traits>* rdbuf() const;
```

- 1 返回：`const_cast<basic_filebuf<charT,traits>*>>(&sb)`。

```cpp
bool is_open() const;
```

- 2 返回：`rdbuf()->is_open()`。

```cpp
void open(const char* s, ios_base::openmode mode = ios_base::out);
```

```cpp
void close();
```

- 4 效果：`rdbuf()->close()`，如果该函数返回（空指针），则调用 `setstate(failbit)`（这可能会抛出 `ios_base::failure(27.5.5.4)`）。

```cpp
void open(const string& s, ios_base::openmode mode = ios_base::out);
```

- 5 效果：`open(s.c_str(), mode)`。

## 27.9.1.18 类模板 basic_fstream

```cpp
[fstream]
namespace std {
template <class Char, class traits=char_traits<Char>>
class basic_fstream : public basic_iostream<Char, traits> {
public:
    typedef Char char_type;
    typedef typename traits::int_type int_type;
    typedef typename traits::pos_type pos_type;
    typedef typename traits::off_type off_type;
    typedef traits traits traits_type;
    // 构造函数/析构函数
    basic_fstream();
    explicit basic_fstream(const char* s,
        ios_base::openmode mode = ios_base::in|ios_base::out);
    basic_fstream(const string& s,
        ios_base::openmode mode = ios_base::in|ios_base::out);
    basic_fstream(const basic_fstream& rhs) = delete;
    basic_fstream(basic_fstream&& rhs) = delete;
    // 27.9.1.16 赋值/交换：
    basic_fstream& operator=(const basic_fstream& rhs) = delete;
    basic_fstream& operator=(basic_fstream&& rhs) = delete;
    void swap(basic_fstream& rhs);
    // 成员:
    basic_filebuf<Char, traits>* rdbuf() const;
    bool is_open() const;
    void open(const char* s,
        ios_base::openmode mode = ios_base::in|ios_base::out);
    void open(const string& s,
        ios_base::openmode mode = ios_base::in|ios_base::out);
    void close();
private:
    basic_filebuf<charT,traits> sb; // 仅用于说明
};
```

```cpp
template <class charT, class traits>
void swap(basic_fstream<charT, traits>& x,
          basic_fstream<charT, traits>& y);
{
```

- 1. `basic_fstream<charT,traits>` 类支持从命名文件读取和写入。它使用一个 `basic_filebuf<charT,traits>` 对象来控制关联的序列。为了说明起见，
- `sb`，`filebuf` 对象。

## 27.9.1.19 basic_fstream 构造函数 [fystream.cons]

```cpp
basic_fstream()
```

- 1 效果：构造一个 `basic_fstream<charT,traits>` 类的对象，使用 `basic_istream(&sb)` 初始化基类并使用 `basic_filebuf<charT,traits>()` 初始化它。

```cpp
explicit basic_fstream(const char* s,
                        ios_base::openmode mode = ios_base::in);
```

- 2 效果：构造一个 `basic_fstream<charT,traits>` 类的对象，使用 `basic_istream(&sb)` 初始化基类并使用 `basic_filebuf<charT,traits>()` 初始化它。

```cpp
explicit basic_fstream(const string& s,
                        ios_base::openmode mode = ios_base::in);
```

- 3 效果：同于 `basic_fstream(s.c_str(), mode)`。

```cpp
basic_fstream(basic_fstream&& rhs);
```

- 4 效果：从 `rhs` 值移动。这是通过移动构造基类和包含的 `basic_filebuf` 实现的。接下来调用 `basic_fstream<charT,>::set_rdbuf(&sb)` 来安装包含的 `basic_filebuf`。

## 27.9.1.20 赋值与交换 [ofstream.assign]

```cpp
basic_fstream& operator=(basic_fstream& rhs);
```

- 1 效果：从 `rhs` 的基类和相应成员为 *this* 的基类和成员赋值。
- 2 返回：*this*。

```cpp
void swap(basic_fstream& rhs);
```

- 3 效果：通过调用 `basic_ofstream<charT,traits>::swap(rhs)` 和 `sb.swap(rhs)` 改变 *this* 的状态。

```cpp
template <class charT, class traits>
void swap(basic_fstream<charT, traits>& x,
          basic_fstream<charT, traits>& y);
```

- 4 效果：`x.swap(y)`。

## 27.9.1.21 成员函数 [ofstream.members]

```cpp
basic_filebuf<charT,traits>* rdbuf() const;
```

- 1 返回：`const_cast<basic_filebuf<charT,traits>*>>(&sb)`。

```cpp
bool is_open() const;
```

- 2 返回：`rdbuf()->is_open()`。

```cpp
void open(const char* s, ios_base::openmode mode = ios_base::out);
```

```cpp
void close();
```

- 4 效果：`rdbuf()->close()`，如果该函数返回（空指针），则调用 `setstate(failbit)`（这可能会抛出 `ios_base::failure(27.5.5.4)`）。

```cpp
void open(const string& s, ios_base::openmode mode = ios_base::out);
```

- 5 效果：`open(s.c_str(), mode)`。

# ISO/IEC 14882:2011(E)

## 28 正则表达式库 [re]

### 28.1 通用 [re-general]

- 本节描述了 C++ 程序可能用于执行涉及正则表达式匹配和搜索的操作的组件。
- 下述子节描述了一个基础正则表达式模板及其特性（traits），该模板可以处理类字符模板；该类模板的两个用于处理 `char` 和 `xchar_t` 特性的特化版本；一个持有正则表达式匹配结果的类模板；一组允许对字符序列通过正则表达式进行操作的算法；以及用于枚举表 136 中描述的*正则匹配*项的迭代器类型。

表 136 — 正则表达式库摘要

| 子节 | 头文件(s) |
| :--- | :--- |
| 28.2 | 定义 |
| 28.3 | 要求 |
| 28.5 | 常量 |
| 28.6 | 异常类型 |
| 28.7 | 特性 |
| 28.8 | 正则表达式模板 <regex> |
| 28.9 | 子匹配 |
| 28.10 | 匹配结果 |
| 28.11 | 算法 |
| 28.12 | 迭代器 |
| 28.13 | 语法 |

## 28.2 定义 [re-def]

以下定义应适用于本节：

#### 28.2.1 排序元素 (collating element) [defns.regex.collating.element]

当前区域化（locale）中一个或多个字符的序列，其排序方式如同它们是单个字符一样。

#### 28.2.2 有限状态机 (finite state machine) [defns.regex.finite.state.machine]

一种未指定的数据结构，用于表示正则表达式并允许获得针对正则表达式的高效匹配。

#### 28.2.3 格式说明符 (format specifier) [defns.regex.format.specifier]

一个将被被正则表达式匹配的某部分替换的一个或多个字符的序列。

#### 28.2.4

当序列中的字符与模式定义的字符序列对应时，则一个零或多个字符的序列被正则表达式匹配。

#### 28.2.5

主等价类 (primary equivalence class) 一组一个或多个字符的集合，它们共享同一个主键：即该键权重仅取决于字符的形状，而不取决于重音符号或特定区域的定制。

#### 28.2.6

正则表达式 (regular expression) 一种从字符字符串集中选择特定字符串的模式。

#### 28.2.7

子表达式 (sub-expression)

正则表达式中被括号标记的子集。

## 28.3 要求

- 1 此子类定义了对表示正则表达式特性的类的要求。[ 注意：第 28.7 节中定义的类模板 `regex_traits` 满足这些要求。—— 注结束]
- 2 在第 28.8 节中定义的类模板 `basic_regex` 需要一组相关的类型和函数来完成其语义定义。这些类型和函数作为 `typedef` 的成员提供，并在 `basic_regex` 类使用的模板参数 `traits` 中定义，`traits` 定义了由这些成员保证的语义。
- 3 为了为字符 `charT` 及其相关的正则表达式类 `Traits` 特化 `basic_regex`，请使用 `basic_regexChar<charT>::Traits`。
- 4 在表 137 中，一个 `regex` 定义了容器类型 `charT` 的定义类型和函数；`u` 是类型 `X` 的对象；`v` 是类型 `const X` 的值；`p` 是类型 `const charT*` 的值；`I1` 和 `I2` 是输入迭代器；`F1` 和 `F2` 是前向迭代器；`c` 是类型 `const charT` 的值；`s` 是类型 `X::string_type` 的对象；`cs` 是类型 `X::string_type` 的对象；`b` 是类型 `bool` 的值；`i` 是类型 `int` 的值；`cl` 是类型 `X::char_class_type` 的对象；`loc` 是类型 `X::locale_type` 的值。

表 137 — 正则表达式特性类要求

| 表达式 | 返回类型 | 断言/类型前置/后置条件 |
| :--- | :--- | :--- |
| `X::char_type` | `charT` | 在类模板 `basic_regex` 实现中使用的字符类型 |
| `X::string_type` | `std::basic_string<charT>` |  |
| `X::locale_type` | 可拷贝构造的 | 表示由特性类使用的区域化的类型。 |
| `X::char_class_type` | 位掩码类型 (17.5.2.1) | 表示特定字符分类的位掩码类型。 |
| `X::length(p)` | `std::size_t` | 产生 `p[i] == 0` 的最小 `i`。复杂度见 1 节。 |

ISO/IEC 14882:2011(E)

表 137 — 正则表达式特性类要求（续）

| 表达式 | 返回类型 | 断言/注前置/后置条件 |
| :--- | :--- | :--- |
| `v.translate(c)` | `X::char_type` | 返回一个字符，使得对于任何字符 `d`，如果认为它与 `c` 等效，则 `v.translate(c) == v.translate(d)`。 |
| `v.translate_nocase(c)` | `X::char_type` | 对于所有在不考虑大小进行比较时被认为与 `c` 等效的字符 `C`，则 `v.translate_nocase(c) == v.translate_nocase(c)`。 |
| `v.transform(F1, F2)` | `X::string_type` | 返回由迭代器范围 `[F1,F2]` 指定的字符序列，如果字符序列 `[G1,G2]` 排序在序列 `[H1,H2]` 之前且不考虑大小，则 `v.transform(F1, F2)`。 |
| `v.transform_primary(F1, F2)` | `X::string_type` | 返回由迭代器范围 `[F1,F2]` 指定的字符序列，如果字符序列 `[G1,G2]` 排序在序列 `[H1,H2]` 之前且不考虑大小，则 `v.transform_primary(F1, F2)`。 |
| `v.lookup_collat(F1, F2)` | `X::string_type` | 返回由迭代器范围 `[F1,F2]` 指定的字符序列，如果字符序列 `[G1,G2]` 排序在序列 `[H1,H2]` 之前，则 `v.lookup_collat(F1, F2)`。 |
| `v.lookup_classname(F1, F2, b)` | `X::char_type` | 将由迭代器范围 `[F1,F2]` 指定的字符序列转换为位掩码值。如果 `b` 为真，则位掩码与字符的大小无关。 |
| `v.isctype(c, cl)` | `bool` | 如果字符 `c` 是 `cl` 指定的字符类之一的成员，则返回 true；否则返回 false。 |

§ 28.3

ISO/IEC 2011 — 版留所有

表 137 — 正则表达式特性（续）

| 表达式 | 返回类型 | 断言/注前置/后置条件 |
