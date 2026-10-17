
```cpp
    vector<int> vec(20);

    for (int i = 0; i < 20; i++)

        vec[i] = i;

    print(vec, 1);

    print(vec, 2);

    print(vec, 4);

    print(vec, 5);

    print(vec, 10);

    cout << endl;

    print_reverse(vec, 1);

    print_reverse(vec, 2);

    print_reverse(vec, 4);

    print_reverse(vec, 5);

    print_reverse(vec, 10);

}
```

列表 18.14 (`iteraterith.cpp`) 输出：

## 18.4 迭代器范围

| 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---||
| 0 | 2 | 4 | 6 | 8 | 10 | 12 | 14 | 16 | 18 | | | | | | | | | | | |
| 0 | 4 | 8 | 12 | 16 | | | | | | | | | | | | | | | | | |
| 0 | 5 | 10 | 15 | | | | | | | | | | | | | | | | | | |
| 0 | 10 | | | | | | | | | | | | | | | | | | | | |
| 19 | 18 | 17 | 16 | 15 | 14 | 13 | 12 | 11 | 10 | 9 | 8 | 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 | |
| 18 | 16 | 14 | 12 | 10 | 8 | 6 | 4 | 2 | 0 | | | | | | | | | | | |
| 16 | 12 | 8 | 4 | 0 | | | | | | | | | | | | | | | | | |
| 15 | 10 | 5 | | | | | | | | | | | | | | | | | | | |
| 10 | 0 | | | | | | | | | | | | | | | | | | |

C++ 标准库中的某些特殊数据结构支持特殊的迭代器，它们对支持的算术类型有一定的限制；例如，某些容器类型支持正向遍历而不支持后向遍历。对于这类迭代器，减法不是可选的。

迭代器对于指定序列（`vector` 和数组）的范围是有价值的。我们可以使用一对迭代器来指定一个范围：一个迭代器指向序列中的第一个元素，另一个迭代器指向序列结束之后的位置。全局函数 `begin` 和 `end` 很好地符合这种范围的定义。

假设 `vec` 是一个 `vector`。两个迭代器 `begin(vec)` 和 `end(vec)` 跨越了 `vec` 中值的完整范围。在以下语句中：

```cpp
auto b = begin(vec), e = b + 1;
```

迭代器 `b` 和 `e` 的范围包含了 `vec` 中的第一个元素。将此范围与以下语句表示的范围对比：

```cpp
auto b = begin(vec), e = b + 10;
```

在这里，迭代器 `b` 和 `e` 的范围跨越了 `vec` 的前 10 个元素。由语句定义的迭代器 `b` 和 `e` 的范围

```cpp
auto e = end(vec), b = e - 5;
```

涵盖了 `vec` 的最后五个元素。

迭代器对 `begin(vec), end(vec)` 指定了 `vector` `vec` 中值的完整范围。接接函数使用迭代器来计算某个值在内部出现的的次数：

```cpp
int count(vector<int>::iterator iter_begin,
            vector<int>::iterator iter_end, int seek) {
    int cnt = 0;
    for (vector<int>::iterator cursor = iter_begin;
         cursor != iter_end; ++cursor)
        if (cursor == seek)
            cnt++;
    return cnt;
}
```

## 18. 迭代器范围

第 11.2 节介绍了一种通过指针范围遍历数组的技术。这种基于范围的方法不是向遍历函数传递数组（字面上的，第一个元素的地址）和它的大小（元素数量），而是再次传递数组（字面上的，指向第一个元素的指针）和指向数组末尾之后位置的指针。注意基于范围的数组技术中的指针如何直接与 `begin` 和 `end` 函数返回的迭代器对象对应。由于迭代器的行为类似于指针，我们可以编写可以同时处理数组和 `vector` 的通用代码。

列表 18.15 (`genericloggingfixesort.cpp`) 使用模板函数和模板类来使我们的日志记录排序真正成为通用的。它还使用了继承来派生自模板类。

```cpp
Listing 18.15: genericloggingfixesort.cpp
#include <iostream>
#include <vector>
#include <cstdlib>
#include <fstream>
#include <string>
using namespace std;

/*
 * 比较器对象管理下方选择排序函数中的
 * 比较和元素交换。
 */
template <typename T>
class Compar {
    // 对象的数据是私有的，因此客户端
    // 和派生类无法访问
    // 跟踪已执行的
    // 比较次数
    int compare_count;
    // 跟踪交换的次数
    int swap_count;
    // 指向比较函数的指针
    bool (*comp)(const T&, const T&);
protected:
    // 实际执行比较
    // 派生类可以重写
    virtual bool compare_impl(const T& m, const T& n);
    // 实际执行交换
    // 派生类可以重写
    virtual void swap_impl(T& m, T& n);
public:
    // 客户端必须使用
    // 比较函数初始化 Compar
    Comparer(bool (*)(const T&, const T&));
    // 重置以准备新的排序
    void reset();
    // 执行比较，它将工作
    // 委托给指向的
    bool compare(const T& m, const T& n);
    // 执行交换，交换参数
    // a 和 b 的值，它们是按引用// 传递的
    void swap(T& m, T& n);
    // 返回对象创建以来
    // 执行的比较次数
    int comparisons() const;
    // 返回对象创建以来
    // 执行的交换次数
    int swaps() const;
};
```

```cpp
template <typename T>
bool Compar<T>::compare_impl(const T& m, const T& n) {
    return comp(m, n);
}
```

