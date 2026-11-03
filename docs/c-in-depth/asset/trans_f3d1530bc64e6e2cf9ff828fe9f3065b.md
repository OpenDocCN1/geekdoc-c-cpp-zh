
我们必须使用for循环逐个复制数组的所有元素。

```c
for (i = 0; i < 5; i++)
    b[i] = a[i];
```

在下面的程序中，我们将找出一个整数数组中的最大值和最小值。

```c
/*P7.4 程序：查找数组中的最大值和最小值*/
#include<stdio.h>
main()
{
    int i,j,arr[10]={2,5,4,1,8,9,11,6,3,7};
    int min,max;
    min=max=arr[0];
    for(i=1;i<10;i++)
    {
        if(arr[i]<min)
            min=arr[i];
        if(arr[i]>max)
            max=arr[i];
    }
    printf("Minimum = %d, Maximum = %d\n",min,max);
}
```

**输出：**

Minimum = 1, Maximum = 11

我们将第一个元素的值作为min和max的初始值。在for循环内部，我们从第二个元素开始比较，所以这次循环从1开始而不是从0开始。

下面的程序将反转数组的元素。

```c
/*P7.5 程序：反转数组的元素*/
#include<stdio.h>
main()
{
    int i,j,temp,arr[10]={1,2,3,4,5,6,7,8,9,10};
    for(i=0,j=9;i<j;i++,j--)
    {
        temp=arr[i];
        arr[i]=arr[j];
        arr[j]=temp;
    }
    printf("After reversing the array is : ");
    for(i=0;i<10;i++)
        printf("%d ",arr[i]);
    printf("\n");
}
```

**输出：**

After reversing the array is : 10 9 8 7 6 5 4 3 2 1

在for循环中，我们使用了逗号运算符，并使用了两个变量i和j。变量i初始化为下界，j初始化为上界。循环每执行一次，i递增而j递减。在循环内部，a[i]与a[j]交换。因此a[0]将与a[9]交换，a[1]与a[8]交换，a[2]与a[7]交换，依此类推。

下一个程序打印一个十进制数的二进制等价形式。从十进制数29得到二进制数的过程如下所示：

| 表达式 | 商 | 余数 | 数组 | 备注 |
|---|---|---|---|---|
| 29/2 | 14 | 1 | a[0] | 最低有效位 |
| 14/2 | 7 | 0 | a[1] | |
| 7/2 | 3 | 1 | a[2] | |
| 3/2 | 1 | 1 | a[3] | |
| 1/2 | 0 | 1 | a[4] | 最高有效位 |

我们将余数存储在数组中，最后按逆序打印数组以得到二进制数。

```c
/*P7.6 程序：将十进制数转换为二进制数*/
#include<stdio.h>
main()
{
 int num,rem,arr[15],i,j;
 printf("Enter a decimal number : ");
 scanf("%d",&num);
 i=0;
 while(num>0)
 {
  arr[i]=num%2;   /*将余数存入数组*/
  num/=2;
  i++;
 }
 printf("Binary number is : ");
 for(j=i-1;j>=0;j--)/*逆序打印数组*/
  printf("%d",arr[j]);
 printf("\n");
}
```

**输出：**

Enter a decimal number : 29
Binary number is : 11101

下一个程序在数组中搜索特定项。

```c
/*P7.7 程序：在数组中搜索某个项*/
#include<stdio.h>
#define SIZE 10
main()
{
 int i,arr[SIZE]={23,12,56,98,76,14,65,11,19,45};
 int item;
 printf("Enter the item to be searched : ");
 scanf("%d",&item);
 for(i=0;i<SIZE;i++)
 {
    if(item==arr[i])
    {
        printf("%d found at position %d\n",item,i+1);
        break;
    }
 }
 if(i==SIZE)
    printf("Item %d not found in array\n", item);
}
```

将要搜索的项与数组的每个元素进行比较，如果找到该元素，则通过break语句终止for循环。控制流可以从循环中出来的情况有两种：第一种是找到项并通过break终止循环；第二种是未找到项且循环完整执行。在第二种情况下，i的值将等于SIZE。这里我们是顺序搜索项的，因此这种搜索被称为线性搜索或顺序搜索。

