![](bbox=[0.143, 0.1, 0.857, 0.243])

**Figure 24.11** The search functions define ranges.

# Searching without a Specific Key

The parameters of `find`-related functions naturally require a key as a parameter for the search. But what if generating a key is very costly or even impossible? Or the search keys are slightly different in form from the stored keys? In that case, you can use a different type as a parameter for the search key. It is important that the keys are equivalent (with respect to the search).

```
```cpp
// https://godbolt.org/z/zEsxd8e7G
#include <string>
#include <set>
#include <iostream>
#include <tuple> // tuple, tie
using std::string; using std::set; using std::cout; using std::tie;
struct Hobbit {
    string firstName;
    string lastName;
    Hobbit(const string v, const string n) : firstName{v}, lastName{n} {}
};
struct CompLastName {
    bool operator()(const Hobbit& x, const Hobbit& y) const { // normal
        return tie(x.lastName, x.firstName) < tie(y.lastName, y.firstName);
    }
    using is_transparent = std::true_type; // allowed for find
    bool operator()(const Hobbit& x, const string& y) const { // for find etc.
        return x.lastName < y;
    }
    bool operator()(const string& x, const Hobbit& y) const { // for find etc.
        return x < y.lastName;
    }
};
int main() {
    using namespace std::literals; // allow "...s"
    set<Hobbit,CompLastName> hobbits;
```
```