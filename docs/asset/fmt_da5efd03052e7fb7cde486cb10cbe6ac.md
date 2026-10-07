
a 的值的和为 15

图 6.4 | 计算数组元素的和。

## 6.4.5 使用数组总结调查结果

我们的示例使用数组来总结调查中收集的数据结果。考虑以下问题描述：

- 要求 20 名学生在 1 到 5 分的范围内对学生食堂的食物质量进行评分（1 表示糟糕，5 表示优秀）。

（注：原文此处 OCR 文本存在大量重复和错误，已根据逻辑进行了清理处理。）

## 6.4.6 使用条形图绘制数组元素值

我们的下一个示例（图 6.6）从数组中读取数字并用条形图绘制信息。我们用由许多星号组成的条形来显示每个数字。嵌套的 `for` 语句（17–19 行）通过遍历 `n[i]` 并每次迭代显示一个星号来显示条形。第 21 行结束每个条形。

```c
// fig06.c
// 绘制条形图。
#include <stdio.h>
#define SIZE 5
// function main 开始程序执行
int main(void) {
```

## 6.4 数组示例

```c
// use initializer list to initialize array n
int n[SIZE] = {19, 3, 15, 7, 11};
printf("%3s%17s\n", "Element", "Value", "Bar Chart");
// for each element of array, output a bar of the bar chart
for (size_t i = 0; i < SIZE; i++) {
    printf("%7zu%13s\n", i, n[i], "");
    for (int j = 1; j < n[i]; j++) { // print one bar
        printf("%c", "*");
    }
}
puts("\n"); // end with a bar newline
```

| 元素 | 数值 | 形图 |
| --- | --- | --- |
| 0 | 19 | ******************* |
| 1 | 3 | *** |
| 2 | 15 | *************** |
| 3 | 7 | ******* |
| 4 | 11 | *********** |

**图 6.6** | 显示条形图。（部分 2/2。）

### 6.4.7 掷骰子 60,000,000 次并并在数组中汇总结果

在第 5 章中，我们提到将展示一种更优雅的方法来编写图 5.5 的掷程序。回想一下该程序掷了六面骰子 60,000,000 次并显示了每个点面的计数。图 6.7 是图 5.5 的数组版本。第 17 行替换了图 5.5 中的 20 行 switch 语句。我们再次使用了一个频率数组，在其中忽略了 0，因此可以使用点数值作为数组的下标。

```c
// fig06_07.c
// 掷六面骰子 60,000,000 次
#include <stdlib.h>
#include <time.h>
#define SIZE 7
// function main begins program execution
int main(void) {
    // seed random number generator
    srand(NULL);
    int frequency[SIZE] = {0}; // initialize all frequency counts to 0
```

**图 6.7** | 掷六面骰子。60,000,000 次。（部分 1/2。）

## 第 6 章 数组

```c
// roll 60,000,000 times
for (int roll = 1; roll <= 60000000; ++roll) {
    size_t face = roll % 6;
    frequency[face]++; // replaces entire switch of Fig. 5.5
}
```

```c
printf("%s%s\n", "Face", "Frequency");
// output frequency elements 1-6 in tabular format
for (size_t face = 1; face < SIZE; ++face) {
  printf("%4u%d\n", face, frequency[face]);
}
```

| 点面 | 频率 |
| --- | --- |
| 1 | 9997167 |
| 2 | 10003506 |
| 3 | 10001940 |
| 4 | 9995833 |
| 5 | 10000843 |
| 6 | 10000711 |

图 6.7 | 掷六面骰子 60,000,000 次。（部分 2/2。）

## 自测

（代码）重写以下代码段以定义一个包含 7 个元素的 double 类型数组 `m`，并将其每个元素初始化为 1：

```c
int n[5]; // n is an array of five integers
// set elements of array n to 0
for (size_t i = 0; i < 5; ++i) {
  n[i] = 0;
}
```

答案：

```c
double m[7]; // m is an array of 7 doubles
// set elements of array m to 10.0
for (size_t i = 0; i < 7; ++i) {
  m[i] = 10.0;
}
```

- 2) （多选题）下列陈述中 a), b) 或 c) 哪个正确？
  a) 对于数组，如果提供的初始化器多于数组元素数量，剩余元素将初始化为零。
  b) 在数组列表中提供比数组元素数量更多的初始化器是语法错误——例如 `int n[3] = {10, 20, 30};` 是语法错误，因为有四个初始化器但只有三个元素。
  
