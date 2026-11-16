

```cpp
#include <iostream>
#include <vector>

#include "rectangle.h"
#include "triangle.h"
#include "circle.h"
#include "ellipse.h"

int main() {
    Rectangle rect(3, 4);
    Circle circ(4, 5);
    Triangle tri(3, 4, 5);
    Ellipse ell(3, 4);

    std::vector<Shape *> shape_list;

    shape_list.push_back(&circ);
    shape_list.push_back(&tri);
    shape_list.push_back(&rect);
    shape_list.push_back(&ell);

    int n = shape_list.size();
    double area_total = 0.0, max_span = 0.0;

    for (int i = 0; i < n; i++) {
        // Examine the area of each shape
        std::cout << "Area = " << shape_list[i]->area() << '\n';
        // Accumulate the areas of all the shapes
        area_total += shape_list[i]->area();
        // Account for the longest object
        if (max_span < shape_list[i]->span())
            max_span = shape_list[i]->span();
    }

    // Report the total area of all the shapes combined
    std::cout << "Total shape area is " << area_total << '\n';
    // Report the minimum length of the container
    std::cout << "Longest shape is " << max_span << '\n';
}
```

请注意，Square 和 Circle 都不需要访问其基类的受保护字段。请参考清单 17.32（drawablerectangle.cpp），它从 Rectangle 派生出一个新类，以允许客户端在控制台窗口中使用文本图形绘制矩形对象。

### 清单 17.32: drawablerectangle.cpp

```cpp
#include <iostream>
#include "Rectangle.h"

class DrawableRectangle: public Rectangle {
public:
    // Delegate construction to the base class
    DrawableRectangle(double length, double width):
        Rectangle(length, width) {
    // Draw a rectangle using text graphics
    void draw() const {
        // Access the inherited protected fields
        int rows = static_cast<int>(length + 0.5),
            columns = static_cast<int>(width + 0.5);
        // Draw the rectangle
        for (int r = 0; r < rows; r++) {
            for (int c = 0; c < columns; c++)
                std::cout << '*';
            std::cout << '\n';
        }
    }
}
int main() {
    DrawableRectangle rec1(3, 2),
        rec2(10, 5),
        rec3(4, 8);
    rec1.draw();
    std::cout << "--------------------\n";
    rec2.draw();
    std::cout << "--------------------\n";
    rec3.draw();
}
```

## 17.7. 受保护成员

清单 17.32（drawablerectangle.cpp）显示

![](img/e84ad11adb18201d71595b31ce6c9eff_541_0.png)

DrawableRectangle::draw 方法需要访问 length 和 width 字段才能绘制矩形。重要的是要记住，每个 DrawableRectangle 对象都包含这些字段，因为它从 Rectangle 继承了它们；但是，如果在 Rectangle 中将 length 和 width 字段声明为 private 而不是 protected，DrawableRectangle::draw 将无法访问这些字段。

类为其成员支持三种保护级别：

- 1. private：这是默认设置。私有成员可被类本身内的任何代码访问，但外部代码不可访问。
- 2. protected：受保护成员可被类本身内的代码以及使用公有继承的派生类内的代码访问。受保护成员对其他（非派生）类不可访问。
- 3. public：公有成员可被任何地方的代码访问。

总之，private 意味着类外部完全不可访问。public 意味着对所有人开放。protected 对子类而言是“公有”的，对所有其他类而言是“私有”的。

## 17.8 精细调整继承

回顾清单 16.5（loggingflexiblesort.cpp）中找到的灵活排序代码。它使用对象来启用以下功能：

- 通过使用自定义比较函数，可以改变选择排序函数所强加的顺序。
- 用于确定排序顺序的对象会收集排序函数执行的比较次数和元素交换次数的数据。

清单 17.35（polymorphicsort.cpp）对清单 16.5（loggingflexiblesort.cpp）进行了略微的变体。除了将代码拆分为多个源文件外，它还添加了两个虚方法，使未来的开发者能够在派生类中自定义 compare 和 swap 方法。

清单 17.33（comparer.h）包含 Comparer 类的声明。

### 清单 17.33: comparer.h

