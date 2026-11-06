
```cpp
        {}
    bool operator()(int value) const
    {
        return value <= d_x;
    }
};
int main()
{
    int ia[] = {1, 3, 5, 7, 9, 10, 2, 8, 6, 4};
    int *split;

    split = partition(ia, ia + 10, LessThan(ia[9]));
    cout << "Last element <= 4 is ia[" << split - ia - 1 << "]\n";

    copy(ia, ia + 10, ostream_iterator<int>(cout, " "));
    cout << '\n';
}
/*
Displays:
    Last element <= 4 is ia[3]
    1 3 4 2 9 10 7 8 6 5
*/
```

### 19.1.38 prev_permutation

- 头文件：`<algorithm>`
- 函数原型：
  - `bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last);`
  - `bool prev_permutation(BidirectionalIterator first, BidirectionalIterator last, Comp comp);`
- 描述：
  - 第一个原型：确定给定范围 `[first, last)` 中元素序列的前一个排列。范围中的元素会重新排序，从而得到表示“更小”值的第一个排列（有关相反排序的示例，请参见 `next_permutation`（第 19.1.32 节））。如果发生了重新排序，则返回 `true`；如果没有发生重新排序，则返回 `false`；后者对应所提供的序列已经按照迭代器所指数据类型的 `operator<` 排好序的情况。
  - 第二个原型：使用二元谓词 `comp` 比较元素，确定给定范围 `[first, last)` 中元素序列的前一个排列。范围中的元素会重新排序。如果发生了重新排序，则返回 `true`；如果没有发生重新排序，则返回 `false`；后者对应原始序列已经使用二元谓词 `comp` 比较两个元素而排好序的情况。
- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <cstring>
#include <iterator>
using namespace std;

class CaseString
```

- 第二个原型：使用 `rand` 随机数生成器对范围 `[first, last)` 中的元素进行随机重排，该生成器应返回一个 `int`，其范围是 `[0, remaining)`，其中 `remaining` 作为参数传递给 `rand` 函数对象的 `operator()`。或者，随机数生成器可以是一个函数，它期望一个 `int` 类型的 remaining 参数，并返回一个位于 `[0, remaining)` 范围内的 `int`。注意，当使用函数对象时，它不能是匿名对象。示例中的函数使用 *Press 等（1992）《C 语言数值算法：科学计算的艺术》*（纽约：剑桥大学出版社，第 2 版，第 277 页）中概述的过程。
- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <time.h>
#include <iterator>
using namespace std;

int randomValue(int remaining)
{
    return rand() % remaining;
}
class RandomGenerator
{
    public:
        RandomGenerator()
        {
            srand(time(0));
        }
        int operator()(int remaining) const
        {
            return randomValue(remaining);
        }
};
void show(string *begin, string *end)
{
    copy(begin, end, ostream_iterator<string>(cout, " "));
    cout << "\n\n";
}
int main()
{
    string words[] =
        { "kilo", "lima", "mike", "november", "oscar", "papa"};
    size_t const size = sizeof(words) / sizeof(string);

    cout << "Using Default Shuffle:\n";
    random_shuffle(words, words + size);
    show(words, words + size);

    cout << "Using RandomGenerator:\n";
    RandomGenerator rg;
    random_shuffle(words, words + size, rg);
    show(words, words + size);

    srand(time(0) << 1);
    cout << "Using the randomValue() function:\n";
    random_shuffle(words, words + size, randomValue);
    show(words, words + size);
}
/*
Displays (for example):
    Using Default Shuffle:
        lima oscar mike november papa kilo

    Using RandomGenerator:
        kilo lima papa oscar mike november

    Using the randomValue() function:
        mike papa november kilo oscar lima
*/
```

### 19.1.40 remove

- 头文件：`<algorithm>`
- 函数原型：
  - `ForwardIterator remove(ForwardIterator first, ForwardIterator last, Type const &value);`
