the insert can occur. A second version of upper_bound takes as a fourth argument a binary
predicate function indicating the order in which the elements were originally sorted.

```
```cpp
// Fig. 22.36: Fig22_36.cpp
// Standard Library functions lower_bound, upper_bound and
// equal_range for a sorted sequence of values.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <vector> // vector class-template definition
#include <iterator> // ostream_iterator
using namespace std;

int main()
{
   const int SIZE = 10;
   int a[ SIZE ] = { 2, 2, 4, 4, 4, 6, 6, 6, 6, 8 };
   vector< int > v( a, a + SIZE ); // copy of a
   ostream_iterator< int > output( cout, " " );

   cout << "The vector contains:\n";
   copy( v.begin(), v.end(), output );

   // determine lower-bound insertion point for 6 in v
   vector< int >::iterator lower;
   lower = lower_bound( v.begin(), v.end(), 6 );
   cout << "\nLower bound of 6 is element "
      << ( lower - v.begin() ) << " of vector v";

   // determine upper-bound insertion point for 6 in v
   vector< int >::iterator upper;
   upper = upper_bound( v.begin(), v.end(), 6 );
   cout << "\nUpper bound of 6 is element "
      << ( upper - v.begin() ) << " of vector v";

   // use equal_range to determine both the lower- and
   // upper-bound insertion points for 6
   pair< vector< int >::iterator, vector< int >::iterator > eq;
   eq = equal_range( v.begin(), v.end(), 6 );
   cout << "\nUsing equal_range:\n Lower bound of 6 is element "
      << ( eq.first - v.begin() ) << " of vector v";
   cout << "\n Upper bound of 6 is element "
      << ( eq.second - v.begin() ) << " of vector v";
   cout << "\nThe upper bound points to the first point\n"
      << "at which 5 can be inserted in order";

   // determine lower-bound insertion point for 5 in v
   lower = lower_bound( v.begin(), v.end(), 5 );
   cout << "\nLower bound of 5 is element "
      << ( lower - v.begin() ) << " of vector v";
   cout << "\nUse upper_bound to locate the last point\n"
      << "at which 7 can be inserted in order";
```

```

**Fig. 22.36** | Algorithms lower_bound, upper_bound and equal_range. (Part 1 of 2.)