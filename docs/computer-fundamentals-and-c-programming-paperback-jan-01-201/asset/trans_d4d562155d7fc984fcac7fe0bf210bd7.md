
## 11 函数

## 学习目标

-   *声明、定义*和调用函数的技巧。
-   探索处理函数*返回值*的各种方式。
-   数据从*实参*传递到*形参*的机制。
-   C 是按*值*还是按*引用*传递实参。
-   函数*副作用*的意义。
-   将一维和二维数组作为函数实参传递。
-   从一个函数调用另一个函数的后果。
-   以*递归*方式使用函数的技巧。
-   使用*存储类*确定变量的*作用域*和*生命周期*。

## 11.1 函数基础

C 程序员将复杂任务分解为称为函数的独立且可管理的模块。被重复使用的代码段——甚至被其他程序重复使用——也实现为函数。与使用一个庞大的 main 函数完成所有工作的程序相比，将大部分工作委托给独立函数的 C 程序更易于开发和维护。虽然像 `printf` 和 `scanf` 这样的函数被视为黑盒，但你必须知道如何创建自己的函数并将它们集成到主程序中。

*函数*是一条语句，表示一段有名称的程序代码体。当函数被调用时，与该函数关联的代码被执行。函数可以选择性地 (i) 接受一个或多个值作为*实参*，并且 (ii) 通过向调用者*返回*单个值来报告其操作结果。函数主要通过以下两种方式之一调用：

```c
message_of_day();        /* No argument, returns no value */
fahrenheit = c2f(40.2);  /* One argument, returns a value */
```

通过函数名后面紧跟的一对匹配括号，可以很容易地识别出函数。`message_of_day` 函数既没有被传入实参，也不返回值。但 **c2f** 函数接受一个实参 (40.2)，并且还返回一个值，该值在这里保存在变量 `fahrenheit` 中。这个保存的值可以在程序后面使用。尽管并非所有函数都接受实参或返回值，但绝大多数函数都会。

函数在被调用之前必须先声明和定义。*声明*指定如何正确调用函数。*定义*提供实现，即在调用时将执行的代码体。与每次调用时行为都相同的 **message_of_day** 不同，**c2f** 的行为由传递给它的实参值（此处为 40.2）决定。

你创建的函数也可以调用其他函数。函数甚至可以调用自身，这一特性在编程领域有重要应用（例如计算一个数的阶乘）。对于我们目前使用过的所有函数，调用者都是 **main**。这是一个特殊的函数，每个独立的 C 程序都必须具有它，因为程序通过调用 **main** 开始执行。本章后面我们还会进一步讨论 **main** 函数。

在本章中，我们将从头创建一些函数，并使用它们重写之前的一些程序。在每种情况下，函数的实现（即定义）都出现在调用它的同一个文件中。因此，在一个程序中定义的函数，如果不复制声明和定义，就不能在另一个程序中重用。我们将使用 ANSI 规定的技术来创建函数，并忽略 K&R C 最初提出的技术。第 17 章探讨将函数隔离到单独文件中以便所有程序都能使用它们的技术。

> **要点：** 函数在使用之前必须先声明和定义。声明指定用法，定义提供被执行的代码。

## 11.2 `first_func.c`：无实参，无返回值

现在让我们考虑第一个程序（程序 11.1），它包含一个名为 **message_of_day** 的简单函数。该函数在 **main** 之前声明，从 **main** 的函数体中调用，并在 **main** 之后定义。该程序打印四行——**main** 和该函数各打印两行。

函数 **message_of_day** 就在预处理指令之后、**main** 之前按以下方式声明：

```c
void message_of_day(void);  /* Function declared */
```

声明或原型并不指定 **message_of_day** 做什么，只指定如何调用它。由于每个声明也是一条语句，所以它必须以分号结尾。该函数不使用实参（第二个 void），也不返回值（第一个 void），因此必须按以下方式调用：

```c
message_of_day();  /* Function called or invoked */
```

