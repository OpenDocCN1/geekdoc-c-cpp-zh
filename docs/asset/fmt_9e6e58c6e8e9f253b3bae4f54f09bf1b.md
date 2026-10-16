
```cpp
auto addr = compose("dmr","bell-labs.com");
```

这里，`addr` 被初始化为字符序列 `dmr@bell-labs.com`。字符串的“加法”意味着连接。你可以将字符串、字符串字面量、C 风格字符串或字符连接到字符串上。标准字符串具有移动构造函数，因此即使按值返回很长的字符串也是高效的 (§3.3.2)。

在许多应用中，连接最常见的形式是在字符串末尾添加内容。这直接由 `+=` 操作支持。例如：

```cpp
void m2(string& s1, string& s2)
{
s1 = s1 + '\n'; // append newline
s2 += '\n'; // append newline
}
```

这两种向字符串末尾添加的方式在语义上是等价的，但我更喜欢后者，因为它更明确地说明了其作用，更简洁，并且可能更高效。

字符串是可变的。除了 `=` 和 `+=` 之外，还支持下标访问（使用 `[]`）和子字符串操作。标准库字符串在第 36 章中描述。除其他有用的特性外，它提供了操作子字符串的能力。例如：

```cpp
string name = "Niels Stroustrup";
```

```cpp
void m3() {
string s = name.substr(6,10); // s="Stroustrup"
name.replace(0,5,"nicholas"); // name becomes "nicholas Stroustrup"
name[0] = toupper(name[0]); // name becomes "Nicholas Stroustrup"
}
```

`substr()` 操作返回一个 `string`，它是其参数指示的子字符串的副本。第一个参数是 `string` 中的一个索引（位置），第二个是所需子字符串的长度。由于索引从 `0` 开始，`s` 得到的值为 `Stroustrup`。

`replace()` 操作用一个值替换子字符串。在这种情况下，从 `0` 开始长度为 `5` 的子字符串是 `Niels`；它被 `nicholas` 替换。最后，我用其大写等价物替换初始字符。因此，`name` 的最终值为 `Nicholas Stroustrup`。请注意，替换字符串的大小不必与它所替换的子字符串相同。

自然地，`string` 可以与彼此以及字符串字面量进行比较。例如：

```cpp
string incantation;
void respond(const string& answer)
{
if (answer == incantation) {
// perform magic
}
else if (answer == "yes") {
//...
}
//...
}
```

`string` 库在第 36 章中描述。实现 `string` 的最常见技术在 `String` 示例 (§19.3) 中给出。

# 4.3 流 I/O

标准库通过 `iostream` 库提供格式化的字符输入和输出。输入操作是类型化的并且可以扩展以处理用户定义的类型。本节是对 `iostreams` 使用的非常简要的介绍；第 38 章是对 `iostream` 库设施的相当完整的描述。

其他形式的交互，例如图形 I/O，是通过非 ISO 标准的一部分的库处理的，因此此处不描述。

## 4.3.1 输出

I/O 流库为每种内置类型定义输出。此外，很容易定义用户定义类型的输出 (§4.3.3)。运算符 `<<`（“put to”）用作 `ostream` 类型对象的输出运算符；`cout` 是标准输出流，`cerr` 是报告错误的标准流。默认情况下，写入 `cout` 的值会被转换为字符序列。例如，要输出十进制数字 `10`，我们可以写：

```cpp
void f()
{
  cout << 10;
}
```

这会在标准输出流上放置字符 `1` 后跟字符 `0`。等价地，我们可以写：

```cpp
void g()
{
  int i {10};
  cout << i;
}
```

不同类型的输出可以以明显的方式组合：

```cpp
void h(int i)
{
  cout << "the value of i is ";
  cout << i;
  cout << '\n';
}
```

对于 `h(10)`，输出将为：

**the value of i is 10**

人们很快就会厌倦在输出多个相关项时重复输出流的名称。幸运的是，输出表达式的结果本身也可以用于进一步输出。例如：

```cpp
void h2(int i)
{
  cout << "the value of i is " << i << '\n';
}
```

这个 `h2()` 产生的输出与 `h()` 相同。

字符常量是单引号括起来的字符。请注意，字符作为字符输出而不是作为数值。例如：

```cpp
void k()
{
  int b = 'b'; // note: char implicitly converted to int
  char c = 'c';
  cout << 'a' << b << c;
}
```

字符 `'b'` 的整数值是 `98`（在我使用的 C++ 实现中使用的 ASCII 编码），所以这将输出 `a98c`。

## 4.3.2 输入

