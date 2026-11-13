
## FIGURE 13.1 Selectionsort

## A Program

```
// FILE: select.cxx
// An interactive test program for the selectionsort function
#include <algorithm> // Provides swap
#include <cstddef> // Provides EXIT_SUCCESS, size_t
#include <iostream> // Provides cout and cin
using namespace std;

// PROTOTYPE of the function used in this test program:
void selectionsort(int data[], size_t n);
// Precondition: data is an array with at least n components.
// Postcondition: The elements are rearranged so that data[0] <= data[1] <= ... <= data[n-1].

int main( )
{
    const char BLANK = ' ';
    const size_t ARRAY_SIZE = 10; // Number of elements in the array to be sorted
    int data[ARRAY_SIZE]; // Array of integers to be sorted
    int user_input; // Number typed by the user
    size_t number_of_elements; // How much of the array is used
    size_t i; // Array index

    // Provide some instructions.
    cout << "Please type up to " << ARRAY_SIZE << " positive integers. ";
    cout << " Indicate the list's end with a zero." << endl;

    // Read the input numbers.
    number_of_elements = 0;
    cin >> user_input;
    while ((user_input != 0) && (number_of_elements < ARRAY_SIZE))
    {
        data[number_of_elements] = user_input;
        ++number_of_elements;
        cin >> user_input;
    }

    // Sort the numbers, and print the result with two blanks after each number.
    selectionsort(data, number_of_elements);
    cout << "In sorted order, your numbers are: " << endl;
    for (i = 0; i < number_of_elements; ++i)
        cout << data[i] << BLANK << BLANK;
    cout << endl;

    return EXIT_SUCCESS;
}
```

## (FIGURE 13.1 continued)

```
void selectionsort(int data[ ], size_t n)
// Library facilities used: algorithm, cstdlib
{
    size_t i, j, index_of_largest;
    int largest;

    if (n == 0)
        return; // No work for an empty array

    for (i = n-1; i > 0; --i)
    {
        largest = data[0];
        index_of_largest = 0;
        for (j = 1; j <= i; ++j)
        {
            if (data[j] > largest)
            {
                largest = data[j];
                index_of_largest = j;
            }
        }
        swap(data[i], data[index_of_largest]);
    }
}
```

## Sample Dialogue

Please type up to 10 positive integers. Indicate the list's end with a zero.

80 10 50 70 60 90 20 30 40 0

In sorted order, your numbers are:

10 20 30 40 50 60 70 80 90

In the selectionsort implementation, you will notice that i and n are both size_t, so we have added an extra if-statement to handle the case of "sorting an empty array" (the case where n is zero). In this case, the function has no work to do (there are no elements to sort), but since size_t values may not be negative, we must avoid the assignment i = n-1.

## Selectionsort—Analysis

We want to analyze the worst-case running time for the selectionsort algorithm that we implemented as the function selectionsort shown in Figure 13.1. Let us use n for the number of items to be sorted. In the function selectionsort, n is the value of the size_t parameter n.
In outline form, the main work of the selectionsort algorithm is given here:

```
for (i = n-1; i > 0; --i)
swap(data[i], data[suitable index]);
```

When i is equal to n-1, then data[suitable index] is the largest element in the array; when i is equal to n-2, then data[suitable index] is the second-largest element in the array, and so forth.

How many operations are performed by this for-loop? The answer is not easy. Many of the operations are hidden. The loop control variable, i, is compared to zero at the start of each loop iteration. The swap function uses some number of assignment operations, and the calculation of the “suitable index” requires some work. The value of i is decremented at the end of each loop iteration. We could determine the precise number of operations for each of these subtasks in the loop. However, that is more detail than we need. We are only looking for a big-O approximation, which means that we do not need the exact values for constants. This will simplify our analysis significantly.

During each iteration of the loop, there is some constant number of operations in managing the loop control variable, and there is some constant number of operations involved in the call to the swap function. So the number of operations in each loop iteration is the sum:

some constant + the cost of finding the suitable index

Since there are n-1 loop iterations, the total count of the number of operations performed is given by the product:

(n - 1) × (some constant + the cost of finding the suitable index)

