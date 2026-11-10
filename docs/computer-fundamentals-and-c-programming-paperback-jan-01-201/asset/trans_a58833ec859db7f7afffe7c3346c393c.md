

![](img/d75612dcf3ab36327142238ab5bb21d8_325_0.png)

**图 10.1** 数组 `a[10]` 的内存布局

> **提示：** 数组经常需要调整大小，因此用符号常量表示大小是合理的（如 `char name[SIZE];`）。当大小改变时，只需更改设置 SIZE 的 **#define** 指令。无需改动程序主体。

### 10.2.1 声明时初始化

简单声明不会初始化数组（除非同时使用关键字 `static`），因此在此阶段各元素具有垃圾值。可以在声明时通过用花括号括起以逗号分隔的值列表来初始化数组。下面的声明中有两个显式指定了大小，但第三个只隐式指定大小：

```c
short months[12] = {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
float rate[10] = {12.5, 13.7, 5};
char type[] = {'A', 'n', 'd', 'r', 'o', 'i', 'd', '\0'};
```

在第一个声明中，值的数量与数组大小匹配。第二个声明只给前三个元素赋值，执行*部分*初始化。*发生这种情况时，其余值会自动初始化为零*（对于 char 类型数组则为 NUL）。

第三个声明使用一对空方括号（`[]`）来*隐式*指定数组大小。这种灵活性对程序员有利，也不会给编译器带来麻烦，因为编译器可以通过计算右侧的八个值轻松算出大小。该数组是一个字符串，因为它包含终止符 NUL（`'\0'`）。我们将在第 13 章讨论作为字符数组的字符串。

### 10.2.2 声明后初始化

你可能在编译时并不知道所有初始值，或者可能需要在程序后面重新赋值。使用花括号的技术在稍后赋值时不起作用；在这种情况下，必须逐个元素赋值：

```c
months[0] = 31;
months[1] = 28.3;        // Decimal portion truncated
rate[4] = 3;             // OK, 3 converted to float
type[5] = '\0';          // The NUL character having ASCII value 0
```

如果所有元素都赋相同的值，或赋通过求值表达式得到的值，通常使用循环来初始化整个数组。数组索引通常是循环的关键变量。下面左侧的示例将数组 rate 的所有元素初始化为 12.5，而右侧的示例赋一个包含索引本身的表达式：

```c
short i;                         short i;
float rate[10];                  float rate[SIZE];
for (i = 0; i < 10; i++)         for (i = 0; i < SIZE; i++)
    rate[i] = 12.5;                  rate[i] = i * 1.1;
```

符号常量 SIZE 必须事先定义为 **#define SIZE 10**。要打印所有元素，类似的两行 for 循环即可完成：

```c
for (i = 0; i < 10; i++)              for (i = 0; i < SIZE; i++)
    printf("%f ", rate[i]);               printf("%f ", rate[i]);
```

未初始化数组和部分初始化数组的初始化规则适用于在 **main** 之类的函数内部定义的数组。在第 11 章中，你将了解如何通过使用附加关键字或在函数外部定义数组来自动初始化数组。

## 10.3 array_init.c：初始化和打印数组

程序 10.1 包含三个类型不同、初始化程度不同的数组。程序显示这些数组的内容，并由此说明使用未初始化数组和部分初始化数组的后果。

```c
/* array_init.c: Shows effects of (i) no initialization, (ii) partial
                   initialization. Also initializes one array. */
#include <stdio.h>
#define SIZE 7
int main(void)
{
    short i;
    short short_arr[SIZE];
    int int_arr[SIZE] = {100, 200};
    long long_arr[] = {10, 20, 30, 40, 50, 60, 100};

    printf("Size of short_arr = %d\n", sizeof short_arr);
    printf("Size of long_arr = %d\n", sizeof long_arr);

    printf("short_arr contains    ");
    for (i = 0; i < SIZE; i++)
        printf("%5hd ", short_arr[i]);        /* Uninitialized */
    printf("\nint_arr contains     ");
    for (i = 0; i < SIZE; i++)
        printf("%5d ", int_arr[i]);           /* Partially initialized */

    printf("\nlong_arr contains    ");
    for (i = 0; i < (sizeof long_arr / sizeof(long)); i++)
        printf("%5ld ", long_arr[i]);         /* Fully initialized */

    for (i = 0; i < SIZE; i++)
        short_arr[i] = i * 2;                  /* Initializing short_arr ... */
    printf("\nshort_arr now contains ");
    for (i = 0; i < SIZE; i++)
        printf("%5hd ", short_arr[i]);        /* ... and printing it */
    return 0;
}
```

