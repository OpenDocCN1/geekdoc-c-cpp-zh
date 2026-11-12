

- ci，一个常量整数；
- pc，一个指向常量整数的指针；
- cpc，一个指向常量整数的常量指针；
- ppc，一个指向“指向常量整数的指针”的指针；
- i，一个整数；
- p，一个指向整数的指针；以及
- cp，一个指向整数的常量指针。

初始化后，ci、cpc 和 cp 的值不能改变。pc 的值可以改变，cp 所指向的对象也可以改变。前六项中的每一项都是正确操作的示例，而其余的是非法操作，会导致以下编译错误

```text
pointers.cpp:14:8:
error: read-only variable is not assignable
  ci = 1;
  ~~ ^

pointers.cpp:15:7:
error: read-only variable is not assignable
  ci++;
  ~~^

pointers.cpp:16:9:
error: read-only variable is not assignable
  *pc = 2;
  ~~~ ^

pointers.cpp:17:8:
error: read-only variable is not assignable
  cp = &ci;
  ~~ ^

pointers.cpp:18:8:
error: read-only variable is not assignable
  cpc++;
  ~~~^

pointers.cpp:19:7:
error: assigning to 'int *' from incompatible type
      'const int *'
  p = pc;
  ~ ^

pointers.cpp:20:9:
error: assigning to 'const int **' from
incompatible type
    'int **'
    ppc = &p;
      ^ ~~
7 errors generated.
```

每一个都是不可接受的，因为它要么会改变声明为 const 的对象的值，要么会允许以后通过不带 cv 限定符的指针来修改它，例如：

```cpp
*ppc = &ci;
```

是可行的，但由于之前的错误，会使 p 指向 ci

```cpp
*p = 5;
```

从而覆写 ci。

## 问题 147 — 左值引用

查看下面的程序。

```cpp
typedef int& A;
const A aref = 3;
```

### 问题 147 的解答

该程序是非良构的，因为非 const 的左值引用被右值初始化了。aref 的类型是 int 的左值引用，而不是 const int 的左值引用。

请注意，引用可以被看作对象的名字；同时，指定类型为“对 cv void 的引用”的声明符也是非良构的。

## 问题 148 — 类型

在下面的程序中，变量 r1、r2、r3、r4、r5、r6 和 r7 的类型分别是什么？

**程序 12.4：类型**

```cpp
int i;
typedef int& LRI;
typedef int&& RRI;

LRI& r1 = i;
const LRI& r2 = i;
const LRI&& r3 = i;

RRI& r4 = i;
RRI&& r5 = 5;

decltype(r2)& r6 = i;
decltype(r2)&& r7 = i;
```

### 问题 148 的解答

它们都具有 int& 类型，因为如果 typedef、类型模板参数或 decltype 说明符表示一个类型 TR，而 TR 是某个类型 T 的引用，那么试图创建“对 cv TR 的左值引用”会创建“对 T 的左值引用”，而试图创建“对 cv TR 的右值引用”则会创建类型 TR。

## 问题 149 — 指向成员的指针

查看下面的程序。

**程序 12.5：指向成员的指针**

```cpp
1 struct X
2 {
3     void f(int);
4     int a;
5 };
6 
7 struct Y;
8 
9 int X::* pmi = &X::a;
10 void (X::* pmf)(int) = &X::f;
11 double X::* pmd;
12 char Y::* pmc;
13 
14 int main()
15 {
16     X obj;
17 
18     obj.*pmi = 7;
19     (obj.*pmf)(7);
20 }
```

### 问题 149 的解答

它分别声明 pmi、pmf、pmd 和 pmc 为：指向 X 的 int 类型成员的指针、指向 X 的 void(int) 类型成员的指针、指向 X 的 double 类型成员的指针，以及指向 Y 的 char 类型成员的指针。

pmd 的声明是良构的，即使 X 没有 double 类型的成员。类似地，pmc 的声明也是良构的，即使 Y 是不完整类型。pmi 和 pmf 可以像程序中展示的那样使用。

## 问题 150 — 数组与 typedef

CA 和 CAA 的类型是什么？

```cpp
1 typedef int A[5] , AA[2][3];
2 typedef const A CA;
3 typedef const AA CAA;
```

### 问题 150 的解答

- CA 表示一种 *包含 5 个 const int 的数组* 类型。
- CAA 表示一种 *包含 2 个“包含 3 个 const int 的数组”的数组* 类型。

