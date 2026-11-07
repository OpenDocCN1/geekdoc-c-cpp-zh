```
// Fig 20.3: BinarySearch.cpp
// Binary search of an array
#include <algorithm>
#include <array>
#include <ctime>
#include <iostream>
#include <random>
using namespace std;

// display array elements from index low through index high
template <typename T, size_t size >
void displayElements( const array<T, size > &items,
   size_t low, size_t high )
{
   for ( size_t i = 0; i < items.size() && i < low; ++i )
      cout << " "; // display spaces for alignment

   for ( size_t i = low; i < items.size() && i <= high; ++i )
      cout << items[ i ] << " "; // display element

   cout << endl;
} // end function displayElements

// perform a binary search on the data
template <typename T, size_t size >
int binarySearch( const array<T, size > &items, const T &key)
{
   int low = 0; // low index of elements to search
   int high = items.size() - 1; // high index of elements to search
   int middle = ( low + high + 1 ) / 2; // middle element
   int location = -1; // key's index; -1 if not found

   do // loop to search for element
   {
      // display remaining elements of array to be searched
      displayElements( items, low, high );

      // output spaces for alignment
      for ( int i = 0; i < middle; ++i )
         cout << " ";

      cout << " " << endl; // indicate current middle

      // if the element is found at the middle
      if ( key == items[ middle ] )
         location = middle; // location is the current middle
      else if ( key < items[ middle ] ) // middle is too high
         high = middle - 1; // eliminate the higher half
      else // middle element is too low
         low = middle + 1; // eliminate the lower half

      middle = ( low + high + 1 ) / 2; // recalculate the middle
   } while ( ( low <= high ) && ( location == -1 ) );
```

Fig. 20.3 | Binary search of an array. (Part 1 of 3.)