## 6.5 使用字符数组存储处理字符串

c) 如果在初始化列表中省略数组大小，编译器将根据初始化器的数量确定元素数量。因此，以下代码创建一个三元素的数组 `s`：

```c
int s[] = {10, 20, 30};
```

d) 以上所有陈述都是正确的。答案：d：

## 6.5 使用字符数组存储处理字符串

数组可以包含任何类型的数据，尽管给定数组的所有元素必须具有相同的类型。我们现在讨论字符数组中的字符串。到目前，我们拥有的字符串处理能力是使用 `printf` 输出字符串。如 "hello" 的字符串实际上是一个字符数组，外加一个字符。

### 6.5.1 使用字符串初始化字符数组

字符数组具有几个独特特征。字符数组可以使用字符串字面量初始化。

```c
char string1[] = "first";
```

将数组 `string1` 的元素初始化为 "first" 中的字符。在这种情况下，编译器根据字符串的长度确定 `string1` 的大小。字符串 "first" 五个字符加上一个终止空，因此 `string1` 实际上包含六个元素。表示空的转义序列是 '\0'。所有字符串以该字符结束。表示字符串的字符数组应该定义为包含字符串字符数量和终止空。

### 6.5.2 使用字符列表初始化字符数组

字符数组也可以用初始化列表中的单个字符进行初始化，但这很麻烦。之前的定义等同于：

```c
char string1[] = {'f', 'i', 'r', 's', '\0'};
```

### 6.5.3 字符串中的字符

你可以使用下标符号直接访问字符串的单个字符。因此 `string1[0]` 是字符 'f'，`string1[3]` 是 's'，`string1[5]` 是 '\0'。

### 6.5.4 向字符数组输入

以下定义创建了一个能够存储最多 19 个字符和一个终止空的字符数组：

```c
char string2[20];
```

`scanf("%19s", string2);` 从键盘读取字符串到 `string2`。你将数组名传递给 `scanf`。`&` 通常用于提供变量在内存中的位置，以便在那里存储值。在第 6.7 节中，当我们讨论将数组传递给函数时，我们会讨论为什么数组名不需要 `&`。

确保数组能够容纳用户在键盘上输入的任何字符串是你的责任。函数 `scanf` 不检查数组的大小。它将一直读取字符直到遇到空格、制表符、换行符或指示符。字符串 `string2` 不应超过19 个字符，以便为空字符留空间。如果用户输入 20 个或更多字符，程序可能会崩溃或创建一个称为缓冲区溢的安全漏洞。由于这个原因，我们使用了格式规范 `%19s`。此 `scanf` 最多读取 19 个字符，防止它向 `string2` 之外的内存写入字符。（在第 6.13 节中，我们将重新审视向字符数组输入引起的安全问题，并讨论 C 标准的 `scanf_s` 函数。）

![](img/01a6e4ce4022df52dc328a037c9d_310_0.png)

### 6.5.5 输出表示字符串的字符数组

表示字符串的数组可以使用 `printf` 和 `%s` 格式规范输出。例如，你可以打印字符数组 `string2`：

```c
printf("%s\n", string2);
```

像 `scanf` 一样，`printf` 不检查字符数组的大小。它显示字符串字符直到遇到一个终止空字符。[考虑如果由于某种原因缺少终止空字符，会打印什么。]

### 6.5.6 演示字符数组

图 6.8 展示了使用字符串初始化字符数组、将字符串读入字符数组、将字符数组作为字符串打印以及访问字符串的字符。程序使用 `for` 语句（第 20-22 行）遍历 `string1` 数组。

## 6.6 静态局部数组与自动局部数组

第 5 章讨论了存储类型限定符 `static`。静态局部变量在整个程序运行期间都存在，但仅在函数体内部可见。我们可以对局部数组定义应用 `static`，以防止数组在每次调用函数时都进行创建和初始化，并在每次函数退出时被销毁。这缩短了程序的执行时间，特别是对于那些包含大型数组且被频繁调用的函数程序。静态数组在程序启动时初始化。如果你没有显式地初始化静态数组，该数组的元素将默认初始化为零。

图 6.9 展示了函数 `staticArrayInit`（第 21–38 行），其中包含局部静态数组（第 23 行），以及函数 `automaticArrayInit`（第 41–58 行），其中包含局部自动数组（第 43 行）。函数 `staticArrayInit` 被调用了两次（第 11 和 15 行）。函数中的局部静态数组在启动时初始化为零（第 23 行）。函数打印数组，为每个元素加 5 后再次打印数组。第二次调用该函数时，静态数组包含了在第一次调用期间存储的值。

