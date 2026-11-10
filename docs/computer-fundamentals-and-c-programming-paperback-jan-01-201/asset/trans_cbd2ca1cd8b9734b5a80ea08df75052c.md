

## 12.6 指针的重要属性

由于间接寻址的强大能力，指针在解决复杂问题方面非常有效。因此，除了最简单的应用之外，它们几乎无处不在。诚然，初学者需要一些时间才能适应这些简单却棘手的概念。然而，遵循以下特性和准则将对你大有裨益：

- *指针的数据类型不同于它所指向变量的类型。* 如果后者是 char 类型，那么正确定义的指针类型是 char *，即指向 char 的指针。此外，变量或常量的数据类型可以使用强制类型转换转换为指针的数据类型。例如，表达式 `(int *) 32657` 将一个 int 转换为指向 int 的指针。

- *指针的大小通常是固定的，并不取决于它所指向对象的大小。* 指针作为地址，表示一个整数值，其宽度足以寻址机器上的每个内存字节。尽管存在例外，但指针的大小与原生字长相同，而原生字长通常与 int 的大小相同。但指针本身并不是 int。

- *可以将值 0 赋给指针。* 地址 0 也由符号常量 NULL 表示，具有该值的指针称为*空指针*。C 保证地址 NULL 永远不会指向程序所使用的对象。

- *不得解引用未初始化或空指针。* 未初始化的指针包含一个垃圾值，它可能指向程序无法访问的内存位置。如果解引用这样的指针，程序可能会行为不可预测或异常终止。

- *对指针变量加 1 并不一定使指针所存储的值加 1。* 结果取决于指针的数据类型。如果一个指针存储地址 1000，那么对其加 1 后，对于 char * 类型的指针结果为 1001，对于 int * 为 1004，对于 float * 为 1008。这种加法属于指针算术的范畴，而指针算术构成了指针与数组之间关系的基础。

- *指针可以断开当前链接并指向另一个变量。* 前面的程序（程序 12.2）已经证明了这一点。例如，如果指针 p 指向变量 x，并且你已经用完 x，那么你可以使用同一个指针指向另一个变量 y（图 12.2）。

  ![](img/d75612dcf3ab36327142238ab5bb21d8_404_0.png)

- *如果两个指针变量类型相同，则可以将一个指针变量赋给另一个指针变量。* 在下面的示例中，p 和 q 都指向 x：

  ```c
  int x = 10;
  int *p = &x;
  int *q = p;
  ```

  前面的程序（程序 12.2）也已经证明了这一点。解引用 p 和 q 会得到相同的值 x（图 12.3）。你也可以通过修改 *p 或 *q 来改变 x 的值。当指针作为参数传递给函数时，发生的正是这种情况。

  ![](img/d75612dcf3ab36327142238ab5bb21d8_405_0.png)

  **图 12.3** 指向同一变量的两个指针

- *指针可以指向另一个指针。* 多维数组或字符串指针数组会隐式利用这一特性。被指向的指针又可以指向另一个指针，依此类推。

程序 12.3 演示了指针的三个特性。它使用了 char、short 和 int 类型的三个普通变量，以及三个匹配的指针变量。程序最终会崩溃，并且不会执行最后的 printf 语句。

- (A) 这里使用 `sizeof` 将指针的大小与其所指向变量的大小进行比较。注意，指针的数据类型并不决定其自身的大小（在此 Linux 系统上为 4 字节），尽管它决定了解引用对象（`*p_char`、`*p_short` 和 `*p_int`）的大小。

- (B) 当对三个指针变量分别加 1 时，结果值增加的不是 1，*而是该数据类型的一个单位*。只有 `p_char` 的值前进 1；`p_short` 和 `p_int` 的值分别增加 2 和 4。指针算术将在 12.9 节中讨论。

