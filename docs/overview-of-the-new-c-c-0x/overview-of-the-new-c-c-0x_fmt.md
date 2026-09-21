
# 新 C++ (C++ 0x) 概览

Scott Meyers, 博士

软件开发顾问

smeyers@aristeia.com

http://www.aristeia.com/

电话: 503/638-6028

传真: 503/974-1888

这些是 Scott Meyers 培训课程“新 C++ (C++0x) 概述”的官方笔记。课程说明见 http://www.aristica.com/C++0x.html。许可信息见 http://aristeia.com/Licensing/licensing.html。

请将错误报告和改进建议发送至 smeyers@aristeia.com。

在这些笔记中，以 N 前缀的编号文档（例如 `N3290`）指的是 C++ 标准化文档。所有此类文档可通过 http://www.open-std.org/jtc/1sc22/wg21/docs/papers 访问。

对 C++0x 草稿章节的引用格式为 `[章节.节]`。这些符号名称在不同草稿之间不会改变。引用给出了章节号和（斜杠后的）特定草稿的段落；这些数字在不同草稿中可能会变化。因此，`[basic.fundamental]`（`N3290` 中的 3.9.1）指的是具有（永久）符号名称 `[basic.fundamental]` 的章节——特别是 `N3290` 中的 3.9.1 第 5 段。

注释（如本）是供授课的讲师使用的。所有注释对讲师和独立阅读笔记的人都应该有用。

第一天通常结束在讨论 C++0x 并发 API 的部分。第二天通常会到库材料的末尾。

## 引言

本课程是一个概述，因此没有时间介绍特性的细节。通常情况下，课程前面的特性（适用于更多程序员）比课程后面的特性有更深入的处理。右值引用未列出，因为它是移动语义的一部分。

## 1265 页

各种编译器对 C++0x 特性的支持见 http://www.aristeia.com/C++0x/Availability.htm。Boost 是唯一合并的部分。

课程中的部分代码未经过测试。我相信代码是正确的，但不保证。

临时对象是移动的理想候选者：

```cpp
std::vector<T> v;
...
v = create(); // C++98 中，工厂函数返回值到 v，然后销毁返回值
```

幻灯片上的图表构成了一个动画。在讨论中，我使用 `T` 容器而不是指定特定类型（例如 `string` 或 `int`）。移动语义的动机在很大程度上与类型无关，尽管类型越大、拷贝越贵，移动就越充分。

C++0x 将此类拷贝操作转换为移动请求：

```cpp
std::vector<T> v;
...
v = create(); // C++0x 中的隐式移动请求
```

幻灯片上的图表构成了一个动画。

移动语义将在以后讨论，但：

- 例如流对象、`std::thread` 对象、`std::unique_ptr` 等。

```
Alice_in_Wonderland.txt War_and_Peace.txt
Dracula.txt The_Kama_Sutra.txt The_Iliad.txt
```

