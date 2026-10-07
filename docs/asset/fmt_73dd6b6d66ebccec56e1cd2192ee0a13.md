
```
literal
postfix-expression - pseudo-destructor-name
postfix-expression -> pseudo-destructor-name
sizeof unary-expression
sizeof ( type-id )
sizeof ~ ( identifier )
alignof ( type-id )
typeid ( expression )
typeid ( type-id )
  ::opt delete cost-expression
  ::opt delete { cast-expression }
throw assignment-expression-opt
except ( expression )
```

> [注：对于标准库偏移量，参见 18.2。-- 注结束]

5 如果类成员访问表达式（5.2.5）中的表达式引用了当前实例化成员且所引用成员的类型是依赖的，或者该类成员访问表达式引用了未知特化的成员，则它是类型依赖的。表达式的类型通常是类 x（或指向的类）的成员 y 的类型。然而，如果 x 引用的是一个不是当前实例化的依赖类型，则 `y` 的类型始终是依赖的。如果 x 引用的是非依赖类型或引用的是当前实例化，则 `y` 的类型就是类成员访问表达式的类型——注结束。

## 14.6.2.3 值依赖表达式 [temp.dep.contexpr]

1 除下文描述的情况外，如果任何子表达式是值依赖的，则常量表达式是值依赖的。

2 如果标识符满足以下条件，则它是值依赖的：

- 使用依赖类型声明的名称，
- 非类型参数的名称，
- 具有字面量类型的常量，且由一个值依赖的表达式初始化。

如果一元表达式或表达式是类型依赖的，或者类型是值依赖的，则以下形式的表达式是值依赖的：

```
sizeof unary-expression
sizeof ( type-id )
typeid ( expression )
typeid ( type-id )
alignof ( expression )
except ( expression )
```

> [注：对于标准库偏移量，参见 18.2。-- 注结束]

3 如果类型标识或简单类型说明符是依赖的，或者表达式或转换表达式是值依赖的，则以下形式的表达式是值依赖的：

```
simple-type-specifier
static_cast < type-id > ( expression )
const_cast < type-id > ( expression )
reinterpret_cast < type-id > ( expression )
( type-id ) cast-expression
```

4 以下形式的表达式是值依赖的：

5 如果类成员访问表达式（5.2.5）中的表达式引用了当前实例化成员且所引用成员的类型是依赖的，或者该类成员访问表达式引用了未知特化的成员，则它是类型依赖的。表达式的类型通常是类 x（或指向的类）的成员 y 的类型。然而，如果 x 引用的是一个不是当前实例化的依赖类型，则 `y` 的类型始终是依赖的。如果 x 引用的是非依赖类型或引用的是当前实例化，则 `y` 的类型就是类成员访问表达式的类型——注结束。

6 如果一个类型满足以下条件，则它是依赖的：

- 模板参数，
- 未知特化类的成员，
- 作为当前实例化成员的嵌套类或枚举，
- 被 cv 限定的类型，且其 cv 未限定的类型是依赖的，
- 由任何依赖类型构造的复合类型，
- 由依赖类型构造的数组类型，或其大小由从值依赖的常量表达式指定的数组类型，
- 简单模板标识（simple-template-id），其中模板名称是模板参数，或者任何模板参数是依赖类型，或者是类型依赖或从值依赖的表达式，或者由 `decltype(expression)` 表示，且其中 `expression` 是类型依赖的 (14.6.2.2)。

7 [注：由于 `typedef` 并不引入新类型，而是引用其他类型，因此指向当前实例化成员的 `typedef` 的名称仅当所引用的类型是依赖的时，该名称才是依赖的。-- 注结束]

### 依赖参数 [temp.arguments]

1 如果一个类型满足以下条件，则它是依赖的：

- 模板参数，
- 未知特化类的成员，
- 作为当前实例化成员的嵌套类或枚举，
- 被 cv 限定的类型，且其 cv 未限定的类型是依赖的，
- 由任何依赖类型构造的复合类型，
- 由依赖类型构造的数组类型，或其大小由从值依赖的常量表达式指定的数组类型，
- 简单模板标识（simple-template-id），其中模板名称是模板参数，或者任何模板参数是依赖类型，或者是类型依赖或从值依赖的表达式，或者由 `decltype(expression)` 表示，且其中 `expression` 是类型依赖的 (14.6.2.2)。

### 依赖名称 [temp.dep.res]

1 在解析依赖名称时，会考虑来自以下来源的：

- 来自模板的声明。
- 在模板定义上下文或模板实例化上下文中找到的声明。

