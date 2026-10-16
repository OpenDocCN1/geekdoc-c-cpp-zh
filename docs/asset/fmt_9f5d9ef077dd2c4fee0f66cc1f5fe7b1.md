

时钟返回一个 `time_point`（时间点）。将两个 `time_point` 相减得到一个 `duration`（时间段）。不同的时钟以不同的时间单位给出结果（我使用的时钟以`纳秒`为单位），因此通常最好将 `duration` 转换为已知单位。这正是 `duration_cast` 所做的。

用于处理时间的标准库设施位于子命名空间 `std::chrono` 中的 `<chrono>` (§35.2) 内。

不要在没有进行时间测量的情况下就对代码的“效率”发表声明。关于性能的猜测是最不可靠的。

## 5.4.2 类型函数

类型函数是在编译时求值的函数，它以类型作为参数或返回类型。标准库提供了多种类型函数，帮助库实现者和一般程序员编写利用语言、标准库和代码本身的特性的代码。

对于数值类型，来自 `<limits>` 的 `numeric_limits` 提供了各种有用信息（§5.6.5）。例如：

```cpp
constexpr float min = numeric_limits<float>::min(); // smallest positive float (§40.2)
```

类似地，可以使用内置的 `sizeof` 运算符（§2.2.2）获取对象大小。例如：

```cpp
constexpr int szi = sizeof(int); // the number of bytes in an int
```

此类类型函数是 C++ 用于编译时计算的机制的一部分，它们允许比以往更严格的类型检查和更好的性能。使用这些特性通常被称为元编程，或者（涉及模板时）模板元编程（第28章）。这里我只介绍标准库提供的两个设施：`iterator_traits`（§5.4.2.1）和类型谓词（§5.4.2.2）。

### 5.4.2.1 iterator_traits

标准库的 `sort()` 接受一对迭代器，它们应该定义一个序列（§4.5）。此外，这些迭代器必须提供对该序列的随机访问，即它们必须是随机访问迭代器。某些容器（例如 `forward_list`）不提供这种访问。特别是，`forward_list` 是单向链表，因此下标访问代价高昂，而且没有合理的方式引用前一个元素。然而，与大多数容器一样，`forward_list` 提供前向迭代器，可用于通过算法和 `for` 语句遍历序列（§33.1.1）。

标准库提供了一种机制 `iterator_traits`，允许我们检查支持哪种迭代器。有了它，我们可以改进 §4.5.6 中的范围 `sort()`，使其接受 `vector` 或 `forward_list`。例如：

```cpp
void test(vector<string>& v, forward_list<int>& lst)
{
    sort(v); // sort the vector
    sort(lst); // sort the singly-linked list
}
```

使这一切工作所需的技术通常很有用。

首先，我编写两个辅助函数，它们接受一个额外参数，指示用于随机访问迭代器还是前向迭代器。接受随机访问迭代器参数的版本很简单：

```cpp
template<typename Ran>
void sort_helper(Ran beg, Ran end, random_access_iterator_tag) {
    sort(beg,end); // just sort it
}
// for random-access iterators // we can subscript into [beg:end)
```

前向迭代器版本几乎一样简单；只需将列表复制到 `vector` 中，排序，然后再复制回来：

```cpp
template<typename For>
void sort_helper(For beg, For end, forward_iterator_tag) {
    vector<decltype(*beg)> v {beg,end}; // initialize a vector from [beg:end)
    sort(v.begin(),v.end());
    copy(v.begin(),v.end(),beg); // copy the elements back
}
```

`decltype()` 是一个内置类型函数，返回其参数声明的类型（§6.3.6.3）。因此，`v` 是一个 `vector<X>`，其中 `X` 是输入序列的元素类型。

真正的“类型魔法”在于辅助函数的选择：

```cpp
template<typename C>
void sort(C& c)
{
    using Iter = Iterator_type<C>;
    sort_helper(c.begin(),c.end(),Iterator_category<Iter>{});
}
```

这里，我使用了两个类型函数：`Iterator_type<C>` 返回 `C` 的迭代器类型（即 `C::iterator`），然后 `Iterator_category<Iter>{}` 构造一个“标签”值，指示所提供的迭代器种类：

- 如果 `C` 的迭代器支持随机访问，则为 `std::random_access_iterator_tag`。
- 如果 `C` 的迭代器支持前向迭代，则为 `std::forward_iterator_tag`。

有了它，我们可以在编译时在两种排序算法之间进行选择。这种称为标签分派（tag dispatch）的技术是标准库及其他地方用于提高灵活性和性能的多种技术之一。

