
```cpp
struct W
{
    int g();
    int y;
};

struct B : virtual V, W
{
    int f(); int x;
    int g(); int y;
};

struct C : virtual V, W { };
struct D : B, C { void glorp(); };

void D::glorp()
{
    x++;
    f();
    y++;
    g();
}
```

## 问题 180 的解答

编译器错误是：

```text
virtual_base.cpp:27:5:
error: member 'y' found in multiple base classes of
    different types
    y++;
    ^

virtual_base.cpp:16:18:
note: member found by ambiguous name lookup
    int g(); int y;
                 ^

virtual_base.cpp:10:9:
note: member found by ambiguous name lookup
    int y;
        ^

virtual_base.cpp:28:5:
error: member 'g' found in multiple base classes of
    different types
    g();
    ^

virtual_base.cpp:16:9:
note: member found by ambiguous name lookup
    int g(); int y;
    ^

virtual_base.cpp:9:9:
note: member found by ambiguous name lookup
      int g();

2 errors generated.
```

在函数 *void D::glorp()* 中：

- `x++` 没问题，因为 `B::x` 隐藏了 `V::x`
- `f()` 没问题，因为 `B::f()` 隐藏了 `V::f()`
- `y++` 有歧义：是 `B::y` 还是 `C` 的 `W::y`？
- `g()` 有歧义：是 `B::g()` 还是 `C` 的 `W::g()`？

使用虚基类时，可以沿一条穿过子对象格的路径到达某个被隐藏的声明，而该路径不经过进行隐藏的声明。这不是歧义。对非虚基类进行相同使用时则是歧义：在这种情况下，不存在隐藏所有其他名称的唯一名称实例。

![](img/78e1bff64796dccbf49e7c84b8201fb2_489_0.png)

在 V 中声明的名称以及 W 的左侧实例中的名称被 B 中的名称隐藏，但 W 的右侧实例中声明的名称根本没有被隐藏。

## 问题 181 — 虚函数

下面程序的输出是什么？

程序 13.5：虚函数

```cpp
1 #include <iostream>
2
3 struct A
4 {
5     virtual void f()
    {
        std::cout << "A::f()" << std::endl;
    }
};
struct B : virtual A
{
    virtual void f()
    {
        std::cout << "B::f()" << std::endl;
    }
};
struct C : B, virtual A
{
    using A::f;
};
int main()
{
    C c;
    c.f();
    c.C::f();
}
```

### 问题 181 的解答

它打印

```text
B::f()
A::f()
```

- `c.f()` 调用 `B::f`，因为最终覆盖者
- `c.C::f()` 调用 `A::f`，因为 using 声明

虚函数支持动态绑定和面向对象编程。声明或继承虚函数的类称为*多态类*。

如果虚成员函数 `vf` 在类 *Base* 中声明，并且在直接或间接派生自 *Base* 的类 *Derived* 中声明了一个成员函数 `vf`，该函数与 `Base::vf` 具有相同的名称、参数类型列表、cv 限定和引用限定符（或缺少相同项），那么 `Derived::vf` 也是虚函数（无论是否如此声明），并且它覆盖 `Base::vf`。

为方便起见，我们说任何虚函数都覆盖自身。

类对象 `S` 的虚成员函数 `C::vf` 是最终覆盖者，除非 `S` 是其基类子对象的最派生类（如果有）声明或继承了另一个覆盖 `vf` 的成员函数。

在派生类中，如果基类子对象的虚成员函数有多个最终覆盖者，则程序非良构。

## 问题 182 — 虚函数与隐藏

审阅下面的程序。

```cpp
struct B
{
    virtual void f();
};
struct D : B
{
    void f(int);
};
struct D2 : D
{
    void f();
};
```

### 问题 182 的解答

需要注意的是，虚成员函数不必可见也能被覆盖。

这里，类 D 中的函数 f(int) 隐藏了其基类 B 中的虚函数 f()；D::f(int) 不是虚函数。

然而，在类 D2 中声明的 f() 与 B::f() 具有相同的名称和相同的参数，因此它是覆盖函数 B::f() 的虚函数，即使 B::f() 在类 D2 中不可见。

## 问题 183 — 虚函数与 final

审阅下面的程序。

程序 13.6：虚函数与 final