2 与非模板类一样，类模板特化类的命名空间友元函数名称在命名空间作用域下的普通声明中是不可见的 (11.3)。此类名称可以在关联类的规则 (3.4.2) 下找到，142 [示例:

```cpp
template<typename T> struct number {
  number(int);
  friend gcd(number x, number y) { return 0; }
};

void g() {
  number<double> a(3), b(4);
  a = gcd(a,b); // 找到 gcd 因为 <double> 是
                // 关联类，使得 gcd 在
                // 命名空间（全局作用域）中可见
                // 错误；gcd 是不可见的
}
b  = gcd(3,4);
```

- 示例结束

## 14.7 模板实例化与特化

实例化函数、类模板成员或成员模板的行为称为模板实例化。

从函数模板实例化的函数称为实例化函数。从类模板实例化的类称为实例化类。类模板实例化的成员函数、成员类、成员枚举或静态数据成员，分别称为实例化成员函数、实例化成员类、实例化枚举或静态成员。从成员函数模板实例化的成员函数称为实例化成员函数。从成员模板实例化的成员类称为实例化成员类。

显式特化可以是函数模板、类模板、类模板成员或模板。显式特化声明由 `<template\` 引入。在类模板或类模板成员的显式特化声明中，被显式特化的类名称应为*简单模板标识 (simple-template-id)*。在函数模板或成员函数的显式特化声明中，被显式特化的函数或成员函数的名称可以是模板标识 (template-id)。[示例:

```cpp
template<class T = int> struct A {
  static int x;
};

template<class U> void g() {
  template<class T> struct A {}; // 为 T = double 特化
  template<class T> struct A {}; // 为 T = int 特化
  template<class U> void g(char) {} // 为 U = char 特化
} // U 根据参数类型推导

template<class U> void g(int) {
  template<int> int A<>::x = 0; // 为 T = int 特化
} // char

template<class T = int> struct B {
  static int x;
};

template<T> int B<>::x = 1; // 为 T = int 特化
```

142) 友元声明不会在任何作用域中引入新名称，即使在模板被声明或实例化时也是如此。

§ 14.7

ISO/IEC 14882:2011(E)

示例结束

4 实例化的模板特化可以是针对给定的列表隐式实例化 (14.7.1)，也可以是显式实例化 (14.7.2)。特化是指类、函数或类成员，它是被实例化或显式特化的 (14.7.3)。

5 对于给定的模板和给定的模板参数集合，

显式实例化在程序中最多出现一次，

显式特化在程序中最多定义一次（根据 3.2），并且

显式实例化和显式特化的声明不应出现在程序中，除非显式实例化跟在显式特化的声明之后。

实现并不强制要求诊断违反此规则的行为。

6 来自模板的每个类模板特化都有其自己的静态成员副本。

示例|

```cpp
template<class T> class X {
    static T s;
}
template<class T> T X<T>::s = 0;
X<int> aa;
X<char> bb;
```

X<int> 有一个类型为 int 的静态成员 s，X<char*> 有一个类型为 char 的静态成员 s。——示例结束

## 14.7.1 隐式实例化 [temp.inst]

7 除非类模板特化已被显式实例化 (14.7.2) 或显式特化 (14.7.3)，否则当特化引于需要完全定义对象类型的上下文，或者当类类型的完整性影响程序的语义时，该类模板特化被隐式实例化。类模板特化的隐式实例化会导致类函数、作用域成员枚举、静态数据成员和模板的成员实例化，但不会导致定义或默认参数；它会导致作用域成员枚举和成员匿名的隐式实例化；然而，为了根据 9.2 确定成员的实例化声明是否有效，与模板中的定义对应的声明被视为定义。示例|

```cpp
template<class T> class U {
struct Outer {
template<class X> class Y struct Inner {\ // 1a
template<class T> class Y struct Inner<T, Y>; // 1b; OK：#1a 的有效声明
template<class T> class Y Inner<U, Y> {}; // #2
};
Outer<int, int> outer; // 在 #2 处错误
```

Outer<int, int>::Inner<int, Y> 在 #1b 处重复声明。（它没有被定义，但没有与 Outer<T, U> 中的定义关联）也是 #1a 的声明。它没有与定义关联，因此是部分特化的无效重复声明。——示例结束

# § 14.7.1

© ISO/IEC 14882:2011 留所有权利保留 367

2 除非类模板或成员模板已被显式实例化或显式特化，否则当特化引于需要成员定义的上下文时，该成员特化被隐式实例化；特别是，静态成员的初始化（以及任何副作用）只有在静态成员本身以需要定义的方式使用时发生。

3 除非函数模板特化已被显式实例化或显式特化，当特化引于需要函数定义的上下文时，该函数被隐式实例化。函数模板显式特化或类模板成员、、类模板或成员模板的默认参数在函数调用于需要默认参数值的上下文时被隐式实例化。

4 [示例]:

```cpp
template<class T> struct Z {
  void f();
  void g();

  void h() {
    Z<int> e;
    Z<char> p;
    Z<double> q;

    // 需要实例化类 Z<int>
    // 不需要实例化类 Z<char>
    // 不需要实例化类 Z<double>

    e.f();
    p->g();
    // 需要实例化 Z<int>::f()
    // 需要实例化 Z<char>::g()，
    // 以及实例化 Z<double>::g()
  }
}
```

此示例中没有任何内容需要隐式实例化 Z<double>、Z<int>g() 或 Z<char>::f()。——示例结束

5 如果类被引于需要完全定义对象类型的上下文，或者类类型可能会影响程序的语义，则类特化被隐式实例化。[注：特别是，如果表达式的语义依赖于类模板特化的成员或基类，则会隐式生成该类模板特化。例如，指向类的转换取决于类是否有析构函数，指针类型转换取决于涉及的两个类之间的继承关系。

——示例结束]:

```cpp
template<class T> class B { /* ... */ };
template<class T> class B : public B { /* ... */; };

void f(void);
void f(B<int>*);

void g(D<int>* p, D<char>* pp, D<double>* ppp) {
  f(p);
  B<char>* q = pp; // 需要实例化 D<int>*：调用 f(B<int>*)
// 需要实例化 D<char>*；
// 将 D<char>* 转换为 B<char>*
  delete ppp; // 需要实例化 D<double>
}
```

——示例结束

# ISO/IEC 14882:2011(E)

6 如果重载解析过程可以在不实例化类模板的情况下确定要调用的正确函数，则实例化是否实际发生是未指定的。[示例：

```cpp
template <class T> struct S {
    operator int();
};

void f(int);
void f(S<int>&);
void f(S<float>&);

void g(S<int>& sr) {
    f(sr); // 允许实例化 S<int> 但并非强制
    // 允许实例化 S<float> 但并非强制
}

end example|
```

7 如果需要类模板特化的隐式实例化，且该模板已声明但未定义，则程序是构造异常的。[示例：

```cpp
template<class T> class X;

X<char> x; // X 的定义

end example|
```

8 类模板的隐式实例化不会导致该类的任何静态数据成员被隐式实例化。

9 如果以涉及重载解析的方式使用函数模板或成员模板特化，则该特化的声明将进行隐式实例化（14.8.3）。

10 实现不应对不需要实例化的类模板、成员模板、非虚成员函数、成员类或类模板的静态数据成员进行实例化。如果一个虚成员函数在其他情况下会被实例化，则实现是否隐式实例化该类模板的虚成员函数是未指定的。在默认参数中使用模板特化不会导致模板被隐式实例化，但在需要其完整类型来确定默认参数的正确性时，可以实例化类模板。在函数调用的特化中使用默认参数时，默认参数中的特化将进行隐式实例化。

11 隐式实例化的类和函数模板特化放置在模板定义的命名空间中。类模板成员的隐式实例化特化放置在所属类或类模板定义的命名空间中。隐式实例化的成员模板放置在所属类或类模板定义的命名空间中。[示例：

```cpp
namespace N {
    template<class T> class List {
    public:
        T* get();
    };
}

template<class K, class V> class Map {
    public:
        N::List<V> lt;
        void get(K);
};

void g(Map<const char*, int>& m) {
    int i = m.get("Nicholas");
} // 从 Map<const char*, int>::get() 调用 get() 会将 List<int>::get() 放置在命名空间中而非全局命名空间。end example

- 如果以需要默认参数的方式调用函数模板 f，则将查找依赖名，检查语义约束；如果该默认参数在与此处函数模板 f 具有相同作用域、相同模板参数和相同访问权限的函数模板特化中作为初始化器使用，则对默认参数中使用的任何模板进行实例化。这种分析被称为默认参数实例化。随后，实例化的默认参数将作为 f 的参数使用。

- 每个参数都是独立实例化的。[示例：
```cpp

template<class T> void f(T x, T y = ydef(T()), T z = zdef(T()));

class A {

    def(A);

};

void g(A a, A b, A c) {

    // 无默认参数实例化

    f(a, b);

    // 实例化默认参数 z = zdef(T())

    f(a);

} // 构造异常；ydef 未声明

``` end example]

> [注：14.6.4.1 定义了模板特化的实例化点。— 注结束 —]

- 存在一个实现定义的数量，用于指定递归实例化的总深度，这可能涉及多个模板。无限递归实例化的结果是未定义的。[示例：
```cpp

template<class T> class X {

X<T>* p;

};

// OK

X<T> 的隐式实例化

``` end example]

 § 14.7.2 显式实例化

- 函数模板、类或类模板的静态数据成员、类模板的成员函数、类模板的成员类或类模板的成员模板可以被显式实例化。显式实例化的语法为：

```cpp

template [template-parameter-list]

identifier;

```

- 显式实例化有两种形式：显式实例化定义和显式实例化声明。显式实例化声明以 **extern** 关键字开始。

- 如果显式实例化类或成员类，声明中的模板限定符应包含模板 ID。如果显式实例化成员函数，声明中的未限定标识符必须是模板 ID。[注：关于限定符中的限定名，见 8.3。 — 注]

- 如果显式实例化成员函数、类或类模板的静态数据成员，声明中的模板限定符应为简单模板。显式实例化应出现在模板的所属命名空间中。示例：

```cpp

template<class T> class Array { void mf(); };

template class Array<char>;

template void Array<int>::mf();

template<class T> void sort(Array<T>& v) { // ... }
```
