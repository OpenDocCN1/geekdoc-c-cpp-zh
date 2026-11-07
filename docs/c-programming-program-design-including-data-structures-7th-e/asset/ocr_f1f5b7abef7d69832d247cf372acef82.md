# EXAMPLE 21-3

Consider the following statements:

```
```cpp
int intArray[7] = {1, 3, 5, 7, 9, 11, 13};    //Line 1
vector<int> vecList(intArray, intArray + 7);      //Line 2
vector<int> intVec;                               //Line 3
```
```

The statement in Line 2 declares and initializes the vector container vecList. Now consider the following statements:

```
```cpp
intVecIter = vecList.begin();                     //Line 4
++intVecIter;                                     //Line 5
vecList.insert(intVecIter, 22);                  //Line 6
```
```

The statement in Line 4 initializes the iterator intVecIter to the first element of vecList; the statement in Line 5 advances intVecIter to the second element of vecList. The statement in Line 6 inserts 22 at the position specified by intVecIter. After the statement in Line 6 executes, vecList = {1, 22, 3, 5, 7, 9, 11, 13}. Notice that the size of the container also increases.

The following example illustrates how to use a vector container in a program and how to process the elements in a vector container.

# EXAMPLE 21-4

```
```cpp
#include <iostream>
#include <vector>

using namespace std;

int main()
{
        vector<int> intList;                         //Line 1
        int i;                                       //Line 2

        intList.push_back(13);                       //Line 3
        intList.push_back(75);                       //Line 4
        intList.push_back(28);                       //Line 5
        intList.push_back(35);                       //Line 6

        cout << "Line 7: List elements: ";          //Line 7
        for (i = 0; i < 4; i++)                     //Line 8
                cout << intList[i] << " ";          //Line 9
        cout << endl;                                //Line 10

        for (i = 0; i < 4; i++)                     //Line 11
                intList[i] *= 2;                    //Line 12
```
```