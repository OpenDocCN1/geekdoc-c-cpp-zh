
想要用某种默认值替换容器内容的情况并不少见，但这个特定的 `swap()` 无法做到这一点。解决方案是将其通过两个重载来增强：`template<class T> void swap(T&& a, T& b); template<class T> void swap(T& a, T&& b)`

我们的示例将由 `swap()` 的最后一个版本处理。标准库采取不同的方法，通过为 `vector`、`string` 等定义 `shrink_to_fit()` 和 `clear()`（§31.3.3）来处理 `swap()` 的 `rvalue` 参数最常见的情况：

```
void f(string& s, vector<int>& v)
{
s.shrink_to_fit(); // makes.capacity()==s.size()
swap(s,string{s}); // makes.capacity()==s.size()
v.clear(); // make it empty
swap(v,vector<int>{}); // make it empty
v = {}; // make it empty
}
```

右值引用也可以用于提供完美转发（§23.5.2.1, §35.5.1）。所有标准库容器都提供移动构造函数和移动赋值（§31.3.2）。此外，它们插入新元素的操作，例如 `insert()` 和 `push_back()`，都有接受右值引用的版本。

### 7.7.3 引用到引用

如果你对一个类型的引用取引用，你得到的是对该类型的引用，而不是某种特殊的引用到引用类型。但是什么样的引用？左值引用还是右值引用？考虑：

```
using rr_i = int&&; using lr_i = int&;
using rr_rr_i = rr_i&&; using lr_rr_i = rr_i&; using rr_lr_i = lr_i&&; using lr_lr_i = lr_i&;

// “int && &&” is an int&&
// “int && &” is an int&
// “int & &&” is an int&
// “int & &” is an int&
```

换句话说，左值引用总是获胜。这是有道理的：我们能做的任何类型操作都无法改变左值引用引用的是左值这一事实。这有时被称为引用折叠。

语法不允许

```
int &&& r = i;
```

引用到引用只能作为别名（§3.4.5, §6.5）或模板类型参数（§23.5.2.1）的结果发生。

### 7.7.4 指针和引用

指针和引用是两种在程序的不同位置引用对象而无需复制的机制。我们可以用图示来展示这种相似性：

pp: &ii

rr: ii: 1

两者各有优缺点。

如果你需要更改所引用的对象，请使用指针。你可以使用 `=`、`+=`、`-=`、`++` 和 `--` 来更改指针变量的值（§11.1.4）。例如：

```
void fp(char* p) {
while (*p)
cout << ++*p; }
void fr(char& r) {
while (r)
cout << ++r; // oops: increments the char referred to,not the reference // near-infinite loop!
}

void fr2(char& r) { char*p = &r; // get a pointer to the object referred to
while (*p)
cout << ++*p;
}
```

相反，如果你想确保一个名字始终引用同一个对象，请使用引用。例如：

```
template<class T> class Proxy {
T& m;
public:
Proxy(T& mm) :m{mm} {}
// ...
};

// Proxy refers to the object with which it is initialized
template<class T> class Handle {
T * m;
public:
Proxy(T* mm) :m{mm} {}

// Handle refers to its current object
void rebind(T* mm) { m = mm; }
// ...
```

```
// no value
}
else {
// use r
}
```

显然，你需要有合适的定义的 `nullX`。这种风格不是惯用的，我不推荐它。程序员可以假定引用是有效的。创建无效引用是可能的，但你必须刻意为之。例如：

```
char* ident(char * p) { return p; }
char& r {*ident(nullptr)}; // invalid code
```

这段代码不是有效的 C++ 代码。即使你的当前实现没有捕获它，也不要编写这样的代码。

## 7.8 建议

