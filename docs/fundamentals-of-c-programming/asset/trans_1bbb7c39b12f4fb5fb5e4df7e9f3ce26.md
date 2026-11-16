

int main() {
  // Make a vector of integers
  std::vector<int> vec = { 23, -3, 10, 4, 215, 0, -3, 2 };

  auto working = vec; // Make a copy to keep the original unchanged
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working), less_than<int>());
  std::cout << "Ascending: " << " " << working << '\n';
  std::cout << '\n';
  working = vec; // Restore the original sequence
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working), greater_than<int>());
  std::cout << "Descending: " << " " << working << '\n';
  std::cout << '\n';
  working = vec; // Restore the original sequence
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working),
            [](int a, int b) { return a > b; });
  std::cout << "Descending: " << " " << working << '\n';
  std::cout << '\n';
  working = vec; // Restore the original sequence
  std::cout << "Before: " << " " << working << '\n';
  std::sort(std::begin(working), std::end(working));
  std::cout << "Ascending: " << " " << working << '\n';
}

以下是清单 20.26 (stdsort.cpp) 排序活动的结果：

| 标签 | 值 |
|---|---|
| 初始: | (23, -3, 10, 0, 4, 215, 0, -3, 2) |
| 升序: | {-3, -3, 0, 2, 4, 10, 10, 23, 215} |
| 初始: | (23, -3, 10, 4, 215, 0, -3, 2) |
| 降序: | {215, 23, 10, 4, 2, 0, -3, -3} |
| 初始: | (23, -3, 10, 0, 4, 215, 0, -3, 2) |
| 降序: | {215, 23, 10, 4, 2, 0, -3, -3} |
| 初始: | (23, -3, 10, 4, 215, 0, -3, 2) |
| 升序: | {-3, -3, 0, 2, 4, 10, 10, 23, 215} |

清单 20.26 (stdsort.cpp) 中对 std::sort 的最后一次调用使用不提供比较函数的重载。在这种情况下，默认比较操作使用 operator< 来比较元素以进行正确排序，因此它按非降序（升序）排序。

如果存在比较函数，它必须接受与容器所持元素相同类型的两个参数。该函数必须返回布尔结果。如果第一个参数在排序序列中必须出现在第二个参数之前，则函数应返回 true。如果第一个参数不应出现在第二个参数之前，则函数应返回 false。

std::copy：std::copy 函数将元素从一个容器复制到另一个容器。以下代码将向量 v1 的内容复制到向量 v2：

```
std::vector<int> v1 { 10, 20, 30, 40 };
std::vector<int> v2(v1.size()); // Make v2 the same size as v1
std::copy(v1.begin(), v1.end(), v2.begin());
```

`std::copy` 函数的前两个参数指定要从 `v1` 复制的值的范围，第三个参数指示在 `v2` 中放置值的起始位置。接收容器必须有足够的空间来接受所有复制的元素。请注意，给定代码对 `v1` 进行精确复制。`std::copy` 函数可能显得多余，因为向量的 `operator=` 也执行向量复制。

```
v2 = v1;
```

使用直接赋值时，无需确保接收向量有足够的空间；赋值运算符会处理此细节。然而，`std::copy` 函数比 `operator=` 灵活得多，如清单 20.27 (copywithtrim.cpp) 所示。

## 清单 20.27: copywithtrim.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include "vectorprint.h"

