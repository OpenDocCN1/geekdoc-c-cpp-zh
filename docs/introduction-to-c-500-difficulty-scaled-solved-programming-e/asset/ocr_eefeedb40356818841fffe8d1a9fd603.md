156 Introduction to C++

# Vector of Vectors

As with two-dimensional arrays, we can declare a two-dimensional vector object. For example:

```
vector<vector<int>> v(5, vector<int>(10));
```

The v is a two-dimensional vector that contains 5 elements, where each element is a vector of 10 integers. For convenience, we can assume that v consists of five rows, where each row contains 10 integers. To access an element we use the [] syntax. For example, the following code displays the values of all elements:

```
for (int row = 0; row < v.size(); row++)
    for (int col = 0; col < v[row].size(); col++)
        cout << arr[row][col] << '\n';
```

A two-dimensional vector provides the facilities that a simple vector object provides. C.7.16 is such an example, where the dimensions of the vector will be determined dynamically, during the program execution, and not statically as with the two-dimensional arrays.

# EXERCISES

C.7.12 Write a program that creates a 5x5 upper triangular array; is in array the elements below the main diagonal should be set to 0. The program should assign random values within [-3, 3 to to the elements and display the array. Then, it should display the determinant of the array, that is, the product of the main diagonal's elements. Finally, the program should display the array in reverse form, that is, from the lower-right element to the upper-left one.

```
#include <iostream>
#include <iomanip>
#include <cstdlib>
#include <ctime>
using std::cout;
```

```
int main() {
    const int SIZE = 5;
    int i, j, determ, arr[SIZE][SIZE];

    determm = 1; // Initialize the determinant.
    srand(time(NULL));

    cout << "\nArray elements\n";
    cout << "--------------------\n";
    for (i = 0; i < SIZE; i++) {
        for (j = 0; j < SIZE; j++) {
            if (i > j)
                arr[i][j] = 0; /* The elements below the main diagonal should be set to 0. */
        }
    }\}
```