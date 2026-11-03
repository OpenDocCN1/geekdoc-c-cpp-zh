
每个 #if 指令都应以 #endif 指令结束。这些指令的工作方式与 if...else 构造类似。

## 12.11.1 #if 和 #endif

后跟 #if 的表达式会被求值，如果结果非零，则 #if 和 #endif 之间的语句会被编译，否则会被跳过。这写成如下形式-

```c
#if constant-expression
........
statements
........
#endif
```

constant-expression 应为整型表达式，且不应包含枚举常量、sizeof 运算符、强制类型转换运算符或任何关键字或变量。它可以包含算术、逻辑、关系运算符。如果表达式中出现任何未定义的标识符，则将其视为值为零。

```c
/*P12.14 Program to understand the use of #if directive*/
#include<stdio.h>
#define FLAG 8
main()
{
    int a=20,b=4;
#if FLAG >= 3
    printf("Value of FLAG is greater than or equal to 3\n");
    a=a+b;
    b=a*b;
    printf("Values of variables a and b have been changed\n");
#endif
    printf("a = %d, b = %d\n",a,b);
    printf("Program completed\n");
}
```

输出：
Value of FLAG is greater than or equal to 3
Values of variables a and b have been changed
a = 24, b = 96
Program completed

在此程序中，FLAG 被定义为值 8。首先求值常量表达式 FLAG >= 3；由于它是真（非零），因此 #if 和 #endif 之间的所有语句都会被编译。假设 FLAG 的值改为 2，现在常量表达式 FLAG >= 3 将求值为假，因此 #if 和 #endif 之间的语句将不会被编译。在这种情况下，程序的输出将为-
a = 20, b = 4
Program completed

## 12.11.2 #else 和 #elif

#else 与 #if 预处理指令一起使用。它类似于 if...else 控制结构。形式如下-

```c
#if constant-expression
    statements
#else
    statements
#endif
```

如果常量表达式求值为非零，则 #if 和 #else 之间的语句会被编译，否则 #else 和 #endif 之间的语句会被编译。

```c
/*P12.15 Program to understand the use of #else directive*/
#include<stdio.h>
#define FLAG 8
main()
{
    int a=20,b=4;
    #if FLAG>=3
    printf("Value of FLAG is greater than or equal to 3\n");
    a=a+b;
    b=a*b;
    #else
    printf("Value of FLAG is less than 3\n");
    a=a-b;
    b=a/b;
    #endif
    printf("a = %d, b = %d\n",a,b);
    printf("Program completed\n");
}
```

### 输出：

Value of FLAG is greater than or equal to 3
    a = 24, b = 96
    Program completed

这里 FLAG 的值是 8，所以常量表达式 FLAG >= 3 求值为真，因此 #if 和 #else 之间的语句会被编译。如果 FLAG 的值改为 2，则常量表达式 FLAG >= 3 将求值为零，所以现在 #else 和 #endif 之间的语句将被编译，程序的输出将为-
Value of FLAG is less than 3
    a = 16, b = 4
    Program completed

#if 和 #else 的嵌套也是可能的，这可以通过使用 #elif 来实现。这类似于我们在控制语句中学习过的 else...if 阶梯。每个 #elif 都有一个常量表达式，首先求值该表达式，如果值为真则编译该部分代码并跳过所有其他 #elif 表达式，否则求值下一个 #elif 表达式。

### 语法：

```c
#if constant-expression1
    ......
#elif constant-expression2
    ......
#elif constant-expression3
    ......
#else
    ......
#endif
```

上述代码可使用 #if 和 #else 指令写成如下形式-

```c
#if constant-expression1
    ......
#else
#if constant-expression2
    ......
#else
#if constant-expression3
    ......
#else
    ......
#endif
#endif
#endif
```

这里每个 #if 都应有一个 #endif，而使用 #elif 时只有一个 #endif。让我们看一个使用 #elif 指令的程序-

```c
/*P12.16 Program to understand the use of #elif directive*/
#include<stdio.h>
#define FLAG 1
main()
{
    int a=20,b=4;
    #if FLAG==0
        printf("Value of FLAG is zero\n");
        a++;
        b++;
    #elif FLAG==1
        printf("Value of FLAG is one\n");
        a--;
        b--;
    #elif FLAG==2
        printf("Value of FLAG is two \n");
        a=a-3;
        b=b-3;
    #else
        printf("Value of FLAG is greater than two or less than zero\n");
        a=a+b;
        b=a-b;
    #endif
    printf("a = %d, b = %d\n",a,b);
    printf("Program completed\n");
}
```

### 输出：