程序 10.1：**array_init.c**

```text
Size of short_arr = 14
Size of long_arr = 28
short_arr contains    -24588  2052  13928  -16479  -31319  2052  -8352
int_arr contains       100    200    0      0       0      0      0
long_arr contains       10     20    30     40      50     60     100
short_arr now contains   0      2     4      6       8      10     12
```

程序输出：**array_init.c**

注意，**sizeof** 计算的是为所有数组元素分配的内存。对于程序中使用的数组，有以下观察结果：

- **short_arr** 最初具有垃圾值，因为它在声明时未初始化。后来它被赋值为一个与其索引相关的表达式的值。
- **int_arr** 是部分初始化的。前两个元素已初始化，因此其余五个元素自动设置为零。
- **long_arr** 的大小是*隐式*声明的。编译器通过计算七个值来确定它。这个大小也通过用数组占用的总空间（**sizeof long_arr**）除以 long 数据类型的大小（**sizeof (long)**）来计算。

通常，接受数组作为参数的函数还需要将元素数量作为另一个参数。这个值应作为表达式 **sizeof array / sizeof (data type)** 传递给函数，而不是作为常量。即使以后更改数组的大小，也无需更改这个表达式。

> **要点：** 未初始化数组包含垃圾值，但部分初始化数组的其余元素会设置为零或 NUL。此外，对数组使用 **sizeof** 求值得到的是该数组所有元素占用的总空间。

## 10.4 scanf_with_array.c：用 scanf 填充数组

在循环中使用 **scanf** 函数，我们可以通过键盘输入填充数组。**程序 10.2** 利用 **scanf** 的返回值来确定输入结束。此程序中的 **while** 循环在 **scanf** 返回 0 时终止，而当键入 **EOF** 或任何非数字字符（例如 *q*）时就会发生这种情况。

最多可以输入 20 个整数——如有必要可分行输入——但每次调用 **scanf** 只读取一个整数，并将剩余输入留在缓冲区中。已输入值的数量可在表达式 *i - 1* 中获得，它决定第二个循环迭代多少次来打印所有已填充的数组元素。

```c
/* scanf_with_array.c: Populates an array with user input. */
#include <stdio.h>
int main(void)
{
    short i = 0, num;
    short arr[20];
    printf("Key in some integers followed by EOF: ");
    while (scanf("%hd", &arr[i++]) == 1)       /* Populates array */
        ;
    num = i - 1;
    for (i = 0; i < num; i++)
        printf("arr[%hd] = %hd, ", i, arr[i]);
    return 0;
}
```

程序 10.2：scanf_with_array.c

```text
Key in some integers followed by EOF: 11 22 [Enter]
44 55 77 [Enter]
99
EOF                    Press [Ctrl-d] or [Ctrl-z] to terminate loop
arr[0] = 11, arr[1] = 22, arr[2] = 44, arr[3] = 55, arr[4] = 77, arr[5] = 99,
```

程序输出：scanf_with_array.c

## 10.5 数组的基本操作

正如上一个程序清楚显示的，就所有实际用途而言，数组元素可以被当作变量处理。因此，元素可以构成任何算术、赋值、关系或逻辑表达式的组成部分。下面从本章程序中摘取的示例展示了在表达式中使用数组元素的各种方式：

```c
arr[i] = arr[i + 1];
temp = arr[i];
arr[c]++;
if (arr[i] > arr[j])
if (num < arr[0] || num > arr[SIZE - 1])
```

元素 arr[i] 中的 [ 和 ] 实际上是一组用于求值该元素的操作符。这些符号具有最高优先级——与圆括号同级。因此，在表达式 arr[c]++ 中，arr[c] 会在应用递增操作之前求值。

### 10.5.1 insert_element.c：在数组中插入元素

要在数组的指定位置插入元素，需要将从该位置到数组末尾的所有元素向右移动。程序 10.3 接受用户输入来初始化数组，然后接受进一步输入以在指定位置插入元素。最后，它显示数组更改后的内容。该程序文档充分，无需进一步详述。

