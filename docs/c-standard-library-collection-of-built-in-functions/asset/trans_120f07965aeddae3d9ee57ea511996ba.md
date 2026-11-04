

```
Going to sleep for a second...
Going to sleep for a second...
Going to sleep for a second...
Caught signal 2, coming out...
```

## int raise(int sig)

### 描述
C 库函数 int raise(int sig) 会生成信号 sig。sig 参数与 SIG 宏兼容。

### 声明
以下是 raise() 函数的声明。

```c
int raise(int sig)
```

### 参数
- sig -- 这是要发送的信号编号。以下是一些重要的标准信号常量：

| 宏 | 信号 |
|---|---|
| SIGABRT | （信号中止）异常终止，例如由 abort 函数发起的终止。 |
| SIGFPE | （信号浮点异常）错误的算术运算，例如除零或导致溢出的运算（不一定是浮点运算）。 |
| SIGILL | （信号非法指令）无效的函数映像，例如非法指令。这通常是由于代码损坏或试图执行数据所致。 |
| SIGINT | （信号中断）交互式注意信号。通常由应用程序用户生成。 |
| SIGSEGV | （信号段违规）对存储器的无效访问：当程序试图读取或写入为其分配的内存之外时。 |
| SIGTERM | （信号终止）发送给程序的终止请求。 |

### 示例
```c
    printf("!! signal caught !!\n");
}
```

让我们编译并运行上面的程序，以产生以下结果：

```
Going to raise a signal
!! signal caught !!
Exiting...
```

## 简介
stdarg.h 头文件定义了一种变量类型 **va_list** 以及三个宏，当参数数量未知（即参数数量可变）时，可使用这些宏获取函数中的参数。

可变参数函数通过在参数列表末尾使用省略号（...）来定义。

## 库变量
以下是 stdarg.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1 | **va_list**<br>这是一种适合保存三个宏 **va_start()**、**va_arg()** 和 **va_end()** 所需信息的类型。 |

## 库宏
以下是 stdarg.h 头文件中定义的宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | `void va_start(va_list ap, last_arg)`<br>该宏初始化 **ap** 变量，以便与 **va_arg** 和 **va_end** 宏一起使用。**last_arg** 是传递给函数的最后一个已知固定参数，即省略号之前的参数。 |
| 2 | `type va_arg(va_list ap, type)`<br>该宏获取函数参数列表中类型为 **type** 的下一个参数。 |
| 3 | `void va_end(va_list ap)`<br>该宏允许使用 va_start 宏的可变参数函数返回。如果在从函数返回之前未调用 va_end，则结果未定义。 |

## void va_start(va_list ap, last_arg)

### 描述
C 库宏 **void va_start(va_list ap, last_arg)** 初始化 **ap** 变量，以便与 **va_arg** 和 **va_end** 宏一起使用。**last_arg** 是传递给函数的最后一个已知固定参数，即省略号之前的参数。

在使用 **va_arg** 和 **va_end** 之前必须先调用此宏。

### 声明
以下是 va_start() 宏的声明。

```c
    void va_start(va_list ap, last_arg);
```

### 参数
- **ap** -- 这是 **va_list** 的对象，它将保存使用 **va_arg** 获取额外参数所需的信息。
- **last_arg** -- 这是传递给函数的最后一个已知固定参数。

### 返回值
无

### 示例
以下示例展示了 va_start() 宏的用法。

```c
    #include<stdarg.h>
    #include<stdio.h>

    int sum(int, ...);

    int main(void)
    {
        printf("Sum of 10, 20 and 30 = %d\n", sum(3, 10, 20, 30) );
        printf("Sum of 4, 20, 25 and 30 = %d\n", sum(4, 4, 20, 25, 30) );

        return 0;
    }
```

## type va_arg(va_list ap, type)

### 参数
- **type** -- 这是一个类型名称。此类型名称用作该宏展开后表达式的类型。

### 返回值
该宏返回下一个额外参数，作为类型为 **type** 的表达式。

### 示例
以下示例展示了 va_arg() 宏的用法。

