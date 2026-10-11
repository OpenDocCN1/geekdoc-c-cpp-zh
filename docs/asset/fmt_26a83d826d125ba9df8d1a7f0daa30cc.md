
你可以放心地将指向对象的指针在 C 和 C++ 之间传递。甚至可以在 C 程序中使用声明来访问 `re` 和 `im`：

```c
/* 在 C 中： */
struct complex {
double re, im;
/* 没有操作 */
};
```

任何语言中的布局规则可能很复杂，语言之间的布局规则甚至可能难以指定。然而，你可以在 C 和 C++ 之间传递内置类型，也可以传递没有虚函数的类（**结构体**）。如果一个类有虚函数，你应该只传递指向其对象的指针，并将实际操作留给 C++ 代码。`call_f()` 就是一个例子：`f()` 可能是 **虚** 函数，然后该示例将展示如何从 C 调用虚函数。

除了坚持使用内置类型外，最简单的、最安全的类型共享方法是在公共 C/C++ 头文件中定义的 **结构体**。然而，这种策略严重限制了 C++ 的使用方式，因此我们不会局限于此。

### 27.2.5 指向函数的指针

如果我们想在 C 中使用面向对象技术（§14.2–4），我们可以做什么？基本上，我们需要虚函数的替代方案。对于大多数人来说，第一个想到的想法是使用带有“类型字段”的 **结构体**，该字段描述给定对象代表的形状类型。例如：

```c
struct Shape1 {
    enum Kind { circle, rectangle } kind;
    /* ... */
};
void draw(struct Shape1* p)
{
    switch (p->kind) {
    case circle:
        /* 绘制为圆形 */
        break;
    case rectangle:
        /* 绘制为矩形 */
        break;
    }
}
int f(struct Shape1* pp)
{
    draw(pp);
    /* ... */
}
```

这是可行的。但是有两个陷阱：

- 对于每个“伪虚”函数（如 `draw()`），我们都必须编写一个新的 `switch` 语句。
- 每次我们添加一个新形状时，我们都必须通过向 `switch` 语句添加一个案例来修改每个“伪虚”函数（如 `draw()`）。

第二个问题相当棘手，因为它意味着我们不能将这些“伪虚”函数作为库的一部分提供，因为我们的用户将不得不经常修改这些函数。最有效的替代方案涉及指向函数的指针：

```c
typedef void (*Pctf0)(struct Shape2*);
typedef void (*Pctfint)(struct Shape2*,int);
struct Shape2 {
    Pctf0 draw;
    Pctfint rotate;
    /* ... */
};
```

```c
void draw(struct Shape2* p)
{
    (p->draw)(p);
}
void rotate(struct Shape2* p, int d)
{
    (p->rotate)(p,d);
}
```

这个 `Shape2` 可以像 `Shape1` 一样使用。

```c
int f(struct Shape2* pp)
{
    draw(pp);
    /* ... */
}
```

通过稍微额外的工作，对象不必为每个伪虚函数持有一个指向函数的指针。相反，它可以持有一个指向函数指针数组的指针（就像 C++ 中实现虚函数那样）。在现实世界程序中使用这种方案的主要问题是正确初始化所有这些指向函数的指针。

### 27.3 次要的语言差异

本节举例说明了次要的 C/C++ 差异，如果你从未听说过它们，这些差异可能会让你跌倒。由于这些差异都有明显的变通方法，因此它们很少会对编程产生严重影响。

#### 27.3.1 struct 标签命名空间

在 C 中，**结构体**的名称（没有 **class** 关键字）与其他标识符处于单独的命名空间中。因此，每个 **结构体** 的名称（称为*结构标签*）都必须以关键字 **struct** 为前缀。例如：

```c
struct pair { int x,y; };   pair p1;              /* 错误：作用域内没有标识符 pair */
struct pair p2;            /* 正确 */
int pair = 7;             /* 正确：结构标签 pair 不在作用域内 */
struct pair p3;            /* 正确：结构标签 pair 没有被 int 隐藏 */
pair = 8;                 /* 正确：pair 指的是 int */
```

令人惊讶的是，由于一个巧妙的兼容性技巧，这在 C++ 中也能正常工作。使用与 `struct` 同名的变量（或函数）是一种相当常见的 C 语言惯用法，尽管我们并不推荐这种做法。

如果你不想在每个结构名称前都写上 `struct`，请使用 `typedef`（§20.5）。以下惯用法很常见：

```c
typedef struct { int x, y; } pair;  
pair p1 = { 1, 2 };
```

一般来说，你会发现 `typedefs` 在 C 中更常见且更有用，因为在 C 中你无法定义带有关联操作的新类型。

在 C 中，嵌套 `struct` 的名称位于它们所嵌套的 `struct` 的同一作用域中。例如：

