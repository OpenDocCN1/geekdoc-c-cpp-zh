
(In the output, the line marked Line 18 contains the output of Lines 18 through 20 of the program.)

The statement in Line 22 creates the vector intList and initializes it using the array declared in Line 21. The statement in Line 25 outputs the values of the elements of intList. The statement in Line 27 uses the function swap_ranges to swap the first four elements of intList with the four elements of intList, starting at the sixth element of intList. The statement in Line 29 outputs the elements of intList. (In the output, the line marked Line 28 contains the output of Lines 28 through 30 of the program.)

The statement in Line 31 swaps the elements of the array list with the elements of the vector intList. The statement in Line 34 outputs the elements of the array list, and the statement in Line 37 outputs intList.

## The Functions `search`, `search_n`, `sort`, and `binary_search`

The functions search, search_n, sort, and binary_search are used to search and sort elements. These functions are defined in the header file algorithm.

![](img/d0be7fc6d804b63484835c6c8bc67a07_1570_0.png)

The prototypes of the function search are:

```cpp
template <class forwardItr1, class forwardItr2>
forwardItr1 search(forwardItr1 first1, forwardItr1 last1,
                   forwardItr2 first2, forwardItr2 last2);
```

```cpp
template <class forwardItr1, class forwardItr2,
          class binaryPredicate>
forwardItr1 search(forwardItr1 first1, forwardItr1 last1,
                  forwardItr2 first2, forwardItr2 last2,
                  binaryPredicate op);
```

Given two ranges of elements, first1...last1−1 and first2...last2−1, the function search searches the first element in the range first1...last1−1 where the range first2...last2−1 occurs as a subrange of first1...last1−1. The first form makes the equality comparison between the elements of the two ranges. For the second form, the comparison op(elemFirstRange, elemSecondRange) must be true. If a match is found, the function returns the position in the range first1...last1−1 where the match occurs; otherwise, the function returns last1.

The prototypes of the function search_n are:

```cpp
template <class forwardItr, class size, class Type>
forwardItr search_n(forwardItr first, forwardItr last,
                     size count, const Type& value);
```

```cpp
using namespace std;

int main()
{
    int intList[15] = {12, 34, 56, 34, 34,
                       78, 38, 43, 12, 25,
                       34, 56, 62, 5, 49};

    vector<int> vecList(intList, intList + 15);
    int list[2] = {34, 56};

    vector<int>::iterator location;

    ostream_iterator<int> screenOut(cout, " ");

    cout << "Line 6: vecList: ";
    copy(vecList.begin(), vecList.end(), screenOut);
    cout << endl;

    cout << "Line 9: list: ";
    copy(list, list + 2, screenOut);
    cout << endl;

    //search
    location = search(vecList.begin(), vecList.end(),
                      list, list + 2);

    if (location != vecList.end())
        cout << "Line 14: list found in vecList. "
             << "The first occurrence of " << endl
             << "the list in vecList is at "
             << "the position "
             << (location - vecList.begin()) << endl;
    else
        cout << "Line 16: list is not in vecList."
             << endl;

    //search_n
    location = search_n(vecList.begin(),
                        vecList.end(), 2, 34);

    if (location != vecList.end())
        cout << "Line 19: two consecutive "
             << "occurrences of 34 found in " << endl
             << "vecList at the position "
             << (location - vecList.begin()) << endl;
    else
        cout << "Line 21: vecList does not contain "
             << "two consecutive occurrences of 34."
             << endl;

    //sort
    sort(vecList.begin(), vecList.end());

    cout << "Line 23: vecList after sorting:"
         << endl << "        ";                  //Line 23
    copy(vecList.begin(), vecList.end(), screenOut); //Line 24
    cout << endl;                                  //Line 25

                 //binary_search
    bool found;                                    //Line 26

    found = binary_search(vecList.begin(),
                          vecList.end(), 78);      //Line 27

    if (found)                                     //Line 28
        cout << "Line 29: 78 found in vecList."
             << endl;                              //Line 29
    else                                           //Line 30
        cout << "Line 31: 78 not in vecList."
             << endl;                              //Line 31

    return 0;
}
```

### Sample Run:

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

The statement in Line 2 creates a vector, vecList, and initializes it using the array intList created in Line 1. The statement in Line 3 creates an array, list, of two components and initializes list. The statement in Line 7 outputs vecList. The statement in Line 12 uses the function search and searches vecList to find the position of the first occurrence in vecList where list occurs as a subsequence. The statements in Lines 13 through 16 output the result of the search; see the line marked Line 14 in the output.

The statement in Line 17 uses the function search_n to find the position in vecList where two consecutive instances of 34 occur. The statements in Lines 18 through 21 output the result of the search.

The statement in Line 22 uses the function sort to sort vecList. The statement in Line 24 outputs vecList. In the output, the line marked Line 23 contains the output of the statements in Lines 23 through 25.

The statement in Line 27 uses the function binary_search to search vecList. The statements in Lines 28 through 31 output the search result.

## The Functions `adjacent_find`, `merge`, and `inplace_merge`

The algorithm `adjacent_find` is used to find the first occurrence of consecutive elements that meet certain criteria. The prototypes of the functions implementing this algorithm are:

```cpp
template <class forwardItr>
forwardItr adjacent_find(forwardItr first, forwardItr last);

template <class forwardItr, class binaryPredicate>
forwardItr adjacent_find(forwardItr first, forwardItr last,
                          binaryPredicate op);
```

The first form of `adjacent_find` uses the equality criteria; that is, it looks for the first consecutive occurrences of the same element. In the second form, the algorithm returns an iterator to the element in the range `first...last−1` for which `op(elem, nextElem)` is true, in which elem is an element in the range `first...last−1` and nextElem is an element in this range next to elem. If no matching elements are found, both algorithms return `last`.

The algorithm `merge` merges the sorted lists. The result is a sorted list. Both lists must be sorted according to the same criteria. For example, both lists should be in either ascending or descending order. The prototypes of the functions to implement the merge algorithms are:

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

Both forms of the algorithm `merge` merge the elements of the sorted ranges `first1...last1−1` and `first2...last2−1`. The destination range, beginning with the iterator `destFirst`, contains the merged elements. The first form uses the less-than operator, <, for ordering the elements. The second form uses the binary predicate op to order the elements; that is, `op(elemRange1, elemRange2)` must be true. Both forms return the position of the last copied element in the destination range. Moreover, the source ranges are not modified, and the destination range should not overlap with the source ranges.

The algorithm `inplace_merge` is used to combine the sorted consecutive sequences. The prototypes of the functions implementing this algorithm are:
