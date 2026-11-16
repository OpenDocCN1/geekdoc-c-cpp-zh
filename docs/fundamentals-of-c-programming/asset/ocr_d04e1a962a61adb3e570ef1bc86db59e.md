Section 10.9 indicated that call-by-value parameter passing is preferred to call-by-reference parameter passing. This is because a function using pass by value cannot modify the actual variable the caller passed to it. Observe closely that our new print function declares its formal parameter v to be a const reference. This means the function cannot modify the actual parameter passed by the caller. Passing a vector object as a constant reference allows us to achieve the efficiency of pass by reference with the safety of pass by value.

Passing by const reference is not the same as pass by value, though. The function receiving a parameter passed by value can modify the parameter and return a modified copy. A function using pass by const reference cannot modify the parameter passed to it.

Like the print function, the sum function in Listing 11.7 (vectortofunc.cpp) does not intend to modify the contents of its vector parameter. Since the sum function needs only look at the vector's contents, its vector parameter should be declared as a const reference. In general, if a function's purpose is to modify a vector, the reference should not be const. Listing 11.8 (makerandomvector.cpp) uses a function named make_random that fills a vector with pseudorandom integer values.

```
Listing 11.8: makerandomvector.cpp

#include <iostream>
#include <vector>
#include <cstdlib> // For rand

/*
 * print(v)
 * Prints the contents of an int vector
 * v is the vector to print; v is not modified
 */
void print(const std::vector<int>& v) {
    for (int elem : v)
        std::cout << elem << " ";
    std::cout << "\n";
}

/*
 * make_random(v)
 * Fills an int vector with pseudorandom numbers
 * v is the vector to fill; v is modified
 * size is the maximum size of the vector
 */
void make_random(std::vector<int>& v, int size) {
    v.clear(); // Empties the contents of vector
    int n = rand() % size + 1; // Random size for v
    for (int i = 0; i < n; i++)
        v.push_back(rand()); // Populate with random values
}

int main() {
    srand(2); // Set pseudorandom number generator seed
    std::vector<int> list;
    // Print the contents of the vector
    std::cout << "<Vector initially: ";
    print(list);
    make_random(list, 20);
    std::cout << "<Last random vector: ";
```