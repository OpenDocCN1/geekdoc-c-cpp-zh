
```cpp
cout << "Line 23: temp1 list after copying "
     << "intList and " << endl
     << "     replacing 34 with 0: ";        //Line 23
copy(temp1.begin(), temp1.end(), screenOut); //Line 24
cout << endl;                               //Line 25

vector<int> temp2(10);                      //Line 26

//replace_copy_if
replace_copy_if(intList.begin(), intList.end(),
                temp2.begin(), lessThanEqualTo50, 50); //Line 27

cout << "Line 28: temp2 after copying intList "
     << "and replacing any " << endl
     << "     numbers less than 50 "
     << "with 50: " << endl << "         "; //Line 28
copy(temp2.begin(), temp2.end(), screenOut); //Line 29
cout << endl;                                //Line 30

return 0;
}

bool lessThanEqualTo50(int num)
{
    return (num <= 50);
}
```

### Sample Run

```text
Line 4: Character list: A a A B A c d e F A
Line 8: Character list after replacing A with Z:
        Z a Z B Z c d e F Z
Line 12: Character list after replacing the uppercase
        letters with *: * a * * * c d e * *
Line 18: intList: 12 34 56 21 34 78 34 55 12 25
Line 23: temp1 list after copying intList and
        replacing 34 with 0: 12 0 56 21 0 78 0 55 12 25
Line 28: temp2 after copying intList and replacing any
        numbers less than 50 with 50:
        50 50 56 50 50 78 50 55 50 50
```

The statement in Line 2 creates a vector, `charList`, of type `char` and initializes `charList` using the array `cList` created in Line 1. The statement in Line 3 declares an ostream iterator, `screen`. The statement in Line 5 outputs the value of `charList`. The statement in Line 7 uses the function `replace` to replace all occurrences of 'A' with 'Z' in `charList`. The statement in Line 9 outputs the elements of `charList`. In the output, the line marked Line 8 contains the outputs of Lines 8 through 10. The statement in Line 11 uses the function `replace_if` to replace the uppercase letters with '*' in the list `charList`. The statement in Line 13 outputs the elements of `charList`. In the output, the line marked Line 12 contains the output of Lines 12 through 14. The statement in Line 16 creates a vector, `intList`, of type `int` and initializes `intList` using the array `list`, created in Line 15. The statement in Line 19 outputs the elements of `intList`. The statement in Line 21 declares a vector `temp1` of type `int`. The statement in Line 22 copies all of the elements of `intList` and replaces 34 with 0. The list `intList` is not modified. The statement in Line 24 outputs the elements of `temp1`. The statement in Line 26 creates a vector, `temp2`, of type `int`, of 10 components. The statement in Line 27 uses the function `replace_copy_if` to copy the elements of `intList` and replaces all of the elements less than 50 with 50. The statement in Line 29 outputs the elements of `temp2`. In the output, the line marked Line 28 contains the output of Lines 28 through 30.

## The Functions `swap`, `iter_swap`, and `swap_ranges`

The functions `swap`, `iter_swap`, and `swap_ranges` are used to swap elements. These functions are defined in the header file algorithm. The prototypes of these functions are:

```cpp
template <class Type>
void swap(Type& object1, Type& object2);

template <class forwardItr1, class forwardItr2>
void iter_swap(forwardItr1 first, forwardItr2 second);

template <class forwardItr1, class forwardItr2>
void swap_ranges(forwardItr1 first1, forwardItr1 last1,
                 forwardItr2 first2);
```

The function `swap` swaps the values of object1 and object2. The function `iter_swap` swaps the values to which the iterators first and second point.

The function `swap_ranges` swaps the elements of the range first1...last1−1 with the consecutive elements starting at position first2. It returns the iterator of the second range positioned one past the last element swapped. The program in Example 21-20 illustrates how to use these functions.

### EXAMPLE 21-20

