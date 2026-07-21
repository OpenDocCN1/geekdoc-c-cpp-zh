# 中级 C 编程



![](img/cover.jpg)





## 4.4 重新理解 Swap 函数

第 4.2 节解释了：

```c
void swap(int x, int y)
{
    int z = x;
    x = y;
    y = z;
}
```

这种方法不起作用，因为对 `x` 和 `y` 的修改在 `swap` 完成（即返回）并弹出栈顶帧帧后就丢失了。

如何编写一个正确的 `swap` 函数呢？`swap` 函数需要修改 `a` 和 `c` 的值。它们的地址位于函数外部。为了做到这一点，`swap` 必须拥有 `a` 和 `c` 的地址。

```c
void swap(int *k, int *m)
{
    /* a 和 c 的地址 */
}
```

```c
void f( void)
{
    int a = 83;
    int c = -74;
    swap(&a, &c);
    /* RL */
}
```

由于 `swap` 函数的参数必须是存储这些地址的指针：

```c
void swap(int *k, int *m)
{
}
```

这是开始 `swap` 函数时的调用栈：

| 符号 | 地址 | 值 |
| :--- | :--- | :--- |
| m | 104 | 101 |
| k | 103 | 100 |
| 返回位置 | 102 | line 13 |
| fc | 101 | -74 |
| a | 100 | 83 |

以下代码实现了 `swap` 函数：

```c
void swap(int *k, int *m)
{
    int s = *k;
    *k = *m;
    *m = s;
}
```

```c
void f( void)
{
    int a = 83;
    int c = -74;
    swap(&a, &c);
}
```

第三行读取地址 100 处的值并将其存储在 `s` 中。

| 符号 | 地址 | 值 |
| :--- | :--- | :--- |
| s | 105 | 83 |
| m | 104 | 101 |
| k | 103 | 100 |
| 返回位置 | 102 | line 13 |
| fc | 101 | -74 |
| a | 100 | 83 |

第四行读取存储在地址 101 处的值；该值为 -74。该值被存储在地址 100 处。

| 符号 | 地址 | 值 |
| :--- | :--- | :--- |
| s | 105 | 83 |
| m | 104 | 101 |
| k | 103 | 100 |
| 返回位置 | 102 | line 13 |
| fc | 101 | -74 |
| a | 100 | 83 |





# 152 中级 C 语言编程

当程序无法从文件中读取内容时，`fgets` 会返回 `NULL`。这意味着已经到达文件末尾。C 标准库包含一个名为 `getline` 的函数，它可以读取任意大小的行。




# 第 11 章：使用文件的编程问题

## 11.1 整数文件排序

此程序从文件中读取整数，对它们进行排序，并将排序后的整数存储在另一个文件中。我们已经在第 10.2.2 节中学习了如何从文件中读取整数。第 9 章解释了如何对数组排序。在这里，我们将这两者结合起来。这些是程序的最初几个步骤：

1. 检查是否有用于输入和输出文件名的命令行参数。
2. 打开输入文件。
3. 从文件中读取整数并统计文件中整数的个数。
4. 分配内存来这些整数。

如图 10.1 所示，文件是一个流。每当从文件中读取内容时，流就会向前移动。在统计完整数个数后，流就到达了末尾。为了填充数组，必须再次从头开始读取文件。我们可以通过几种方法实现。一种方法是关闭文件并重新打开。更优的方法是使用 `fseek`。它可以跳转到文件的特定位置。跳转到文件开头的方法：`fseek(fptr, 0, SEEK_SET)`。

有些人人认为调用 `rewind` 等同于 `fseek(fptr, 0, SEEK_SET)`。这并不是真的。`fseek` 的返回值报告了执行是否成功，但 `rewind` 既不报告成功也不报告失败。

剩余步骤为：

5. 使用 `fseek` 回文件开头。
6. 再次读取文件并填充数组。
7. 对数组排序。
8. 关闭输入文件。
9. 打开输出文件。
10. 将排序后的数组写入输出文件。
11. 关闭输出文件。
12. 释放数组的内存。

这些某些步骤的顺序可以改变。例如，程序可以在关闭输出文件（步骤 11 和 12）之前或之后释放数组内存。步骤 8 和 9 的顺序也可以交换。然而，某些步骤的顺序是不能改变。例如，步骤 9（打开输出文件）必须在步骤 10（写入文件）之前。这只能通过对代码逻辑思考来确定。在编写复杂程序时，在编写代码之前写下步骤是非常重要的。这可以节省大量时间，而且通常在输入第一行代码之前就可以考虑潜在的问题。

下面是该程序的示例解决方案。如果我们将程序与上述步骤进行比较，会发现它们之间的对应关系。此程序使用内置的 `qsort` 函数对整数进行排序。

```c
#include <stdio.h>
#include <stdlib.h>
int compare(const void* arg1, const void* arg2) {
    int *ptr1 = (int*)arg1; // 类型转换
    int *ptr2 = (int*)arg2;
    int val1 = *ptr1; // 从地址获取值
    int val2 = *ptr2;
    if (val1 < val2) // 比较值
        return -1;
    if (val1 == val2)
        return 0;
    return 1;
}
int main(int argc, char* argv[]) {
    // 需要两个文件名：输入和输出
    if (argc < 3)
        return EXIT_FAILURE;
    // 打开输入文件
    FILE *infptr;
    infptr = fopen(argv[1], "r");
    if (infptr == NULL)
        return EXIT_FAILURE;
    // 统计文件中整数的个数
    int count = 0;
    int val;
    while (fscanf(infptr, "%d", &val) == 1)
        count++;
    // 为数组分配内存
    int *arr;
    arr = malloc(sizeof(int) * count);
    if (arr == NULL) {
        fclose(infptr);
        return EXIT_FAILURE;
    }
    // 跳转到文件开头
    fseek(infptr, 0, SEEK_SET);
    // 再次读取文件并填充数组
    int ind = 0; // 数组索引
    while (fscanf(infptr, "%d", &val) == 1) {
        arr[ind] = val;
        ind++;
    }
    // 对数组排序
    qsort(&arr[0], count, sizeof(int), compare);
    // 关闭输入文件
    fclose(infptr);
    // 打开输出文件
    FILE *outfptr;
    outfptr = fopen(argv[2], "w");
    if (outfptr == NULL) {
        free(arr); // 不要忘记释放内存
        return EXIT_FAILURE;
    }
    // 将排序后的数组写入输出文件
    for (ind = 0; ind < count; ind++) {
        fprintf(outfptr, "%d\n", arr[ind]);
    }
    // 关闭输出文件
    fclose(outfptr);
    // 释放数组内存
    free(arr);
    return EXIT_SUCCESS;
}
```

## 11.2 统计字符出现次数

该程序从文件中读取字符并统计它们的出现次数。程序不区分大写和小写字符。只统计英语中使用的拉丁字母。如果字符不是拉丁字母，则该字符将被忽略。然后程序将出现次数保存到输出文件中。

该程序包含以下步骤：

1. 检查是否有用于输入和输出文件的命令行参数。
2. 创建一个整数数组。首选固定大小数组，因为数组的大小是预知的。这意味着数组可以放置在栈上，我们不需要调用 `malloc` 和 `free`。
3. 打开输入文件。
4. 从文件中读取字符。如果字符是拉丁字母，则对应的数组元素加一。
5. 关闭输入文件。
6. 打开输出文件。
7. 将数组元素写入输出文件。
8. 关闭输出文件。

