# 7.7 Searching Arrays with Linear Search

Often a programmer will be working with large amounts of data stored in arrays. It may be necessary to determine whether an array contains a value that matches a certain key value. The process of finding a particular element of an array is called searching. In this section we discuss the simple linear search.

# Linear Search

The linear search (Fig. 7.19, lines 37–44) compares each element of an array with a search key (line 40). Because the array is not in any particular order, it is just as likely that the value will be found in the first element as the last. On average, therefore, the program must compare the search key with half the elements of the array. To determine that a value is not in the array, the program must compare the search key to every element of the array.

The linear searching method works well for small arrays or for unsorted arrays (i.e., arrays whose elements are in no particular order). However, for large arrays, linear searching is inefficient.

```
// Fig. 7.19: fig07_19.cpp
// Linear search of an array.
#include <iostream>
using std::cout;
using std::cin;
using std::endl;

int linearSearch( const int [], int, int ); // prototype

int main()
{
    const int arraySize = 100; // size of array a
    int a[ arraySize ]; // create array a
    int searchKey; // value to locate in array a

    for ( int i = 0; i < arraySize; i++ )
        a[ i ] = 2 * i; // create some data

    cout << "Enter integer search key: ";
    cin >> searchKey;

    // attempt to locate searchKey in array a
    int element = linearSearch( a, searchKey, arraySize );

    // display results
    if ( element != -1 )
        cout << "Found value in element " << element << endl;
    else
        cout << "Value not found" << endl;

    return 0; // indicates successful termination
} // end main
```