
| `i_first` | `i_second` | `c_operator` | `i_first` | `i_second` | `c_operator` | `i_result` |

| 45 | 25 | + | 45 | 25 | + | 70 |

| 45 | 25 | - | 45 | 25 | - | 20 |

| 45 | 25 | * | 45 | 25 | * | 1125 |

| 45 | 25 | / | 45 | 25 | / | 1 |

| 45 | 25 | % | 45 | 25 | % | 20 |

表 3 展示了当函数调用按情况 2 进行时，程序 4 的输出结果：

### 表 3：情况 2 下的函数调用结果

| 函数 `main` 中实际参数的值 | | | 函数 `calculator` 中形式参数的值 | | | 按情况 2 调用 |

|---|---|---|---|---|---|---|

| `i_first` | `i_second` | `c_operator` | `i_first` | `i_second` | `c_operator` | `i_result` |

| 45 | 25 | + | 25 | 45 | + | 70 |

| 45 | 25 | - | 25 | 45 | - | -20 |

| 45 | 25 | * | 25 | 45 | * | 1125 |

| 45 | 25 | / | 25 | 45 | / | 0 |

| 45 | 25 | % | 25 | 45 | % | 25 |

从表 2 和表 3 可以看出，在情况 1 和情况 2 中，减法、除法和取模运算符的结果是不同的。下一小节将讨论带有参数且无返回值的函数。

#### 带有参数且无返回值的函数

接受调用函数传入的输入参数但不向调用函数返回值的函数，被称为带有参数且无返回值的函数。在此，数据是从调用函数到被调用函数的单向传输。程序 5 展示了一个接受参数但不返回值的函数：

#### 程序 5

```c
/* Program to illustrate the use of a function that takes parameter but does not return value */
/* Program prints the Fibonacci series 0 1 1 2 3 .... */

#include <stdio.h>

/* Beginning of function fibonacci */
void fibonacci(int i_number)
{
    /* Declare local variables */
    int i_fibo1 = 0, i_fibo2 = 1, i_fibo3;
    /* Beginning of switch */
    switch(i_number)
    {
        case 1:
            printf("\n%d  ", i_fibo1);
            break;
        default:
            printf("\n%d  %d  ", i_fibo1, i_fibo2);
            while(i_number > 2)
            {
                /* generate new term */
                i_fibo3 = i_fibo1 + i_fibo2 ;

                /* swap values */
                i_fibo1 = i_fibo2;
                i_fibo2 = i_fibo3;

                /* print fibonacci number */
                printf("%d  ", i_fibo3 );

                i_number--;
            }
    }
    /* End of switch */
}
/* End of function fibonacci */

/* Beginning of function main */
main()
{
    /* Declare local variables */
    int i_number;

    /* Accept value from user */
    printf("\nEnter number of elements required in fibonacci series : ");
    scanf("%d", &i_number);

    /* Check if value entered is positive */
    if(i_number > 0)
        fibonacci(i_number);
    else
        printf("Enter a positive number.\n");
        return;
}
/* End of function main */
```

**输出：**

```
Enter number of elements required in fibonacci series : 6
0   1   1   2   3   5
```

从程序 5 中可以看出，我们定义了一个名为 `fibonacci` 的函数，它从函数 `main` 接收一个整数参数作为输入。函数 `fibonacci` 不向函数 `main` 返回任何值。函数 `fibonacci` 的作用是根据用户输入的元素数量生成斐波那契数列。图 9 展示了在函数 `main` 中调用函数 `fibonacci` 后，执行序列流发生的变化：

![](img/5d422ba7108ffdf64376be51eaf0c459_185_0.png)

> 图 9：调用函数 `fibonacci` 后的执行序列

从图 9 中可以看出，一旦在函数 `main` 中调用了函数 `fibonacci`，执行序列流就会发生改变。从函数调用点开始，执行控制跳转到函数 `fibonacci` 的起始地址。在这里，除了控制转移外，编译器还将变量 `i_number` 的值发送给函数 `fibonacci`。该值随后被赋值给函数 `fibonacci` 的局部变量 `i_number`。然后执行函数 `fibonacci` 内部的语句。一旦函数 `fibonacci` 的执行完成，执行控制流便转移回函数 `main` 中发起函数调用的语句。接着，函数 `main` 内部的语句再次按顺序执行。

