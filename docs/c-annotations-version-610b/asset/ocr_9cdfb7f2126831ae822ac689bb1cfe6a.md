```
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
```

# 19.1.57  set_union

+   - Header file: `<algorithm>`
+   - Function prototypes:
+     - `OutputIterator set_union(InputIterator1 first, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, OutputIterator result);`
+     - `OutputIterator set_union(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, OutputIterator result, Compare comp);`
+   - Description:
+     - The first prototype: a sorted sequence of the elements that are present in either the range `[first1, last1)` or the range `[first2, last2)` or in both ranges is returned, starting at `result`, and ending at the `OutputIterator` returned by the function. The elements in the two ranges must have been sorted using `operator<` of the data type to which the iterators point. Note that in the final range each element appears only once.
+     - The second prototype: a sorted sequence of the elements that are present in either the range `[first1, last1)` or the range `[first2, last2)` or in both ranges is returned, starting at `result`, and ending at the `OutputIterator` returned by the function. The elements in