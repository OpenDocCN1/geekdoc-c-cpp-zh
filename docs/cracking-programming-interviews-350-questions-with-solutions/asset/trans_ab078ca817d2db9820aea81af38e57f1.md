
4. 接下来是全局作用域，在 outer::inner::func 定义之前，即如果第 20、11 和 7 行没有因第 3 行而声明/定义 a，那么输出将是 10。

## 问题 20 非限定名称查找

程序的输出是什么？

```text
Program 8.2: Unqualified Name Lookup

 1  #include <iostream>
 2
 3  namespace first
 4  {
 5      struct base
 6      {
 7          static int i;
 8      };
 9      // namespace A
10
11  int first::base::i = 10;
12
13  namespace second
14  {
15      struct derived : first::base
16      {
17          struct nested
18          {
19              nested()
20              {
21                  std::cout << "nested() : "
22                            << i << std::endl;
23              }
24          } n; // struct nested
25      }; // struct derived
26  }
27
28  int main()
29  {
30      second::derived d;
31  }
```

讨论在 nested 的构造函数定义期间尝试使用变量 i 时，变量 i 的声明是如何被查找的。

### 问题 20 的解答

输出为：

```text
nested() : 10
```

按给定顺序在以下作用域中查找变量 i 的声明/定义：

### 程序 8.26：ADL

```cpp
#include <iostream>

namespace A
{
    struct B {};

    void func(B b)
    {
        std::cout << "A::func" << std::endl;
    }
} // namespace A

void func(A::B b)
{
    std::cout << "func(A::B)" << std::endl;
}

void test()
{
    A::B b1;
    func(b1);
}

int main()
{
    test();
}
```

### 问题 25 的解答

该程序无法通过编译。编译器错误为：

```text
adl2.cpp:22:5: error: call to 'func' is ambiguous
    func(b1);
    ^~~~
adl2.cpp:7:10: note: candidate function
    void func(B b)

adl2.cpp:13:6: note: candidate function
void func(A::B b)

1 error generated.
```

从编译器错误中可以一目了然。

## 问题 26 ADL（参数依赖查找）

修改前一个程序以调用 `func(A::B)`？

### 问题 26 的解答

修改后的程序如下

### 程序 8.27：ADL

```cpp
#include <iostream>
namespace A
{
    struct B {};

    void func(B b)
    {
        std::cout << "A::func" << std::endl;
    }
} // namespace A
void func(A::B b)
{
    std::cout << "func(A::B)" << std::endl;
}

void test()
{
    A::B b1;

    extern void func(A::B);

    func(b1);
}

int main()
{
    test();
}
```

现在输出如下

```text
func(A::B)
```

## 问题 27 基本查找

审查下面的程序？

### 程序 8.28：基本查找

```cpp
struct A
{
    static int a;
};
int A::a = 10;

struct A
{
    int A = 20;

    A::a = 100;

    A a1;
}
```

### 问题 27 的解答

该程序无法通过编译，编译器错误为

```text
basic_lookup.cpp:14:5:
error: must use 'struct' tag to refer
to type 'A' in this
    scope
    A a1;

    struct
basic_lookup.cpp:10:9:
note: struct 'A' is hidden by a
non-type declaration of
    'A' here
    int A = 20;

1 error generated.
```

该错误本身已经说明问题，因为第 14 行：A 不再是类型。

## 问题 28 基本查找

审查下面静态数据成员 array 的定义。

### 程序 8.29：基本查找

```cpp
struct A { };

struct B
{
    struct A { };

    static const int n = 10;

    static A array[n];
};

A B::array[n];
```

### 问题 28 的解答

该程序无法通过编译，编译器错误为

```text
basic_lookup1.cpp:12:13:
error: conflicting declaration
'A B::array [10]'
A B::array[n];
        ^

basic_lookup1.cpp:9:14:
error: 'B::array' has previous
declaration as 'B::A B::array [10]'
    static A array[n];

basic_lookup1.cpp:12:13: error: declaration of
'B::A B::array [10]'
outside of class is not definition
[-fpermissive]
 A B::array[n];
        ^
```

