
对表达式进行分词（§7.8.2）。例如，我们希望将 `1+4*x<=y/z*5` 分离为十一个标记：

```cpp
1 + 4 * x <= y / z * 5
```

我们可以使用 `>>` 来读取数字，但如果试图将标识符作为字符串读取，会导致 `x<=y` 被读为一个字符串（因为 `<` 和 `=` 不是空白字符），并且 `z*` 也会被读为一个字符串（因为 `*` 也不是空白字符）。相反，我们可以编写如下代码：

```cpp
for (char ch; cin.get(ch); ) {
    if (isspace(ch)) {       // 如果 ch 是空白
        // 什么也不做（即，跳过空白）
    }
    if (isdigit(ch)) {
        // 读取一个数字
    }
    else if (isalpha(ch)) {
        // 读取一个标识符
    }
    else {
        // 处理运算符
    }
}
```

`istream::get()` 函数将一个字符读取到其参数中。它不会跳过空白字符。与 `>>` 类似，`get()` 返回对 `istream` 的引用，以便我们可以检查其状态。

当我们读取单个字符时，通常希望对它们进行分类：这个字符是数字吗？这个字符是大写字母吗？等等。标准库提供了一组函数用于此目的：

### 字符分类

| 函数 | 描述 |
|---|---|
| `isspace(c)` | `c` 是否是空白字符（' '、'\t'、'\n' 等）？ |
| `isalpha(c)` | `c` 是否是字母（'a'...'z'、'A'...'Z'）（注意：不包括 '_'）？ |
| `isdigit(c)` | `c` 是否是十进制数字（'0'...'9'）？ |
| `isxdigit(c)` | `c` 是否是十六进制数字（十进制数字或 'a'..'f' 或 'A'..'F'）？ |
| `isupper(c)` | `c` 是否是大写字母？ |
| `islower(c)` | `c` 是否是小写字母？ |
| `isalnum(c)` | `c` 是否是字母或十进制数字？ |
| `iscntrl(c)` | `c` 是否是控制字符（ASCII 0..31 和 127）？ |
| `ispunct(c)` | `c` 是否既不是字母、数字、空白，也不是不可见的控制字符？ |
| `isprint(c)` | `c` 是否可打印（ASCII `'!'... '~'`）？ |
| `isgraph(c)` | 是否满足 `isalpha(c)` 或 `isdigit(c)` 或 `ispunct(c)`（注意：不包括空格）？ |

请注意，可以使用“或”运算符（\|\|）将这些分类组合起来。例如，`isalnum(c)` 意味着 `isalpha(c)||isdigit(c)`；也就是说，“`c` 是字母还是数字？”

此外，标准库还提供了两个用于消除大小写差异的有用函数：

### 字符大小写

| 函数 | 描述 |
|---|---|
| `toupper(c)` | `c` 或 `c` 的大写等价形式 |
| `tolower(c)` | `c` 或 `c` 的小写等价形式 |

这些功能在需要忽略大小写差异时非常有用。例如，在用户输入中，`Right`、`right` 和 `rigHT` 很可能表示同一个词（`rigHT` 很可能是误触 Caps Lock 键的结果）。在对这些字符串中的每个字符应用 `tolower()` 之后，我们得到了每个词的 `right`。我们可以对任意 `string` 做到这一点：

```cpp
void tolower(string& s)        // 将 s 转换为小写
{
    for (char& x : s) x = tolower(x);
}
```

我们使用按引用传递（§8.5.5）来实际改变 `string`。如果我们想保留旧字符串，我们可以编写一个函数来创建一个 lowercase 副本。优先使用 `tolower()` 而不是 `toupper()`，因为对于某些自然语言（如德语）中的文本，这种处理方式效果更好，在这些语言中，并非每个小写字符都有对应的大写等价形式。

## 11.7 使用非标准分隔符

本节提供了使用 `iostreams` 解决实际问题的一个半真实示例。当我们读取字符串时，单词默认由空白字符分隔。不幸的是，`istream` 并不提供我们定义哪些字符构成空白，或以其他方式直接更改 `>>` 如何读取字符串的功能。那么，如果我们需要对空白有另一种定义，该怎么办？考虑一下

§4.6.3 中的示例，其中我们读取了“单词”并对它们进行比较。这些单词是由空白字符分隔的，因此如果我们读取：

> *如计划中所说，客人们到了；然后，*

