```
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
```

Both forms merge the sorted consecutive sequences first...middle-1 and middle...last-1. The merged elements overwrite the two ranges beginning at first. The first form uses the less-than criterion to merge the two consecutive sequences. The second form uses the binary predicate op to merge the sequences; that is, for the elements of the two sequences, op(elemSeq1, elemSeq2) must be true. For example, suppose that:

`vecList = {1, 3, 5, 7, 9, 2, 4, 6, 8}`

in which vecList is a vector container. Further suppose that vecItr is a vector iterator pointing to element 2. Then, after the execution of the statement:

```
```cpp
inplace_merge(vecList.begin(), vecItr, vecList.end());
```
```

the elements in vecList are in the following order:

`vecList = {1, 2, 3, 4, 5, 6, 7, 8, 9}`

The program in Example 21-22 illustrates how these algorithms work.

# EXAMPLE 21-22

```
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
    int list1[10] = {1, 3, 5, 7, 9, 0, 2, 4, 6, 8};    //Line 1
    int list2[10] = {0, 1, 1, 2, 3, 4, 4, 5, 6, 6};    //Line 2

    int list3[5] = {0, 2, 4, 6, 8};                     //Line 3
    int list4[5] = {1, 3, 5, 7, 9};                     //Line 4
```
```