你肯定已经观察到，在上一节讨论的四种类型的函数中，有两种函数类型从调用函数接受参数。下一节将讨论函数中参数传递的概念。

### 8.5 函数中的参数传递

从程序 4 和程序 5 中可以看出，这两个程序都从函数 `main` 接受参数。这些参数具有 `int`、`float`、`char`、`struct` 和 `union` 等数据类型。函数的参数也可能是一个函数调用。传递给被调用函数的实际内容可以是变量的值或变量的地址。根据传递的内容不同，C 语言中有两种参数传递机制，即按值传递（pass by value）和按地址传递（pass by address）。下一小节将讨论按值传递机制。

#### 按值传递机制

如果调用函数将变量的值作为内容传递给被调用函数，则称为使用了按值传递的概念。当调用函数将一个变量的值传递给被调用函数时，编译器会将传递的值分配给被调用函数的一个适当的局部变量。一旦完成此赋值操作，调用函数中参数的原始值就被屏蔽，直到函数调用处理结束前都不能被修改。然后所有操作都使用被调用函数的局部变量进行。由于按值传递技术保护了调用函数中变量的数据，因此它是首选的参数传递方式。程序 4 和程序 5 都使用了按值传递技术来传递参数。下一小节将讨论按地址传递技术。

#### 按地址传递机制

有时，有必要将调用函数中变量的引用传递给被调用函数。传递引用会在实际参数和对应的形式参数之间建立直接链接。当被调用函数更改形式参数的值时，这种更改实际上会修改实际参数的值。像 C++ 这样的编程语言将此技术称为按引用传递（pass by reference）。C 语言实际上并不直接支持按引用传递。在 C 语言中，为了传递引用，我们实际上传递的是变量的地址。这种由调用函数向被调用函数传递变量地址的技术称为按地址传递。按地址传递技术使用了在第 3 章中学到的指针概念。程序 6 展示了按地址传递技术的使用。

#### 程序 6

```c
/* Program to illustrate the use of pass by address */
/* Program swaps the values of two integers */
#include <stdio.h>
/* Beginning of function swap */
void swap(int *i_first, int *i_second)
{
    /* Declare local variables */
    int i_temp;
    /* Swap values */
    i_temp = *i_first;
    *i_first = *i_second;
    *i_second = i_temp;
}
/* End of function swap */
/* Beginning of function main */
main()
{
    /* Declare local variables */
    int i_first, i_second;
    /* Accept value from user */
    printf("\nEnter first number: ");
```

`scanf("%d", &i_first);`

`printf("\n请输入第二个数字：");`

`scanf("%d", &i_second);`

/* 调用 `swap` 函数 */

`swap(&i_first, &i_second);`

/* 打印新值 */

`printf("\n第一个数字的新值是 %d。\n", i_first);`

`printf("\n第二个数字的新值是 %d。\n", i_second);`

`return;`

} /* `main` 函数结束 */

**输出：**

请输入第一个数字：75

请输入第二个数字：50

第一个数字的新值是 50

第二个数字的新值是 75。

从程序 6 中可以看出，我们定义了一个名为 `swap` 的函数，它接收两个指针变量作为参数。`swap` 函数不向 `main` 函数返回任何值。`swap` 函数的作用是交换在 `main` 函数中使用的变量 `i_first` 和 `i_second` 的值。图 10 说明了 `main` 函数和 `swap` 函数的栈帧：

![](img/5d422ba7108ffdf64376be51eaf0c459_187_0.png)

从图 10 中可以看出，当操作系统调用 `main` 函数时，`main` 函数的两个局部变量在内存中创建。当在 `main` 函数中调用 `swap` 函数时，内存中总共创建三个局部变量，即 `i_first`、`i_second` 和 `i_temp`。`swap` 函数中的变量 `i_first` 和 `i_second` 被赋值 `0x2000` 和 `0x2006`。这些值是 `main` 函数中变量的地址。当处理 `swap` 函数时，我们取消引用这些地址值并交换 `main` 函数中的实际内容。图 11 说明了值的最终交换过程：

![](img/5d422ba7108ffdf64376be51eaf0c459_188_0.png)

使用按地址传递机制时，程序员必须谨慎，因为程序逻辑中的微小问题可能导致正在运行的程序崩溃或产生非预期的结果。下一节讨论函数中的递归概念。

