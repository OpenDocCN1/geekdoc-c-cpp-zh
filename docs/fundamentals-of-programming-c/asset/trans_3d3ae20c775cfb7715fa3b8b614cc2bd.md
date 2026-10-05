

## 17.6. 细化继承关系

**DrawableRectangle::draw** 方法需要访问 **length** 和 **width** 字段才能绘制矩形。需要记住，每个 **DrawableRectangle** 对象都包含这些字段，因为它们是从 **Rectangle** 继承来的；然而，如果 **Rectangle** 中的 **length** 和 **width** 字段被声明为 `private` 而不是 `protected`，那么 **DrawableRectangle::draw** 将无法访问这些字段。

- 类对其成员支持三个级别的保护：
1. **private**: 这是默认设置。私有成员可以被类内部的任何代码访问，但对类外部的代码不可访问。
2. **protected**: 受保护成员可以被类内部的代码以及可以被使用公共继承的派生类内部的代码访问。受保护成员对其他（非派生）类不可见。
3. **public**: 公有成员可以被任何地方的代码访问。

总之，private 意味着类外不可访问，如此。public 意味着对所有人开放。protected 意味着对子类是“公共”的，而对所有其他类是“私有”的。

# 17.6 细化继承关系

回想列表 16.5 (loggingflexible.cpp) 中相当简单的排序代码。它使用对象来实现以下功能：

- 通过使用自定义比较函数，可以更改选择排序函数强制规定的顺序。
- 用于确定排序顺序的对象收集了排序函数执行的比较次数和元素交换次数的数据。

列表 17.20 (polymorphicsort.cpp) 列表 16.5 (loggingflexiblesort.cpp) 的轻微变体。除了将代码拆分为多个源文件外，它添加了两个虚方法，允许未来的开发者在派生类中自定义比较和交换方法。

列表 17.18 (comparator.h) 包含了 Comparator 类的声明。

```cpp
Listing17.18: comparator.h
#ifndef _COMPARATOR_H_
#define _COMPARATOR_H_
/*
 * Comparator 对象管理下方选择排序函数
 * 中的比较和元素
 * 交换。
 */
class Comparator {
    // 对象的数据是私有的，因此客户端和
    // 派生类无法访问

    // 跟踪已执行的比较次数
    int compare_count;

    // 跟踪已执行的交换次数
    int swap_count;

    // 指向执行比较的
    // 函数的指针
    bool (*comp)(int, int);

protected:
    // 实际执行比较的方法
    // 派生类可以自定义此方法
    virtual bool compare_impl(int m, int n);

    // 实际执行交换的方法
    // 派生类可以自定义此方法
    virtual void swap_impl(int m, int n);

public:
    // 客户端必须使用合适的比较函数
    // 初始化 Comparator 对象。
    Comparator(bool (*f)(int, int));

    // 重置计数器以为新排序做准备
    void reset();

    // 执行比较的方法。它将实际工作
    // 委托给由 comp 指向的函数。
    // 此方法记录每次调用。
    bool compare(int m, int n);

    // 执行交换的方法。交换通过引用传递的
    // 的参数 a 和 b 的值。
    // 此方法记录每次调用。
    void swap(int m, int n);

    // 返回该对象自创建以来
    // 执行的比较次数。
    int comparisons() const;

    // 返回该对象自创建以来
    // 执行的交换次数。
    int swaps() const;
};
#endif
```

列表 17.19: compar.cpp 提供了 Compar 方法的实现。

