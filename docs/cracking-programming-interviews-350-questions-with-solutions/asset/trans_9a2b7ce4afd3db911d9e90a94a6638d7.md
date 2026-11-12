

## 问题57

以下 lambda 表达式的返回类型是如何确定的？

程序8.48：lambda 的返回类型

```cpp
auto x1 = [] ( int i ){ return i; };
auto x2 = []{ return { 1, 2 }; };
```

### 问题57的解答

如果 lambda 表达式的尾随返回类型缺失，则返回类型为返回表达式经过以下转换后的类型：

- 左值到右值转换
- 数组到指针转换
- 函数到指针转换

否则为 void。

因此，第 1 行 lambda 表达式的返回类型是 int。因为花括号初始化列表不是表达式，所以 {1, 2} 不是表达式。这意味着第 2 行 lambda 表达式的返回类型是 void。所以这会导致编译器错误。

## 问题58 lambda 与默认实参

以下哪些 lambda 表达式是合法的？

程序8.49：lambda 与默认实参

```cpp
void func()
{
    int i = 1;

    void g1(int = []{ return i; }());
    void g2(int = [=]{ return 0; }());
    void g3(int = [=]{ return i; }());
    void g4(int = [=]{ return 0; }());
    void g5(int = []{ return sizeof i; }());
}
```

### 问题58的解答

lambda 表达式出现在默认实参中时，不能隐式或显式捕获任何实体。因此，第 5、6 和 7 行出现的 lambda 表达式将引发编译器错误。

```text
lambda2.cpp:5:20:
error: lambda expression in default
argument cannot capture
    any entity
    void g1(int = ([]){ return i; })();

lambda2.cpp:6:20:
error: lambda expression in default
argument cannot capture
    any entity
    void g2(int = ([]){ return 0; })();

lambda2.cpp:7:20:
error: lambda expression in default
argument cannot capture
    any entity
    void g3(int = ([=]){ return i; })();

3 errors generated.
```

## 问题59 嵌套 lambda 表达式

该程序的输出是什么？

程序8.50：嵌套 lambda 表达式

```cpp
#include <iostream>
int main()
{
    int a = 1, b = 1, c = 1;
    auto m1 = [a, &b, &c]() mutable
    {
        auto m2 = [a, b, &c]() mutable
        {
            std::cout << a << b << c
                      << std::endl;
            a = 4; b = 4; c = 4;
        };
        a = 3; b = 3; c = 3;
        m2();
    };
    a = 2; b = 2; c = 2;
    m1();
    std::cout << a << b << c << std::endl;
}
```

### 问题59的解答

```text
123
234
```

## 问题60 decltype((auto 变量)) 的类型

表达式 *decltype((x))* 的类型是什么？其中 *x* 是一个 auto 变量。

### 问题60的解答

表达式 *decltype((x))* 的类型是 const x &，其中 *x* 是一个 auto 变量。

例如，在下面的示例中：

程序8.51：decltype((x)) 的类型

```cpp
void func()
{
    float x, &r = x;
    [=]
    {
        decltype(x) y1;
        decltype((x)) y2 = y1;
        decltype(r) r1 = y1;
        decltype((r)) r2 = y2;
    };
}
```

y1 的类型是 float，y2 的类型是 float const &，r1 的类型是 float &，r2 的类型是 float const &。

## 问题61 花括号初始化列表作为下标

花括号初始化列表可以用作下标吗？

### 问题61的解答

它不能用于内置的下标运算符，但可以用于用户自定义的下标运算符，在这种情况下，它将被视为 operator[] 的下标实参的初始化器，如下面这个程序所示：

程序8.52：花括号初始化列表作为下标

```cpp
#include <initializer_list>
struct A
{
    int operator[](std::initializer_list<int>);
};

int main()
{
    A a;

    a[{1,2,3}] = 10;

    int b[5];

    b[{1, 2, 3}] = 20;
}
```

这里第 12 行是合法的，但第 16 行是错误的。

## 问题62 伪析构函数

什么是*伪析构函数*？

### 问题62的解答

*伪析构函数*是非类类型的析构函数，它只能用作函数调用运算符 () 的操作数，并且这种调用的结果类型为 *void*。下面的示例针对整数类型调用了伪析构函数：

程序8.53：伪析构函数

