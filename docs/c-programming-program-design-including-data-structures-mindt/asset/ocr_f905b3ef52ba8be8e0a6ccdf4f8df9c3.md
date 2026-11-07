```
```cpp
    if (found)
        return loc;
    else
        return -1;
}
```
```

If the function seqSearch returns a value greater than or equal to 0, it is a successful search; otherwise, it is an unsuccessful search.

As you can see from this code, you start the search by comparing searchItem with the first element in the list. If searchItem is equal to the first element in the list, you exit the loop; otherwise, loc is incremented by 1 to point to the next element in the list. You then compare searchItem with the next element in the list, and so on.

# EXAMPLE 8-8

```
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

    if (pos!= -1)                                     //Line 17
        cout <<"Line 18: " << number
```
```