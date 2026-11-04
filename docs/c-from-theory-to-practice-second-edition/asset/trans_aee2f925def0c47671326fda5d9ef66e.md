
请注意，free() 用于释放动态分配的内存，而不是静态内存。例如，如果我们将 ptr 声明为数组（即 int ptr[100]），程序再次会失败。此外，不要尝试释放已经被释放的内存。在下面的示例中，第二次调用 free() 是错误的，因为内存已经被释放：

```c
int *ptr = (int*) malloc(100*sizeof(int));
if(ptr != NULL)
{
    free(ptr);
    free(ptr);
}
```

![](img/b8da5dcf9ba7f1fad5213c453d095246_476_0.png)

不要忘记在不再需要时调用 free() 来释放动态分配的内存，以避免内存泄漏。

例如，以下代码写得好吗？

```c
char *ptr = (char*) malloc(10);
strcpy(ptr, "test");
ptr = (char*) malloc(20);
printf("%c\n", *ptr);
free(ptr);
```

由于在 ptr 指向第二个块之前没有释放第一个内存块，因此产生了内存泄漏；该内存保持不可用。代码输出该新内存中第一个字符的值。请注意内存泄漏，否则您可能会因内存不足错误而导致程序崩溃。找出以下程序中的错误：

```c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    char *p1, *p2;

    p1 = (char*) malloc(10);
    p2 = (char*) malloc(10);
    if(p1 != NULL && p2 != NULL)
    {
        p1 = p2;
        free(p1);
        p2[0] = 'a';
        free(p2);
    }
    return 0;
}
```

- a. 语句 p1 = p2; 使 p1 和 p2 指向同一块内存。语句 free(p1); 释放了该内存，因此下一条语句向未分配的内存赋值。
- b. 语句 free(p2); 释放了已经被释放的内存。
- c. p1 指向的第一个内存块从未被释放。

需要更多练习吗？找出以下程序中的错误：

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct
{
    int *i;
    char *c;
} test;

int main(void)
{
    test *t;
    int i;

    t = (test*) malloc(sizeof(test));
    t->i = (int*) malloc(10*sizeof(int));
    t->c = (char*) malloc(10);
    t->i[0] = 'a';
    t->c[5] = 50;
    for(i = 0; i < 10; i++)
        printf("%d %d\n", t->i[i], t->c[i]);
    free(t);
    free(t->i);
    free(t->c);
    return 0;
}
```

t->i[0] = 'a' 或 t->c[5] = 50 错了吗？当然不是，我们只是赋值了两个整数。循环呢？那也没问题；它使用数组下标来显示现有值。内存释放呢？好吧，这里就是 bug。首先我们必须释放为结构成员分配的内存，然后再释放整个结构的内存，而不是反过来。因此，我们必须将 free(t) 移到末尾。

在大型程序中，同一个指针可能在程序的不同部分使用，我们的建议是每次释放它时都将其设为 NULL 以提高安全性。这一做法在调试内存问题时帮助了我们很多。看看我曾经遇到过什么情况。有一次，我使用了一个包含数千个指向结构的指针的数组。我用 NULL 初始化它们，并在程序执行期间为其中一些分配内存。到目前为止，一切都很好。偶尔，内存会以随机顺序被释放。之后，程序崩溃了。最糟糕的是，程序有时会崩溃，而不是总是崩溃。这真是一场噩梦。经过数天的压力和艰难调试后，我们得出结论，崩溃是由于某些指针误用（……还有什么？）。以下是 buggy 代码：

```c
if(arr[i] != NULL)
    x = arr[i]->member;
```

if 条件不允许空指针访问成员。这没问题，但如果一个指针曾经指向一块内存，而该内存后来被释放了怎么办？例如，假设 arr[i] 指向的内存被释放了。条件仍然为真，因为内存被释放并不意味着 arr[i] 的值会变成 NULL。因此，使用 arr[i] 访问成员时，程序会崩溃。NULL 值必须显式赋值，因此当我在释放内存后添加语句 arr[i] = NULL 时，问题就解决了，我们直接去喝啤酒了。干杯！！！

## 内存管理函数

本节简要讨论了常用于内存管理的 memcpy()、memmove() 和 memcmp() 函数。memcpy() 用于从一个内存区域复制任何类型的数据到另一个内存区域。它在 string.h 中声明：

```c
void *memcpy(void *dest, const void *src, size_t size);
```

memcpy() 从 src 指向的内存复制 size 个字节到 dest 指向的地址。如果源地址和目标地址重叠，其行为未定义。例如，以下程序分配内存来存储字符串 "ABCDE" 并显示其内容：

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(void)
{
    char *arr;
    /* Allocate one extra byte for the null character. */
    arr = (char *) malloc(6);
    if(arr != NULL)
    {
        memcpy(arr, "ABCDE", 6);
        printf("%s\n", arr);
        free(arr);
    }
    return 0;
}
```

