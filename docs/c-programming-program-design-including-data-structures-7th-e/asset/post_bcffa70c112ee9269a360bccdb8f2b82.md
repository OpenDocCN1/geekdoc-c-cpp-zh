
```
Line 17: Largest element in list = 78
Line 19: Smallest element in list = 12
Line 21: list after random shuffle:
             12 34 25 56 12 78 55 21 34 34
```

The preceding output is self-explanatory. The details are left as an exercise for you.

## The Functions for_each and transform

The algorithm for_each is used to access and process each element in a given range by applying a function, which is passed as a parameter. The prototype of the function implementing this algorithm is:

```cpp
template <class inputItr, class function>
function for_each(inputItr first, inputItr last, function func);
```

The function specified by the parameter func is applied to each element in the range first...last-1. The function func can modify the element. The returned value of the function for_each is usually ignored.

The algorithm transform has two forms. The prototypes of the functions implementing this algorithm are:

```cpp
template <class inputItr, class outputItr,
          class unaryOperation>
outputItr transform(inputItr first, inputItr last,
                   outputItr destFirst,
                   unaryOperation op);
```

```cpp
template <class inputItr1, class inputItr2,
          class outputItr, class binaryOperation>
outputItr transform(inputItr1 first1, inputItr1 last1,
                    inputItr2 first2,
                    outputItr destFirst,
                    binaryOperation bOp);
```

The first form of the function transform has four parameters. This function creates a sequence of elements at the destination, beginning with destFirst, by applying the unary operation op to each element in the range first1...last1-1. This function returns the position one past the last element copied at the destination.

The second form of the function transform has five parameters. This function creates a sequence of elements by applying the binary operation bOp—that is, bOp(elemRange1, elemRange2)—to the corresponding elements in the range first1...last1-1 and the range beginning with first2. The resulting sequence is placed at the destination beginning with destFirst. The function returns the position one element past the last element copied at the destination.

Example 21-26 illustrates how to use these functions.

### EXAMPLE 21-26

```cpp
//STL Functions for for_each and transform

#include <iostream>
#include <cctype>
#include <algorithm>
#include <iterator>
#include <vector>

using namespace std;

void doubleNum(int& num);

int main()
{
    char cList[5] = {'a', 'b', 'c', 'd', 'e'};      //Line 1

    vector<char> charList(cList, cList + 5);        //Line 2

    ostream_iterator<char> screen(cout, " ");       //Line 3

    cout << "Line 4: cList: ";                      //Line 4
    copy(charList.begin(), charList.end(), screen); //Line 5
    cout << endl;                                   //Line 6

        //transform
    transform(charList.begin(), charList.end(),
              charList.begin(), toupper);           //Line 7

    cout << "Line 8: cList after changing all "
         << "lowercase letters to \n"
         << "          uppercase: ";                //Line 8
    copy(charList.begin(), charList.end(), screen); //Line 9
    cout << endl;                                   //Line 10

    int list[7] = {2, 8, 5, 1, 7, 11, 3};           //Line 11

    ostream_iterator<int> screenOut(cout, " ");     //Line 12

    cout << "Line 13: list: ";                      //Line 13
    copy(list, list + 7, screenOut);                //Line 14
    cout << endl;                                   //Line 15

    cout << "Line 16: The effect of for_each "
         << "function:\n        ";                  //Line 16

        //for_each
    for_each(list, list + 7, doubleNum);            //Line 17
    cout << endl;                                   //Line 18

    cout << "Line 19: list after a call to "
         << "for_each function:\n        ";         //Line 19
    copy(list, list + 7, screenOut);                //Line 20
    cout << endl;                                   //Line 21

    return 0;
}

void doubleNum(int& num)
{
    num = 2 * num;

    cout << num << " ";
}
```

### Sample Run:

```
Line 4: cList: a b c d e
Line 8: cList after changing all lowercase letters to
         uppercase: A B C D E
Line 13: list: 2 8 5 1 7 11 3
Line 16: The effect of for_each function:
          4 16 10 2 14 22 6
Line 19: list after a call to for_each function:
          4 16 10 2 14 22 6
```

