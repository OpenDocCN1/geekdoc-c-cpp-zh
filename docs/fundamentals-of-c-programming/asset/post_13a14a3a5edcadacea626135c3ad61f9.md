

```
std::cout << std::boolalpha << is_sorted({5, 4, 3, 2, 1}) << '\n';
std::cout << std::boolalpha << is_sorted({5, 5, 5, 5, 5}) << '\n';
std::cout << "" << '\n';
std::cout << max({1, 2, 3, 4, 5}) << '\n';
std::cout << max({5, 4, 3, 2, 1}) << '\n';
std::cout << max({3, 4, 5, 2, 1}) << '\n';
std::cout << max({5, 2, 3, 4, 5}) << '\n';
std::cout << max({5, 4, 5, 2, 5}) << '\n';
std::cout << max({5}) << '\n';
std::cout << max({5, 5, 5, 5, 5}) << '\n';
}
```

In Listing 20.53 (bettermaxvector.cpp) because of the missing `std::` prefixes the compiler knows that the calls to `max` cannot be the calls to `std::max`.

Identifiers (variable names, function names, and type names) should be meaningful, clearly communicating their intent. Well-chosen English words or simple variations of common words are ideal. This means it is quite likely that a library developed by a team of developers would contain function names and type names that also appear in a different library developed by a different team of programmers. Each library used separately is not a problem, but issues can arise when building a software system atop multiple libraries; for example, consider the task of building a program that models and visualizes the spread of an infectious agent. Such a system could make good use of the following libraries:

- a 3-D graphics library that defines a mathematical vector class, used for a number computer graphics rendering processes, such as scene orientation and light intensities,
- an epidemiology modeling library with a vector type that represents the means of transmission of a disease, such as a mosquito or tick, and
- the C++ standard library which includes a vector generic class used to store sequences of any type.

The name `vector` has a different meaning in each of these contexts. C++ namespaces allow us to manage simultaneously and effectively all of these vector types within a single software system.

Ideally, any code meant for widespread use should be part of a namespace. A company developing libraries for internal use could place them in a namespace based on the company name. Components intended for public consumption could be placed in a namespace with a different name.

In C++ it is easy to put the functions and types we develop into custom namespaces. Suppose we wish to make the functions from Listing 20.53 (bettermaxvector.cpp) available to a wider audience. Listing 20.54 (vectutils.h) and Listing 20.55 (vectutils.cpp) package the two functions into a namespace named `vectutils`. Listing 20.54 (vectutils.h) provides the function declarations, and Listing 20.55 (vectutils.cpp) contains the function definitions.

### Listing 20.54: vectutils.h

```
#include <vector>

namespace vectutils {

// Counts the number of occurrences of the maximum value in
// a nonempty vector vec
int max(const std::vector<int>& vec);

// Returns true if all the elements in vector vec appear
```

// in nondecreasing order; otherwise, returns false.
bool is_sorted(const std::vector<int>& vec);
} // End vectutils namespace

### Listing 20.55: vectutils.cpp

```
#include "vectutils.h"

namespace vectutils {
// Counts the number of occurrences of the maximum value in
// a nonempty vector vec
int max(const std::vector<int>& vec) {
    auto p = std::begin(vec); // p points to the first element
    // Determine maximum value
    int m = *p++;             // Set m to the first element and move p
    while (p != std::end(vec)) {
        if (*p > m)           // Found a reason to update m
            m = *p;           //
        p++;
    }
    // Count the number of times the maximum appears
    int count = 0;
    for (auto elem : vec)
        if (elem == m)
            count++;
    return count;
}

// Returns true if all the elements in vector vec appear
// in nondecreasing order; otherwise, returns false.
bool is_sorted(const std::vector<int>& vec) {
    for (unsigned i = 0; i < vec.size() - 1; i++)
        if (vec[i] > vec[i + 1])
            return false;     // Found elements out of order
    return true;
} // End vectutils namespace
```

The general form of a namespace declaration is

![](img/e84ad11adb18201d71595b31ce6c9eff_712_0.png)

