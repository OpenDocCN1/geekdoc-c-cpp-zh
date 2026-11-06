
## 16.4.5 数学算法

**图 16.6** 演示了几种常见的数学算法，包括 `shuffle`、`count`、`count_if`、`min_element`、`max_element`、`minmax_element`、`accumulate` 和 `transform`。我们已在 **16.3 节** 中介绍过 `for_each` 数学算法。

```cpp
// Fig. 16.6: fig16_06.cpp
// Mathematical algorithms of the Standard Library.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <numeric> // accumulate is defined here
#include <array>
#include <iterator>
#include <random> // contains C++11 random number generation features
using namespace std;

int main() {
   const size_t SIZE{10};
   array<int, SIZE> a1{1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
   ostream_iterator<int> output{cout, " "};

   cout << "a1 before random_shuffle: ";
   copy(a1.cbegin(), a1.cend(), output);

   // create random-number engine and use it to help shuffle a1's elements
   default_random_engine randomEngine{random_device{}()};
   shuffle(a1.begin(), a1.end(), randomEngine); // randomly order elements
   cout << "\na1 after random_shuffle: ";
   copy(a1.cbegin(), a1.cend(), output);

   array<int, SIZE> a2{100, 2, 8, 1, 50, 3, 8, 8, 9, 10};
   cout << "\na2 contains: ";
   copy(a2.cbegin(), a2.cend(), output);

   // count number of elements in a2 with value 8
   auto result = count(a2.cbegin(), a2.cend(), 8);
   cout << "\nNumber of elements matching 8: " << result;

   // count number of elements in a2 that are greater than 9
   result = count_if(a2.cbegin(), a2.cend(), [](auto x){return x > 9;});
   cout << "\nNumber of elements greater than 9: " << result;

   // locate minimum element in a2
   cout << "\nMinimum element in a2 is: "
        << *(min_element(a2.cbegin(), a2.cend()));

   // locate maximum element in a2
   cout << "\nMaximum element in a2 is: "
        << *(max_element(a2.cbegin(), a2.cend()));

   // locate minimum and maximum elements in a2
   auto minAndMax = minmax_element(a2.cbegin(), a2.cend());
   cout << "\nThe minimum and maximum elements in a2 are "
        << *minAndMax.first << " and " << *minAndMax.second
        << ", respectively";

   // calculate sum of elements in a1
   cout << "\n\nThe total of the elements in a1 is: "
        << accumulate(a1.cbegin(), a1.cend(), 0);

   array<int, SIZE> cubes; // instantiate cubes

   // calculate cube of each element in a1; place results in cubes
   transform(a1.cbegin(), a1.cend(), cubes.begin(),
             [](auto x){return x * x * x;});
   cout << "\n\nThe cube of every integer in a1 is:\n";
   copy(cubes.cbegin(), cubes.cend(), output);
   cout << endl;
}
```

```text
a1 before random_shuffle: 1 2 3 4 5 6 7 8 9 10
a1 after random_shuffle: 9 2 10 3 1 6 8 4 5 7

a2 contains: 100 2 8 1 50 3 8 8 9 10
Number of elements matching 8: 3
Number of elements greater than 9: 3

Minimum element in a2 is: 1
Maximum element in a2 is: 100
The minimum and maximum elements in a2 are 1 and 100, respectively

The total of the elements in a1 is: 55

The cube of every integer in a1 is:
729 8 1000 27 1 216 512 64 125 343
```

图 16.6 标准库的数学算法。

### `shuffle` 算法

第 21 行使用 C++11 的 `shuffle` 算法，将 `a1.begin()` 到（*不*包含）`a1.end()` 范围内的元素随机重新排序。该算法接受*两个随机访问迭代器*参数和一个 C++11 随机数生成器引擎。第 20 行——`default_random_engine randomEngine{random_device{}()};`——使用 C++11 的 `random_device` 对象创建一个 `default_random_engine`，以非确定性种子（即无法预测的种子）来为随机数生成器设置种子。在表达式 `random_device{}()` 中，花括号初始化 `random_device` 对象，圆括号调用其重载的圆括号运算符以获取种子。第 23 行显示打乱后的结果。

### `count` 算法