- 描述：
  - 由 `[first, last)` 指向的范围中的元素会被重新排序，使得所有不等于 `value` 的值都放在该范围的开头。返回的前向迭代器指向重新排序后第一个可被移除的元素。范围 `[returnvalue, last)` 称为该算法的剩余部分。注意，剩余部分可能包含不同于 `value` 的元素，但这些元素可以安全地移除，因为此类元素也存在于范围 `[first, returnvalue)` 中。这种重复是算法将元素复制（而不是移动）到新位置的结果。该函数使用迭代器所指数据类型的 `operator==` 来确定要移除哪些元素。
- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <iterator>
using namespace std;

int main()
{
    string words[] =
        { "kilo", "alpha", "lima", "mike", "alpha", "november", "alpha",
          "alpha", "alpha", "papa", "quebec" };
    string *removed;
    size_t const size = sizeof(words) / sizeof(string);

    cout << "Removing all \"alpha\"s:\n";
    removed = remove(words, words + size, "alpha");
    copy(words, removed, ostream_iterator<string>(cout, " "));
    cout << '\n';
    cout << "Leftover elements are:\n";
    copy(removed, words + size, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
Displays:
              Removing all "alpha"s:
              kilo lima mike november papa quebec
    Leftover elements are:
    alpha alpha alpha papa quebec
*/
```

### 19.1.41 remove_copy

- 头文件：`<algorithm>`
- 函数原型：
  - `OutputIterator remove_copy(InputIterator first, InputIterator last, OutputIterator result, Type const &value);`
- 描述：
  - 由 `[first, last)` 指向的范围中与 value 不匹配的元素会被复制到范围 `[result, returnvalue)`，其中 `returnvalue` 是该函数返回的值。范围 `[first, last)` 不会被修改。该函数使用迭代器所指数据类型的 `operator==` 来确定哪些元素不复制。
- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <functional>
#include <iterator>
using namespace std;

int main()
{
    string words[] =
        { "kilo", "alpha", "lima", "mike", "alpha", "november", "alpha",
            "oscar", "alpha", "alpha", "papa", "quebec" };
    size_t const size = sizeof(words) / sizeof(string);
    string remaining
        [
            size -
            count_if
            (
                words, words + size,
                bind2nd(equal_to<string>(), string("alpha"))
            )
        ];
    string *returnvalue =
        remove_copy(words, words + size, remaining, "alpha");

    cout << "Removing all \"alpha\"s:\n";
    copy(remaining, returnvalue, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        Removing all "alpha"s:
        kilo lima mike november oscar papa quebec
*/
```

### 19.1.42 remove_copy_if

- 头文件：`<algorithm>`

- 函数原型：

```cpp
OutputIterator remove_copy_if(InputIterator first, InputIterator last,
    OutputIterator result, UnaryPredicate pred);
```

- 描述：

由 `[first, last)` 指向的范围中，一元谓词 `pred` 返回 true 的元素会从结果副本中移除。所有其他元素会被复制到范围 `[result, returnvalue)`，其中 returnvalue 是该函数返回的值。范围 `[first, last)` 不会被修改。

- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <functional>
#include <iterator>
using namespace std;

int main()
{
    string words[] =
        { "kilo", "alpha", "lima", "mike", "alpha", "november", "alpha",
          "oscar", "alpha", "alpha", "papa", "quebec" };
    size_t const size = sizeof(words) / sizeof(string);
    string remaining[
                    size -
                    count_if
                    (
                        words, words + size,
                        bind2nd(equal_to<string>(), "alpha")
                    )
                  ];
    string *returnvalue =
        remove_copy_if
        (
            words, words + size, remaining,
            bind2nd(equal_to<string>(), "alpha")
        );

    cout << "Removing all \"alpha\"s:\n";
    copy(remaining, returnvalue, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        Removing all "alpha"s:
        kilo lima mike november oscar papa quebec
*/
```

### 19.1.43 remove_if

- 头文件：`<algorithm>`
