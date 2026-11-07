```
```cpp
cAssignmentOpOverload::cAssignmentOpOverload(int size)
{
    maxSize = size;
    length = 0;

    if (maxSize == 0)
        list = nullptr;
    else
        list = new int[maxSize];
}
```
```

```
```cpp
const cAssignmentOpOverload& cAssignmentOpOverload::operator=       //Line 1
                         (const cAssignmentOpOverload& otherList)   //Line 2
{
    if (this != &otherList)                 //avoid self-assignment; //Line 3
    {
        delete [] list;                                               //Line 4
        maxSize = otherList.maxSize;                                  //Line 5
        length = otherList.length;                                    //Line 6

        list = new int[maxSize];                                      //Line 8
        for (int i = 0; i < length; i++)                              //Line 9
            list[i] = otherList.list[i];                              //Line 10
    }                                                                  //Line 11

    return *this;                                                      //Line 12
}                                                                      //Line 13
```
```

The function to overload the assignment operator works as follows. The statement in Line 3 checks whether an object is copying itself. The statement in Line 5 destroys list. The statements in Lines 6 and 7 copy the values of the member variables maxSize and length of otherList into the member variables maxSize and length of list, respectively. The statement in Line 8 creates the array to store the numbers. The for loop in Line 9 copies otherList into list. The statement in Line 12 returns the address of this object, because the return type of the function operator= is a reference type.

The following program tests the class cAssignmentOpOverload:

```
```cpp
#include <iostream>                                      //Line 1

#include "classAssignmentOverload.h"                     //Line 2

using namespace std;                                      //Line 3

int main()                                               //Line 4
{
    cAssignmentOpOverload intList1(10);                   //Line 5
    cAssignmentOpOverload intList2;                       //Line 6
    cAssignmentOpOverload intList3;                       //Line 7
}                                                         //Line 8
```
```