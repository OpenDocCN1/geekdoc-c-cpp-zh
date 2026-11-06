# 12.3  SEQUENTIAL CONTAINERS

means to determine all elements in the multimap that have the same keys. An example illustrating the use of these member functions is given at the end of this section.

+   - `multimap::iterator find(key)`:  
+     this member returns an iterator pointing to the first value whose key is key. If the element isn’t available, an iterator to the end is returned. The iterator could be incremented to visit all elements having the same key until it is either end, or the iterator’s first member is not equal to key anymore.

+   - `multimap::iterator insert()`:  
+     this member function normally succeeds, and so a `multimap::iterator` is returned, instead of a `pair<multimap::iterator, bool>` as returned with the map container. The returned iterator points to the newly added element.

Although the functions lower_bound and upper_bound act identically in the map and multimap containers, their operation in a multimap deserves some additional attention. The next example illustrates lower_bound, upper_bound and equal_range applied to a multimap.

```
```cpp
#include <iostream>
#include <map>
using namespace std;

int main()
{
    pair<string, int> pa[] =
    {
        pair<string,int>("alpha", 1),
        pair<string,int>("bravo", 2),
        pair<string,int>("charley", 3),
        pair<string,int>("bravo", 7),  // unordered ‘bravo’ values
        pair<string,int>("delta", 5),
        pair<string,int>("bravo", 4),
    };
    multimap<string, int> object(&pa[0], &pa[6]);

    typedef multimap<string, int>::iterator msiIterator;

    msiIterator it = object.lower_bound("brava");

    cout << "Lower bound for ‘brava’: " <<
        it->first << ", " << it->second << '\n';

    it = object.upper_bound("bravu");

    cout << "Upper bound for ‘bravu’: " <<
        it->first << ", " << it->second << '\n';

    pair<msiIterator, msiIterator>
        itPair = object.equal_range("bravo");

    cout << "Equal range for ‘bravo’:\n";
    for (it = itPair.first; it != itPair.second; ++it)
        cout << it->first << ", " << it->second << '\n';
    cout << "Upper bound: " << it->first << ", " << it->second << '\n';

    cout << "Equal range for ‘brav’:\n";
    itPair = object.equal_range("brav");
    for (it = itPair.first; it != itPair.second; ++it)
```
```