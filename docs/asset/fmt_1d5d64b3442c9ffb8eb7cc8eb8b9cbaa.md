
反复从文件中读取数据到数组中，使用内部排序算法对数组进行排序，并将数据输出到临时文件。该过程如图 19.14 所示。理想情况下，你希望创建一个大数组，但数组的最大尺寸有限。假设最大数组大小为 100000 个 `int` 值。在临时文件中，每 10000 个 `int` 值进行一次排序。它们被标记为 $S_1, S_2, \dots,$ 和 $S_k$，其中最后一段 $S_k$ 可能包含少于 100000 个值。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_634_0.png)

图 19.14 原文件分段排序。

## 第二阶段

将每对已排序的段（例如 $S_1$ 与 $S_2$，$S_3$ 与 $S_4, \dots$ 等）合并成一个更大的排序段，并将新段保存到新的临时文件中。继续相同的过程，直到产生一个排序后的段。图 19.15 显示了如何合并八段。

![](img/3b8bc24ba08ad32ac1a370eb095746a9_634_1.png)

图 19.15 迭代合并已排序段。

（注：不需要合并两个相邻的段。例如，在第一个合并步骤中，你可以将 $S_1$ 与 $S_5$，$S_2$ 与 $S_6$，$S_3$ 与 $S_7$，$S_4$ 与 $S_8$ 合并。这一观察对于高效实现第二阶段很有用。）

## 19.7.1 实现第一阶段

列出文件中的每一段数据，对该段进行排序，并将排序后的段存入新文件。该函数返回段的数量。

### 列表 19.13 创建初始排序段

```cpp
/* 将原始文件排序为排序段 */
int initializeSegments(int segmentSize, char* originalFile, char* f1)
{
    int *list = new int[segmentSize];
    fstream input;
    input.open(originalFile, ios::in | ios::binary);
    fstream output;
    output.open(f1, ios::out | ios::binary);
    int numberOfSegments = 0;
    while (!input.eof()) {
        int i = 0;
        for ( !input.eof() && i < segmentSize; i++) {
            input.read(reinterpret_cast<char *>(&list[i]), sizeof(list[i]));
        }
        if (input.eof() || i <= 0)
            break;
        else
            numberOfSegments++;
    }
    // 对数组 list[0..i-1] 排序
    quickSort(list, i);
    // 将数组写入 f1.dat
    for (int j = 0; j < i; j++) {
        output.write(reinterpret_cast<char *>(&list[j]), sizeof(list[j]));
    }
    input.close();
    delete[] list;
    return numberOfSegments;
}
```

## 19.7.2 实现第二阶段

在第二阶段中，将每对已排序段合并成更大的排序段，并将新段保存到新的临时文件中。重复相同的过程，直到产生一个排序后的段。每合并一次，段的数量会减半。

# 19.7 外部排序

剩余 `f2` 分段

```cpp
while (!f2.eof() && f2Count < segmentSize)
{
    int value;
    f2.read(reinterpret_cast<char *>
        (&value), sizeof(value));
    if (f2.eof()) break;
    f3.write(reinterpret_cast<char *>
        (&value), sizeof(value));
}
```

## 19.7.3 合并两个阶段

列表 19.17 给出了排序 `largedata.dat` 中的 `int` 值并将排序后的数据存储在 `sortedlargata.dat` 中的完整程序。

### 列表 19.17 SortLargeFile.cpp

