
```cpp
bool lessThanEqualTo50(int num)
{
    return (num <= 50);
}
```

## Sample Run:

```text
Line 6: Character list: A a A B A C D E F A
Line 9: Character list after removing A: a B C D E F
Line 13: Character list after removing the uppercase
         letters: a c e
Line 20: intList: 12 34 56 21 34 78 34 55 12 25
Line 25: temp1 list after copying all the elements of intList
         except 34: 12 56 21 78 55 12 25
Line 30: temp2 after copying all the elements of intList except
         numbers less than 50: 56 78 55 0 0 0 0 0 0 0
```

The statement in Line 2 creates a vector list, charList, of type char and initializes charList using the array cList created in Line 1. The statement in Line 3 declares two vector iterators, lastElem and newLastElem. The statement in Line 4 declares an ostream iterator, screen. The statement in Line 6 outputs the value of charList. The statement in Line 8 uses the function remove to remove all occurrences of 'A' from charList. The function returns a pointer to one past the last element of the new range, which is stored in lastElem. The statement in Line 10 outputs the elements in the new range. (Note that the statement in Line 10 outputs the elements in the range charList.begin()...lastElem−1.) The statement in Line 12 uses the function remove_if to remove the uppercase letters from the list charList and stores the pointer returned by the function remove_if in newLastElem. The statement in Line 14 outputs the elements in the new range.

The statement in Line 17 creates a vector, intList, of type int and initializes intList using the array list, created in Line 16. The statement in Line 21 outputs the elements of intList. The statement in Line 24 copies all of the elements, except the occurrences of 34, of intList into temp1. The list intList is not modified. The statement in Line 26 outputs the elements of temp1. The statement in Line 28 creates a vector, temp2, of type int of 10 components and initializes all of the elements of temp2 to 0. The statement in Line 29 uses the function remove_copy_if to copy those elements of intList that are greater than 50. The statement in Line 31 outputs the elements of temp2.

## The Functions `replace`, `replace_if`, `replace_copy`, and `replace_copy_if`

The function replace is used to replace all occurrences, within a given range, of a given element with a new value. The function replace_if is used to replace the values of the elements, within a given range, satisfying certain criteria with a new value. The prototypes of these functions are:

```cpp
using namespace std;

bool lessThanEqualTo50(int num);

int main()
{
    char cList[10] = {'A', 'a', 'A', 'B', 'A',
                      'C', 'D', 'E', 'F', 'A'};          //Line 1

    vector<char> charList(cList, cList + 10);             //Line 2

    ostream_iterator<char> screen(cout, " ");            //Line 3

    cout << "Line 4: Character list: ";                  //Line 4
    copy(charList.begin(), charList.end(), screen);      //Line 5
    cout << endl;                                         //Line 6

        //replace
    replace(charList.begin(), charList.end(),
            'A', 'Z');                                   //Line 7

    cout << "Line 8: Character list after replacing "
         << "A with Z: " << endl
         << "                 ";                         //Line 8
    copy(charList.begin(), charList.end(), screen);       //Line 9
    cout << endl;                                         //Line 10

        //replace_if
    replace_if(charList.begin(), charList.end(),
               isupper, '*');                             //Line 11
    cout << "Line 12: Character list after "
         << "replacing the uppercase " << endl
         << "characters with *: ";                        //Line 12
    copy(charList.begin(), charList.end(), screen);       //Line 13
    cout << endl;                                         //Line 14

    int list[10] = {12, 34, 56, 21, 34,
                    78, 34, 55, 12, 25};                 //Line 15

    vector<int> intList(list, list + 10);                 //Line 16

    ostream_iterator<int> screenOut(cout, " ");           //Line 17

    cout << "Line 18: intList: ";                        //Line 18
    copy(intList.begin(), intList.end(), screenOut);      //Line 19
    cout << endl;                                         //Line 20

    vector<int> temp1(10);                                //Line 21

        //replace_copy
    replace_copy(intList.begin(), intList.end(),
                 temp1.begin(), 34, 0);                   //Line 22

    cout << "Line 23: temp1 list after copying "
         << "intList and " << endl
         << "          replacing 34 with 0: ";        //Line 23
    copy(temp1.begin(), temp1.end(), screenOut);       //Line 24
    cout << endl;                                      //Line 25

    vector<int> temp2(10);                             //Line 26

                 //replace_copy_if
    replace_copy_if(intList.begin(), intList.end(),
                    temp2.begin(), lessThanEqualTo50, 50); //Line 27

    cout << "Line 28: temp2 after copying intList "
         << "and replacing any " << endl
         << "          numbers less than 50 "
         << "          with 50: " << endl << "         "; //Line 28
    copy(temp2.begin(), temp2.end(), screenOut);       //Line 29
    cout << endl;                                      //Line 30

    return 0;
}

bool lessThanEqualTo50(int num)
{
    return (num <= 50);
}
```

