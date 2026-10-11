
```
string test("Take a turn at Main Street.");
test.replace(7,5,"left"); // replace right with left
```

## Output and Input

请注意，你可以使用 `find()` 来查找 `replace` 中使用的位置：

```
string s1 = "old";
string s2 = "mature";
string s3 = "The old man and the sea";
string::size_type pos = s3.find(s1);
if (pos != string::npos)
s3.replace(pos, s1.size(), s2);
```

此示例将 `old` 替换为 `mature`。

## Other Modifying Methods: `copy()` and `swap()`

`copy()` 方法将字符串对象或其一部分复制到指定的字符数组：

`size_type copy(char* s, size_type n, size_type pos = 0) const;`

在这种情况下，`s` 指向目标数组，`n` 表示要复制的字符数，`pos` 表示从字符串对象中开始复制的位置。

复制进行 `n` 个字符或字符串对象中的最后一个字符，以先到者为准。该函数返回复制的字符数。

该方法不附加空字符，并且程序员需要确保数组足够大以容纳副本。

### Caution

`copy()` 方法不附加空字符，也不检查目标数组是否足够大。

`swap()` 方法使用恒定时间算法交换两个字符串对象的内容：

```
void swap(basic_string& str);
```

## Output and Input

`string` 类重载了 `<<` 运算符以显示字符串对象。它返回 `istream` 对象的引用，以便输出可以连接：

```
string claim("The string class has many features.");
cout << claim << endl;
```

`string` 类重载了 `>>` 运算符，以便你可以将输入读入字符串：

```
string who;
cin >> who;
```

输入在遇到文件结束、读取字符串允许的最大字符数或遇到空白字符时终止。（空白的定义取决于字符集和 `char` 所代表的类型。）

## Appendix F The string Template Class

有两个 `getline()` 函数。第一个具有以下原型：

`template<class charT, class traits, class Allocator>`

`basic_istream<charT,traits>& getline(basic_istream<charT,traits>& is,`

`basic_string<charT,traits,Allocator>& str, charT delim);`

它从输入流中读取字符到字符串 `str`，直到遇到文件结束。`delim` 字符被读取（即从输入流中移除）但不存储。第二个版本缺少第三个参数并使用换行符（或其泛化）代替 `delim`：

```
string str1, str2;
getline(cin, str1);      // read to end-of-line
getline(cin, str2, '.'); // read to period
```

## The Standard Template Library Methods and Functions

标准模板库 `STL` 旨在提供常见算法的高效实现。它以通用函数表达这些算法，这些函数可与满足特定算法要求的任何容器一起使用，并在可与特定容器类实例化一起使用的方法中表达。本附录假设你对 `STL` 有一定的熟悉程度，因此阅读第 16 章 "The string Class and the Standard Template Library" 可能大有裨益。例如，本章假设你了解迭代器和构造函数。

## The STL and C++11

正如 `C++11` 对 `C++` 语言的更改过于广泛，无法在本书中完全涵盖一样，`STL` 的更改也过于广泛，无法在本附录中完全涵盖。然而，我们可以总结许多新增内容。`C++11` 为 `STL` 带来了几个新元素。首先，它添加了几个容器。其次，它为旧容器添加了一些新功能。第三，它为其算法添加了一些模板函数。所有这些更改都已纳入本附录，但你可能会发现对前两类内容的概述有所帮助。

## New Containers

`C++11` 添加了以下容器：`array`、`forward_list`、`unordered_set` 以及无序关联容器 `unordered_multiset`、`unordered_map` 和 `unordered_multimap`。

一旦声明，`array` 的大小就固定，并且使用静态或栈内存而不是动态分配的内存。它旨在作为内置数组类型的替代品；它比 `vector` 更受限制，但更高效。

`list` 容器是一个双向链表，每个项目除两端外，都链接到前一个项目和后一个项目。`forward_list` 是一个单向

# 附录 G 标准模板库方法与函数

`list`，每个条目除最后一个外都链接到下一个条目。它提供了一种更紧凑、但更受限的列表替代方案。

像 `set` 和其他关联容器一样，无序关联容器允许通过使用键快速检索数据。区别在于关联容器使用树作为底层数据结构，而无序关联容器使用哈希表。

## 对 C++98 容器的更改

`C++11` 对容器类方法带来了三个主要更改。

首先，右值引用的添加使得为容器提供移动语义（第 18 章，“使用新 C++ 标准访问”）成为可能。因此，`STL` 现在为容器提供了移动构造函数和赋值运算符。这些方法接受右值引用。

