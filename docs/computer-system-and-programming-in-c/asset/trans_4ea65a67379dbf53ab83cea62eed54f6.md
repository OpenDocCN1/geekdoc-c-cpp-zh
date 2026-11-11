
在Java中，错误的解引用会被运行时系统礼貌地标记出来。在C、C++和Pascal等编译型语言中，错误的解引用有时会导致程序崩溃，有时又会以某种微妙、随机的方式破坏内存。因此，编译型语言中的指针错误可能很难追踪。

## 指针赋值

两个指针之间的**指针赋值**会使它们指向同一个指针所指对象。因此，赋值`y = x;`会使`y`与`x`指向同一个所指对象。

指针赋值不会触及所指对象。它只是将一个指针改为与另一个指针具有相同的引用。指针赋值之后，这两个指针就被称为“共享”同一个所指对象。

## 指针算术

指针变量也可以用于算术表达式。可以对指针执行以下操作。

- 1. 指针可以递增或递减，以指向不同的位置，例如

  ```
  ptr1 = ptr2 + 4;
  ptr++;
  --ptr;
  ```

  但是，`ptr++`会使指针`ptr`指向其类型的下一个地址值。

  例如，如果`ptr`是一个指向float的指针，初始值为65526，那么在执行`ptr++`或`ptr = ptr+1`之后，`ptr`的值将变为65530。因此，如果我们递增或递减一个指针，其值会按它所指向的数据类型的长度增加或减少。

- 2. 如果`ptr1`和`ptr2`是正确声明并初始化的指针，则以下操作是有效的：

  ```
  res = res + *ptr1;
  *ptr1 = *ptr2 + 5;
  prod = *ptr1 * *ptr2;
  quo = *ptr1 / *ptr2;
  ```

  注意，最后一条语句中`/`和`*`之间有一个空格，因为如果你连写`/*`，它会被视为注释的开始，导致该语句失败。

- 3. 像`ptr1 = ptr2`、`ptr1 < ptr2`和`ptr2 != ptr1`这样的表达式是允许的，前提是指针`ptr1`和`ptr2`指向相同或相关的变量。这些比较在处理数组时很常见。

## 不能对指针执行的操作

假设`p1`和`p2`是指向相关变量的指针。以下操作不能用于指针：

- 1. 指针变量不能相加。例如，`p1 = p1 + p2`是无效的。
- 2. 不允许将指针与常量相乘或相除。例如，`p1 * p2`或`p2 / 5`是无效的。
- 3. 当指针的值被引用，但该指针并未指向一个有效的内存块时，就会发生无效的指针引用。假设`p`和`q`是两个指针。如果我们在`q`未初始化时执行`p = q`，那么指针`p`也会变成未初始化，此时对`*p`的任何引用都是无效的指针引用。

**注意：** 一旦我们创建了一个指向某个变量的指针，我们可以将它重新赋值为另一个变量的地址，也可以通过执行**指针算术**来移动它。

假设我们有一个int指针ptr。如果我们执行`ptr++`、`++ptr`或`ptr+=1`，实际上是将指针向前移动2个字节（即其数据类型的大小）。因此，它将指向计算机内存中的其他位置。

类似地，`ptr--`、`--ptr`和`ptr-=1`会将int指针“向后”移动2个字节。

而且你也不限于以1为步长移动：`ptr+=n`会将它“向前”移动`n*2`个字节（假设ptr是int指针）。数据类型越大，步长越大。所以如果ptr是一个double指针，`ptr-=3`会将它“向后”移动`3*8 = 24`个字节。

可用于指针的算术赋值运算符是`+=`和`-=`。不能使用`ptr*=2`和`ptr/=2`！

## 示例

以下是指针算术的示例。

### 示例1

```
char s[100];
char *ptr = s;
ptr += 1;
```

### 解决方案

我假设ptr增加1个字节，指向数组中的第2个元素，因为字符数组每个字符占用1个字节。

### 示例2

```
int i[100]; // suppose the size of an int is 4 bytes
int *ptr = i;
ptr += 1;
```

### 解决方案

由于数据类型是整数类型，占用4个字节，所以这里ptr增加4个字节。

### 示例3

```
int i[100];
void *ptr = i;
ptr += 1; // So how many bytes is the ptr increased by here?
// Will it point to the 2nd element of the array.
```

### 解决方案