显示的数据来自从 Project Gutenberg (http://www.gutenberg.org/) 下载的列书籍的纯文本版本。

```cpp
#include <stdio>                       // 格式化输出比 iostream 
#include <iostream>
#include <iterator>
#include <string>
#include <fstream>
#include <algorithm>
#include <vector>
#include <map>


WordCountMap wordsInFile(const char * const fileName) // 对于每个单词
{
    std::ifstream file;                                // 在文件中，返回
    WordCountMapType wordCounts;                            // 的
    for (std::string word; file >> word; ) {           // 出现
        ++wordCounts[word];
    }
    return wordCounts;
}
```

更好的软件工程是让 `wordsInFile` 检查文件名的有效性，然后调用另一个函数（例如 `wordsInStream`）来执行实际计数，但结果代码在串行情况（C++98）中会有些重复，在并发情况（C++0x）中会变得更加复杂，为了保持示例程序简单并专注于 C++0x 特性，我们假设每个通过的文件名都是合法的，即：我们接受“可能不会发生任何问题”的假设。

```cpp
struct Ptr2Pair2GT {
    template<typename It>
    bool operator()(It it1, It it2) { return it1->second < it2->second; }
}

template<typename Mapl>
void shiftCommonWords(Mapl begin, Mapl end, const std::size_t n) {
    typedef std::vector<Mapl> TempContainer;
    typedef TempContainer::iterator IterType;

    TempContainer wordlitters;
    wordlitters.reserve(distance(begin, end));
    for (Mapl i = begin; i != end; ++i) wordlitters.push_back(i);

    IterType sortedRangeEnd(wordlitters.begin(), wordlitters.end(), Ptr2Pair2GT());
    for (IterType it = wordlitters.begin(); it != sortedRangeEnd; ++it) {
        std::printf("-%10s%10lu\n", (it)->first.c_str(), (it)->second);
    }
}
```

对 `wordlitters` 使用范围初始化（即 `TempContainer wordlitters(begin, end)`）将是错误的，因为我们希望 `wordlitters` 包含的是迭代器本身，而不是迭代器所指向的内容。

使用 `"%u"` 来打印 `std::size_t` 类型的对象在技术上是不正确的，因为无法保证 `std::size_t` 一定是无符号的（例如 `unsigned long`）。技术上可移植的解决方案可能是使用 `"%lu"` 格式说明符并将 `(it*)second` 强制转换为 `unsigned long`（或将 `printf` 替换为 `iostreams`），但我选择了偷懒忽略了这个问题。除非在这个注释中：

```cpp
int main(int argc, const char** argv) { // 在命令行上获取文件名列表，
    // 打印内部最常见的20个单词
    WordCountMap wordCounts;
    for (int argNum = 1; argNum < argc; ++argNum) { // 拷贝由 wordsInFile 返回的
        const WordCountMap results = wordsInFile(argv[argNum]); // wordsInFile（忽略
        // 编译器优化）
        for (WordCountMapType::const_iterator i = results.begin(); i != results.end(); ++i) {
            wordCounts[i->first] += i->second;
        }
    }
    std::cout << wordCounts.size() << " words found. Most common:\n";
    const std::size_t maxWordsToShow = 20;
    showCommonWords(wordCounts.begin(), wordCounts.end());
    std::min(wordCounts.size(), maxWordsToShow);
}
```

`results` 是通过拷贝构造初始化的，由于 `WordCountMap` 是一个持有字符串的 map，这开销可能很大。因为这是一个初始化（而不是赋值），编译器可能会优化拷贝操作。

从技术上讲，`maxWordsToShow` 的类型应该是 `WordCountMap::size_type` 而不是 `std::size_t`，因为无法保证它们是相同类型（如果类型不同，对 `std::min` 的调用可能无法编译），但我并不知道有任何实现是不同的，且使用官方正确的格式会导致后续几页幻灯片中并排程序对比出现格式问题，所以我在这里抄了捷径。

```cpp
#include <cstdio>
#include <iostream>
#include <iterator>
#include <string>
#include <fstream>
#include <algorithm>
#include <vector>
#include <unordered_map>
#include <future>
```

```cpp
using WordCountMapType = std::unordered_map<std::string, std::size_t>;
WordCountMapType wordInFile(const char * const fileName) // 对于文件中的每个单词
{
    std::ifstream file(fileName); // 返回
    WordCountMapType wordCounts; // 统计
    for (std::string word; file >> word; ) { // 出现频次
        ++wordCounts[word];
    }
    return wordCounts;
}
```

```cpp
template<typename Maplt>
void showCommonWords(Maplt begin, Maplt end, const std::size_t n) {
  typedef std::vector<Maplt> TempContainerType;
  typedef typename TempContainerType::iterator iterType;
  std::vector<Maplt> wordslist;
  wordslist.reserve(distance(begin, end));
  for (auto i = begin; i != end; ++i) wordslist.push_back(i);
  auto sortedRangeEnd = wordslist.begin() + n;
  std::partial_sort(wordslist.begin(), sortedRangeEnd, wordslist.end(),
    [](Maplt it1, Maplt it2) { return it1->second > it2->second; });
  for (auto it = begin; it != sortedRangeEnd; ++it) {
    std::printf("-%10s%10zu\n", (it)->first.c_str(), (it)->second);
  }
}
```

`sortedRangeEnd` 是使用 `begin` 的表达式结果初始化的，因为 `sortedRangeEnd` 之后会被传递给 `partial_sort`，而如果混合了迭代器和常量迭代器，`partial_sort` 的实例化将失败。该调用中的 `begin` 和 `end` 迭代器必须是迭代器（而不是常量迭代器），因为 `partial_sort` 会移动元素并正确打印 `size_t` 类型的变量。

```cpp
int main(int argc, const char** argv) { // 在命令行上获取文件名列表，
    // 使用以下方式打印最常见的20个单词：
    // 同时处理文件
    std::vector<std::future<WordCountMapType>> futures;
    for (int argNum = 1; argNum < argc; ++argNum) {
        futures.push_back(std::async([=]{ return wordsInFile(argv[argNum]); })); // 这为了保持示例简单
    }

    WordCountMapType wordCounts;
    for (auto& f : futures) {
        const auto results = f.get(); // 获取 wordsInFile 返回的 map
        for (const auto& pair : results) {
            wordCounts[pair.first] += pair.second;
        }
    }

    std::cout << wordCounts.size() << " words found. Most common:\n";
    const std::size_t maxWordsToShow = 20;
    showCommonWords(wordCounts.begin(), wordCounts.end());
    std::min(wordCounts.size(), maxWordsToShow);
}
```

这段代码让主线程等待每个文件在独立线程上处理完成，而不是自己处理文件。这只是为了保持示例简单。

`">"` 现在在可能的情况下关闭嵌套模板：

C++98 的“额外空格”方法是有效的：

对于移位操作，使用括号：

- 例如，`">"` 现在在模板解析期间被视为与 `">"` 相同：

```cpp
const int n = ...; // n, m 是编译时常量
const int m = ...; 
std::array<int, n>m?n:m> > a1; // 错误（如 C++98 所示）
std::array<int, (n>m?n:m) > a2; // 有效（如 C++98 所示）
std::list<std::array<int, n>>2 >> L1; // 在 '98 中报错：2次移位；
// 在 '0x 中报错：第一个 '>>'
// 同时关闭了两个模板
std::list<std::array<int, (n>>2)> >> L2; // 在 C++0x 中有效，
// 在 '98 中报错（2次移位）
```

[`std::array` 尚未引入。]

# auto 用于类型声明

`auto` 变量的类型为其初始化表达式的类型：

```
auto x1 = 10; // x1: int
std::map<int, std::string> m;
auto i1 = m.begin(); // i1: std::map<int, std::string>::iterator
```

可以添加 `const`/`volatile` 和引用/指针修饰：

```
const auto *x2 = &x1; // x2: const int*
const auto &i2 = m; // i2: const std::map<int, std::string>&
```

要获取 `const_iterator`，请使用新的 `cbegin` 容器函数：

```
auto ci = m.cbegin(); // ci: std::map<int, std::string>::const_iterator
```

`auto` 的类型推导与模板参数的推导相似：

```
template<typename T> void f(T t);
...
f(expr);               // 从 expr 推导 t 的类型
auto v = expr;         // 对 v 的类型执行本质相同的操作
```

Scott Meyers, 软件开发顾问

幻灯片 23

关于 `auto` 的规则在 `N3290` 的 `[dcl.spec.auto]`（7.1.6.4）中。

关于 `auto` 的规则在 `[dcl....`

据我所知，`auto` 类型推导与模板类型推导不一致的唯一情况是从大括号初始化列表中推导类型时。`auto` 使用 `{x, y, z}` 的类型为 `std::initializer_list<T>`（其中 `T` 是 `x`、`y` 和 `z` 的类型），但模板参数推导不适用于大括号初始化列表。（这是一个“非推导上下文”）。

正如在右值引用的讨论中提到的，`auto` 使用与模板相同的类型推导规则这一事实意味着，类型为 `auto&&` 的变量在引用折叠（reference collapsing）后，可能会变成左值：



# C++11 特性详解

## 引用折叠与 `auto` 类型推导

```cpp
int x;
auto&&& a1 = x;         // x 是左值，所以 a1 是 int&
auto&&& a2 = std::move(x); // move(x) 是右值，所以 a2 是 int&&
```

Scott Meyers，软件开发顾问

来自 ebook.com

对于显式声明为引用的变量：

- 顶层 `volatile` 被忽略。
- 数组名退化为指针。

```cpp
const std::list<int> li;
auto v1 = li;               // v1: std::list<int>
auto &v2 = li;              // v2: std::list<int>&
float data[ArraySize];
auto v3 = data;            // v3: float*
```

之前的示例：

```cpp
auto x1 = 10;                    // x1: int
std::map<int, std::string> m;
auto i1 = m.begin();             // i1: std::map<int, std::string>::iterator
const auto *x2 = m.begin();      // x2: const std::map<int, std::string>::const_iterator
                                 // （const 是顶层的）
const auto &i2 = m.begin();      // i2: std::map<int, std::string>::const_iterator
auto ci = m.begin();             // ci: std::map<int, std::string>::iterator
```

```cpp
void f(std::string& s) {
  auto temp = s, *pOrig = &s; // temp: std::string, pOrig: std::string*
}
```

每次初始化必须产生相同的类型。

```cpp
auto i = 10, d = 5; // 错误！
```

直接初始化和拷贝初始化语法都是允许的。

```cpp
auto v1(expr); // 直接初始化
auto v2 = expr; // 拷贝初始化
```

对于 `auto`，两种语法的含义相同。

普通初始化可以调用显式构造函数，而拷贝初始化不能，这一事实并不重要，因为 `auto` 的推导取决于初始化表达式的类型。来自 Daniel Klaus：

```cpp
struct Explicit {
    Explicit() {}
    explicit Explicit(const Explicit&);
} ex;
auto ex2 = ex; // 错误
auto ex3(ex);  // OK
```

## 基于范围的 for 循环

遍历容器可以采用这种简化的形式：

```cpp
std::vector<int> v;
...
for (int i : v) std::cout << i; // 迭代设置 v 中的每一个元素
```

迭代变量也可以是引用：

```cpp
for (int& i : v) std::cout << ++i; // 增加 v 中的所有元素
```

允许 `auto`、`const` 和 `volatile`：

```cpp
for (auto i : v) std::cout << i; // 与上述相同
for (auto& i : v) std::cout << ++i; // 同上
for (volatile int i : v) someOtherFunc(i); // 或者 volatile auto i
```

适用于任何支持范围概念的类型。

包含：

> [初始化列表、正则表达式和元组尚未引入。]

![](img/68a90f505054116271758fb914871a74_29_0.png)

支持对正则表达式匹配进行迭代，因为 `std::match_results` 提供了 `begin` 和 `end` 成员函数用于迭代匹配中的子项。

“UDT” = “用户定义类型”。

示例：

```cpp
std::unordered_multiset<std::shared_ptr<Widget>> msspw;
...
for (const auto& p : msspw) {
    std::cout << p << '\n';
    // 打印指针值
}
```

```cpp
short vals[ArraySize];
...
for (auto& v : vals) { v = -v; }
```

> [unordered_multiset 和 shared_ptr 尚未引入。]

循环变量 `p` 为引用，是因为拷贝 `msspw` 中的 `shared_ptr` 会导致额外的引用计数操作，这在多线程代码中可能会产生性能影响（即使在 `shared_ptr` 使用线程安全的引用计数增减的单线程代码中也是如此）。

```cpp
for ( iterVarDeclaration : expression ) statementToExecute
```

本质等同于

```cpp
{
  auto&& range = expression;
  for (auto b = begin(range), e = end(range);
       b != e;
       ++b) {
    iterVarDeclaration = *b;
    statementToExecute
  }
}
```

标准描述较为复杂。

此幻灯片仅供参考，不期望其自明其义。未提及的细节包括：(1) 数组由特殊处理而非调用 `begin`/`end`；(2) 当使用 ADL 查找 `begin`/`end` 时，标准命名空间中的版本始终可用；(3) 表达式可以是大括号初始化列表。

范围形式仅适用于 `for` 循环。

- 不适用于 `do` 循环，不适用于 `while` 循环。

## `nullptr`

一个新关键字。表示空指针。

- 可以转换为任何指针类型和 `bool`，但不再限于此。
- 不能作为整数值使用。

```cpp
const char *p = nullptr; // p 为空
if (p) ... // 代码编译通过，测试失败
int i = nullptr; // 错误！
```

`0` 和 `NULL` 的传统用法仍然有效：

```cpp
int *p1 = nullptr; // p1 为空
int *p2 = 0; // p2 为空
int *p3 = NULL; // p3 为空
if (p1 == p2 && p1 == p3) // 代码编译通过，测试成功
```

“关键字”一词比“保留字”更强。关键字无条件保留（除了作为属性名称外），而例如，“main”仅在用作全局作用域内的函数名时被保留。

`nullptr` 的类型为 `std::nullptr_t`。其他指针类型可以通过 `static_cast`（或 C 风格转换）转换为此类型。结果始终是一个空指针。

只有 `nullptr` 是无歧的指针：

```cpp
void f(int* ptr); // 对指针和 int 进行重载
void f(int val);
f(nullptr); // 调用 f(int*)
f(0);       // 调用 f(int)
f(NULL);    // 可能调用 f(int)
```

- 除非 `NULL` 未定义为 `0`，否则最后一个调用是可以编译的。
- 例如，它可能被定义为 `0L`。

### `nullptr` 与转发模板

与 `0` 和 `NULL` 不同，`nullptr` 与转发模板配合得很好：

```cpp
template<typename F, typename P> // 创建日志项，然后
void logAndCall(F func, P param) // 在 param 上调用 func
{
    ... // 写入日志项
    func(param);
}
void f(int* p); // 某个调用的函数

f(0);           // OK
f(nullptr);     // 同样
logAndCall(f, 0);      // 错误！P 被推导为 int，且 f(int) 无效
logAndCall(f, NULL);   // 错误
logAndCall(f, nullptr); // OK，P 被推导为 std::nullptr_t，且 f(std::nullptr_t) 是允许的
```

因此 `nullptr` 完美了 C++11 对完美转发的支持，这在课程后面的部分会提到。

## Unicode 支持

这些类型带有 `u`/`U` 前缀的字面量是 UCS 编码的：

当然，C++98 的字符类型仍然存在：

根据 C++11 ([basic.fundamental], N3290 中的 3.9/5)：“类型 `char16_t` 和 `char32_t` 表示与 `<cstdint>` 中的 `uint_least16_t` 和 `uint_least32_t` 具有相同大小、符号性和对齐方式的类型，称为底层类型。”

UCS-2 是一种 16 位编码，与 UTF-16 的基本多语言平面 (BMP) 中的项匹配。UTF-16 可以使用代理对来表示 BMP 之外的代码点；UCS-2 则不能。UCS-4 和 UTF-32 本质上是完全相同的。

`char16_t` 字符字面量只能使用 UCS-2，因为无法在单个 `char16_t` 对象中放入一个 UTF-16 代理对（即两个 16 位值）。注意 [lex.ccon](N3290 中的 2.14.3/2)：“以字母 `u` 开头的字符字面量，如 `u'Y'` 是类型为 `char16_t` 的字符字面量……如果值无法在 16 位内表示，程序是格式错误的。”

代码点可以通过 `\unnnn` 和 `\Unnnnnnnn` 指定：

- `u8"clef: \U0001D11E"`

有相应的字符串字面量：

- `u8"UTF-8 string literal"`  // ⇒ `char` 数组 (UTF-8 编码)
- `u"UTF-16 string literal"`  // ⇒ `char16_t` 数组
- `U"UTF-32 string literal"`  // ⇒ `char32_t` 数组
- `L"Wide string literal"`    // ⇒ `wchar_t` 数组

## 大括号初始化

容器需要另一个容器：

```cpp
int vals[] = { 10, 20, 30 };
const std::vector<int> cv(vals, vals+3); // 从另一个容器初始化
```

成员数组和堆上的数组在 C++98 中无法初始化：

```cpp
class Widget {
public:
    Widget(): data(???) {} // C++98 无法初始化成员数组
private:
    const int data[5]; // 不初始化
};
const float * pData = new const float[4]; // C++98 无法初始化堆数组
```

大括号初始化语法现在在处处可用：

```cpp
const int val1 {5};
const int val2 {5};
int a[] {1, 2, val1, val1+val2 };
struct Point1 { int x, y; }; // 与以前一样
const Point1 p1 {10, 20};
class Point2 { int x, y; }; // 与以前一样
const Point2 p2 {10, 20};
class Widget {
public:
  Widget(): data {1, 2, a[3], 4, 5} {}
private:
  const int data[5];
};
const float * pData = new const float[4] {1.5, val1-val2, 3.5, 4.5 }; // OK
Point2 makePoint() { return { 0, 0 }; } // OK
```

```cpp
void f(const std::vector<int>& v); // 与以前一样
f({ val1, val2, 10, 30 }); // OK：通过 std::initializer_list 隐式转换
```

`T var = expr` 不能调用显式构造函数：

```cpp
class Widget {
public:
    explicit Widget(int);
    ...
};
Widget w1(10); // OK，直接初始化
Widget w2{10}; // OK，直接列表初始化
Widget w3 = 10; // 错误！拷贝初始化不能调用 explicit 构造函数
```



大括号初始化语法现在允许处处可用：

```cpp
const int val1 {5};
const int val2 {5};
int a[] {1, 2, val1, val1+val2 };
struct Point1 { ... }; // 与以前一样
const Point1 p1 {10, 20};
class Point2 { ... }; // 与以前一样
const Point2 p2 {10, 20};
class Widget {
public:
  Widget(): data {1, 2, a[3], 4, 5}
private:
  const int data[5];
};
const float * pData = new const float[4] = {1.5, val1-val2, 3.5, 4.5 }; // 错误！
Point2 makePoint() { return { 0, 0 }; // 错误！
```

```cpp
void f(const std::vector<int>& v); // 与以前一样
f({ val1, val2, 10, 30 }); // 错误！
```

# 统一初始化语法

"T var = expr" 不能调用显式构造函数：

```cpp
class Widget {
public:
    explicit Widget(int);
    ...
};
Widget w1(10); // 确认为，直接初始化
Widget w2{10}; // 确认为
Widget w3 = 10; // 错误！调用显式构造函数
```

# 初始化列表

`std::initializer_list` 参数可以与其他参数一起使用：

```cpp
class Widget {
public:
    Widget(const std::string& name, double epsilon,
    std::initializer_list<int> il);
    ...
};
```

```cpp
std::string name("Buffy");

Widget w { name, 0.5, // 等同于
    {5, 10, 15 }; // Widget w(name, 0.5,
    // std::initializer_list({5,10,15}));
```

- 注意嵌套的大括号集合。

## 初始化列表

它们可以被模板化：

```cpp
class Widget {
public:
    template<typename T> Widget(std::initializer_list<T> il);
};
```

```cpp
Widget w1 { -55, 25, 16 }; // 合法，T = int
```

只有同质初始化列表允许类型推导成功。

```cpp
Widget w2 { -55, 2.5, 16 }; // 错误，T 无法推导
```

## 初始化列表与重载解析

在解析构造函数调用时，对于大括号分隔的参数，`std::initializer_list` 参数会被优先考虑：

```cpp
class Widget {
public:
    Widget(double value, double uncertainty); // #1
    Widget(std::initializer_list<double> values); // #2
    ...
    double d1, d2;
    ...
    Widget w1 {d1, d2}; // 调用 #2
```

对于普通大括号分隔的参数：

```cpp
Widget w2(d1, d2); // 调用 #1
```

## 初始化列表与重载解析

`std::initializer_list` 参数*始终* 优于其他类型：

```cpp
class Widget {
public:
    Widget(double value, double uncertainty); // #1
    Widget(std::initializer_list<std::string> values); // #2

    double d1, d2;

    Widget w1 {d1, d2}; // 尝试调用 #2；失败原因是
    没有 double ⇒ string 转换
```

只要可能，大括号初始化器就会被视为 `std::initializer_lists`。

仅对大括号初始化器有效：

```cpp
Widget w2(d1, d2); // 仍然调用 #1
```

C++0x 草案中关于此主题的相关部分为 [over.match.list] (N3290 中的 13.3.1.7), [dcl.init.list] (N3290 中的 8.5.4/2-3) 以及 [temp.deduct.call] (N3290 中的 14.8.2/1)。

## 初始化列表与重载解析

给定多个 `std::initializer_list` 候选者，最佳匹配由最元素转换决定：

```cpp
class Widget {
public:
    Widget(std::initializer_list<int>); // #1
    Widget(std::initializer_list<double>); // #2
    Widget(std::initializer_list<std::string>); // #3

    Widget(int, int, int); // 由于上述构造函数，此构造函数不
    // 被考虑 "{...}" 参数

    Widget w1 { 1, 2, 0, 3 }; // int -> double 级别同于
    // double -> int，因此存在歧义

    Widget w2 { 1.0f, 2.0, 3.0 }; // float -> double 优于
    // float -> int，因此调用 #2

    std::string s;
    Widget w3 { s, "Init", "Lists" }; // 调用 #3
```

## 初始化列表与重载解析

如果最佳匹配涉及收缩转换，则调用是无效的：

```cpp
class Widget {
public:
    Widget(std::initializer_list<int>);
    Widget(int, int, int); // 由于上述构造函数，不
    // 被考虑 "{...}" 参数
};
Widget w = { 1, 2.0, 3 }; // 错误！double -> int 收缩
```

## 一致初始化总结

- 大括号初始化语法现在随处可用。

- ➡ 聚合体（Aggregates）从上到下/从左到右进行初始化。

- ➡ 非聚合体通过构造函数进行初始化。

- 不允许隐式收缩。

- `std::initializer_list` 参数允许将“初始化”列表传递给函数。

- ➡ 实际上并不限于初始化（例如 `std::vector::insert`）。

# Lambda 表达式

一种在用点处创建函数对象的快速方法。

```cpp
std::vector<int> v;
...
auto it = std::find_if(v.cbegin(), v.cend(),
[](int i) { return i > 0 && i < 10; });
```

本质上生成了：

```cpp
class MagicType1 {
public:
    bool operator()(int i) const { return i > 0 && i < 10; }
}
auto it = std::find_if(v.cbegin(), v.cend(), MagicType1());
```

上述生成的 `MagicType` 在技术上并不完全准确，因为闭包类型不是默认可构造的，但该细节对于理解 lambda 作用的本质并不重要。

我在本课程中忽略了 `mutable` lambda 表达式，因为它们的用例并不常见，且本课程是概述，而非详尽处理。我同样忽略了按值捕获如何保留捕获变量的 cv 限定符。

## 捕获变量

捕获局部变量会产生副本：

```cpp
{
  int minVal = 0, maxVal = 10;
  // 捕获捕Val 的副本
  auto f = [minVal, maxVal](int i) { return i > minVal && i < maxVal; };
}
```

按引用捕获可以使用原始变量：

```cpp
{
  int minVal = 0, maxVal = 10;
  // 引用获引用Val max引用
  auto f = [&minVal, &maxVal](int i) { return i > minVal && i < maxVal; };
}
```

### 捕获局部变量

不同的局部变量捕获方式不同：

```cpp
{
  int minVal;
  double maxVal;
  ...
  auto it = std::find_if(v.cbegin(), v.cend(),
    [minVal, &maxVal](int i)
    { return i > minVal && i < maxVal; });
}
```

对应于：

```cpp
class MagicType{
public:
  MagicType(int v1, double& v2): _minVal(v1), _maxVal(v2) {}
  bool operator()(int i) const { return i > _minVal && i < _maxVal; }
private:
  int _minVal;
  double& _maxVal;
}
```

```cpp
auto it = std::find_if(v.cbegin(), v.cend(), // 与之前相同
  MagicType(minVal, maxVal)); 
```

### 捕获局部变量

可以指定默认捕获模式：

```cpp
auto it = std::find_if(v.cbegin(), v.rend(), // 默认是
    [](int i) // 值传递
    { return i > minVal && i < maxVal; });
auto it = std::find_if(v.cbegin(), v.rend(), // 默认是
    [&](int i) // 引用传递
    { return i > minVal && i < maxVal; });
```

使用默认捕获模式时，不需要列出捕获的变量。

- 如上所示。

### 捕获局部变量

默认值可以按变量进行覆盖：

```cpp
auto it = std::find_if(v.cbegin(), v.cend(), // 默认捕获是
                                 [=, &maxVal](int i // 值传递，但 maxVal
                               { return i > minVal && // 是引用传递
                                 i < maxVal; });
```

对应于：

```cpp
class MagicType {
public:
    MagicType(int v1, double& v2): _minVal(v1), _maxVal(v2)
    bool operator()(int i) const { return i > _minVal && i < _maxVal; }
private:
    int _minVal;
    double& _maxVal;
};
auto it = std::find_if(v.cbegin(), v.cend(), MagicType(minVal, maxVal));
```

### 捕获类成员

要在成员函数内部访问类成员，请捕获 `this`：

```cpp
class Widget {
public:
    void doSomething();
private:
    std::list<int> li;
    int minVal;
};

void Widget::doSomething() {
    auto it = std::find_if(li.begin(), li.end(),
        [minVal](int i) { return i > minVal; } // 错误！
    ...
}

void Widget::doSomething() {
    auto it = std::find_if(li.begin(), li.end(),
        [this](int i) { return i > minVal; } // OK
    );
}
```

在成员函数使用的 Lambda 产生的闭包类型定义在成员函数内部，因此闭包包含了该成员函数。这使得闭包的 `operator()` 可以引用类的所有成员，例如 Lambda 中本页的 `minVal`。不需要友元权限，因为闭包类型位于类内部（即是类的一部分）。

### 捕获类成员

默认捕获模式也使得这成为可用：

```cpp
class Widget {
public:
  void doSomething();
private:
  std::list<int> li;
  int minVal;
};

void Widget::doSomething() {
  auto it = std::find_if(li.begin(), li.end(),
    [=](int i) { return i > minVal; } // OK
  );
}

void Widget::doSomething() {
  auto it = std::find_if(li.begin(), li.end(),
    [&](int i) { return i > minVal; } // 同样 OK，效果
    // 相同（对于 "this"）
  );
}
```

按引用捕获可能比按值捕获效率低，因为通过引用需要双重间接（编译器优化除外）。

### Lambda 返回类型

在以下情况下可选的：

- 返回类型为 `void`。

- Lambda 实体为“return expr”。

- 返回类型是 `expr` 的类型。

否则必须通过后续返回类型语法指定：

```cpp
std::vector<double> v;
std::transform(v.begin(), v.end(), v.begin(),
[](double d)->double
{
  makeLogEntry("std::transform", d);
  return std::sqrt(std::abs(d));
});
```

### 后续返回类型

- 必须与 Lambda 使用（当给出返回类型时）。

- 通常配合 `decltype`（后文描述）非常有用。

- 在声明时通常很有用：

```cpp
void f1(int);                          // 后续返回类型
auto f2(int);                         // 

class Widget {
public:
    void f3(int);                      // 传统写法
    auto f4();               // 自动类型
};
```

由于闭包类型在类内部（即是类的一部分），因此不需要友元。

### Lambda 无参数列表

- 必须与 Lambda 使用（当给出返回类型时）。

- 通常配合 `decltype` 很有用。

- 允许用于任何函数。

```cpp
void f1(int);                          // 后续返回类型
auto f2(int);                         //

class Widget {
public:
    void f3(int);                      // 传统写法
    auto f4();               // 自动类型
};
```

### Lambda 无参数列表

- 必须与 Lambda 使用（当给出返回类型时）。

- 通常配合 `decltype` 很有用。

- 允许用于任何函数。

```cpp
void f1(int);                          // 后续返回类型
auto f2(int);                         //

class Widget {
public:
    void f3(int);                      // 传统写法
    auto f4();               // 自动类型
};
```

### Lambda 无参数列表

- 必须与 Lambda 使用（当给出返回类型时）。

- 通常配合 `decltype` 很有用。

- 允许用于任何函数。

```cpp
void f1(int);                          // 后续返回类型
auto f2(int);                         //

class Widget {
public:
    void f3(int);                      // 传统写法
    auto f4();               // 自动类型
};
```

### Lambda 无参数列表

- 必须与 Lambda 使用（当给出返回类型时）。

- 通常配合 `decltype` 很有用。

- 允许用于任何函数。



```cpp
void f1(int);                          // 后续返回类型
auto f2(int);                         //

class Widget {
public:
    void f3(int);                      // 传统写法
    auto f4();               // 自动类型
};
```

### Lambda 无参数列表

- 必须与 Lambda 使用（当给出返回类型时）。
- 通常配合 `decltype` 很有用。
- 允许用于任何函数。

### 捕获局部变量

不同的局部变量捕获方式不同：

```cpp
{
  int minVal;
  double maxVal;
  ...
  auto it = std::find_if(v.cbegin(), v.cend(),
    [minVal, &maxVal](int i)
    { return i > minVal && i < maxVal; });
}
```

对应于：

```cpp
class MagicType{
public:
  MagicType(int v1, double& v2): _minVal(v1), _maxVal(v2) {}
  bool operator()(int i) const { return i > _minVal && i < _maxVal; }
private:
  int _minVal;
  double& _maxVal;
}
```

```cpp
auto it = std::find_if(v.cbegin(), v.cend(), // 与之前相同
  MagicType(minVal, maxVal)); // 之前
```

#### 默认捕获模式

可以指定默认捕获模式：

```cpp
auto it = std::find_if(v.cbegin(), v.rend(), // 默认是
    [](int i) // 值传递
    { return i > minVal && i < maxVal; });
auto it = std::find_if(v.cbegin(), v.rend(), // 默认是
    [&](int i) // 引用传递
    { return i > minVal && i < maxVal; });
```

使用默认捕获模式时，不需要列出捕获的变量。

#### 覆盖默认捕获

默认值可以按变量进行覆盖：

```cpp
auto it = std::find_if(v.cbegin(), v.cend(), // 默认捕获是
                                 [=, &maxVal](int i // 值传递，但 maxVal
                               { return i > minVal && // 是引用传递
                                 i < maxVal; });
```

对应于：

```cpp
class MagicType {
public:
    MagicType(int v1, double& v2): _minVal(v1), _maxVal(v2)
    bool operator()(int i) const { return i > _minVal && i < _maxVal; }
private:
    int _minVal;
    double& _maxVal;
};
auto it = std::find_if(v.cbegin(), v.cend(), MagicType(minVal, maxVal));
```

### 捕获类成员

要在成员函数内部访问类成员，请捕获 `this`：

```cpp
class Widget {
public:
    void doSomething();
private:
    std::list<int> li;
    int minVal;
};

void Widget::doSomething() {
    auto it = std::find_if(li.begin(), li.end(),
        [minVal](int i) { return i > minVal; } // 错误！
    ...
}

void Widget::doSomething() {
    auto it = std::find_if(li.begin(), li.end(),
        [this](int i) { return i > minVal; } // OK
    );
}
```

在成员函数使用的 Lambda 产生的闭包类型定义在成员函数内部，因此闭包包含了该成员函数。这使得闭包的 `operator()` 可以引用类的所有成员，例如 Lambda 中本页的 `minVal`。不需要友元权限，因为闭包类型位于类内部（即是类的一部分）。

#### 默认捕获模式与类成员

默认捕获模式也使得这成为可用：

```cpp
class Widget {
public:
  void doSomething();
private:
  std::list<int> li;
  int minVal;
};

void Widget::doSomething() {
  auto it = std::find_if(li.begin(), li.end(),
    [=](int i) { return i > minVal; } // OK
  );
}

void Widget::doSomething() {
  auto it = std::find_if(li.begin(), li.end(),
    [&](int i) { return i > minVal; } // 同样 OK，效果
    // 相同（对于 "this"）
  );
}
```

按引用捕获可能比按值捕获效率低，因为通过引用需要双重间接（编译器优化除外）。

### Lambda 返回类型

在以下情况下可选的：

- 返回类型为 `void`。
- Lambda 实体为“return expr”。
- 返回类型是 `expr` 的类型。

否则必须通过后续返回类型语法指定：

```cpp
std::vector<double> v;
std::transform(v.begin(), v.end(), v.begin(),
[](double d)->double
{
  makeLogEntry("std::transform", d);
  return std::sqrt(std::abs(d));
});
```

### 后续返回类型

- 必须与 Lambda 使用（当给出返回类型时）。
- 通常配合 `decltype` 非常有用。
- 在声明时通常很有用：

```cpp
void f1(int);                          // 后续返回类型
auto f2(int);                         // 

class Widget {
public:
    void f3(int);                      // 传统写法
    auto f4();               // 自动类型
};
```

## 将 Lambda 作为容器比较函数

将闭包传递给容器构造函数：

```cpp
auto cmpFnc = [](int *pa, int *pb)    // 比较值
                              { return *pa < *pb };         // 而不是指针
std::set<int*, decltype(cmpFnc)> s(cmpFnc); // 按此方式对 s 排序
```

`decltype` 尚未引入。

闭包类型不是默认构造的，因此这会导致失败：

```cpp
std::set<int*, decltype(cmpFnc)> s;     // 错误！比较对象无法
                                            // 
```

## Lambda/闭包总结

- Lambda 表达式生成闭包。
- 调用状态可以按值或按引用进行捕获。
- 返回类型在指定时，使用尾随返回类型语法。
- 闭包可以使用 `auto` 或 `std::function` 存储。
- 注意存储在闭包中的悬空引用/指针。
- 短、清晰且源于上下文的 Lambda 是最好的。

# 模板别名 (Template Aliases)

`using` 声明现在可以用于“部分绑定”模板：

```cpp
template<typename T>
using MyAllocVec = std::vector<T, MyAllocator>;
MyAllocVec<int> v; // std::vector<int, MyAllocator>

template<std::size_t N>
using StringArray = std::array<std::string, N>;
StringArray<15> sa; // std::array<std::string, 15>

template<typename K, typename V>
using MapGT = std::map<K, V, std::greater<K>>;
MapGT<long long, std::shared_ptr<std::string>> myMap; // std::map<long long, std::shared_ptr<std::string>, std::greater<long long>>
```

## 模板别名特化限制

模板别名不能被特化：

```cpp
template<typename T> // 之前的
using MyAllocVec = std::vector<T, Allocator>; // 页面
template<typename T>
using MyAllocVec = std::vector<T*, MyPtrAllocator>; // 错误！
```

要实现这种效果，请使用特征类（traits class）：

```cpp
template<typename T> // 主
struct VecAllocator {
  typedef MyAllocator type;
};
```

```cpp
template<typename T> // 特化
struct VecAllocator<T*> // 模板
  typedef MyPtrAllocator type;
};
```

```cpp
template<typename T>
using MyAllocVec = std::vector<T, typename VecAllocator<T>::type>;
```

## using 作为 typedef

在没有模板化的情况下，`using` 可以等同于 `typedef`：

```cpp
typedef std::unordered_set<int> IntHash; // 这两行有效
using IntHash = std::unordered_set<int>; // 相同
```

`using` 声明更具可读性：

```cpp
typedef void (*CallbackPtr)(int); // 函数指针 typedef
using CallbackPtr = void (*)(int); // 等同的 using 声明.
```

本课程关于 C++0x 标准，而不是并发，因此我假设与会者熟悉线程的基本问题，包括何时应该使用和不应该使用线程、竞态条件、同步、死锁、测试等。此页上的功能列表并不详尽，在并发讨论的末尾有一个“其他功能”的列表。

# 线程 (Threads)

`std::thread` 接受任何“可调用对象”并异步运行它：

```cpp
void doThis();
class Widget {
  public:
    void operator()() const;
    void normalize(long double, int, std::vector<float>);
};

std::thread t1(doThis); // 异步运行函数
Widget w;
std::thread t2(w); // 异步“运行”函数对象
```

要传递参数，可以使用 lambda：

```cpp
long double id;
int x;
std::thread t3([&]{w.normalize(id, x, {1, 2, 3});}); // 异步运行
```

多线程的行为与经典单线程行为相似，尽管未同步的访问可能会导致竞态。如果主函数退出而其他线程仍在运行，这意味着“意外终止”，将导致未定义行为。线程不能挂起状态启动，但 `std::thread::native_handle` 应该是可用的。通过 `pthread_cancel` 线程被强制杀死。

# 数据生命周期 (Data Lifetime)

在 ST 中调用的函数知道数据是“冻结”的：

- 它们在调用期间不会被销毁。
- 只有调用的函数可以改变它们的值。



```cpp
int x, y, z;
Widget *pw;
...
f(x, y); // ST 中的调用
```

在 `f` 的执行期间：

- `x`, `y`, `z` 和 `pw` 将继续存在。
- 除非 `f` 导致 `pw` 被删除。

取决于 `f` 如何声明其参数：

```cpp
void f(int xParam, int yParam);      // 按值传递：
void f(int& xParam, int& yParam);             // 按引用传递：
void f(const int& xParam, const int& yParam); 
```

异步调用中的数据是冻结的：

- 闭包包含 `x` 和 `w` 的拷贝。
- 闭包被线程构造函数拷贝；直到 `f` 返回才存在。
- `x`, `y`, `z` 和 `pw` 可能会改变。

结论：数据生命周期问题在多线程 (MT) 设计中至关重要。即使是共享数据也受生命周期问题影响。异步调用中的按引用/按指针参数是有风险的。同步/竞态问题。优先按值传递。通过 Lambda！

```cpp
void f(int xParam); // 异步调用函数

{
  int x;
  std::thread t1([&]{f(x)}); // 有风险！闭包持有 x 的引用
  std::thread t2([=]{f(x)}); // 可以，闭包持有 x 的拷贝
} // x 被销毁
```

在 `t1` 的情况下，lambda 的闭包对象在调用线程继续之前创建，但调用线程可能在 `f` 开始执行之前继续。等到 `xParam` 初始化，闭包可能持有悬空引用，因为 `x` 已经被销毁。

## 避免生命周期问题

基本策略：

- 为异步调用拷贝数据。
- 确保引用的对象足够持久。

## 为异步调用拷贝参数

`std::thread` 的变长构造函数（概念上）拷贝所有内容：

```cpp
void f(int xVal, const Widget& wVal);
int x;
Widget w;
std::thread t(f, x, w);      // 在 x, w 的拷贝上调用 f
```

- `f`, `x`, `w` 的拷贝保证持续到异步调用返回。
- 在 `f` 内部，`wVal` 指向 `w` 的拷贝，而不是本身。
- 我们移动语义时的细节。

尽可能将拷贝优化为移动。

在这个示例中，“拷贝”意味着拷贝指向它的指针，将此拷贝优化为移动没有意义，因为拷贝指针是廉价的。通用规则是线程构造函数拷贝/移动它的第一个参数，即要异步执行的函数。

### 拷贝参数

在闭包中使用按值捕获也有效：

```cpp
void f(int xVal, const Widget& wVal);
int x;
Widget w;
...
std::thread t([=]{ f(x, w); }); // 在 x, w 的拷贝上调用 f
```

- 闭包包含 `x` 和 `w` 的拷贝。
- 闭包被线程构造函数拷贝；直到 `f` 返回才存在。
- 尽可能将拷贝优化为移动。
- 在 `f` 内部，`wVal` 指向 `w` 的拷贝，而不是本身。

### 拷贝参数

另一种方法基于 `std::bind`：

```cpp
void f(int xVal, const Widget& wVal);
int x;
Widget w;
...
std::thread t(std::bind(f, x, w)); // 在 x, w 的拷贝上调用 f
```

- `bind` 返回的对象包含 `x` 和 `w` 的拷贝。
- 该对象被线程构造函数拷贝；直到 `f` 返回才存在。
- 在 `f` 内部，`wVal` 指向 `w` 的拷贝，而不是本身。

我们稍后会检查 `std::bind`。

- Lambda 通常比 `bind` 是更好的选择。
- 读者更易理解。
- 更高效。

## 新 C++ (C++0x) 概述

### 拷贝参数

摘要：

- 创建具有足够生命期的参数拷贝的选项：
- 使用变长线程构造函数。
- 使用按值捕获的 lambda。
- 使用 `bind`。

Scott Meyers，软件开发顾问

http://www.aristeia.com/

© 2011 Scott Meyers, 保留所有权利

幻灯片 101

Scott Meyers，软件开发顾问

http://www.aristeia.com/

© 2011 Scott Meyers, 保留所有权利

从 Wow! eBook 下载 <www.wowebook.com>

## 确保参数有足够的生命周期

一种方法是推迟局部变量的析构直到异步调用完成：

```cpp
void f(int xVal, const Widget& wVal);    // 与之前

{
    int x;
    Widget w;
    ...
    std::thread t([&]{ f(x, w); });      // wVal 实际上引用 w
    ...
    t.join();                          // 只有在 t
                                     // 结束后才析构 w
}
```

## 混合按值和按引用参数

给定

```cpp
void f(int xVal, int yVal, int zVal, Widget& wVal);
```

如果你真的想通过引用传递 `w` 怎么办？

- Lambdas：使用按引用捕获：

```cpp
{
  Widget w;
  int x, y, z;
  ...
  std::thread t([=, &w]{f(x, y, z, w);}); // 传递 x, y, z 的拷贝
  ... // 按引用传递 w
}
```

- 你负责避免在 `w` 上发生数据竞态。

## 混合按值和按引用参数

- 变长线程构造函数或 `bind`：使用 C++0x 的 `std::ref`：

- 创建行为引用的对象。
- `std::ref` 生成的对象的拷贝引用同一个对象。

```cpp
void f(int xVal, int yVal, int zVal, Widget& wVal); // 与之前
{
    static Widget w;
    int x, y, z;

    std::thread t1(f, x, y, z, std::ref(w)); // 传递
    std::thread t2(std::bind(f, x, y, z, std::ref(w))); // x, y, z; 传递 w
    ... // 按引用
}
```

- `std::cref` 也存在（用于常量的引用），但隐式的 `ref(T) -> const T&` 意味着 `std::ref` 往往足够。

# 异步调用

构建块：

- `std::async`：请求异步执行一个函数。
- Future：代表函数结果的令牌。

与原始的 `std::thread` 对象不同：

- 允许返回值或异常。
- 就像“普通”函数调用一样。

本课程既不也不讨论 `std::packaged_task` 或 `std::promise`。

## async

```cpp
double bestValue(int x, int y); // 某些可用的
std::future<double> f = // 异步运行 λ;
std::async([](){ return bestValue(10, 20); }); // 获取其对应的 future
... // 执行其他工作
double val = f.get(); // 获取 λ 的结果（或
// 异常）
```

一如既往，`auto` 减少了冗余：

```cpp
auto f = std::async([]{ return bestValue(10, 20); });
...
auto val = f.get();
```

`bestValue` 背后的想法是它根据参数 `x` 和 `y` 计算某项的最优值。推测这种计算需要一些时间，因此使其成为自然的独立任务。

`std::async` 不仅可以传递 lambda，还可以传递一个函数及其参数（类似于 `std::thread`），但我没有展示任何此类示例。

## async 启动策略

- `std::launch::async`：在新线程上运行函数。
- 保持调用线程的响应性（例如 GUI 线程）。

```cpp
auto f = std::async(std::launch::async, doWork);
```

- `std::launch::deferred`：在调用线程上运行函数。
- 用于调试、性能调优。
- 调用在调用 `get` 或 `wait` 时发生。

```cpp
auto f = std::async(std::launch::deferred,
  [](){ returnValue(10, 20); });
auto val = f.get(); // 在此处异步运行
```

默认情况下，实现选择，目标是：

- 利用所有硬件并发性。
- 避免过度订阅。

`std::async` 使用的线程可能（但不需要）从线程池提取，并在重用线程之前销毁并初始化线程局部变量。直到 2010 年，`std::launch::deferred` 被命名为 `launch::sync`。

当启动多个异步策略（例如通过指定 `std::launch::async | std::launch::deferred`）时，同步和异步执行的决策需要在 `std::async` 返回之前做出。

## Futures

两种类型：

- `std::future<T>`：结果只能访问一次。
- 适用于大多数场景。
- 可移动，不可拷贝。
- 只有一个 future 有权访问结果。
- `std::shared_future<T>`：结果可以被多次访问。
- 当访问单个结果时适用。
- 可拷贝且可移动。
- 同一个结果可能存在多个 `shared_futures`。
- 可从 `future` 创建。
- 这种创建转移了所有权。

`std::async` 和 `promise` 都返回 `future` 对象，因此创建非空 `future` 的唯一方法是来自 `shared_future`。直到 2009 年，`std::future` 被命名为 `unique_future`。

关于 futures 的实现，Anthony Williams 写道：“`std::future<T>` 的实现必须提供存储 `T` 或 `exception_ptr` 的空间，以及计数共享引用的方法。可能需要额外的存储来管理状态以及某些标志。在来自 `std::async` 的情况下，状态必须包含可调用对象及其参数（对于 `std::launch::deferred` 策略），或新线程的句柄（对于 `std::launch::async` 策略）。”

## Futures

通过 `get` 获取结果：

- 阻塞直到可用，然后获取。
- 对于 `future<T>`，“获取” = “移动（如果可能）或 拷贝”。
- 对于 `shared_future<T>`，“获取” = “获取引用”。
- “返回”可能是异常（随后被传播）。

在 `std::future` 上多次调用 `get` 会导致未定义行为。在 `shared_future` 上多次调用 `get` 会产生相同的结果（返回值或异常）。不需要拷贝此类结果或异常，因为 (1) 非异常是通过引用访问的，(2) 只有在按值捕获时才会创建异常的拷贝。

## Futures

另一种选择是 `wait`：

- 阻塞直到结果可用。

```cpp
std::future<double> f = std::async([]{ return bestValue(10, 20); });
f.wait(); // 阻塞直到 lambda 完成
```

- 可以指定超时。
- 在指定 `std::launch::async` 时最有用。

```cpp
std::future<double> f = std::async([](){ return bestValue(10, 20); });
while (f.wait_for(std::chrono::seconds(0)) != std::future_status::ready) { // 未就绪，
    // 执行更多工作
}
double val = f.get(); // 获取结果
```

对于 unique futures，当任务异步运行时，`wait_for` 最有用，因为如果它是延迟任务（即计划同步运行），调用 `wait_for` 将永远不会超时（它将同步调用延迟任务，你必须等待它完成）。

枚举 `future::ready` 必须用 `future::status` 限定，因为 `std::future_status` 是一个枚举类，而不仅仅是一个枚举。类似的有类似于 Unix select 的支持，但 select 仅适用于异步 IO（它等待文件），并且不是 C++ 并发支持的一部分。

## void Futures

当调用者只想知道被调用者何时结束时有用。

- 返回 `void` 的调用对象。
- 调用者对返回值感兴趣。
- 但可能对异常感兴趣。

```cpp
void initDataStructs(int defValue);
void initGUI();
```

```cpp
std::future<void> f1 = std::async([]{ initDataStructs(-1); });
std::future<void> f2 = std::async([]{ initGUI(); } });

// 初始化一切
// 等待异步初始化
// 完成（并获取异常）
// 如果有
// 继续程序
```

```cpp
f1.get();
f2.get();
```

在等待 `join` 线程或 `future` 之间进行选择取决于几点。首先，如果你只有线程或只有 `future`，你没有选择。如果一个返回 `future` 的线程抛出异常，调用者可以通过 `future` 获取该异常，但如果你只是简单的 `join`，异常就会被静静地丢弃。调用者可以轮询 `future` 是否可用（通过超时时间为 0 的 `wait_for`），但没有方法可以轮询线程是否就绪。

# 互斥锁 (Mutexes)

四种：

- `std::mutex`: 非递归，不支持超时
- `std::timed_mutex`: 非递归，支持超时
- `std::recursive_mutex`: 递归，不支持超时
- `std::recursive_timed_mutex`: 递归，支持超时

递归地锁定非递归互斥锁 ⇒ 未定义行为。

互斥锁对象既不可拷贝也不可移动。拷贝互斥锁并没有意义（你最终会为同一数据拥有多个互斥锁）。—— Anthony Williams

## 用于互斥锁的 RAII 类

互斥锁通常由 RAII 类管理：

- `std::lock_guard`：构造函数锁定互斥锁，析构函数中解锁。

```cpp
std::mutex m; // 互斥锁对象
std::lock_guard<std::mutex> L(m); // 锁定 m
... // 临区域
} // 解锁 m
```

- 无操作。
- 不可拷贝/移动，无赋值，无手动解锁。

RAII = “资源获取即初始化”。

通常，“lock（锁）”这一术语指的是用于管理互斥锁锁定/解锁的 RAII 或类 RAII 类。

`std::lock_guard` 既不可拷贝也不可移动。同样，拷贝没有意义。禁止移动是因为正如 Daniel Krüger 在 2010 年 4 月 4 日 comp.std.c++ 帖子中所说，`lock_guard` 旨在以最小开销提供最基本的功能。如果你需要可移动的锁，应该使用 `unique_lock`。

- `std::unique_lock`：灵活得多。
- 可以在构造后锁定互斥锁，在析构前解锁。
- 可移动但不可拷贝。
- 支持超时互斥锁操作：
- 通常是超时互斥锁的最佳选择。

```cpp
using RCM = std::recursive_timed_mutex; // typedef
RCM m; // 互斥锁对象
{
    std::unique_lock<RCM> L(m); // 锁定 m
    ... // 临区域
    L.unlock(); // 解锁 m
    ... // 什么都没有发生
}
```

`unique_lock` 的命名类比 `unique_ptr`。最初提过一种 "shared_lock" 类型（作为读写锁），但它未被采用 C++0x。

## 额外的 unique_lock 功能

```cpp
using TM = std::timed_mutex; // typedef
TM m; // 互斥锁对象
{
    std::unique_lock<TM> L(m, std::defer_lock); // 与 m 关联
    // 但不锁定它
    
    if (L.try_lock_for(std::chrono::microseconds(10))) {
        // 临区域
        ...
    } else {
        // 超时且未
        // 锁定 m
        ...
    }
    if (L) {
        // 转换为 bool
        // 临区域
        ...
    } else {
        // m 未被锁定
        ...
    }
}
// 如果 m 已锁定，则解锁
```

## 多重互斥锁获取

以不同的顺序获取互斥锁会导致死锁：



```cpp
int weight, value;
std::mutex wt_mutex, val_mutex;

{
    std::lock_guard<std::mutex> wt_lock(wt_mutex); // 线程 1 // 先锁 wt
    std::lock_guard<std::mutex> val_lock(val_mutex); // 后锁 val
    work with weight and value // 临区域
}

{
    std::lock_guard<std::mutex> val_lock(val_mutex); // 线程 2 // 先锁 val
    std::lock_guard<std::mutex> wt_lock(wt_mutex); // 后锁 wt
    work with weight and value // 临区域
}
```

`std::lock` 解决了这个问题：

```cpp
{ // 线程 1
  std::unique_lock<std::mutex> wt_lock(wt_mutex, std::defer_lock);
  std::unique_lock<std::mutex> val_lock(val_mutex, std::defer_lock);
  std::lock(wt_lock, val_lock); // 获取互斥锁以避免
                                // 死锁
  work with weight and value // 临区域
}
// 线程 2
{
  std::unique_lock<std::mutex> val_lock(val_mutex, std::defer_lock);
  std::unique_lock<std::mutex> wt_lock(wt_mutex, std::defer_lock);
  std::lock(val_lock, wt_lock); // 获取互斥锁以避免
                                // 死锁
  work with weight and value // 临区域
}
```

`std::lock` 避免死锁的方式未指定。它可能是常规地对锁进行排序、使用退避算法等。

如果调用 `std::lock` 时传入一个已经锁定的锁对象，则会抛出异常。如果调用 `std::lock` 时传入互斥锁对象且其中一个互斥锁已锁定，则行为可能是未定义的。（取决于互斥锁类型的细节。）

# 条件变量

允许线程之间关于共享数据的更改进行通信。

- 消费者等待直到生产者通知状态已更改。

规则：

- 在持有已锁互斥锁时调用 `wait`。
- `wait` 会解锁互斥锁，阻塞线程，并将其加入队列等待通知。

条件变量类型：

- `condition_variable`: 在 `std::unique_lock<mutex>` 上等待。最高效，适用于大多数情况。
- `condition_variable_any`: 在任何锁类型上等待。

## 等待参数

- 用于共享数据的互斥锁（必须）。
- 超时（可选）。
- 线程继续执行必须为真的谓词（可选）。

## 通知选项

- `notify_one`: 通知一个线程。
- `notify_all`: 通知所有线程。

## 等待示例

```cpp
std::atomic<bool> readyFlag(false);
std::mutex m;
std::condition_variable cv;
{
    std::unique_lock<std::mutex> lock(m); // 防止虚假唤醒
    while (!readyFlag) // 等待通知
        cv.wait(lock, []{ return readyFlag; });
    if (cv.wait_for(lock, std::chrono::seconds(1), // 谓词为
            []{ return readyFlag; })) { // 真。
            // 临区域
        }
    else {
        // 超时
        // 临区域
    }
}
```

`atomic` 类型的拷贝构造函数已删除，因此必须使用直接初始化或列表初始化语法；拷贝初始化无法编译。

原子类型定义在 `<atomic>` 中。

等待函数有 `wait`、`wait_for` 和 `wait_until`。`wait_for` 和 `wait_until` 之间的区别在于前者接受一个持续时间（等待多久），而后者接受一个绝对时间（等待到什么时候）。等待时间是绝对的（例如，无论发生多少虚假唤醒，上面的示例将总等待 1 秒）。

本页示例假设 `readyFlag`、`m` 和 `cv` 是局部变量，例如位于全局或命名空间作用域。这就是为什么 lambda 可以在不捕获的情况下引用 `readyFlag`。

## 通知示例

```cpp
std::atomic<bool> readyFlag(false); // 同前
std::condition_variable cv;
{
    readyFlag = true; // 标记为就绪
    cv.notify_one(); // 唤醒 ~1 个线程
    // 阻塞在 cv
}
{
    readyFlag = true; // 标记为就绪
    cv.notify_all(); // 唤醒所有线程
    // 阻塞在 cv（除 1 个外，其余将在 m 上阻塞）
}
```

`notify_all` 将所有阻塞线程从条件变量队列移动到相应的互斥锁队列。

示例未提及互斥锁，因为通知者在信号条件时不需要持有互斥锁。

# 线程本地数据

符合静态存储生存期的变量可以声明为 `thread_local`。

- 即全局/文件/命名空间作用域变量；类静态成员、文件变量。
- `thread_local std::string threadName;` // 例如，在全局或命名空间作用域
- `static thread_local std::chrono::microseconds timeUsed(0);` // 例如，在文件作用域

```cpp
void f(int x)
{
  static thread_local unsigned timesCalled;
  ...
}
class Widget {
private:
  thread_local static std::unordered_map<std::string, int> cache;
  ...
};
```

例如，`threadName` 变量可以由启动线程的函数设置（即传递给 `std::thread` 构造函数的函数）。

标准并没有要求对未使用的线程本地变量进行构造，因此在实现良好的实现中，线程应该只为它们使用的线程本地变量提供构造/析构。这与全局对象不同，除非实现能够证明它们没有副作用，否则它们必须被构造/析构。

## 一些细节

- 线程本地变量可以动态初始化。
- 它们的构造函数可以是任意复杂的。
- `thread_local` 可以与 `extern` 结合。

# 其他并发特性

- 静态存储生存期对象的线程安全初始化。
- 通过 `std::call_once` 和 `std::once_flag` 实现线程安全的一次性函数调用。
- 不需要等待（join）时的线程分离（detach）。
- 通过 `std::packaged_task` 实现任务设置与调用的分离。
- 通过标准接口支持互斥锁（mutex）和锁的 UDT。
- 带有内存排序操作的原子类型（例如 `std::atomic<int>`）。
- 对当前线程的操作，例如 `yield` 和 `sleep`。
- 查询硬件支持的线程数。
- 库线程安全保证（例如针对 `std::cin/std::cout`、STL 容器、`std::shared_ptr` 等）。
- 许多关于线程、锁、条件变量等的其他特性。
- 这是一个概述。

还有一个标准 API 用于获取线程背后的平台特定句柄。

"UDT" = "用户定义类型 (User Defined Type)"

查找 C++ 库线程安全保证的最佳方法是搜索草稿标准第 17 页中的 "data race（数据竞态）"。N3290 的相关章节有 17.6.5/9（通用规则）、18.6.1/4（内存分配器）、23.2.2 和 21.4/3（STL 容器和字符串），以及 27.4.1/4（栈）。有时必须读懂字外之意，例如 N3290 的 17.6.5/7 规定引用计数操作（例如在 `shared_ptr`、`promise`、`shared_future` 中）必须是线程安全的。

## 并发支持总结

- 线程运行调用对象，支持合并（join）和分离（detach）。
- 调用者必须避免参数生命周期问题。
- `std::async` 和未来（futures）支持异步调用。
- 互斥锁可能支持超时或递归；典型用法是通过锁。
- `std::lock_guard` 通常足够，`std::unique_lock` 更灵活。
- `std::lock` 在不产生死锁的情况下锁定多个互斥锁。
- 条件变量支持超时、谓词、自定义互斥锁类型。
- 符合静态存储生存期的数据可以是线程本地的。
- 本次演讲未涉及许多并发支持细节。

## 所有人适用特性总结

- 嵌套模板结束处的 `>>` 消除了一个语法陷阱。
- `auto` 变量的类型是初始化表达式的类型。
- 基于范围的 `for` 循环简化了对容器、数组等内容的迭代。
- `nullptr` 避免了整型/指针的混淆并有助于完美转发。
- Unicode 字符串编码支持 UTF-8、UCS-16 和 UTF-32。
- 统一初始化语法和 `std::initializer_list` 使得大括号初始化列表在任何地方都有效。
- Lambda 表达式在它们使用点创建函数对象。
- 模板别名允许创建“类型定义别名”。
- 并发支持包括互斥锁、锁、条件变量、线程本地数据、异步调用等。

# 概述

- 简介
- 所有人适用特性
- 库增强
- 类作者适用特性
- 库作者适用特性
- 更多特性
- 进一步信息

通常，关于库增强的材料比其他部分更简洁，因为我假设许多听者熟悉 STL 甚至可能熟悉 TR1，因此不需要提供背景信息。

# C++0xx 标准库的影响

![](img/68a90f505054116271758fb914871a74_129_0.png)

虽然 C++98 框最小，但它对 C++0xx 标准库的影响最强。

# 标准容器的新特性

## 通用

- 初始化列表支持。
- 支持移动语义以避免不必要的拷贝。
- 改进的 `const_iterator` 支持
  - `cbegin`/`cend`/`crbe` 生成常量迭代器/常量反向迭代器。
- 使用 `const_iterators` 代替迭代器来指定位置。
- `emplace`/`emplace_hint`

```cpp
std::vector<Widget> vw;
vw.emplace_back(10, 20);
```

## 特定容器

- 初始化列表支持。
- 支持移动语义以避免不必要的拷贝。
- 改进的 `const_iterator` 支持
  - `cbegin`/`cend`/`crbe` 生成常量迭代器/常量反向迭代器。
- 使用 `const_iterators` 代替迭代器来指定位置。
- `emplace`/`emplace_hint`



# C++ 并发与标准库特性

## 线程与并发支持

- 静态存储生存期对象的线程安全初始化。
- 通过 `std::call_once` 和 `std::once_flag` 实现线程安全的一次性函数调用。
- 不需要等待（join）时的线程分离（detach）。
- 通过 `std::packaged_task` 实现任务设置与调用的分离。
- 通过标准接口支持互斥锁和锁的 UDT。
- 带有内存排序操作的原子类型（例如 `std::atomic<int>`）。
- 对当前线程的操作，例如 `yield` 和 `sleep`。
- 查询硬件支持的线程数。
- 库线程安全保证（例如针对 `std::cin/std::cout`、STL 容器、`std::shared_ptr` 等）。
- 许多关于线程、锁、条件变量等的其他特性。

## 容器增强

- 初始化列表支持。
- 支持移动语义以避免不必要的拷贝。
- 改进的 `const_iterator` 支持
  - `cbegin`/`cend`/`crbegin`/`crend` 生成常量迭代器/常量反向迭代器。
- 使用 `const_iterator` 代替迭代器来指定位置。
- `emplace`/`emplace_hint`

## 线程本地存储

- 线程本地变量可以动态初始化。
- 它们的构造函数可以是任意复杂的。
- `thread_local` 可以与 `extern` 结合。

## 标准库组件总结

| 功能 | 总结 |
| --- | --- |
| 引用包装 | 像引用一样的对象 |
| 智能指针 | 引用计数智能指针 |
| 返回类型确定 | 用于模板编程 |
| 增强的成员指针适配器 | 第二代 `mem_fun`/`mem_fun_ref` |
| 增强的绑定器 | 第二代 `bind1st`/`bind2nd` |
| 通用泛型 | 函数指针的泛化 |
| 类型特质 | 编译时类型反射 |
| 随机数 | 支持自定义分布 |
| 数学特殊函数 | 拉盖尔多项式、Beta 函数等 |
| 元组 | `pair` 的泛化 |
| 固定大小数组 | 像 `vector`，但不分配动态内存 |
| 哈希表 | 基于哈希表的 `multiset`/`map`/`multimap` |
| 正则表达式 | 通用正则搜索/替换 |
| 与 C99 兼容性 | 64 位整型、`<cstdint>`、新格式规范等 |

- 变长模板消除了参数数量限制。
- 新容器约定。

# 从 TR1 到 C++0x

| TR1 功能 | C++0x 功能变化 |
| --- | --- |
| 引用包装器 (Reference Wrapper) | 无。 |
| 智能指针 (Smart Pointers) | 支持分配器和 `unique_ptr`。少量新功能（细节稍后详述）。 |
| 返回类型推导 (Return Type Determination) | 消除了固有的 C++98 限制。 |
| 增强成员指针适配器 (Enhanced Member Pointer Adapter) | 无。 |
| 增强绑定器 (Enhanced Binder) | 消除了固有的 C++98 限制。 |
| 通用泛函数 (Generalized Functors) | 支持分配器。新增 `assign`。 |
| 类型特质 (Type Traits) | 消除了固有的 C++98 限制。一些新增/重命名。 |
| 随机数 (Random Numbers) | 修改了引擎/分布器。删除了 `variate_generator`。 |
| 数学特殊函数 (Mathematical Special Functions) | C++0x 未包含。（将作为一个独立标准。） |
| 元组 (Tuples) | 添加了 `tuple_cat`。 |
| 固定尺寸数组 (Fixed Size Array) | 将 `assign` 重命名为 `fill`。 |
| 哈希表 (Hash Tables) | 支持运算符 `==` 和 `!=`。 |
| 正则表达式 (Regular Expressions) | 支持字符串字面量（不仅是 `std::string`）。 |
| C99 兼容 | `fabs(complex<T>) -> abs(complex<T>)`。 |

在 TR1 提出的 23 个数学函数中，有 21 个保留在独立的草案标准《支持数学特殊函数的 C++ 库扩展》中。缺失的两个函数是合流超几何函数和超几何函数。

“消除固有的 C++98 限制”意味着 C++0x 规范中移除了基于 C++98 库功能固有的限制。正如 Stephen T. Lavave 所述：“在 C++0x 中，`result_of` 由 `decltype` 驱动，因此始终能获得正确答案，而无需 TR1 繁琐且不完整的库机制。同样，`bind` 由右值引用驱动，消除了它对右值的限制。类型特质保证使用编译器钩子并始终获得正确答案。”从实践上讲，TR1 的许多边缘情况已不再是边缘情况了。

## 从 TR1：`shared_ptr` 和 `weak_ptr`

动机：

- 智能指针简化了资源管理。
- 例如，在抛出异常时防止内存泄漏。

标题中的“From TR1”表示这是基于 TR1 功能的 C++0x 特性。

### `shared_ptr`

- 定义在 `<memory>` 中。
- 一种引用计数的智能指针。
- 当引用计数 (RC) -> 0 时，指向的资源会被释放。

```cpp
{
  std::shared_ptr<Widget> p1(new Widget);
  std::shared_ptr<Widget> p2(p1);
  p1->doThis();
  if (p2) p2->doThat();
  ...
  p2 = nullptr;
  ...
  // RC = 0; Widget deleted
}
```

`p2 = nullptr;` 本质上等同于 `p2.reset();`

"RC" = "Reference Count"（引用计数）。

### `shared_ptr` 构造函数

- 默认、拷贝、原始指针。

```cpp
std::shared_ptr<Widget> pw1;
std::shared_ptr<Widget> pw2(pw1);
std::shared_ptr<Widget> pw3(new Widget); // 典型情况
```

- 后者是显式的：

```cpp
std::shared_ptr<Widget> pw4 = new Widget; // 错误！
```

- 兼容 `unique_ptr`、`auto_ptr`、`shared_ptr` 或 `weak_ptr`。

```cpp
std::unique_ptr<Widget> makeUP(); // 工厂函数
std::auto_ptr<Widget> makeAP();
std::shared_ptr<Widget> pw5(makeUP()); // 来自 unique_ptr
std::shared_ptr<Widget> pw6(makeAP()); // 来自 auto_ptr
std::shared_ptr<const Widget> pw7(pw3); // 添加 const
```

[`std::unique_ptr` 尚未引入。]

“兼容”指针类型考虑了派生类到基类的转换（例如，从 `shared_ptr<Derived>` 生成 `shared_ptr<Base>`）。

从 `unique_ptr` 和 `auto_ptr` 的转换仅支持非 const 源（如示例所示）。使用左值或 `unique_ptr` 初始化 `shared_ptr` 需要使用 `std::move`。

### `shared_ptr` 构造函数（进阶）

- 来自 `this` 指针：
  -> 这是一个原始指针，但可能已经存在其他的 `shared_ptr`！

```cpp
std::shared_ptr<ISomething>
Widget::getSomething()
{
    return std::shared_ptr<ISomething>(this); // 危险！
} // 可能会创建一个引用计数！
```

```cpp
std::shared_ptr<ISomething>
Widget::getSomething()
{
    return shared_from_this();
} // 安全，没有产生新 RC 的可能
```

-> 需要继承 `enable_shared_from_this`：

```cpp
class Widget : public ISomething,
    public std::enable_shared_from_this<Widget> {
    ...
};
```

"RC" = "Reference Count"。

`shared_from_this` 不能用于创建对象的第一个 `shared_ptr`。

在构造函数中使用 `shared_from_this`（例如在构造期间注册对象）是不可靠的。关于该问题的简短讨论可见：http://www.boost.org/libs/smart_ptr/sp_techniques.html#in_constructor。

### 部分 `shared_ptr` 特性

- 访问原始指针：用于遗留 API。

```cpp
std::shared_ptr<Widget> spw(new Widget);
```

- 访问引用计数：

```cpp
size_t refs = spw.use_count();
```

### 其他 `shared_ptr` 特性

- `static_pointer_cast`、`dynamic_pointer_cast`、`const_pointer_cast`
- 关系运算符：`==`、`!=`
- 输出：`std::cout << spw;`

### `weak_ptr`

`weak_ptr` 类似于原始指针，但它们知道自己可能悬空：

- 当资源的 RC -> 0 时，其 `weak_ptr` 失效。
- 释放资源的 `shared_ptr` 会让所有的 `weak_ptr` 失效：

```cpp
std::shared_ptr<Widget> spw(new Widget); // RC = 1
std::weak_ptr<Widget> wpw(spw); // RC 保持为 1
if (!wpw.expired()) ... // 如果 RC >= 1 ...
```

- 用于“观察”他人管理的数据结构。

![img](img/68a90f505054116271758fb914871a74_145_0.png)

调用 `expired()` 可能比调用 `use_count()` 快，因为 `use_count` 可能不是常数时间复杂度。

### `weak_ptr` 与循环引用

- 也为了便于处理会破坏引用计数（RC）的循环结构：
  ➡ 先重新赋值红色指针，稍后赋值蓝色指针。

![img](img/68a90f505054116271758fb914871a74_146_0.png)

使用 `shared_ptr`，在两个指针都重新赋值后，将产生一个无法回收的循环。

使用原始指针，ObjectB 无法在红色指针赋值后判断其原始指针已悬空。（蓝色指针保持了 ObjectB 的存活且可被引用）。使用 `weak_ptr` 作为后指针，ObjectB 可以检测其后指针是否悬空。

"RC" = "Reference Count"（引用计数）。

### `weak_ptr` 使用限制

`weak_ptr` 并不是真正的智能指针！

- 没有解引用运算符（没有 `operator->` 或 `operator*`）
- 没有隐式空测试（转换为类似布尔类型）。

要将 `weak_ptr` 作为指针使用，请从它创建一个 `shared_ptr`：

```cpp
std::weak_ptr<Widget> wpw(spw);                   // 危险且无法编译
wpw->doSomething();
if (!wpw.expired()) wpw->doSomething();      // 无法编译
```

```cpp
std::shared_ptr<Widget> pw1(wpw);                // 创建 shared_ptr;
// 如果 wpw 已过期则抛出异常
pw1->doSomething();                   // 正常（如果 pw1 构造成功）
```

```cpp
std::shared_ptr<Widget> pw2(wpw.lock());      // 如果 wpw 已过期则 pw2 为空
// 正常
if (pw2) pw2->doSomething();
```

### `shared_ptr` 的开销

示例实现 (Boost 1.41):

- 大小为 2 个字（指向对象的指针，指向 RC 的指针）。

![img](img/68a90f505054116271758fb914871a74_148_0.png)

- 使用动态分配的内存用于 RC。
- 通过虚函数调用释放资源（即删除） -> vbtls。
- 即使没有使用 `weak_ptr`，也会产生 `weak_ptr` 计数的代价。

"RC" = "Reference Count"。

如果构造智能指针时使用了自定义删除器或自定义分配器，Boost 实现会为其分配空间。如果使用默认删除器/分配器，则不使用内存来存储它们的指针。

弱计数跟踪对应该对象存在多少个弱指针。当 RC 变为 0 时，对象本身被销毁，RC 会持续存在直到弱计数变为 0。弱指针可以通过检查 RC 是否等于 0 来判断自己是否过期。如果是，它们会保持状态。

如果使用了 `std::make_shared`（在下一页讨论），则可以避免为 RC 进行单独内存分配。

`px` 和 `*pn.pi` 中的指针都指向受 RC 保护的对象，但指针值可能不同。根据 N1450（向 TR1 添加智能指针的提案）：“需要记住构造时传递的原始指针，以便 `shared_ptr<X>` 在 X 不完整或为 void、`~X` 不可访问或 `~X` 为虚运行时能够正确销毁对象。”

## 从 TR1 到 C++0x：`make_shared` 与 `allocate_shared`

- `make_shared<T>` 和 `allocate_shared<T>` 通过一次分配分配对象和 RC。

```cpp
auto p = std::make_shared<Widget>(ctor_args);
class MyAllocator { ... };
MyAllocator a;
auto p = std::allocate_shared<Widget>(a, Widget_args);
```

- 支持“p1 和 p2 指向同一对象”的语义
  -> `p1.get() == p2.get()`
  -> 所有权：p1 和 p2 影响同一个对象的 RC
  - 适用于指向基于 MI（多重继承）类型的 `shared_ptr<void>`。

`make_shared`/`allocate_shared` 除了指定自定义删除器的可能，无法将这些参数与对象（例如 `Widget`）构造函数的参数区分开。

`shared_ptr` 的运算符 `==` 和 `<` 使用“指向同一对象”的值语义。所有权语义可以通过 `std::shared_ptr::owner_before` 获取。

"RC" = "Reference Count"。

## TR1 派生智能指针总结

- `shared_ptr` 使用引用计数管理资源生命周期。
- 它们支持不完整类型、基于继承的转换、自定义删除器以及 C++ 风格的强制类型转换。
- `weak_ptr` 可以检测悬空指针并帮助打破循环。
- `shared_ptr` 比内置指针更大/更慢。
- `make_shared` 和 `allocate_shared` 避免了为引用计数进行专门内存分配。

## `unique_ptr`

`auto_ptr` 的继承者（C++0x 已将其废弃）。

- 定义在 `<memory>` 中。
- 与 `auto_ptr` 类似，支持移动值而不是拷贝。
- 但避免了“实际上执行了移动的拷贝语法”。
- 比 `auto_ptr` 更通用：
  - 在容器和数组中安全。
  - 支持继承转换和自定义删除器。
  - 可以指向数组。
  - 对于工厂函数的返回值，比 `shared_ptr` 更高效。
  - 可能比 `auto_ptr` 大。
- gcc 4.5: `auto_ptr` 持有 1 个指针，`unique_ptr` 持有 1 个指针。

## `forward_list`

单向链表。

- 声明在 `<forward_list>` 中
- 目标：与手写的 C 语言相比，零时间/空间开销。
- 为了实现这一目标，牺牲了 STL 容器规范：
  - 使用 `insert_after`/`emplace_after`/`erase_after` 代替 `insert`/`erase`。
  - 正常的 “insert/emplace/erase before” 行为代价高昂。



![](img/68a90f505054116271758fb914871a74_159_0.png)

- `before_begin` 返回指向 `begin` 之前的迭代器。
  - 用于在列表头部进行插入/构造/删除操作。
- 不存储大小（`size`）或末尾节点（`end`）（内存占用），且运行时间为 O(n)（这令人惊讶！）。
- 仅提供前向迭代器。

让迭代器指向所引用节点之前的节点，可以提供一种更像 STL 其他部分的接口，但其代价是增加了额外的间接解引用，这与达到等同手写 C 语言性能的目标相悖。

`forward_list` 的迭代器失效规则与 `list` 基本相同：插入不会使任何迭代器失效，删除只会使指向被删除元素的迭代器失效。

## forward_list

示例：

```cpp
#include <forward_list>
#include <algorithm>
std::forward_list<int> fli { 1, 2, 3, 4, 5 };
auto it = std::find(fli.begin(), fli.end(), 3);
fli.erase(it); // ！没有 erase
--it; // 错误！前向迭代器
fli.erase_after(it); // fli = 1, 2, 3, 5
fli.push_back(10); // ！没有 push back
fli.push_front(0); // fli = 0, 1, 2, 3, 5
fli.erase_after(fli.before_begin()); // fli = 1, 2, 3, 5
```

## 来自 TR1: 哈希表

- 声明在 `<unordered_set>` 和 `<unordered_map>` 中。
- 默认哈希功能声明在 `<functional>` 中。
- 设计为不与预-TR1/C++0x 实现冲突。
- 即 `hash_set`, `hash_map`, `hash_multiset`, `hash_multimap`。
- 接口各异——因此需要标准化的。
- 标准名称为 `unordered_set`, `unordered_map` 等。
- 尽可能与 `hash_*` 接口兼容。
- 每个桶（bucket）都有自己的元素链：

![](img/68a90f505054116271758fb914871a74_161_0.png)

- 桶的数量可以动态变化。

## 容器的特性

- 存在常规成员：
  - `iterator`/`const_iterator` 以及其他类型定义（`typedef`）。
  - `begin`/`end`/`cbegin`/`cend`, `insert`/`erase`, `size`, `swap` 等。
- 还有 3 个关联容器函数：`find`, `count`, `equal_range`。
  - 缺少 `lower_bound`/`upper_bound`。
- `unordered_map`/`unordered_multimap` 提供了 `operator[]` 和 `at`。
- 大多数关系运算符不支持：`<`, `<=`, `>=`, `>`
  - 不定的排序使得这些操作代价过高。
  - 存在 `==` 和 `!=`：结果基于内容而非排序。
    - 预期复杂度为 O(n)；最坏情况为 O(n²)。
- 仅提供前向迭代。
  - 没有反向迭代器（`reverse_iterators`），没有 `begin`/`rend`/`crbegin`/`crend`。

当 `equal_range` 未找到任何元素时，它返回 `(container.end(), container.end())`。这使得无法将 `upper_bound` 和 `lower_bound` 纳入容器接口的情况变得稍微容易接受。

## 哈希表参数

哈希和等性检查类型是模板参数：

```cpp
template<class Value, class Hash = std::hash<Value>, class Pred = std::equal_to<Value>, class Alloc = std::allocator<Value>>
class unordered_set;

template<class Key, class T, class Hash = std::hash<Key>, class Pred = std::equal_to<Key>, class Alloc = std::allocator<std::pair<const Key, T>>>
class unordered_map;
```

## TR1 元组 (Tuples)

- 元组在 `<tuple>` 中声明，辅助模板在 `<utility>` 中。
- 提供了固定大小的异构“容器”：
  - 固定大小 ⇒ 无动态内存 ⇒ 无分配器。

```cpp
class Name { ... };
class Address { ... };
class Date { ... };

std::tuple<Name, Address, Date> // 用于返回的函数
employeeInfo(unsigned employeeID); // 员工姓名，
...\ // 地址, 入职日期

unsigned eid;
...

std::tuple<Name, Address, Date> // 初始化元组
info(employeeInfo(eid)); // 使用来自
employeeInfo 的值
```

“容器”一词加了引号，是因为元组通常并不遵循容器接口。

## get

通过 `get` 访问元组元素：

- 接受一个编译时索引；索引从 0 开始：
  - `Name empName(std::get<0>(info));`
  - `Address empAddr(std::get<1>(info));`
  - `Date empHDate(std::get<2>(info));`
- 必须是编译时索引！
  - `get` 是模板，且索引是模板参数。
  - `int nameIdx = 0;`
  - `Name empName(std::get<nameIdx>(info));` // 错误；
  - 不支持对元组内容进行 for/do/while 循环。

可以使用 TMP（模板元编程）生成遍历元组内容的代码。

## get

使用命名索引使代码更可读性：

```cpp
enum { EmpName, EmpAddr, EmpHireDate };
Name empName(std::get<EmpName>(info));
Address empAddr(std::get<EmpAddr>(info));
Date empHireDate(std::get<EmpHireDate>(info));
```

## tie

`tie` 可以完成多个 `get` 的工作：

```cpp
std::tie(empName, empAddr, empHDate) = // 赋值给所有3个
               employeeInfo(eid);      // 变量
```

`ignore` 可以在 `tie` 中使用以仅获取选定的元素：

```cpp
std::tie(empName, empAddr, std::ignore) = // 仅赋值姓名
               employeeInfo(eid);      // 和地址
```

```cpp
std::tie(std::ignore,
           empAddr,\                // 仅赋值地址。
           std::ignore) = employeeInfo(eid); // (这里使用 get 会更简单。)
```

`std::tie` 可以与 `std::pair` 对象一起，因为 `std::tie` 返回一个元组，而 `std::tuple` 有一个接受 `std::pair` 的构造函数：

```cpp
std::pair<Name, Address> empNameAddr(unsigned employeeID);
```

```cpp
std::tie(empName, empAddr) = empNameAddr(eid);
```

## make_tuple

`make_pair` 的泛化：

```cpp
class Employee {
public:
    Name name() const;
    Address address() const;
    Date hireDate() const;
    ...
};
```

Employee findByID(unsigned eid);

```cpp
std::tuple<Name, Address, Date>
employeeInfo(unsigned employeeID)
{
    Employee e(findByID(employeeID));
    return std::make_tuple(e.name(), e.address(), e.hireDate());
}
```

示例中的最后一个返回语句不能写成：

`return { e.name(), e.address(), e.hireDate() };`

因为相关的元组构造函数要么是显式的（因此在此不可用），要么是模板（同样不可用，因为模板无法为大括号初始化列表推导出类型）。

## 反射 (Reflection)

支持编译反射：

```cpp
template<typename Tuple>
void someFunc(Tuple t)
{
    std::size_t numElems = // Tuple 中的
    std::tuple_size<Tuple>::value; // 元素数量
    typedef
    typename std::tuple_element<0, Tuple>::type // 第 1 个元素的
    FirstType; // 类型
...}
```

## 其他元组功能

通常的 STL 容器关系运算符 (`<`, `<=`, `!=`, `>=`, `>`)：

- `==` 和 `!=` 使用逐元素的 `==`
- 其他关系测试仅使用 `<` 进行字典序比较
- 如果值是价的（基于 `<`），则被视为相等
- `pair<T1, T2>` 经常可以当作 `tuple<T1, T2>` 使用：
  - 可以从兼容的 pair 创建或赋值 2元素元组。
  - `get<0>` 和 `get<1>` 可作用于 pair。
  - 同样适用于 `tuple_size` 和 `tuple_element`。

## 元组总结

- 元组是 `std::pair` 的泛化。
- 通过 `get` 或 `tie` 使用编译时索引访问元素。
- 支持编译时反射。它也适用于 `std::pair`。

## 来自固定大小数组

动机：

- 内置数组不是 STL 容器：
  - 没有 `begin`、`end` 等。
  - 它们不知道自己的大小。
  - 它们会退化为指针。
- `vector` 带来了开销：
  - 动态内存分配。
- 具有内置数组性能的 STL 容器。

## 固定大小数组

- 定义在 `<array>` 中。
- 提供常规成员：`iterator`/`const_iterator`/`reverse_iterator` 以及 `begin`/`end`/`cbegin`/`cend`、`swap`、关系运算符。
- `swap` 以线性（而非常数）时间运行。
- 其他成员：`operator[]`、`at`、`front`、`back`，布局与 C 数组（以及 vector）兼容。
- 通过 `data` 获取元素的指针：

```cpp
std::array<int, 5> arr; // 创建数组
int *p = arr.data(); // 获取元素指针
```

由于是固定大小的：

- 没有 `insert`、`push_back`、`clear`。
- STL 容器具有内置数组的性能。

## 聚合体 (Aggregates)

`std::array` 是聚合体，所以：

- 所有成员都是公共的！
- 只支持默认、拷贝和移动构造。
- 这些构造函数是编译器生成的。
- 不支持范围构造：

```cpp
std::vector<int> v;
...
std::array<int, 10> // 错误！数组仅支持
arr(v.begin(), v.begin()+10); // 默认和拷贝构造
```

技术上，聚合体可能有非公共静态成员。

## 作为元组的数组 (arrays as Tuples)

`array<T, n>` 有时可以被视为 `tuple<T, T, ..., T>`：

```cpp
class Widget { ... };
const std::size_t arraySz = 10;
typedef std::array<Widget, arraySz> WidgetArray;
WidgetArray arr; // 10 个 Widget 默认构造
...
std::size_t numElements = std::tuple_size<WidgetArray>::value;
std::size_t elemSize =
sizeof(std::tuple_element<0, WidgetArray>::type);
const auto& value = std::get<0>(arr);
std::cout << "arr 有 " << numElements
          << " 个元素，每个大小为 " << elemSize
          << ". 第一个元素的值是 " << value
          << "\n";
```

## array vs. vector

- `array` 是固定大小的，`vector` 是动态大小的。
- `array` 不使用动态内存，`vector` 则使用。
- `array::swap` 是线性时间且可能抛出异常，`vector::swap` 是常数时间且不会抛出异常。
- `array` 可以被视为元组（tuple）处理，`vector` 则不能。

## array vs. C 数组

- `array` 对象知道自己的大小，C 数组不知道。
- `array` 允许包含 0 个元素，C 数组不允许。
- `array` 需要显式大小，C 数组可以从初始化器中推导出大小。
- `array` 支持赋值，C 数组不支持。
- `array` 可以被视为元组处理，C 数组不能。

既然已经有了 `array`、`vector` 和 `string`，已经没有理由继续使用 C 风格的数组了。

## 固定大小数组总结

- `array` 对象是 STL 化的 C 数组。
- 它们支持大括号初始化，但不支持范围初始化。
- 它们支持一些元组操作。
- 既然已经有了 `array`、`std::vector` 和 `std::string`，已经没有理由继续使用 C 风格的数组。

## 来自 TR1：正则表达式

动机：



# 正则表达式（RE）功能非常有用

- 许多编程语言和工具都支持它。
- C 语言的正则库仅支持基于 `char*` 的字符串。
  - C++ 也应该支持 `wchar_t*` 字符串和字符串对象。

概念上来说，C++0x 的正则支持不仅适用于 `std::string`，还适用于所有 `std::basic_string` 的实例化（例如 `std::wstring`、`std::u16string`、`std::u32string`）。然而，库的特化和重载仅存在基于 `char*`、`wchar_t*`、`std::string` 和 `std::wstring` 的字符串。将库的正则组件与其他字符串类型配合有多困难我不知道。

## TR1 正则表达式

- 定义在 `<regex>` 中。
- RE 对象以字符串对象为模型：
- 支持 `char`、`wchar_t` Unicode 编码以及本地化配置因素（locals）。
- RE 语法默认使用修改后的 ECMAScript。

```cpp
std::regex capStartRegex("[A-Z][[:alnum:]]");
```

- 备选方案：POSIX Basic、POSIX Extended、awk、grep、egrep。
- 原始字符串字面量在 RE 规范中非常有用。
- 提供对状态机行为的控制：

```cpp
std::regex filenameRegex // 某些文件的正则
("(\\w+(\\.txt))(dat))"), // .txt, dat 和 .log 文件；
std::regex::icase // 搜索时忽略大小写；
std::regex::optimize // 匹配速度比正则 c 语言速度更重要
```

Scott Meyers，软件开发顾问

http://www.aristeia.com/

© 2011 Scott Meyers，保留所有权利。

第190 页幻灯片

ECMAScript 本质上是 Perl RE 语法的标准版本。

"SSN" 是 "Security Number"（安全号码）的缩写。

## 基础功能

- `regex_match`：RE 是否匹配整个字符串？
- `regex_search`：RE 是否出现在字符串中？
- `regex_replace`：将匹配 RE 的文本替换为其他文本。
- 替换不是原地的：返回新文本。

匹配结果存储在 `match_results` 对象中。支持迭代：

- `regex_iterator`：遍历字符串的匹配项。
- `regex_token_iterator`：遍历匹配项并匹配子字段。

这些是常用的实例化类型：

- 对于字符串：`smatch`/`sregex_iterator`/`sregex_token_iterator`
- 对于 wstrings：`wmatch`/`wsregex_iterator`/`wsregex_token_iterator`
- 对于 `char*`：`cmatch`/`creg_iterator`/`creg_token_iterator`
- 对于 `wchar_t*`：`wcmatch`/`wregex_iterator`/`wregex_token_iterator`

`regex_replace` 可以配置标志以 (1) 仅替换第一个匹配项和/或 (2) 不覆盖未匹配的文本，但默认情况下，正如这些幻灯片所总结的那样。我不熟悉这些选项的用例。

正则迭代器只迭代非重叠匹配项。对重叠匹配项的迭代必须手动完成，并且必须考虑 Becker 书中描述的问题（在随后的幻灯片中提到）。

我不知道为什么没有基于 `char16_t` 和 `char32_t` 类型的 `typedef`（例如 `char16_t*` 和 `u16strings`）。

## 示例：regex_match, regex_search

文本看起来像 SSN 吗？

```cpp
const std::regex SSNRegex(R"(\d{3}-\d{2}-\d{4})");
```

```cpp
bool looksLikeSSN(const std::string& text)
{
    return std::regex_match(text, SSNRegex);
}
```

文本包含包含像 SSN 的子字符串吗？

```cpp
bool mayContainSSN(const std::string& text)
{
    return std::regex_search(text, SSNRegex);
}
```

找到匹配的信息可以通过可选的 `match_results` 参数获取。下一页幻灯片提供了一个示例。

## 示例：regex_search

收集所有像 SSN 的（非重叠）子字符串：

```cpp
void possibleSSNs1(const std::string& text, std::list<std::string>& results) {
  auto b = std::sregex_iterator(text.begin(), text.end(), SSNRegex);
  auto e = std::sregex_iterator();
  for (; b != e; ++b) {
    results.push_back(b->str());
  }
}
```

## 可调用实体

可以像函数一样调用的东西：

- 函数、函数指针、函数引用：

```cpp
void f(int x);               // 函数
void (*fp)(int) = f;      // 函数指针
int val;
...
f(val);                   // 调用 f
fp(val);                  // 调用 *fp
```

“可调用实体”（callable entity）这个术语是我自创的，它比 C++0x 的“可调用对象”（callable object）的概念稍微受限一些，因为可调用对象包含了成员数据指针。可调用对象还包括指向非静态成员函数的指针，而我在讨论 `std::function` 时没有提到它们。（不过我在结合 `std::bind` 和 lambda 表达式时讨论过它们，这两者都会产生可以存储在 `std::function` 对象中的函数对象。）

## 可调用实体

- 可以隐式转换为其中一种的对象：

```cpp
class Widget {
public:
    using FuncPtr = void (*)(int);
    operator FuncPtr() const; // 转换为函数指针
    ...
};
Widget w;                 // 具有转换为函数指针转换的对象
int val;
...
w(val);                   // “调用” w，即：
                          // 调用 (w.operator FuncPtr())
```

## 可调用实体

- 函数对象（包括闭包）：

```cpp
class Gadget {
public:
    void operator()(int); // 函数调用运算符
    ...
};
Gadget g; // 支持 operator()) 的对象
int val;

g(val); // “调用” g，即：调用 w.operator())

auto f = [](int x) { return x < currentThreshold(); };
if (f(val)) ... // “调用”闭包
```

## std::function 基础

- 定义在 `<functional>` 中。
- `std::function` 是可调用实体的类型安全封装器：

```cpp
std::function<int(std::string&)> f; // f 指向可调用实体
// 与给定的签名兼容
```

```cpp
int someFunc(std::string&); // 某个函数
f = someFunc; // f 指向 someFunc
```

```cpp
f = [](std::string s)->unsigned
    { s = "!"; return s.size(); }; // f 指向 lambda 的闭包
```

```cpp
class Gadget {
public:
    int operator()(std::string&);
    ...
}; // 函数调用运算符
```

```cpp
f = g; // f 指向 g
```

## 新 C++ (C++0x) 概述

### 基础行为

![](img/68a90f505054116271758fb914871a74_205_0.png)

```cpp
int someFunc(std::string); // 某个函数
f = someFunc;
std::string str;
...
int result = f(str); // 调用 someFunc
f = [](std::string& s)->unsigned { s += "!"; return s.size(); };
...
result = f(str); // 调用 λ 的闭包
```

Scott Meyers, 开发顾问 http://www.aristeia.com/ 2011 Scott Meyers, 版权所有。

幻灯片 204

外框表示 `std::function` 对象，内框表示它封装的可调用实体（即转发调用的地方）。

Scott Meyers, 开发顾问

http://www.aristeia.com/ 2011 Scott Meyers, 版权所有。

从 Wow! eBook 下载：www.wowebook.com *

## 兼容的签名

如果满足以下条件，可调用实体与函数对象是兼容的：

- 函数对象的参数类型可以转换为实体的参数类型。
- 实体的返回类型可以转换为函数的对象的类型。

![](img/68a90f505054116271758fb914871a74_206_0.png)

所有实体的返回类型都与返回 void 的函数对象兼容。

## 函数回调示例

支持点击事件回调的 Button 类：

- 回调参数表示按下或松起点击。

```cpp
class Button: public SomeGUIFrameworkBaseClass {
public:
    using CallbackType = std::function<void(short)>;
    void setCallback(const CallbackType& cb) {
        clickHandler = cb;
    }
    virtual void onClick(short upOrDown) // 由基类调用 {
        clickHandler(upOrDown); // 调用函数对象
    }
private:
    CallbackType clickHandler;
};
```

## 函数回调示例

```cpp
void buttonClickHandler(int eventType); // 非成员函数
class ButtonHandler {
public:
    static int clicked(short upOrDown); // 静态成员函数
};
void (*clicker)(int) = buttonClickHandler; // 函数指针
Button b;

b.setCallback(buttonClickHandler); // 传递非成员函数
b.setCallback(ButtonHandler::clicked); // 传递静态成员函数
b.setCallback(clicker); // 传递函数指针
```

注意（兼容的）类型不匹配：

- `buttonClickHandler` 和 `clicker` 接收 `int`，而不是 `short`
- `ButtonHandler::clicked` 返回 `int`，而不是 `void`

| Scott Meyers, 开发顾问 | © 2011 Scott Meyers, 版权所有。 |
| http://www.aristeia.com/ | 幻灯片 207 |

对于静态成员函数，在获取它们的地址时（即作为非成员函数使用时），在名称前使用 "&" 是可选的。

## 函数回调示例

```cpp
class ButtonClickCallback {
public:
    void operator()(short upOrDown) const;
};
Button b;
...
ButtonClickCallback bccb;
b.setCallback(bccb);
void logClick(short upOrDown);
b.setCallback([&](int v) { logClick(v); });
```

## 函数回调示例

```cpp
class ButtonHandler {
public:
    int clicked(short upOrDown) const; // 同前，但是非静态的
};
Button b;
ButtonHandler bh;
...
b.setCallback(std::bind(&ButtonHandler::clicked, bh, _1)); // 传递非静态成员函数
// 即将提供 std::bind 的信息
```

`ButtonHandler::clicked` 是 const，因为 `_1` 实际上在 `std::placeholders` 中，所以本页提到的 bind 涉及 lambda。

## 新 C++ (C++0x) 概述

### 其他特性

- 定义在 `<functional>` 中。
- `std::function` 是可调用实体的类型安全封装器：

```cpp
std::function<int(std::string&)> f; // f 指向可调用实体
// 与给定的签名兼容
```

```cpp
int someFunc(std::string&); // 某个函数
f = someFunc; // f 指向 someFunc
```

```cpp
f = [](std::string s)->unsigned
    { s = "!"; return s.size(); }; // f 指向 lambda 的闭包
```

```cpp
class Gadget {
public:
    int operator()(std::string&);
    ...
}; // 函数调用运算符
```

```cpp
f = g; // f 指向 g
```

### 基础行为

![](img/68a90f505054116271758fb914871a74_205_0.png)

```cpp
int someFunc(std::string); // 某个函数
f = someFunc;
std::string str;
...
int result = f(str); // 调用 someFunc
f = [](std::string& s)->unsigned { s += "!"; return s.size(); };
...
result = f(str); // 调用 λ 的闭包
```

Scott Meyers, 开发顾问 http://www.aristeia.com/ 2011 Scott Meyers, 版权所有。

幻灯片 204

外框表示 `std::function` 对象，内框表示它封装的可调用实体（即转发调用的地方）。

Scott Meyers, 开发顾问

http://www.aristeia.com/ 2011 Scott Meyers, 版权所有。

从 Wow! eBook 下载：www.wowebook.com *

## 兼容的签名

如果满足以下条件，可调用实体与函数对象是兼容的：

- 函数对象的参数类型可以转换为实体的参数类型。
- 实体的返回类型可以转换为函数的对象的类型。

![](img/68a90f505054116271758fb914871a74_206_0.png)

所有实体的返回类型都与返回 void 的函数对象兼容。

## 函数回调示例

支持点击事件回调的 Button 类：

- 回调参数表示按下或松起点击。

```cpp
class Button: public SomeGUIFrameworkBaseClass {
public:
    using CallbackType = std::function<void(short)>;
    void setCallback(const CallbackType& cb) {
        clickHandler = cb;
    }
    virtual void onClick(short upOrDown) // 由基类调用 {
        clickHandler(upOrDown); // 调用函数对象
    }
private:
    CallbackType clickHandler;
};
```

## 函数回调示例

```cpp
void buttonClickHandler(int eventType); // 非成员函数
class ButtonHandler {
public:
    static int clicked(short upOrDown); // 静态成员函数
};
void (*clicker)(int) = buttonClickHandler; // 函数指针
Button b;

b.setCallback(buttonClickHandler); // 传递非成员函数
b.setCallback(ButtonHandler::clicked); // 传递静态成员函数
b.setCallback(clicker); // 传递函数指针
```

注意（兼容的）类型不匹配：

- `buttonClickHandler` 和 `clicker` 接收 `int`，而不是 `short`



- `ButtonHandler::clicked` 返回 `int`，而不是 `void`

| Scott Meyers, 开发顾问 | © 2011 Scott Meyers, 版权所有。 |
| http://www.aristeia.com/ | 幻灯片 207 |

对于静态成员函数，在获取它们的地址时（即作为非成员函数使用时），在名称前使用 `&` 是可选的。

## 函数回调示例

```cpp
class ButtonClickCallback {
public:
    void operator()(short upOrDown) const;
};
Button b;
...
ButtonClickCallback bccb;
b.setCallback(bccb);
void logClick(short upOrDown);
b.setCallback([&](int v) { logClick(v); });
```

## 函数回调示例

```cpp
class ButtonHandler {
public:
    int clicked(short upOrDown) const; // 同前，但是非静态的
};
Button b;
ButtonHandler bh;
...
b.setCallback(std::bind(&ButtonHandler::clicked, bh, _1)); // 传递非静态成员函数； // 即将提供 std::bind 的信息
```

`ButtonHandler::clicked` 是 `const`，因为 `_1` 实际上在 `std::placeholders` 中，所以本页提到的 `bind` 涉及 `lambda`。

## 新 C++ (C++0x) 概述

### 其他特性

- 定义在 `<functional>` 中。
- `std::function` 是可调用实体的类型安全封装器：

```cpp
std::function<int(std::string&)> f; // f 指向可调用实体
// 与给定的签名兼容
```

```cpp
int someFunc(std::string&); // 某个函数
f = someFunc; // f 指向 someFunc
```

```cpp
f = [](std::string s)->unsigned
    { s = "!"; return s.size(); }; // f 指向 lambda 的闭包
```

```cpp
class Gadget {
public:
    int operator()(std::string&);
    ...
}; // 函数调用运算符
```

```cpp
f = g; // f 指向 g
```

### 基础行为

![](img/68a90f505054116271758fb914871a74_205_0.png)

```cpp
int someFunc(std::string); // 某个函数
f = someFunc;
std::string str;
...
int result = f(str); // 调用 someFunc
f = [](std::string& s)->unsigned { s += "!"; return s.size(); };
...
result = f(str); // 调用 λ 的闭包
```

Scott Meyers, 开发顾问 http://www.aristeia.com/ 2011 Scott Meyers, 版权所有。

幻灯片 204

外框表示 `std::function` 对象，内框表示它封装的可调用实体（即转发调用的地方）。

Scott Meyers, 开发顾问

http://www.aristeia.com/ 2011 Scott Meyers, 版权所有。

从 Wow! eBook 下载：www.wowebook.com *

## 兼容的签名

如果满足以下条件，可调用实体与函数对象是兼容的：

- 函数对象的参数类型可以转换为实体的参数类型。
- 实体的返回类型可以转换为函数的对象的类型。

![](img/68a90f505054116271758fb914871a74_206_0.png)

所有实体的返回类型都与返回 `void` 的函数对象兼容。

## 函数回调示例

支持点击事件回调的 `Button` 类：

- 回调参数表示按下或松起点击。

```cpp
class Button: public SomeGUIFrameworkBaseClass {
public:
    using CallbackType = std::function<void(short)>;
    void setColor(const CallbackType& cb) {
        clickHandler = cb;
    }
    virtual void onClick(short upOrDown) // 由基类调用 {
        clickHandler(upOrDown); // 调用函数对象
    }
private:
    CallbackType clickHandler;
};
```

## 函数回调示例

```cpp
void buttonClickHandler(int eventType); // 非成员函数
class ButtonHandler {
public:
    static int clicked(short upOrDown); // 静态成员函数
};
void (*clicker)(int) = buttonClickHandler; // 函数指针
Button b;

b.setCallback(buttonClickHandler); // 传递非成员函数
b.setCallback(ButtonHandler::clicked); // 传递静态成员函数
b.setCallback(clicker); // 传递函数指针
```

注意（兼容的）类型不匹配：

- `buttonClickHandler` 和 `clicker` 接收 `int`，而不是 `short`
- `ButtonHandler::clicked` 返回 `int`，而不是 `void`

| Scott Meyers, 开发顾问 | © 2011 Scott Meyers, 版权所有。 |
| http://www.aristeia.com/ | 幻灯片 207 |

对于静态成员函数，在获取它们的地址时（即作为非成员函数使用时），在名称前使用 `&` 是可选的。

## 函数回调示例

```cpp
class ButtonClickCallback {
public:
    void operator()(short upOrDown) const;
};
Button b;
...
ButtonClickCallback bccb;
b.setCallback(bccb);
void logClick(short upOrDown);
b.setCallback([&](int v) { logClick(v); });
```

## 函数回调示例

```cpp
class ButtonHandler {
public:
    int clicked(short upOrDown) const; // 同前，但是非静态的
};
Button b;
ButtonHandler bh;
...
b.setCallback(std::bind(&ButtonHandler::clicked, bh, _1)); // 传递非静态成员函数； // 即将提供 std::bind 的信息
```

`ButtonHandler::clicked` 是 `const`，因为 `_1` 实际上在 `std::placeholders` 中，所以本页提到的 `bind` 涉及 `lambda`。

## From TR1: bind

Motivation:

- `bind1st` 和 `bind2nd` 受限：
  - 只能绑定第一个或第二个参数。
  - 每次只能绑定一个。
  - 不能绑定引用参数的函数。
  - 需要适配器函数对象。
  - 通常需要 `ptr_fun`, `mem_fun` 和 `mem_fun_ref`。

`bind1st` 和 `bind2nd` 在 C++0x 中被废弃。

### bind

- 定义在 `<functional>` 中。
- 从以下内容产生函数对象：
  - 一个可调用实体。
  - 绑定参数的指定。
    `functionObject std::bind(callableEntity, 1stArgBinding, 2ndArgBinding, ... nthArgBinding);`
- 占位符允许将 `bind` 的返回值映射到可调用对象。
  - `_n` 指定传递给 `bind` 对象的第 n 个参数。

### bind Basics

```cpp
int f(int x, int y);
auto bf = std::bind(f, 10, _1); // 等于 std::bind1st(f, _1);
```

![](img/68a90f505054116271758fb914871a74_215_0.png)

```cpp
int val = bf(99); // 调用绑定函数
```

![](img/68a90f505054116271758fb914871a74_215_1.png)

占位符或形式参数名显示在表示它们所属实体的框内部。因此，外框（表示 `std::bind` 返回的函数）的占位符名称为 `_1`。

`_1` 实际上在 namespace `std::placeholders` 中，所以除非通过 `using` 声明使 `std::placeholders::_1` 可用，否则本页的 `bind` 调用无法编译。

`bf` 不是从 `bind` 返回的对象相同，但极有可能，它是从 `bind` 返回的值移动构造而来的。

### 绑定非静态成员函数

对于非静态成员函数，这种绑定来自于第一个参数：

- 就像 `bind1st` 和 `bind2nd` 一样。

```cpp
class ButtonHandler {
    // 来自 std::function 示例
    ...
    int clicked(short upOrDown) const;

    Button b;
    ButtonHandler bh;
    ...
    b.setCallback(std::bind(&ButtonHandler::clicked, bh, _1));
}
```![](img/68a90f505054116271758fb914871a74_216_0.png)

`_1` 实际上位于 `std::placeholders` 命名空间中，因此除非使 `std::placeholders::_1` 可见（例如，通过 `using` 声明），否则本页上的 `bind` 调用将无法如所示通过编译。在实践中，这几乎总是在使用 `bind` 的代码中完成的。

`std::bind` 会拷贝它所绑定的参数，因此在 `bind` 返回的函数对象内部使用了 `copyOfbh` 这个名称。

### 绑定非静态成员函数

`bind` 通过以下方式支持此操作：

- **对象：**
  `EventHandler bh; b.setCallback(std::bind(&EventHandler::clicked, bh, _1));`
- **指针：**
  `ButtonHandler *pbh; b.setCallback(std::bind(&ButtonHandler::clicked, pbh, _1));`
- **智能指针：**
  `std::unique_ptr<ButtonHandler> sp;
  b.setCallback(std::bind(&ButtonHandler::clicked, sp, _1));`
  `std::unique_ptr<ButtonHandler> up;
  b.setCallback(std::bind(&ButtonHandler::clicked, std::ref(up), _1));`
  `MyCustomSmartPtr<ButtonHandler> mcsp;
  b.setCallback(std::bind(&ButtonHandler::clicked, mcsp, _1));`

`std::unique_ptr` 在绑定时必须由 `std::ref` 封装，因为 `std::unique_ptr` 是不可拷贝的（它只是可移动的）。

只要智能指针按照常规方式定义了 `operator*`（即返回指向所指对象的引用），就可以与 `bind` 使用。（这意味着 `std::weak_ptr` 无法与 `bind` 使用。）

### 绑定第 2 个之后的参数

绑定第 2 个之后的参数很容易：

```cpp
class Point {
public:
  ...
  void translate(int deltaX, int deltaY);
};
std::vector<Point> vp;
...
std::for_each( // 移动点
  vp.begin(), vp.end(), // 在 vp 中移动 (10, 20)
  std::bind(&Point::translate, _1, 10, 20) // 注意 deltaY
  ); // 是第 3 个参数
```

- `bind` 的占位符参数通过引用传递，因此此循环修改的是 `vp` 中的 `Points`，而不是它们的拷贝。

对应于 `bind` 占位符的参数使用完美转发传递传递。

`_1` 实际上位于 `std::placeholders` 命名空间中，除非使 `std::placeholders::_1` 可见（例如，通过 `using` 声明），否则本页上的 `bind` 调用将无法如所示通过编译。在实践中，这几乎总是在使用 `bind` 的代码中完成的。

### bind 与适配器

与 `bind1st` 和 `bind2nd` 不同，`bind` 不需要适配器：

```cpp
class Point {
public:
  ...
  void setColor(Color c);
};
std::forward_list<Point> flp;
...
// 不使用 bind
std::for_each(
  flp.begin(), flp.end(),
  std::bind2nd(std::mem_fun_ref(&Point::setColor), _1, green);
);
// 使用 bind
std::for_each(flp.begin(), flp.end(),
  std::bind(&Point::setColor, _1, green));
```

`_1` 实际上位于 `std::placeholders` 命名空间中，除非使 `std::placeholders::_1` 可见（例如，通过 `using` 声明），否则本页上的 `bind` 调用将无法如所示通过编译。在实践中，这几乎总是在使用 `bind` 的代码中完成的。

### bind 与函数对象

`bind` 的结果通常存储在函数对象中：

```cpp
class Button : public SomeGUIFrameworkBase { // 来自
public:
    typedef std::function<void(short)> CallbackType; // 讨论
    void setCallback(const CallbackType& cb) {
    { clickHandler = cb; }
    ...
private:
    CallbackType clickHandler;
};
class ButtonHandler { // 来自
public:
    int clicked(short upOrDown) const; // 较早
};
Button b;
ButtonHandler bh;
...
b.setCallback(std::bind(&ButtonHandler::clicked, bh, _1));
```

`_1` 实际上位于 `std::placeholders` 命名空间中，除非使 `std::placeholders::_1` 可见（例如，通过 `using` 声明），本页上的 `bind` 调用将无法如所示通过编译。在实践中，这几乎总是在使用 `bind` 的代码中完成的。

## 新 C++ (C++11x) 概述

### bind 的趣味

`bind` 允许对重排列和重复参数：

```cpp
void f(int a, int b, int c);
int x, y, z;
...
std::function<void(int, int)> f1 = std::bind(f, _1, _1, _2);
f1(x, y);
```![](img/68a90f505054116271758fb914871a74_216_0.png)

```cpp
std::function<void(int, int)> f2 = std::bind(f, _3, _2, _1);
f2(x, y);
```![](img/68a90f505054116271758fb914871a74_221.png)

这些图具有误导性，因为它们没有显示由 `bind` 封装的 `std::function` 对象。`_1`、`_2` 和 `_3` 实际上位于 `std::placeholders` 命名空间，除非 `std::placeholders::_1`（同样对于 `_2` 和 `_3`）可见（例如，通过 `using` 声明）。在实践中，这几乎总是使用 `bind` 的代码完成的。

## Lambda vs bind

`Lambda` 和 `bind` 都会创建函数对象：

```cpp
std::for_each(vp.begin(), vp.end(),
  std::bind(&Point::translate, _1, 10, 20));
std::for_each(vp.begin(), vp.end(),
  [](Point& p) { p.translate(10, 20); });
```



```cpp
b.setCallback(std::bind(&ButtonHandler::clicked, _1));
b.setCallback([=](short upOrDown) { bh.clicked(upOrDown); });
```

```cpp
std::function<void(int, int, int)> f2 = std::bind(f, _3, _2, _1);
std::function<void(int, int, int)> f2 = [](int a, int b, int c) { f(c, b, a); };
```

很多人发现 Lambda 更清晰。

- 没有 `_1`、`_2` 等。本页上的所有示例均来自。

## Lambda vs bind

当需要比简单的绑定时，Lambda 更加清晰：

```cpp
class Person {
  public:
    std::size_t age() const;
    ...
};
std::vector<Person> vp;
...
std::partition(vp.begin(), vp.end(),
  [](const Person& p) { return p.age() < 10; }
);
std::partition(vp.begin(), vp.end(),
  std::bind(std::less<std::size_t>(), 10), // ???
  std::bind(std::greater<std::size_t>(), 20) // ???
);
```

据我所知，没有方法在 `partition` 调用中使用 `bind`，因为没有方法将外部调用的 `_1` 映射到另外两个调用。

## Lambda vs bind

Lambda 通常生成更好的代码。

- 通过 `bind` 调用会涉及函数指针 ⇒ 无法内联。
- 通过闭包调用允许完全内联。

## bind 总结

- 泛化了 `bind1st` 和 `bind2nd`（现已废用）。
- 不需要 `ptr_fun`、`mem_fun`、`mem_fun_ref` 或 `std::mem_fn`。
- 结果通常存储在函数对象中。
- 通常通常优于 Lambda。

## C++0x 新算法

R 是一个范围，e 是一个元素，p 是谓词：

- `all_of`：R 中的所有元素是否满足 p 为真？
- `any_of`：R 中的任意元素是否满足 p 为真？
- `none_of`：R 中没有元素是否满足 p 为真？
- `find_if_not`：在 R 中查找第一个 p 为假的元素。
- `copy_if`：拷贝 R 中所有 p 为真的元素。
- `copy_n`：拷贝 R 的前 n 个元素。
- `iota`：为 R 中的所有元素赋值从 v 开始的值。
- `minmax`：对于给定输入返回 (minVal, maxVal)。
- `minmax_element`：对于 R 返回 (min_element, max_element)。
- `min`/`max`/`minmax` 返回值。
- `min_element`/`max_element`/`minmax_element` 返回迭代器。

`minmax` 和 `minmax_element` 的描述不同，因为 `minmax` 重载了以接受单个对象或初始化列表，但不接受范围。

`max_element` 仅接受范围。

## C++0x 新算法

R 是一个范围，e 是一个元素，p 是谓词，v 是一个值：

- `partition_copy`：根据 `p(e)` 将 R 中的所有 e 拷贝到两个目标地之一。
- `is_partitioned`：R 是否按照 p 划分？
- `partition_point`：在 R 中查找第一个 `p(e)` 为假的元素。
- `is_sorted`：R 是否排序？
- `is_sorted_until`：在 R 中查找第一个无序的 e。
- `is_heap`：R 中的元素是否形成一个堆？
- `is_heap_until`：在 R 中查找第一个不在堆顺序的 e。
- `move`：像 `copy`，但 R 中的每个 e 都会被移动。
- `move_backward`：像 `copy_backward`，但 R 中的每个 e 都会被移动。
- `std::move_iterator` 将拷贝算法转换为移动，例如：

```cpp
std::copy_if(std::move_iterator<Lt>(b), // == std::copy_if(b, e, p),
  std::move_iterator<Lt>(e), // 但是移动而不是
  p);
```

实际上不需要 `std::move` 和 `std::move_backward`，因为它们的效果可以通过 `copy`、`copy_backward` 和 `move_iterators` 实现，但根据 Howard Hinnant 在 `comp.std.c++` 上的帖子，委员会认为这两个算法可能会被频繁使用，为了符号表示上的方便，提供了它们的移动版本。

## C++0x 中扩展的 C++98 算法

- `swap`: 接收数组的新重载
- `min`: 接收初始化列表的新重载
- `max`: 接收初始化列表的新重载

## 库的增强总结

- C++98 容器增加了初始化列表、就地构造（`emplace`）和移动语义。
- 采纳了除数学函数外的 TR1 功能。
- `forward_list` 是一个单向链表。
- `unique_ptr` 替换了 `auto_ptr`。
- 18 种新算法。

从 C++03 迁移到 C++0x 时，还有许多细微的库变化，例如，在 C++03 中用于 STL 算法的函数对象通常禁止产生副作用，而在 C++0x 中，允许某些副作用。例如，在 C++03 中，`accumulate` 的规范说“binary_op 不得引起副作用”，但在 `accumulate` (26.7.2/2 of N3290) 中，相应的表述是“在范围 [first,last] 内，binary_op 既不修改元素，也不使迭代器或子范围失效”。

## 概述

- 引言
- 面向所有人的功能
- 库增强
- 面类作者的功能
- 面库作者的功能
- 更多功能
- 更多信息

## 移动支持

C++ 有时会执行不拷贝：

```cpp
typedef std::vector<T> TVec;
TVec createTVec(); // 工厂函数
TVec vt;
...
vt = createTVec(); // 将返回值对象拷贝到 vt，
// 然后销毁返回值
```

![](img/68a90f505054116271758fb914871a74_231_0.png)

幻灯片上的图是一个 PowerPoint 动画。

在讨论过程中，我使用 T 的容器而不是指定特定类型，例如 string 容器或 int 容器。移动语义的动机在很大程度上独立于涉及的类型，尽管类型越大、拷贝开销越贵，移动优于拷贝的理由就越充分。

## 移动支持

移动值会更便宜：

```cpp
TVec vt;
...
vt = createTVec();
// 将返回值对象中的数据移动
到 vt，然后销毁返回值
// 对象
```

![](img/68a90f505054116271758fb914871a74_232_0.png)

幻灯片上的图是一个 PowerPoint 动画。

## 移动支持

向满的 vector 添加元素会在添加之前导致大量拷贝：

```cpp
std::vector<T> vt;
...
t.push_back(T object); // 假设 vt 缺乏
// 未使用的容量
```

![](img/68a90f505054116271758fb914871a74_233_0.png)

幻灯片上的图是一个 PowerPoint 动画。

新元素必须在销毁旧元素之前被添加到 vector 的新存储中，因为新元素可能是现有元素的拷贝，例如 `vt.emplace_back(vt{0})`。

## 移动支持

再次，移动会更高效：

```cpp
std::vector<T> vt;
...
vt.push_back(T object); // 假设 vt 缺乏
                          未使用的容量
```

![](img/68a90f505054116271758fb914871a74_234_0.png)

其他的 vector 和 deque 操作同样可以受益。

- `insert`、`emplace`、`resize`、`erase` 等。

幻灯片上的图是一个 PowerPoint 动画。

## 移动支持

另一个例子：

```cpp
template<typename T> // 简单的 std::swap 实现
void swap(T& a, T& b)
{
    T tmp(a); // 将 a 拷贝到 tmp (⇒ 2 次 a 的拷贝)
    a = b; // 将 b 拷贝到 a (⇒ 2 次 b 的拷贝)
    b = tmp; // 将 tmp 拷贝到 b (⇒ 2 次 tmp 的拷贝)
} // 销毁 tmp
```

![](img/68a90f505054116271758fb914871a74_235_0.png)

幻灯片上的图是一个 PowerPoint 动画。这就是为什么文本看起来重叠。

## 移动支持

```cpp
template<typename T>
void swap(T& a, T& b)
{
    T tmp(std::move(a));   // 将 a 的数据移动到 tmp
    a = std::move(b);      // 将 b 的数据移动到 a
    b = std::move(tmp);    // 将 tmp 的数据移动到 b
} // 简单的 std::swap 实现
```

![](img/68a90f505054116271758fb914871a74_236_0.png)

幻灯片上的图是一个 PowerPoint 动画。

`std::move` 定义在 `<utility>` 中。

## 移动支持

在以下情况下最为重要：

- 对象在独立的内存中拥有数据（例如堆）。
- 拷贝是深拷贝。

移动只拷贝对象内存。

- 拷贝拷贝对象内存 + 独立内存。

考虑将 A 拷贝/移动到 B：

![](img/68a90f505054116271758fb914871a74_237_0.png)

移动永远比拷贝慢，而且通常更快。

幻灯片上的图是一个 PowerPoint 动画。上行显示带有和没有独立内存的对象拷贝，下行显示移动此类对象。

## 性能数据

再次考虑这些用例：

`vt = createTVec();` // 返回/赋值

`vt.push_back(T object);` // push_back

拷贝与移动的差异显著：

![](img/68a90f505054116271758fb914871a74_238_0.png)

> 拷贝与移动的差异显著：
>
> Scott Meyers，保留所有权利。
>
> 幻灯片上的图是一个 PowerPoint 动画。上行显示带有和没有独立内存的对象拷贝，下行显示移动此类对象。

## 引用绑定规则

这对重载解析至关重要。

如下：

- 左值（Lvalues）可以绑定到左值引用。
- 右值（Rvalues）可以绑定到常量左值引用。

此外：

- 右值可以绑定到非常量的右值引用。
- 左值不能绑定到右值引用。
- 否则，左值可能会被意外修改。

控制引用绑定的通用规则可见 `[dcl.init.ref]` (N3290 中的 8.5.3)，而规定引用绑定与重载解析之间相互作用的规则可见 `[over.ics.ref]` (N3290 中的 13.3.1.4) 和 `[over.ics.rank]` (N3290 中的 13.3.2)，特别是 13.3.3.2，该规则规定：在左值引用或右值引用之间存在绑定竞争时，右值优先选择 `const T&` 参数，而另一种类型是 `const T&&`，因为右值无法绑定到所有非常量的 `T` 参数，且非常量右值相较于 `const T` 参数，更倾向于绑定到 `T&` 参数，因为后者需要添加 `const`。

在 C++00 曾有一段时期允许左值绑定到右值引用，某些编译器（例如 gcc 4.3 和 4.4（但不是 4.5），VC10 beta（但不是 beta 2 或后续版本））实现了这种行为。这有时被称为“右值引用版本 1”。受 N2818 驱动，规则发生了变化，使得左值不能绑定到右值引用，这有时被称为“右值引用版本 2”。开发者需要注意，某些支持右值引用的旧编译器可能实现“版本 1”而不是版本 2 规则。

## 右值引用

示例：

```cpp
void f1(const TVec&); // 接收常量左值引用
TVec vt;
f1(vt);                 // 正常（如既往）
f1(createTVec());     // 正常（如既往）
```

```cpp
void f2(const TVec&); // #1: 接收常量左值引用
void f2(TVec&&);      // #2: 接收非常量右值引用
f2(vt);               // 左值 => #1
f2(createTVec());   // 均可行，非常量右值 => #2
```

```cpp
void f3(const TVec&); // #1: 接收常量右值引用
void f3(TVec&&);      // #2: 接收非常量右值引用
f3(vt);               // 错误！左值
f3(createTVec());   // 均可行，非常量右值 => #2
```

## 右值引用与 const

C++ 保持了常量正确性（const-correct）：

- 常量左值/右值只绑定到常量引用。

但常量的右值引用本质上是无用的。

- 右值引用为两个特定问题设计：
  - 移动语义
  - 完美转发
- C++0x 语言规则是针对这些需求精心设计的。
- 这些规则中没有考虑常量的右值引用。
- `T&&` 是合法的，但并非设计为有用。
- 使用了已经新兴的 `::`

const 右值引用无用的核心原因在于 `[temp.duct.call]` (N3290 中的 14.8.2.1/3) 对 `T&&` 参数赋予的特殊处理：“如果 P 是指向未限定 const 模板参数的右值引用 [即 T&] 且实参为左值，则在类型推导中使用‘A 的左值引用’ [即 T&] 代替 A。” 这种特殊变通方法仅适用于 `T&` 参数，不适用于 `const T&` 参数。

`const T&` 模板参数的新用途是允许绑定左值同时禁止引用，例如来自 `[function.objects]` (N3290 中的 20.8/2)：

```cpp
template <class T> reference_wrapper<T> ref(T&) noexcept;
template <class T> reference_wrapper<const T> cref(const T&) noexcept;
template <class T> void ref(const T&&) = delete;
template <class T> void cref(const T&&) = delete;
```

## 右值引用与 const

影响：

- 不要声明 `const T&&` 参数。
- 反无论如何你都无法从中移动。
- 因此此写法（来自之前的幻灯片）很少有意义：
  `void f3(const T&&);` // 合法，但很少合理
- 避免创建常量右值。
- 它们无法绑定到 `T&&` 参数。
- 例如，避免使用常量函数返回值：
  - 这是相对于 C++98 的改变。

```cpp
class Rational { ... };

const Rational operator+(const Rational&, // 合法，但
  const Rational&);    // 设计不佳

Rational operator+(const Rational&, // 更好的设计
  const Rational&);
```

## 区分拷贝与移动

重载暴露了“用移动代替拷贝”的机会：

```cpp
class Widget {
public:
    Widget(const Widget&); // 拷贝构造函数
    Widget(Widget&&); // 移动构造函数

    Widget& operator=(const Widget&); // 拷贝赋值
    Widget& operator=(Widget&&); // 移动赋值
};

Widget w;
Widget w1 = w;           // 拷贝
Widget w2 = std::move(w); // 移动
```

## 实现语义

移动操作获取源值，并将源对象留在有效状态：

```cpp
class Widget {
private:
    std::string pds;
public:
    Widget() = default;
    Widget(const Widget& rhs) : pds(rhs.pds) {} // 拷贝
    Widget(Widget&& rhs) : pds(std::move(rhs.pds)) {} // 移动

    Widget& operator=(const Widget& rhs) {
        pds = rhs.pds;
        return *this;
    }
    Widget& operator=(Widget&& rhs) {
        if (this != &rhs) {
            pds = std::move(rhs.pds);
        }
        return *this;
    }
};
```

## 显式移动请求

要对左值（lvalue）请求移动，请使用 `std::move`：

`std::move` 将左值转换为右值（rvalues）。

- 重载规则会完成剩余工作。

本页面的移动赋值运算符没有考虑移动到自身（move-to-self）。



# 为什么用移动而不是转换？

`std::move` 使用隐式类型推导。考虑：

```cpp
template<typename It>
void someAlgorithm(It begin, It end)
{
    // 允许从 *begin 移动到 temp，使用 static_cast 版本
    auto temp1 = static_cast<typename std::iterator_traits<It>::value_type&>(*begin);
    // 相同，C语言风格转换版本
    auto temp2 = (typename std::iterator_traits<It>::value_type&)**begin;
    // 相同，std::move 版本
    auto temp3 = std::move(*begin);
    ...
}
```

你更倾向于输入哪一个？

# 实现 std::move

`std::move` 在概念上非常简单：

```cpp
template<typename T> // 无论传入什么都返回右值
T&                         // 传入的；必须兼容
move(MagicReferenceType obj) // 同时左值/右值
{
    return obj;
}
```

在概念与实现之间存在着奥的语言规则。

# 模板中的引用折叠

在 C++98 中，给定：

```cpp
template<typename T>
void f(T& param);
int x;
f<int&>(x); // T 是 int&
```

f 初始实例化为：

```cpp
void f(int& param); // 引用的引用
```

C++98 的引用折叠规则规定：

- T & ⇒ T&

所以 f 的实例化实际上是：

```cpp
void f(int& param); // 引用折叠后
```

# 模板中的引用折叠

C++0x 的规则考虑了右值引用：

- T& -> T& // 来自 C++98
- T&& -> T& // C++0x 新增
- T& -> T&& // C++0x 新增
- T&& -> T&& // C++0x 新增

总结：

- 涉及 & 的引用折叠始终是 T&。
- 仅涉及 && 的引用折叠是 T&。

这些规则由 [dcl.ref] (8.3.2/6 in N3290) 定义。

# std::move 的返回值

为了保证返回值为右值，`std::move` 执行了如下操作：

```cpp
template<typename T>
typename std::remove_reference<T>::type&
move(MagicReferenceType obj)
{
  return obj;
}
```

- 记住，T& 返回类型将是一个左值！

因此：

```cpp
int x;
std::move<int>(x); // 调用 remove_reference<int>::&& std::move(/*...*/)
// => int&& && std::move(/*...**)
```

- 如果没有 remove_reference，move<int> 将返回 int。

`std::remove_reference` 是 C++0x 类型特质功能的一部分。它将 T 和 T& 类型都转换为 T。

# std::move 的参数类型

必须是非 const 引用，因为我们想要移动它的值。

左值引用是不行的。

- 右值无法绑定到它们：

```cpp
TVec createTVec();           // 如前所示
TVec&&& std::move(TVec& obj); // 可能移动
                                // 实例化
std::move(createTVec());     // 错误！
```

![](img/68a90f505054116271758fb914871a74_259_0.png)

注意本页展示的移动是一个函数，而不是模板。

# std::move 的参数类型

右值引用也不行。

- 左值无法绑定到它们。

```cpp
TVec&&& move(TVec&&); // 可能移动
TVec& vt;
move(vt); // 
```

`std::move` 需要：

- 对于左值参数，参数类型为 T&。
- 对于右值参数，参数类型为 T&&。

注意本页显示移动是一个函数，而不是模板。

# 为什么不直接重载？

重载可以解决问题：

```cpp
template<typename T>
typename std::remove_reference<T>::type& move(T& lvalue) { return static_cast<T&&>(lvalue); }

template<typename T>
typename std::remove_reference<T>::type& move(T&& rvalue) { return static_cast<T&&>(rvalue); }
```

但完美转发问题仍然存在：

- 如何将参数转发到另一个函数？
- 我们需要重载！

针对 `std::move` 和完美转发的右值引用幻灯片假设 C++98/C++03 的模板参数推导不区分左值和右值参数。

# 模板中的 T&& 参数推导

给定：

```cpp
template<typename T>
void f(T& param); // 注意是非 const 右值引用
```

T 的推导类型取决于传入 param 的内容：

- 左值 ⇒ T 是左值引用
- 右值 ⇒ T 是非引用

结合引用折叠：

```cpp
int x;
f(x);                          // 左值：生成 f<int&>(int&)
f(10);                         // 右值：生成 f<int&>(int&)
TVec vt;
f(vt);                         // 左值：生成 f<TVec&>(TVec&)
f(createTVec());               // 右值：生成 f<TVec&>(TVec&)
```

# 实现 std::move

`std::move` 的参数是 T&：

```cpp
template<typename T>
typename std::remove_reference<T>::type&&
move(T& obj)
{
  return obj;
}
```

这几乎是正确的。问题在于：

- obj 是左值（它有一个名字）。
- move 的返回值是右值引用。
- 左值无法绑定到右值引用。

# 实现 std::move

转换消除了问题：

```cpp
template<typename T>
typename std::remove_reference<T>::type&&
move(T& obj)
{
    using ReturnType = typename std::remove_reference<T>::type&&;
    return static_cast<ReturnType>(obj);
}
```

我相信（但未证实）可以通过对自身应用 `decltype` 来避免在体体内重复 `std::move` 的返回类型：

```cpp
template<typename T>
typename std::remove_reference<T>::type&&
move(T& obj)
{
    using ReturnType = decltype(move(obj));
    return static_cast<ReturnType>(obj);
}
```

# 模板中的 T& 参数

注意带有 T& 参数的函数模板需要生成接收 T& 的函数：

```cpp
template<typename T>
void f(T& param);    // 如前所示
int x;
f(x);                        // 仍然调用 f<int>(int&)，即 f(int&)
f(10);                   // 仍然调用 f<int>(int&)，即 f(int&)
TVec vt;
f(vt);                    // 仍然调用 f<TVec&>(TVec&)，即 f(TVec&)
f(createTVec());      // 仍然调用 f<TVec&>(TVec&)，即 f(TVec&)
```

# 模板中的 T& 参数

```cpp
template<typename T>
void f(T& param);    // 接受任何类型：左值或右值，const 或非 const
```

- 左值无法绑定到右值引用，但 param 可以绑定到左值。
- 实例化后，param 的类型可能是 T&。
- 对于完美转发（稍后描述）很重要。

T& 作为“接受任何类型”参数仅适用于模板！

- 对于函数，&& 参数仅绑定到非 const 右值：

```cpp
void f(Widget&& param); // 仅接受非 const 右值
```

# auto&& ≡ T&&

`auto` 类型推导等于模板推导，因此 `auto&&` 变量的类型可能是左值引用：

```cpp
int calcVal();
int x;
auto&& v1 = calcVal(); // 从右值推导类型 -> v1 的类型是 int&&
auto&& v2 = x; // 从左值推导类型 -> v2 的类型是 int&
```

![](img/68a90f505054116271758fb914871a74_267_0.png)

# 移动是拷贝的优化

支持移动的可拷贝类型，移动请求会产生拷贝：

```cpp
class Widget { // 不支持移动的类
public:
    Widget(const Widget&); // 拷贝构造
};
class Gadget { // 支持移动的类
public:
    Gadget(Gadget& rhs) // 移动构造
    : w(std::move(rhs.w)) // 请求移动 w 的值
    { ... }
private:
    Widget w; // 不支持移动
};
```

rhs.w 被拷贝到 w：

* `std::move(rhs.w)` 返回 Widget 类型的右值。
* 该值传递给 Widget 的拷贝构造函数。

对于不可拷贝且不支持移动的类型，移动请求将失败。

# 移动是拷贝的优化

如果 Widget 支持移动：

```cpp
class Widget {
public:
    Widget(const Widget&); // 拷贝构造
    Widget(Widget&&); // 移动构造
}

class Gadget {
public:
    Gadget(Gadget&& rhs) // 如前所示
    : w(std::move(rhs.w)) { ... } // 如前所示
private:
    Widget w;
};
```

rhs.w 现在被移动到 w：

`std::move(rhs.w)` 仍然返回 Widget 类型的右值。

- 该值现在传递给 Widget 的移动构造函数。
- 通过正常的重载解析。

## 移动是拷贝的优化

影响：

- 为类提供移动支持即使对于感知移动的代码也能提高性能。
- 针对右值的拷贝请求可能会静默地变为拷贝。
- 对于没有显式移动支持的类型，移动请求是安全的。
- 这些类型将转执行拷贝。
- 例如，所有内置类型。

简而言之：

- 为类提供移动支持。
- 对于可以安全移动的左值，使用 `std::move`。

![](img/68a90f505054116271758fb914871a74_270_0.png)

移动和拷贝操作都可能抛出异常，移动函数中的异常问题与拷贝函数的问题本质上是相同的。例如，两者都必须至少实现基本保证，但应该记录它们提供的保证；客户端必须考虑此类函数如何抛出异常等。

N2983 建议，泛型（即基于模板的）编码如果希望提供对未知类型 `T` 使用移动操作的强保证，应提供一种条件保证：只有当 `T` 版本的移动操作提供的强（或不抛出）方法对于使用任何未知操作的泛型代码可行时，泛型才提供强保证；然而，这并没有特殊之处。

N2983 还解释了 `std::move_noexcept` 如何在极少数的特殊情况下使用：(1) 提供强保证的遗留代码 (2) 正在被修改以用未知提供保证的移动操作替换拷贝操作。在类型 `T` 的对象上使用 `std::move_noexcept` 就像在对象上使用 `std::move`，除非相关的 `T` 操作已知会抛出异常，否则执行执行拷贝而不是移动。

## 隐式生成的移动操作

移动构造函数和移动赋值运算符是特殊的：

- 由编译器在适当条件下生成。

条件：

- 所有数据成员和基类都是可移动的。
- 隐式移动操作移动所有内容。
- 大多数类型符合条件：
    - 所有内置类型（移动 = 拷贝）。
    - 大多数标准库类型（例如，所有容器）。
- 为了维护类不变性的生成的操作。
- 无用户声明的拷贝或移动操作。
- 自定义语义使得默认语义不适用。
- 移动是拷贝的优化。
- 无用户声明的析构函数。
- 通常表示存在隐式类不变性。

不可移动的库类型是基础设施相关的，例如（引用 Daniel Krüler 在 comp.std.c++ 线程 http://tinyurl.com/3afblwik 中的帖子）“type_info, error_category, 所有异常类, reference_wrapper, 所有来自主分配器模板的特化版本, weak_ptr, enable_shared_from_this, duration, time_point, 我知道的所有迭代器/迭代器适配器，local::facet, locale::id, random_device, seed_seq, ios_base, basic_istream<charT,traits::>::sentry, 所有原子类型, once_flag, 所有互锁类型, lock_guard, 所有条件变量类型。”

## 析构函数与隐式类不变性

```cpp
class Widget {
private:
  std::vector<int> v;
  std::set<double> s;
  std::size_t sizeSum;
public:
  ~Widget() { assert(sizeSum == v.size()+s.size()); };
  ...
};
```

如果 Widget 有隐式生成的移动操作：

```cpp
{
  std::vector<Widget> vw;
  Widget w;
  vw.push_back(std::move(w)); // 将内容放入 w 的容器中
                             // 将 w 移动到 vw
                             // 不再使用 w
  ...
  // 断言触发！
}
```

用户声明的析构函数 => Widget 没有编译器生成的移动操作。

断言将会触发，因为被移动后的 `w` 将拥有空容器（推测），但 `sizeSum` 将继续保持对应容器移动前大小的值。

## 隐式生成的移动操作

示例：

```cpp
class Widget1 { // 可拷贝且可移动类型
private:
    std::u16string name; // 可拷贝/可移动类型
    long long value; // 可拷贝/可移动类型
public:
    explicit Widget1(std::u16string name); // 隐式拷贝/移动构造函数
}; // 隐式拷贝/移动赋值运算符
```

```cpp
class Widget2 {
private:
    std::u16string name; // 可拷贝类型；不可移动
    long long value;
public:
    explicit Widget2(std::u16string name); // 用户声明的拷贝构造函数
    Widget2(const Widget2& rhs); // => 无隐式移动操作
}; // 隐式拷贝赋值运算符
```

## 自定义移动 ⇒ 自定义拷贝

声明移动操作会防止拷贝操作的生成。

- 自定义移动语义 -> 自定义拷贝语义。
- 移动是拷贝的优化。

```cpp
class Widget3 { // 可移动类型；不可拷贝
private:
    std::u16string name;
    long long value;
public:
    explicit Widget3(std::u16string n); // 用户声明的移动构造函数
    Widget3(Widget3&& rhs); // 无隐式拷贝操作
    Widget3& operator=(Widget3&& rhs); // 用户声明的移动赋值运算符
// 无隐式拷贝操作
};
```

## 隐式生成的移动操作（继续）

*实际上，查看 OCR，标题“Implicitly-Generated Move Operations”出现在第 271 页和第 273 页。我将它们视为章节。*

## 隐式生成的移动操作（继续）

*等等，OCR 文本在第 274 页开始“Custom Moving ⇒ Copy Copy”。让我们根据提供的文本进行对齐。*

## 隐式生成的移动操作（等等，让我们重新检查 OCR 流程）

*OCR 的流程是：*

1. 移动是拷贝的优化（第 270 页）
2. 隐式生成的移动操作（第 271 页）



# 移动是拷贝的优化

## 隐式生成的移动操作

## 析构函数与隐式类不变性

## 隐式生成的移动操作

## 自定义移动 ⇒ 自定义拷贝

## 隐式生成的移动操作

---

## 移动是拷贝的优化

简而言之：

- 为类提供移动支持。
- 对于可以安全移动的左值，使用 `std::move`。

## 构造与完美转发

构造函数通常将参数拷贝到数据成员：

```cpp
class Widget {
public:
    Widget(const std::string& n, const std::vector<int>& c)
        : name(n), // 将 n 拷贝到 name
          coordinates(c) // 将 c 拷贝到 coordinates
    ...
private:
    std::string name;
    std::vector<int> coordinates;
};
```

## 构造与完美转发

对于右值参数，移动语义会更优：

```cpp
std::string lookupName(int id);
int widgetID;
```

```cpp
std::vector<int> tempVec; // 仅用于 Widget 构造函数
```

```cpp
Widget w(lookupName(widgetID), // 右值参数，但 Widget
std::move(tempVec)); // 将拷贝到成员
```

为为左值/右值组合重载 `Widget` 构造函数 → 需要 4 个函数。

- 通常情况下，n 个参数需要 2ⁿ 种重载。
- 对于较大的 n 来说是不切行的。
- 对于较小的 n 来说是枯燥/重复/容易出错。

## 构造与完美转发

目标：一个能“做正确的事”的函数；

- 拷贝左值参数，移动右值参数。

解决方案是使用完美转发构造函数：

- 模板构造函数，将 `T&&` 参数转发给成员：

```cpp
class Widget {
public:
    template<typename T1, typename T2>
    Widget(T1&& n, T2&& c)
        : name(std::forward<T1>(n)), // 将 n 转发到 string 构造函数
          coordinates(std::forward<T2>(c)) // 将 c 转发到 vector 构造函数
    ...
private:
    std::string name;
    std::vector<int> coordinates;
};
```

> © 2011 Scott Meyers，保留所有权利。

正如后面的幻灯片所示，它的行为与非模板构造函数并不完全，因为完美转发并不完美。

## 构造之外的完美转发

再次：

- 一个将 `T&&` 参数转发给成员的模板构造函数：

```cpp
class Widget {
public:
    template<typename T1, typename T2>
    Widget(T1&& n, T2&& c)
        : name(std::forward<T1>(n)),      // 将 n 转发到 string 构造函数
          coordinates(std::forward<T2>(c)) // 将 c 转发到 vector 构造函数
{}

private:
    std::string name;
    std::vector<int> coordinates;
};
```

效果：

- 传递给 n 的左值 -> `std::string` 构造函数接收左值。
- 传递给 n 的右值 -> `std::string` 构造函数接收右值。
- c 和 `std::vector` 构造函数同样如此。

## 构造之外的完美转发

不仅用于构造，例如 setter：

```cpp
class Widget {
public:
  // 修改后的
  // 示例
  template<typename T>
  void setName(T&& name) // 转发
  { name = std::forward<T>(name); } // 新
  template<typename T>
  void setCoords(T&& newCoords) // 转发
  { coordinates = std::forward<T>(newCoords); } // newCoords

private:
  std::string name;
  std::vector<int> coordinates;
};
```

正如后面的幻灯片所示，它的行为与非模板 setter 并不完全，因为完美转发并不完美。

## 构造之外的完美转发

尽管使用了 `T&&` 参数，代码仍然是完全类型安全的：

- 类型兼容性在实例化时进行验证。
  - 例如，在 `setName` 中只有与 `std::string` 兼容的类型是有效的。

比带类型的参数更灵活。

- 接受/转发所有兼容的参数类型。
  - 例如，`setName` 接受 `std::string`, `char*`, `const char*`。

## 新 C++ (C++0x) 概览

## 构造之外的完美转发

可以通过 `static_assert` 移除灵活性（稍后描述）：

```cpp
template<typename T>
void setName(T& newName)
{
    static_assert(std::is_same<std::decay<T>::type, std::string>::value,
"T 必须是 [const] std::string");
    name = std::forward<T>(newName);
}
```

对于非数组和非函数类型，`std::decay<T>::type` 等于 `std::remove_cv<std::remove_reference<T>>::type::type`。

`static_assert` 尚未引入。

也可以使用 `std::enable_if`，但在这种情况下 `static_assert` 似乎更简单更清晰。`std::enable_if` 会将 `setName` 从重载集合移除，而 `static_assert` 只有在 `setName` 被选中为调用的重载后才会求值。

## std::forward

再次考虑：

```cpp
template<typename T>
void setName(T& newName)
{ name = std::forward<T>(newName); }
```

- 引用（即 T 是 `T&`）⇒ 传递了左值给 `setName`
  - `std::forward<T>(newName)` 应该返回左值。
- 非引用（即 T 是 `T`）⇒ 传递了右值给 `setName`
  - `std::forward<T>(newName)` 应该返回右值。

## 完美转发

- 仅适用于函数模板。
- 在转发时保留左值/右值属性。

完美转发并不真的完美。有几种类型的参数无法被完美转发，包括但不限于：

- 指针常量 0。
- 函数模板名（例如 `std::endl` 和其他操纵符）。
- 初始化列表。
- 类内初始化的静态成员。
- 位域。

## 默认函数

如果使用，将隐含生成“特殊”成员函数：

- 默认构造函数
  - 仅当没有用户声明的构造函数时。
- 析构函数
- 拷贝操作（拷贝构造函数、拷贝赋值）
  - 仅当未声明移动操作时。
- 移动操作（移动构造函数、移动赋值）
  - 仅当未声明拷贝操作时。

## 默认函数

生成的版本为：

- 公
- Inline
- 非显式

默认函数具有：

- 用户指定的声明以及由编译器生成的实现。

## 默认函数

典型用法：“取消”隐式生成的函数：

```cpp
class Widget {
public:
    Widget(const Widget&);    // 拷贝构造函数阻止了隐式
                                声明的默认构造函数和
                                移动操作

    Widget() = default;         // 默认构造函数，使用
                                默认实现。

    Widget(Widget&&) = default;  // 移动构造函数，使用
                                  默认实现。

    ...
};
```

## 默认函数

或者更改“正常的”访问权限、显式或虚属性：

```cpp
class Widget {
public:
    virtual ~Widget() = default; // 声明为虚
    explicit Widget(const Widget&) = default; // 声明为显式
private:
    Widget& operator=(Widget&&) = default; // 声明为私有
};
```

## delete Functions

被删除的函数已声明，但无法使用。

- 最常见的应用：防止对象拷贝：

```cpp
class Widget {
    Widget(const Widget&) = delete; // 声明并删除
    Widget& operator=(const Widget&) = delete; // 变为不可调用
...
};
```

注意 `Widget` 也是不可移动的。

* 声明拷贝操作会抑制隐式的移动操作！

* 它双向都有效：

```cpp
class Gadget {
    Gadget(Gadget&) = delete; // 这些也被删除
    Gadget& operator=(const Gadget&) = delete; // 抑制拷贝
...
}
```

"delete" 函数不能以任何方式使用：它们不能被调用、不能取地址、不能在 `sizeof` 表达式中使用等。

模板函数可以被删除。例如，`std::reference_wrapper` 就是通过这种方式防止从右值构造的（例如作为 `std::ref` 的返回值）。

虚函数可以被删除，但如果被删除，则该虚函数的所有基类和派生版本也必须被删除。也就是说，要么层级结构中所有的虚函数声明都被删除，要么一个都没有。

## delete Functions

不局限于成员函数。

- 另一个常见应用：控制参数转换。
- 被删除的函数已声明，因此参与重载解析：

```cpp
void f(void*);                          // f 可以用任何指针类型调用
void f(const char*) = delete;      // f 无法用 [const] char* 调用

auto p1 = new std::list<int>();      // p1 的类型为 std::list<int>*
extern char *p2;
...
f(p1);                             // 正常，调用 f(void*)
f(p2);                              // 错误！f(const char*) 不可用
f("Fahrvergnügen");               // 错误！
f(u"Fahrvergnügen");               // 正常(char16_t* != char*)
```

## Default Member Initialization

现在可以为非静态数据成员提供默认初始化：

```cpp
class Widget {
private:
    int x = 5;
    std::string id = defaultID();
};
Widget w1; // w1.x 初始化为 5，
           // w1.id 根据 defaultID 初始化。
```

也允许统一初始化语法：

```cpp
class Widget { // 语义上与上面相同
private:
    int x { 5 }; // 不需要 "="
    std::string id = {defaultID()}; // 但是允许的
};
Widget w2; // 同上
```

默认成员初始化不允许使用直接初始化语法（使用括号）进行默认成员初始化。

默认成员初始化的值可以相互依赖：

```cpp
class Widget {
private:
    int x { 15 };
    int y { 2 * x };
}
```

根据 N2756，任何在成员初始化列表中作为初始化器有效的项，都应该作为默认初始化器是有效的。特别是，非静态成员函数的调用是有效的，例如在 `Widget::id` 的初始化中，`defaultID` 可以是静态成员或非静态成员函数。如果使用了非静态成员函数，可能会出现引用未初始化的数据成员的问题。

静态数据成员的类内初始化继续仅对具有静态初始化器的 `const` 对象有效（即类内动态初始化是无效的）。然而，在 C++0x 中，“字面量”——而不是整数类型——也可以这样初始化。（字面量类型定义在 [basic.types] (N3290 中的 3.9/10)。

## Default Member Initialization

构造函数初始化列表会覆盖默认值：

```cpp
class Widget {
public:
    Widget() = default;
    explicit Widget(int xVal) : x(xVal) {}
private:
    int x = 5;
    std::string id = defaultID();
};
```

Widget w3; // w3.x == 5, w3.id == defaultID()

Widget w4(-99); // w4.x == -99, w4.id == defaultID()

默认成员初始化在初始化独立于调用的构造函数时最有用。

- 消除构造函数中冗余初始化代码。

使用默认成员初始化会导致类/结构变为非聚合体，因此：

```cpp
struct Widget {
    int x = 5;
}
```

```cpp
Widget w { 10 }; // 错误！尝试调用接受 int 的构造函数，
// 但 Widget 没有这样的构造函数
```

## Delegating Constructors

考虑一个具有多个构造函数的类：

```cpp
class Base {
public:
    explicit Base(int);
    ...
};
class Widget : public Base { // 4 个构造函数
public:
    Widget();
    explicit Widget(double fl);
    explicit Widget(int sz);
    Widget(const Widget& w);
private:
    static int calcBaseVal();
    static const double defaultFlex = 1.5;
    const int size;
    long double flex;
```

Java 有委托构造函数。

在本示例及随后的示例中，`Base` 的构造函数是 `explicit` 的，仅是为了展示良好的默认风格。没有任何示例依赖于它。

## Delegating Constructors

通常，实现包含冗余：

```cpp
Widget::Widget()
  : Base(calcBaseVal()), size(0), flex(defaultFlex)
{}

Widget::Widget(double fl)
  : Base(calcBaseVal()), size(0), flex(defaultFlex)
{}

Widget::Widget(int sz)
  : Base(calcBaseVal()), size(sz), flex(defaultFlex)
{}

Widget::Widget(const Widget& w)
  : Base(calcBaseVal()), size(0), flex(defaultFlex)
{}
```

（注：此部分的原文文本碎片化，根据标准 C++ 委托构造函数模式进行了重建）。

## Delegating Constructors

委托与构造函数的特征无关。

- 委托者和被委托者各自可以是 `inline`、`explicit`、`public`/`private` 等。
- 被委托者本身也可以进行委托。
- 委托者的代码体在返回时执行：

```cpp
class Widget: public Base {
public:
    Widget(const Widget& w): Widget(w.size, w.flex)
    {
        makeLogEntry("Widget constructor");
    }
    ...
private:
    Widget(int sz, double fl); // 如前
    ...
};
```



## 继承构造函数

现在可以使用 `using` 配合基类构造函数：

```cpp
class Base {
public:
    explicit Base(int);
    void f(int);
}
class Derived : public Base {
public:
    using Base::f; // C++98 和 C++0x 均有效
    using Base::Base; // 仅 C++0x 有效；会导致隐式
                     // 声明 Derived(int);

    void f(); // 重载继承的 Base::f
    Derived(int x, int y); // 重载继承的 Base::f 构造函数
}
Derived d1(44); // C++0x 中由于构造函数继承而有效
Derived d2(5, 10); // 正常使用 Derived::Derived(int, int)
```

### 继承构造函数的风险

将构造函数继承到带有数据成员的类是有风险的：

```cpp
class Base {
  public:
    explicit Base(int);
};
class Derived : public Base {
  public:
    using Base::Base;
  private:
    std::u16string name;
    int x, y;
};
```

```cpp
Derived d(10);
// 可以编译，但 d.name 被
// 默认初始化，且
// d.x 和 d.y 未初始化
```

说 `Derived::x` 和 `Derived::y` 未初始化并不完全准确。相反，它们被处理为未在继承构造函数的成员初始化列表中提及。如果 `Derived` 对象具有静态或线程存储生存期，则其 x 和 y 数据成员将被初始化为零。

### 使用默认成员初始化缓解风险

默认成员初始化可以缓解这种风险：

```cpp
class Base { ... }; // 如前所示
class Derived: public Base {
public:
    using Base::Base;
private:
    std::string name = "Uninitialized";
    int x = 0, y = 0;
};
Derived d(10); // d.name == "Uninitialized",
// d.x == d.y == 0
```

## 类作者特性总结

- 右值引用促进了移动语义和完美转发。
- `default` 为用户声明的特殊函数产生默认函数体。
- `delete` 使声明的函数不可用。
- 所有数据成员都可以有默认初始化值。
- 委托构造函数调用其他构造函数。
- 继承的构造函数来自基类。

## 概述

- 引言
- 适用于所有人的特性
- 库增强
- 类作者特性
- 库作者特性
- 更多特性
- 进一步信息

## 静态断言

当编译时测试失败时生成用户定义的诊断：

```cpp
static_assert(sizeof(void)==sizeof(long),
    "指针和长整型的大小不同");
```

在任何声明的地方均有效：

- 全局/命名空间作用域。
- 类作用域。
- 函数/块作用域。

### 模板中的应用

在模板中特别有用：

```cpp
template<typename T>
void f(const T& obj)
{
    static_assert(std::is_base_of<Widget,T>::value,
                  "T 没有继承自 Widget");
    ...
}
template<short val>
class Gadget {
    static_assert(1 <= val && val <= 10,
                  "val 超出范围（必须是1-10)");
    ...
};
```

### 诊断信息的字符串类型

诊断信息可以是任何类型的字符串字面量：

```cpp
static_assert(CHAR_BIT == 8,                 // 普通字符
                "chars没有8位比特 \u2620"); // 字符串
```

```cpp
static_assert(CHAR_BIT == 8,                 // 宽字符串
                L"chars没有8位比特 \u2620");
```

```cpp
static_assert(CHAR_BIT == 8,                 // UTF-8
                u8"chars没有8位比特 \u2620");
```

```cpp
static_assert(CHAR_BIT == 8,                 // UTF-16
                u16"chars没有8位比特 \u2620");
```

```cpp
static_assert(CHAR_BIT == 8,                 // UTF-32
                u32"chars没有8位比特 \u2620");
```

原始字符串字面量也是有效的。

代码点 2620 是骷髅交叉骨头符号 (`\u2620`)。

当通过转义序列指定的代码点是窄字符串字面量的一部分（例如本页上的第一个示例）时，生成的字符串包含该代码点所需的字节数。因此，表示 `\u2620` 需要 2 个字节，那么 2 个字节将作为窄字符串字面量的一部分包含。

某些 `static_assert` 条件是自言自语的，可能希望将其作为诊断信息，即将条件本身作为默认信息。这种行为可以通过合适的宏提供：

```cpp
#define STATIC_ASSERT(condition) static_assert(condition, #condition)
```

## 显式转换函数

`explicit` 现在适用于转换函数：

```cpp
class Widget {
public:
    explicit Widget(int i); // C++98 和 C++0x
    ...
    explicit operator std::string() const; // 仅限 C++0x
};
```

行为类似于构造函数：

```cpp
void fw(const Widget& w);
int i;

fw(i); // 错误！
fw(static_cast<Widget>(i)); // 可以
void fs(const std::string& s);
Widget w;
...
fs(w); // 错误！
fs(static_cast<std::string>(w)); // 可以
```

此幻灯片展示了 `static_cast` 的用法，但其他转换语法（即 C 风格和函数风格）的行为将相同。

### `explicit operator bool` 的特殊处理

`explicit operator bool` 函数被特殊对待。

- 当“安全”时允许隐式使用（即在“安全”的环境文中）

```cpp
template<typename T>
class SmartPtr {
public:
    ...
    explicit operator bool() const;
};
SmartPtr<int> p;
if (p) // 错误
```

此幻灯片展示了 `static_cast` 的用法，但其他转换语法（即 C 风格和函数风格）的行为将相同。

## 可变模板

两种类型：

- 模板：持有可变参数。
- 函数：持有对应的参数。

```cpp
template<typename... Types> // 模板参数
class tuple;

template<class T, class... Args> // 函数参数
shared_ptr<T>(Args... params);
```

### 参数包

基于“第一个”“剩余”的操作：

- 主要操作是通过 `...` 进行解包

```cpp
template<typename... Types>
struct Count;
template<typename T, typename... Rest>
...
```

`Count` 纯粹是一个练习；C++0x 的 `sizeof...` 执行相同的操作：

```cpp
template<typename... Types>
struct VerifyCount{
    static_assert(Count<Types...>::value == sizeof...(Types),
    "Count<T>::value != sizeof...(T)");
};
```

### 变参数函数模板

示例：任意对象的类型安全打印：

```cpp
void print() { std::cout << '\n'; }; // 打印 0 个对象
template<typename T,
    typename... TRest> // 第1个对象的类型
void print(const T& obj,   // 其他对象的类型
           const TRest&... rest) // 打印第1个对象
{
    std::cout << obj << " "; // 打印剩余对象
    print(rest..);
} // 打印剩余对象

double p = 3.14;
std::string s("Vari");
print(-22, p, &p, s, "adic"); // -22 3.14 0x22ff40 Vari adic
```

- Gregor Järvi 的文章展示了一个经过编译时检查的 printf。
- 确保格式字符串与传递的参数一致。

此示例通过 `const T&` 传递所有参数，但使用完美转发（perfect forwarding）可能是更好的方法。

### 解包模式

解包使用了被解包表达式的模式：

```cpp
template<class T, class... Args>
shared_ptr<T> // 为每个元素加上 "&&"
    make_shared(Args&&... params);    // 解包元素.
template<typename T, typename... TRest> // 加上 "const" 和
    void print(const T& obj, const TRest&... rest) // 为每个元素加上 "&&"
{
    std::cout << obj << " ";
    print(rest...);
}
// 为每个元素的名字不添加任何内容
```

对 print 的调用展开为：

print(rest1, rest2, ..., restn);

省略号（ellipsis）始终位于模式的末尾。

### 解包模式示例 2

```cpp
template<typename T> // 返回一个 归一化的
T normalize(T& obj); // obj 的拷贝
template<typename F, typename... PTypes>
void normalizedCall(F func,
    PTypes&... params) // 同上
{
    func(normalize(params...));   // 对每个解包
// 元素调用 normalize
}
```

对 func 的调用展开为：

```
func(normalize(params₁), normalize(params₂), ..., normalize(paramsₙ));
```

## 变参数类模板

TMP（模板元编程）的基础。示例包括：

- 类型计算：
  - `<type_traits>` 拥有模板结构体 `<class... T> struct common_type;`
- 对象结构生成：
  - `std::tuple<T1, T2, ..., Tn>` 需要 n 个字段，每个字段的类型都正确。
  - `std::tuple<T1, T2, ..., Tn>` 继承自 `std::tuple<T2, T3, ..., Tn>`

给定一个类型列表，`std::common_type` 返回列表中的类型，列表中的所有类型都可以转换为该类型。如果没有这样的类型，或者存在多个这样的类型，代码将无法编译。对于内建类型，按照其通常顺序应用标准的提升和转换规则，例如 `std::common_type<int, double>::type` 是 `double`，因为 int->double 优于 double->int，尽管二者都是可能的。

### `std::tuple` 的草图

```cpp
template <class... Types> // 声明主模板
class tuple:
template<> class tuple<>; // 用于空元组
template<typename T, typename... TRest> // 带有数据成员的类
class tuple<T, TRest...> { // 用于包中的第一个 T // 继承自 // 包的剩余部分
private:
    tuple<TRest... > { // 类型为 T 的数据成员
    T data;
public:
    tuple() : data() {}; // 默认构造函数；所有类型必须是可以默认构造的 // 非默认构造函数。
...
};
```

在成员初始化行上执行 `data()` 可以确保内建类型初始化为零（指针为空）。

Douglas Gregor 和 Jaakko Järvi 发表的实现（见更多信息部分）将其声明为 `protected` 但没有给出理由，而真实的实现（例如 VC 10, gcc 4.5）将其声明为 `private`。因此我使用了 `private`。

### 生成的层次结构

`std::tuple<int, char, std::string> t;`

![](img/68a90f505054116271758fb914871a74_323_0.png)

data 是 `private` 的这一事实引发了关于 `std::get` 如何实现的问题。在示例未列出的 tuple 成员函数中，有一个返回 data 引用的公共函数。在 Gregor 和 Järvi 的实现中，该函数被称为 `head`。对 `tuple<T, TRest...>` 使用 `std::get<n>` 会递归地向上遍历 TRest，每层减少 n 直到 0。然后它返回该类的 `head` 结果。

## decltype

产生表达式的类型而不对其值。

```cpp
int x, *ptr;
decltype(x) i1;               // i1 的类型是 int
decltype(ptr) p1;             // p1 的类型是 int*
std::size_t sz = sizeof(decltype(ptr[44])); // sz = sizeof(
```

这非常直观，但某些奇怪的情况，例如括号可能会产生影响：

```cpp
struct S { double d; };
const S* p;
...
decltype(p->d) x1;         // double
decltype((p->d)) x2;        // const&
```

- 奇怪的情况很少相关（当需要时可以查看)。

### 主要用途：依赖参数类型的模板返回类型

- 转发模板：

```cpp
template<typename F, typename... Ts> // logAndInvoke
auto logAndInvoke(std::ostream& os, // 返回什么
F& func, Ts&... args) -> // func(args...) 执行。
decltype(func(args...)) // 不正确
os << std::chrono::system_clock::now(); // 来自时间库
return func(args...); // 不正确
```

- 数学数学库：

```cpp
template<typename T1, typename T2> // mult 的返回类型
auto mult(T1& a, T2&& b) -> // 与 a*b 相同
decltype(func(args...)) // 不正确
os << std::chrono::system_clock::now(); // 来自时间库
return func(args...); // 不正确
```

data 是 `private` 的这一事实引发了关于 `std::get` 如何实现的问题。在未列出的 tuple 成员函数中，有一个返回 data 引用的公共函数。在 Gregor 和 Järvi 的实现中，该函数被称为 `head`。对 `tuple<T, TRest...>` 使用 `std::get<n>` 会递归地向上遍历 TRest，每层减少 n 直到 0。然后它返回该类的 `head` 结果。

（注：此处原文存在大量重复内容，已按要求不重复输出）



# TMP（模板元编程）的基础

示例包括：

- **类型计算**：
  - `<type_traits>` 拥有模板结构体 `struct common_type<class... T>;`

