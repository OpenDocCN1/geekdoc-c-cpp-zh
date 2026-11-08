# 23.4　C++ Concepts

Since C++20, there is the possibility to restrict the types you use as template parameters. For this, concepts were introduced. These define language within C++ that allows you to make assertions about template parameters. When you then instantiate (i.e., use) a template, these assertions are checked and acknowledged with a clearer error message than would be possible without a concept.

The standard library comes with a lot of concepts, many of them in the `<concepts>` header, but also in `<iterators>`, `<ranges>`, and so on.

# 23.4.1　How to Read Concepts

When you look at a function header with a concept, you see something like the following listing.

```
```cpp
// https://godbolt.org/z/jP75nY4EW
#include <concepts>  // integral
#include <iostream>
using namespace std;
// Concept explicitly with requires
template<typename T> requires integral<T>
auto add_1(T val) { return val+1; }
// abbreviated concept
template<integral T>
auto add_2(T val) { return val+2; }
// abbreviated function template with concept
auto add_3(integral auto val) { return val+3; }
// Ad-hoc requirements for function template
auto add_4(auto val) requires integral<decltype(val)>
{ return val+4; }
int main() {
    cout << add_1(1) << '\n';              // Output: 2
    cout << add_2(1) << '\n';              // Output: 3
    cout << add_3(1) << '\n';              // Output: 4
    cout << add_4(1) << '\n';              // Output: 5
    cout << add_3("text") << '\n';          // Error
    integral auto val = add_1(99);           // also for auto variables
    cout << val << '\n';                     // Output: 100
}
```
```

**Listing 23.24** Concepts can be written in different ways.

The functions add_1, add_2, add_3, and add_4 are essentially the same, just using different notations: