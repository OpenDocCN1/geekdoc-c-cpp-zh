
```cpp
// time how long it takes

// Largest potential prime considered
// const int MAX = 500000;
const int MAX = 500;

// Each position in the Boolean array indicates
// if the number of that position is not prime;
// false means "prime," and true means "composite."
// Initially all numbers are prime until proven otherwise
bool nonprimes[MAX]; // Global array initialized to all zeros

int main() {
    clock start_time = clock(); // Record start time
    // First prime number is 2; 0 and 1 are not prime
    nonprimes[0] = true;

    // Start at the first prime number, 2.
    for (int i = 2; i < MAX; i++) {
        if (!nonprimes[i]) {
            cout << i << ", \n            // It is prime, so eliminate all of its
            // multiples that cannot be prime
            for (int j = i+2; j < MAX; j += i)
                nonprimes[j] = true;
        }
    }
    cout << endl; // Move cursor down to next line
    // Print the elapsed time:
    cout << "Elapsed time: "
         << static_cast<double>(clock() - start_time)/CLOCKS_PER_SEC
         << " seconds" << endl;
}
```

Listing 8.8 (measuresprimespeed.cpp), which also prints all the prime numbers up to 500,000. Using reduction (Section 8.4), Listing 8.8 (measuresprimespeed.cpp) takes 77 seconds. In comparison, Listing F4 (fasterprimespeed.cpp) takes about two seconds to perform the same task on the system. This is comparable to the square root version, Listing 8.5 (moreefficientprimes.cpp), which takes two seconds to run. If the goal is to print the prime numbers up to 1,000,000, the original version averages 271 seconds, or about four and one half minutes. The square root version averages 4.5 seconds. The new, array-based version averages 25 seconds. For 5,000,000 the optimized original version takes over an hour and 33 minutes, the square root version takes a respectable 39 seconds, but array version averages 9 seconds to run.

## F.4 Multidimensional Arrays

The arrays we have so far have been one dimensional—simple sequences of values. C++ supports higher-dimensional arrays. A two-dimensional array is a block of memory that is visualized with rows and columns. The statement

## F.4. MULTIDIMENSIONAL ARRAYS

```cpp
int a[2][3];
```

declares a to be a two-dimensional (2D) array of integers. A 2D array is sometimes called a matrix. In this case, the declaration specifies that array contains two rows and three columns. Figure F.4 shows the logical structure of the array created by the following sequence of code:

```cpp
int a[2][3]; // a is a 2D array
a[0][0] = 5;
a[0][1] = 19;
a[0][2] = 3;
a[1][0] = 22;
a[1][1] = -8;
a[1][2] = 10;
```

| | 5 | 19 | 3 |
|---|---|---|---|
| 1 | 22 | -8 | 10 |
| | 0 | 1 | 2 |

Figure F.4: A 2 × 3 two-dimensional array

The two-dimensional array is said to be a 2 × 3 array, meaning it has two rows and three columns (as shown in Figure F.4). Rows are arranged horizontally, and the values in columns are arranged vertically. In each of the assignment statements above, for example

```cpp
a[1][0] = 22;
```

the first index (1) signifies the row and the second index (here 0) denotes the column of the element within the array.

Using a syntax to initialize the lists of one-dimensional arrays, the 2D array a from above could have been declared and created:

```cpp
int a[2][3] = { { 5, 19, 3 }, { 22, -8, 10 } };
```

Note that each array has its own set of curly braces, and each row looks like 1D array initialization list. You may omit the first index, as shown:

```cpp
int a[][3] = { { 5, 19, 3 }, { 22, -8, 10 } };
```

## F4. MULTIDIMENSIONAL ARRAYS

For 2D arrays initialized in this manner the first subscript is optional, but the second subscript (that is, the size of each column) is required.

To access an element of a 2D array, use two subscripts:

```cpp
a[r][c] = 4;                                // Assign element at row r, column c
cout << a[m][n] << endl;                     // Display element at row m, column n
```

