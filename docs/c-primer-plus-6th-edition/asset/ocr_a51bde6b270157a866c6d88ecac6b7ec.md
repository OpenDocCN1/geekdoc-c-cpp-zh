# Generic Programming 1021

The set_intersection() and set_difference() functions find the set intersection
and difference of two sets, and they have the same interface as set_union().
Two useful methods are lower_bound() and upper_bound(). The lower_bound()\method takes a key-type value as its argument and returns an iterator that points to the
first member of the set that is not less than the key argument. Similarly,
upper_bound() method takes a key as its argument and returns an iterator that points to
the member of the set that is greater than the key argument. For example, if you
a set of strings, you could use these methods to identify a range encompassing all strings
of "b" to "f" in the set.
Because sorting determines where additions to a set go, the class has insertion methods
that justify the material to be inserted, without specifying a position. If A and B are
of sets of strings, for example you can use this:

```
string s("tennis");
A.insert(s); // insert a value
B.insert(A.begin(), A.end()); // insert a range
```

Listing 16.13 illustrates these uses of sets.

# Listing 16.13 sets.cpp

```
// sets.cpp -- some set operations
#include <iostream>
#include <string>
#include <set>
#include <algorithm>
#include <iterator>

int main() {
    using namespace std;
    const int N = 6;
    string s1[N] = {"buffer", "thinkers", "for", "heavy", "can", "for"};
    string s2[N] = {"metal", "any", "food", "elegant", "deliver","for"};

    set<string> A(s1, s1 + N);
    set<string> B(s2, s2 + N);

    ostream_iterator<string, char> out(cout, " ");
    cout << "Set A: " <<;
    copy(A.begin(), A.end(), out);
    cout << endl;
    cout << "Set B: " <<;
    copy(B.begin(), B.end(), out);
    cout << endl;
```