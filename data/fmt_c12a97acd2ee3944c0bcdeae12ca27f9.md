
通过数组偏移输入输出

可以使用嵌套循环和数组偏移将数据输入二维数组的存储。数组名标识数组的起始地址。由于存储是按行分配的，按行顺序向二维数组输入数据是高效的。输出可以按行列格式显示。以下示例展示了按行输入输出。

### 输入数据

```
28.5 46.3 57.9 72.6

14.3 15.7 31.4 19.4

48.9 13.9 90.6 57.8
```

值的存储如下：

| | | | |
| :--- | :--- | :--- | :--- |
| `a[0][0]` | 28.5 | 1000 | `a + 0` |
| `a[0][1]` | 46.3 | 1004 | |
| `a[0][2]` | 57.9 | 1008 | |
| `a[0][3]` | 72.6 | 1012 | |
| `a[1][0]` | 14.3 | 1016 | `a + 1` |
| `a[1][1]` | 15.7 | 1020 | |
| `a[1][2]` | 31.4 | 1024 | |
| `a[1][3]` | 19.4 | 1028 | |
| `a[2][0]` | 48.9 | 1032 | `a + 2` |
| `a[2][1]` | 13.9 | 1036 | |
| `a[2][2]` | 90.6 | 1040 | |
| `a[2][3]` | 57.8 | 1044 | |

这些数据从输入设备键盘输入（如行所示），输出显示在显示器上（这是一个标准输出设备）。使用数组偏移输入输出这些数据的代码如下。

嵌套循环用于按行和按列递增数组指针。

```c
#include <stdio.h>

#define IMAX 3

#define JMAX 4

int main() 
{
    float values[IMAX][JMAX];
    int i, j;
    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            scanf("%f", *(values + i) + j);
        }
    }
    for(i = 0; i < IMAX; i++) {
        for(j = 0; j < JMAX; j++) {
            printf("%5.2f ", *(values + i) + j);
        }
        printf("\n");
    }
    return 0;
}
```

由于计算机不检查数组边界，如果数组是按行序存储的，则可以使用数组指针和单循环来输入或输出所有元素，如下：

```c
float values[IMAX][JMAX];
float *ptr, valuesend, i;
ptr = values;
valuesend = IMAX * JMAX;
for(i = 0; i < valuesend; i++)
    scanf("%f", *(ptr + i));
ptr = values;
for(i = 0; i < valuesend; i++)
    printf("%.2f \n", *(ptr+i));
```

## 10.3 指针与数组

```c
#include <stdio.h>
int main() {
    int numbers[10] = {12,25,67,85,90,72,94,86,9,18};
    int *ptr;
    ptr = numbers;
    printf("The address printed is: %d\n", ptr);
    printf("The number printed is: %d\n", *ptr);
    printf("The number printed is: %d\n", ++ptr);
    printf("The number printed is: %d\n", ++ptr);
    printf("The number printed is: %d\n", *ptr++);
    printf("The number printed is: %d\n", ++ptr);
    return 0;
}
```

`++ptr` 等同于 `++(ptr)`
`++*ptr` 等同于 `++(*ptr)`
`*ptr++` 等同于 `*(ptr++)`

输出如下：

- 打印的地址是: 10000 /* 使用了指针 */
- 打印的数字是: 12 /* 指针递增后使用 */
- 打印的数字是: 25 /* 数组元素递增 */
- 打印的数字是: 26 /* 指针使用后递增 */
- 打印的数字是: 26 /* 使用了指针 */
- 打印的数字是: 67 /* 指针递增后使用 */
- 打印的数字是: 85

注意，在第一个语句中，数值数组的地址被打印为 10000。在第二个打印语句中，通过 `*ptr` 打印了数字 12，这仅仅是对第一个内存位置进行解引用。在第三个打印语句中，指针递增然后解引用，打印出数字 25。在下一个打印语句中，指针被解引用，它指向包含数字 25 的位置，并将值 25 加了 1，因此打印出 26。数字 26 替换了内存中的数字 25。在下一个语句中，打印了数字 26（它已从 25 改变），且后置递增在该打印语句中无效。在 `*ptr++` 打印语句中，递增发生在数字 26 打印之后。在下一个语句中，由于上一个打印语句中的后置递增，打印了数字 67。在最后一个语句中，指针递增并打印了数字 85。

### 10.3.4 复习题

1. 判断以下陈述的正确（True）或错误（False）。
   a. 数组是一个地址变量。
   b. 数组的地址可以通过数组名或第一个元素的显式地址找到。
   c. 一维数组的元素可以通过对数组名解引用来访问，因为它是一个指针。
   d. 二维数组的元素可以通过对偏移地址解引用一次来访问。
   e. 使用指针变量向数组输入数据时可以使用数组名指定数组的地址。
   f. 可以在不对名称解引用的情况下通过数组名执行算术运算。
   g. 可以通过将地址赋值指针变量来复制数组。