标准库对使用迭代器技术（如标签分派）的支持，以来自 `<iterator>`（§33.1.3）的简单类模板 `iterator_traits` 的形式提供。这允许对 `sort()` 中使用的类型函数进行简单定义：

```cpp
template<typename C>
using Iterator_type = typename C::iterator; // C’s iterator type
template<typename Iter>
using Iterator_category = typename std::iterator_traits<Iter>::iterator_category; // Iter’s category
```

如果你不想了解用于提供标准库功能的“编译时类型魔法”是什么，你可以自由地忽略诸如 `iterator_traits` 之类的设施。但那样你就无法使用它们支持的技术来改进自己的代码。

### 5.4.2.2 类型谓词

标准库类型谓词是一种简单的类型函数，回答关于类型的基本问题。例如：

```cpp
bool b1 = Is_arithmetic<int>(); bool b2 = Is_arithmetic<string>();
// yes,int is an arithmetic type
// no,std::string is not an arithmetic type
```

这些谓词位于 `<type_traits>` 中，并在 §35.4.1 中描述。其他示例包括 `is_class`、`is_pod`、`is_literal_type`、`has_virtual_destructor` 和 `is_base_of`。当我们编写模板时，它们最为有用。例如：

命名并不是特别有创意，一开始可能看起来有点奇怪，但当我们想要编写泛型代码时，这种一致的命名是一种恩惠。

标准库的 `pair`（来自 `<utility>`）在标准库和其他地方都很常用。如果 `pair` 的元素支持运算符（如 `=`、`==` 和 `<`），则 `pair` 也支持这些运算符。`make_pair()` 函数可以轻松地创建 `pair`，而无需显式提及其类型（§34.2.4.1）。例如：

```cpp
void f(vector<string>& v)
{
    auto pp = make_pair(v.begin(),2); // pp is a pair<vector<string>::iterator,int>
    // ...
}
```

如果你需要多于两个（或更少）元素，可以使用 `tuple`（来自 `<utility>`；§34.2.4.2）。`tuple` 是元素的异构序列；例如：

```cpp
tuple<string,int,double> t2("Sild",123, 3.14); // the type is explicitly specified
auto t = make_tuple(string("Herring"),10, 1.23); // the type is deduced
// tisatuple<string,int,double>
```

`tuple` 的元素是编号的（从零开始），而不是像 `pair` 的元素那样命名（`first` 和 `second`）。要获得元素的编译时选择，我遗憾地必须使用丑陋的 `get<1>(t)`，而不是 `get(t,1)` 或 `t[1]`（§28.5.2）。

与 `pair` 类似，如果 `tuple` 的元素可以被赋值和比较，那么 `tuple` 也可以。

`pair` 在接口中很常见，因为我们经常希望返回多个值，例如结果和该结果质量的指示。需要三个或更多部分的结果较少见，因此 `tuple` 更常用于泛型算法的实现中。

# 5.5 正则表达式

正则表达式是文本处理的强大工具。它们提供了一种简单而简洁地描述文本模式的方法（例如，美国邮政编码如 TX 77845，或 ISO 风格的日期如 2009-06-07），并能在文本中高效地查找这些模式。在 `<regex>` 中，标准库以 `std::regex` 类及其支持函数的形式提供正则表达式支持。为了体验一下 `regex` 库的风格，让我们定义一个模式并打印它：

```cpp
regex pat (R"(\w{2}\s*\d{5}(-\d{4})?)"); // ZIP code pattern: XXdddd-dddd and variants
cout << "pattern: " << pat << '\n';
```

几乎使用过任何语言正则表达式的人都会对 `\w{2}\s*\d{5}(-\d{4})?` 感到熟悉。它指定了一个模式：以两个字母 `\w{2}` 开头，可选地后跟一些空格 `\s*`，然后是五个数字 `\d{5}`，并且可选地后跟一个连字符和四位数字 `-\d{4}`。如果你不熟悉正则表达式，现在可能正是学习它们的好时机（[Stroustrup,2009]，[Maddock,2009]，[Friedl,1997]）。

正则表达式在 §37.1.1 中进行了总结。

为了表达模式，我使用一个以 `R"(` 开头、以 `)"` 结尾的原始字符串字面量（§7.3.2.1）。这样可以在字符串中直接使用反斜杠和引号。使用模式的最简单方式是在流中搜索它：

```cpp
int lineno = 0;
for (string line; getline(cin,line);) { // read into line buffer
    ++lineno;
    smatch matches; // matched strings go here
    if (regex_search(line,matches,pat)) // search for pat in line
        cout << lineno << ": " << matches[0] << '\n';
}
```

