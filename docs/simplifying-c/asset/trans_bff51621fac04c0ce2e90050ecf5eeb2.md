

一旦已知二维数组的内存表示，下一个问题便是如何使用指针访问各个元素。与一维数组类似，数组名本身包含数组首元素的地址。因此，数组名充当指针变量。如果对指向数组的指针变量应用指针算术运算，就可以访问各个元素。理解如何使用指向数组的指针访问各个地址，这一点稍微有些棘手。

如图 13 所示，数组 i_arr 是一个包含九个元素的二维数组。实际上，它有三行和三列。一个非常常见的想法是，可以通过给数组指针添加一个计数器变量来访问每个单独的单元。然而事实并非如此。假设数组 i_arr 从内存位置 1000 开始。当给 i_arr 加 1 时，访问的地址应该是 1004。但当指针变量 i_arr 指向一个二维数组时，情况并非如此。相反，访问的下一个地址是下一行的地址。

让我们编写一个程序，打印出通过给数组指针添加整数值所访问的地址位置。程序 8 说明了指针与二维数组的用法。

## 程序 8

```c
/* Program to illustrate pointers and two-dimensional arrays */
#include<stdio.h>

/* Beginning of function main */
main()
{
    /* Initialization of array at compile time*/
    int i_arr[3][3]={45,60,12,43,44,65,57,18,32};

    /* Address of array */
    printf("\nThe address stored in i_arr is %u",i_arr);
    printf("\nThe address stored in i_arr + 1 is %u", i_arr+1);
    printf("\nThe address stored in i_arr + 2 is %u \n",i_arr+2);
    return;
}
/* End of function main */
```

### 输出

i_arr 中存储的地址是 65508

i_arr + 1 中存储的地址是 65520

i_arr + 2 中存储的地址是 65532

当执行程序 8 时，会显示三个地址作为输出。存储在 i_arr（指向任何数组的指针）中的第一个地址是 65508。存储在 i_arr+1 中的第二个地址是 65520，这是未曾预料到的。原本期望 i_arr + 1 指向第一行中的第二个元素的地址。然而，当 i_arr 增加 1 时，实际上直接增加了 12。地址 65520 是第二行中第一个元素的地址。类似地，i_arr+2 返回了 65532。预期的地址是第一行中第三个元素的地址，但返回的地址是第三行中第一个元素的地址。因此，当向数组 i_arr 中的指针添加一个整数时，地址位置会前进 24（12 × 2）字节。请注意，每次执行程序时，我们可能会得到不同的地址。

让我们通过添加一些语句来修改程序 8。程序 9 说明了这一修改：

## 程序 9

```c
/* Program to illustrate dereference pointer and two-dimensional array*/
#include<stdio.h>

/* Beginning of function main */
main()
{
    /* Initialization of array at compile time*/
    int i_arr[3][3]={45,60,12,43,44,65,57,18,32};

    printf("\nThe address stored in *(i_arr + 0) is %u",*i_arr);
    printf("\nThe address stored in *(i_arr + 1) is %u", *(i_arr+1));
    printf("\nThe address stored in *(i_arr + 2) is %u",*(i_arr+2));

    printf("\n\nThe address stored in i_arr is %u",i_arr);
    printf("\nThe address stored in i_arr + 1 is %u", i_arr+1);
    printf("\nThe address stored in i_arr + 2 is %u",i_arr+2);

    return;
}

/* End of function main */
```

### 输出

*(i_arr + 0) 中存储的地址是 65508
*(i_arr + 1) 中存储的地址是 65520
*(i_arr + 2) 中存储的地址是 65532

i_arr 中存储的地址是 65508
i_arr + 1 中存储的地址是 65520
i_arr + 2 中存储的地址是 65532

您可能已经注意到，当执行程序 9 时，*(i_arr+1) 和 (i_arr+1) 的结果是相同的。类似地，i_arr + 1 和 *(i_arr +1) 的结果，以及 i_arr+2 和 *(i_arr+2) 的结果也是相同的。它们指向不同行的第一个元素。图 14 清楚地展示了在指向二维数组的指针上执行指针算术运算的结果：

![](img/5d422ba7108ffdf64376be51eaf0c459_275_0.png)

**图 14：二维数组元素的指针算术运算**

