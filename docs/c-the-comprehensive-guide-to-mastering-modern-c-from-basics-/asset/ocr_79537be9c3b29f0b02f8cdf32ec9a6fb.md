```
auto it2 = even.begin();               // vector<char>::iterator
auto it3 = vowels.begin();                // enforces const_iterator
*it2 = '5'; *it3 = 'a';                               // error: 'const char*' is not modifiable
for(auto it1=vowels.begin(); it1!=vowels.end(); ++it1) {
    cout << *it1 << '\n'; }                           // Output: eiou
for(auto it1=vowels.rbegin(); it1!=vowels.rend(); ++it1) {\   // despite reverse!
    cout << *it1 << '\n'; }                             // Output: oiea
```

# **Listing 24.20** With "begin", "end", and their relatives, you get iterators.

With the variants begin and cend, you get a const_iterator back, which does not allow you to modify the element upon dereferencing. begin and end, on the other hand, return either const_iterator or an iterator depending on the container's modifier.

The r_. variants of these functions allow reverse iteration through the vector. Note that you need to increment reverse_iterator const_reverse_iterator with ++ to actually iterate backward.

# **Notation for "begin()", "cbegin()", "rbegin()", and "crbegin()"**

To be concise, I write

+   * [cbegin()] for begin() and cbegin();
* [rbegin()] for rbegin() and rbegin();
* [crbegin()] for begin(), cbegin(), rbegin(), and crbegin().

**The same applies to the variants of end.**

Access via iterator is universal for all containers. vector has random access—that is, via random_access_tag. In practice, you can add a positive or negative offset to a vector, as you can in **Listing 24.21.**

```
https://cppbolt.org/z/srcxz737G
#include <vector>
#include <iostream>
#include <algorithm>
using std::vector; using std::cout; // ranges: sort
vector<int> data(data); // copied
sort(data);                   // C++20, otherwise std::sort(data);
auto it = data.begin();
it += data.size() / 2;
if(it == data.end()) return 0;   // special case
int median = *it;               // approximately the middle
if(data.size()%2 != 0) {     // odd number of elements
    return median;
} else {
    return double(*it + *(it+1)) / 2; // even number of elements
}

 main() {
    vector<int> data { 12, 22, 34, 10, 1, 99, 33 };
    cout << median(data) << '\\n';
    vector<int> data2 { 30, 2, 80, 99, 31, 3 };
```