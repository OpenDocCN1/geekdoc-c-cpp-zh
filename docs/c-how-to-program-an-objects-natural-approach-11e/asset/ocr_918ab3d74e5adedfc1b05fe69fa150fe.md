```
```cpp
// fig06_10.cpp
// Initializing multidimensional arrays.
#include <iostream>
#include <array>

constexpr size_t rows{2};
constexpr size_t columns{3};
void printArray(const std::array<std::array<int, columns>, rows>& a);

int main() {
   constexpr std::array values1{std::array{1, 2, 3}, std::array{4, 5, 6}};
   constexpr std::array values2{std::array{1, 2, 3}, std::array{4, 5, 0}};

   std::cout << "values1 by row:\n";
   printArray(values1);

   std::cout << "\nvalues2 by row:\n";
   printArray(values2);
}

// output array with two rows and three columns
void printArray(const std::array<std::array<int, columns>, rows>& a) {
   // loop through array
   for (const auto& row : a) {
      // loop through columns of current row
      for (const auto& element : row) {
         std::cout << element << ' ';
      }

      std::cout << '\n'; // start new line of output
   }
}
```
```

```
```text
values1 by row:
1 2 3
4 5 6

values2 by row:
1 2 3
4 5 0
```
```

Fig. 6.10 | Initializing multidimensional arrays.

# Declaring an array of arrays

In lines 11–12, the compiler infers that values1 and values2 are arrays of arrays with two rows of three columns each and in which the elements are type int. Consider the two initializers for values1:

```
```cpp
std::array{1, 2, 3};
std::array{4, 5, 6};
```
```

From these, the compiler infers that values1 has two rows. Each of these initializers creates an array of three elements, so the compiler infers each row of values1 has three col-