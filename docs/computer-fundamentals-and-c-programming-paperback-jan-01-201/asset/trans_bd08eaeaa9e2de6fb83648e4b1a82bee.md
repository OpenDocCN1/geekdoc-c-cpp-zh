

```c
printf("Contents of table[0][0] = %3d\n", **table);
printf("Contents of table[1][0] = %3d\n", **(table + 1));
printf("Contents of table[2][0] = %3d\n", **(table + 2));

printf("\nPrinting entire array ...\n");
for (i = 0; i < ROWS ; putchar('\n'), i++ )
    for (j = 0 ; j < COLUMNS ; j++)
        printf("%3d ", *(*(table + i) + j));

printf("\nBut table is actually a one-dimensional array ...\n");
for (i = 0; i < ROWS * COLUMNS ; i++ )
    printf("%3d ", *(p + i));
return 0;
}
```

程序 12.14：`pointers_in_2darray.c`

```text
Size of table = 60                                      Size of entire array
Size of table[0] = 20                                   Size of 5 elements
Size of table[0][0] = 4                                 Size of 1 element

Key in 15 integers: 1 3 5 7 9 11 33 55 77 99 111 333 555 777 999
Contents of table[0][0] =   1
Contents of table[1][0] =  11
Contents of table[2][0] = 111

Printing entire array ...
  1   3   5   7   9
 11  33  55  77  99
111 333 555 777 999

But table is actually a one-dimensional array ...
  1   3   5   7   9  11  33  55  77  99 111 333 555 777 999
```

程序输出：`pointers_in_2darray.c`

### 12.17 通用指针或 void 指针

如果你认为三种数据类型的变量需要三种类型的指针来指向它们，那么你可能还不知道*通用指针*。这种特殊的指针可以指向任何类型的变量。通用指针使用关键字 `void` 声明，类型为 `void *`。请看下面名为 `void_p` 的通用指针变量的声明：

```c
void *void_p;
```

尽管 `void_p` 没有特定的数据类型，但它可以指向一个 `int` 变量 `x`：

```c
int x = 5;
void_p = &x;
```

现在 `void_p` 知道 `x` 所表示的数据存放在哪里，但它还不知道如何解释这些数据。因此我们不能解引用 `void_p` 来获取 `x` 的值。要获得数据的类型信息，我们需要在解引用之前将这个指针强制转换为指向 `int` 的指针，即在使用 `*` 获取 `x` 的值之前进行类型转换：

```c
printf("x = %d\n", *(int *) void_p);
```

_打印 x = 5_

与任何其他解引用的指针表达式一样，这个表达式 `*(int *) void_p` 也可以用在赋值表达式的左侧，以更新所指向的变量：

```c
*(int *) void_p = 100;
```

_将 x 改为 100_

我们还可以将 `void_p` 从 `x` 上“脱钩”，让它指向另一种数据类型的变量。程序 12.15 使用一个通用指针依次指向 `short`、`int` 和 `long` 三种类型的变量。该程序还用同一个通用指针更新它所指向的变量。

通用指针可以与任何指针进行比较而无需进行强制类型转换（如 **`void_p == p`**），也可以被赋值为 `NULL`。这种指针类型在设计需要处理多种参数数据类型的函数时非常有用。动态分配内存的函数 **malloc** 和 **calloc** 返回一个指向所分配内存的通用指针。我们将在第 16 章再次遇到 void 指针。

```c
/* void_pointer.c: Uses a void pointer to access variables of 3 types.
                    Also uses the same pointer to update a variable. */
#include <stdio.h>

int main(void)
{
    short short_x = 10; int int_x = 200; long long_x = 4000L;
    void *void_x;                    /* A pointer of type void */

    void_x = &short_x;
    printf("Value of short_x = %hd\n", *(short *) void_x);

    void_x = &int_x;
    printf("Value of int_x = %d\n", *(int *) void_x);

    void_x = &long_x;
    printf("Value of long_x = %ld\n", *(long *) void_x);
    *(long *) void_x = 8000L;        /* Updates long_x */
    printf("New value of long_x = %ld\n", long_x);
    return 0;
}
```

