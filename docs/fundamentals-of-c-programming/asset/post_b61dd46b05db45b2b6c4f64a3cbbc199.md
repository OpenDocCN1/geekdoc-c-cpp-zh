
The real value of the set class comes from the speed of access it provides to its elements. As an associative container, we do not access an element via an index as we do with a vector or array. In fact, std::set does not even provide `operator[]`. We want to place an item into a set and retrieve it later without regard to its location within its internal data structure.

Recall the `std::find` algorithm provided by the STL (see Section 20.5). Given an iterator to the beginning of the container, an iterator just past the end of the container, and an item to find, `std::find` returns an iterator that points to the sought element within the container. If the container does not contain the sought element, `std::find` returns the iterator that equals the just-past-the-end iterator.

The `std::find` function works with a `std::set` object just as it does with other containers, but the `std::set` class provides its own find method that exploits the structure of the data within the set object to locate elements very quickly. Listing 21.5 (`setsvsvector.cpp`) illustrates the use of the `std::set::find` method, comparing the time to locate an element in a vector versus the time to locate the same element in a set containing the exact elements contained in the vector.

### Listing 21.5: setsvsvector.cpp

```cpp
#include <iostream>
#include <set>
#include <vector>
#include <algorithm>
#include <iterator>
#include <ctime>

#include "uniformrandom.h"

int main() {
    const int SIZE = 250000;
    // Make a vector and set
    std::vector<int> v;
    std::set<int> s;

    // Populate the vector and set with the first SIZE integers
    for (int i = 0; i < SIZE; i++) {
        v.push_back(i);
    }
    for (int i = 0; i < SIZE; i++) {
        s.insert(i);
    }

    // Make a vector that contains random numbers in the range
    // stored within the vector and set
    UniformRandomGenerator gen(0, SIZE - 1);
    std::vector<int> search_values;
    for (int i = 0; i < SIZE; i++) {
        search_values.push_back(gen());
    }

    clock_t start_time, stop_time;

    // Search each data structure for the integers 0 to 1,000,000
    start_time = clock();
    for (int i = 0; i < SIZE; i++) {
        int seek = search_values[i];
        std::find(std::begin(v), std::end(v), seek);
    }
    stop_time = clock();
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

The vector and set objects within Listing 21.5 (setsvsvector.cpp) each contain the integers 0, 1, ..., 249,999. Note that the container contains the elements in ascending order. We then create a vector containing pseudo-random values in the range 0, 1, ..., 249,999. The program will search for these random values within each container. The program measures the time it takes to complete the searches.

The output from Listing 21.5 (setsvsvector.cpp) reveals the dramatic difference in performance between the `std::find` function on a vector and the `std::set::find` method with a set:

```
Vector time: 84044 msec
Set time: 234 msec
```

We see on this particular run that the vector search required almost one and a half minutes to complete, while the set search took only about a quarter of a second. While the exact numbers will vary from run to run and be higher or lower depending on the host machine, the disparity of times will be consistent. The two data structures contain exactly the same elements, and the program uses the exact same search values. The `std::set`'s search is so much quicker because `std::set::find` performs binary search on its internal data structure, while `std::find` uses linear search (see Section 12.3.2).

## 21.3 Tuples

In C++ a function can return only one thing. That one thing might be an integer or a single object like a vector or an instance of some other class, but it must be just one thing. What if we need a function to return more than one thing? We could put the desired return values into a vector and return the vector. The caller then would extract the components from the vector upon the function's return. Unfortunately, this will not work if the multiple elements to return have different types. The container types we have examined thus far—vectors, arrays, lists, and sets—have been homogeneous; that is, their elements all have the same type.

We could define a `struct` or `class` that has fields of different types, but this creates a new, named, custom type. In a large program we may need many different `struct`s to cover all the combinations of multiple-valued return types we need. Providing a named `struct` or `class` introduces a new type into the system, thereby increasing the system's complexity.

All we want is to be able to package multiple elements together for some simple purpose, without needing to create a new custom type. Fortunately, C++ provides the `std::tuple` generic class in its standard library. Listing 21.6 (simpletuples.cpp) shows how to use tuples in a C++ program.

### Listing 21.6: simpletuples.cpp

```cpp
#include <iostream>
#include <string>
#include <tuple>
#include <cmath> // For sqrt

