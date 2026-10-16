
# 19.3.3 String 类设计与实现

```cpp
class String { public:
//...
char& operator[](int n) { return ptr[n]; } char operator[](int n) const { return ptr[n]; }
// 未检查的元素访问
char& at(int n) { check(n); return ptr[n]; } char at(int n) const { check(n); return ptr[n]; }
// 进行范围检查的元素访问
String& operator+=(char c); // 在末尾添加 c
const char* c_str() { return ptr; } const char* c_str() const { return ptr; }
// C 风格字符串访问
int size() const { return sz; } int capacity() const
// 元素数量
// 元素加可用空间 { return (sz<=short_max) ? short_max : sz+space; }
//...
};
```

其思想是将 `[]` 用于普通场景。例如：

第 19.3.2 节 对字符的访问 563

```cpp
int hash(const String& s) {
int h {s[0]};
for (int i {1}; i!=s.size(); i++) h ^= s[i]>>1; return h;
}
// 对 s 的未检查访问
```

这里，使用经过检查的 `at()` 是多余的，因为我们只会从 0 到 `s.size()-1` 正确访问 `s`。

当我们认为可能出错时，可以使用 `at()`。例如：

```cpp
void print_in_order(const String& s,const vector<int>& index)
{
for (x : index) cout << s.at(x) << '\n';
}
```

遗憾的是，假定人们会在可能出错的地方始终一致地使用 `at()`，未免过于乐观。因此，某些 `std::string` 的实现（`[]`/`at()` 约定正是借鉴自 `std::string`）也会检查 `[]`。我个人更倾向于至少在

```cpp
void move_from(String& x);
};

```

这支持了众所周知的短字符串优化，使用两种字符串表示：

+   • 如果 `sz<=short_max`，字符存储在 `String` 对象本身的数组 `ch` 中。

+   • 如果 `!(sz<=short_max)`，字符存储在自由存储区，我们可以为扩展分配额外空间。成员 `space` 是此类字符的数量。在这两种情况下，元素数量保存在 `sz` 中，我们查看 `sz` 来确定给定字符串使用哪种实现方案。

在这两种情况下，`ptr` 都指向元素。这对性能至关重要：访问函数无需测试使用哪种表示；它们只需使用 `ptr`。只有构造函数、赋值、移动和析构函数 (§19.3.4) 必须关心这两种替代方案。

我们仅在 `sz<=short_max` 时使用数组 `ch`，仅在 `!(sz<=short_max)` 时使用整数 `space`。因此，为 `String` 对象同时为 `ch` 和 `space` 分配空间是浪费的。为了避免这种浪费，我使用了一个联合 (§8.3)。特别是，我使用了一种称为匿名联合 (§8.3.2) 的联合形式，它专门设计用于允许类管理对象的替代表示。匿名联合的所有成员都分配在同一内存中，从同一地址开始。任何时候只能使用其中一个成员，但除此之外，它们的使用方式与包围匿名联合的范围的独立成员完全相同。确保它们不会被误用是程序员的工作。例如，`String` 中使用 `space` 的所有成员函数都必须确保设置的是 `space` 而不是 `ch`。这是通过查看 `sz<=short_max` 来完成的。换句话说，`String` 在某种程度上是一个带判别式的联合，`sz<=short_max` 作为判别式。

## Section 19.3.3.1 Ancillary Functions

## 19.3.3.1 Ancillary Functions

除了为通用使用而设计的函数外，我发现当我提供三个辅助函数作为“构建块”来帮助我处理 somewhat tricky 的表示并最大限度地减少代码重复时，我的代码变得更清晰。其中两个需要访问 `String` 的表示，因此我将它们设为成员。然而，我将它们设为私有成员，因为它们不代表通常有用且安全使用的操作。对于许多有趣的类，实现不仅仅是表示加上公共函数。辅助函数可以减少代码重复、改善设计并提高可维护性。

第一个这样的函数将字符移动到新分配的内存中：

```cpp
char * expand(const char* ptr, int n) // expand into free store
{
char* p = new char[n];
strcpy(p,ptr); // §43.4
return p;
}
```

该函数不访问 `String` 表示，因此我没有将其设为成员。第二个实现函数由复制操作使用，为 `String` 提供另一个成员的副本：

```cpp
void String::copy_from(const String& x)
// make *this a copy of x
{
if (x.sz<=short_max) { // copy *this
memcpy(this,&x,sizeof(x)); // §43.5
ptr = ch;
}
else { // copy the elements
ptr = expand(x.ptr,x.sz+1);
sz = x.sz;
space = 0;
}
}
```

