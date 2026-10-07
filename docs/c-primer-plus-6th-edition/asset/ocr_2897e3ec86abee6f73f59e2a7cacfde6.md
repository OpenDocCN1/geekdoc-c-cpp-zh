# Introducing Arrays

Much of the usefulness of the array comes from the fact that you can access array elements individually.The way to do this is to use a subscript, or an index, to number the elements. C++ array numbering starts with zero. (This is nonnegotiable; you have to start at zero. Pascal and BASIC you will have to adjust.) C++ uses a bracket notation with the index to specify an array element. For example, months[0] is the first element of the months, and months[11] is the last. Note that the last element is less than the size of the array (see Figure 4.1).Thus, an array declaration enables you to create a lot of variables with a single declaration, and you can then use an index to identify and access individual elements.

```
int ragnar[7];
```

| 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---||
| ragnar | | | | | | | |

subscripts (or indices)
ragnar
third element
second element
first element
ragnar is an array holding seven values, each of which is a type int variable

Figure 4.1 Creating an array.

The Importance of Valid Subscript Values
The compiler does not check to see if you use a valid subscript. For instance, the compiler will not complain if you assign a value to the nonexistent element months[101]. But that assignment could cause problems when the program runs, possibly corrupting data or code, possibly causing the program to abort. It is your responsibility to make sure that your program uses only subscript values.

The yam analysis program in Listing 4.1 demonstrates a few properties of arrays, including declaring an array, assigning values to array elements, and initializing an array.

Listing 4.1 arrayone.cpp

```
// arrayone.cpp -- small arrays of integers
#include <iostream>
int main() {
    using namespace std;
    int yams[3]; // creates array with three elements
yams[0] = 7; // assign value to first element
```