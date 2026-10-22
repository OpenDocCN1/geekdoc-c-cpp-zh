
这是另一种用途。假设我们将这一行

```c
#include "arrays.h"
```

放在文件开头。这会使 `SIZE` 被定义为 100。但将

```c
#define SIZE 10
#include "arrays.h"
```

放在文件开头，则会将 `SIZE` 定义为 10。这里，在处理 `arrays.h` 中的各行时，`SIZE` 已经被定义，因此 `#define SIZE 100` 这一行会被跳过。例如，你可以这样做来测试一个使用更小数组大小的程序。当程序按你的要求正常工作时，你可以删除 `#define SIZE 10` 这条语句并重新编译。这样，你就不必担心修改数组头文件本身了。

`#ifndef` 指令通常用于防止一个文件被多次包含。也就是说，头文件通常按照以下方式设置：

```c
/* things.h */
#ifndef THINGS_H_
    #define THINGS_H_
    /* rest of include file */
#endif
```

假设这个文件由于某种原因被包含了多次。当预处理器第一次遇到这个包含文件时，`THINGS_H_` 尚未定义，因此程序会继续定义 `THINGS_H_` 并处理文件的其余部分。下一次预处理器遇到这个文件时，`THINGS_H_` 已经被定义，因此预处理器会跳过文件的其余部分。

为什么要多次包含一个文件呢？最常见的原因是许多包含文件本身又包含其他文件，因此你可能会显式地包含一个另一个包含文件已经包含过的文件。为什么这会成为问题？因为包含文件中出现的一些项（如结构类型声明）在一个文件中只能出现一次。标准 C 头文件使用 `#ifndef` 技术来避免多次包含。其中一个问题是要确保你正在测试的标识符没有在其他地方被定义。供应商通常的解决办法是使用文件名作为标识符，采用大写形式，将句点替换为下划线，并使用一个下划线（也许两个下划线）作为前缀和后缀。例如，如果你检查自己的 `stdio.h` 头文件，你很可能会发现类似这样的内容：

```c
#ifndef _STDIO_H
#define _STDIO_H
// contents of file
#endif
```

你也可以做类似的事情。但是，你应该避免使用下划线作为前缀，因为标准规定这种用法是保留的。你不会希望意外定义一个与标准头文件中的某些内容冲突的宏。程序清单 16.10 使用 `#ifndef` 为程序清单 16.6 中的头文件提供多重包含保护。

## 程序清单 16.10 names.h 头文件

```c
// names.h --revised with include protection

#ifndef NAMES_H_
#define NAMES_H_

// constants
#define SLEN 32

// structure declarations
struct names_st
{
    char first[SLEN];
    char last[SLEN];
};

// typedefs
typedef struct names_st names;

// function prototypes
void get_names(names *);
void show_names(const names *);
char * s_gets(char * st, int n);

#endif
```

你可以使用程序清单 16.11 中的程序测试这个头文件。当使用程序清单 16.10 中显示的头文件时，这个程序应该能正确工作；如果你从程序清单 16.10 中移除 `#ifndef` 保护，它应该编译失败。

## 程序清单 16.11 doubincl.c 程序

```c
// doubincl.c -- include header twice
#include <stdio.h>
#include "names.h"
#include "names.h"  // accidental second inclusion

int main()
{
    names winner = {"Less", "Ismoor"};
    printf("The winner is %s %s.\n", winner.first,
           winner.last);
    return 0;
}
```

## #if 和 #elif 指令

`#if` 指令与常规的 C `if` 更相似。它后面跟着一个常量整数表达式，如果该表达式非零，则被视为真；你可以在其中使用 C 的关系运算符和逻辑运算符：

```c
#if SYS == 1
#include "ibm.h"
#endif
```

你可以使用 `#elif` 指令（在某些较旧的实现中不可用）来扩展 `if`-`else` 序列。例如，你可以这样做：

```c
#if SYS == 1
    #include "ibmpc.h"
#elif SYS == 2
    #include "vax.h"
#elif SYS == 3
    #include "mac.h"
#else
    #include "general.h"
#endif
```

较新的实现提供了另一种测试名称是否已定义的方法。除了使用

```c
#ifdef VAX
```

你也可以使用这种形式：

```c
#if defined (VAX)
```

这里，`defined` 是一个预处理器运算符，如果其参数已被 `#defined`，则返回 1，否则返回 0。这种新形式的优点是它可以与 `#elif` 一起使用。利用它，你可以将前面的示例改写成这样：

```c
#if defined (IBMPC)
    #include "ibmpc.h"
#elif defined (VAX)
    #include "vax.h"
#elif defined (MAC)
    #include "mac.h"
#else
    #include "general.h"
#endif
```

