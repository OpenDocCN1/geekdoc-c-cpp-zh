
```
{
return a += b; // access representation through +=
}
```

对该运算符+()的参数按值传递，因此 a+b 不会修改其操作数。给定这些声明，我们可以写：

```
void f(complex x, complex y, complex z)
{
complex r1 {x+y+z}; // r1 = operator+(operator+(x,y),z)
complex r2 {x}; // r2 = x
r2 += y; // r2.operator+=(y)
r2 += z; // r2.operator+=(z)
}
```

除了可能的效率差异外，r1 和 r2 的计算是等价的。复合赋值运算符如 += 和 *= 通常比其“简单”对应运算符 + 和 * 更容易定义。这起初让大多数人感到惊讶，但它源于这样一个事实：+ 操作涉及三个对象（两个操作数和结果），而 += 操作只涉及两个对象。在后一种情况下，通过消除对临时变量的需求，运行时效率得到提高。例如：

```
inline complex& complex::operator+=(complex a)
{
re += a.re;
im += a.im;
return *this;
}
```

这不需要临时变量来保存加法的结果，并且编译器很容易将其完美内联。

一个好的优化器也会为普通 + 运算符的使用生成接近最优的代码。然而，我们并不总是拥有好的优化器，而且并非所有类型都像 complex 那样简单，因此 §19.4 讨论了通过直接访问类的表示来定义运算符的方法。

## 18.3.2 混合模式算术

为了处理 2+z，其中 z 是 complex，我们需要定义 operator + 以接受不同类型的操作数。在 Fortran 术语中，我们需要混合模式算术。我们可以通过添加运算符的适当版本来简单实现：

```
class complex {
double re, im;
public:
complex& operator+=(complex a) {
re += a.re; im += a.im; return *this; }
```

接受单个参数指定了从其参数类型到构造函数的类型的转换。例如：

```
class complex {
double re, im;
public:
complex(double r) : re{r}, im{0} { } // 从 double 构建 complex
// …
};
```

构造函数指定了实数轴在复平面中的传统嵌入。

构造函数是创建给定类型值的规定。当期望一个类型的值并且该值可以通过构造函数从作为初始化器或赋值值的提供值创建时，就会使用构造函数。因此，接受单个参数的构造函数不必显式调用。例如：

```
complex b {3};
```

意味着

```
complex b {3,0};
```

用户定义的转换仅在唯一时才会被隐式应用 (§12.3)。如果您不希望构造函数被隐式使用，请将其声明为 explicit (§16.2.6)。

自然地，我们仍然需要接受两个 double 的构造函数，并且默认构造函数将 complex 初始化为 {0,0} 也很有用：

```
class complex {
double re, im;
public:
complex() : re{0}, im{0} { }
complex(double r) : re{r}, im{0} { }
complex(double r, double i) : re{r}, im{i} { }
// …
};
```

使用默认参数，我们可以缩写：

```
class complex {
double re, im;
public:
complex(double r =0, double i =0) : re{r}, im{i} { }
// …
};
```

默认情况下，复制 complex 值被定义为复制实部和虚部 (§16.2.2)。例如：

```
void f()
{
complex z;
complex x {1,2};
```

```
complex y {x}; // y 也有值 {1,2} z=x; // z 也有值 {1,2}
}
```

## 18.3.3.1 操作数的转换

我们为四种标准算术运算符中的每一种定义了三个版本：

```
complex operator+(complex,complex);
complex operator+(complex,double);
complex operator+(double ,complex);
// ...
```

这可能会很繁琐，而繁琐的事情很容易出错。如果每个函数每个参数的类型有三种替代方案怎么办？我们需要每个单参数函数的三个版本，每个双参数函数的九个版本，每个三参数函数的 27 个版本，等等。通常这些变体非常相似。事实上，几乎所有变体都涉及将参数转换为通用类型然后执行标准算法的简单转换。

为每种参数组合提供函数的不同版本的一种替代方法是依赖转换。例如，我们的 complex 类提供了一个将 double 转换为 complex 的构造函数。因此，我们只需声明 complex 的相等运算符的一个版本：

```
bool operator==(complex,complex);
```

```
void f(complex x, complex y) {
x==y; // 意味着 operator==(x,y)
x==3; // 意味着 operator==(x,complex(3))
3==y; // 意味着 operator==(complex(3),y)
}
```

