In general, suppose that $L$ is a sorted list of size $n$. Moreover, suppose that $n$ is a power of 2, that is, $n = 2^m$ for some nonnegative integer $m$. After each iteration of the while loop, about half of the elements are left to search, that is, the search sublist for the next iteration is half the size of the current sublist. For example, after the first iteration, the search sublist size is about $n/2 = 2^{m-1}$. It is easy to see that the maximum number of the iteration of the while loop is about $m + 1$. Also, $m = \log_2 n$. Each iteration makes two key comparisons. Thus, the maximum number of comparisons to determine whether an element $x$ is in $L$ is $2(m + 1) = 2(\log_2 n + 1) = 2\log_2 n + 2$.

In the case of a successful search, it can be shown that for a list of length $n$, on average, a binary search makes $2\log_2 n - 3$ key comparisons. In the case of an unsuccessful search, it can be shown that for a list of length $n$, a binary search makes approximately $2\log_2 n$ key comparisons.

# Binary Search Algorithm and the class

```
`orderedArrayListType`
```

The class orderedArrayListType, designed in Chapter 13, does not contain the binary search algorithm. Now that you know how to implement the binary search algorithm, you can learn how to use it in the class orderedArrayListType.

To use the binary search algorithm within the class orderedArrayListType, we add the function binSearch to this class and call the functions binarySearch with the appropriate parameters.

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
    int seqSearch(const elemType& searchItem) const;
    void insert(const elemType& insertItem);
    void remove(const elemType& removeItem);

    int binSearch(const elemType& removeItem);

    orderedArrayListType(int size = 100);
        //Constructor
};
```

The definition of the member function binSearch is:

```
template <class elemType>
int orderedArrayListType<elemType>::
                         binSearch(const elemType& item) const
```