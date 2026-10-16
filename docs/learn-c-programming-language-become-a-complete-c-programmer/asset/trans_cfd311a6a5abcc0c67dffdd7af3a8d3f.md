

## 4.5 算法

并将每个唯一向量的元素复制一份放到一个列表中：

```cpp
bool operator<(const Entry& x, const Entry& y) // less than
{
    return x.name < y.name; // order Entries by their names
}
```

```cpp
void f(vector<Entry>& vec, list<Entry>& lst) {
    sort(vec.begin(), vec.end()); // use < for order
    unique_copy(vec.begin(), vec.end(), lst.begin()); // don’t copy adjacent equal elements
}
```

标准算法在第 32 章中描述。它们以元素序列为表达形式。序列由一对迭代器表示，指定第一个元素和最后一个元素之后的元素：

```
iterators: begin() end()

elements:
```

在示例中，`sort()` 对迭代器对 `vec.begin()` 和 `vec.end()` 定义的序列进行排序——恰好是向量的所有元素。对于写入（输出），你只需要指定要写入的第一个元素。如果写入多个元素，则该初始元素之后的元素将被覆盖。因此，为了避免错误，`lst` 必须至少有与 `vec` 中唯一值一样多的元素。

如果我们想将唯一元素放在一个新容器中，我们可以这样写：

```cpp
list<Entry> f(vector<Entry>& vec)
{
    list<Entry> res;
    sort(vec.begin(), vec.end());
    unique_copy(vec.begin(), vec.end(), back_inserter(res)); // append to res
    return res;
}
```

`back_inserter()` 在容器的末尾添加元素，扩展容器以容纳它们（§33.2.2）。因此，标准容器加上 `back_inserter()` 消除了使用易出错的显式 C 风格内存管理使用 `realloc()` 的需求（§31.5.1）。标准库的 `list` 具有移动构造函数（§3.3.2，§17.5.2），使得按值返回 `res` 是高效的（即使对于包含数千个元素的列表也是如此）。

如果你发现像 `sort(vec.begin(), vec.end())` 这样的成对迭代器风格的代码很繁琐，你可以定义算法的容器版本并写成 `sort(vec)`（§4.5.6）。

### 4.5.1 迭代器的使用

当你第一次遇到一个容器时，可以获得一些指向有用元素的迭代器；`begin()` 和 `end()` 就是最好的例子。此外，许多算法返回迭代器。例如，标准算法 `find` 在序列中查找值并返回指向找到元素的迭代器：

```cpp
bool has_c(const string& s, char c) // does s contain the character c?
{
    auto p = find(s.begin(), s.end(), c);
    if (p != s.end())
        return true;
    else
        return false;
}
```

像许多标准库搜索算法一样，`find` 返回 `end()` 表示“未找到”。`has_c()` 的等价、更短的定义是：

```cpp
bool has_c(const string& s, char c) // does s contain the character c?
{
    return find(s.begin(), s.end(), c) != s.end();
}
```

一个更有趣的练习是找到字符串中字符的所有出现位置。我们可以将出现位置的集合作为字符串迭代器的向量返回。返回向量是高效的，因为向量提供移动语义（§3.3.1）。假设我们希望修改找到的位置，我们传递一个非 const 字符串：

```cpp
vector<string::iterator> find_all(string& s, char c) // find all occurrences of c in s
{
    vector<string::iterator> res;
    for (auto p = s.begin(); p != s.end(); ++p)
        if (*p == c)
            res.push_back(p);
    return res;
}
```

我们使用常规循环遍历字符串，使用 `++` 一次移动迭代器 `p` 一个元素，并使用解引用运算符 `*` 查看元素。我们可以这样测试 `find_all()`：

```cpp
void test()
{
    string m {"Mary had a little lamb"};
    for (auto p : find_all(m, 'a'))
        if (*p != 'a')
            cerr << "a bug!\n";
}
```

对 `find_all()` 的该调用可以像这样图形化表示：

```
find_all(m, 'a'):

m: M a r y h a d a l i t t l e l a m b
```

迭代器和标准算法在所有使用它们有意义的标准容器上等价地工作。因此，我们可以对 `find_all()` 泛化：