- [1] 保持指针的使用简单直接；§7.4.1。
- [2] 避免非平凡的指针算术；§7.4。
- [3] 注意不要写出数组的边界之外；§7.4.1。
- [4] 避免多维数组；改用合适的容器；§7.4.2。
- [5] 使用 `nullptr` 而不是 `0` 或 `NULL`；§7.2.2。
- [6] 使用容器（例如，`vector`、`array` 和 `valarray`）而不是内置的（C 风格）数组；§7.4.1。
- [7] 使用 `string` 而不是零终止的 `char` 数组；§7.4。
- [8] 对于使用反斜杠的复杂字符串字面量，使用原始字符串；§7.3.2.1。
- [9] 优先使用 `const` 引用参数而不是普通引用参数；§7.7.3。
- [10] 仅对转发和移动语义使用右值引用；§7.7.2。
- [11] 将表示所有权的指针放在句柄类中；§7.6。
- [12] 除低级代码外避免 `void*`；§7.2.1。
- [13] 使用 `const` 指针和 `const` 引用在接口中表达不可变性；§7.5。
- [14] 优先使用引用作为参数而不是指针，除非“无对象”是合理的选项；§7.7.4。

*本页故意留空*

- - 引言

- - 结构体 `struct` 布局；`struct` 名称；结构体和类；结构体和数组；类型等价；Plain Old Data；字段

- - 联合体

- 联合体和类；匿名 `union`

- - 枚举

- `enum classes`；普通 `enums`；未命名 `enums`

- - 建议

## 8.2 Structures

结构体类型的变量可以使用 `{}` 记法进行初始化（§6.3.5）。例如：

```
Address jd = {
"Jim Dandy",
61, "South St",
"New Providence",
{'N','J'}, "07974"
};
```

请注意 `jd.state` 不能由字符串 “NJ” 初始化。字符串以零字符 `'\0'` 终止，所以 “NJ” 有三个字符——比 `jd.state` 能容纳的还要多一个。我故意为成员使用相当低级的类型，以说明如何做到这一点以及可能导致什么样的问题。

结构体通常通过使用 `->`（结构体指针解引用）运算符的指针来访问。例如：

```
void print_addr(Address* p)
{
cout << p->name << '\n'
<< p->number << ' ' << p->street << '\n' << p->town << '\n'
<< p->state[0] << p->state[1] << ' ' << p->zip << '\n';
}
```

当 `p` 是指针时，`p->m` 等价于 `(*p).m`。

或者，结构体可以通过引用传递并使用 `.`（结构体成员访问）运算符访问：

```
void print_addr2(const Address& r)
{
cout << r.name << '\n'
<< r.number << ' ' << r.street << '\n'
<< r.town << '\n'
<< r.state[0] << r.state[1] << ' ' << r.zip << '\n';
}
```

参数传递在 §12.2 中讨论。

结构体类型的对象可以赋值、作为函数参数传递，并作为函数的结果返回。例如：

```
Address current;

Address set_current(Address next) {
address prev = current;
current = next;
return prev;
```

其他合理的操作，例如比较（`==` 和 `!=`），默认不可用。然而，用户可以定义此类运算符（§3.2.1.1, 第 18 章）。

### 8.2.1 `struct` 布局

`struct` 的对象按声明顺序保存其成员。例如，我们可能将原始设备读数存储在如下结构中：

```
struct Readout {
    char hour; // [0:23]
    int value;
    char seq; // sequence mark['a':'z']
};
```

你可以想象 `Readout` 对象的成员在内存中的布局如下：

`hour`: `value`: `seq`:

成员按声明顺序分配在内存中，因此 `hour` 的地址必须小于 `value` 的地址。另见 §8.2.6。

然而，`struct` 对象的大小不一定是其成员大小之和。这是因为许多机器要求某些类型的对象分配在架构相关的边界上，或者如果它们这样分配会更高效。例如，整数通常分配在字边界上。在这样的机器上，对象被认为必须正确对齐（§6.2.9）。这导致结构中出现“空洞”。在具有 4 字节 `int` 的机器上，`Readout` 更现实的布局为：

`hour`: `value`: `seq`:

在这种情况下，如许多机器上一样，`sizeof(Readout)` 为 12，而不是从简单地将各个成员的大小相加所期望的 6。你可以通过按大小排序成员（先大后小）来最小化浪费的空间。例如：

```
struct Readout { int value; char hour; char seq;
};
```

```
// [0:23]
// sequence mark['a':'z']
value: (hour,seq):
```

请注意，这仍然在 `Readout` 中留下 2 字节的“空洞”（未使用空间），并且 `sizeof(Readout)==8`。原因是当我们把两个对象放在一起时，例如在一个 `Readout` 数组中，我们需要保持对齐。10 个 `Readout` 对象的数组大小为 `10*sizeof(Readout)`。