2. 编写代码使用指针变量向以下一维数组输入并输出数据。

```c
int a[10], *ptra;
float b[20][20];
```

## 10.4 动态存储与数组

动态存储是指在程序执行期间分配的存储。在程序确定需要多少存储后，它从计算机内存的可用部分进行分配。在程序中声明的存储称为静态存储。它在程序执行之前分配。当数组的大小无法预知，或者必须重用最小空间空间时，可以使用 `stdlib.h` 库中的 `calloc()` 函数来分配动态存储并为其分配一个数组指针。`calloc()` 函数分配一个存储块，直到它被 `free()` 函数释放或程序终止为止。`calloc()` 函数传递的参数告诉它需要多少个数据单元以及它们的大小（字节）。`calloc()` 函数返回的地址必须转换为赋值给它的指针的声明数据类型。

### 10.4.1 一维数组

一维数组的动态存储分配如下：

```c
int *ptr;
xptr = (int *) calloc(5, sizeof(int));
```

此 `calloc()` 调用请求了五个每个四字节的数据单元。返回的地址被转换为数据类型 `int *`。

| | | |
|---|---|---|
| `xptr + 0` | 45 | 1000 |
| `xptr` | 1 | 86 | 1004 |
| `xptr + 2` | 63 | 1008 |
| `xptr + 3` | 96 | 1012 |
| `xptr + 4` | 54 | 1016 |

以下代码展示了动态存储并打印了每个地址。

```c
#include <stdio.h>
#include <stdlib.h>
int main() {
    int i, *arptr, SIZE;
    scanf("%d", &SIZE);
    arptr = (int *) calloc(SIZE, sizeof(int));
    for(i = 0; i < SIZE; i++) {
        scanf("%d", arptr);
        arptr++;
    }
    arptr = arptr - SIZE;
    printf("The output is:\n");
    for(i = 0; i < SIZE; i++) {
        printf("%d. %d\n", i + 1, *arptr);
        arptr++;
    }
    return 0;
}
```

### 指针与动态存储

### 数组赋值

存储在一个动态数组中的值可以拷贝到另一个动态数组中。可以使用 `for` 循环逐个元素地将一个数组拷贝到另一个数组。当复制数值数组时，如果源数组和目标数组的数据类型不匹配，将会在 C 语言规则内发生适当的数据类型转换。以下代码展示了使用动态指针将一个数组赋值给另一个数组。

```c
#include <stdlib.h>
#define ARMAX 5
int main() {
    int i;
    float *ptrr, *bptr;
    ptrr = (float*)calloc(ARMAX, sizeof(float));
    bptr = (float*)calloc(ARMAX, sizeof(float));
    *(ptrr + 0) = 12.75;
    *(ptrr + 1) = 18.34;
    *(ptrr + 2) = 9.85;
    *(ptrr + 3) = 23.78;
    *(ptrr + 4) = 16.96;
    for(i = 0; i < ARMAX; i++) {
        *bptr++ = *ptrr++;
    }
    bptr = bptr - ARMAX;
    ptrr = ptrr - ARMAX;
    return 0;
}
```

赋值前后，指针 `aptr` 和 `bptr` 所指向的动态数组包含的值如下：

#### 赋值前

| `aptr + 0` | 12.75 | `bptr + 0` | uuuuuu |
|---|---|---|--- |
| `aptr + 1` | 18.34 | `bptr + 1` | uuuuuu |
| `aptr + 2` | 9.85 | `bptr + 2` | uuuuuu |
| `aptr + 3` | 23.78 | `bptr + 3` | uuuuuu |
| `aptr + 4` | 16.96 | `bptr + 4` | uuuuuu |

## 10.4 动态存储与数组

#### 赋值后

| `aptr + 0` | 12.75 | `bptr + 0` | 12.75 |
|---|---|---|---|
| `aptr + 1` | 18.34 | `bptr + 1` | 18.34 |
| `aptr + 2` | 9.85 | `bptr + 2` | 9.85 |
| `aptr + 3` | 23.78 | `bptr + 3` | 23.78 |
| `aptr + 4` | 16.96 | `bptr + 4` | 16.96 |

如果安排了单个数组的两个副本，必须逐元素地拷贝数组。不能使用赋值语句 `bptr = aptr`，因为会导致两个指针指向同一个数组，并丢失分配给 `bptr` 的存储存储块。

### 10.4.2 二维数组

二维数组的动态存储可以使用标准库中的动态存储分配函数 `calloc()`。从空存储器中分配一块存储块。该存储块被划分为 `calloc()` 参数指定的单元数量。存储地址被分配给指针，该指针的数据类型与 `calloc()` 函数分配的空存储器中要存储的数据类型相同。`calloc()` 函数不区分一维和二维数组，它仅仅是分配请求的存储量。

对于数组 `[IMAX][JMAX]`，调用 `calloc()` 的形式应为

`calloc(IMAX * JMAX, sizeof(data type of array));`

