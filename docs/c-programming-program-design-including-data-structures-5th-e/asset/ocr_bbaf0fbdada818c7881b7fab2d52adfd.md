# The Functions includes, set_intersection, set_union, set_difference, and set_symmetric_difference

This section describes the set theory operations includes (subset), set_intersection, set_union, set_difference, and set_symmetric_difference. All of these algorithms assume that the elements within each given range are already sorted.

The algorithm includes determines whether the elements in one range appear in another range. This function has two forms, as shown by the following prototypes:

```
```cpp
template <class inputItr1, class inputItr2>
bool includes(inputItr1 first1, inputItr1 last1,
              inputItr2 first2, inputItr2 last2);

template <class inputItr1, class inputItr2,
          class binaryPredicate>
bool includes(inputItr1 first1, inputItr1 last1,
              inputItr2 first2, inputItr2 last2,
              binaryPredicate op );
```
```

Both forms of the function includes assume that the elements in the ranges first1...last1−1 and first2...last2−1 are sorted according to the same sorting criterion. The function returns true if all of the elements in the range first2...last2−1 are also in first1...last1−1. In other words, the function returns true if first1...last1−1 contains all of the elements in the range first2...last2−1. The first form assumes that the elements in both ranges are in ascending order. The second form uses the operation op to determine the ordering of the elements.

Example 22−26 illustrates how the function includes works.

# EXAMPLE 22-26

```
```cpp
//STL function includes
//This function assumes that the elements in the given ranges
//are ordered according to some sorting criteria

#include <iostream>
#include <algorithm>

using namespace std;

int main()
{
    char setA[5] = {'A', 'B', 'C', 'D', 'E'};       //Line 1
    char setB[10] = {'A', 'B', 'C', 'D', 'E',
                     'F', 'G', 'J', 'K', 'L'};     //Line 2
    char setC[5] = {'A', 'E', 'I', 'O', 'U'};       //Line 3

    ostream_iterator<char> screen(cout, " ");      //Line 4
    cout << "Line 5: setA: ";                     //Line 5
```
```

![](bbox=[0.904, 0.474, 1.0, 0.579])