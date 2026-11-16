```
for (int value : numbers)
    std::cout << value << ' ';
std::cout << '\n';
}
catch (std::out_of_range& e) {
    std::cout << "Error: vector bounds exceeded\n";
    std::cout << e.what() << '\n';
}
catch (FileNotFoundException& e) {
    std::cout << "Error: cannot open file\n";
    std::cout << e.what() << '\n';
}
}
```

# 22.5 Exception Mechanics

An exception handler within a `catch` block may take a few steps to handle the exception and then *re-throw* the exception or throw a completely different exception.

# Listing 22.11: rethrow.cpp

```
#include <iostream>
#include <fstream>
#include <vector>

void filter(std::vector<int>& v, int i) {
    v.at(i)++;
}

void compute(std::vector<int>& a) {
    for (int i = 0; i < 6; i++) {
        try {
            filter(a, i);
        }
        catch (std::exception& ex) {
            std::cout << "******************************************\n";
            std::cout << "For loop terminated prematurely\n";
            std::cout << "* when i = " << i << '\n';
            std::cout << "******************************************\n";
            throw ex; // Rethrow the same exception
        }
    }
}

int main() {
    std::vector<int> list { 10, 20, 30, 40, 50 };
    try {
        compute(list);
    }
    catch (std::exception& e) {
        std::cout << "Caught an exception: " << e.what() << '\n';
    }
    std::cout << "Program finished\n";
}
```