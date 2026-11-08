
```c
printf("\n This code is always compiled");
getch();
return 0;
}
```

在清单7.8中，我们使用 #define 指令定义了 __DEBUG__ 编译标志，这使得 #ifdef 和 #endif 块内的代码被编译。

上述程序的输出如下：

```text
This code is skipped
This code is always compiled
```

同样，我们可以使用 #undef 指令关闭 __DEBUG__ 标志，以便相同的代码不会被编译。清单7.9展示了 #undef 指令的工作方式：

**清单 7.9：展示 #undef 指令的工作方式**

```c
#include<stdio.h>
#undef __DEBUG__
int main()
{
    #ifdef __DEBUG__
        printf("\n This code is skipped ");
    #endif
    printf("\n This code is always compiled");
    getch();
    return 0;
}
```

上述程序的输出如下：

```text
This code is always compiled
```

#ifdef 和 #else 指令的工作方式与 if 和 else 条件语句相同，但这些指令专门用于宏。清单7.10展示了 #ifdef 和 #else 指令的用法：

**清单 7.10：使用 #ifdef 和 #else 指令**

```c
#include<stdio.h>
#define __DEBUG__
int main()
{
    #ifdef __DEBUG__
        printf("\n Disabling flag");
        #undef __DEBUG__
    #else
        printf("\n Enabling flag");
        #define __DEBUG__
    #endif

    #ifndef __DEBUG__
        printf("\n Enabling the flag once again");
        #define __DEBUG__
    #else
        printf("\n Disabling the flag once again");
        #undef __DEBUG__
    #endif

    getch();
    return 0;
}
```

上述程序的输出如下：

```text
Disabling flag
Enabling the flag once again
```

在清单7.10中，我们首先检查了 __DEBUG__ 宏是否已定义。如果该宏已经定义，那么它将在 #ifdef 块中被取消定义。然而，如果该宏未定义，那么它将在 #else 块中被定义。请注意，如果我们不定义该宏，那么我们会得到相反的输出。

现在，考虑这样一种场景：utilityFunc() 函数定义在 header1.h 文件中，而该文件又被包含在另一个名为 header2.h 的头文件中。假设一个程序同时包含这两个头文件。在这种情况下，编译器将抛出错误消息——utilityFunc() 的多次声明。这是因为 header1.h 文件的一个实例已经被包含在 header2.h 文件中。如果我们在一个程序中包含这两个头文件，那么同一个函数的多个实例将被包含其中。为了解决这个问题，我们需要避免多次包含同一个头文件。以下代码片段展示了避免在程序中多次包含一个函数的解决方案：

```c
#ifndef __myheader_h
#define __myheader_h
utilityFunc()
{
}
#endif
```

当 __myHeader.h 文件第一次被包含到程序中时，预处理器会检查该标志，并发现它未定义。因此，预处理器会设置该标志，并将 utilityFunc() 函数的主体包含到程序中。然而，如果同一个头文件第二次被包含到程序中，那么预处理器会发现该标志已定义；因此，它会跳过这部分代码。

现在让我们了解一些其他指令。

## 其他指令

有些预处理器指令无法归入任何特定类型，因为它们用于不同的目的。以下就是这类其他指令：

- #undef
- #pragma
- #error
- #line

让我们逐一详细了解它们。

### #undef

#undef 指令会移除其后宏的先前定义。换句话说，它会取消定义一个宏。#undef 指令的一般语法如下：

```c
#undef macro_name
```

**清单 7.11：展示 #undef 指令的工作方式**

```c
#include<stdio.h>
#define VARIABLE 50
int main()
{
    #undef VARIABLE
    printf("\n The value is %d ",VARIABLE);
    getch();
}
```

当我们编译上述程序时，它会产生以下编译错误：

```text
'VARIABLE' undeclared (first use in this function)
```

### #pragma

#pragma 指令是一种实现驱动的指令，用于向编译器提供各种指令。Pragma 因编译器而异。某些 pragma，例如 startup 和 exit，用于在源代码中插入注释。清单7.12展示了 pragma 的工作方式：

