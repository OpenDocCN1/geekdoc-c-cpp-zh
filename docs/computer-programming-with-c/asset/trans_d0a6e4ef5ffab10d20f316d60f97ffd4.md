

while 循环之所以终止，是因为条件 `a[i]!=x` 为假，这意味着 `a[i]==x` 为真，因此元素 x 存在于数组中的位置 i 处。因此，我们在 else 块中打印以下消息：

```c
printf("Element is present at position %d in the array\n", i);
```

## 注意

逻辑运算符 && 和 || 具有短路行为。当两个条件 C1 和 C2 使用 & 运算符连接时，C1 是第一个条件，C2 是第二个条件，如下所示：

`C1&&C2`

**只有当 C1 为真时，C2 才会被求值。** 这是因为，当 C1 为假时，无论 C2 是什么，&& 的最终结果始终为假。因此，如果 C1 为假，C/C++ 的优化器不会对 C2 进行求值。这称为在求值逻辑 && 运算符时的短路行为。在给定的程序中，我们使用 && 运算符连接了两个条件

```c
i<n && a[i]!=x
```

因此，如果 `i<n` 为假，则不会对条件 `a[i]!=x` 进行求值。这是非常重要的一点，因为如果条件 `i<n` 为假，则表示 i 已经越过了数组的边界，因此不应访问 `a[i]`。如果你访问了 `a[i]`，它将会是一个垃圾值，将垃圾值与 x 比较没有任何意义。因此，我们绝不能改变给定程序的 while 循环中指定条件的顺序。

## 例题 6.3

编写一个程序，读取包含 n 个整数的数组，并在不使用任何临时数组的情况下反转数组中元素的顺序。

例如，如果输入的数组为

![](img/57c0d966bb33c67a5a188e6bf39e4e02_285_0.png)

数组中元素的顺序必须反转，如下所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_285_1.png)

```c
#include<stdio.h>
void main()
{
    int n, i, mid, temp, a[100];
    printf("How many elements are to be stored in the array?\n");
    scanf("%d",&n);
    printf("Enter the %d elements\n",n);
    /*Input the array elements*/
    for(i=0;i<=n-1;i++)
    {
        scanf("%d",&a[i]);
    }
    /*Calculate the midpoint of the array*/
    if( n%2 == 0 )
    {
        mid = n/2 - 1;
    }
    else
    {
        mid = n/2;
    }
    /*Swap the left side of the array with right side of the array*/
    for ( i = 0 ; i < mid ; i++ )
    {
        temp = a[i];
        a[i] = a[n-i-1];
        a[n-i-1] = temp;
    }
    printf("Reverse of the array is\n");
    for( i = 0 ; i < n ; i++ )
    {
        printf("%d ",a[i]);
    }
}
```

### 输出

```text
How many elements are to be stored in the array?
5
Enter the 5 elements
10 20 30 40 50
Reverse of the array is
50 40 30 20 10
```

### 草稿

> 要反转数组中元素的顺序，我们将数组左半部分存储的元素与数组右半部分对应的元素进行交换。

例如，如果数组大小为 5，我们将 a[0] 与 a[4] 交换，并将 a[1] 与 a[3] 交换。

注意，中间元素（即 30）的位置不受交换操作的影响。

下面给出了用于执行反转数组所需交换操作的 for 循环：

```c
for( i = 0 ; i < mid ; i++ )
{
    temp = a[i];
    a[i] = a[n-i-1];
    a[n-i-1] = temp;
}
```

变量 mid 表示数组中心元素的位置。变量 mid 将计算为 n/2 - 1（如果数组长度为偶数）或 n/2（如果数组长度为奇数）。这是因为数组索引总是从 0 开始。例如，如果数组长度为 5，则中点将计算为

```c
mid = 5/2 = 2
```

另一方面，如果数组长度为 6，则 mid 的位置将按如下方式计算：

```c
mid = 6/2 - 1 = 2
```

## 例题 6.4

编写一个程序，从用户那里获取两个向量作为输入，并计算这两个向量的标量积。

```c
#include<stdio.h>
void main()
{
    int n, i, v1[100], v2[100], scalar_prod = 0;
    printf("Enter the number of elements in each of the vectors\n");
    scanf("%d",&n);
    /*Input the first vector from the user*/
    printf("Enter the first vector\n");
    for(i=0;i<=n-1;i++)
    {
        scanf("%d",&v1[i]);
    }
    /*Input the second vector from the user*/
    printf("Enter the second vector\n");
    for(i=0;i<=n-1;i++)
    {
        scanf("%d",&v2[i]);
    }
    /*Calculate the scalar product of the vectors*/
    for(i=0;i<=n-1;i++)
    {
        scalar_prod = scalar_prod + v1[i] * v2[i];
    }
    printf("Scalar product is %d", scalar_prod);
}
```