这些步骤与上一个程序相似，除了统计字符的部分。下面是上述步骤的示例实现。

```c
#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#define NUM_CHAR 26
int main(int argc, char* argv[]) {
    if (argc < 3) // 需要输入和输出
        return EXIT_FAILURE;
    // 创建整数数组
    int count[NUM_CHAR] = {0}; // 初始化为零
    // 打开输入文件
    FILE *infptr;
    infptr = fopen(argv[1], "r");
    if (infptr == NULL)
        return EXIT_FAILURE;
    // 统计字符的出现次数
    int onechar;
    do {
        onechar = fgetc(infptr);
        if (isupper(onechar))
            count[onechar - 'A']++;
        if (islower(onechar))
            count[onechar - 'a']++;
    } while (onechar != EOF);
    // 关闭输入文件
    fclose(infptr);
    // 打开输出文件
    FILE *outfptr;
    outfptr = fopen(argv[2], "w");
    if (outfptr == NULL)
        return EXIT_FAILURE;
    // 将数组元素写入文件
    int ind;
    for (ind = 0; ind < NUM_CHAR; ind++) {
        fprintf(outfptr, "%c: %d\n", ind + 'A', count[ind]);
    }
    // 关闭输出文件
    fclose(outfptr);
    return EXIT_SUCCESS;
}
```

## 11.3 统计单词出现次数

此程序接受三个参数：

1. `argv[1]`：输入文件名。
2. `argv[2]`：输出文件名。
3. `argv[3]`：要查找的单词。

该程序检测并统计输入文件中 `word` 的出现次数。如果输入文件中包含 `word`，程序会将该行写入输出文件。在检查完文件中所有行后，程序将总数写入输出文件。我们必须首先考虑如何统计单词。如果搜索单词是 "eye"，而文件中包含 "eyeye"，你数 1 还是 2？在不同情况下两种定义都是接受的，我们需要决定使用哪种。为了简单起见，文件的每行最多包含 80 个字符。程序不统计跨行的单词。程序使用 `strstr` 在行内搜索单词。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#define LINE_LENGTH 80
int main(int argc, char* argv[]) {
    if (argc < 4) {
        printf("需要三个参数。\n");
        return EXIT_FAILURE;
    }
    // 打开输入文件
    FILE *infptr;
    infptr = fopen(argv[1], "r");
    if (infptr == NULL)
        return EXIT_FAILURE;
    // 打开输出文件
    FILE *outfptr;
    outfptr = fopen(argv[2], "w");
    if (outfptr == NULL) {
        fclose(infptr);
        return EXIT_FAILURE;
    }
    int count = 0;
    char line[LINE_LENGTH];
    while (fgets(line, LINE_LENGTH, infptr) != NULL) {
        if (strstr(line, argv[3]) != NULL) {
            fprintf(outfptr, "%s", line);
        }
        char* chptr = line;
        while ((chptr = strstr(chptr, argv[3])) != NULL) {
            count++;
            // 如果 "eyeye" 计两个 "eye"
            chptr++;
            // 如果 "eyeye" 计为一个 "eye"
            // chptr += strlen(argv[3]);
        }
    }
    fprintf(outfptr, "%d\n", count);
    // 关闭输入文件
    fclose(infptr);
    // 关闭输出文件
    fclose(outfptr);
    return EXIT_SUCCESS;
}
```

## 11.4 如何注释代码

几乎所有的编程课程都要求学生对代码进行注释。此外，几乎所有的编程书籍都告诉读者注释代码。然而，很少有课程或书籍说明如何注释代码。写注释就像写文章，注释很难评分的。注释是为了与代码的阅读者交流：风格和清晰度非常重要。如果注释没有解释代码，它们就没有用。目前还无法通过计算机程序来检查注释的用性。通过肉眼（通常由助教）评价注释是耗费人力的。因此，某些教授在评分时不考虑注释，而大多数学生并不认真对待注释。有时学生甚至会写像“因为教授是这么说的”这样的注释。有些学生问我：“我需要为你写注释吗？”我的回答是：“你需要为你自己写注释”。在编写复杂程序时，在编写代码之前写下步骤是非常重要的。这可以节省大量时间，而且通常在输入第一行代码之前就可以考虑潜在的问题。

# 13 递归函数

## 13.1 带有限制的球选择

## 13.2 单向道街道

## 13.3 汉诺塔

## 13.4 整数划分

## 13.5 阶乘

## 13.6 斐波那契数列

## 13.7 使用 gprof 进行性能分析





# 第 14 章：整数划分

## 14.1 栈与堆内存
## 14.2 追踪递归函数调用
## 14.3 带限制的划分生成 
### 14.3.1 仅使用奇数
### 14.3.2 使用递增序列
### 14.3.3 使用奇偶数交替序列
### 14.3.4 使用 `gprof` 和 `gcov` 识别性能瓶颈

前两章解释了如何获取整数划分的公式，以及如何编写实现该公式的 C 程序。本章解释了如何打印划分结果，并引入了该问题的某些变体。以下程序打印在命令行指定整数的划分方案：

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
void printPartition(int *arr, int length) {
    int ind;
    for (ind = 0; ind < length - 1; ind++) {
        printf("  %d + ", arr[ind]);
    }
    printf("  %d\n", arr[length - 1]);
}

void partition(int *arr, int ind, int left) {
    int val;
    if (left == 0) {
        printPartition(arr, ind);
        return; // 不是必要的
    }
    for (val = 1; val <= left; val++) {
        arr[ind] = val;
        partition(arr, ind + 1, left - val);
    }
}

int main(int argc, char *argv[]) {
    if (argc != 2) {
        return EXIT_FAILURE;
    }
    int n = (int)strtol(argv[1], NULL, 10);
    if (n <= 0) {
        return EXIT_FAILURE;
    }
    int *arr;
    arr = malloc(sizeof(int) * n);
    partition(arr, 0, n);
    free(arr);
    return EXIT_SUCCESS;
}
```

`partition` 函数是该程序的核心。该函数接受三个参数：
1. `arr` 是一个整数指针。它是一个存储划分中所用数字的数组。
2. `ind` 是一个整数。它是数组的索引。该值表示下一个元素写入的位置。它也提供了到目前划分的长度。
3. `left` 是一个整数。它是剩余划分的数值。

第 21 行的 `return` 是必要的。当 `left` 为 0 时，函数不会进入 `for` 循环。添加这个返回语句使程序更易读。当 `main` 调用 `partition` 时，`ind` 为 0——即数组第一个元素的索引。`left` 是剩余划分的数值。尽管这个程序很短，但它回顾了之前解释过的许多重要概念。因此，值得详细解释。

### 1. 栈与堆内存
假设 `n` 的值为 4。下表显示了在运行第 42 行之后、第 43 行之前的栈和堆内存情况。表假设每个整数占用 4 字节（`sizeof(int)` 为 4）。

（为了简洁，省略表格数据）

## 14.2 追踪递归函数调用
理解此程序的另一种方法是绘制它的调用树。调用树是函数调用之间关系的图形化表示。这棵树是“倒置”绘制的，根在顶部，叶节点在底部。考虑以下示例：

