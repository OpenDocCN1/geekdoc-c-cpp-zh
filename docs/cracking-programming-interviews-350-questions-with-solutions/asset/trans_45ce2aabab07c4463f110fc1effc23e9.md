
由 using 声明（using-declaration）声明的实体，在 using 声明的位置，应当根据其定义，在使用它的上下文中是已知的。当使用该名称时，不会考虑在 using 声明之后添加到命名空间中的定义。

## 问题 134：using 声明与相同函数

请审阅下面的代码。

**程序 11.15：using 声明与相同函数**

```cpp
    1 namespace B
    2 {
    3     void f(int);
    4     void f(double);
    5 }
    6
    7 namespace C
    8 {
    9     void f(int);
    10    void f(double);
    11    void f(char);
    12 }
    13
    14 void h()
    15 {
    16    using B::f;
    17    using C::f;
    18    f('h');
    19    f(1);
    20    void f(int);
    21 }
```

### 问题 134 的解答

编译器错误信息为：

```text
using8.cpp:19:5: error: call to 'f' is ambiguous
    f(1);
    ^
using8.cpp:3:10: note: candidate function
    void f(int);
         ^
using8.cpp:9:10: note: candidate function
    void f(int);
         ^
using8.cpp:4:10: note: candidate function
    void f(double);
         ^
using8.cpp:10:10: note: candidate function
    void f(double);

using8.cpp:11:10: note: candidate function
    void f(char);
    ^

using8.cpp:20:10:
error: declaration conflicts with target
of using declaration
    already in scope
    void f(int);

using8.cpp:9:10: note: target of using declaration
    void f(int);
    ^

using8.cpp:17:14: note: using declaration
    using C::f;
        ^

2 errors generated.
```

- 如果命名空间作用域或块作用域中的函数声明与 using 声明引入的函数具有相同的名称和相同的参数类型列表，并且这些声明并非声明同一个函数，则程序为格式错误（ill-formed）。
- 如果命名空间作用域中的函数模板声明与 using 声明引入的函数模板具有相同的名称、参数类型列表、返回类型和模板参数列表，则程序为格式错误。
- 两个 using 声明可以引入具有相同名称和相同参数类型列表的函数。如果对于非限定函数名的调用，函数重载解析选择了由这些 using 声明引入的函数，则该函数调用是格式错误的。

因此，在函数 `void h()` 中：

- `using B::f;` 表示 `B::f(int)` 和 `B::f(double)` 两者。
- `using C::f;` 表示 `C::f(int)`、`C::f(double)` 和 `C::f(char)`。
- `f('h')` 调用 `C::f(char)`。
- `f(1)` 是一个有歧义的调用：是 `B::f(int)` 还是 `C::f(int)`？
- `void f(int)` 与 `C::f(int)` 和 `B::f(int)` 冲突。

## 问题 135：隐藏/覆盖与 using 声明

请审阅下面的代码。

**程序 11.16：隐藏/覆盖与 using 声明**

```cpp
 1  struct B
 2  {
 3      virtual void f(int);
 4      virtual void f(char);
 5      void g(int);
 6      void h(int);
 7  };
 8
 9  struct D : B
 10 {
 11     using B::f;
 12     void f(int);
 13     using B::g;
 14     void g(char);
 15     using B::h;
 16     void h(int);
 17 };
 18
 19 void k(D* p)
 20 {
 21     p->f(1);
 22     p->f('a');
 23     p->g(1);
 24     p->g('a');
 25 }
```

### 问题 135 的解答

当 *using 声明* 将名称从基类带入 *派生类* 作用域时，*派生类* 中的成员函数和成员函数模板会 *覆盖* 和/或 *隐藏* 基类中具有相同名称、参数类型列表、cv 限定符和引用限定符（如果有）的成员函数和成员函数模板（而不是发生冲突）。

在代码中，结构体 D 内：

- `void f(int)` 没问题，因为 `D::f(int)` 覆盖了 `B::f(int)`。
- `void g(char)` 没问题，它只是另一个重载函数。
- `void h(int)` 也没问题，因为 `D::h(int)` 隐藏了 `B::h(int)`。

在函数 `void k(D* p)` 中：

- `p->f(1)` 调用 `D::f(int)`
- `p->f('a')` 调用 `B::f(char)`
- `p->g(1)` 调用 `B::g(int)`
- `p->g('a')` 调用 `D::g(char)`

## 问题 136：using 声明与有歧义的基类