对目标 `String` 所需的任何清理都是 `copy_from()` 调用者的任务；`copy_from()` 无条件地覆盖其目标。我使用标准库 `memcpy()` (§43.5) 将源的字节复制到目标中。这是一种低级且有时相当糟糕的函数。只有在复制的内存中没有带构造函数或析构函数的对象时才应使用它，因为 `memcpy()` 对类型一无所知。两个 `String` 复制操作都使用 `copy_from()`。

用于移动操作的对应函数是：

```cpp
void String::move_from(String& x)
{
if (x.sz<=short_max) { // copy *this
memcpy(this,&x,sizeof(x)); // §43.5
ptr = ch;
}
else { // grab the elements
ptr = x.ptr;
sz = x.sz;
space = x.space;
x.ptr = x.ch; // x = ""
x.sz = 0;
x.ch[0]=0;
}
}
```

它也无条件地使目标成为其参数的副本。然而，它不会让其参数拥有任何自由存储。我本也可以在长字符串情况下使用 `memcpy()`，但由于长字符串表示仅使用 `String` 表示的一部分，我决定单独复制使用的成员。

# 19.3.4 Member Functions

默认构造函数将 `String` 定义为空：

```cpp
String::String() // default constructor :x{""}
: sz{0}, ptr{ch} // ptr points to elements,ch is an initial location (§19.3.3)
{
ch[0] = 0; // terminating 0
}
```

有了 `copy_from()` 和 `move_from()`，构造函数、移动和赋值实现起来相当简单。接受 C 风格字符串参数的构造函数必须确定字符数并适当地存储它们：

```cpp
String::String(const char * p)
:sz{strlen(p)},
ptr{(sz<=short_max) ? ch : new char[sz+1]},
space{0}
{
strcpy(ptr,p); // copy characters into ptr from p
}
```

如果参数是短字符串，`ptr` 设置为指向 `ch`；否则，在自由存储上分配 `space`。在任何一种情况下，字符都从参数字符串复制到 `String` 管理的内存中。

复制构造函数只是复制其参数的表示：

```cpp
String::String(const String& x) // copy constructor
{
copy_from(x); // copy representation from x
}
```

我没有费心去优化源大小等于目标大小的情况（如 `vector` 所做的；§13.6.3）。我不知道这是否值得。同样的，移动构造函数将表示从其源移动（并且可能将其参数设为空字符串）：

```cpp
String::String(String&& x) // move constructor
{
move_from(x);
}
```

与复制构造函数类似，复制赋值使用 `copy_from()` 来克隆其参数的表示。此外，它必须删除目标拥有的任何自由存储并确保不会出现自赋值问题（例如，`s=s`）：

```cpp
String& String::operator=(const String& x)
{
if (this==&x) return *this; // deal with self-assignment
char* p = (short_max<sz) ? ptr : 0;
copy_from(x);
delete[] p;
return *this;
}
```

`String` 移动赋值删除其目标的自由存储（如果有），然后进行移动：

```cpp
String& String::operator=(String&& x)
{
if (this==&x) return *this; // deal with self-assignment (x = move(x) is insanity)
if (short_max<sz) delete[] ptr; // delete target
move_from(x); // does not throw
return *this;
}
```

在逻辑上，将源移动到自身是可能的（例如，`s=std::move(s)`），因此我们再次需要防止自赋值（尽管可能性不大）。

在逻辑上最复杂的 `String` 操作是 `+=`，它将字符添加到字符串末尾，使其大小增加一：

```cpp
String& String::operator+=(char c)
{
if (sz==short_max) { // expand to long string
int n = sz+sz+2; // double the allocation (+2 because of the terminating 0)
ptr = expand(ptr,n);
space = n-sz-2;
}
else if (short_max<sz) {
if (space==0) { // expand in free store
int n = sz+sz+2; // double the allocation (+2 because of the terminating 0)
char* p = expand(ptr,n);
delete[] ptr;
ptr = p;
space = n-sz-2;
}
}
else
--space;
ptr[sz] = c; // add c at end
ptr[++sz] = 0; // increase size and set terminator
return *this;
}
```

这里有很多事情：`operator+=()` 必须跟踪使用的是哪种表示（短或长）以及是否有额外的可用空间可供扩展。如果需要更多空间，将调用 `expand()` 为该空间分配内存并将旧字符移动到新空间。如果需要删除旧分配，则将其返回，以便 `+=` 可以删除它。一旦有足够的空间可用，将新字符 `c` 放入其中并添加终止符 `0` 就很简单了。