```cpp
Listing17.19: compar.cpp
#include "compar.h"

// 实际执行比较的方法
// 派生类可以自定义此方法
bool Compar::compare_impl(int m, int n) {
    return comp(m, n);
}

// 实际执行交换的方法
// 派生类可以自定义此方法
void Compar::swap_impl(int m, int n) {
    int temp = m;
    m = temp;
    n = temp;
}

// 客户端必须使用合适的比较函数
// 初始化 Compar 对象。
Compar::Comparator(bool (*xf)(int, int)) : compare_count(0), swap_count(0), comp(xf) {}

// 重置计数器以为新排序做准备
void Compar::reset() {
    compare_count = 0;
}

// 执行比较的方法。它将实际工作
// 委托给由 comp 指向的函数。
// 此方法记录每次调用。
bool Compar::compare(int m, int n) {
    compare_count++;
    return compare_impl(m, n);
}

// 执行交换的方法。交换通过引用传递的
// 的参数 a 和 b 的值。
// 此方法记录每次调用。
void Compar::swap(int m, int n) {
    swap_count++;
    swap_impl(m, n);
}
```

列表 17.20: polymorphic.cpp 提供了测试 Compar 类的客户端代码。

```cpp
#include <iostream>
#include <vector>
#include "compare.h"

using namespace std;

/*
 * selection_sort(a, compare)
* 根据比较对象对 vector a
 * 的元素进行排序。
 * a 是一个整型 vector。
 * compare 是一个比较两个整数
 * 顺序的函数。
 * a 的内容在物理上重排。
 */
void selection_sort(vector<int>& a, Comparer& compare) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // 注意：i, small, 和 j 代表 a 内部的位置
        // a[i], a[small], 和 a[j] 代表对应位置
        // 的元素。
        // small 是我们目前为止看到的最小值的
        // 位置；我们用它来找到比 a[i] 
        // 小的值。
        int small = i;
        // 查看在数组后面是否可以找到更小的值
        for (int j = i + 1; j < n; j++)
            if (compare.compare(a[j], a[small]))
                small = j; // 找到了更小的值
        // 如果找到了更小的值，则交换 a[i] 和 a[small]
        if (i != small)
            compare.swap(a[i], a[small]);
    }
}

/*
 * 打印整数 vector 的内容
 * a 是要打印的 vector。
 * a 不被修改。
 */
void print(const vector<int>& a) {
    int n = a.size();
    cout << '<';
    if (n > 0) {
        cout << a[0]; // 打印第一个元素
        for (int i = 1; i < n; i++)
            cout << ', ' << a[i];
    }
    cout << '>';
}

/*
 * less_than(a, b)
 * 如果 a < b 则返回 true；否则返回
 * false。
 */
bool less_than(int a, int b) {
    return a < b;
}

/*
 * greater_than(a, b)
 * 如果 a > b 则返回 true；否则返回
 * false。
 */
bool greater_than(int a, int b) {
    return a > b;
}

int main() {
    // 创建一个整数 vector
    vector<int> original { 23, -3, 4, 215, 0, -3, 22, 100, 88, -10 };

    // 创建原始 vector 的拷贝
    vector<int> working = original;
    cout << "Before: ";
    print(working);
    cout << endl;
    Comparer lt(less_than), gt(greater_than);
    selection_sort(working, lt);
}
```

列表 17.20 (polymorphic.cpp) 中的函数与列表 16.5 (flexible.sort) 是相同的，但并不一定，列表 17.20 (polymorphic.cpp) 的输出与列表 16.5 (flexible.sort) 相同。

| 之前 | 升序 |
| :--- | :--- |
| (23,3,4,215,0,-3,2,23,100,88,-10) | (-10,-3,0,2,4,23,88,100,215) (55 次比较, 7 次交换) |
| (23,3,4,215,0,-3,2,23,100,88,-10) | (215,100,88,23,4,2,0,-3,-10) (55 次比较, 5 次交换) |
| (23,3,4,215,0,-3,2,23,100,88,-10) | (215,100,88,23,4,2,0,-3,-10) (55 次比较, 0 次交换) |

问题问的是：新的 Comparer 类相比原始类有什么优势？
这个新 Comparer 类的设计很有趣：

- 由于其当前字段是私有的，因此只有 Comparer 类内部的方法可以访问 Comparer 对象的数据。
- 两个虚方法 compare_impl 和 swap_impl 是受保护的，因此学生无法直接访问它们。派生类可以看到它们并重写它们。后缀 _impl 代表