```cpp
#ifndef COMPARER_H
#define COMPARER_H
/*
 * Comparer objects manage the comparisons and element
 * interchanges on the selection sort function below.
 */
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
bool (*comp)(int, int);

protected:
// Method that actually performs the comparison
// Derived classes may customize this method
virtual bool compare_impl(int m, int n);

// Method that actually performs the swap
// Derived classes may customize this method
virtual void swap_impl(int& m, int& n);

public:
// The client must initialize a Comparer object with a
// suitable comparison function.
Comparer(bool (*f)(int, int));

// Resets the counters to make ready for a new sort
void reset();

// Method that performs the comparison. It delegates
// the actual work to the function pointed to by comp.
// This method logs each invocation.
bool compare(int m, int n);

// Method that performs the swap.
// Interchange the values of
// its parameters a and b which are
// passed by reference.
// This method logs each invocation.
void swap(int& m, int& n);

// Returns the number of comparisons this object has
// performed since it was created.
int comparisons() const;

// Returns the number of swaps this object has
// performed since it was created.
int swaps() const;
};
#endif
```

清单 17.34（comparer.cpp）提供了 Comparer 类方法的实现。

### 清单 17.34: comparer.cpp

```cpp
#include "comparer.h"

// Method that actually performs the comparison
// Derived classes may customize this method
bool Comparer::compare_impl(int m, int n) {
    return comp(m, n);
}

// Method that actually performs the swap
// Derived classes may customize this method
void Comparer::swap_impl(int& m, int& n) {
    int temp = m;
    m = n;
    n = temp;
}

// The client must initialize a Comparer object with a
// suitable comparison function.
Comparer::Comparer(bool (*f)(int, int)):
    compare_count(0), swap_count(0), comp(f) {}

// Resets the counters to make ready for a new sort
void Comparer::reset() {
    compare_count = swap_count = 0;
}

// Method that performs the comparison. It delegates
// the actual work to the function pointed to by comp.
// This method logs each invocation.
bool Comparer::compare(int m, int n) {
    compare_count++;
    return compare_impl(m, n);
}

// Method that performs the swap.
// Interchange the values of
// its parameters a and b which are
// passed by reference.
// This method logs each invocation.
void Comparer::swap(int& m, int& n) {
    swap_count++;
    swap_impl(m, n);
}

// Returns the number of comparisons this object has
// performed since it was created.
int Comparer::comparisons() const {
    return compare_count;
}

// Returns the number of swaps this object has
// performed since it was created.
int Comparer::swaps() const {
    return swap_count;
}
```

请注意，尽管 virtual 关键字出现在 comparer.h 的方法声明之前，但它并未出现在 comparer.cpp 的方法实现之前。

清单 17.35（polymorphicsort.cpp）提供了用于测试新 Comparer 类的客户端代码。

### 清单 17.35: polymorphicsort.cpp

```cpp
#include <iostream>
#include <vector>
#include "comparer.h"

/*
 * selection_sort(a, compare)
 *
 *   Arranges the elements of vector a in an order determined
 *   by the compare object.
 *   a is a vector of ints.
 *   compare is a function that compares the ordering of
 *   two integers.
 *   The contents of a are physically rearranged.
 */
void selection_sort(std::vector<int>& a, Comparer& compare) {
    int n = a.size();
    for (int i = 0; i < n - 1; i++) {
        // Note: i, small, and j represent positions within a
        // a[i], a[small], and a[j] represents the elements at
        // those positions.
        //
        // small is the position of the smallest value we've seen
        // so far; we use it to find the smallest value less
        // than a[i];
        int small = i;
        // See if a smaller value can be found later in the array
        for (int j = i + 1; j < n; j++)
            if (compare(a[j], a[small])) // found a smaller value
                small = j; // remember a[small], if a smaller value was found
        // Swap a[i] and a[small], if a smaller value was found
        if (i != small)
            compare.swap(a[i], a[small]);
    }
}
```

```cpp
/*
 * print
 *
 *   Prints the contents of an integer vector
 *   a is the vector to print.
 *   a is not modified.
 */
void print(const std::vector<int>& a) {
    int n = a.size();
    std::cout << '{';
    if (n > 0) {
        std::cout << a[0]; // Print the first element
        for (int i = 1; i < n; i++)
            std::cout << ', ' << a[i]; // Print the rest
    }
    std::cout << '}';
}
```

```cpp
/*
 * less_than(a, b)
 *
 *   Returns true if a < b; otherwise, returns
 *   false.
 */
```

