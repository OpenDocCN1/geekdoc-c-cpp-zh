

清单 12.4 (binarysearch.cpp) 包含一个实现二分查找算法的 C++ 函数。

## 清单 12.4: binarysearch.cpp

```cpp
#include <iostream>
#include <vector>
#include <iomanip>

/*
 * binary_search(a, seek)
 * Returns the index of element seek in vector a;
 * returns -1 if seek is not an element of
 * a is the vector to search; a's contents must be
 * sorted in ascending order.
 * seek is the element to find.
 */
int binary_search(const std::vector<int>& a, int seek) {
    int first = 0, // Initially the first position
        last = a.size() - 1, // Initially the last position
        mid; // The middle of the last position
    while (first <= last) {
        mid = first + (last - first + 1)/2;
        if (a[mid] == seek) {
            return mid; // Found it
        } else if (a[mid] > seek) // continue with 1st half
            last = mid - 1;
        else // a[mid] < seek // continue with 2nd half
            first = mid + 1;
    }
    return -1; // Not there
}

/*
 * format(i)
 * Prints integer i right justified in a 4-space
 * field. Prints "****" if i > 9,999.
 */
void format(int i) {
    if (i > 9999)
        std::cout << "****\n"; // Too big!
    else
        std::cout << std::setw(4) << i;
}

/*
 * print(v)
 * Prints the contents of an int vector.
 * v is the vector to print.
 */
void print(const std::vector<int>& v) {
    for (int i : v)
        format(i);
}

/**
 * display(a, value)
 *
 * Draws an ASCII art arrow showing where
 * the given value is within the vector.
 * a is the vector.
 * value is the element to locate.
 */
void display(const std::vector<int>& a, int value) {
  int position = binary_search(a, value);
  if (position >= 0) {
    print(a); // Print contents of the vector
    std::cout << '\n';
    position = 4*position + 7; // Compute spacing for arrow
    std::cout << std::setw(position);
    std::cout << " ^\n";
    std::cout << std::setw(position);
    std::cout << " |\n";
    std::cout << std::setw(position);
    std::cout << " |\n";
    std::cout << std::setw(position);
    std::cout << " +-- " << value << '\n';
  } else {
    std::cout << value << " not in ";
    print(a);
    std::cout << '\n';
  }
  std::cout << "=======" << '\n';
}

int main() {
  // Check binary search on even- and odd-length vectors and
  // on empty vector
  std::vector<int> even_list{ 1, 2, 3, 4, 5, 6, 7, 8 },
                   odd_list{ 1, 2, 3, 4, 5, 6, 7, 8, 9 },
                   empty_list;

  for (int i = -1; i < 10; i++)
    display(even_list, i);
  for (int i = -1; i < 10; i++)
    display(odd_list, i);
  for (int i = -1; i < 10; i++)
    display(empty_list, i);
}
```

在 binary_search 函数中：

- first 和 last 的初始化：

```cpp
int first = 0, // Initially the first position
last = a.size() - 1, // Initially the last position
```

可确保对于非空向量，first 小于或等于 last。如果向量为空，first 为零，而 last 等于 n - 1，即 -1。因此，在空向量的情况下，binary_search 将跳过循环体并立即返回 -1。这是正确的行为，因为空向量不可能包含我们要查找的任何项。

## 图 12.2 二分查找。查找过程中不考虑灰显的元素。

```cpp
std::vector<int> list = { 10, 14, 20, 28, 29, 33,
34, 45, 48 };
int x = binary_search(list, 33);
```

![](img/e84ad11adb18201d71595b31ce6c9eff_373_0.png)

- 变量 mid 表示 first 和 last 之间的中点值，并在以下语句中计算：

```cpp
mid = first + (last - first + 1)/2;
```

这种算法看起来可能有点复杂。计算两个值平均值的更直接的方法是

```cpp
mid = (first + last)/2; // Alternate calculation
```