```c
void f1() {
    f2();
}
```
图 14.1 展示了这两个函数的调用关系。这里是另一个例子，图 14.2 显示了调用关系：

```c
void f1() {
    f2();
    f3();
}
void f2() {
    f3();
}
```
图 14.2：`f1` 调用 `f2` 和 `f3` 的图形化说明。`f2` 也调用了 `f3`。

这是第三个例子，调用关系如图 14.3 所示：

```c
void f1() {
    f2();
    f3();
}
void f2() {
    f3();
}
```
图 14.3：`f1` 调用 `f2` 和 `f3`；`f2` 也调用 `f3`。

在这里我们在函数 `f1` 中添加了一个循环，图 14.4 显示了该关系：

```c
void f1() {
    int count;
    for (count = 1; count < 4; count++) {
        f2();
    }
    f3();
}
void f2() {
    f3();
}
```
图 14.4：`f1` 在循环中调用 `f2` 并在循环外调用 `f3`；`f2` 调用 `f3`。

接下来，让我们考虑 `partition` 函数的骨架：

```c
void partition(int *arr, int ind, int left) {
    int val;
    for (val = 1; val <= left; val++) {
        arr[ind] = val;
        partition(arr, ind + 1, left - val);
    }
}
```
图 14.5 展示了调用关系。当 `left` 为 3 时，`val` 可以为 1、2 或 3。
1. 当 `val` 为 1 时，`left-val` 为 2。调用了 `partition(arr, 1, 2)`。
2. 当 `val` 为 2 时，`left-val` 为 1。调用了 `partition(arr, 1, 1)`。
3. 当 `val` 为 3 时，`left-val` 为 0。调用了 `partition(arr, 1, 0)`。

当 `left` 为 2 时，`val` 可以为 1 或 2。调用关系如图 14.6 和 14.7 所示。调用树是理解关系的另一种方法，因为每次调用由参数表示，我们不需要检查每次栈中的地址和值。

## 14.3 带限制的划分
程序开头打印了所有可能的划分。本节解释了如何生成带限制的划分，例如使用奇数或使用递增序列。一种简单的解决方案是在打印之前检查是否满足了限制。因此，在基准情况中，函数检查该划分是否有效。例如，如果我们使用奇数进行划分，`printPartition` 可以修改如下：

```c
void printPartition(int *arr, int length) {
    int ind;
    // 检查是否有数字为偶数
    // 如果使用了偶数，则不打印
    for (ind = 0; ind < length; ind++) {
        if (arr[ind] % 2 == 0) {
            return;
        }
    }
    for (ind = 0; ind < length - 1; ind++) {
        printf("  %d + ", arr[ind]);
    }
    printf("  %d\n", arr[length - 1]);
}
```

检查数字是否形成递增序列：

```c
void printPartition(int *arr, int length) {
    int ind;
    for (ind = 0; ind < length - 1; ind++) {
        if (arr[ind] >= arr[ind + 1]) { // 不是递增
            return;
        }
    }
    for (ind = 0; ind < length - 1; ind++) {
        printf("  %d + ", arr[ind]);
    }
    printf("  %d\n", arr[length - 1]);
}
```

在打印之前检查是无效的，因为已经生成了许多无效划分。相反，更高效的解决方案是不生成无效划分。本节解释了如何生成满足以下限制的划分：
(i) 仅使用奇数，
(ii) 使用递增数字，以及
(iii) 使用奇偶交替数字。

### 14.3.1 仅使用奇数
`partition` 函数仅生成符合标准的划分。因此比生成所有划分后再进行过滤的方法快。如果仅使用奇数，`val` 只能是奇数。

```c
void partition(int *arr, int ind, int left) {
    int val;
    if (left == 0) {
        printPartition(arr, ind);
        return;
    }
    for (val = 1; val <= left; val += 2) { // 仅奇数
        arr[ind] = val;
        partition(arr, ind + 1, left - val);
    }
}
```
这将生成更少的划分且所有都是有效的。

### 14.3.2 使用递增序列
为了生成递增数字的划分，`val` 的最小值必须大于存储在 `arr` 中最近使用的值。然而，如果 `ind` 为 0，则 `arr` 中没有存储之前使用的值，`val` 可以从 1 开始。

```c
void partition(int *arr, int ind, int left) {
    int val;
    if (left == 0) {
        printPartition(arr, ind);
        return;
    }
    int min = 1;
    if (ind != 0) {
        min = arr[ind - 1] + 1;
    }
    for (val = min; val <= left; val++) {
        arr[ind] = val;
        partition(arr, ind + 1, left - val);
    }
}
```

### 14.3.3 使用奇偶数交替序列
为了生成奇偶交替数字，函数必须检查 `ind` 是否为 0。如果是 0，`val` 可以是奇数或偶数，因为 `val` 正在写入划分的第一个位置。如果 `ind` 大于 0，则函数需要检查 `arr[ind-1]`。如果 `arr[ind-1]` 是奇数，则 `val` 必须是偶数；如果 `arr[ind-1]` 是偶数，则 `val` 必须是奇数。这在第 18 行进行了检查。

```c
void partition(int *arr, int ind, int left) {
    int val;
    if (left == 0) {
        printPartition(arr, ind);
        return;
    }
    for (val = 1; val <= left; val++) {
        int valid = 0;
        if (ind == 0) { // 第一个数字没有限制
            valid = 1;
        } else {
            valid = (arr[ind - 1] % 2) != (val % 2);
        }
        if (valid == 1) {
            arr[ind] = val;
            partition(arr, ind + 1, left - val);
        }
    }
}
```
第 18 行测试 `arr[ind-1]` 和 `val` 是否同为偶数或奇数。你可以看到，通过少量的更改，程序就可以处理不同限制下的划分问题。

### 14.3.4 使用 `gprof` 和 `gcov` 识别性能瓶颈
第 13 解释了如何使用 `gprof` 来识别改进机会。本节使用 `gprof` 比较不同的划分方法。在以下程序中，`partition1` 生成有效划分，但 `partition2` 生成了所有可能的划分。由于 `printPartition` 在此例子中什么都没做（因为打印大量行会显著降低程序速度），不需要检查这个函数。我们可以检查 `partition1` 和 `partition2` 的性能。

（包含 `partition1`, `partition2` 和 `isValid` 的 C 代码）

这是 `n` 为 30 时的 `gprof` 报告。Flat profile：每个样本计为 0.01 秒。

| function | self | self_total | calls |
| :--- | :--- | :--- | :--- |
| partition1 | 0.18 | 0.18 | 1001 |
| partition2 | 0.75 | 0.75 | 10374 |
| isValid | 0.28 | 0.28 | 5368012 |
| printPartition | 0.00 | 0.00 | 20786 |

这显示程序的 99% 执行时间被 `partition2` (55.7%) 和 `isValid` (43.3%) 占用。由于 `isValid` 仅由 `partition2` 调用，报告显示时间为 98.5%。为什么会有如此大的差异？原因是 `partition2` 在打印之前生成了许多无效划分并进行了过滤。相比之下，`partition1` 只生成有效划分。后者减少了大量的调用树，因此高效得多。注意 `printPartition` 被 `partition1` 调用了 1001 次，被 `partition2` 调用了 10393 次。这是预期的，因为 `partition1` 和 `partition2` 应该打印相同的划分。`partition2` 被递归调用了 10374 次，而 `partition1` 只被调用了 30288 次。报告还显示 `isValid` 被调用了 5368012 次，而 `printPartition` 只调用了 20786 次。注意 55.7%、43.28% 和 1.50% 之和为 100.5%。累计时间可能超过 100% 吗？

