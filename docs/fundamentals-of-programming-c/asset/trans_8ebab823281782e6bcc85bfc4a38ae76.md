

## 18.1. 函数模板

```cpp
b = temp;
```

限制是参数必须是相同的类型。在这里，类型参数的名字是 EType。这个 swap 函数可以工作，但我们不需要自己写这样一个函数；C++ 标准库已经包含一个 `std::swap` 模板函数，它的功能与我们上面展示的 swap 函数相同。

下面的函数将打印任何任意类型 vector 的内容：

```cpp
/*
* print
* 打印 vector 的内容
* a 是要打印的 vector。
* a 不会被修改。
 */
template <typename T>
void print(const vector<T>& a) {
    int n = a.size();
    cout << '<';
    if (n > 0) {
        cout << a[0]; // 打印第一个元素
        for (int i = 1; i < n; i++)
            cout << ', ' << a[i]; // 打印其余元素
    }
    cout << '>';
}
```

这里的限制是 vector 中的元素必须能被 `cout <<` 对象打印。列表 18.3 (templateflexsort.cpp) 使用我们新的泛型函数，增加了列表 12.2 (flexibleisort.cpp) 中灵活排序程序的灵活性。

列表 18.3: templateflexsort.cpp

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <utility> // 用于通用 swap 函数

using less_than(a, b)

/*
* less_than(const T a)
* 如果 a < b 则返回 true；否则返回
* false。
 */
template <typename T>
bool less_than(const T a, const T b) {
    return a < b;
}

/*
* greater_than(a, b)
* 如果 a > b 则返回 true；否则返回
* false。
 */
template <typename T>
bool greater_than(const T& a, const T& b) {
    return a > b;
}
```

```cpp
/*
 * selection_sort(a, n, compare)
 * 将 vector vec 中的元素按照 compare 函数决定的
 * 顺序进行排列。
 * vec 是一个 vector。
 * compare 是一个比较两个支持 < 运算符的
 * 类型顺序的函数。
 * vec 的内容会被物理上重排。
 */
template <typename T>
void selection_sort(vector<T>& vec, int n, bool (*compare)(const T&, const T&)) {
    int n = vec.size();
    for (int i = 0; i < n - 1; i++) {
        // 注意：i 和 j 代表 vec 内部的索引。
        // vec[i], vec[j], 和 a[j] 代表这些
        // 位置上的元素
        // small 是我们目前为止见过的最小值的索引；
        // 我们用它来找到比 vec[i] 小的最小值
        int small = i;
        for (int j = i + 1; j < n; j++) {
            if (compare(vec[j], vec[small]))
                small = j; // 找到了一个更小的值
        }
        // 如果找到了更小的值，则交换 vec[i] 和 vec[small]
        if (i != small)
            swap(vec[i], vec[small]); // 使用 <utility> 中的 std::swap
    }
}
```

```cpp
/*
 * print
 * 打印 vector 的内容
 * vec 是要打印的 vector。
 * 函数不会修改 vec。
 */
template <typename T>
void print(const vector<T>& vec) {
    int n = vec.size();
    cout << '<';
    if (n > 0) {
        cout << vec[0]; // 打印第一个元素
        for (int i = 1; i < n; i++)
            cout << ', ' << vec[i]; // 打印其余元素
    }
    cout << '>';
}
```

int main() {
    vector<int> list{23, -3, 4, 215, 0, -3, 2, 100, 88, -10};
    cout << "Original: " << endl;
    print(list);
    cout << endl;
    selection_sort(list, less_than<int>);
    cout << "Ascending: " << endl;
    print(list);
    cout << endl;
    selection_sort(list, greater_than<int>);
    cout << "Descending: " << endl;
    print(list);
    cout << endl;
    cout << "--------------------------------------" << endl;
    vector<string> words { "tree", "girl", "boy", "apple", "dog", "cat", "bird" };
    cout << "Original: " << endl;
    print(words);
    cout << endl;
    selection_sort(words, less_than<string>);
    cout << "Ascending: " << endl;
    print(words);
    cout << endl;
    selection_sort(words, greater_than<string>);
    cout << "Descending: " << endl;
    print(words);
    cout << endl;
}
```

注意，main 函数之外的所有函数都是泛型函数。`selection_sort` 函数是最有趣的。它接受一个泛型函数和一个接收相同泛型参数的指针。在 main 的一次迭代中：

selection_sort(list, greater_than<int>);

表达式 `greater_than<int>` 是一个显式模板实例化，它告诉编译器我们要向 `selection_sort` 函数发送一个用整数实例化的 `greater_than` 指针。这种显式实例化是必要的，因为如果没有实际的函数调用，编译器无法自动实例化 `greater_than` 函数，而函数指针并不是函数调用。在程序的此点，我们并没有调用 `greater_than` 函数，只是传递了它的指针。调用它会通过实际参数为编译器提供必要的类型信息，但函数指针不包含参数信息。编译器需要 std 这种显式模板实例化的帮助：

swap 的调用实际上调用了标准库中的 `swap` 函数。`#include <utility>` 指令引入了 `std::swap` 的声明，它本身就是一个模板函数。

只有当用于模板参数的类型在函数内部支持操作时，编译器才能从模板函数实例化实际函数。考虑以下代码：

```cpp
// 创建两个 ofstream 对象
std::ofstream fout1("file1.data"), fout2("file2.data");
```

表达式 `less_than(fout1, fout2)` 是非法的，因为不存在比较两个 ostream 对象的运算符；当 a 和 b 是 ofstream 时，编译器不会产生表示表达式 `a < b` 的机器语言。最终，编译器无法实例化一个接受 ofstream 对象的 `less_than` 函数。

当程序员错误使用或构造了错误的模板函数或类时，编译器可以检测并报告这些问题。这是因为模板信息对程序员来说也很难以理解。

```cpp
// 比较它们 // <-- 错误！
if (less_than(fout1, fout2)) // <-- 错误！
    cout << "fout1 is less than fout2" << endl;
```

