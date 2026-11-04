
例如，如果用户输入 2 和 5，程序会显示：

i+j = 7
i*j+i*j = 20

## 运算符用于将标识符合并在一起。它不允许出现在序列的开头或末尾。如果该标识符是宏参数，预处理器会先将其替换为实参的值，然后进行粘贴。例如：

```
#include <stdio.h>

#define f(a) s##u##m##a

int sum1(int a, int b);

int main(void)
{
    int i, j;

    printf("Enter numbers: ");
    scanf("%d%d", &i, &j);
    printf("%d\n", f(1)(i, j));
    return 0;
}

int sum1(int a, int b)
{
    return a+b;
}
```

当预处理器展开 f 宏时，因为字符 a 与参数同名，预处理器会将 a 替换为参数的值，即 1，然后将该值与 s、u 和 m 字符合并。因此，f(1)(i, j) 被展开为 sum1(i, j)，程序调用 sum1() 来显示两个输入数字之和。

## 预处理器指令与条件编译

本节讨论允许对程序的一部分进行条件编译的预处理器指令。条件编译在许多情况下非常有用，例如调试程序、监视程序执行，或维护同一程序的多个版本。

### #if、#else、#elif 和 #endif 指令

#if 和 #endif 指令用于根据表达式的值定义程序的哪些部分将被编译。一般语法为：

```
#if expression
... /* block of statements */
#endif
```

该表达式是一个常量整数表达式，不允许包含 sizeof、强制类型转换或枚举常量。如果其值为真，预处理器会保留要编译的语句块。否则，该语句块将被移除，编译器不会看到它。请注意，如果表达式是未定义的标识符，则 #if 指令求值为假。例如：

```
#if NUM
```

如果 NUM 未定义，结果为假，而 #if !NUM 的值为真。如果 NUM 定义为 0，则 #if NUM 求值为假，#if !NUM 求值为真。

#else 指令与 #if 指令一起使用，用于定义当表达式值为假时将被编译的语句块。

```
#if expression
... /* block of statements A */
#else
... /* block of statements B */
#endif
```

例如，在下面的程序中，#else 部分将被编译，因为 NUM 大于 0：

```
#include <stdio.h>

#define NUM 10

int main(void)
{
    #if NUM < 0
        printf("Seg_1\n");
    #else
        printf("Seg_2\n");
    #endif
    return 0;
}
```

因此，程序显示 Seg_2。请注意，如果缺少 NUM 的定义，程序也会显示 Seg_2。

由于不允许嵌套注释，因此不能将程序中包含注释的部分放入注释中。相反，我们可以使用 #if 指令。例如：

```
#if 0
    /* Comment. */
    ...    /* Code. */
    /* Another comment. */
#endif
```

#elif 指令可以与 #if、#ifdef 和 #ifndef 指令一起使用，以定义多个编译路径。例如：

```c
#if expression_A
    ... /* block of statements A */
#elif expression_B
    ... /* block of statements B */
.
.
#else
    ... /* block of statements N */
#endif
```

仅当 expression_A 的值为假且 expression_B 的值为真时，才会编译第二个语句块。一旦发现某个 #if 或 #elif 表达式为真，后续的 #elif 和 #else 指令就会被丢弃。最后一个 #else 是可选的，仅当之前的表达式均为假时，才会编译其语句块。在实践中，我们经常使用这种语法来支持同一程序的多个版本。例如：

```c
#include <stdio.h>

#define VER_2 1

int main(void)
{
    int cnt = 0;

    #if VER_1
        cnt = 1;
        printf("Version_1\n");
    #elif VER_2
        cnt = 2;
        printf("Version_2\n");
    #else
        cnt = 3;
        printf("Version_3\n");
    #endif

    printf("Cnt = %d\n", cnt);
    return 0;
}
```

由于 VER_1 未定义且 VER_2 的值为真，预处理器会保留这些行并丢弃其余部分，cnt 变为 2，程序显示：

```text
Version_2
Cnt = 2
```

如果我们将 VER_2 的值改为 0，则 #elif 表达式变为假，预处理器会保留 #else 指令的行。因此，程序显示：

```
Version_3
Cnt = 3
```

如果缺少 #else 指令，程序将显示：Cnt = 0

### #ifdef、#ifndef 和 #undef 指令

#ifdef 指令用于检查某个标识符是否被定义为宏。一般语法为：

