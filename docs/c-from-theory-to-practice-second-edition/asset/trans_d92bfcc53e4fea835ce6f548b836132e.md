
```c
printf("No digit appears multiple times\n");
return 0;
}
```

## C.7.16 下面的程序正确吗？如果是，它输出什么？如果有错误，能否想到一个副作用？在查看答案之前先思考。

```c
#include <stdio.h>
int main(void)
{
    int i, a[] = {i, i+1, i+2};
    for(i = 0; i < 4; i++)
    {
        a[i] = 0;
        printf("%d ", a[i]);
    }
    return 0;
}
```

答案：你是否回答数组 a 的初始化是错误的？那里没有任何问题：i 有一个任意值，所以呢？错误在于重复次数。因为 a 包含三个元素，所以应该是 3，而不是 4。特别是当 i 变为 3 时，语句 a[i] = 0; 会给 a 之外的内存位置赋值。如果 i 存储在该位置，则 i 变为 0，循环变得无限。

> 小心，再小心数组边界，如果你想安稳入睡的话。

## C.7.17 编写一个程序读取一个整数并以二进制显示它。使用数组存储数字的位。要显示负数的位，使用补码技术。例如，如果用户输入 -5：

- a. 将其转换为正数（即 5）。
- b. 反转其位（即 101₂ 变为 11111111111111111111111111111010₂）。
- c. 加 1 即，数字变为 11111111111111111111111111111011₂）。

```c
#include <stdio.h>
int main(void)
{
    int i, j, tmp, bits[32]; /* This array holds the bits of the number, that is 0 or 1. The size is 32, because we assume that the size of an integer is 32 bits. */
    unsigned int num;

    printf("Enter number: ");
    scanf("%d", &tmp);
    if(tmp < 0)
    {
        tmp = -tmp;
        tmp = ~tmp;
        tmp++;
    }
    num = tmp;    /* It is stored as positive. */
    i = 0;
    /* Successive divisions by 2 and store each bit in the respective
    array position. */
    while (num > 0)
    {
        bits[i] = num & 1;
        num >>= 1; /* Equivalent to num /= 2. */
        i++;
    }
    printf("Binary form: ");
    /* Display the bits from left to right. */
    for (j = i-1; j >= 0; j--)
        printf("%d", bits[j]);
    return 0;
}
```

注释：我们使用移位运算符的原因是为了提高性能。然而，这很可能是不必要的，因为编译器本身会优化该操作。

## C.7.18 编写一个程序读取产品代码并将它们存储在 50 个位置的整数数组中。程序只有在代码尚未存储时才应将代码存储在数组中。如果数组已满或用户输入 -1，程序应显示存储的代码并终止。

```c
#include <stdio.h>

#define SIZE 50

int main(void)
{
    int i, j, pos, num, found, code[SIZE];

    pos = 0;
    while(pos < SIZE)
    {
        printf("Enter code: ");
        scanf("%d", &num);
        if(num == -1)
            break;

        found = 0;
        /* The pos variable indicates how many codes have been
        stored in the array. The loop checks if the input code is already stored.
        If it is, found becomes 1 and the loop terminates. */
        for(j = 0; j < pos; j++)
        {
            if(code[j] == num)
            {
                printf("Error: Code %d exists. ", num);
                found = 1;
                break;
            }
        }

        /* If the code is not stored, we store it and the index
        position is incremented. */
        if(found == 0)
        {
            code[pos] = num;
            pos++;
        }
    }
    printf("\nCodes: ");
    for(i = 0; i < pos; i++)
        printf("%d ", code[i]);
    return 0;
}
```

## C.7.19 编写一个程序读取 100 个整数并将它们存储在数组中。然后，程序应查找并显示两个不同的较大值。

```c
#include <stdio.h>

#define SIZE 100

int main(void)
{
    int i, max_1, max_2, arr[SIZE];

    for(i = 0; i < SIZE; i++)
    {
        printf("Enter number: ");
        scanf("%d", &arr[i]);
    }
    max_1 = max_2 = arr[0];
    for(i = 1; i < SIZE; i++)
    {
        if(max_1 != arr[i])
        {
            max_2 = arr[i]; /* We assign that value to max_2, to compare it with the remaining elements. */
            break;
        }
    }
    if(i == SIZE)
    {
        printf("Array contains the same value: %d\n", max_1);
        return 0;
    }
    /* Continue with the loop execution from the point the second loop ended. */
    for(; i < SIZE; i++)
    {
        if(arr[i] > max_1)
        {
            max_2 = max_1; /* The second higher value becomes equal to the first one. */
            max_1 = arr[i];
        }
        else if(arr[i] > max_2 && arr[i] != max_1) /* Search for the second higher value that is not equal to the first one. */
            max_2 = arr[i];
    }
    printf("First_Max = %d and Sec_Max = %d\n", max_1, max_2);
    return 0;
}
```

