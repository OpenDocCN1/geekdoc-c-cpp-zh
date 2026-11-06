
```cpp
#include <iostream>
#include <string>
#include <cstring>
#include <iterator>
using namespace std;

bool caseless(string const &left, string const &right)
{
    return strcasecmp(left.c_str(), right.c_str()) < 0;
}
int main()
{
    string set1[] = { "kilo", "lima", "mike", "november",
                      "oscar", "papa", "quebec" };
    string set2[] = { "papa", "quebec", "romeo"};
    string result[7];

    copy(result,
         set_symmetric_difference(set1, set1 + 7, set2, set2 + 3,
                                  result),
         ostream_iterator<string>(cout, " "));
    cout << '\n';

    string set3[] = { "PAPA", "QUEBEC", "ROMEO"};

    copy(result,
         set_symmetric_difference(set1, set1 + 7, set3, set3 + 3,
                                  result, caseless),
         ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        kilo lima mike november oscar romeo
        kilo lima mike november oscar ROMEO
*/
```

### 19.1.57 set_union

- 头文件：`<algorithm>`
- 函数原型：
  - `OutputIterator set_union(InputIterator1 first, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, OutputIterator result);`
  - `OutputIterator set_union(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, OutputIterator result, Compare comp);`
- 描述：
  - 第一个原型：返回一个有序序列，其中包含出现在范围 `[first1, last1)` 或范围 `[first2, last2)` 中，或同时出现在两个范围中的元素；该序列从 `result` 开始，到该函数返回的 `OutputIterator` 结束。两个范围中的元素必须已经使用迭代器所指向数据类型的 `operator<` 进行排序。注意，在最终范围中每个元素只出现一次。
  - 第二个原型：返回一个有序序列，其中包含出现在范围 `[first1, last1)` 或范围 `[first2, last2)` 中，或同时出现在两个范围中的元素；该序列从 `result` 开始，到该函数返回的 `OutputIterator` 结束。两个范围中的元素必须已经使用 comp 函数对象进行排序。注意，在最终范围中每个元素只出现一次。

- 示例：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <cstring>
#include <iterator>
using namespace std;

