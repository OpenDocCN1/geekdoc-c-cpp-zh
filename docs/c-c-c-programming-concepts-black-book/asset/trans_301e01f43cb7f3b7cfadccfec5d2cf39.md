

```c
return 0;
}

void myFunc(int value1, int value2)
{
    printf("\n value is [%d]",value1);
}
```

清单 2.4 的输出如下：

```text
too few arguments to function 'myFunc'
```

在清单 2.4 中，myFunc 函数在其参数列表中定义了两个参数。当仅使用一个参数调用该函数时，会抛出编译错误。错误指出没有为该函数提供足够的参数。一种良好的编程实践是，即使函数不返回任何内容，也始终为函数体包含返回类型。可以在函数体内包含一个空的 return 语句，如下面的代码片段所示：

```c
void myFunc(int value1, int value2)
{
    printf("\n value is [%d]",value1);

    return;
}
```

## 函数的调用约定

可以通过提及函数名并后跟参数列表来访问函数，参数列表括在圆括号中，并用逗号分隔。函数调用可能具有空参数列表，在这种情况下，一对圆括号也将为空。函数调用中出现的参数称为实参，它们不同于函数定义第一行中提到的形参。普通函数调用在实参和形参之间具有一一对应关系。应始终牢记，实参的数据类型应与形参中提供的数据类型完全相似。在函数调用期间，实际参数的值会被传递给函数，并分配给每一个形参。清单 2.5 展示了一个说明函数中一些基本调用约定的示例：

清单 2.5：函数中的调用约定

```c
# include<stdio.h>

void myFunc(int value1, int value2);

int main()
{
    printf("\n value passed to function");
    myFunc(10,20);
    getch();
    return 0;
}

void myFunc(int value1, int value2)
{
    printf("\n value are [%d] and [%d] ",value1, value2);

    return;
}
```

第 2 章

在清单 2.5 中，可以看到两个不同的值作为实参传递给 myFunc 函数。进行函数调用时，这两个值会分配给形参“value1”和“value2”。当在 myFunc 函数内部显示这些变量时，这种赋值就变得清晰了。如果函数返回任何值，那么函数调用必须看起来像一条赋值语句，其中从函数返回的值存储在变量中。

清单 2.6：函数返回值

```c
#include<stdio.h>

int myFunc(int value1, int value2);
int main()
{
    int sum;
    printf("\n Value passed to function");
    sum = myFunc(10,20);
    printf("\n The sum returned by the function is [%d]",sum);
    getch();
    return 0;
}
int myFunc(int value1, int value2)
{
    printf("\n Value are [%d] and [%d] ",value1, value2);

    return (value1 + value2);
}
```

清单 2.6 的输出如下：

```text
Value passed to function
Value are [10] and [20]
The sum returned by the function is [30]
```

在清单 2.6 中，可以看到在调用函数时使用了一条赋值语句，其中函数调用被放在赋值语句的右侧。这表明函数返回的值将存储在赋值语句左侧的变量中。执行此类赋值时需要遵循的一个重要点是，用于赋值的变量的数据类型必须与函数的返回类型相似。

将参数传递给函数有两种方式——按值调用和按引用调用。现在让我们详细讨论这两种方式。

### 按值调用

按值调用方法将实参的值复制到函数相应的形参中。对形参所做的任何更改都不会影响实参。清单 2.7 展示了按值调用方法的一个示例：

清单 2.7：在 C 中演示按值调用

```c
#include<stdio.h>

void myFunc(int);

int main()
{
int arg_1 = 10;

printf("\n Value before function call [%d]",arg_1);
myFunc(arg_1);
printf("\n Value after function call [%d]",arg_1);


getch();
}

void myFunc(int arg_1)
{
    arg_1--;
    printf("\n Value inside function call [%d] ",arg_1);
}
```

清单 2.7 的输出如下：

```text
Value before function call [10]
Value inside function call [9]
Value after function call [10]
```

清单 2.7 中显示的程序输出表明，传递给 myFunc 函数的参数只是主调用模块中声明的变量的一个副本。

### *按引用调用*

在按引用调用方法中，参数的地址被复制到形参中，并传递给函数。按引用调用保证函数内部发生的更改会从调用函数中反映出来。在 C 中，按引用调用借助指针实现。指针是一种特殊类型的变量，用于保存内存位置的地址。关于指针的详细内容将在本书第 3 章 *C 中的指针与函数指针* 中介绍。由于我们使用内存位置的地址来访问实参的值，因此函数内部发生的操作可以改变参数的内容。清单 2.8 展示了按引用调用在 C 中如何工作：

清单 2.8：在 C 中演示按引用调用

```c
#include<stdio.h>

void mySwap(int *x, int *y);

int main()
{
    int x = 10;
    int y = 50;

    printf("\n Value before function call [%d] and [%d]",x,y);
    mySwap(&x,&y);
    printf("\n Value after function call [%d] and [%d] ",x,y);

    getch();
}
void mySwap(int *x, int *y)
{
    int temp;

    temp = *x;
    *x = *y;
    *y = temp;
}
```

在许多情况下，命令行参数需要用双引号括起来，或者通过在其中插入逗号或空格来分隔。按照常见标准，使用空白字符分隔多个命令行参数。argv 数组的声明应使用空方括号。空方括号表示数组长度未确定。

清单 2.10 展示了另一个描述命令行参数用法的示例：

清单 2.10：C 中的多个命令行参数

```c
#include<stdio.h>

int main(int argc, char *argv[])
{
    int i;
    if(argc < 2)
    {
        printf("\n Too few parameters");
        return;
    }

    printf("\n Number of arguments is [%d]",argc);
    for(i=0;i < argc; i++)
    {
        printf("\n Argument passed [%s] ",argv[i]);
    }
    getch();
    return 0;
}
```

清单 2.10 的输出如下：

```text
D:\Tanuman\Progs>check.exe Ron Lucy Harry Jim John Tom

Number of arguments is [7]
Argument passed [check.exe]
Argument passed [Ron]
Argument passed [Lucy]
Argument passed [Harry]
Argument passed [Jim]
Argument passed [John]
Argument passed [Tom]
```

前面输出中展示的程序演示了 argc 参数的用法，并显示了程序命令行中提供的参数数量。

## 函数原型

可以通过两种方式在程序中包含函数。在第一种方式中，函数体位于程序的主模块之前。这意味着当程序编译时，用户定义函数会在访问该函数之前就已被定义。然而，这种方式也有某些限制。遵循这种方式意味着我们必须始终将主模块放在程序的末尾，而情况并非总是如此。如果我们把函数定义放在主模块之后，代码将产生编译错误。这种情况发生在我们试图在定义函数之前访问该函数时。

