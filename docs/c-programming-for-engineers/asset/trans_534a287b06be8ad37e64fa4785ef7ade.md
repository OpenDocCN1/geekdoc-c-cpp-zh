

## 10.8 库函数

```c
char destination[20]; // Ensure destination has enough space
strcat(destination, source);
printf("Copied string: %s\n", destination);
return 0;
```

## 字符串连接函数

`strcat()` 函数将一个字符串连接到另一个字符串的末尾。

```c
#include <stdio.h>
#include <string.h>

int main() {
    char str1[] = "Hello, ";
    char str2[] = "World!";
    strcat(str1, str2);
    printf("Concatenated string: %s\n", str1);
    return 0;
}
```

## 字符串比较函数

`strcmp()` 函数比较两个字符串并返回一个指示其字典关系的整数。

这些函数简化了 C 程序中的字符串处理任务。更多细节可以在 https://en.wikibooks.org/wiki/C_Programming/string.h 处找到。

### 10.8.3 标准库

C 语言中的 `stdlib.h` 库提供了内存管理、字符串、数字和文件 I/O 操作的实用函数。它们包括：

- 字符串转换函数，用于将字符串转换为整数和浮点类型反之。
- 随机数生成函数，用于生成伪随机整数。
- 排序和搜索函数，用于大型数组的高效数据操作、排序和搜索。
- 内存管理函数，用于处理动态内存分配。
- 进程控制函数，用于管理外部进程和程序终止。

这些函数有助于开发高效、灵活且安全的 C 程序。

表 10.4：stdlib.h 中的常用函数

| 函数 | 描述 |
|---|---|
| malloc() | 在堆上动态分配一块内存 |
| free() | 释放之前分配的内存 |
| realloc() | 重新调整之前分配的内存块的大小 |
| calloc() | 为数组分配内存并将其初始化为零 |
| exit() | 使用指定的退出退出状态立即终止程序执行 |
| abort() | 通过引发信号终止程序执行 |
| atoi() | 将字符串转换为整数 |
| atof() | 将字符串转换为浮点数 |
| rand() | 生成一个伪随机数 |
| srand() | 为 `rand()` 使用的随机数生成器种子 |

更多细节可以在 https://en.wikibooks.org/wiki/Programming/stdlib.h 处找到。

## ASCII 转整数

`atoi()` 函数将字符串转换为整数（即 `int`）并返回它。它等同于 `(strtol(s, (char**)NULL, 10))`。如果字符串无法进行任何有效转换，则返回零。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int main () {
  int value;
  char str[20];
  strcpy(str, "81310");
  value = atoi(str);
  printf("String = %s, Int value = %d\n", str, value);
  strncpy(str, "UTM Skudai");
  value = atoi(str);
  printf("String = %s, Int value = %d\n", str, value);
  return 0;
}
```

编译程序时，我们将得到如下结果：

String = 81310, Int value = 81310
String = UTM Skudai, Int value = 0

## 随机数生成与排序

`stdlib.h` 中两个对工程师非常有用的函数是 `rand()` 和 `qsort()`。
`rand()` 函数在 C 中生成伪随机整数，用于模拟、随机算法或创建不可预测的行为。通常做法是使用基于当前时间的种子值来使用随机数生成器 `srand()`，以确保每次程序运行时都有不同的随机数序列。

`qsort` 是流行且高效的排序算法的 C 实现。它接受四个参数：数组的指针、元素数量、每个元素的大小以及定义排序顺序的比较函数。比较函数比较两个元素并返回一个指示它们相对顺序的整数。下面是一个演示这两个函数的示例代码。注意使用了 `<time.h>` 以允许使用 `time()` 函数。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define ARRAY_SIZE 10

// Comparison function for qsort
int compare(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

int main() {
    // Seed the random number generator
    srand(time(NULL));

    // Initialize an array of ARRAY_SIZE integers
    int array[ARRAY_SIZE];

    // Fill the array with random values
    for (int i = 0; i < ARRAY_SIZE; i++) {
        array[i] = rand() % 101; // Generate random value between 0 and 100
    }

    // Display the original array
    printf("Original array:\n");
    for (int i = 0; i < ARRAY_SIZE; i++) {
        printf("%d ", array[i]);
    }
    printf("\n\n");

    // Sort the array using qsort
    qsort(array, ARRAY_SIZE, sizeof(int), compare);

    // Display the sorted array
    printf("Sorted array:\n");
    for (int i = 0; i < ARRAY_SIZE; i++) {
        printf("%d ", array[i]);
    }
    printf("\n\n");

    return 0;
}
```