```cpp
#include <iostream>
#include <fstream>
#include "QuickSort.h"
using namespace std;

// 函数原型
int initializeSegments(int segmentSize,
    char* originalFile, char* f1);
void mergeSegments(int segmentSize, fstream& f1, fstream& f2,
    fstream& f3);
void merge(int numberOfSegments, int segmentSize,
    char* f1, char* f2, char* f3);
void copyHalfTo2(int numberOfSegments, int segmentSize,
    fstream& f1, fstream& f2);
void mergeSegments(int numberOfSegments, int segmentSize,
    char* f1, char* f2, char* f3);
void mergeSegments(int numberOfSegments, int segmentSize,
    fstream& f1, fstream& f2, fstream& f3);
void copyFile(char* f1, char* target);

int main() {
    const int MAX_ARRAY_SIZE = 100000;

    // 实现阶段 1：创建初始分段
    int numberOfSegments =
    initializeSegments(MAX_ARRAY_SIZE, "largedata.dat", "f1.dat");

    // 实现阶段 2：递归合并分段
    merge(numberOfSegments, MAX_ARRAY_SIZE,
        "f1.dat", "f2.dat", "f3.dat");

    /* 将原始文件排序到排序后的分段 */
    initializeSegments(int segmentSize, char* originalFile, char* f1);

    // 与列表 19.13 相同，此处省略
}

/* 递归合并排序后的分段 */
void merge(int numberOfSegments, int segmentSize,
    char* f1, char* f2, char* f3)
{
    if (numberSegments > 1)
    {
        mergeStep(numberSegments, segmentSize, f1, f2, f3);
        merge((numberSegments + 1) / 2, segmentSize * 2, f3, f1, f2);
    }
    else
    {
        // 将 f1 重命名为最终排序后的文件
        copyFile(f1, "sortedlarged.dat");
        cout << "\nsorted into the file sortedlarged.dat" << endl;
    }
}
// 从 f1 复制文件到 target */
void copyFile(char* f1, char* target)
{
    fstream fInput;
    fInput.open(f1, ios::in | ios::binary);
    fstream fOutput;
    fOutput.open(target, ios::out | ios::binary);
    while (!fInput.eof()) // 继续直到文件末尾
    {
        int value;
        fInput.read(reinterpret_cast<char*>(&value), sizeof(value));
        if (fInput.eof()) break;
        fOutput.write(reinterpret_cast<char*>(&value), sizeof(value));
    }
    fInput.close();
    fOutput.close();
}
 /* 合并两个分段 */
void mergeStep(int numberOfSegments, int segmentSize, char* f1, char* f2, char* f3)
{
    fstream fInput;
    fInput.open(f1, ios::in | ios::binary);
    fstream fOutput;
    fOutput.open(f2, ios::out | ios::binary);
    // 从 f1.dat 复制一半数量的分段到 f2.dat
    copyHalfToF2(numberOfSegments, segmentSize, fInput, f2Output);
    f2Output.close();
// 将 f1 中的分段与 f2 中的分段合并到 f3
    fstream fInput;
    fInput.open(f2, ios::in | ios::binary);
    fstream fOutput;
    fOutput.open(f3, ios::out | ios::binary);
    mergeSegments(numberOfSegments / 2, segmentSize,
    fInput, f2Input, f3Output);
    fInput.close();
    f2Input.close();
    f3Output.close();
}
// 从 f1.dat 复制一半数量的分段到 f2.dat /
void copyHalfToF2(int numberOfSegments, int segmentSize,
    fstream&f1, fstream&f2);
// 与列表 19.14 相同，此处省略
}
// 合并所有分段 /
void mergeSegments(int numberOfSegments, int segmentSize, fstream& f1, fstream& f2, fstream& f3);
// 与列表 19.15 相同，此处省略
}
// 合并两个分段 /
void mergeTwoSegments(int segmentSize, fstream& f1, fstream& f2, fstream& f3);
// 与列表 19.16 相同，此处省略
}
```

假设 `MAX_ARRAY_SIZE` 为 100000（第 23 行），这也就是初始的分段大小。第 27 行从原始文件创建初始分段，并将排序后的分段存储在新文件 `f1.dat` 中，在 `sorted.dat` 中生成一个排序后的文件。`merge` 函数

```cpp
merge(int numberOfSegments, int segmentSize, char *f1, char *f2, char *f3);
```

将 `f1` 中的分段合并到 `f3`，并使用 `f2` 辅助合并。`merge` 函数通过多次递归调用执行许多合并步骤。每次合并使 `numberOfSegments` 减少一半并使分段大小翻倍。在完成一个合并步骤后，下一个合并步骤将 `f3` 中的新分段合并到 `f2`，使用 `f1` 辅助合并。调用 `merge` 函数的语句是（第 18 行）：

```cpp
merge((numberOfSegments + 1) / 2, segmentSize * 2, f3, f1, f2);
```

下一个合并步骤的 `numberOfSegments` 为 `(numberOfSegments + 1) / 2`。例如，如果 `numberOfSegments` 为 5，则下一个合并步骤的 `numberOfSegments` 为 `(5+1)/2 = 3`。

