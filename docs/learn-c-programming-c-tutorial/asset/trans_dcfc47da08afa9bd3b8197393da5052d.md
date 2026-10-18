

当上述代码被编译并执行时，会产生以下结果：

```text
Address of var[0] = bf882b30
Value of var[0] = 10
Address of var[1] = bf882b34
Value of var[1] = 100
Address of var[2] = bf882b38
Value of var[2] = 200
```

## 递减指针

递减指针时也是如此，指针的值会按其数据类型所占的字节数减少，如下所示：

```c
#include <stdio.h>

const int MAX = 3;

int main ()
{
    int var[] = {10, 100, 200};
    int i, *ptr;

    /* let us have array address in pointer */
    ptr = &var[MAX-1];
    for ( i = MAX; i > 0; i--)
    {
        printf("Address of var[%d] = %x\n", i, ptr );
        printf("Value of var[%d] = %d\n", i, *ptr );

        /* move to the previous location */
        ptr--;
    }
    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```text
Address of var[3] = bfedbcd8
Value of var[3] = 200
Address of var[2] = bfedbcd4
Value of var[2] = 100
Address of var[1] = bfedbcd0
Value of var[1] = 10
```

## 指针比较

指针可以使用关系运算符进行比较，例如 ==、< 和 >。如果 p1 和 p2 指向彼此相关的变量，例如同一数组中的元素，那么 p1 和 p2 就可以进行有意义的比较。

下面的程序修改了前面的示例——通过递增指针变量，只要它指向的地址小于或等于数组最后一个元素的地址（即 &var[MAX - 1]）：

```c
#include <stdio.h>

const int MAX = 3;

