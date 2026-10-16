

- **sizeof(char)** ≤ **sizeof(wchar_t)** ≤ **sizeof(long)**
- **sizeof(float)** ≤ **sizeof(double)** ≤ **sizeof(long double)**
- **sizeof(N)** ≡ **sizeof(signed N)** ≡ **sizeof(unsigned N)**

在最后一行中，N 可以是 **char**、**short**、**int**、**long** 或 **long long**。此外，可以保证 **char** 至少有 8 位，**short** 至少有 16 位，**long** 至少有 32 位。**char** 可以保存机器字符集的一个字符。**char** 类型应由实现选择为在给定计算机上保存和操作字符的最合适的类型；它通常是一个 8 位字节。类似地，**int** 类型应被选择为在给定计算机上保存和操作整数的最合适的类型；它通常是一个 4 字节（32 位）字。不要假设更多。例如，有些机器的 **char** 为 32 位。假设 **int** 的大小与指针的大小相同是非常不明智的；许多机器（“64 位架构”）的指针比整数更大。请注意，并不保证 **sizeof(long)** < **sizeof(long long)** 或 **sizeof(double)** < **sizeof(long double)**。

一些基本类型的实现定义方面可以通过简单使用 **sizeof** 找到，更多内容可在 **<limits>** 中找到。例如：

```
#include <limits> // §40.2
#include <iostream>

int main() {
cout << “size of long ” << sizeof(1L) << ‘\n’; cout << “size of long long ” << sizeof(1LL) << ‘\n’;

cout << “largest float == ” << std::numeric_limits<float>::max() << ‘\n’;
cout << “char is signed == ” << std::numeric_limits<char>::is_signed << ‘\n’;
}
```

**<limits>**（§40.2）中的函数是 **constexpr**（§10.4），因此它们可以在不产生运行时开销的情况下使用，并且可以在需要常量表达式的上下文中使用。

基本类型可以在赋值和表达式中自由混合。在可能的情况下，值会被转换以不丢失信息（§10.5）。
如果值 **v** 可以精确表示为类型 **T** 的变量，则将 **v** 转换为 **T** 是值保持的。非值保持的转换最好避免（§2.2.2，§10.5.2.6）。

如果需要特定大小的整数，例如 16 位整数，可以 **#include** 标准头文件 **<cstdint>**，它定义了多种类型（或更确切地说是类型别名；§6.5）。例如：

```
int16_t x {0xaabb}; // 2bytes
int64_t xxxx {0xaaaaabbbbccccdddd}; // 8bytes
int_least16_t y; // at least 2 bytes (just like int)
int_least32_t yy // at least 4 bytes (just like long)
int_fast32_t z; // the fastest int type with at least 4 bytes
```

标准头文件 **<cstddef>** 定义了一个在标准库声明和用户代码中广泛使用的别名：**size_t** 是一个实现定义的无符号整数类型，可以容纳每个对象的字节大小。因此，它用于需要保存对象大小的地方。例如：

```
void *allocate(size_t n); // get n bytes
```

类似地，<cstddef> 定义了有符号整数类型 ptrdiff_t，用于保存减去两个指针得到的元素数量的结果。

## Section 6.2.9 Alignment 151
## 6.2.9 Alignment

对象不仅需要足够的存储空间来保存其表示。此外，在某些机器架构上，用于保存它的字节必须具有适当的对齐，以便硬件能够高效地（在极端情况下能够）访问它。例如，4 字节的 int 通常必须在字（4 字节）边界上对齐，有时 8 字节的 double 必须在字（8 字节）边界上对齐。当然，这完全取决于实现，对大多数程序员来说是完全隐式的。你可以在几十年内编写良好的 C++ 代码，而无需显式考虑对齐。对齐最常在对象布局中变得可见：有时结构体包含“空洞”以改善对齐（§8.2.1）。

alignof() 运算符返回其参数表达式的对齐方式。例如：

```
auto ac = alignof('c'); auto ai = alignof(1); auto ad = alignof(2.0);
```

```
// the alignment of a char // the alignment of an int // the alignment of a double
```

```
int a[20];
```

```
auto aa = alignof(a); // the alignment of an int
```

有时，我们需要在声明中使用对齐方式，其中 alignof(x+y) 这样的表达式是不允许的。相反，我们可以使用类型说明符 alignas：alignas(T) 表示“与 T 一样对齐”。例如，我们可以为某个类型 X 预留未初始化的存储空间，如下所示：

