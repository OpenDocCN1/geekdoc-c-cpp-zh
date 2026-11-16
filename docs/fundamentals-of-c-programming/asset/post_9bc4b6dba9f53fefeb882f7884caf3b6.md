

```
int count = 1;
double quant = 10.0;
// Populate the vector
for (auto& [s, i, d] : vec) {
    s = "Item #" + std::to_string(count);
    i = count++;
    d = quant;
    quant += 10;
}
// Print the contents of the vector
for (auto [s, i, d] : vec)
    std::cout << "[" << s << ", " << i << ", " << d << "]\n";
}
```

Listing 21.7 (tupleloop.cpp) prints the following:

```
[Item #1, 1, 10]
[Item #2, 2, 20]
[Item #3, 3, 30]
[Item #4, 4, 40]
[Item #5, 5, 50]
[Item #6, 6, 60]
[Item #7, 7, 70]
[Item #8, 8, 80]
[Item #9, 9, 90]
[Item #10, 10, 100]
```

The C++ standard library supports a special case of std::tuple called std::pair. While a std::tuple supports zero or more components, each std::pair object must contain exactly two components. Listing 21.8 (pairtest.cpp) shows std::pair in action.

## Listing 21.8: pairtest.cpp

```cpp
#include <iostream>
#include <string>
#include <tuple>

int main() {
    // Declare some local variables
    // string word;
    int number;
    double quantity;

    // Construct a pair directly with some literal values
    std::pair<std::string, double> t1 ("Bob", 9.5);
    // Unpack the pair using ::tie
    std::tie(word, quantity) = t1;
    // Print the results
    std::cout << "word = " << word << ", quantity = " << quantity << '\n';

    // Use std::make_pair convenience function
    auto t2 = std::make_pair("Eve", 22);
    // Unpack the pair using std::get
    word = std::get<0>(t2); // 1st component
    number = std::get<1>(t2); // 2nd component
    // Print the results
    std::cout << "word = " << word << ", number = " << number << '\n';
    // Declare some variables
    std::string name = "Jo";
    int age = 12;
    // Build a pair from more general expressions
    auto t3 = std::make_pair(name + "ann", 2 * age);
    // Unpack the tuple using first and second fields
    word = t3.first; // 1st component
    number = t3.second; // 2nd component
    // Print the results
    std::cout << "word = " << word << ", number = " << number << '\n';
    // Use structured binding to extract components
    auto [wrd, nbr] = t3;
    // Print the results
    std::cout << "word = " << wrd << ", number = " << nbr << '\n';
}
```

As Listing 21.8 (pairtest.cpp) shows, we can use `std::tie`, `std::get`, and structured binding with a `std::pair` object, and they work exactly as they do with `std::tuple`. Since pair objects always contain exactly two elements the `std::pair` class provides the public fields `first` and `second` through which we can unpack a pair using simpler syntax.

Neither `std::tuple` nor `std::pair` are associative containers. The `std::pair` class is used by the two associative containers we will consider next: `std::map` and `std::unordered_map`.

## 21.4 The std::map Data Type

The `std::map` data structure is another example of a C++ associative container. In order to use a `std::map` object within a program we must use the appropriate `#include` directive:

```cpp
#include <map>
```

The `std::map` class is a template class, so when declaring an instance we must supply type parameters within angle brackets as shown in the following example:

```cpp
std::map<std::string, int> my_map;
```

Here the `my_map` variable refers to an associative container that holds `std::pair` objects, each of which consist of a string key and an integer value. We say each integer in the map object has an associated string key. In the expression `std::map<std::string, int>` the first template argument (here `std::string`) indicates the map's key type, and the second template argument indicates the type of values stored in the map (here `int`). Listing 21.9 (simplemap.cpp) provides a simple example that uses a C++ map object.

### Listing 21.9: simplemap.cpp

