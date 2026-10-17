
```cpp
auto x = 123;     // x 是一个 int
auto c = 'y';     // c 是一个 char
auto& r = x;      // r 是一个 int&
auto y = r;       // y 是一个 int（引用被隐式解引用）
```

请注意，字符串字面量的类型是 `const char*`，因此对字符串字面量使用 `auto` 可能会导致不愉快的意外：

```cpp
auto s1 = "San Antonio";       // s1 是一个 const char*（意外吗？！）
string s2 = "Fredricksburg";   // s2 是一个 string
```

当我们确切知道想要的类型时，使用 `auto` 往往和直接指定类型一样容易。

使用 `auto` 的常见用途之一是指定范围-`for`-循环中的循环变量。考虑：

```cpp
template<typename C>       // 要求 Container<T>
void print3(const C& cont)
{
    for (const auto& x : cont)
        cout << x << "\n";
}
```

在这里，我们使用 `auto`，因为为容器 `cont` 的元素类型命名并不那么简单。我们使用 `const`，因为我们不会写入容器元素，并且使用 `&`（引用），以防元素过大而导致复制成本过高。

## 20.6 一个例子：简单的文本编辑器

列表的基本特性是你可以添加和删除元素，而无需移动列表中的其他元素。让我们尝试一个简单的示例来说明这一点。考虑一下如何在简单的文本编辑器中表征文本文档中的字符。表征方式应使对文档的操作简单且效率合理。

哪些操作？假设文档能装入计算机的主内存中。这样，我们可以选择任何适合我们的表征方式，并在想要将其存储到文件时简单地将其转换为字节流。类似地，我们可以从文件中读取字节流，并将其转换为我们内存中的表征方式。决定了这一点后，我们可以专注于选择一个方便的内存表征方式。基本上，有五种事情是我们的表征方式必须很好地支持的：

- 从输入的字节流构建它

- 插入一个或多个字符

- 删除一个或多个字符

- 搜索字符串

- 为输出到文件或屏幕生成字节流

最简单的表征方式将是 `vector<char>`。然而，要添加或删除一个字符，我们将不得不移动文档中每个后续字符。考虑：

> This is he start of a very long document.

> There are lots of . . .

我们可以添加所需的 `t` 以获得

> This is the start of a very long document.

> There are lots of . . .

然而，如果这些字符存储在单个 `vector<char>` 中，我们将不得不从 `h` 开始的每个字符向右移动一个位置。这可能涉及大量的复制。事实上，对于一个长 70,000 个字符的文档（如此章节，包括空格），插入或删除一个字符时，平均需要移动 35,000 个字符。由此产生的实时延迟可能会明显且令用户烦恼。因此，我们将表征方式“分解”为“块”，以便在不移动大量字符的情况下更改文档的一部分。我们将文档表征为“行”列表 `list<Line>`，其中 `Line` 是 `vector<char>`。例如：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_767_0.png)

现在，当我们插入那个 `t` 时，我们只需移动该行上其余的字符。此外，当我们需要时，我们可以添加一行而无需移动任何字符。例如，我们可以在 `document.` 之后插入 `This is a new line.` 以获得

```
This is the start of a very long document.
This is a new line.
There are lots of . . .
```

我们只需要在中间插入一个新“行”：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_767_1.png)

逻辑上，能够插入新链接而不移动现有链接之所以重要，是因为我们可能有指向这些链接的迭代器或指针（以及引用）指向这些链接中的对象。这样的迭代器和指针不受行的插入或删除的影响。例如，字处理器可以保持一个 `vector<list<Line>::iterator>`，持有指向当前 `Document` 中每个标题和副标题开头的迭代器：

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_768_0.png)

我们可以向“段落 20.2”添加行，而不会使指向“段落 20.3”的迭代器失效。

总之，出于逻辑和性能原因，我们使用行**列表**而不是行**向量**或所有字符的**向量**。请注意，这些原因适用的情况相当罕见，因此“默认使用 `vector`”的经验法则仍然成立。你需要特定的理由来优先选择 `list` 而不是 `vector` – 即使你认为你的数据是元素列表！（参见 §20.7）列表是一个逻辑概念，你可以在程序中将其表征为（链接）`list`或`vector`。与我们日常概念中的列表（例如，待办事项列表、杂货清单或日程表）最接近的 STL 类似物是序列，大多数序列最好表征为 `vector`。

### 20.6.1 行

我们如何决定文档中的“行”是什么？有三个明显选择：

1. 依赖用户输入中的换行符（例如，`\n`）。

