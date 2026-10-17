
类模板的特化在一个编译单元内至少有一个实例化点。任何模板的特化在多个编译单元内可能有实例化点。如果两个实例化点根据单一定义规则（6.5.2, 6.5.3）赋予模板特化不同的含义，则程序格式错误，不需要诊断。

### 13.8.5.2 候选函数

1 对于后缀表达式为依赖名称的调用，使用模板定义上下文的查找规则（6.5.2, 6.5.3）查找候选函数。

> [注 1: 对于使用关联命名空间的查找点 (6.5.3)，模板实例化上下文中的函数声明通过此查找被找到，如 6.5.3 所示。结束注]；

如果考虑了所有编译单元中在命名空间内引入的外部链接函数后，该调用是格式错误的，或者在关联命名空间的查找中能找到更好的匹配，则程序具有未定义行为。

[示例 1:

```
Source file "X.h":
namespace Q {
    struct X { };
}
```

```
Source file "G.h":
namespace Q {
    void g_impl(X, X);
}
```

M1 的模块接口单元：

```
module;
#include "X.h"
#include "G.h"
export module M1;
export template<typename T>
void g(T t, Q::X x) {}; // ADL 在定义环境中找到 Q::g_impl，g_impl 未被丢弃
```

M2 的模块接口单元：

```
module;
#include "X.h"
export module M2;
import M1;
void h(Q::X x) {
    g(x); // OK
}
```

```
-- 示例结束
```

[示例 2:

Std 的模块接口单元：

```
export module Std;
export template<typename Iter>
void indirect_swap(Iter lhs, Iter* rhs) {
    swap(*lhs, *rhs); // swap 无法通过非限定查找找到，只能通过 ADL 找到
}
```

M 的模块接口单元：

```
export module M;
import Std;
struct S { /* ... */; };
void swap(S& s, S& k); // #1
```

```
void f(S* p, S* q) {
    indirect_swap(p, q); // 在实例化环境中通过 ADL 找到 #1
}
```

```
-- 示例结束
```

[示例 3:

```
Source file "X.h":
struct X { /* ... */; };
nX operator+(X, X);
```

F 的模块接口单元：

```
export module F;
```

```
export template<typename T>
void f(T t) {
  t + t;
}
```

```
M 的模块接口单元:
module;
#include "X.h"
export module M;
import F;
void g(T x) {
  f(x);
}
```

```
// 从 F 实例化 f，
// operator+ 在实例化环境中可见
```

```
-- 示例结束
```

[示例 4]

A 的模块接口单元：

```
export module A;
export template<typename T>
void f(T t) {
  cat(t, t);
  dog(t, t);
}
```

```
// #1
//#2
```

B 的模块接口单元：

```
export module B;
import A;
export template<typename T, typename U>
void g(T t, U u) {
  f(t);
}
```

源文件 "foo.h"，不是可导入的头文件：

```
struct foo {
  friend int cat(foo, foo);
  int dog(foo, foo);
}
```

C1 的模块接口单元：

```
module;
#include "foo.h"
export module C1;
import B;
export template<typename T>
void h(T t) {
  g(foo{ }, t);
}
```

翻译单元：

```
import C1;
void i() {
  h(0);
}
```

```
// error: dog 在 #2 未找到
```

可导入头文件 "bar.h"：

```
struct bar {
  friend int cat(bar, bar);
  int dog(bar, bar);
}
```

C2 的模块接口单元：

```
module;
#include "bar.h"
// 导入头单元 "bar.h"
export module C2;
import B;
export template<typename T>
void g(T t) {
    g(bar(t));
}
```

翻译单元：

```
import C2;
void k() {
    j(0);
// OK, 在实例化环境中找到 dog：
// 在 C2 模块接口单元的末尾可见
}
```

``` -- 示例结束
```

# 13.8.6 类模板内声明的友元名称 [temp.inject]

- 1 可以在类模板内声明友元或函数。当模板实例化时，其友元名称被视为在实例化点已显式声明的特化版本。

- 2 作为非模板类，类特化类的命名空间作用友元名称在查找期间不可见，除非在命名空间作用域显式声明（11.9.4）。此类名称可能根据关联类的规则（6.5.3）找到。

示例 1：

```
template<typename T> struct number {
    number(int);
    friend number gcd(number x, number y) { return 0; }
}
void g() {
    number<double> a(3, b);
    a = gcd(a,b); // 找到 gcd是因为 number<double> 是关联类，
    // 使 gcd 在其命名空间（全局作用域）中可见
    b = gcd(3,4); // error gcd 不可见
}
```

-- 示例结束

# 13.9 模板实例化与特化 [temp.spec.general]

## 13.9.1 通用

- 1 实例化函数、类、类的成员或成员的行为称为模板实例化。

- 2 从模板实例化的函数称为实例化函数。从模板实例化的类称为实例化类。从类定义实例化的成员函数、成员枚举或静态数据成员分别称为实例化函数、成员枚举或静态数据。从成员模板实例化的成员函数称为实例化函数。从成员模板实例化的类称为实例化类。从变量模板实例化的变量称为实例化变量。从静态模板实例化的静态数据成员称为实例化数据成员。

- 3 可以为函数、变量模板、类模板、类模板的成员或成员模板声明显式特化。显式特化由模板引入。在函数模板或成员函数的显式声明中，显式特化的函数或成员名称可以是模板标识符（template-id）。即使在模板声明或实例化时，友元声明也不会向作用域引入新名称。

示例 1：

```
template<class T = int> struct A {
    static int x;
};
template<class T> A<double>; // 特化 T == double
template<class T> A<int>; // 特化 T == int
template<class U> g(char) {}; // 特化 U == char
template<void> g(int)(int) { // U 从参数类型推导
    A<char>::x = 0; // 特化 T == char
}
template<class T = int> struct B {
    static int x;
};
template<class T> B<int>::x = 1; // 特化 T == int
```

-- 示例结束

- 4 实例化的模板特化可以通过给定参数列表实例化（13.9.2）或显式实例化（13.9.3）。特化是一个变量、函数或类成员，其来自模板的实例化（13.9.2）或模板的显式特化（13.9.4）。

- 5 对于给定的模板和参数集，

(1) 显式实例化定义在程序中最多出现一次，

(2) 显式特化在程序中最多出现一次，如 6.3 所示，

(3) 显式实例化和显式特化的声明不能出现在程序中。实现不需要诊断此类违规。

- 6 通常的访问检查规则不适用于实例化或显式特化声明中的名称，但函数体、默认参数、基类句、成员说明、枚举列表或静态数据成员初始化器中的名称除外。

注意：特别是如果表达式的语义依赖于类特化的成员或基类列表，则类模板特化会被隐式生成。例如，删除类指针取决于该类是否声明了析构函数，而类指针之间的转换取决于两个类之间的继承关系。

示例 1：

```
template<class T> class B { /* */; };
template<class T> class D : public B<T> { /* */; };

void f(void*);
void f(B<int>* p);

void g(D<int>* p, D<char>* pp) {
  // 需要实例化 D<int>：调用 f(B<int>)
  B<char>* q = pp; // 需要实例化 D<char>：将 D<char>* 转换为 B<char>*
  delete pp; // 需要实例化 D<double>
}
```

- 7 每个从模板实例化的类特化都有其任何静态成员的拷贝。

示例 2：

```
template<class T> class X {
    static T s;
};
template<class T> X<T>::s = 0;
X<int>* x;
X<char>* b;

X<int>* 拥有类型为 int 的静态成员，而 X<char>* 拥有类型为 char 的静态成员。
```

-- 示例结束

- 8 如果函数声明通过依赖类型（13.8.2）获取其函数类型而不使用函数标识符的形式，则程序是错误的。

示例 3：

```
template<class T> struct A {
    static T t;
};
typedef int function();
A<function> a; // error: 将声明 A<function>::t 为静态成员
```

-- 示例结束

## 13.9.2 隐式实例化

如果模板特化 E 有可达的显式实例化定义（13.9.3）或显式声明（13.9.4），或者如果 E 有可达的隐式实例化且不是：

- 从其初始化器或返回值推导出类型的内联函数（9.2.6），

- 潜在的常量变量（7.7），

- 模板的特化。

注意：翻译单元中的隐式实例化不能使用来自导入翻译单元（6.6）的内部链接名称。

除非类模板特化作为声明的特化被引用，否则当特化在包含完全定义对象类型或类型完整性影响程序语义的环境中被引用时，类模板会被隐式实例化。

注意：特别是如果表达式的语义依赖于类特化的成员或基类列表，则类模板特化会被隐式生成。例如，删除类指针取决于该类是否声明了析构函数，而类指针之间的转换取决于两个类之间的继承关系。

示例 1：

```
template<class T> class B { /* */; };
template<class T> class D : public B<T> { /* */; };

void f(void*);
void f(B<int>* p);

void g(D<int>* p, D<char>* pp) {
  // 需要实例化 D<int>：调用 f(B<int>)
  B<char>* q = pp; // 需要实例化 D<char>：将 D<char>* 转换为 B<char>*
  delete pp; // 需要实例化 D<double>
}
```

如果类在实例化点已声明但未定义（13.8.5.1），则实例化产生一个不完整的类类型（6.8）。

示例 2：

```
template<class T> class X;
Xchar* ch; // error: 不完整类型 Xchar
```

注意：3：在模板声明内部，局部类（11.6）或枚举以及局部类的成员从未被视为可以单独实例化的实体（这包括它们的默认参数、noexcept 说明和静态数据成员初始化器，如果有，但不包括它们的约束-requires）。结果是名称会被查找，语义约束会被检查，任何模板都会作为声明该类的实体的一部分被实例化。

类模板特化的隐式实例化会导致

- 声明的隐式实例化

- 删除成员函数、无作用域成员枚举和成员匿名定义的隐式实例化

类模板特化的隐式实例化不会导致类成员默认参数或 noexcept 说明的隐式实例化。

示例 3：

```
template<class T>
struct C {
  void f() { T; };
}
```

# ISO/IEC 14882:20(E)

```cpp
void g() = delete;

C<void> c;                // OK，此处未实例化 C<void>::f
template<class> void C<int>::g() {} // 重定义了 C<int>::
// 示例结束
```

然而

示例 4：

```cpp
template<class T, class U>
struct Outer {
	template<class X, class Y> struct Inner {
	template<class Y> Inner<X, Y>;   // #1a
	template<class Y> Inner<T, Y> {}; // #1b; OK: 重定义了 #1a
	template<class Y> Inner<U, Y>;   // #2
	};
};
```

```
Outer, int outer;
Outer<int>::Inner<int> 在 #1b 处被重复声明（它没有被定义，但被标记为与 Outer<T,U> 中的定义相关）；#2 是同一个偏特化化的无效声明）。
```

```cpp
template<typename T> struct Friendly {
	template<typename D> friend int f(D) { return sizeof(T); }
};
Friendly<float> f;
float f(); // 错误产生了 f(U) 的第二个定义
// 示例结束
```

+   4 除非类模板成员或成员模板是已声明的特化版本，否则当特化版本被引用于需要成员存在的上下文中，或者定义的存在会影响程序语义时，该成员不会被实例化；特别是，静态成员的初始化（或任何相关的副作用）不会发生，除非该静态成员本身以需要静态成员存在的方式被使用。

+   5 除非函数模板是已声明的特化版本，否则当特化版本被引用于需要函数定义的上下文中，或者定义的存在会影响程序语义时，该函数模板会被实例化。当一个从函数模板实例化为定义的函数声明，在被引用于需要函数定义的上下文中，或者定义的存在会影响程序语义时，会被隐式实例化。当调用函数模板特化版本、或显式特化类模板的成员、函数模板的默认参数或类模板的成员时，如果函数在需要默认参数值的上下文中调用，则会被实例化。

> [注意 4：作为显式声明部分的内联函数不是已声明的特化版本；其意图是在 odr-used（6.3）时被隐式实例化，以便考虑对其进行内联，但在翻译单元中不生成其行外代码。-- 注意]

+   6 示例 5：

```cpp
template<class T> struct Z {
	void f();
	void g();
};

void h() {
	Z<int> a;                // 需要实例化类 Z<int>
	Z<char*> p;               // 不需要实例化类 Z<char*>
	Z<double*> q;            // 不需要实例化类 Z<double*>

	a.f();                   // 需要实例化 Z<int>::f()
	p->g();                  // 需要实例化 Z<int>::g()
}
```

§ 13.9.2 ISO/IEC 2020 – 版权所有 420

# ISO/IEC 14882:2020(E)

```cpp
}
// 实例化 Z<char>::g()
```

此示例中没有任何内容要求类 Z<double>、Z<int>::g() 或 Z<char>::f() 被隐式实例化。

// 示例结束

+   7 除非变量模板特化是已声明的，否则当它被引用于需要变量定义的上下文中，或者定义的存在会影响程序语义。当变量模板被引用于需要该变量模板的上下文中，变量模板的默认模板会被隐式实例化。

+   8 如果变量或函数用于常量求值，则该变量或函数的定义被认为影响程序语义。

```cpp
// 示例结束
template<typename T> struct S {
	T value;
};

template<typename T>
S<int> s;

template<typename T>
S<float> f;

void g() {
    s<int> x; // 实例化 s
    f<float> y; // 需要实例化 f
}
```

```cpp
template<typename T>
struct S {
	T value;
};

template<typename T>
S<int> s;

template<typename T>
S<float> f;

void g() {
    s<int> x; // 实例化 s
    f<float> y; // 需要实例化 f
}
```