### 8.6 递归函数

递归是 C 语言结构化编程中的一个主要概念。根据某些条件反复调用自身的函数被称为递归函数。这简单地意味着，设计的函数中可执行语句之一是对其自身的调用。递归用于将复杂问题分解为最简单的单一解决方案。因此，递归函数只能给我们最简单的可能解。大多数本质上是迭代的问题都可以通过递归来解决。然而，迭代和递归仍然是两个不同的实体。程序 7 说明了一个递归函数，该函数计算一个数的幂值：

### ▶ 程序 7

```c
/* Program to illustrate recursive function */
#include <stdio.h>
/* Beginning of function raistopower */
int raisetopower(int i_number, int i_power)
{
if(i_power == 0)
    return (1);
else
    return (i_number * raisetopower(i_number, i_power - 1));
}
/* End of function raisetopower */
/* Beginning of function main */
main()
{
/* Declare local variables */
int i_number, i_power, i_result;
/* Accept value from user */
printf("\nEnter the number: ");
scanf("%d", &i_number);
printf("\nEnter the power: ");
scanf("%d", &i_power);
/* Check if power is positive or not */
if(i_power > 0)
{
/* Call function raisetopower */
i_result = raisetopower(i_number, i_power);
printf("\nThe number %d raised to the power of %d is %d.\n",
       i_number, i_power, i_result);
}
else
    printf("\nCalculation for negative power is not performed.\n");
return;
}
/* End of function main */
```

##### 输出 1：

请输入数字：3

请输入幂：2

数字 3 的 2 次幂是 9。

##### 输出 2：

请输入数字：-5

请输入幂：3

数字 -5 的 3 次幂是 -125。

##### 输出 3：

请输入数字：9

请输入幂：-2

不执行负幂的计算。

从程序 7 中可以看出，我们定义了一个名为 `raisetopower` 的函数，它从 `main` 函数接收两个整型参数值作为输入。它还向 `main` 函数返回一个整数值。这个函数的作用是计算一个整数数的幂值。`raisetopower` 函数是一个递归函数。观察函数的最后一条语句，即 `return (i_number * raisetopower(i_number, i_power - 1));`。在此语句中，再次调用 `raisetopower` 函数。图 12 说明了程序 7 中函数递归的工作方式：

![](img/5d422ba7108ffdf64376be51eaf0c459_190_0.png)

**图 12：递归函数调用**

从图 12 中可以看出，`main` 函数中一次 `raisetopower` 函数的调用递归地产生了另外两次调用。可以看出，在处理完第 3 次调用之前，我们无法向调用函数返回任何值。一旦第 3 次函数调用接收到值 1，其执行即完成。同样，第 2 次函数调用接收到值 3，最后，第 1 次函数调用接收到值 9，该值被赋值给变量 `i_result`。图 12 中显示的符号表示，在返回值之后，该函数从栈中移除。

递归函数可以有效地用于解决那些解可以用重复应用相同解来表示的问题。使用递归函数还可以减少程序代码的大小，使程序看起来更简单。递归函数的唯一缺点是内存需求。每次调用时，递归函数的内存内容都会被复制。用户应先开始使用程序的迭代解决方案，然后再尝试将其转换为递归解决方案。

下一节讨论称为命令行参数的概念。

## 8.7 **命令行参数**

纵观本书，你会发现所有可执行的 C 程序都有一个 `main` 函数。`main` 函数是程序的入口点，由执行程序的环境（操作系统）调用。我们已经提到，函数可以接受来自调用函数的参数。`main` 函数也是如此。`main` 函数也可以接受参数：接受的参数通常是通过环境输入的。这些参数通常被称为命令行参数。要将命令行参数传递给 `main` 函数，需要从操作系统的命令提示符运行程序。

到目前为止，我们使用 `main()` 或 `int main()` 语法定义了 `main` 函数；要使用命令行参数，我们需要使用如下语法：

`int main(int argc, char *argv[])`

在上面的语法中，参数 `argc` 是一个整型变量，指向传递的命令行参数的数量。`argc` 的最小值始终为 1，通常指程序名称。参数 `argv` 是一个字符指针数组（概念在第 9 章中详细讨论）。程序 8 说明了命令行参数的使用；

### **程序 8**