```cpp
#include <map>
#include <string>
#include <iostream>

int main() {
    std::map<std::string, int> container;
    container["Fred"] = 22;
    container["Ella"] = 21;
    container["Owen"] = 34;
    container["Zoe"] = 29;
    std::cout << container["Ella"] << '\n';
    std::cout << container["Zoe"] << '\n';
}
```

Note that in this case we access an element in a map object via operator[] with a string "index" rather than a nonnegative integer index as we would in a vector. In Listing 21.9 (simplemap.cpp) the statement

```cpp
container["Fred"] = 22;
```

associates the value 22 with the key "Fred". Keys must be unique; that is, no two values in an unordered map can have the same key. Duplicate values are allowed; that is, two different keys can have the same value, but two different values cannot have the same key. This is similar to a vector or array, in that the same value may be stored at different indices, but only one value may be associated with a particular index.

One big difference between a map and vector is a vector of size n allows any index in the range 0..n - 1, while a map contains a key only when the programmer specifically uses it with the unordered map. Consider the statement

```cpp
container["Fred"] = 22;
```

if the key within the square brackets ("Fred") does not exist in the map before this statement executes, the statement adds the key to the map and pairs it with the value on the right of the assignment operator. If the key already exists in the map, the statement replaces the value previously associated with the key with the new value on the right of the assignment operator.

Consider accessing a value with a given key rather than assigning the value: the statement

```cpp
std::cout << container["Fred"] << '\n';
```

prints the value associated with the key "Fred". If "Fred" is not currently a key in the map, this statement will add the key "Fred" with the default value for the type of value declared for the map. For integers, the default value is 0. As other examples, the default floating-point value is 0.0, the default string value is the empty string, "", and the default bool value is false.

You would use a map object when you need fast and convenient access to an element of a collection based on a search key rather than an index. Consider the problem of implementing a simple telephone contact list. Most people are very familiar with the names of their friends, family, and business contacts but can remember only a handful of telephone numbers. A contact list associates a name with a telephone number.

It would be inappropriate to place the names in a vector, for example, and locate a name using the associated phone number as an index into the vector. This look-up method is backwards—we do not want to find a name given a phone number; we want to look up a number based on a name. Besides, each phone number contains many digits, and we would not need or want to have a vector with indices that large—most of the space in the data structure would be unused.

In our situation a person or company's name is a unique identifier for that contact. In this case the name is a key to that contact. A map is an ideal data structure for mapping keys to values. It allows for the fast retrieval of a value given its associated key. Listing 21.10 (phonelist.cpp) uses a C++ map to implement a simple telephone contact database with a rudimentary command line interface.

## Listing 21.10: phonelist.cpp

```cpp
#include <iostream>
#include <string>
#include <map>
#include <algorithm>

int main() {
    std::map<std::string, int> contacts; // Telephone contact list
    bool running = true;

    while (running) {
        std::string name;
        int number;
        char command;
        std::cout << "(A)dd (L)ook up (Q)uit: ";
        std::cin >> command;
        switch (command) {
        case 'A':
        case 'a':
            //std::cout << "Enter new name: " << '\n';
            std::cin >> name;
            std::transform(std::begin(name), std::end(name),
                           std::begin(name), toupper);
            //std::cout << "Enter phone number for " << name << ": ";
            std::cin >> number;
            contacts[name] = number;
            break;

        case 'L':
        case 'l':
            std::cin >> name;
            transform(std::begin(name), std::end(name), std::begin(name),
                      toupper);
            std::cout << name << " " << contacts[name] << '\n';
            break;
        case 'Q':
        case 'q':
            running = false;
            break;
        case 'D': // Secret command
        case 'd':
            for (auto& elem : contacts)
                std::cout << elem.first << " " << elem.second << '\n';
            break;
        default:
            std::cout << command << " is not a valid command" << '\n';
        }
    }
}
```

The following shows a sample run of Listing 21.10 (phonelist.cpp):