### 输出

```text
Enter the number of elements in each of the vectors
4
Enter the first vector
10 20 30 40
Enter the second vector
5 10 15 20
Scalar product is 1500
```

## 例题 6.5

编写一个程序，如果 X 和 Y 是两个各包含 n 个整数的集合，则计算以下表达式的结果。

∑Xᵢ + ∑Yᵢ − √|∑Xᵢ|

```c
#include<stdio.h>
#include<math.h>
void main()
{
    int n, i, x[100], y[100], sumX = 0, sumY = 0, absX;
    float result;
    printf("Enter the number of elements to be stored in each of the arrays\n");
    scanf("%d",&n);
    printf("Enter the %d elements of array x\n",n);
    for(i=0;i<=n-1;i++)
    {
        scanf("%d",&x[i]);
        /*calculate sum of x in parallel*/
        sumX = sumX + x[i];
    }
    printf("Enter the %d elements of array y\n",n);
    for(i=0;i<=n-1;i++)
    {
        scanf("%d",&y[i]);
        /*calculate the sum of y in parallel*/
        sumY = sumY + y[i];
    }
    /*Find absolute of sum of X elements*/
    absX = abs(sumX);
    /*Calculate the resultant expression*/
    result = sumX + sumY + sqrt(absX);
    printf("Result is %f\n",result);
}
```

### 输出

```text
Enter the number of elements to be stored in each of the arrays
5
Enter the 5 elements of array x
10 20 30 40 50
Enter the 5 elements of array y
12 45 67 88 2
Result is 376.247437
```

## 例题 6.6

编写一个程序，从用户那里获取一个数组作为输入，并通过接受旋转因子作为用户输入，将数组中的元素向右旋转。

假设，提供给程序的原始数组如下：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_289_0.png)

如果我们对数组应用右旋转，经过一轮旋转后数组的状态将如下所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_290_0.png)

**图 6.43：** 经过第一轮右旋转后数组的状态

请注意，原为数组第一个元素的 10 现在变成了最后一个元素，其余元素则如图 6.43 所示向前移动。如果再应用一轮右旋转，数组的新状态将如下所示：

![](img/57c0d966bb33c67a5a188e6bf39e4e02_290_1.png)

**图 6.44：** 经过第二轮右旋转后数组的状态

因此，经过两轮之后，30 成为数组的第一个元素，20 成为最后一个元素，如图 6.44 所示。要应用于数组的旋转轮数由旋转因子指定。如果旋转因子为 m，则程序应对数组 a 应用 m 轮旋转。程序应从用户那里获取以下输入：

- 1. 数组 a 的大小。
- 2. 数组 a 的元素。
- 3. 旋转因子 m，用于指定要对数组 a 执行的右旋转轮数。

程序应在应用 m 轮旋转后，在计算机屏幕上打印结果数组 a。

```c
#include<stdio.h>
void main()
{
    int n, i, k, m, temp[100], a[100];
    printf("How many elements are to be stored in the array\n");
    scanf("%d",&n);
    /*read the array of n elements*/
    printf("Enter the %d elements\n",n);
    for(i=0;i<=n-1;i++)
    {
        scanf("%d",&a[i]);
    }
    printf("Enter the amount by which rotation is to be applied\n");
    scanf("%d",&m);
    /*copy the first m elements of the array into temp folder*/
    for(i=0;i<=m-1;i++)
    {
        temp[i] = a[i];
    }
    /*left shift the remaining elements*/
    for(i=0;i<=n-m-1;i++)
    {
        a[i] = a[i+m];
    }
    /*copy the array temp as the last m elements of the array*/
    k=0;
    for(i= n-m;i<=n-1;i++)
    {
        a[i] = temp[k];
        k++;
    }
    /*Print the result*/
    printf("The array elements after rotation are \n");
    for(i=0;i<=n-1;i++)
    {
        printf("%d ",a[i]);
    }
}
```

### 输出

```text
How many elements are to be stored in the array?
5
Enter the 5 elements
10 20 30 40 50
Enter the amount by which rotation is to be applied
2
The array elements after rotation are
30 40 50 10 20
```