存储分配方式如下：

```c
#include <stdlib.h>
#define IMAX 3
#define JMAX 4
int main()
{
    int *aptr; /* 动态指针声明 */
    aptr = (int *) calloc(IMAX * JMAX, sizeof(int));
    return 0;
}
```

## 指针与动态存储

存储分配：

| 地址 | 指针 |
|---|---|
| 1000 | `aprtr + 0` |
| 1004 | `aprtr + 1` |
| 1008 | `aprtr + 2` |
| 1012 | `aprtr + 3` |
| 1016 | `aprtr + 4` |
| 1020 | `aprtr + 5` |
| 1024 | `aprtr + 6` |
| 1028 | `aprtr + 7` |
| 1032 | `aprtr + 8` |
| 1036 | `aprtr + 9` |
| 1040 | `aprtr + 10` |
| 1044 | `aprtr + 11` |

注意，在这种情况下分配了一块存储。该块由 `IMAX * JMAX` 个单元组成，每个单元的大小是为该动态存储分配的数据类型所需的字节数。对于 `int` 和 `float` 数据类型，单元大小为 4 字节。动态指针 `aprtr` 指向包含 12 个 `int` 类型单元的存储块，每个单元包含 4 个 `long`。可以通过动态指针 `aprtr` 对动态存储进行输入/输出、赋值和算术操作。程序中处理存储的方式决定了数组是一维还是二维的。

## 10.4 动态存储与数组

### 10.4.1 动态存储（续）

解引的 `aprtr` 指向包含 12 个 `int` 类型单元的存储块，每个单元包含 4 个 `long`，可以通过动态指针 `aprtr` 对动态存储进行输入/输出、赋值和算术操作。程序中处理存储的方式决定了数组是一维还是二维的。

- 3. 编写代码声明一个动态指针并分配空间，以存储一个包含 80,000 个 `float` 类型元素的一维数组。
- 4. 编写一个程序声明一个动态指针并分配空间以存储一个 $50 \times 60$ 的 `float` 类型二维数组。同时编写向动态数组输入数据以及从动态数组输出输出数据的代码。

## 10.5 字符串与指针

可以使用指针和动态指针对字符串进行操作。当字符串的长度差异很大时，会使用动态指针。可以使用 `stdlib.h` 库头文件中的 `malloc()` 函数为变长字符串分配存储空间。

动态存储分配函数 `malloc()` 是一个单参数函数，该参数是存储单个变量所需的字节数；而动态存储分配函数 `calloc()` 是一个双参数函数，其第一个参数是存储单元的数量，第二个参数是每个存储单元的大小。函数 `malloc()` 通常用于为字符串分配存储空间。

### 10.5.1 字符串的动态存储

平滑数组（Smooth arrays）对于存储长度差异很大的字符串并不是高效的。它们应该从空闲存储（free store）中分配空间，并将地址赋值给 `char` 类型的指针变量。

以下代码展示了如何使用动态存储分配函数 `malloc()` 从空闲存储中分配空间。为了给每个字符串分配恰好的存储空间，必须将字符串输入到一个最大尺寸的静态 `char` 数组中，确定字符串的实际长度，使用动态存储分配函数 `malloc()` 分配正确数量的存储，并将字符串复制到其中。为了跟踪所有的字符串，它们的指针被存储在一个字符指针数组中。使用 `malloc()` 而不是 `calloc()` 来存储字符串，是因为字符串可以作为一个整体进行操作。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
```
#define NUMSTR 4
#define STLNG 80
int main() {
    int i;
    char strname[STLNG]; /* 用于存储字符串的输入缓冲区 */
    char *strptr[NUMSTR]; /* 字符串指针数组 */
    printf("Input strings:\n");
    for(i= 0; i<NUMSTR; i++) {
        gets(strname);
        strptr[i] = (char *)malloc(strlen(strname) + 1);
        strcpy(strptr[i],strname);
    }
    printf("Output strings:\n");
    for(i= 0; i<NUMSTR; i++) {
        puts(strptr[i]);
    }
    return 0;
}
```

Input strings:

AAAAAAA

BBBBBBBBBBBBBB

EEEE

PPPPPPPPPPPPPPPP

Output strings:

AAAAAAA

BBBBBBBBBBBBBB

EEEE

PPPPPPPPPPPPPPPP

每次调用动态存储分配函数 `malloc()` 时，它都会分配单块存储空间并返回其地址，该地址被强制转换为 `char*` 类型并存储在指针数组中。该函数位于 `stdlib.h` 库，必须通过 `#include <stdlib.h>` 包含。其他函数 `strlen()` 和 `strcpy()` 位于 `string.h` 库，必须通过 `#include <string.h>` 包含。

# 程序终止时的存储分配情况如下：

| | 4 |

| :--- | :--- |

| `str` | P | P | P | P | P | P | P | P | P | P | P | \0 | | | | |

| `strptr` | A | A | A | A | A | A | A | \0 |
