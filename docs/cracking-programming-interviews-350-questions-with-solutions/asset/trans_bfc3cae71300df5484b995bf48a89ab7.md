

-   其函数体为空，即其函数体中没有任何语句。
-   每个非静态数据成员和基类子对象都被初始化。
-   参与初始化非静态数据成员和基类子对象的每个构造函数都是 `constexpr` 构造函数。
-   对于未被 mem-initializer-id 命名的非静态数据成员，直接或间接出现在其花括号或等号初始化器中的、作为初始化子句的每个赋值表达式都是常量表达式。
-   用于将构造函数实参转换为相应形参类型，以及将完整表达式转换为相应成员类型的每个隐式转换都是常量表达式。

```cpp
struct A
{
    explicit constexpr A(int i = 0)
        : m(i)
    {
    }

private:
    int m;
};
```

平凡的复制/移动构造函数也是 constexpr 构造函数。

## 问题 109 — constexpr 函数示例

程序的输出是什么？

### 程序 9.1：constexpr 函数示例

```cpp
#include <iostream>
constexpr int func(void *)
{
    return 10;
}
constexpr int func(...)
{
    return 20;
}

constexpr int invoke1_func()
{
    return func(0);
}

constexpr int invoke2_func(int n)
{
    return func(n);
}

constexpr int invoke3_func(int n)
{
    return func(n * 0);
}

int main()
{
    std::cout << "invoke1_func(): "
              << invoke1_func() << std::endl;

    std::cout << "invoke2_func(200): "
              << invoke2_func(200) << std::endl;

    std::cout << "invoke3_func(0): "
              << invoke2_func(0) << std::endl;

    std::cout << "invoke3_func(200): "
              << invoke3_func(200) << std::endl;
}
```

### 问题 109 的解答

程序输出为：

```text
invoke1_func(): 10
invoke2_func(200): 20
invoke3_func(0): 20
invoke3_func(200): 20
```

请注意，即使 n = 0，`invoke2_func` 也会调用 `func(...)`。

## 问题 110 — `constexpr` 函数与替换

程序的输出是什么？

### 程序 9.2：constexpr 函数与替换

```cpp
#include <iostream>
namespace A
{
    constexpr int x = 10;
    constexpr int func()
    {
        return x;
    }
} // namespace A

constexpr int x = 20;

constexpr int invoke_func()
{
    return A::func();
}

int main()
{
    std::cout << "invoke_func() : "
              << invoke_func() << std::endl;
}
```

### 问题 110 的解答

程序输出为：

`invoke_func() : 10`

请注意，替换之后不会再次查找 *x*。

## 问题 111 — 修改 constexpr 函数

程序的输出是什么？

### 程序 9.3：修改 constexpr 函数

```cpp
#include <iostream>

constexpr int func(bool b)
{
    return b ? throw 0 : 0;
}

constexpr int func()
{
    throw 0;
}

int main()
{
    func(true);
}
```

### 问题 111 的解答

该程序无法通过编译。编译器错误为

```text
constexpr_function1.cpp:10:5:
error: statement not allowed
in constexpr function
    throw 0;
    ^
1 error generated.
```

另一个编译器给出以下错误：

```text
constexpr_function1.cpp:
In function ‘constexpr int func()’:
constexpr_function1.cpp:11:1:
error: body of constexpr
function ‘constexpr int func()’
not a return-statement
}
~
```

从错误描述本身即可说明。

## 问题 112 — 修改 constexpr 构造函数

请审查该程序。

### 程序 9.4：修改 constexpr 构造函数

```cpp
1 struct Base
2 {
3     constexpr Base(int i)
4     : m(0)
5     {}
6
7     int m;
8 };
9
10 int x;
11
12 struct Derived : Base
13 {
14     constexpr Derived()
15     : Base(x)
16     {}
17
18 };
```

### 问题 112 的解答

该程序无法通过编译。编译器错误为

```text
constexpr_constructor1.cpp:14:15:
error: constexpr constructor never produces a
    constant expression [-Winvalid-constexpr]
    constexpr Derived()

constexpr_constructor1.cpp:16:10:
note: read of non-const variable 'x' is not
    allowed in a constant expression
    Base(x)

constexpr_constructor1.cpp:10:5:
note: declared here
int x;
^

1 error generated.
```

另一个编译器给出以下错误：