注意对 `space` 可用内存的计算。在所有 `String` 实现中，这花费了最长的时间才弄对：这是一个容易出现差一错误的混乱的小计算。那个重复的常量 `2` 感觉非常像一个“魔数”。

所有 `String` 成员在确定可以放置新表示之前都不会修改新表示。特别是，它们在任何可能的 `new` 操作完成之后才 `delete`。事实上，`String` 成员提供强异常保证 (§13.2)。

如果你不喜欢作为 `String` 实现一部分呈现的那种繁琐代码，只需使用 `std::string`。在很大程度上，标准库设施存在是为了在大多数情况下让我们免于在如此低的级别编程。更进一步：编写字符串类、`vector` 类或 `map` 是极好的练习。然而，一旦练习完成，一个结果应该是欣赏标准所提供的东西并希望不维护自己的版本。

# 19.3.5 Helper Functions

为了完成类 `String`，我提供了一组有用的函数、流 I/O、range-for 循环支持、比较和连接。这些都镜像了 `std::string` 使用的设计选择。特别是，`<<` 只是打印字符而不添加格式，而 `>>` 在读取前跳过初始空白，直到找到终止空白（或流的末尾）：

```cpp
ostream& operator<<(ostream& os, const String& s)
{
    return os << s.c_str(); // §36.3.3
}

istream& operator>>(istream& is, String& s) {
    s = ""; // clear the target string
    is >> ws; // skip whitespace (§38.4.5.1)
    char ch = ' ';
    while(is.get(ch) && !isspace(ch)) s+=ch;
    return is;
}
```

我提供 `==` 和 `!=` 用于比较：

```cpp
bool operator==(const String& a, const String& b) {
    if (a.size()!=b.size())
        return false;
    for (int i = 0; i<a.size(); ++i) if (a[i]!=b[i])
        return false;
    return true;
}
bool operator!=(const String& a, const String& b)
{

return !(a==b);

}
```

添加 `<` 等运算符并不困难。

为了支持范围 `for` 循环，我们需要 `begin()` 和 `end()`（§9.5.1）。同样，我们可以将它们提供为独立的（非成员）函数，而无需直接访问 `String` 的实现：

```cpp
char* begin(String& x) // C-string-style access
{
return x.c_str();
}

char* end(String& x)
{
return x.c_str()+x.size();
}

const char* begin(const String& x)
{
return x.c_str();
}

const char* end(const String& x)
{
return x.c_str()+x.size();
}
```

给定用于在末尾添加字符的成员函数 `+=`，很容易通过非成员函数提供连接运算符：

```cpp
String& operator+=(String& a, const String& b) // concatenation
{
for (auto x : b) a+=x;

return a;
String operator+(const String& a, const String& b) // concatenation {
String res {a};
res += b;
return res;
}
```

我觉得自己在这里可能有一点“作弊”。我是否应该提供一个将 C 风格字符串添加到末尾的成员 `+=`？标准库字符串确实提供了这样的功能，但即使没有它，与 C 风格字符串进行连接仍然可以正常工作。例如：

```cpp
String s = “Njal “;
s += “Gunnar”; // concatenate: add to the end of s
```

这里对 `+=` 的使用会被解释为 `operator+=(s,String(“Gunnar”))`。我的猜测是，我可以提供一个更高效的 `String::operator+=(const char*)`，但我不知道这种额外的性能在实际代码中是否值得。在这种情况下，我倾向于采取保守做法，提供最小化的设计。能够实现某件事本身，并不是实现它的充分理由。

同样，我也没有尝试通过考虑源字符串的大小来优化 `+=`。添加表示 `String` 的 `_s` 字符串字面量后缀非常简单：

```cpp
String operator""_s(const char* p, size_t)
{
return String{p};
}
```

现在我们可以这样写：

```cpp
void f(const char*); // C-style string
void f(const String&); // our string
void g() {
f(“Madden’s”); // f(const char*)
f(“Christopher’s”_s); // f(const String&);
}
```

# 19.3.6 使用我们的 String

主程序只是对 `String` 运算符进行了一些简单测试：

```cpp
int main()
{
String s (“abcdefghij”); cout << s << ‘\n’;
s+=‘k’;
s += ‘l’;
s+=‘m’;
s += ‘n’;
cout << s << ‘\n’;
```