出于某些原因，可能更喜欢定义单独的函数。例如，在某些情况下，转换会带来开销，而在其他情况下，对于特定参数类型可以使用更简单的算法。在这些问题不显著的情况下，依赖转换并仅提供函数的最通用变体——以及可能几个关键变体——可以遏制混合模式算术可能产生的变体组合爆炸。

当存在函数的多个变体或运算符时，编译器必须根据参数类型和可用的（标准和用户定义）转换来选择“正确”的变体。除非存在最佳匹配，否则表达式是模糊的并且是错误（参见 §12.3）。

在表达式中通过构造函数显式或隐式构造的对象是自动的，并且将在第一个机会时被销毁（参见 §10.3.4）。
不会对 .（或 ->）的左手边应用隐式用户定义转换。这即使在 . 是隐式的情况下也是如此。例如：

```
void g(complex z)
{
3+z; // OK: complex(3)+z
3.operator+=(z); // error :3 is not a class object
```

```
3+=z; // error :3 is not a class object
}
```

因此，您可以通过将该运算符设为成员来近似运算符要求其左操作数为左值的概念。然而，这只是近似，因为可以使用修改操作（如 operator+=( )）访问临时对象：

```
complex x {4,5}
complex z {sqrt(x)+={1,2}}; // like tmp=sqrt(x), tmp+={1,2}
```

如果我们不想要隐式转换，我们可以使用 explicit 来抑制它们 (§16.2.6, §18.4.2)。

## 18.3.4 字面量

我们有内置类型的字面量。例如，1.2 和 12e3 是 double 类型的字面量。对于 complex，我们可以通过声明 constexpr 构造函数 (§10.4) 来非常接近地实现这一点。例如：

```
class complex {
public:
constexpr complex(double r =0, double i =0) : re{r}, im{i} { }
// ...
}
```

有了这个，complex 可以在编译时从其组成部分构造，就像内置类型的字面量一样。例如：

```
complex z1 {1.2,12e3};
constexpr complex z2 {1.2,12e3}; // 保证编译时初始化
```

当构造函数简单且内联时，尤其是当它们是 constexpr 时，将字面量参数的构造函数调用视为字面量是相当合理的。

我们可以更进一步并引入用户定义的字面量 (§19.2.6) 来支持我们的 complex 类型。特别是，我们可以定义 i 为表示“虚数”的后缀。例如：

```
constexpr complex<double> operator "" i(long double d) // 虚数字面量
{
return {0,d}; // complex 是字面量类型
}
```

这将允许我们写：

```
complex z1 {1.2+12e3i};
```

```
complex f(double d) {
auto x {2.3i};
return x+sqrt(d+12e3i)+12e3i;
}
```

这个用户定义的字面量给我们一个优势，超过 constexpr 构造函数所能提供的：我们可以在表达式中间使用用户定义的字面量，而 {} 记法只能在由类型名限定时使用。上面的示例大致等价于：

```
complex z1 {1.2,12e3};
complex f(double d) {
complex x {0,2.3};
return x+sqrt(complex{d,12e3})+complex{0,12e3};
}
```

我怀疑字面量的风格选择取决于你的审美感和你工作领域的惯例。标准库的 complex 使用 constexpr 构造函数而不是用户定义的字面量。

## 第 18.3.4 节 字面量 541

## 18.3.5 访问器函数

到目前为止，我们只为 class complex 提供了构造函数和算术运算符。这对于实际使用来说还不够。特别是，我们通常需要能够检查和更改实部和虚部的值：

```
class complex {
double re, im;
public:
constexpr double real() const { return re; }
constexpr double imag() const { return im; }
void real(double r) { re = r; }
void imag(double i) { im = i; }
// ...
};
```

我不认为提供对类所有成员的单独访问是个好主意；通常不是这样。对于许多类型，单独访问（有时称为 get-and-set 函数）是灾难的邀请。如果我们不小心，单独访问可能会破坏不变量，并且通常会使表示的更改变得复杂。例如，考虑从 §16.3 的 Date 或（甚至更多）从 §19.3 的 String 提供每个成员的 getter 和 setter 所带来的误用机会。然而，对于 complex，real() 和 imag() 在语义上是重要的：一些算法如果能够独立设置实部和虚部则可以更清晰地编写。例如，给定 real() 和 imag()，我们可以将简单、常见且有用的操作，如 ==，简化为非成员函数（而不损害性能）：

```
inline bool operator==(complex a, complex b)
{
return a.real()==b.real() && a.imag()==b.imag();
}
```

## 18.3.6 辅助函数
