```
/*
 * print
 *
 * Prints the contents of a vector
 *  a is the vector to print.
 *  a is not modified.
 */
template <typename T>
void print(const std::vector<T>& a) {
    int n = a.size();
    std::cout << '{';
    if (n > 0) {
        std::cout << a[0]; // Print the first element
        for (int i = 1; i < n; i++)
            std::cout << ',' << a[i]; // Print the rest
    }
    std::cout << '}';
}
```

The restriction here is that the elements in the vector must be printable to the `std::cout` object using `<<`.

Listing 19.3 (templateflexsort.cpp) uses our new generic functions to increase the flexibility of our flexible sorting program from Listing 12.2 (flexibleinsertion.cpp).

# Listing 19.3: templateflexsort.cpp

```
#include <iostream>
#include <string>
#include <vector>
#include <utility> // For generic swap function

/*
 * less_than(a, b)
 *
 * Returns true if a < b; otherwise, returns
 * false.
 */
template <typename T>
bool less_than(const T& a, const T& b) {
    return a < b;
}

/*
 * greater_than(a, b)
 *
 * Returns true if a > b; otherwise, returns
 * false.
 */
template <typename T>
bool greater_than(const T& a, const T& b) {
    return a > b;
}

/*
 * selection_sort(a, n, compare)
 *
 * Arranges the elements of vector vec in an order determined
 * by the compare function.
 *
```