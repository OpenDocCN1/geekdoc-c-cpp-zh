
```cpp
string sarr[] = { "alpha", "bravo", "charley", "delta" };

string dest[4] = { "", "", "", "" };

auto last = end(sarr);

auto lastDest = move(sarr, last, dest); // 将所有元素移动到 dest

cout << "sarr after move:\n";

for(auto const& s : sarr) cout << s << " ";

cout << "\n";

cout << "dest after move:\n";

for(auto const& s : dest) cout << s << " ";

cout << "\n";

move_backward(dest, lastDest, sarr); // 反向移动到 sarr

cout << "sarr after move_backward:\n";

for(auto const& s : sarr) cout << s << " ";

cout << "\n";

}
```

## 19.1.37 next_permutation / prev_permutation

- 头文件：`<algorithm>`
- 函数原型：
  - `bool next_permutation(BidirectionalIterator first, BidirectionalIterator last);`
  - `bool next_permutation(BidirectionalIterator last, Comp comp);`
  - `bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last);`
  - `bool prev_permutation(BidirectionalIterator last, Comp comp);`

- 描述：
  - 第一个原型：`next_permutation`，给定范围 `[first, last)` 内元素的序列，确定其下一个排列。例如，如果元素 1, 2 和 3 是调用 `next_permutation` 的范围，后续的 `next_permutation` 调用将重新排列序列：
    ```
    1 2 3
    1 3 2
    2 1 3
    2 3 1
    3 1 2
    3 2 1
    ```
    这个示例显示了元素被重新排序，使得每个新排列都代表更大的值（132 比 123 大，213 比 132 大），使用的是迭代器所指向数据类型的 `operator<`。如果发生了重排序，返回值 `true`；如果没有发生重排序，则返回值 `false`，即序列表示的是（最大的）值的情况。在这种情况下，序列也会使用 `operator<` 进行排序。
  - 第二个原型：给定范围 `[first, last)` 内元素的序列，使用二元谓词 `comp` 确定下一个排列。范围内的元素被重排序。如果发生了重排序，返回值 `true`；如果没有发生重排序，则返回值 `false`，即结果序列按照二元谓词 `comp` 排序。
  - 最后两个原型实际上意图前两个，但计算的不是下一个排列而是上一个排列。

- 示例：
```cpp
#include <algorithm>
#include <iterator>
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

bool caseString(string const &first, string const &second)
{
  return strcmp(first.c_str(), second.c_str()) < 0;
}

// // 将 'next_' 改为 'prev_' 以获取上一个排列

int main() {

    string saints[] = {"Oh", "when", "the", "saints"};

    cout << "All permutations of Oh when the saints:\n";

    do {

        copy(saints, saints + 4, ostream_iterator<string>(cout, " "));

        cout << "\n";

    } while (next_permutation(saints, saints + 4, caseString));

    cout << "After sorting the sequence:\n";

    sort(saints, saints + 4, caseString);

    cout << "Sequences:\n";

    do {

        copy(saints, saints + 4, ostream_iterator<string>(cout, " "));

        cout << "\n";

    } while (next_permutation(saints, saints + 4, caseString));

// 显示部分:

// 'Oh when the saints' 的排列：

// 序列：

// Oh when the saints

// saints the when

// ... 
```

## 19.1.38 nth_element

- 头文件：`<algorithm>`
- 函数原型：
  - `void nth_element(RandomAccessIterator first, RandomAccessIterator nth, RandomAccessIterator last);`
  - `void nth_element(RandomAccessIterator first, RandomAccessIterator nth, RandomAccessIterator last, Compare comp);`

- 描述：
  - 第一个原型：范围 `[first, last)` 内的所有元素相对于 `nth` 所指向的元素进行排序：`[first, nth)` 内的元素小于 `nth` 指向的元素，`[nth, last)` 内的元素大于 `nth` 指向的元素。这两个子集本身并没有排序。使用迭代器指向的数据类型的 `operator<` 来比较元素。
  - 第二个原型：范围 `[first, last)` 内的所有元素相对于 `nth` 所指向的元素进行排序：`[first, nth)` 范围内的元素小于 `nth` 指向的元素，`[nth, last)` 内的元素大于 `nth` 指向的元素。这两个子集本身并没有排序。使用函数对象 `comp` 来比较元素。

- 示例：
```cpp
#include <algorithm>
#include <iostream>
#include <iterator>
#include <functional>
using namespace std;

int main() {

    int ia[] = {1, 3, 5, 7, 9, 2, 4, 6, 8, 10};

    nth_element(ia, ia + 3, ia + 10);

    cout << "sorting with respect to " << ia[3] << '\n';

    copy(ia, ia + 10, ostream_iterator<int>(cout, " "));

}

// 显示:

// 关于 4 的排序

// 1 2 3 4 5 6 7 8 9 10
```

## 19.39 partial_sort / partial_sort_copy

- 头文件：`<algorithm>`
- 函数原型：
  - `void partial_sort(RandomAccessIterator first, RandomAccessIterator middle, RandomAccessIterator last);`
  - `void partial_sort(RandomAccessIterator first, RandomAccessIterator middle, RandomAccessIterator last, BinaryPredicate pred);`

