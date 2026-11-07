![](bbox=[0.2475, 0.0893, 0.8325, 0.3139])

**Legend:**
- recursive call
- main function
- call
- p: pivot

**Note:** The base case in each branch is reached when the corresponding partition is empty.

**Figure 17.11** The idea of the quick sort algorithm

# **Program 17.8** Quick sort program

```
```cpp
/***************************************************************
 * A program that uses the quicksort algorithm to sort an array *
 * by calling the partition algorithm recursively              *
 ***************************************************************/
#include <iostream>
using namespace std;

// Function declarations
void swap (int& x, int& y);
void print (int array[], int size);
int partition (int arr[], int beg, int end);
void quickSort (int arr[], int beg, int end);

int main ()
{
    // Declaration of an unsorted array
    int array [10] = {27, 22, 11, 94, 83, 14, 30, 19, 46, 33};
    // Printing unsorted array
    cout << "Original array: " << endl;
    print (array, 10);
    // Calling quickSort function
    quickSort (array, 0, 9);
    // Printing sorted array
    cout << "Sorted array: " << endl;
```
```