
```cpp
/*
 * print
 *
 * Prints the contents of a vector
 *  a is the vector to print.
 *  a is not modified.
 */
template <typename T>
void print(const std::vector<T>& a) {
    int n = a.size();
    std::cout << '{';
    if (n > 0) {
        std::cout << a[0]; // Print the first element
        for (int i = 1; i < n; i++)
            std::cout << ',' << a[i]; // Print the rest
    }
    std::cout << '}';
}
```

这里的限制是，向量中的元素必须能够使用 `<<` 打印到 `std::cout` 对象。

清单 19.3（templateflexsort.cpp）使用我们的新泛型函数，提高了我们来自清单 12.2（flexibleinsertion.cpp）的灵活排序程序的灵活性。

### 清单 19.3: templateflexsort.cpp

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <utility> // For generic swap function

/*
 * less_than(a, b)
 *
 * Returns true if a < b; otherwise, returns
 * false.
 */
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}

/*
 * greater_than(a, b)
 *
 * Returns true if a > b; otherwise, returns
 * false.
 */
template <typename T>
bool greater_than(const T& a, const T& b) {
    return a > b;
}

/*
 * selection_sort(a, n, compare)
 *
 * Arranges the elements of vector vec in an order determined
 * by the compare function.
 *
 * vec is a vector.
 *
 * compare is a function that compares the ordering of
 * two types that support the < operator.
 * The contents of vec are physically rearranged.
 */
template <typename T>
void selection_sort(std::vector<T>& vec,
                    bool (*compare)(const T&, const T&)) {
    int n = vec.size();
    for (int i = 0; i < n - 1; i++) {
        // Note: i, small, and j represent positions within vec.
        // vec[i], vec[small], and a[j] represents the elements at
        // those positions.
        // small is the position of the smallest value we've seen
        // so far; we use it to find the smallest value less
        // than vec[i]
        int small = i;
        // See if a smaller value can be found later in the vector
        for (int j = i + 1; j < n; j++)
            if (compare(vec[j], vec[small]))
                small = j; // Found a smaller value
        // Swap vec[i] and vec[small], if a smaller value was found
        if (i != small)
            std::swap(vec[i], vec[small]); // Uses swap from <utility>
    }
}

/*
 * print
 *
 * Prints the contents of a vector
 * vec is the vector to print.
 * The function does not modify vec.
 */
template <typename T>
void print(const std::vector<T>& vec) {
    int n = vec.size();
    std::cout << '{';
    if (n > 0) {
        std::cout << vec[0]; // Print the first element
        for (int i = 1; i < n; i++)
            std::cout << ', ' << vec[i]; // Print the rest
    }
    std::cout << '}';
}

int main() {
    std::vector<int> list{23, -3, 4, 215, 0, -3, 2, 23, 100, 88, -10};
    std::cout << "Original: ";
    print(list);
    std::cout << "\n";
    selection_sort(list, less_than<int>);
    std::cout << "\nAscending: ";
    print(list);
    std::cout << '\n';
    selection_sort(list, greater_than<int>);
    std::cout << "Descending: ";
    print(list);
    std::cout << '\n';
    std::cout << "-----------------------------------\n";
    std::vector<std::string> words { "tree", "girl", "boy", "apple",
                                     "dog", "cat", "bird" };
    std::cout << "Original: ";
    print(words);
    std::cout << '\n';
    selection_sort(words, less_than<std::string>);
    std::cout << "Ascending: ";
    print(words);
    std::cout << '\n';
    selection_sort(words, greater_than<std::string>);
    std::cout << "Descending: ";
    print(words);
    std::cout << '\n';
}
```

注意，除了 main 之外的所有函数都是泛型函数。selection_sort 函数是最有趣的一个。它接受一个泛型向量和一个函数指针，该函数指针接受两个相同类型的泛型参数。在 main 中的一次调用中：

```
selection_sort(list, greater_than<int>);
```

表达式 greater_than<int> 是一个显式模板实例化，它告诉编译器我们希望向 selection_sort 函数传递一个指向使用整数参数实例化的 greater_than 函数的指针。需要这种显式实例化，因为编译器无法在没有实际调用函数并传递真实参数的情况下自动实例化 greater_than 函数，而函数指针并不是函数调用。在程序的这一点上，我们并不是在调用 greater_than 函数，而只是传递一个指向它的指针。调用它将通过实际使用的参数向编译器提供必要的类型信息，但函数指针不包含参数信息。编译器需要这种显式模板实例化的帮助。

selection_sort 中对 swap 的调用实际上是在调用标准库中的 std::swap 函数。#include <utility> 指令引入了 std::swap 的声明，而 std::swap 本身也是一个模板函数。

编译器只有在替换模板参数的类型支持在函数中使用时，才能从模板函数实例化一个实际函数。考虑以下代码：

```
// Make two ofstream objects
std::ofstream fout1("file1.data"), fout2("file2.data");
// Compare them
if (less_than(fout1, fout2)) // <-- Error!
    std::cout << "fout1 is less than fout2\n";