## 7.1.5 一维数组与函数

### 7.1.5.1 向函数传递单个数组元素

我们知道，数组元素在程序中与任何其他简单变量一样对待。因此，我们可以像传递其他简单变量一样，将单个数组元素作为参数传递给函数。

```c
/*P7.8 程序：向函数传递数组元素*/
#include<stdio.h>
main()
{
    int arr[10],i;
    printf("Enter the array elements : ");
    for(i=0;i<10;i++)
    {
        scanf("%d",&arr[i]);
        check(arr[i]);
    }
}
check(int num)
{
    if(num%2==0)
        printf("%d is even\n",num);
    else
        printf("%d is odd\n",num);
}
```

### 7.1.5.2 向函数传递整个一维数组

我们可以将整个数组作为实际参数传递给函数。相应的形式参数应声明为相同数据类型的数组变量。

```c
main()
{
    int arr[10];
    .......
    .......
    func(arr); /*在函数调用中，指定数组名时不带方括号*/
}
func(int val[10])
{
    .......
    .......
}
```

在形式参数中指定数组的大小是可选的，例如我们可以将函数定义写为：

```c
func(int val[ ])
{
    .......
    .......
}
```

我们之前学过，对形式参数所做的更改不会影响实际参数，但在将数组传递给函数时情况并非如此。将数组传递给函数的机制与传递简单变量完全不同。我们之前学过，对于简单变量，被调用函数会创建变量的副本并对其进行操作，因此函数中所做的任何更改都不会影响原始变量。当数组作为实际参数传递时，被调用函数实际上可以访问原始数组并对其操作，因此函数内部所做的任何更改都会影响原始数组。下面是一个将数组传递给函数的程序。

```c
/*P7.9 程序：理解将数组传递给函数的影响*/
#include<stdio.h>
main()
{
    int i,arr[6]={1,2,3,4,5,6};
    func(arr);
    printf("Contents of array are now : ");
    for(i=0;i<6;i++)
        printf("%d ",arr[i]);
    printf("\n");
}
func(int val[])
{
    int sum=0,i;
    for(i=0;i<6;i++)
    {
        val[i]=val[i]*val[i];
        sum+=val[i];
    }
    printf("The sum of squares = %d\n",sum);
}
```

**输出：**

The sum of squares = 91
The contents of array are now : 1 4 9 16 25 36

这里我们可以看到，在被调用函数内部对数组所做的更改会反映在调用函数中。形式参数的名称不同，但它引用的是原始数组。

由于在函数定义中不必指定数组的大小，因此我们可以编写能够处理相同类型但不同大小数组的通用函数。例如，在下一个程序中，函数add()能够对任意大小的整数数组的元素进行求和。

```c
/*P7.10 程序：使用一个可处理不同大小数组的通用函数*/
#include<stdio.h>
main()
{
    int a[5]={2,4,6,8,10};
    int b[8]={1,3,5,7,9,11,13,15};
    int c[10]={1,2,3,4,5,6,7,8,9,10};
    printf("Sum of elements of array a : %d\n",add(a,5));
    printf("Sum of elements of array b : %d\n",add(b,8));
    printf("Sum of elements of array c : %d\n",add(c,10));
}
add(int arr[],int n)
{
    int i,sum=0;
    for(i=0;i<n;i++)
        sum+=arr[i];
    return sum;
}
```

**输出：**

Sum of elements of array a : 30
Sum of elements of array b : 64
Sum of elements of array c : 55

## 7.2 二维数组

### 7.2.1 二维数组的声明与访问单个元素

二维数组的声明语法与一维数组类似，但这里有两个下标。

`data_type array_name[行数][列数];`

这里行数指定数组的行数，列数表示数组中的列数。数组中元素的总数为行数 * 列数。例如：

`int arr[4][5];`

这里arr是一个有4行5列的二维数组。该数组的单个元素可以通过使用两个下标来访问，其中第一个下标表示行号，第二个下标表示列号。该数组的起始元素是arr[0][0]，最后一个元素是arr[3][4]。此数组中的元素总数为4*5 = 20。

