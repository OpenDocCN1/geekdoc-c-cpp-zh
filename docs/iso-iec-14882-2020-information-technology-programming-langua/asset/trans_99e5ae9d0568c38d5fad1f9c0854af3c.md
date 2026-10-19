

# ISO/IEC 14882:2020(E)

对于 v1 和 v2，initializer_list 对象是函数调用中的一个参数，因此为 { 1, 2, 3 } 创建的数组具有完整表达式生命周期。对于 i3，initializer_list 对象是一个变量，因此数组在变量的生命周期内持续存在。对于 i4，initializer_list 对象在构造函数构造器初始化列表中初始化，就像将临时数组绑定到引用成员一样，因此程序是不良形成的（11.10.3）。——示例结束]

[注意 6：实现可以自由地将数组分配在只读内存中，如果具有相同初始化器的显式数组可以如此分配。——注释结束]

7 缩窄转换是一种隐式转换

- (7.1) — 从浮点类型到整数类型，或
- (7.2) — 从 long double 到 double 或 float，或从 double 到 float，除非源是常量表达式并且转换后的实际值在可表示的值范围内（即使不能精确表示），或
- (7.3) — 从整数类型或无作用域枚举类型到浮点类型，除非源是常量表达式并且转换后的实际值将适合目标类型并且转换回原始类型时将产生原始值，或
- (7.4) — 从整数类型或无作用域枚举类型到不能表示原始类型所有值的整数类型，除非源是常量表达式，其在积分提升后的值将适合目标类型，或
- (7.5) — 从指针类型或指向成员的指针类型到 bool。

[注意 7：如上所述，此类转换在列表初始化的顶层不被允许。——注释结束]

[示例 14：

```
int x = 999;                     // x is not a constant expression
const int y = 999;
const int z = 99;
char c1 = x;                     // OK, though it potentially narrows (in this case, it does narrow)
char c2{x};                     // error: potentially narrows
char c3{y};                     // error: narrows (assuming char is 8 bits)
char c4{z};                     // OK: no narrowing needed
unsigned char uc1 = {5};        // OK: no narrowing needed
unsigned char uc2 = {-1};       // error: narrows
unsigned int ui1 = {-1};        // error: narrows
signed int si1 =
    { (unsigned int)-1 };       // error: narrows
int ii = {2.0};                 // error: narrows
float f1 { x };                 // error: potentially narrows
float f2 { 7 };                 // OK: 7 can be exactly represented as a float
bool b = {"meow"};             // error: narrows
int f(int);
int a[] = { 2, f(2), f(2.0) };  // OK: the double-to-int conversion is not at the top level
```

——示例结束]

## 9.5 函数定义 [dcl.fct.def]

### 9.5.1 一般情况 [dcl.fct.def.general]

1 函数定义的形式为

```
function-definition:
    attribute-specifier-seqopt decl-specifier-seqopt declarator virt-specifier-seqopt function-body
    attribute-specifier-seqopt decl-specifier-seqopt declarator requires-clause function-body

function-body:
    ctor-initializer opt compound-statement
    function-try-block
    = default ;
    = delete ;
```

对函数体的任何非正式引用应解释为对非终结符 function-body 的引用。函数定义中可选的 attribute-specifier-seq 属于该函数。virt-specifier-seq 只能是成员声明（11.4）时才可作为函数定义的一部分。

2 在函数定义中，void declarator ; 或 declarator ; 必须是一个如 9.3.4.6 中所述的良好形成的函数声明。函数只能在命名空间或类作用域中定义。函数定义的参数类型或返回类型不得是（可能是 cv 限定的）在函数体内不完整或抽象的类类型，除非该函数被删除（9.5.3）。

