only read the elements in the range, everything will definitely work. Here, we only let the loop run forward. Maybe you want to write an algorithm that accesses the elements of the range backward or even randomly. Then it may be that some containers do not cooperate with your function or behave undesirably. A `list` does not allow random access to its elements. With the choice of the right range concept, you can document that.

So long as you keep this in mind, you are definitely on the safe side for functions that only read. If you also need write access, you need to be a bit more cautious. When you describe an element with a new value, you must consider that, for example, a `set` wants to keep its elements sorted—and it will do so, causing the order of elements to change and thus the range as well.

# 23.2.2 Example: Information about Numbers

In the following example, you will not only see the use of a function template but also that there is a very interesting helper template, `numeric_limits<>`. With it, you can find out all sorts of useful internals and use them in your program. If you want to initialize a vector large enough to hold all possible values of `unsigned short`, you can do it like this:

```
const auto sz = std::numeric_limits<unsigned short>::max();
std::vector<string> dictionary(sz);
```

If the `unsigned short` type on your system has a width of 16 bits, then `unsigned short` variables can hold values from 0 to 65536. The `sz` variable takes this value, and the vector `dictionary` is initialized with this size.

A few examples of what else you can find out using `numeric_limits` are shown in Listing 23.11.

```
// https://godbolt.org/z/t83Yeon7r
#include <iostream>              // cout
#include <limits>                // numeric_limits
template<typename INT_TYP>       // Template with type argument
void infos(const char* name) {
    using L = typename std::numeric_limits<INT_TYP>; // rename for brevity
    std::cout
        << name
        << " number of bits:" << L::digits      // Bits without sign bit
        << " sign:" << L::is_signed             // stores sign?
        << " min:"<< (long long)L::min()        // smallest possible value
        << " max:"<< (long long)L::max()        // largest possible value
        << "\n";
}
```