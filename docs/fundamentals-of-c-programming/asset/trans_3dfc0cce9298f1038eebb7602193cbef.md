

std::cout << '\n';
std::cout << "-----------------------------------\n";
std::cout << "Partitioned sequence" << '\n';
std::partition(std::begin(words), std::end(words),
               [](const std::string& w) { return w.length() > 3; });
std::copy(std::begin(words), std::end(words), string_output);
std::cout << '\n';
}

### 清单 20.43 (testpartition.cpp) 的输出

```
Original sequence
81 80 2 63 13 25 12 7 8 16 84 91 56 91 56 7 59 94 18 68 68 71 78 66 60

Partitioned sequence
60 80 2 66 78 68 12 68 8 16 84 18 56 94 56 7 59 91 91 7 25 71 13 63 81
...............................................................

Original sequence
fred ella adam jo pat mel anna ed oscar will tom ingrid

Partitioned sequence
fred ella adam ingrid will oscar anna ed mel pat tom jo
```

请注意，std::partition 不会尝试保持分区内元素的原始相对顺序。另外，std::partition 不会创建任何新的字符串对象；它只是在容器内移动现有的字符串对象。这使得 std::partition 对字符串的效率与对简单数字一样高。

## std::merge。

假设我们有两个已排序的序列，希望将它们合并为一个大的已排序序列。一种方法是将两个序列复制到一个更大的容器中，然后对容器进行排序，如下所示：

```
// v1 and v2 are two sorted vectors containing integers
std::vector<int> merged(v1.size() + v2.size());
auto last = std::copy(v1.begin(), v1.end(), merged.begin());
std::copy(v2.begin(), v2.end(), last);
std::sort(merged.begin(), merged.end());
```

此过程会产生正确的结果，但效率不高。请考虑如何将两叠已排序的卡片合并成一叠更大的已排序卡片。你会把一叠卡片放在另一叠卡片上面，然后重新排序这叠新的、更大的卡片吗？排序是一个耗时的过程。你必须查看每张卡片，并搜索在牌堆中重新定位它的正确位置。这种反复搜索就是拖慢过程的原因。更快的方法是查看两叠卡片顶部的卡片，选择两张顶部卡片中较小的一张，并将其面朝下放在新堆上。继续此过程，始终选择较小的顶部卡片并将其面朝下放在新堆上。当原来的两叠卡片都空了时，将新形成的堆翻转过来（使其卡片面朝上），那么得到的堆将包含所有按顺序排列的卡片。这快得多，因为你永远不需要搜索放置卡片的位置——你只需从两张可见的卡片中选出较小的一张，并将其放在新堆上。

STL 中 std::sort 的实现是一个好的实现，但即使有最好的实现，排序一般来说也是耗时的。由于将两个已排序的序列合并为一个新的已排序序列是一项常见的活动，STL 提供了 std::merge 函数。std::merge 函数将两个有序容器合并到第三个容器中。得到的容器将是有序的。清单 20.44 (testmerge.cpp) 提供了使用 std::merge 的示例。

### 清单 20.44：testmerge.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <iterator>
#include <random>

// Uniform pseudorandom number generator from an earlier chapter
// include "uniformrandom.h"

