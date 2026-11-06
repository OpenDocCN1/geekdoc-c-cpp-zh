```
(
    search_n(range1, range1 + 8, 2, 4),
    range1 + 8,
    ostream_iterator<int>(cout, " ")
);
cout << '\n';

copy
(
    search_n(range1, range1 + 8, 2, 4, eqInt),
    range1 + 8,
    ostream_iterator<int>(cout, " ")
);
cout << '\n';
}
/*
    Displays:
        4 4
        -4 -4 -6 -8 2 4 4
*/
```

# 19.1.54  set_difference

+   - Header file: `<algorithm>`

+   - Function prototypes:
+     - `OutputIterator set_difference(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, OutputIterator result);`
+     - `OutputIterator set_difference(InputIterator1 first1, InputIterator1 last1, InputIterator2 first2, InputIterator2 last2, OutputIterator result, Compare comp);`

+   - Description:
+     - The first prototype: a sorted sequence of the elements pointed to by the range `[first1, last1)` that are not present in the range `[first2, last2)` is returned, starting at `result`, and ending at the `OutputIterator` returned by the function. The elements in the two ranges must have been sorted using `operator<` of the data type to which the iterators point.
+     - The second prototype: a sorted sequence of the elements pointed to by the range `[first1, last1)` that are not present in the range `[first2, last2)` is returned, starting at `result`, and ending at the `OutputIterator` returned by the function. The elements in the two ranges must have been sorted using the `comp` function object.

+   - Example:

```
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
```