

# 预处理器指令

# 示例

```c
#include <stdio.h>
#define a(x, y) x##y
#define b(x) #x
#define c(x) b(x)
void main() {
    printf("%s\n", c(a(sachin, tendulkar)));
    printf("%s\n", b(a(22,55)));
    printf("%s\n", b(18*));
    getch();
}
```

# 程序 14.4 标记粘贴运算符

当执行程序 14.4 时，将出现以下输出。

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_228_0.png)

输出 14.4

查看输出后，可以自己推出以下几点：

- 1. 预处理器指令会在打印前清除空白字符。因此，tendulkar 前面的空格被忽略了！
- 2. # 简单地将提供的内容原样打印，并将它们全部视为字符串。因此，它允许任何类型的值，包括字符串（字符数组）、整数、浮点数等。
- 3. 由于 # 原样打印参数，要体验标记粘贴运算符的作用会变得复杂。因为 b(a(123,45)) 仅仅会打印“a(123,45)”而不是 12345。c(x) 是被定义并调用的。

# 14.2.3 条件编译

到目前为止，读者已经学习了关于预处理器指令的基本知识。本节将通过引入条件编译构造进行更深入的探讨。如果读者在处理 `if`、`else if`、`else` 等条件构造方面足够经验，可以轻松跳过本节。

一些预处理器条件构造包括：

- #if <identifier>
- #elif <identifier>
- #else
- #endif
- #ifdef <identifier>
- #ifndef <identifier>
- #defined <identifier>
- #!defined <identifier>

接下来将讨论上述每一个构造。

```c
#define PI 3.14
#define i1 10
#define j1 20
#ifdef inc
#define dec(x) --x
#elif !defined inc
#define inc(x) ++x
#define dec(x) --x
#else
#endif
#ifdef PI
//undef PI
#endif
#if((j1-i1)>0)
#define positive 1
#else
#define negative -1
#endif
int i=10,j=11;
main() {
    printf("inc(10)=%d\n", inc(i));
    printf("dec(10)=%d\n", dec(j));
    printf("PI*10=%f\n", PI*10);
    getch();
}
```

![](img/5bbdccabcf90cef7ee48b1b48eaa187d_229_0.png)

# 程序 14.5 条件编译

在程序 14.5 中，已经存在以下指令：

- #define inc → 已在 14.2.2 节讨论过。
- #ifdef inc → 检查在此处是否定义了预处理器指令。
- #elif defined 这里的 elif 并不是什么，而是 else if 构造。此语句检查到目前为止 inc 是否未定义。在这种情况下，它是真的。随后的语句将得到执行。此语句也可以写为 #undef inc。
- #if ((j1-i1)>0) → #if defined 可以配合常量表达式一起。
- #else → 必须关闭 #if 块。
- #endif
- #undef <identifier> → #undef 构造用于取消已定义的指令。如果没有匹配到标识符，则不执行。（#undef PI 在程序 14.5 的 main() 中注释掉了）
- #defined 可以像 !defined 一样使用。

# 14.2.4. 其它指令

一些不重要的指令也存在于 ‘C’ 中。它们在本节中介绍。

# 语言

# 预处理器指令

# 14.2.4.1. NULL 指令

# 可用于预处理器指令的位置，没有用处！

# 14.2.4.2. 三标记序列 (Trigraph Sequences)

C 标记和字符集在第 1 章中详细讨论过。其中某些符号在几乎所有编译器中都。但 ANSI 决定包含三标记序列。下面是其中一些：

| 三标记序列 | 代表的字符 |
|--- |--- |
| ?? | # |
| ??/ | \ |
| ??' | ^ |
| ??( | [ |
| ??) | ] |
| !! | |
| ??< | < |
| ??> | } |
| ??- | ~ |

表 14.1 三标记序列

如果读者想尝试，请执行以下步骤：

为了测试目的，在程序中使用 printf("%%%c",);

- 1. 进入命令行提示符 (Start->Run)
- 2. 转到保存文件的路径。
- 3. 按如下编译源文件。
- 4. 编译成功后，按如下链接源文件。