典型的运行产生输出：

Original array: 68 91 40 20 21 78 47 72
Sorted array: 20 21 40 47 68 72 78

该程序使用当前时间初始化随机数生成器，初始化一个0到100之间的随机整数数组，使用 `qsort` 排序并打印原始和排序后的数组。

## 总结

总之，C语言中的函数对于组织代码、使其复用和模块化至关重要。它们提高了可读性，简化了测试，并促进了程序员之间的协作。

## 问题

- 10.1 C 中按值传递和引用传递的区别是什么？
- 10.2 什么是函数，它为什么对编程有用？
- 10.3 函数原型和函数定义的区别是什么？
- 10.4 C 中局部变量和全局变量的区别是什么？
- 10.5 如何在 C 中创建递归函数？
- 10.6 下述函数本返回两个整数之和，但无法编译。识别并修复问题。
```c
#include <stdio.h>

int add(int a, int b) {
    return a + b;
}

int main() {
    printf("%d\n", add(3, 5));
    return 0;
}
```
- 10.7 下述函数旨在返回数的阶乘，但对某些输入产生了错误结果。识别并修正它。
```c
#include <stdio.h>

int factorial(int n) {
    if (n == 0)
        return 1;
    else
        return n * factorial(n - 1);
}

int main() {
    printf("%d\n", factorial(5)); // Expected: 120
    return 0;
}
```
- 10.8 编写一个函数 `celsiusToFahrenheit()` 将摄氏度转换为华氏度。使用-40、0、40和100度测试该函数的准确性。
- 10.9 编写一个程序生成整数数组 `grade[60]`，填充0-100的随机数，然后找到平均值标准差。
- 10.10 修改程序，使每个元素通过添加两个随机数（即 `rand() % 51 + rand() % 51`）定义，并与之前的方法标准差。
- 10.11 编写一个C函数，接收整数数组及其大小，返回一个元素反序排列的新数组。
- 10.12 编写一个程序，定义并调用一个C函数接收整数数组及其长度，返回元素的平均值。
- 10.13 编写一个程序，定义并调用一个C函数接收字符并检查其是元音还是辅音。
- 10.14 编写一个程序，定义并调用一个C函数接收整数数组及其长度，找到数组中的最大值最小值。

## 第10章 函数

- 10.15 编写函数 `rc_time_constant()`，在给定电阻 $R$（欧姆）和电容 $C$（法拉）计算RC电路的时间常数 $\tau$。使用公式：

$\tau = R \times C$

使用以下 `main()` 函数测试：

```c
int main() {
    double R = 1000; // 1 kiloohm
    double C = 0.000001; // 1 microFarad
    printf("Time constant: %lf\n", rc_time_constant(R, C));
    return 0;
}
```
- 10.16 编写函数 `voltage_divider()`，给定输入电压 $V_{in}$、电阻 $R1$ 和电阻 $R2$ 计算电压分压电路的输出电压，使用公式：

$V_{out} = V_{in} \times \frac{R_2}{R_1 + R_2}$

使用以下 `main()` 函数测试：

```c
int main() {
    double Vin = 12.0; // 12V input
    double R1 = 1000; // 1 kiloohm
    double R2 = 2000; // 2 kiloohm
    printf("Output Voltage: %lf\n", voltage_divider(Vin, R1, R2));
    return 0;
}
```
- 10.17 编写一个函数计算：

$\cos \omega t = \frac{e^{j\omega t} + e^{-j\omega t}}{2}$
- 10.18 下述函数本应返回电压读取数组的均方根 (RMS)，但有时会产生错误结果。找到并修复问题。

```c
#include <stdio.h>
#include <math.h>

double rms(int arr[], int size) {
    double sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i] * arr[i];
    }
    return sqrt(sum / size); // Possible issue?
}
```
```
