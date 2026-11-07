
```cpp
char setC[5] = {'A', 'E', 'I', 'O', 'U'};          //Line 9
ostream_iterator<char> screen(cout, " ");          //Line 10

cout << "Line 11: setA: ";                         //Line 11
copy(setA, setA + 5, screen);                      //Line 12
cout << endl;                                      //Line 13

cout << "Line 14: setB: ";                         //Line 14
copy(setB, setB + 10, screen);                     //Line 15
cout << endl;                                      //Line 16

cout << "Line 17: setC: ";                         //Line 17
copy(setC, setC + 5, screen);                      //Line 18
cout << endl;                                      //Line 19

if (includes(setB, setB + 10, setA, setA + 5))     //Line 20
    cout << "Line 21: setA is a subset of "        //Line 21
         << "setB." << endl;
else                                                //Line 22
    cout << "Line 23: setA is not a subset "       //Line 23
         << "of setB." << endl;

if (includes(setB, setB + 10, setC, setC + 5))     //Line 24
    cout << "Line 25: setC is a subset of "        //Line 25
         << "setB." << endl;
else                                                //Line 26
    cout << "Line 27: setC is not a subset "       //Line 27
         << "of setB." << endl;                    //Line 27

return 0;                                           //Line 28
}                                                   //Line 29
```

## Sample Run

```text
Line 11: setA: A B C D E
Line 14: setB: A B C D E F I J K L
Line 17: setC: A E I O U
Line 21: setA is a subset of setB.
Line 27: setC is not a subset of setB.
```

The preceding output is self-explanatory. The details are left as an exercise for you.

The algorithm `set_intersection` is used to find the elements that are common to two ranges of elements. This algorithm has two forms, as given by the following prototypes:

```cpp
template <class inputItr1, class inputItr2,
          class outputItr>
outputItr set_intersection(inputItr1 first1, inputItr1 last1,
                           inputItr2 first2, inputItr2 last2,
                           outputItr destFirst);
```

```cpp
template <class inputItr1, class inputItr2, class outputItr,
          class binaryPredicate>
outputItr set_intersection(inputItr1 first1, inputItr1 last1,
                           inputItr2 first2, inputItr2 last2,
                           outputItr destFirst,
                           binaryPredicate op);
```

Both forms create a sequence of sorted elements that are common to two sorted ranges, `first1...last1-1` and `first2...last2-1`. The created sequence is placed in the container beginning with `destFirst`. Both forms return an iterator positioned one past the last element copied at the destination range. The first form assumes that the elements are in ascending order; the second form assumes that both ranges are sorted using the operation specified by `op`. The elements in the source ranges are not modified.

Suppose that

```cpp
setA[5] = {2, 4, 5, 7, 8};
setB[7] = {1, 2, 3, 4, 5, 6, 7};
setC[5] = {2, 5, 8, 8, 15};
setD[6] = {1, 4, 4, 6, 7, 12};
setE[7] = {2, 3, 4, 4, 5, 6, 10};
```

Then:

```cpp
AintersectB = {2, 4, 5, 7}
AintersectC = {2, 5, 8}
DintersectE = {4, 4, 6}
```

Notice that because 8 appears only once in `setA`, 8 appears only once in `AintersectC`, even though 8 appears twice in `setC`. However, because 4 appears twice in both `setD` and `setE`, 4 also appears twice in `DintersectE`.

The algorithm `set_union` is used to find the elements that are contained in two ranges of elements. This algorithm has two forms, as given by the following prototypes:

```cpp
template <class inputItr1, class inputItr2,
          class outputItr>
outputItr set_union(inputItr1 first1, inputItr1 last1,
                    inputItr2 first2, inputItr2 last2,
                    outputItr destFirst);
```

```cpp
template <class inputItr1, class inputItr2,
          class outputItr, class binaryPredicate>
outputItr set_union(inputItr1 first1, inputItr1 last1,
                    inputItr2 first2, inputItr2 last2,
                    outputItr result, binaryPredicate op);
```

