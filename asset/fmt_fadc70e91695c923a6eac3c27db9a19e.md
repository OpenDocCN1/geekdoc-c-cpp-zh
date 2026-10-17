
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

表 10.4：`stdlib.h` 中的常用函数

| 函数 | 描述 |
|---|---|
| `malloc()` | 在堆上动态分配一块内存 |
| `free()` | 释放之前分配的内存 |
| `realloc()` | 重新调整之前分配的内存块的大小 |
| `calloc()` | 为数组分配内存并将其初始化为零 |
| `exit()` | 使用指定的退出退出状态立即终止程序执行 |
| `abort()` | 通过引发信号终止程序执行 |
| `atoi()` | 将字符串转换为整数 |
| `atof()` | 将字符串转换为浮点数 |
| `rand()` | 生成一个伪随机数 |
| `srand()` | 为 `rand()` 使用的随机数生成器种子 |

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

## 第 11 章

## 文件输入/输出

文件处理是编程中至关重要的一个，它允许程序读取、写入和处理存储在文件中的数据，对于数据管理、软件开发和 Web 应用程序等应用至关重要。

C 语言中的文件输入/输出（I/O）允许程序与硬盘、USB 驱动器和内存卡等外部存储设备交互。这种能力使程序能够存储和检索大量数据，这对许多应用程序都是必不可少的。

与处理键盘、屏幕和其他硬件输入输出的标准 I/O 不同，文件 I/O 专门处理外部存储的访问。在 C 语言中需要文件处理的原因包括：

- **持久化**：通过在程序运行之外保存数据，程序可以维持偏好、保存应用状态并归档历史数据。
- **数据交换**：文件有助于协作、应用程序之间的数据传输以及跨平台兼容性，因为它们允许程序以标准格式共享数据。
- **处理大型数据集**：文件 I/O 通过通过分块读取数据、高效执行操作并增量写入结果，能够处理超过内存限制的海量数据。

注意的是，文件处理依赖于操作系统，因此本章可能与裸机嵌入式系统无关。

## 11.1 打开和关闭文件

- `fopen()`：初始化文件流并返回指向 `FILE` 结构体的指针。它接受两个参数：
  - `filename`：要打开的文件名，以空空结尾字符串的形式提供。
  - `mode`：指定文件模式：
    - `r`: 只读模式。允许从文件中读取数据。
    - `w`: 只写模式。擦除现有内容，或如果文件不存在则创建一个新文件。
    - `a`: 附加模式。将数据添加到文件末尾，而不会覆盖现有内容。

```c
FILE *fp;
fp = fopen("my_file.txt", "w");
```

- `fclose()`：打开文件后，完成后使用 `fclose()` 关闭它是至关重要的。该函数释放与文件相关的系统资源。它接受由之前的 `fopen()` 调用返回的 `FILE` 结构体指针。

```c
fclose(fp);
```

这是一个简单的示例演示了如何打开、写入并关闭文件：
```c
#include <stdio.h>
int main() {
    FILE *fp;
    // 以写入模式打开文件
    fp = fopen("my_file.txt", "w");
    // 检查打开期间的错误
    if (fp == NULL) {
        printf("Error opening file!\n");
        return 1;
    }
    // 将内容写入文件
    fprintf(fp, "This is some text written to the file.\n");
    fprintf(fp, "This is another line of text.\n");
    // 关闭文件
    fclose(fp);
    printf("File written successfully!\n");
    return 0;
}
```

此代码包含了错误检查，并演示了打开文件、写入以及关闭文件。

## 11.2 从文件中读取

### 11.2.1 读取文件的函数

C 提供了几个从文件中读取数据的函数：

- `fscanf()`：从文件中读取格式化数据到变量中。它接受一个文件指针、一个格式字符串和可变参数。
```c
int num;
float price;
sscanf(file, "%d %f", &num, &price);
```
- `fgets()`：从文件中读取一行文本（包括空白符），并将其存储在字符数组中。
```c
char line[100];
fgets(line, sizeof(line), file);
```
- `fread()`：从文件中读取一个数据块到缓冲区。它接受一个缓冲区的指针、每个元素的大小、读取的元素数量以及一个指针。
```c
char buffer[100];
size_t n = fread(buffer, 1, sizeof(buffer), file);
```

### 11.2.2 从文件读取时处理不同数据类型

确保在从文件中读取数据时对不同类型进行正确处理：

- `int`: 使用 `%d` 或 `%i`
- `float`: 使用 `%f` 或 `%e`
- `double`: 使用 `%lf` 或 `%le`
- `char`: 使用 `%c`
- `string`: 使用 `%s`（注意缓冲区溢出）

### 11.2.3 从文件读取时的错误处理

在从文件中读取数据时，检查错误是非常重要的。`feof()` 函数用于检查文件结束条件，而 `ferror()` 则在发生错误时返回非零值。以下是一个示例：
```c
if (fread(data, sizeof(data), 1, fp) != 1) {
    perror("Error reading from file");
    exit(1);
}
```

## 11.5 处理文本文件

### 11.5.1 使用 C 操作文本文件

在 C 中处理文本文件不仅是读取和写入。你还可以对文本文件中的数据进行修改、过滤和清洗。例如，你可以移除不需要的字符、替换文本或根据数据进行计算。以下是从文件中移除所有字符 'x' 的示例：
```c
FILE in = fopen("input.txt", "r");
FILE out = fopen("output.txt", "w");
while (fgets(line, sizeof(line), in)) {
    fputs(str_replace(line, "x", ""), out);
}
```
```c
fclose(in);
fclose(out);
```

### 11.5.2 读取和写入 CSV 文件

逗号分隔值（CSV）文件通常用于存储表格化数据，包括传感器数据。这是一个 CSV 文件的示例：

| 时间戳 | 传感器 ID | 温度 | 湿度 |
| :--- | :--- | :--- | :--- |
| 2024-03-10 08:00:00 | 001 | 25.5 | 60 |
| 2024-03-10 08:05:00 | 002 | 24.8 | 58 |
| 2024-03-10 08:10:00 | 003 | 26.2 | 63 |
| 2024-03-10 08:15:00 | 001 | 26.8 | 62 |

在此 CSV 文件中：

- 行代表一条记录。
- 每条记录中的字段由逗号分隔。
- 第一行包含表头，指示每个字段的含义（时间戳、传感器 ID、温度、湿度）。
- 后续行包含对应表头的传感器数据。

在 C 中，你可以使用之前节介绍的函数读取和写入 CSV 文件。要读取包含时间戳、传感器 ID、温度和湿度的传感器数据的 CSV 文件，请遵循以下步骤：

1. 打开文件进行读取：
- `FILE file = fopen("sensor_data.csv", "r");`
2. 声明变量存储传感器数据并读取文件中的记录数：
