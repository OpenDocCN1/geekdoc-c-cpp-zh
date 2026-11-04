
## C.73

编写一个程序，声明一个包含五个元素的数组，并使用 for 循环将值 1.1、1.2、1.3、1.4 和 1.5 分配给它们。然后，程序应以相反的顺序显示数组的元素。

```
#include <stdio.h>
int main(void)
{
    int i;
    double arr[5];
    for(i = 0; i < 5; i++)
        arr[i] = 1.1 + (i*0.1);
    for(i = 4; i >= 0; i--)
        printf("%f\n", arr[i]);
    return 0;
}
```

注释：另一种解决方案可以是用以下内容替换第一个循环：

```
arr[0] = 1.1;
for(i = 1; i < 5; i++)
    arr[i] = arr[i-1] + 0.1;
```

## C.74

下列程序中数组 a 的值会是什么？

```
#include <stdio.h>
int main(void)
{
    int i, a[3] = {4, 2, 0}, b[3] = {2, 3, 4};
    for(i = 0; i < 3; i++)
        a[b[i]-a[2-i]]++;
    return 0;
}
```

答案：当声明 a 时，我们有 a[0] = 4, a[1] = 2, 且 a[2] = 0。同样地，当声明 b 时我们有 b[0] = 2, b[1] = 3, 且 b[2] = 4。让我们追踪迭代：
第一次迭代 (i=0)。 a[b[0]-a[2]]++ = a[2-0]++ = a[2]++ = 1。
第二次迭代 (i=1)。 a[b[1]-a[1]]++ = a[3-2]++ = a[1]++ = 3。
第三次迭代 (i=2)。 a[b[2]-a[0]]++ = a[4-4]++ = a[0]++ = 5。
因此，a[0]、a[1] 和 a[2] 分别变为 5、3 和 1。

## C.75

编写一个程序，读取 10 个整数并将它们存储在数组中。然后，程序应检查数组是否对称，即第一个元素的值等于最后一个元素的值，第二个元素的值等于倒数第二个元素的值，以此类推。

```
#include <stdio.h>
#define SIZE 10
int main(void)
{
    int i;
    double sum, arr[SIZE];
    sum = 0; /* Initialize with 0 the variable that calculates the sum of the array elements. */
    srand(time(NULL));
    for(i = 0; i < SIZE; i++)
    {
        arr[i] = (double)rand() / RAND_MAX;
        sum += arr[i];
    }
    printf("Avg = %f\n", sum/SIZE);
    return 0;
}
```

## C.78 下列程序中数组 a 的值会是什么？

```
#include <stdio.h>
int main(void)
{
    int i, a[3] = {0, 1, 2};

    for(i = 1; i < 4; i++)
        a[a[a[3-i]]] = i-1;
    return 0;
}
```

答案：当声明 a 时，我们有 a[0] = 0, a[1] = 1, 且 a[2] = 2。让我们追踪迭代：

第一次迭代 (i=1): a[a[a[2]]] = a[a[2]] = a[2] = i-1 = 1-1 = 0。
第二次迭代 (i=2): a[a[a[1]]] = a[a[1]] = a[1] = i-1 = 2-1 = 1。
第三次迭代 (i=3): a[a[a[0]]] = a[a[0]] = a[0] = i-1 = 3-1 = 2。

因此，a[0]、a[1] 和 a[2] 分别变为 2、1 和 0。

## C.79

编写一个程序，读取 100 名学生的成绩并将它们存储在数组中。然后，程序应显示平均分、最好成绩和最差成绩，以及它们首次出现时在数组中的位置。程序应强制用户输入 [0, 10] 范围内的成绩。

```
#include <stdio.h>

#define SIZE 100

int main(void)
{
    int i, min_pos, max_pos;
    float sum, min_grd, max_grd, grd[SIZE];

    sum = 0;
    max_grd = -1;
    min_grd = 11;
```

```
for(i = 0; i < SIZE; i++)
{
    printf("Enter grade in [0-10]: ");
    scanf("%f", &grd[i]);
    /* There are several ways to check whether the input grade is valid. In C.7.14, we'll use do-while. */
    while(grd[i] < 0 || grd[i] > 10)
    {
        printf("Error - Enter new grade in [0-10]: ");
        scanf("%f", &grd[i]);
    }
    sum += grd[i];
    if(grd[i] > max_grd)
    {
        max_grd = grd[i];
        max_pos = i; /* Store the position with the best grade. */
    }
    if(grd[i] < min_grd)
    {
        min_grd = grd[i];
        min_pos = i; /* Store the position with the worst grade. */
    }
}
printf("Avg: %.2f H(%d): %.2f L(%d): %.2f\n", sum/SIZE, max_pos, max_grd, min_pos, min_grd);
return 0;
}
```

## C.7.10 以下程序的目的是生成 10 个随机整数，将它们存储在数组中，然后在 freq 频率数组中存储 0 到 9 每个数字出现的次数。你能找到程序中的任何错误吗？如果有，请纠正它们。

