
它根据表达式 `responses[answer]` 的值递增相应的频数计数器。当计数器变量 `answer` 为 0 时，`responses[answer]` 为 1，因此 `++frequency[responses[answer]];` 会被解释为 `++frequency[1];`，从而递增 `frequency[1]`。当 `answer` 为 1 时，`responses[answer]` 为 2，因此 `++frequency[responses[answer]];` 会被解释为 `++frequency[2];`，从而递增 `frequency[2]`。当 `answer` 为 2 时，`responses[answer]` 为 5，因此 `++frequency[responses[answer]];` 会被解释为 `++frequency[5];`，从而递增 `frequency[5]`，依此类推。

### 无效的调查响应

无论处理了多少个调查响应，都只需要一个由 6 个元素组成的频数数组（忽略元素 0）来汇总结果。但如果数据中包含像 13 这样的无效值呢？在这种情况下，程序会尝试给 `frequency[13]` 加 1，而该位置超出了数组边界。C 语言没有数组边界检查来阻止程序引用不存在的元素。因此，正在运行的程序可能会在毫无警告的情况下“走出”数组的任意一端，这是我们在 6.13 节讨论的一个安全问题。程序应验证所有输入值是否正确，以防止错误信息影响程序的计算。

### 验证数组下标

引用数组边界以外的元素属于逻辑错误。遍历数组时，数组下标不应小于 0，并且应始终小于数组中元素的总数，即数组大小减 1。你应该确保所有数组引用都保持在数组边界之内。

### 6.4.6 用条形图绘制数组元素值

下一个示例（图 6.6）从数组读取数字，并将这些信息绘制成条形图。我们显示每个数字，后面跟上由相应数量星号组成的条形。嵌套的 `for` 语句（第 17–19 行）通过迭代 `n[i]` 次来显示条形，每次迭代显示一个星号。第 21 行结束每个条形。

```c
// fig06_06.c
// Displaying a bar chart.
#include <stdio.h>
#define SIZE 5

// function main begins program execution
int main(void) {
    // use initializer list to initialize array n
    int n[SIZE] = {19, 3, 15, 7, 11};

    printf("%s%13s%17s\n", "Element", "Value", "Bar Chart");

    // for each element of array n, output a bar of the bar chart
    for (size_t i = 0; i < SIZE; ++i) {
        printf("%7zu%13d%8s", i, n[i], "");

        for (int j = 1; j <= n[i]; ++j) { // print one bar
            printf("%c", '*');
        }

        puts(""); // end a bar with a newline
    }
}
```

| 元素 | 值 | 条形图 |
|---|---|---|
| 0 | 19 | ******************* |
| 1 | 3 | *** |
| 2 | 15 | *************** |
| 3 | 7 | ******* |
| 4 | 11 | *********** |

**图 6.6** | 显示条形图。（第 2 部分，共 2 部分。）

### 6.4.7 掷骰子 60,000,000 次并用数组汇总结果

在第 5 章中，我们说过会展示一种更优雅地编写图 5.5 中掷骰子程序的方式。回想一下，该程序掷一个六面骰子 60,000,000 次，并显示各面出现的次数。图 6.7 是图 5.5 的数组版本。第 17 行取代了图 5.5 中整个 20 行的 `switch` 语句。我们再次使用频数数组，并忽略元素 0，从而可以直接使用骰子面值作为数组下标。

```c
// Fig06_07.c
// Roll a six-sided die 60,000,000 times
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#define SIZE 7

// function main begins program execution
int main(void) {
    srand(time(NULL)); // seed random number generator

    int frequency[SIZE] = {0}; // initialize all frequency counts to 0

    // roll die 60,000,000 times
    for (int roll = 1; roll <= 60000000; ++roll) {
        size_t face = 1 + rand() % 6;
        ++frequency[face]; // replaces entire switch of Fig. 5.5
    }

    printf("%s\t%s\n", "Face", "Frequency");

    // output frequency elements 1-6 in tabular format
    for (size_t face = 1; face < SIZE; ++face) {
        printf("%4zu\t%7d\n", face, frequency[face]);
    }
}
```

| 面值 | 频数 |
|------|-----------|
| 1 | 9997167 |
| 2 | 10003506 |
| 3 | 10001940 |
| 4 | 9995833 |
| 5 | 10000843 |
| 6 | 10000711 |

**图 6.7** | 掷六面骰子 60,000,000 次。（第 2 部分，共 2 部分。）

## 自测题

1. **(代码)** 将下面的代码段改写为定义七元素的 `double` 数组 `m`，并将其每个元素初始化为 10：

```c
int n[5]; // n is an array of five integers
// set elements of array n to 0
for (size_t i = 0; i < 5; ++i) {
    n[i] = 0; // set element at location i to 0
}
```

答案：

```c
double m[7]; // m is an array of 7 doubles
// set elements of array m to 10.0
for (size_t i = 0; i < 7; ++i) {
    m[i] = 10.0; // set element at location i to 10.0
}
```

