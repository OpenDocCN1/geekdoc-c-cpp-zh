
```cpp
}

struct B
{
    B()
    {
        std::cout << "B()" << std::endl;
        std::atexit(&func);
    }
    ~B()
    {
        std::cout << "~B()" << std::endl;
    }
};
static B b;

static A a;

int main()
{
}
```

### 问题 41 的解答

程序的输出是：

```text
B()
A()
~A()
~B()
func()
```

请注意，此处对 `std::atexit` 的调用先序于具有静态存储期的对象初始化完成，因此对对象 `a` 的析构函数的调用先序于对传递给 `std::atexit` 的函数 `func` 的调用。

以类似方式，让我们回顾下面的程序：

### 程序 8.41：std::atexit 与 static

```cpp
#include <cstdlib>
#include <iostream>

void func()
{
    std::cout << "func()" << std::endl;
}
struct A

21
22 static A a ;
23 int main ( )
24 {
25 }
26
```

### 问题 42 的解答

程序的输出是：

```text
f2()
f1()
```

不言自明。

## 问题 43 存储期

一个给定对象一旦创建，可能有多少种存储期？

### 问题 43 的解答

确定包含该对象的存储的最小潜在生存期，有如下四种存储期：

- 1. 动态存储期：由全局分配函数 *operator new* 和 *operator new[]* 启用，
- 2. 静态存储期：由 *static* 启用。这些实体的存储应持续整个程序运行期间。
- 3. 线程存储期：由 *thread_local* 启用
- 4. 自动存储期：由 *register* 启用，或未显式声明为 *static* 或 *extern*。

## 问题 44 整数类型

什么是整数类型？

### 问题 44 的解答

以下类型统称为*整数类型*：

- bool
- char
- char16_t
- char32_t
- wchar_t
- 有符号整数类型，以及
- 无符号整数类型

## 问题 45 整数类型

什么是整数类型？

### 问题 45 的解答

以下类型统称为*整数类型*：

- bool
- char
- char16_t
- char32_t
- wchar_t
- 有符号整数类型，以及
- 无符号整数类型

## 问题 46 排序：const/volatile

列举 *const* 和 *volatile* 上的偏序关系？

### 问题 46 的解答

请注意，cv 表示 const 和/或 volatile。

- 无 cv 限定符 < const
- 无 cv 限定符 < volatile
- 无 cv 限定符 < const volatile
- const < const volatile
- volatile < const volatile

## 问题 47 值类别：左值/右值

什么是左值？

什么是右值？

讨论表达式值类别的其他成员。

### 问题 47 的解答

与表达式关联的值的层次结构如下：

![](img/78e1bff64796dccbf49e7c84b8201fb2_378_0.png)

图 8.1：表达式值类别分类

- 1. *左值*：这个名称来源于早期含义，即与其出现在赋值左侧相关联。
  - *左值*指定一个函数或一个对象。
  - 如果 *ptr* 是指向对象或函数的指针，那么 `*ptr` 是*左值*表达式。
  - 调用返回类型为*左值*引用的函数，结果是*左值*。
- 2. *将亡值*：代表*将亡值*。
  - 调用返回类型为*右值*引用的函数，结果是*将亡值*。
  - 它指代一个对象，通常接近其生存期末尾，因此其资源可以被移动。
- 3. *泛左值*：代表*泛化左值*。因此它指代*左值*或*将亡值*。泛左值也可以具有不完整类型。
- 4. *右值*：这个名称来源于早期含义，即与其出现在赋值右侧相关联。

  它是：
  - 一个将亡值
  - 一个临时对象
  - 一个子对象
  - 一个不与对象关联的值。
- 5. *纯右值*：代表*纯右值*，即不是将亡值的右值。
  - 纯右值保存返回类型不是引用的函数的结果。
  - 字面量（如 10、true 或 1.2e3）的值是纯右值。
  - 类类型的纯右值可以具有 cv 限定类型。
  - 非类类型的纯右值总是具有无 cv 限定的类型。
  - 纯右值是完整类型或 void 类型。

## 问题 48 对齐

什么是*对齐*？

### 问题 48 的解答