```text
constexpr_constructor1.cpp:
  In constructor 'constexpr Derived::Derived()':
constexpr_constructor1.cpp:17:6:
error: the value of 'x' is not usable
in a constant expression
    {}
    ^
constexpr_constructor1.cpp:10:5:
note: 'int x' is not const
    int x;
    ^
```

从错误描述本身即可说明。

## 问题 113 — 字面类型

什么是*字面类型*？

### 问题 113 的解答

如果满足以下条件，则类型是字面类型：

-   标量类型；或
-   具有以下条件的类类型：
    -   平凡的复制构造函数，
    -   没有非平凡的移动构造函数，
    -   平凡的析构函数，
    -   平凡的默认构造函数，或至少一个除复制或移动构造函数之外的 constexpr 构造函数，并且
    -   所有非静态数据成员和基类都是字面类型；或
-   字面类型的数组。

## 问题 114 — constexpr 与字面类型

该程序有什么问题？

### 程序 9.5：constexpr 与字面类型

```cpp
struct A
{
    A();

    constexpr void func();
};
```

### 问题 114 的解答

此代码无法通过编译。编译器错误为

```text
constexpr_literal_type.cpp:5:20:
error: non-literal type 'A' cannot have
       constexpr members
       constexpr void func();
                      ^

constexpr_literal_type.cpp:1:8:
note: 'A' is not literal because it is not an
      aggregate and has no constexpr constructors
      other than copy or move
      constructors

struct A
       ^

1 error generated.
```

另一个编译器给出如下错误：

```text
constexpr_literal_type.cpp:5:20:
error: enclosing class of constexpr non-static
 member function 'void A::func() const' is not a
 literal type
        constexpr void func();

constexpr_literal_type.cpp:1:8: note:
 'A' is not literal
because:
  struct A
  ^

constexpr_literal_type.cpp:1:8:
 note: 'A' is not an aggregate, does not have a
 trivial default constructor, and has
 no constexpr constructor that is not a copy or move
 constructor
```

从错误描述本身即可说明。

## 问题 115 — constexpr 与构造函数

该程序有什么问题？

### 程序 9.6：constexpr 与构造函数

```cpp
1 struct Point
2 {
3     int x, y;
4 };
5 constexpr Point p1 = { 10, 20 };
6 
7 constexpr Point p2;
```

### 问题 115 的解答

此代码无法通过编译。编译器错误为

```text
constexpr_object.cpp:8:17:
error: default initialization of
an object of const
    type 'const Point' requires a user-provided
    default
    constructor
constexpr Point p2;

1 error generated.
```

另一个编译器给出如下错误：

```text
constexpr_object.cpp:8:17:
error: uninitialized const ‘p2’
[-fpermissive]
    constexpr Point p2;
                  ^
constexpr_object.cpp:1:8:
note: ‘const struct Point’ has no
user-provided default constructor
    struct Point
          ^
constexpr_object.cpp:3:9:
note: and the implicitly-defined
constructor does not initialize ‘int Point::x’
    int x, y;
          ^
```

请注意，在对象声明中使用的 constexpr 说明符将该对象声明为 const，该对象应被初始化并具有字面类型。如果它由构造函数调用初始化，则该调用应为常量表达式；否则，其初始化器中出现的每个完整表达式都必须是常量表达式。

```cpp
34  int* ip;
35  ip = const_cast<int*>(cip);
36  *ip = 4;
37
38  const int* ciq = new const int (3);
39  int* iq = const_cast<int*>(ciq);
40  *iq = 4;
41 }
```

### 问题 116 的解答

此代码无法通过编译。编译器错误为

```text
const_volatile.cpp:19:10:
error: read-only variable is not assignable
    y.x.j++;
    ~~~~ ^
const_volatile.cpp:27:8:
error: read-only variable is not assignable
    ci = 11;
    ~~ ^
const_volatile.cpp:32:10:
error: read-only variable is not assignable
    *cip = 4;
    ~~~~ ^
3 errors generated.
```

另一个编译器给出如下错误：

```text
const_volatile.cpp: In function ‘int main()’:
const_volatile.cpp:19:10:
error: increment of member ‘X::j’ in
read-only object
    y.x.j++;
      ^
const_volatile.cpp:27:8:
error: assignment of read-only variable ‘ci’
    ci = 11;
      ^
const_volatile.cpp:32:10:
error: assignment of read-only location ‘* cip’
    *cip = 4;
       ^
```

