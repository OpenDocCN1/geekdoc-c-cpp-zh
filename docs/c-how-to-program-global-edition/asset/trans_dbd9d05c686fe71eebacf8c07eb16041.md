
已定义。在 main 中，局部变量 x 被定义并初始化为 5（第 13 行）。该变量随后被打印，以显示全局 x 在 main 中被隐藏。接下来，在 main 中定义了一个新的块，其中另一个局部变量 x 初始化为 7（第 18 行）。该变量被打印，以显示它隐藏了 main 外层块中的 x。值为 7 的变量 x 在退出块时自动销毁，并且 main 外层块中的局部变量 x 再次被打印，以显示它不再被隐藏。

```c
// Fig. 5.16: fig05_16.c
// Scoping.
#include <stdio.h>

void useLocal(void); // function prototype
void useStaticLocal(void); // function prototype
void useGlobal(void); // function prototype

int x = 1; // global variable

int main(void)
{
    int x = 5; // local variable to main

    printf("local x in outer scope of main is %d\n", x);

    { // start new scope
        int x = 7; // local variable to new scope

        printf("local x in inner scope of main is %d\n", x);
    } // end new scope

    printf("local x in outer scope of main is %d\n", x);

    useLocal(); // useLocal has automatic local x
    useStaticLocal(); // useStaticLocal has static local x
    useGlobal(); // useGlobal uses global x
    useLocal(); // useLocal reinitializes automatic local x
    useStaticLocal(); // static local x retains its prior value
    useGlobal(); // global x also retains its value

    printf("\nlocal x in main is %d\n", x);
}

// useLocal reinitializes local variable x during each call
void useLocal(void)
{
    int x = 25; // initialized each time useLocal is called

    printf("\nlocal x in useLocal is %d after entering useLocal\n", x);
    x++;
    printf("local x in useLocal is %d before exiting useLocal\n", x);
}
```

```c
// useStaticLocal initializes static local variable x only the first time
// the function is called; value of x is saved between calls to this
// function
void useStaticLocal(void)
{
    // initialized once
    static int x = 50;

    printf("\nlocal static x is %d on entering useStaticLocal\n", x);
    x++;
    printf("local static x is %d on exiting useStaticLocal\n", x);
}

// function useGlobal modifies global variable x during each call
void useGlobal(void)
{
    printf("\nglobal x is %d on entering useGlobal\n", x);
    x *= 10;
    printf("global x is %d on exiting useGlobal\n", x);
}
```

main 外层作用域中的局部 x 为 5
main 内层作用域中的局部 x 为 7
main 外层作用域中的局部 x 为 5

进入 useLocal 后，useLocal 中的局部 x 为 25
退出 useLocal 前，useLocal 中的局部 x 为 26

进入 useStaticLocal 时，局部静态 x 为 50
退出 useStaticLocal 时，局部静态 x 为 51

进入 useGlobal 时，全局 x 为 1
退出 useGlobal 时，全局 x 为 10

进入 useLocal 后，useLocal 中的局部 x 为 25
退出 useLocal 前，useLocal 中的局部 x 为 26

进入 useStaticLocal 时，局部静态 x 为 51
退出 useStaticLocal 时，局部静态 x 为 52

进入 useGlobal 时，全局 x 为 10
退出 useGlobal 时，全局 x 为 100

main 中的局部 x 为 5

## 图 5.16 | 作用域。 (第 2 部分，共 2 部分。)

该程序定义了三个函数，每个函数都不接受参数也不返回任何值。函数 useLocal 定义了一个自动变量 x 并将其初始化为 25（第 38 行）。当调用 useLocal 时，该变量会被打印、递增，然后在函数结束前再次打印。每次调用此函数时，自动变量 x 都会重新初始化为 25。

