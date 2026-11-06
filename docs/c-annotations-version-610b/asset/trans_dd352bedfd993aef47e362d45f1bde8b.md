
## 19.1. 泛型算法

```cpp
using namespace std;

class NaturalSquares
{
    size_t d_newsqr;
    size_t d_last;

    public:
        NaturalSquares(): d_newsqr(0), d_last(0)
        {}
        size_t operator()()
        {                         // using: (a + 1)^2 == a^2 + 2*a + 1
            return d_newsqr += (d_last++ << 1) + 1;
        }
};
int main()
{
    vector<size_t>    uv(10);

    generate_n(uv.begin(), 5, NaturalSquares());

    copy(uv.begin(), uv.end(), ostream_iterator<int>(cout, " "));
    cout << '\n';
}
// Displays:   1 4 9 16 25 0 0 0 0 0
```

### 19.1.20 includes

- 头文件：`<algorithm>`
- 函数原型：
  - `bool includes(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2);`
  - `bool includes(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, Compare comp);`
- 描述：
  - 第一个原型：范围 `[first1, last1)` 和 `[first2, last2)` 所隐含的两个元素序列都应已使用迭代器所指数据类型的 `operator<` 排序。如果第二个序列 `[first2, last2)` 中的每个元素都包含在第一个序列 `[first1, last1)` 中（第二个范围是第一个范围的子集），则函数返回 `true`。
  - 第二个原型：范围 `[first1, last1)` 和 `[first2, last2)` 所隐含的两个元素序列都应已使用 `comp` 函数对象排序。如果第二个序列 `[first2, last2)` 中的每个元素都包含在第一个序列 `[first1, last1)` 中（第二个范围是第一个范围的子集），则函数返回 `true`。
- 示例：

```cpp
#include <algorithm>
#include <string>
#include <cstring>
#include <iostream>
using namespace std;

class CaseString
{
public:
    bool operator()(string const &first,
                    string const &second) const
    {
        return !strcasecmp(first.c_str(), second.c_str());
    }
};
int main()
{
    string first1[] =
    {
        "alpha", "bravo", "charley", "delta", "echo",
        "foxtrot", "golf", "hotel"
    };
    string first2[] =
    {
        "Alpha", "bravo", "Charley", "delta", "Echo",
        "foxtrot", "Golf", "hotel"
    };
    string second[] =
    {
        "charley", "foxtrot", "hotel"
    };
    size_t n = sizeof(first1) / sizeof(string);

    cout << "The elements of `second` are " <<
        (includes(first1, first1 + n, second, second + 3) ? "" : "not")
        << " contained in the first sequence:\n"
        "second is a subset of first1\n";

    cout << "The elements of `first1` are " <<
        (includes(second, second + 3, first1, first1 + n) ? "" : "not")
        << " contained in the second sequence\n";

    cout << "The elements of `second` are " <<
        (includes(first2, first2 + n, second, second + 3) ? "" : "not")
        << " contained in the first2 sequence\n";

    cout << "Using case-insensitive comparison,\n"
        "the elements of `second` are "
        <<
        (includes(first2, first2 + n, second, second + 3, CaseString()) ?
            "" : "not")
        << " contained in the first2 sequence\n";
}
/*
    Displays:
        The elements of `second` are  contained in the first sequence:
        second is a subset of first1
        The elements of `first1` are not contained in the second sequence
        The elements of `second` are not contained in the first2 sequence
        Using case-insensitive comparison,
        the elements of `second` are  contained in the first2 sequence
*/
```

### 19.1.21 inner_product

- 头文件：`<numeric>`
- 函数原型：
  - `Type inner_product(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, Type init);`
  - `Type inner_product(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, Type init, BinaryOperator1 op1, BinaryOperator2 op2);`
- 描述：
  - 第一个原型：范围 `[first1, last1)` 所隐含的元素与从 `first2` 指向的元素开始、数量相同的元素，其所有两两乘积之和被添加到 `init`，并返回该总和。该函数使用迭代器所指数据类型的 `operator+` 和 `operator*`。
  - 第二个原型：对范围 `[first1, last1)` 所隐含的元素以及从 `first2` 指向的元素开始、数量相同的元素，应用二元操作符 `op1` 替代默认加法操作符，应用二元操作符 `op2` 替代默认乘法操作符。二元操作符调用的结果被添加到 `init`，并返回 `init` 的最终值。
- 示例：

