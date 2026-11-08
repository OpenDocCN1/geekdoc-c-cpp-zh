elements in a given order. With [c]begin()/[/c]end(), this order is ascending; with [r]cbegin()/[/r]cend(), it is descending.

# Access via Search

The most important search function is find. It takes a search element as a parameter and returns an iterator. If the element is found, it points to the found element; if not, it points to end(). lower_bound behaves somewhat differently: it finds the first element that is not less than the search element. That means if it is present, it points to it; if not, it points to the next larger element. With upper_bound, you get the first element that is greater than the search element. Both combined form equal_range: you get a pair of two iterators that mark an area enclosing the search element (so, not a C++20 range). With count, you find the number of matching keys, as in auto r = equal_range(key); auto count = distance(r.first, r.second). Naturally, in a set, this is either zero or one. Since C++20, there is also contains, which returns a bool. All searches are guaranteed to take at most log n steps.

Note the somewhat asymmetric behavior of upper_bound: when you search in the set s with elements {1,2,3} using it = s.upper_bound(2), it points to 3, because it is the first element greater than 2. In contrast, it = s.lower_bound(2) returns an iterator to 2, because it is the last element not less than 2. Together, they are exactly what equal_range returns as a pair. This is illustrated in Listing 24.56.

```
```cpp
// https://godbolt.org/z/MW74f97f7
#include <set>
#include <iostream>
using std::cout; using std::ostream; using std::set;
void search(const std::set<int>& data, int what, ostream& os) {
    os << what << " ";
    // contains
    auto inside = data.contains(what);  // C++20
    os << "inside: " << (inside ? "yes " : "no "); // check contains
    auto where = data.find(what);
    if(where != data.end()) {
        os << " found: " << "";
    } else {
        os << " not found: ";
    }
    auto lo = data.lower_bound(what);
    if(lo != data.end()) {
        os << "lo:" << *lo;
    } else {
        os << "lo:-";
    }
    auto up = data.upper_bound(what);
    if(up != data.end()) {
```
```