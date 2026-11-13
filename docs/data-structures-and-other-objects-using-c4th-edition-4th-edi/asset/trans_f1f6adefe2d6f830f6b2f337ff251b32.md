

具有对数运行时间的算法运行速度很快，因为 n 的对数远小于 n。而且，n 越大，这种差异就越显著。例如，2 的以 2 为底的对数是 1，8 的以 2 为底的对数是 3，64 的以 2 为底的对数是 6，一千的以 2 为底的对数小于 10，一百万的以 2 为底的对数小于 20。

这意味着二分查找算法非常高效。在包含一千个元素的数组上，运行时间为 18(⌊log₂ n⌋ + 1) + 2 的我们的二分查找算法将执行不超过 182 次操作。即使是一百万个条目，最坏情况下的时间也少于 400 次操作。

我们不会对二分查找的平均运行时间进行严格分析，但可以告诉你，实际查找一个数字的平均运行时间是 O(log n)。不难看出为什么这是真的。我们已经看到，当未找到目标时，递归深度是 ⌊log₂ n⌋ + 1。在最坏情况下，即使找到了目标，也需要 ⌊log₂ n⌋ 的递归深度（比未找到目标少一次）。在某些情况下，算法不需要那么多递归调用。如果所要查找的目标被找到，算法可以在不进行额外递归调用的情况下终止。因此，在某些输入上递归调用深度为 0，在其他输入上为 1，在其他输入上为 2，依此类推，直到 ⌊log₂ n⌋。然而，更完整的分析会显示，数组中近一半的键最终需要 ⌊log₂ n⌋ 的递归深度。即使另一半键完全不需要递归，这也会导致平均递归深度为 ⌊log₂ n⌋ 的一半。因此，查找一个键的平均递归调用次数至少是 ⌊log₂ n⌋ 的一半。所以，平均情况最多只能比最坏情况节省 ½ 或更小的因子。但是像 ½ 这样的常数在大 O 表示中无关紧要；因此平均情况运行时间是 O(log n)，与最坏情况运行时间相同。

## 标准库搜索函数

标准模板库在 <algorithm> 中提供操作，用于在已排序和未排序范围内查找元素。这些函数适用于前向迭代器、双向迭代器和随机访问迭代器（参见第 6.3 节）。

### 已排序范围的函数

以下函数各有两个版本。一个版本使用运算符 < 来比较项目。第二个版本（我们不予讨论）在末尾使用额外参数来提供比较函数。在每种情况下，两个迭代器 first 和 last 提供一个元素范围 [first..last)，其中包括从 *first 到但不包括 *last 的所有元素，且这些元素必须从小到大排序。

```
bool binary_search
(Iterator first, Iterator last, const Item& target);
```

```
Iterator lower_bound
(Iterator first, Iterator last, const Item& target);
```

```
Iterator upper_bound
(Iterator first, Iterator last, const Item& target);
```

binary_search 函数如果在已排序范围中找到指定值则返回 true，否则返回 false。

lower_bound 和 upper_bound 函数都返回范围 [first..last) 中的一个迭代器。

通常，lower_bound 返回的迭代器是指向范围 [first..last) 中目标第一次出现位置的迭代器。例如，假设我们序列中的元素是整数 2、4、6、7、9 和 11；如果我们的目标是数字 6，那么 lower_bound 将返回一个指向数字 6 第一次出现位置的迭代器。如果目标不在范围内，那么 lower_bound 返回的迭代器将指向第一个大于目标的项目。使用相同的序列（2、4、6、7、9、11）和目标 8，lower_bound 函数将返回一个指向数字 9 的迭代器。如果序列中的所有项目都小于目标，那么返回值将等于 last 迭代器。另一种看待 lower bound 迭代器的方式是，它是序列中最左侧的位置，在该位置之前可以插入目标，同时数字仍然保持有序。

upper_bound 返回的迭代器是指向第一个大于目标的项目的迭代器。在我们的示例序列（2、4、6、7、9、11）和目标 6 中，upper_bound 函数将返回一个指向数字 7 的迭代器。同样，如果找不到这样的元素，那么返回值是 last 迭代器。另一种看待 upper bound 迭代器的方式是，它是序列中最右侧的位置，在该位置之前可以插入目标，同时数字保持有序。

下面是另一个使用字符串向量的示例：

```
vector<string> pets;
// Put some strings into alphabetical order:
pets.push_back("cat");
pets.push_back("dog");
pets.push_back("dog");
pets.push_back("fish");
pets.push_back("snake");
pets.push_back("turtle");
```

向量现在包含六个字符串，按字母顺序排序：

| "cat" | "dog" | "dog" | "fish" | "snake" | "turtle" |

此时，我们可以找到 "dog" 的第一次出现以及所有 "dog" 之后的第一个项目，如下所示：

```
vector<string>::iterator first_dog =
    lower_bound(pets.begin(), pets.end(), "dog");
vector<string>::iterator after_dog =
    upper_bound(pets.begin(), pets.end(), "dog");
```

此时在代码中，*first_dog 将是 "dog" 的第一次出现，*after_dog 将是 "fish"。

顺便说一句，lower_bound 和 upper_bound 返回相同迭代器的唯一情况是目标不在已排序范围内。这两个函数使用的技术是二分查找，因此它们的行为保证在范围大小上是对数的。

### 未排序范围的函数

STL 的 find 和 count 函数适用于任何带有迭代器的 STL 序列类，无论序列是否已排序。请注意，一些容器（如 set 和 map）实现了它们自己的 find 和 count 函数版本。这些函数的原型是

```
difference_type count
(Iterator first, Iterator last, const Item& target);
iterator find
(Iterator first, Iterator last, const Item& target);
```

count 函数的返回类型是一种特殊的整数类型，允许计算机存储可能太大而无法用 int 存储的整数。count 函数的返回值是目标值在范围 [first..last) 中出现的次数。它使用 Item 类型的 == 运算符来确定项目是否等于目标。

find 函数返回一个指向目标第一次出现位置的迭代器。如果未找到目标，则返回 last 迭代器。find 和 count 函数可用于任何 STL 容器类或数组。甚至可以使用这些函数搜索 STL string 类，如图 12.3 所示。

### STL search 函数

名为 search 的 STL 函数可用于确定一个序列的副本（由两个迭代器 [target_first..target_last) 确定）是否作为连续片段出现在另一个序列（由另外两个迭代器 [first..last) 确定）的某个位置中。原型如下所示：

```
Iterator search(
    Iterator first, Iterator last,
    Iterator target_first, Iterator target_last
);
```

返回值是 [first..last) 中的一个迭代器，它是 [target_first..target_last) 副本出现位置的起始处。如果不存在这样的出现，则返回值是 last 迭代器。

### 图 12.3 将 find 函数与字符串一起使用

### 一个程序

```
#include <algorithm> // Provides the find function
#include <iostream> // Provides getline and cout
#include <string> // Provides the string class
using namespace std;

int main()
{
    string line;
    string::iterator i, where_is_e;

    cout << "Please enter a line of text: ";
    getline(cin, line);
    where_is_e = find(line.begin(), line.end(), 'e');

    cout << "You entered the following before entering an e: ";
    for (i = line.begin(); i != where_is_e; ++i)
        cout << *i;
    cout << endl;

    cout << "The rest of your input was: ";
    for (i = where_is_e; i != line.end(); ++i)
        cout << *i;
    cout << endl;

    return 0;
}
```

### 示例对话

请输入一行文本：Cyclops has just one eye.
在输入 e 之前，您输入了以下内容：Cyclops has just on
您其余的输入是：e eye.

