
```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

bool caseString(string const &str, string const &second)
{
    return strcasecmp(str.c_str(), second.c_str()) < 0;
}

void compare(string const &word1, string const &word2)
{
    cout << '`' << word1 << '` is " << " <<
    (
        lexicographical_compare(word1.begin(), word1.end(),
        word2.begin(), word2.end()) ?
        "before " : "beyond or at "
    )
    word2 << " in the alphabet\n";
}

int main(int argc, char **argv)
{
    string word1 = "hello";
    string word2 = "help";
    bool fun = argc == 1;
    char const *where = fun ? "last\n" : "first\n";

    if (argc > 1) {
        compare(word1, word2);
        compare(word1, word1);
        compare(word2, word1);
    } else {
        string one[] = {"alpha", "bravo", "charley"};
        string two[] = {"ALPHA", "BRAVO", "DELTA"};
        // 此处省略部分逻辑以匹配原文结构，实际展示case-insensitive比较逻辑
    }
}
```

*（注：由于原文文本在示例处存在部分逻辑错乱和重复，此处已根据上下文和 Markdown 逻辑进行了结构化翻译）*

## 19.1.32 `max_element`/`min_element`/`minmax_element`

- 头文件：`<algorithm>`

- 函数原型：

  - `ForwardIterator max_element(ForwardIterator first, ForwardIterator last);`

  - `ForwardIterator max_element(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);`

  - `ForwardIterator min_element(ForwardIterator first, ForwardIterator last);`

  - `ForwardIterator min_element(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);`

  - `pair<ForwardIterator, ForwardIterator> min_element(ForwardIterator first, ForwardIterator last);`

  - `pair<ForwardIterator, ForwardIterator> min_element(ForwardIterator first, ForwardIterator last, BinaryPredicate pred);`

- 描述：

  - 第一个原型：返回迭代器范围 `[first, last]` 中最大元素的迭代器。使用迭代器所指数据类型的运算符决定哪个元素是最大的。

  - 第二个原型：不是使用 `operator<`，而是使用二元谓词 `pred` 对从范围 `[first, last]` Reach 的元素进行比较。返回与其他元素比较时 `pred` 返回 `true` 次越多的元素。

  - 第二个和第四个原型分别与第一个、第二个原型相同，使用 `std::min_element` 代替 `std::max_element`，返回迭代器范围 `[first, last)` 内最小元素的迭代器。

  - 最后两个原型分别与第一个、第二个原型相同，返回 `std::pair` 对象，其第一个成员包含 `min` 通用算法返回的迭代器，第二个成员包含 `max` 通用算法返回的迭代器。

- 示例：

```cpp
#include <algorithm>
#include <iostream>
using namespace std;

int main()
{
    int v[] = {1, 5, 2, 4, 3};
    cout << "max: " << *max_element(v, v + 5) << endl;
    cout << "min: " << *min_element(v, v + 5) << endl;
    auto res = minmax_element(v, v + 5);
    cout << "min: " << *res.first << ", max: " << *res.second << endl;
    return 0;
}
```

## 19.1. 通用算法

```cpp
bool absCompare(int first, int second)
{
    return abs(first) < abs(second);
}
```

```cpp
int *maxMin(bool high, int *begin, int *end)
{
    return high ? max_element(begin, end) : min_element(begin, end);
}
```

```cpp
int *maxMin(bool high, int *begin, int *end, bool (*comp) (int, int))
{
    return high ? max_element(begin, end, comp)
               : min_element(begin, end, comp);
}
```

```cpp
// 无参数：调用 max_element，否则调用 min_element
int main(int argc, char **argv)
{
    bool max = argc == 1;
    char const *type = max ? "max" : "min";
    int ia[] = {-4, 7, -2, 10, -12};

    cout << "The " << type << ": int value is " 
         << max_element(ia, ia + 5) << "\n";
    cout << "The. absolute value is " 
         << min_element(ia, ia + 5, absCompare) << "\n";
}
// 不带参数调用时显示：
// The max. int value is 10
// The max. absolute int value is -12
// 否则：
// The minimum int value is -12
// The minimum absolute int value is -12
```

## 19.1.33 `merge`

- 头文件：`<algorithm>`

- 函数原型：

    - `OutputIterator merge([ExecPol], InputIterator first1,`

      `InputIterator last1, InputIterator first2, InputIterator last2,`

      `OutputIterator result);`

    - `OutputIterator merge([ExecPol], InputIterator first1,`

      `InputIterator last1, InputIterator first2, InputIterator last2,`

      `OutputIterator result, Compare comp);`

- 描述：

    - 第一个原型：将两个（有序的）范围 `[first1, last1]` 和 `[first2, last2]`

      合并，并保持一个有序列表（使用迭代器指向的数据类型的运算符`<`）。

      最终的序列存储在从 `result` 开始、到函数返回的 `OutputIterator` 

      之前结束的范围内。

    - 第二个原型：将两个（有序的）范围 `[first1, last1)` 和 `[first2, last2)`

      合并，并保持一个有序列表（使用二元比较运算符 `comp` 的布尔结果）。

      最终的序列存储在从 `result` 开始、到函数返回的 `OutputIterator`

      之前结束的范围内。

