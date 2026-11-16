

图 20.2 std::copy 函数返回一个迭代器，指向目标容器中紧随最后一个被复制元素之后的位置。这里迭代器 r 说明了在给定代码序列中 std::copy 返回的值。

之前：

```cpp
std::vector<int> vec { 4, 1, 7 };
std::vector<int> seq(5);
```

![](img/e84ad11adb18201d71595b31ce6c9eff_685_0.png)

之后：

```cpp
auto r = std::copy(vec.begin(), vec.end(),
             seq.begin());
```

![](img/e84ad11adb18201d71595b31ce6c9eff_685_1.png)

```cpp
#include <algorithm>
#include "vectprint.h"

int main() {
  std::vector<int> v1 { 34, 0, -19, 8, 3 },
                   v2 { 66, 10, -7, -3, 0, 11, 5 };
  std::cout << "v1 = " << v1 << ", v2 = " << v2 << '\n';
  // Create v3 with the exact size needed for the concatenation
  // of v1 and v2
  std::vector<int> v3(v1.size() + v2.size());
  // Copy v1 first
  auto last = std::copy(v1.begin(), v1.end(), v3.begin());
  // The last iterator now points to the position in v3
  // immediately following the last element copied by std::copy.

  // Copy v2 into the place where the v1 copy left off
  std::copy(v2.begin(), v2.end(), last);
  std::cout << "v3 = " << v3 << '\n';
}
```

清单 20.31 (concatsequences.cpp) 中的 last 变量（由第一次调用 std::copy 返回）确定了放置第二个序列 v2 元素的起始位置。程序输出：

```
v1 = { 34, 0, -19, 8, 3 }, v2 = { 66, 10, -7, -3, 0, 11, 5 }
v3 = { 34, 0, -19, 8, 3, 66, 10, -7, -3, 0, 11, 5 }
```

如果我们正在开发一个需要在代码各处拼接向量的应用程序，可以通过将两次 std::copy 调用封装到自定义函数中来简化此过程。我们还通过重载 operator+ 使该函数使用起来更自然，这与 std::string 类设计者为字符串拼接所做的一样。清单 20.32 (vectorconcatfunction.cpp) 借用了我们在清单 20.31 (concatsequences.cpp) 中编写的代码来实现这样的函数。

### Listing 20.32: vectorconcatfunction.cpp

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include "vectprint.h"

template <typename T>
std::vector<T> operator+(const std::vector<T>& left,
                 const std::vector<T>& right) {
  // Create result vector with the exact size needed for the
  // concatenation of the left vector and right vector.
  std::vector<T> result(left.size() + right.size());
  // Copy the left vector first
  auto last = std::copy(left.begin(), left.end(), result.begin());
  // The last iterator now points to the position in the result
  // immediately following the last element copied by std::copy.
  // Copy the right vector into the place where the previous copy left off
  std::copy(right.begin(), right.end(), last);
  return result;
}

int main() {
  std::vector<int> v1 { 34, 0, -19, 8, 3 },
                   v2 { 66, 10, -7, -3, 0, 11, 5 };
  std::cout << "v1 = " << v1 << ", v2 = " << v2 << '\n';
  auto combined = v1 + v2;
  std::cout << "v1 + v2 = " << combined << '\n';
}
```

清单 20.32 (vectorconcatfunction.cpp) 输出如下：

```
v1 = {34, 0, -19, 8, 3}, v2 = {66, 10, -7, -3, 0, 11, 5}
v1 + v2 = {34, 0, -19, 8, 3, 66, 10, -7, -3, 0, 11, 5}
```

请注意，我们的模板化 operator+ 方法会拼接任何两个持有相同类型元素的向量。

### std::transform

std::transform 函数的工作方式类似于 std::copy，不同之处在于它需要一个可以修改被复制元素的函数。std::copy 和 std::transform 函数都需要源容器的起始迭代器和结束迭代器，以及目标容器的起始迭代器。清单 20.33 (testtransform.cpp) 说明了 std::transform 的用法。

### Listing 20.33: testtransform.cpp

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <numeric>
#include "vectorprint.h"

int main() {
  const int SIZE = 20;

  // Make a vector of SIZE integers
  std::vector<int> seq(SIZE);
  // Populate the vector with 0, 1, 2, 3, ..., SIZE - 1
  std::iota(std::begin(seq), std::end(seq), 0);

  // Display the vector
  std::cout << seq << '\n';

  // Make a vector large enough to hold the transformed values
  std::vector<int> seq2(SIZE);

  // Copy the seq to seq2, transforming each value
  std::transform(std::begin(seq), std::end(seq), std::begin(seq2),
                 [](int n) { return 2*n; });

  // Display the two sequences
  std::cout << seq << '\n';
  std::cout << seq2 << '\n';
}
```