2. **(选择题)** 下列说法 a)、b) 或 c) 中哪一项是正确的？

- a) 对于 `int` 数组，如果提供的初始化器数量少于数组元素数量，其余元素会被初始化为 0。
- b) 如果数组初始化列表中提供的初始化器数量多于数组元素数量，则属于语法错误。例如，`int n[3] = {32, 27, 64, 18};` 是一个语法错误，因为有四个初始化器，但只有三个数组元素。
- c) 如果定义时带有初始化列表但省略了数组大小，编译器将根据初始化列表中的元素数量确定元素个数。因此，下面代码创建了三元素的 `int` 数组 `s`：

  ```c
  int s[] = {10, 20, 30};
  ```

- d) 以上说法都正确。

答案：d.

## 6.5 使用字符数组存储和操作字符串

数组可以保存任意类型的数据，但给定数组中的所有元素必须具有相同的类型。现在我们讨论如何在字符数组中存储字符串。到目前为止，我们唯一的字符串处理能力是用 `printf` 输出字符串。像 `"hello"` 这样的字符串实际上是一个由单个字符组成的数组，还要再加上一个东西。

### 6.5.1 使用字符串初始化字符数组

字符数组有几个独特的功能。可以使用字符串字面量初始化字符数组。例如，

```c
char string1[] = "first";
```

将数组 `string1` 的元素初始化为字符串字面量 `"first"` 中的各个字符。在这种情况下，编译器会根据字符串的长度确定数组 `string1` 的大小。字符串 `"first"` 包含五个字符，外加一个*字符串结尾的空字符*。因此，`string1` 实际上包含六个元素。表示空字符的转义序列是 `'\0'`。所有字符串都以这个字符结尾。表示字符串的字符数组在定义时应始终足够大，以容纳字符串的字符数以及末尾的空字符。

### 6.5.2 使用字符初始化列表初始化字符数组

字符数组也可以使用初始化列表中的单个字符常量来初始化，但这样做可能很繁琐。前面的定义等价于

```c
char string1[] = {'f', 'i', 'r', 's', 't', '\0'};
```

### 6.5.3 访问字符串中的字符

你可以直接使用数组下标表示法访问字符串中的单个字符。因此，`string1[0]` 是字符 `'f'`，`string1[3]` 是 `'s'`，`string1[5]` 是 `'\0'`。

### 6.5.4 向字符数组中输入

下面的定义创建了一个能够存储*最多 19 个字符*以及*一个末尾空字符*的字符串的字符数组：

```c
char string2[20];
```

语句

```c
scanf("%19s", string2);
```

会从键盘读取一个字符串到 `string2` 中。你可以将数组名传递给 `scanf`，无需像非字符串变量那样使用 `&`。`&` 通常用于向 `scanf` 提供变量在内存中的*位置*，以便将值存储到那里。在 6.7 节讨论将数组传递给函数时，我们会说明为什么数组名不需要 `&`。

你有责任确保接收字符串的数组能够容纳用户在键盘上输入的任何字符串。`scanf` 函数*不会*检查数组有多大。它会一直读取字符，直到遇到*空格*、*制表符*、*换行符*或*文件结束指示符*。字符串 `string2` 不应超过 19 个字符，以便为末尾的空字符留出空间。如果用户输入 20 个或更多字符，程序可能会崩溃，或产生一种称为缓冲区溢出的安全漏洞。因此，我们使用转换说明 `%19s`。这会告诉 `scanf` 最多读取 19 个字符，防止它将字符写入超出 `string2` 末尾的内存。（在 6.13 节中，我们会重新讨论向字符数组输入可能带来的安全问题，并介绍 C 标准中的 `scanf_s` 函数。）

### 6.5.5 输出表示字符串的字符数组

表示字符串的字符数组可以使用 `%s` 转换说明通过 `printf` 输出。例如，你可以使用

```c
printf("%s\n", string2);
```

打印字符数组 `string2`。和 `scanf` 一样，`printf` 不会检查字符数组有多大。它会显示字符串中的字符，直到遇到末尾的空字符。[想一想，如果由于某种原因缺少末尾的空字符，会打印出什么。]

### 6.5.6 演示字符数组

图 6.8 演示了用字符串字面量初始化字符数组、将字符串读入字符数组、将字符数组作为字符串打印，以及访问字符串中的单个字符。程序使用 `for` 语句（第 20–22 行）遍历 `string1` 数组，并使用 `%c` 转换说明打印由空格分隔的各个字符。当计数器小于数组大小且字符串中尚未遇到末尾的空字符时，`for` 语句中的条件为真。该程序只读取不含空白字符的字符串。我们将在第 8 章展示如何读取包含空白字符的字符串。

```c
// fig06_08.c
// Treating character arrays as strings.
#include <stdio.h>
#define SIZE 20
```

**图 6.8** | 将字符数组作为字符串处理。（第 1 部分，共 2 部分。）

