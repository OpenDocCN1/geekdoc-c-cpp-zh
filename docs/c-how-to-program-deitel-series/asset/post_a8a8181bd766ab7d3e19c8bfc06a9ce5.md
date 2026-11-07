
comes inconsequential. Big O is designed to highlight these dominant terms and ignore terms that become unimportant as *n* grows. For this reason, an algorithm that requires a total of *n* − 1 comparisons (such as the one we described in this paragraph) is said to be **O(n)** and is referred to as having a *linear runtime*. **O(n)** is often pronounced “on the order of *n*” or more simply “order *n*.”

## *Big O: Quadratic Runtime*

Now suppose you have an algorithm that tests whether *any* element of an array is duplicated elsewhere in the array. The first element must be compared with *all the other elements*. The second element must be compared with all the other elements except the first (it was already compared to the first). The third element then must be compared with all the other elements except the first two. In the end, this algorithm will end up making (*n* − 1) + (*n* − 2) + … + 2 + 1 or *n*²/2 − *n*/2 comparisons. As *n* increases, the *n*² term dominates and the *n* term becomes inconsequential. Again, Big O notation highlights the *n*² term, leaving *n*²/2. As we’ll soon see, even constant factors, such as the 1/2 here, are omitted in Big O notation.

Big O is concerned with how an algorithm’s runtime grows in relation to the *number of items processed*. Suppose an algorithm requires *n*² comparisons. With four elements, the algorithm will require 16 comparisons; with eight elements, 64 comparisons. With this algorithm, *doubling* the number of elements *quadruples* the number of comparisons. Consider a similar algorithm requiring *n*²/2 comparisons. With four elements, the algorithm will require eight comparisons; with eight elements, 32 comparisons. Again, doubling the number of elements quadruples the number of comparisons. Both of these algorithms grow as the square of *n*, so Big O ignores the constant, and both algorithms are considered to be **O(n²)**, which is referred to as *quadratic runtime* and pronounced “on the order of *n*-squared” or more simply “order *n*-squared.”

## *O(n²) Performance*

When *n* is small, **O(n²)** algorithms (running on today’s billions-of-operations-per-second personal computers) will not noticeably affect performance. But as *n* grows, you’ll start to notice the performance degradation. An **O(n²)** algorithm running on a million-element array would require a trillion “operations” (where each could actually require several machine instructions to execute). This could require hours to execute. A billion-element array would require a quintillion operations, a number so large that the algorithm could take decades! Unfortunately, **O(n²)** algorithms tend to be easy to write. In this chapter, you’ll see algorithms with more favorable Big O measures. Such efficient algorithms often take a bit more cleverness and effort to create, but their superior performance can be worth the extra effort, especially as *n* gets large.

## *Linear Search's Runtime*

The *linear search* algorithm runs in **O(n)** time. The worst case in this algorithm is that *every* element must be checked to determine whether the search key is in the array. If the array’s size *doubles*, the number of comparisons that the algorithm must perform also *doubles*. Linear search can provide outstanding performance if the element matching the search key happens to be at or near the front of the array. But we seek algorithms that perform well, on average, across *all* searches, including those where the element matching the search key is near the end of the array. If a program needs to perform many searches

```cpp
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

   return location; // return location of key
} // end function binarySearch

int main()
{
   // use the default random-number generation engine to produce
   // uniformly distributed pseudorandom int values from 10 to 99
   default_random_engine engine;
   static_cast<unsigned int>( time( nullptr ) );
   uniform_int_distribution<unsigned int> randomInt( 10, 99 );

   const size_t arraySize = 15; // size of array
   array< int, arraySize > arrayToSearch; // create array

   // fill arrayToSearch with random values
   for ( int &item: arrayToSearch )
      item = randomInt( engine );

   sort( arrayToSearch.begin(), arrayToSearch.end() ); // sort the array

   // display arrayToSearch's values
   displayElements( arrayToSearch, 0, arrayToSearch.size() - 1 );

   // get input from user
   cout << "\nPlease enter an integer value (-1 to quit): ";
   int searchKey; // value to locate
   cin >> searchKey; // read an int from user
   cout << endl;

   // repeatedly input an integer; -1 terminates the program
   while ( searchKey != -1 )
   {
      // use binary search to try to find integer
      int position = binarySearch( arrayToSearch, searchKey );

      // return value of -1 indicates integer was not found
      if ( position == -1 )
         cout << "The integer " << searchKey << " was not found.\n";
      else
         cout << "The integer " << searchKey
              << " was found in position " << position << ".\n";

      // get input from user
      cout << "\n\nPlease enter an integer value (-1 to quit): ";
      cin >> searchKey; // read an int from user
      cout << endl;
   } // end while
} // end main
```

**Fig. 20.3** | Binary search of an array. (Part 1 of 3.)

**Fig. 20.3** | Binary search of an array. (Part 2 of 3.)

```text
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97

Please enter an integer value (-1 to quit): 48
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                  *
10 23 27 48 52 55 58
         *
The integer 48 was found in position 3.

Please enter an integer value (-1 to quit): 92
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                                      *
                        62 63 68 72 75 92 97
                                             *
                                    75 92 97
                                           *
The integer 92 was found in position 13.

Please enter an integer value (-1 to quit): 22
10 23 27 48 52 55 58 60 62 63 68 72 75 92 97
                  *
10 23 27 48 52 55 58
         *
10 23 27
   *
10
 *
The integer 22 was not found.

Please enter an integer value (-1 to quit): -1
```

**Fig. 20.3** | Binary search of an array. (Part 3 of 3.)

### *Function Template* **binarySearch**

Lines 25–56 define function template binarySearch, which has two parameters—a reference to the array to search and a reference to the search key. Lines 28–30 calculate the low end index, high end index and middle index of the portion of the array that the algorithm is currently searching. When binarySearch is first called, low is 0, high is the array’s size minus 1 and middle is the average of these two values. Line 31 initializes location to −1—the value that binarySearch returns if the search key is not found. Lines 33–53 loop until low is greater than high (indicating that the element was not found) or location does not equal −1 (indicating that the search key was found). Line 45 tests whether the value in the middle element is equal to key. If so, line 46 assigns the middle index to location. Then the loop terminates and location is returned to the caller. Each iteration of the loop that does not find the search key tests a single value (line 45) and eliminates half of the remaining values in the array (line 48 or 50).
