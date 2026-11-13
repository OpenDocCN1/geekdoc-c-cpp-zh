# Self-Test Exercises for Section 4.2

+   8. Suppose that p is a value parameter of type int*. What happens when a function does an assignment to *p?
+   9. When should a pointer parameter be a reference parameter?
+   10. Suppose that an array is passed as a parameter. How does this differ from the usual use of a value parameter?
+   11. Write the prototype for a function called make_intarray. The function takes two reference parameters: a pointer that will be used to point to the array, and a size_t data type to indicate the size of the array.
+   12. Write a function with one reference parameter that is a pointer to an integer. The function allocates a dynamic array of n integers, making the pointer point to this new array. It then fills the array with 0 through n - 1.
+   13. Why do average and compare on page 175 use the keyword const with the data array, but fill_array does not?
+   14. Write a function that copies n elements from the front of one integer array to the front of another. One of the arrays should be a const parameter, and the other should be an ordinary array parameter.
+   15. Describe in English the behavior of the program in Figure 4.7.

# FIGURE 4.7 Demonstration Program for Dynamic Arrays

# A Program

```
// FILE: dynamdemo.cxx
// This is a small demonstration program showing how a dynamic array is used.
#include <iostream> // Provides cout and cin
#include <cstddef> // Provides EXIT_SUCCESS and size_t
#include <cassert> // Provides assert
using namespace std;

// PROTOTYPES for functions used by this demonstration program
void allocate_doubles(double*& p, size_t& n);
// Postcondition: The user has been prompted for a size n, and this size has been read.
// The pointer p has been set to point to a new dynamic array containing n doubles.
// NOTE: If there is insufficient dynamic memory, then bad_alloc is thrown.

void fill_array(double data[], size_t n);
// Precondition: data is an array with at least n components.
// Postcondition: The user has been prompted to type n doubles, and these
// numbers have been read and placed in the first n components of the array.
```