标准库为输入提供 `istreams`。与 `ostreams` 一样，`istreams` 处理内置类型的字符字符串表示，并且可以很容易地扩展以处理用户定义的类型。

运算符 `>>`（“get from”）用作输入运算符；`cin` 是标准输入流。`>>` 的右操作数的类型决定了接受什么输入以及输入操作的目标。例如：

```cpp
void f()
{
    int i;
    cin >> i; // read an integer into i
    double d;
    cin >> d; // read a double-precision floating-point number into d
}
```

这会从标准输入读取一个数字，例如 `1234`，到整数变量 `i`，以及一个浮点数，例如 `12.34e5`，到双精度浮点变量 `d`。

通常，我们想要读取一系列字符。一种方便的方法是读取到 `string` 中。例如：

```cpp
void hello()
{
    cout << "Please enter your name\n";
    string str;
    cin >> str;
    cout << "Hello, " << str << "\n";
}
```

如果你输入 `Eric`，响应是：

**Hello, Eric!**

默认情况下，空白字符 (§7.3.2)，例如空格，会终止读取，所以如果你输入 `Eric Bloodaxe` 假装成不幸的约克国王，响应仍然是：

**Hello, Eric!**

你可以使用 `getline()` 函数读取整行（包括终止的换行符）。例如：

```cpp
void hello_line()
{
    cout << "Please enter your name\n";
    string str;
    getline(cin,str);
    cout << "Hello, " << str << "\n";
}
```

使用此程序，输入 `Eric Bloodaxe` 会产生期望的输出：**Hello, Eric**

终止行的换行符会被丢弃，所以 `cin` 已准备好进行下一次输入行。

标准字符串具有很好的属性，即会扩展以容纳你放入的内容；你不必预先计算最大大小。所以，如果你输入几兆字节的分号，程序会回显数页的分号给你。

## 4.3.3 用户定义类型 I/O

除了内置类型和标准 `strings` 的 I/O 外，`iostream` 库允许程序员为自己的类型定义 I/O。例如，考虑一个简单的类型 `Entry`，我们可能用它来表示电话簿中的条目：

```cpp
struct Entry {
  string name;
  int number;
};
```

我们可以定义一个简单的输出运算符以使用 `{"name",number}` 格式写入 `Entry`，类似于我们在代码中用于初始化的格式：

```cpp
ostream& operator<<(ostream& os, const Entry& e)
{
  return os << "{" << e.name << ", " << e.number << "}";
}
```

用户定义的输出运算符将其输出流（按引用）作为第一个参数并将其作为结果返回。详情见 §38.4.2。

相应的输入运算符更复杂，因为它必须检查正确的格式并处理错误：

```cpp
istream& operator>>(istream& is, Entry& e)
// read { "name", number } pair. Note: formatted with { " ", and }
{
  char c, c2;
  if (is >> c && c == '{' && is >> c2 && c2 == '"') { // start with a {
    string name;
    while (is.get(c) && c != '"')
      name += c;
    // the default value of a string is the empty string: "" // anything before a " is part of the name
    if (is >> c && c == ',') {
      int number = 0;
      if (is >> number >> c && c == '}') { // read the number and a }
        e = {name, number}; // assign to the entry
        return is;
      }
    }
  }
}
is.setf(ios_base::failbit); // register the failure in the stream
return is;
}
```

输入操作返回其 `istream` 的引用，可用于测试操作是否成功。例如，当用作条件时，`is>>c` 表示“我们是否成功地从 `is` 读取到 `c`？”

`is>>c` 默认会跳过空白字符，但 `is.get(c)` 不会，因此此 `Entry` 输入运算符会忽略（跳过）名称字符串外部的空白字符，但不会忽略名称字符串内部的空白字符。例如：

```
{ "John Marwood Cleese", 123456 }
{"Michael Edward Palin",987654}
```

我们可以像这样从输入中读取这样的一对值到一个 `Entry` 中：

```cpp
for (Entry ee; cin>>ee; )
cout << ee << '\n';
```

输出为：

```cpp
// read from cin into ee
// write ee to cout
```

```cpp
{"John Marwood Cleese", 123456}
{"Michael Edward Palin", 987654}
```

有关编写用户定义类型的输入运算符的更多技术细节和技术，请参阅 §38.4.1。有关在字符流中识别模式的更系统技术（正则表达式匹配），请参阅 §5.5 和第 37 章。

# 4.4 容器

大多数计算涉及创建值的集合然后操作这些集合。读取字符到字符串中并打印出字符串就是一个简单的例子。主要目的是保存对象的类通常称为容器。为给定任务提供合适的容器并用有用的基本操作支持它们，是构建任何程序的重要步骤。

