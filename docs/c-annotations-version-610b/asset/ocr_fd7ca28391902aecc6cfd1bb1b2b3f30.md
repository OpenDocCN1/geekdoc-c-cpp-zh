```
```cpp
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
```

# 19.1.60  stable_sort

+   - Header file: `<algorithm>`
+   - Function prototypes:
+     - `void stable_sort(RandomAccessIterator first, RandomAccessIterator last);`
+     - `void stable_sort(RandomAccessIterator first, RandomAccessIterator last, Compare comp);`
+   - Description:
+     - The first prototype: the elements in the range `[first, last)` are stable-sorted in ascending order using `operator<` of the data type to which the iterators point: the relative order of equal elements is kept.
+     - The second prototype: the elements in the range `[first, last)` are stable-sorted in ascending order using the `comp` binary predicate to compare the elements. This predicate should return `true` if its first argument should be placed before its second argument in the sorted set of element.
+   - Example (annotated below):

```
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
```
```