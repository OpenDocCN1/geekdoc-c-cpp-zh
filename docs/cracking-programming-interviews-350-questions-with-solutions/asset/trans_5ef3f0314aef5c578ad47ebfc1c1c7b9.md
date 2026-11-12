
```cpp
2 template <typename T> void g(T);
3
4
5 namespace A
6 {
7     struct X
8     {
9         friend void f1(X);
10
11         struct Y
12         {
13             friend void f2();
14
15             friend void func(int);
16
17             friend void g<>(int);
18         };
19     };
20
21     X x;
22
23     void f2() { f1(x); }
24
25     void f1(X) { }
26
27     void func(int) { }
28 }
29
30 int main()
31 {
32     using A::x;
33
34     A::f1(x);
35
36     A::X::f1(x);
37
38     A::X::Y::f2();
39 }
```

### 问题125的解答

编译器错误是：

```text
namespace_friend.cpp:36:11:
error: no type named 'f1' in 'A::X'
   A::X::f1(x);
   ^~~~~~~~~
namespace_friend.cpp:38:14:
error: no member named 'f2' in 'A::X::Y'
   A::X::Y::f2();
   ^~~~~~~~~~~~~
2 errors generated.
```

另一个编译器给出了以下错误：

```text
namespace_friend.cpp: In function ‘int main()’:
namespace_friend.cpp:36:5:
error: ‘f1’ is not a member of ‘A::X’
    A::X::f1(x);
    ^
namespace_friend.cpp:38:5:
error: ‘f2’ is not a member of ‘A::X::Y’
    A::X::Y::f2();
    ^
```

请注意，f1不是A::X的成员，f2也不是A::X::Y的成员。

## 问题126 命名空间别名

什么是命名空间别名？

### 问题126的解答

命名空间别名，比如B，为给定的命名空间（比如A）声明一个替代名称，如下所示：

```cpp
namespace A {}
namespace B = A;
```

### 程序11.4：命名空间别名

```cpp
#include <cassert>
namespace long_name_123456789
{
    int i = 10;
} // namespace long_name_123456789

namespace short_name1 = long_name_123456789;
int main()
{
    assert(short_name1::i ==
        long_name_123456789::i);
}
```

请注意，命名空间别名是实际命名空间的同义词，但在命名空间别名定义中查找命名空间名称时，只考虑命名空间名称。

重复声明是允许的，从下面的程序可以看出：

### 程序11.5：重声明命名空间别名

```cpp
1 #include <cassert>
2
3 namespace long_name_123456789
4 {
5     int i = 10;
6 } // namespace long_name_123456789
7
8 namespace short_name = long_name_123456789;
9 namespace short_name = long_name_123456789;
10
11 int main()
12 {
13     assert(short_name::i ==
14            long_name_123456789::i);
15 }
```

### 程序11.6：重声明命名空间别名

```cpp
1 #include <cassert>
2
3 namespace long_name_123456789
4 {
5     int i = 10;
6 } // namespace long_name_123456789
7
8 namespace short_name1 = long_name_123456789;
9 namespace short_name2 = short_name1;
10 namespace short_name2 = short_name2;
11
12 int main()
13 {
14     assert(short_name1::i ==
15            long_name_123456789::i);
16 }
```

但重定义是不允许的：

### 程序11.7：重定义命名空间别名

```cpp
1 #include <cassert>
2
3 namespace long_name_1 {}
4 namespace long_name_2 {}
5
6 namespace A = long_name_1;
7 namespace A = long_name_2;
```

该程序无法编译，错误如下：

```text
namespace_alias3.cpp:7:11:
error: redefinition of 'A' as different kind of
       symbol
namespace A = long_name_2;
^
namespace_alias3.cpp:6:11:
note: previous definition is here
namespace A = long_name_1;

1 error generated
```

## 问题127 using声明

在这个程序中，类Derived的成员函数会调用哪些函数？

### 程序11.8：using声明

```cpp
1 struct Base
2 {
3     void f1(char);
4
5     void f2(char);
6 };
7
8 struct Derived : Base
9 {
10    using Base::f1;
11
12    void f1(int)
13    {
14        f1('a');
15    }
16
17    void f2(int)
18    {
19        f2('a');
20    }
21 };
```

### 问题127的解答

- 第14行调用 Base::f1(char)
- 第19行递归调用 Derived::f2(int)

## 问题128 using声明与基类

using声明能否像该程序所示那样，用来引用非基类的成员函数？

### 程序11.9：using声明与基类

```cpp
struct Base
{
    void f1();
};
struct Test
{
    void f2();
};
struct Derived : Base
{
    using Base::f1;
    using Test::f2;
};
```