```c
// fig0609.c
// 如果不显式初始化，静态数组将初始化为零。
#include <stdio.h>
void staticArrayInit(void); // 函数原型
void automaticArrayInit(void); // 函数原型
int main(void) {
    puts("First call to each function:");
    staticArrayInit();
    automaticArrayInit();
    puts("\nsecond call to each function:");
    staticArrayInit();
    automaticArrayInit();
    puts("");
}
// // 用于演示静态局部数组的函数
void staticArrayInit(void) {
    // 在调用函数之前初始化元素为 0
    static int array[3];
    puts("\nValues on entering staticArrayInit:");
    for (size_t i = 0; i < 2; i++) {
        printf("array[%u] = %d\n", i, array[i]);
    }
}
```

**图 6.9** 如果不显式初始化，静态数组将初始化为零。（2 部分中的第 1 部分）

```c
// ... (lines 31-38)
    puts("\nValues exiting staticArrayInit:");
    // 修改并输出 array1 的内容
    for (size_t i = 0; i < 2; ++i) {
        printf("array1[%u] = %d", i, array1[i] += 5);
    }
}
// 用于演示自动局部数组的函数
void automaticArrayInit(void) {
    // 每次调用函数时初始化元素
    int array2[] = {1, 2, 3};
    puts("\nValues on entering automaticArrayInit:");
    // 输出 array2 的内容
    for (size_t i = 0; i < 2; ++i) {
        printf("array2[%u] = %d", i, array2[i]);
    }
    puts("\nValues on exiting automaticArrayInit:");
    // 修改并输出 array2 的内容
    for (size_t i = 0; i < 2; ++i) {
        printf("array2[%u] = %d", i, array2[i] += 5);
    }
}
```

First call to each function:
Values on entering staticArrayInit:
array1[0] = 0 array1[2] = 0
Values on exiting staticArrayInit:
array1[0] = 5 array1[2] = 5

Values on entering automaticArrayInit:
array2[0] = 1 array2[1] = 2 array2[2] = 3
Values on exiting automaticArrayInit:
array2[0] = 6 array2[1] = 7

Second call to each function:
Values on entering staticArrayInit:
array1[0] = 5 array1[2] = 5 — 保留自上次调用的值
Values on exiting staticArrayInit:
array1[0] = 10 array1[2] = 10

Values on entering automaticArrayInit:
array2[0] = 1 array2[1] = 2 array2[2] = 3 — 上次调用后恢复
Values on exiting automaticArrayInit:
array2[0] = 6 array2[1] = 7

Fig. 6.9 如果不显式初始化，静态数组将初始化为零。（2 部分中的第 2 部分）

函数 `automaticArrayInit` 被调用了两次（第 12 和 16 行）。自动数组的元素用值 1、2 和 3 进行初始化（第 43 行）。函数打印数组，为每个元素加 5 后再次打印数组。第二次调用该函数时，数组元素被初始化为 1、2 和 3，因为该数组具有自动存储期。

## 自测
多项选择：下列陈述 a、b、或 c 哪一个是错误的？
- a 静态局部变量在整个程序运行期间都存在，但仅在函数体内部可见。
- b 静态局部数组只创建和初始化一次，而不是每次调用函数时。这缩短了程序的执行时间，特别是对于那些包含大型数组且被频繁调用的函数程序。
- c 如果你没有初始化静态数组，该数组的元素将默认初始化为零。
- d 以上所有陈述都是正确的。

答案：d。

## 6.7 将数组传递给函数

要向函数传递数组参数，请指定数组名。例如，如果定义了数组：

```c
int hourlyTemperatures[24];
```

调用函数时：
```c
modifyArray(hourlyTemperatures);
```

记住，C 的参数是值传递的。然而，通过引用传递数组意味着函数可以修改原始数组的值。

## 显示数组名是地址

图 6.10 展示了“数组名”是地址，使用 `%p` 格式说明符打印数组的第一个元素。这种输出是取决于编译器的。

```c
// fig0610.c
// 数组名与数组第一个元素的地址是相同的式的。
#include <stdio.h>
// 函数开始
int main(void) {
    char array[5] = ""; // 定义一个大小为5的数组
    printf("array = %p\narray[0] = %p\n&array = %p\n",
           array, &array[0], &array);
}
```
