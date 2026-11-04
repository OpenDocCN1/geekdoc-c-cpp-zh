
```c
#include <stdio.h>
int main(void)
{
    int *ptr, i, arr[5] = {10, 20, 30, 40, 50};

    ptr = arr;
    for(i = 0; i < 5; i++)
        printf("Addr = %p Val = %d\n", &ptr[i], ptr[i]);
    return 0;
}
```

请注意，虽然 arr[i] 和 ptr[i] 访问的是同一个元素，但编译器到达的方式不同。例如，要访问 arr[2]，它获取 arr 的地址，加上 8（正如所说，我们假设 int 的大小为 4 字节），然后前往所得地址获取值。另一方面，要访问 ptr[2]，它获取 ptr 的地址，检索存储在其中的值，加上 8，然后前往该地址获取值。换句话说，arr[2] 位于 arr 地址之后 8 个位置，而 ptr[2] 位于 ptr 指向的地址之后 8 个位置。

## 练习

### C.8.16

程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    int *ptr, arr[] = {10, 20, 30, 40, 50};

    ptr = arr;
    *ptr = 3;

    ptr += 2;
    *ptr = 5;
    printf("%d\n", arr[0]+arr[2]);
    return 0;
}
```

**答案：** 使用语句 ptr = arr; ptr 指向 arr[0] 的地址，因此 *ptr 等于 arr[0]。因此，语句 `*ptr = 3;` 等价于 `arr[0] = 3;`。语句 ptr += 2; 使 ptr 等于 arr[2] 的地址，因此 *ptr 等于 arr[2]。因此，语句 `*ptr = 5;` 等价于 `arr[2] = 5;`。结果，程序显示 8。

### C.8.17

程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    int i = 10, *p = &i;
    p[0] = 50;
    printf("%d\n", i+p[0]);
    return 0;
}
```

**答案：** 由于 p 指向 i 的地址，我们可以将其作为单个元素的数组进行索引。因此，语句 p[0] = 50; 等价于 i = 50; 程序显示 100。如果我们改写为 p[1] = 50; 而不是 p[0] = 50; 会发生什么？

语句 p[1] = 50; 尝试更改越界地址的值，这可能导致程序崩溃。

### C.8.18

编写一个程序，读取一月份的每日温度并将其存储在数组中。然后，程序应读取一个温度并显示温度小于该值的第一个日期编号。使用指针算术处理数组。

```c
#include <stdio.h>
#define SIZE 31
int main(void)
{
    int i;
    double temp, arr[SIZE];
    for(i = 0; i < SIZE; i++)
    {
        printf("Enter temperatures: ");
        scanf("%lf", arr+i); /* arr+i is equivalent to &arr[i]. */
    }
    printf("Enter temperature to check: ");
    scanf("%lf", &temp);
    for(i = 0; i < SIZE; i++)
    { /* The braces are not necessary. We put them to make the code easier to read. */
        if(*(arr+i) < temp)
            break;
    }
    if(i == SIZE)
        printf("No temperature less than %.1f\n", temp);
    else
        printf("The first temperature less than %.1f was %.1f in day %d\n", temp, *(arr+i), i+1);
    return 0;
}
```

### C.8.19

程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    int i, *ptr1, *ptr2, arr[] = {10, 20, 30, 40, 50, 60, 70};
    ptr1 = &arr[2];
    ptr2 = &arr[4];
    for(i = ptr2-ptr1; i < 5; i+=2)
        printf("%d ", ptr1[i]);
    return 0;
}
```

**答案：** 正如所说，当两个指向同一数组的指针相减时，结果是它们之间的元素个数，而不是它们在内存中的距离。因此，尽管 arr[4] 的地址比 arr[2] 的地址高八个位置，ptr2-ptr1 的结果等于它们下标的差，即 4-2 = 2。由于 ptr1 指向 arr[2]，ptr1[2] 对应 arr[4] 且 ptr1[4] 对应 arr[6]。因此，程序输出 50 和 70。

### C.8.20

编写一个程序，读取 10 名学生的成绩，将其存储在数组中，并显示最佳成绩和最差成绩以及它们在数组中首次出现的位置。程序应强制用户输入 [0, 10] 范围内的成绩。使用指针算术处理数组。

```c
#include <stdio.h>

#define SIZE 10

