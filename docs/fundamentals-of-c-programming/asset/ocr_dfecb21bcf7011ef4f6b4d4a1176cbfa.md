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
    std::cout << "[" << s << ", " << ", " << i << ", " << d << "]\n";
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

# Listing 21.8: pairtest.cpp

```
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
}
```