## 19.7.4 外部排序

假设 `MAX_ARRAY_SIZE` 为 100000（第 23 行），这也就是初始的分段大小。第 27 行从原始文件创建初始分段，并将排序后的分段存储在新文件 `f1.dat` 中，在 `sorted.dat` 中生成一个排序后的文件。`merge` 函数

```cpp
merge(int numberOfSegments, int segmentSize, char *f1, char *f2, char *f3);
```

将 `f1` 中的分段合并到 `f3`，并使用 `f2` 辅助合并。`merge` 函数通过多次递归调用执行许多合并步骤。每次合并使 `numberOfSegments` 减少一半并使分段大小翻倍。完成一个合并步骤后，下一个合并步骤将 `f3` 中的新分段合并到 `f2`，使用 `f1` 辅助合并。调用 `merge` 函数的语句是（第 18 行）：

```cpp
merge((numberOfSegments + 1) / 2, segmentSize * 2, f3, f1, f2);
```

下一个合并步骤的 `numberOfSegments` 为 `(numberOfSegments + 1) / 2`。例如，如果 `numberOfSegments` 为 5，则下一个合并步骤的 `numberOfSegments` 为 `(5+1)/2 = 3`。

（注：原文文本中部分段存在逻辑乱码或重复，已按要求尽量翻译）

## 术语

| 术语 | 页 |
|---|---|
| 冒泡排序 (Bubble Sort) | 592 |
| 合并排序 (Merge Sort) | 594 |
| 桶排序 (Bucket Sort) | 602 |
| 堆排序 (Heap Sort) | 608 |

## 总结

1. 冒泡排序、插入排序、快速排序的最坏时间复杂度为 $O(n^2)$。
2. 合并排序和快速排序的平均时间复杂度以及最坏情况的时间复杂度为 $O(n \log n)$。
3. 堆排序（Heap Sort）的平均复杂度为 $O(n \log n)$。
4. 堆是用于设计高效队列的有效结构。
5. 堆（Heap）具有以下性质：(1) 它是一个完全二叉树；(2) 每个节点都大于其子节点。
6. 桶排序可以应用于文件。

## 习题

### 19.2–19.4

- 19.1 使用图 19.1 作为示例展示如何应用冒泡排序 {45, 11, 50, 59, 60, 2}。
- 19.2 使用图 19.2 作为示例展示如何应用合并排序 {45, 11, 50, 59, 60, 2}。
- 19.3 使用图 19.4 作为示例展示如何应用快速排序 {45, 11, 50, 59, 60, 2}。

### 19.5

- 19.4 什么是完全二叉树？什么是堆？描述如何从堆中删除根并向堆中添加新对象。
- 19.5 如果堆为空，调用删除函数的返回值是什么？
- 19.6 按此顺序将 4, 5, 1, 2, 9, 3 加入堆。画出每个元素添加后的堆图。
- 19.7 显示移除图 19.12(c) 中的堆根。

### 19.6–19.7

- 19.8 展示如何应用桶排序 {232, 353, 344, 20, 35, 326, 377, 679, 681, 3}。
- 19.9 有十个数字 {2, 3, 4, 0, 5, 6, 7, 9, 8, 1} 存储在外部文件 `large-data.dat` 中。用 `MAX_ARRAY_SIZE` 手动跟踪 `SortLargeFile` 程序。

# 第19章 排序

19.8（排序的执行时间）编写一个程序，获取选择排序、插入排序、冒泡排序、合并排序、快速排序和堆排序在输入规模为 500,000、1,000,000、1,500,000、2,000,000、2,500,000 和 3,000,000 时的执行时间。你的程序应该打印如下表所示：

| 数组大小 | 选择排序 | 插入排序 | 冒泡排序 | 合并排序 | 快速排序 | 堆排序 |
| --- | --- | --- | --- | --- | --- | --- |
| 500000 | | | | | | |
| 1000000 | | | | | | |
| 1500000 | | | | | | |
| 2000000 | | | | | | |
| 2500000 | | | | | | |
| 3000000 | | | | | | |

（提示：你可以使用以下代码模板来获取执行时间。）

```cpp
long startTime = time(0);

perform the task;

long endTime = time(0);

long executionTime = endTime - startTime;
```
