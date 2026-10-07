
### `vector` 基础

```
void print_book(const vector<Entry>& book)
{
  for (int i = 0; i!=book.size(); ++i) 
    cout << book[i] << '\n';
  }
```

像通常一样，从 0 开始，因此 `book[0]` 持有 David Hume 的条目。`vector` 函数 `size(0)` 给出元素的数量。

`vector` 的元素构成一个范围，因此我们可以使用 `range-for` 循环（§1.7）：

```
void print_book(const vector<Entry>& book)
{
  for (const auto &x : book) 
    cout << x << ' "auto" see §1.4';
  }
```

当我们定义一个 `vector` 时，我们给它指定一个初始大小（初始元素数量）：

```
vector<int> v1 = {1, 2, 3, 4};
vector<string> v2;
vector<Shape> v3(23);
vector<double> v4(32,9.9);
```

显式的大小包含在括号中，`(23)`，默认情况下，元素被初始化为元素类型的默认值（例如指针的 `nullptr` 和数字的 `0`）。如果你不想要默认值，可以作为第二个参数指定一个（例如为 32 个元素的 `v4` 指定 `9.9`）。

初始大小可以改变。对 `vector` 最有用的操作之一是 `push_back()`，它将一个新元素添加到 `vector` 的末尾，使其大小增加 1。例如，假设我们已经为 `Entry` 定义了 `>>`，我们可以写：

```
void input() {
    for (Entry e : ele);
        phone_book.push_back(e);
}
```

这从标准输入读取 `Entry` 到 `phone_book`，直到到达输入结束（例如文件末尾）或输入操作遇到错误。

标准库 `vector` 的实现使得通过重复的 `push_back()` 扩展 `vector` 是高效的。为了展示这一点，考虑对第 5 章和第 7 章中的简单 `Vector` 进行详细说明，使用如下图所示的表示：

```
template<typename T> alloc;
class Vector {
    allocator alloc_; // Ts 的标准库分配器
    T* ele; // 指向第一个元素的指针
    T* space; // 指向第一个未使用（空）槽位的指针
    T* last; // 指向最后一个槽位的指针
public:
    // ...
    int size() const { return last-ele; } // 元素数量
    int capacity() const { return last-ele; } // 可用槽数量
    // ...
    void reserve(int newsz); // 将容量增加到 newsz
    // ...
    void push_back(const T& t); // 将 t拷贝到 Vector
    void push_back(T&& t); // 将 t移动到 Vector
```

标准库 `vector` 拥有 `capacity()`、`reserve()` 和 `push_back()`。`reserve()` 方法分配新内存以容纳更多元素。它可能分配新内存，当这样做时，它将元素移动到新的分配空间。当 `reserve()` 将元素移动到更大的分配空间时，指向这些元素的任何指针将指向错误位置；它们会失效且不应使用。

给定 `capacity()` 和 `reserve()`，实现 `push_back()` 是轻而易见的：

```
template<typename>::push_back(T& t)
{
    if (capacity()<=size()) // 确保有空间给 t
        reserve(size()=0?8:2+size()); // 容量翻倍
    construct_at(space, t); // 初始化空间 t（放在空间中）
    ++space;
}
```

现在元素的分配和移动很少发生。以前使用 `reserve()` 来尝试提高性能，但事实证明浪费精力：`vector` 的启发式比我的猜测更好，因此现在我显式地使用 `reserve()` 在需要元素赋值和初始化时避免重新分配。

`vector` 可以在赋值和初始化中拷贝。例如：

```
vector<Entry> book2 = ...
```

拷贝和移动在 6.2 中描述。标准库 `vector` 非常高效。将其作为默认值使用（§12.7）。如果你不想要默认值，可以作为第二个参数指定一个（例如为 32 个元素的 `v4` 指定 `9.9`）。

初始大小可以改变。对 `vector` 最有用的操作之一是 `push_back()`，它将一个新元素添加到 `vector` 的末尾，使其大小增加 1。例如，假设我们已经为 `Entry` 定义了 `>>`，我们可以写：

```
void input() {
    for (Entry e : ele);
        phone_book.push_back(e);
}
```

这从标准输入读取 `Entry` 到 `phone_book` 直到输入结束（例如文件末尾）或输入操作遇到错误。

标准库 `vector` 的实现使得通过重复 `push_back()` 扩展 `vector` 是高效的。为了展示这一点，使用如下所示的表示对第 5 章和第 7 章中的简单 `Vector` 进行详细说明：

