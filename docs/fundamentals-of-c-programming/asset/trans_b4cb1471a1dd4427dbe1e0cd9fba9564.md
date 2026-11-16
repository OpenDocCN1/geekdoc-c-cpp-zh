

```cpp
class Point {
public:
    int x;
    int y;
    Point(int x, int y): x(x), y(y) {}
};
```

如果客户端改为声明一个 Point 对象，如下所示：

```cpp
Point<double> pixel(10.0, 20.0);
```

编译器将实例化一个 Point<double> 类，其外观如下：

```cpp
class Point {
public:
    double x;
    double y;
    Point(double x, double y): x(x), y(y) {}
};
```

这些实例化都不会出现在任何源代码中，因此程序员看不到它们。编译器会用实际类型（int 或 double）替换参数化类型（T）。

作为一个更重要的示例，清单 19.7（genericcomparer.h）包含 Comparer 类的声明，它是清单 17.33（comparer.h）的泛型等价物。

## 清单 19.7：genericcomparer.h

```cpp
#ifndef GENERICCOMPARER_H_
#define GENERICCOMPARER_H_
/*
 * Comparer objects manage the comparisons and element
 * interchanges on the selection sort function below.
 */
template <typename T>
class Comparer {
    // The object's data is private, so it is inaccessible to
    // clients and derived classes
    // Keeps track of the number of comparisons
    // performed
    int compare_count;
    // Keeps track of the number of swaps performed
    int swap_count;
    // Function pointer directed to the function to
    // perform the comparison
    bool (*comp)(const T&, const T&);
protected:
    // Method that actually performs the comparison
    // Derived classes may customize this method
    virtual bool compare_impl(const T& m, const T& n) {
        return comp(m, n);
    }
    // Method that actually performs the swap
    // Derived classes may customize this method
    virtual void swap_impl(T& m, T& n) {
        T temp = m;
        m = n;
        n = temp;
    }

public:
    // The client must initialize a Comparer object with a
    // suitable comparison function.
    Comparer(bool (*f)(const T&, const T&)):
        compare_count(0), swap_count(0), comp(f) {}

    // Resets the counters to make ready for a new sort
    void reset() {
        compare_count = swap_count = 0;
    }

    // Method that performs the comparison. It delegates
    // the actual work to the function pointed to by comp.
    // This method logs each invocation.
    bool compare(const T& m, const T& n) {
        compare_count++;
        return compare_impl(m, n);
    }

    // Method that performs the swap.
    // Interchange the values of
    // its parameters a and b which are
    // passed by reference.
    // This method logs each invocation.
    void swap(T& m, T& n) {
        swap_count++;
        swap_impl(m, n);
    }

    // Returns the number of comparisons this object has
    // performed since it was created.
    int comparisons() const {
        return compare_count;
    }

    // Returns the number of swaps this object has
    // performed since it was created.
    int swaps() const {
        return swap_count;
    }
};
#endif
```

与清单 17.33（comparer.h）一样，清单 19.7（genericcomparer.h）中指定的 Comparer 对象可以比较和交换任何类型的值，旨在用于向量或数组排序程序。给定函数

```cpp
bool less_than(int m, int n) {
    return m < n;
}
```

以下代码片段实例化了一个用于整数的 Comparer 模板：

```cpp
Comparer comp(less_than); // Make an integer comparer object
```

清单 19.8（genericstatisticssort.cpp）提供了测试新 Comparer 类的客户端代码。

## 清单 19.8：genericstatisticssort.cpp

