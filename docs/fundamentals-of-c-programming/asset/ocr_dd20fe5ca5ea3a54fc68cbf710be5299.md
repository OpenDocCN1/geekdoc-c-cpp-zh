```
std::cout << "Vector time: " << stop_time - start_time << '\n';
start_time = clock();
for (int i = 0; i < SIZE; i++) {
    int seek = search_values[i];
    s.find(seek);
}
stop_time = clock();
std::cout << "Set time: " << stop_time - start_time << '\n';
}
```

The vector and set objects within Listing 21.5 (setsvsvector.cpp) each contain the integers 0, 1, ..., 249, 000. Note that the container contains the elements in ascending order. We then create a vector containing pseudo-random values in the range 0, 1, ..., 249, 000. The program will search for these random values within each container. The program measures the time it takes to complete the searches.

The output Listing 21.5 (setsvsvector.cpp) reveals the dramatic difference in performance between the `std::find` function on a vector and the `std::set::find` method with a set:

```
Vector time: 84044 msec
Set time: 234 msec
```

We see on this particular run that the vector search required almost one and a half minutes to complete, while the set search took only about a quarter of a second. While the exact numbers will vary from run to run and be higher or lower depending on the host machine, the disparity of times will be consistent. The two data structure contain exactly the same elements, and program uses the exact same search values. The `std::set`'s search is so much quicker because `std::set::find` performs binary search on its internal data structure, while `std::find` uses linear search (see Section 12.3.2).

# 21.3 Tuples

In C++ a function can return only one thing. That one thing might be an integer or a single object like a vector or an instance of some other class, but it must be just one thing. What if we need a function to return more than one thing? We could put the desired return values into a vector and return the vector. The caller then would extract the components from the vector upon the function's return. Unfortunately, this will not work if the multiple elements to return have different types. The container types we have examined thus far—vectors, arrays, lists, and sets—have been homogeneous; that is, their elements all have the same type.

We could define a `struct` or `class` that has fields of different types, but this creates a new, named, custom type. In a large program we may need many different `struct`s to cover all the combinations of multiple-valued return types we need. Providing a named `struct` or `class` introduces a new type into the system, thereby increasing the system's complexity.

All we want is to be able to package multiple elements together for some simple purpose, without needing to create a new custom type. Fortunately, C++ provides the `std::tuple` generic class in its standard library. Listing 21.6 (simpletuples.cpp) shows how to use tuples in a C++ program.

# Listing 21.6: simpletuples.cpp

```
#include <iostream>
#include <string>
#include <tuple>
```