- **对象结构生成**：
  - `std::tuple<T1, T2, ..., Tn>` 需要 n 个字段，每个字段的类型都正确。
  - `std::tuple<T1, T2, ..., Tn>` 继承自 `std::tuple<T2, T3, ..., Tn>`

给定一个类型列表，`std::common_type` 返回列表中的类型，列表中的所有类型都可以转换为该类型。如果没有这样的类型，或者存在多个这样的类型，代码将无法编译。对于内建类型，按照其通常顺序应用标准的提升和转换规则，例如 `std::common_type<int, double>::type` 是 `double`，因为 `int->double` 优于 `double->int`，尽管二者都是可能的。

# std::tuple 的草图

```cpp
template <class... Types> // 声明主模板
class tuple;

template<> class tuple<>; // 用于空元组

template<typename T, typename... TRest> // 带有数据成员的类
class tuple<T, TRest...> { // 用于包中的第一个 T // 继承自 // 包的剩余部分
private:
    tuple<TRest...> base; // 类型为 T 的数据成员
    T data;
public:
    tuple() : data() {}; // 默认构造函数；所有类型必须是可以默认构造的 // 非默认构造函数。
    ...
};
```

在成员初始化行上执行 `data()` 可以确保内建类型初始化为零（指针为空）。

Douglas Gregor 和 Jaakko Järvi 发表的实现（见更多信息部分）将其声明为 `protected` 但没有给出理由，而真实的实现（例如 VC 10, gcc 4.5）将其声明为 `private`。因此我使用了 `private`。

