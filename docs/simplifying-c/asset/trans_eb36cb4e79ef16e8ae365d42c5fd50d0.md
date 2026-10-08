
scanf("%d", &i_first);
printf("\n请输入第二个数字：");
scanf("%d", &i_second);
/* 调用 swap 函数 */
swap(&i_first, &i_second);
/* 打印新值 */
printf("\n第一个数字的新值是 %d。\n", i_first);
printf("\n第二个数字的新值是 %d。\n", i_second);
return;
} /* main 函数结束 */

**输出：**

请输入第一个数字：75

请输入第二个数字：50

第一个数字的新值是 50

第二个数字的新值是 75。

从程序 6 中可以看出，我们定义了一个名为 swap 的函数，它接收两个指针变量作为参数。swap 函数不向 main 函数返回任何值。swap 函数的作用是交换在 main 函数中使用的变量 i_first 和 i_second 的值。图 10 说明了 main 函数和 swap 函数的栈帧：

![](img/5d422ba7108ffdf64376be51eaf0c459_187_0.png)

从图 10 中可以看出，当操作系统调用 main 函数时，main 函数的两个局部变量在内存中创建。当在 main 函数中调用 swap 函数时，内存中总共创建三个局部变量，即 i_first、i_second 和 i_temp。swap 函数中的变量 i_first 和 i_second 被赋值 0x2000 和 0x2006。这些值是 main 函数中变量的地址。当处理 swap 函数时，我们取消引用这些地址值并交换 main 函数中的实际内容。图 11 说明了值的最终交换过程：

![](img/5d422ba7108ffdf64376be51eaf0c459_188_0.png)

使用按地址传递机制时，程序员必须谨慎，因为程序逻辑中的微小问题可能导致正在运行的程序崩溃或产生非预期的结果。下一节讨论函数中的递归概念。

## 8.6 递归函数

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

### 输出 1：

请输入数字：3

请输入幂：2

数字 3 的 2 次幂是 9。

### 输出 2：

请输入数字：-5

请输入幂：3

数字 -5 的 3 次幂是 -125。

### 输出 3：

请输入数字：9

请输入幂：-2

不执行负幂的计算。

从程序 7 中可以看出，我们定义了一个名为 raisetopower 的函数，它从 main 函数接收两个整型参数值作为输入。它还向 main 函数返回一个整数值。这个函数的作用是计算一个整数数的幂值。raisetopower 函数是一个递归函数。观察函数的最后一条语句，即 `return (i_number * raisetopower(i_number, i_power - 1));`。在此语句中，再次调用 raisetopower 函数。图 12 说明了程序 7 中函数递归的工作方式：

![](img/5d422ba7108ffdf64376be51eaf0c459_190_0.png)

**图 12：递归函数调用**

从图 12 中可以看出，main 函数中一次 raisetopower 函数的调用递归地产生了另外两次调用。可以看出，在处理完第 3 次调用之前，我们无法向调用函数返回任何值。一旦第 3 次函数调用接收到值 1，其执行即完成。同样，第 2 次函数调用接收到值 3，最后，第 1 次函数调用接收到值 9，该值被赋值给变量 i_result。图 12 中显示的符号表示，在返回值之后，该函数从栈中移除。

递归函数可以有效地用于解决那些解可以用重复应用相同解来表示的问题。使用递归函数还可以减少程序代码的大小，使程序看起来更简单。递归函数的唯一缺点是内存需求。每次调用时，递归函数的内存内容都会被复制。用户应先开始使用程序的迭代解决方案，然后再尝试将其转换为递归解决方案。

下一节讨论称为命令行参数的概念。

## 8.7 **命令行参数**

纵观本书，你会发现所有可执行的 C 程序都有一个 main 函数。main 函数是程序的入口点，由执行程序的环境（操作系统）调用。我们已经提到，函数可以接受来自调用函数的参数。main 函数也是如此。main 函数也可以接受参数：接受的参数通常是通过环境输入的。这些参数通常被称为命令行参数。要将命令行参数传递给 main 函数，需要从操作系统的命令提示符运行程序。

到目前为止，我们使用 `main()` 或 `int main()` 语法定义了 main 函数；要使用命令行参数，我们需要使用如下语法：

`int main(int argc, char *argv[])`

在上面的语法中，参数 argc 是一个整型变量，指向传递的命令行参数的数量。argc 的最小值始终为 1，通常指程序名称。参数 argv 是一个字符指针数组（概念在第 9 章中详细讨论）。程序 8 说明了命令行参数的使用；

### **程序 8**

```c
/* Program to illustrate command line arguments */
#include <stdio.h>
#include <string.h>

/* Beginning of function main */
main(int argc, char *argv[]) 
{ 
    /* Declare local variables */
    int i_octr, i_length, i_maxlength;
    int i_strindex = 1;

    /* Check number of command line arguments */
    if(argc > 1) 
    { 
        /* Find maximum length string */
        i_maxlength = strlen(argv[1]);
        
        for(i_octr = 2; i_octr <= argc; i_octr++)
        {
            i_length = strlen(argv[i_octr]);
            
            if(i_length >= i_maxlength)
            { 
                i_maxlength = i_length;
                i_strindex = i_octr;
            }
        }
    }
    
    /* Print the last string with maximum length */
    printf("The string %s is the longest.\n", argv[i_strindex]);
    return 0;
}
```

从程序 8 中可以看出，我们在 main 函数中使用了命令行参数。该程序检查作为命令行参数提供的字符串的长度，以识别具有最大长度的字符串。如果列表中有多个具有最大长度的字符串，则序列中最后一个字符串被视为具有最大长度。请注意，我们没有为该程序提供任何输出。程序 8 不能直接从任何集成开发环境 (IDE) 运行，而必须从命令提示符执行。图 13 显示了在磁盘操作系统 (DOS) 以及 Linux/UNIX 环境中执行程序的语法，以及将生成的输出：

![](img/5d422ba7108ffdf64376be51eaf0c459_192_0.png)

从图 13 中可以看出，我们输入了可执行文件的名称（在 DOS 情况下是 prog8_8.exe，在 Linux/UNIX 情况下是 prog8_8.o）以及一些名称。所有这些名称加上可执行程序的名称都是参数 argv 的内容。在 DOS 环境中，argv[0] 存储值 *prog8_8.exe*，argv[1] 存储值 *navya*，等等。存储在 argv[5] 中的最后一个值是 *vidita*。在 DOS 环境中，argc 的值等于 6。在 Linux/UNIX 环境中，argc 的值等于 4，参数 argv 的内容也不同，如图 13 所示。

