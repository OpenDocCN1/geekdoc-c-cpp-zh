+   - void erase(pos) erases the element pointed to by the iterator pos. Other elements possibly having the same values are not erased.

+   - void erase(first, beyond) erases all elements indicated by the iterator range [first, beyond).

+   - pair<multiset::iterator, multiset::iterator> equal_range(value):

this member function returns a pair of iterators, being respectively the return values of lower_bound and upper_bound, introduced below. The function provides a simple means to determine all elements in the multiset that have the same values.

+   - multiset::iterator find(value):

this member returns an iterator pointing to the first element having the specified value. If the element isn't available, end is returned. The iterator could be incremented to visit all elements having the given value until it is either end, or the iterator doesn't point to 'value' anymore.

+   - ... insert():

this member function normally succeeds and returns a multiset::iterator rather than a pair<multiset::iterator, bool> as returned with the set container. The returned iterator points to the newly added element.

Although the functions lower_bound and upper_bound act identically in the set and multiset containers, their operation in a multiset deserves some additional attention. With a multiset container lower_bound and upper_bound produce the same result for non-existing keys: they both return the first element having a key exceeding the provided key.

Here is an example showing the use of various member functions of a multiset:

```
```cpp
#include <iostream>
#include <set>

using namespace std;

int main()
{
    string
        sa[] =
        {
            "alpha",
            "echo",
            "hotel",
            "mike",
            "romeo"
        };

    multiset<string>
        object(&sa[0], &sa[5]);

    object.insert("echo");
    object.insert("echo");

    multiset<string>::iterator
        it = object.find("echo");

    for (; it != object.end(); ++it)
        cout << *it << " ";
    cout << '\n';
}
```
```