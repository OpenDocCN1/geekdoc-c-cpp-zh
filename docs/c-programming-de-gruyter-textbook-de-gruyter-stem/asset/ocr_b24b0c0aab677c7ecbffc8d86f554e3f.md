# 6 Arrays, Pointers, and Strings

```
int main()
{
    cout<<"Step One:"<<endl;
    Point *Ptr1=new Point;
    //create object dynamically and initial value is not given,
    //so default constructor is called.
    delete Ptr1; //delete object, call destructor automatically
    cout<<"Step Two:"<<endl;
    Ptr1=new Point(1,2);
    //create object dynamically and initial value is given,
    //constructor with formal parameters is called
    delete Ptr1; //delete object, call destructor automatically
}
```

The running result of the program is as follows.

Step One:
Default Constructor called.
Destructor called.
Step Two:
Constructor called.
Destructor called.

The new operator can also create heap objects of the array type. In this case, we need to specify the array's structure. The syntax form of using the new operator to create a one-dimensional array is:

```
new type name T[Subscript expression];
```

The subscript expression denotes the number of array elements. Initial values of array elements cannot be assigned during the memory allocation of array. Note that if the array is created by new, when it is deleted by delete, we should add "[]" before the pointer name.

# Example 6.17: Create an object array dynamically.

```
//6_17.cpp
#include<iostream>
using namespace std;
class Point
{ //definition of the class is the same as in Example 6.16
    //....
}
```