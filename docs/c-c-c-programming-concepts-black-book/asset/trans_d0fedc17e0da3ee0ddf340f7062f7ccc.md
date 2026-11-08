
```c
            {
                {4,40,400},
                {5,50,500},
                {6,60,600}
            },
            {
                {7,70,700},
                {8,80,800},
                {9,90,900}
            }
        };
        return (int(*)[3][3])array_D;
}

int main()
{
    int *ptr_A,*ptr_temp;
    int (*ptr_B)[3];
    int (*ptr_C)[3][3];
    int (*ptr_D)[3][3][3];
    int i,j,k;

    printf("\nFirst method of returning \n");

    ptr_A = funcType_A();
    for(i=0;i < 3; i++)
    {
        for(j=0;j < 3 ;j++)
        {
            for(k=0; k < 3;k++)
            {
                printf("%d ",*(ptr_A + i*3*3 + j*3 + k));
            }
            printf("\n");
        }
        printf("\n");
    }

    printf("\nSecond method of returning\n");

    ptr_B = funcType_B();
    for(i=0;i < 3; i++)
    {
        ptr_temp = (int*)(ptr_B+i*3);

        for(j=0;j < 3 ;j++)
        {
            for(k=0; k < 3;k++)
            {
                printf("%d ",*ptr_temp);
                ptr_temp++;
            }
            printf("\n");
        }
        printf("\n");
    }

    printf("\nThird method of returning\n");
    ptr_C = funcType_C();

    for(i=0;i < 3; i++)
    {
        ptr_temp = (int*)(ptr_C + i);

        for(j=0; j < 3 ;j++)
        {
            for(k=0; k < 3;k++)
            {
                printf("%d ",*ptr_temp);
                ptr_temp++;
            }
            printf("\n");
        }
        printf("\n");
    }

    printf("\nFourth method of returning\n");
    ptr_D = funcType_D();

    for(i=0;i < 3; i++)
    {
        for(j=0; j < 3 ;j++)
        {
            for(k=0; k < 3;k++)
            {
                printf("%d ",(*ptr_D)[i][j][k]);
            }
            printf("\n");
        }
        printf("\n");
    }
    getch();
}
```

上述代码的输出如下：

```text
First method of returning
1 10 100
2 20 200
3 30 300

4 40 400
5 50 500
6 60 600

7 70 700
8 80 800
9 90 900

Second method of returning
1 10 100
2 20 200
3 30 300

4 40 400
5 50 500
6 60 600

7 70 700
8 80 800
9 90 900

Third method of returning
1 10 100
2 20 200
3 30 300

4 40 400
5 50 500
6 60 600

7 70 700
8 80 800
9 90 900

Fourth method of returning
1 10 100
2 20 200
3 30 300

4 40 400
5 50 500
6 60 600

7 70 700
8 80 800
9 90 900
```

下一节，我们将学习指针数组。

## 指针数组

与整数数组、浮点数数组和字符数组类似，C语言中也有指针数组。指针保存的是内存位置的地址；因此，指针数组不过是此类地址的集合。普通数组上可以执行的所有操作，在指针数组上也可以执行。清单4.13展示了指针数组的用法：

### 清单 4.13：展示指针数组的用法

```c
#include<stdio.h>
int main()
{
    int *array_ptr[3];
    int i=1,j=2,k=3;
    int ct;
    array_ptr[0]=&i;
    array_ptr[1]=&j;
    array_ptr[2]=&k;

    for(ct=0; ct < 3 ;ct++)
    {
        printf("\n Address [%u] Value [%d]",
               array_ptr[ct],*array_ptr[ct]);
    }
    getch();
}
```

在清单4.13中，`array_ptr` 变量被声明为指针数组，其中数组的每个单元格都将保存一个指向整数的指针。我们还声明了三个整数，并将它们的内存地址存入该指针数组。请注意，当我们显示数组内容时，得到的是这些变量的地址。我们可以通过使用解引用运算符来显示内存位置的内容。

上述代码的输出如下：

```text
Address [2293596] Value [1]
Address [2293592] Value [2]
Address [2293588] Value [3]
```

在学习了指针数组之后，你一定会想：指针数组和指向数组的指针之间是否有任何区别。为此，让我们考虑以下两种表示法：

```c
int *array_ptr[5];

int (*array_ptr)[5];
```