B:\Folders\Dev-cpp> gcc -c graph.c，此处让编译器读取三标记序列。
B:\Folders\Dev-cpp> gcc -o output graph.c，此处是源文件名。链接成功后，在提示符中输入 output 查看答案。

# 14.2.4.3. pragma 指令

该指令被程序员用于向编译器提供各种指令。有很多选项可以与 pragma 指令一起使用。以下是其中一些：

- 1. #pragma optimize(on | off) 强制编译器根据优化列表执行优化。
- 2. #pragma warning(disable) 使用此抑制警告。例如，考虑以下代码，pragma 用于抑制初始化警告。
- 3. #pragma warning(default) 用于全局优化。
- 4. #pragma optimize("", on) 生成机器码。
- 5. #pragma warning(default:stack) 用于栈指针。

注意这些指令取决于平台。因此，结果会随平台而异。

```c
#pragma warning(disable:default)
void Test() {
    int x;
    int y = x;
}
#pragma warning(default)
int main() {
    int x;
    int y = x;
}
```
等待，OCR 文本在 pragma 部分有一些错乱。让我们根据提供的片段重建逻辑流：

# 程序 14.6 Pragma 示例

现在读者将熟悉预处理器指令。尝试回答测试部分进行测试。

# 记住

- 预处理器指令在编译阶段之前处理。
- 文件包含、宏替换、条件编译是预处理器指令的主要用法。
- #define, #ifdef, #include 是一些广泛使用的指令。
- 在程序中包含两次文件不是错误。
- 标记粘贴运算符拼接参数。
- 字符串运算符将参数视为字符串。

# 14.3 测试 (QUIZ)

- 1. 找出以下代码中的错误。

```c
#include <stdio.h>
#define SWAP(a,b,c) (temp=a,a=b,b=temp)
int main() {
    int x=10,y=20;
    SWAP(x,y,int);
    printf("%d %d",x,y);
    getch();
}
```
(a) 无错误
(b) 在括号内声明是非合法的
(c) 括号内不应进行赋值

- 2. 找出以下代码的输出。

```c
#include <stdio.h>
#define MAX(x, y) ((x)>(y)) ? (x):(y)
void main() {
    int i=10, j=5, k=0;
    k = MAX(++i, j++);
    printf("%d, %d, %d\n", i, j, k);
    getch();
}
```
(a) 12 6 12 (b) 11 5 11 (c) 12 垃圾值 (d) 垃圾值 6 11

- 3. 找出以下程序的输出。

```c
#include <stdio.h>
#define SQUARE(x) x*x
void main() {
    float a=10, b=30, c=2, d;
    d = 2*(a-b*c)/SQUARE(c);
    printf("Result = %f", d);
    getch();
}
```
(a) -100.000000 (b) -25.000000 (c) 100.000000 (d) 40.000000

- 4. 找出以下程序的答案。

```c
#include <stdio.h>
#define FUN(i, j) i##j
void main() {
    int val1=10;
    int val2=20;
    printf("%d\n", FUN(val1,2));
    getch();
}
```
(a) 20 (b) 10 (c) 1020 (d) 2010

- 5. 找出以下程序的输出。

```c
void main() {
    int i=2;
    WHILE(i<3);
    getch();
}
```
(a) India...India (b) India... India... (c) 产生错误 (d) 无输出

- 6. 找出输出/错误

```c
#include <stdio.h>
void main() {
    int i;
    #if A="i"
    printf("i?",&i);
    scanf("%d", &i);
#elif B
    printf("The number is odd");
#endif
    getch();
}
```
(a) 无错误
(b) 在 main() 内使用预处理器指令是非合法的
(c) 无输出
(d) a 和 c

7. #undef 可以在没有 #define 的情况下使用？（是/否）

8. 在程序中包含两次文件不是错误。会产生错误。（真/假）

9. 宏和函数的工作方式相同。（真/假）

10. 定义 NULL 指令。
# # 是 NULL 指令。它什么都不定义。