The name of a namespace is an identifier; therefore, the same rules governing variable names, function names, and type names apply equally to namespace names.

Listing 20.54 (vectutils.h) and Listing 20.55 (vectutils.cpp) demonstrate that namespace declarations can span multiple files. The components of the std namespace are scattered over many different files.

Listing 20.56 (testns.cpp) tests the functions in our new namespace.

### Listing 20.56: testns.cpp

```
Listing 20.56: testns.cpp

#include <iostream>
#include "vectutils.h"

int main() {
    std::cout << std::boolalpha << vecutils::is_sorted({1, 2, 3, 4, 5}) << '\n';
    std::cout << std::boolalpha << vecutils::is_sorted({5, 4, 3, 2, 1}) << '\n';
    std::cout << std::boolalpha << vecutils::is_sorted({5, 5, 5, 5, 5}) << '\n';
    std::cout << vecutils::max({1, 2, 3, 4, 5}) << '\n';
    std::cout << vecutils::max({5, 4, 3, 2, 1}) << '\n';
    std::cout << vecutils::max({5, 5, 5, 5, 5}) << '\n';
    std::cout << vecutils::max({3, 4, 5, 2, 1}) << '\n';
    std::cout << vecutils::max({5, 2, 3, 4, 5}) << '\n';
    std::cout << vecutils::max({5, 4, 5, 2, 5}) << '\n';
    std::cout << vecutils::max({5}) << '\n';
    std::cout << vecutils::max({5, 5, 5, 5, 5}) << '\n';
}
```

Note that instead of using the long names for vecutils::is_sorted and vecutils::max, we could have used the focused using declarations:

```
using vecutils::is_sorted;
using vecutils::max;
```

We also could use the blanket using directive

```
using namespace vecutils;
```

but this introduces the possibility of name clashes, especially with the similar-named functions from the std namespace declared in the <algorithm> header. Just as with the std namespace, it is best to avoid blanket using directives for custom namespaces.

C++ permits namespaces to be nested, as in

```
namespace utils {
    namespace graphics {
        namespace math {
            double f(double v) { /* Details omitted . . . */ }
        }
    }
}
```

Absent of any using directives, we would call function f as

```
std::cout << utils::graphics::math::f(9.4) << '\n';
```

Since nested namespace names can become quite lengthy, C++ supports namespace aliases, as in

```
namespace ugm = utils::graphics::math;
```

This namespace alias makes it possible for us to call f with the more compact statement

```
std::cout << ugm::f(9.4) << '\n';
```

Nesting allows developers to organize better the components within libraries; for example, a company may have an outer namespace derived from the company's name and nested namespaces that correspond to departments or divisions within the company.

## Chapter 21

## Associative Containers

### 21.1 Associative Containers

Chapter 11 introduced the vector and array data types. Both of these data structures represent linear sequences of elements. Vectors and arrays are convenient for storing collections of data, but they have some limitations. For one, we locate an element within a vector or array based on its position (index). To retrieve a specific element we must supply its index. While this approach is fine for many applications, in other situations access-by-index approach is awkward or inefficient.

In contrast, an associative container permits access based on a key, rather than an index. Unlike an index, a key is not restricted to an integer expression. The C++ standard library supports three kinds of associative containers: set, map, and unordered_map. Here we will examine each of these types in some detail.

### 21.2 The std::set Data Type

C++ provides a data structure that models to some extent a mathematical set. Unlike C++ vectors, arrays, and lists, mathematical sets are unordered and may contain no duplicate elements. The C++ std::set container, like mathematical sets, ignores any attempts to include duplicate elements; however, std::set objects do order their elements internally in a particular way. This ordering permits very fast access to elements. Listing 21.1 (settest.cpp) demonstrates these properties.

### Listing 21.1: settest.cpp

```
Listing 21.1: settest.cpp

#include <iostream>
#include <set>

// A custom type
struct MyClass {
    int data;
    MyClass(int d): data(d) {}
};

// We need this operator so we can insert our MyClass into a set
bool operator<(const MyClass& a, const MyClass& b) {
```