如果我知道数组中元素的字节大小，但不知道实际类型。我怎样才能让`void *`指针指向数组的下一个元素呢？

## 将指针传递给函数

我们知道，在函数中，参数通常可以通过以下两种方式之一传递给函数：

- 1. 按值传递方法
- 2. 按引用传递方法

在第一种方法中，当参数按值传递时，实际参数的值的一份副本被传递给被调函数。因此，函数内对变量所做的任何更改都不会影响实际参数列表中的变量。

然而，当参数按引用传递时（即，当一个指针作为参数传递给函数时），传递的是变量的地址。无论是在被调函数中还是在调用函数中，都可以自由访问该地址的内容。因此，通过引用调用的函数可以更改调用中使用的变量的值。

下面的程序说明了这种区别。

### 问题1

编写一个程序，使用传值方法和传引用方法交换两个值。

### 解决方案

```
/* Program that illustrates the difference between ordinary arguments, which are passed by value, and pointer arguments, which are passed by reference */
#include <stdio.h>
#include <conio.h>

void swapVal ( int, int ); /* function prototype */
void swapRef ( int*, int* ); /* function prototype */

void main ()
{
    int x = 10;
    int y = 20;
    printf("Pass by Value Method \n");
    printf("Before calling function swapVal x=%d y=%d", x,y);
    swapVal (x, y); /* copy of the arguments are passed */
    printf ("\n after calling function swapVal x=%d y=%d", x,y);
    printf("\n\n pass by Reference Method");
    printf ("\n before calling function swapRef x=%d y=%d",x,y);
    swapRef (&x,&y); /*address of arguments are passed */
    printf("\n after calling function swapRef x=%d y=%d",x,y);
    getch();
}

/* Function using the pass by value method*/
void swapVal (int x, int y)
{
    int temp;
    temp = x;
    x = y;
    y = temp;
    printf ("\nWithin function swapVal x=%d y=%d",x,y);
}

/*Function using the pass by reference method*/
void swapRef (int *px, int *py)
{
    int temp;
    temp = *px;
    *px = *py;
    *py = temp;
    printf ("\nWithin function swapRef *px=%d *py=%d",*px,*py);
}
```

上述代码段的输出如下：

```
Pass by Value Method
Before calling function swapVal x=10 y=20
Within function swapVal x=20 y=10
After calling function swapVal x=10 y=20

Pass by Reference Method
Before calling function swapRef x=10 y=20
Within function swapRef *px=20 *py=10
After calling function swapRef *px=20 *py=10
```

对上述程序段的解释如下：

该程序包含两个函数：*swapVal*和*swapRef*。

在函数*swapVal*中，参数x和y是按*值*传递的。因此，对参数的任何更改都只局限于发生更改的函数内部。注意，即使在函数*swapVal*内部交换了x和y的值，x和y的值仍然保持不变。

现在考虑函数*swapRef*。该函数接收两个指向整数变量的*指针*作为参数，这些参数由声明中出现的间接运算符标识为指针。这意味着在函数*swapRef*中，参数x和y是按*引用*传递的。因此，在函数*swapRef*内部对参数所做的任何更改都会反映到函数*main()*中。注意，在函数调用*swapRef*之后，x和y的值被交换了。

### 返回多个值的函数

使用*按引用调用*方法，我们可以让一个函数一次返回多个值，这在*按值调用*方法中是不可能的。

### 示例

如果我们编写以下函数原型

```
int * sort(int *);
```

这一行的意思是：sort是一个函数，它接受一个整数类型的指针，即一个整数类型的数组，并根据该数组返回一个整数类型的指针，即整个数组。

这个概念通过下面的问题来说明。

### 问题

编写一个程序，输入10个数字，并借助函数按升序打印这些数字，使用带参数并有返回类型的方法。

### 解决方案

```
#include <stdio.h>
#include <conio.h>

int * sort (int *);

void main()
{
    int a[10],*p,i;
    clrscr();
    for(i=0;i<10;i++)
    {
        printf("\n enter the value of a[%d]",i);
        scanf("%d",&a[i]);
    }
    p=sort(a);//Calling of the function
    printf("\n the sorted array is ");
    for(i=0;i<10;i++)
    {
        printf("\n %d",*(p+i));
    }
    getch();
}

int *sort(int *p)
{
    int temp,i,j;
    for(i=0;i<10;i++)
    {
```

