
$$(n-1)+(n-2)+\cdots+2+1=\frac{n(n-1)}{2}=\frac{1}{2}n^2-\frac{1}{2}n=O(n^2).$$

In the worst case, the body of the `if` statement always executes. So in the worst case, the number of assignments is

$$\frac{3n(n-1)}{2}=\frac{3}{2}n^2-\frac{3}{2}n=O(n^2).$$

If the list is already sorted, which is the best case, the number of assignments is 0.

It can be shown that, on average, bubble sort makes about $\frac{n(n-1)}{4}$ item assignments. However, the number of comparisons for the bubble sort, as given in this chapter, is always $\frac{n(n-1)}{2}$.

Therefore, to sort a list of size 1000, bubble sort makes about 500,000 key comparisons and about 250,000 item assignments. The next section presents the selection sort algorithm that reduces the number of item assignments.

> **NOTE** Exercise 9 at the end of this chapter gives a version of the bubble sort algorithm in which the number of comparisons in the best case is $O(n)$.

## Bubble Sort Algorithm and the class `unorderedArrayListType`

The class `unorderedArrayListType`, designed in Chapter 13, does not contain any sorting algorithm. Now that you know how to implement the bubble sort algorithm, you can learn how to use it in the class `unorderedArrayListType`.

To use the binary search algorithm within the `class unorderedArrayListType`, we add the function `sort` to this class and call the function `bubbleSort` with the appropriate parameters. (Note that we have also added the function to use the binary search algorithm.)

```cpp
template <class elemType>
class unorderedArrayListType: public arrayListType<elemType>
{
public:
    void insertAt(int location, const elemType& insertItem);
    void insertEnd(const elemType& insertItem);
    void replaceAt(int location, const elemType& replaceItem);
    int seqSearch(const elemType& searchItem) const;
    void remove(const elemType& removeItem);
    void sort();
    int binSearch(const elemType& item) const;

    unorderedArrayListType(int size = 100);
        //Constructor
};
```

The definitions of the member functions `binSearch` and `sort` are as follows:

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

We leave it as an exercise for you to write a program to test the member functions `sort` and `binSearch`.

## Selection Sort: Array-Based Lists

Chapter 8 described the selection sort algorithm for array-based lists. However, the selection sort algorithm given in Chapter 8 works only for arrays of type `int`. In this section, using templates we give a generic selection sort algorithm. Note that the algorithm given here is slightly different than the one given in Chapter 8.

Suppose that `list` is the array to be sorted and `length` denotes the length, that is, the number of elements in `list`. As described in Chapter 8, a selection sort involves the following steps:

- a. Find the location of the smallest element.
- b. Move the smallest element to the beginning of the unsorted list.

Given the starting index, `first`, and the ending index, `last`, of the list, the following C++ function returns the index of the smallest element in `list[first]...list[last]`.

```cpp
template <class elemType>
int minLocation(elemType list[], int first, int last)
{
    int minIndex;

    minIndex = first;

    for (int loc = first + 1; loc <= last; loc++)
        if (list[loc] < list[minIndex])
            minIndex = loc;

    return minIndex;
}  //end minLocation
```

Given the locations in the list of the elements to be swapped, the following C++ function, **swap**, swaps those elements:

```cpp
template <class elemType>
void swap(elemType list[], int first, int second)
{
    elemType temp;

    temp = list[first];
    list[first] = list[second];
    list[second] = temp;
}  //end swap
```

We can now complete the definition of the function **selectionSort**:

```cpp
template <class elemType>
void selectionSort(elemType list[], int length)
{
    int minIndex;

    for (int loc = 0; loc < length; loc++)
    {
        minIndex = minLocation(list, loc, length - 1);
        swap(list, loc, minIndex);
    }
}  //end selectionSort
```

We leave it as an exercise for you to write a program to test the selection sort algorithm. (See Programming Exercise 6 at the end of this chapter.)

> **NOTE**
>
> - 1. A selection sort can also be implemented by selecting the largest element in the unsorted portion of the list and moving it to the bottom of the list. You can easily implement this form of selection sort by altering the `if` statement in the function `minLocation` and passing the appropriate parameters to both the corresponding function and the function `swap` (when these functions are called in the function `selectionSort`).
> - 2. A selection sort can also be applied to linked lists. The general algorithm is the same, and the details are left as an exercise for you. See Programming Exercise 7 at the end of this chapter.