其次，`initializer_list` 模板类的添加（第 18 章）导致了接受 `initializer_list` 参数的构造函数和赋值运算符。这使得以下代码成为可能：

```
vector<int> vi(100, 99, 97, 98);
vi = {96, 99, 94, 95, 102};
```

第三，可变参数模板和函数参数包的添加（第 18 章）使得就地构造方法成为可能。这意味着什么？与移动语义类似，就地构造是一种提高效率的手段。考虑以下代码片段：

```
class Items {
    double x;
    double y;
    int m;
public:
    Items();                // #1
    Items(double xx, double yy, int mm); // #2
};
```

```
vector<Items> vt(10);
t.push_back(Items(8.2, 2.8, 3)); //
```

对 `insert()` 的调用会导致内存分配函数在 `vt` 末尾创建一个默认的 `Items` 对象。接下来，`Items()` 构造函数创建一个临时的 `Items` 对象；该对象被复制到 `vector` `vt` 的前端，然后临时对象被删除。使用 `C++11`，你可以这样做：

```
vi.emplace_back(8.2, 2.8, 3);
```

## 所有或大多数容器共有的成员

`emplacement_back()` 方法是一个可变参数模板，其参数为函数参数包：

```
template<class...> void emplace_back(Args&... args);
```

三个参数 `8.2`、`2.8` 和 `3` 被打包到 `args` 中。这些参数连同分配函数一起传递，分配函数随后解包参数并使用带三个参数的 `Items` 构造函数（#2）而不是默认构造函数（#1）。也就是说，它可以使用 `Items(args...)`，其中它展开为 `Items(8.2, 2.8, 3)`。因此期望的对象是在 `vector` 中就地构造，而不是在临时位置构造并复制到 `vector` 中。

`STL` 使用这种技术来实现几种就地构造方法。

## 所有或大多数容器共有的成员

所有容器都定义了表 G.1 中的类型。在此表中，`x` 是一个容器类型，例如 `vector<int>`，而 `T` 是存储在容器中的类型，例如 `int`。表后的示例阐明了含义。

### 表 G.1 为所有容器定义

| Type | Value |
|---|---|
| `X::value_type` | `T`, the element type. |
| `X::reference` | `T &` |
| `X::const_reference` | `const T &` |
| `X::iterator` | Iterator type pointing to `T`; behaves like type `T` |
| `X::const_iterator` | Iterator type pointing to `const T`; behaves like `const T *` |
| `X::difference_type` | Signed integer type to represent the distance from one iterator to another (for, the difference between two pointers). |
| `X::size_type` | Unsigned integer type `size_type` can represent size of data objects, number of elements, and subscripts. |

类定义使用 `typedef` 来定义这些成员。你可以使用一种迂回的方式，用“bogus”替换 `vector` of `string` 对象中第一个出现的“bonus”，以展示如何使用成员类型声明变量：

```
using namespace std;
vector<string> input;
string temp;
while (cin >> temp && temp != "quit")
input.push_back(temp);
vector<string>::iterator want =
```

```
find(input.begin(), input.end(), string("bonus"));
if (want != input.end())
{
    vector<string>::reference r = *want;
    r = "bonus";
}
```

此代码使 `r` 成为对 `input` 中 `want` 所指向元素的引用。同样，继续前面的示例，你可以编写如下代码：

```
vector<string>::value_type s1 = input[0]; // s1 is type string
vector<string>::reference s2 = input[1]; // s2 is type string &
```

这导致 `s1` 成为 `input[0]` 的副本的字符串对象，而 `s2` 成为对 `input[1]` 的引用。在此示例中，由于你已经知道模板的类型为 `string`，更简单地编写以下等效代码：

```
string s1 = input[0]; // s1 is type string
string s2 = input[1]; // s2 is type string &
```

然而，表 G.1 中的详细类型也可以用于更通用的代码，其中容器和元素的类型是泛型的。例如，假设你想要一个函数，其参数为容器引用，并返回容器中的最小项。这假设 `<` 运算符已为用于实例化模板的值类型定义，并且你不想使用 `STL` 的 `min_element` 算法，该算法使用迭代器接口。由于参数可能是 `vector<int>` 或 `list<string>` 或 `deque<double>`，你使用模板参数，例如 `Bag`，来表示容器（即 `Bag` 是一个模板类型，可能会实例化为 `vector<int>`、`list<string>` 或其他容器类型）。因此函数的参数为 `const Bag &`。返回类型会是什么？它应该是容器的值类型——即 `Bag::value_type`。然而，在这一点上，`Bag` 是一个模板参数，编译器无法知道 `value_type` 成员是什么。你可以使用 `typename` 关键字来澄清类成员是一个 `typedef`：