我们将得到以下“单词”：

- * As
- planned,
- the
- guests
- arrived;
- then,

这并不是我们在词典中会找到的内容：`planned,` 和 `arrived;` 不是单词。它们是单词加上令人分心且无关的标点字符。对于大多数目的，我们必须将标点字符当作空白字符来处理。我们如何去除这样的标点字符？我们可以读取字符，去除标点字符——或者将它们转换为空白——然后再次读取“清理后”的输入：

```cpp
string line;
getline(cin, line);        // 读取到 line
for (char& ch : line)      // 用空格替换每个标点字符
    switch(ch) {
        case ';': case '.': case ',': case '?': case '!':
            ch = ' ';
    }

stringstream ss(line);   // 创建一个从 line 读取的 istream ss
vector<string> vs;
for (string word; ss >> word; ) // 读取没有标点字符的单词
    vs.push_back(word);
```

使用该方法读取该行，我们得到期望的：

- * As
- planned
- the
- guests
- arrived
- then

不幸的是，上面的代码很杂乱且比较特殊化。如果我们有了另一个标点的定义，该怎么办？让我们提供一种更通用且更有用的方法来去除输入流中不需要的字符。那应该是什么样的？我们希望用户代码看起来像什么？比如：

```cpp
ps.whitespace(";:,.");  // 将分号、冒号、逗号和点号视为空白
for (string word; ps >> word; )
    vs.push_back(word);
```

我们如何定义一个像 `ps` 这样工作的流？基本想法是从普通输入流中读取单词，然后将用户指定的“空白”字符视为空白；也就是说，我们不将“空白”字符交给用户，只是使用它们来分隔单词。例如，

as.not

应该是两个单词：

- as
- not

我们可以定义一个类来为我们做到这一点。它必须从 `istream` 获取字符，并且拥有一个 `>>` 运算符，其行为与 `istream` 的相同，只是我们可以告诉它哪些字符应被视为空白。为了简化起见，我们将不提供一种将现有的空白字符（空格、换行符等）视为非空白字符的方法；我们只是允许用户指定额外的“空白”字符。同样，我们也不会提供一种从流中完全移除指定字符的方法；像以前一样，我们只是将它们转换为空白。让我们把这个类称为 `Punct_stream`：

```cpp
class Punct_stream {   // 类似于 istream，但用户可以添加到
                       // 空白字符集中
    public:
        Punct_stream(istream& is)
            : source(is), sensitive(true) { }

        void whitespace(const string& s)     // 使 s 成为空白集
        { white = s; }
        void add_white(char c) { white += c; }  // 添加到空白集
        bool is_whitespace(char c);          // c 在空白集中吗？

        void case_sensitive(bool b) { sensitive = b; }
        bool is_case_sensitive() { return sensitive; }

        Punct_stream& operator>>(string& s);
        operator bool();

    private:
        istream& source;           // 字符源
        istringstream buffer;     // 我们让 buffer 执行格式化
        string white;             // 被视为“空白”的字符
        bool sensitive;          // 流是否区分大小写？
};
```

基本想法是——正如上面的示例所示——从 `istream` 一次读取一行，将“空白”字符转换为空格，然后使用 `istringstream` 进行格式化。除了处理用户定义的空白之外，我们还赋予了 `Punct_stream` 一个相关功能：如果我们要求使用 `case_sensitive()`，它可以区分大小写的输入转换为不区分大小写的输入。例如，如果我们要请求，我们可以让 `Punct_stream` 将

**Man bites dog!**

读取为：

- man
- bites
- dog

`Punct_stream` 的构造函数接受用作字符源的 `istream`，并将其命名为 `source`。构造函数还默认将流设置为通常的区分大小写的行为。我们可以创建一个 `Punct_stream`，从 `cin` 读取，将分号、冒号和点号视为空白，并将所有字符转换为小写：

```cpp
Punct_stream ps(cin);          // ps 从 cin 读取
ps.whitespace(";:.");        // 分号、冒号和点号也是空白
ps.case_sensitive(false);     // 不区分大小写
```

显然，最有趣的運算是输入运算符 `>>`。它也是定义起来最困难的。我们的一般策略是从 `istream` 中读取整行到一个字符串中（称为 `line`）。然后我们将所有“我们的”空白字符转换为空格字符（' '）。完成后，我们将该行放入 `istringstream`

