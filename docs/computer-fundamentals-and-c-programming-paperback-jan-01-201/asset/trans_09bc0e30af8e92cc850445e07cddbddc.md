

```c
/* variable_arguments.c: Uses a variable of type va_list and 3 macros. */

#include <stdio.h>
#include <stdarg.h>          /* Defines 3 macros -- va_start, va_arg, va_end */
int sum(int argc, ...);      /* ... indicates variable number of arguments */
int main(void) {
    printf("10 + 20 + 40 = %d\n", sum(3, 10, 20, 40));
    printf("1 + 2 + 3 + 5 + 10 = %d\n", sum(5, 1, 2, 3, 5, 10));

    return 0;
}

int sum(int argc, ...)        /* Function definition */
{
    int i, total = 0;

    /* First define a variable arglist of type va_list */
    va_list arglist;
    /* Initialize arglist */
    va_start(arglist, argc);
    /* Retrieve all arguments from arglist */
    for (i = 0; i < argc; i++)
        total += va_arg(arglist, int);

    /* Clean up arglist */
    va_end(arglist);
    return total;
}
```

程序 17.6：**variable_arguments.c**

```text
10 + 20 + 40 = 70
1 + 2 + 3 + 5 + 10 = 21
```

程序输出：**variable_arguments.c**

## 17.13 多源程序文件

最简单的应用程序使用单个源文件。典型的商业应用程序分散在多个 .c（源）文件、.h（包含）文件和 .o（目标）文件中，并带有一个或多个可执行文件。使用 `gcc foo.c` 或 `cl foo.c` 的标准做法在这种情况下不起作用。当代码分布在多个文件中时，编译时必须包含所有 .c 文件。GCC 和 Visual Studio 就是这样编译多文件程序的：

| 命令 | 描述 |
|---|---|
| `gcc a.c b.c c.c` | 创建 a.out；没有 .o 文件 |
| `cl a.c b.c c.c` | 创建 a.exe 和三个 .obj 文件 |

在 Linux 系统上，**gcc** 会在调用链接器创建单个可执行文件之前调用汇编器（4.2.3）创建 .o 文件。使用 -c 选项，你可以只创建目标文件而不创建 **a.out**。

```text
gcc -c a.c b.c c.c
```

*只创建* a.o、b.o *和* c.o

对于单源程序（函数与主程序本身存储在同一文件中），我们通常不需要中间 .o 文件。然而，在现实场景中，我们常常不得不进行*部分*编译并维护这些 .o 文件。要理解原因，让我们考察一个多源应用程序。

### 17.13.1 一个多源应用程序

我们的示例应用程序计算定期存款的利息。主程序 **rec_deposit.c**（程序 17.7a）接受三个参数，分别表示本金、利率和期限。到期金额写入标准输出。主程序调用三个函数：

- **arg_check** 此函数检查是否已输入正确数量的参数。它定义在 **arg_check.c** 中，该文件包含 arg_check.h（程序 17.7b）。
- **quit** 此函数打印一条消息并终止程序。它定义在 **quit.c** 中，并包含 quit.h（程序 17.7c）。
- **compute** 它根据提供的三个参数计算利息。此函数未放在单独的文件中。

**arg_check** 和 **quit** 是有用的可重用函数。**compute** 保留在主文件中，只是为了理解为什么它也应该移到自己的源文件中。两个头文件除了通常的 include 语句外，还包含各自函数的原型。这些函数在 **main** 中使用，因此它们的头文件也必须包含在 **rec_deposit.c** 中。

```c
#include <math.h>
#include "quit.h"
#include "arg_check.h"
float compute(float, float, float);
int main(int argc, char **argv) {
    float principal, interest, term, sum;
    char *mesg = "Three arguments required\n";
    char *mesg2 = "All arguments must be positive\n";
    arg_check(4, argc, mesg, 1);       /* Checks for three arguments */
    sscanf(argv[1], "%f", &principal); /* Converting strings to float */
    sscanf(argv[2], "%f", &interest);
    sscanf(argv[3], "%f", &term);

    if (principal <= 0 || interest <= 0 || term <= 0)
        quit(mesg2, 2);                /* Quits with 2 as $? on error */
    sum = compute(principal, interest, term);
    printf("Maturity amount: %f\n", sum );
    exit(0);
}

float compute(float principal, float interest, float term) {
    int i;
    float maturity = 0;
    interest = 1 + interest / 100 ;
    for (i = 1 ; i <= term ; i++)
        maturity += principal * pow(interest, i) ;
    return maturity;
}
```

程序 17.7a：**rec_deposit.c**

```c
#include "arg_check.h"
void arg_check (int args, int argc, char *message, int exit_status) {
    if (argc != args) {
        fprintf(stderr, message);
        exit(exit_status);
    }
}
```

程序 17.7b：**arg_check.c**

```c
#include <stdio.h>
#include <stdlib.h>
void arg_check (int, int, char *, int);
```

