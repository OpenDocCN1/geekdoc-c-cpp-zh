map<string, int>::value_type. These value types themselves are pairs too, having 'first' and 'second' fields. Consequently, 'ret.first->first' is the key of the map value (a string), and 'ret.first->second' is the value (an int).

+   - map::iterator insert(pos, keyvalue). This way a map::value_type may also be inserted into the map. pos is ignored, and an iterator to the inserted element is returned.
+   - void insert(first, beyond) inserts the (map::value_type) elements pointed to by the iterator range [first, beyond).
+   - map::iterator lower_bound(key):
+   
+     this member returns an iterator pointing to the first keyvalue element of which the key is at least equal to the specified key. If no such element exists, the function returns end.
+   
+   - map::reverse_iterator rbegin():
+   
+     this member returns an iterator pointing to the last element of the map.
+   
+   - map::reverse_iterator rend():
+   
+     this member returns an iterator pointing before the first element of the map.
+   
+   - size_t size():
+   
+     this member returns the number of elements in the map.
+   
+   - void swap(argument):
+   
+     this member can be used to swap two maps using identical key/value types.
+   
+   - map::iterator upper_bound(key):
+   
+     this member returns an iterator pointing to the first keyvalue element having a key exceeding the specified key. If no such element exists, the function returns end. The following example illustrates the member functions equal_range, lower_bound and upper_bound:

```
```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    pair<string, int> pa[] =
    {
        pair<string,int>("one", 10),
        pair<string,int>("two", 20),
        pair<string,int>("three", 30),
    };
    map<string, int> object(&pa[0], &pa[3]);
    map<string, int>::iterator it;

    if ((it = object.lower_bound("tw")) != object.end())
        cout << "lower-bound `tw' is available, it is: " <<
                it->first << '\n';

    if (object.lower_bound("twoo") == object.end())
        cout << "lower-bound `twoo' not available" << '\n';

    cout << "lower-bound two: " <<
            object.lower_bound("two")->first <<
            " is available\n";
```
```