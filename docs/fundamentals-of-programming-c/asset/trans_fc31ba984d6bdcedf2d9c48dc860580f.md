

## 12.1. 排序

} 

第 2 步中以“检查所有元素 A[j]，其中 j > i”头的指令也需要一个循环。
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

为了确定是否存在任何元素小于 A[i]，我们引入了一个名为 `small` 的新变量。`small` 的目的是跟踪目前为止找到的最小元素。我们最初将 `small` 设置为 `i`，因为我们想要找到小于位置 i 处元素的元素。

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

列表 12.1: sortintegers.cpp
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

## 12.2. 灵活排序

列表 12.1 (sortintegers.cpp) 使用了一种花哨打印程序，用逗号分隔 vector 的元素。程序的输出是：

```
Before: (23,-3,4,215,0,-3,2,23,100,88,-10)
After: (-10,-3,0,2,4,23,88,100,215)
```

我们不需要自己写一个函数来交换两个整数的值，如列表 12.1 (sortintegers.cpp) 所示的那样。C++ 标准库包含了 `std::swap`，它的工作方式与列表 12.1 (sortintegers.cpp) 中的 `swap` 函数完全相同；如果你想改变列表 12.1 中排序函数的行为，使其按降序而不是升序排列，呢？这实际上是一个简单的修改；只需将代码行 `if (a[j] < a[small])` 改为 `if (a[j] > a[small])` 即可。

下一个问题更有趣：我们如何通过传递一个排序函数作为参数来使我们的排序更加灵活？我们可以通过传递一个排序函数（参见第 12.9 节）来让排序更加灵活，按我们想要的任何方式对 vector 进行排序。