# 生成的层次结构

`std::tuple<int, char, std::string> t;`

![](img/68a90f505054116271758fb914871a74_323_0.png)

`data` 是 `private` 的这一事实引发了关于 `std::get` 如何实现的问题。在示例未列出的 tuple 成员函数中，有一个返回 `data` 引用的公共函数。在 Gregor 和 Järvi 的实现中，该函数被称为 `head`。对 `tuple<T, TRest...>` 使用 `std::get<n>` 会递归地向上遍历 `TRest`，每层减少 `n` 直到 0。然后它返回该类的 `head` 结果。

# decltype

产生表达式的类型而不对其值。

```cpp
int x, *ptr;
decltype(x) i1;               // i1 的类型是 int
decltype(ptr) p1;             // p1 的类型是 int*
std::size_t sz = sizeof(decltype(ptr[44])); // sz = sizeof(
```

这非常直观，但某些奇怪的情况，例如括号可能会产生影响：

```cpp
struct S { double d; };
const S* p;
...
decltype(p->d) x1;         // double
decltype((p->d)) x2;        // const&
```

# 解包模式

```cpp
template<typename T> // 返回一个归一化的
T normalize(T& obj); // obj 的拷贝

template<typename F, typename... PTypes>
void normalizedCall(F func, PTypes&... params) // 同上
{
    func(normalize(params)...);   // 对每个解包元素调用 normalize
}
```

