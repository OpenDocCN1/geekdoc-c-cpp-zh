
# Listing 11.2: averagenumbers2.cpp

```cpp
#include <iostream>

using namespace std;

int main() {
    double sum = 0.0, num;
    const int NUMBER_OF_ENTRIES = 5;
    cout << "Please enter " << NUMBER_OF_ENTRIES
    cout << " numbers: ";
    for (int i = 0; i < NUMBER_OF_ENTRIES; i++) {
        cin >> num;
        sum += num;
    }
    cout << "The average of " << NUMBER_OF_ENTRIES << " values is " << sum/NUMBER_OF_ENTRIES << endl;
}
```

Listing 11.2 (averagenumbers2.cpp) behaves differently from Listing 11.1 (averagenumbers.cpp), as the following sample run using the data shows:

```
Please enter five numbers: 9 3.5 0.2 100 15.3
The average of the five is 25.6
```

Listing 11.2 (averagenumbers2.cpp) can be modified to handle 25 values more easily than Listing 11.1 (averagenumbers.cpp) that must use 25 separate variables—just change the constant NUMBER_OF_ENTRIES. In fact, coding the change to 1,000 numbers is no more difficult. However, unlike the original, this new version does not display the numbers entered. This is a significant difference; it may be necessary to retain all the values so the user can verify their correctness.

- All values can be displayed in different ways; for example, they may be placed in a graphical user interface component, like a visual grid (spreadsheet).
- The values may need to be processed in a different way after they are all entered; for example, we may wish to display the values entered after a certain value (greater than zero), but the limit is not determined until all the numbers are entered.

In all of these situations we must retain the values of all the variables for future recall. We need to combine the advantages of both of the above programs; specifically we want:

- the ability to retain individual values, and
- the ability to dispense with creating individual variables to store all the individual values

These may seem like contradictory requirements, but C++ provides several standard data structures that simultaneously provide both of these advantages. In this chapter we will examine two of these structures: vectors and arrays.

## 11.1 Vectors

A vector in C++ is an object that manages a block of memory that can hold multiple values simultaneously; a vector, therefore, represents a collection of values. A vector has a name, and we may access the values it contains via position within the block of memory managed by the vector. A vector stores a sequence of values, and the values must all be of the same type. A collection of all of the same type is said to be homogeneous.

### 11.1.1 Declaring and Using Vectors

In order to use a vector object within a C++ program, you must add the preprocessor directive

```cpp
#include <vector>
```

The vector type is part of the standard (std) namespace, so its full name is std::vector, just like the full name of count is std::cout (Section 2.1). If you include the statement

```cpp
using namespace std;
```

or

```cpp
using std::vector;
```

at the top of your source file, you can use the shorter name vector within your code. The remainder of the examples in this chapter assume the necessary using and so uses the short name, vector.

We declare a vector object that can hold integers as simply as

```cpp
vector<int> vec_a;
```

The type angle brackets may be any valid C++ data type. When declared this, the vector vec_a is initially empty.
We declare a vector with a particular initial size as follows:

```cpp
vector<int> vec_b(10);
```

Here vec_b initially holds 10 integers. All 10 elements are zero by default. The vector's size appears within parentheses following the vector's name.
We declare a vector object of given size and specify the initial value of all its elements:

```cpp
vector<int> vec_c(10, 8);
```

In this example vec_c initially holds 10 integers, all having the value 8. The first number in the parentheses following the vector's name identifies the number of elements, and the second specifies the initial value of all the elements.
We declare a vector and specify each element separately:

```cpp
vector<int> vec_d{10, 20, 30, 40};
```

Note the elements appear within curly braces, not parentheses. The list of elements within the curly braces constructs a vector. This kind of declaration is practical only for small vectors. Figure 11.1 provides a conceptual illustration of the vectors vec_a, vec_b, and vec_d.

```cpp
vector<int> vec_a;
vector<int> vec_b(10);
vector<int> vec_c(10, 8);
vector<int> vec_d{10, 20, 30, 40};
```

| vec_a | vec_b | vec_c | vec_d |
| :--- | :--- | :--- | :--- |
| 0 | 0 | 8 | 10 |
| 1 | 0 | 8 | 20 |
| 2 | 0 | 8 | 30 |
| 3 | 0 | 8 | 40 |
| 4 | 0 | 8 | |
| 5 | 0 | 8 | |
| 6 | 0 | 8 | |
| 7 | 0 | 8 | |
| 8 | 0 | 8 | |
| 9 | 0 | 8 | |

Figure 11.1: Four different declaration statements and conceptual illustrations of the resulting vectors

Like any other variable, a vector can be local or global, and it must be declared before it is used. The vector initializes `vector<int> vec_d{10, 20, 30, 40};` is a C++11 language feature and, therefore, is not supported by older C++ compilers; in particular, C++ compilers for Visual Studio prior to 2013 do not support this syntax.

When we have a non-empty vector object, we can access its elements using the vector's name, the square bracket, and an integer index:

```cpp
vector<int> list(3);      // Declare list to be a vector of three ints
list[0] = 5;               // Make the first element 5
list[1] = -3;              // Make the second element -3
list[2] = 12;             // Make the last element 12
cout << list[1] << endl; // Print the element at index 1
```

This code fragment shows how the square brackets allow us to access an individual element based on the element's position within the vector. The number within the square brackets indicates the distance from the beginning of the vector. The expression `list[0]` indicates the element at the very beginning (a distance of zero from the beginning), and `list[1]` is the second element (a distance of one away from the beginning). After executing these assignment statements, the list vector looks like Figure 11.2.

```cpp
vector<int> list(3);
list[0] = 5;
list[1] = -3;
list[2] = 12;
```

| index | value |
|---|---|
| 0 | 5 |
| 1 | -3 |
| 2 | 12 |

Figure 11.2: The numbers below the vectors represent index, or positions, within the vector. The first element in a vector is found at index 0, not 1.

Vectors may hold any valid C++ data type. The following code fragment declares three vectors of

```cpp
vector<int> list;
vector<double> collection{1.0, 3.5, 0.5, 7.2};
vector<char> letters{'a', 'b', 'c'};
```

Here list is empty but can contain values, collection is a vector of double-precision floating-point numbers initialized the values contained in the initializer list, and letters holds the lowercase version of the first three letters of the English alphabet. Figure 11.3 illustrates these three vector objects. We can observe two key points from Figures 11.1–11.3:

- Vectors store their elements in a contiguous block of memory. This is, for example, the memory occupied by the element at index 2 follows immediately after the memory occupied by the element at index 1 and immediately before the element at index 3.
- Elements in a vector are located by a numeric index. The first element is at index zero, not one.

In an expression such as `list[3]`, it would be out of bounds.

```cpp
vector<int> list;
vector<double> collection{1.0, 3.5, 0.5, 7.2};
vector<char> letters{'a', 'b', 'c'};
```

| collection | letters |
|--- |--- |
| 1.0 | 'a' |
| 3.5 | 'b' |
| 0.5 | 'c' |
| 7.2 | |

Figure 11.3: Vectors containing different types of elements.