## Sample Run:

```text
Line 4: Character list: A a A B A C D E F A
Line 8: Character list after replacing A with Z:
          Z a Z B Z C D E F Z
Line 12: Character list after replacing the uppercase
          letters with *: * * a * * c * e * *
Line 18: intList: 12 34 56 21 34 55 12 25
Line 23: temp1 list after copying intList and
          replacing 34 with 0: 12 0 56 21 0 55 12 25
Line 28: temp2 after copying intList and replacing any
          numbers less than 50 with 50:
          50 50 56 50 50 55 50 50
```

The statement in Line 2 creates a vector list, charList, of type `char` and initializes charList using the array cList created in Line 1. The statement in Line 3 declares an ostream iterator, screen. The statement in Line 5 outputs the value of charList. The statement in Line 7 uses the function `replace` to replace all occurrences of 'A' with 'Z' in charList. The statement in Line 9 outputs the elements of charList. In the output, the line marked Line 8 contains the output of Lines 8 through 10. The statement in Line 11 uses the function `replace_if` to replace the uppercase letters with '*' in the list charList. The statement in Line 13 outputs the elements of charList. In the output, the line marked Line 12 contains the output of Lines 12 through 14.

The statement in Line 16 creates a vector, `intList`, of type `int` and initializes `intList` using the array list, created in Line 15. The statement in Line 19 outputs the elements of `intList`. The statement in Line 21 declares a vector temp1 of type `int`. The statement in Line 22 copies all of the elements of `intList` and replaces 34 with 0. The list `intList` is not modified. The statement in Line 24 outputs the elements of temp1. The statement in Line 26 creates a vector, temp2, of type `int`, of 10 components. The statement in Line 27 uses the function `replace_copy_if` to copy the elements of `intList` and replaces all of the elements less than 50 with 50. The statement in Line 29 outputs the elements of temp2. In the output, the line marked Line 28 contains the output of Lines 28 through 30.

## The Functions `swap`, `iter_swap`, and `swap_ranges`

The functions `swap`, `iter_swap`, and `swap_ranges` are used to swap elements. These functions are defined in the header file algorithm. The prototypes of these functions are:

```cpp
template <class Type>
void swap(Type& object1, Type& object2);

template <class forwardItr1, class forwardItr2>
void iter_swap(forwardItr1 first, forwardItr2 second);

template <class forwardItr1, class forwardItr2>
forwardItr2 swap_ranges(forwardItr1 first1, forwardItr1 last1,
                         forwardItr2 first2);
```

The function `swap` swaps the values of object1 and object2. The function `iter_swap` swaps the values to which the iterators first and second point.

The function `swap_ranges` swaps the elements of the range first1...last1−1 with the consecutive elements starting at position first2. It returns the iterator of the second range positioned one past the last element swapped. The program in Example 22–20 illustrates how to use these functions.

## EXAMPLE 22-20

```cpp
//STL functions swap, iter_swap, and swap_ranges

#include <iostream>
#include <algorithm>
#include <vector>
#include <iterator>

using namespace std;
```
