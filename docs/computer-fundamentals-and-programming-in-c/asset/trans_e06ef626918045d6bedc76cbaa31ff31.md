

```c
int main()
{ /* main() program body starts here...*/
  int a, b;       /* local variables */
  a = 5;
  b = 7;
  printf(" In main: a = %d, b = %d\n", a, b);
  exchange(a, b);
  printf("\n Back in main:");
  printf("a = %d, b = %d\n", a, b);
  return 0;
} /* main() program body ends here... */
void exchange(int a, int b)
{ /* function body starts here...*/
  int temp; /* local variable */
  printf("\n In function exchange() before change:
         just received from main... a=%d and
         b=%d",a,b);
  temp = a;
  a = b;
  b = temp; /* interchange over */
  printf("\n In function exchange() after change:");
  printf("a = %d, b = %d\n", a, b);
} /* function body ends here...*/
```

```text
Output
In main: a = 5, b = 7
In function exchange() before change: just received
from main... a=5 and b=7
In function exchange() after change: a = 7, b = 5
Back in main: a = 5, b = 7
```

结果表明，上述程序代码未能在 main() 函数中的变量之间交换数值。这是因为，首先，main() 中的变量 a 和 b 与 exchange() 函数中的 a 和 b 并不相同。exchange() 中的 a 和 b 是局部变量，在函数被调用时创建。这意味着程序控制权由该函数接管，当程序控制权返回 main() 程序时，这些变量立即被销毁。当从 main() 调用 exchange() 函数时，main() 中局部变量 a 和 b 所持有的值的副本被传递给 exchange() 函数中各自的局部变量 a 和 b。在这个 exchange() 函数内部，其局部变量 a 和 b 之间的数值交换任务成功完成，这一点从程序运行时显示的消息中可以明显看出。但这丝毫不会影响 main() 中变量 a 和 b 的值。此外，交换后的变量值副本也没有从 exchange() 函数传回给 main() 中的变量。因此，main() 内变量 a 和 b 的值保持不变、未受影响。这说明了 main() 和 exchange() 函数中局部变量作用域的区别。实现交换的一种方法是，将要交换的变量（即 a 和 b）声明为全局变量。下面的示例程序代码演示了这一点。

### 示例

17.

```c
#include <stdio.h>
void exchange(void);
int a, b;   /* declaration of global variables */
int main()
{ /* main program starts here...*/
  a = 5;
  b = 7;
  printf(" In main: a = %d, b = %d\n", a, b);
  exchange(); /* function call, no parameters are
                 passed */
  printf("\n Back in main:");
  printf("a = %d, b = %d\n", a, b);
  return 0;
} /* main program ends here */
void exchange(void)
{ /* function body starts here...*/
  int temp; /* decl. of local variable in function */
  printf("\n In function exchange() before change:
         just received from\n
         main... a=%d and b=%d",a,b);
  temp = a;
  a = b;
  b = temp; /* interchange over */
  printf("\n In function exchange() after change:");
  printf("a = %d, b = %d\n", a, b);
} /* function body ends here*/
```

```text
Output
In main: a = 5, b = 7
In function exchange() before change: just received
from main... a=5 and b=7
In function exchange() after change: a = 7, b = 5
Back in main: a = 7, b = 5
```

该示例表明，对于全局变量，遵循作用域规则即可实现交换。通过在函数中使用指针，可以更高效地完成同样的工作，这种函数调用技术称为按引用调用，更严格地说是按地址调用。这将在第 13 章中讨论。

-   可以将所有变量设为全局变量，而不是将它们作为参数传递给函数。但这样做并不被推荐，因为全局变量会破坏函数提供的正常保护机制。通过使用参数传递机制并根据需要声明局部变量，C 语言提供了使函数相互独立、彼此隔离的机制，包括需要仔细指定函数所需的参数类型、函数中使用的变量以及返回值。在包含许多用户自定义函数的大型程序中，仅使用全局变量尤其具有灾难性。由于全局变量可以被全局声明之后的任何函数访问和修改，因此要查找错误值的来源将是一项耗时且令人沮丧的任务。
-   但这并不意味着使用全局变量总是有害的。在某些情况下，使用全局变量是被提倡的。然而，全局变量在创建必须由多个函数共享的数据数组和常量时极其有用。如果许多函数需要访问一组数组，全局变量允许这些函数高效地修改同一个数组，而无需传递多个数组。

## 12.7.2 作用域规则

程序中标识符声明可被访问的区域称为该标识符的作用域。作用域涉及程序中声明的变量的可访问性、存在周期和使用边界。作用域有四种类型。

-   块
-   文件
-   函数
-   函数原型

以下各节描述与变量相关的作用域。

### 块作用域

这意味着标识符只能在其声明的块中使用。这些变量在块内声明的位置被创建，并在块外不复存在。在块外，这些变量是未知且不存在的。对于块中嵌套块（称为嵌套块），只要这些变量未在内部块中重新声明，在内部块外部声明的变量就可被嵌套块访问。在内部块中重新声明与外部块中同名的变量，会在执行内部块时屏蔽外部块变量。

一般来说，对于外部块和内部块不共用的变量，最好使用不同的名称，以避免无根据的错误。以下是一些说明块中作用域规则的示例。

### 示例

-   18. 编写一个程序，演示块中的作用域规则

```c
#include <stdio.h>
int main()
{
    int x= 3;    /* variable declaration in outer
                    block */
    printf("\n in outer block x = %d before executing
            inner block", x);
    {
        int x= 45; /* variable declaration in inner
                      block */
        printf("\n in inner block x = %d", x);
    }
    printf("\n in outer block x = %d after executing
            inner block", x);
    return 0;
}
```

```text
Output
in outer block x = 3 before executing inner block
in inner block x = 45
in outer block x = 3 after executing inner block
```

该程序表明，由于变量 x 在内部块中被重新声明为 45，因此在内部块中创建了一个局部变量。该变量只能被内部块访问和知晓。

函数被视为命名块。在函数块内声明的变量可以在其定义所在的函数内的任何位置使用。在外部块中声明的变量 x 具有块作用域。与块类似，函数可以并行定义，即一个接一个地放置，并且任何函数都可以从其他函数调用。但 C 语言不允许函数嵌套，即不能在一个函数定义内部定义另一个函数。

### 函数作用域

这仅适用于标签。通常标签与 goto 语句一起使用。这仅表示标签可以在其定义所在的函数内的任何位置使用。这包括在定义之前使用。

### 文件作用域

这意味着在标识符声明之后，可以在当前文件中的任何位置使用该标识符。这适用于函数以及所有在函数外部声明的变量。文件作用域变量也称为全局变量。涉及全局或文件作用域变量的说明已在 12.7.1 节中讨论过。文件作用域标识符可能被具有相同名称的块作用域声明所隐藏。

