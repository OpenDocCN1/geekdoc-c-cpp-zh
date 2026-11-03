
```c
func(int a[])
{
    int i;
    printf("Inside func() : ");
    for(i=0;i<5;i++)
    {
        a[i]=a[i]*2;
        printf("%d",a[i]);
    }
    printf("\n");
}
```

# 输出：

Inside func() : 5 8 4 9 3
Inside main() : 5 8 4 9 3

现在，在学习指针之后，我们已经能够理解当数组传递给函数时实际发生了什么。用于接收数组的形式参数有三种声明方式。我们可以将其声明为无大小数组或有大小数组，也可以将其声明为指针。

```c
func(int a[])
{
    ....
}
func(int a[5])
{
    ....
}
func(int *a)
{
    ....
}
```

在这三种情况下，编译器在函数内部都只为指针变量保留空间。在函数调用中，数组名不带任何下标或地址运算符传递。由于数组名表示数组第一个元素的地址，因此该地址被赋给函数中的指针变量。所以在函数内部，我们有一个包含数组基地址的指针。

在上面的程序中，参数 a 被声明为基类型为 int 的指针变量，并用数组 arr 的基地址初始化。我们已经学过，如果有一个包含数组基地址的指针变量，那么我们可以通过指针表示法或下标表示法访问任何数组元素。所以在函数内部，我们可以通过写 *(a+i) 或 a[i] 来访问 arr 的第 i 个元素。由于我们直接访问原始数组，因此对被调用函数中的数组所做的所有更改都会反映到调用函数中。

![](img/a76c706396af8b310f291a5313a27079_239_0.png)

下面的程序将说明我们讨论过的这一点。

```
/*P8.21 Program to verify the fact that when an array is passed to a function, the receiving argument is declared as a pointer */
#include<stdio.h>
main()
{
    float f_arr[5]={1.4,2.5,3.7,4.1,5.9};
    int i_arr[5]={1,2,3,4,5};
    char c_arr[5]={'a','b','c','d','e'};
    printf("Inside main() : ");
    printf("Size of arr = %u\t",sizeof(f_arr));
    printf("Size of arr = %u\t",sizeof(i_arr));
    printf("Size of arr = %u\n",sizeof(c_arr));
    func(f_arr,i_arr,c_arr);
}
func(float f [],int *i,char c[5])
{
    printf("Inside func() : ");
    printf("Size of f = %d\t",sizeof(f));
    printf("Size of i = %d\t",sizeof(i));
    printf("Size of c = %d\n",sizeof(c));
}
```

输出：
    Inside main() : Size of f_arr = 20          Size of i_arr = 10          Size of c_arr = 5
    Inside func() : Size of f = 2               Size of i = 2               Size of c = 2

在函数 func( ) 内部，f、i、c 被声明为指针，这一点从它们每个的大小都是 2 字节可以明显看出。

## 8.18 将二维数组传递给函数

我们在上一章已经学过，每当多维数组传递给函数时，最左边的维度可以省略，但所有其他维度都必须指定。因此，如果我们有一个 3 行 4 列的二维数组，那么接受它的函数定义可以写成以下两种方式：

```
func(int a[3][4])
{
```

```
}
func(int a[][4])
{
    -----
}
```

在函数中对数组所做的任何更改都会反映到调用函数中。

每当二维数组传递给函数时，函数实际上接收的是一个指向一维数组的指针，其中一维数组的大小等于列数。例如在上面的情况中，函数接收的是一个指向包含 4 个整数的数组的指针。因此我们也可以按这种形式编写函数定义：

```c
func(int (*a)[4])
{
    -----
}
```

这里 a 被声明为指向包含 4 个整数的数组的指针，并用原始二维数组的基地址初始化。现在在函数内部，我们可以使用指针表示法或下标表示法来访问元素。下面的程序将把这些点讲清楚。

```c
/*P8.22 Program to pass a 2-D array to a function*/
#include<stdio.h>
main()
{
    int i,j,arr[3][4]={ 
                    (11,12,13,14),
                    (15,16,17,18),
                    (19,20,21,22),
                    };
    printf("Inside main() : sizeof(arr) = %u\n",sizeof(arr));
    func(arr);
    printf("Contents of array after calling func() are :\n");
    for(i=0;i<3;i++)
    {
        for(j=0;j<4;j++)
            printf("%d ",arr[i][j]);
        printf("\n");
    }
}
func(int (*a)[4])
{
    int i,j;
    printf("Inside func() : sizeof(a) = %u\n",sizeof(a));
    printf("Inside func() : sizeof(*a) = %u\n",sizeof(*a));
    for(i=0;i<3;i++)
        for(j=0;j<4;j++)
            a[i][j]=a[i][j]+2;
}
```

