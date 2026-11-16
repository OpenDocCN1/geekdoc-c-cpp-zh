

```cpp
bool less_than(int a, int b) {
    return a < b;
}

/*
 * greater_than(a, b)
 *
 * Returns true if a > b; otherwise, returns
 * false.
 */
bool greater_than(int a, int b) {
    return a > b;
}

int main() {
    // Make a vector of integers
    std::vector<int> original { 23, -3, 4, 215, 0, -3, 2, 23, 100, 88, -10 };

    // Make a working copy of the original vector
    std::vector<int> working = original;
    std::cout << "Before: \n";
    print(working);
    std::cout << "\n";

    Comparator lt(less_than), gt(greater_than);
    selection_sort(working, lt);
    std::cout << "Ascending: \n";
    print(working);
    std::cout << " (" << lt.comparisons() << " comparisons, "
              << lt.swaps() << " swaps)\n\n";

    // Make another copy of the original vector
    working = original;
    std::cout << "Before: \n";
    print(working);
    std::cout << "\n";
    selection_sort(working, gt);
    std::cout << "Descending: \n";
    print(working);
    std::cout << " (" << gt.comparisons() << " comparisons, "
              << gt.swaps() << " swaps)\n\n";

    // Sort a sorted vector
    std::cout << "Before: \n";
    print(working);
    std::cout << "\n";
    // Reset the greater than comparator so we start counting at
    // zero
    gt.reset();
    selection_sort(working, gt);
    std::cout << "Descending: \n";
    print(working);
    std::cout << " (" << gt.comparisons() << " comparisons, "
              << gt.swaps() << " swaps)\n";
}
```

清单 17.35（polymorphicsort.cpp）中的函数与清单 16.5（loggingflexiblesort.cpp）中的函数相同，毫不奇怪，清单 17.35（polymorphicsort.cpp）的输出与清单 16.5（loggingflexiblesort.cpp）的输出也相同：

```
Before: {23,-3,4,215,0,-3,2,23,100,88,-10}
Ascending: {-10,-3,-3,0,2,4,23,23,88,100,215} (55 comparisons, 7 swaps)
------------------------------------------------------------
Before: {23,-3,4,215,0,-3,2,23,100,88,-10}
Descending: {215,100,88,23,23,4,2,0,-3,-3,-10} (55 comparisons, 5 swaps)
------------------------------------------------------------
Before: {215,100,88,23,23,4,2,0,-3,-3,-10}
Descending: {215,100,88,23,23,4,2,0,-3,-3,-10} (55 comparisons, 0 swaps)
```

由此产生一个问题：新的 Comparer 类相对于原始类有什么优势？

### 这个新 Comparer 类的设计很有趣：

- 由于其计数器字段是私有的，只有 Comparer 类本身的方法才能访问 Comparer 对象的数据。
- 两个虚方法 `compare_impl` 和 `swap_impl` 是受保护的，因此客户端不能直接访问它们。不过，派生类可以看到它们并重写它们。后缀 `_impl` 代表 "implementation"，因此 `compare_impl` 表示 `compare` 方法的实现细节，而 `swap_impl` 表示 `swap` 方法的实现细节。
- 公共 compare 和 swap 方法都将部分工作委托给受保护的 `compare_impl` 和 `swap_impl` 方法。
- compare 和 swap 方法未声明为 `virtual`，因此派生类不能重写它们。
- compare 和 swap 方法管理 `compare_count` 和 `swap_count` 计数器字段。由于派生类看不到这些字段，派生类设计者在重写 `compare_impl` 或 `swap_impl` 时，无法干扰对客户端调用 `compare` 或 `swap` 次数的正确统计。
- 向客户端报告结果的 comparisons 和 swaps 方法是非虚的，因此派生类不能重写它们的行为。

请注意，Comparer 类的设计者允许派生类中的比较和交换具有灵活性，但在如何执行和报告计数方面非常严格。如 `Comparer` 所示，在基类中正确使用 `protected` 和 `private` 说明符，使类设计者能够大大控制派生类设计者究竟可以做什么。派生类可以调整某些行为，但其他行为是不可协商的。

程序员除了更改比较的执行方式之外，还希望对 Comparer 类进行什么样的自定义？请考虑在清单 17.36（logcomparer.h）中声明的 `LogComparer` 类。

```cpp
#ifndef LOGCOMPARER_H_
#define LOGCOMPARER_H_

#include <fstream>
#include <string>
#include "comparer.h"

/*
 * Comparer objects manage the comparisons and element
 * interchanges on the selection sort function below.
 */
class LogComparer: public Comparer {
  // Output stream to which logging messages are directed
  std::ofstream fout;

protected:
  // Method that actually performs the comparison
  bool compare_impl(int m, int n) override;

  // Method that actually performs the swap
  void swap_impl(int m, int n) override;

public:
  // The client must initialize a LogComparer object with a
  // suitable comparison function and the file name of a text
  // file to which the object will direct logging messages
  LogComparer(bool (*f)(int, int), const std::string& filename);

  // The destructor must close the log file
  ~LogComparer();
};

#endif
```

`LogComparer` 类重写了 `compare_impl` 和 `swap_impl` 方法。`LogComparer` 类的实例使用 `std::ofstream` 对象将日志信息记录到文本文件中。

`LogComparer` 方法的实现可以在清单 17.37（logcomparer.cpp）中找到。

## 清单 17.37：logcomparer.cpp

```cpp
#include "logcomparer.h"
#include <cstdlib>
#include <iostream>

// Method that actually performs the comparison
// Derived classes may override this method
bool LogComparer::compare_impl(int m, int n) {
  fout << "Comparing " << m << " to " << n << '\n';
  // Base class method does the comparison
  return Comparer::compare_impl(m, n);
}

// Method that actually performs the swap
// Derived classes may override this method
void LogComparer::swap_impl(int m, int n) {
  fout << "Swapping " << m << " and " << n << '\n';
  int temp = m;
  m = n;
  n = temp;
}
}
// The client must initialize a LogComparer object with a
// suitable comparison function and the file name of the
// text file to receive logging messages.
LogComparer::LogComparer(bool (*f)(int, int), const std::string& filename):
   Comparer(f)
   {
   fout.open(filename);
   if (!fout.good()) {
      std::cout << "Could not open log file " << filename
                << " for writing\n";
      exit(1); // Terminate the program
   }
   // fout is an instance variable, not a local variable,
   // so the file stays open when the constructor finishes
}
```

构造函数尝试打开一个文件输出流，以将日志信息写入文本文件。如果构造函数出于任何原因无法打开文本文件进行写入，它将终止程序的执行。当 `LogComparer` 对象的生命周期结束时，析构函数会关闭文件流对象。

被重写的两个方法 `compare_impl` 和 `swap_impl` 会将文本写入日志文件。这两个方法都使用 `LogComparer` 对象的 `fout` 字段，而不是 `std::cout` 控制台输出流对象。

请注意，尽管 `override` 关键字出现在 `logcomparer.h` 的方法声明之后，但它并未出现在 `logcomparer.cpp` 的方法实现之后。

清单 17.38（loggingsort.cpp）中的客户端代码使用 `LogComparer` 对象创建一个名为 `sort.log` 的文本文件。

## 清单 17.38：loggingsort.cpp

```cpp
#include <iostream>
#include <vector>
#include "LogComparer.h"
/*
 * selection_sort(a, compare)
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
      // Note: i,small, and j represent positions within a
      // a[i], a[small], and a[j] represents the elements at
      // those positions.
      // small is the position of the smallest value we've seen
      // so far; we use it to find the smallest value less
      // than a[i]
      int small = i;
```