另一个编译器的错误为

```text
basic_lookup1.cpp:12:6:
error: redefinition of 'array'
with a different type:
    'A [10]' vs 'B::A [10]'
A B::array[n];
  ^

basic_lookup1.cpp:9:14:
note: previous definition is here
    static A array[n];
         ^

1 error generated.
```

该错误本身已经说明问题。

下面的程序修复了此错误：

### 程序 8.30：基本查找

```cpp
1 struct A { };
2 struct B
3 {
5     struct A { };
6
7  static const int n = 10;
8  static A array[n];
9  };
10
11
12 B::A B::array[n];
```

## 问题 29 析构函数与 typedef

如何为给定类的 typedef 显式调用析构函数？

### 问题 29 的解答

下面的程序演示了这一点：

### 程序 8.31：析构函数与 typedef

```cpp
1 struct B
2 {
3     ~B() {}
4 };
5
6 typedef B AnotherB;
7
8 int main()
9 {
10     AnotherB * third;
11
12     third->AnotherB::~AnotherB();
13 }
```

## 问题 30 构造函数名称查找

在给定程序中，如何在两种情况下查找类 Base 的构造函数：一种作为 Base 本身，另一种作为 Derived 的基类？

```cpp
struct Base
{
    Base();
};

struct Derived : Base
{
    Derived();
};

Base::Base() { }
Derived::Derived() { }
```

### 问题 30 的解答

将 Base 的构造函数作为派生类的基类部分调用，形式如下：

```text
Derived::Base db;
```

同理，下面的调用不合法

```text
Base::Base b;
```

因为 Base::Base 并不命名一个类型。

要实现这一点，应尝试以下写法：

```text
struct Base::Base b1;
```

## 问题 31 理解命名空间

给定下面的程序：

```cpp
int x;

namespace Y
{
    void f(float);
    void h(int);
}

namespace Z
{
    void h(double);
}

namespace A
{
    using namespace Y;

    void f(int);
    void g(int);
}

int i;

namespace B
{
    using namespace Z;

    void f(char);

    int i;
}

namespace AB
{
    using namespace A;
    using namespace B;

    void g();
}
```

以下代码片段会发生什么：

1. `AB::g();`

   由于 g 直接在 AB 中声明，因此调用 AB::g()。

2. `AB::f(1);`

   由于 f 并未直接在 AB 中声明，因此规则会递归应用于 A 和 B，不搜索命名空间 Y，也不考虑 Y::f(float)；所以候选集合为 A::f(int)、B::f(char)，重载解析选择 A::f(int)。

3. `AB::f('e');`

   同上，但重载解析选择 B::f(char)。

4. `AB::x++;`

   由于 x 未直接在 AB 中声明，也未在 A 或 B 中声明，因此规则会递归应用于 Y 和 Z，结果什么也找不到，所以该程序非良构。

5. `AB::i++;`

   由于 i 未直接在 AB 中声明，因此规则会递归应用于 A 和 B，所以可选的是 A::i、B::i，因此该使用有歧义，程序非良构。

6. `AB::h(2.7);`

   由于 h 未直接在 AB 中声明，也未直接在 A 或 B 中声明，因此规则会递归应用于 Y 和 Z，所以可选的是 Y::h(int)、Z::h(double)，重载解析选择 Z::h(double)。

## 问题 32 多重声明没有问题

给定下面的程序，第 24 行和第 40 行会发生什么？

### 程序 8.32：多重声明没有问题

```cpp
1 namespace A
2 {
3     int a;
4 }
5
6 namespace B
7 {
8     using namespace A;
9 }
10
11 namespace C
12 {
13     using namespace A;
14 }
15
16 namespace BC
17 {
18     using namespace B;
19     using namespace C;
20 }
21
22 void f( )
23 {
24     BC::a++;
25 }
26
27 namespace D
28 {
29     using A::a;
30 }
31
32 namespace BD
33 {
34     using namespace B;
35     using namespace D;
36 }
```