对 `func` 的调用展开为：

```
func(normalize(params₁), normalize(params₂), ..., normalize(paramsₙ));
```

# 变参数类模板

TMP（模板元编程）的基础。示例包括：

- **类型计算**：
  - `<type_traits>` 拥有模板结构体 `struct common_type<class... T>;`

- **对象结构生成**：
  - `std::tuple<T1, T2, ..., Tn>` 需要 n 个字段，每个字段的类型都正确。
  - `std::tuple<T1, T2, ..., Tn>` 继承自 `std::tuple<T2, T3, ..., Tn>`

给定一个类型列表，`std::common_type` 返回列表中的类型，列表中的所有类型都可以转换为该类型。如果没有这样的类型，或者存在多个这样的类型，代码将无法编译。对于内建类型，按照其通常顺序应用标准的提升和转换规则，例如 `std::common_type<int, double>::type` 是 `double`，因为 `int->double` 优于 `double->int`，尽管二者都是可能的。

# std::tuple 的草图

```cpp
template <class... Types> // 声明主模板
class tuple;

template<> class tuple<>; // 用于空元组

template<typename T, typename... TRest> // 带有数据成员的类
class tuple<T, TRest...> { // 用于包中的第一个 T // 继承自 // 包的剩余部分
private:
    tuple<TRest...> base; // 类型为 T 的数据成员
    T data;
public:
    tuple() : data() {}; // 默认构造函数；所有类型必须是可以默认构造的 // 非默认构造函数。
    ...
};
```

