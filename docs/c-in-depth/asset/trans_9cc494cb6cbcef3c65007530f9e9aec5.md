
Similarly if we have some code in the program that is different for different machines, we can use the above structure.

## 12.11.6 Debugging

编译器可以检测语法错误，但无法检测导致输出错误的结果运行时错误。为了追踪程序中这类错误，调试必须由程序员完成。在涉及许多函数和变量的大型程序中，这可能是一项困难的任务。为此调试目的，我们可以在代码中插入一些 printf 语句来告诉我们中间结果。调试完成后，我们不需要这些语句，可以删除它们。但假设几天后我们再次需要调试程序，那么我们就必须再次插入所有这些语句。如果使用预处理器指令，我们有另一种更好的替代方案。使用这些指令，我们可以根据需要使这些调试语句处于活动或非活动状态。以下程序展示了这一点-

```c
#include<stdio.h>
#define DEBUG
main()
{
    int x;
    #ifdef DEBUG
        printf("Starting main()\n");
    #endif
    ............
    func();
    ............
    #ifdef DEBUG
        printf("Now value of x = %d and y = %d \n",x,y);
    #endif
    ........
}
func(){
    #ifdef DEBUG
        printf("Inside func()\n");
    #endif
    ..........
}
```

调试完成后，我们只需取消定义或删除宏 DEBUG。这将使 #ifdef 条件为假，所有调试语句都不会被编译。这样，我们就可以通过定义或删除宏 DEBUG 在调试模式和正常模式之间切换，而无需删除所有调试语句。

为每个调试语句包含 #ifdef 和 #endif 会使内容看起来更冗长且令人困惑。为了使其更简洁，我们可以定义另一个宏 SHOW。宏 SHOW 的定义方式是：如果宏 DEBUG 已定义，则 SHOW 将被替换为一个 printf 语句，而如果 DEBUG 未定义，则 SHOW 不会被替换为任何内容。

```c
#include<stdio.h>
#define DEBUG
#ifdef DEBUG
#define SHOW(message)    printf message
#else
    #define SHOW(message)
#endif
main()
{
    int x, y;
    SHOW("*Starting main()\n");
    func();
    SHOW("*Now value of x = %d and y = %d \n",x,y);
}
func()
{
    SHOW("*Inside func()\n");
}
```

这里发送给宏 SHOW 的参数 message 由控制字符串和我们想要发送给 printf() 的所有参数组成，并且这些参数需要用括号括起来。这就是为什么我们在调用 SHOW 时使用了两对括号。

## 12.11.7 Commenting A Part Of Code

假设在测试时或出于其他原因，我们想要注释掉源代码中包含许多注释的部分。这不能使用我们通常的技术（/*.... */）来完成，因为 C 中注释不能嵌套。因此，这里我们可以使用条件编译指令来注释掉源代码的部分

```c
#include<stdio.h>
#define COMMENT
main()
{
    .........
    .........
    #ifndef COMMENT
        statement...     /* ...comment ....*/
        statement...     /* ...comment.....*/      Code to be commented
    #endif
    .......
    .......
}
```

如果宏 COMMENT 已定义，则代码将被注释掉（不编译），如果该宏未定义，则它将被视为常规代码并进行编译。

## 12.11.8 Other Uses of conditional compilation

如果打开任何头文件，你会看到文件的整个内容都被 #ifndef ... #endif 指令包围。例如，如果我们打开 stdio.h 文件

```c
#ifndef __STDIO_H
#define __STDIO_H
....contents of stdio.h file.....
#endif
```

这种编码方式确保此文件的内容只会被包含一次。第一次包含 stdio.h 文件时，预处理器发现宏 __STDIO_H 未定义，因此它定义此宏并包含文件内容。此后，每当在程序中包含 stdio.h 时，预处理器发现宏 __STDIO_H 已定义，因此它跳过 #ifndef 和 #endif 之间的所有语句。

