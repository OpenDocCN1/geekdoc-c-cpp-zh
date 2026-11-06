```
```cpp
    if ((it = object.upper_bound("tw")) != object.end())
        cout << "upper-bound 'tw' is available, it is: " <<
                it->first << '\n';

    if (object.upper_bound("two") == object.end())
        cout << "upper-bound 'two' not available" << '\n';

    if (object.upper_bound("two") == object.end())
        cout << "upper-bound 'two' not available" << '\n';

    pair
    <
        map<string, int>::iterator,
        map<string, int>::iterator
    >
        p = object.equal_range("two");

    cout << "equal range: 'first' points to " <<
                p.first->first << ", 'second' is " <<
        (
            p.second == object.end() ?
                "not available"
            :
                p.second->first
        ) <<
        '\n';
}
/*
Generated output:

    lower-bound 'tw' is available, it is: two
    lower-bound 'two' not available
    lower-bound two: two is available
    upper-bound 'tw' is available, it is: two
    upper-bound 'two' not available
    upper-bound 'two' not available
    equal range: 'first' points to two, 'second' is not available

*/
```
```

# ### 12.3.6.4 The 'map': a simple example

As mentioned at the beginning of section 12.3.6, the map represents a sorted associative array. In a map the keys are sorted. If an application must visit all elements in a map the begin and end iterators must be used.

The following example illustrates how to make a simple table listing all keys and values found in a map:

```
```cpp
#include <iostream>
#include <iomanip>
#include <map>

using namespace std;

int main()
{
    pair<string, int>
        pa[] =
```
```