注释：查找数组中第 n 个最小或最大值元素的典型方法是使用排序算法，例如第 12 章中介绍的算法之一。特别是，数组首先被排序，我们要查找的元素是 a[n-1]。

## C.7.20 编写一个程序声明一个包含 10 个整数的数组，并为其元素分配 [5, 20] 范围内的随机值。然后，程序应检查数组是否包含重复值，如果有，则应删除它们。当元素被删除时，后续元素应向左移动一个位置。空位置应赋值为 -1。例如，如果数组为 [9, 12, 8, 12, 17, 8, 8, 19, 1, 19]，它应变为 [9, 12, 8, 17, 19, 1, -1, -1, -1]。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 10

int main(void)
{
    int i, j, k, size, arr[SIZE];

    srand(time(NULL));
    for(i = 0; i < SIZE; i++)
        arr[i] = rand()%16+5;

    size = SIZE;
    for(i = 0; i < size; i++)
    {
        j = i+1;
        while(j < size)
        {
            if(arr[i] == arr[j])
            {
                for(k = j; k < size-1; k++)
                    arr[k] = arr[k+1]; /* Shift the elements one position to the left. */
                size--; /* Since the element is deleted, their number is decremented. */
            }
            else
                j++;
        }
    }
    for(i = size; i < SIZE; i++)
        arr[i] = -1;
    for(i = 0; i < SIZE; i++)
        printf("%d ", arr[i]);
    return 0;
}
```

## C.7.21 可容纳 20 辆车的停车场对前三个小时收费 6 美元。每个额外小时收费 1.50 美元（即使多一分钟整个小时也收费）。最高收费为 12 美元，最大停车时间为 24 小时。编写一个程序读取停放车辆的数量和每辆车以小时和分钟为单位的停车时间，并以以下形式显示费用：

| 车 | 时间 | 费用 |
|---|---|---|
| 1 | 2.30' | 6.00 |
| 2 | 4.30' | 9.00 |
| 3 | 3.12' | 7.50 |
| 4 | 4.0' | 7.50 |
| 5 | 8.0' | 12.00 |
| 总计 |  | 42.00 |

```c
#include <stdio.h>

#define MAX_CARS 20

int main(void)
{
    int i, tmp, cars, car_mins[MAX_CARS], car_hours[MAX_CARS];
    double bill, total_bill;

    do
    {
        printf("Enter number of cars [1-%d]: ", MAX_CARS);
        scanf("%d", &cars);
    } while(cars <= 0 || cars >= MAX_CARS);

    for(i = 0; i < cars; i++)
    {
        do
        {
            printf("Enter hours for car_%d [max=24h]: ", i+1);
            scanf("%d", &car_hours[i]);
        } while(car_hours[i] > 24 || car_hours[i] < 0);

        if(car_hours[i] == 24) /* Maximum duration. */
        {
            car_mins[i] = 0;
            continue;
        }
        do
        {
            printf("Enter minutes for car_%d [max=59min]: ", i+1);
            scanf("%d", &car_mins[i]);
        } while(car_mins[i] > 59 || car_mins[i] < 0);
    }
    total_bill = 0;
    printf("\nCar\tTime\tCharge\n");
    for(i = 0; i < cars; i++)
    {
        bill = 6; /* For the first 3 hours. */
        tmp = car_hours[i]-3;
        if(tmp >= 0)
        {
            bill += tmp*1.5; /* For extra hours. */
            if(car_mins[i] > 0)
                bill += 1.5;
            if(bill > 12)
                bill = 12;
        }
        printf("%d\t%d.%d\t$%.2f\n", i+1, car_hours[i], car_mins[i],
        bill);
        total_bill += bill;
    }
    printf("SUM\t$%.2f\n", total_bill);
    return 0;
}
```

## C.7.22 编写一个程序模拟在线彩票游戏。假设中奖号码为 10 个，其值在 [0, 100] 范围内。然而，程序应以能够控制中奖号码的方式编写。特别是，“作弊”之处在于每次彩票中 3 个中奖号码也应出现在上一期中。程序应询问用户是否继续游戏，如果答案是否，则程序终止。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define SIZE 10

int main(void)
{
    int i, pos1, pos2, pos3, ans, arr[SIZE];
    srand(time(NULL));
    /* First lottery. */
    for(i = 0; i < SIZE; i++)
    {
        arr[i] = rand()%101;
        printf("%d ", arr[i]);
    }
    while(1)
    {
        printf("\nContinue to play? (0:No): ");
        scanf("%d", &ans);
        if(ans == 0)
            return 0;
```
