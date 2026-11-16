```
```cpp
// Compare vector outcomes
// void Tester::check_equals(const std::string& msg,
    const std::vector<int>& expected,
    const std::vector<int>& actual) {
    std::cout << "[" << msg << "] ";
    total_count++; // Count this test
    if (expected == actual) {
        std::cout << "OK\n";
    } else {
        error_count++; // Count this failed test
        std::cout << "*** Failed! Expected: ";
        print_vector(expected);
        std::cout << " Actual: ";
        print_vector(actual);
        std::cout << "\n";
    }
}
// Display final test statistics
void Tester::report_results() const {
    std::cout << "\n----------------------------------------\n";
    std::cout << "[" << total_count << " tests run, "
        << total_count - error_count << " passed, "
        << error_count << " failed]\n";
    std::cout << "----------------------------------------\n";
}
```
```

# Listing 16.8: testvectorstuff.cpp

```
```cpp
#include <iostream>
#include <vector>
#include "tester.h"

// sort has a bug (it does not do anything)
void sort(std::vector<int>& vec) { // Not yet implemented
}

// sum has a bug (misses first element)
int sum(const std::vector<int>& vec) {
    int total = 0;
    for (size_t i = 1; i < vec.size(); i++)
        total += vec[i];
    return total;
}

int main() {
    Tester t; // Declare a test object
    // Some test cases to sort
    std::vector<int> vec { 4, 2, 3 };
    sort(vec);
    t.check_equals("Sort test #1", {2, 3, 4}, vec);
    vec = { 2, 3, 4};
```
```