int main(void)
{
    int i, max_pos, min_pos;
    float max, min, arr[SIZE];

    max = -1;
    min = 11;
    for(i = 0; i < SIZE; i++)
    {
        do
        {
            printf("Enter grade: ");
            scanf("%f", arr+i);
        } while(*(arr+i) > 10 || *(arr+i) < 0); /* Check if the grade is within [0, 10]. */
        if(*(arr+i) > max)
        {
            max = *(arr+i);
            max_pos = i;
        }
        if(*(arr+i) < min)
        {
            min = *(arr+i);
            min_pos = i;
        }
    }
    printf("Max grade is %.2f in pos %d\nMin grade is %.2f in pos %d\n", max, max_pos, min, min_pos);
    return 0;
}
```

### C.8.21

使用 ptr 指针和迭代循环完成以下程序，将 arr 元素递减一。程序应在终止前显示它们的和。使用指针算术处理数组。

```c
#include <stdio.h>
int main(void)
{
    int *ptr, sum, arr[5] = {11, 21, 31, 41, 51};
    ...
}
```

**答案：**

```c
#include <stdio.h>
int main(void)
{
    int *ptr, sum, arr[5] = {11, 21, 31, 41, 51};

    sum = 0;
    for(ptr = arr; ptr < arr+5; ptr++)
    {
        --*ptr;
        sum += *ptr;
    }
    printf("Sum = %d\n", sum);
    return 0;
}
```

**注释：**

第一次迭代中，语句 ptr = arr; 使 ptr 指向 arr[0]。因此，*ptr 等于 arr[0]，即 11。语句 --*ptr; 等价于 --arr[0]; 因此 arr[0] 变为 10。该值被加到 sum。

以类似的方式，后续迭代将剩余元素递减一，它们的数值分别变为 20、30、40 和 50。当循环结束时，sum 等于新值的总和，程序输出：Sum = 150

### C.8.22

使用 ptr 指针完成以下程序，读取并将 50 名学生的成绩存储到 arr 中，然后以逆序显示数组的值。使用指针算术处理数组。

```c
#include <stdio.h>

#define SIZE 50

int main(void)
{
    float *ptr, arr[SIZE];
    ...
}
```

**答案：**

```c
#include <stdio.h>
#define SIZE 50
int main(void)
{
    float *ptr, arr[SIZE];
    ptr = arr;
    while(ptr < arr+SIZE)
    {
        printf("Enter grade: ");
        scanf("%f", ptr);
        ptr++;
    }
    ptr--;
    while(ptr >= arr)
    {
        printf("%f\n", *ptr);
        ptr--;
    }
    return 0;
}
```

### C.8.23

程序的输出是什么？

```c
#include <stdio.h>
int main(void)
{
    int *ptr1, *ptr2, i = 10, j = 20;
    ptr1 = &i;
    *ptr1 = 150;
    ptr2 = &j;
    *ptr2 = 50;
    ptr2 = ptr1;
    *ptr2 = 250;
    ptr1 = ptr2;
    *ptr1 += *ptr2;
    printf("%d\n", i+j);
    return 0;
}
```

**答案：** 由于 ptr1 指向 i 的地址，语句 `*ptr1 = 150;` 等价于 `i = 150;`。类似地，语句 `*ptr2 = 50;` 等价于 `j = 50;`。语句 `ptr2 = ptr1;` 使 ptr2 指向 ptr1 指向的同一地址，即 i 的地址。因此，语句 `*ptr2 = 250;` 等价于 `i = 250;`。

下一个语句不会改变 ptr1 的值；也就是说，它仍然指向 i 的地址。因此，语句 `*ptr1 += *ptr2;` 等价于 `i += i;`，即 i = i+i = 250+250 = 500。结果，程序输出 550。

### C.8.24

使用 ptr 指针完成以下程序，读取 50 个整数并将值在 [30, 40] 范围内的存储到 arr 中。程序应显示数组中存储了多少个值。程序应将 -1 设置为剩余元素。使用指针算术处理数组。

```c
#include <stdio.h>

#define SIZE 50

int main(void)
{
        int *ptr, i, arr[SIZE];
        ...
}
```

**答案：**

```c
#include <stdio.h>

#define SIZE 50

int main(void)
{
        int *ptr, i, arr[SIZE];

        ptr = arr;
        for(i = 0; i < SIZE; i++)
        {
                printf("Enter number: ");
                scanf("%d", ptr);

                if(*ptr >= 30 && *ptr <= 40)
                        ptr++;
        }
        printf("%d elements are stored\n", ptr-arr);
        for(; ptr < arr+SIZE; ptr++)
                *ptr = -1;
        return 0;
}
```

### C.8.25

你能检测到多少个编译错误？

```c
#include <stdio.h>
int main(void)
{
        int i, arr[5] = {10, 20, 30, 40, 50};

        for(i = 0; i < 5; i++)
                printf("%d\n", i[arr]);

        printf("%d\n", 2[arr]-3[arr]);
        return 0;
}
```