Value of FLAG is one
a = 19, b = 3
Program completed

这里表达式 FLAG == 1 为真，因此与此 #elif 对应的语句会被编译。

## 12.11.3 defined 运算符

语法：defined(macro_name )

该运算符仅与 #if 和 #elif 指令一起使用。如果 macro_name 已使用 #define 定义，则求值为 1，否则求值为零。例如：

```c
#if defined(FLAG)
```

如果宏 FLAG 已使用 #define 定义，则表达式 defined(FLAG) 的值将为 1，否则其值为 0。

## 12.11.4 #ifdef 和 #ifndef

#ifdef 和 #ifndef 指令提供了将 #if 与 defined 运算符结合使用的替代简写形式。

#if defined(macro_name ) 等价于 #ifdef macro_name

#if !defined(macro_name ) 等价于 #ifndef macro_name

#ifdef 的语法-

```c
#ifdef macro_name
......
#endif
```

如果 macro_name 已使用 #define 指令定义，则 #ifdef 和 #endif 之间的语句将被编译。如果 macro_name 未定义或已使用 #undef 取消定义，则这些语句不会被编译。

#ifndef 的语法-

让我们看一个程序-

```c
/*P12.17 Program to understand the use of #ifdef directive*/
#include<stdio.h>
#define FLAG
main()
{
 int a=20,b=4;
 #ifdef FLAG
 printf("FLAG is defined\n ");
 a++;
 b++;
 #endif
 printf("a = %d, b= %d\n",a,b);
 printf("Program completed\n");
}
```

### 输出：

    FLAG is defined
    a = 21, b = 5
    Program completed

宏 FLAG 已被定义，所以 #ifdef 和 #endif 之间的语句会被编译。如果我们从程序中删除宏 FLAG 的定义，则这些语句不会被编译，程序的输出将为-
    a = 20, b = 4
    Program completed

```c
/*P12.18 Program to understand the use of #undef and #ifdef directives*/
#include<stdio.h>
#define FLAG
main()
{
    int a=20,b=4;
    #ifdef FLAG
    printf("FLAG is defined\n");
    a++;
    b++;
    #endif
    #undef FLAG
    #ifdef FLAG
    printf("Preprocessor\n");
    a++;
    b++;
    #endif
    printf("a = %d, b= %d\n",a,b);
    printf("Program completed\n");
}
```

### 输出：

    FLAG is defined
    a = 21, b = 5
    Program completed

这里我们在程序中间取消定义了宏 FLAG。所以宏 FLAG 仅在 #undef 指令之前的程序部分中被定义，在其后的程序部分中未被定义。

```c
/*P12.19 Program to understand the use of #ifndef directive*/
#include<stdio.h>
main()
{
    int a=20,b=4;
    #ifndef MAX
    printf("MAX is not defined\n");
    a--;
    b--;
    #endif
    printf("a = %d, b = %d\n",a,b);
    printf("Program completed\n");
}
```

### 输出：

MAX is not defined
a = 19, b = 3
Program completed

这里宏 MAX 未被定义，所以 #ifndef 和 #endif 之间的语句会被编译。

defined 运算符的存在在某些情况下很重要。例如，我们不能在此处使用简写形式（#ifdef 和 #ifndef）-

- (i) 当我们需要检查多个宏的存在时，例如-

```c
#if defined(ABC) && defined(PQR) && !defined(XYZ)
```

- (ii) 当需要在 #elif 中检查宏的存在时

```c
#if defined(ABC)
       ...........
#elif defined( PQR)
       ...........
#elif defined(XYZ)
       ...........
#endif
```

条件编译在许多情况下都很有用，例如编写可移植代码、调试、注释。我们将逐一讨论这些情况。

## 12.11.5 编写可移植代码

假设我们想编写一个可以在不同系统上运行的程序。在这种情况下，代码中的某些行将是系统相关的。这些行可以使用条件编译指令编写。假设我们为不同的机器制作了不同的头文件。我们可以编写代码以在特定机器上工作时包含适当的头文件。

```c
#if MACHINE == ABC
#define hfile abc.h
#elif MACHINE == PQR
#define hfile pqr.h
#elif MACHINE == XYZ
#define hfile xyz.h
#else
#define hfile newfile.h
#endif
#include"hfile"
```

现在当我们想在机器 ABC 上工作时，我们可以将宏 MACHINE 定义为-
#define MACHINE ABC
所以文件 abc.h 将被包含。
如果我们想在机器 XYZ 上工作，我们可以将 MACHINE 定义为-
#define MACHINE XYZ
现在文件 xyz.h 将被包含。