Both forms create a sequence of sorted elements that appear in the two sorted ranges `first1...last1-1` or `first2...last2-1`. The created sequence is placed in the container beginning with `destFirst`. Both forms return an iterator positioned one past the last element copied at the destination range. The first form assumes that the elements are in ascending order. The second form assumes that both ranges are sorted using the operation specified by `op`. The elements in the source ranges are not modified.

Suppose that you have `setA`, `setB`, `setC`, `setD`, and `setE` as defined previously. Then

```text
AunionB = {1, 2, 3, 4, 5, 6, 7, 8}
AunionC = {2, 4, 5, 7, 8, 8, 15}
BunionD = {1, 2, 3, 4, 4, 5, 6, 7, 12}
DunionE = {1, 2, 3, 4, 4, 5, 6, 7, 10, 12}
```

Notice that because 8 appears twice in `setC`, it appears twice in `AunionC`. Because 4 appears twice in `setD` and `setE`, 4 appears twice in `BunionD`.

Example 21-28 illustrates how the functions `set_union` and `set_intersection` work.

## EXAMPLE 21-28

```cpp
// STL set theory functions set_union and set_intersection
// These functions assume that the elements in the given
// ranges are ordered according to some sorting criteria

#include <iostream>                                      //Line 1
#include <algorithm>                                     //Line 2
#include <iterator>                                      //Line 3

using namespace std;                                     //Line 4

int main()                                              //Line 5
{
    int setA[5] = {2, 4, 5, 7, 8};                      //Line 7
    int setB[7] = {1, 2, 3, 4, 5, 6, 7};                //Line 8
    int setC[5] = {2, 5, 8, 8, 15};                     //Line 9
    int setD[6] = {1, 4, 4, 6, 7, 12};                  //Line 10

    int AunionB[10];                                     //Line 11
    int AunionC[10];                                     //Line 12
    int BunionD[15];                                     //Line 13
    int AintersectB[10];                                 //Line 14
    int AintersectC[10];                                 //Line 15

    int *lastElem;                                       //Line 16

    ostream_iterator<int> screen(cout, " ");             //Line 17

    cout << "Line 18: setA = ";                          //Line 18
    copy(setA, setA + 5, screen);                        //Line 19
    cout << endl;                                        //Line 20

    cout << "Line 21: setB = ";                          //Line 21
    copy(setB, setB + 7, screen);                        //Line 22
    cout << endl;                                        //Line 23

    cout << "Line 24: setC = ";                          //Line 24
    copy(setC, setC + 5, screen);                        //Line 25
    cout << endl;                                        //Line 26

    cout << "Line 27: setD = ";                          //Line 27
    copy(setD, setD + 6, screen);                        //Line 28
    cout << endl;                                        //Line 29

    lastElem = set_union(setA, setA + 5,
                         setB, setB + 7,
                         AunionB);                      //Line 30

    cout << "Line 31: Set AunionB: ";                    //Line 31
    copy(AunionB, lastElem, screen);                     //Line 32
    cout << endl;                                        //Line 33

    lastElem = set_union(setA, setA + 5,
                         setC, setC + 5,
                         AunionC);                      //Line 34

    cout << "Line 35: Set AunionC: ";                    //Line 35
    copy(AunionC, lastElem, screen);                     //Line 36
    cout << endl;                                        //Line 37

    lastElem = set_union(setB, setB + 7,
                         setD, setD + 6,
                         BunionD);                      //Line 38

    cout << "Line 39: Set BunionD: ";                    //Line 39
    copy(BunionD, lastElem, screen);                     //Line 40
    cout << endl;                                        //Line 41

    lastElem = set_intersection(setA, setA + 5,
                                setB, setB + 7,
                                AintersectB);            //Line 42

    cout << "Line 43: Set AintersectB: ";                //Line 43
    copy(AintersectB, lastElem, screen);                 //Line 44
    cout << endl;                                        //Line 45

    lastElem = set_intersection(setA, setA + 5,
                                setC, setC + 5,
                                AintersectC);            //Line 46

    cout << "Line 47: Set AintersectC: ";                //Line 47
    copy(AintersectC, lastElem, screen);                 //Line 48
    cout << endl;                                        //Line 49

    return 0;                                            //Line 50
}                                                        //Line 51
```
