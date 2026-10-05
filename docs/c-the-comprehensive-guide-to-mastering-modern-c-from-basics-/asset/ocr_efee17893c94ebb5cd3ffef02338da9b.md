many containers or very small elements.

# Initialize

A multiset has exactly the same construction options as a set:

+   - Without arguments via default constructor
- A range from another container using a pair of iterators
- Another multiset for copying
- From C++23, a constructor with the from_range template tag

In many cases, the compiler can deduce the template parameters from the constructor arguments if you are using C++17.

If you choose an initializer list from another container, you get a container that contains the elements sorted and retains the duplicate entries.

```
// https://godbolt.org/z/agTGkdBMP
#include <vector>
///
multiset ms{1,2,3,1}; // sorted at initialization
cout << in{7,7,7,7,7,7}; // Output: 1 2 2 3
std::set range(in.begin(), in.end()); // set removes duplicates
cout << range.size() << ": " << *range.begin() << '\\n'; // Output: 7
multiset msrange(in.begin(), in.end()); // multiset retains duplicates
cout << msrange; // Output: 7 7 7 7 7 7
```

**Listing 24.69** Entries are sorted, and duplicates are retained.

# Assignment

With operator=, you can reassign the contents of multiset just like a set, either by copy or move. The swap method is also used here to implement common idioms.