To change this into a nice formula expressed in terms of n, we need to determine the cost of finding the “suitable index.”

As it turns out, when the algorithm is looking for the value to place in location data[i], the “suitable index” is the index of the largest of the values

```
data[0], data[1], ..., data[i]
```

The selectionsort algorithm uses a for-loop to determine the location of this largest element and thereby the value of the “suitable index.” This loop looks at each of these array elements and performs some constant number of operations with each of them. Since i can be as large as n-1, in the worst case, the loop will look at all n array elements from data[0] to data[n-1] and perform a constant number of operations on each one. Hence, our estimate of the number of operations to find this “suitable index” is at most a constant times n.

Putting this information together, we see that the total count of the number of operations performed in the selectionsort is this:

Total = (n - 1) × (some constant + the cost of finding the suitable index)
≤ (n - 1) × [some constant + (some other constant) × n]

Now we need to estimate the quantity:

(n - 1) × [some constant + (some other constant) × n]

If you multiply this out, you will get an n² term, an n term, and a constant term without any n. Thus, the number of operations performed is:

```
n² × (some new constant)
+
n × (some other new constant)
+
(yet another new constant)
```

This is our estimate of the worst-case running time for selectionsort. Because we are doing a big-O analysis, we can ignore the constants and only consider the highest exponent of n. Hence, we see that the worst-case running time for selectionsort is O(n²).

This analysis of the running time for selectionsort did not depend on the initial values in the array. The selectionsort algorithm performs the same number of operations no matter what values are in the array that it sorts. Thus, the average-case running time (and even the best-case running time) is the same as the worst-case running time.

> **Selectionsort Running Time**
> 
> The worst-case running time, the average-case running time,
> and the best-case running time for selectionsort are all
> quadratic.

## PROGRAMMING TIP

### ROUGH ESTIMATES SUFFICE FOR BIG-O

We have just computed big-O expressions for the worst-case running time of the selectionsort algorithm. Notice that when we performed the big-O analyses, we did not compute exact formulas for the running times. For example, when we estimated the number of operations in one iteration of the primary loop used in the algorithm, we decided that the algorithm performed the following number of operations in each loop iteration:

```
some constant + the cost of finding the suitable index
```

Notice that we never computed the exact value of "some constant." Because big-O expressions are accurate only "to within a constant multiple," the exact value of the constant does not matter. If we want only a big-O expression, there is no reason to spend time computing an exact value for this constant.

## Insertionsort

Another simple and natural sorting algorithm is based on the following illustration of sorting an array that contains this list of 10 integers:

```
( 8, 2, 5, 3, 10, 7, 1, 4, 6, 9 )
```

One way to proceed is to take the numbers one at a time and build up another sorted list of values. The first number is 8, so make a list that contains only the one number 8. That is certainly a sorted list. Next take the 2 and combine it with the 8 to obtain a longer sorted list, namely (2, 8). Next, add the 5 to obtain the list: (2, 5, 8).

If you keep adding numbers to the list, you will eventually obtain a sorted list containing all the numbers. The original list decreases by one on each iteration, and the list we are building increases by one on each iteration. The progress of this process is shown here for the example list:

- ( ) ( 8, 2, 5, 3, 10, 7, 1, 4, 6, 9 )
- ( 8 ) ( 2, 5, 3, 10, 7, 1, 4, 6, 9 )
- ( 2, 8 ) ( 5, 3, 10, 7, 1, 4, 6, 9 )
- ( 2, 5, 8 ) ( 3, 10, 7, 1, 4, 6, 9 )
- ( 2, 3, 5, 8 ) ( 10, 7, 1, 4, 6, 9 )
- ( 2, 3, 5, 8, 10 ) ( 7, 1, 4, 6, 9 )
- ( 2, 3, 5, 7, 8, 10 ) ( 1, 4, 6, 9 )
- ( 1, 2, 3, 5, 7, 8, 10 ) ( 4, 6, 9 )
- ( 1, 2, 3, 4, 5, 7, 8, 10 ) ( 6, 9 )
- ( 1, 2, 3, 4, 5, 6, 7, 8, 10 ) ( 9 )
- ( 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ) ( )
