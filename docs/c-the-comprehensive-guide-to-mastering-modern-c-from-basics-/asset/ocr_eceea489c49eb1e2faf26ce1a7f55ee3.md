Long run is to get used to the correct use of const. Coming from C (or Java), this probably means using more of it. Once in the C++ world, the compiler can already uncover many logical errors in the code with const in the right places—where something was changed that was not meant to be changed.

The second aspect is documentation. A const tells subsequent programmers (all too often yourself) what this value is intended for. Is the variable used for computation, or just for temporary storage? Is it an input parameter or an output parameter?

# Iterators for Constants

In addition, there are other places where the immutability of a value can be indicated. I will go into iterators in more detail in Chapter 20, but as they are somewhat constant, I should explain them here.

A Container::const_iterator is a reference into a standard library container that does not modify the elements within. It should be considered similar to int const*: the value cannot be changed, but the reference can. Thus, it is different from Container::iterator, which is comparable to an int const. The iterator itself remains fixed.

```
// https://cppbolt.org/z/GE5v6Ea8x
#include <map>
#include <string>
using std::map; using std::string;
struct MyClass {
    bool isFound(const map<int,string> &dict, // immutable input
    parameter);
```