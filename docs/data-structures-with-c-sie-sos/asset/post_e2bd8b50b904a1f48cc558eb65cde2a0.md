
![](img/f1df4c31f1795198a6843c842acc2216_113_0.png)

You have either reached a page that is unavailable for viewing or reached your viewing limit for this book.

![](img/f1df4c31f1795198a6843c842acc2216_114_0.png)

You have either reached a page that is unavailable for viewing or reached your viewing limit for this book.

In each stage we can see that either r is decreased or y is increased, thus showing the algorithm is finite and the length |X| of the region X, which is r + 1 - y decreases each time, and the 'sorted' condition B < Y < X < R remains true. When X = 0, the algorithm terminates, and thus we get our sorted list. The loop executed N number of times there are |B| + |R| calls to the routine swap.

## 4.4 REPRESENTATION OF LINEAR ARRAYS IN MEMORY

Let LA be a linear array in the memory of the computer. Recall that the memory of the computer is simply a sequence of addressed locations as pictured in Fig. 4.3. Let us use the notation

LOC(LA[K]) = address of the element LA[K] of the array LA

![](img/f1df4c31f1795198a6843c842acc2216_115_0.png)

Fig. 4.3 Computer Memory

As previously noted, the elements of LA are stored in successive memory cells. Accordingly, the computer does not need to keep track of the address of every element of LA, but needs to keep track only of the address of the first element of LA, denoted by

Base(LA)

and called the base address of LA. Using this address Base(LA), the computer calculates the address of any element of LA by the following formula:

```
LOC (LA[K]) = Base(LA) + w(K – lower bound) (4.2)
```

where w is the number of words per memory cell for the array LA. Observe that the time to calculate LOC(LA[K]) is essentially the same for any value of K. Furthermore, given any subscript K, one can locate and access the content of LA[K] without scanning any other element of LA.

## Example 4.4

Consider the array AUTO in Example 4.1(b), which records the number of automobiles sold each year from 1932 through 1984. Suppose AUTO appears in memory as pictured in Fig. 4.4. That is, Base(AUTO) = 200, and w = 4 words per memory cell for AUTO. Then

LOC(AUTO[1932]) = 200, LOC(AUTO[1933]) = 204, LOC(AUTO[1934]) = 208, ...

The address of the array element for the year K = 1965 can be obtained by using Eq. (4.2):

LOC(AUTO[1965]) = Base(AUTO) + w(1965 - lower bound)
= 200 + 4(1965 - 1932) = 332

Again we emphasize that the contents of this element can be obtained without scanning any other element in array AUTO.

![](img/f1df4c31f1795198a6843c842acc2216_116_0.png)

Fig. 4.4

## Program 4.8

There is a memory address for all the elements of an array. In the following program, we can see how an array limit value and an array element address are printed.

```
#include <stdio.h>
void printarray(int x[]);
main()
{
    int x[15];
    for(int i = 0;i<15;i++)
    {
    x[i]=i;
    }
    printarray(x);
}
void printarray(int x[])
{
    for(int i = 0;i<15;i++)
    {
    printf("Value in the array %d\n",x[i]);
    }
}
void printdetail(int x[])
{
    for(int i = 0;i<15;i++)
    {
    printf("Value in the array %d and address is %16lu\n",x[i],&x[i]);
    }
}
}
```

In the above program, the function ‘printarray’ is used to print values of each element in the array ‘array’. To print the value and address of all the elements and its address the printdetail function is used.

Now that we know all the elements are integer type, the difference between address is 2.

All the elements in the array are placed in consecutive memory spaces. The memory addresses can be printed using place holders %16lu or %p.

Remark: A collection A of data elements is said to be indexed if any element of A, which we shall call A<sub>K</sub>, can be located and processed in a time that is independent of K. The above discussion indicates that linear arrays can be indexed. This is very important property of linear arrays. In fact, linked lists, which are covered in the next chapter, do not have this property.

## 4.5 TRAVERSING LINEAR ARRAYS

Let A be a collection of data elements stored in the memory of the computer. Suppose we want to print the contents of each element of A or suppose we want to count the number of elements of A with a given property. This can be accomplished by traversing A, that is, by accessing and processing (frequently called visiting) each element of A exactly once.

The following algorithm traverses a linear array LA. The simplicity of the algorithm comes from the fact that LA is a linear structure. Other linear structures, such as linked lists, can also be easily traversed. On the other hand, the traversal of nonlinear structures, such as trees and graphs, is considerably more complicated.

![](img/f1df4c31f1795198a6843c842acc2216_118_0.png)

You have either reached a page that is unavailable for viewing or reached your viewing limit for this book.

## Example 4.5

Consider the array AUTO in Example 4.1(b), which records the number of automobiles sold each year from 1932 through 1984. Each of the following modules, which carry out the given operation, involves traversing AUTO.

