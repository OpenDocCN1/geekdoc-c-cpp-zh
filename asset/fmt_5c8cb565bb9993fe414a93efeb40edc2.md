
- `size_type count(const key_type &k) const`; - 返回 `k` 在 `map` 中出现的次数（必须为 1 或 0）。

`void clear()`; 删除 `map` 中的所有元素。

`bool empty() const`; - 如果 `map` 为空则返回 true，否则返回 false。

`void erase(iterator i)`; 删除由 `i` 指向的元素。

# 向 Map 中插入元素

`insert` 函数的声明为：

```cpp
iterator map_name.insert({key, element})
```

注意括号是必须的，因为我们正在插入一个 `pair` 对象。此成员函数返回一个指向插入元素的迭代器。

这是一个示例：

```cpp
#include <map>
#include <iostream>
#include <string>
namespace std;
int main() {
    // 初始化一个 int map 容器
    map<int, int> mp;
    // 插入一些元素
    mp.insert({{2, 30}});
    mp.insert({1, 10});
    // 声明一个用于遍历 map<int,int> 的迭代器
    map<int, int>::iterator p;
    // 初始化迭代器
    p = mp.begin();

    // 遍历 map 获取键和值

    for (; p != mp.end(); ++p) {
        cout << "key: " << p->first << "\n";
        cout << "value: " << p->second << "\n";
    }
}
```

# 获取 Map 的键和键值

给定一个 `map` 迭代器 `p`，它指向一个 `pair` 对象 `{key, value}`。`p->first` 指向键，`p->second` 指向值。

程序创建一个电话簿 `map`，将名称映射到电话号码。

# Map 容器示例

```cpp
#include <iostream>
#include <map>
#include <string>

using namespace std;

int main() {
    map<string, string> tel;

    // 向 map 插入元素
    tel.insert({"alice smith", "555-555-5555"});
    tel.insert({"john brown", "656-890-9080"});

    map<string, string> iter;

    // 给定一个名称查找号码
    iter = tel.find("alice smith");

    if(iter != tel.end()) {
        cout << "name: " << iter->first << endl;
        cout << "telephone number is: " << iter->second << endl;
    }
    else
    cout << "Name is not in map.\n"
    return 0;
}
// 输出：
name is alice smith
telephone number is: 555-555-5555
```

## 算法

算法作用于容器。虽然每个容器都提供了基本操作的支持，但标准算法实现了复杂的动作。它们允许我们同时处理不同类型的容器。使用 STL 算法，必须在程序中包含 `<algorithm>` 头文件。

所有的算法都是函数模板。它们可以应用于任何容器。

有很多 STL 算法，一些有趣的有：

| binary_search | 在有序序列上执行二分查找。 |
| count_if | 返回满足谓词的元素数量。 |
| find | 在范围内查找值，并返回指向该元素的迭代器。 |
| find_if | 在范围内查找满足用户定义的一元谓词的元素。 |

`<` 小于

`<=` 小于或等于

`>`, `>=` 大于和大于等于

`[]` 索引运算符

`<<` 输出

`>>` 输入

这些运算符消除了对调用 `strcpy` 和 `strcat` 等函数的需要。

## 字符串拼接

`+` 运算符可以将一个字符串对象与另一个字符串对象或 C 风格字符串拼接。

```cpp
// 字符串示例

#include <iostream>

#include <string>

using namespace std;

int main() {

    string str1("Alpha");

    string str2("Beta");

    string str3("Omega");

    string str4;

    // 赋值一个字符串

    str4 = str1;

    cout << str1 << "\n" << str4 << "\n";

    // 拼接两个字符串

    str4 = str1 + str2;

    cout << str4 << "\n";

    // 将字符串与 C 字符串拼接

    str4 = str1 + " " + str3;

    cout << str4 << "\n";

    // 比较字符串

    if(str3 > str1) cout << str3 > str1 << "\n";

    if(str3 == str1 + str2)

    cout << "str3 == str1+str2\n";

}

// 将 C 风格字符串赋值给字符串对象

str1 = "This is a null-terminated string: ";

// 拷贝构造的字符串对象

str5(str1);

cout << str5 << endl;

// 输入和输出字符串

cout << "Enter a string: ";

cin >> str5;

cout << str5 << endl;
```

字符串对象会自动调整大小，以容纳其封装的字符串。因此，在赋值或拼接字符串时，目标字符串会根据需要增长或收缩，以适应新字符串的大小。字符串对象不会发生缓冲区溢出。