当我们想要提高程序性能时，首先需要识别耗时最长的函数。我们可以通过 `gprof` 获得帮助。

# 第 15 章：递归算法问题
本章描述了几个可以使用递归解决的问题。

## 15.1 二分查找
使用 `for` 或 `while` 循环解决这些问题更为困难。在每个情况下，计算所需的迭代次数是不直观的，实现细节也会非常复杂。递归之所以简单，是因为可以假设简单的情况已经解决。只需要弄清楚如何用更小的解决方案表示解决方案，只要基准情况正确，整个就能工作。本书非常强调递归，因为递归总是一个良好的策略，而且因为它是解决某类问题的极方法。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int binaryHelper(int *arr, int low, int high, int key) {
    if (low > high) {
        return -1;
    }
    int ind = (low + high) / 2;
    if (arr[ind] == key) {
        return ind;
    }
    if (arr[ind] > key) {
        return binaryHelper(arr, low, ind - 1, key);
    }
    return binaryHelper(arr, ind + 1, high, key);
}

int binarySearch(int *arr, int len, int key) {
    return binaryHelper(arr, 0, len - 1, key);
}
```

二分查找是在排序数组中搜索某个内容的有效方法。函数定义应该类似于：`int search(int *arr, int len, int key)`。`search` 函数返回 `key` 在 `arr` 中的索引。如果 `arr` 不包含该键，则函数返回 -1。参数含义如下：
- `arr`：整数数组。元素是按升序排序的。
- `len`：数组的长度，即数组中元素的个数。
- `key`：要查找的值。将其想象成大海捞针。

由于数组已经排序，可以通过将 `key` 与数组中间的元素进行比较来快速丢弃许多元素。如果 `key` 大于中间元素，则不需要考虑的下半部分；如果 `key` 小于中间元素，则不需要考虑的上半部分。这种想法可以推广为：不是考虑整个数组，而是只考虑数组的一个连续部分。因此，有四种情况：
- 数组的连续部分没有元素，函数返回 -1。
- `key` 与连续部分的中间元素相同，找到了索引，返回该索引。
- `key` 大于中间元素，函数丢弃下半部分。
- `key` 小于中间元素，函数丢弃上半部分。

这些步骤持续进行直到找到索引或无法匹配。图 15.1 是步骤的图形化视图：在每一步中，二分查找将搜索元素数量减半。在第一步中，`key` 与中间的元素进行比较。如果 `key` 小于中间元素，则在数组的上半部分查找。如果 `key` 大于中间元素，则在数组的下半部分查找。必须排序。

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

#define RANGE 100

int *arrGen(int size); // 生成排序整数数组
int binaryHelper(int *arr, int low, int high, int key);
int binarySearch(int *arr, int len, int key);
void printArray(int *arr, int len);

int main(int argc, char **argv[]) {
    if (argc < 2) {
        printf("需要一个整数\n");
        return EXIT_FAILURE;
    }
    int num = strtol(argv[1], NULL, 10);
    if (num <= 0) {
        printf("需要一个整数\n");
        return EXIT_FAILURE;
    }
    int *arr = arrGen(num);
    printArray(arr, num);
    for (int count = 0; count < 10; count++) {
        int key;
        if (count % 2 == 0) {
            key = arr[rand() % num];
        } else {
            key = rand() % 100;
        }
        printf("search (%d), result = %d\n", key, binarySearch(arr, num, key));
    }
    free(arr);
    return EXIT_SUCCESS;
}
```

此程序引入了辅助函数的概念。在递归中，辅助函数用于正确组织参数。在这个例子中，`binarySearch` 有三个参数；然而递归函数需要四个参数。与其传递数组的长度，不如用两个参数表示剩余剩余数组。范围用两个参数表示：`low` 和 `high`。请注意范围在递归调用中的变化：范围在每次调用中必须缩小。这确保了递归调用链最终到达终止条件。第 16 行使用整除：如果 `low + high` 是奇数，余数会被丢弃，因为 `ind` 是整数。仔细注意第 23 行使用 `ind - 1` 作为新的高索引。一个常见的错误是使用 `ind`。这将导致问题，因为无法保证范围在递归调用中缩小。例如，考虑范围只有一个元素的情况。这发生在 `low` 等 `high` 时。它们的平均 `ind` 也是相同的。如果第 23 行使用 `ind`，那么对辅助函数的下次调用也将具有 `low` 等于 `high`。参数保持不变，递归不会结束。同样，在第 25 行，`low` 索引必须是 `ind + 1` 而不是 `ind`。另一个常见错误是在第 12 行条件使用 `if (low >= high)`。当数组只有一个元素需要检查时，这是错误的。该函数在没有检查该单个元素是否等于 `key` 的情况下返回了 -1。

## 15.3 排列与组合
排列可以通过以下递归生成：将第一个元素与任何后续位置交换，然后将第二个元素与任何后续位置交换，依此类推。以下示例应使其更清晰：

A B C D

第一个元素 A 可能出现在第一、第二、第三或第四列。每当 A 移动时，它与该列的原始元素交换。第二个元素 B 也可能出现在第一、第二、第三或第四列。然而，我们需要排除将 B 放在第一列，因为 A 通过与 B 交换出现在第二列。因此，B 已经有机会移动到第一列，只需要移动到第二（原始位置）、第三和第四列。同样，C 可能出现在第三或第四列。

以下实现生成数组的所有排列。它需要一个命令行参数来设置数组长度。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void printArray(int *arr, int length) {
    int ind;
    for (ind = 0; ind < length - 1; ind++) {
        printf("  %c ", arr[ind]);
    }
    printf("  %c\n", arr[length - 1]);
}

void swap(int *a, int *b) {
    int s = *a;
    *a = *b;
    *b = s;
}

void permuteHelp(int *arr, int ind, int num) {
    if (ind == num) {
        printArray(arr, ind);
        return;
    }
    int loc; // arr[ind] 的目标
    for (loc = ind; loc < num; loc++) {
        swap(&arr[ind], &arr[loc]);
        permuteHelp(arr, ind + 1, num);
        swap(&arr[ind], &arr[loc]); // 回溯
    }
}

void permute(int *arr, int num) {
    permuteHelp(arr, 0, num);
}

