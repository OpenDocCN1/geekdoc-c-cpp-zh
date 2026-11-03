
```c
// Fig. 7.16: fig07_16.c
// Applying sizeof to an array name returns
// the number of bytes in the array.
#include <stdio.h>
#define SIZE 20

size_t getSize(float *ptr); // prototype

int main(void)
{
    float array[SIZE]; // create array

    printf("The number of bytes in the array is %u\n"
           "The number of bytes returned by getSize is %u\n",
           sizeof(array), getSize(array));
}

// return size of ptr
size_t getSize(float *ptr)
{
    return sizeof(ptr);
}
```

The number of bytes in the array is 80
The number of bytes returned by getSize is 4

图 7.16 | 对数组名应用 `sizeof` 会返回数组中的字节数。

数组中的元素个数也可以用 `sizeof` 确定。例如，考虑下面的数组定义：

```c
double real[22];
```

`double` 类型的变量通常存储在 8 字节内存中。因此，数组 `real` 总共包含 176 字节。要确定数组中的元素个数，可以使用下面的表达式：

```c
sizeof(real) / sizeof(real[0])
```

该表达式确定数组 `real` 中的字节数，并将该值除以在内存中存储数组 `real` 第一个元素（一个 `double` 值）所用的字节数。即使函数 `getSize` 接收一个包含 20 个元素的数组作为实参，该函数的形参 `ptr` 也只是一个指向数组第一个元素的指针。当对指针使用 `sizeof` 时，它返回的是指针的大小，而不是该指针所指向项的大小。在我们的 Windows 和 Linux 测试系统上，指针的大小是 4 字节，因此 `getSize` 返回 4；在我们的 Mac 上，指针的大小是 8 字节，因此 `getSize` 返回 8。此外，上面展示的用 `sizeof` 确定数组元素个数的计算方法只在使用实际数组时有效，而在使用指向该数组的指针时无效。确定标准类型、数组和指针的大小 图 7.17 计算存储每种标准数据类型所用的字节数。该程序的结果取决于具体实现，并且经常因平台不同而不同，有时在同一平台上的不同编译器之间也不同。输出显示了我们在使用 Visual C++ 编译器的 Windows 系统上的结果。在使用 GNU gcc 编译器的 Linux 系统上，`long double` 的大小是 12 字节。在使用 Xcode 的 LLVM 编译器的 Mac 系统上，`long` 的大小是 8 字节，`long double` 的大小是 16 字节。

```c
1 // Fig. 7.17: fig07_17.c
2 // Using operator sizeof to determine standard data type sizes.
3 #include <stdio.h>
4
5 int main(void)
6 {
7    char c;
8    short s;
9    int i;
10   long l;
11   long long ll;
12   float f;
13   double d;
14   long double ld;
15   int array[20]; // create array of 20 int elements
16   int *ptr = array; // create pointer to array
17
18   printf( "sizeof c = %u\tsizeof(char) = %u"
19          "\n     sizeof s = %u\tsizeof(short) = %u"
20          "\n     sizeof i = %u\tsizeof(int) = %u"
21          "\n     sizeof l = %u\tsizeof(long) = %u"
22          "\n     sizeof ll = %u\tsizeof(long long) = %u"
23          "\n     sizeof f = %u\tsizeof(float) = %u"
24          "\n     sizeof d = %u\tsizeof(double) = %u"
25          "\n     sizeof ld = %u\tsizeof(long double) = %u"
26          "\n     sizeof array = %u"
27          "\n     sizeof ptr = %u\n",
28          sizeof c, sizeof(char), sizeof s, sizeof(short), sizeof i,
29          sizeof(int), sizeof l, sizeof(long), sizeof ll,
30          sizeof(long long), sizeof f, sizeof(float), sizeof d,
31          sizeof(double), sizeof ld, sizeof(long double),
32          sizeof array, sizeof ptr);
33 }
```