```cpp
//STL functions swap, iter_swap, and swap_ranges

#include <iostream>
#include <algorithm>
#include <vector>
#include <iterator>

using namespace std;

int main()
{
    char cList[10] = {'A', 'B', 'C', 'D', 'F',
                      'G', 'H', 'I', 'J', 'K'};             //Line 1

    vector<char> charList(cList, cList + 10);               //Line 2
    vector<char>::iterator charItr;                         //Line 3

    ostream_iterator<char> screen(cout, " ");              //Line 4

    cout << "Line 5: Character list: ";                    //Line 5
    copy(charList.begin(), charList.end(), screen);         //Line 6
    cout << endl;                                           //Line 7

    swap(charList[0], charList[1]);                         //Line 8

    cout << "Line 9: Character list after swapping "
         << "the first and second " << endl
         << "        elements: ";                           //Line 9
    copy(charList.begin(), charList.end(), screen);         //Line 10
    cout << endl;                                           //Line 11

    iter_swap(charList.begin() + 2,
              charList.begin() + 3);                        //Line 12

    cout << "Line 13: Character list after swapping "
         << "the third and fourth " << endl
         << "        elements: ";                           //Line 13
    copy(charList.begin(), charList.end(), screen);         //Line 14
    cout << endl;                                           //Line 15

    charItr = charList.begin() + 4;                         //Line 16
    iter_swap(charItr, charItr + 1);                        //Line 17

    cout << "Line 18: Character list after swapping "
         << "the fifth and sixth " << endl
         << "        elements: ";                           //Line 18
    copy(charList.begin(), charList.end(), screen);         //Line 19
    cout << endl;                                           //Line 20

    int list[10] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};        //Line 21

    vector<int> intList(list, list + 10);                   //Line 22

    ostream_iterator<int> screenOut(cout, " ");             //Line 23

    cout << "Line 24: intList: ";                          //Line 24
    copy(intList.begin(), intList.end(), screenOut);        //Line 25
    cout << endl;                                           //Line 26

    //swap_ranges
    swap_ranges(intList.begin(), intList.begin() + 4,
                intList.begin() + 5);                     //Line 27

    cout << "Line 28: intList after swapping the first "
         << "four elements" << endl
         << "        with four elements starting at "
         << "the sixth element" << endl
         << "        of intList: ";                    //Line 28
    copy(intList.begin(), intList.end(), screenOut);     //Line 29
    cout << endl;                                        //Line 30

    swap_ranges(list, list + 10, intList.begin());       //Line 31

    cout << "Line 32: list and intList after"
         << " swapping their elements" << endl;          //Line 32
    cout << "Line 33: list: ";                           //Line 33
    copy(list, list + 10, screenOut);                    //Line 34
    cout << endl;                                        //Line 35
    cout << "Line 36: intList: ";                       //Line 36
    copy(intList.begin(), intList.end(), screenOut);     //Line 37
    cout << endl;                                        //Line 38

    return 0;
}
```

### Sample Run

```text
Line 5: Character list: A B C D F G H I J K
Line 9: Character list after swapping the first and second
         elements: B A C D F G H I J K
Line 13: Character list after swapping the third and fourth
          elements: B A D C F G H I J K
Line 18: Character list after swapping the fifth and sixth
          elements: B A D C G F H I J K
Line 24: intList: 1 2 3 4 5 6 7 8 9 10
Line 28: intList after swapping the first four elements
          with four elements starting at the sixth element
          of intList: 6 7 8 9 5 1 2 3 4 10
Line 32: list and intList after swapping their elements
Line 33: list: 6 7 8 9 5 1 2 3 4 10
Line 36: intList: 1 2 3 4 5 6 7 8 9 10
```

The statement in Line 2 creates the vector charList and initializes it using the array cList declared in Line 1. The statement in Line 6 outputs the values of charList. The statement in Line 8 swaps the first and second elements of charList. The statement in Line 12, using the function iter_swap, swaps the third and fourth elements of charList. (Recall that the position of the first element in charList is 0.) After the statement in Line 16 executes, charItr points to the fifth element of charList. The statement in Line 17 uses the iterator charItr to swap the fifth and sixth elements of charList. The statement in Line 19 outputs the values of the elements of charList.
