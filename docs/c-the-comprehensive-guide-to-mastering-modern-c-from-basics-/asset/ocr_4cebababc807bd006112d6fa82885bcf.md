# Specialty: List Operations

Just like list, forward_list has a set of methods that serve as replacements for some free functions from <algorithm>, but always operate on the entire list instead of just a range between two iterators. Fortunately, merge is also available for merging two presorted lists.

The specialty of efficiently merging lists or ranges works again with a special case in forward_list compared to list—namely, splice_after, as shown in Listing 24.44.

```
// https://github.com/Ka7wSjWh
#include <forward_list>
#include <iostream>

using std::cout; using std::forward_list; using std::ostream;

std::ostream& operator<<(std::ostream& os, const forward_list<int>& data) {
    for (auto i : data) { os << i << '\n'; }
    return os;
}

int main() {
    forward_list fw1 {10, 20, 30, 48};
    forward_list fw2 {5, 6, 7};
    fw1.splice_after(fw1.begin(), fw2); // transfers everything
    cout << fw1;
    // Output: 10 5 6 7 20 30 40
    // Output:

    forward_list fw1 {10, 20, 30, 48};
    forward_list fw2 {5, 6, 7};
    // one element left
    fw1.splice_after(fw1.begin(), fw2, fw2.end());
    cout << fw1;
    // Output: 10 6 7 8 20 30 40
    cout << fw2;
    // Output: 5
}
```

**Listing 24.44** "splice_after" can very efficiently merge lists.

splice comes in several variants to merge entire forward_list containers or just ranges of them. Note that the special nature of the forward_list interface is it once again a bit tricky. As you can see in Listing 24.44, the two very similar calls to splice after yield different results: The first variant only takes the source list as a parameter and transfers the entire content of the source list. However, if you pass two iterators as the source area, the forward list is not spliced at the first iterator before it; that is, the "after" rule applies again. Because I pass begin() here, the splice happens one element after the begin. As a result, one element remains in the source.