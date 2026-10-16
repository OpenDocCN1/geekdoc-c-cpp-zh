

```
constexpr complex(const complex<float>&);
explicit constexpr complex(const complex<long double>&);
```

```
constexpr double real(); void real(double);
constexpr double imag(); void imag(double);
```

```
// read the real part
// set the real part
// read the imaginary part
// set the imaginary part
```

```
complex<double>& operator= (double);
complex<double>& operator+=(double);
//...
```

```
};
```

显然，像 = 和 += 这样修改对象的操作不能是 constexpr。相反，像 real() 和 imag() 这样仅读取对象的操作可以是 constexpr，并且在给定常量表达式时可以在编译时求值。有趣的成员是从另一种 complex 类型的模板构造函数。考虑：

```
constexpr complex< float> z1 {1,2}; constexpr double re = z1.real();
constexpr double im = z1.imag(); constexpr complex<double> z2 {re,im}; constexpr complex<double> z3 {z1};
```

```
// note: <float> not <double>
// z2 becomes a copy of z1
// z3 becomes a copy of z1
```

## Section 10.4.4 Reference Arguments 267

拷贝构造函数之所以有效，是因为编译器识别出引用（const complex<float>&）引用的是一个常量值，并且我们只是使用该值（而不是尝试对引用或指针做任何高级或愚蠢的操作）。

文字类型允许进行类型丰富的编译时编程。传统上，C++ 编译时求值仅限于使用整数值（并且没有函数）。这导致代码不必要地复杂且容易出错，因为人们将每种类型的信息都编码为整数。模板元编程（第 28 章）的一些用法就是例子。其他程序员则更喜欢运行时求值，以避免在贫乏的语言中编写的困难。

## 10.4.5 Address Constant Expressions

静态分配对象的地址（§6.4.2），例如全局变量，是一个常量。然而，其值是由链接器分配，而不是编译器，因此编译器无法知道此类地址常量的值。这限制了指针和引用类型的常量表达式的范围。例如：

```
constexpr const char * p1 = “asdf”;
constexpr const char* p2 = p1; // OK
constexpr const char* p2 = p1+2; // error :the compiler does not know the value of p1
constexpr char c = p1[2]; // OK, c==‘d’; the compiler knows the value pointed to by p1
```

悄悄丢弃信息（“窄化转换”）。
编译器可以警告许多可疑的转换。幸运的是，许多编译器确实会这样做。
{}-初始化器语法可防止窄化（§6.3.5）。例如：

```
void f(double d)
{
char c {d}; // error :double-precision floating-point to char conversion
}
```

如果不可避免地需要可能窄化的转换，请考虑使用某种形式的运行时检查转换函数，例如 narrow_cast<>()（§11.5）。

## 10.5.2.1 Integral Conversions

整数可以转换为另一种整数类型。普通枚举值可以转换为整数类型（§8.4.2）。

如果目标类型为无符号，则结果值只是源中尽可能多的位以适应目标（如果需要则丢弃高位）。更精确地说，结果是与源整数模 2 的 n 次方同余的最小无符号整数，其中 n 是用于表示无符号类型的位数。例如：

```
unsigned char uc = 1023; // binary111111111: uc becomes binary11111111, that is,255
```

如果目标类型为有符号，则如果它可以在目标类型中表示，则值不变；否则，值是实现定义的：

```
signed char sc = 1023; // implementation-defined
```

合理的結果是 127 和 −1（§6.2.3）。
布尔值或普通枚举值可以隐式转换为其整数等价物（§6.2.2, §8.4）。

## 10.5.2.2 Floating-Point Conversions 269

## 10.5.2.2 Floating-Point Conversions

浮点值可以转换为另一种浮点类型。如果源值可以在目标类型中精确表示，则结果是原始数值。如果源值介于两个相邻目标值之间，则结果是这两个值之一。否则，行为未定义。例如：

```
float f = FLT_MAX; double d = f;
// largest float value // OK: d == f
double d2 = DBL_MAX; float f2 = d2;
```

```
long double ld = d2; long double ld2 = numeric_limits<long double>::max();
double d3 = ld2; // undefined if sizeof(long double)>sizeof(double)
```

```
DBL_MAX
```

和 FLT_MAX 在 <climits> 中定义；numeric_limits 在 <limits> 中定义（§40.2）。

```
// largest double value
// undefined if FLT_MAX<DBL_MAX
// OK: ld = d3
```

## 10.5.2.3 Pointer and Reference Conversions

