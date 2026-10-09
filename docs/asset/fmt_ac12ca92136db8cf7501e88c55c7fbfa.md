
```cpp
struct A {
  A() = default; // OK
  A(int v) : v(v) {} // OK
  const int& v = 42; // OK
};
A a;
A(2); // error: 遗憾，绑定引用的错误 // 示例
```

在非委托构造函数中，每个已构造类类型的析构函数可能会被调用（11.4.7）。

> [注 5：此规定确保了在抛出异常时可以对完全构造的子对象调用析构函数（14.3）。] 注

在非委托构造函数中，初始化按照以下顺序进行：

- 首先，对于最派生类（6.7.2），虚基类按照基类无环图的深度遍历顺序进行初始化，“从左到右”是基类在派生类基说明列表中出现的顺序。
- 然后，基类按照它们在基说明中的声明顺序进行初始化（无论初始化器的顺序如何）。
- 然后，非静态数据成员按照它们在类定义中的声明顺序进行初始化（同样不取决于初始化器的顺序）。
- 最后，执行构造函数体的复合语句。

> [注 6：强制声明顺序是为了确保基类和成员对象按照初始化的反序进行析构。注

示例 9:

```cpp
struct V {
  V();
  V(int);
};
struct A : virtual V {
  A();
  A(int);
};
```

§ 11.103 ©ISO/IEC 2020 – 所有权利保留 311

```cpp
struct B : virtual V {
B();
B(int);
};
```

```cpp
struct C : A, B, virtual V {
C();
C(int);
};
```

```cpp
A::A(int i) : V(i) { /* ... */ }
B::B(int i) { /* ... */ }
C::C(int i) : { /* ... */ }
```

```cpp
V() : V(int)
A(2) : V(int)
B(3) : V()
C(4) : V()
```

`*mem-initializer*`（成员初始化器）的`*expression-list*`（表达式列表）或 braced-init-list（大括号初始化列表）中的名称是在该`*mem-initializer*`所指定的构造函数的作用域内求求的。

示例 10:
```cpp
class X {
int a;
int b;
int i;
int j;
public:
const int& r;
X(int i) : r(a), b(i), i(i), j(this->i) { };
```

初始化 `X:a` 指向 `X::a`，并用构造函数参数 `i` 的值初始化 `X:b`，并用构造函数参数 `i` 的值初始化 `X::i`，以及用 `X::i` 的值初始化 `X::j`；这些操作在每次创建类 `X` 的对象时都会发生。 — 示例结束

> Note 7：由于 mem-initializers 在构造函数的作用域内求值，因此该指针可以在`*mem-initializer*`的`*expression-list*` 中用于指向正在初始化的对象。 — 示例结束

成员函数（包括虚函数，11.7.3）可以在对象构造期间被调用。同样，可以使用 `*typeid*` 运算符（7.6.1.8）或 `*dynamic_cast*`（7.7.2）构造对象。然而，如果这些操作在 ctor-initializer（构造函数初始化列表）（或从 ctor-initializer 直接或间接调用的函数）中，在所有基类的 mem-initializers 完成之前执行，程序将具有未定义行为。

示例 11:
```cpp
class A {
public:
int a;
};
class B : public A {
public:
int j;
int f();
B() : A(f()) { // 未定义行为：调用了成员函数但基类 A 未初始化
f(f()) {} // 定义良好：所有基类均已初始化
};
```
class C : B {
public:
int c;
C(int);
};
```

# ISO/IEC 14882:2020(E)

```cpp
class D : public B, C {
    int i;
public:
    D() : C(f()), // 未定义行为：在基类 C 尚未初始化之前调用了成员函数
        i(f()) {} // 定义良好：所有基类均已初始化
};
```

Note 8：11.10.5 描述了在定义良好的情况下，构造期间虚函数调用、typeid 和 dynamic_casts 的结果；即，描述了正在构造的对象的多态行为。 — 注释结束

跟随省略号的成员初始化器是一个包展开（pack expansion，13.7.4），用于初始化类基类规范中由包展开指定的基类。

示例 12:

```cpp
template<class... Mixins>
class X : public Mixins... {
public:
    X(const Mixins&... mixins) : Mixins(mixins...) {}
};
```

# 11.10.4 通过继承的构造函数初始化

当使用类型 `B` 的构造函数来初始化不同类型 `D` 的对象时（即当构造函数被继承（9.9））时），初始化过程就像使用默认构造函数来初始化 `D` 对象和每个继承自该构造函数的基类子对象，但 `B` 对象是通过调用继承的构造函数来初始化的。整个初始化被视为单次函数调用；该初始化在 `D` 对象任何部分的初始化之前顺序执行。

示例 1:

```cpp
struct B1 {
    B1(int, ... ) {}
};
struct B2 {
    B2(double) {}
};
int get();
struct D1 : B1 {
    using B1::B1; // 继承 B1(int, ...)
    int x;
    int y = get();
};
void test() {
    D1 d(2, 3, 4); // OK：通过调用 B1(2, 3, 4) 初始化 B1，
                   // 然后初始化 d.x（无初始化），
                   // 接着通过 get() 初始化 d.y
    D1 e;
    struct D2 : B2 {
        using B2::B2;
        B1 b;
    };
    D2 f(1); // 错误：B1 删除了默认构造函数
    struct W { W(W) };
    struct X : virtual W { using W::W; X() = delete; };
    struct Y : X { using X::X; }
}
```

ISO/IEC 14882:2020(E)

```cpp
struct Z : Y, virtual W { using Y::Y };
Z(0); // Y 的初始化没有调用 X 的构造函数
template<class T> struct Log : T {
    using T::T;
    ~Log() { std::cout << "Destroying wrapper" << std::endl; }
};
```

类 `Log` 复制并转发了它所有的构造函数，而类 `Log` 对象被销毁。 — 示例结束

2 如果构造函数继承自多个类型 `B` 的基类对象，则程序格式非法。

示例 2:

```cpp
struct A { int; };
struct B : A { using A::A; };
struct C1 : B { using B::B; };
struct C2 : B { using B::B; };
struct D1 : C1, C2 {
    using C1::C1;
    using C2::C2;
};
D1 d1(0); // 错误：歧义
```

注，此处根据原文逻辑，文应为：

```cpp
extern struct D;
struct D {
D(int a) : a(a), b(d) {}
int a, b;
D d = D(1);
// d.b 的值是未指定的
```

（注：原文提供的文本片段存在部分乱乱和重复，翻译已遵循示例 2 - 示例 4 的逻辑）

33 式或或式地转换为指向 `X` 对象（（ 的间间接基基类）的指针（glvaluevaluevalue所有子子完成完成完成对象完成完成完成

完成，否则转换将具有未定义行为。

示例 3:

```cpp
struct A { int; };
struct B : virtual A { };
struct C : virtual A { };
struct D : B, C {
    D() {
    }
};
```

4 成员函数（包括虚函数，11.7.3）可以在构造期间被调用。同样，可以使用 `*typeid*` 运算符（7.6.1.8）或 `*dynamic_cast*`（7.7.2）构造对象。然而，如果这些操作在 ctor-initializer（构造函数初始化列表）（或从 ctor-initializer 直接或间接调用的函数）中，在所有基类的 mem-initializers 完成之前执行，程序将具有未定义行为。

示例 4:

```cpp
class A {
public:
int a;
};
class B : public A {
public:
int j;
int f();
B() : A(f()) { // 未定义行为：调用了成员函数但基类 A 未初始化
f(f()) {} // 定义良好：所有基类均已初始化
};
class C : B {
public:
int c;
C(int);
};
class D : public B, C {
    int i;
public:
    D() : C(f()), // 未定义行为：在基类 C 尚未初始化之前调用了成员函数
        i(f()) {} // 定义良好：所有基类均已初始化
};
```

Note 8：11.10.5 描述了在定义良好的情况下，构造期间虚函数调用、typeid 和 dynamic_casts 的结果；即，描述了正在构造的对象的多态行为。 — 注释结束

## 11.0.5 构造与析构

1 对于具有非平凡构造函数的对象，在构造函数开始之前引用任何非静态成员或基类将导致未定义行为。对于具有非平凡析构函数的对象，在析构函数执行后引用任何非静态成员或基类将导致未定义行为。

示例 1:

```cpp
struct X { int; };
struct Y : X { Y(int); }; // 非平凡
struct A { int; };
struct B : public A { int y; Y(int); }; // 非平凡
extern B bobj;
B* p = &bobj; // OK：引用基类
int* p1 = &bobj.a; // 未定义行为：引用基成员
int* p2 = &bobj.y; // 未定义行为：引用成员
```

ISO/IEC 14882:2020(E)

```cpp
A* pa = &bobj;
B bobj = xobj;
// 未定义行为：向上转换到基类
// bobj 的定义
extern X xobj;
int* p3 = &xobj.i;
X xobj;
// OK，X 是平凡类
对于另一个示例，
struct W { int j; };
struct X : public W { };
struct Y {
int* p;
Y() : p(&j) { // 未定义，x 尚未构造
};2 在对象的构造期间，如果通过从构造函数直接或间接获取的值访问对象或其任何成员，则该对象或成员是未指定的。
```

示例 2:
```cpp
struct C;
void no_opt(C*);
struct C {
int c;
C() : c(0) { no_opt(this); };
};
const C bobj;
void no_opt(C* cptr) {
int i = bobj.c * 100; // bobj.c 的值是未指定的
cptr = i;
out << bobj.c << 100; // bobj.c 的值是未指定的
cout << 'un';
}
```

```cpp
extern struct D;
struct D {
D(int a) : a(a), b(d) {}
int a, b;
D d = D(1);
// d.b 的值是未指定的
```

3 显式或隐式地指向 `X` 对象（直接或间接基类的引用）的指针（glvalue），当所有子对象完成后，对象的构造完成，否则转换将具有未定义行为。

示例 3:
```cpp
struct A { int; };
struct B : virtual A { };
struct C : virtual A { };
struct D : B, C {
    D() {
    }
};
```

# ISO/IEC 14882:2020(E)

如果不是指向构造函数或析构函数的某个基类的对象的指针，则 `dynamic_cast` 将导致未定义行为。

示例 5:

```cpp
struct V {
    virtual void f();
};
struct A : virtual V {};
struct B : virtual V {
    B(A*);
};
struct D : A, B {
    D() : B(A*), this() {}
};
```

```cpp
B(V*, A* a) {
    typeid(*this);
    typeid(v);
    dynamic_cast<B>(v);
    dynamic_cast<B>(a);
} // B 的 type_info
// 定义良好：*v 类型为 V，作为 B 的基类会产生 B 的 type_info
// 未定义：类型 A 不是 B 的基类
// 定义良好：v 类型为 V，在 B* 中 V 是基类
// 未定义：a 类型为 A，不是 B 的基类
```
// 示例结束

## 11.10.6 拷贝/移动省略 [class.copy.elision]

+ 1 当实现允许省略类对象的拷贝/移动构造时，即使为拷贝/移动操作调用了构造函数，或者对象的析构函数有副作用也是如此。在某些情况下，实现将拷贝/移动操作的源和目标视为引用同一对象的两种不同方式。如果所选构造函数的第一个参数是对象类型的引用，则该对象在目标本应被销毁时出现；否则，析构发生在如果没有省略时对象应被销毁的时间的较晚者。¹¹ 这种拷贝/移动操作的省略被称为拷贝省略（copy elision），在以下情况下允许（这些情况可以组合以消除多个）：

+ (1.1) 在带有返回类型的返回语句中，当表达式是一个具有自动存储区的非 volatile 对象的名称（除函数参数或由处理程序的异常声明引入的变量外 [14.4]），且该对象的类型与返回类型相同（忽略 cv 质限定符）时，可以通过直接在函数的返回对象中构造该对象来省略移动操作。
+ (1.2) 在 throw 表达式 (7.6.18) 中，当操作数是一个具有自动存储区的非 volatile 对象的名称（除函数或 catch 子句参数），其作用域未超出所在 try 块的结束（如果存在），可以通过直接在异常对象中构造该对象来省略拷贝/移动操作。
+ (1.3) 在协程 (9.5.4) 中，可以省略协程的拷贝，并将该拷贝的引用替换为对参数的引用，只要该参数在协程体执行之前或参数对象保持不变。

当异常处理程序的异常声明 [14.1] 创建与异常对象 [14.2] 类型相同（除 cv 质限定符）的对象时，如果对于异常声明创建的对象执行构造函数和析构函数，程序的含义保持不变，可以将异常声明视为省略来省略拷贝对象。

> [注 1：无法从异常对象进行移动，因为它始终是一个左值。注 结束]

当表达式在需要常量表达式的上下文中 (7.7) 以及常量初始化 (6.9.3.2) 中求值时，不允许拷贝省略。

118) 因为销毁了一个对象而不是两个，且没有执行一个拷贝/移动构造函数，因此每个构造的对象仍然有一个对象被销毁。

[注 2：如果在另一个上下文中求值相同的表达式，可能会执行拷贝省略。— 注 结束

[示例 1:

```cpp
class Thing {
public:
    Thing();
    ~Thing();
    Thing(const Thing&);
};
Thing f() {
    Thing t;
    return t;
}
Thing t2 = f();
struct A {
    void *p;
    constexpr A(int t) : p(this)
};
constexpr A g() {
    A loc;
    return loc;
}
```

```cpp
constexpr A a; // 良好，a.p 指 a
constexpr A b = g(); // 错误：b.p 将悬空 (8.5)
```

```cpp
void h() { // 良好，c.p 可能指向 c 或指向一个临时临时对象
    A c = g();
}
```