清单 20.33 (testtransform.cpp) 输出：

```
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19}
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19}
{0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38}
```

std::transform 函数非常适合将 std::string 中的所有字母大写。清单 20.34 (uppercasestring.cpp) 将 C 函数 toupper 应用于字符串中的所有字符。

### Listing 20.34: uppercasestring.cpp

```cpp
#include <iostream>
#include <string>
#include <algorithm>
#include <cctype>

int main() {
    std::string name = "Fred",
               str = "abcDEF-GHiJkL345qw";

    std::cout << "Before: " << name << " " << str << "\n";
    // Uppercase the strings
    std::transform(std::begin(name), std::end(name),
                   std::begin(name), std::toupper);
    std::transform(std::begin(str), std::end(str),
                   std::begin(str), std::toupper);

    std::cout << "After : " << name << " " << str << "\n";
}
```

清单 20.34 (uppercasestring.cpp) 输出：

```
Before: Fred abcDEF-GHiJkL345qw
After: FRED ABCDEF-GHIJKL345QW
```

### std::count

std::count 的行为与清单 20.13 (genericcount.cpp) 中的 count_value 函数完全相同。清单 20.35 (stdcount.cpp) 说明了其用法。

### Listing 20.35: stdcount.cpp

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> a { 34, 5, 12, 5, 8, 5, 11, 2};
    std::cout << std::count(std::begin(a), std::end(a), 5) << '\n';
    std::cout << std::count(std::begin(a), std::end(a), 7) << '\n';
    std::cout << std::count(std::begin(a), std::end(a), 8) << '\n';
    a = {}; // Try on empty vector
    std::cout << std::count(std::begin(a), std::end(a), 5) << '\n';
    std::cout << std::count(std::begin(a), std::end(a), 7) << '\n';
    std::cout << std::count(std::begin(a), std::end(a), 8) << '\n';
}
```

### std::count_if

std::count_if 函数计算容器中具有特定属性的元素数量；例如，以下代码将打印 vec 中偶数值的数量：

```cpp
// vec is a vector of integers
std::cout << std::count_if(std::begin(vec), std::end(vec),
             [](int n) { return n % 2 == 0 });
```

传递给 std::count_if 的最后一个参数是一个函数，它接受容器声明持有的类型的单个值。该函数返回 true 或 false。返回布尔结果的函数称为谓词。某些 STL 算法（如 std::count_if）期望将谓词作为参数，以便它们只处理满足谓词的元素。

### std::copy_if

std::copy_if 函数使用谓词，从一个容器有选择地复制满足给定条件的元素到另一个容器。清单 20.36 (copyevens.cpp) 使用 std::count_if 和 std::copy_if 来复制向量的相关部分。

### Listing 20.36: copyevens.cpp

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include "vectorprint.h"

int main() {
    // Make a vector of SIZE integers
    std::vector<int> seq { 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 };
    std::cout << "Copying even numbers from " << seq << '\n';

    // A function to test for evenness
    auto is_even = [](int n) { return n % 2 == 0 };

    // Count the number of even integers in seq
    int even_count = std::count_if(std::begin(seq), std::end(seq), is_even);

    // Make a copy of vec omitting all the odd numbers
    std::vector<int> seq2(even_count);
    std::copy_if(std::begin(seq), std::end(seq), std::begin(seq2), is_even);

    // Display seq2
    std::cout << "New sequence " << seq2 << '\n';
}
```

清单 20.36 (copyevens.cpp) 输出：

```
Copying even numbers from { 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12 }
New sequence { 2, 4, 6, 8, 10, 12 }
```

请注意，在清单 20.36 (copyevens.cpp) 中，我们将一个 lambda 函数赋值给变量 is_even。这样我们就不必编写两次相同的 lambda 表达式：一次用于在 std::count_if 中测试偶数，另一次用于在 std::copy_if 中测试偶数。谓词不必是 lambda 函数——它们也可以是全局命名函数。lambda 函数通常更方便，如果谓词在程序的其他地方不需要，则无需编写全局函数。

### std::find_if

std::find_if 函数使用谓词来定位容器中满足给定谓词的第一个元素。清单 20.37 (testfindif.cpp) 在整数向量中查找第一个偶数。

