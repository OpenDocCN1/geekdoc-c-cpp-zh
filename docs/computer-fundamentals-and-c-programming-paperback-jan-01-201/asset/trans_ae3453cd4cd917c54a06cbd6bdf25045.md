

指针的强大之处在于前面的语句。赋值 `*p = 10` 与 `x = 10` 相同。因此，指针提供了对两个值的访问——它存储的地址以及该地址处存储的值。该指针的类型不是 `int`，而是*指向 int 的指针*，我们也称之为 `int *`。

尽管指针具有整数值，但它只支持一种受限的算术形式。当所指变量类型为 `char` 时，对值为 100 的指针值加 1 得到 101；当所指变量类型为 `int` 时，得到 104。利用指针算术，我们可以在内存中导航，并更新任何合法内存位置的内容。你可以修改指针中存储的值，也可以修改指针所指的值：

| 表达式 | 效果 |
|---|---|
| `p++` | *指针的值加 1* |
| `(*p)++` | *所指的值加 1* |

与数组一样，指针属于派生数据类型。由于每个变量都有地址，我们可以为每种数据类型定义指针，包括数组和结构体。此外，C 语言中没有任何机制阻止我们创建指向另一个指针的指针。

尽管指针通常是一个变量，但任何计算结果为内存地址的表达式都可以在需要指针值的地方使用。在大多数情况下，数组和字符串也可以被视为指针。数组名的计算结果为第一个元素的地址，而双引号字符串的计算结果为该字符串第一个字符的地址。

> **注意：** 指针具有与其解引用值的数据类型相对应的数据类型。如果指针 `p` 指向一个 `int` 类型的变量，那么 `p` 的类型就是 `int *`，即指向 int 的指针。将 `*p` 视为具有 `int` 类型的值也会很有帮助。

> **要点：** 指针值可以来自三个来源：(i) 任何带有 `&` 运算符前缀的变量名，(ii) 数组名，以及 (iii) 用双引号括起来的字符串。

### 12.3 `intro2pointers.c`：指针的简单演示

程序 12.1 验证了目前为止关于指针所做的最基本论断。指针 `p`（类型为 `int *`）的未初始化值首先使用 `%p` 格式说明符以十六进制打印。然后使其指向一个 `int` 变量 `x`。注意，`*p` 和 `x` 的值都为 420。但是当 `*p` 被赋值为 840 时，`x` 的值也变为 840。这表明指针可以用来修改其所指的值。

### 程序 12.1：`intro2pointers.c`

```c
/* intro2pointers.c: A simple example of a pointer in action. */
#include <stdio.h>
int main(void)
{
    int x = 420;
    int *p;                         /* p has type int * */

    printf("Value of x = %d\n", x);
    printf("Uninitialized value of pointer p = %p\n", p);
    p = &x;                         /* p stores address of x */
    printf("Initialized value of pointer p = %p\n", p);
    printf("Value at address pointed to by p = %d\n", *p);
    printf("This is the same value as x: %d\n", x);

    *p = 840;                       /* Same as x = 840; */
    printf("New value of x = %d\n", x);
    return 0;
}
```

### 程序输出：`intro2pointers.c`

```
Value of x = 420
Uninitialized value of pointer p = 0xb7f1df60    %p prints in hex
Initialized value of pointer p = 0xbf1b163c     Address of x
Value at address pointed to by p = 420
This is the same value as x: 420
New value of x = 840
```

### 12.4 声明、初始化与解引用指针

指针变量在使用前必须先声明（并自动定义）。声明指定了类型，并为指针分配了必要的内存。下面的语句声明了一个名为 `p` 的指针变量，它可以存储一个 `int` 变量的地址：

```c
int *p;
```

*现在还不能解引用 `*p`*

按照惯例，`*` 放在变量前面，但你可以把它放在 `int` 和 `p` 之间的任何位置（例如，`int * p` 或 `int* p`）。指针 `p` 现在包含一个不可预测的值，只有在它被指向一个合法的内存位置之后才能使用。这个位置可以是某个 int 变量（例如 x）的地址，使用 & 运算符即可获得：

```c
int x = 5;
p = &x;    /* p stores the address of x */
```

& 运算符将其操作数（x）求值为一个地址。我们当然可以将声明和赋值组合起来，如下所示：

```c
int *p = &x;    /* int* p = &x; is also OK */
```

p 的数据类型是 `int *`，即指向 int 的指针，这仅表示其所指的值具有 int 类型。类似地，`float` 变量由 `float *`（指向 float 的指针）类型的指针指向。然而，指针本身的大小与所指变量的大小无关。指针有固定大小，其值使用 printf 的 `%p` 格式说明符打印。