```
template<typename T> alloc;
class Vector {
    allocator alloc_; // Ts 的标准库分配器
    T* ele; // 指向第一个元素的指针
    T* space; // 指向第一个未使用（空）槽位的指针
    T* last; // 指向最后一个槽位的指针
public:
    // ...
    int size() const { return last-ele; } // 元素数量
    int capacity() const { return last-ele; } // 可用槽数量
    // ...
    void reserve(int newsz); // 将容量增加到 newsz
    // ...
    void push_back(const T& t); // 将 t拷贝到 Vector
    void push_back(T&& t); // 将 t移动到 Vector
```

### 12.2.2 范围检查

标准库 `vector` 不保证范围检查。例如：

```
void silly(vector<Entry>&) {
    int i = book(size()); // book.size() 超出范围
    // ...
}
```

这种初始化在 `i` 中留下了某些随机值而不是，并且越界错误是一个常见问题。因此，我经常使用 `vector` 的简单范围检查适配器：

```
template<typename T>
struct Vec : std::vector<T> {
    using vector<T>::vector; // 使用 vector 的构造函数（命名为 Vec）
    T& operator[](int i) { return vector<T>::at(i); } // 范围检查
    const T& operator[](int i) const { return vector<T>::at(i); } // 范围检查$5.2.1
    auto begin() { return Checked_iter<vector<T>>(this); } // 见 $13.1
    auto end() { return Checked_iter<vector<T>>(this, vector<T>::end()); }
}
```

`Vec` 继承 `vector` 的所有内容，除了重定义为范围检查的下标运算符。`at()` 操作在参数超出 `vector` 范围时抛出异常（4.2）。对于 `Vec`，越界访问将抛出一个用户可以捕获的异常。例如：

```
void checked(Vec& book) {
    try {
        book[book.size()] = {"Joe",999999}; // 会抛出异常
        // ...
    } catch (out_of_range& e) {
        cerr << "range error\n";
    }
}
```

异常将被抛出并被捕获（4.2）。如果用户不捕获异常，程序将定义的方式终止，而不是以未定义的方式继续或失败。要尽量减少未捕获异常带来的意外，是使用一个带有 `try` 块作为体的 `main()`。例如：

```
int main() {
    try {
        // 你的代码
    }
}
```

# 容器

```cpp
catch (out_of_range) {
    cerr << "range error\n";
}
catch (...) {
    cerr << "unknown exception thrown\n";
}
```

如果我们未能捕获到任何异常，这提供了默认的句程序，错误消息将打印在标准错误诊断输出流 `cerr` 上 (§11.2)。

为什么标准不保证范围检查呢？许多对性能敏感的应用程序使用 `vector`，而检查所有的下标访问意味着大约 10% 左右的开销。显然，这种开销由于硬件、优化以及订阅选项而发生巨大变化。然而，经验表明，这种开销会导致人们害怕使用更不安全的数组。即使是对这种开销的恐惧也可能导致灭亡。至少 `vector` 在调试时可以容易地进行范围检查，我们可以在未检查的默认版本之上构建经过检查的版本。

`range-for` 循环通过简单访问范围内的所有元素，零成本地避免了范围错误。由于它们的参数是有效的，标准库会执行相同的操作以确保没有范围错误。

如果你在代码中直接使用 `vector::at()`，你就不需要 `Vec` 的替代方案。此外，某些标准库提供了范围检查的 `vector` 实现，它们提供了比 `Vec` 更完整的检查。

## 12.3 list（列表）

标准库提供了一个双向链表 `list`：

![](img/c00e25f90ff6ca6a5619b7dcdafeb9db_174_0.png)

对于我们想要插入和删除元素而不移动其他元素的序列，我们使用 `list`。电话簿条目的插入和删除可能是常见的，`list` 可能适用于表示一个简单的电话簿。

```cpp
list<Entry> phone_book = {
    {"David Hume", 123456},
    {"Karl Popper", 234567},
    {"Bertrand Arthur William Russell", 345678}
};
```

当我们使用链表时，我们通常不会像 `vector` 那样频繁地通过下标访问元素。相反，我们在列表中查找具有给定值的元素。为了做到这一点，我们利用了 `list` 是第 13 节描述的序列这一事实：

## 第 12.3 节

```cpp
int get_number(const string &s)
{
    for (const auto &x : phone_book)
        if (x.name==s)
            return x.number;
    return 0; // 使用 0 表示“未找到号码”
}
```

对 `s` 的搜索从列表开始，一直持续到找到 `s` 或到达 `phone_book` 的末尾。