第 30 行使用 `count` 算法统计 `a2.cbegin()` 到（*不*包含）`a2.cend()` 范围内值为 `8` 的元素个数。该算法要求它的两个迭代器参数至少是*输入迭代器*。

### `count_if` 算法

第 34 行使用 `count_if` 算法统计 `a2.cbegin()` 到（*不*包含）`a2.cend()` 范围内使*一元谓词*函数返回 `true` 的元素个数——我们再次使用 lambda 定义了一个一元谓词，对于大于 9 的值返回 `true`。`count_if` 算法要求它的两个迭代器参数至少是*输入迭代器*。

### `min_element` 算法

第 39 行使用 `min_element` 算法定位 `a2.cbegin()` 到（*不*包含）`a2.cend()` 范围内的*最小*元素。该算法返回一个指向*第一个*最小元素的*前向迭代器*；如果范围内*没有元素*，则返回 `a2.end()`。该算法的两个迭代器参数至少必须是*前向迭代器*。该算法的一个重载版本接收一个二元谓词函数作为第三个参数，该函数比较序列中的两个元素，如果第一个参数*小于*第二个参数，则返回 `bool` 值 `true`。

### `max_element` 算法

第 43 行使用 `max_element` 算法定位 `a2.cbegin()` 到（*不*包含）`a2.cend()` 范围内的*最大元素*。该算法返回一个位于*第一个最大元素*处的*前向迭代器*。该算法的两个迭代器参数至少必须是*前向迭代器*。该算法的一个重载版本接收一个二元谓词函数作为第三个参数，该函数比较序列中的两个元素，如果第一个参数*小于*第二个参数，则返回 `bool` 值 `true`。

![](img/eaad48f0d708c37231c1ca852bf6cf9_2065_0.png)

### 防错提示 16.3

*请确保调用* `min_element` *或* `max_element` *时指定的范围不为空，并且返回值不是“尾后”迭代器。*

### C++11：`minmax_element` 算法

第 46 行使用 C++11 的 `minmax_element` 算法，在 `a2.cbegin()` 到（*不*包含）`a2.cend()` 范围内同时定位*最小*和*最大*元素。该算法返回一对*前向迭代器*，分别位于最小和最大元素处。如果存在重复的最小或最大元素，则迭代器分别位于*第一个*最小值和*最后一个*最大值处。该算法的两个迭代器参数至少必须是*前向迭代器*。该算法的第二个版本将*二元谓词函数*作为第三个参数，用于比较序列中的元素。该二元函数接受两个参数，如果第一个参数*小于*第二个参数，则返回 `bool` 值 `true`。

### `accumulate` 算法

第 53 行使用 `accumulate` 算法（其模板位于头文件 `<numeric>` 中）对 `a1.cbegin()` 到（*不*包含）`a1.cend()` 范围内的值求和。该算法的两个迭代器参数至少必须是*输入迭代器*，其第三个参数表示总和（累加）的初始值。该算法的第二个版本将一通用函数作为第四个参数，该函数决定元素如何累加。该通用函数必须接受*两个参数*并返回一个结果。该函数的第一个参数是当前累加值，第二个参数是正在累加的序列中当前元素的值。函数返回累加结果。

### `transform` 算法

第 58–59 行使用 `transform` 算法将一个通用函数应用于 `a1.cbegin()` 到（*不*包含）`a1.cend()` 范围内的*每一个*元素。该通用函数（第四个参数）应以当前元素为参数，*不得*修改该元素，并应返回 `transformed` 值。`transform` 算法要求其前两个迭代器参数至少是*输入迭代器*，第三个参数至少是*输出迭代器*。第三个参数指定 `transformed` 值应放置的位置。请注意，第三个参数可以等于第一个参数。

`transform` 的一个重载版本接受五个参数——前两个参数是*输入迭代器*，指定来自一个源容器的元素范围；第三个参数是一个*输入迭代器*，指定另一个源容器中的第一个元素；第四个参数是一个*输出迭代器*，指定转换后的值应放置的位置；最后一个参数是一个接受两个参数并返回结果的通用函数。这个版本的 `transform` 从两个输入源中各取一个元素，将该通用函数应用于这一对元素，然后将转换后的值放置在第四个参数指定的位置。
