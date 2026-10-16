
You can convert a pointer to function to a different pointer-to-function type, but you must cast the resulting pointer back to its original type or strange things may happen:

```
using P1 = int(*)(int*);
using P2 = void(*)(void);
```

```cpp
void f(P1 pf) {

P2 pf2 = reinterpret_cast<P2>(pf);

pf2(); // likely serious problem

// convert pf2 “back again” P1 pf1 = reinterpret_cast<P1>(pf2);

int x = 7;

int y = pf1(&x);

// ...

}
// OK
```

我们需要最糟糕的转换，即 `reinterpret_cast`，来进行函数指针类型的转换。原因在于使用错误类型的函数指针的结果是如此不可预测且依赖于系统。例如，在上面的示例中，被调用的函数可能会写入其参数所指向的对象，但调用 `pf2()` 并未提供任何参数！

函数指针提供了一种参数化算法的方式。由于 C 没有函数对象 (§3.4.3) 或 lambda 表达式 (§11.4)，因此在 C 风格代码中，函数指针被广泛用作函数参数。例如，我们可以将排序函数所需的比较操作作为函数指针提供：

```
using CFT = int(const void*, const void*);
void ssort(void * base, size_t n, size_t sz, CFT cmp) /*
Sort the “n” elements of vector “base” into increasing order using the comparison function pointed to by”cmp”. The elements are of size”sz”.
Shell sort(Knuth, Vol3, pg84) */
{ for (int gap=n/2; 0<gap; gap/=2)
for (int i=gap; i!=n; i++)
for (int j=i -gap; 0<=j; j-=gap) {
char* b = static_cast<char*>(base); // necessary cast
char* pj = b+j*sz; // &base[j]
char* pjg = b+(j+gap)*sz; // &base[j+gap]
if (cmp(pjg,pj)<0) { // swap base[j] and base[j+gap]:
for (int k=0; k!=sz; k++) {
char temp = pj[k];
pj[k] = pjg[k];
pjg[k] = temp;
}
}
}
}
```

`ssort()` 例程并不知道它所排序对象的类型，只知道元素的数量（数组大小）、每个元素的大小以及用于执行比较的函数。`ssort()` 的类型被选为与标准 C 库排序例程 `qsort()` 的类型相同。实际程序使用 `qsort()`、C++ 标准库算法 `sort()` (§32.6) 或专门的排序例程。这种代码风格在 C 中很常见，但在 C++ 中表达该算法并非最优雅的方式（参见 §23.5，§25.3.4.1）。

这样的排序函数可用于排序如下表：

```
struct User {
const char* name;
const char* id;
int dept;
};

vector<User> heads = {
“Ritchie D.M.”, “dmr”, 11271, “Sethi R.”, “ravi”, 11272, “Szymanski T.G.”, “tgs”, 11273, “Schryer N.L.”, “nls”, 11274, “Schryer N.L.”, “nls”, 11275, “Kernighan B.W.”, “bwk”, 11276
};
void print_id(vector<User>& v) {
for (auto& x : v)
cout << x.name << ‘\t’ << x.id << ‘\t’ << x.dept << ‘\n’;
}
```

为了能够排序，我们必须首先定义适当的比较函数。比较函数必须在其第一个参数小于第二个参数时返回负值，相等时返回零，否则返回正数：

```
int cmp1(const void* p, const void* q) // Compare name strings
{
return strcmp(static_cast<const User*>(p)->name,static_cast<const User*>(q)->name);
}

int cmp2(const void* p, const void* q) // Compare dept numbers
{
return static_cast<const User*>(p)->dept - static_cast<const User*>(q)->dept;
}
```

在指针到函数的赋值或初始化时，参数或返回类型的隐式转换不存在。这意味着你无法通过编写以下内容来避免丑陋且容易出错的转换：

```
int cmp3(const User* p, const User* q) // Compare ids
{
return strcmp(p->id,q->id);
}
```

原因在于将 `cmp3` 作为 `ssort()` 的参数会违反 `cmp3` 将以 `const User*` 类型参数被调用的保证（另见 §15.2.6）。

该程序排序并打印：

```cpp
int main()
{
  cout << “Heads in alphabetical order:\n”; ssort(heads,6,sizeof(User),cmp1);
  print_id(heads);
  cout << ‘\n’;

  cout << “Heads in order of department number:\n”;
  ssort(heads,6,sizeof(User),cmp2);
  print_id(heads);
}
```