# 将字符串对象转换为 C 风格字符串

成员函数 `c_str()` 将字符串对象转换为以空结尾的 C 风格字符串：

```cpp
#include <iostream>
#include <cstring>
#include <string>
int main () {
    std::string str("hello world");
    const char* cstr = str.c_str();
    // cstr 现在包含 str 的 C 风格字符串拷贝；包括
    // 终止的空字符
}
```

# 用于字符串的 STL 算法

字符串类满足容器所需的所有基本要求。因此，它支持大多数常见的容器函数，例如 `begin`, `end`, `size` 等。它还支持迭代器。字符串对象也可以通过 STL 算法进行操作。

# 现代 C++ Type_Traits (C++11)

类型特性（Type traits）是一种模板元编程技术，允许我们能够在编译时确定变量的类型属性。由于类型信息是在编译时获取的，因此零运行时开销。

C++ 标准库实现了大量的预定义类型特性，这些特性定义在 `<type_traits>` 头文件中。

类型特性是一个包含单个常量静态数据成员的 `struct`。如果该成员回答了关于某个类型的问题，则该成员命名为 `value`。如果该成员转换了类型，则该成员命名为 `type`。

考虑以下类型特性的声明：

```cpp
#include <type_traits>
template<typename T>
struct is_floating_point;
```

该特性询问 `T` 是否为浮点类型。该结构体回答了这个问题。`is_floating_point` 结构体包含一个静态常量变量 `value`。`value` 为 `true` 或 `false`。

假设我们想要确定给定的类型是否为浮点类型。以下代码示例展示了如何实现：

```cpp
#include <iostream>
#include <type_traits>
using namespace std;
class Foo {};
int main() {
	cout << is_floating_point<Foo>::value << '\n';
	cout << is_floating_point<float>::value << '\n';
	cout << is_floating_point<int>::value << '\n';
}
// 输出
```

为了计算之前的表达式，编译器在编译时生成了以下显式 `struct` 和静态常量值：

```cpp
struct is_floating_point_Foo {
    static const bool value = false;
};
struct is_floating_point_float {
    static const bool value = true;
};
struct is_floating_point_int {
    static const bool value = false;
};
```

**注意：** 类或结构体的 `const static` 数据成员可以像如上所示通过赋值进行初始化。

由于 `struct` 数据成员 `value` 是静态常量，我们可以通过作用域运算符访问它，如下：

```cpp
std::is_floating_point<Foo>::value
```

# 现代 C++：自动类型推导 (C++11)

在 C++11 之前，每个程序变量的类型必须在变量声明中显式指定。从 C++11 开始，我们可以要求编译器为我们推导变量的类型。C++11 有两个用于自动类型推导的新关键字：`auto` 和 `decltype`。

在 C++11 中，我们可以通过将变量的类型设置为 `auto` 来不指定类型声明变量。

```cpp
auto i = 42; // i 的类型为 int
```

`auto` 类型声明指示编译器在编译时推导 `i` 的类型。由于类型推导，我们可以将 `int i = 42;` 语句替换为 `auto i = 42;`。

这里有一个更复杂的示例，使用 `auto` 来简化类型声明：

```cpp
std::vector<int> vec;
```
（注：此处原文示例似乎不完整，仅显示了声明）

以下声明将导致编译错误：

```cpp
#include <iostream>
template<class T, class U>
decltype(lhs * rhs) multiply(T lhs, U rhs) 
{
    return lhs * rhs;
}
int main() {
    auto value = multiply(2.3, 6);
    std::cout << value << std::endl;
}
```

输出：
error: 'lhs' was not declared in this scope

由于编译器是从左到右解析语句的。因此，当它遇到表达式 `(lhs * rhs)` 时，它不知道 `lhs` 和 `rhs` 是什么。尾随返回类型解决了这个问题。

# 代码简化

使用尾随返回类型可以简化代码。考虑以下函数指针声明：

```
void (*func(int i))(int) newFunc;
```

这声明 `newFunc` 为一个函数指针，它接受一个 `int` 参数并返回一个接受 `int` 参数并返回 `void` 的函数指针。这可以用更清晰的方式声明为：

```
auto newFunc(int x) -> void (*)(int);
```

# 现代 C++：变量初始化 (C++11)

变量初始化涉及声明变量并赋予其一个值。C++11 引入了变量初始化的标准语法。