- (a) Find the number NUM of years during which more than 300 automobiles were sold.
  - 1. [Initialization step.] Set NUM := 0.
  - 2. Repeat for K = 1932 to 1984: If AUTO[K] > 300, then: Set NUM := NUM + 1. [End of loop.]
  - 3. Return.

- (b) Print each year and the number of automobiles sold in that year.
  - 1. Repeat for K = 1932 to 1984: Write: K, AUTO[K]. [End of loop.]
  - 2. Return.

(Observe that (a) requires an initialization step for the variable NUM before traversing the array AUTO.)

## 4.6 INSERTING AND DELETING

Let A be a collection of data elements in the memory of the computer. “Inserting” refers to the operation of adding another element to the collection A, and “deleting” refers to the operation of removing one of the elements from A. This section discusses inserting and deleting when A is a linear array.

Inserting an element at the “end” of a linear array can be easily done provided the memory space allocated for the array is large enough to accommodate the additional element. On the other hand, suppose we need to insert an element in the middle of the array. Then, on the average, half of the elements must be moved downward to new locations to accommodate the new element and keep the order of the other elements.

Similarly, deleting an element at the “end” of an array presents no difficulties, but deleting an element somewhere in the middle of the array would require that each subsequent element be moved one location upward in order to “fill up” the array.

Remark: Since linear arrays are usually pictured extending downward, as in Fig. 4.1, the term “downward” refers to locations with larger subscripts, and the term “upward” refers to locations with smaller subscripts.

## Example 4.6

Suppose TEST has been declared to be a 5-element array but data have been recorded only for TEST[1], TEST[2] and TEST[3]. If X is the value of the next test, then one simply assigns

```
TEST[4] := X
```

to add X to the list. Similarly, if Y is the value of the subsequent test, then we simply assign

```
TEST[5] := Y
```

to add Y to the list. Now, however, we cannot add any new test scores to the list.

## Example 4.7

Suppose NAME is an 8-element linear array, and suppose five names are in the array, as in Fig. 4.5(a). Observe that the names are listed alphabetically, and suppose we want to keep the array names alphabetical at all times. Suppose Ford is added to the array. Then Johnson, Smith and Wagner must each be moved downward one location, as in Fig. 4.5(b). Next suppose Taylor is added to the array; then Wagner must be moved, as in Fig. 4.5(c). Last, suppose Davis is removed from the array. Then the five names Ford, Johnson, Smith, Taylor and Wagner must each be moved upward one location, as in Fig. 4.5(d). Clearly such movement of data would be very expensive if thousands of names were in the array.

### (a)
| | NAME |
|---|---|
| 1 | Brown |
| 2 | Davis |
| 3 | Johnson |
| 4 | Smith |
| 5 | Wagner |
| 6 | |
| 7 | |
| 8 | |

### (b)
| | NAME |
|---|---|
| 1 | Brown |
| 2 | Davis |
| 3 | Ford |
| 4 | Johnson |
| 5 | Smith |
| 6 | Wagner |
| 7 | |
| 8 | |

### (c)
| | NAME |
|---|---|
| 1 | Brown |
| 2 | Davis |
| 3 | Ford |
| 4 | Johnson |
| 5 | Smith |
| 6 | Taylor |
| 7 | Wagner |
| 8 | |

### (d)
| | NAME |
|---|---|
| 1 | Brown |
| 2 | Ford |
| 3 | Johnson |
| 4 | Smith |
| 5 | Taylor |
| 6 | Wagner |
| 7 | |
| 8 | |

Fig. 4.5

The following algorithm inserts a data element ITEM into the Kth position in a linear array LA with N elements. The first four steps create space in LA by moving downward one location each element from the Kth position on. We emphasize that these elements are moved in reverse order—i.e., first LA[N], then LA[N – 1], ..., and last LA[K]; otherwise data might be erased. (See Solved Problem 4.3) In more detail, we first set J := N and then, using J as a counter, decrease J each time the loop is executed until J reaches K. The next step, Step 5, inserts ITEM into the array in the space just created. Before the exit from the algorithm, the number N of elements in LA is increased by 1 to account for the new element.

```
**Algorithm 4.2:** (Inserting into a Linear Array) INSERT (LA, N, K, ITEM)
Here LA is a linear array with N elements and K is a positive integer such that K ≤ N. This algorithm inserts an element ITEM into the Kth position in LA.
1. [Initialize counter.] Set J := N.
2. Repeat Steps 3 and 4 while J ≥ K.
3. [Move Jth element downward.] Set LA[J + 1] := LA[J].
4. [Decrease counter.] Set J := J – 1.
[End of Step 2 loop.]
5. [Insert element.] Set LA[K] := ITEM.
6. [Reset N.] Set N := N + 1.
7. Exit.
```
