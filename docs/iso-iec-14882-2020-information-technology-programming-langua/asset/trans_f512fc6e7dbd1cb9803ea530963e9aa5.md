

[示例 4：

```
class C {
    int g();
};

class D2 : public B {
    using B::f;        // OK: B is a base of D2
    using B::e;        // OK: e is an enumerator of base B
    using B::x;        // OK: x is a union member of base B
    using C::g;        // error: C isn't a base of D2
};
```

— 示例结束]

4 [注意 2：由于析构函数没有名称，using 声明不能引用基类的析构函数。由于转换函数的成员模板特化不能通过名称查找找到，因此当 using 声明指定转换函数时（13.7.3），不会考虑它们。— 注意结束]

如果从基类引入到派生类的构造函数或赋值运算符具有该派生类的复制/移动构造函数或赋值运算符的签名（11.4.5.3、11.4.6），则 using 声明本身并不抑制派生类成员的隐式声明；基类的成员会被派生类的隐式声明的复制/移动构造函数或赋值运算符隐藏或覆盖，如下所述。

5 using 声明不得指名模板 id。

[示例 5：

```
struct A {
    template <class T> void f(T);
    template <class T> struct X { };
};
struct B : A {
    using A::f<double>;    // error
    using A::X<int>;       // error
};
```

— 示例结束]

6 using 声明不得指名命名空间。

7 指名除枚举器以外的类成员的 using 声明应是成员声明。

[示例 6：

```
struct X {
    int i;
    static int s;
};

void f() {
    using X::i;    // error: X::i is a class member and this is not a member declaration.
    using X::s;    // error: X::s is a class member and this is not a member declaration.
}
```

— 示例结束]

8 由 using 声明声明的成员可以像其他成员名称一样通过显式限定来引用（6.5.4.3）。

[示例 7：

```
void f();

namespace A {
    void g();
}

namespace X {
    using ::f;    // global f
    using A::g;   // A's g
}
```

```
void h()
{
    X::f();            // calls ::f
    X::g();            // calls A::g
}
```

— 示例结束]

9 using 声明是一个声明，因此可以在允许（且仅允许）多重声明的地方重复使用。

```
[Example 8:
namespace A {
    int i;
}

namespace A1 {
    using A::i, A::i;    // OK: double declaration
}

struct B {
    int i;
};

struct X : B {
    using B::i, B::i;    // error: double member declaration
};
— end example]
```

10 [注意 3：对于其嵌套名称说明符指名命名空间的 using 声明，在该 using 声明之后添加到命名空间的成员不在所引入的声明集中，因此在使用该名称时不会考虑它们。因此，在 using 声明之后添加的额外重载会被忽略，但默认函数实参（9.3.4.7）、默认模板实参（13.2）和模板特化（13.7.6、13.9.4）会被考虑。— 注意结束]

```
[Example 9:
namespace A {
    void f(int);
}

using A::f;            // f is a synonym for A::f; that is, for A::f(int).
namespace A {
    void f(char);
}

void foo() {
    f('a');            // calls f(int), even though f(char) exists.
}

void bar() {
    using A::f;        // f is a synonym for A::f; that is, for A::f(int) and A::f(char).
    f('a');            // calls f(char)
}
— end example]
```

11 [注意 4：类模板的部分特化是通过查找主类模板，然后考虑该模板的所有部分特化来找到的。如果 using 声明指名一个类模板，则在 using 声明之后引入的部分特化实际上是可见的，因为主模板是可见的（13.7.6）。— 注意结束]

12 由于 using 声明是一个声明，因此同一声明区域（6.4）中对同名声明的限制也适用于 using 声明。

```
[Example 10:
namespace A {
    int x;
```

```
[Example 12:
struct B {
    virtual void f(int);
    virtual void f(char);
    void g(int);
    void h(int);
};

struct D : B {
    using B::f;
    void f(int);        // OK: D::f(int) overrides B::f(int);

    using B::g;
    void g(char);       // OK

    using B::h;
    void h(int);        // OK: D::h(int) hides B::h(int)
};

void k(D* p)
{
    p->f(1);            // calls D::f(int)
    p->f('a');          // calls B::f(char)
    p->g(1);            // calls B::g(int)
    p->g('a');          // calls D::g(char)
}

struct B1 {
    B1(int);
};

struct B2 {
    B2(int);
};

struct D1 : B1, B2 {
    using B1::B1;
    using B2::B2;
};
D1 d1();                // error: ambiguous

struct D2 : B1, B2 {
    using B1::B1;
    using B2::B2;
    D2(int);            // OK: D2::D2(int) hides B1::B1(int) and B2::B2(int)
};
D2 d2();                // calls D2::D2(int)
— end example]
```

15 [注意 6：为了在重载决议期间形成候选集，通过 using 声明引入派生类的函数被视为派生类的成员（11.8）。特别是，隐式对象参数被视为对派生类的引用，而不是对基类的引用（12.4.2）。这对函数的类型没有影响，并且在所有其他方面，该函数仍然是基类的成员。— 注意结束]

16 当查找派生类的构造函数（6.5.4.2）或形成重载候选集（12.4.2.4、12.4.2.5、12.4.2.8）时，通过 using 声明引入的构造函数被视为派生类的构造函数。

[注意 7：如果选择这样的构造函数来执行类类型对象的初始化，则除了构造函数来源的基类之外的所有子对象都被隐式初始化（11.10.4）。如果派生类的构造函数和基类的构造函数本来会有歧义，则有时派生类的构造函数更受青睐（12.4.4）。— 注意结束]

## ISO/IEC 14882:2020(E)

17 在不指名构造函数的 using 声明符中，所引入声明集中的所有成员都应是可访问的。在指名构造函数的 using 声明符中，不执行访问检查。特别是，如果派生类使用 using 声明符来访问基类的成员，则该成员名称应是可访问的。如果该名称是重载成员函数的名称，则所有被指名的函数都应是可访问的。using 声明符所提及的基类成员，应在指定该 using 声明符的类的至少一个直接基类的作用域内可见。

18 [注意 8：由于 using 声明符指定的是一个基类成员（而不是成员子对象或基类子对象的成员函数），因此 using 声明符不能用于解决继承成员歧义。

[示例 13：

```
struct A { int x(); };
struct B : A {};
struct C : A {
    using A::x;
    int x(int);
};

struct D : B, C {
    using C::x;
    int x(double);
};
int f(D* d) {
    return d->x();    // error: overload resolution selects A::x, but A is an ambiguous base class
}
```

— 示例结束]

— 注意结束]

19 由 using 声明创建的同义词对于成员声明具有通常的可访问性。指名构造函数的 using 声明符不会创建同义词；相反，如果这些额外的构造函数在用于构造相应基类的对象时可访问，则它们是可访问的，而 using 声明的可访问性被忽略。

[示例 14：

```
class A {
    private:
        void f(char);
    public:
        void f(int);
    protected:
        void g();
};

class B : public A {
    using A::f;        // error: A::f(char) is inaccessible
    public:
    using A::g;        // B::g is a public synonym for A::g
};
```

— 示例结束]

20 如果 using 声明符使用关键字 typename 并指定一个依赖名称（13.8.3），则 using 声明引入的名称被视为 typedef 名称（9.2.4）。

## 9.10 asm 声明 [dcl.asm]

1 asm 声明具有如下形式：

```
asm-declaration:
    attribute-specifier-seq_opt asm ( string-literal ) ;
```

asm 声明是有条件支持的；其含义由实现定义。asm 声明中的可选属性说明符序列从属于该 asm 声明。

> [注意 1：通常它用于通过实现向汇编器传递信息。— 注意结束]