此时产生的问题是，如何访问该行中的其他元素。指针算术运算 *(i_arr+0) 的结果是第一行第一个元素的地址。当向 *(i_arr + 0) 添加整数值 1 时，结果是第一行第二个元素的地址。当向 *(i_arr + 0) 添加整数值 2 时，结果是第一行第三个元素的地址。类似地，当向 *(i_arr + 1) 添加整数值 1 和 2 时，结果分别是第二行第二个和第三个元素的地址。当向 *(i_arr + 2) 添加整数值 1 和 2 时，结果分别是第三行第二个和第三个元素的地址。如果 *(i_arr + 1) + 1 的结果是第二行第二个元素的地址，那么极有可能在 *(i_arr + 1) + 1 前缀解引用运算符 * 后，会得到存储在第二行第二列的值。让我们编写一个程序来交叉验证上述说法。程序 10 说明了如何使用指针访问二维数组中的元素。

## 程序 10

```c
/* Program to illustrate the access of elements in two-dimensional array
with pointers*/
#include<stdio.h>

/* Beginning of function main */
main()
{
    /* Declare variables */
    int i_arr[3][3]={45,60,12,43,44,65,57,18,32};

    /* Print address of array element */
    printf("\nADDRESS OF ARRAY ELEMENTS\n");
    printf("\n\nThe address stored in *(i_arr + 0) + 0 is %u",*(i_arr + 0)+0);
    printf("\nThe address stored in *(i_arr + 0) + 1 is %u",*(i_arr + 0)+1);
    printf("\nThe address stored in *(i_arr + 0) + 2 is %u",*(i_arr + 0)+2);

    printf("\n\nThe address stored in *(i_arr + 1) + 0 is  %u",
    *(i_arr+1)+0);
    printf("\nThe address stored in *(i_arr + 1) + 1 is %u", *(i_arr+1)+1);
    printf("\nThe address stored in *(i_arr + 1) + 2 is %u", *(i_arr+1)+2);
    printf("\nThe address stored in *(i_arr + 2) + 0 is %u\n",*(i_arr+2)+0);
    printf("\nThe address stored in *(i_arr + 2) + 1 is %u\n",*(i_arr+2)+1);
    printf("\nThe address stored in *(i_arr + 2) + 2 is %u\n",*(i_arr+2)+2);

    /* Print values of array element */
    printf("\n\nVALUE OF ARRAY ELEMENTS\n");
    printf("\nThe value stored in *(*(i_arr + 0) + 0) is %u",*(*(i_arr + 0)+0));
    printf("\nThe value stored in *(*(i_arr + 0) + 1) is %u",*(*(i_arr + 0)+1));
    printf("\nThe value stored in *(*(i_arr + 0) + 2) is %u",*(*(i_arr + 0)+2));

    printf("\nThe value stored in *(*(i_arr + 1) + 0) is %u",*(*(i_arr+1)+0));
    printf("\nThe value stored in *(*(i_arr + 1) + 1) is %u",
    *(*(i_arr+1)+1));
    printf("\nThe value stored in *(*(i_arr + 1) + 2) is %u",
    *(*(i_arr+1)+2));
    printf("\nThe value stored in *(*(i_arr + 2) + 0) is %u\n",*(i_arr+2)+0);
    printf("\nThe value stored in *(*(i_arr + 2) + 1) is %u\n",*(i_arr+2)+1);
    printf("\nThe value stored in *(*(i_arr + 2) + 2) is %u\n",*(i_arr+2)+2);
    return;
}
/* End of function main */
```

### 输出

```
ADDRESS OF ARRAY ELEMENTS
The address stored in *(i_arr + 0) + 0 is 65508
The address stored in *(i_arr + 0) + 1 is 65512
The address stored in *(i_arr + 0) + 2 is 65516

The address stored in *(i_arr + 1) + 0 is 65520
The address stored in *(i_arr + 1) + 1 is 65524
The address stored in *(i_arr + 1) + 2 is 65528

The address stored in *(i_arr + 2) + 0 is 65532
The address stored in *(i_arr + 2) + 1 is 65536
The address stored in *(i_arr + 2) + 2 is 65540

VALUE OF ARRAY ELEMENTS
The value stored in *(*(i_arr + 0) + 0) is 45
The value stored in *(*(i_arr + 0) + 1) is 60
The value stored in *(*(i_arr + 0) + 2) is 12

The value stored in *(*(i_arr + 1) + 0) is 43
The value stored in *(*(i_arr + 1) + 1) is 44
The value stored in *(*(i_arr + 1) + 2) is 65

The value stored in *(*(i_arr + 2) + 0) is 57
The value stored in *(*(i_arr + 2) + 1) is 18
The value stored in *(*(i_arr + 2) + 2) is 32
```

