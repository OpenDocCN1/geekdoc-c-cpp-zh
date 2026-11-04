
- b. 从栈中提取下一条语句的地址，程序的执行将继续执行该语句。
- c. 分配用于存储函数数据的内存将被释放（当然不包括静态变量的内存）。

例如，在下面的程序中，当调用 test() 时，编译器在栈中分配 808 字节来存储 i、j 和 arr 元素的值：

```c
#include <stdio.h>

void test(int i, int j);

int main(void)
{
    float a[1000], b[10];
    test(10, 20);
    return 0;
}

void test(int i, int j)
{
    int arr[200];
    ...
}
```

该内存会在 test() 终止时被释放。同样，为 main() 的局部变量分配的 4040 字节内存会在程序终止时被释放。

> 如果栈没有足够的内存来存储函数的数据，程序的执行将异常终止，并且可能会出现 “Stack overflow” 消息。

这种情况可能发生在函数分配大块内存并调用其他具有相当内存需求的嵌套函数时。例如，一个递归函数多次调用自身可能会导致可用栈内存耗尽。

## 动态内存分配

在动态分配中，内存是在程序执行期间从堆中分配的。与静态分配不同，其大小可以动态指定。此外，该大小可以根据程序的需求动态缩小或增长。通常，默认的栈大小并不大。例如，下面的程序可能因栈内存不可用而无法运行：

```c
#include <stdio.h>
int main(void)
{
    int arr[1000000]; /* Static allocation. */
    return 0;
}
```

另一方面，堆的大小通常远大于栈的大小。要使用动态分配，我们可以这样写：

```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int *arr;
    arr = (int*) malloc(1000000* sizeof(int));
    if(arr != NULL)
        free(arr);
    return 0;
}
```

接下来，我们将讨论 malloc() 和 free() 函数。现在请记住，动态分配的内存在使用完毕后应被释放。

## malloc() 函数

要动态分配内存，我们必须使用在 stdlib.h 中声明的 realloc()、calloc() 或 malloc() 函数之一。其中最常用的是 malloc()。其原型如下：

```c
void *malloc(size_t size);
```

请注意 size_t 类型通常是 unsigned int 类型的别名。size 参数声明要分配的字节数。如果内存分配成功，malloc() 返回指向该内存的指针，否则返回 NULL。malloc() 不会用某个值初始化内存，而 calloc() 则会将所有位设为 0。例如：

```c
int *ptr;
ptr = (int*) malloc(100);
```

> 始终检查 malloc() 的返回值。如果它为 NULL，尝试使用空指针会导致不可预测的结果；程序可能会崩溃。

在之前的程序中，最多可存储的整数数为 25，因为每个整数需要四个字节。请注意，我们可以写成 25*sizeof(int) 而不是 100。事实上，最佳实践是使用 sizeof 运算符，以便获得平台无关的程序。例如，int 类型在一个系统中可能占用两个字节，在另一个系统中占用四个字节。如果我们不使用 sizeof 运算符，malloc() 在第一个系统中会为 50 个整数保留内存，在第二个系统中则为 25 个。

> 提示：始终使用 sizeof 运算符来指定要分配的字节数。

然而，在为 char 类型分配内存时，可以安全地省略 sizeof 运算符，因为 char 类型的大小始终为一。例如，要为长度为 n 的字符串分配内存，我们写：

```c
char *ptr;
ptr = (char*) malloc(n+1);
```

额外的空间用于空字符。

另一个例子，要为 100 个 student 类型的结构体分配内存，我们写：

```c
struct student *ptr;
ptr = (struct student*) malloc(100*sizeof(student));
```

另外，许多人更喜欢使用指针。例如：

```c
ptr = (struct student*) malloc(100*sizeof(*ptr));
```

> 提示：始终记住已分配内存的大小以字节计算。

例如，下面的程序是错误的，因为在已分配的内存中只能存储一个整数，而不是四个：

```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int *arr, i;
    arr = (int*) malloc(4);
    if(arr != NULL)
    {
        for(i = 0; i < 4; i++)
            arr[i] = 10;
        free(arr);
    }
    return 0;
}
```

将 10 赋给 arr[0] 是正确的，但将值赋给 arr[1]、arr[2] 和 arr[3] 是错误的，因为没有为它们分配内存。如果我们写成：

```c
arr = (int*) malloc(4*sizeof(int));
```

程序将正常执行。希望你不会疑惑是否允许将指针用作数组。如果有疑问，请再次阅读第 8 章中的“指针和数组”部分。

malloc() 的典型用途是动态创建二维数组。假设在程序编译时维度未知。下面的程序读取浮点数数组的两个维度，分配内存，读取值并将它们存储到数组中。

```c
#include <stdio.h>
#include <stdlib.h>

void set_values(double **arr, int rows, int cols);

int main(void)
{
    int i, rows, cols;
    double **arr; /* We use a pointer to pointer variable to handle the two-dimensional array. */

    do
    {
        printf("Enter dimensions of array [N] [M] : ");
        scanf("%d%d", &rows, &cols);
    } while (rows <= 0 || cols <= 0);

    arr = (double**) malloc(rows * sizeof(double*)); /* The expression sizeof(double*) is used to allocate memory for 'rows' pointers to doubles. For example, if rows is 3, we allocate memory for arr[0], arr[1], and arr[2] pointers.*/
    if(arr == NULL)
    {
        printf("Error: Not available memory\n");
        exit(EXIT_FAILURE);
    }
    for(i = 0; i < rows; i++)
    {
        /* Allocate memory to store the elements of each row. Each row contains 'cols' elements. */
        arr[i] = (double*) malloc(cols * sizeof(double));
        if(arr[i] == NULL)
        {
            printf("Error: Not available memory\n");
            exit(EXIT_FAILURE);
        }
    }
    set_values(arr, rows, cols);
    for(i = 0; i < rows; i++)
        free(arr[i]);
    free(arr);
    return 0;
}
void set_values(double **arr, int rows, int cols)
{
    int i, j;
    for(i = 0; i < rows; i++)
        for(j = 0; j < cols; j++)
        {
            printf("Set arr[%d][%d]: ", i, j);
            scanf("%lf", &arr[i][j]);
            printf("arr[%d][%d] = %f\n", i, j, arr[i][j]);
        }
}
```

如你所见，我们将每个 arr[i] 用作指向包含 cols 个 double 的第 i 行的指针。我们添加该函数的原因是向你展示如何传递指向指针变量的指针，以及如何使用数组下标来处理它。还请注意，以这种方式分配内存时，元素可能不像普通声明（如 int arr[10][20]）那样位于连续的位置。

另外，我们也可以使用 malloc() 将二维数组模拟为一维数组。例如：

```c
double *arr = (double*) malloc(rows * cols * sizeof(double)); and write arr[i*cols+j] to access each i, j element.
```

## free() 函数

要释放动态分配的内存，我们必须使用在 stdlib.h 中声明的 free() 函数。其原型如下：

```c
void free(void *ptr);
```

ptr 必须指向动态分配的内存。否则，程序可能会有不可预测的行为。请注意，动态内存可以由一个函数分配并由另一个函数释放，前提是第二个函数可以访问该内存（例如，通过返回的指针）。如果 ptr 为 NULL，free() 不会产生任何效果。例如，下面的程序可能会崩溃，因为 ptr 并未指向已分配的内存：

```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int *ptr;
    free(ptr);
    return 0;
}
```