### 问题128的解答

不。该程序会导致编译器错误：

```text
using2.cpp:14:11:
error: using declaration refers into
    'Test::', which is not a
        base class of 'Derived'
        using Test::f2;
               ^~~~~
1 error generated.
```

## 问题129 using声明与模板标识

这段代码有什么问题？

### 程序11.10：using声明与模板标识

```cpp
struct A
{
    template <typename T> void func(T);

    template <typename T> struct B { };
};
struct B : A
{
    using A::func<double>;
    using A::B<int>;
};
```

### 问题129的解答

该程序会导致编译器错误：

```text
using3.cpp:10:14:
error: using declaration cannot refer
to a template
      specialization
      using A::func<double>;
      -------
using3.cpp:12:14:
error: using declaration cannot refer
to a template
      specialization
      using A::B<int>;
      -----
2 errors generated.
```

原因很简单：using声明不能用来命名模板标识（template-id）。

## 问题130 using声明与成员声明

这段代码有什么问题？

### 程序11.11：using声明与成员声明

```cpp
1 struct A
2 {
3     int i;
4     static int si;
5 };
6
7 void f()
8 {
9     using A::i;
10    using A::si;
11 }
```

### 问题130的解答

该程序会导致编译器错误：

```text
using4.cpp:9:14:
error: using declaration cannot refer to
class member
      using A::i;
      ---
using4.cpp:10:14:
error: using declaration cannot refer to
class member
    using A::si;
          ^

2 errors generated.
```

另一个编译器给出的错误是：

```text
using4.cpp: In function ‘void f()’:
using4.cpp:9:14: error: ‘A’ is not a namespace
    using A::i;
         ^

using4.cpp:10:14: error: ‘A’ is not a namespace
    using A::si;
         ^
```

针对类成员的using声明应该是一个成员声明。

A::i是一个类成员，而这不是成员声明。A::si是一个类成员，而这不是成员声明。因此出现错误。

## 问题131 using声明与引用成员

请查看下面的代码。

### 程序11.12：using声明与引用成员

```cpp
void f();

namespace A
{
    void g();
}

namespace B
{
    using ::f;
    using A::g;
}

void h()
{
    B::f();
    B::g();
}
```

### 问题131的解答

在命名空间B中，`using ::f`调用全局的f。`using A::g`调用A的g。在函数h()中，`B::f()`调用全局的f，`B::g()`调用A::g。简而言之，由using声明声明的成员可以像其他成员名称一样通过显式限定来引用，并且在using声明中，前缀`::`指的是全局命名空间。

## 问题132 —— 多重using声明

请查看下面的代码。

### 程序11.13：多重using声明

```cpp
namespace A
{
    int i;
}
namespace A1
{
    using A::i;
    using A::i;
}
void f()
{
    using A::i;
    using A::i;
}
struct B
{
    int i;
};
struct X : B
{
    using B::i;
    using B::i;
};
```

### 问题132的解答

编译器错误是：

```text
using6.cpp: In function ‘void f()’:
using6.cpp:15:14:
error: ‘i’ is already declared in this
scope
        using A::i;
              ^
using6.cpp: At global scope:
using6.cpp:26:14:
error: redeclaration of 'using B::i'
    using B::i;
       ^
using6.cpp:25:14:
note: previous declaration 'using B::i'
    using B::i;
       ^
```

using声明是一种声明，因此可以在允许重复声明的地方（且仅在这些地方）重复使用。在这段代码中，在命名空间A1中，第二次出现的`*using A::i*`是一个有效的重复声明，而在void f中的`*using A::i*`以及struct X中的`*using B::i*`则是无效的重复成员声明。

## 问题133 using声明的可用性

请查看下面的代码。

### 程序11.14：using声明的可用性

```cpp
 1 namespace A
 2 {
 3     void f(int);
 4 }
 5
 6 using A::f;
 7
 8 namespace A
 9 {
10     void f(char);
11 }
12
13 void foo()
14 {
15     f('a');
16 }
17
18 void bar()
19 {
20     using A::f;
21     f('a');
22 }
```

### 问题133的解答

在全局命名空间中，`*using A::f*`的第一次出现将`*f*`标记为`*A::f*`的同义词；也就是说，是`*A::f(int)*`的同义词。在`*void foo()*`中，`*f('a')*`调用`*f(int)*`，即使`*f(char)*`存在。在函数`*void bar()*`中，`*using A::f*`将`*f*`标记为`*A::f*`的同义词；也就是说，是`*A::f(int)*`和`*A::f(char)*`的同义词，而`*f('a')*`调用`*f(char)*`。

