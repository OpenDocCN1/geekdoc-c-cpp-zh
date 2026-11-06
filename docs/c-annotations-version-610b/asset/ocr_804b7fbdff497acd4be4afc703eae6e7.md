writes the string values to the specified ostream (i.e., cout), separating the values by the specified separation string (i.e., " ").

```
```cpp
#include <algorithm>
#include <string>
#include <iostream>
#include <iterator>
using namespace std;

int main()
{
    string sarr[] =
    {
        "alpha", "bravo", "charley", "delta", "echo",
        "foxtrot", "golf", "hotel"
    };
    string *last = sarr + sizeof(sarr) / sizeof(string);

    copy(sarr + 2, last, sarr); // move all elements two positions left

                                      // copy to cout using an ostream_iterator
                                      // for strings,
    copy(sarr, last, ostream_iterator<string>(cout, " "));
    cout << '\n';
}
// Displays: charley delta echo foxtrot golf hotel golf hotel
```
```

+   - See also: `unique_copy`

# 19.1.6  `copy_backward`

+   - Header file: `<algorithm>`
+   - Function prototype:
+     - `BidirectionalIterator copy_backward(InputIterator first, InputIterator last, BidirectionalIterator last2);`
+   - Description:
+     - The series of elements implied by the iterator range `[first, last)` are copied from the element at position `last - 1` until (and including) the element at position `first` to the element range, ending at position `last2 - 1` using the assignment operator of the underlying data type. The destination range is therefore `[last2 - (last - first), last2)`. Note that this algorithm does *not* reverse the order of the elements when copying them to the destination range.
+   
+       The return value is the BidirectionalIterator pointing to the last element that was copied to the destination range (so, ‘first’ in the destination range, pointed to by `last2 - (last - first)`, is returned).
+   - Example:

```
```cpp
#include <algorithm>
#include <string>
#include <iostream>
#include <iterator>
using namespace std;

int main()
```
```