int main() {
    std::vector<int> nums1(15),
                     nums2(13);

    UniformRandomGenerator gen1(0, 40),
                               gen2(0, 40);

    auto output = std::ostream_iterator<int>(std::cout, " ");

    // Populate the vectors with pseudorandom
    // integers in the range 0, 1, ..., 50
    std::generate(std::begin(nums1), std::end(nums1), gen1);
    std::generate(std::begin(nums2), std::end(nums2), gen2);

    std::cout << "Original sequences\n";
    std::copy(std::begin(nums1), std::end(nums1), output);
    std::cout << "\n";
    std::copy(std::begin(nums2), std::end(nums2), output);
    std::cout << "\n------------------\n";

    std::sort(std::begin(nums1), std::end(nums1));
    std::sort(std::begin(nums2), std::end(nums2));

    std::cout << "Sorted sequences\n";
    std::copy(std::begin(nums1), std::end(nums1), output);
    std::cout << "\n";
    std::copy(std::begin(nums2), std::end(nums2), output);
    std::cout << "\n------------------\n";

    // Merge the sequences
    std::vector<int> merged(nums1.size() + nums2.size());
    std::merge(std::begin(nums1), std::end(nums1),
               std::begin(nums2), std::end(nums2),
               std::begin(merged));

    std::cout << "Merged sequence\n";
    std::copy(std::begin(merged), std::end(merged), output);
    std::cout << "\n";
}
```

运行清单 20.44 (testmerge.cpp) 一次会打印以下内容：

```
Original sequences
8 26 8 17 26 23 31 7 16 30 5 21 37 20 4
-------------------------------------------
29 0 22 32 18 4 4 36 26 38 21 14 34 32
-------------------------------------------
Sorted sequences
4 5 7 8 8 16 17 20 21 23 26 26 30 31 37
-------------------------------------------
0 4 4 14 18 21 22 26 29 32 32 34 36 38
-------------------------------------------
Merged sequence
0 4 4 5 7 8 8 14 16 17 18 20 21 21 22 23 26 26 26 29 30 31 32 32 34 36 37 38
```

如您所见，如果您有两个希望合并的有序容器，并且希望得到的容器中的元素是有序的，那么 std::merge 函数将非常有用。

如前所述，使用 std::merge 合并两个容器，如下面的代码所示：

```
std::vector<int> merged(nums1.size() + nums2.size());
std::merge(std::begin(nums1), std::end(nums1),
           std::begin(nums2), std::end(nums2),
           std::begin(merged));
```

比复制然后排序（如下面的代码所示）在计算上高效得多。

```
std::vector<int> merged(nums1.size() + nums2.size());
auto last = std::copy(std::begin(nums1), std::end(nums1),
                      std::begin(merged));
std::copy(std::begin(nums2), std::end(nums2), last);
std::sort(std::begin(merged), std::end(merged));
```

清单 20.45 (comparemerges.cpp) 比较了合并两个已排序序列的两种不同方法。

### 清单 20.45：comparemerges.cpp

```
#include <iostream>
#include <vector>
#include <algorithm>
#include <iterator>
#include <random>
#include <ctime>

#include "vectorprint.h"
// Uniform pseudorandom number generator from an earlier chapter
#include "uniformrandom.h"

// The vectors v1 and v2 must be in sorted order
std::vector<int> merge1(const std::vector<int>& v1,
                        const std::vector<int>& v2) {
    clock_t start = clock();
    std::vector<int> result(v1.size() + v2.size());
    std::merge(std::begin(v1), std::end(v1),
               std::begin(v2), std::end(v2),
               std::begin(result));
    clock_t stop = clock();
    std::cout << "Merge 1 elapsed time: "
              << static_cast<double>(stop - start) / CLOCKS_PER_SEC
              << " sec\n";
    return result;
}

// The vectors v1 and v2 must be in sorted order
std::vector<int> merge2(const std::vector<int>& v1,
                        const std::vector<int>& v2) {
    clock_t start = clock();
    std::vector<int> result(v1.size() + v2.size());
    auto last = std::copy(std::begin(v1), std::end(v1),
                          std::begin(result));
    std::copy(std::begin(v2), std::end(v2), last);
    std::sort(std::begin(result), std::end(result));
    clock_t stop = clock();
    std::cout << "Merge 2 elapsed time: "
              << static_cast<double>(stop - start) / CLOCKS_PER_SEC
              << " sec\n";
    return result;
}

int main() {
    const int SIZE = 10'000'000;
    std::vector<int> nums1(SIZE), nums2(SIZE);

    UniformRandomGenerator gen1(0, SIZE), gen2(0, SIZE);

    // Populate the vectors with pseudorandom
    // integers in the range 0, 1, ..., 50
    std::generate(std::begin(nums1), std::end(nums1), gen1);
    std::generate(std::begin(nums2), std::end(nums2), gen2);

    //std::cout << "Original sequences\n";
    //std::cout << "nums1\n";
    //std::cout << "nums2\n";
    //std::cout << "nums2\n";

    std::sort(std::begin(nums1), std::end(nums1));
    std::sort(std::begin(nums2), std::end(nums2));

    //std::cout << "Sorted sequences\n";
    //std::cout << "nums1\n";
    //std::cout << "nums2\n";
    //std::cout << "nums2\n";

    std::cout << "Merging . . " << '\n';
}
