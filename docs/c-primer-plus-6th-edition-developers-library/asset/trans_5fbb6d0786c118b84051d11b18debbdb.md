

### 列表 16.20 mems.c 程序

```
// mems.c -- using memcpy() and memmove()
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#define SIZE 10
void show_array(const int ar[], int n);
// remove following if C11 _Static_assert not supported
_Static_assert(sizeof(double) == 2 * sizeof(int), "double not twice int size");
int main()
{
    int values[SIZE] = {1,2,3,4,5,6,7,8,9,10};
    int target[SIZE];
    double curious[SIZE / 2] = {2.0, 2.0e5, 2.0e10, 2.0e20, 5.0e30};

    puts("memcpy() used:");
    puts("values (original data): ");
    show_array(values, SIZE);
    memcpy(target, values, SIZE * sizeof(int));
    puts("target (copy of values):");
    show_array(target, SIZE);

    puts("\nUsing memmove() with overlapping ranges:");
    memmove(values + 2, values, 5 * sizeof(int));
    puts("values -- elements 0-5 copied to 2-7:");
    show_array(values, SIZE);

    puts("\nUsing memcpy() to copy double to int:");
    memcpy(target, curious, (SIZE / 2) * sizeof(double));
    puts("target -- 5 doubles into 10 int positions:");
    show_array(target, SIZE/2);
    show_array(target + 5, SIZE/2);

    return 0;
}

void show_array(const int ar[], int n)
{
    int i;

    for (i = 0; i < n; i++)
        printf("%d ", ar[i]);
    putchar('\n');
}
```

以下是输出：

```
memcpy() used:
values (original data):
1 2 3 4 5 6 7 8 9 10
target (copy of values):
1 2 3 4 5 6 7 8 9 10
```

```
Using memmove() with overlapping ranges:
values -- elements 0-5 copied to 2-7:
1 2 1 2 3 4 5 8 9 10
```

```
Using memcpy() to copy double to int:
target -- 5 doubles into 10 int positions:
0 1073741824 0 1091070464 536870912
1108516959 2025163840 1143320349 -2012696540 1179618799
```

最后一次调用 memcpy() 将数据从类型为 double 的数组复制到类型为 int 的数组。这表明 memcpy() 不知道也不关心数据类型；它只是从一个位置复制字节到另一个位置。 （例如，你可以从一个结构体复制字节到一个字符数组。）此外，没有数据转换。如果你有一个逐元素赋值的循环，类型为 double 的值在赋值期间会被转换为类型为 int。在这种情况下，字节是“原样”复制的，然后程序将位模式解释为好像它们是类型为 int 一样。

## 可变参数：stdarg.h

前面，本章讨论了可变宏——可以接受可变数量参数的宏。 stdarg.h 头文件为函数提供了类似的功能。但使用起来稍微复杂一些。你必须执行以下操作：

- 1. 使用省略号提供函数原型。
- 2. 在函数定义中创建一个 va_list 类型变量。
- 3. 使用宏将变量初始化为参数列表。
- 4. 使用宏访问参数列表。
- 5. 使用宏进行清理。

让我们更详细地看看这些步骤。这样的函数的原型应该有一个参数列表，其中至少有一个参数后跟省略号：

```
void f1(int n, ...);      // valid
int f2(const char * s, int k, ...);  // valid
char f3(char c1, ..., char c2);      // invalid, ellipsis not last
double f3(...);                      // invalid, no parameter
```

最右边的参数（省略号之前的那个）起着特殊的作用；标准使用术语 parmN 作为讨论时使用的名称。在前面的示例中，parmN 对于第一种情况是 n，对于第二种情况是 k。传递给此参数的实际参数将是省略号部分表示的参数数量。例如，以前原型化的 f1() 函数可以这样使用：

```
f1(2, 200, 400);      // 2 additional arguments
f1(4, 13, 117, 18, 23);  // 4 additional arguments
```

接下来，va_list 类型，该类型在 stdarg.h 头文件中声明，表示用于保存对应于参数列表省略号部分的参数的数据对象。可变函数定义的开始看起来像这样：

```
double sum(int lim,...)
{
    va_list ap;             // declare object to hold arguments
```

在此示例中，lim 是 parmN 参数，它将指示可变参数列表中的参数数量。