**message_of_day** 被设计用来做什么，在 **main** 之后的定义中指定。按照惯例，所有函数定义都位于 **main** 之后，尽管它们也可以放在 **main** 之前。

```c
/* first_func.c: Uses a function that has no arguments and returns nothing. */
#include <stdio.h>

/* Function declaration or prototype */
void message_of_day(void);                 /* Try deleting this statement */

int main(void)
{
    printf("Invoking function ...\n");
    message_of_day();                      /* Function invocation or call */
    printf("Returned from function.\n");

    return 0;
}

/* Function definition or implementation */
void message_of_day(void)                  /* The header */
{
    printf("This function uses no arguments and returns nothing.\n");
    printf("The next program uses one argument and returns a value.\n");
    return;
}
```

**程序 11.1：first_func.c**

```text
Invoking function ...
This function uses no arguments and returns nothing.
The next program uses one argument and returns a value.
Returned from function.
```

**程序输出：first_func.c**

定义包含一个*头部*和一个由一对花括号括起来的函数体。该函数体包含两条 **printf** 语句和一条不带值的 **return** 语句。

编译器发现函数声明与定义和调用一致。当 **message_of_day** 被调用时，程序控制转移到函数体，在那里执行放置其中的所有语句。函数中的 **return;** 语句将控制权移回调用者（即 **main**）。然后执行继续从函数调用之后的下一条语句开始。

函数中的 **return;** 语句与我们一直使用的 **main** 中的那条语句具有相同意义。它终止函数并将控制权返回给调用者。然而，该函数不返回值（是 **return;** 而不是 **return 0;**）。尽管这里的 **return** 并非必需，但在每个函数中都包含它——即使它可能不返回任何内容——也是一种良好的编程实践。

![](img/d75612dcf3ab36327142238ab5bb21d8_358_0.png)

> **要点：** 函数名在一个程序中至少出现三次。声明出现在开头，调用发生在 **main** 的函数体中，定义放在 **main** 之后。如果它们的形式不匹配，编译器将输出错误。

> **注意：** 我们不需要为标准库中的函数提供定义，但仍然需要它们的声明。文件 `stdio.h` 包含 `printf` 和 `scanf` 的声明，这就是到目前为止我们在每个程序中都包含此文件的原因。

## 11.3 函数的构成

函数是一个标识符，这意味着与变量和数组命名相关的规则也适用于函数 (5.2.1)。因此，名称可以由字母、数字和下划线字符组成，其中第一个字符不能是数字。大小写有意义，因此，area 和 AREA 是两个不同的函数。现在让我们考察函数的三个主要属性：声明、定义和调用。

### 11.3.1 声明、原型或签名

声明是一条正式语句，它告诉编译器如何调用函数。声明也称为原型或签名。由于它放在 main 之前，编译器首先看到它，然后将其与调用和定义进行比较。为了进行比较，编译器确定函数是否

-   使用任何实参，如果是，则确定这些实参的数量及其数据类型。
-   返回一个值，如果是，则确定其数据类型。

这会产生四种可能的情况——有或没有实参，以及有或没有返回值。以下语法和支持示例展示了如何声明一个既没有实参也没有返回值的函数：

```c
void function_name(void);
void message_of_day(void);                    /* Used in first_func.c */
```

第一个 void 表示该函数不返回值。第二个 void 表示该函数不使用实参。然而，大多数函数使用一个或多个实参，并且还使用以下通用语法返回一个值：

```c
return_type function_name(type1 arg1, type2 arg2 ...);
```

这里，return_type 表示返回值的数据类型。函数实参表示为 arg1、arg2 等，其中每个实参前面都有其数据类型 type1、type2 等。实参可以是变量、常量或表达式。以下是一个示例：

```c
double area(float length, float breadth);
```

area 函数接受两个类型为 float 的实参，并返回一个类型为 double 的值。由于编译器只需将声明中实参的类型和数量与定义中使用的实参进行匹配，它不需要知道这些变量名，因此 C 允许你省略它们：

```c
double area(float, float);                    /* Not recommended */
```
