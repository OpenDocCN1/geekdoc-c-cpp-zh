```
```cpp
int list[25];                 // Allocate a static array
for (int i = 0; i < 25; i++) {
    list[i] = rand() % 1000;  // Fill with pseudorandom values
    print(list, list + 25);   // Print the elements of list
```
```

The advantage of the begin/end pointer approach is that it allows a programmer to pass a *slice* of the array to the function; for example, if we wish to print the elements of the array from index 3 to index 7, we would call the function as

```
```cpp
print(list + 3, list + 8);   // Print elements at indices 3, 4, 5, 6, 7
```
```

# 11.2.3 Dynamic Arrays

Programmers need not worry about managing the memory used by static arrays. The compiler and run-time environment automatically ensure the array has enough space to hold all of its elements. The space held by local arrays is freed up automatically when the local array goes out of the scope of its declaration. Global arrays live for the lifetime of the executing program. Memory management for static arrays, therefore, works just like scalar variables.

Static arrays have a significant limitation: The size of a static array is determined at compile time. The programmer may change the size of the array in the source code and recompile the program, but once the program is compiled into an executable program any static array's size is fixed. For many applications the circumstances of the executing program must determine the size of an array. Static arrays lack such flexibility.

One approach to implementing a flexibly-sized array defines the array to hold as many items as it conceivably will ever need. Listing 11.17 (largearrayaverage.cpp) uses this approach.

```
```cpp
Listing 11.17: largearrayaverage.cpp
#include <iostream>
// Maximum number of expected values is 1,000,000
const int MAX_NUMBER_OF_ENTRIES = 10000000;
double numbers[MAX_NUMBER_OF_ENTRIES];
int main() {
    double sum = 0.0;
    int size;   // Actual number of entries
    // Get effective size of the array
    std::cout << "Please enter number of values to process: ";
    std::cin >> size;
    if (size > 0) {   // Nothing to do with no entries
        std::cout << "Please enter " << size << " numbers: ";
        // Allow the user to enter in the values.
        for (int i = 0; i < size; i++) {
            std::cin >> numbers[i];
            sum += numbers[i];
        }
        std::cout << "The average of ";
        for (int i = 0; i < size - 1; i++)
```
```