与 strcpy() 的主要区别是 strcpy() 在遇到空字符时会停止复制。另一方面，memcpy() 不会在复制指定数量的字节之前停止复制。例如，如果我们有：

```c
char str2[6], str1[] = {'a', 'b', 'c', '\0', 'd', 'e'};
```

并写：

```c
memcpy(str2, str1, 6);
```

str2 的内容将与 str1 相同。

另一方面，如果我们写：

```c
strcpy(str2, str1);
```

str2 的内容将为：{'a', 'b', 'c', '\0'}。

memmove() 与 memcpy() 类似，只是 memmove() 保证即使源内存和目标内存重叠，数据也会被正确复制。因为 memcpy() 不检查两个内存区域是否重叠，所以它的执行速度比 memmove() 快。请注意，目标内存的大小应至少为 size 个字节。如果不是，多余的字节将被写入未分配的内存，这意味着现有数据将被覆盖。例如，下一次复制是错误的，因为目标内存的大小为 3 字节，而复制的字节数为 6：

```c
char str1[3], str2[] = "abcde";
memcpy(str1, str2, sizeof(str2));
```

> memcpy() 通常非常有用，因为它通常以这样的方式实现，即复制大块数据可能比迭代循环更快。

例如，以下程序声明了两个包含 100000 个整数的数组，将 1 到 100000 的值设置到第一个数组的元素中，并使用 memcpy() 将它们复制到第二个数组中：

```c
#include <stdio.h>
#include <string.h>

#define SIZE 100000

int main(void)
{
    int i, arr1[SIZE], arr2[SIZE];

    for(i = 0; i < SIZE; i++)
        arr1[i] = i+1;

    memcpy(arr2, arr1, sizeof(arr1));
    /* We use memcpy() instead of an iteration loop such as:
    for(i = 0; i < SIZE; i++)
        arr2[i] = arr1[i]; */
    for(i = 0; i < SIZE; i++)
        printf("%d\n", arr2[i]);
    return 0;
}
```

memcmp() 用于比较存储在一个内存区域中的数据与存储在另一个内存区域中的数据。它在 string.h 中声明：

```c
int memcmp(const void *ptr1, const void *ptr2, size_t size);
```

memcmp() 比较 ptr1 和 ptr2 指向的内存区域的 size 个字节。memcmp() 的返回值与 strcmp() 相同。与 strcmp() 的主要区别是 strcmp() 在遇到任一字符串中的空字符时会停止比较；而 memcmp() 则只在比较了 size 个字节后才停止比较；它不会查找空字符。例如：

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int main(void)
{
    char str1[] = {'a', 'b', 'c', '\0', 'd', 'e'};
    char str2[] = {'a', 'b', 'c', '\0', 'd', 'f'};
    if(strcmp(str1, str2) == 0)
        printf("Same\n");
    else
        printf("Different\n");
    if(memcmp(str1, str2, sizeof(str1)) == 0)
        printf("Same\n");
    else
        printf("Different\n");
    return 0;
}
```

因为 strcmp() 在遇到空字符时会停止比较，所以程序显示 Same。相反，memcmp() 比较所有字节，程序显示 Different。

## 练习

- C.14.1 以下 malloc() 分配了多少字节？

```c
double *ptr;
ptr = (double*) malloc(100*sizeof(*ptr));
```

答案：由于 ptr 是指向 double 的指针，sizeof(*ptr) 计算 double 类型的大小，即 8。因此，malloc() 分配了 800 字节。

- C.14.2 以下程序的输出是什么？

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
void test(char *p);
int main(void)
{
    char *p1, *p2;
    p1 = p2 = (char*) malloc(5);
```
