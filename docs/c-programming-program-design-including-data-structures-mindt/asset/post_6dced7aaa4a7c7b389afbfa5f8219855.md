
Suppose that you want to determine whether 27 is in the list. A sequential search works as follows: First, you compare 27 with list[0], that is, compare 27 with 35. Because list[0] ≠ 27, you then compare 27 with list[1], that is, with 12, the second item in the list. Because list[1] ≠ 27, you compare 27 with the next element in the list, that is, compare 27 with list[2]. Because list[2] = 27, the search stops. This search is successful.

Let us now search for 10. As before, the search starts at the first element in the list, that is, at list[0]. Proceeding as before, we see that, this time, the search item, which is 10, is compared with every item in the list. Eventually, no more data is left in the list to compare with the search item. This is an unsuccessful search.

It now follows that, as soon as you find an element in the list that is equal to the search item, you must stop the search and report success. (In this case, you usually also report the location in the list where the search item was found.) Otherwise, after the search item is unsuccessfully compared with every element in the list, you must stop the search and report failure.

Suppose that the name of the array containing the list elements is `list`. The previous discussion translates into the following algorithm for the sequential search:

```text
found is set to false
loc = 0;

while (loc < listLength and not found)
    if (list[loc] is equal to searchItem)
        found is set to true
    else
        increment loc

if (found)
    return loc;
else
    return -1;
```

The following function performs a sequential search on a list. To be specific, and for illustration purposes, we assume that the list elements are of type `int`.

```cpp
int seqSearch(const int list[], int listLength, int searchItem)
{
    int loc;
    bool found = false;

    loc = 0;

    while (loc < listLength && !found)
        if (list[loc] == searchItem)
            found = true;
        else
            loc++;

    if (found)
        return loc;
    else
        return -1;
}
```

If the function seqSearch returns a value greater than or equal to 0, it is a successful search; otherwise, it is an unsuccessful search.

As you can see from this code, you start the search by comparing searchItem with the first element in the list. If searchItem is equal to the first element in the list, you exit the loop; otherwise, loc is incremented by 1 to point to the next element in the list. You then compare searchItem with the next element in the list, and so on.

## EXAMPLE 8-8

```cpp
// This program illustrates how to use a sequential search in a
// program.

#include <iostream>                                   //Line 1

using namespace std;                                  //Line 2

const int ARRAY_SIZE = 10;                            //Line 3

int seqSearch(const int list[], int listLength,
              int searchItem);                        //Line 4

int main()                                            //Line 5
{                                                     //Line 6
    int intList[ARRAY_SIZE];                          //Line 7
    int number;                                       //Line 8

    cout << "Line 9: Enter " << ARRAY_SIZE
         << " integers." << endl;                     //Line 9

    for (int index = 0; index < ARRAY_SIZE; index++) //Line 10
        cin >> intList[index];                        //Line 11

    cout << endl;                                     //Line 12

    cout << "Line 13: Enter the number to be "
         << "searched: ";                             //Line 13
    cin >> number;                                    //Line 14
    cout << endl;                                     //Line 15

    int pos = seqSearch(intList, ARRAY_SIZE, number); //Line 16

    if (pos != -1)                                    //Line 17
        cout << "Line 18: " << number
             << " is found at index " << pos
             << endl;                                 //Line 18
    else                                              //Line 19
        cout << "Line 20: " << number
             << " is not in the list." << endl;      //Line 20

    return 0;                                        //Line 21
}                                                    //Line 22

//Place the definition of the function seqSearch
//given previously here.
```

**Sample Run 1:** In this sample run, the user input is shaded.

```text
Line 9: Enter 10 integers.
16 45 37 29 80 32 67 78 10 30

Line 13: Enter the number to be searched: 29

Line 18: 29 is found at index 3
```

**Sample Run 2:**

```text
Line 9: Enter 10 integers.
16 45 37 29 80 32 67 78 10 30

Line 13: Enter the number to be searched: 12

Line 20: 12 is not in the list.
```

## Sorting