```cpp
#include <iostream>
#include <vector>
#include <string>
#include "genericcomparer.h"

/*
 * selection_sort(a, compare)
 *
 * Arranges the elements of vector a in an order determined
 * by the compare object.
 * a is a vector.
 * compare is a function that compares the ordering of
 * two integers.
 *
 * The contents of a are physically rearranged.
 */
template <typename T>
void selection_sort(std::vector<T>& a, Comparer<T>& compare) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // Note: i, small, and j represent positions within a
        // a[i], a[small], and a[j] represents the elements at
        // those positions.
        //
        // small is the position of the smallest value we've seen
        // so far; we use it to find the smallest value less
        // than a[i]
        int small = i;
        // See if a smaller value can be found later in the array
        for (int j = i + 1; j < n; j++)
            if (compare.compare(a[j], a[small]))
                small = j; // Found a smaller value

        // Swap a[i] and a[small], if a smaller value was found
        if (i != small)
            compare.swap(a[i], a[small]);
    }
}

/*
 * Prints the contents of a vector
 *
 * a is the vector to print.
 * a is not modified.
 */
template <typename T>
std::ostream& operator<<(std::ostream& os, const std::vector<T>& a) {
    int n = a.size();
    os << '{';
    if (n > 0) {
        os << a[0]; // Print the first element
        for (int i = 1; i < n; i++)
            std::cout << ', ' << a[i]; // Print the rest
    }
    os << '}';
    return os;
}

/*
 * less_than(a, b)
 * Returns true if a < b; otherwise, returns
 * false.
 */
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}

/*
 * greater_than(a, b)
 * Returns true if a > b; otherwise, returns
 * false.
 */
template <typename T>
bool greater_than(const T& a, const T& b) {
    return a > b;
}

int main() {
    // Make a vector of integers
    std::vector<int> original { 23, -3, 4, 215, 0, -3, 2, 23, 100, 88, -10 };

    // Make a working copy of the original vector
    std::vector<int> working = original;
    std::cout << "Before: ";
    std::cout << working << '\n';
    Comparer<int> lt(less_than<int>), gt(greater_than<int>);
    selection_sort(working, lt);
    std::cout << "Ascending: ";
    std::cout << " (" << lt.comparisons() << " comparisons, "
              << lt.swaps() << " swaps)\n";
    // Make another copy of the original vector
    working = original;
    std::cout << "Before: ";
    std::cout << working << '\n';
    selection_sort(working, gt);
    std::cout << "Descending: ";
    std::cout << working << '\n';
    std::cout << " (" << gt.comparisons() << " comparisons, "
          << gt.swaps() << " swaps)\n";
    std::cout << "-----------------------------------\n";

    // Make a vector of strings
    std::vector<std::string> str_original { "tree", "boy", "apple",
                                            "girl", "dog", "cat" };

    // Make a working copy of the original vector
    std::vector<std::string> str_working = str_original;
    std::cout << "Before: ";
    std::cout << str_working << "\n";
    Comparer<std::string> str_lt(less_than<std::string>),
                          str_gt(greater_than<std::string>);
    selection_sort(str_working, str_lt);
    std::cout << "Ascending: ";
    std::cout << str_working << "\n";
    std::cout << " (" << str_lt.comparisons() << " comparisons, "
          << str_lt.swaps() << " swaps)\n";
    std::cout << "\n";

    // Make another copy of the original vector
    str_working = str_original;
    std::cout << "Before: ";
    std::cout << str_working << "\n";
    selection_sort(str_working, str_gt);
    std::cout << "Descending: ";
    std::cout << str_working << "\n";
    std::cout << " (" << str_gt.comparisons() << " comparisons, "
          << str_gt.swaps() << " swaps)\n";
    std::cout << "\n";
}
```

清单 19.8（genericstatisticssort.cpp）表明，泛型 Comparer 类对整数和字符串同样有效：

```
Before: {23,-3,4,215,0,-3,2,23,100,88,-10}
Ascending: {-10,-3,-3,0,2,4,23,23,88,100,215}
(55 comparisons, 7 swaps)
----------------------------------------
Before: {23,-3,4,215,0,-3,2,23,100,88,-10}
Descending: {215,100,88,23,23,4,2,0,-3,-3,-10}
(55 comparisons, 5 swaps)
----------------------------------------
Before: {tree,boy,apple,girl,dog,cat}
Ascending: {apple,boy,cat,dog,girl,tree}
(15 comparisons, 3 swaps)
----------------------------------------
Before: {tree,boy,apple,girl,dog,cat}
Descending: {tree,girl,dog,cat,boy,apple}
(15 comparisons, 4 swaps)
----------------------------------------
```

回顾清单 18.18（intlist5.h）和清单 18.19（intlist5.cpp）中的 IntList 链表类。它实现了一个整数元素的链表。假设我们改为想要创建一个 std::string 的链表