- 描述：
  - 第一个原型：范围 `[first, middle)` 内的所有元素使用迭代器指向的数据类型的 `operator<` 进行排序。`[middle, last)` 范围内的元素没有排序。
  - 第二个原型：范围 `[first, middle)` 内的元素根据提供的谓词 `pred` 进行排序。`[middle, last)` 范围内的元素没有排序。

- 示例：
```cpp
#include <algorithm>
#include <iostream>
#include <iterator>
#include <functional>
using namespace std;

int main() {

    int ia[] = {1, 9, 5, 3, 7, 2, 4, 6, 8, 10};

    partial_sort(ia, ia + 3, ia + 10);

    cout << "first 3 sorted:\n";

    copy(ia, ia + 3, ostream_iterator<int>(cout, " "));

    cout << '\n';

    partial_sort(ia, ia + 3, ia + 10, greater<int>());

    cout << "first 3 sorted (descending):\n";

    copy(ia, ia + 3, ostream_iterator<int>(cout, " "));

    cout << '\n';

}

// 显示:

// first 3 sorted: 1 2 3

// first 3 sorted (descending): 10 9 8
```

```cpp
#include <algorithm>
#include <iostream>
#include <iterator>
#include <functional>
using namespace std;

int main() {
    int ia[] = {1, 9, 5, 3, 7, 2, 4, 6, 8, 10};
    int ia2[6];

    partial_sort_copy(ia, ia + 3, ia + 10, ia2);
    cout << "first 3 elements sorted and copied to ia2:\n";
    copy(ia2, ia2 + 6, ostream_iterator<int>(cout, " "));
    cout << '\n';

    partial_sort_copy(ia, ia + 3, ia + 10, ia2, greater<int>());
    cout << "first 3 elements sorted and copied to ia2:\n";
    copy(ia2, ia2 + 6, ostream_iterator<int>(cout, " "));
    cout << '\n';
}

// 显示:
// first 3 elements sorted and copied to ia2: 1 2 3
// first 3 elements sorted and copied to ia2: 10 9 8
```

## 19.1. 通用算法

## 19.1.41 partition / partition_point / stable_partition

- 头文件：`<algorithm>`
- 函数原型：
  - `BidirectionalIterator partition([ExecPol] BidirectionalIterator first, BidirectionalIterator last, UnaryPredicate pred);`
  - `BidirectionalIterator stable_partition([ExecPol] BidirectionalIterator first, BidirectionalIterator last, UnaryPredicate pred);`
  - `ForwardIterator partition_point (ForwardIterator first, ForwardIterator last, UnaryPredicate pred);`

- 描述：
  - 第一个原型：范围 `[first, last)` 中所有一元谓词求值为为 `true` 的元素被放在求值为为 `false` 的元素之前。
  - 第二个原型：与第一个原型相同，但保留了所有谓词求值为为 `false` 的元素的相对顺序，以及所有谓词求值为为 `true` 的元素的相对顺序。
  - 第三个原型：不重排 `[first, last)` 范围内的元素，但返回一个指向第一个 `pred` 返回 `false` 的元素的迭代器。如果 `pred` 对所有元素都返回 `true`，则返回 `last`。

返回值指向分区范围内最后一个 `pred` 求值为为 `true` 的元素之后。

- 示例：
```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <iterator>
using namespace std;

void show(int *begin, int *end)
{
  copy(begin, end, ostream_iterator<int>(cout, " "));
  cout << '\n';
}

int main()
{
  int org[] = { 1, 3, 5, 7, 9, 10, 2, 8, 6, 4 };
  int ia[10];

  copy(org, org + 10, ia);

  auto lessThan4 = [&](int value)
  {
    return value <= 4;
  };

  int *split = partition(ia, ia + 10, lessThan4);

  cout << "Last ia[] element <= 4 is ia[" << split - ia << "]\n";

  show(ia, end(ia));

  copy(org, org + 10, ia);

  split = stable_partition(ia, ia + 10, lessThan4);

  cout << "Last org[]-element <= 4 is ia[" << split - ia << "]\n";

  show(org, end(ia));

  cout << "org[]-elements up to the partition 4 are:\n";

  copy(org, partition_point(org, org + 10, lessThan4), ostream_iterator<int>(cout, " "));

// Last ia[] element <= 4 is ia[3]

// 1 3 4 2 9 10 7 8 6 5

// Last org[]-element <= 4 is ia[3]

// 1 3 2 4 5 7 9 10 8 6

// org[]-elements up to the partition 4 are:

1 3
```

## 19.42 partition_copy

- 头文件：`<algorithm>`
- 原型类型：
  - `std::pair<ForwardIter2, ForwardIter3> partition_copy(ExecPol, ForwardIter1 first, ForwardIter1 last, ForwardIter2 trueDest, ForwardIter3 falseDest, UnaryPredicate pred);`

- 描述：
  - 从迭代器范围 `[first, last)` 达到的所有 `pred` 返回 `true` 的元素被复制到从 `trueDest` 开始的位置，而剩余元素被复制到从 `falseDest` 开始的位置。范围 `[first, last)` 不可与从 `trueDest` 或 `falseDest` 开始的范围重叠。

- 示例：
