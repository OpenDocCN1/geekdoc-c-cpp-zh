
## FIGURE 4.6 A Reference Parameter That Is a Pointer

### A Function Implementation

```cpp
void allocate_doubles(double*& p, size_t& n)
    // Postcondition: The user has been prompted for a size n, and this size has been read.
    // The pointer p has been set to point to a new dynamic array containing n doubles.
    // NOTE: If there is insufficient dynamic memory, then bad_alloc is thrown.
    // Library facilities used: iostream, cstdlib
{
    cout << "How many doubles should I allocate? " << endl;
    cout << "Please type a positive integer answer: ";
    cin >> n;
    p = new double[n]; <——— Allocate the array of n doubles.
}
```

argument, array_size. The function then allocates an array of the requested size, and the argument called numbers is set to point to the first component of the array. Because the function makes its formal parameter p point to a newly allocated array of double numbers, and we want the actual argument numbers to point to the newly allocated memory, we are required to use a reference parameter.

If you have defined a type definition for a pointer type, then you can avoid the cumbersome syntax of *&. For example, if double_ptr has been defined to be a pointer to a double number, then we could write this prototype:

```cpp
void allocate_doubles(double_ptr& p, size_t& n);
```

### Reference Parameters That Are Pointers

Sometimes a function will actually change a pointer parameter so that the pointer points to a new location, and the programmer needs the change to affect the actual parameter. This is the only situation in which a reference parameter will be a pointer.

Syntax in the parameter list: Type_Name*& var_name

Example from Figure 4.6: void allocate_doubles(double*& p, size_t& n);

## Self-Test Exercises for Section 4.2

- 8. Suppose that p is a value parameter of type int*. What happens when a function does an assignment to *p?
- 9. When should a pointer parameter be a reference parameter?
- 10. Suppose that an array is passed as a parameter. How does this differ from the usual use of a value parameter?
- 11. Write the prototype for a function called make_intarray. The function takes two reference parameters: a pointer that will be used to point to the array, and a size_t data type to indicate the size of the array.
- 12. Write a function with one reference parameter that is a pointer to an integer. The function allocates a dynamic array of n integers, making the pointer point to this new array. It then fills the array with 0 through n - 1.
- 13. Why do average and compare on page 175 use the keyword const with the data array, but fill_array does not?
- 14. Write a function that copies n elements from the front of one integer array to the front of another. One of the arrays should be a const parameter, and the other should be an ordinary array parameter.
- 15. Describe in English the behavior of the program in Figure 4.7.

### FIGURE 4.7 Demonstration Program for Dynamic Arrays

### A Program

```cpp
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

### (FIGURE 4.7 continued)

```cpp
double average(const double data[], size_t n);
// Precondition: data is an array with at least n components, and n > 0.
// Postcondition: The value returned is the average of data[0]..data[n-1].

void compare(const double data[], size_t n, double value);
// Precondition: data is an array with at least n components.
// Postcondition: The values data[0] through data[n - 1] have been printed with a
// message saying whether they are above, below, or equal to value.

int main( )
{
    double *numbers; // Will point to the first component of an array
    size_t array_size;
    double mean_value;

    // Allocate an array of doubles to hold the user's input.
    cout << "This program will compute the average of some numbers. The\n";
    cout << "numbers will be stored in an array of doubles that I allocate.\n";
    allocate_doubles(numbers, array_size);

    // Read the user's input and compute the average.
    fill_array(numbers, array_size);
    mean_value = average(numbers, array_size);

    // Print the output.
    cout << "The average is: " << mean_value << endl;
    compare(numbers, array_size, mean_value);
    cout << "This was a mean program.";

    return EXIT_SUCCESS;
}
```

```cpp
void allocate_doubles(double*& p, size_t& n)
    See Figure 4.6 on page 172 for the body of this function.
```

```cpp
void fill_array(double data[], size_t n)
// Library facilities used: cstdlib
{
    size_t i;
    cout << "Please type " << n << " double numbers: " << endl;

    // Read the n numbers one at a time.
    for (i = 0; i < n; ++i)
        cin >> data[i];
}
```

### (FIGURE 4.7 continued)

```cpp
void compare(const double data[], size_t n, double value)
{
    size_t i;

    for (i = 0; i < n; ++i)
    {
        cout << data[i];
        if (data[i] < value)
            cout << " is less than ";
        else if (data[i] > value)
            cout << " is more than ";
        else
            cout << " is equal to ";
        cout << value << endl;
    }
}
```

```cpp
double average(const double data[], size_t n)
// Library facilities used: cassert, cstdlib
{
    size_t i; // An array index
    double sum; // The sum of data[0] through data[n - 1]

    assert(n > 0);

    // Add up the n numbers and return the average.
    sum = 0;
    for (i = 0; i < n; ++i)
        sum += data[i];
    return (sum/n);
}
```

### A Sample Dialogue

This program will compute the average of some numbers. The
numbers will be stored in an array of doubles that I allocate.
How many doubles should I allocate?
Please type an integer answer: 3
Please type 3 double numbers:
15.1 24.6 86.3
The average is: 42
15.1 is less than 42
24.6 is less than 42
86.3 is more than 42
This was a mean program.

## 4.3 THE BAG CLASS WITH A DYNAMIC ARRAY

Pointers enable us to define data structures whose size is determined when a program is actually running rather than at compilation time. Such data structures are called **dynamic data structures**. This is in contrast to **static data structures**, which have their size determined when a program is compiled.

A class may be a dynamic data structure—in other words, it may use dynamic memory. When a class uses dynamic memory, several new factors come into play. In this section, we’ll illustrate these factors by implementing a new bag class that contains its items in a dynamic array rather than an array of fixed size. Apart from the use of a dynamic array, the new bag is much the same as the original bag class from Section 3.1.

### Pointer Member Variables

The original bag class in Section 3.1 has a member variable that is a static array containing the bag’s items. Our new, dynamic bag has a member variable that is a pointer to a dynamic array. In both cases, the array is a **partially filled array**, containing the bag’s items at the front of the array. Here is a comparison of the member variables of the two class definitions:

```
**The Static Bag:**

// From bag1.h in Section 3.1:
class bag
{
...
private:
    value_type data[CAPACITY];
    size_type used;
};

**The Dynamic Bag:**

// From bag2.h in this section:
class bag
{
...
private:
    value_type *data;
    size_type used;
};
...
```

A static bag has a private member variable, data, which is an array that can hold up to CAPACITY items. The static bag can never hold more than CAPACITY items. That’s the limit.

On the other hand, a dynamic bag has a private variable, also called data, which is a pointer to a value_type item. The constructor for the dynamic bag will allocate a dynamic array, and point data at the newly allocated array. As a program runs, a new, larger dynamic array can be allocated when we need more capacity. Because the size of the dynamic array can change, the dynamic bag actually needs one more private member variable to keep track of how much memory is currently allocated. At the top of the next page, we show the complete private section of the new bag class, including the extra member variable.
