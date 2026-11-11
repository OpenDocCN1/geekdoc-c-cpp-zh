![](bbox=[0.355, 0.153, 0.723, 0.252])

▲ **Figure 5: Representation of bucket2 Pointed by ptr2**

You can use the arrow (`->`) operator to access the individual members of `bucket1` as:

```
```cpp
ptr1->quantity = 3000;
ptr1->price = 30;
```
```

Similarly, members of `bucket2` can be accessed as:

```
```cpp
ptr2->quantity = 4000;
ptr2->price = 40;
```
```

Listing 10 shows how to use the pointer variables of a structure (you can find the StructurePointer.cpp file on the CD in the code\chapter5 folder):

# ▶ **Listing 10: Printing Structure Members by Using the Pointer and the Arrow -> Operator**

```
```cpp
#include <iostream.h>

struct bucket
{
    int quantity;
    int price;
};

int main()
{
    bucket bucket1,bucket2;   // declaring variables of the bucket structure
    bucket1.quantity = 1000;  //assigning values to the structure member
    bucket1.price = 10;      //assigning values to the structure member
    bucket2.quantity = 2000; //assigning values to the structure member
    bucket2.price = 20;      //assigning values to the structure member
    bucket  *ptr1, *ptr2;    //declaring pointer variables of a structure
    ptr1 = & bucket1;        //assigning pointer variable
    ptr2 = & bucket2;        //assigning pointer variable
    cout<<"printing quantity of bucket1 with pointer:"<<ptr1->quantity<<endl;
    cout<<"printing price of bucket1 with pointer:"<<ptr1->price<<endl;
    cout<<"printing quantity of bucket2 with pointer:"<<ptr2->quantity<<endl;
    cout<<"printing price of bucket2 with pointer:"<<ptr2->price<<endl;

    return 0;
}
```
```