```
#ifdef name
... /* block of statements */
#endif
```

与 #if 指令的区别在于，#ifdef 指令只检查标识符是否被定义为宏；它不对其值进行求值。例如：

```
#include <stdio.h>

#define VER_1 0

int main(void)
{
    #ifdef VER_1
        printf("Version_1\n");
    #else
        printf("Version_2\n");
    #endif
    return 0;
}
```

由于 VER_1 已定义，程序显示 Version_1。

#ifndef 指令用于检查某个标识符是否未被定义为宏。#ifndef 指令的一个典型用途是防止同一文件被多次包含。这不仅是为了避免不必要的重新编译并节省一些时间，还有另一个原因。假设一个程序由多个源文件组成，其中一些源文件包含了同一个文件（例如 test.h）。如果 test.h 包含类型定义（例如结构体），则编译将失败，因为不允许重新定义相同的类型。为了避免这种情况，我们在其开头添加以下行：

```
#ifndef SOME_TAG /* Use a name not defined somewhere else. */
#define SOME_TAG
/* Contents of test.h */
#endif
```

一旦包含 test.h 的第一个文件被编译，预处理器就会包含 test.h 的内容，因为 SOME_TAG 宏尚未定义。在后续包含 test.h 时，预处理器会跳过其内容，因为 SOME_TAG 已定义，且 #ifdef 求值为假。常见的做法是为 SOME_TAG 选择一个与头文件名相似的名称。

此外，使用 #ifndef 可以防止无限包含。例如，如果一个文件（例如 one.h）包含第二个文件（例如 sec.h），而第二个文件又包含第一个文件，就可能发生这种情况。

#undef 指令取消宏的定义。如果该宏尚未定义，#undef 没有效果。例如：

```c
#include <stdio.h>

#define NUM 100

int main(void)
{
    int arr[NUM];
#undef NUM

    printf("Array contains %d elements\n", NUM);
    return 0;
}
```

由于指令 #undef NUM 取消了 NUM 的定义，编译器将在 printf() 中产生错误消息。

### defined 运算符

检查标识符是否被定义为宏的另一种方法是使用 defined 运算符。defined 运算符通常与 #if 或 #elif 指令一起使用。例如：

```c
#if defined(VER_1) /* Equivalent to #ifdef VER_1 */
...
#endif
```

括号不是必需的；这取决于个人偏好。类似地，表达式 #if !defined(VER_1) 等价于 #ifndef VER_1。与 #ifdef 和 #ifndef 相比的优势在于，它们只能用于检查某一个宏是否已定义，而 defined 运算符和 #if 指令可用于检查多个宏。看看我们如何使用 && 运算符检查多个条件：

```c
#if defined(VER_1) && !defined(VER_2) && defined(VER_3)
...
#endif
```

或者使用 || 运算符检查某个宏是否已定义：

```c
#if defined(VER_1) || defined(VER_2)
...
#endif
```

下面是条件编译的另一个常见应用。假设我们正在编写一个依赖于某些外部因素的程序，例如操作系统或编译器。我们可以使用条件编译，而不是编写不同的版本。例如：

```c
#if defined(UNIX)
...
#elif defined(LINUX)
...
#elif defined(WINDOWS)
...
#endif
```

在程序开头定义相应的宏，预处理器就会保留对应的代码。

### 其他指令

在继续练习之前，我们简要讨论一下 #error、#line 和 #pragma 指令。

#error 指令的语法为 #error message，它指示预处理器显示一条包含 message 的错误消息。编译会失败。通常，它用于 #if-#elif-#else 系列的 #else 部分，以指示不期望出现的情况。例如：

```c
#if defined(VER_1)
...
#elif defined(VER_2)
...
#else
#error Unspecified version
#endif
```

#line 指令有两种形式。第一种是 #line n，其中 n 是整数。它将程序中后续行的编号改为 n、n+1、n+2、…… 第二种形式是 #line n "file"，编译器会假定该指令之后的行来自 file，并且行号从 n 开始。

#pragma 指令用于请求编译器执行特殊行为。可以出现在 #pragma 指令中的命令集因编译器而异。如果该命令不受支持，编译器会忽略该指令。例如，如果编译器支持 warning 命令，则可以使用指令 #pragma warning(disable: 4244) 来禁止出现代码为 4244 的警告消息。

