
```cpp
    cout << "Line 23: vecList after sorting:"
         << endl << "          ";
    copy(vecList.begin(), vecList.end(), screenOut); //Line 24
    cout << endl; //Line 25

      //binary_search
    bool found; //Line 26

    found = binary_search(vecList.begin(),
                          vecList.end(), 78); //Line 27

    if (found)
        cout << "Line 29: 78 found in vecList."
             << endl; //Line 29
    else
        cout << "Line 31: 78 not in vecList."
             << endl; //Line 31

    return 0;
}
```

### Sample Run

```text
Line 6: vecList: 12 34 56 34 34 78 38 43 12 25 34 56 62 5 49
Line 9: list: 34 56
Line 14: list found in vecList. The first occurrence of
         list in vecList is at the position 1
Line 19: two consecutive occurrences of 34 found in
         vecList at the position 3
Line 23: vecList after sorting:
         5 12 12 25 34 34 34 34 38 43 49 56 56 62 78
Line 29: 78 found in vecList.
```

The statement in Line 2 creates a vector, vecList, and initializes it using the array intList created in Line 1. The statement in Line 3 creates an array, list, of two components and initializes list. The statement in Line 7 outputs vecList. The statement in Line 12 uses the function search and searches vecList to find the position (of the first occurrence) in vecList where list occurs as a subsequence. The statements in Lines 13 through 16 output the result of the search; see the line marked Line 14 in the output.

The statement in Line 17 uses the function search_n to find the position in vecList where two consecutive instances of 34 occur. The statements in Lines 18 through 21 output the result of the search.

The statement in Line 22 uses the function sort to sort vecList. The statement in Line 24 outputs vecList. In the output, the line marked Line 23 contains the output of the statements in Lines 23 through 25.

The statement in Line 27 uses the function binary_search to search vecList. The statements in Lines 28 through 31 output the search result.

## The Functions `adjacent_find`, `merge`, and `inplace_merge`

The algorithm adjacent_find is used to find the first occurrence of consecutive elements that meet certain criteria. The prototypes of the functions implementing this algorithm are:

```cpp
template <class forwardItr>
forwardItr adjacent_find(forwardItr first, forwardItr last);
```

```cpp
template <class forwardItr, class binaryPredicate>
forwardItr adjacent_find(forwardItr first, forwardItr last,
                          binaryPredicate op);
```

The first form of adjacent_find uses the equality criteria; that is, it looks for the first consecutive occurrences of the same element. In the second form, the algorithm returns an iterator to the element in the range first...last−1 for which op(elem, nextElem) is true, in which elem is an element in the range first...last−1 and nextElem is an element in this range next to elem. If no matching elements are found, both algorithms return last.

The algorithm merge merges the sorted lists. The result is a sorted list. Both lists must be sorted according to the same criteria. For example, both lists should be in either ascending or descending order. The prototypes of the functions to implement the merge algorithms are:

```cpp
template <class inputItr1, class inputItr2, class outputItr>
outputItr merge(inputItr1 first1, inputItr1 last1,
               inputItr2 first2, inputItr2 last2,
               outputItr destFirst);
```

```cpp
template <class inputItr1, class inputItr2,
          class outputItr, class binaryPredicate>
outputItr merge(inputItr1 first1, inputItr1 last1,
               inputItr2 first2, inputItr2 last2,
               outputItr destFirst, binaryPredicate op);
```

Both forms of the algorithm merge merge the elements of the sorted ranges first1...last1−1 and first2...last2−1. The destination range, beginning with the iterator destFirst, contains the merged elements. The first form uses the less-than operator, <, for ordering the elements. The second form uses the binary predicate op to order the elements; that is, op(elemRange1, elemRange2) must be true. Both forms return the position after the last copied element in the destination range. Moreover, the source ranges are not modified, and the destination range should not overlap with the source ranges.

