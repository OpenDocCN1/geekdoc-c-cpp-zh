# Function Templates 703

# EXAMPLE: (continued)

Our generic sorting function has separated the implementation from the declaration of the sorting function by placing the definition of the sorting function in the file sort.cpp (Display 16.3). However, most compilers do not allow for separate compilation of templates in the usual sense. So, we have separated the implementation from the programmer's point of view, but from the compiler's point of view it looks like everything is in one file. The file sort.cpp #included in our main file, so it is as if everything is in one file. Note the include directive for sort.cpp is placed before any invocation of the functions defined by templates. For most compilers, this is the only way to get templates to work.

Display 16.2 A Generic Sorting Function (part 1 of 2)

```
//Demonstrates a template function that implements
// a generic version of the selection sort algorithm.
#include <iostream>
using std::cout;
using std::endl;
```

```
template<class T>
void sort(T a[], int numberUsed)
//Precondition: numberUsed <= declared size of the array a.
//The array elements a[numberUsed - 1] have values.
//The assignment and < operator work for values of type T.
//Postcondition: The values of a[0] through a[numberUsed - 1] have
been rearranged so that a[0] <= a[1] <= <= a[numberUsed - 1].
```

```
template<class T>
void swapValues(T& variable1, T& variable2);
//Interchanges the values of variable1 and variable2.
//The assignment must work correctly for the type T.
```

```
template<class T>
int indexOfSmallest(const T& a, int startIndex, int numberUsed);
//Precondition: 0 <= startIndex < numberUsed. Array elements have
//values.
//The assignment and < operator work for values of type T.
//Returns the index i such that a[i] is the smallest of the values
//a[startIndex], a[startIndex+1], ..., a[numberUsed - 1].
```

```
#include "sort.cpp"
int main ()\{
    int i;
    int a[] = {9, 8, 7, 6, 5, 1, 2, 3, 0, 4};
    cout << "Unsorted integers:\n";
```

This is equivalent to placing the function template definitions in this file at this location.

(continued)