在使用 `p = &x;` 给指针分配了有效地址后，我们可以利用间接引用（indirection）的概念从 p 获得 x 的值。表达式 `*p` 的值等于 x：

```c
printf("Value of x is %d\n", *p);    /* Prints the value 5 */
```

用作解引用或间接引用的一元运算符 `*`，按以下顺序运行：

- 它计算其操作数（`p`），以获得存储的地址（`&x`）。
- 然后取出该地址处存储的值（`x`）。

因此，`*p` 与 x 同义，可以在任何使用 x 的地方使用。因此，以下面的方式使用 `*p` 会改变 x：

```c
*p = 10;
```

*等同于 `x = 10;`*

只要 p 指向 x，对 x 所做的任何更改都能通过 p 体现出来，反之亦然。*这是指针最重要的特性。* 因此，p 有两个值——一个直接值（&x）和一个间接值（*p）。p 的解引用值也可以赋给变量或用于算术表达式：

```c
int y;
y = *p;
y = *p + 1;
```

*y 也等于 10*

*等同于 `y = x + 1;`*

正如 x 在左侧是变量、在右侧是值一样，`*p` 也是如此。指针与其所指变量之间的关系如图 12.1 所示。

![](img/d75612dcf3ab36327142238ab5bb21d8_402_0.png)

**图 12.1** 指针与所指变量

> **注意：** C 语言需要的运算符比计算机键盘能提供的更多，因此有时同一个符号不得不承担多种角色。用于乘法的运算符 `*`，也用于声明指针（`int *p;`）和解引用指针（`int y = *p;`）。

> **注意：** 语句 `int *p;` 可以有两种解释：
>
> - (i) `p` 的类型是 `int *`（指向 int 的指针）。
> - (ii) `*p` 的类型是 `int`。

这种灵活性解释了 `*` 的两种用法。由于 (i)，许多程序员更喜欢将声明写成 `int * p;` 而不是 `int *p;`。

### 12.5 `pointers.c`：使用两个指针

程序 12.2 使用了两个类型为指向 short 的指针（`short *`）的指针 p 和 q，以及两个 short 变量 x 和 y。第一部分中，p 和 q 都指向 x，展示了解引用 p 和 q 对 x 值的影响。第二部分演示了当 p 被改为指向 y 时对 `*q` 的影响。

### 程序 12.2：`pointers.c`

```c
/* pointers.c: Uses two pointers to point to same and different variables. */
#include <stdio.h>
int main(void)
{
    short x = 100, y = 300;
    short *p = &x;
    short *q = p;              /* Both p and q point to x */
    printf("When x = 100, *p = %hd, *q = %hd\n", *p, *q);
    *p = 150;                  /* Same as x = 150; */
    printf("When *p = 150, *q = %hd, x = %hd\n", *q, x);
    *q = 200;                  /* Same as x = 200; */
    printf("When *q = 200, *p = %hd, x = %hd\n", *p, x);
    p = &y;                    /* q now points to y */
    printf("\np now points to y, *p = %hd, y = %hd\n", *p, y);
    printf("But *q is still %hd\n\n", *q);
    return 0;
}
```

### 程序输出：`pointers.c`

```
When x = 100, *p = 100, *q = 100
When *p = 150, *q = 150, x = 150
When *q = 200, *p = 200, x = 200
p now points to y, *p = 300, y = 300
But *q is still 200
```

在声明时，x 的地址直接赋给了 p，并间接赋给了 q。前三个 `printf` 语句展示了修改 `*p` 或 `*q` 如何也会改变 x，这意味着 `*p`、`*q` 和 x 在所有方面都是等价的。在第二部分中，通过使 p 指向 y，打破了 p 与 x 之间的连接。q 现在不再是 p 的副本，因为它继续指向 x。

你现在可以理解为什么指针需要具有数据类型。没有它，你固然可以访问其中包含的地址，但无法解引用该指针。p 和 q 声明中的 `short *` 类型表明，必须从每个指针存储的地址处取出两个字节，并将这些字节解释为 short 类型的值。

![](img/d75612dcf3ab36327142238ab5bb21d8_403_0.png)

> **要点：** 赋值 `p = &x` 在两个变量之间建立了一种互惠关系。可以通过修改 `*p` 来改变 x，反之亦然。这种关系在赋值 `x = y` 中是不存在的；该赋值涉及两个普通变量。在这里，*之后*改变其中一个变量并不会改变另一个变量。