```c
struct S {
    struct T { /* … */ };
    /* … */
};
struct T x;   /* 在 C 中合法（在 C++ 中不合法） */
```

在 C++ 中，你会这样写：

```cpp
S::T x;       // 在 C++ 中合法（在 C 中不合法）
```

在 C 中，尽可能避免嵌套 `struct`：它们的作用域规则与大多数人天真（且合理）的期望不同。

#### 27.3.2 关键字

C++ 中的许多关键字在 C 中并非关键字（因为 C 不提供相应的功能），因此可以在 C 中用作标识符：

**在 C++ 中是关键字但在 C 中不是关键字的**

| alignas | class | inline | private | true |
| :--- | :--- | :--- | :--- | :--- |
| alignof | compl | mutable | protected | try |
| and | concept | namespace | public | typeid |
| and_eq | const_cast | new | reinterpret_cast | typename |
| asm | constexpr | noexcept | requires | using |
| bitand | delete | not | static_assert | virtual |
| bitor | dynamic_cast | not_eq | static_cast | wchar_t |
| bool | explicit | nullptr | template | xor |
| catch | export | operator | this | xor_eq |
| char16_t | false | or | thread_local | |
| char32_t | friend | or_eq | throw | |

不要在 C 中使用这些名称作为标识符，否则你的代码将无法移植到 C++。如果你在一个头文件中使用这些名称之一，那么该头文件在 C++ 中将无法使用。

一些 C++ 关键字在 C 中是宏：

**在 C++ 中是关键字但在 C 中是宏的**

| and | bitor | false | or | wchar_t |
| :--- | :--- | :--- | :--- | :--- |
| and_eq | bool | not | or_eq | xor |
| bitand | compl | not_eq | true | xor_eq |

在 C 中，它们定义在 `<ciso646.h>` 和 `<stdbool.h>`（bool, true, false）中。不要利用它们在 C 中是宏这一事实。

#### 27.3.3 定义

C++ 允许在比 C89 更多的地方进行定义。例如：

```c
for (int i = 0; i<max; ++i) x[i] = y[i];    // i 的定义在 C 中不被允许
while (struct S* p = next(q)) {               // p 的定义在 C 中不被允许
    /* ... */
}
void f(int i)
{
    if (i<0 || max<=i) error("range error");
    int a[max];       // 错误：在语句后声明在 C 中不被允许
    /* ... */
}
```

C（C89）不允许在 for 语句的初始化部分、条件中，或块内的语句之后使用声明作为初始化。我们必须写成类似这样的形式：

```c
int i;
for (i = 0; i<max; ++i) x[i] = y[i];
struct S* p;
while (p = next(q)) {
    /* ... */
}
void f(int i)
{
    if (i<0 || max<=i) error("range error");
    {
        int a[max];
        /* ... */
    }
}
```

在 C++ 中，未初始化的声明是一个定义；在 C 中，它只是一个声明，因此可以有两个：

```c
int x;
int x;    /* 在 C 中定义或声明一个名为 x 的单个整数；在 C++ 中是错误 */
```

在 C++ 中，一个实体必须恰好被定义一次。如果两个 **int** 位于不同的翻译单元中，情况会变得更有趣一些：

```c
/* 在文件 x.c 中： */
int x;
/* 在文件 y.c 中： */
int x;
```

无论是 C 还是 C++ 编译器，在 **x.c** 或 **y.c** 中都不会发现任何错误。然而，如果 **x.c** 和 **y.c** 作为 C++ 编译，链接器会给出一个“重复定义”错误。如果 **x.c** 和 **y.c** 作为 C 编译，链接器接受该程序，并根据 C 规则（正确地）认为只有一个 **x**，它在 **x.c** 和 **y.c** 的代码之间共享。如果你希望在一个程序共享全局变量 **x**，请明确说明：

```c
/* 在文件 x.c 中： */
int x = 0;             /* 定义 */
/* 在文件 y.c 中： */
extern int x;         /* 声明，而非定义 */
```

更好的做法是使用头文件：

```c
/* 在文件 x.h 中： */
extern int x;        /* 声明，而非定义 */
/* 在文件 x.c 中： */
#include "x.h"
int x = 0;            /* 定义 */
/* 在文件 y.c 中： */
#include "x.h"
/* x 的声明在头文件中 */
```

更好的做法是避免使用全局变量。

#### 27.3.4 C 风格转换

在 C（以及 C++）中，你可以使用以下最小化表示法将值 `v` 显式转换为类型 `T`：

```c
(T)v
```