![](img/b217c421655b51e7494cf3b89bb5432d_1355_0.png)

FIGURE 18-11  list

The length of the list is 8. In this list, the elements list[0], list[1], list[2], and list[3] are in order. That is, list[0]...list[3] is sorted (see Figure 18-12).

![](img/b217c421655b51e7494cf3b89bb5432d_1355_1.png)

FIGURE 18-12  Sorted and unsorted portion of list

Next, we consider the element list[4], the first element of the unsorted list. Because list[4] < list[3], we need to move the element list[4] to its proper location. It thus follows that element list[4] should be moved to list[2] (see Figure 18-13).

![](img/b217c421655b51e7494cf3b89bb5432d_1355_2.png)

FIGURE 18-13  Move list[4] into list[2]

To move list[4] into list[2], first we copy list[4] into temp, a temporary memory space (see Figure 18-14).

![](img/b217c421655b51e7494cf3b89bb5432d_1355_3.png)

FIGURE 18-14  Copy list[4] into temp

Next, we copy `list[3]` into `list[4]` and then `list[2]` into `list[3]` (see Figure 18-15).

![](img/b217c421655b51e7494cf3b89bb5432d_1356_0.png)

FIGURE 18-15  List before copying `list[3]` into `list[4]` and then `list[2]` into `list[3]`

After copying `list[3]` into `list[4]` and `list[2]` into `list[3]`, the list is as shown in Figure 18-16.

![](img/b217c421655b51e7494cf3b89bb5432d_1356_1.png)

FIGURE 18-16  List after copying `list[3]` into `list[4]` and then `list[2]` into `list[3]`

We now copy `temp` into `list[2]`. Figure 18-17 shows the resulting list.

![](img/b217c421655b51e7494cf3b89bb5432d_1356_2.png)

FIGURE 18-17  List after copying `temp` into `list[2]`

Now `list[0]...list[4]` is sorted, and `list[5]...list[7]` is unsorted. We repeat this process on the resulting list by moving the first element of the unsorted list into the sorted list in the proper place.

We leave it as an exercise for you to write a program to test the insertion sort algorithm. (See Programming Exercise 8 at the end of this chapter.)

> **NOTE**
>
> An insertion sort can also be applied to linked lists. The general algorithm is the same, and the details are left as an exercise for you. See Programming Exercise 9 at the end of this chapter.

## Analysis: Insertion Sort

Let $L$ be a list of length $n$. Suppose $L$ is to be sorted using insertion sort. The `for` loop executes $n - 1$ times. In the best case, when the list is already sorted, for each iteration of the `for` loop, the `if` statement evaluates to `false`, so there are $n - 1$ key comparisons. Thus, in the best case, the number of key comparisons is $n - 1 = O(n)$. Let us consider the worst case. In this case, for each iteration of the `for` loop, the `if` statement evaluates to `true`. Moreover, for each iteration of the `for` loop, the `do...while` loop executes `firstOutOfOrder - 1` times. It follows that in the worst case, the number of key comparisons is

$1 + 2 + \cdots + (n - 1) = n(n - 1) / 2 = O(n^2)$.

It can be shown that the average number of key comparisons and the average number of item assignments in an insertion sort algorithm are

$\frac{1}{4}n^2 + O(n) = O(n^2)$

Table 18-9 summarizes the behavior of the bubble sort, selection sort, and insertion sort algorithms.

**TABLE 18-9. Average Case Behavior of the Bubble Sort, Selection Sort, and Insertion Sort Algorithms for a List of Length $n$**

| Algorithm | Number of comparisons | Number of swaps |
|---|---|---|
| Bubble sort | $\frac{n(n-1)}{2} = O(n^2)$ | $\frac{n(n-1)}{4} = O(n^2)$ |
| Selection sort | $\frac{n(n-1)}{2} = O(n^2)$ | $3(n-1) = O(n)$ |
| Insertion sort | $\frac{1}{4}n^2 + O(n) = O(n^2)$ | $\frac{1}{4}n^2 + O(n) = O(n^2)$ |