int main(int argc, char **argv[]) {
    if (argc != 2) {
        return EXIT_FAILURE;
    }
    int num = strtol(argv[1], NULL, 10);
    if (num <= 0) {
        return EXIT_FAILURE;
    }
    int *arr = malloc(sizeof(int) * num);
    for (int ind = 0; ind < num; ind++) {
        arr[ind] = ind;
    }
    permute(arr, num);
    free(arr);
    return EXIT_SUCCESS;
}
```

第 28 到 33 行是生成排列的核心。理解其工作原理的方法是检查迭代次数。当 `ind` 为 0 时，循环执行 `num` 次。当 `ind` 为 1 时，循环执行 `num-1` 次。当 `ind` 为 2 时，循环执行 `num-2` 次。最后，当 `ind` 为 `num-1` 时，循环执行一次。程序将执行执行 $num \times (num-1) \times \dots = num!$ 次。这是 $num$ 个元素的排列数。

另一种方法用于生成组合。与其排列数组，不如使用一个数组来存储每个元素是否被选中。例如，如果 `arr[0]` 为 0，则元素未被选中；如果 `arr[0]` 为 1，则元素被选中。如果 `arr[2]` 为 0，则元素未被选中；如果 `arr[2]` 为 1，则元素被选中。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void printArray(int *arr, int length) {
    int ind;
    for (ind = 0; ind < length - 1; ind++) {
        if (arr[ind] == 1) printf("  A ");
        else printf("  B ");
    }
    printf("\n");
}

void combineHelp(int *arr, int ind, int sel, int sum) {
    if (sum == sel) { // 元素足够
        printArray(arr, ind);
        return;
    }
    if (ind == num) { // 数组结束，没有更多元素可选
        return;
    }
    // 选中此元素
    arr[ind] = 1;
    combineHelp(arr, ind + 1, sel, sum + 1);
    // 不选择此元素
    arr[ind] = 0;
    combineHelp(arr, ind + 1, sel, sum);
}

void combine(int *arr, int num, int sel) {
    combineHelp(arr, 0, sel, 0);
}

int main(int argc, char **argv[]) {
    if (argc != 3) {
        return EXIT_FAILURE;
    }
    int num = strtol(argv[1], NULL, 10);
    if (num <= 0) {
        return EXIT_FAILURE;
    }
    int sel = strtol(argv[2], NULL, 10);
    if (sel <= 0 || sel > num) {
        return EXIT_FAILURE;
    }
    int *arr = malloc(sizeof(int) * num);
    for (int ind = 0; ind < num; ind++) {
        arr[ind] = 0;
    }
    combine(arr, num, sel);
    free(arr);
    return EXIT_SUCCESS;
}
```

## 15.2 快速排序
第 9 节解释了如何使用 `qsort` 函数。本节解释了 `quicksort` 的工作原理。如之前提到的，快速排序使用了传递性概念：如果 $x > y$ 且 $y > z$，那么 $x > z$。

该算法首先从数组中选择一个元素：是哪一个并不重要。该元素被称为基值（pivot）。有些实现使用第一个或最后一个元素；有些使用随机选择的元素。选择基值后，算法将数组分为三部分：
(i) 小于基值的元素，
(ii) 等于基值的元素，以及
(iii) 大于基值的元素。通过将元素分为三部分，算法避免了不必要的比较。这种算法通常比其他算法快，被称为“快速排序”。将元素分为三部分后，算法然后递归地排序 (i) 和 (iii)。

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void swap(int *a, int *b) {
    int s = *a;
    *a = *b;
    *b = s;
}

void quickSortHelp(int *arr, int first, int last) {
    if (first >= last) {
        return;
    }
    int pivot = arr[first];
    int low = first + 1;
    int high = last;
    while (low <= high) {
        while (low <= high && arr[low] <= pivot) {
            low++;
        }
        while (low <= high && arr[high] > pivot) {
            high--;
        }
        if (low < high) {
            swap(&arr[low], &arr[high]);
        }
    }
    swap(&arr[first], &arr[high]);
    quickSortHelp(arr, first, high - 1);
    quickSortHelp(arr, low, last);
}