2. 以某种方式解析文档并使用某些“自然”标点符号（例如，`.`）。

3. 将超过给定长度（例如，50 个字符）的任何一行分成两行。

无疑还有一些不太明显的选择。为了简单起见，我们在这里使用替代方案 1。

我们将编辑器中的文档表征为类 `Document` 的对象。去除了所有修饰，我们的文档类型看起来像这样：

```cpp
using Line = vector<char>;        // 一行是字符向量

struct Document {
    list<Line> line;              // 文档是行的列表
    Document() { line.push_back(Line{}); }
};
```

每个 `Document` 都以一个空行开始：`Document` 的构造函数创建一个空行并将其压入行的列表中。读取和拆分行可以像这样完成：

```cpp
istream& operator>>(istream& is, Document& d)
{
    for (char ch; is.get(ch); ) {
        d.line.back().push_back(ch);        // 添加字符
        if (ch=='\n')
            d.line.push_back(Line{});       // 添加另一行
    }
    if (d.line.back().size()) d.line.push_back(Line{}); // 添加最后的空行
    return is;
}
```

`vector` 和 `list` 都有一个成员函数 `back()`，它返回最后一个元素的引用。要使用它，你必须确实存在最后一个元素供 `back()` 引用 – 不要在对空容器上使用它。这就是为什么我们定义 `Document` 以一个空 `Line` 结束的原因。注意，我们存储来自输入的每个字符，即使是换行符（`"\n"`）。存储这些换行符极大地简化了输出，但你必须小心如何定义字符计数（仅计算字符会给出包含空格和换行符的数字）。

### 20.6.2 迭代

如果文档只是一个 `vector<char>`，迭代它将很简单。我们如何迭代行列表？显然，我们可以使用 `list<Line>::iterator` 迭代列表。但是，如果我们想要按顺序访问字符，而不必担心换行符怎么办？我们可以提供一个专门为我们的 `Document` 设计的迭代器：

```cpp
class Text_iterator {  // 跟踪行和行内字符位置
    list<Line>::iterator ln;
    Line::iterator pos;
public:
    // 将迭代器启动于行 ll 的字符位置 pp：
    Text_iterator(list<Line>::iterator ll, Line::iterator pp)
        :ln(ll), pos(pp) { }

    char& operator*() { return *pos; }
    Text_iterator& operator++();
    bool operator==(const Text_iterator& other) const;
    bool operator!=(const Text_iterator& other) const;
};
```

```cpp
bool Text_iterator::operator==(const Text_iterator& other) const
{
    return ln==other.ln && pos==other.pos;
}
bool Text_iterator::operator!=(const Text_iterator& other) const
{
    return !(*this==other);
}
```

```cpp
Text_iterator& Text_iterator::operator++()
{
    ++pos; // 移动到下一个字符
    if (pos==(*ln).end()) {
        ++ln; // 移动到下一行
        pos = (*ln).begin(); // 如果 ln==line.end() 则无效；所以确保它不是
    }
    return *this;
}
```

为了使 `Text_iterator` 有用，我们需要为类 `Document` 配备传统的 `begin()` 和 `end()` 函数：

```cpp
struct Document {
    list<Line> line;
    Text_iterator begin() // 第一行的第一个字符
    {
        return Text_iterator(line.begin(), (*line.begin()).begin());
    }
    Text_iterator end() // 最后一行的最后一个字符之后一个位置
    {
        auto last = line.end();
        --last; // 我们知道文档不为空
        return Text_iterator(last, (*last).end());
    }
};
```

我们需要奇特的 `(*line.begin()).begin()` 表示法，因为我们要 `line.begin()` 所指内容的开头；或者我们可以使用 `line.begin()->begin()`，因为标准库迭代器支持 `->`。

现在我们可以通过这种方式迭代文档中的字符：

```cpp
void print(Document& d)
{
    for (auto p : d) cout << p;
}

print(my_doc);
```

### 展示文档与迭代

将文档表示为字符序列在许多方面都有用，但我们通常会在文档中查找比单个字符更具体的内容。例如，下面是一段用于删除第 `n` 行的代码：

```c++
void erase_line(Document& d, int n)
{
    if (n<0 || d.line.size()-1<=n) return;
    auto p = d.line.begin();
    advance(p,n);
    d.line.erase(p);
}
```

调用 `advance(p,n)` 会将迭代器 `p` 向前移动 `n` 个元素；`advance()` 是标准库函数，但我们可以自己实现它，如下所示：

