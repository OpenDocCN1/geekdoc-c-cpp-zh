
## 练习

### 9
完成以下函数，将整数向量中的所有正值相加。例如，如果向量 `vec` 包含元素 `12, -3, 5, 2, -1`，那么 `sum_positive(vec)` 的求值为 `12, 3 + 5 + 2 = 12`。如果向量为空，该函数返回零。该函数不影响向量的内容。

```cpp
int sum_positive(const vector<int>& v) {
    // 添加你的代码...
}
```

### 10
完成以下函数，统计整数向量中的偶数。例如，如果向量 `vec` 包含元素 `3, 5, 2, -1, 2`，那么调用 `count_evens(vec)` 的求值为 `4`，因为 `vec` 中有两个 `2`（注：此处处 `vec + 2 = 2` 疑为原题笔误）。如果 `vec` 为空，该函数返回零。该函数不影响向量的内容。

```cpp
int count_evens(const vector<int>& v) {
    // 添加你的代码...
}
```

### 11
完成以下函数，统计二维整数向量中的偶数数量。

```cpp
int count_evens(const vector<vector<int>>& v) {
    // 添加你的代码...
}
```

### 12
完成以下函数，比较两个向量以检查它们是否按相同顺序相同元素。如果向量相等，函数返回 `true`；否则返回 `false`。例如，如果向量 `vec1` 包含元素 `3, 5, 2, -1, 2`，而向量 `vec2` 包含元素 `3, 5, 2, -1, 2`，调用 `equals(vec1, vec2)` 的求值为 `true`。如果此时 `vec2` 包含元素 `3, 2, 5, -1, 2`，则调用 `equals(vec1, vec2)` 的求值为 `false`（第二个和第三个元素不在相同顺序）。两个大小不同的向量不可能相等。该函数不影响内容。

```cpp
bool equals(const vector<int>& v1, const vector<int>& v2) {
    // 添加你的代码...
}
```

### 13
完成以下函数，确定第二个向量中的所有元素是否出现在第一个向量中。如果第二个向量中的所有元素都出现在第一个向量中，函数返回 `true`；否则返回 `false`。例如，如果 `vec1` 包含元素 `3, 5, 2, -1, 7`，而 `vec2` 包含元素 `5, 7, 2`，调用 `contains(vec1, vec2)` 的求值为 `true`。如果 `vec2` 包含元素 `3, 8, -1, 2`，则调用 `contains(vec1, vec2)` 的求值为 `false`（`5` 在 `vec2` 中出现两次但在 `vec1` 中仅出现一次）。该函数不影响向量。

```cpp
bool contains(const vector<int>& v1, const vector<int>& v2) {
    // 添加你的代码...
}
```

### 14
假设你的任务是实现以下原型函数：

```cpp
void proc(vector<int> v);
```

当你实现 `proc` 的函数体时，如何确定向量的大小？

### 15
考虑声明：

```cpp
vector<vector<int>> collection(100, vector<int>(200));
```

(a) 表达式 `collection[15]` 代表什么？

(b) `collection` 包含多少个元素？

(c) 编写 C++ 代码打印 `collection` 中的元素。同一行的所有元素应该出现在同一行中，每个后续的行应该出现在单独的一行。

(d) 表达式 `collection[15][2]` 代表什么？

### 16
考虑声明：

```cpp
vector<vector<vector<int>>> mesh(100, vector<int>(200, vector<int>(50)));
```

`mesh` 包含多少个元素？

### 17
C++ 数组与向量有何区别？

### 18
与数组相比，C++ 向量提供了哪些优势？

### 19
提供声明语句，声明并创建一个名为 `a` 的可以包含 20 个整数的静态数组。

### 20
提供声明语句，声明并创建一个可以包含 20 个整数的动态数组。

### 21
程序员在使用静态数组时需要注意哪些边界？

### 22
程序员在使用动态数组时需要注意哪些边界？

### 23
程序员在使用向量时需要注意哪些边界？

### 24
考虑以下处理范围的函数：

```cpp
bool proc(const int *begin, const int *end) {
  // 细节省略
}
```

以及如下定义的数组和向量：

```cpp
int a[10];
vector<int> v;
```

(a) 提供调用 `proc` 的数组语句。

(b) 提供调用 `proc` 的语句。

# 第 12 章：排序与搜索

第 11 章介绍了向量的制作和使用。在本章中，我们将探索对向量进行排序以及通过值而非索引定位元素的算法。

## 12.1 排序

我们将使用通用术语序列（sequence）来指代向量或数组。排序——将序列中的元素按特定顺序排列——是一种常见的活动。例如，整数序列可以按升序（即从小到大）排列或按字典序（通常称为字母顺序）排列。有很多排序算法，性能各不相同。我们将考虑一种相对容易实现的排序算法。

选择排序相对容易实现，对于较小的序列性能良好。如果 `A` 是一个序列，`i` 代表序列的索引，选择排序的工作如下：

1. 设置 `$i = 0$`。
2. 检查所有 `j > i` 的元素 `A[j]`。如果这些元素中有任何小于 `A[i]` 的，则将 `A[i]` 与其中的最小值交换。（这确保了位置 `i` 之后的所有元素大于或等于 `A[i]`）。
3. 如果 `i` 小于 `A` 的长度，将 `i` 加 1 并跳转第 2 步。

当第 3 步的条件不再满足时，算法终止。第 3 步中的“跳转第 2 步”代表一个循环。我们可以开始将描述翻译为 C++：

```cpp
// n 是 A 的长度
for (int i = 0; i < n - 1; i++) {
// 检查所有 j > i 的元素 A[j];
// 如果这些 A[j] 中有一个小于 A[i]，
// 则将 A[i] 与最小值交换。
}
```

第 2 步中以“检查所有元素 `A[j]`，其中 `j > i`”头的指令也需要一个循环。

通过以下代码继续完善实现：

```cpp
// n is A's length
for (int i = 0; i < n; i++) {
    for (int j = i + 1; j < n; j++) {
        // 检查所有元素
        // A[j], where j > i.
    }
}
```

```cpp
// 如果任何 A[j] 小于 A[i]，
// 则将 A[i] 与这些元素中最小的一个交换。
```

为了确定是否存在任何元素小于 `A[i]`，我们引入了一个名为 `small` 的新变量。`small` 的目的是跟踪目前为止找到的最小元素。我们最初将 `small` 设置为 `i`，因为我们想要找到小于位置 `i` 处元素的元素。

```cpp
// n is A's length
for (int i = 0; i < n - 1; i++) {
    // small 是我们目前为止看到的最小值的位置
    // 我们用它来找到小于 A[i] 的最小值
    int small = i;
    for (int j = i + 1; j < n; j++) {
        if (A[j] < A[i])
            small = j; // 找到了更小的元素，更新
    }
    // 如果 small 发生了变化，说明我们找到了小于 A[i] 的元素
    if (small != i)
        exchange A[i] and A[small];
}
```

列表 12.1:(sortintegers.cpp) 提供了 `selection_sort` 函数的完整 C++ 实现并对其进行了测试。

### 列表 12.1: sortintegers.cpp

```cpp
#include <iostream>
#include <vector>

using namespace std;

/*
 * swap(a, b) 交换参数 a 和 b 所引用的内存值。
 * 它实际上交换了调用者上下文中变量的值。
 */
void swap(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

Draft date: January 26, 2014

```cpp

/*

* selection_sort

* 将 vector 中的元素按升序排列。

* a 是一个包含整数的 vector。

*/

void selection_sort(vector<int>& a) {

    int n = a.size();

    for (int i = 0; i < n - 1; i++) {

        // 注意：i, small, 和 j 代表 a 中的位置

        // a[i], a[small], 和 a[j] 代表对应位置的元素

        int small = i;

        // 如果在 vector 后面可以找到更小的值，

        // 我们目前为止看到的；我们用它来找到小于 a[i] 的最小值

        for (int j = i + 1; j < n; j++) {

            if (a[j] < a[small])

                small = j; // 找到了更小的值

        }

        // 如果找到了更小的值，则交换 a[i] 和 a[small]

        if (i != small)

            swap(a[i], a[small]);

    }

}

```

```cpp