## 问题 151 — 数组与 sizeof

程序的输出是什么？

**程序 12.6：数组与 sizeof**

```cpp
#include <iostream>

extern int x[10];

struct S
{
    static int y[20];
};

int x[];
int S::y[];

void f()
{
    std::cout << sizeof(x)/sizeof(int) << std::endl;
}

void g()
{
    std::cout << sizeof(S::y)/sizeof(int) << std::endl;
}

void h()
{
    extern int x[];
    std::cout << sizeof(x)/sizeof(int) << std::endl;
}

int main()
{
    f();
    g();
    h();
}
```

### 问题 151 的解答

程序无法编译，因为函数 *h* 对不完整对象类型 *x* 调用了 sizeof。如果省略该函数，程序的其余部分将分别输出 *10* 和 *20*。

## 问题 152 — 函数的类型

下面的说法正确吗？

由

`int (*)(const int p, decltype(p)*)`

表示的函数类型与由

`int (*)(int, const int*)`

表示的函数类型相同。

### 问题 152 的解答

是的。因为函数的类型是根据以下规则确定的：

- 每个参数（包括函数参数包）的类型由其自身的 *声明说明符序列* 和 *声明符* 确定。
- 在确定每个参数的类型后，任何类型为 *T 的数组* 或 *返回 T 的函数* 的参数，都会被分别调整为 *指向 T 的指针* 或 *指向返回 T 的函数的指针*。
- 在生成参数类型列表后，形成函数类型时，任何修饰参数类型的顶层 cv 限定符都会被删除。
- 转换后的参数类型列表，以及省略号或函数参数包存在与否，共同构成函数的 *参数类型列表*。

请注意，这种转换不会影响参数的类型。

## 问题 153 — 成员函数的类型

成员函数 `f` 的类型是什么？

```cpp
typedef void F();
struct A
{
    const F f;
};
```

### 问题 153 的解答

它等价于 `void f();`

## 问题 154 — typedef 与函数定义

这个代码片段有什么问题？

**程序 12.7：typedef 与函数定义**

```c
1 typedef void F();
2 F fv;
3 F fv { }
4 void fv() { }
```

### 问题 154 的解答

编译器错误为：

```text
typedef.cpp:3:3: error: illegal initializer
  (only variables can be initialized)
F fv { }

typedef.cpp:3:9:
error: expected ';' after top level declarator
F fv { }
       ^
2 errors generated.
```

原因很简单：函数类型的 typedef 可以用来声明函数，但不能用来定义函数。

- F fv; 是可以的，它等价于 *void fv();*
- F fv{ }; 是非良构的
- void fv() { } 也是可以的，因为它是 fv 的定义

## 问题 155 — typedef 与 const volatile 函数

这个代码片段有什么问题？

**程序 12.8：typedef 与 const volatile 函数**

```c
1 typedef int FIC(int) const;
2 
3 FIC f;
4 
5 struct A
6 {
7     FIC f;
8 };
9 
10 FIC A::*pm = &A::f;
```

### 问题 155 的解答

编译器错误为：

```text
typedef1.cpp:3:1:
error: non-member function of type 'FIC'
    (aka 'int (int const)' cannot have 'const'
        qualifier
FIC f;
^
1 error generated.
```

原因是：声明符中包含 cv 限定符序列的函数类型的 typedef 只能用于

- 声明非静态成员函数的函数类型，
- 声明成员指针所指向的函数类型。
  或
- 声明另一个函数 typedef 声明的顶层函数类型。

因此，FIC f 是非良构的，因为它并没有声明一个成员函数。

## 问题 156 — 尾随返回类型

声明一个函数模板 add，它接受两个不同类型的参数，并返回所传参数之和。

### 问题 156 的解答

```cpp
¹ template <typename T, typename U>
² auto add(T t, U u) -> decltype(t + u);
```

另一种写法是：

```cpp
¹ template <typename T, typename U>
² decltype((* (T*)0) + (* (U*)0)) add(T t, U u);
```

## 问题 157 — 尾随返回类型

声明一个函数 f，使我们能够编写以下代码：

```cpp
¹ int add(int, int);
² float subtract(int, int);
³ void g()
⁴ {
⁵     f(add, subtract);
⁶ }
```

### 问题 157 的解答