有时，我们需要识别列表中的一个元素。例如，我们可能想要删除一个元素或在其之前插入一个新元素。为了做到这一点，我们使用迭代器：`list` 标识列表中的一个元素并可以用于遍历列表（因此得此名）。每个标准库容器都提供了 `begin()` 和 `end()`，它们分别返回指向第一个元素和指向最后一个元素之后元素的迭代器 (§13.1)。通过显式使用迭代器，我们可以以这种不那么优雅的方式编写 `get_number()` 函数：

```cpp
int get_number(const string &s)
{
    for (auto p = phone_book.begin(); p!=phone_book.end(); ++p)
        if (p->name==s)
            return p->number;
    return 0; // 使用 0 表示“未找到号码”
}
```

事实上，这大致是编译器实现更短和更简单的 `range-for` 循环的方式。在迭代 `p` 时，`*p` 是它所引用的元素，`++p` 使 `p` 进阶以指向下一个元素，而当 `p` 指向一个具有成员 `m` 的类时，`p->m` 等同于 `(*p).m`。向列表中添加元素和从列表中移除元素是很容易的：

```cpp
void f(const Entry &e, list<Entry>::iterator p, list<Entry>::iterator q)
{
    phone_book.insert(p, e); // 在 p 指向的元素之前添加 e
    phone_book.erase(q); //  q 指向的元素
}
```

对于 `list`，`insert(p,elem)` 在由 `p` 指向的元素之前插入一个值为 `elem` 的元素。`p` 可能是一个指向列表末尾之外的迭代器。相反，`erase(p)` 移除 `p` 指向的元素并销毁它。

这些示例可以使用 `vector` 以相同的方式编写，而且令人惊讶的是，由于机器架构的原因，`vector` 的性能通常比 `list` 更好。当人们想要一个元素序列时，我们可以在使用 `vector` 和 `list` 之间进行选择。除非你有理由不使用它，否则 `vector` 在遍历（例如 `find(i)` 和 `count(j)`）以及排序和搜索（例如 `sort(i)` 和 `equal_range()`）方面表现得更好 (§13.5, §15.3)。

## 12.4 forward_list（单向链表）

标准库还提供了一种名为 `forward_list` 的单向链表：

`forward_list`:

![](img/c00e25f90ff6ca6a5619b7dcdafeb9db_174_0.png)

`forward_list` 与双向链表的区别在于只允许向前移动。由于其参数是有效的，标准库执行相同的操作以确保没有范围错误。`forward_list` 的目的是为了节省空间。

## 12.5 map（映射）

在某些上下文中，我们需要在映射中标识一个元素。例如，我们可能想要删除一个元素或在其之前插入一个新元素。为了做到这一点，我们使用迭代器：`map` 标识映射中的一个元素并可以用于遍历映射（因此得此名）。每个标准库容器都提供了 `begin()` 和 `end()`，它们分别返回指向第一个元素和指向最后一个元素之后元素的迭代器 (§13.1)。通过显式使用迭代器，我们可以以这种不那么优雅的方式编写 `get_number()` 函数：

```cpp
int get_number(const string &s)
{
    for (auto p = phone_book.begin(); p!=phone_book.end(); ++p)
        if (p->first==s)
            return p->second;
    return 0; // 使用 0 表示“未找到号码”
}
```

编写在映射中查找元素是繁琐的。标准库提供了一个平衡树（通常是红黑树）作为：

`map`:

![](img/c00e25f90ff6ca6a5619b7dcdafeb9db_174_0.png)

对于 `map`，我们使用键值对。电话簿条目的插入和删除可能是常见的，一个映射适用于：

```cpp
map<string, int> phone_book = {
    {"David Hume", 123456},
    {"Karl Popper", 234567},
    {"Bertrand Arthur William Russell", 345678}
};
```

对 `s` 的搜索从映射的开始，一直持续到找到 `s` 或到达 `phone_book` 的末尾。

有时，我们需要识别映射中的一个元素。例如，我们可能想要删除一个元素或在其之前插入一个新元素。为了做到这一点，我们使用迭代器：`map` 标识映射中的一个元素并可以用于遍历映射（因此得此名）。每个标准库容器都提供了 `begin()` 和 `end()`，它们分别返回指向第一个元素和指向最后一个元素之后元素的迭代器 (§13.1)。通过显式使用迭代器，我们可以以这种不那么优雅的方式编写 `get_number()` 函数：

```cpp
int get_number(const string &s)
{
    for (auto p = phone_book.begin(); p!=phone_book.end(); ++p)
        if (p->first==s)
            return p->second;
    return 0; // 使用 0 表示“未找到号码”
}
```

## 12.6 unordered_map（哈希映射）

标准库还提供了一种名为 `unordered_map` 的哈希表：

`unordered_map`:

![](img/c00e25f90ff6ca6a5619b7dcdafeb9db_174_0.png)
