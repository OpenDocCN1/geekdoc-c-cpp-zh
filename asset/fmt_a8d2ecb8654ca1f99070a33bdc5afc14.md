
```cpp
ifstream ifs("source"); // "i" 代表 "input"
if (!ifs)
    error("couldn't open 'source'");
```

假设 `ofs` 可以当作普通的 `ostream` 使用（就像 `cout` 一样），而 `ifs` 可以当作普通的 `istream` 使用（就像 `cin` 一样）。

可以进行文件定位以及对文件打开方式进行更详细的控制，但这超出了本书的范围。

对于文件名的组合和文件系统操作，请参见 §11.9。

### 11.7.3 字符串流

在 `sstream` 中，标准库提供了在字符串之间传输的流：

- `stringstream`：用于从字符串读取
- `ostringstream`：用于向字符串写入
- `stringstream`：用于对字符串进行读取和写入。

例如：

```cpp
void test() {
    ostringstream oss;
    oss << "temperature," << scientific << 123.4567890 << "";
    cout << oss.view() << "in";
}
```

可以使用 `str()`（内容的字符串拷贝）或 `view()`（内容的 `string_view`）读取 `ostringstream` 的内容。`ostringstream` 的一个常见用途是在将结果字符串交给 GUI 之前进行格式化。同样，从 GUI 接收到的字符串可以通过将其放入 `stringstream` 中并使用格式化输入操作 (§11.3) 来读取。

`stringstream` 可可用于读取和写入。例如，我们可以定义一种操作，将任何带有字符串的类型转换为也可以表示为字符串的其他表示：

```cpp
template<typename Target=string, typename Source=string>
Target(Source arg) // 将 Source 转换为 Target
{
    stringstream buf;
    Target result;

    if (!(buf << arg) // 将 arg 流
        || !(buf >> result) // 从流中读取 result
        || (!(buf == std::eof())) // 如果流中还有任何东西？
            throw runtime_error("to<T>() failed");

    return result;
}
```

只有当模板参数无法推导或没有默认值时 (§8.2.4) 才需要提到它，我们可以写：

```cpp
auto x1 = to<string,double>(1.2); // 非常明确（且冗长）
auto x2 = to<string>(1.2); // Source 被推导为 double
auto x3 = to<int>(1.2); // Target 默认为 string；Source 被推导为 double
auto x4 = to(1.2); // < 是多余的；Target 默认为 string；Source 被推导为 double
```

如果所有函数参数都被推导，则可以省略 `<`。我认为这是一个通过语言特性和标准库设施相结合实现通用性和易用性的良好示例。

### 11.7.4 内存流

如果我们直接使用流的缓冲区或用于其他输出设备的缓冲区，这在性能上就会变得有趣：

### 11.7.5 同步流

在多线程环境中，并发可能是很棘手的，请小心

## 11.8 C 风格 I/O

标准库也支持 `printf()` 和 `scanf()`。许多程序员为了性能更喜欢这些。

## 11.9 文件系统

大多数系统都有文件系统的概念，用于访问存储在文件信息。遗憾的是，文件系统的属性和操作方法差异很大。为了处理这些，`<filesystem>` 库提供了一个统一的接口。使用 `<filesystem>`，我们可以表示文件路径并遍历文件系统，检查文件类型以及关联的权限。

文件库可以处理 Unicode，但说明如何超出本书范围。我建议使用 cppreference [Cppreference] 和 Boost 文档 [Boost] 获取详细信息。

### 11.9.1 路径

考虑一个示例：

```cpp
path f = "dir/hypothetical/f"; // 命名文件

assert(exists(f)); // f 必须存在

if (is_regular_file(f)) // f 是普通文件吗？
    cout << f << " is a file; its size is " << file_size(f) << " "\n";
```

注意操作文件系统的程序通常与其他程序一起运行。然而，文件系统的内容在程序之间可能会发生。例如，尽管我们首先断言 f 存在，但在下一行可能不再成立，我们仍然询问它是否为普通文件。

路径 是一个什么样的对象类，能够处理各种字符集和许多操作。特别是，它可以处理来自 `main()` 呈现的命令行文件名；例如：

```cpp
int main(int argc, char* argv[]) {
    if (argc < 2) {
        cout << "arguments expected\n";
        return 1;
    }

    path p(argv[1]); // 从命令行创建路径

    cout << p << " " << exists(p) << " "\n";
    // 注意：路径可以像字符串一样打印
    // ...
}
```

路径在被使用之前不会对其有效性进行检查。即便是如此，其有效性也取决于运行该程序的系统约定。

自然地，可以使用路径来打开文件。

```cpp
void use(path p)
{
    ofstream f(p);
    if (!f) error("bad file name: ", p);
    f << "Hello, file";
}
```

除了 `path` 之外，`<filesystem>` 还提供了用于遍历目录和查询所用文件属性的类型：

## 文件系统类型（部分）

| path | 目录路径 |
|---|---|
| filesystem_error | 文件系统异常 |
| directory_entry | 目录条目 |
| directory_iterator | 用于遍历目录 |
| recursive_directory_iterator | 用于遍历目录及其子目录 |

考虑一个简单但并非不实际的示例：

