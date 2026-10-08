
## C.5 复数

```c
// figC_04.c
// 复数运算。
#include <complex.h> // 用于复数类型和数学函数
#include <stdio.h>

int main(void) {
    double complex a = 3.0 + 2.0 * I;
    double complex b = 2.7 + 4.9 * I;

    printf("a is %f + %fI\n", real(a), imag(a));
    printf("b is %f + %fI\n", real(b), imag(b));

    double complex sum = a + b; // 执行复数加法
    printf("a+b is %f + %fI\n", real(sum), imag(sum));

    double complex difference = a - b; // 执行复数减法
    printf("a-b is %f + %fI\n", real(difference), imag(difference));

    double complex product = a * b; // 执行复数乘法
    printf("a*b is %f + %fI\n", real(product), imag(product));

    double complex quotient = a / b; // 执行复数除法
    printf("a/b is %f + %fI\n", real(quotient), imag(quotient));

    double complex power = cpow(a, b); // 执行复数幂
    printf("a^b is %f + %fI\n", real(power), imag(power));
}
```
a is 3.0 + 2.0I
b is 2.7 + 4.9I
a + b is 5.7 + 6.9I
a - b is 0.3 - 2.9I
a * b is -8.6 + 16.3I
a / b is 0.543585 + 0.153355I
a^b is 0.000155 + 0.000155I

**图 C.4** | 复数运算。

要使用复数，请包含 `<complex.h>` 头文件（第 3 行）。`Complex` 类型预留了恰好两个元素的数组，对应于复数的实部和虚部。在第 7、8、13、19、22 和 25 行中，将每个变量定义为 `double`，表示复数的实部和虚部存储为 `double`。它还支持 `float` 或 `long double`。

复数的算术运算符和 `<complex.h>` 头提供了额外的数学函数，如第 25 行中的 `cpow`。你可以对复数使用运算符 `+`, `*`, `/`。第 23–26 行输出了算术运算的结果。通过 `real` 和 `imag` 分别访问复数的实部和虚部，如第 26 行所示。在第 26 行的输出中，我们使用符号 `^` 表示幂。

录 C 多线程/多核以及其他 C18/C1/C99

## C.6 变长参数列表的宏

宏可以具有变长参数列表。这允许对 `printf` 等函数进行封装。例如，要在调试语句中添加当前文件名，可以如下定义宏：

```c
#define DEBUG(...)printf(__FILE__, __VA_ARGS__)
```

`DEBUG` 接收任意数量的参数，由参数列表中的 `...` 表示。与函数不同，`...` 必须是最后一个参数。以下划线开头的标识符 `__VA_ARGS__` 是变量列表的占位符。假设该宏出现在 `file.c`，预处理器会将宏调用：

```c
DEBUG("x = %d, y = %d\n", x, y);
```

替换为：

```c
printf("file.c:x = %d, y = %d\n", x, y);
```

空白分隔的字符串在预处理期间会被合并，因此三个字面量将形成 `printf` 的第一个参数。

## C.7 其他 C99 特性

提供了 C99 特性的简要概述。这些包括关键字、语言能力和标准库的扩展。

### C.7.1 编译器资源限制

[本节可以在第 15.4 节后阅读。]

在 C99 之前，标准要求 C 实现对以下标识符的支持：
- 内部链接（internal linkage）的标识符少于 31 个字符
- 外部链接（external linkage）的标识符少于六个字符

C99 将这些限制增加到内部链接 63 个字符，外部链接 31 个字符。这些是下限。编译器可以支持多于这些限制的标识符。更多信息，请参见 C18 标准的 5.2.4.1。

C 还对许多语言特性设置了最小限制。例如，结构体、枚举或联合体至少支持 1023 个成员，函数至少支持 127 个参数。关于其他限制的更多信息，请参见 C18 标准 5.2.4.1。

### C.7.2 restrict 关键字

[本节可以在第 7.5 节后阅读。]

