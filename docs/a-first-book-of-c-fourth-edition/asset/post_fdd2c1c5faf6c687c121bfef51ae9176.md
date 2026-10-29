
## 7.6 Chapter Summary

1. A one-dimensional array is a data structure that can be used to store a list of values of the same data type. These arrays must be declared by giving the data type of values stored in the array and the array size. For example, the declaration

```cpp
int num[100];
```

creates an array of 100 integers. A preferable approach is first using a symbolic constant to set the array size, and then using this constant in the array definition, as shown in these examples:

```cpp
const int MAXSIZE = 100;
```

and

```cpp
int num[MAXSIZE];
```

2. Array elements are stored in contiguous locations in memory and referenced by using the array name and a subscript (or index), such as `num[22]`. Any non-negative integer value expression can be used as a subscript, and the subscript 0 always refers to the first element in an array.

3. A two-dimensional array is declared by listing a row and a column size with the data type and array name. For example, the following declarations create a two-dimensional array consisting of five rows and seven columns of integer values:

```cpp
const int ROWS = 5;
const int COLS = 7;
int mat[ROWS][COLS];
```

4. Arrays can be initialized when they’re declared. For two-dimensional arrays, you can list the initial values, row by row, inside braces and separate them with commas. For example, the declaration

```cpp
int vals[3][2] = { {1, 2},
                   {3, 4},
                   {5, 6} };
```

produces the following three-row-by-two-column array:

```text
1  2
3  4
5  6
```

As C++ uses the convention that initialization proceeds in row order, the inner braces can be omitted. Therefore, the following statement is an equivalent initialization:

```cpp
int vals[3][2] = {1, 2, 3, 4, 5, 6};
```

5. Arrays are passed to a function by passing the array name as an argument. The value actually passed is the address of the first array storage location. Therefore, the called function
receives direct access to the original array, not a copy of the array elements. A parameter must be declared in the called function to receive the passed array name. The declaration of the parameter can omit the array's row size for both one- and two-dimensional arrays.

## 7.7 Chapter Supplement: Searching and Sorting Methods

Most programmers encounter the need to both sort and search a list of data items at some time in their programming careers. For example, you might have to arrange experiment results in increasing (ascending) or decreasing (descending) order for statistical analysis or sort a list of names in alphabetical order and search this list to find a particular name. Similarly, you might have to arrange a list of dates in ascending or descending order and search this list to locate a certain date. This section introduces the fundamentals of sorting and searching lists. Note that sorting a list before searching it isn't necessary, although much faster searches are possible if the list is in sorted order, as you'll see.

### Search Algorithms

A common requirement of many programs is searching a list for a given element. For example, in a list of names and phone numbers, you might search for a specific name so that the corresponding phone number can be printed, or you might need to search the list simply to determine whether a name is there. The two most common methods of performing these searches are the linear and binary search algorithms.

### Linear Search

In a linear search, also known as a sequential search, each item in the list is examined in the order in which it occurs until the desired item is found or the end of the list is reached. This search method is analogous to looking at every name in the phone directory, beginning with Aardvark, Aaron, until you find the one you want or until you reach Zzxgy, Zora. Obviously, it's not the most efficient way to search a long alphabetized list. However, a linear search has these advantages:

- The algorithm is simple.
- The list need not be in any particular order.

In a linear search, the search begins at the first item in the list and continues sequentially, item by item, through the list. The pseudocode for a function performing a linear search is as follows:

```
For all items in the list
  Compare the item with the desired item
  If the item is found
    Return the index value of the current item
  EndIf
EndFor
Return -1 if the item is not found
```

Notice that the function's return value indicates whether the item was found. If the return value is -1, the item isn't in the list; otherwise, the return value in the for loop provides the index of where the item is located in the list. The linearSearch() function illustrates this procedure as a C++ function:

```
// this function returns the location of key in the list
// a -1 is returned if the value is not found
int linearSearch(int list[], int size, int key)
{
    int i;

    for (i = 0; i < size; i++)
    {
        if (list[i] == key)
            return i;
    }

    return -1;
}
```

In reviewing linearSearch(), notice that the for loop is simply used to access each element in the list, from first to last, until a match with the desired item is found. If the item is located, the index value of the current item is returned, which causes the loop to terminate; otherwise, the search continues until the end of the list is encountered.

To test this function, a main() driver function has been written to call linearSearch() and display the results it returns. Program 7.9 shows the complete test program.

### Program 7.9

```
#include <iostream>
using namespace std;

int linearSearch(int [], int, int); // function prototype

int main()
{
    const int NUMEL = 10;
    int nums[NUMEL] = {5,10,22,32,45,67,73,98,99,101};
    int item, location;

    cout << "Enter the item you are searching for: ";
    cin >> item;

    location = linearSearch(nums, NUMEL, item);

if (location > -1)
    cout << "The item was found at index location "
         << location << endl;
else
    cout << "The item was not found in the list\n";

return 0;
}

// this function returns the location of key in the list
// a -1 is returned if the value is not found
int linearSearch(int list[], int size, int key)
{
    int i;

    for (i = 0; i < size; i++)
    {
        if (list[i] == key)
            return i;
    }
    return -1;

}
```

The following are sample runs of Program 7.9:

```
Enter the item you are searching for: 101
The item was found at index location 9

and

Enter the item you are searching for: 65
The item was not found in the list
```

As noted previously, an advantage of linear searches is that the list doesn’t have to be in sorted order to perform the search. Another advantage is that if the search item is toward the front of the list, only a small number of comparisons are made. The worst case, of course, occurs when the search item is at the end of the list. On average, however, assuming the item is equally likely to be anywhere in the list, the number of required comparisons is n/2, where n is the list’s size. Therefore, for a 10-element list, the average number of comparisons needed for a linear search is 5, and for a 10,000-element list, the average number of comparisons needed is 5000. As you see next, this number can be reduced substantially by using a binary search algorithm.

### Binary Search

In a binary search, the list must be in sorted order. Starting with an ordered list, the desired item is first compared with the element in the middle of the list. (For lists with an even number of elements, either of the two middle elements can be used.) There are three possibilities after the comparison is made: The desired item might be equal to the middle element, it might be greater than the middle element, or it might be less than the middle element.

In the first case, the search has been successful, and no further searches are required. In the second case, because the desired item is greater than the middle element, it must be in the second half of the list, if it's found at all. This means the first part of the list, consisting of all elements from the first to the midpoint, can be discarded from any further search. In the third case, because the desired item is less than the middle element, it must be in the first part of the list, if it's found at all. For this case, the second half of the list, containing all elements from the midpoint to the last element, can be discarded from any further search.

The algorithm for this search strategy is shown in Figure 7.11 and defined by the following pseudocode:

```
Set the left index to 0
Set the right index to 1 less than the size of the list
Begin with the first item in the list

While the left index is less than or equal to the right index
Set the midpoint index to the integer average of the left and right index values
Compare the desired item with the midpoint element
If the desired element equals the midpoint element
Return the index value of the current item
Else If the desired element is greater than the midpoint element
Set the left index value to the midpoint value plus 1
Else If the desired element is less than the midpoint element
Set the right index value to the midpoint value less 1
EndIf
EndWhile
Return -1 if the item is not found
```
