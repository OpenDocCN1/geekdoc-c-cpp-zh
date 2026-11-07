```
```cpp
private:
    int size; // vector size
    vector< int > data; // vector of ints
    void sortSubVector( int, int ); // sort subvector
    void merge( int, int, int, int ); // merge two sorted vectors
    void displaySubVector( int, int ) const; // display subvector
}; // end class SelectionSort
```
```

**Fig. 19.5** | *MergeSort class definition. (Part 2 of 2.)*

```
```cpp
// Fig 19.6: MergeSort.cpp
// Class MergeSort member-function definition.
#include <iostream>
#include <vector>
#include <cstdlib> // prototypes for functions srand and rand
#include <ctime> // prototype for function time
#include "MergeSort.h" // class MergeSort definition
using namespace std;

// constructor fill vector with random integers
MergeSort::MergeSort( int vectorSize )
{
    size = ( vectorSize > 0 ? vectorSize : 10 ); // validate vectorSize
    srand( time( 0 ) ); // seed random number generator using current time

    // fill vector with random ints in range 10-99
    for ( int i = 0; i < size; ++i )
        data.push_back( 10 + rand() % 90 );
} // end MergeSort constructor

// split vector, sort subvectors and merge subvectors into sorted vector
void MergeSort::sort()
{
    sortSubVector( 0, size - 1 ); // recursively sort entire vector
} // end function sort

// recursive function to sort subvectors
void MergeSort::sortSubVector( int low, int high )
{
    // test base case; size of vector equals 1
    if ( ( high - low ) >= 1 ) // if not base case
    {
        int middle1 = ( low + high ) / 2; // calculate middle of vector
        int middle2 = middle1 + 1; // calculate next element over

        // output split step
        cout << "split:   ";
        displaySubVector( low, high );
        cout << endl << "       ";
        displaySubVector( low, middle1 );
        cout << endl << "       ";
```
```

**Fig. 19.6** | *MergeSort class member-function definition. (Part 1 of 3.)*