该关键字声明了一个对内存区域具有独占访问权的 `restrict` 指针。通过 `restrict` 指针访问的对象不能被其他指针访问，除非这些指针的值源自 `restrict` 指针，例如通过将一个 `restrict` 限定的指针赋值给非 `restrict` 限定的指针。

我们可以这样声明一个指向 `int` 的 `restrict` 指针：

```c
int *restrict ptr;
```

`restrict` 指针允许编译器优化内存访问。例如，标准库函数 `memcpy` 定义如下：
`void *memcpy(void *restrict s1, const void *restrict s, size_t n);`

函数规范规定不应在重叠的内存区域之间拷贝。使用 `restrict` 指针允许通过同时拷贝多个字节来优化拷贝操作，这样效率更高。当另一个指针指向同一内存区域时将其声明为 `restrict` 会未定义行为。更多信息，请参见 C99 标准 6.7.3.1。

### C.7.3 可靠的整数除法

[本节可以在第 2.5 节后阅读。]

在早期 C 编译器中，整数除法的行为随实现而异。某些实现将负商向负无穷舍入，而另一些则向零舍入，导致产生不同的答案。将 `-28` 除以 `5`：精确答案是 `-5.6`。如果我们向零舍入，得到 `-5`。如果我们将 `-5.6` 向负无穷舍入，得到 `-6`。今天的编译器简单地丢弃小数部分（相当于向零舍入），使得整数除法结果在各个系统中都是可靠的。更多信息，请参见 C 标准 6.5.5。

### C.7.4 灵活数组成员

[本节可以在第 10.3 节后阅读。]

结构体的最后一个成员可以是长度未指定的数组，如下：

```c
struct s {
    int arraySize;
    int array[];
};
```

这被称为灵活数组成员，通过在名称后指定空方括号 `[]` 来声明。要分配带有灵活数组成员的结构体，使用如下代码：

```c
int desiredSize = 5;
struct s *ptr = malloc(sizeof(struct s) + sizeof(int) * desiredSize);
```

`sizeof` 运算符忽略灵活数组成员，因此 `sizeof(struct s)` 返回结构体除灵活数组成员外的所有成员的大小。我们通过 `sizeof(int) * desiredSize` 分配的额外空间是灵活数组的大小。

## 灵活数组成员限制

灵活数组成员有许多限制：

# 附录 C 多线程/多核以及其他 C18/C99 话题

- 灵活数组可以被声明为结构体的最后一个成员，因此每个结构体最多可以包含一个灵活数组成员。
- 灵活数组不能是结构体的唯一成员——结构体必须有一个或多个固定大小的成员。
- 包含灵活数组的结构体不能作为另一个结构体的成员。
- 带有灵活数组的结构体必须动态分配内存。你无法在编译时固定灵活数组成员的大小。

欲需更多信息，请参阅 C99 标准第 6.7.2.1 节。

## C.7.5 类型泛型数学

[本节可以在第 5.3 节后阅读。]
`<math.h>` 头文件为 `<math.h>` 中的许多函数提供了类型泛型宏。例如，在包含 `<math.h>` 后，表达式 `sin(x)` 将调用：

- 如果 `x` 是 `float`（单点型），则调用 `sinf`（sin 的浮点版本）；
- 如果 `x` 是 `double`（双精度浮点型），则调用 `sin`（接受 `double` 参数）；
- 如果 `x` 是 `long double`（长双浮点型），则调用 `sinl`（sin 的 `long double` 版本）；
- 如果 `x` 是复数，则调用 `cssin`、`csinf` 或 `cssl` 之一（复数类型的 sin 函数）。

C11/C18 增加了更多泛型，我们将在本附录后续部分提到。

## C.7.6 内联函数

[本节可以在第 5.5 节后阅读。]
你可以通过在函数声明前使用 `inline` 关键字来声明内联函数，例如：

```
inline void someFunction();
```