任何指向对象类型的指针都可以隐式转换为 void*（§7.2.1）。指向派生类的指针（引用）可以隐式转换为指向可访问且无歧义的基的指针（引用）（§20.2）。请注意，指向函数或指向成员的指针不能隐式转换为 void*。

求值为 0 的常量表达式（§10.4）可以隐式转换为任何指针类型的空指针。同样，求值为 0 的常量表达式可以隐式转换为指向成员的类型（§20.6）。例如：

```
int * p = (1+2)*(2*(1-1)); // OK, but weird
```

优先使用 nullptr（§7.2.2）。

T* 可以隐式转换为 const T*（§7.5）。同样，T& 可以隐式转换为 const T&。

## 10.5.2.4 Pointer-to-Member Conversions

指向成员的指针和引用可以按 §20.6.3 中所述隐式转换。

## 10.5.2.5 Boolean Conversions

指针、整数和浮点值可以隐式转换为 bool（§6.2.2）。非零值转换为 true；零值转换为 false。例如：

```
void f(int * p, int i)
{
bool is_not_zero = p; // true if p!=0
bool b2 = i; // true if i!=0
```

指针到 bool 的转换在条件中很有用，但在其他地方令人困惑：

```
void fi(int);
void fb(bool);

void ff(int * p, int* q) {
if (p) do_something(*p); // OK
if (q!=nullptr) do_something(*q); // OK, but verbose
// ...
fi(p); // error :no pointer to int conversion
fb(p); // OK: pointer to bool conversion (surprise!?)
}
```

希望编译器对 fb(p) 发出警告。

## 10.5.2.6 Floating-Integral Conversions

当浮点值转换为整数值时，小数部分会被丢弃。换句话说，从浮点类型到整数类型的转换会截断。例如，int(1.6) 的值是 1。如果截断后的值无法在目标类型中表示，则行为未定义。例如：

```
int i = 2.7; // i becomes 2
char b = 2000.7; // undefined for 8-bit chars: 2000 cannot be represented as an 8-bit char
```

从整数到浮点类型的转换在硬件允许的范围内尽可能数学正确。如果积分值不能精确表示为浮点类型的值，则会发生精度损失。例如：

```
int i = float(1234567890);
```

在 int 和 float 都使用 32 位表示的机器上，i 的值是 1234567936。

显然，最好避免可能破坏值的隐式转换。事实上，编译器可以检测并警告一些明显危险的转换，例如从浮点到整数以及从 long int 到 char。然而，一般的编译时检测是不切实际的，因此程序员必须小心。当“小心”不够时，程序员可以插入显式检查。例如：

```
char checked_cast(int i)
{
char c = i; // warning: not portable (§10.5.2.1) if (i != c) throw std::runtime_error{"int-to-char check failed"}; return c;
}
```

```
void my_code(int i) {
char c = checked_cast(i);
```

## Section 10.5.2.6 Floating-Integral Conversions 271

表达检查转换的更通用技术在 §25.2.5.1 中介绍。

要以保证可移植的方式截断，需要使用 numeric_limits（§40.2）。

在初始化中，可以通过使用 {}-初始化器符号（§6.3.5）来避免截断。

## 10.5.3 Usual Arithmetic Conversions

这些转换在二元运算符的操作数上执行，以将它们带到共同类型，然后该类型用作结果的类型：

- [1] 如果任一操作数为 long double 类型，则另一个转换为 long double。
- • 否则，如果任一操作数为 double，则另一个转换为 double。
- • 否则，如果任一操作数为 float，则另一个转换为 float。
- • 否则，对两个操作数执行积分提升（§10.5.1）。

- [2] 否则，如果任一操作数为 unsigned long long，则另一个转换为 unsigned long long。
- • 否则，如果一个操作数为 long long int，另一个为 unsigned long int，则如果 long long int 可以表示 unsigned long int 的所有值，则 unsigned long int 转换为 long long int；否则，两个操作数都转换为 unsigned long long int。否则，如果任一操作数为 unsigned long long，则另一个转换为 unsigned long long。
- • 否则，如果一个操作数为 long int，另一个为 unsigned int，则如果 long int 可以表示 unsigned int 的所有值，则 unsigned int 转换为 long int；否则，两个操作数都转换为 unsigned long int。
- • 否则，如果任一操作数为 long，则另一个转换为 long。
- • 否则，如果任一操作数为 unsigned，则另一个转换为 unsigned。
- • 否则，两个操作数都是 int。

这些规则使得将无符号整数转换为可能

