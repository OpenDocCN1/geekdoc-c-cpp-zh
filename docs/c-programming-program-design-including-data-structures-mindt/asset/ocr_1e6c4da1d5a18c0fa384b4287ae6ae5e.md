# Binary Search Algorithm and the `class orderedArrayListType`

The `class orderedArrayListType`, designed in Chapter 13, does not contain the binary search algorithm. Now that you know how to implement the binary search algorithm, you can learn how to use it in the `class orderedArrayListType`.

To use the binary search algorithm within the `class orderedArrayListType`, we add the function `binSearch` to this class and call the function `binarySearch` with the appropriate parameters.

```
#include "arrayListType.h"
#include "searchSortAlgorithms.h"

template <class elemType>
class orderedArrayListType: public arrayListType<elemType>
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& repItem);
    void seqSearch(const elemType& searchItem) const;
    void insert(const elemType& insertItem);
    void remove(const elemType& removeItem);

    int binSearch(const elemType& removeItem);

    orderedArrayListType(int size = 100);
        //Constructor
};
```

The definition of the member function `binSearch` is as follows:

```
template <class elemType>
int orderedArrayListType<elemType>::
                         binSearch(const elemType& item) const
{
    return binarySearch(list, length, item);
}
```

# Asymptotic Notation: Big-O Notation

Just as a problem is analyzed before writing the algorithm and the computer program, after an algorithm is designed, it should also be analyzed. Usually, there are various ways to design a particular algorithm. Certain algorithms take very little computer time to execute, while others take a considerable amount of time. Consider the following examples.