The following function prints the contents of a ROWS x COLUMNS 2D array of doubles:

```cpp
void print (const double [ROWS][COLUMNS]) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++) {
            cout << setw(5) << m[row][col];
        }
    }
}
```

The declaration of the parameter m is quite complicated. We can simplify the syntax by a C++ typedef. The statement

```cpp
typedef Matrix [ROWS][COLUMNS];
```

defines a new name Matrix. If you use the word typedef from the statement, it defines a declaration of a 2D array Matrix. The typedef keyword changes the meaning of the statement so instead of declaring a variable it defines a type. typedef statements usually appear near the top of a source file and often have global scope. It is uncommon to see a local typedef within a function body.

Given the typedef statement defines the new type name Matrix, the parameter for the print function may be expressed more simply:

```cpp
void print (const Matrix m) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++) {
            cout << setw(5) << m[row][col];
        }
    }
```

Listing F.5 (twodimarray.cpp) experiments with 2D arrays and takes advantage of the typedef to simplify the code.

Listing F.5: twodimarray.cpp
```cpp
#include <iostream>
#include <iomanip>
using namespace std;
const int ROWS = 3,
COLUMNS = 5;

// The name Matrix represents a new type
// that means a ROWS x COLUMNS
// two-dimensional array of double-precision
// floating-point numbers.
typedef double Matrix[ROWS][COLUMNS];

// Allow the user to enter the elements of a matrix
void populate_matrix(Matrix m) {
    cout << "Enter the " << ROWS << " rows of the matrix. " << endl;
    for (int row = 0; row < ROWS; row++) {
        cout << "Row " << row << " enter (" << COLUMNS << " values):";
        for (int col = 0; col < COLUMNS; col++) {
            cin >> m[row][col];
        }
    }
}

void print_matrix(const Matrix m) {
    for (int row = 0; row < ROWS; row++) {
        for (int col = 0; col < COLUMNS; col++) {
            cout << setw(5) << m[row][col];
        }
    }
}

int main() {
    Matrix mat;
    // Populate the array
    populate_matrix(mat);
    // Print the array
    print_matrix(mat);
}
```

## F.5. POINTERS AND ARRAYS

Listing F.6: pointerprint.cpp
```cpp
#include <iostream>

using namespace std;

int main() {
    int a[] = { 2, 4, 6, 8, 10, 12, 14, 16, 18, 20 },
        *p;

    p = &a[0]; // p points to first element of array

    // Print out the contents of the array
    for (int i = 0; i < 10; i++) {
        cout << *p << ' '; // Print the element p
        p++; // Increment p so it points to the next element
    }
    cout << endl;
}
```

The statement
p = &a[0];

sets p to the first element of array a. A shorter way to accomplish the same thing
p = a;

since a is itself a reference to the array's location in memory. This assignment statement clearly demonstrates the association between array variables and pointer variables. Note that the opposite assignment (a = p) is impossible, because array declared as above may not appear by itself on the left side of the assignment.

Pointer variables can participate in addition and subtraction operations.

p++;

changes the address stored in p so subsequently the pointer will point to the next integer position in memory. If p is assigned to array, incrementing p reduces it to point to a's next element. In Figure E.5, pointer is assigned to array a, incrementing it to an integer and referred to as values within a.

The expression

p[0]

is another way to write

*p

Byte in memory has a unique numeric address. Most C++ types require more than one byte of storage, incrementing a pointer by 1 does not simply add 1 to the address it holds. The amount added depends on the type of the pointer; for example, on systems using 32-bit (4 bytes) integers, incrementing an integer variable increments by 4, not 1. The compiler knows the type of the pointer because variable must declare all variables. The compiler, therefore, can automatically adjust the arithmetic to perform work. If a pointer points to memory within an array and is of the same type as the array, incrementing the pointer correctly repositions the pointer to point to the next element in the array.

©2014 Richard L. Halterman Draft date: January 26, 2014
