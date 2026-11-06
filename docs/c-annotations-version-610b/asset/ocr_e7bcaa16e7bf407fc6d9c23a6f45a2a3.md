```
```cpp
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
```

# 19.1.23 iter_swap

+   - Header file: `<algorithm>`
+   - Function prototype:
+     - `void iter_swap(ForwardIterator1 iter1, ForwardIterator2 iter2);`
+   - Description:
+     - The elements pointed to by iter1 and iter2 are swapped.
+   - Example:

```
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
```