`regex_search(line,matches,pat)` 在 `line` 中搜索与存储在 `pat` 中的正则表达式匹配的内容，如果找到任何匹配，就将它们存储在 `matches` 中。如果没有找到匹配，`regex_search(line,matches,pat)` 返回 `false`。`matches` 变量的类型是 `smatch`。这个“s”代表“sub”（子匹配），`smatch` 是子匹配的 `vector`。第一个元素，这里是 `matches[0]`，是完整匹配。

更完整的描述请参见第 37 章。

# 5.6 数学

C++ 并非主要为了数值计算而设计。然而，C++ 被大量用于数值计算，标准库也反映了这一点。

## 5.6.1 数学函数与算法

在 `<cmath>` 中，我们可以找到“常用数学函数”，例如用于 `float`、`double` 和 `long double` 类型参数的 `sqrt()`、`log()` 和 `sin()`（§40.3）。这些函数的复数版本可以在 `<complex>` 中找到（§40.4）。

在 `<numeric>` 中，我们可以找到一小组通用数值算法，例如 `accumulate()`。例如：

```cpp
void f()
{
    list<double> lst {1, 2, 3, 4, 5, 9999.99999};
    auto s = accumulate(lst.begin(),lst.end(),0.0); // calculate the sum
    cout << s << '\n'; // print 10014.9999
}
```

这些算法适用于所有标准库序列，并且可以接受操作作为参数（§40.6）。

## 5.6.2 复数

标准库支持一组复数类型，类似于 §2.3 中描述的 `complex` 类。为了支持标量为单精度浮点数（`float`）、双精度浮点数（`double`）等的复数，标准库的 `complex` 是一个模板：

```cpp
template<typename Scalar>
class complex {
public:
    complex(const Scalar& re ={}, const Scalar& im ={});
    // ...
};
```

复数支持常用的算术运算和最常用的数学函数。例如：

```cpp
void f(complex<float> fl, complex<double> db)
{
    complex<long double> ld {fl+sqrt(db)};
    db += fl*3;
    fl = pow(1/fl,2);
    // ...
}
```

`sqrt()` 和 `pow()`（幂运算）函数是 `<complex>` 中定义的常用数学函数之一。更多细节请参见 §40.4。

## 5.6.3 随机数

随机数在许多场景中都很有用，例如测试、游戏、模拟和安全。应用领域的多样性体现在标准库在 `<random>` 中提供的多种随机数生成器上。随机数生成器由两部分组成：

- [1] 一个引擎，用于产生随机或伪随机值序列。
- [2] 一个分布，将这些值映射到某个范围内的数学分布。

分布的例子包括 `uniform_int_distribution`（生成的所有整数概率均等）、`normal_distribution`（“钟形曲线”）和 `exponential_distribution`（指数增长）；每一种都作用于某个指定范围。例如：

```cpp
using my_engine = default_random_engine; // type of engine
using my_distribution = uniform_int_distribution<>; // type of distribution
my_engine re {};
my_distribution one_to_six {1,6};
auto die = bind(one_to_six,re); // make a generator
int x = die(); // roll the die: x becomes a value in [1:6]
```

标准库函数 `bind()` 创建一个函数对象，该对象将在给定其第二个参数（此处为 `re`）作为其参数的情况下调用其第一个参数（此处为 `one_to_six`）（§33.5.1）。因此，调用 `die()` 等价于调用 `one_to_six(re)`。

由于其毫不妥协地关注通用性和性能，一位专家将标准库随机数组件称为“每个随机数库长大后的理想模样”。然而，它很难被称为“对新手友好”。`using` 语句让所做的事情更加明显。否则，我本可以这样写：

```cpp
auto die = bind(uniform_int_distribution<>{1,6}, default_random_engine{});
```

哪个版本更易读完全取决于上下文和读者。对于新手（无论背景如何），随机数库完全通用的接口可能是一个严重的障碍。一个简单的均匀随机数生成器通常足以入门。例如：

```cpp
Rand_int rnd {1,10}; // make a random number generator for [1:10]
int x = rnd(); // x is a number in [1:10]
```

那么，我们怎样才能得到它呢？我们必须将类似 `die()` 的东西封装到 `Rand_int` 类中：

```cpp
class Rand_int {
public:
    Rand_int(int low, int high) : dist{low,high} { }
    int operator()() { return dist(re); } // draw an int
private:
    default_random_engine re;
    uniform_int_distribution<> dist;
};
```

这个定义仍然是“专家级”的，但在面向新手的 C++ 课程的第一周，使用 `Rand_int()` 是可以应付的。例如：

```cpp
int main()
{
    Rand_int rnd {0,4}; // make a uniform random number generator
```

