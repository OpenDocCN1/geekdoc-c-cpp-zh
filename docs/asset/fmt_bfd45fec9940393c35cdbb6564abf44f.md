
```cpp
void Example::use_ptr() const
{
    Example yard(3);
    int Example::*ptr;
    ptr = &Example::inches;
    cout << "this->*ptr: " << this->*ptr << endl;
    cout << "yard.*ptr: " << yard.*ptr << endl;
    ptr = &Example::feet;
    cout << "Set ptr to &Example::feet\n";
    cout << "this->*ptr: " << this->*ptr << endl;
    cout << "yard.*ptr: " << yard.*ptr << endl;
    void (Example::*pf)() const;
    pf = &Example::show_in;
    cout << "Set pf to &Example::show_in\n";
    cout << "Using (this->*pf)(): ";
    (this->*pf)();
    cout << "Using (yard.*pf)(): ";
    (yard.*pf)();
}
```

```cpp
int main()
{
    Example car(15);
    Example van(20);
    Example garage;

    cout << "car.use_ptr() output:\n";
    car.use_ptr();

    cout << "\nvan.use_ptr() output:\n";
    van.use_ptr();

    return 0;
}
```

# 1246 附录 E 其他运算符

以下是列表 E.1 中程序的示例运行结果：

```
car.use_ptr() output:
Set ptr to &Example::inches:
this->*ptr: 180
yard.*ptr: 36
Set ptr to &Example::feet:
this->*ptr: 15
yard.*ptr: 3
Set pf to &Example::show_in:
Using (this->*pf)(): 180 inches
Using (yard.*pf)(): 36 inches
```

```
van.use_ptr() output:
Set ptr to &Example::inches:
this->*ptr: 240
yard.*ptr: 36
Set ptr to &Example::feet:
this->*ptr: 20
yard.*ptr: 3
Set pf to &Example::show_in:
Using (this->*pf)(): 240 inches
Using (yard.*pf)(): 36 inches
```

此示例在编译时分配了指针值。在更复杂的类中，你可以使用成员指针指向数据成员和方法，而指针关联的精确值是在运行时确定的。

## `alignof` (C++11)

计算机系统对内存中存储数据的方式有限制。例如，某个系统可能要求 `double` 值存储在偶数位置，而另一个系统可能要求存储起始必须是 8 的倍数的位置。`alignof` 运算符接受一个类型作为参数，并返回指示所需对齐类型的整数。对齐要求（例如列表 E.2 所示）决定了信息在结构体内部的排列方式。

### 列表 E.2 `align.cpp`

```cpp
// align.cpp -- 检查对齐
#include <iostream>
using namespace std;
struct thing1
{
    char ch;
    int a;
    double x;
};
struct thing2
{
    int a;
    double x;
    char ch;
};
```

```cpp
int main() {
    thing1 th1;
    thing2 th2;
    cout << "char alignment: " << alignof(char) << endl;
    cout << "int alignment: " << alignof(int) << endl;
    cout << "double alignment: " << alignof(double) << endl;
    cout << "thing1 alignment: " << alignof(thing1) << endl;
    cout << "thing2 alignment: " << alignof(thing2) << endl;
    cout << "thing2 size: " << sizeof(thing2) << endl;
    return 0;
}
```

以下是某系统上的输出：

```
char alignment: 1
int alignment: 4
double alignment: 8
thing1 alignment: 8
thing2 alignment: 8
thing1 size: 16
thing2 size: 24
```

这两个结构体都有 8 的对齐要求。其中一个影响是结构体的大小应该是 8 的倍数，这样在创建结构体数组时，每个元素都能与下一个相邻，并且起始于 8 的倍数的对齐边界上。列表 E.2 中每个结构体的单独成员总共仅使用 13 字节，但 8 字节倍数的要求意味着每个结构体都需要一些填充。接下来，在每个结构体内部，`double` 成员需要对齐到 8 的倍数。`thing1` 和 `thing2` 中成员的不同排列方式导致 `thing2` 需要更多的内部填充以使边界正确。

# `noexcept` (C++11)

`noexcept` 关键字用于指示函数不会抛出异常。它也可以用作运算符，用于确定其操作数（表达式）是否可能抛出异常。如果操作数可能抛出异常，则返回 `false`。