```

表达式 less_than(fout1, fout2) 是非法的，因为不存在用于比较两个 std::ofstream 对象的 operator<；因此，编译器无法生成表示表达式 a < b 的机器语言，当 a 和 b 是 std::ofstream 时。最终，因此，编译器无法实例化接受两个 std::ofstream 对象的实际 less_than 函数。

当程序员错误地使用模板或构建错误的模板函数或类时，编译器可以检测并报告问题。所有当前的 C++ 编译器在模板处理方面都共享一个弱点：缺乏人类可读的错误信息。在这些情况下，编译器生成的错误信息往往冗长且难以解读，即使对于经验丰富的 C++ 程序员也是如此。这是因为编译器基于其对实例化代码的处理（而非原始未实例化源代码）来生成错误信息。由于程序员只能看到未实例化的源代码，因此解读编译器的模板错误信息通常比平时更具挑战性。

如清单 19.4（templatescale.cpp）所示，模板可以接受非类型参数。

### 清单 19.4: templatescale.cpp

```cpp
#include <iostream>

template <int N>
int scale(int value) {
    return value * N;
}

int main() {
    std::cout << scale<3>(5) << '\n';
    std::cout << scale<4>(10) << '\n';
}
```

请注意，在清单 19.4（templatescale.cpp）中，typename 关键字缺失，取而代之的是实际类型 int。这意味着参数 N 是一个非类型模板参数。程序输出：

```
15
40
```

清单 19.5（templatescale2.cpp）同时使用了类型参数和非类型参数。

### 清单 19.5: templatescale2.cpp

```cpp
#include <iostream>

template <typename T, int N>
T scale(const T& value) {
    return value * N;
}

int main() {
    std::cout << scale<double, 3>(5.3) << '\n';
    std::cout << scale<int, 4>(10) << '\n';
}
```

清单 19.5（templatescale2.cpp）在执行期间显示以下内容：

```
15.9
40
```

编译器将实例化两个 scale 函数：

```cpp
// Instantiated by the compiler due to scale<double, 3>:
double scale(const double& value) {
    return value * 3;
}
```

and

```cpp
// Instantiated by the compiler due to scale<int, 4>:
int scale(const int& value) {
    return value * 4;
}
```

C++ 允许的非类型模板参数类型非常有限。整数类型（int、unsigned、long 等）是可接受的，指针和引用也是如此。其他类型（如浮点类型和程序员定义的类型）可能不能作为非类型模板参数。

C++ 标准库包含许多泛型函数，我们已经见过其中一些：

- std::max—计算两个值的最大值
- std::min—计算两个值的最小值
- std::swap—交换两个变量的值

## 19.2 类模板

函数模板（第 19.1 节）使我们能够构建泛型函数。C++ 也支持类模板。使用类模板，我们可以以与类型无关的方式指定对象类的模式或结构。类模板机制是创建泛型类型的关键工具。

作为一个简单的示例，请考虑一个表示二维点对象的基本 Point 类。数学点对象应具有实数坐标，我们可以使用双精度浮点值来近似。另一方面，图形显示上的点更适合使用整数坐标，因为屏幕像素具有离散的整数位置。

与其提供两个单独的类，不如编写一个类模板，让编译器根据特定程序的要求实例化坐标。清单 19.6（genericpoint.h）包含泛型类。

### 清单 19.6: genericpoint.h

```cpp
#ifndef GENERICPOINT_H
#define GENERICPOINT_H

template <typename T>
class Point {
public:
    T x;
    T y;
    Point(T x, T y) : x(x), y(y) {}
};

#endif
```

如果客户端按如下方式声明 Point 对象：

```
Point<int> pixel(10, 10);
```

编译器将实例化一个看起来如下的 Point<int> 类：