int main() {
    // Declare some local variables
    std::string word;
    int number;
    double quantity;

    // Construct a tuple directly with some literal values
    std::tuple<std::string, int, double> t1("Bob", 4, 9.5);
    // Unpack the tuple's components
    std::tie(word, number, quantity) = t1;
    // Print the results
    std::cout << "word = " << word << ", number = " << number
              << ", quantity = " << quantity << '\n';

    // Use std::make_tuple convenience function
    auto t2 = std::make_tuple("Eve", 22, 8.3);
    // Unpack the tuple's components
    std::tie(word, number, quantity) = t2;
    // Print the results
    std::cout << "word = " << word << ", number = " << number
              << ", quantity = " << quantity << '\n';

    // Declare some variables
    std::string name = "Jan";
    int age = 12;
    double amount = 50.2;

    // Build a tuple from more general expressions
    auto t3 = std::make_tuple(name, age * 2, std::sqrt(amount));
    // Unpack the tuple's components one at a time
    word = std::get<0>(t3); // 1st component is at index 0
    number = std::get<1>(t3); // 2nd component is at index 1
    quantity = std::get<2>(t3); // 3rd component is at index 2
    // Print the results
    std::cout << "word = " << word << ", number = " << number
              << ", quantity = " << quantity << '\n';
}
```

When compiled and executed, Listing 21.6 (simpletuples.cpp) prints

```
word = Bob, number = 4, quantity = 9.5
word = Eve, number = 22, quantity = 8.3
word = Jan, number = 24, quantity = 7.0852
```

As the program shows, we can construct a std::tuple directly, as in the case of t1, but the std::make_tuple function results in simpler code. The arguments used when making a tuple can consist of literals, variables, and other more complex expressions.

Extracting the components of a tuple is known as unpacking. Listing 21.6 (simpletuples.cpp) shows how to use the std::tie function to assign the components of a tuple to individual variables in one statement. The std::tie function is a generic function that works with any types storable within a tuple. If we wish to extract just one element from a tuple, we can use the std::get generic function. The generic std::get function is parameterized by an integer that serves as an index into the tuple. As with vectors, the first element of the tuple is found at index zero.

C++ supports another way of unpacking tuples. Structured binding is similar to `std::tie` but can be used only when declaring the variables used to represent the components of a tuple. With structured binding we can rewrite the following code:

```
std::string word, name = "Jan";
int number, age = 25;
double quantity, amount = 50.2;
auto t = std::make_tuple(name, age, amount);
// Unpack the tuple's components
std::tie(word, number, quantity) = t;
```

as

```
std::string name = "Jan";
int age = 25;
double amount = 50.2;
auto t = std::make_tuple(name, age, amount);
// Unpack the tuple's components
auto [word, number, quantity] = t;
```

The statement

```
auto [word, number, quantity] = t;
```

constitutes the structured binding. Note that we can use this special syntax only when declaring the variables to be bound to the components of the tuple. This copies the components of the tuple into the newly declared variables. Specifically, the following statement:

```
[word, number, quantity] = t; // Illegal, not a declaration
```

is illegal, even if the variables `word`, `number`, and `quantity` are properly declared before this statement.

We can specify that the structured binding be done by reference, as in the following:

```
auto& [word, number, quantity] = t;
```

In this case each name within the binding becomes an alias to a component of the tuple. In the previous code fragment above, reassigning `number` will similarly modify the second component of tuple `t`.

Structured binding is especially convenient when processing tuples within loops. Listing 21.7 (`tupleloop.cpp`) uses structured bindings by reference to reassign the elements in a vector of tuples. The program then uses structured bindings to extract the components of each tuple to print them out.

### Listing 21.7: tupleloop.cpp

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <tuple>

int main() {
    // Create a vector that can hold ten tuples
    std::vector<std::tuple<std::string, int, double>> vec(10);
}
```