**清单 7.12：展示 Pragma 的工作方式**

```c
void fun1( ) ;

void fun2( ) ;

#pragma startup fun1

#pragma exit fun2

main( )
{
    printf ( "\ninside main" ) ;
}
void fun1( )
{
    printf ( "\ninside fun1" ) ;
}
void fun2( )
{
    printf ( "\ninside fun2" ) ;
}
```

在清单7.12中，#pragma startup 和 #pragma exit 指令允许用户分别指定在 main() 函数执行之前和之后应调用的函数。

清单7.12的输出如下：

```text
Inside fun1
Inside main
Inside fun2
```

### #line

#line 指令会更改 __LINE__ 和 __FILE__ 的内容，它们是编译器中的两个预定义标识符。__LINE__ 标识符保存当前编译代码行的行号。__FILE__ 标识符保存一个字符串，其中包含正在编译的源文件的名称。清单7.13展示了未使用 #line 指令编写的代码：

**清单 7.13：展示未使用 #line 指令的代码**

```c
#include<stdio.h>

int main()
{
    printf("\n In Line [%d] File name [%s] ",__LINE__,__FILE__);
    getch();
}
```

上述程序的输出如下：

```text
In Line [5] File name [D:\Tanuman\Progs\conditional.c]
```

现在，如果使用 #line 指令重写清单7.13中的代码，那么它如清单7.14所示：

**清单 7.14：展示使用 #line 指令编写的代码**

```c
#include<stdio.h>
#line 500 "Tanuman"
int main()
{
    printf("\n In Line [%d] File name [%s] ",__LINE__,__FILE__);
    getch();
}
```

上述程序的输出如下：

```text
In Line [503] File name [Tanuman]
```

如输出所示，#line 指令不仅更改了行号并将其重置为 500，而且还更改了程序的文件名。

### #error

#error 指令会阻止编译器进行编译。它主要用于调试。#error 指令的一般形式如下：

```c
#error error-message
```

请注意，error-message 不应放在双引号内。每当遇到 #error 指令时，就会显示 error-message。清单7.15展示了 #error 指令的用法：

**清单 7.15：展示 #error 指令的工作方式**

```c
#include<stdio.h>
int main()
{
    #error Stop here
    printf("\n This is Test");
    getch();
}
```

清单7.15的输出如下：

```text
#error Stop here
```

如输出所示，代码编译会通过给出错误消息而停止。

现在让我们总结本章讨论的要点。

## 小结

在本章中，我们学习了预处理器在编译 C 源代码时的作用。我们还学习了预处理器指令，例如 #define、#ifdef、#endif、#undef、#else、#pragma、#error 和 #line。

在下一章中，我们将学习 C 中的标准库函数。

## 快速复习

### 多项选择题

- **Q1.** 以下哪一项不是有效的预处理器指令？
- i. `#define`
- ii. `#ifdef`
- iii. `#ifdefine`
- iv. `#line`

**Q2.** 以下代码的输出将是什么？

```c
#include<stdio.h>
#define TEST 50
int main()
{
    printf("\n Test value %d ",TEST--);
    getch();
}
```

- i. 49
- ii. 50
- iii. 无法编译
- iv. 以上都不是

**Q3.** 以下哪条指令用于在源代码中包含头文件？

- i. #include
- ii. #define
- iii. #ifdef
- iv. #pragma

**Q4.** 以下代码的输出将是什么？

```c
#include<stdio.h>
#define TEST(x)                 \
{                              \
    printf("\n In a Macro ");    \
}
int main()
{
    TEST(10);
    getch();
}
```

- i. 导致宏展开
- ii. 编译错误
- iii. 运行时错误
- iv. 以上都不是

### 主观题

- Q1. 编写一个使用宏来找出输入的两个数中最大数的程序。
- Q2. 编写一个使用宏来检查输入的字符是否为大写字母的程序。
- Q3. 编写一个使用宏计算单利的程序。将宏存储在头文件中，并在编译程序时在源文件中包含该头文件。