第一种表示法声明一个大小为五的整型指针数组。在这种情况下，内存分配在声明时就已经完成。然而，第二种表示法声明一个指向包含五个整数的数组的指针，但不分配任何内存。由于圆括号具有更高的优先级；因此，在第二种声明中，首先将 `array_ptr` 声明为指针，然后将其关联到包含五个整数的数组。类似地，以下表示法声明一个指向数组的指针，但分配是静态的：

```c
int array_ptr[10];
```

清单4.14展示了指向数组的指针的用法：

### 清单 4.14：展示指向数组的指针的用法

```c
#include<stdio.h>

int main()
{
    int *array_a[2];
    int (*array_b)[2];
    int array_c[2] = {1,2};
    int var_a = 10;
    int var_b = 20;

    array_a[0] = &var_a;
    array_a[1] = &var_b;
    array_b = &(array_c);
    printf("\n Size of a [%d] ",sizeof(array_a));
    printf("\n Size of b [%d] ",sizeof(array_b));
    printf("\n Size of b [%d] ",sizeof(array_c));
    printf("\n Value at array_a is %d ",*(array_a[0]));
    printf("\n Value at array_a is %d ",*(array_a[1]));
    printf("\n Address of array_b [%p] ",array_b);
    printf("\n Address of array_c [%p] ",&array_c);
    printf("\n Value at array_b is %d ",*(array_b[0]));
}
```

在清单4.14中，我们将 `array_c` 的地址赋给了 `array_b`，而 `array_b` 恰好是一个指向整数数组的指针。此外，我们还借助 `array_b` 访问了 `array_c` 的元素。

前面的语句准确告诉函数指针它需要指向哪个函数。最终，将执行以下函数调用：

```c
(*func_ptr)();
```

在借助函数指针调用函数时，我们应注意圆括号的用法。一个典型的错误调用如下：

```c
*func_ptr()  -  Error.
```

这将意味着我们调用 func_ptr() 函数，而该函数将返回一个指针。我们还可以使用函数指针向目标函数传递参数。

要处理函数指针，值得一提的是，应当知道声明、赋值和调用函数指针的正确方式；否则，可能会导致严重的歧义。函数指针最简单的定义如下：

```c
int (*func_ptr)()
```

前面的语句将 func_ptr 声明为指向函数的指针，该函数将返回一个整数。从声明中可以明显看出，* 运算符表示涉及指针，而圆括号表示函数。然而，一个有趣的因素是 *func_ptr 周围圆括号的用法。其原因只是为了确保声明中的优先级关系。如果我们不提供圆括号，那么声明将如下所示：

```c
int *func_ptr() /* Incorrect declaration */
```

前面的语句将意味着 func_ptr 是一个返回指向整数的指针的函数。因此，圆括号有助于表明 func_ptr 首先是一个指针，然后是一个指向返回整数的函数的指针。为了避免任何此类语法异常，最好按如下方式使用 typedef：

```c
typedef int (*func_ptr)()
```

前面的语句意味着 func_ptr 等价于指向返回整数的函数的指针。

现在，让我们借助一个示例来讨论函数指针赋值的各种特性。考虑前面包含 typedef 的函数指针声明。在这种情况下，我们想要将以下函数赋给一个函数指针：

```c
int my_function1();
int my_function2();
```

我们可以直接按如下方式赋第一个函数的地址：

```c
func_ptr = &my_function1;
```

否则，赋值可以是有条件的，如下所示：

```c
if(cond)
    func_ptr = &my_function1;
else
    func_ptr = &my_function2;
```

函数指针赋值最有趣的方面之一是：将函数赋给函数指针时，并不总是必须使用 & 运算符。当我们使用函数名而不是调用函数本身时，它会被解释为我们使用它是为了将其赋给函数指针。大多数函数指针赋值都采用标准语法，其中会省略 & 的使用。因此，以下代码将编译通过而不会产生任何错误：

```c
func_ptr = my_function1;
```

现在，让我们讨论函数指针的一些复杂声明。以下代码片段展示了一个函数指针声明。

```c
typedef int (*func_ptr)(float, float);
func_ptr fp1;
```

在前面的代码片段中，fp1 成为一个指向函数的指针，该函数接受两个 float 变量作为参数并返回一个整数。

