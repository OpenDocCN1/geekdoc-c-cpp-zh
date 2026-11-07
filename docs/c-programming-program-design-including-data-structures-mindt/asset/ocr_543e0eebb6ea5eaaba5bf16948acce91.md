```
```cpp
void sort();
int binSearch(const elemType& item) const;

unorderedArrayListType(int size = 100);
    //Constructor
};
```
```

The definitions of the member functions `binSearch` and `sort` are as follows:

```
```cpp
template <class elemType>
int unorderedArrayListType<elemType>::
        binSearch(const elemType& item) const
{
    return binarySearch(list, length, item);
}

template <class elemType>
void unorderedArrayListType<elemType>::sort()
{
    bubbleSort(list, length);
}
```
```

We leave it as an exercise for you to write a program to test the member functions `sort` and `binSearch`.

# # Selection Sort: Array-Based Lists

Chapter 8 described the selection sort algorithm for array-based lists. However, the selection sort algorithm given in Chapter 8 works only for arrays of type `int`. In this section, using templates we give a generic selection sort algorithm. Note that the algorithm given here is slightly different than the one given in Chapter 8.

Suppose that `list` is the array to be sorted and `length` denotes the length, that is, the number of elements in `list`. As described in Chapter 8, a selection sort involves the following steps:

+   a. Find the location of the smallest element.
+   b. Move the smallest element to the beginning of the unsorted list.

Given the starting index, `first`, and the ending index, `last`, of the list, the following C++ function returns the index of the smallest element in `list[first]...list[last]`.

```
```cpp
template <class elemType>
int minLocation(elemType list[], int first, int last)
{
    int minIndex;

    minIndex = first;
```
```