在这个程序中，`d->x()` 将调用哪个函数？

**程序 11.17：using 声明与有歧义的基类**

```cpp
1 struct A
2 {
3     int x();
4 };
5
6 struct B : A { };
7
8 struct C : A
9 {
10     using A::x;
11     int x(int);
12 };
13
14 struct D : B, C
15 {
16     using C::x;
17     int x(double);
18 };
19
20 int f(D* d)
21 {
22     return d->x();
23 }
```

### 问题 136 的解答

这个程序无法编译。编译器错误信息为：

```text
using10.cpp:22:12: error: ambiguous conversion from
derived class 'D' to base class 'A':
    struct D -> struct B -> struct A
    struct D -> struct C -> struct A
    return d->x();
                ^
1 error generated.
```

另一个编译器给出了以下错误：

```text
using10.cpp: In function ‘int f(D*)’:
using10.cpp:22:17:
error: ‘A’ is an ambiguous base of ‘D’
    return d->x();
```

如果派生类使用 using 声明来访问基类的成员，则该成员名称是可访问的。如果该名称是重载成员函数的名称，则所有具有该名称的函数都是可访问的。using 声明所提及的基类成员，在指定该 using 声明的类的至少一个直接基类的作用域内是可见的。由于 using 声明指定的是基类成员（而不是成员子对象或基类子对象的成员函数），因此不能使用 using 声明来解决继承成员的二义性。这就是为什么 `d->x()` 是一个有歧义的调用：是 `B::x` 还是 `C::x`？

## 问题 137：using 声明与访问

请审阅下面的程序。

**程序 11.18：using 声明与可访问性规则**

```cpp
class A
{
private:
    void f(char);

public:
    void f(int);

protected:
    void g();
};

class B : public A
{
    using A::f;

public:
    using A::g;
};
```

### 问题 137 的解答

这个程序无法编译。编译器错误信息为：

```text
using11.cpp:15:14:
error: ‘f’ is a private member of ‘A’
    using A::f;

using11.cpp:4:10: note: declared private here
void f(char);
      ^
```

using 声明创建的别名具有成员声明通常的可访问性。

## 问题 138：using 指令

请审阅下面的程序。

**程序 11.19：using 指令**

```cpp
namespace A
{
    int i;
    namespace B
    {
        namespace C
        {
            int i;
        } // namespace C

        using namespace A::B::C;

        void f1()
        {
            i = 5;
        }
    } // namespace B
    namespace D
    {
        using namespace B;
        using namespace C;

        void f2()
        {
            i = 5;
        }
    } // namespace D
    void f3()
    {
        i = 5;
    }
} // namespace A
void f4()
{
    i = 5;
}
```

### 问题 138 的解答

这个程序无法编译。编译器错误信息为：

```text
using12.cpp:27:13:
error: reference to 'i' is ambiguous
        i = 5;
        ^

using12.cpp:3:9:
note: candidate found by name lookup is
'A::i'
        int i;

using12.cpp:9:17:
note: candidate found by name lookup is
'A::B::C::i'
            int i;
            ^

using12.cpp:39:5:
error: use of undeclared identifier 'i';
did you mean 'A::i'?
    i = 5;
    ^
    A::i
using12.cpp:3:9: note: 'A::i' declared here
        int i;

2 errors generated.
```

using 指令（using-directive）不会向它出现的声明区域添加任何成员。因此，

- 在 `f1` 中，`i = 5` 没问题，`C::i` 在 `B` 中可见，并隐藏了 `A::i`
- 在 `f2` 中，`i = 5` 是有歧义的，是 `B::C::i` 还是 `A::i`？
- 在 `f3` 中，`i = 5` 使用 `A::i`
- 在 `f4` 中，`i = 5` 是格式错误的；两个 `i` 都不可见

## 第 12 章：杂项

### 问题 139：嵌套链接规范

请审阅下面的程序。

**程序 12.1：嵌套链接规范**

```c
extern "C" void f1(void (*pf)(int));
extern "C" typedef void FUNC();
FUNC f2;
extern "C" FUNC f3;
void (*pf2)(FUNC*);
extern "C"
{
    static void f4();
}
extern "C" void f5()
{
    extern void f4();
}
extern void f4();
void f6()
{
    extern void f4();
}
```

### 问题 139 的解答

- `f1`：名称 `f1` 及其函数类型具有 C 语言链接；`pf` 是指向 C 函数的指针
