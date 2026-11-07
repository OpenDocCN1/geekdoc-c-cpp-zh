The algorithm `rotate_copy` is a combination of `rotate` and `copy`. That is, the elements of the source are copied at the destination in a rotated order. The source is not modified. The prototype of the function implementing this algorithm is:

```
```cpp
template <class forwardItr, class outputItr>
outputItr rotate_copy(forwardItr first, forwardItr middle,
                      forwardItr last,
                      outputItr destFirst);
```
```

The elements in the range `first...last-1` are copied into the destination range beginning with `destFirst` in the rotated order, so that the element specified by `middle` in the range `first...last-1` becomes the first element of the destination. The function also returns the position one past the last element copied at the destination.

The algorithms `reverse`, `reverse_copy`, `rotate`, and `rotate_copy` are contained in the header file `<algorithm>`. The program in Example 21–24 illustrates how to use these algorithms.

# EXAMPLE 21-24

```
```cpp
//STL Functions: reverse, reverse_copy, rotate, and rotate_copy

#include <iostream>
#include <algorithm>
#include <iterator>
#include <list>

using namespace std;

int main()
{
    int temp[10] = {1, 3, 5, 7, 9, 0, 2, 4, 6, 8};      //line 1

    list<int> intList(temp, temp + 10);                  //line 2
    list<int> resultList;                                //line 3
    list<int>::iterator listItr;                         //line 4

    ostream_iterator<int> screen(cout, " ");             //line 5

    cout << "Line 6: intList: ";                         //line 6
    copy(intList.begin(), intList.end(), screen);        //line 7
    cout << endl;                                         //line 8

                    //reverse
    reverse(intList.begin(), intList.end());             //line 9

    cout << "Line 10: intList after reversal: ";        //line 10
    copy(intList.begin(), intList.end(), screen);        //line 11
    cout << endl;                                         //line 12
```
```