void quickSort(int *arr, int len) {
    quickSortHelp(arr, 0, len - 1);
}
```

## 15.4 栈排序
栈可以用于排序序列，根据“后进先出”（LIFO）规则。栈排序算法如下：
1. 创建一个空栈。
2. 从序列中读取一个数字，称为 $x$。
3. 如果栈不为空且栈顶元素大于 $x$，则弹出栈顶元素并将其输出。
4. 将 $x$ 入栈。
5. 重复步骤 2-4 直到序列结束。
6. 最后，将栈中的所有元素弹出并输出。

栈排序是基于“后进先出”规则的。栈可以存储信息。栈排序是有效的，如果满足某些条件。几个示例说明了栈排序如何工作。

### 15.4.1 示例 1
考虑序列 2, 1。读取 2，栈空，将 2 入栈。读取 1，栈不为空且栈顶（2）大于 1，弹出 2 并输出。将 1 入栈。序列结束，最后将栈中的所有元素弹出：输出 2 1。结果为 2, 1。

### 15.4.2 示例 2
考虑序列 1, 2。读取 1，栈空，将 1 入栈。读取 2，栈不为空但栈顶（1）不大于 2，将 2 入栈。序列结束，最后将栈中的所有元素弹出：输出 2 1。结果为 2, 1。

### 15.4.3 示例 3
考虑序列 1, 3, 2。读取 1，栈空，将 1 入栈。读取 3，栈不为空但栈顶（1）不大于 3，将 3 入栈。读取 2，栈不为空且栈顶（3）大于 2，弹出 3 并输出。将 2 入栈。序列结束，最后将栈中的所有元素弹出：输出 3 2 1。结果为 3, 2 1。

### 15.4.4 示例 4
考虑序列 2, 3, 1。读取 2，栈空，将 2 入栈。读取 3，栈不为空但栈顶（2）不大于 3，将 3 入栈。读取 1，栈不为空且栈顶（3）大于 1，弹出 3 并输出。将 1 入栈。此时栈不为空且栈顶（2）大于 1，弹出 2 并输出。将 1 入栈。序列结束，最后将栈中的所有元素弹出：输出 3 2 1。结果为 3 2 1。

### 15.4.5 栈可排序的
令 $M$ 为整个序列的最大值。泛指地说，一个序列可以分为三部分：$M$ 之前的 $A$，$M$ 以及 $M$ 之后的 $B$。第一部分或第三部分（或两者）可能是空的。如果 $M$ 是第一个数字，则 $A$ 是空的。如果 $M$ 是最后一个数字，则 $B$ 是空的。

算法的第 5 步在读取 $M$ 时弹出栈中的所有数字。假设 $M$ 是 $A$ 中的最大值。所有值都满足 $A < M$，因为 $M$ 是最大值。假设 $B$ 是 $B$ 中的最小值。如果 $B < M$，则 $B$ 应该在 $M$ 弹出之前弹出。然而，当 $M$ 入栈时，$A$ 已经弹出，没有机会让 $B$ 在 $M$ 之前弹出。因此，对于该序列栈失败了。在最后一个例子 2, 3, 1 中，$M$ 为 3，$A$ 为 2，$B$ 为 1。满足 $B < M$ 的条件，所以 2, 3, 1 不是栈可排序的。

序列 1, 5, 2, 3, 5, 4 是栈可排序的吗？注意最大值 5 在序列中出现了两次。按照之前描述的步骤，第一个数字 1 入栈。下一个数字 5 比 1 大，所以弹出 1 并入栈 5。第三个数字 2 比 5 小，入栈。下一个数字 3，所以弹出 2 并入栈 3。下一个数字 5，所以弹出 3 并入栈 5。最后一个数字 4 入栈。最后，所有数字弹出，结果为 1, 2, 5, 4.





# 第 18 章 链表

## 18.1 可扩展类型

在之前的章节中，我们描述了两种常见的内存分配方法。第一种是静态分配。静态分配的优点是不会发生内存泄漏；然而，数组的大小在编写程序时必须已知。例如 `int arr[100];`，这创建了一个包含 100 个元素的数组。

在很多情况下，当程序编译时大小是未知的，但在程序开始执行后是知的。这是第二种场景。下例所示，大小由用户给出：

```c
int *arr2;
int length;
printf (" Please enter the length of the array : ");
scanf (" %d", &length);
arr2 = malloc (length * sizeof (int));
```

这种场景通常用于从文件中读取数据。一种常见的策略是：
1. 读取一次文件以确定需要多少内存。
2. 分配所需的内存。
3. 调用 `fseek` 返回文件开头。
4. 再次读取文件并将数据存储在分配的内存中。

本章描述了另一种常见场景：即使在程序开始后，知道大小也是不现实或不可能的内存必须根据需要分配和释放。这是一个非常常见的场景。想象你正在创建一个社交网络。会有多少用户注册？可能会有百万用户，但我们对此没有直接控制权。我们不能设定一个预定的数字（例如五百万），并在五百万之后拒绝注册。也许我们可以为几十亿用户分配足够的内存以备未来，但那是浪费的。此外，用户会来来去。有些用户注册后忘记了密码并重新创建账户。可能需要删除超过一年的账户。为了管理这类应用程序，我们必须根据需要分配内存。内存使用必须根据应用程序的需求增长和缩小。本章描述了如何使用结构体。本书仅涵盖了基本概念，并没有提供足够构建实际社交网络的知识。然而，本章的信息提供了一个基础。

如果数据结构（如数组）在程序运行时需要更改大小，我们可以创建一个更大（或更小）的数组，复制数据，然后释放旧数组。第 17.2 节给出自动调整大小数组的示例：如果插入数字太多，数组的大小将翻倍。本章解释了如何创建一个不需要复制现有数据即可的简单数据结构。它支持以下函数：
* Insert（插入）：添加新数据，并根据需要分配内存。
* Search（查找）：确定某条数据是否已经插入。
* Delete（删除）：移除数据并在不再需要时释放内存。
* Print（打印）：打印存储的数据。
* Destroy（销）：在程序结束前删除所有内容。

这种简单的数据结构被称为链表，它是动态结构的一个示例，也是容器结构的示例。此类结构可以包含不同类型的数据（`int`、`char`、`Person` ...）。对于每个不同类型，插入、查找、删除、打印和销的代码非常相似。下一章将描述另一种容器结构，称为二叉树。

## 18.2 链表

链表是由指针连接在一起的节点集合。每个节点都是包含至少两个属性的对象：
* 指向另一个节点的指针。按照惯例，该属性称为 `next`。如果给定节点没有“下一个”节点，则 `next` 属性存储 `NULL`。
* 一些数据。该属性可以是指针、对象或原始类型，如 `int`、`char` 或 `double`。

下面是一个示例结构体，具有两个属性，用作链表的节点。为了简单起见，数据属性是一个整数。

```c
typedef struct listnode {
    struct listnode *next;
    int value;
} Node; // 不要忘记
```

这引入了“自引用结构体”的概念。注意 `next` 是如何指向 `struct listnode` 的指针吗？这就是它自引用的原因。因为 C 编译器从上到下读取源文件，在声明 `next` 的时候它看不到类型名称 `Node`。因此，我们分配了一个临时名称：`struct listnode`。虽然称呼它们为 `struct listnode` 也是可以的，但从现在起该结构体被称为 `Node`。

图 18.1 显示了创建链表时第一个操作的三种视图。(b) 中的图示视图是最常用的。在 (b) 中，当指针的值为 `NULL` 时，通常让它指向电子学中使用的“地”（Ground）符号。同时显示三种视图是为了让我们看到不同表示形式之间的关系。

（图 18.1：链表从空开始，即没有任何 Node。此图显示了三种视图：(a) 源代码，(b) 图表，以及 (c) 栈内存。）

## 18.3 插入数据

图 18.2 显示了如何在链表中创建第一个节点，并为 value 属性赋值。

```c
Node *head = NULL;
head = malloc(sizeof(Node));
head->next = NULL;
head->value = 917;
```

`malloc` 将在堆内存中为这两个属性分配空间。假设 `malloc` 返回地址 `60000`，那么该值被赋值给 `head` 的 value。

（图 18.2：创建一个值为为 917 的 Node。注意 `head` 是一个指针。）

下一行是 `head->next = NULL;`。这一行将 `NULL` 赋值给节点的 `next` 属性。然后，我们赋值 `head->value = 917`，即数据。

在 `->` 之前或之后添加空格没有区别。我们创建了一个函数 `List_insert`，它可以让插入节点变得简单得多。该函数可以：
* 为新节点分配内存。
* 为 `next` 属性赋值地址。
* 为 `value` 属性赋值值。

图 18.3 显示了该函数如何简化节点插入。使用 `-504` 作为参数调用 `List_insert` 会创建一个额外的节点并将其插入到链表开头。稍后，我们将解释如何在链表末尾插入 `-504`。在链表头部插入节点更为简单。请注意，这意味着存储在 `head` 中的值发生了变化。

```c
Node *head = NULL;
head = List_insert(head, 917);
```





# 霍曼压缩

425(a)(b)(c)  图 24.13: (a) 下一个命令（第八个字节中的第二个位）是 `0`。这将为前两个树节点创建一个公共父节点。(b) 下一个命令（第八个字节中的第三个位）也是 `0`。这将为前两个树节点创建一个公共父节点。(c) 下一个命令（第八个字节中的第四个位）是 `1`。这将创建一个用于存储值 `g` 的树节点。

![](img/bg1cb.png)

426 中级 C 语言编程

(a) (b)  图 24.14: 剩余的命令均为 `0`。继续构建树结构。(a) (b)  图 24.15: 完成树的构建。

霍曼压缩

427 以下是完整程序的最终版本，同时用于压缩和解压缩。

```c
// main.c
#include "encode.h"
#include "constant.h"
#include <stdlib.h>
#include <string.h>
int main(int argc, char **argv)
{
    // argv[1]: "e" 编码
    // "d" 解码
    // argv[2]: 输入文件名
    // argv[3]: 输出文件名
    if (argc != 4)
    {
        return EXIT_FAILURE;
    }
    if (strcmp(argv[1], "e") == 0)
    {
        encode(argv[2], argv[3]);
    }
    if (strcmp(argv[1], "d") == 0)
    {
        decode(argv[2], argv[3]);
    }
    return EXIT_SUCCESS;
}
```

```c
// encode.h
#ifndef ENCODE_H
#define ENCODE_H
// 编码输入（文本）文件
// 将结果保存到输出（二进制）文件中
// 如果无法从文件读取或写入文件则返回 0
// 如果成功返回 1
int encode(char *infile, char *outfile);
// 解码输入（二进制）文件
// 将结果保存到输出（文本）文件中
// 如果无法从文件读取或写入文件则返回 0
// 如果成功返回 1
int decode(char *infile, char *outfile);
#endif
```

```c
// encode.c
#include "encode.h"
#include "constant.h"
#include "freq.h"
#include "list.h"
#include "utility.h"
#include <stdio.h>
#include <strings.h>
#include <stdlib.h>
#include <values.h>
#define ENCODE_MODE 0
#define DECODE_MODE 1
void printFrequencyLate(CharFreq *frequencies);
void buildCodeBookHelper(TreeNode *tn, int **codebook, int *row, int col)
{
    if (tn == NULL)
    {
        return;
    }
    // 是叶子节点吗？
    TreeNode *lc = tn->left;
    TreeNode *rc = tn->right;
    if ((lc == NULL) && (rc == NULL))
    {
        // 完成一个编码
        codebook[*row][0] = tn->value;
        (*row)++;
        return;
    }
    if (lc != NULL)
    {
        // 填充整棵树的这一列
        int numRow = TreeLeaf(lc);
        int ind;
        for (ind = *row; ind < (*row) + numRow; ind++)
        {
            codebook[ind][col] = 0;
        }
        buildCodeBookHelper(lc, codebook, *row, col + 1);
    }
    if (rc != NULL)
    {
        int numRow = TreeLeaf(rc);
        int ind;
        for (ind = *row; ind < (*row) + numRow; ind++)
        {
            codebook[ind][col] = 1;
        }
        buildCodeBookHelper(rc, codebook, *row, col + 1);
    }
}
void buildCode(TreeNode *root, int **codebook)
{
    int row = 0;
    // 列起始 [0] 存储字符
    buildCodeBookHelper(root, codebook, &row, 1);
}
void printCode(int **codebook, int numRow)
{
    霍曼压缩
    for (int row = 0; row < numRow; row++)
    {
        // 输出字符
        printf("%c:", codebook[row][0]);
        int col = 1;
        while (codebook[row][col] != -1)
        {
            printf("%d ", codebook[row][col]);
            col++;
        }
        printf("\n");
    }
}
int compress(char *infile, char *outfile, int **codebook, int *mapping)
{
    FILE *infptr = fopen(infile, "r");
    if (infptr == NULL)
    {
        return 0;
    }
    FILE *outfptr = fopen(outfile, "a"); // 追加
    if (outfptr == NULL)
    {
        fclose(infptr);
        return 0;
    }
    unsigned char whichbit = 0;
    unsigned char curbyte = 0;
    while (!feof(infptr))
    {
        int onechar = fgetc(infptr);
        if (onechar != EOF)
        {
            int ind = mapping[onechar];
            int ind2 = 1;
            while (codebook[ind][ind2] != -1)
            {
                writeBit(outfptr, (codebook[ind][ind2] == 1), &whichbit, &curbyte);
                // fprintf(outfptr, "%d ", codebook[ind][ind2]);
                ind2++;
            }
        }
    }
    padZero(outfptr, &whichbit, &curbyte);
    fclose(infptr);
    fclose(outfptr);
    return 1;
}
```

```c
// 中级 C 语言编程
// 如果 endec 为 0: 编码，如果为 1: 解码
// 编码和解码必须翻转两个子树的顺序
static ListNode *MergeListNode(ListNode *head, int endec)
{
    ListNode *second = head->next;
    // second 不能为 NULL，否则将进入
    ListNode *third = second->next;
    // third 可能为 NULL
    // 获取前两个节点的树节点
    TreeNode *tn1 = head->tnptr;
    TreeNode *tn2 = second->tnptr;
    // 移除前两个节点
    free(head);
    free(second);
    head = third;
    TreeNode *mrg;
    if (endec == ENCODEMODE)
    {
        mrg = Merge(tn1, tn2);
    }
    else
    {
        mrg = Merge(tn2, tn1);
    }
    ListNode *ln = ListNodeCreate(mrg);
    if (endec == ENCODEMODE)
    {
        head = ListInsert(head, ln, SORTED);
    }
    else
    {
        head = ListInsert(head, ln, STACK);
    }
    return head;
}
// 合并前两个列表节点直到剩下一个列表节点
static TreeNode *list2Tree(ListNode *head)
{
    // ... 实现 ...
```

```c
#include <stdlib.h>
#include <values.h>
#define ENCODE_MODE 0
#define DECODE_MODE 1
void printFrequencyLate(CharFreq *frequencies);
void buildCodeBookHelper(TreeNode *tn, int **codebook, int *row, int col);
// ... 实现 ...
```

```c
// tree.h
#ifndef TREE_H
#define TREE_H
typedef struct node
{
    struct node *left;
    struct node *right;
    char value; // 字符
    int freq; // 频率
} TreeNode;
TreeNode *TreeNodeCreate(char val, int freq);
TreeNode *TreeMerge(TreeNode *tn1, TreeNode *tn2);
void TreePrint(TreeNode *tn, int level);
// 查找叶节点的高度
int TreeHeight(TreeNode *tn);
// 查找叶节点的数量
int TreeLeaf(TreeNode *tn);
// 保存压缩文件的头
void TreeHeader(TreeNode *tn, unsigned int numChar, char *outfile);
void TreeDestroy(TreeNode *tn);
#endif
```

```c
// tree.c
#include "tree.h"
#include "utility.h"
#include <stdio.h>
#include <stdlib.h>
TreeNode *TreeNodeCreate(char val, int freq)
{
    TreeNode *tn = malloc(sizeof(TreeNode));
    tn->left = NULL;
    tn->right = NULL;
    tn->value = val;
    tn->freq = freq;
    return tn;
}
TreeNode *TreeMerge(TreeNode *tn1, TreeNode *tn2)
{
    TreeNode *tn = malloc(sizeof(TreeNode));
    tn->left = tn1;
    tn->right = tn2;
    tn->value = 0; // 忽略
    tn->freq = tn1->freq + tn2->freq;
    return tn;
}
// 后序遍历
void TreePrint(TreeNode *tn, int level)
{
    if (tn == NULL)
    {
        return;
    }
    TreeNode *lc = tn->left; // 左孩子
    TreeNode *rc = tn->right; // 右孩子
    TreePrint(lc, level + 1);
    TreePrint(rc, level + 1);
    int depth;
    for (depth = 0; depth < level; depth++)
    {
        printf("");
    }
    printf("freq = %d", tn->freq);
    if ((lc == NULL) && (rc == NULL))
    {
        // 叶节点
        printf("value = %d,%c", tn->value, tn->value);
    }
    printf("\n");
}
static int TreeHeight(TreeNode *tn, int height)
{
    if (tn == NULL)
    {
        return height;
    }
    int lh = TreeHeight(tn->left, height + 1);
    int rh = TreeHeight(tn->right, height + 1);
    if (lh < rh)
    {
        return rh;
    }
    if (lh > rh)
    {
        return lh;
    }
    return lh;
}
int TreeHeight(TreeNode *tn)
{
    return TreeHeight(tn, 0);
}
static void TreeLeaf(TreeNode *tn, int *num)
{
    if (tn == NULL)
    {
        return;
    }
    // 如果是叶节点，加 1
    TreeNode *lc = tn->left;
    TreeNode *rc = tn->right;
    if ((lc == NULL) && (rc == NULL))
    {
        (*num)++;
        return;
    }
    TreeLeaf(lc, num);
    TreeLeaf(rc, num);
}
int TreeLeaf(TreeNode *tn)
{
    int num = 0;
    TreeLeaf(tn, &num);
    return num;
}
```

```c
// utility.h
#ifndef UTILITY_H
#define UTILITY_H
#include <stdio.h>
// 将一个位写入文件
// whichbit 指示写入位置（0 表示最左侧，7 表示右侧）
// curbyte 是当前字节
// 如果 whichbit 为 0，curbyte 重置并将位 放在最左侧
// 当位达到 7 时，将字节写入文件并将 whichbit 重置
// 函数返回 1 如果写入了字节
// 返回 0 如果没有写入字节
// 返回 -1 如果尝试写入失败
int writeBit(FILE *fptr, unsigned char bit, unsigned char *whichbit, unsigned char *curbyte);
// 如果 whichbit 不是 0，curbyte 的某些位未未使用
// 用这些位填充 0 并将字节写入文件
void padZero(FILE *fptr, unsigned char *whichbit, unsigned char *curbyte);
int readBit(FILE *fptr, unsigned char bit, unsigned char *whichbit, unsigned char *curbyte);
#endif
```

```c
// utility.c
#include <stdio.h>
#include "utility.h"
void padZero(FILE *fptr, unsigned char *whichbit, unsigned char *curbyte)
{
    int rtv;
    while (*whichbit != 0)
    {
        rtv = writeBit(fptr, 0, &whichbit, curbyte);
        if (rtv == -1)
        {
            return -1;
        }
    }
}
int readBit(FILE *fptr, unsigned char bit, unsigned char *whichbit, unsigned char *curbyte)
{
    int ret = 1;
    if (*whichbit == 0)
    {
        // 从文件中读取一个字节
        ret = fread(curbyte, sizeof(unsigned char), 1, fptr);
        if (ret != 1)
        {
            // 读取失败
            return -1;
        }
    }
    // 将位移动到正确位置
    unsigned char temp = (*curbyte) >> (7 - (*whichbit));
    temp = temp & 0X1; // 只获取 1 位，忽略其他的
    // 增加 1
    *whichbit = ((*whichbit) + 1) % 8;
    *bit = temp;
    return 1;
}
```

```c
// list.h
#ifndef LIST_H
#define LIST_H
#include "tree.h"
#include "constant.h"
#include "freq.h"
#include <stdio.h>
#define QUEUE 0
#define STACK 1
#define SORTED 2
typedef struct listnode
{
    struct listnode *next;
    TreeNode *tnptr;
} ListNode;
ListNode *ListBuild(CharFreq *frequencies);
ListNode *ListNodeCreate(TreeNode *tn);
// 模式是 QUEUE, STACK 或 SORTED
ListNode *ListInsert(ListNode *head, ListNode *ln, int mode);
void ListPrint(ListNode *head);
#endif
```

```c
// list.c
#include "list.h"
#include "freq.h"
#include <stdlib.h>
ListNode *ListNodeCreate(TreeNode *tn)
{
    ListNode *ln = malloc(sizeof(ListNode));
    ln->next = NULL;
    ln->tnptr = tn;
    return ln;
}
// ... 实现 ...
```

```makefile
# 这是是该程序的 Makefile。
CFLAGS = -g -Wall -Wshadow
GCC = gcc $(CFLAGS)
SRCS = main.c encode.c freq.c tree.c list.c utility.c
OBJS = $(SRCS:%.c=%.o)
VALGRIND = valgrind --leak-check=full --tool=memcheck --verbose --log-file
code: $(OBJS)
	$(GCC) $(OBJS) -o code
test1: code
	$(VALGRIND) ./code > input1
	./code > output1
test2: code
	$(VALGRIND) ./code > input2
	./code > output2
test3: code
	$(VALGRIND) ./code > input3
	./code > output3
.o: %.c
	$(GCC) $(CFLAGS) -c $<
clean:
	rm -f *.o code
```

# 附录

# 版本控制

## B 复杂的程序无法在一天内完成。此外，通常通过创建不同的版本来发布文件。版本控制是跟踪文件更改的方法。许多版本控制工具已经开发出来，例如：CVS, SVN, mercurial 和 git。

### B.1 Github.com

github.com 是一个为学生和老师提供免费版本控制服务的网站。在创建账户后，使用界面创建一个仓库（也称为 repo）。

## B.2 克隆仓库和修改文件

在创建仓库后，在 Linux 终端中输入：

`git clone https://account:password@github.com/.../dempo.git`

account 是你的用户名，password 是你的密码。将 `github.com/.../dempo.git` 替换为仓库的正确路径。你将在终端上看到如下内容：

```
Cloning into 'dempo'...
Counting objects: 4, done.
Compressing objects: 100% (4/4), done.
Total 4 (delta 0) reused 0
Unpacking objects: 100% (4/4), done.
```

在终端中输入 `ls` 命令，你可以看到 `dempo` 目录和文件。这里还有一个隐藏文件 `.gitignore`。

### B: 创建新仓库

在这个例子中，我将其命名为“dempo”。作为老师，我可以创建一个新版本。使用 `git commit` 来确保你有最新版本。必要时，新版本允许你回滚到之前的版本。

# 附录

# A Linux

## A.1 安装 Linux 的选项

设置 Linux 开发环境有多种选择：

*   购买一台已安装 Linux 的电脑。许多计算机厂商都提供这种。这是最简单的解决方案。
*   构建你自己的台式电脑：你可以购买主板、处理器、硬盘、显示器…… 组装硬件后，再安装 Linux。这是理解电脑组件的极佳体验。
*   与现有操作系统并行安装 Linux（也称为双启动）。如果你的电脑已经有另一个操作系统（例如 Microsoft Windows 或 MacOS），这是可能的。MacOS 和 Linux 都是“基于 UNIX 的”，但某些基础知识不同。在本书期间，某些编程工具在 Linux 中比 MacOS 更稳定。因此，即使你已经有了 MacOS，我也建议安装 Linux。双启动的优点是每个操作系统拥有整个电脑的资源。缺点是操作系统难以共享数据，因为一次只能使用操作系统。切换操作系统需要重启电脑。
*   双启动曾经比现在流行。现在我们可以访问高质量且廉价（免费）的虚拟机，它们得到了特殊硬件的支持。这是我的首选方案，因为方便且在行业中应用广泛。虚拟机是一个在内部运行操作系统的计算机程序。操作系统认为它直接运行在硬件上，但实际上它被嵌入在某种容器中。为了保护程序，你可以使用 github 来存储仓库。如果你在团队中工作或有几台电脑，在 commit 之后应该 `git pull` 以确保你有最新版本。

## B.3 添加文件和目录

你可以通过 `git add` 命令添加文件和目录。执行以下命令：

```bash
git add prog.c
git commit -m "add program" prog.c
git push
```

## B.4 修改程序

版本控制设计用于跟踪更改。尝试向 `prog.c` 添加两行，然后执行以下命令：

```bash
git commit -m "added lines" prog.c
git push
```

现在删除一些行并执行以下命令：

```bash
git commit -m "changed some lines" prog.c
git push
```

更改的历史可以在 github 上看到。如果添加了行，行前面会出现 `+` 符号。如果删除了一行，行前面会出现 `-` 符号。使用 `git`，你可以逐行跟踪更改。为了构建复杂的程序，有必要分步进行。专业程序员每次添加一个功能，确保其工作，并在添加另一个功能之前 commit 一个新版本。