函数 useStaticLocal 定义了一个静态变量 x 并在第 51 行将其初始化为 50（请回忆，静态变量的存储空间在程序开始执行前只分配并初始化一次）。声明为 static 的局部变量即使超出作用域也会保留其值。当调用 useStaticLocal 时，x 会被打印、递增，然后在退出函数前再次打印。在对该函数的下一次调用中，静态局部变量 x 将包含之前递增后的值 51。

函数 useGlobal 没有定义任何变量。因此，当它引用变量 x 时，使用的是全局 x（第 9 行）。当调用 useGlobal 时，全局变量会被打印、乘以 10，然后在退出函数前再次打印。下一次调用函数 useGlobal 时，全局变量仍然保持其被修改后的值 10。最后，程序再次打印 main 中的局部变量 x（第 32 行），以显示没有任何函数调用修改了 x 的值，因为这些函数都引用了其他作用域中的变量。

## 5.14 递归

对于某些类型的问题，让函数调用自身是有用的。递归函数是指直接或通过另一个函数间接调用自身的函数。递归是一个复杂的话题，在高年级计算机科学课程中会详细讨论。在本节和下一节中，我们将介绍递归的简单示例。本书对递归进行了广泛的论述，分布在第 5–8 章、第 12 章以及附录 D 和 E 中。第 5.16 节中的图 5.21 总结了本书的递归示例和练习。

我们首先从概念上考虑递归，然后检查包含递归函数的几个程序。递归问题求解方法有许多共同的元素。递归函数被调用来解决一个问题。该函数实际上只知道如何解决最简单的情况，即所谓的基例。如果函数被基例调用，函数只需返回一个结果。如果函数被更复杂的问题调用，函数通常会将问题分为两个概念部分：函数知道如何处理的部分和函数不知道如何处理的部分。为了使递归可行，后一部分必须类似于原始问题，但是一个稍微简单或更小的版本。因为这个新问题看起来像原始问题，函数会启动（调用）一个全新的副本来处理较小的问题——这被称为递归调用或递归步骤。递归步骤还包括一个 return 语句，因为其结果将与函数已知如何解决的问题部分结合，形成一个结果并传回原始调用者。

递归步骤在原始函数调用暂停等待递归步骤的结果时执行。递归步骤可能导致更多这样的递归调用，因为函数不断将每次调用的问题分为两个概念部分。为了使递归终止，每次函数用原始问题的稍微简单版本调用自身时，这一序列的较小问题必须最终收敛到基例。当函数识别出基例时，它会向之前的函数副本返回结果，随后一系列返回会一直进行，直到原始函数调用最终向其调用者返回最终结果。作为这些概念应用的示例，让我们编写一个递归程序来执行一种流行的数学计算。

### 递归计算阶乘

非负整数 n 的阶乘，写作 n!（读作“n 阶乘”），是乘积

n · (n - 1) · (n - 2) · ... · 1

其中 1! 等于 1，且 0! 定义为 1。例如，5! 是乘积 5 * 4 * 3 * 2 * 1，等于 120。

整数 number 的阶乘，大于或等于 0，可以使用 for 语句迭代（非递归）计算如下：

```
factorial = 1;
for (counter = number; counter >= 1; --counter)
    factorial *= counter;
```

通过观察以下关系可以得到阶乘函数的递归定义：

n! = n · (n − 1)!

例如，5! 显然等于 5 * 4!，如下所示：

5! = 5 · 4 · 3 · 2 · 1
5! = 5 · (4 · 3 · 2 · 1)
5! = 5 · (4!)

计算 5! 的过程如 图 5.17 所示。图 5.17(a) 显示了递归调用的连续过程，直到 1! 被计算为 1（即基例），从而终止递归。图 5.17(b) 显示了从每次递归调用返回给其调用者的值，直到最终值被计算并返回。

![](img/bf54db922e6fa8319cba11069e785521_214_0.png)

图 5.17 | 5! 的递归求值

图 5.18 使用递归计算并打印整数 0–21 的阶乘（类型 unsigned long long int 的选择稍后会解释）。
