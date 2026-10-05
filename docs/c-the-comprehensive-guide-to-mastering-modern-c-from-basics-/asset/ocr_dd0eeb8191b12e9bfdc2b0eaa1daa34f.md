# Specialties: Tuple Interface

From an array, you can not only access elements with the usual container methods, but you can also use an array like a tuple. A detailed description of tuple follows in Chapter 28, Section 28.1. For this, there is an overload of the free function std::get<size_t>(std::array<...>).

```
// https://godbolt.org/z/KrbTrXlAg
array<int,5> data = {10, 11, 12, 13, 14};
cout << get<2>(data) << "\n";
```

Listing 24.36 "array" supports "get" from "tuple".

As with tuples, the index must be constexpr as is a template argument to get. There is more similarity to tuple, as the element and tuple_size class templates are also declared for array, case you need them for your metaprogramming. One of the most practical things is undoubtedly that you can bind the elements of an array like tuple structured to declared variables.

```
// https://godbolt.org/p/j6nrRPWfm
#include <array>
#include <iostream>
int main() {
    std::array ports = {80, 443}; // array<int>
    auto [ht, htt] = ports; // declares variables and binds them
    auto [const& rht, int& rhts] = ports; // Reference and const are possible
    std::cout << ht << "\n";
    std::cout << rht << " " << rhts << "\n";
}
```

Listing 24.37 An array supports structured binding.

Here, int ht and int htt are defined and initialized with the values 80 and 443. For rht and rhts, you can see that references to the array also work—here, const int& rht.

# Specialties: Comparisons

You can compare two arrays of the same type with all comparison operators: <, =, and so on. You get the lexicographical result. For arrays, operator<=> is defined, from which all comparisons are derived. The operator behaves as if the free function lexicographical_compare_three() from the <algorithm> header is called. Here, <=> or < is used, depending on the availability for the element type. Instead of operator<=, all comparison operators for containers were overloaded in C++20. In both cases, this means that the first elements of both arrays are compared first, and if they are not equal, the result is