```cpp
template<typename C, typename V>
vector<typename C::iterator> find_all(C& c, V v) // find all occurrences of v in c
{
    vector<typename C::iterator> res;
    for (auto p = c.begin(); p != c.end(); ++p)
        if (*p == v)
            res.push_back(p);
    return res;
}
```

需要 `typename` 来告知编译器 `C` 的 `iterator` 应该是一个类型，而不是某个类型的数值，例如整数 7。我们可以通过引入类型别名（§3.4.5）来隐藏此实现细节：

```cpp
template<typename T>
using Iterator = typename T::iterator;
```

```cpp
template<typename C, typename V>
vector<Iterator<C>> find_all(C& c, V v)
{
    vector<Iterator<C>> res;
    for (auto p = c.begin(); p != c.end(); ++p)
        if (*p == v)
            res.push_back(p);
    return res;
}
```

我们现在可以写：

```cpp
void test()
{
    string m {"Mary had a little lamb"};
    for (auto p : find_all(m, 'a')) // p is a string::iterator
        if (*p != 'a')
            cerr << "string bug!\n";

    list<double> ld {1.1, 2.2, 3.3, 1.1};
    for (auto p : find_all(ld, 1.1))
        if (*p != 1.1)
            cerr << "list bug!\n";

    vector<string> vs {"red", "blue", "green", "green", "orange", "green"};
    for (auto p : find_all(vs, "green"))
        if (*p != "green")
            cerr << "vector bug!\n";
    for (auto p : find_all(vs, "green"))
        *p = "vert";
}
```

迭代器用于分离算法和容器。算法通过迭代器操作其数据，并且不知道元素存储在哪个容器中。相反，容器不知道在其元素上操作的算法；它所做的只是按请求提供迭代器（例如，`begin()` 和 `end()`）。这种数据存储与算法之间的分离模型提供了非常通用和灵活的软件。

### 4.5.2 迭代器类型

迭代器到底是什么？任何特定的迭代器都是某种类型的对象。然而，存在许多不同的迭代器类型，因为迭代器需要保存执行其工作所需的信息，特别是针对特定容器类型。这些迭代器类型可能与容器和它们服务的专门需求一样不同。例如，`vector` 的迭代器可以是普通指针，因为指针是引用 `vector` 元素的合理方式：

```
iterator: p
vector: P i e t H e i n
```

或者，`vector` 迭代器可以实现为指向 `vector` 的指针加上一个索引：

```
iterator: (start == p, position == 3)
vector: P i e t H e i n
```

使用这样的迭代器可以允许范围检查。

`list` 迭代器必须比简单的元素指针更复杂，因为 `list` 的元素通常不知道该 `list` 的下一个元素在哪里。因此，`list` 迭代器可能是指向链接的指针：

```
iterator: p
list: link link link link ...
elements: P i e t
```

所有迭代器的共同点是它们的语义和操作命名。例如，对任何迭代器应用 `++` 都会产生引用下一个元素的迭代器。类似地，`*` 产生迭代器所引用的元素。事实上，任何遵循这些简单规则的对象都是迭代器（§33.1.4）。此外，用户很少需要知道特定迭代器的类型；每个容器“知道”其迭代器类型，并在约定名称 `iterator` 和 `const_iterator` 下提供它们。例如，`list<Entry>::iterator` 是 `list<Entry>` 的通用迭代器类型。我们很少需要担心该类型是如何定义的细节。

### 4.5.3 流迭代器

迭代器是处理容器中元素序列的通用且有用的概念。然而，容器并不是我们找到元素序列的唯一地方。例如，输入流产生一系列值，我们将一系列值写入输出流。因此，迭代器的概念可以有效地应用于输入和输出。

要创建一个 `ostream_iterator`，我们需要指定将使用哪个流以及写入其中的对象的类型。例如：

```cpp
ostream_iterator<string> oo {cout}; // writes strings to cout
```

对 `*oo` 进行赋值的效果是将所赋的值写入 `cout`。例如：

```cpp
int main()
{
    *oo = "Hello, ";
    ++oo;
    *oo = "world!\n";
}
```