这种“C 风格转换”或“旧式转换”深受打字不熟练者和思维粗糙者的喜爱，因为它很简洁，你无需知道如何将 **v** 转换为 **T**。另一方面，这种转换风格被维护程序员正当地所恐惧，因为它几乎不可见，且没有留下关于作者意图的任何线索。C++ 转换（*命名转换* 或 *模板风格转换*；参见 §A.5.7）的引入旨在使显式类型转换易于识别（丑陋）且具体。在 C 中，你别无选择：

```c
int* p = (int*)7;     /* 重新解释位模式：reinterpret_cast<int*>(7) */
int x = (int)7.5;     /* 截断双精度浮点数：static_cast<int>(7.5) */
typedef struct S1 { /* . . . */ } S1;
typedef struct S2 { /* . . . */ } S2;
S2 a;
const S2 b;           /* 在 C 中允许未初始化的 const */
S1* p = (S1*)&a;     /* 重新解释位模式：reinterpret_cast<S1*>(&a) */
S2* q = (S2*)&b;     /* 去除 const：const_cast<S2*>(&b) */
S1* r = (S1*)&b;     /* 去除 const 并更改类型；可能是一个 bug */
```

即使在 C 中，我们也不建议推荐使用宏（§27.8），但像这样表达意图可能是一个好主意：

```cpp
#define REINTERPRET_CAST(T, v) ((T) (v))
#define CONST_CAST(T, v) ((T) (v))
S1* p = REINTERPRET_CAST(S1*, &a);
S2* q = CONST_CAST(S2*, &b);
```

这并没有提供由 **reinterpret_cast** 和 **const_cast** 进行的类型检查，但它确实使这些本质上丑陋的操作可见，并使程序员的意图明确。

#### 27.3.5 void* 的转换

在 C 中，**void\*** 可以作为赋值给或初始化任意指针类型变量的操作数的右操作数；在 C++ 中则不允许。例如：

```cpp
void* alloc(size_t x);            /* 分配 x 字节 */
void f(int n)
{
    int* p = alloc(n * sizeof(int));  /* 在 C 中合法；在 C++ 中是错误 */
    /* ... */
}
```

在这里，**alloc()** 的 **void\*** 结果被隐式转换为 **int\***。在 C++ 中，我们必须将该行重写为：

```cpp
int* p = (int*) alloc(n * sizeof(int));  /* 在 C 和 C++ 中都合法 */
```

我们使用了 C 风格转换（§27.3.4），以便在 C 和 C++ 中都合法。

为什么 **void\*-to-T\*** 的隐式转换在 C++ 中是非法的？因为这样的转换可能不安全：

```cpp
void f()
{
    char i = 0;
    char j = 0;
    char* p = &i;
    void* q = p;
    int* pp = q;       /* 不安全；在 C 中合法，在 C++ 中是错误 */
    *pp = -1;          /* 覆盖从 &i 开始的内存 */
}
```

在这里，我们甚至无法确定覆盖了哪些内存。也许是 **j** 和 **p** 的一部分？也许是用于管理 **f()** 调用的内存（f 的栈帧）？无论这里覆盖了什么数据，调用 **f()** 都是坏消息。

请注意，（相反的）从 **T\*** 到 **void\*** 的转换是完全安全的——你无法为这种情况构造像上面那样的糟糕示例——并且这些转换在 C 和 C++ 中都是允许的。

不幸的是，隐式的 **void\*** 到 **T\*** 转换在 C 中很常见，并且可能是实际代码中主要的 C/C++ 兼容性问题（参见 §27.4）。

#### 27.3.6 enum

在 C 中，你可以将一个 **int** 赋值给一个 **enum** 而无需转换。例如：

```c
enum color { red, blue, green };
int x = green;         /* 在 C 和 C++ 中都合法 */
enum color col = 7;    /* 在 C 中合法；在 C++ 中是错误 */
```

其中一个影响是，在 C 中我们可以对枚举类型的变量使用自增（**++**）和自减（**--**）。这很方便，但意味着存在危险：

```c
enum color x = blue;
++x;      /* x 变为 green；在 C++ 中是错误 */
++x;      /* x 变为 3；在 C++ 中是错误 */
```

“掉出”枚举值列表的末尾可能不是我们想要的结果。

请注意，与结构标签类似，枚举的名称位于它们自己的命名空间中，因此每次使用它们时都必须加上关键字 **enum**：

```c
color c2 = blue;      /* 在 C 中是错误：color 不在作用域内；在 C++ 中合法 */
enum color c3 = red;  /* 合法 */
```

#### 27.3.7 命名空间

C 中没有命名空间（C++ 意义下的命名空间）。那么当你想在大型 C 程序中避免名称冲突时该怎么办？通常，人们使用前缀或后缀。例如：

```c
/* 在 bs.h 中： */
typedef struct bs_string { /* ... */ } bs_string;  /* Bjarne 的字符串 */
typedef int bs_bool;                          /* Bjarne 的布尔类型 */
