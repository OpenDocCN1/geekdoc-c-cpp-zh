```
```cpp
std::cout << "\n";
}

int main()
{
    std::cout << (1, 2, 3);                         // prints #1
    std::cout << ("hello", "initializer", "list"); // prints #2
    std::cout << (1, 2, 3, 5);                      // prints #3
    std::cout << (1, 2, 5);                         // prints #4
    std::cout << (1, 2);                            // prints #5
}
```
```

In the first test, due to the initializer-list arguments are promoted to `std::initializer_list` values, which involves converting each of the elements in the initializer list to the element type of the `std::initializer_list`. In the first test, the elements are of type `int`. In the second call, no additional conversion is needed. In the second call, each string literal in the initializer list is converted to a `std::string` by calling the `std::string(char const*)` constructor. The third call to `ovl()` performs a user-defined conversion using the `std::vector<std::initializer_list>` constructor. The next call invokes the `std::initializer_list` overload, but a `std::initializer_list<int>` is a better match. The final call performs aggregate initialization, which initializes the members of an instance of the `Point` class from the elements in the initializer list without calling a constructor or creating a temporary object.

There are several interesting overloading cases for initializer lists. When converting an initializer list to an `initializer_list<T>`, as in the first two calls of the example above, the overall conversion is given the same ranking as the user conversion from any given element in the initializer list to the element type of the `initializer_list<T>`.

In the first call to `ovl()`, each element of the initializer list is a `char`. For the first `ovl()` function, these elements require no conversion at all. For the second `ovl()` function, these elements require a promotion to `int`. Because the perfect match is better than a promotion, the first call to `ovl()` calls `#1`.

# Click here to view code image

```
```cpp
#include <initializer_list>
#include <iostream>

void ovl(std::initializer_list<char>) {  // #1
    std::cout << "#1\n";
}

void ovl(std::initializer_list<int>) {   // #2
    std::cout << "#2\n";
}

int main()
{
    ovl({'1', '2', '3', '4', '5'});       // prints #1
    ovl({'1', '2', '3', '4', '5', 0});    // prints #2
}
```
```

In the second call to `ovl()`, the first five elements are of type `char`, while the last is of type `int`. For the first `ovl()` function, the `char` elements are a perfect match, but the `int` requires a standard conversion, so the overall conversion is ranked as a standard conversion. For the second `ovl()` function, the `char` elements require a promotion to `int`, while the `int` element at the end is a perfect match. The overall conversion for the second `ovl()` function is ranked as a promotion, which makes it a better candidate than the first `ovl()`, even though only a single element's conversion is better.

When initializing an object of class type with an initializer list, as in the calls to `q()` and `ovl()` in our original example, overload resolution proceeds in two phases:

+   1. The first phase considers only initializer-list constructors; that is, constructors whose only non-defaulted parameter is of type `std::initializer_list<T>`. If one type is found, the initializer-list constructor is selected, regardless of the other available constructors and conversion sequences.
+   2. If no suitable constructor is found, then the second phase considers the remaining constructors.