```cpp
template <typename T>
void Compar<T>::swap_impl(T& m, T& n) {
    T temp = m;
    m = n;
    n = temp;
}
```

```cpp
template <typename T>
Comparer<T>::Comparer(bool (*f)(const T&, const T&)) :
    compare_count(0), swap_count(0), comp(f) {}
```

```cpp
template <typename T>
void Compar<T>::reset() {
    compare_count = swap_count = 0;
}
```

```cpp
template <typename T>
bool Compar<T>::compare(const T& m, const T& n) {
    compare_count++;
    return compare_impl(m, n);
}
```

```cpp
template <typename T>
void Compar<T>::swap(T& m, T& n) {
    swap_count++;
    swap_impl(m, n);
}
```

```cpp
template <typename T>
int Compar<T>::comparisons() const {
    return compare_count;
}
```

```cpp
template <typename T>
int Compar<T>::swaps() const {
    return swap_count;
}
```

* `selection_sort(s, compare)`
* 根据比较对象确定的顺序排列序列元素。
* `begin` 指向序列的开始。
* `end` 指向序列最后一个元素之后的虚拟元素。
* `compare` 是一个用于比较两个元素顺序并
* 记录它所执行的操作的对象。
* 该函数物理上重新排列序列的内容。

```cpp
template<typename T, typename V>
void selection_sort(const T begin, const T end, Compar<V>& compare) {
    for (auto i = begin; i != end - 1; i++) {
        // 注意：i, small, 和 j 代表序列中的
        // 位置
        // a[i], a[small], 和 a[j] 代表对应位置的
        // 元素
```

## 18. 迭代器范围

```cpp
// small 是我们目前为止看到的最小值的位置
// 我们用它来寻找比 a[i] 小的最小值
auto small = i;
// 在序列中是否可以找到更小的值
for (auto j = i + 1; j != end; j++) {
    if (compare.compare(*j, *small))
        small = j; // 找到了更小的值
}
// 如果找到了更小的值，则交换 a[i] 和 a[small]
if (i != small)
    Compare.swap(i,small);
}
```

* `print`
* 序列的内容
* `begin` 指向序列的开始。
* `end` 指向最后一个元素之后的虚拟元素。
* 该函数不会修改序列。

```cpp
template <typename T>
void print(const T begin, const T end) {
    cout << '(';
    if (begin != end) {
        T iter = begin;
        cout << *iter; // 打印第一个元素
        iter++; // 移动到下一个元素
        while (iter != end) { // 打印剩余部分
            cout << ', ' << *iter;
            iter++; // 移动到下一个元素
        }
    }
    cout << ')';
}
```

* `less_than(a, b)`
* 如果 `a < b` 则返回 `true`；否则返回
* `false`。

```cpp
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}
```

* `greater_than(a, b)`
* 如果 `a > b` 则返回 `true`；否则返回
* `false`。

```cpp
template <typename T>
bool greater_than(const T& a, const T& b) {
    return a > b;
}
```

## 18.4. 迭代器范围 (ITERATOR RANGES)

```cpp
/*
 * Comparer 对象管理下方选择排序函数中的
 * 比较和元素交换。
 */
template<typename T>
class LogComparer : public Comparer<T> {
    // 日志消息的输出流
    std::ostream fout;
protected:
    // 实际执行比较的方法
    bool compare(const T& m, const T& n) override;
    // 实际执行交换的方法
    void swap_impl(const T& m, const T& n) override;
public:
    // 客户端必须使用合适的比较函数和文本文件名
    // 初始化 LogComparer 对象，该对象将日志消息重定向到该文件
    LogComparer(bool (*f)(const T&, const T&), const std::string& filename);
    // 析构函数必须关闭日志文件
    ~LogComparer();
    // 实际执行比较的方法
    // 生生类重写此方法
```

```cpp
template<typename T>
bool LogComparer<T>::compare(const T& m, const T& n) {
    fout << "Comparing " << m << " to " << n << std::endl;
    // 基类方法执行比较
    return Comparer<T>::compare_impl(m, n);
}
```

```cpp
template<typename T>
void LogComparer<T>::swap_impl(const T& m, const T& n) {
    fout << "Swapping " << m << " and " << n << std::endl;
    // temp = m;
    // n = temp;
    // 基类方法执行交换
    Comparer<T>::swap_impl(m, n);
}
```

```cpp
template<typename T>
LogComparer<T>::LogComparer(bool (*f)(const T&, const T&));
const string& filename): Comparer<T> (f) {
fout.open(filename);
if (!fout.good()) {
    fout.close();
    cout << "Could not open file " << filename
    cout << " for writing" << endl;
    exit(1); // 终止程序
}
}
```

```cpp
template<typename T>
LogComparator<T>::~LogComparator() {
    fout.close();
}
```

```cpp
int main() {
// 创建一个整数向量
vector<int> vec = {23, -3, 10, 4, 215, 0, -3, 2};
cout << "Before: "
print(begin(vec), end(vec));
cout << endl;
LogComparator<int> lt(less_than<int>, "upsort.log");
selection_sort(begin(vec), end(vec), lt);
cout << "Ascending: "
print(begin(vec), end(vec));
cout << endl;
cout << lt.comparisons << " " << comparisons << " "
cout << lt.swaps << " " << swaps << " " << endl;
LogComparator<int> gt(greater_than<int>, "downsort.log");
selection_sort(begin(vec), end(vec), gt);
cout << "Descending: "
print(begin(vec), end(vec));
cout << endl;
```
