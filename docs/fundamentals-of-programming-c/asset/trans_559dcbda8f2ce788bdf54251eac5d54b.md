

## F.7. C字符串

```cpp
using namespace std;
bool find_char(const char *s, char ch) {
    while (*s != '\0') { // 扫描直到遇到空字符
        if (*s == ch) // 找到匹配字符
            return true;
        }
        s++; // 移动到字符串中的下一个位置
    }
    return false; // 未找到
}

int main() {
    const char *phrase = "this is a phrase";
    // 尝试所有 a 到 z 的字符
    for (char ch = 'a'; ch <= 'z'; ch++) {
        cout << '\' << ch << '\' << " is ";
        if (!find_char(phrase, ch))
            cout << " NOT ";
    }
    cout << "in " << '\' << phrase << '\' << endl;
}
return 0;
```

列表 F.9 (findchar.cpp) 的输出如下：

```
'a' is in "this is a phrase"
'b' is NOT in "this is a phrase"
'c' is NOT in "this is a phrase"
'd' is NOT in "this is a phrase"
'e' is in "this is a phrase"
'f' is NOT in "this is a phrase"
'g' is NOT in "this is a phrase"
'h' is in "this is a phrase"
'i' is in "this is a phrase"
'j' is NOT in "this is a phrase"
'k' is NOT in "this is a phrase"
'l' is NOT in "this is a phrase"
'm' is NOT in "this is a phrase"
'n' is NOT in "this is a phrase"
'o' is in "this is a phrase"
'p' is NOT in "this is a phrase"
'q' is NOT in "this is a phrase"
'r' is in "this is a phrase"
's' is in "this is a phrase"
't' is in "this is a phrase"
'u' is NOT in "this is a phrase"
'v' is NOT in "this is a phrase"
'w' is NOT in "this is a phrase"
'x' is NOT in "this is a phrase"
'y' is in "this is a phrase"
'z' is NOT in "this is a phrase"
```

列表 F.9 (findchar.cpp) 中的 **find_char** 函数使用指针符号来遍历字符串。它不需要知道字符串中的字符数，因为它从开始处逐个扫描每个字符，直到找到它或遇到空终止字符。

回想第 5.1 节，对于布尔表达式，C++ 将零值视为 false，将任何非零值视为 true。由于对布尔表达式有这种宽松的解释，上面的 **find_char** 函数可以写得更紧凑：

```cpp
char find(const char *cs, char ch) {
    // 扫描直到遇到空字符或我们寻找的字符
    while (*cs != '\0' && *cs != ch) {
        cs++; // 移动到字符串中的下一个位置
    }
    return *cs; // 空字符 = false，其他任何值 true
}
```

退出循环的唯一方法是扫描空终止字符或寻求的字符。在这里，如果循环遇到空终止字符，它将退出并返回空字符。空字符仅仅是 ASCII 零——布尔 false。如果循环定位了寻求的字符，它将退出并返回该字符，该字符不是 ASCII 零。除空字符以外的任何字符其 ASCII 值大于零；布尔 true。

## F.8. 动态数组

大多数处理字符串的程序都依赖字符串的空终止才能正常工作。一些标准 C 字符串函数包括：

- int strlen(const char *s) 返回 s 中字符的数量，不包括空终止符。
- char *strcpy(char *s, const char *t) 将字符串 t 的内容拷贝到字符串 s 并包括空终止符；
- char *strncpy(char *s, const char *t, unsigned n) 通过拷贝 n 个字符工作；s 指向至少容纳 n 个字符的缓冲区。
- int strcmp(const char *s, const char *t) 比较两个字符串的字典顺序。如果 s 在字典上于 t 之前，函数返回小于零的整数；如果 s 在 t 之后，函数返回大于零的整数。

以下代码片段：

```cpp
cout << strcmp("ABC", "XYZ") << endl;
cout << strcmp("XYZ", "ABC") << endl;
cout << strcmp("ABC", "ABC") << endl;
```

打印：

![](img/e326304bd50f4d7a56417eb635140.png)

- int strncmp(const char *s, const char *t, int n) 比较两个字符串的前 n 个字符的字典顺序。如果 s 的前 n 个字符在 t 的前 n 个字符之前，函数返回小于零的整数；如果 s 在 t 之后，函数返回大于零的整数。如果两个字符串的前 n 个字符相同，函数返回零。

你应该小心使用 C 字符串，因为 C++ 库经常使用 C 字符串。然而，大多数情况下，你应该使用 string 对象（见第 13.1）。

## F.8 动态数组

在本章目前检查的所有程序中，数组的大小是在编译时确定的。程序员可以在源代码中更改数组的大小，但必须重新编译。我们希望有一个灵活且能够处理用户需要的任何数量条目的程序。

实现灵活大小数组的一种方法是定义容纳概念上需要的所有项目的数组。F.10 (largearray.cpp) 使用了这种方法。

## F.8. 动态数组

列表 F10: largearray.cpp

```cpp
#include <iostream>

using namespace std;

// 预期的最大值为 1,000,000
const int MAX_NUMBER_OF_ENTRIES = 1000000;
double numbers[MAX_NUMBER_OF_ENTRIES];

int main() {
    double sum = 0.0;
    int size; // 实际条目

    // 获取数组的有效大小
    cout << "Please enter number of values to process: ";
    cin >> size;

    if (size > 0) { // 没有条目时不
        cout << "Please enter " << size << " numbers: ";
        // 允许用户输入值
        for (int i = 0; i < size; i++) {
            cin >> numbers[i];
            sum += numbers[i];
        }

        cout << "The average of ";
        for (int i = 0; i < size; i++) {
            cout << numbers[i] << " ";
        }
        // 元素后没有逗号
        cout << numbers[size - 1] << " is " << sum / size << endl;
    }

    return 0;
}
```

虽然 F10 (largearray.cpp) 的方法可行，但它浪费了内存。在现代计算中，用户可能同时打开多个程序。栈的大小只有一兆，可能没有足够的内存（RAM），计算机将被使用更多的虚拟内存（磁盘上）。虚拟内存访问会极大降低程序的速度，因此用户体验会受到。每个程序明智地使用资源非常重要。幸运的是，程序员可以创建一个精确大小的数组，即使该大小直到运行时才知道。列表 F11 (flexiblearrayaverage.cpp) 展示了如何做。

列表 F11: flexiblearrayaverage.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    double sum = 0.0;
    double *numbers; // 注意：numbers 是指针，不是数组
    int size; // 实际条目

    // 获取数组的有效大小
    cout << "Please enter number of values to process: ";
    cin >> size;

    if (size > 0) { // 没有条目时不
        cout << "Please enter " << size << " numbers: ";
        // 分配所需的精确大小
        numbers = new double[size]; // 动态分配数组
        // 允许用户输入值
        for (int i = 0; i < size; i++) {
            cin >> numbers[i];
            sum += numbers[i];
        }

        cout << "The average of ";
        for (int i = 0; i < size; i++) {
            cout << numbers[i] << " ";
        }
        // 元素后没有逗号
        cout << numbers[size - 1] << " is " << sum / size << endl;
        delete [] numbers; // 释放 numbers 占据的空间
    }
}
```

注意 numbers 没有声明为数组；它是一个指针：

double *numbers; // 注意：numbers 是指针，不是数组

该语句为单个指针分配空间，在 32 位系统上仅为 4 字节，在 64 位系统上为 8 字节。表达式

```
new double[size]
```

在运行时分配一个内存块，用于容纳恰好 size 个双精度浮点数元素的数组。该表达式的值是新分配内存块的起始地址。