bool caseless(string const &left, string const &right)
{
    return strcasecmp(left.c_str(), right.c_str()) < 0;
}
int main()
{
    string set1[] = { "kilo", "lima", "mike", "november",
                      "oscar", "papa", "quebec" };
    string set2[] = { "papa", "quebec", "romeo" };
    string result[8];

    copy(result,
         set_union(set1, set1 + 7, set2, set2 + 3, result),
         ostream_iterator<string>(cout, " "));
    cout << '\n';

    string set3[] = { "PAPA", "QUEBEC", "ROMEO" };

    copy(result,
         set_union(set1, set1 + 7, set3, set3 + 3, result, caseless),
         ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        kilo lima mike november oscar papa quebec romeo
        kilo lima mike november oscar papa quebec ROMEO
*/
```

### 19.1.58 sort

- 头文件：`<algorithm>`
- 函数原型：
  - `void sort(RandomAccessIterator first, RandomAccessIterator last);`
  - `void sort(RandomAccessIterator first, RandomAccessIterator last, Compare comp);`
- 描述：
  - 第一个原型：范围 `[first, last)` 中的元素使用迭代器所指向数据类型的 `operator<` 按升序排序。
  - 第二个原型：范围 `[first, last)` 中的元素使用 `comp` 函数对象比较元素，并按升序排序。如果其第一个参数在排序序列中应放在第二个参数之前，则二元谓词 `comp` 应返回 true。

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
    string words[] = {"november", "kilo", "mike", "lima",
                      "oscar", "quebec", "papa"};

    sort(words, words + 7);
    copy(words, words + 7, ostream_iterator<string>(cout, " "));
    cout << '\n';

    sort(words, words + 7, greater<string>());
    copy(words, words + 7, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
/*
    Displays:
        kilo lima mike november oscar papa quebec
        quebec papa oscar november mike lima kilo
*/
```

### 19.1.59 stable_partition

- 头文件：`<algorithm>`
- 函数原型：
  - `BidirectionalIterator stable_partition(BidirectionalIterator first, BidirectionalIterator last, UnaryPredicate pred);`
- 描述：
  - 范围 `[first, last)` 中所有使一元谓词 `pred` 求值为 `true` 的元素都会被放在求值为 `false` 的元素之前。除了这种重新排序之外，谓词求值为 `false` 的所有元素的相对顺序，以及谓词求值为 `true` 的所有元素的相对顺序都保持不变。返回值指向分区范围中使 `pred` 求值为 `true` 的最后一个元素之后的位置。
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
    int org[] = {1, 3, 5, 7, 9, 10, 2, 8, 6, 4};
    int ia[10];
    int *split;

    copy(org, org + 10, ia);
    split = partition(ia, ia + 10, bind2nd(less_equal<int>(), ia[9]));
    cout << "Last element <= 4 is ia[" << split - ia - 1 << "]\n";

    copy(ia, ia + 10, ostream_iterator<int>(cout, " "));
    cout << '\n';

    copy(org, org + 10, ia);
    split = stable_partition(ia, ia + 10,
                             bind2nd(less_equal<int>(), ia[9]));

    cout << "Last element <= 4 is ia[" << split - ia - 1 << "]\n";

    copy(ia, ia + 10, ostream_iterator<int>(cout, " "));
    cout << '\n';
}
/*
   Displays:
      Last element <= 4 is ia[3]
      1 3 4 2 9 10 7 8 6 5
      Last element <= 4 is ia[3]
      1 3 2 4 5 7 9 10 8 6
*/
```

### 19.1.60 stable_sort

- 头文件：`<algorithm>`
- 函数原型：
  - `void stable_sort(RandomAccessIterator first, RandomAccessIterator last);`
  - `void stable_sort(RandomAccessIterator first, RandomAccessIterator last, Compare comp);`
- 描述：
  - 第一个原型：范围 `[first, last)` 中的元素使用迭代器所指向数据类型的 `operator<` 按升序进行稳定排序：相等元素的相对顺序保持不变。
  - 第二个原型：范围 `[first, last)` 中的元素使用 `comp` 二元谓词比较元素，并按升序进行稳定排序。如果其第一个参数在排序后的元素集合中应放在第二个参数之前，则该谓词应返回 `true`。
- 示例（下方带注释）：

```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <vector>
#include <iterator>
using namespace std;

struct Pss: public pair<string, string>                         // 1
{
    Pss(string const &s1, string const &s2)
    :
        pair<string, string>(s1, s2)
    {}
};
ostream &operator<<(ostream &out, Pss const &p)                 // 2
{
    return out << "     " << p.first << " " << p.second << '\n';
}
class Sortby
{
    string Pss::*d_field;
public:
    Sortby(string Pss::*field)                                      // 3
        :
        d_field(field)
    {}
    bool operator()(Pss const &p1, Pss const &p2) const             // 4
    {
        return p1.*d_field < p2.*d_field;
    }
};
int main()
{
    vector<Pss> namecity;                                           // 5

    namecity.push_back(Pss("Hampson",  "Godalming"));
    namecity.push_back(Pss("Moran",    "Eugene"));
    namecity.push_back(Pss("Goldberg", "Eugene"));
    namecity.push_back(Pss("Moran",    "Godalming"));
    namecity.push_back(Pss("Goldberg", "Chicago"));
    namecity.push_back(Pss("Hampson",  "Eugene"));

    sort(namecity.begin(), namecity.end(), Sortby(&Pss::first));    // 6

    cout << "sorted by names:\n";
    copy(namecity.begin(), namecity.end(), ostream_iterator<Pss>(cout));

                                                            // 7
    stable_sort(namecity.begin(), namecity.end(), Sortby(&Pss::second));

    cout << "sorted by names within sorted cities:\n";
    copy(namecity.begin(), namecity.end(), ostream_iterator<Pss>(cout));
}
/*
    Displays:
        sorted by names:
            Goldberg Eugene
            Goldberg Chicago
            Hampson Godalming
            Hampson Eugene
            Moran Eugene
            Moran Godalming
        sorted by names within sorted cities:
            Goldberg Chicago
            Goldberg Eugene
            Hampson Eugene
            Moran Eugene
            Hampson Godalming
            Moran Godalming

*/
```

注意，该示例实现了一个常见问题的解决方案：如何使用多个