在成员初始化行上执行 `data()` 可以确保内建类型初始化为零（指针为空）。

Douglas Gregor 和 Jaakko Järvi 发表的实现（见更多信息部分）将其声明为 `protected` 但没有给出理由，而真实的实现（例如 VC 10, gcc 4.5）将其声明为 `private`。因此我使用了 `private`。

# 生成的层次结构

`std::tuple<int, char, std::string> t;`

![](img/68a90f505054116271758fb914871a74_323_0.png)

`data` 是 `private` 的这一事实引发了关于 `std::get` 如何实现的问题。在示例未列出的 tuple 成员函数中，有一个返回 `data` 引用的公共函数。在 Gregor 和 Järvi 的实现中，该函数被称为 `head`。对 `tuple<T, TRest...>` 使用 `std::get<n>` 会递归地向上遍历 `TRest`，每层减少 `n` 直到 0。然后它返回该类的 `head` 结果。

# decltype

产生表达式的类型而不对其值。

```cpp
int x, *ptr;
decltype(x) i1;               // i1 的类型是 int
decltype(ptr) p1;             // p1 的类型是 int*
std::size_t sz = sizeof(decltype(ptr[44])); // sz = sizeof(
```

## 概述

- 介绍
- 适合所有人的特性
- 库的增强
- 类作者的特性
- 库作者的特性
- 更多特性
- 更多信息

