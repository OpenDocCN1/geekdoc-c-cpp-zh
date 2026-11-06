```
```cpp
cout << "Sequence: ";
copy (ia, ia + 3, ostream_iterator<int>(cout, " "));
cout << '\n';

cout << "15 can be inserted before " <<
        *lower_bound(ia, ia + 3, 15, greater<int>()) << '\n';
cout << "35 can be inserted before " <<
        (lower_bound(ia, ia + 3, 35, greater<int>()) == ia ?
                         "the first element" : "???") << '\n';
}
/*
 Displays:
        Sequence: 10 20 30
        15 can be inserted before 20
        35 can be inserted after the last element
        Sequence: 30 20 10
        15 can be inserted before 10
        35 can be inserted before the first element
*/
```
```

# 19.1.26  max

+   - Header file: `<algorithm>`
+   - Function prototypes:
+     - `Type const &max(Type const &one, Type const &two);`
+     - `Type const &max(Type const &one, Type const &two, Comparator comp);`
+   - Description:
+     - The first prototype: the larger of the two elements one and two is returned, using the `operator>` of the data type to which the iterator points to determine which element is the larger one.
+     - The second prototype: one is returned if the binary predicate `comp(one, two)` returns true, otherwise two is returned.
+   - Example:

```
```cpp
#include <algorithm>
#include <iostream>
#include <string>
#include <cstring>
using namespace std;

class CaseString
{
    public:
        bool operator()(string const &first, string const &second) const
        {
            return strcasecmp(second.c_str(), first.c_str()) > 0;
        }
};
int main()
{
    cout << "Word \"" << max(string("first"), string("second")) <<
                         "\" is lexicographically last\n";

    cout << "Word \"" << max(string("first"), string("SECOND")) <<
```
```