文件：**arg_check.h**

```c
#include "quit.h"
void quit (char *message, int exit_status) {
    fprintf(stderr, message);
    exit(exit_status);
}
```

程序 17.7c：**quit.c**

```c
#include <stdio.h>
#include <stdlib.h>
void quit (char *, int);
```

文件：**quit.h**

主程序 `rec_deposit.c` 调用 `arg_check` 以确定是否输入了三个参数。它调用 `sscanf` 三次，将参数字符串转换为浮点数。如果任一参数不是正数，`quit` 会向标准错误打印用户指定的消息并终止程序。如果验证成功，`main` 调用 `compute` 进行实际计算。

### 17.13.2 编译和链接应用程序

函数 `arg_check` 和 `quit` 足够通用，也可供其他程序使用，因此保留它们的目标文件是有意义的。生成这些文件的技术在 GCC 和 Visual Studio 之间有所不同。对于 GCC，以下调用 `gcc -c` 会创建三个 `.o` 文件：

```text
$ rm *.o                         First remove all object files
$ gcc -c rec_deposit.c arg_check.c quit.c
$ ls *.o
arg_check.o       quit.o       rec_deposit.o       No .o file for compute
```

现在必须链接这些目标文件以创建可执行文件。然而，这一次必须*显式*指示链接器从数学库中获取 `pow` 函数的代码。这通过 `-l` 选项完成，该选项假定库名带有“lib”前缀和“.a”后缀，并且只需要指定文件名的剩余部分。

因此，要链接包含 `pow` 代码的 `libm.a`，需要使用 `-lm` 选项。请注意，此选项必须放在命令行的末尾：

```text
$ gcc -o rec_deposit rec_deposit.o arg_check.o quit.o -lm
$ _                                  Compilation successful
```

我们还使用了 `-o` 选项来指定自己的可执行文件名（`rec_deposit` 而不是 `a.out`）。多次运行程序以测试用户定义的函数：

```text
$ rec_deposit                                      arg_check working
Three arguments required
$ rec_deposit 100 5 0                                quit working
All arguments must be positive
$ rec_deposit 100 5 2                                compute working
Maturity amount: 215.249985
```

输出显示 215.25 为每年投资 100 单位、连续两年、利率 5% 的到期价值。既然程序运行正常，你还需要保留 `.o` 文件吗？是的，因为如果你后来决定修改，比如 `quit.c`，你必须在重新链接三个 `.o` 文件之前重新创建 `quit.o`。如果这些文件不可用，你必须用 `gcc -c` 重新生成它们——如果你保留了 `.o` 文件，这项工作本来是可以避免的。

> **注意：** Visual Studio 所遵循的过程与 GCC 所遵循的过程截然不同。对于 Visual Studio，你不需要发出特定指令来与数学库链接。命令 `cl rec_deposit.c quit.c arg_check.c` 一次性完成所有事情，包括创建 `.obj` 文件。

> **注意：** 此应用程序没有为 **compute** 单独生成目标文件；其代码嵌入在 `rec_deposit.o` 中。这不是正确的做法，因为可重用函数应放在单独的文件中。

## 接下来做什么？

我们已经到达本书的结尾，也暂时结束了我们的 C 语言之旅——至少目前如此。C 是一门强大但棘手的语言，既能让人兴奋，也能让人沮丧。有本书在手，请确保同时探索网络内外可用的大量资源（附录 E）。

## 你学到了什么？

C 预处理器在编译之前修改包含以 # 为前缀的*指令*的程序。这些指令有助于最大限度减少可能的编辑位置数量，从而使程序更易于修改。

**#define** 指令创建*命名常量*和*宏*，它们在程序全局范围内执行替换。宏接受与类型无关的参数，并且常常可以替代函数。

**#include** 指令将文件内容放入程序中。该文件通常包含 **#define** 指令以及全局变量、结构和函数原型的声明。

预处理器使用*条件编译*特性来使程序的某些部分被包含在编译过程中或被排除在外。

*按位运算符*使整数的特定比特位能够被访问和操作。按位运算符（&、|、^ 和 ~）使特定比特位能够被设置或清除。数字的所有比特位都可以用移位运算符（<< 和 >>）向左或向右移位。

函数可以通过其指针访问，而该指针可以作为参数传递给另一个函数。

可以设计一个函数，使用三个宏（**va_start**、**va_arg** 和 **va_end**）来接受多个参数，这些宏对 `va_list` 类型的列表进行操作。

程序可以组织在多个文件中，这些文件分别编译以生成各自的目标文件。函数声明、**#define** 和 **#include** 指令可以存储在单独的文件中，并在编译期间合并。

## 客观题

### A1. 判断题

- 17.1 如果指令以分号结尾，预处理器会输出错误。
- 17.2 可以在不先取消定义的情况下，将命名常量重新定义为不同的值。