```cpp
// 可能抛出异常的情况
noexcept(expression) // false

// 保证不会抛出异常的情况
noexcept(expression) // true
```

`noexcept` 关键字用于指示函数不会抛出异常。它也可以用作运算符，用于确定其操作数（表达式）是否可能抛出异常。如果操作数可能抛出异常，则返回 `false`。

# `string` 模板类

注意 `traits` 是一个模板参数，对应某个特定类型，如 `char_traits<char>`；`traits_type` 成为该特定类型的别名。`string` 模板定义了若干用于定义方法的类型：

```cpp
typedef typename traits::char_type    traits_type;
typedef typename traits::value_type   value_type;
typedef Allocator                     allocator_type;
typedef typename Allocator::size_type      size_type;
typedef typename Allocator::difference_type difference_type;
typedef typename Allocator::reference reference;
typedef typename Allocator::const_reference const_reference;
typedef typename Allocator::pointer     pointer;
typedef typename Allocator::const_pointer const_pointer;
```

`typename` 关键字用于告诉编译器表达式 `::char_type` 是一个类型。对于 `string` 的特化，例如，`value_type` 是 `char`。

`size_type` 的用法类似于 `sizeof`，但它返回的是相对于存储类型的字符串大小。对于 `string` 的特化，对于 `char`，`size_type` 与 `size_t` 相同。它是一个无符号类型。`difference_type` 用于测量字符串两个元素之间的距离，以单个元素的大小为单位。通常，它是 `size_type` 的有符号版本。

对于 `char` 特化，`pointer` 是 `char *` 类型，而 `reference` 是 `char&` 类型。然而，如果你为你设计的类型创建特化，这些类型（`pointer` 和 `reference`）将指向与基础指针和引用相同属性的类。

为了让标准模板库（STL）算法与字符串配合，模板定义了一些迭代器：

```cpp
typedef (models random access iterator)     iterator;
typedef (models random access iterator)     const_iterator;
typedef std::reverse_iterator<iterator>      reverse_iterator;
typedef std::reverse_iterator<const_iterator> const_reverse_iterator;
```

# 数据信息、构造函数及其他杂项 1251

模板定义了一个静态常量：

```cpp
static const size_type npos = -1;
```

由于 `size_type` 是无符号的，将值 `-1` 分配给它实际上相当于将最大的可能无符号值分配给 `npos`。该值对应于最大可能数组索引的下一个值。

# 数据信息、构造函数及其他杂项

构造函数可以根据它们产生的影响来描述。由于类的私有部分可能依赖于实现，因此这些影响应以公共接口中可用的信息来描述。表 F1 列出了其返回值可用于描述构造函数和其他方法影响的方法。请注意，其中大部分术语来自 STL。

表 F.1 一些 `string` 数据方法

| Method | Returns |
| --- | --- |
| `begin()` | An iterator to the first character in a string. |
| `cbegin()` | A const_iterator to the first character in a string (C++11). |
| `end()` | An iterator that is the past-end-value. |
| `cend()` | A const_iterator that is the past-end-value (C++11). |
| `rbegin()` | A reverse iterator that is the past-end. |
| `crbegin()` | A reverse const_iterator that is the past-end (C++11). |
| `rend()` | A reverse iterator that refers to the first character. |
| `crend()` | A reverse const_iterator that refers to the first character (C++11). |
| `size()` | The number of elements in a string, to the distance from begin() to end(). |
| `length()` | The same as size(). |
| `capacity()` | The allocated number of elements in a string. This can be greater than the actual number of characters. The value of capacity() - size() represents the number of characters that can be appended to a string before more memory is allocated. |
| `max_size()` | The maximum allowable size of a string. |
| `data()` | A pointer of type const* to the first element of an array whose first size() elements equal the corresponding elements in the string controlled by *this. The pointer should not be assumed to be valid after the string object itself has been modified. |

# 1252 附录 F `string` 模板类

| Table F.1 Some string Data Methods |
| Method | Returns |
| `c_str()` | A pointer of type const char* that points to the first element of an array whose first size() elements the corresponding elements in the string controlled by *this and whose next element is the charT (end-of-string marker) for the char type. The pointer should not be assumed to be valid after the string object itself has been modified. |

`get_allocator()` A copy of the allocator object that is used to allocate memory for the string object.