3 [示例 1：一个完整的函数定义的简单示例是

```
int max(int a, int b, int c) {
    int m = (a > b) ? a : b;
    return (m > c) ? m : c;
}
```

这里 int 是 decl-specifier-seq；max(int a, int b, int c) 是 declarator；{ /* ... */ } 是 function-body。——示例结束

4 ctor-initializer 仅在构造函数中使用；参见 11.4.5 和 11.10。

5 [注意 1：cv-qualifier-seq 影响成员函数体中 this 的类型；参见 7.5.2。——注释结束]

6 [注意 2：未使用的参数不必命名。例如，

```
void print(int a, int) {
    std::printf("a = %d\n",a);
}
```

——注释结束

7 在 function-body 中，函数局部预定义变量表示一个隐式定义（参见 6.4.3）的静态存储期块作用域对象。

8 函数局部预定义变量 __func__ 的定义方式就像提供了如下形式的定义

```
static const char __func__[] = "function-name";
```

其中 function-name 是一个实现定义的字符串。是否此类变量具有与程序中任何其他对象不同的地址是不确定的。97

[示例 2：

```
struct S {
    S() : s(__func__) { }        // OK
    const char* s;
};
void f(const char* s = __func__);   // error: __func__ is undeclared
```

——示例结束

### 9.5.2 显式默认函数 [dcl.fct.def.default]

1 函数体形式为 = default ; 的函数定义称为显式默认定义。显式默认的函数必须

- (1.1) — 是特殊成员函数或比较运算符函数（12.6.3），并且
- (1.2) — 没有默认参数。

2 显式默认特殊成员函数 F 的类型 T1 允许与如果隐式声明时将具有的类型 T2 不同，如下：

- (2.1) — T1 和 T2 可能具有不同的 ref-qualifiers；
- (2.2) — T1 和 T2 可能具有不同的异常规范；并且
- (2.3) — 如果 T2 具有 const C& 类型的参数，则 T1 的对应参数可以是 C& 类型。

如果 T1 在任何其他方面与 T2 不同，则：

- (2.4) — 如果 F 是赋值运算符，并且 T1 的返回类型与 T2 的返回类型不同或 T1 的参数类型不是引用，则程序是不良形成的；
- (2.5) — 否则，如果 F 在其首次声明时显式默认，则定义为已删除；
- (2.6) — 否则，程序是不良形成的。

3 显式默认且未定义为已删除的函数只有在是 constexpr 兼容的（11.4.4，11.11.1）时才可声明为 constexpr 或 consteval。首次声明时显式默认的函数是隐式内联的（9.2.8），并且如果它是 constexpr 兼容的，则是隐式 constexpr（9.2.6）。

```
struct S {
  constexpr S() = default;                 // error: implicit S() is not constexpr
  S(int a = 0) = default;                   // error: default argument
  void operator=(const S&) = default;       // error: non-matching return type
  ~S() noexcept(false) = default;           // OK, despite mismatched exception specification
private:
  int i;
  S(S&);
};
S::S(S&&) = default;                        // OK: defines copy constructor

struct T {
  T();
  T(T &&) noexcept(false);
};
struct U {
  T t;
  U();
  U(U &&) noexcept = default;
};
U u1;
U u2 = static_cast<U&&>(u1);                // OK, calls std::terminate if T::T(T&&) throws
```

——示例结束]

显式默认函数和隐式声明函数统称为默认函数，实现应为它们提供隐式定义（[11.4.5]、[11.4.7]、[11.5.3]、[11.4.6]），包括可能将它们定义为已删除。未作为析构函数的前景析构函数（[11.4.7]）被定义为已删除。既不是前景析构函数也不是合格特殊成员函数（[11.4.4]）的默认特殊成员函数被定义为已删除。函数在首次声明时既未显式默认也未删除且被用户声明时称为用户提供的。用户提供的显式默认函数（即在其首次声明后显式默认）在显式默认的位置定义；如果此类函数被隐式定义为已删除，则程序是不良形成的。

> [注意 1：在首次声明后将函数声明为默认可以提供高效执行和简洁定义，同时使演进代码库的稳定二进制接口成为可能。——注释结束]

```
struct trivial {
  trivial() = default;
  trivial(const trivial&) = default;
  trivial(trivial&&) = default;
  trivial& operator=(const trivial&) = default;
  trivial& operator=(trivial&&) = default;
  ~trivial() = default;
};

struct nontrivial1 {
  nontrivial1();
};
nontrivial1::nontrivial1() = default;  // not first declaration
```

——示例结束]

### 9.5.3 已删除定义

函数体形式为 = delete ; 的函数定义称为已删除定义。具有已删除定义的函数也称为已删除函数。

引用已删除函数（隐式或显式）的程序，除声明外，是不良形成的。

> [注意 1：这包括隐式或显式调用该函数以及形成指向该函数的指针或指向成员的指针。即使在并非潜在求值的表达式中的引用也适用。如果函数被重载，只有在重载决议选择了该函数时才引用该函数。虚拟函数的隐式 odr-use（[6.3]）本身并不构成引用。——注释结束]

