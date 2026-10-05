

# 18.2. 类模板

### 列表 18.6: genericpoint.h
```cpp
#ifndef GENERICPOINT_H
#define GENERICPOINT_H_

template <typename T>
class Point {
public:
    T x;
    T y;
    Point(T x, T y) : x(x), y(y) {}
};

#endif
```

如果客户端声明一个 Point 对象为：
`Point<int> pixel(10, 10);`

编译器将实例化一个 `Point<int>` 类，看起来如下：

```cpp
class Point {
public:
    int x;
    int y;
    Point(int x, int y) : x(x), y(y) {}
};
```

如果客户端声明一个 Point 对象为：
`Point<float> pixel(10.0, 20.0);`

编译器将实例化一个 `Point<double>` 类，看起来如下：

```cpp
class Point {
public:
    double x;
    double y;
    Point(double x, double y) : x(x), y(y) {}
};
```

在任何源代码中，这两个实例化都不会出现，程序员是看不到它们的。编译器会用实际类型（`int` 或 `double`）替换参数化类型（`T`）。

为了一个重要的例子，列表 18.7（genericcompar.h）包含一个 `Comparator` 类的声明，该类是列表 17.18（compar.h）的泛型等效类。

### 列表 18.7: genericcompar.h
```cpp
#ifndef GENERICCOMPAR_H
#define GENERICCOMPAR_H_

/*
 * Comparator 对象管理选择排序函数中的
 * 比较和元素交换。
 * */

template <typename T>
class Comparator {
    // 对象的数据是私有的，因此客户端和
    // 派生类无法访问

    // 记录已执行的比较次数
    int compare_count;

    // 记录已执行的交换次数
    int swap_count;

    // 指向执行比较函数的函数指针
    bool (*comp)(const T&, const T&);

protected:
    // 实际执行比较的方法
    // 派生类可以自定义此方法
    virtual bool compare_impl(const T& m, const T& n) {
        return comp(m, n);
    }

    // 实际执行交换的方法
    // 派生类可以自定义此方法
    virtual void swap_impl(T& m, T& n) {
        T temp = m;
        m = n;
        n = temp;
    }

public:
    // 客户端必须使用合适的比较函数来
    // 初始化 Comparator 对象。
    Comparator(bool (*f)(const T&, const T&)),
        compare_count(0), swap_count(0), comp(f) {}

    // 重置计数器为新排序做好准备
    void reset() {
        swap_count = 0;
    }

    // 执行比较的方法。它将实际工作
    // 委托 comp 指向的函数。
    // 此方法记录每次调用。
    bool compare(const T& m, const T& n) {
        compare_count++;
        return compare_impl(m, n);
    }

    // 执行交换的方法。交换
    // 传递的 a 和 b 的值
    // 此方法记录每次调用。
    void swap(T& m, T& n) {
        swap_count++;
        swap_impl(m, n);
    }

    // 返回此对象自创建以来
    // 执行的比较次数。
    int comparisons() const {
        return compare_count;
    }

    // 返回此对象自创建以来
    // 执行的交换次数。
    int swaps() const {
        return swap_count;
    }
};
```

与列表 17.18（compar.h）一样，列表 18.7（genericcompar.h）中指定的 `Comparator` 对象可以比较任何类型，并设计用于 vector 或数组。以下代码片段引入了一个可以处理整数的 `Comparator` 模板类：

```cpp
bool less_than(int m, int n) {
    return m < n;
}
```

测试新 `Comparator` 类的客户端代码是列表 18.8（generisticsort.cpp）：

```cpp
#include <iostream>
#include <vector>
#include "genericcompar.h"

using namespace std;

/*
* selection_sort(a, compare)
* 根据 compare 对象确定的顺序
* 排列 vector a 中的元素。
* compare 是一个比较两个整数的函数。
* a 的内容被物理地重排。
*/
template <typename T>
void selection_sort(vector<T>& a, Comparator<T>& compare) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // 注意：i, small 和 j 代表位置，
        // 而 a[i], a[small], 和 a[j] 代表
        // 这些位置上的元素。small 是目前为止可见的最小
        // 值的位置，我们用它来找到比 a[i] 最小的；
        int small = i;
        // 查看在数组中是否可以找到更小的值
        for (int j = i + 1; j < n; j++) {
            if (compare(a[j], a[small])) {
                small = j;
            }
        }
        // 交换 a[i] 和 a[small]
        swap(a[i], a[small]);
    }
}
```