The statement in Line 7 uses the function transform to change every lowercase letter of charList into its uppercase counterpart. The statement in Line 9 outputs the elements of charList. In the output, the line marked Line 8 contains the output of the statements in Lines 8 through 10 in the program. Notice that the fourth parameter of the function transform (in Line 7) is the function toupper from the header file cctype.

The statement in Line 17 calls the function for_each to process each element in the list using the function doubleNum. The function doubleNum has a reference parameter, num, of type int. Moreover, this function doubles the value of num and then outputs the value of num. Because num is a reference parameter, the value of the actual parameter is changed. In the output, the line marked Line 16 contains the output produced by the cout statement in the function doubleNum, which is passed as the third parameter of the function for_each (see Line 17). The statement in Line 20 outputs the values of the elements of list. In the output, Line 19 contains the output of the statements in Lines 19 through 20.

## The Functions includes, set_intersection, set_union, set_difference, and set_symmetric_difference

This section describes the set theory operations includes (subset), set_intersection, set_union, set_difference, and set_symmetric_difference. All of these algorithms assume that the elements within each given range are already sorted.

The algorithm includes determines whether the elements in one range appear in another range. This function has two forms, as shown by the following prototypes:

```cpp
template <class inputItr1, class inputItr2>
bool includes(inputItr1 first1, inputItr1 last1,
              inputItr2 first2, inputItr2 last2);

template <class inputItr1, class inputItr2,
          class binaryPredicate>
bool includes(inputItr1 first1, inputItr1 last1,
              inputItr2 first2, inputItr2 last2,
              binaryPredicate op);
```

Both forms of the function includes assume that the elements in the ranges first1...last1-1 and first2...last2-1 are sorted according to the same sorting criterion. The function returns true if all of the elements in the range first2...last2-1 are also in first1...last1-1. In other words, the function returns true if first1...last1-1 contains all of the elements in the range first2...last2-1. The first form assumes that the elements in both ranges are in ascending order. The second form uses the operation op to determine the ordering of the elements.

Example 21-27 illustrates how the function includes works.

### EXAMPLE 21-27

```cpp
//STL function includes
//This function assumes that the elements in the given ranges
//are ordered according to some sorting criteria

#include <iostream>
#include <algorithm>
#include <iterator>

using namespace std;

int main()
{
    char setA[5] = {'A', 'B', 'C', 'D', 'E'};       //Line 1
    char setB[10] = {'A', 'B', 'C', 'D', 'E',
                     'F', 'I', 'J', 'K', 'L'};      //Line 2
    char setC[5] = {'A', 'E', 'I', 'O', 'U'};       //Line 3

    ostream_iterator<char> screen(cout, " ");       //Line 4
    cout << "Line 5: setA: ";                       //Line 5
    copy(setA, setA + 5, screen);                   //Line 6
    cout << endl;                                   //Line 7

    cout << "Line 8: setB: ";                       //Line 8
    copy(setB, setB + 10, screen);                  //Line 9
    cout << endl;                                   //Line 10

    cout << "Line 11: setC: ";                      //Line 11
    copy(setC, setC + 5, screen);                   //Line 12
    cout << endl;                                   //Line 13

    if (includes(setB, setB + 10, setA, setA + 5))  //Line 14
        cout << "Line 15: setA is a subset of "
             << " setB." << endl;
    else
        cout << "Line 17: setA is not a subset "
             << "of setB." << endl;                 //Line 17

    if (includes(setB, setB + 10, setC, setC + 5))  //Line 18
        cout << "Line 19: setC is a subset of "
             << " setB." << endl;
    else
        cout << "Line 21: setC is not a subset "
             << "of setB." << endl;                 //Line 21

    return 0;
}
```

### Sample Run:

```
Line 5: setA: A B C D E
Line 8: setB: A B C D E F I J K L
Line 11: setC: A E I O U
Line 15: setA is a subset of setB
Line 21: setC is not a subset of setB
```

The preceding output is self-explanatory. The details are left as an exercise for you.

The algorithm set_intersection is used to find the elements that are common to two ranges of elements. This algorithm has two forms, as shown by the following prototypes:

```cpp
template <class inputItr1, class inputItr2,
          class outputItr>
outputItr set_intersection(inputItr1 first1, inputItr1 last1,
                          inputItr2 first2, inputItr2 last2,
                          outputItr destFirst);
```
