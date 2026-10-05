there is also insert_range. You cannot provide a position hint in this case. You do not get information about whether and which elements were actually added or already existed. The return type is void.

```
// https://godbolt.org/z/rTvovhrM
#include <vector>
set data={ 10, 20, 30 };
data.insert({ 40, 50, 60, 70 }); // Initializer list
std::vector<int> new_vec {5, 25, 35, 15, 25, 75, 95};
data.insert(new_vec.begin(), new_vec.end() - 1); // area
cout << data; // Output: 10 15 20 25 30 40 50 60 70 75
```

# Listing 24.55 You can also insert multiple elements.

You can see that the 25 from new_vec is not inserted twice.

# Accessing

# Access via Iterators

The iterators of set are bidirectional; see Table 24.2. Because the ordered associative containers are ordered at all times (hence the name), you always iterate over the elements in a given order. With [c]begin()/[c]end(), this order is ascending; with [c]rbegin()/[c]rend(), it is descending.

# Access via Search

The most important search function is find. It takes a search element as a parameter and returns an iterator. If the element is found, it points to the found element; if not, it points to end(). lower_bound behaves differently: it finds the first element that is not less than the search element. That means if it is present, it points to it; if not, it points to the next larger element. With upper_bound, you get the first element that is greater than the search element. Both combined equal_range: you get a pair of two iterators that mark an area enclosing the search element (so, not a C++20 range). With count, you find the number of matching keys, as in auto r = equal_range(key); auto count = distance(r.first,