```cpp
void print_directory(path p) // 打印 p 中所有文件的名称
{
    if (is_directory(p)) {
        cout << p << "\n";
        for (const directory_entry& x : directory_entry(p)) {
            cout << " " << x << "\n";
        }
    }
}
catch (const filesystem_error& ex) {
    cerr << ex.what() << "\n";
}
```

字符串可以隐式转换为 `path`，因此我们可以这样练练 `print_directory`：

```cpp
void use()
{
    print_directory(""); // 当前目录
    print_directory("..."); // 父目录
    print_directory("/"); // Unix 根目录
    print_directory("c:"); // Windows C 卷
    for (string s; cin>>s);
    print_directory(s);
}
```

如果我想列出子目录，我会使用 `recursive_directory_iterator(p)`。如果我想按字典顺序打印条目，我将把路径复制到 `vector` 中并在打印之前进行排序。`path` 类提供了许多常用且实用的操作：

| 路径操作（部分） | p 和 p2 |
|---|---|
| value_type | 用于文件系统的原生编码：POSIX 上为 `char`，Windows 上为 `wchar_t` |
| string_type | `basic_string<value_type>` |
| const_iterator | `const_iterator` 的别名 |
| iterator | p=p2 : 将 p2 赋值给 p |
| /=p2 | p 和 p2 使用文件名分隔符（默认认为 `/`）拼接 |
| p+=p2 | p 和 p2 拼接（无分隔符） |
| s=p.native() | p 的原生格式的引用 |
| s=p.string() | 原生格式的字符串 |
| s=p.generic_string(p) | 通用格式的字符串 |
| p2=filename() | p 的文件名 |
| p2=extension() | p 的扩展名部分 |
| i=begin() | p 元素序列的起始迭代器 |
| i=end() | p 元素序列的结束迭代器 |
| p2=p1, p1=p2 | p 和 p2 的相等与不相等判断 |
| p2<p1, p1<p2>p1 | 字典序比较 |
| p2=p2 | 到/从 p 的流 I/O |
| iss>>p, os<<p | |
| upath(s) | 来自 UTF-8 源 s 的路径 |

```cpp
if (is_directory(p)) {
    cout << f.stem() << " 是一个 Windows 可执行文件\n";
} else {
    string n = f.extension().string();
    if (n == ".cpp" || n == ".cc") {
        cout << f.stem() << " 是一个 C++ 文件\n";
    }
}
```

# 12 容器

> 它是新的。它是单一的。它是简单的。
> 它必须成功！
> – H. Nelson

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

```cpp
vector<Entry> phone_book = {
  "David Hume",123456,
  "Karl Popper",234567,
  "Bertrand Arthur Russell",345678
};
```

可以通过下标操作访问元素。因此，假设我们已经定义了 << Entry，可以写道：

```cpp
void print_book(const vector<Entry>& book)
{
  for (int i = 0; i != book.size(); ++i)
    cout << book[i] << "\n";
}
```

通常情况下，索引从 0 开始，所以 `book[0]` 保存了 David Hume 的条目。vector 的成员函数 `size()` 给元素的个数。

vector 的元素构成了一个范围，因此我们可以使用范围-for 循环 (§1.7)：

```cpp
void print_book(const vector<Entry>& book)
{
    for (const auto& x : book) // "auto" 参见 §1.4
    cout << x << "\n";
}
```

当我们定义 vector 时，我们给它一个初始大小（初始元素数量）：

| vector<int> v1={1, 2, 3, 4}; | size 为 4 |
| vector<string> v2; | size 为 0 |
| vector<Shape> v3(23); | size 为 23；初始值: nullptr |
| vector<double> v4(32,9); | size 为 32；初始值: 9.9 |

普通括号中用于显式大小，例如 (23)，默认情况下，元素被初始化为元素类型的默认值（例如指针为 nullptr，数字为 0）。如果你不想要默认值，可以作为第二个参数指定它（例如，对于 v4 的元素指定 9.9）。

初始大小是可以改变的。vector 最用的操作之一是 `push_back()`，它在 vector 的末尾添加一个新元素，使其大小增加一。例如，假设我们已经为 Entry 定义了 <<，可以写道：

```cpp
void input()
{
    for (Entry& e; cin>>e);
    book.push_back(e);
}
```

从标准输入读取 Entries 直到结束（例如文件结束）。标准库 vector 的实现使得通过重复 `push_back()` 增长 vector 是高效的。为了增长，考虑第 5 章和第 7 章中的 Vector 实现：

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

```cpp
vector<Entry> book2= phone_book;
```

vector 的拷贝和移动是通过 §6.2 中的构造函数和赋值运算符实现的。拷贝涉及其元素的拷贝。因此，book2 和 phone_book 的初始化持有 Entry 的独立副本。当 vector 有许多元素时，此类重新分配赋值和初始化可能是昂贵的。在不希望拷贝的地方，应该使用引用或指针 (§1.7) 或移动操作 (§6.2)。标准库 vector 非常灵活且高效。它是你的默认容器；除非你有充分理由使用其他容器，否则请使用它。如果你是因为对“效率”有模糊的担心而使用 vector，请进行测量。我们在容器用户性能方面的直觉往往是错误的。

### 12.2.1 元素