```cpp
#include <numeric>
#include <algorithm>
#include <iterator>
#include <iostream>
#include <string>
using namespace std;

class Cat
{
    std::string  d_sep;
public:
    Cat(string const &sep)
        :
            d_sep(sep)
    {}
    string operator()
        (string const &s1, string const &s2) const
    {
        return s1 + d_sep + s2;
    }
};
int main()
{
        size_t ia1[] = {1, 2, 3, 4, 5, 6, 7};
        size_t ia2[] = {7, 6, 5, 4, 3, 2, 1};
        size_t init = 0;

        cout << "The sum of all squares in ";
        copy(ia1, ia1 + 7, ostream_iterator<size_t>(cout, " "));
        cout << " is " <<
            inner_product(ia1, ia1 + 7, ia1, init) << '\n';

        cout << "The sum of all cross-products in ";
        copy(ia1, ia1 + 7, ostream_iterator<size_t>(cout, " "));
        cout << "and ";
        copy(ia2, ia2 + 7, ostream_iterator<size_t>(cout, " "));
        cout << " is " <<
            inner_product(ia1, ia1 + 7, ia2, init) << '\n';

        string names1[] = {"Frank", "Karel", "Piet"};
        string names2[] = {"Brokken", "Kubat", "Plomp"};

        cout << "A list of all combined names in ";
        copy(names1, names1 + 3, ostream_iterator<string>(cout, " "));
        cout << "and\n";
        copy(names2, names2 + 3, ostream_iterator<string>(cout, " "));
        cout << "is:" <<
            inner_product(names1, names1 + 3, names2, string("\t"),
                Cat("\n\t"), Cat(" ")) <<
            '\n';
}
/*
Displays:
    The sum of all squares in 1 2 3 4 5 6 7 is 140
    The sum of all cross-products in 1 2 3 4 5 6 7 and 7 6 5 4 3 2 1 is 84
    A list of all combined names in Frank Karel Piet and
    Brokken Kubat Plomp is:
        Frank Brokken
        Karel Kubat
        Piet Plomp
*/
```

### 19.1.22 inplace_merge

- 头文件：`<algorithm>`
- 函数原型：
  - `void inplace_merge(BidirectionalIterator first, BidirectionalIterator middle, BidirectionalIterator last);`
  - `void inplace_merge(BidirectionalIterator first, BidirectionalIterator middle, BidirectionalIterator last, Compare comp);`
- 描述：
  - 第一个原型：将两个（已排序的）范围 `[first, middle)` 和 `[middle, last)` 合并，保持排序的列表（使用迭代器所指数据类型的 `operator<`）。最终序列存储在范围 `[first, last)` 中。
  - 第二个原型：将两个（已排序的）范围 `[first, middle)` 和 `[middle, last)` 合并，保持排序的列表（使用二元比较操作符 `comp` 的布尔结果）。最终序列存储在范围 `[first, last)` 中。
- 示例：

```cpp
#include <algorithm>
#include <string>
#include <cstring>
#include <iterator>
#include <iostream>
using namespace std;

class CaseString
{
    public:
        bool operator()(string const &first, string const &second) const
        {
            return strcasecmp(first.c_str(), second.c_str()) < 0;
        }
};

int main()
{
    string range[] =
    {
        "alpha", "charley", "echo", "golf",
        "bravo", "delta", "foxtrot",
    };

    inplace_merge(range, range + 4, range + 7);
    copy(range, range + 7, ostream_iterator<string>(cout, " "));
    cout << '\n';

    string range2[] =
    {
        "ALFA", "CHARLEY", "DELTA", "foxtrot", "hotel",
        "bravo", "ECHO", "GOLF"
    };

    inplace_merge(range2, range2 + 5, range2 + 8, CaseString());
    copy(range2, range2 + 8, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        alpha bravo charley delta echo foxtrot golf
        ALFA bravo CHARLEY DELTA ECHO foxtrot GOLF hotel
*/
```

### 19.1.23 iter_swap

- 头文件：`<algorithm>`
- 函数原型：
  - `void iter_swap(ForwardIterator1 iter1, ForwardIterator2 iter2);`
- 描述：
  - `iter1` 和 `iter2` 所指向的元素被交换。
- 示例：

```cpp
#include <algorithm>
#include <iterator>
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string first[] = {"alpha", "bravo", "charley"};
    string second[] = {"echo", "foxtrot", "golf"};
    size_t const n = sizeof(first) / sizeof(string);

    cout << "Before:\n";
    copy(first, first + n, ostream_iterator<string>(cout, " "));
    cout << '\n';
    copy(second, second + n, ostream_iterator<string>(cout, " "));
    cout << '\n';
```