```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 10

int main(void)
{
    int i, num, arr[SIZE], freq[SIZE];

    srand(time(NULL));
    for(i = 0; i < SIZE; i++)
        arr[i] = rand();

    for(i = 0; i < SIZE; i++)
    {
        num = arr[i];
        freq[num]++;
    }
```

```
```c
printf("\nNumber occurrences\n");
for(i = 0; i < SIZE; i++)
    printf("%d appears %d times\n", i, freq[i]);
return 0;
}
```
```

**答案：** 第一个错误是 freq 数组的元素未初始化为 0，因此语句 freq[num]++; 会递增 freq[num] 的无意义值。因此，我们应将声明改为 freq[SIZE] = {0}。

然而，最严重的错误发生在 arr 包含一个超出 [0, SIZE-1] 的数字时。例如，如果存储数字 30，则 num 变为 30，语句 freq[30]++; 会更改 arr 之外的内存位置的内容。此错误可通过使用 **if** 语句来纠正。例如：

```
```c
if (num >= 0 && num <= SIZE-1)
    freq[num]++;
```
```

## C.7.11 编写一个程序，读取 20 个整数并将它们存储在两个各有 10 个元素的数组中。然后，程序应检查这两个数组是否有共同元素，如果有，程序应显示每个共同元素的值及其在两个数组中的位置。否则，应显示一条消息，说明它们的元素不同。

```
#include <stdio.h>

#define SIZE 10

int main(void)
{
    int i, j, cnt, arr1[SIZE], arr2[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        printf("Enter number for the 1st array: ");
        scanf("%d", &arr1[i]);

        printf("Enter number for the 2nd array: ");
        scanf("%d", &arr2[i]);
    }
    cnt = 0; /* This variable counts the common elements. */
    for(i = 0; i < SIZE; i++)
    {
        for(j = 0; j < SIZE; j++) /* This loop checks if an element
        of the first array is contained in the second one. */
        {
            if(arr1[i] == arr2[j])
            {
                cnt++;
                printf("Common = %d (Pos_1 = %d Pos_2 = %d)\n", arr1[i], i, j);
            }
        }
    }
}
```

```
{
    sum_fail += grd;
    arr2[m] = grd;
    m++;
}
}
if(i != 0)
{
    if(k != 0)
        printf("\nSuccess_Avg: %.2f\n", sum_suc/k);
    else
        printf("\nAll students failed\n");
    if(m != 0)
        printf("\nFail_Avg: %.2f\n", sum_fail/m);
    else
        printf("\nAll students passed\n");
}
return 0;
}
```

## C.7.14 编写一个程序，读取 10 个整数并仅在以下任一情况下将它们存储在数组中：

- a. 当前位置为偶数，即 0、2、4、...，且输入的数字为偶数，或
- b. 当前位置为奇数，即 1、3、5、...，且输入的数字为奇数。

程序不应接受值 0 和 -1 并提示用户输入新值。完成数字插入后，未分配的元素应设为 -1。程序应在结束前显示数组元素。

```
#include <stdio.h>

#define SIZE 10

int main(void)
{
    int i, num, arr[SIZE] = {0}; /* Since the value 0 is not an acceptable value, we use it as a special value to indicate that an element is unassigned. */
    for(i = 0; i < SIZE; i++)
    {
        do
        {
            printf("Enter number: ");
            scanf("%d", &num);
            if(num == 0 || num == -1)
                printf("Not valid input !!!\n");
        } while(num == 0 || num == -1);
        if(i & 1) /* Check if the position is odd. */
        {
            if(num & 1) /* Store the number only if both the position and the number are odd. */
                arr[i] = num;
        }
        else
        {
            if((num & 1) == 0) /* Store the number only if both
the position and the number are even. */
                arr[i] = num;
        }
        printf("\n*** Array elements ***\n");
        for(i = 0; i < SIZE; i++)
        {
            if(arr[i] == 0)
                arr[i] = -1;
            printf("%d\n", arr[i]);
        }
        return 0;
    }
}
```

## C.7.15 编写一个程序，读取一个整数并显示出现超过一次的数字及其出现次数。例如，如果用户输入 1868，程序应显示数字 8 出现了两次。如果没有数字出现超过一次，程序应显示相关消息。

```
#include <stdio.h>
int main(void)
{
    int i, rem, flag, dig_times[10] = {0}; /* This array holds the
appearances of each digit. For example, dig_times[0] indicates how many
times digit 0 appears. */
    printf("Enter number: ");
    scanf("%d", &i);
    if(i != 0) /* Check if 0 is entered. */
        dig_times[0] = 1;
    while(i != 0)
    {
        rem = i%10;
        if(rem < 0)
            rem = -rem;
        dig_times[rem]++;
        i /= 10;
    }
    flag = 0;
    for(i = 0; i < 10; i++)
    {
        if(dig_times[i] > 1)
        {
            printf("Digit %d appears %d times\n", i,
dig_times[i]);
            flag = 1;
        }
    }
    if(flag == 0)
```