## 更多 C++0x 特性

- **枚举增强**：
  - 前向声明
  - 指定底层类型
  - 枚举成员作用域限定于枚举内
  - 不允许隐式转换为 `int`

- **无限制的联合体**（成员可以是任何非引用类型）。

- **时间库支持**：时钟、持续时间、时间点。

- 允许将局部类型作为模板参数。

- 与 C99 兼容性，例如 `long long`、`__func__` 等。

- 内联命名空间方便了库的版本管理。

- 作用域分配器允许容器及其元素使用不同的分配器，例如 `vector<string>`。

时间库的主要动力是能够为并发 API 指定超时（例如睡眠持续时间、获取锁的超时等）。

## 更多的 C++0x 特性

- 通用常数表达式 (`constexpr`)。
- 用户自定义字面量（例如 `10_km`、`30_sec`）。
- 放宽的 POD 类型定义；新的标准布局类型。
- 用于控制隐式模板实例化的 `extern` 外部模板。
- `sizeof` 仅适用于类数据成员（例如 `sizeof(C::m)`）。
- `&` 和 `&&` 成员函数。
- 放宽类内初始化静态数据数据的规则。
- 用于对齐控制和限制虚函数重载的上下文关键字。
- 属性（Attributes）表示特殊的优化机会，并为特定平台的扩展提供了标准语法。

## 已移除和废用的特性

- `auto` 作为存储类说明已被移除。
- `export` 作为语言特性已被移除。
- `export` 仍然是一个关键字（但无语义）。
- `register` 作为存储类说明已废用。
- 异常规范已废用。
- `noexcept` 在概念上替换了 `"throw()"` 指定。
- `auto_ptr` 已废用（请改用 `unique_ptr`）。
- `bind1st/bind2nd` 已废用（请改用 `bind` 或 lambda 表达式）。

如果异常尝试传播到 `noexcept(true)` 函数之外，将调用 `terminate`。这与 C++03 中违反 `"throw()"` 指定时发生的情况不同。在那种情况下，在栈解绑后会调用 `unexpected`。

来自 Herb Sutter 2010 年 12 月 8 日的博客文章：“行程报告：2010 年 11 月 C++ 标准会议；‘析构函数和 delete 运算符默认为 noexcept’……简而言之，除非成员或基类析构函数为 `noexcept(false)`，否则每个析构函数默认都是 `noexcept`；你当然仍然可以显式覆盖默认并在任何析构函数中使用 `noexcept(false)`。”

Herb Sutter 认为 `noexcept` 相比 `throw()` 的主要优势是它为编译器提供了额外的优化机会。根据 2010 年 3 月 30 日的 comp.std.cpp 帖子：“`noexcept` 不仅允许调用者进行优化，也允许调用者进行优化，因此优化器可以假设在 `noexcept` 函数中调用且未被 `try/catch` 包的函数本身也是 `noexcept` 的（例如，C 标准库函数并未此类标注）。”

## 概述

- 介绍
- 适合所有人的特性
- 库的增强
- 类作者的特性
- 库作者的特性
- 更多特性
- 更多信息

## 更多信息

C++0x 的 FDIS（特性草案）：

- 编程语言 — C++, Pete Becker (Ed.), 2011-04-11, [http://www.open-std.org/jjtc1/sc22/wg21/docs/papers/2011/n3290.pdf](http://www.open-std.org/jjtc1/sc22/wg21/docs/papers/2011/n3290.pdf)。

关于 C++0x：

- “C++0x”，Wikipedia。
- C++0x - 下一个 ISO C++ 标准，Bjarne Stroustrup, [http://www.research.att.com/~bs/C++0xFAQ.html](http://www.research.att.com/~bs/C++0xFAQ.html)。
- “C++0X: 标准 C++ 的新面貌，”Danny Kalev, informit.com, [http://www.informit.com/guide/content.aspx?g=cplusplus&seqNum216](http://www.informit.com/guide/content.aspx?g=cplusplus&seqNum216)。
- 点击“Guide Contents”（目录），滚动到 C++0X 章节，选择主题。

本节列出的许多来源没有 URL，因为通过搜索引擎很容易找到。我发布的 URL 越少，当目标网站重组结构时失效的链接就越少。

## 更多信息

关于 C++0x：

- “C++0x with Scott Meyers，”Software Engineering Radio (音频), 2010 年 4 月 5 日。
- “即将到来的 C++ (C++0x) 标准概述，”Matt Austen and Lawrence Crowl, Google Tech Talk (视频), 2008 年 10 月 31 日。
- “概述：C++ 迎来大修，”Danny Kalev, DevX.com, 2008 年 8 月 18 日。
- “C++0x 语言特性清单，”VC10 Slow Chat, CodeGuru.com, 2008 年 12 月, [http://www.codeguru.com/forum/showthread?t=4668939](http://www.codeguru.com/forum/showthread?t=4668939)。
  - 讨论了 VC10 对 C++0x 的支持。
- “关于 nullptr 你想的一切，”Stefan T. Lavave, Channel 9 (视频), 2009 年 10 月 19 日。
  - 也讨论了 NULL、make_shared、完美转发、auto。

## 更多信息

关于 C++0x：

- “C++ 中标准库的更改，”Merkle, 2009 年 1 月 12 日。
- “关于 C++0x，”Danny Kalev, DevX.com, 2008 年 8 月 15 日。
- “Scott Meyers 与 C++0x，”Software Engineering Radio, 2010 年 4 月 5 日。
- “C++0x 的通用概述，”Danny Kalev, DevX.com, 2008 年 8 月 15 日。
- “Scott Meyers 与 C++0x，”Software Engineering Radio, 2010 年 4 月 5 日。
- “即将到来的 C++ (C++0x) 标准，”Matt Austen and Lawrence Crowl, Google Tech Talk (视频), 2008 年 10 月 31 日。
- “C++ 迎来大修，”Danny Kalev, DevX.com, 2008 年 8 月 18 日。
- “C++0x 语言特性清单，”VC10 Slow Chat, CodeGuru.com, 2008 年 12 月, [http://www.codeguru.com/forum/showthread?t=4668939](http://www.codeguru.com/forum/showthread?t=4668939)。
  - 讨论了 VC10 对 C++0x 的支持。
- “关于 nullptr 你想的一切，”Stefan T. Lavave, Channel 9 (视频), 2009 年 10 月 19 日。
  - 也讨论了 NULL、make_shared、完美转发、auto。

## 更多信息

auto:

- “Lambdas, auto, and static_assert: C++0x Features in VC10, Part 1，”Stephan T. Lavave, Visual C++ Blog, 2008 年 10 月 28 日。
- “Designing Multreaded Programs in C++，”Anthony Williams, ACCU 2009, 2009 年 4 月 28 日。
  - ➡ 演示幻灯片。
- “Concurrency in the Real World，”Anthony Williams, ACCU 2010, 2010 年 4 月 14 日。
  - ➡ 演示幻灯片。

## 更多信息

统一初始化：

- “Uniform Initialization，”Danny Kalev, DevX.com, 2008 年 11 月 13 日。
- “Uniform Initialization，”Bjarne Stroustrup, Google Tech Talk (视频), 2007 年 2 月 21 日。
- “Sequence Adds to Your Classes，”Danny Kalev, DevX.com, 2009 年 3 月 13 日。

## 新 C++ (C++0x) 概述

Lambda 表达式：

- “Lambda Functions are Ready for Prime Time，”Danny Kalev, DevX.com, 2009 年 1 月 16 日。
- “Lambdas, auto, and static_assert: C++0x Features in VC10, Part 1，”Stephan T. Lavave, Visual C++ Blog, 2008 年 10 月 28 日。
- “Lambdas, everywhere，”Herb Sutter, PDC10, 2010 年 10 月 29 日。
  - ➡ 展示了多种（某些非常非常规的）使用 lambda 方法。

并发：

- 《C++ Concurrency in Action》，Anthony Williams, Manning Publications, 2011 夏季（预计）。



- 草稿版见：<http://www.manning.com/williams/>。

- “Simpler Multithreading in C++0x，”Anthony Williams, DevEx.com, 2007 年 12 月 13 日。

- “Just Software Solutions Blog，”Anthony Williams, <http://www.justsoftwaresolutions.co.uk/blog/>。

  包含了多个“C++0x 多线程”教程帖子。

- “Broken promises – C++0x futures，”Bartosz Milewski, Bartosz Milewski’s Programming Café, 2009 年 3 月 3 日。

- “Thanks for Not Sharing, Or, How to Define Thread-Local Data，”Danny Kalev, DevX.com, 2008 年 3 月 13 日。

并发：

- “Concurrency C++ Threads Right，”Hans Boehm, Google Tech Talk (视频), 2007 年 12 月 12 日。

- “Designing Multithreaded Programs in C++，”Anthony Williams, ACCU 2009, 2009 年 4 月 28 日。

  ➡ 演示幻灯片。

- “Concurrency in the Real World，”Anthony Williams, ACCU 2010, 2010 年 4 月 14 日。

  ➡ 演示幻灯片。

# 更多信息

## TR1 概览：

- Scott Meyers 的 TR1 信息页，<http://www.aristeia.com/EC3E/TR1_info.html>。

- 包含提案文档的链接。

- 《C++ Standard Library Extensions》，Pete Becker, Addison-Wesley, 2007, ISBN 0-321-41299-0。

- TR1 的全面参考指南。

- “The Technical Report on C++ Library Extensions，”Matthew H. Austern, Dr. Dobb’s Journal, 2005年6月。

- “The New C++ Not-So-Standard Library，”Pete Becker, C/C++ Users Journal, 2005年6月。

## Boost:

- Boost C++ Libraries，<http://www.boost.org/>

# 更多信息

## `shared_ptr` 和 `weak_ptr` (TR1 版本):

- “Bad Pointers,” Pete Becker, C/C++ Users Journal, 2005年9月。

- “More Bad Pointers,” Pete Becker, C/C++ Users Journal, 2005年10月。

- “Weak Pointers，” Pete Becker, C/C++ Users Journal, 2005年11月。

- 《Effective C++, 第三版》，Scott Meyers, Addison-Wesley, 2005。

  - 描述了 `tr1::shared_ptr` 并在全书中使用它。

  - 附有目录（TOC）。

- Smart Pointer Timings，<http://www.boost.org/libs/smart_ptr/smarttests.htm>。

  - 比较了 5 种实现的性能。

# 更多信息

## `unique_ptr`:

- “Who’s the Smartest of ‘Em All? Get to Know `std::unique_ptr`，”Danny Kalev, DevX.com, 2008年9月11日。

## 指针容器 (Pointer containers):

- 不在 C++0x 中。智能指针容器的替代方案。

- Boost.PointerContainer 文档，Thorsten Ottosen, <http://www.boost.org/libs/ptr_container/>。

- “Pointer Containers，”Thorsten Ottosen, Dr. Dobbs Journal, 2005年10月。

# 更多信息

## 哈希表 (`unordered_containers`) (TR1 版本):

- “STL and TR1: Part III，”Pete Becker, C/C++ Users Journal, 2006年2月。

- “Hash Tables for the Standard Library，”Matt Austern, C/C++ Journal Experts Forum, 2002年4月。

## 正则表达式 (`regex`) (TR1 版本):

- “Regular Expressions，”Pete Becker, Dr. Dobb’s Journal, 2006。

- “A TR1 Tutorial: Regular Expressions，”Marius Bancila, CodeGuru.com, 2008年7月2日。

- Boost.RegEx 文档，John Maddock, <http://www.boost.org/libs/regex/doc/index.html>。

  - 描述了 Boost 的 RE 库，TR1 正基于此库。

# 更多信息

## 元组 (Tuples) (TR1 版本):

- “The Header `<tuple>` ” Pete Becker, C/C++ Users Journal, 2005年7月。

- “GCC C++0x Features Exploration，”Dean Michael Berris, C++ Soupl!, 2009年3月15日。

  - 展示了 `tuple` 的用法。

## 固定大小数组 (`array`):

- “`std::array`: The Secure, Convenient Option for Fixed-Sized Sequences，”Danny Kalev, DevX.com, 2009年6月11日。

- “STL and TR1: Part II，”Pete Becker, C/C++ Users Journal, 2006年1月。

# 更多信息

## 泛化函数指针 (`function`) (TR1 版本):

- “Generalized Function Pointers，”Herb Sutter, C/C++ Users Journal, 2003年8月。

- “Generalizing Observer，”Herb Sutter, C/C++ Users Journal Experts Forum, 2003年9月。

- 《Effective C++, 第三版》，Scott Meyers, Addison-Wesley, 2005。

- Item 35 解释并演示了 `tr1::function` 的用法。

- 附有目录（TOC）。

## 从 TR1 到 C++00x:

- “Improvements to TR1’s Facility for Random Number Generation，”Walter E. Brown 等人., 2006年2月23日，<http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n1933.pdf>。

# 更多信息

## 右值引用和移动语义 (Rvalue References and Move Semantics):

- “A Brief Introduction to Rvalue References，”Howard E. Hinnant 等, The C++ Source, 2008年3月10日。

  - 细节有些过时。

- C++ Rvalue References Explained，Thomas Becker, 2009年6月，<http://thbecker.net/articles/value_references/section_01.html>。

  - 对 `std::move`、`std::forward` 实现的良好解释。

- “Rvalue References: C++0x Features in VC10, Part 2，”Stephan T. Lavavej, Visual C++ Team Blog, 2009年2月3日。

- “GCC C++0x Features，”Dean Michael Berr, C++ Soup!。

- “Howard's STL / Move Semantics，”Howard Hinnant, C++Next, 2010年10月13日。

- 使用 gcc 4.0.1 对 `std::vector` 进行移动加速。

  - 针对新版本编译器的读者评论数据。

# 更多信息

## 右值引用和移动语义 (Rvalue References and Move Semantics):

- “Making Your Next Move，”Dave, C++Next, 2009年9月17日。

- “Your Next Assignment...” Dave Abhams, C++Next, 2009年9月28日。

  - 关于 `operator=` 的正确性和性能问题。

- “Exceptionally Moving!” Dave Abhams, C++Next, 2009年10月5日。

  - 移动操作的异常安全性。

- “To move or not move，”Bjarne Stroustrup, C++ 标准委员会, 2010年。

  - 描述了隐式移动的规则。

- “Class invariants and implicit move，”comp.lang++ 始于8月14日。

# 更多信息

## 完美转发 (Perfect Forwarding):

- “Onward, Forwarding，”Dave, C++Next, 2009年12月7日。

- “Perfect Forwarding Cases，”comp.std++ 始于2010年1月16日。

  - 讨论了可以转发的类型。

# 更多信息

## 显式转换函数 (Explicit functions):

- “Use Explicit Functions to Avert Reckless Conversions，”Danny Kalev, DevX.com, 2008年10月9日。

## 变参模板 (Variadic Templates):

- “Variadic Templates for C++x，”Douglas Gregor and Jaakko Järvi, Journal of Object Technology, 2008年2月。

- “An Introduction to Variadic Templates in C++x，”Anthony Williams, DevX.com, 2009年4月24日。

- “Variadic Templates，”BoostCon, <http://tinyurl.com/mt66>。

# 更多信息

## `decltype`:

- “decltype: C++0x Features in VC10, Part 3，”Stephan T. Lavavej, Visual C++ Team Blog, 2009年4月22日。

- “Clean up Function Syntax with decltype，”Danny Kalev, DevX.com, 2008年5月8日。

# 更多信息

## 其他特性 (Other Features):

- “C++0x Forward Declarations Cut Down Time and Dependencies，”Danny Kalev, DevX.com, 2009年8月13日。

- “C++09 Attributes: Specify Your Constructs’ Properties，”Danny Kalev, DevX.com, 2009年5月14日。

- “Overriding Virtual Functions? Use C++0x Attributes to Avoid Bugs，”Danny Kalev, DevX.com, 2009年11月12日。

# 谢谢

非常感谢我的发布材料的审查员：

- Stephan T. Lavavej

- Bernhard Merkle

- Stanley Friesen

- Leor Zolman

- Hendrik Schober

Anthony Williams 贡献了 C++0x 知识以及 `std::thread` 库。

- 库网站：<http://www.stdthread.co.uk/>

- 使用 <http://www.stdthread.co.uk/sm20/> 可享20% 折扣。

comp.std++ 的参与者提供了宝贵的信息和启发性的讨论。

# 许可信息

Scott Meyers 授权本材料和其他培训课程用于商业或个人使用。详情：

- **商业使用**：<http://aristeia.com/Licensing/licensing.html>

- **个人使用**：<http://aristeia.com/Licensing/personalUse.html>

目前可供个人使用的课程包括：

![](img/68a90f505054116271758fb914871a74_360_0.png)

# 关于 Scott Meyers

Scott 是一位 C++ 软件设计与实现的培训师和顾问顾问。他的网站 提供了以下信息：

- 培训和咨询服务

- 书籍、文章和其他出版物

- 即将进行的演讲

- 专业活动博客

![](img/68a90f505054116271758fb914871a74_361_0.png)

# 新 C++ (C++0x) 概览

Item 14：仔细考虑资源管理类中的拷贝行为。

Item 15：在资源管理类中提供资源的访问。

Item 16：在使用新旧对象拷贝时使用相同的形式。

Item 17：在独立结构中使用智能指针存储新创建的对象。

# 目录

前言

致谢

引言

## 第一章：让自己积累 C++

Item 1：将 C++ 视为多种语言的联邦。

Item 2：优先使用 `const`、枚举 (`enums`) 和 `inline` 而非 `define`。

Item 3：尽可能使用 `const`。

Item 4：确保对象在使用之前已初始化。

## 第二章：构造函数、析构函数和赋值运算符

Item 5：了解哪些你没有编写的函数在写入和调用了了什么。

Item 6：避免使用编译器生成的函数。

Item 7：在多态基类中声明 `virtual` 析构函数。

Item 8：防止从析构函数抛出异常。

Item 9：让赋值运算符返回 `*this` 的引用。

Item 10：避免使用内联赋值。

Item 11：拷贝对象的所有部分。

## 第三章：资源管理

Item 13：使用对象来管理资源。

Item 22：将数据成员声明为 `private`。

Item 23：优先使用非 `const` 函数而非可变 (`mutable`) 函数。

Item 24：当所有项都适用于所有参数时，声明非 `const` 函数。

Item 25：考虑用于非抛异常的交换 (`swap`)。

## 第五章：实现

Item 26：尽可能推迟虚函数定义的定义。

Item 27：最小化转换。

Item 28：避免过度使用 "base" 到对象。

Item 29：理解 `inline` 的代价。

Item 30：避免文件间的编译依赖。

## 第六章：继承和面向对象的设计

Item 32：使公继承建模“is-a”关系。

Item 33：避免隐藏继承的名字。

Item 34：区分接口继承和实现的继承。

Item 35：考虑虚函数的替代方案。

Item 36：永远不要重定义继承的非虚函数。

## 新 C++ (C++0x) 概述

- Item 37: 重新定义函数继承的默认参数值 180

- Item 38: 通过组合模拟“拥有”（has-a）与“实现”（implemented-in-of） 184

- Item 39: 谨慎使用继承 187

- Item 40: 谨慎使用多重继承 192

# 第 7 章：模板与泛型编程 199

- Item 41: 理解模板的两种含义 199

- Item 42: 理解模板是如何实例化的 203

- Item 43: 了解如何访问基类中的模板 207

- Item 44: 优先使用与参数无关的模板代码 212

- Item 45: 使用成员函数接受所有“泛型类型” 218

- Item 46: 发生转换时避免在模板内部使用非成员函数 222

- Item 47: 使用特征类（trait classes）获取类型信息 226

- Item 48: 注意模板元编程 233

# 第 8 章：自定义 new 和 delete 239

- Item 49: 理解 new-handler 和 delete 的行为 240

- Item 50: 理解在何时替换 new 和 delete是有意义的 247

- Item 51: 在编写 new 和 delete 时避免转换 252

- Item 52: 如果你编写了定位 new（placement new），请使用定位 delete 256

# 第 9 章：其他杂记 262

- Item 53: 注意编译器警告，包括 TLI 262

- Item 55: 熟悉 Boost 269

# 附录 A：超越《Effective C++》273

# 附录 B：第二版与第三版之间的 Item 映射 277

# 索引 280



> 转自《Effective C++, Third Edition: 55 Specific Ways to Improve Your Programs and Designs》，作者 Scott Meyers, Addison-Wesley Publishing Company, 2005.