```
vector<string>::value_type st; // vector<string> a defined class
typename Bag::value_type m; // Bag as an ended typedef type
```

对于第一个定义，编译器可以访问 `vector` 模板定义，其中声明 `value_type` 是一个 `typedef`。对于第二个定义，`typename` 提供了无论 `Bag` 最终是什么，`Bag::value_type` 都是一个类型的名称。这些考虑导致了以下定义：

```
template <typename Bag>
typename Bag::value_type min(const Bag & b)
{
```

```
typename Bag::const_iterator it;
typename Bag::value_type m = *b.begin();
```

```
for (it = b.begin(); it != b.end(); ++it)
  if (*it < m)
    m = *it;
return m;
```

你可以使用此模板函数如下：

```
vector<int> temperatures;
// input temperature values into the vector
int coldest = min(temperatures);
```

`Temperatures` 参数会导致 `Bag` 被求值为 `vector<int>`，而 `typename Bag::value_type` 被求值为 `vector<int>::value_type`，后者又为 `int`。

所有容器都有表 G.2 中列出的成员函数或操作。同样，`X` 是一个容器类型，如 `vector<int>`，而 `T` 是存储在容器中的内容，如 `int`。`a` 和 `b` 也是 `x` 的值，`u` 是一个标识符，`r` 是类型 `x` 的非 `const` 值，`rv` 是类型 `x` 的非 `const` 值。移动操作是在 `C++11` 中添加的。

### 表 G.2 为所有容器定义的操作

| Operation | Description |
|---|---|
| `X u` | Constructs an empty object `u`. |
| `X()` | Constructs an empty object. |
| `X(a)` | Constructs a copy of object `a`. |
| `X u(a)` | `u` is a copy of `a` (copy constructor). |
| `X u = a;` | `u` is a copy of `a` (copy constructor). |
| `r = a` | `r` equals the value of `a` (copy assignment). |
| `X u(rv)` | `u` equals the value that `rv` had before construction (move constructor). |
| `X u = rv;` | `u` equals the value that `rv` had before construction (move constructor). |
| `a = rv` | `a` equals the value that `rv` had before construction (move assignment). |
| `begin()` | Returns an iterator to the first element. |
| `end()` | Returns an iterator to the end. |
| `cbegin()` | Returns a const iterator to the first element. |
| `cend()` | Returns a const iterator to the end. |
| `size()` | Returns the number of elements. |
| `maxsize()` | Returns the size of the largest possible container. |
| `empty()` | Returns true if the container is empty. |

## 1276 附录 G 标准模板库方法与函数

表 G.2 为所有容器定义的操作

| 操作 | 描述 |
|---|---|
| `swap()` | 交换两个容器的内容。 |
| `==` | 如果两个容器大小相同且元素按相同顺序相同，则返回 true。 |
| `!=` | `a != b` 返回 `! (a == b)`。 |

使用双向或随机迭代器的容器（`vector`、`list`、`deque`、`queue`、`array`、`set` 和 `map`）是可逆的，并提供表 G.3 中的方法。

表 G.3 为可逆容器定义的类型和操作

| 操作 | 描述 |
|---|---|
| `X::reverse_iterator` | 指向类型 `T` 的反向迭代器。 |
| `X::const_reverse_iterator` | 指向类型 `T` 的 const 反向迭代器。 |
| `a.rbegin()` | 返回指向 `a` 末尾的反向迭代器。 |
| `a.rend()` | 返回指向 `a` 开头的反向迭代器。 |
| `a.crbegin()` | 返回指向 `a` 末尾的 const 反向迭代器。 |
| `a.crend()` | 返回指向 `a` 开头的 const 反向迭代器。 |

`unordered set` 和 `unordered map` 容器不要求支持表 G.4 中的可选容器操作，但其余容器都支持它们。

表 G.4 可选容器操作

| 操作 | 描述 |
|---|---|
| `<` | `a < b` 如果 `a` 字典序先于 `b` 则返回 true。 |
| `>` | `a > b` 返回 `b < a`。 |
| `<=` | `a <= b` 返回 `! (a > b)`。 |
| `>=` | `a >= b` 返回 `! (a < b)`。 |