sizeof c = 1            sizeof(char) = 1
sizeof s = 2            sizeof(short) = 2
sizeof i = 4            sizeof(int) = 4
sizeof l = 4            sizeof(long) = 4
sizeof ll = 8           sizeof(long long) = 8
sizeof f = 4            sizeof(float) = 4
sizeof d = 8            sizeof(double) = 8
sizeof ld = 8           sizeof(long double) = 8
sizeof array = 80
sizeof ptr = 4

图 7.17 | 使用运算符 `sizeof` 确定标准数据类型的大小。

## 可移植性提示 7.1

存储特定数据类型所用的字节数可能因系统而异。编写依赖数据类型大小并且将在多个计算机系统上运行的程序时，请使用 `sizeof` 确定存储这些数据类型所用的字节数。

运算符 `sizeof` 可应用于任何变量名、类型或值（包括表达式的值）。当应用于变量名（不是数组名）或常量时，返回存储该特定类型变量或常量所用的字节数。当提供类型作为 `sizeof` 的操作数时，必须使用括号。

## 7.8 指针表达式与指针算术

指针是算术表达式、赋值表达式和比较表达式中的有效操作数。然而，并非这些表达式中通常使用的所有运算符都能与指针变量一起有效使用。本节介绍可以将指针作为操作数的运算符，以及这些运算符的用法。

### 7.8.1 指针算术允许的运算符

指针可以递增（+）或递减（--），整数可以加到指针上（+ 或 +=），整数可以从指针中减去（- 或 -=），并且一个指针可以从另一个指针中减去——最后这个操作只有在两个指针都指向同一数组的元素时才有意义。

### 7.8.2 让指针指向数组

假设已定义数组 `int v[5]`，其第一个元素位于内存中的位置 3000。假设指针 `vPtr` 已初始化为指向 `v[0]`——即 `vPtr` 的值为 3000。图 7.18 说明了在整数为 4 字节的机器上的这种情况。可以用以下任一语句将变量 `vPtr` 初始化为指向数组 `v`：

```
vPtr = v;
vPtr = &v[0];
```

## 可移植性提示 7.2

由于指针算术的结果取决于指针所指向对象的大小，因此指针算术依赖于机器和编译器。

![](img/bf54db922e6fa8319cba11069e785521_321_0.png)

图 7.18 | 数组 `v` 和指向 `v` 的指针变量 `vPtr`。

### 7.8.3 将整数加到指针上

在常规算术中，3000 + 2 的值为 3002。指针算术通常并非如此。当整数加到指针上或从指针中减去时，指针不是简单地按该整数递增或递减，而是按该整数乘以指针所指向对象的大小来递增或递减。字节数取决于对象的数据类型。例如，语句

```
vPtr += 2;
```

将产生 3008（3000 + 2 * 4），假设一个整数存储在 4 字节内存中。在数组 `v` 中，`vPtr` 现在将指向 `v[2]`（图 7.19）。如果一个整数存储在 2 字节内存中，那么前面的计算将得到内存位置 3004（3000 + 2 * 2）。如果数组是不同数据类型，前面的语句将使指针递增存储该数据类型对象所需字节数的两倍。对字符数组执行指针算术时，结果将与常规算术一致，因为每个字符长 1 字节。

> 常见编程错误 7.4
> 对不指向数组中元素的指针使用指针算术。

![](img/bf54db922e6fa8319cba11069e785521_322_0.png)

图 7.19 | 指针算术后的指针 `vPtr`。

### 7.8.4 从指针中减去整数

如果 `vPtr` 已递增到 3016，即指向 `v[4]`，则语句

```
vPtr -= 4;
```

会将 `vPtr` 重新设置为 3000——数组的起始位置。

> 常见编程错误 7.5
> 使用指针算术时越过数组的任一端。

### 7.8.5 递增和递减指针

如果要将指针递增或递减 1，可以使用递增（++）和递减（--）运算符。以下任一语句

```
++vPtr;
vPtr++;
```
