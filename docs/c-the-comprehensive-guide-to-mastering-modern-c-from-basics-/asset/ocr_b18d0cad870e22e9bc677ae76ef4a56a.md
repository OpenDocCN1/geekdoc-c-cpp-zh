I will cover all methods of array here as well as the most useful free functions and other tools. Much is similar to vector, so I will be brief. You will find a directly transferable detailed discussion of the corresponding feature of vector in Section 24.6.3.

All examples in this section for array should be considered embedded in the following code.

```
// https://cppbolt.org/z/PrM4fGCW0
#include <array>
#include <iostream>
using std::array; using std::cout;
template<typename Elem, size_t SZ>
std::ostream& operator<<(std::ostream& os, const std::array<Elem, SZ>& data) {
  for (auto& e : data) {
    os << e << " ";
  }
  return os;
}

int main() {
  // Example code here
}
```

+   1.  **Listing 24.34** Template for the example listings of this section on "array".

# # Initialize

The initialization operations for array are:

+   * **constructor**
When you define array<int,4> x{}, all elements are zero initialized. You can also initialize all—or some—elements according to the rules of aggregate initialization with array<int,4>{1,2,3,4} Or array<int,4>{1,2}.
* **Copy constructor, move constructor**
You can copy arrays of the same size and pass and return them by value. Moving is also possible if the element type allows it.

# # Assignment

You have the following operations available to modify content of an array at once:

+   * **Assignment operator**
You can assign new values to an array by assigning it another array with a compatible element type and the same size. operator= is therefore defined as expected.
* **Assign**
There is no assign because array also does not have a complete set of constructors.