```cpp
#include <iostream>

typedef int Integer;

int main()
{
    Integer i = 100;

    i.Integer::~Integer();

    std::cout << "i : " << i << std::endl;

    i = 200;

    std::cout << "i : " << i << std::endl;
}
```

对伪析构函数的调用

```cpp
i.Integer::~Integer()
```

没有任何效果。

对象 i 并没有被销毁；赋值 i = 200 仍然是合法的。

该程序的输出为：

```text
i : 100
i : 200
```

因为伪析构函数要求显式调用非类类型的析构函数的语法必须是合法的，所以我们可以编写代码，而不必知道给定类型是否存在析构函数。

## 问题63 动态转换

什么是*动态转换*？

### 问题63的解答

*dynamic_cast<T>(v)* 是将表达式 *v* 转换为类型 *T* 的结果，其中 *T* 是：

- 指向完整类类型的指针或引用，或
- 指向 const/volatile void 的指针。

请注意，它不会去除 const 限定。

- 1. 如果 T 是指针类型，则 v 是指向完整类类型的指针纯右值 ⇒ 结果是 T 类型的纯右值。
- 2. 如果 T 是左值引用类型，则 v 是完整类类型的左值 ⇒ 结果是 T 所引用的类型的左值。
- 3. 如果 T 是右值引用类型，则 v 是具有完整类类型的表达式 ⇒ 结果是 T 所引用的类型的将亡值（xvalue）。
- 4. 如果 v 的类型与 T 相同，或者与 T 相同，只是 T 中的类对象类型比 v 中的类对象类型具有更多 cv 限定，则结果是 v（必要时进行转换）。
- 5. 如果 v 的值在指针情况下是空指针值，则结果是 T 类型的空指针值。

## 问题64 动态转换与基类/派生类

在基类/派生类场景下，*动态转换*是如何运作的？

### 问题64的解答

假设 B 是 D 的基类。

- 如果 T 是指向 B 的指针类型，且 v 是指向 D 的指针，则结果是指向 v 所指 D 对象的唯一子对象的指针。
- 如果 T 是对 B 的引用，且 v 的类型是 D，则结果是 v 所指 D 对象的唯一 B 子对象。
- 如果 T 是左值引用，则结果是左值。
- 如果 T 是右值引用，则结果是将亡值（xvalue）。

在下面的示例中，动态转换等同于 `B* bp = dp;`。

程序8.54：动态转换与基类/派生类

```cpp
struct B {};
struct D : B {};

void func(D* dp)
{
    B* bp = dynamic_cast<B*>(dp);

}
```

## 问题65 动态转换与 void

当 T 是指向 void 的指针时，dynamic_cast<T>(v) 的结果是什么？

### 问题65的解答

- 结果是指向 v 所指的最派生对象的指针，或者
- 会执行运行时检查，以确定 v 所指向或引用的对象是否可以转换为 T 所指向或引用的类型。

## 问题66 动态转换的运行时检查

当 T 是指向类 A 的指针时，dynamic_cast<T>(v) 的结果是什么？

### 问题66的解答

- 如果在 v 所指向（或引用）的最派生对象中，v 指向（或引用）某个 A 对象的公共基类子对象，并且从 v 所指向（或引用）的子对象仅派生出一个类型为 A 的对象，则结果指向（或引用）该 A 对象。
- 否则，如果 v 指向（或引用）最派生对象的公共基类子对象，且最派生对象的类型具有一个类型为 A 的基类，该基类是明确且公共的，则结果指向（或引用）最派生对象的 A 子对象。
- 否则，运行时检查失败。
- 转换到指针类型失败时，其值为所需结果类型的空指针值。
- 转换到引用类型失败时，抛出 std::bad_cast。

## 问题67 理解动态转换

该程序的输出是什么？

程序8.55：理解动态转换

```cpp
#include <cassert>
#include <typeinfo>
#include <iostream>

class A
{
    virtual void f() {}
};

class B
{
    virtual void g() {}
};

class D : public virtual A, private B
{
};

void func()
{
    D d;

    B* bp = (B*)&d;

    A* ap = &d;

    try
    {
        D& dr = dynamic_cast<D&>(*bp);
    }
    catch(std::bad_cast & e)
    {
        std::cout << "Exception is : "
                  << e.what() << std::endl;
    }

    ap = dynamic_cast<A*>(bp);

    assert(ap == nullptr);

    bp = dynamic_cast<B*>(ap);

    assert(ap == nullptr);
}
```