/*

* 打印整数 vector的内容。

* a 是要打印的 vector。

* a 不会被修改。

*/

void print(const vector<int>& a) {

    int n = a.size();

    cout << '<';

    if (n > 0) {

        cout << a[0]; // 打印第一个元素

        for (int i = 1; i < n; i++)

            cout << ', ' << a[i]; // 打印其余部分

    }

    cout << '>';

}

int main() {

    vector<int> list(23, -3, 4, 215, 0, -3, 2, 23, 100, 88, -10);

    cout << "Before: ";

    print(list);

    cout << endl;

    selection_sort(list);

    cout << "After: ";

    print(list);

    cout << endl;

}

```

## 12.2 灵活排序

列表 12.1 (sortintegers.cpp) 使用了一种花哨打印程序，用逗号分隔 vector 的元素。程序的输出是：

```
Before: (23,-3,4,215,0,-3,2,23,100,88,-10)
After: (-10,-3,0,2,4,23,88,100,215)
```

我们不需要自己写一个函数来交换两个整数的值，如列表 12.1 (sortintegers.cpp) 所示的那样。C++ 标准库包含了 `std::swap`，它的工作方式与列表 12.1 (sortintegers.cpp) 中的 `swap` 函数完全相同；如果你想改变列表 12.1 中排序函数的行为，使其按降序而不是升序排列，呢？这实际上是一个简单的修改；只需将代码行 `if (a[j] < a[small])` 改为 `if (a[j] > a[small])` 即可。

下一个问题更有趣：我们如何通过传递一个排序函数作为参数来使我们的排序更加灵活？我们可以通过传递一个排序函数（参见第 12.9 节）来让排序更加灵活，按我们想要的任何方式对 vector 进行排序。

## 12.3 搜索

### 列表 12.3: linearsearch.cpp

```cpp
#include <iostream>
#include <vector>
#include <cstdio>
#include <iomanip>
using namespace std;

/**
 * locate(a, seek)
 * 返回元素 seek 在 vector a 中的索引
 * 如果 seek 不在 a 中，则返回 -1
 * a 是需要搜索的 vector
 * seek 是要查找的元素。
 */
int locate(const vector<int>& a, int seek) {
    int n = a.size();
    for (int i = 0; i < n; i++) {
        if (a[i] == seek)
            return i; // 立即返回位置
    }
    return -1; // 未找到元素
}

/**
 * format(i)
 * 在 4 宽度的字段内右对齐打印整数
 * 如果 i > 9999，则打印 """""。
 */
void format(int i) {
    if (i > 9999)
        cout << """" << endl; // 太大了！
    else
        cout << setw(4) << i;
}

/**
 * print(v)
 * 打印 int vector 的内容
 * v 是要打印的 vector
 */
void print(const vector<int>& v) {
    for (int i : v) {
        format(i);
    }
}

/**
 * display(a, value)
 * 绘制一个 ASCII 箭头，显示
 * 给定的值在 vector 中
 * a 是 vector。
 * value 是要定位的元素。
 */
void display(const vector<int>& a, int value) {
    int position = locate(a, value);
    if (position >= 0) {
        print(a);    // 打印 vector 的内容
        cout << endl;
        position = 4+position + 7;    // 计算箭头的间距
        cout << setw(position);
        cout << "   " << endl;
        cout << setw(position);
        cout << " | " << endl;
        cout << setw(position);
        cout << " +-" << value << endl;
    } else {
        cout << value << " not in ";
        print(a);
        cout << endl;
    }
    cout << "======" << endl;
}

int main() {
    vector<int> list = { 100, 44, 2, 80, 5, 13, 11, 2, 110 };
    display(list, 13);
    display(list, 2);
    display(list, 7);
    display(list, 100);
    display(list, 110);
}
```

列表 12.3 (linearsearch.cpp) 的输出是

```
100 44 2 80 5 13 11 2 110
      |
      +-- 13
=======
100 44 2 80 5 13 11 2 110
      |
      +-- 2
=======
7 not in 100 44 2 80 5 13 11 2 110
=======
100 44 2 80 5 13 11 2 110
      |
      +-- 100
=======
100 44 2 80 5 13 11 2 110
      |
      +-- 110
=======
```