The algorithm inplace_merge is used to combine the sorted consecutive sequences. The prototypes of the functions implementing this algorithm are:

```cpp
template <class biDirectionalItr>
void inplace_merge(biDirectionalItr first,
                   biDirectionalItr middle,
                   biDirectionalItr last);

template <class biDirectionalItr, class binaryPredicate>
void inplace_merge(biDirectionalItr first,
                   biDirectionalItr middle,
                   biDirectionalItr last,
                   binaryPredicate op);
```

Both forms merge the sorted consecutive sequences first...middle−1 and middle...last−1. The merged elements overwrite the two ranges beginning at first. The first form uses the less-than criterion to merge the two consecutive sequences. The second form uses the binary predicate op to merge the sequences; that is, for the elements of the two sequences, op(elemSeq1, elemSeq2) must be true. For example, suppose that:

```cpp
vecList = {1, 3, 5, 7, 9, 2, 4, 6, 8}
```

in which vecList is a vector container. Further suppose that vecItr is a vector iterator pointing to element 2. Then, after the execution of the statement:

```cpp
inplace_merge(vecList.begin(), vecItr, vecList.end());
```

the elements in vecList are in the following order:

```cpp
vecList = {1, 2, 3, 4, 5, 6, 7, 8, 9}
```

The program in Example 22–22 illustrates how these algorithms work.

### EXAMPLE 22-22

```cpp
//STL Functions adjacent_find, merge, and inplace_merge

#include <iostream>
#include <functional>
#include <algorithm>
#include <iterator>
#include <vector>
#include <list>

using namespace std;

int main()
{
    int list1[10] = {1, 3, 5, 7, 9, 0, 2, 4, 6, 8};   //Line 1
    int list2[10] = {0, 1, 1, 2, 3, 4, 4, 5, 6, 6};   //Line 2

    int list3[5] = {0, 2, 4, 6, 8};                    //Line 3
    int list4[5] = {1, 3, 5, 7, 9};                    //Line 4

    list<int> intList(list2, list2 + 10);                      //Line 5
    list<int>::iterator listItr;                               //Line 6

    vector<int> vecList(list1, list1 + 10);                    //Line 7
    vector<int>::iterator     intItr;                          //Line 8

    ostream_iterator<int> screen(cout, " ");                   //Line 9

    cout << "Line 10: intList : ";                             //Line 10
    copy(intList.begin(), intList.end(), screen);              //Line 11
    cout << endl;                                              //Line 12

        //adjacent_find
    listItr = adjacent_find(intList.begin(),
                            intList.end());                    //Line 13

    if (listItr != intList.end())                              //Line 14
        cout << "Line 15: Adjacent equal "
             << "elements are found " << endl
             << "            The first set of "
             << "adjacent equal elements: "
             << *listItr << endl;                              //Line 15
    else                                                       //Line 16
        cout << "Line 17: No adjacent equal "
             << "element found" << endl;                       //Line 17

    intList.clear();                                           //Line 18

        //merge
    merge(list3, list3 + 5, list4, list4 + 5,
          back_inserter(intList));                             //Line 19

    cout << "Line 20: intList after merging list3 "
         << "and " << "list4:\n"
         << "          ";                                      //Line 20
    copy(intList.begin(), intList.end(), screen);              //Line 21
    cout << endl;                                              //Line 22

        //adjacent_find: second form
    intItr = adjacent_find(vecList.begin(),
                           vecList.end(),
                           greater<int>());                    //Line 23

    cout << "Line 24: Last element of first "
         << "sorted sublist: " << *intItr << endl;             //Line 24
    intItr++;                                                  //Line 25
    cout << "Line 26: First element of second "
         << "sorted sublist: " << *intItr << endl;             //Line 26

    cout << "Line 27: vecList before "
         << "inplace merge: ";                                 //Line 27
    copy(vecList.begin(), vecList.end(), screen);              //Line 28
    cout << endl;                                              //Line 29
```
