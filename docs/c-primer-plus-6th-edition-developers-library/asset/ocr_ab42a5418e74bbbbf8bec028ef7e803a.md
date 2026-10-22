then runs a loop until that amount of time has passed. Write a simple program that tests the function.

5. Write a function that takes as arguments the name of an array of type int elements, the size of an array, and a value representing the number of picks. The function then should select the indicated number of items at random from the array and prints them. No array element is to be picked more than once. (This simulates picking lottery numbers or jury members.) Also, if your implementation has time() (discussed in Chapter 12) or a similar function available, use its output with srand() to initialize the rand() random-number generator. Write a simple program that tests the function.

6. Modify Listing 16.17 so that it uses an array of struct names elements (as defined after the listing) instead of an array of double. Use fewer elements, and initialize the array explicitly to a suitable selection of names.

7. Here’s a partial program using a variadic function:

```
#include <stdio.h>
#include <stdlib.h>
#include <stdarg.h>
void show_array(const double ar[], int n);
double * new_d_array(int n, ...);

int main()
{
    double * p1;
    double * p2;

    p1 = new_d_array(5, 1.2, 2.3, 3.4, 4.5, 5.6);
    p2 = new_d_array(4, 100.0, 20.00, 8.08, -1890.0);
    show_array(p1, 5);
    show_array(p2, 4);
    free(p1);
    free(p2);

    return 0;
}
```

The new_d_array() function takes an int argument and a variable number of double arguments. The function returns a pointer to a block of memory allocated by malloc(). The int argument indicates the number of elements to be in the dynamic array, and the double values are used to initialize the elements, with the first value being assigned to the first element, and so on. Complete the program by providing the code for show_array() and new_d_array().