int main ()
{
    int var[] = {10, 100, 200};
    int i, *ptr;

    /* let us have address of the first element in pointer */
    ptr = var;
    i = 0;
    while ( ptr <= &var[MAX - 1] )
    {

        printf("Address of var[%d] = %x\n", i, ptr );
        printf("Value of var[%d] = %d\n", i, *ptr );

        /* point to the next location */
        ptr++;
        i++;
    }
    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```text
Address of var[0] = bfdbcb20
Value of var[0] = 10
Address of var[1] = bfdbcb24
Value of var[1] = 100
Address of var[2] = bfdbcb28
Value of var[2] = 200
```

在我们理解指针数组的概念之前，先来看一个使用包含 3 个整数的数组的示例：

```c
#include <stdio.h>

const int MAX = 3;

int main ()
{
    int var[] = {10, 100, 200};
    int i;

    for (i = 0; i < MAX; i++)
    {
        printf("Value of var[%d] = %d\n", i, var[i] );
    }
    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```text
Value of var[0] = 10
Value of var[1] = 100
Value of var[2] = 200
```

有时我们可能需要维护一个数组，该数组可以存储指向 int、char 或任何其他可用数据类型的指针。下面是指向整数的指针数组的声明：

```c
int *ptr[MAX];
```

它将 **ptr** 声明为包含 MAX 个整数指针的数组。因此，ptr 中的每个元素都保存着一个指向 int 值的指针。下面的示例使用了三个整数，它们存储在一个指针数组中，如下所示：

```c
#include <stdio.h>

const int MAX = 3;

int main ()
{
    int var[] = {10, 100, 200};
    int i, *ptr[MAX];

    for ( i = 0; i < MAX; i++)
    {
        ptr[i] = &var[i]; /* assign the address of integer. */
    }

    for ( i = 0; i < MAX; i++)
    {
        printf("Value of var[%d] = %d\n", i, *ptr[i] );
    }
    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```text
Value of var[0] = 10
Value of var[1] = 100
Value of var[2] = 200
```

你也可以使用字符指针数组来存储字符串列表，如下所示：

```c
#include <stdio.h>

const int MAX = 4;

int main ()
{
    char *names[] = {
                    "Zara Ali",
                    "Hina Ali",
                    "Nuha Ali",
                    "Sara Ali",
                };
    int i = 0;

    for ( i = 0; i < MAX; i++)
    {
        printf("Value of names[%d] = %s\n", i, names[i] );
    }
    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```text
Value of names[0] = Zara Ali
Value of names[1] = Hina Ali
Value of names[2] = Nuha Ali
Value of names[3] = Sara Ali
```

## 指向指针的指针

指向指针的指针是一种多级间接寻址形式，或者说是指针链。通常，指针包含一个变量的地址。当我们定义一个指向指针的指针时，第一个指针包含第二个指针的地址，而第二个指针则指向包含实际值的位置，如下所示。

![](img/6e49c39a6ef9e32d938b03dc613e44f6_119_0.png)

作为指向指针的指针的变量必须这样声明。做法是在其名称前额外放置一个星号。例如，下面的声明声明了一个指向 int 类型的指针的指针：

```c
int **var;
```

当一个目标值被指向指针的指针间接指向时，访问该值需要对星号运算符应用两次，如下面的示例所示：

```c
#include <stdio.h>

int main ()
{
    int  var;
    int *ptr;
    int **pptr;

    var = 3000;

    /* take the address of var */
    ptr = &var;

    /* take the address of ptr using address of operator & */
    pptr = &ptr;

    /* take the value using pptr */
    printf("Value of var = %d\n", var );
    printf("Value available at *ptr = %d\n", *ptr );
    printf("Value available at **pptr = %d\n", **pptr);

    return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

```text
Value of var = 3000
Value available at *ptr = 3000
Value available at **pptr = 3000
```

## 向函数传递指针

C 语言允许将指针传递给函数。要做到这一点，只需将函数参数声明为指针类型。

下面是一个简单的示例，我们将一个指向 unsigned long 的指针传递给函数，并在函数内部修改该值，这个修改会反映回调用函数中：

```c
#include <stdio.h>
#include <time.h>

void getSeconds(unsigned long *par);

int main ()
{
    unsigned long sec;

    getSeconds( &sec );

    /* print the actual value */
    printf("Number of seconds: %ld\n", sec );

    return 0;
}

void getSeconds(unsigned long *par)
{
    /* get the current number of seconds */
    *par = time( NULL );
    return;
}
```

![](img/6e49c39a6ef9e32d938b03dc613e44f6_120_0.png)

当上述代码被编译并执行时，会产生以下结果：

```text
Number of seconds: 1294450468
```

一个能够接受指针的函数，也可以接受数组，如下面的示例所示：

```c
#include <stdio.h>

/* function declaration */
double getAverage(int *arr, int size);

int main ()
{
    /* an int array with 5 elements */
    int balance[5] = {1000, 2, 3, 17, 50};
    double avg;

    /* pass pointer to the array as an argument */
    avg = getAverage( balance, 5 ) ;

    /* output the returned value */
    printf("Average value is: %f\n", avg );

    return 0;
}

double getAverage(int *arr, int size)
{
    int i, sum = 0;
    double avg;

    for (i = 0; i < size; ++i)
    {
        sum += arr[i];
    }

    avg = (double)sum / size;

    return avg;
}
```

![](img/6e49c39a6ef9e32d938b03dc613e44f6_121_0.png)

当上述代码一起编译并执行时，会产生以下结果：

```text
Average value is: 214.400000
```

## 从函数返回指针

在上一章中，我们已经了解了 C 语言如何允许函数返回数组。类似地，C 语言也允许函数返回指针。要做到这一点，你需要像下面的示例那样声明一个返回指针的函数：

```c
int * myFunction()
{
    .
    .
    .
}
```

需要记住的第二点是，在函数外部返回局部变量的地址并不是一个好主意，因此你必须将局部变量定义为静态变量（static）。

现在，考虑下面的函数，它将生成 10 个随机数，并使用一个表示指针的数组名（即第一个数组元素的地址）来返回这些随机数。

```c
#include <stdio.h>
#include <time.h>

/* function to generate and return random numbers. */
int * getRandom( )
{
    static int r[10];
    int i;
}
```

![](img/6e49c39a6ef9e32d938b03dc613e44f6_122_0.png)