为了比较，我们可以等价地写成：

```cpp
int main()
{
  cout << “Heads in alphabetical order:\n”;
  sort(heads.begin(), head.end(),
       [](const User& x, const User& y) { return x.name<y.name; });
  print_id(heads);
  cout << ‘\n’;

  cout << “Heads in order of department number:\n”; sort(heads.begin(), head.end(),
       [](const User& x, const User& y) { return x.dept<y.dept; });
  print_id(heads);
}
```

无需提及大小，也无需任何辅助函数。如果显式使用 `begin()` 和 `end()` 很烦人，可以通过使用接受容器的 `sort()` 版本来消除它 (§14.4.5)：

```cpp
sort(heads, [](const User& x, const User& y) { return x.name<y.name; });
```

你可以通过赋值或初始化函数指针来获取重载函数的地址。在这种情况下，目标的类型用于从重载函数集合中选择。例如：

```cpp
void f(int); int f(char);

void (*pf1)(int) = &f; int (*pf2)(char) = &f; void (*pf3)(char) = &f;

// void f(int)
// int f(char)
// error : no void f(char)
```

也可以获取成员函数的地址 (§20.6)，但指向成员函数的指针与指向（非成员）函数的指针截然不同。指向 `noexcept` 函数的指针可以声明为 `noexcept`。例如：

```cpp
void f(int) noexcept; void g(int);

void (*p1)(int) = f;

void (*p2)(int) noexcept = f; void (*p3)(int) noexcept = g;

// OK: but we throw away useful information
// OK: we preserve the noexcept information
// error: we don’t know that g doesn’t throw
```

函数指针必须反映函数的链接方式 (§15.2.6)。链接说明或 `noexcept` 不能出现在类型别名中：

`using Pc = extern “C” void(int);` // error: linkage specification in alias
`using Pn = void(int) noexcept;` // error: noexcept in alias

# 12.6 宏

宏在 C 中非常重要，但在 C++ 中用途要少得多。关于宏的第一条规则是：除非必须，否则不要使用它们。几乎每个宏都展示了编程语言、程序或程序员中的缺陷。由于它们在编译器正式处理之前重新排列程序文本，因此宏也是许多编程支持工具的主要问题。因此，当你使用宏时，应期望诸如调试器、交叉引用工具和剖析器等工具的服务质量下降。如果你必须使用宏，请仔细阅读你所使用的 C++ 预处理器参考手册，并尽量不要过于聪明。此外，为了提醒读者，请遵循使用大量大写字母命名宏的约定。宏的语法在 §iso.16.3 中介绍。

我建议仅将宏用于条件编译 (§12.6.1)，特别是用于包含保护 (§15.3.3)。

一个简单的宏是这样定义的：

```
#define NAME rest of line
```

在 `NAME` 作为标记出现时，它会被 `rest of line` 替换。例如：

```
named = NAME

will expand into

named = rest of line
```

宏也可以定义为带参数。例如：

```
#define MAC(x,y) argument1: x argument2: y
```

当 `MAC` 被使用时，必须提供两个参数字符串。它们将在 `MAC()` 展开时替换 `x` 和 `y`。例如：

```
expanded = MAC(foo bar, yuk yuk)

will be expanded into

expanded = argument1: foo bar argument2: yuk yuk
```

宏名不能重载，宏预处理器无法处理递归调用：

```
#define PRINT(a,b) cout<<(a)<<(b)

#define PRINT(a,b,c) cout<<(a)<<(b)<<(c) /* trouble?: redefines, does not overload*/

#define FAC(n) (n>1)?n*FAC(n−1):1 /* trouble: recursive macro*/
```

宏操作字符字符串，对 C++ 语法知之甚少，对 C++ 类型或作用域规则一无所知。只有宏的展开形式会被编译器看到，因此宏中的错误会在宏展开时报告，而不是在定义时报告。这会导致非常晦涩的错误信息。

以下是一些合理的宏：

```
#define CASE break;case
```

```
#define FOREVER for(;;)
```

以下是一些完全不必要的宏：

```
#define PI 3.141593
```

```
#define BEGIN {
```

```
#define END }
```

以下是一些危险的宏：

```
#define SQUARE(a) a*a
```

```
#define INCR_xx (xx)++
```