在此之后，函数将使用 va_start() 宏，该宏也定义在 stdarg.h 中，将参数列表复制到 va_list 变量。宏有两个参数：va_list 变量和 parmN 参数。继续前面的示例，va_list 变量称为 ap，parmN 参数称为 lim，因此调用看起来像这样：

```
va_start(ap, lim);      // initialize ap to argument list
```

下一步是获取对参数列表内容的访问权限。这涉及使用 va_arg()，另一个宏。它接受两个参数：va_list 变量和类型名称。第一次调用时，它返回列表中的第一项；下一次调用时，它返回下一项，依此类推。类型参数指定返回值的类型。例如，如果列表中的第一个参数是 double，第二个是 int，你可以这样做：

```
double tic;
int toc;
...
tic = va_arg(ap, double);  // retrieve first argument
toc = va_arg(ap, int);     // retrieve second argument
```

要小心。参数类型确实必须与规范匹配。如果第一个参数是 10.0，以上代码对 tic 来说效果很好。但如果参数是 10，代码可能无法工作；赋值时起作用的 double 到 int 的自动转换在这里不会发生。

最后，你应该使用 va_end() 宏进行清理。它可能例如释放动态分配以保存参数的内存。此宏以 va_list 变量作为其参数：

```
va_end(ap);             // clean up
```

在此之后，除非使用 va_start 重新初始化它，否则变量 ap 可能无法使用。

由于 va_arg() 不提供返回到以前参数的方法，因此保留 va_list 类型变量的副本可能很有用。C99 添加了一个用于此目的的宏。它称为 va_copy()。它的两个参数都是 va_list 类型变量，它将第二个参数复制到第一个参数：

```
va_list ap;
va_list apcopy;
double tic;
int toc;
...
va_start(ap, lim);      // initialize ap to argument list
va_copy(apcopy, ap);    // make apcopy a copy of ap
tic = va_arg(ap, double);  // retrieve first argument
toc = va_arg(ap, int);     // retrieve second argument
```

此时，即使它们已从 ap 中删除，你仍然可以从 apcopy 中检索前两项。

列表 16.21 是如何使用这些设施来创建求和可变数量参数的函数的简短示例；这里，sum() 的第一个参数是要求和的项目数。

### 列表 16.21 varargs.c 程序

```
//varargs.c -- use variable number of arguments
#include <stdio.h>
#include <stdarg.h>
double sum(int, ...);

int main(void)
{
    double s,t;

    s = sum(3, 1.1, 2.5, 13.3);
    t = sum(6, 1.1, 2.1, 13.1, 4.1, 5.1, 6.1);
    printf("return value for "
           "sum(3, 1.1, 2.5, 13.3):           %g\n", s);
    printf("return value for "
           "sum(6, 1.1, 2.1, 13.1, 4.1, 5.1, 6.1): %g\n", t);

    return 0;
}

double sum(int lim,...)
{
    va_list ap;                 // declare object to hold arguments
    double tot = 0;
    int i;
    va_start(ap, lim); // initialize ap to argument list
    for (i = 0; i < lim; i++)
        tot += va_arg(ap, double); // access each item in argument list
    va_end(ap); // clean up
    return tot;
}
```

```
return value for sum(3, 1.1, 2.5, 13.3): 16.9
return value for sum(6, 1.1, 2.1, 13.1, 4.1, 5.1, 6.1): 31.6
```

如果你检查算术，你会发现 sum() 对第一次函数调用求和了三个数字，对第二次函数调用求和了六个数字。

总的来说，使用可变函数比使用可变宏更复杂，但函数的应用范围更广。

## 关键概念

C 标准不仅仅描述了 C 语言；它描述了一个由 C 语言、C 预处理器和标准 C 库组成的包。预处理器让你能够塑造编译过程，列出要进行的替换，指示应编译哪些代码行，以及编译器行为的其他方面。C 库扩展了语言的范围，并为许多编程问题提供了预包装的解决方案。

## 摘要

C 预处理器和 C 库是 C 语言的两个重要补充。C 预处理器在源代码被编译之前，根据预处理器指令调整你的源代码。C 库提供了许多旨在帮助输入、输出、文件处理、内存管理、排序和搜索、数学计算和字符串处理等任务的函数，等等。附录 B 参考部分 V 列出了完整的 ANSI C 库。

## 复习问题

- 1. 这里有一组一个或多个宏，后面跟着使用它们的源代码行。每个情况下的结果代码是什么？它是否有效代码？（假设 C 变量已被声明。）