```c
/* pointer_attributes.c: Highlights (i) difference between size of pointer and
                 its dereferenced object, (ii) effect of adding 1 to a pointer,
                 (iii) effect of dereferencing a null pointer. */
#include <stdio.h>

int main(void)
{
    int i = 97;        char c = 'A';       short s = 97;
    int *p_int = &i;   char *p_char = &c;  short *p_short = &s;

    /* (A) Size of pointer compared to size of dereferenced object */
    printf("Size of: p_char = %d, *p_char = %d\n",
           sizeof p_char, sizeof *p_char);
    printf("Size of: p_short = %d, *p_short = %d\n",
           sizeof p_short, sizeof *p_short);
    printf("Size of: p_int = %d, *p_int = %d\n",
           sizeof p_int, sizeof *p_int);

    /* (B) Adding 1 to a pointer */
    printf("p_char = %p,  p_char + 1 = %p\n",  p_char, p_char + 1);
    printf("p_short = %p, p_short + 1 = %p\n", p_short, p_short + 1);
    printf("p_int = %p,   p_int + 1 = %p\n",   p_int, p_int + 1);

    /* (C) Dereferencing a null pointer - Program will crash here!!!!!!! */
    p_short = NULL;                 /* Pointer snaps current link */
    printf("Dereferenced value of a null pointer = %d\n", *p_short);
    return 0;
}
```

程序 12.3：**pointer_attributes.c**

```
Size of: p_char = 4, *p_char = 1
Size of: p_short = 4, *p_short = 2
Size of: p_int = 4, *p_int = 4
p_char = 0xbfc22833,  p_char + 1 = 0xbfc22834       Increases by 1
p_short = 0xbfc22830, p_short + 1 = 0xbfc22832    Increases by 2
p_int = 0xbfc22834,   p_int + 1 = 0xbfc22838      Increases by 4
Segmentation fault                                      Linux
pointer_attributes.exe has encountered a problem and needs to close.  Visual Studio
```

程序输出：**pointer_attributes.c**

(C) 指针变量 p_short 与变量 s 断开连接，并被赋值为 NULL。当解引用该指针时，程序提前终止，并且没有执行最后的 **printf** 语句。GCC（Linux）和 Visual Studio 输出不同的消息（两者都显示在输出中），但含义很明确：不能解引用空指针。

> **注意：** 解引用一个不指向对象或可访问内存位置的指针是一个常见错误。例如，下面的代码序列可能不会更新 p 中存储的地址处的内容，反而可能导致程序崩溃：

```c
int *p, x;
*p = 1;                                  /* Should have done p = &x; first */
```

未初始化的指针指向“内存中的某个位置”，这可能是非法的内存位置。在解引用指针之前，请为该指针分配一个对象的地址。

## 12.7 指针与函数

前面的程序演示了指针的基本特性，并强调了安全使用指针的重要性。但它们由人为构造的场景组成，实际上完全没有为使用指针提供理由。只有当你使用函数时，才会意识到 C 需要指针，原因如下：

- 函数按值传递参数。因为参数的*值*被复制到函数形参中，所以这些副本不能用于更改原始值。

- 函数使用 **return** 语句返回单个值。它不能使用这种机制返回多个值。

我们可以通过将指针用作函数参数来克服这两个障碍。让我们先克服第一个障碍。程序 12.4 将变量 *x* 的地址传递给 **change_x** 函数，该函数使用这个地址将 *x* 的现有值加倍。该函数被调用两次，以两种不同方式返回 *x* 更改后的值。观察 **change_x** 函数的声明；它使用一个指向 `short` 的指针作为参数。

```c
/* change_x.c: Uses a pointer as an argument to a function
              to change a variable defined in main. */
#include <stdio.h>
short change_x(short *fx);
int main(void)
{
    short x = 100;
    short *px = &x;

    change_x(px);                      /* Return value ... */
    printf("New value of x: %hd, %hd\n", *px, x);   /* ... not saved here ... */
    printf("New value of x: %hd\n", change_x(px));  /* ... but captured here */
    return 0;
}
short change_x(short *fx)
{
    *fx *= 2;
    return *fx;
}
```

**程序 12.4：** change_x.c