int main() {
    // v1 is the vector to copy from
    std::vector<int> v1 {10, 20, 30, 40, 50, 60, 70, 80};
    // Ensure the v2, the vector to copy to, has the correct size
    std::vector<int> v2(v1.size() - 2);

    std::cout << "v1: " << '\n';
    std::cout << "v2: " << '\n';

    // Copy all but the first and last element from v1
    // (in other words, trim off the front and back)
    std::copy(v1.begin() + 1, v1.end() - 1, v2.begin());

    std::cout << "v1: " << '\n';
    std::cout << "v2: " << '\n';
}
```

清单 20.27 (copywithtrim.cpp) 复制了一个向量，并去掉了其首尾元素，如其输出所示：

```
{10, 20, 30, 40, 50, 60, 70, 80}
{0, 0, 0, 0, 0, 0}
{10, 20, 30, 40, 50, 60, 70, 80}
{20, 30, 40, 50, 60, 70}
```

请注意，清单 20.27 (copywithtrim.cpp) 如何推进源向量的 begin 迭代器并减小 end 迭代器，以限制其复制的值范围。程序员有责任确保目标容器有足够的空间来容纳复制的元素，在此我们将 v2 创建为所需的精确大小。

清单 20.28 (copyintomiddle.cpp) 将一个向量的一部分复制到另一个向量的中间。

## 清单 20.28: copyintomiddle.cpp

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include "vectorprint.h"

int main() {
  // v1 is the vector to copy from
  // vector<int> v1 {10, 20, 30, 40, 50, 60, 70, 80, 90, 100};
  // v2 is the vector to copy into
  std::vector<int> v2 {100, 200, 300, 400, 500, 600, 700, 800};

  std::cout << "Before: \n";
  std::cout << v1 << " \n";
  std::cout << v2 << " \n";

  // Replace a part of v2 with a portion of v1
  std::copy(v1.begin() + 3, v1.begin() + 6, v2.begin() + 3);

  std::cout << "After: \n";
  std::cout << v1 << " \n";
  std::cout << v2 << " \n";
}
```

清单 20.28 (copyintomiddle.cpp) 打印以下内容：

| 初始: |
|---|
| {10, 20, 30, 40, 50, 60, 70, 80, 90, 100} |
| {100, 200, 300, 400, 500, 600, 700, 800} |
| 之后: |
| {10, 20, 30, 40, 50, 60, 70, 80, 90, 100} |
| {100, 200, 300, 40, 50, 60, 700, 800} |

该程序用向量 v1 中的元素 40、50 和 60 覆盖向量 v2 中的元素 400、500 和 600。

标准库提供了一种特殊迭代器 std::ostream_iterator，它使 std::copy 函数能够将容器的内容复制到输出流而不是另一个容器。清单 20.29 (copytostream.cpp) 展示了此特殊迭代器的工作原理。

## 清单 20.29: copytostream.cpp

```cpp
#include <iostream>
#include <vector>
#include <iterator>

int main() {
  std::vector<int> vec { 10, 20, 30, 35, 40, 45, 50, 55 };

  // Copy the contents of the container to std::cout, separating
  // elements with a single space
  auto strm = std::ostream_iterator<int>(std::cout, " ");
  std::copy(std::begin(vec), std::end(vec), strm);
  std::cout << "\n";
}
```

清单 20.29 (copytostream.cpp) 将以下内容打印到控制台：

```
10 20 30 35 40 45 50 55
```

请注意，`std::ostream_iterator` 是一个泛型类，由输出流要接收的对象类型参数化。

清单 20.30 (copyfile.cpp) 展示了如何使用 `std::copy` 和 `std::ostream_iterator` 对象，同样轻松地将容器内容保存到文本文件中。

## 清单 20.30: copyfile.cpp

```cpp
#include <fstream>
#include <vector>
#include <iterator>

int main() {
  std::vector<int> vec { 10, 20, 30, 35, 40, 45, 50, 55 };

  // Open a text file for writing
  std::ofstream fout("output.txt");

  if (fout.good()) { // Confirm the file is ready to receive output
    // Copy the contents of the container to a text file,
    // separating elements with a single space
    auto strm = std::ostream_iterator<int>(fout, " ");
    std::copy(std::begin(vec), std::end(vec), strm);
    fout << '\n';
  }
}
```

请注意，下面两条语句

```cpp
auto strm = std::ostream_iterator<int>(fout, " ");
std::copy(std::begin(vec), std::end(vec), strm);
```

可以合并为一条语句，如

```cpp
std::copy(std::begin(vec), std::end(vec),
          std::ostream_iterator<int>(fout, " "));
```

从而避免额外变量。

`std::copy` 函数返回一个迭代器，指向目标容器中紧随函数复制的最后一个元素之后的位置。图 20.2 对此过程进行了图形表示。

当我们使用 `std::copy` 连接两个容器时，可以很好地利用此返回值。清单 20.31 (concatsequences.cpp) 提供了实现。

## 清单 20.31: concatsequences.cpp

```cpp
#include <iostream>
#include <vector>
```

