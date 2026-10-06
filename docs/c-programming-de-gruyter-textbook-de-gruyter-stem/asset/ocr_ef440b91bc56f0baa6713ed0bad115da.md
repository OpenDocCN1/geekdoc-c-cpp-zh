# 6.2.11 Object Pointers

1. General Concepts of Object Pointers
Like various of basic data types, an object will take up some space in memory after the initialization. Therefore, we can access an either by its name or by its address. Although an object contains two types of members (data and functions), which is slightly different from general variables, the memory space occupied is used to store data members, without the copies of function members. Object pointers are used to store addresses, which follow the rules of general variables. The general form of declaring object pointers is

```
Class *object pointer name;
```

For example,

```
Point *p_Point;      //declare an object pointer variable of Point class
//p_Point
Point p1;               //declare the object of Point class p1
p_Point=&p1;           //assign the address of object p1 to p_Point and
                         //make p_Point point to p1
```

Like accessing members of an object using the object's name, we can access members of an object conveniently using the object pointer, whose syntax form is:

```
Object pointer name->member name
```

Example 6.12: Using pointers to access members of the Point class.cpp

```
//6_12.cpp
#include <iostream>
using namespace std;
class Point                            //Definition of the class
{
public:\                               //external interfaces
    Point(int xx=0, int yy=0) (X=xx;yy=yy); //constructor
    int GetX() {return X;}               //inline function, return X
    int GetY() {return Y;}\               //inline function, return Y
private:
    int X, Y;                           //private data
}

int main()                             //main function
{
    Point A(4,5);                      //declare and initialize object A
    Point *p1;                          //declare object pointer
```