要了解它们为何危险，请尝试展开以下内容：

```
int xx = 0; // global counter
```

```
void f(int xx)
{
int y = SQUARE(xx+2); // y=xx+2*xx+2; that is,y=xx+(2*xx)+2 INCR_xx; // increments argument xx (not the global xx)
```

如果你必须使用宏，请在引用全局名称时使用作用域解析运算符 `::` (§6.3.4)，并在可能的情况下将宏参数名出现的地方用括号括起来。例如：

```
#define MIN(a,b) (((a)<(b))?(a):(b))
```

这处理了更简单的语法问题（通常会被编译器捕获），但没有处理副作用问题。例如：

```
int x = 1;
int y = 10;
int z = MIN(x++,y++); // x becomes 3; y becomes 11
```

如果你必须编写需要注释的复杂宏，使用 `/* */` 注释是明智的，因为某些旧的 C 预处理器不了解 `//` 注释，有时会被用作 C++ 工具的一部分。例如：

```
#define M2(a) something(a) /* thoughtful comment*/
```

使用宏，你可以设计自己的私有语言。即使你更喜欢这种“增强语言”而不是纯 C++，大多数 C++ 程序员也会觉得它难以理解。此外，预处理器是一个非常简单的大脑宏处理器。当你尝试做一些非平凡的事情时，你可能会发现它要么不可能，要么不必要地困难。`auto`、`constexpr`、`const`、`decltype`、`enum`、`inline`、lambda 表达式、`namespace` 和 `template` 机制可以用作对预处理器构造的许多传统用途的更好行为的替代。例如：

```
const int answer = 42;
```

```
template<class T>
inline const T& min(const T& a, const T& b) {
return (a<b)?a:b;
}
```

编写宏时，通常需要为某事物取一个新名字。可以使用 `##` 宏操作符将两个字符串连接起来创建一个字符串。例如：

```
#define NAME2(a,b) a##b

int NAME2(hack,cah)();
```

会生成

```
int hackcah();
```

在替换字符串中，参数名前面的单个 `#` 表示包含宏参数的字符串。例如：

```
#define printx(x) cout << "x" << " = " << x << '\n';

int a = 7;
string str = "asdf";

void f() {
    printx(a); // cout << "a" << " = " << a << '\n';
    printx(str); // cout << "str" << " = " << str << '\n';
}
```

写 `#x` = " 而不是 `#x` << " = " 是晦涩的“巧妙代码”，而不是错误。相邻的字符串字面量会被连接起来 (§7.3.2)。

指令

```
#undef X
```

确保没有名为 `X` 的宏被定义——无论该指令之前是否已定义。这为防止不期望的宏提供了一些保护。然而，要知道 `X` 对一段代码的影响本应是什么并不总是容易的。

宏的参数列表（“替换列表”）可以为空：

```
#define EMPTY() std::cout<<"empty\n"

EMPTY(); // print"empty\n"

EMPTY; // error : macro replacement list missing
```

我很难想到空宏参数列表的用途，而这些用途不是容易出错的或恶意的。

宏甚至可以是可变参数的。例如：

```
#define err_print(...) fprintf(stderr,"error: %s %d\n", __VA_ARGS__)

err_print("The answer",54);
```

省略号 (`...`) 表示 `__VA_ARGS__` 代表实际作为字符串传递的参数，因此输出为：

```
error: The answer 54
```

# 12.6.1 条件编译

宏的一种用途几乎无法避免。指令

```
#ifdef IDENTIFIER
```

如果 `IDENTIFIER` 已被定义则不执行任何操作，但如果未定义，则该指令会导致忽略所有输入，直到遇到 `#endif` 指令为止。例如：

```c
int f(int a
#ifdef arg_two
,int b
#endif
);
```

除非已 `#defined` 一个名为 `arg_two` 的宏，否则会生成：

```c
int f(int a
);
```

此示例会让假设程序员行为正常的工具感到困惑。

大多数 `#ifdef` 的使用没那么奇怪，并且在适度使用时，`#ifdef` 及其补充 `#ifndef` 危害不大。另见 §15.3.3。

用于控制 `#ifdef` 的宏的名称应仔细选择，以免与普通标识符冲突。例如：

```c
struct Call_info {
Node* arg_one;
Node* arg_two;
// ...

};
```

这段看似无害的源文本如果有人写下：

```c
#define arg_two x
```
