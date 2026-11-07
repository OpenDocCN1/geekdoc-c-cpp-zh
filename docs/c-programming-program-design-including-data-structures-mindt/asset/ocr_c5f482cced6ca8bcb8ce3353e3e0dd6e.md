# EXAMPLE 21-18

```
```cpp
//STL functions find_end and find_first_of

#include <iostream>
#include <algorithm>
#include <iterator>

using namespace std;

int main()
{
    int list1[10] = {12, 34, 56, 21, 34,
                     78, 34, 56, 12, 25};
    int list2[2] = {34, 56};
    int list3[3] = {56, 21, 35};
    int list4[5] = {33, 40, 21, 34, 73};

    int* location;

    ostream_iterator<int> screenOut(cout, " ");

    cout << "Line 13: list1: ";
    copy(list1, list1 + 10, screenOut);
    cout << endl;

    cout << "Line 16: list2: ";
    copy(list2, list2 + 2, screenOut);
    cout << endl;

    //find_end
    location = find_end(list1, list1 + 10,
                        list2, list2 + 2);

    if (location != list1 + 10)
        cout << "Line 21: list2 is found in list1. "
             << "The last occurrence of \\n          "
             << "list2 in list 1 is at position "
             << (location - list1) << endl;
    else
        cout << "Line 23: list2 is not in list1."
             << endl;

    cout << "Line 24: list3: ";
    copy(list3, list3 + 3, screenOut);
    cout << endl;

    location = find_end(list1, list1 + 10,
                        list3, list3 + 3);
    if (location != list1 + 10)
        cout << "Line 29: list3 is found in list1. "
```
```