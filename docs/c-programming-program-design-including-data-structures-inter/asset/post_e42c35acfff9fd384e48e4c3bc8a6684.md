
## EXAMPLE 21-32

```cpp
//STL set theory functions: set_difference and
//                         set_symmetric_difference.
//These functions assume that the elements in the given
//ranges are ordered according to some sorting criteria.

#include <iostream>
#include <algorithm>
#include <iterator>

using namespace std;

int main()
{
    int setA[5] = {2, 4, 5, 7, 8};                 //Line 1
    int setB[7] = {3, 4, 5, 6, 7, 8, 10};          //Line 2
    int setC[5] = {1, 5, 6, 8, 15};                //Line 3

    int ADifferenceC[5];                            //Line 4
    int BsymDiffC[10];                              //Line 5

    int *lastElem;                                  //Line 6

    ostream_iterator<int> screen(cout, " ");       //Line 7

    cout << "Line 8: setA = ";                    //Line 8
    copy(setA, setA + 5, screen);                  //Line 9
    cout << endl;                                  //Line 10

    cout << "Line 11: setB = ";                   //Line 11
    copy(setB, setB + 7, screen);                  //Line 12
    cout << endl;                                  //Line 13

    cout << "Line 14: setC = ";                   //Line 14
    copy(setC, setC + 5, screen);                  //Line 15
    cout << endl;                                  //Line 16

    lastElem = set_difference(setA, setA + 5,
                              setC, setC + 5,
                              ADifferenceC);       //Line 17

    cout << "Line 18: ADifferenceC: ";            //Line 18
    copy(ADifferenceC, lastElem, screen);          //Line 19
    cout << endl;                                  //Line 20

    lastElem = set_symmetric_difference(setB, setB + 7,
                                        setC, setC + 5,
                                        BsymDiffC); //Line 21

    cout << "Line 22: BsymDiffC: ";               //Line 22
    copy(BsymDiffC, lastElem, screen);            //Line 23
    cout << endl;                                 //Line 24

    return 0;
}
```

### Sample Run:

```text
Line 8: setA = 2 4 5 7 8
Line 11: setB = 3 4 5 6 7 8 10
Line 14: setC = 1 5 6 8 15
Line 18: ADifferenceC: 2 4 7
Line 22: BsymDiffC: 1 3 4 7 10 15
```

The preceding output is self-explanatory. The details are left as an exercise for you.

## The Functions accumulate, adjacent_difference, inner_product, and partial_sum

The algorithms accumulate, adjacent_difference, inner_product, and partial_sum are numerical functions and thus manipulate numeric data. Each of these functions has two forms. The first form uses the natural operation to manipulate the data. For example, the algorithm accumulate finds the sum of all of the elements in a given range. In the second form, we can specify the operation to be applied to the elements of the range. For example, rather than add the elements of a given range, we can specify the multiplication operation to the algorithm accumulate to multiply the elements of the range. Next, we give the prototype of each of these algorithms followed by a brief explanation. The algorithms are contained in the header file numeric.

```cpp
template<class inputItr, class Type>
Type accumulate(inputItr first, inputItr last, Type init);
```

```cpp
template<class inputItr, class Type, class binaryOperation>
Type accumulate(inputItr first, inputItr last,
                Type init, binaryOperation op);
```

The first form of the algorithm accumulate adds all of the elements to an initial value specified by the parameter init in the range first...last-1. For example, if the value of init is 0, the algorithm returns the sum of all of the elements. In the second form, we can specify a binary operation, such as multiplication, to be applied to the elements of the range. For example, if the value of init is 1 and the binary operation is multiplication, the algorithm returns the product of the elements of the range.

Next, we describe the algorithm adjacent_difference. Its prototypes are:

```cpp
template <class inputItr, class outputItr>
outputItr adjacent_difference(inputItr first, inputItr last,
                              outputItr destFirst);
```

```cpp
template <class inputItr, class outputItr,
          class binaryOperation>
outputItr adjacent_difference(inputItr first, inputItr last,
                              outputItr destFirst,
                              binaryOperation op);
```

The first form creates a sequence of elements in which the first element is the same as the first element in the range first...last-1, and all other elements are the differences of the current and previous elements. For example, if the range of elements is:

```cpp
{2, 5, 6, 8, 3, 7}
```

then the sequence created by the function adjacent_difference is:

```cpp
{2, 3, 1, 2, -5, 4}
```

The first element is the same as the first element in the original range. The second element is equal to the second element in the original range minus the first element in the original range. Similarly, the third element is equal to the third element in the original range minus the second element in the original range, and so on.

In the second form of adjacent_difference, the binary operation op is applied to the elements in the range. The resulting sequence is copied at the destination specified by destFirst. For example, if the sequence is {2, 5, 6, 8, 3, 7} and the operation is multiplication, the resulting sequence is {2, 10, 30, 48, 24, 21}.

Both forms return an iterator positioned one past the last element copied at the destination.

The algorithm inner_product is used to manipulate the elements of two ranges. The prototypes of this algorithm are:

```cpp
template <class inputItr1, class inputItr2, class Type>
Type inner_product(inputItr1 first1, inputItr1 last,
                   inputItr2 first2, Type init);
```

```cpp
template <class inputItr1, class inputItr2, class Type,
          class binaryOperation1, class binaryOperation2>
Type inner_product(inputItr1 first1, inputItr1 last,
                   inputItr2 first2, Type init,
                   binaryOperation1 op1, binaryOperation2 op2);
```

The first form multiplies the corresponding elements in the range first1...last-1 and the range of elements starting with first2. The products of the elements are then added to the value specified by the parameter init. To be specific, suppose that elem1 ranges over the first range and elem2 ranges over the second range starting with first2. The first form computes:

```cpp
init = init + elem1 * elem2
```

For example, suppose that the two ranges are {2, 4, 7, 8} and {1, 4, 6, 9} and that init is 0. The function computes and returns:

```cpp
0 + 2 * 1 + 4 * 4 + 7 * 6 + 8 * 9 = 132
```

In the second form, the default addition can be replaced by the operation specified by `op1`, and the default multiplication can be replaced by the operation specified by `op2`. This form, in fact, computes:

```cpp
init = init op1 (elem1 op2 elem2);
```

The algorithm `partial_sum` has two forms, as shown by the following prototypes:

```cpp
template <class inputItr, class outputItr>
outputItr partial_sum(inputItr first, inputItr last,
                     outputItr destFirst);
```

```cpp
template <class inputItr, class outputItr,
          class binaryOperation>
outputItr partial_sum(inputItr first, inputItr last,
                     outputItr destFirst, binaryOperation op);
```

The first form creates a sequence of elements in which each element is the sum of all of the previous elements in the range `first . . . last-1` up to the position of the element. For example, the first element of the new sequence is the same as the first element in the range `first . . . last-1`, the second element is the sum of the first two elements in the range `first . . . last-1`, the third element of the new sequence is the sum of the first three elements in the range `first . . . last-1`, and so on. For example, for the sequence of elements:

```cpp
{1, 3, 4, 6}
```

the function `partial_sum` generates the following sequence:

```cpp
{1, 4, 8, 14}
```

In the second form, the default addition can be replaced by the operation specified by `op`. For example, if the sequence is:

```cpp
{1, 3, 4, 6}
```

and the operation is multiplication, the function `partial_sum` generates the following sequence:

```cpp
{1, 3, 12, 72}
```

The created sequence is copied at the destination specified by `destFirst` and returns an iterator positioned one past the last copied element at the destination.

Example 21-29 illustrates how the functions of this section work.
