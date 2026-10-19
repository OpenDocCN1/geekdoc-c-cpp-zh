

```
struct A {
    int a;
    static int  s;
    enum { e };
};
struct B : A, virtual V { };
struct C : A, virtual V { };
struct D : B, C { };

void f(D* pd) {
    pd->v++;
    pd->s++;
    int i = pd->e;
    pd->a++;
}
— end example]
```

10 [Note 3: 当使用虚基类时，隐藏声明可以通过不经过隐藏声明的子对象格中的路径到达。这不是二义性。使用非虚基类的相同用法是二义性的；在这种情况下，没有唯一的实例代表该名称隐藏所有其他名称。 — end note]

[Example 4:

```
struct V { int f();  int x; };
struct W { int g();  int y; };
struct B : virtual V, W {
    int f();  int x;
    int g();  int y;
};
struct C : virtual V, W { };

struct D : B, C { void glorp(); };
```

![Figure 6: Name lookup [fig:class.lookup]](img/f00894146489220e5849acc131e0a0e1_308_0.png)

如 Figure 6 所示，V 中声明的名称和左侧的 W 实例被 B 中的名称隐藏，但右侧的 W 实例中声明的名称根本没有被隐藏。

```
void D::glorp() {
    x++;
    f();
    y++;
    g();
}
— end example]
```

11 从派生类对象指针或指定派生类对象的表达式到其基类指针或引用的显式或隐式转换必须无二义性地引用表示基类的唯一对象。

[Example 5:

```
struct V { };
struct A { };
struct B : A, virtual V { };
struct C : A, virtual V { };
struct D : B, C { };

void g() {
    D d;
    B* pb = &d;
    A* pa = &d;        // error: ambiguous: C's A or B's A?
    V* pv = &d;        // OK: only one V subobject
}
— end example]
```

12 [Note 4: 即使名称查找的结果是无二义性的，使用在多个子对象中发现的名称仍然可能是二义性的（7.3.13, 7.6.1.5, 11.9.3）。 — end note]

[Example 6:

```
struct B1 {
    void f();
    static void f(int);
    int i;
};
struct B2 {
    void f(double);
};
struct I1: B1 { };
struct I2: B1 { };

struct D: I1, I2, B2 {
    using B1::f;
    using B2::f;
    void g() {
        f();                // Ambiguous conversion of this
        f(0);               // Unambiguous (static)
        f(0.0);             // Unambiguous (only one B2)
        int B1::* mpB1 = &D::i;   // Unambiguous
        int D::* mpD = &D::i;     // Ambiguous conversion
    }
};
— end example]
```

## 11.9 成员访问控制 [class.access]

### 11.9.1 通用 [class.access.general]

1 类的成员可以是

-   (1.1) — 私有；即其名称只能由声明它的类中的成员和友元使用。
-   (1.2) — 受保护；即其名称只能由声明它的类中的成员和友元、从该类派生的类以及它们的友元使用（见 11.9.5）。
-   (1.3) — 公共；即其名称可以在任何地方使用而无访问限制。

2 类的成员还可以访问该类有权访问的所有名称。成员函数的局部类可以访问成员函数本身可以访问的相同名称。115

3 使用关键字 class 定义的类的成员默认为私有。使用关键字 struct 或 union 定义的类的成员默认为公共。

[Example 1:

```
class X {
    int a;            // X::a is private by default
};

struct S {
    int a;
};
// S::a is public by default
— end example]
```

4 访问控制均匀地应用于所有名称，无论名称是从声明还是表达式中引用的。

[Note 1: 访问控制适用于 friend 声明（11.9.4）和 using-declaration（9.9）所命名的名称。 — end note]

对于重载函数名，访问控制应用于重载决议所选择的功能。

[Note 2: 因为访问控制应用于名称，如果访问控制应用于 typedef 名称，则仅考虑 typedef 名称本身的可访问性。typedef 所引用的实体的可访问性不予考虑。例如，

```
class A {
    class B { };
    public:
        typedef B BB;
};

void f() {
    A::BB x;        // OK, typedef name A::BB is public
    A::B y;         // access error, A::B is private
}
```

— end note]

5 [Note 3: 成员和基类的访问是受控的，而不是它们的可见性（6.4.10）。成员的名称仍然可见，并且隐式转换到基类仍然被考虑，即使这些成员和基类是不可访问的。 — end note]

给定构造的解释是在不考虑访问控制的情况下建立的。如果所建立的解释使用了不可访问的成员名称或基类，则该构造是不良形成的。

6 11.9 中的所有访问控制都影响从特定实体的声明访问类成员名称的能力，包括在被声明的实体名称之前声明的一部分，以及如果该实体是类，则在类的 member-specification 之外出现的类成员的定义。

[Note 4: 这也适用于对构造函数、转换函数和析构函数的隐式引用。 — end note]

7 [Example 2:

```
class A {
    typedef int I;      // private member
    I f();
    friend I g(I);
    static I x;
    template<int> struct Q;
    template<int> friend struct R;
protected:
    struct B { };
};
```

```
A::I A::f() { return 0; }
A::I g(A::I p = A::x);
A::I g(A::I p) { return 0; }
A::I A::x = 0;
template<A::I> struct A::Q { };
template<A::I> struct R { };

struct D: A::B, A { };
```

这里，所有对 A::I 的使用都是 well-formed 的，因为 A::f、A::x 和 A::Q 是类 A 的成员，而 g 和 R 是类 A 的友元。这意味着，例如，对 A::I 的第一次使用作为返回类型的访问检查必须推迟到确定此 A::I 的使用是作为类 A 的成员的返回类型时。同样，使用 A::B 作为 *base-specifier* 是 well-formed 的，因为 D 从 A 派生，因此对 *base-specifier-list* 的检查必须推迟到整个 *base-specifier-list* 被看到之后。 — end example]

8 默认参数（9.3.4.7）中的名称在声明点绑定，并在该点检查访问，而不是在默认参数的任何使用点。函数模板和类模板成员函数的默认参数的访问检查按 13.9.2 中所述执行。

9 默认 *template-argument*（13.2）中的名称在其出现上下文中检查访问，而不是在默认 *template-argument* 的任何使用点检查访问。

[Example 3:

```
class B { };
template <class T> class C {
protected:
    typedef T TT;
};

template <class U, class V = typename U::TT>
class D : public U { };

D <C<B> *> d;        // access error, C::TT is protected
```

— end example]

### 11.9.2 访问说明符 [class.access.spec]

1 成员声明可以由 *access-specifier*（11.7）标记：

```
*access-specifier* : *member-specification*opt
```

*access-specifier* 指定在其后直到类结束或遇到另一个 *access-specifier* 为止的成员的访问规则。

[Example 1:

```
class X {
    int a;            // X::a is private by default: class used
public:
    int b;            // X::b is public
    int c;            // X::c is public
};
```

— end example]

2 允许任意数量的访问说明符，且不需要特定顺序。

[Example 2:

```
struct S {
    int a;            // S::a is public by default: struct used
protected:
    int b;            // S::b is protected
private:
    int c;            // S::c is private
public:
    int d;            // S::d is public
};
```

— end example]

3 [Note 1: 访问控制对数据成员分配顺序的影响在 7.6.9 中指定。 — end note]

4 当成员在其类定义中被重新声明时，其在重新声明时指定的访问必须与其在初始声明时指定的访问相同。

[Example 3:

```
struct S {
    class A;
    enum E : int;
private:
    class A { };        // error: cannot change access
```

