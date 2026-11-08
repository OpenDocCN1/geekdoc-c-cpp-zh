
Other than integers, C++ allows any integral type to be used as an array index. This feature can greatly enhance a program’s readability. Consider the following statements:

```cpp
enum paintType {GREEN, RED, BLUE, BROWN, WHITE, ORANGE, YELLOW};
double paintSale[7];
paintType paint;
```

The following loop initializes each component of the array paintSale to 0:

```cpp
for (paint = GREEN; paint <= YELLOW;
             paint = static_cast<paintType>(paint + 1))
    paintSale[paint] = 0.0;
```

The following statement updates the sale amount of RED paint:

```cpp
paintSale[RED] = paintSale[RED] + 75.69;
```

As you can see, the above code is much easier to follow than the code that used integers for the index. For this reason, you should use the enumeration type for the array index or other integral data types wherever possible. Note that when using the enumeration type for array indices, use the default values of the identifiers in the enumeration type. That is, the value of the first identifier must be 0, and so on. (Recall from Chapter 7 that the default values of identifiers in an enumeration type start at 0; however, the identifiers can be set to other values.)

## Other Ways to Declare Arrays

Suppose that a class has 20 students and you need to keep track of their scores. Because the number of students can change from semester to semester, instead of specifying the size of the array while declaring it, you can declare the array as follows:

```cpp
const int NO_OF_STUDENTS = 20;
int testScores[NO_OF_STUDENTS];
```

Other forms used to declare arrays are:

```cpp
const int SIZE = 50;          //Line 1
typedef double list[SIZE];    //Line 2

list yourList;                //Line 3
list myList;                  //Line 4
```

The statement in Line 2 defines a data type list, which is an array of 50 components of type double. The statements in Lines 3 and 4 declare two variables, yourList and myList. Both are arrays of 50 components of type double. Of course, these statements are equivalent to:

```cpp
double yourList[50];
double myList[50];
```

## Searching an Array for a Specific Item

Searching a list for a given item is one of the most common operations performed on a list. The search algorithm we describe is called the sequential search or linear search. As the name implies, you search the array sequentially, starting from the first array element. You compare searchItem with the elements in the array (the list) and continue the search until either you find the item or no more data is left in the list to compare with searchItem.

Consider the list of seven elements shown in Figure 8-8.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_571_0.png)

**FIGURE 8-8**  List of seven elements

Suppose that you want to determine whether 27 is in the list. A sequential search works as follows: First, you compare 27 with list[0], that is, compare 27 with 35. Because list[0] ≠ 27, you compare 27 with list[1], that is, with 12, the second item in the list. Because list[1] ≠ 27, you compare 27 with the next element in the list, that is, compare 27 with list[2]. Because list[2] = 27, the search stops. This search is successful.

Let us now search for 10. As before, the search starts at the first element in the list, that is, at list[0]. Proceeding as before, we see that, this time, the search item, which is 10, is compared with every item in the list. Eventually, no more data is left in the list to compare with the search item. This is an unsuccessful search.

It now follows that, as soon as you find an element in the list that is equal to the search item, you must stop the search and report success. (In this case, you would also report the location in the list where the search item was found.) Otherwise, after the search item is unsuccessfully compared with every element in the list, you must stop the search and report failure.

Suppose that the name of the array containing the list elements is list. The previous discussion translates into the following algorithm for the sequential search:

```
found is set to false
loc = 0

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

The following function performs a sequential search on a list. To be specific, and for illustration purposes, we assume that the list elements are of type int.

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

### EXAMPLE 8-8

```cpp
// This program illustrates how to use a sequential search in a
// program.

#include <iostream>                                      //Line 1

using namespace std;                                     //Line 2

const int ARRAY_SIZE = 10;                               //Line 3

int seqSearch(const int list[], int listLength,          //Line 4
              int searchItem);

int main()                                               //Line 5
{
    int intList[ARRAY_SIZE];                              //Line 6
    int number;                                           //Line 7

    cout << "Line 9: Enter " << ARRAY_SIZE                //Line 9
         << " integers." << endl;

    for (int index = 0; index < ARRAY_SIZE; index++)      //Line 10
        cin >> intList[index];                            //Line 11

    cout << endl;                                         //Line 12

    cout << "Line 13: Enter the number to be "            //Line 13
         << "searched: ";
    cin >> number;                                        //Line 14
    cout << endl;                                         //Line 15

    int pos = seqSearch(intList, ARRAY_SIZE, number);     //Line 16

    if (pos != -1)                                        //Line 17
        cout << "Line 18: " << number
             << " is found at position " << pos
             << endl;                                     //Line 18
    else                                                  //Line 19
        cout << "Line 20: " << number
             << " is not in the list." << endl;           //Line 20

    return 0;                                             //Line 21
}                                                         //Line 22

//place the definition of the function seqSearch
//given previously here.
```

**Sample Run 1:** In this sample run, the user input is shaded.

Line 9: Enter 10 integers.

`2 56 34 25 73 46 89 10 5 16`

Line 13: Enter the number to be searched: **25**

Line 18: 25 is found at position 3

**Sample Run 2:**

Line 9: Enter 10 integers.

`2 56 34 25 73 46 89 10 5 16`

Line 13: Enter the number to be searched: **38**

Line 20: 38 is not in the list.

## Selection Sort

The previous section discussed a searching algorithm. In this section, we discuss how to sort an array using the algorithm, called **selection sort**. Additional searching and sorting algorithms are discussed in Chapter 16.

As the name implies, in the **selection sort** algorithm, we rearrange the list by selecting an element in the list and moving it to its proper position. This algorithm finds the location of the smallest element in the unsorted portion of the list and moves it to the top of the unsorted portion of the list. The first time, we locate the smallest item in the entire list. The second time, we locate the smallest item in the list starting from the second element in the list, and so on.

Suppose you have the list shown in Figure 8-9.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_574_0.png)

**FIGURE 8-9**  List of eight elements

Figure 8-10 shows the elements of list in the first iteration.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_574_1.png)

**FIGURE 8-10**  Elements of list during the first iteration

Initially, the entire list is unsorted. So, we find the smallest item in the list. The smallest item is at position 6, as shown in Figure 8-10(a). This is the smallest item, it must be moved to position 0. So, we swap 16 (that is, list[0]) with 5 (that is, list[6]), as shown in Figure 8-10(b). After swapping these elements, the resulting list is as shown in Figure 8-10(c).