例如，如果你在一台 VAX 机器上使用这些代码行，你需要在文件前面的某个位置用这样一行定义 VAX：

```c
#define VAX
```

条件编译功能的一个用途是使程序更具可移植性。通过更改文件开头的一些关键定义，你可以为不同的系统设置不同的值并包含不同的文件。

## 预定义宏

C 标准规定了几种预定义宏，表 16.1 列出了这些宏。

| 宏 | 含义 |
|-------|---------|
| `__DATE__` | 一个字符字符串字面量，形式为 "Mmm dd yyyy"，表示预处理时的日期，例如 Nov 23 2013 |
| `__FILE__` | 一个表示当前源代码文件名的字符串字面量 |
| `__LINE__` | 一个表示当前源代码文件中行号的整型常量 |
| `__STDC__` | 设置为 1 表示实现符合 C 标准 |
| `__STDC_HOSTED__` | 对于宿主环境设置为 1；否则为 0 |
| `__STDC_VERSION__` | 对于 C99，设置为 199901L；对于 C11，设置为 201112L |
| `__TIME__` | 以 "hh:mm:ss" 形式表示的翻译时间 |

在我们讨论预定义标识符时，C99 标准规定了一个名为 `__func__` 的标识符。它展开为一个字符串，表示包含该标识符的函数名称。因此，这个标识符必须具有函数作用域，而宏本质上具有文件作用域。所以，`__func__` 是 C 语言的预定义标识符，而不是预定义宏。

## 程序清单 16.12 predif.c 程序

```c
// predif.c -- predefined identifiers
#include <stdio.h>
void why_me();

int main()
{
    printf("The file is %s.\n", __FILE__);
    printf("The date is %s.\n", __DATE__);
    printf("The time is %s.\n", __TIME__);
    printf("The version is %ld.\n", __STDC_VERSION__);
    printf("This is line %d.\n", __LINE__);
    printf("This function is %s\n", __func__);
    why_me();

    return 0;
}

void why_me()
{
    printf("This function is %s\n", __func__);
    printf("This is line %d.\n", __LINE__);
}
```

下面是一个示例运行：

```c
The file is predef.c.
The date is Sep 23 2013.
The time is 22:01:09.
The version is 201112.
This is line 11.
This function is main
This function is why_me
This is line 21.
```

## #line 和 #error

`#line` 指令允许你重置 `__LINE__` 和 `__FILE__` 宏所报告的行号和文件名。你可以像这样使用 `#line`：

```c
#line 1000    // reset current line number to 1000
#line 10 "cool.c" // reset line number to 10, file name to cool.c
```

`#error` 指令会促使预处理器发出一条错误消息，其中包含该指令中的所有文本。如果可能的话，编译过程应该停止。你可以像这样使用该指令：

```c
#if __STDC_VERSION__ != 201112L
#error Not C11

#endif
```

然后尝试编译该程序可能会产生如下结果：

```c
$ gcc newish.c
newish.c:14:2: error: #error Not C11
$ gcc -std=c11 newish.c
$
```

当编译器使用较旧的标准时，编译过程会失败；而当它使用 C11 标准时，编译过程会成功。

## #pragma

现代编译器有若干设置，可以通过命令行参数或使用 IDE 菜单进行修改。`#pragma` 允许你在源代码中放置编译器指令。例如，在 C99 标准开发期间，它被称为 C9X，一家编译器使用了以下 pragma 来开启 C9X 支持：

```c
#pragma c9x on
```

通常，每种编译器都有自己的 pragma 集合。例如，它们可能用于控制为自动变量预留的内存量、设置错误检查的严格程度，或启用非标准语言特性。C99 标准确实提供了三个技术性较强的标准 pragma，但这里就不讨论了。

C99 还提供了 `_Pragma` 预处理器运算符。它可以将一个字符串转换为普通的 pragma。例如，

```c
_Pragma("nonstandardtreatmenttypeB on")
```

等价于以下内容：

```c
#pragma nonstandardtreatmenttypeB on
```

由于该运算符不使用 `#` 符号，你可以将它用作宏展开的一部分：

```c
#define PRAGMA(X) _Pragma(#X)
#define LIMRG(X) PRAGMA(STDC CX LIMITED RANGE  X)
```

然后你可以使用这样的代码：

```c
LIMRG ( ON )
```

顺便说一下，下面的定义并不起作用，尽管它看起来似乎可以：

```c
#define LIMRG(X) _Pragma(STDC CX_LIMITED_RANGE  #X)
```

问题在于它依赖于字符串拼接，但编译器要等到预处理完成之后才会拼接字符串。

`_Pragma` 运算符会完整地执行“去字符串化”操作；也就是说，字符串中的转义序列会被转换成它们所代表的字符。因此，

```c
_Pragma("use_bool \"true \"false")
```

