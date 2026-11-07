```
```cpp
template <class forwardItr, class size, class Type>
void fill_n(forwardItr first, size n, const Type& value);
```
```

The first two parameters of the function `fill` are forward iterators specifying the starting and ending positions of the container; the third parameter is the filling element. The first parameter of the function `fill_n` is a forward iterator that specifies the starting position of the container, the second parameter specifies the number of elements to be filled, and the third parameter is the filling element. The program in Example 21-15 illustrates how to use these functions.

# ## EXAMPLE 21-15

```
```cpp
//STL functions fill and fill_n

#include <iostream>                                     //Line 1
#include <algorithm>                                    //Line 2
#include <iterator>                                     //Line 3
#include <vector>                                       //Line 4

using namespace std;                                    //Line 5

int main()                                              //Line 6
{                                                       //Line 7
    vector<int> vecList(8);                             //Line 8
    ostream_iterator<int> screen(cout, " ");            //Line 9

    fill(vecList.begin(), vecList.end(), 2);            //Line 10

    cout << "Line 11: After filling vecList "
         << "with 2s: ";                                //Line 11
    copy(vecList.begin(), vecList.end(), screen);       //Line 12
    cout << endl;                                       //Line 13

    fill_n(vecList.begin(), 3, 5);                      //Line 14

    cout << "Line 15: After filling the first three "
         << "elements with 5s: "
         << endl << "       ";                          //Line 15
    copy(vecList.begin(), vecList.end(), screen);       //Line 16
    cout << endl;                                       //Line 17

    return 0;                                           //Line 18
}                                                       //Line 19
```
```

```
```text
Sample Run:
Line 11: After filling vecList with 2s: 2 2 2 2 2 2 2 2
Line 15: After filling the first three elements with 5s:
       5 5 5 2 2 2 2 2
```
```