为了说明标准库容器，考虑一个用于保存姓名和电话号码的简单程序。这是不同背景的人会认为不同方法“简单且显而易见”的那种程序。§4.3.3 中的 `Entry` 类可用于保存简单的电话簿条目。在这里，我们故意忽略许多现实世界的复杂性，例如许多电话号码没有简单的 32 位 `int` 表示形式这一事实。

## 4.4.1 `vector`

最有用的标准库容器是 `vector`。`vector` 是给定类型元素的序列。元素在内存中连续存储：

```cpp
vector:
elem: 0: 1: 2: 3: 4: 5:
sz: 6
```

§3.2.2 和 §3.4 中的 `Vector` 示例给出了 `vector` 实现的想法，而 §13.6 和 §31.4 提供了详尽的讨论。

我们可以用其元素类型的一组值初始化一个 `vector`：

```cpp
vector<Entry> phone_book = {
{"David Hume",123456},
{"Karl Popper",234567},
{"Bertrand Arthur William Russell",345678}
};
```

元素可以通过下标访问：

```cpp
void print_book(const vector<Entry>& book)
{
for (int i = 0; i!=book.size(); ++i)
cout << book[i] << '\n';
}
```

与往常一样，索引从 `0` 开始，因此 `book[0]` 包含 `David Hume` 的条目。`vector` 成员函数 `size()` 给出元素的数量。

`vector` 的元素构成一个范围，因此我们可以使用范围 for 循环（§2.2.5）：

```cpp
void print_book(const vector<Entry>& book)
{
for (const auto& x : book) // for ”auto” see §2.2.2
cout << x << '\n';
}
```

当我们定义一个 `vector` 时，我们为其指定初始大小（初始元素数量）：

```cpp
vector<int> v1 = {1, 2, 3, 4}; // size is 4
vector<string> v2; // size is 0
vector<Shape*> v3(23); // size is 23; initial element value: nullptr
vector<double> v4(32,9.9); // size is 32; initial element value: 9.9
```

显式大小用普通括号括起来，例如，`(23)`，并且默认情况下元素被初始化为元素类型的默认值（例如，指针的 `nullptr` 和数字的 `0`）。如果你不想要默认值，可以将其指定为第二个参数（例如，`v4` 的 32 个元素的 `9.9`）。

初始大小可以更改。`vector` 上最有用的操作之一是 `push_back()`，它在 `vector` 的末尾添加一个新元素，使其大小增加一。例如：

```cpp
void input()
{
for (Entry e; cin>>e;)
phone_book.push_back(e);
}
```

这会从标准输入读取 `Entry` 到 `phone_book`，直到到达输入结束（例如文件结束）或输入操作遇到格式错误。标准库 `vector` 的实现使得通过重复 `push_back()` 增长 `vector` 是高效的。

`vector` 可以在赋值和初始化中复制。例如：

```cpp
vector<Entry> book2 = phone_book;
```

`vector` 的复制和移动由构造函数和赋值运算符实现，如 §3.3 中所述。赋值 `vector` 涉及复制其元素。因此，在 `book2` 的初始化之后，`book2` 和 `phone_book` 持有电话簿中每个 `Entry` 的单独副本。当 `vector` 包含许多元素时，这种看似无害的赋值和初始化可能代价高昂。在不希望复制的情况下，应使用引用或指针（§7.2，§7.7）或移动操作（§3.3.2，§17.5.2）。

#### 4.4.1.1 元素

像所有标准库容器一样，`vector` 是某些类型 `T` 的元素的容器，即 `vector<T>`。几乎任何类型都符合元素类型的条件：内置数字类型（如 `char`、`int` 和 `double`）、用户定义类型（如 `string`、`Entry`、`list<int>` 和 `Matrix<double,2>`）以及指针（如 `const char *`、`Shape*` 和 `double*`）。当你插入一个新元素时，其值会被复制到容器中。例如，当你将整数值 `7` 放入容器时，结果元素确实具有值 `7`。元素不是指向包含 `7` 的对象的引用或指针。这使得容器紧凑且访问速度快。对于关心内存大小和运行时间性能的人来说，这一点至关重要。

#### 4.4.1.2 范围检查

标准库 `vector` 不保证范围检查（§31.2.2）。例如：

```cpp
void silly(vector<Entry>& book)
{
int i = book[ph.size()].number; // book.size() is out of range
// ...
}
```

该初始化很可能会将一些随机值放入 `i` 而不是给出错误。这是不希望的，并且超出范围的错误是一个常见问题。因此，我经常使用 `vector` 的简单范围检查适配：

```cpp
template<typename T>
class Vec : public std::vector<T> {

public:
```