```cpp
struct B
{
    virtual void f() const final;
};
struct D : B
{
    void f() const;
};
```

### 问题 183 的解答

编译器错误是：

```text
final_virtual.cpp:8:10:
error: declaration of 'f' overrides a
        'final' function
        void f() const;

final_virtual.cpp:3:18:
note: overridden virtual function is here
        virtual void f() const final;

1 error generated.
```

如果某个类 *B* 中的虚函数 *f* 用 *虚说明符 final* 标记，并且在派生自 *B* 的类 *D* 中，函数 *D::f* 覆盖 *B::f*，则程序非良构。

## 问题 184 — 虚函数与 override

审阅下面的程序。

程序 13.7：虚函数与 override

```cpp
1 struct B
2 {
3     virtual void f(int);
4 };
5
6 struct D : B
7 {
8     virtual void f(long) override;
9     virtual void f(int) override;
10 };
```

### 问题 184 的解答

编译器错误是：

```text
override_virtual.cpp:8:18:
error: 'f' marked 'override' but does not override
        any member functions
        virtual void f(long) override;

1 error generated.
```

如果虚函数用 *虚说明符 override* 标记，但没有覆盖基类的成员函数，则程序非良构。

## 问题 185 — 访问默认模板实参

审阅下面的程序。

```cpp
};
```

## 问题 186 的解答

是。

当友元声明引用重载名称或运算符时，只有由参数类型指定的函数成为友元。类 *X* 的成员函数可以是类 *Y* 的友元。因此，构造函数和析构函数也可以成为友元。

## 问题 187 — 访问虚函数

下面的程序有效吗？如果有效，输出是什么？

程序 13.9：访问虚函数

```cpp
#include <iostream>

struct B
{
    virtual void f()
    {
        std::cout << "B::f()" << std::endl;
    }
};

struct D : B
{
private:
    void f()
    {
        std::cout << "D::f()" << std::endl;
    }
};

int main()
{
    D d;
    B* pb = &d;
    pb->f();
}
```

### 问题 187 的解答

是。

它打印

```text
D::f()
```

虚函数的访问规则由其声明决定，不受后来覆盖它的函数的规则影响。

## 问题 188 — const/volatile 构造函数

构造函数可以声明为 `const`、`volatile` 或 `const volatile` 吗？

### 问题 188 的解答

否。

构造函数不能声明为 `const`、`volatile` 或 `const volatile`。`const` 和 `volatile` 语义不应用于正在构造的对象。它们在针对最派生对象的构造函数结束时生效。

## 问题 189 — new 与悬垂引用

审阅下面的程序。

程序 13.10：new 与悬垂引用

```cpp
#include <utility>
struct A
{
    int i;
    const std::pair<int,int>& p;
};
int main()
{
    A * p = new A{ 1, {2, 3} };
}
```

### 问题 189 的解答

这会导致编译错误：

```text
dangling_ref_new.cpp:11:24: error:
reference to type 'const std::pair<int, int>'
    could not bind to an rvalue of type 'int'
    A * p = new A{ 1, {2, 3} };
                         ^

1 error generated.
```

在 new 初始化器中绑定到引用的临时对象会持续到包含该 new 初始化器的完整表达式结束。这里，第 11 行创建了一个悬垂引用。

## 问题 190 — 用户定义转换

下面的用户定义转换允许吗？

程序 13.11：用户定义转换

```cpp
struct X
{
    operator int ();
};
struct Y
{
    operator X();
};
int main()
{
    Y a;
    int b = a;
    int c = X(a);
}
```

### 问题 190 的解答

这会导致编译错误：

```text
conversion.cpp:14:9:
error: no viable conversion from 'Y' to 'int'
    int b = a;
        ~   ^
conversion.cpp:8:5: note: candidate function
    operator X();
    ^

1 error generated.
```

*至多一个用户定义转换（构造函数或转换函数）会隐式应用于单个值。*

- `int b = a;` 是错误的：这里不会尝试 `a.operator X().operator int()`。
- `int c = X(a);` 没问题：会应用 `a.operator X().operator int()`。

## 问题 191 — 通过构造函数进行转换

审阅下面的程序。

程序 13.12：通过构造函数进行转换

```cpp
struct A
{
    A(int);
    A(const char*, int = 0);
    A(int, int);
};
```