The previous section discussed a searching algorithm. In this section, we discuss how to sort an array using the algorithm, called **selection sort**.

As the name implies, in the **selection sort** algorithm, we rearrange the list by selecting an element in the list and moving it to its proper position. This algorithm finds the location of the smallest element in the unsorted portion of the list and moves it to the top of the unsorted portion of the list. The first time, we locate the smallest item in the entire list. The second time, we locate the smallest item in the list starting from the second element in the list, and so on.

Suppose you have the list shown in Figure 8-9.

![FIGURE 8-9](img/b217c421655b51e7494cf3b89bb5432d_596_0.png)

*FIGURE 8-9*  List of eight elements

Figure 8-10 shows the elements of `list` in the first iteration.

Initially, the entire list is unsorted. So, we find the smallest item in the list. The smallest item is at position 6, as shown in Figure 8-10(a). Since this is the smallest item, it must be moved to position 0. So, we swap 16 (that is, `list[0]`) with 5 (that is, `list[6]`), as shown in Figure 8-10(b). After swapping these elements, the resulting list is as shown in Figure 8-10(c).

![FIGURE 8-10](img/b217c421655b51e7494cf3b89bb5432d_597_0.png)

*FIGURE 8-10*  Elements of list during the first iteration

Figure 8-11 shows the elements of list during the second iteration.

Now the unsorted list is `list[1]...list[7]`. So, we find the smallest element in the unsorted list. The smallest element is at position 3, as shown in Figure 8-11(a). Because the smallest element in the unsorted list is at position 3, it must be moved to position 1. So, we swap 7 (that is, `list[3]`) with 30 (that is, `list[1]`), as shown in Figure 8-11(b). After swapping `list[1]` with `list[3]`, the resulting list is as shown in Figure 8-11(c).

![FIGURE 8-11](img/b217c421655b51e7494cf3b89bb5432d_597_1.png)

*FIGURE 8-11*  Elements of list during the second iteration

Now, the unsorted list is `list[2]...list[7]`. So, we repeat the preceding process of finding the (position of the) smallest element in the unsorted portion of the list and moving it to the beginning of the unsorted portion of the list. Selection sort thus involves the following steps.

In the unsorted portion of the list:

- a. Find the location of the smallest element.
- b. Move the smallest element to the beginning of the unsorted list.

Initially, the entire list (that is, `list[0]...list[length - 1]`) is the unsorted list. After executing Steps a and b once, the unsorted list is `list[1]...list[length - 1]`. After executing Steps a and b a second time, the unsorted list is `list[2]...list[length - 1]`, and so on. In this way, we can keep track of the unsorted portion of the list and repeat Steps a and b with the help of a `for` loop, as shown in the following pseudocode:

```text
for (index = 0; index < length - 1; index++)
{
    a. Find the location, smallestIndex, of the smallest element in
       list[index]...list[length - 1].

    b. Swap the smallest element with list[index]. That is, swap
       list[smallestIndex] with list[index].
}
```

The first time through the loop, we locate the smallest element in `list[0]...list[length - 1]` and swap the smallest element with `list[0]`. The second time through the loop, we locate the smallest element in `list[1]...list[length - 1]` and swap the smallest element with `list[1]`, and so on.

Step a is similar to the algorithm for finding the index of the largest item in the list, as discussed earlier in this chapter. (Also see Programming Exercise 2a at the end of this chapter.) Here, we find the index of the smallest item in the list. The general form of Step a is:

```text
smallestIndex = index;    // assume first element is the smallest

for (location = index + 1; location < length; location++)
    if (list[location] < list[smallestIndex])
        smallestIndex = location;    // current element in the list
                                      // is smaller than the smallest so
                                      // far, so update smallestIndex
```

Step b swaps the contents of `list[smallestIndex]` with `list[index]`. The following statements accomplish this task:

```text
temp = list[smallestIndex];
list[smallestIndex] = list[index];
list[index] = temp;
```

It follows that to swap the values, three item assignments are needed. The following function, `selectionSort`, implements the selection sort algorithm.
