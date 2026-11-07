is the current value of the accumulation. The second argument is the value of the current element in the sequence being accumulated.

# **for_each Algorithm**

Line 59 uses the **for_each** algorithm to apply a general function to every element in the range from a1.cbegin() up to, but *not* including, a1.cend(). The general function takes the current element as an argument and may modify that element (if it’s received by reference and is not const). Algorithm for_each requires its two iterator arguments to be at least *input iterators*.

# **transform Algorithm**

Line 63 uses the **transform** algorithm to apply a general function to *every* element in the range from a1.cbegin() up to, but *not* including, a1.cend(). The general function (the fourth argument) should take the current element as an argument, must *not* modify the element and should return the transformed value. Algorithm transform requires its first two iterator arguments to be at least *input iterators* and its third argument to be at least an *output iterator*. The third argument specifies where the transformed values should be placed. Note that the third argument can equal the first. Another version of transform accepts five arguments—the first two arguments are *input iterators* that specify a range of elements from one source container, the third argument is an *input iterator* that specifies the first element in another source container, the fourth argument is an *output iterator* that specifies where the transformed values should be placed and the last argument is a general function that takes two arguments. This version of transform takes one element from each of the two input sources and applies the general function to that pair of elements, then places the transformed value at the location specified by the fourth argument.

# 16.3.6 Basic Searching and Sorting Algorithms

Figure 16.6 demonstrates some basic searching and sorting Standard Library algorithms, including find, find_if, sort, binary_search, all_of, any_of, none_of and find_if_not.

```
```cpp
// Fig. 16.6: fig16_06.cpp
// Standard Library search and sort algorithms.
#include <iostream>
#include <algorithm> // algorithm definitions
#include <array> // array class-template definition
#include <iterator>
using namespace std;

bool greater10( int value ); // predicate function prototype

int main()
{
   const size_t SIZE = 10;
   array< int, SIZE > a = { 10, 2, 17, 5, 16, 8, 13, 11, 20, 7 };
   ostream_iterator< int > output( cout, " " );
```
```

**Fig. 16.6** | Standard Library search and sort algorithms. (Part 1 of 3.)