```c
#include <stdarg.h>
#include <stdio.h>

int sum(int, ...);

int main()
{
    printf("Sum of 15 and 56 = %d\n",  sum(2, 15, 56) );
    return 0;
}

int sum(int num_args, ...)
{
    int val = 0;
    va_list ap;
    int i;

    va_start(ap, num_args);
    for(i = 0; i < num_args; i++)
    {
        val += va_arg(ap, int);
    }
    va_end(ap);

    return val;
}
```

让我们编译并运行上面的程序，以产生以下结果：

```
Sum of 15 and 56 = 71
```

## void va_end(va_list ap)

### 描述
C 库宏 void va_end(va_list ap) 允许使用了 va_start 宏的可变参数函数返回。如果在从函数返回之前未调用 va_end，则结果未定义。

### 声明
以下是 va_end() 宏的声明。

```c
void va_end(va_list ap)
```

### 参数
- ap -- 这是之前由同一函数中的 va_start 初始化的 va_list 对象。

### 返回值
该宏不返回任何值。

### 示例
以下示例展示了 va_end() 宏的用法。

```c
#include <stdarg.h>
#include <stdio.h>

int mul(int, ...);

int main()
{
    printf("15 * 12 = %d\n",  mul(2, 15, 12) );

    return 0;
}

int mul(int num_args, ...)
{
    int val = 1;
    va_list ap;
    int i;

    va_start(ap, num_args);
    for(i = 0; i < num_args; i++)
    {
        val *= va_arg(ap, int);
    }
    va_end(ap);

    return val;
}
```

让我们编译并运行上面的程序，以产生以下结果：

```
15 * 12 =  180
```

## 简介
stddef.h 头文件定义了各种变量类型和宏。其中许多定义也出现在其他头文件中。

## 库变量
以下是 stddef.h 头文件中定义的变量类型：

| 序号 | 变量与描述 |
|------|------------------------|
| 1 | ptrdiff_t<br>这是一种有符号整型，是两个指针相减的结果。 |
| 2 | size_t<br>这是一种无符号整型，是 sizeof 关键字的结果。 |
| 3 | wchar_t<br>这是一种大小与宽字符常量相同的整型。 |

## 库宏
以下是 stddef.h 头文件中定义的宏：

| 序号 | 宏与描述 |
|------|---------------------|
| 1 | NULL<br>该宏是空指针常量的值。 |
| 2 | offsetof(type, member-designator)<br>这会生成一个类型为 size_t 的常量整数，它是结构体成员距结构体起始位置的字节偏移量。该成员由 member-designator 给出，结构体名称由 *type* 给出。 |

## NULL

### 描述
C 库宏 **NULL** 是空指针常量的值。根据编译器供应商的不同，它可能定义为 **((void*)0)**、**0** 或 **0L**。

### 声明
根据编译器的不同，NULL 宏的声明可能如下。

```c
#define NULL ((char *)0)

or

#define NULL 0L

or

#define NULL 0
```

### 参数
- 无

### 返回值
- 无

### 示例
以下示例展示了 NULL 宏的用法。

```c
#include <stddef.h>
#include <stdio.h>

int main ()
{
    FILE *fp;

    fp = fopen("file.txt", "r");
    if( fp != NULL )
    {
        printf("Opened file file.txt successfully\n");
        fclose(fp);
    }

    fp = fopen("nofile.txt", "r");
    if( fp == NULL )
    {
        printf("Could not open file nofile.txt\n");
    }

    return(0);
}
```

假设我们有一个已存在的文件 **file.txt**，但 **nofile.txt** 不存在。让我们编译并运行上面的程序，它将产生以下结果：

```
Opened file file.txt successfully
Could not open file nofile.txt
```

## offsetof(type, member-designator)

### 描述
C 库宏 **offsetof(type, member-designator)** 会生成一个类型为 **size_t** 的常量整数，它是结构体成员距结构体起始位置的字节偏移量。该成员由 member-designator 给出，结构体名称由 type 给出。

### 声明
以下是 offsetof() 宏的声明。

```c
offsetof(type, member-designator)
```

### 参数
- **type** -- 这是类类型，其中 member-designator 是有效的成员指示符。
- **member-designator** -- 这是类类型的成员指示符。

### 返回值
该宏返回类型为 **size_t** 的值，即成员在 type 中的偏移值。