- 示例：

```cpp
#include <algorithm>
#include <string>
#include <cstring>
#include <iterator>
#include <iostream>
using namespace std;

bool strcasecmp(string const &first, string const &second)
{
    return strcasecmp(first.c_str(), second.c_str()) < 0;
}

int main()
{
    string range1[] = // 5个元素
        { "bravo", "foxtrot", "hotel", "zulu", "alpha" };
    string range2[] = // 4个元素
        { "delta", "echo", "golf", "romeo" };
    string result[5 + 4];

    copy(result,
        merge(range1, range1 + 5, range2, range2 + 4, result,
             ostream_iterator<string>(cout, " ")));
    cout << '\n';

    string range3[] = 
        { "ALPHA", "bravo", "foxtrot", "HOTEL", "ZULU" };
    string range4[] = { "delta", "ECHO", "GOLF", "romeo" };

    copy(result,
        merge(range3, range3 + 5, range4, range4 + 4, result,
             strcasecmp),
             ostream_iterator<string>(cout, " ")));
    cout << '\n';

    // 显示：
    alpha delta echo foxtrot romeo zulu
    ALPHA delta ECHO foxtrot GOLF HOTEL romeo ZULU
}
```

## 19.1.34 `minmax`

- 头文件：`<algorithm>`

- 函数原型：
    - `pair<Type const, Type const> minmax(Type const &t1, Type const &t2);`
    - `pair<Type const, Type const> minmax(Type const &t1, Type const &t2, BinaryPred pred);`
    - `pair<Type const &, Type const &> minmax(std::initializer_list<Type> values);`
    - `pair<Type const &, Type const &> minmax(std::initializer_list<Type> values, BinaryPred);`

- 描述：
    - 第一个原型：返回一个 `std::pair`，其 `first` 和 `second` 成员分别包含参数的较小较大值（使用 `Type` 的 `operator<`）。
    - 第二个原型：与第一个原型相同，但如果 `pred(t1, t2)` 返回 `true`，则 `t1` 是较小的元素。
    - 第三个和第四个原型的作用与第一、二原型相同，但返回提供的 `iterator_range` 对象中最小和最大的值。

- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <functional>
using namespace std;

int main() {
    vector<size_t> uv(10);
    auto values = minmax(5, 2, less<int>());
    cout << values.first << " is smaller than " << values.second << '\n';
}
// 显示：2 is smaller than 5
```

## 19.1.35 `mismatch`

- 头文件：`<algorithm>`

- 函数原型：
    - `pair<InputIterator1, InputIterator2> mismatch([ExecPol], InputIterator first1, InputIterator last1, InputIterator first2);`
    - `pair<InputIterator1, InputIterator2> mismatch([ExecPol], InputIterator first1, InputIterator last1, InputIterator first2, Compare comp);`

- 描述：
    - 第一个原型：使用迭代器指向的数据类型的相等运算符比较从 `first1` 和 `first2` 开始的序列。如果元素不同或到达末尾则停止。返回一个包含结束位置的 `pair`。第二个序列可能比第一个更多的元素。
    - 第二个原型：使用二元比较运算符 `comp` 比较 `first1` 和 `first2` 开始的序列。如果元素不同或到达末尾则停止。返回一个包含结束位置的 `pair`。第二个序列可能比第一个更多的元素。

- 示例：

```cpp
#include <algorithm>
#include <string>
#include <cstring>
#include <iostream>
#include <utility>
using namespace std;

bool caseString(string const &first, string const &second)
{
    return strcasecmp(first.c_str(), second.c_str()) == 0;
}

int main() {
    string range1[] = { "alpha", "bravo", "foxtrot", "hotel", "zulu" };
    string range2[] = { "delta", "echo", "golf", "romeo" };
    auto p1 = mismatch(range1, range1 + 5, range2, range2 + 4);
    cout << "First mismatch: " << *p1.first << " and " << *p1.second << endl;

    string range3[] = { "ALPHA", "bravo", "foxtrot", "HOTEL", "ZULU" };
    string range4[] = { "delta", "ECHO", "GOLF", "romeo" };
    auto p2 = mismatch(range3, range3 + 5, range4, range4 + 4, caseString);
    cout << "Second mismatch: " << *p2.first << " and " << *p2.second << endl;
}
```

## 19.1.36 `move` / `move_backward`

- 头文件：`<algorithm>`

- 函数原型：
    - `OutputIterator move([ExecPol], InputIterator first, InputIterator last, OutputIterator dest);`
    - `BidirIterator move_backward(BidirIterator first, BidirIterator last, BidirIterator dest);`

- 描述：
    - 第一个原型：将 `[first, last)` 范围内的所有元素移动到从 `dest` 开始的范围，返回指向 `dest` 开始范围中最后一个元素之后的迭代器。
    - 第二个原型：将 `[first, last)` 范围内的所有元素反序移动到以 `dest` 结束的范围，返回指向以 `dest` 结束范围起始的迭代器。

- 示例：

```cpp
#include <algorithm>
#include <string>
#include <iostream>
using namespace std;

int main() {
```