```
void user(const vector<X>& vx)
{
constexpr int bufmax = 1024;
alignas(X) buffer[bufmax]; // uninitialized

const int max = min(vx.size(),bufmax/sizeof(X));
uninitialized_copy(vx.begin(),vx.begin()+max,buffer); // ...
}
```

## 6.3 Declarations

在使用 C++ 程序中的名称（标识符）之前，必须先声明它。也就是说，必须指定其类型以告知编译器该名称指的是何种实体。例如：

```
char ch;
string s;
auto count = 1;
```

```
const double pi {3.1415926535897};
extern int error_number;
const char * name = “Njal”;
const char* season[] = { “spring”, “summer”, “fall”, “winter” }; vector<string> people { name, “Skarkhedin”, “Gunnar” }; struct Date { int d, m, y; };
int day(Date* p) { return p->d; }
double sqrt(double);
template<class T> T abs(T a) { return a<0 ? -a : a; }
```

```
constexpr int fac(int n) { return (n<2)?1:n*fac(n-1); } constexpr double zz { ii*fac(7) };
```

```
// possible compile-time evaluation (§2.2.3) // compile-time initialization
```

```
using Cmplx = std::complex<double>; struct User;
enum class Beer { Carlsberg, Tuborg, Thor }; namespace NS { int a; }
```

```
// type alias (§3.4.5, §6.5) // type name
```

从这些示例可以看出，声明不仅仅是简单地将类型与名称关联。大多数这些声明也是定义。定义是在程序中使用实体所需的所有内容都已提供的声明。特别是，如果表示某事物需要内存，则其定义会为该内存分配空间。另一种术语将声明视为接口的一部分，将定义视为实现的一部分。采用这种观点时，我们尝试用可以在单独文件中复制的声明来组成接口（§15.2.2）；为内存分配空间的定义不属于接口。

假设这些声明在全局作用域中（§6.3.4），我们有：

```
char ch;
auto count = 1;
const char* name = “Njal”;
```

```
// set aside memory for a char and initialize it to 0 // set aside memory for an int initialized to 1
// set aside memory for a pointer to char
// set aside memory for a string literal “Njal”
// initialize the pointer with the address of that string literal
```

```
struct Date { int d, m, y; }; int day(Date* p) { return p->d; }
```

```
// Date is a struct with three members
// day is a function that executes the specified code
```

```
using Point = std::complex<short>;// Point is a name for std::complex<short>
```

在上述声明中，只有三个不是定义：

```
double sqrt(double); extern int error_number; struct User;
```

```
// function declaration // variable declaration // type name declaration
```

也就是说，如果使用，它们所引用的实体必须在其他地方定义。例如：

```
double sqrt(double d) { /* ... */ }
```

```
int error_number = 1;
struct User {/*...*/};
```

在 C++ 程序中，每个名称必须有且仅有一个定义（对于 #include 的影响，参见 §15.2.3）。然而，可以有多个声明。

实体的所有声明必须在其类型上达成一致。因此，此片段有两个错误：

```
int count;
int count; // error : redefinition
```

## Section 6.3 Declarations 153

```
extern int error_number;
extern short error_number; // error : type mismatch
```

这没有错误（对于 extern 的使用，参见 §15.2）：

```
extern int error_number;
extern int error_number; // OK: redeclaration
```

一些定义明确指定了它们所定义实体的“值”。例如：

```
struct Date { int d, m, y; };
using Point = std::complex<short>; // Point is a name for std::complex<short>
int day(Date* p) { return p->d; }
const double pi {3.1415926535897};
```

对于类型、别名、模板、函数和常量，“值”是永久的。对于非 const 数据类型，初始值以后可能会更改。例如：

```
void f()
{
int count {1}; // initialize count to 1
const char* name {"Bjarne"}; // name is a variable that points to a constant (§7.5)
count = 2; // assign 2 to count
name = "Marian";
}
```

在定义中，只有两个没有指定值：

```
char ch;
string s;
```

参见 §6.3.5 和 §17.3.3，了解变量何时以及如何被赋予默认值。任何指定值的声明都是定义。

## 6.3.1 The Structure of Declarations

声明的结构由 C++ 语法定义（§iso.A）。该语法从早期的 C 语法开始，历经四十年演变，相当复杂。然而，在不做太多激进简化的情况下，我们可以将声明视为具有五个部分（按顺序）：

- 可选的前缀说明符（例如，static 或 virtual）
- 基本类型（例如，vector<double> 或 const int）
- 可选包含名称的声明符（例如，p[7]、n 或 *(* )[]）
- 可选后缀函数说明符（例如，const 或 noexcept）