我们可以使用类似的策略来避免程序中的多次定义。例如，常量 NULL 的定义可能需要由 stdio.h、stdlib.h、string.h、alloc.h 等多个文件使用。此常量可以在所有这些文件中定义，但如果我们包含多个具有 NULL 定义的文件，则程序将有 NULL 的多个定义。因此，NULL 的定义被放在单独的文件 _null.h 中，并且该文件被包含在所有其他文件中。

这些文件不会直接包含 _null.h 文件，而是将包含指令放在 #ifndef 和 #endif 内部，如下所示-

```c
#ifndef NULL
#include<_null.h>
#endif
```

现在只有在 NULL 未定义时才会包含此文件。

## 12.12 Predefined Macro Names

存在某些预定义宏名称，不能通过 #undef 或 #define 取消定义或重新定义。

| 宏 | 描述 |
|---|---|
| __DATE__ | 表示编译日期的字符串常量，格式为 "mm dd yyyy" |
| __TIME__ | 表示编译时间的字符串常量，格式为 "hh:mm:ss" |
| __FILE__ | 表示正在编译的文件名的字符串常量。 |
| __LINE__ | 表示正在编译的行号的十进制常量。 |
| __STDC__ | 十进制常量，如果使用 ANSI 标准编译则为 1 |

```c
/*P12.20 Program to display the values of predefined constants*/
#include<stdio.h>
main( )
{
    printf("%s\n", __DATE__);
    printf("%s\n", __TIME__);
    printf("%s\n", __FILE__);
    printf("%d\n", __LINE__);
}
```

输出:
Sep 24 2003
10:24:42

宏 __FILE__ 和 __LINE__ 可用于在程序中编写错误消息，可指示发生错误的行号和文件名。

## 12.13 #line

该指令用于调试目的。

语法:

```c
#line dec_const string_const
```

这里 dec_const 是任意十进制常量，string_const 是任意字符串常量。该指令将 dec_const 和 string_const 分别赋给宏 __LINE__ 和 __FILE__。如果未指定 string_const，则宏 __FILE__ 保持不变。

```c
/* P12.21 Program to understand the use of #line, name of this file is prog.c */
#include<stdio.h>
main()
{
    printf("C in depth\n");
    printf("%d %s\n",__LINE__,__FILE__);
    #line 25 "myprog.c"
    printf("%d %s\n",__LINE__,__FILE__);
}
```

输出:

C in depth
6 C:\prog.c
25 myprog.c

## 12.14 #error

该预处理器指令用于调试目的。#error 指令会停止编译并显示与其关联的致命错误消息。

语法:

```c
#error message
```

```c
#error Timer not available for Windows
#endif
```

假设程序使用 ANSI C 标准编写，则此行可以插入代码开头。

```c
#ifndef __STDC__
#error This program should be run using ANSI C
#endif
```

假设有两个文件，不能同时包含，那么我们可以使用 #error 指令来阻止同时包含这两个文件。例如，假设文件 stdarg.h 和 varargs.h 不能同时包含，那么我们可以在文件中插入 #error 指令，如下所示-

```c
/*Structure of file stdarg.h*/
#ifndef __STDARG_H
#define __STDARG_H

#ifdef __VARARGS_H
#error Can't include both stdarg.h and varargs.h
#endif
...contents of file.......
#endif
```

```c
/*Structure of file varargs.h*/
#ifndef __VARARGS_H
#define __VARARGS_H

#ifdef __STDARG_H
#error Can't include both stdarg.h and varargs.h
#endif
...contents of file.......
#endif
```

## 12.15 Null Directive

仅由符号 # 组成的预处理器指令称为空指令，它没有任何效果。

## 12.16 #pragma

这是一个实现定义的指令，允许向编译器提供各种指令

语法:

```c
#pragma name
```

这里 name 是我们想要的 pragma 的名称。不同编译器的 pragma 可能不同。你应该查阅编译器手册以了解可用的 pragma 及其详细信息。任何无法识别的 pragma 指令都会被忽略，不会显示错误或警告。Turbo C 中可用的一些 #pragma 语句如下-

# #pragma startup

它允许程序员指定应在程序启动时调用的函数，即在 main 之前