这种计算中点的方法的问题是，它产生正确结果的次数比清单 12.4 (binarysearch.cpp) 中的版本更少。如果向量很大，且 first 和 last 都有相对较大的值，就会出现此问题。表达式 first + last 可能会溢出整数范围，产生无意义的结果。随后的除以二操作为时已晚，无法提供帮助。表达式 first + last 溢出整数范围的次数比表达式 first + (last - first + 1)/2 更多，因为 (last - first + 1)/2 要添加到 first 的值要小得多。如果你在想“我永远不会想到这个问题”，请不要太担心。大量称职的专业软件工程师都曾陷入过这一疏忽（参见 http://googleresearch.blogspot.com/2006/06/extra-extra-read-all-about-it-nearly.html）。

mid 的计算可确保 first <= mid <= last。

- 如果 mid 是所查找元素的位置（在第一个 if 语句中检查），则循环终止并返回正确位置。

- 第二个 if 语句可确保每次循环时 last 减小或 first 增加。因此，如果循环未因其他原因终止，最终 first 将大于 last，循环将终止。如果出于此原因终止循环，则函数返回 -1。这是正确的行为。

- 第二个 if 语句将无关元素排除在后续查找之外。剩余待考虑的元素数量实际上被减半。

图 12.2 说明了二分查找的工作原理。

二分查找算法的实现比更简单的线性查找算法更复杂。通常，简单越好，但对于处理可能包含大量数据的数据结构的算法，采用利用数据结构的巧妙技巧的更复杂算法（如二分查找所做的）通常会显著优于更简单、更容易编码的算法。

为了公平比较线性查找与二分查找，假设我们要在已排序的向量中定位一个元素。向量有序对二分查找至关重要，但对线性查找也有帮助。修订后的线性查找算法是

```cpp
// This version requires vector a to be sorted in
// ascending order.
int linear_search(const std::vector<int>& a, int seek) {
    int n = a.size();
    for (int i = 0; i < n && a[i] <= seek; i++)
        if (a[i] == seek)
            return i; // Return position immediately
    return -1; // Element not found
}
```

请注意，与线性查找的原始版本一样，循环将在检查完所有元素时终止，但当它遇到大于所查找元素的元素时也会提前终止。由于向量已排序，一旦开始看到大于所查找值的元素，就无需继续搜索；在已排序的向量中，seek 不可能出现在较大元素之后。

假设待搜索的向量包含 n 个元素。在最坏情况下（查找比向量中任何当前元素都大的元素），线性查找的循环需要 n 次迭代。在最佳情况下（查找比向量中任何当前元素都小的元素），函数会立即返回而不考虑任何其他元素。因此，循环迭代次数范围从 1 到 n，平均而言，线性查找在循环结束并返回之前需要 n/2 次比较。

现在考虑对包含 n 个元素的向量进行二分查找。每次比较后，剩余待考虑的向量大小为原始大小的一半。如果第一次探测未找到所查找项，则剩余待搜索的元素数量为 n/2。下一次循环后，剩余待考虑的元素数量为 n/2 的一半，即 n/4。第三次迭代后，向量中的搜索空间降至 n/4 的一半，即 n/8。每次循环都会继续将搜索区域减半，直到找到所查找元素或没有元素可考虑为止。确定一组事物可以对半分割多少次直到只剩一个元素的问题，可以用以 2 为底的对数来解决。对于二分查找，未找到所查找元素的最坏情况需要循环进行 log2 n 次迭代。

这种分析如何帮助我们确定哪种查找更好？算法的质量由两个关键特征来判断：

- 运行需要多少时间（处理器周期）？
- 运行需要多少空间（内存）？

在我们的情况中，两种查找算法处理序列时只需少量额外局部变量，因此对于大型序列，它们所需的空间基本相同。这里的巨大区别在于速度。二分查找每次循环都会执行更复杂的计算，每个操作都需要时间，因此二分查找可能更慢。线性查找更简单（循环中的操作更少），但其循环执行次数可能比二分查找的循环多得多，因此总体上它更慢。

我们可以通过两种方式推断出更快的算法：经验法和分析法。经验测试是一

