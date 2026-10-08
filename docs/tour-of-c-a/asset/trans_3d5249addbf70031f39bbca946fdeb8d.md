

# 12 容器

> 它是新的。它是单一的。它是简单的。
它必须成功！
– H. Nelson

- 引言
- vector
- 元素；范围检查
- list
- forward_list
- map
- unordered_map
- 内存分配器
- 容器概述
- 建议

## 12.1 引言

大多数计算都涉及创建值的集合，然后对这些集合进行操作。将字符读入字符串并打印出该字符串就是一个简单的例子。一个主要目的是存储对象的类通常被称为容器。为特定任务提供合适的容器并用实用的基础操作来支持它们，是构建任何程序的的重要步骤。

为了说明标准库容器，考虑一个存储姓名和电话号码的简单程序。对于不同背景的人来说，这种程序的不同方法似乎都是“简单且显而易见的”。可以使用 §11.5 中的 Entry 类来存储简单的电话簿条目。在这里，我们故意忽略了许多现实世界的复杂性，例如电话号码无法简单地表示为 32 位整数。

## 12.2 vector

最常用的标准库容器是 vector。vector 是给定类型元素的序列。元素连续存储在内存中。vector 的典型实现 (§5.2.2, §6.2) 将包含指向第一个元素、最后一个元素之后位置以及最后一个分配空间之后位置 (§13.1) 的指针（或表示为指针加偏移量的等效信息）：

![](img/0bd2e25eba2737c3c5daca16fad1b65b_176_0.png)

此外，它还持有一个内存分配器 (alloc)，vector 可以从那里获取其元素所需的内存。默认分配器使用 `new` 和 `delete` 来获取和释放内存 (§12.7)。通过略有不同的实现技术，我们可以避免在 vector 对象中为简单的分配器存储任何数据。

我们用一组其元素类型的值来初始化 vector：

点击此处查看代码图像

```cpp
vector<Entry> phone_book = {
  "David Hume",123456,
  "Karl Popper",234567,
  "Bertrand Arthur Russell",345678
};
```

可以通过下标操作访问元素。因此，假设我们已经定义了 << Entry，可以写道：

点击此处查看代码图像

```cpp
void print_book(const vector<Entry>& book)
{
  for (int i = 0; i != book.size(); ++i)
    cout << book[i] << "\n";
}
```

通常情况下，索引从 0 开始，所以 `book[0]` 保存了 David Hume 的条目。vector 的成员函数 `size()` 给元素的个数。

vector 的元素构成了一个范围，因此我们可以使用范围-for 循环 (§1.7)：

点击此处查看代码图像

```cpp
void print_book(const vector<Entry>& book)
{
    for (const auto& x : book) // "auto" 参见 §1.4
    cout << x << "\n";
}
```

当我们定义 vector 时，我们给它一个初始大小（初始元素数量）：

点击此处查看图像

| vector<int> v1={1, 2, 3, 4}; | size 为 4 |
| vector<string> v2; | size 为 0 |
| vector<Shape> v3(23); | size 为 23；初始值: nullptr |
| vector<double> v4(32,9); | size 为 32；初始值: 9.9 |

普通括号中用于显式大小，例如 (23)，默认情况下，元素被初始化为元素类型的默认值（例如指针为 nullptr，数字为 0）。如果你不想要默认值，可以作为第二个参数指定它（例如，对于 v4 的元素指定 9.9）。

初始大小是可以改变的。vector 最用的操作之一是 `push_back()`，它在 vector 的末尾添加一个新元素，使其大小增加一。例如，假设我们已经为 Entry 定义了 <<，可以写道：

点击此处查看图像

```cpp
void input()
{
    for (Entry& e; cin>>e);
    book.push_back(e);
}
```

从标准输入读取 Entries 直到结束（例如文件结束）。标准库 vector 的实现使得通过重复 `push_back()` 增长 vector 是高效的。为了增长，考虑第 5 章和第 7 章中的 Vector 实现：

点击此处查看图像

```cpp
template <typename T>
class Vector {
    allocator<T> alloc; // 元素的元素的分配器
    T* elem; // 指向第一个元素
    T* space; // 指向第一个未使用的槽
    T* last; // 指向最后一个槽
public:
    // ...
    int size() const { return space; } // 元素的个数
    int capacity() const { return last; } // 槽的数量
    // ...
    void reserve(int n); // 增加容量
    // ...
    void push_back(const T& t); //拷贝 t 到 Vector
    void push_back(T&& t); // 移动 t 到 Vector
};
```

