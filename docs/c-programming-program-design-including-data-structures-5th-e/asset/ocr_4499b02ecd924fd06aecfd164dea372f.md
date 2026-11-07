TABLE 22-18  Operations to Insert or Delete Elements from a Set (continued)

| Expression | Effect |
|---|---|
| `ct.erase(elem);` | Deletes all of the elements with the value *elem*. The number of deleted elements is returned. |
| `ct.erase(position);` | Deletes the element at the position specified by the iterator position. No value is returned. |
| `ct.erase(beg, end);` | Deletes all of the elements starting at the position *beg* until the position *end−1*. Both *beg* and *end* are iterators. No value is returned. |
| `ct.clear();` | Deletes all of the elements from the container *ct*. After this operation, the container *ct* is empty. |

Example 22-8 shows the various operations on a set/multiset container.

# EXAMPLE 22-8

```
```cpp
#include <iostream>
#include <set>
#include <string>
#include <iterator>
#include <algorithm>

using namespace std;

int main()
{
    set<int> intSet;                              //Line 1
    set<int, greater<int> > intSetA;              //Line 2

    set<int, greater<int> >::iterator intGtIt;    //Line 3

    ostream_iterator<int> screen(cout, " ");     //Line 4

    intSet.insert(16);                            //Line 5
    intSet.insert(8);                             //Line 6
    intSet.insert(20);                            //Line 7
    intSet.insert(3);                             //Line 8

    cout << "Line 9: intSet: ";                  //Line 9
    copy(intSet.begin(), intSet.end(), screen);   //Line 10
    cout << endl;                                 //Line 11

    intSetA.insert(36);                            //Line 12
    intSetA.insert(84);                            //Line 13
```

```