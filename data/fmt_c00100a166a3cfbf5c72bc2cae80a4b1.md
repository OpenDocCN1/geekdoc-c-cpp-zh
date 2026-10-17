
`template<double&> class Z;` // 允许

结束示例|

7 非类型模板参数是 "T" 的模板参数数组，或者类型 T 被调整为指向 T 的 "指针"。[示例：

`template<int> struct R { /* ... */ };`

`template<int[5]> struct S { /* ... */ };`

`int p;`

`R* p;` // 允许

`S* q;` // 由于调整而允许

`int v[5];` // 允许

`Rv w;` // 由于转换而允许

结束示例|

9 默认模板参数是在模板参数后通过 `=` 指定的模板参数（17.3）。对于任何不是模板参数包的模板模板参数（非类型、类型），都可以指定默认模板参数。可以在模板声明中指定默认模板参数。在成员函数定义的模板参数列表中不应指定默认模板参数。如果函数模板声明指定了默认模板参数，则该声明应为定义，并且是该翻译单元中该函数模板的唯一声明。

10 可用的默认参数集通过合并该模板之前的所有声明中的默认参数获得，方式类似于默认函数参数（11.3.6）。[示例：

`template<class T1, class T2 = int> class A;`

`template<class T1 = int, class T2 = int> class A;`

等同于

`template<class T1 = int, class T2 = int> class A;`

结束示例|

11 如果类模板、变量模板或别名模板的模板参数具有默认模板参数，后续每个都应是模板参数包。如果主类模板、主变量模板或别名模板也是模板参数包，它应该是最后一个模板参数。函数模板中的模板参数包后面应跟随另一个模板参数，除非该模板参数可以从函数的参数类型列表（11.3.5）推导出来或具有默认参数（17.8.2）。推导引导模板（17.9）中没有默认参数的模板参数应从推导引导模板的参数类型列表中推导。[示例：

```cpp
template<class T1 = int, class T2 = class> class B; // 错误
```

```cpp
// U 无法从参数类型列表推导也无法指定
template<class... T, class... U> void f() {} // 错误
template<class... T, class... U> void g() {} // 错误
```

# ISO/IEC 14882:2017(E)

— end example

12 模板参数不应在同一作用域内的两个不同声明赋予默认参数。
[Example]:

```cpp
template<class T = int> class X;
template<class T = int> class X { /* ... */ }; // error
```
— end example

13 在解析非类型模板参数的默认模板参数时，第一个非嵌套的 `>` 被视为模板参数列表的结束，而不是大于运算符。[Example]:

```cpp
template<int i = 3 > 4>
class X { /* ... */ }; // syntax error
template<int i = (3) > 4>
class Y { /* ... */ }; // OK
```
— end example

14 模板模板参数的模板参数的模板参数允许有一个默认模板参数。
当指定了此类参数时，它们适用于该模板参数作用域内的该模板参数....[Example]:

```cpp
template <class T = float> struct B {};
template <class TT = float> struct A {
inline void f();
inline void g();
template <class TT> T> void A<TT>::f() {
T--; // error TT 没有默认参数
}
template <class TT = char> T> void A<TT>::g() {
T--; // OK
}
```
— end example

15 如果模板参数是一个在其可选标识符前带有省略号的类型参数，或者是一个声明参数包为包展开的参数声明，那么该模板参数就是模板参数包（17.5.3）。一个作为参数声明的模板包是包展开。同样，一个包含一个或多个展开参数包的、带有模板参数列表的类型参数的参数包是包展开。一个作为包展开的模板参数包不会在同一个模板参数列表中展开....[Example]:

```cpp
template<class...> Types> class Tuple;
// Types 是一个模板类型参数包
// 不是包展开
template<class T, int...> struct multi_array;
// Dims 不是一个非类型模板参数包
// 不是包展开
template<class...> T> struct value_holder {
template<T... Values> struct apply {};
};
// Values 是一个非类型模板参数包
// 并且是包展开
template<class...> T, T... Values...> struct static_array;
// error: Values 在同一个模板参数列表中
// 展开模板类型参数 T
```
— end example

§ 17.1

©ISO/IEC 2017 – 保留所有权利

# ISO/IEC 14882:2017(E)

## 17.2 模板特化的名称

- 模板特化（17.7）可以通过模板标识符引用：
- 简单模板标识符:
- 模板名 <可选的模板参数列表>
- 模板标识符:
- 简单模板标识符:
- 运算符函数标识符 <可选的模板参数列表>
- 字面量运算符标识符 <可选的模板参数列表>
- 模板名:
- 模板参数列表:
- 模板参数列表 , 模板参数 ...opt（可选）
- 模板参数:
- 常量表达式
- 标识符表达式

> 注意：名称查找（6.4）用于将名称的使用与模板声明关联起来；即将名称识别为模板名。 — end note

- 为了让模板标识符通过模板参数显式限定，该名称必须已知是指一个模板。

- 在名称查找（6.4）发现一个名称是模板名，或者运算符函数标识符或字面量运算符标识符指向一组任一成员为函数的重载函数，那么如果后面跟着 `<`，则它始终被视为模板参数列表的分隔符，而不是运算符。在解析模板参数列表时，第一个非嵌套¹³⁶被视为分隔符而不是大于运算符。同样，第一个非嵌套被视为两个连续但不同的标记，其中第一个标记是模板参数列表的结束并完成了模板标识符。— — 注意：由此替换规则产生的第二个标记可能会终止模板标识符，也可能是不同构造的一部分（例如类型转换）。 — end note [Example:

```
template<int i> class Y { /* ... */ };
Xi<2> > x2;
Y<1> x3;
Y<X>>> x4;
Y<Y<1)>> x5;
// syntax error
```

如果模板名出现在模板参数列表或 `decltype` 之外，则称该模板出现在顶层。由类名（第 12 节）或枚举名（第 10.3 节）形成的限定标识符中，模板不出现在顶层。在使用的类型名（17.6）、详述类型规格（10.7.3）、使用声明（10.3.3）或类 `decltype`（第 13 节）中，顶层可选的关键字 `template` 被忽略。在这些范围内，`<` 始终用于引入模板参数列表。在所有其他范围内，当命名一个未知特化（17.6.2.1）的成员的模板特化时，该成员模板名应带有 `template` 前缀。[Example: 

```
struct X {
    template<size_t> X alloc();
    template<size_t> static X adjust();
};
template<class T> void f(T* p) {
    T* q = p->alloc<200>();
    T* r = p->alloc<200>();
    T::adjust(100);
    T::adjust(100);
}
```

`template` 前缀的名称应该是模板标识符，或者该名称指向一个类模板或数组模板。[注意：带有 `template` 前缀的名称应该是模板标识符，或者该名称指向一个类模板或数组模板。]¹³⁶包含了 `dynamic_cast`、`static_cast`、`reinterpret_cast` 或 `const_cast` 的类型标识，或包含了后续模板标识符的模板参数，对于本描述而言是必要的。

- 6. 指向类名（第 12 节）的模板标识符。
7. 指向别名的模板标识符。

## 17.3 模板参数

模板参数有三种形式，对应模板参数。当模板声明的参数是包（17.5.3）时，它对应于零或多个模板参数。示例： 

```
template<class T> class Array {
    T* v;
    int sz;
public:
    explicit Array(int);
    T& operator[](int);
    T& elem(int i) { return v[i]; }
};
Array<int> v1(20);
typedef std::complex<double> dcomplex; // std::complex 是标准库
Array<dcomplex> v2(30);
Array<dcomplex> v3(40);
void bar() {
v1[3] = 7;
v3.elem(4) = dcomplex(7,8);
}
```

- 2. 在模板参数中，类型标识符和表达式之间的歧义解析为类型标识符，无论模板参数的形式如何。

- 3. 模板参数的名称在作为模板参数使用的地方应当是可访问的。
注意：如果模板参数的名称在作为模板参数使用的地方是可访问的，那么在使用了相应的模板参数名称的实例化中没有进一步的限制。示例：

```
template<class T> class X {
static T;
};
class Y {
private:
struct S { /* ... */ };
nX<S> x;
// OK: S 是可访问的
// XY::S 有一个类型为 Y::S 的静态成员
// OK: 即使 Y::S 是私有的
};
X<Y::S> y;
// Error: S 不可访问
```

对于模板参数，模板定义对该模板参数的成员没有特殊的访问权限。[示例：

```
template<class T, class D> class A {
typename T<int>::S s;
};
template<class U> class B {
private:
```

— end example.

137 默认模板参数没有歧义，因为模板参数的形式决定了模板参数的允许形式。

# ISO/IEC 14882:2017(E)

```cpp
struct S { /* ... */ 
};
A<B> b;
// 格式错误：A 没有访问 B:: 的权限
// 示例结束;
```

当使用模板参数或默认模板参数时，模板参数列表可以为空。空的 `<>` 括号应被用作模板参数列表。[示例：templateClass T = char String; String<*> p; // OK: String<char> String; // 语法错误 templateClass Tuple<*> t; // OK: Elements 是空的 // 语法错误 // // 示例结束]

对于类型为类模板对象的显式析构函数可以显式地指定模板参数。[示例：template<T> struct A { ~A();
 void f(A* p, A* q) {
 p->~A(); // OK: 调用析构函数
q->~A(); // OK: 调用析构函数
 } // 示例结束]

如果对模板参数的使用导致模板特化实例实例化产生了格式错误的结构，则该程序是格式错误的。

当模板标识符是一个重载函数模板时，则重载集合中的非模板函数以及重载集合中模板参数与模板参数不匹配的函数模板均被忽略。如果没有这些函数具有匹配的模板参数，则该程序是格式错误的。

当一个简单的模板参数没有名称时，当需要默认参数的值时，会隐式实例化一个默认模板参数（17.7.1）。[示例：templatetypename T, typename U = int* struct S { }; Sbool* p; // p 的类型是 Sbool, int*]

对于 U 的默认参数，在省略号处实例化是为了包展开（17.5.3）。

### 17.3.1 模板类型参数

对于类型为类型的模板参数的模板参数是一个类型标识符。

示例：
```cpp
template <class T> class X {};
template <class T> void f(T t) {}
struct { } unnamed_obj;
void f() {
struct A {};
enum { el }; };
```

17.3.1 ©/IECIEC2017 – 保留所有权利 350

```cpp
typedef struct { } B;
B b;
X<4> x1; // OK
X<4> x2; // OK
X<B> x3; // OK
f(el1); // OK
f(unnamed_obj); // OK
f(b); // OK
```

> [注：模板类型参数可以是不完整类型（6.9）。-- 注释结束]

### 17.3.2 模板非类型参数

- 如果非模板参数的类型通过模板推导包含一个占位符类型（10.1.7.4, 17.1），则推导出的参数根据模板参数的类型通过模板推导来确定（10.1.7.4.1）。如果推导出的参数类型在模板参数声明中是不允许的（17.1），则它是格式错误的。

- 对于非类型模板参数的模板参数应当是模板参数值的经过转换的常量表达式（8.2）。对于引用或指针类型的非类型模板参数，常量表达式的值不应引用以下对象的地址：

  - 主体（4.5），
  - 临时对象（15.2），
  - 字符串字面量（5.13.5），
  - 类型表达式的结果（8.2.8），或
  - 预命名的 __func__ 变量（11.4.1）。

> [注：如果模板参数代表一组重载函数（或指向此类函数的指针或指针成员），则从集合中选择匹配的函数（16.4）。-- 注释结束]

- [示例：
```cpp
template<const int*> ptr> struct X { /* ... */ };
int ai[];
X(ai); // 数组到指针及限定转换
struct Y {
template<const Y&> struct Z { /* ... */ };
Y y;
// 没有转换，但有额外的 cv 限定
Z(y);
template<int <span>> struct W { /* ... */ };
int b[5];
W(b); // 没有转换
void f(char);
void f(int);
template<void (*)(int)> struct A { /* ... */ };
A&f(int) a; // 选择了 f(int)
template<auto n> struct B { /* ... */ };
B<1 = b1; // OK: 模板参数类型为 int
B<'a'> = b2; // OK: 模板参数类型为 char
B<2.5> = b3; // error: 模板参数类型不能为 double
```
§ 17.3.2

©ISO/IEC 2017 - 保留所有权利 351

- 示例结束

[注：字符串字面量（5.13.5）不是可选模板参数。[示例：
```cpp
template<class T, const char*> class X {
/* ... */
};
int x1, "Studebaker"; // error: 字符串字面量作为模板参数
const char* p = "Viveist";
int x2; // OK
```

[注：元素或非静态成员的地址不是可选模板参数。[示例：
```cpp
template<int> class X { };
struct S { int m; };
int a[10];
X<&a[0]>; // error: 元素的地址
X<&S::m>; // error: 非静态成员的地址
X<int*>; // OK: 静态成员的地址
```]

[注：当相应的模板参数具有引用类型时，临时对象不是可选模板参数。[示例：
```cpp
template<const int&> struct B { /* ... */ };
B c1;
B(1); // error: 需要临时对象
```

### 17.3.3 模板参数

对于模板参数的模板参数应当是类模板或别名模板的名称，用 id 表达式表示。当模板参数命名一个类模板时，在将模板与相应参数进行匹配时，只考虑主类；如果其特化的参数列表与模板匹配，则不考虑这些特化。当基于模板参数的特化被实例化时，与主类或变量相关的任何特化都会被考虑在内。如果在实例化点处该特化是不可可见的，且它本应被选中，则需要进行诊断。[示例：
```cpp
template<class T> class A {
int x;
};
template<class T> class A<T*> { // 部分特化
long x;
};
```
§ 17.3.3 ISO/IEC 2017 - 保留所有权利 352

```cpp
template<class T> class A {
int x;
};
template<class T> class A<T*> { // 部分特化
long x;
};
```
