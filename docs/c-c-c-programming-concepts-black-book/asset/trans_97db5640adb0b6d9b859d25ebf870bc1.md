
清单 2.29 展示了 C 语言中的外部链接：

### 清单 2.29：C 语言中的外部链接

```c
#include<stdio.h>

int main()
{
    extern int varA;
    printf("\n The value of the variable is [%d] ",varA);
    getch();
    return 0;
}

int varA = 10;
```

清单 2.29 的输出如下：

```text
The value of the variable is [10]
```

该程序的输出为 10，因为全局变量“varA”被赋值为 10。注意，此程序中使用 extern 关键字，是因为 varA 变量在 main 函数中的声明之前被访问。如果编译器在当前作用域内发现未声明的变量，它会检查封闭块内所有变量是否匹配。之后，编译器会尝试与全局变量匹配。extern 允许我们声明一个变量而不定义它。如果我们为同一变量提供初始化，那么 extern 声明就变成了该变量的定义。

extern 存储类说明符的另一个重要用途是在多文件编程中。程序可能会跨越两个单独的文件，这些文件分别编译但链接在一起。在这种情况下，让编译器知道全局变量存在的唯一方法是使用 extern 关键字。假设我们有两个文件 File_1 和 File_2。一个变量已在 File_1 中声明为全局变量，并在其中被修改。如果我们想在 File_2 中使用同一个变量，并且也使用相同的值，那么我们需要在 File_2 中将该变量声明为 extern 变量并使用它。extern 关键字会通知编译器，跟随在 extern 关键字后面的变量名已在程序的其他位置声明，因此它将采用 File_1 中声明的那个变量。

为了理解全局变量从一个文件到另一个文件的流转，我们需要在 C 中创建一个多文件项目，该项目将包含多个源文件和一个公共头文件。头文件包含全局变量和一个公共显示函数，该函数用于打印全局变量。在我们的示例中，头文件定义在清单 2.30 中：

### 清单 2.30：C 语言中的多文件编程

```c
/* test.h */

/* Header file that contains the global variable */

int global_var = 10;

void display_file1();

void display()
{
    printf("\n global variable [%d]",global_var);
    return;
}
```

以下源文件（源文件 1 和源文件 2）包含在项目中：

```c
/* Source file 1 */

#include<stdio.h>

extern int global_var;

void display_file1()
{
    global_var++;
    display();
    return;
}
/* Source file 2 */

#include<stdio.h>

extern int global_var;

void display_file2()
{
    global_var++;
    display();
    return;
}
```

以下主模块也包含在内：

```c
/* The main module */

#include <stdio.h>
#include <stdlib.h>
#include "test.h"

int main(int argc, char *argv[])
{
    display();
    display_file1();
    display_file2();
    getch();
    return 0;
}
```

两个源文件都使用全局变量“global_var”，并在显示该变量之前将其递增 1。在主模块内部，我们调用两个不同的函数“display_file1()”和“display_file2()”，它们分别定义在源文件 1 和源文件 2 中。

清单 2.30 的输出如下：

```text
global variable [10]
global variable [11]
global variable [12]
```

在清单 2.30 中，在 main 函数内部，首先调用头文件中定义的公共显示函数。该函数显示全局变量。在第一种情况下，尚未对全局变量做任何更改，因此我们得到的值为 10。接下来调用“display_file1()”，它定义在源文件 1 中。在源文件内部，全局变量通过 extern 关键字被引用，然后该值递增 1。当从源文件 1 调用公共显示函数时，由于所进行的递增，我们得到的值为 11。控制权回到主模块后，调用“display_file2()”，它定义在源文件 2 中。同样的事情在源文件 2 中重复，并且由于全局变量内部已经是 11，接下来显示的值是 12。通过使用 extern 关键字，这个变量可用于将值从一个文件传递到另一个文件。

## 静态存储类

静态存储类说明符用于创建永久变量。一旦变量在函数或文件中被声明为 static，它们就会在函数调用之间保持其值。如果变量在函数内部被声明为 static，它们的作用域与自动变量相同。自动变量和静态变量之间的主要区别在于，静态变量在程序的整个生命周期内保留其值。如果控制权从函数返回，然后再次调用该函数，该函数内定义的静态变量将保留它们以前的值。

### 静态局部变量

当对函数内定义的局部变量使用静态存储类说明符时，就会为该变量创建永久存储。static 关键字确保变量在函数调用之间保留其值。清单 2.31 展示了 C 语言中的非静态存储类说明。

### 清单 2.31：C 语言中的非静态存储类说明

```c
#include<stdio.h>

void display();

int main()
{
    int i;

    for(i=0; i < 5; i++)
    {
        display();
    }
    getch();

}

void display()
{
    int x = 1;
    printf("\n Value of x is [%d] ",x);
    x++;
}
```

清单 2.31 的输出如下：

```text
Value of x is [1]
Value of x is [1]
Value of x is [1]
Value of x is [1]
Value of x is [1]
```

每次调用 display() 函数时，x 变量都会被重新初始化为 1，这就是我们得到该输出的原因。如果使用 static 关键字重写同样的代码，那么它看起来将如清单 2.32 所示：

### 清单 2.32：C 语言中的静态存储类说明

```c
#include<stdio.h>

void display();

int main()
{
    int i;

    for(i=0; i < 5; i++)
    {
        display();
    }
    getch();
}

void display()
{
        static int x = 1;

        printf("\n Value of X is [%d] ",x);
        x++;
}
```

清单 2.32 的输出如下：

```text
Value of X is [1]
Value of X is [2]
Value of X is [3]
Value of X is [4]
Value of X is [5]
```

静态存储类说明符使局部变量的内容永久化。初始化只发生一次，也就是说，当 display() 函数第一次被调用时，后续对该函数的调用会使用先前递增后的值。静态变量可以有多种用例。考虑这样一种场景：我们需要生成一个数字，而该数字将由上一次迭代的值决定。解决这个问题的方法之一是通过全局变量。然而，可能会发生其他函数访问该变量并在实际目的实现之前修改其值的情况。为了避免这种情况，静态变量是可供使用的最佳解决方案。

### 静态全局变量

如果我们将 static 说明符应用于全局变量，它会指示编译器创建一个全局变量，而该变量只在其声明的文件内部可见。与 extern 不同，静态全局变量具有内部链接。即使该变量被声明为全局变量，其他文件中的函数和例程也无法访问该变量。

尽管 static 说明符提供了所有优点，但它也有一些缺点。静态变量也被定义为永久变量，即使变量未被访问，它们的值也会保留在内存中，这最终可能导致内存浪费。