程序 12.15：**void_pointer.c**

```text
Value of short_x = 10
Value of int_x = 200
Value of long_x = 4000
New value of long_x = 8000
```

程序输出：**void_pointer.c**

> **要点：** 通用指针或 void 指针可以指向任何类型的变量，但在被转换为常规指针类型之前不能被解引用。使用通用指针更新所指向的变量时，也需要进行强制类型转换。

### 12.18 将 `const` 限定符用于指针

我们已经在普通变量上使用 `const` 限定符来防止其值被无意修改。同样的限定符也可以用于指针变量，但有所不同。因为指针关联着两个值——它存储的地址值以及它指向的值，你可能希望阻止对以下内容的修改：

-   所指向的值。
-   指针变量中存储的值。
-   两者都不可修改。

对于普通变量，`const` 是声明中的第一个词（如 `const int x;`）。当同样的技术应用于指针时，所指向的值（`x`）受到保护，不能被修改：

```c
const int *p = &x;                         p 可以改变，但 x 不能
```

然而，通过改变 `const` 的位置，你可以保护指针本身的值：

```c
int * const p = &x;                         x 可以改变，但 p 不能
```

你也可以将两种用法结合起来，同时保护指针和所指向的值。这需要两次使用 `const`：

```c
const int * const p = &x;                   p 和 x 都不能改变
```

程序 12.16 使用三个指针 `p`、`q` 和 `r` 测试了这三种情况，尝试改变一个本应保持常量的变量。GCC 编译器输出的错误消息证实了上述论断。你应该不难找出程序中出错的行，因为诊断输出中标注的四个行号也正是包含注释的行。

`const` 限定符经常出现在标准库许多字符串处理函数的原型中，例如复制字符串的 `strcpy` 函数：

```c
char *strcpy(char *dest, const char *src);
```

因为要复制的源字符串不会改变，所以对源字符串使用 `const` 限定符是合理的。在设计以指针作为参数的函数时，请确保对函数不允许修改的参数使用 `const`。

```c
/* const_in_pointers.c: Three ways of using const in pointer declaration. */
int main(void)
{
    int x, y, z;
    const int *p = &x;
    *p = 10;                         /* Can't change value pointed to */
    int * const q = &x;
    q = &y;                          /* Can't change value of pointer */

    const int * const r = &z;
    r = &y;                          /* Can't change either value of pointer ... */
    *r = 30;                         /* ... or value pointed to */
    return 0;
}
```

程序 12.16：**const_in_pointers.c**

```text
const_in_pointers.c: In function main:
const_in_pointers.c:7: error: assignment of read-only location
const_in_pointers.c:10: error: assignment of read-only variable q
const_in_pointers.c:13: error: assignment of read-only variable r
const_in_pointers.c:14: error: assignment of read-only location
```

程序输出：**const_in_pointers.c**

指针是非常强大的对象，这也是 C 语言在诞生 40 年后依然广受欢迎的主要原因。我们已经尽力将这些概念讲清楚，但还没有完全结束。我们还需要将这些概念应用到字符串、结构体、磁盘文件的输入/输出操作中。最后，我们还需要了解如何处理指向函数的指针。

## 接下来是什么？

本章我们避免了对字符串的讨论，尽管字符串本身就是一个指针。字符串的世界广阔而独特，值得单独探讨。标准库中所有字符串处理函数都使用指针作为参数，其中一些函数还返回指针。

## 你学到了什么？

指针是一种派生数据类型，包含一个内存地址。指针可以访问任何合法的内存位置，并检索或更改该位置的内容。

通过在一元运算符 `&`（取地址运算符）后加变量名来获得指针。一元运算符 `*`（间接寻址运算符）对指针解引用，以获得所指向地址处的值。

指针具有固定的大小，其类型与所指向对象的数据类型直接相关。