# 输出：

Inside main() : sizeof(arr) = 24

Inside func() : sizeof(a) = 2
Inside func() : sizeof(*a) = 8
Contents of array after calling func() are -
13 14 15 16
17 18 19 20
21 22 23 24

![](img/a76c706396af8b310f291a5313a27079_241_0.png)

## 8.19 指针数组

我们可以声明一个以指针为元素的数组。这个数组的每个元素都是一个指针变量，可以保存适当类型任何变量的地址。声明指针数组的语法与声明数组类似，只是在数组名之前放置一个星号。

datatype *arrayname[size];

例如，要声明一个包含整数指针、大小为 10 的数组，我们可以写：
int *arrp[10];

```
/*P8.23 Program for understanding the concept of array of pointers*/
#include<stdio.h>
main()
{
    int *pa[3];
    int i,a=5,b=10,c=15;
    pa[0]=&a;
    pa[1]=&b;
    pa[2]=&c;
    for(i=0;i<3;i++)
    {
        printf("pa[%d] = %u\t",i,pa[i]);
        printf("*pa[%d] = %d\n",i,*pa[i]);
    }
}
```

输出：

pa[0] = 2012    *pa[0] = 5
pa[1] = 2560    *pa[1] = 10
pa[2] = 3020    *pa[2] = 15

![](img/a76c706396af8b310f291a5313a27079_242_0.png)

这里 pa 被声明为指针数组。这个数组的每个元素都是指向整数的指针。pa[i] 给出 ‘pa’ 的第 i 个元素的值，该值是某个 int 变量的地址，而 *pa[i] 给出该 int 变量的值。

指针数组也可以包含另一个数组元素的地址。

```
/*P8.24 Program for understanding array of pointers*/
#include<stdio.h>
main()
{
    int i,arr[4]={5,10,15,20};
    int *pa[4];
    for(i=0;i<4;i++)
        pa[i] = &arr[i];
    for(i=0;i<4;i++)
    {
        printf("pa[%d] = %u\t",i,pa[i]);
        printf("*pa[%d] = %d\n",i,*pa[i]);
    }
}
```

# 输出：

pa[0] = 1000    *pa[0] = 5
pa[1] = 1002    *pa[1] = 10
pa[2] = 1004    *pa[2] = 15
pa[3] = 1006    *pa[3] = 20

这里 'pa' 被声明为指针数组。这个数组的每个元素都包含数组 'arr' 的每个元素的地址。

![](img/a76c706396af8b310f291a5313a27079_242_1.png)

现在我们取一个 3 行 4 列的二维数组 arr。声明一个大小为 3 的指针数组，并将该数组中每个指针赋为二维数组每一行第 0 个元素的地址，即 pa 的第 i 个元素是指向二维数组第 i 行第 0 个元素的指针。这可以这样做：

```
int arr[3][4]={{10,11,12,13},{20,21,22,23},{30,31,32,33}};
int *pa[3];
for(i=0;i<3;i++)
    pa[i]=arr[i];
```

![](img/a76c706396af8b310f291a5313a27079_243_0.png)

现在让我们看看如何使用指针数组 pa 访问二维数组 arr 的元素。pa[0] 是指向数组 arr 的第 0 个一维数组第 0 个元素的指针，类似地，pa[i] 将是指向第 i 个一维数组第 0 个元素的指针。

由于指针 pa[i] 的基类型是 int，所以如果我们想要第 i 个一维数组第 j 个元素的地址，那么我们可以将 j 加到表达式 pa[i] 上。因此表达式 pa[i]+j 将给出第 i 个一维数组第 j 个元素的地址。所以表达式 *(pa[i]+j) 将给出第 i 个一维数组第 j 个元素的值。

我们知道 pa[i] 等价于 *(pa+i)。因此上面的表达式可以写成 *((pa+i)+j)，并且我们知道这个表达式等价于 pa[i][j]。所以最后我们可以通过写 pa[i][j] 来访问第 i 个一维数组的第 j 个元素。

```
/*P8.25 program for understanding array of pointers*/
#include<stdio.h>
main()
{
    int i,j,arr[3][4]={{10,11,12,13},{20,21,22,23},{30,31,32,33}};
    int *pa[3];
    for(i=0;i<3;i++)
        pa[i]=arr[i];
    for(i=0;i<3;i++)
    {
        for(j=0;j<4;j++)
            printf("%d ",pa[i][j]);
        printf("\n");
    }
}
```

# 输出：

10 11 12 13
20 21 22 23
30 31 32 33

## 8.20 void 指针

我们已经学习过，应该给指针分配与指针声明中所述类型相同的地址。