通常最好按可读性顺序排列成员，仅在有 demonstrated need to optimize. Use of multiple access specifiers (i.e., `public`, `private`, or `protected`) can affect layout (§20.5).

### 8.2.2 `struct` 名称

类型的名称在遇到后立即可用，而不仅仅是在完整的声明被看到之后。例如：

```
struct Link {
Link* previous;
Link* successor;
};
```

然而，直到看到其完整声明之前，不可能声明 `struct` 的新对象。例如：

```
struct No_good {
No_good member; // error : recursive definition
};
```

这是错误，因为编译器无法确定 `No_good` 的大小。为了允许两个（或更多）`struct` 互相引用，我们可以声明一个名称为 `struct` 的名称。例如：

```
struct List; // structname declaration: List to be defined later

struct Link {
Link* pre;
Link* suc;
List* member_of; int data;
};
struct List {
Link* head;
};
```

如果没有 `List` 的第一次声明，在 `Link` 的声明中使用指针类型 `List*` 将会是语法错误。

只要该使用不需要知道名称的成员或结构的大小，`struct` 的名称就可以在类型定义之前使用。然而，直到 `struct` 声明完成之前，该 `struct` 都是不完整类型。例如：

```
struct S; // “S” is the name of some type

extern S a;
S f();
void g(S);
```

```
Point p0; // danger :uninitialized if in local scope (§6.3.5.1)
Point p1 {}; // default construction: {{},{}}; that is {0,0}
Point p2 {1}; // the second member is default constructed: {1,{}}; that is {1,0}
Point p3 {1,2}; // {1,2}
```

如果需要重新排序参数、验证参数、修改参数、建立不变量（§2.4.3.2, §13.4）等，则需要构造函数。例如：

```
struct Address { string name; int number; string street; string town; char state[2]; char zip[5];

// “Jim Dandy”
// 61
// “South St”
// “NewProvidence” // ’N’ ’J’
// 07974

Address(const string n, int nu, const string& s, const string& t, const string& st, int z); };
```

这里，我添加了一个构造函数以确保每个成员都被初始化，并允许我对邮政编码使用 `string` 和 `int`，而不是处理单个字符。例如：

```
Address jd = {
“Jim Dandy”,
61, “South St”,
“New Providence”,
“NJ”, 7974 // (07974 would be octal; §6.2.4.1)
};
```

`Address` 构造函数可以这样定义：

```
Address::Address(const string& n, int nu, const string& s, const string& t, const string& st, int z) // validate postal code
:name{n},
number{nu},
street{s},
town{t}
{
if (st.size()!=2)
error(“State abbreviation should be two characters”)
state = {st[0],st[1]}; ostringstream ost; ost << z;
string zi {ost.str()}; switch (zi.size()) { case 5:
// store postal code as characters // an output string stream; see §38.4.2 // extract
characters from int
zip = {zi[0], zi[1], zi[2], zi[3], zi[4]}; break;
case 4: // star ts with '0'
zip = {'0', zi[0], zi[1], zi[2], zi[3]}; break;
default:
error("unexpected ZIP code format"); }
// ... check that the code makes sense ...
}
```

### 8.2.4 Structures and Arrays

自然地，我们可以有 `struct` 的数组和包含数组的 `struct`。例如：

```
struct Point {
int x,y
};

Point points[3] {{1,2},{3,4},{5,6}}; int x2 = points[2].x;
struct Array {
Point elem[3]; };
Array points2 {{1,2},{3,4},{5,6}};
int y2 = points2.elem[2].y;
```

将内置数组放在 `struct` 中允许我们将该数组视为对象：我们可以在初始化（包括参数传递和函数返回）和赋值中复制包含它的 `struct`。例如：

```
Array shift(Array a, Point p)
{
for (int i=0; i!=3; ++i) { a.elem[i].x += p.x; a.elem[i].y += p.y;
}
return a;
}
```

```
Array ax = shift(points2,{10,20});
```

`Array` 的记法有点原始：为什么是 `i!=3`？为什么要不断重复 `.elem[i]`？为什么只是 `Point` 类型的元素？标准库提供了 `std::array` (§34.2.1) 作为固定大小数组作为 `struct` 的想法更完整、更优雅的发展：