在传统上，C++ 中的初始化可以通过括号、大括号或赋值运算符完成的。这导致了关于如何初始化变量或对象的困惑。C++11 引入了统一初始化，这意味着我们可以使用标准语法进行初始化。

## 拷贝赋值

拷贝赋值是将值放入变量的传统方法。在变量声明后，我们可以使用赋值运算符 `=` 赋予它一个值。这种类型的初始化被称为拷贝赋值（或简称为赋值）。

```cpp
int width               // 声明一个名为 width 的整型变量
width = 5;              // 将值 5 拷贝赋值给变量
```

拷贝赋值之所以这样命名，是因为它将 `=` 运算符右侧的值拷贝到运算符左侧的变量中。`=` 运算符被称为赋值运算符。

拷贝赋值的问题是它使用了两个语句（一个声明和一个赋值），因此消耗了更多的 CPU 周期。

我们可以将变量的声明和初始化合并为一步，以节省 CPU 周期：

```cpp
int width = 5;
```

## 直接初始化

C++11 引入了直接初始化：

```cpp
// 使用值 5 直接初始化变量 width
int width(5); // 等同于 int width (5);
```

对于原生数据类型（如整数），拷贝赋值和直接初始化在本质上是相同的。但对于某些复杂类型，直接初始化的性能可能于拷贝初始化。

接下来考虑：

```cpp
Foo foo(obj)
```

为了让该对象 `foo` 的直接初始化生效，`Foo` 必须有一个拷贝构造函数，或者一个接受 `obj` 作为按值调用的构造函数。否则该语句将无法编译。

## 大括号初始化

大括号初始化有两种形式：

```cpp
// 使用 5 直接大括号初始化变量 width（首选技术）
int width { 5 };
// 使用 5 拷贝大括号初始化变量
int width = { 5 };
```

使用空大括号初始化变量或对象表示零初始化。零初始化将变量初始化为符号零（适用于给定类型的零）。对于对象，零初始化需要一个不接受任何参数的构造函数。

```cpp
// 将字符串零初始化为空字符串
std::string msg {};
```

大括号初始化的额外优点是不允许收窄类型转换。这意味着如果我们尝试使用大括号初始化一个无法安全容纳该值的变量，编译器将抛出警告或错误。

从浮点数到整数的转换总是收窄的——即使是从 5.0 到 5。

```cpp
// 错误：收窄初始化：尝试将 float 类型
// 转换为 int 类型
```

```cpp
int width { 4.0 };
```

最佳实践是始终初始化变量。但有时，为了节省 CPU 周期，我们可以留未初始化变量。

使用大括号初始化强制执行值初始化。使用 `{}` 初始变量被设置为该类型的零值（例如，如果是指针，则设置为 `nullptr`）：

```cpp
string s;
string s {};
// s 有未定义的值
// s 初始化为空字符串
```

```cpp
int j;
int j {};
// j 有未定义的值
// j 初始化为 0
```

```cpp
int* p;
int* p {};
// p 有未定义的值
// p 初始化为 nullptr
```

## 返回 {} 的含义

考虑以下函数声明：

```cpp
FooFunction() { return {}; };
```

函数将返回一个 `Foo` 类型的默认对象。为了使该语句正常编译，`Foo` 必须有一个不接受任何参数的默认构造函数。

## std::initializer_list

另参：标准库：initializer_list

考虑 C++ 中的整数数组：

```cpp
int array[5];
```

我们可以用初始化列表初始化此数组：

```cpp
int array[5] {0, 1, 2, 3, 4};
```

大括号中的表达式被称为初始化列表。

以下对动态分配数组的初始化也可以编译：

```cpp
int *pArray = new int[5] {5, 4, 3, 2, 1};
```

现在考虑以下数组类：

```cpp
#include <iostream>
#include <initializer_list>
class IntArray {
    private:
    int m_length;
    int *m_data;
    public:
    IntArray(): m_length(0), m_data(nullptr) { }
    IntArray(int length) : m_length(length)
    {
      m_data = new int[length];
    }
    ~IntArray()
    {
      delete[] m_data;
    }
    int& operator[](int index)
    {
      return m_data[index];
    }
    int getLength() { return m_length; }
};
int main()
{
    IntArray array { 5, 4, 3, 2, 1 };
    for (int i = 0; i < array.getLength(); i++)
    {
        std::cout << array[i] << " ";
    }
    return 0;
}
```