*对齐*是给定对象可被分配的连续地址之间的字节数。

- 每个对齐值都是非负的 2 的整数次幂。
- 它表示为 `std::size_t` 类型的整数常量。
- 完整类型、数组或对完整对象类型的引用的对齐要求，可以使用 *alignof* 表达式获得。
- 基础对齐 ≤ `alignof(std::max_align_t)` < 扩展对齐。

## 问题 49 左值到右值转换

什么是左值到右值转换？

### 问题 49 的解答

从技术上讲，它是泛左值到纯右值的转换。

- 对于完整类型 T，如果它不是函数或数组，则可以转换为纯右值。
- 对于不完整类型，该转换具有未定义行为。
- 对于类类型 T，泛左值应当是 T 类型的对象或派生自 T 的类型的对象。
- 该对象应当已初始化。
- 对于非类类型 T，纯右值的类型是不带任何 const 和/或 volatile 的 T 类型。
- 对于类类型 T，纯右值的类型是 T。

```cpp
5
6 A&& operator+(A, A);
7
8 A&& f();
9
10 int main()
11 {
12     A a;
13
14     A&& a1 = static_cast<A&&>(a);
15 }
```

### 问题 51 的解答

以下表达式是*将亡值*：

- `f()`
- `f().m`
- `static_cast<A&&>(a)`
- `a + a`

表达式 *a* 是左值。

## 问题 52 字面量与左值

字面量是*左值*吗？

### 问题 52 的解答

字符串字面量是*左值*。所有其他字面量都是*纯右值*。

## 问题 53 this 指针的有效用法

### 程序 8.45：this 指针的有效用法

```cpp
1 class Outer
2 {
3     int a[sizeof(*this)];
4
5     unsigned int sz = sizeof(*this);
6
7     void f()
8     {
9         int b[sizeof(*this)];
10
11         struct Inner
12         {
13             int c[sizeof(*this)];
14         };
15     }
16 };
17
18 int main() {}
```

### 问题 53 的解答

该程序无法编译。编译器错误为：

```text
this.cpp:3:19:
error: invalid use of 'this' outside of a
        non-static member
        function
        int a[sizeof(*this)];

this.cpp:13:27:
error: invalid use of 'this' outside of a
        non-static member
        function
        int c[sizeof(*this)];

2 errors generated.
```

从这个编译器错误可以明显看出，*this* 在第 3 行和第 13 行的用法无效，因为第 3 行不在成员函数内部，而第 13 行不在类 *Inner* 的成员函数内部。

## 问题 54 sizeof

该程序的输出是什么？

### 程序 8.46：sizeof

```text
1:#include <iostream>
2:#include <iomanip>
3
4 struct A
5 {
6    int i ;
7 };
8
9 int main()
10 {
11    std::cout << sizeof(A::i) << std::endl;
12    std::cout << sizeof(A::i + 10) << std::endl;
13    std::cout << sizeof(A::i - 10) << std::endl;
14
15    std::cout << std::boolalpha;
16
17    std::cout << (sizeof(A::i + 20)
18                 ==
19                sizeof(A::i - 20) )
20        << std::endl;
21 }
```

### 问题 54 的解答

程序的输出是：

```text
4
4
4
true
```

## 问题 55 lambda 与排序

编写一个函数，根据绝对值对浮点数向量进行排序。

### 问题 55 的解答

我们可以使用 lambda 表达式创建简单的未命名函数对象：

### 程序 8.47：lambda 与排序

```cpp
1:#include <algorithm>
2:#include <cmath>
3:#include <vector>
4:
5 void absort(std::vector<float> vf)
6 {
7     std::sort(vf.begin(),
8               vf.end(),
9               [](float a, float b)
10              {
11                  return std::abs(a)
12                         <
13                         std::abs(b);
14              }
15              );
16 }
```

lambda 表达式的求值结果是一个纯右值临时对象，称为闭包对象。

## 问题 56 lambda 的类型

lambda 表达式的类型是什么？

### 问题 56 的解答

lambda 表达式的类型是唯一的未命名类类型（联合类型除外）。它也称为闭包类型。请注意，此类型不是聚合类型。

## 问题 57 lambda 的返回类型