```c++
template<typename Iter>    // requires Forward_iterator<Iter>
void advance(Iter& p, int n)
{
    while (0<n) { ++p; --n; }
}
```

请注意，`advance()` 可用于模拟下标访问。实际上，对于一个名为 `v` 的 `vector`，`p=v.begin`；`advance(p,n)`；`p=x` 大致等同于 `v[n]=x`。注意，“大致”意味着 `advance()` 费力地逐个跳过前 `n-1` 个元素，而下标访问直接跳转到第 `n` 个元素。对于 `list`，我们必须使用这种费力的方法。这是为了获得 `list` 元素更灵活的布局所必须支付的成本。

对于可以向前和向后移动的迭代器，例如 `list` 的迭代器，标准库 `advance()` 的负参数会使迭代器向后移动。对于可以处理下标访问的迭代器，例如 `vector` 的迭代器，标准库 `advance()` 会直接跳到正确的元素，而不是使用 `++` 缓慢地移动。显然，标准库的 `advance()` 比我们的实现更智能。这一点值得注意：通常，标准库设施投入了更多的精力和时间，超出了我们所能负担的范围，因此应优先使用标准设施而非“自制”方案。

### 尝试一下

![](img/e0ceba017429f80f5cf63e81a1e7ef4f_771_0.png)

重写 `advance()`，使其在提供负参数时能够“向后移动”。

## 搜索迭代

可能，搜索是用户最直观的一种迭代方式。我们搜索单个单词（例如 `milkshake` 或 `Gavin`），搜索不容易被视为单词的字母序列（例如 `secret` 后接下一行的 `homestead`），搜索正则表达式（例如 `[bB]\w*\ne` – 即一个大写或小写的 `B` 后跟 0 个或多个字母，再后跟 `ne`；参见第 23 章），等等。让我们展示如何处理第二种情况，即在 `Document` 布局中寻找字符串。我们使用一个简单的 – 非最优的 – 算法：

- 在文档中找到搜索字符串的第一个字符。

- 检查该字符及其后续字符是否匹配我们的搜索字符串。

- 如果匹配，则完成；如果不匹配，则查找该第一个字符的下一个出现位置。

为了通用性，我们采用 STL 惯例，将搜索文本定义为由一对迭代器定义的序列。这样，我们可以将搜索函数用于文档的任何部分以及完整文档。如果我们在文档中找到字符串的出现位置，我们返回指向其第一个字符的迭代器；如果我们未找到出现位置，我们返回指向序列末尾的迭代器：

```cpp
Text_iterator find_txt(Text_iterator first, Text_iterator last, const string& s)
{ 
    if (s.size()==0) return last;  // 找不到空字符串
    char first_char = s[0];
    while (true) {
        auto p = find(first,last,first_char);
        if (p==last || match(p,last,s)) return p;
        first = ++p;           // 查看下一个字符
    }
}
```

返回序列末尾以指示“未找到”是一个重要的 STL 惯例。`match()` 函数很琐碎：它只是比较两个字符序列。请尝试自己编写它。用于在字符序列中查找字符的 `find()` 可以说是最简单的标准库算法（§21.2）。我们可以这样使用 `find_txt()`：

```cpp
auto p = find_txt(my_doc.begin(), my_doc.end(), "secret\nhomestead");
if (p==my_doc.end())
    cout << "not found";
else {
    // 执行某些操作
}
```

## 文本处理操作

我们的“文本处理器”及其操作非常简单。显然，我们追求的是简单性和合理的效率，而不是提供“功能丰富”的编辑器。但不要误以为提供对任意字符序列的*高效*插入、删除和搜索是微不足道的。我们选择这个例子是为了说明 STL 概念 `sequence`（序列）、`iterator`（迭代器）和 `container`（容器）（如 `list` 和 `vector`）的功能和通用性，以及一些 STL 编程惯例（技术），例如返回序列末尾以指示失败。注意，如果我们愿意，我们可以将 `Document` 开发为 STL 容器 – 通过提供 `Text_iterator`，我们已经完成了将 `Document` 表示为值序列的关键部分。

## 20.7 vector、list 和 string

为什么我们使用 `list` 存储行，使用 `vector` 存储字符？更准确地说，为什么我们使用 `list` 存储行序列，使用 `vector` 存储字符序列？此外，为什么我们不用 `string` 来存储一行？

我们可以提出这个问题的一个稍微更通用的变体。我们现在已经看到了四种存储字符序列的方法：

- `char[]`（字符数组）

- `vector<char>`

- `string`

- `list<char>`