标准库 vector 有 `capacity()`、`reserve()` 和 `push_back()`。vector 的用户使用 `reserve()` 为更多元素留空间。它可能分配新内存，这样做时，会将元素移动到新的分配空间。这些元素的指针现在将指向错误的位置；它们已失效且不应再使用。考虑到 `capacity()` 和 `reserve()`，实现 `push_back()` 是微不足道的：

```cpp
template<typename T>
void Vector<T>::push_back(const T& t)
{
    if (capacity()<=size())                // 确保有空间
        reserve(size()*2);             // 容量翻倍
    construct(space,t);                   // 将 t 置于 space
    ++size;
}
```

现在分配和迁移发生很少。我曾使用 `reserve()` 来提高性能，但证明是浪费精力：vector 使用的启发式平均要好得多，所以我现在专门使用 `reserve()` 来在想要放入元素时避免重新分配。vector 可以在赋值和初始化中拷贝。例如：

点击此处查看代码图像

```cpp
vector<Entry> book2= phone_book;
```

vector 的拷贝和移动是通过 §6.2 中的构造函数和赋值运算符实现的。拷贝涉及其元素的拷贝。因此，book2 和 phone_book 的初始化持有 Entry 的独立副本。当 vector 有许多元素时，此类重新分配赋值和初始化可能是昂贵的。在不希望拷贝的地方，应该使用引用或指针 (§1.7) 或移动操作 (§6.2)。标准库 vector 非常灵活且高效。它是你的默认容器；除非你有充分理由使用其他容器，否则请使用它。如果你是因为对“效率”有模糊的担心而使用 vector，请进行测量。我们在容器用户性能方面的直觉往往是错误的。

## 12.2.1 元素

与标准库容器一样，vector 是类型 T 元素的容器，即 `vector<T>`。几乎任何类型都可以元素类型（如 char、int 和 double）、用户定义类型（如 string、Entry、list<int> 和 Matrix<double,2>）以及指针（如 char*, Shape 和 double*）。当你插入一个新元素时，它的值会被拷贝到容器中。对于存入容器的整数 7，结果元素确实值 7。元素不是引用或指向对象的指针，这创建了良好的、紧凑且访问快速的容器。对于内存大小和运行时性能的人来说，这是关重要的。

如果你有一个依赖虚函数获取多态行为的类层次 (§5.5)，不要直接在容器中存储对象。相反，存储指针（或智能指针；§15.2.1）。例如：

点击此处查看代码图像

```cpp
vector<Shape> vs;
vector<Shape*> vps;
vector<unique_ptr<Shape>> vps;
```

| 不，没有存放 Circle 或 Smiley 的空间 (§5.5) | 更好，但请参见 §5.5.3 (不要泄漏) |
| OK |

## 12.2.2 范围检查

标准库 vector 不保证范围检查。例如：

点击此处查看代码图像

```cpp
void silly(vector<Entry>& book) {
    int i = book[book.size()].number;
    // ...
}
```

| book.size() 超出范围 | 那种初始化是在 i 中放置某个随机值而不是给出错误。这是不可取的，且越界错误是常见问题。因此，我经常使用 vector 的简单范围检查适配：

点击此处查看代码图像

```cpp
template<typename T>
struct Vec {
    vector<T> vec;
    using vector<T>::vector;

    T& operator[](int i) { return vec.at(i); }
    const T& operator[](int i) const { return vec.at(i); }

    auto begin() { return checked_iter<vector<T>>(*this).begin(); }
    auto end() { return checked_iter<vector<T>>(*this).end(); }
};
```

| 使用 vector 的构造函数（重名为 Vec） | 范围检查 |
| const 对象的范围检查；5.2.1 |
| 参见 §13.1 |

Vec 继承了 vector 除它重定义以进行范围检查的下标操作之外的所有内容。`at()` 是在参数不在 vector 范围内时抛出 out_of_range 类型异常的操作 ($4.2)。对于 Vec，越界访问将抛出一个用户可以捕获的异常。例如：

```cpp
void checked(Vec<Entry>& book) {
    try {
        book[book.size()] = {"Joe", 999999};
        // ...
    } catch (const out_of_range& e) {
        cerr << "range error";
    }
}
```

它将抛出一个异常

