An example of how you can write back into the underlying container through an extension is shown in the next listing.

```
// https://github.com/bolt/org/6Er5Gdo2G
#include <vector>
#include <span>
#include <iostream>
using namespace std;
void inc(span<int> span) {
    for(auto& e : span) { // Reference
        e += 1;
    }
}
int main() {
    vector<int> data={1,2,3,4,5};
    span<int> span(data);
    inc(span.first(3)); // -> 2,3,4
    inc(span.last(3)); // -> 3,4,5
    inc(span.last(4).first(3)); // -> 4,6,6
    inc(span.subspan(first(3))); // -> 5,7,7
    for(auto i:span) cout << i << " "; // Output: 2 5 7 7 6
    return 0;
}
```

# Listing 24.28

Here, inc() writes through the span into the container. In addition, you see other ways to create a span with first, last, and subspan.

span also offers the begin() and end()container methods as well as front() and back() and also operator().

# Dangerous Uses of "span":

You must be careful, with all references, that the underlying data is not destroyed while you are using span. Be particularly careful when dealing with temp-values:

```
vector<int> create_data() { return {1,2,3,4,5}; };
span<int> sp = create_data(); // sp references a temporary object
sp_m = create_data(); // This also references a temp-value
for(auto e : create_data().last(3)) { // e references a temp-value
auto data = create_data();
span ref = data(data); // okay, data is not a temp-value
data.push_back(4); // may trigger a reallocation
cout << ref[0] << " \ "; // possibly invalid access
```

The span (multidimensional span) added in C++23 works differently. You can overlay it on a one-dimensional data range, and the span can calculate the indices for you so you can use it like a multidimensional array. Together with another feature added in C++23, with which operator[] can now receive multidimensional indices, it looks as shown in the next listing.