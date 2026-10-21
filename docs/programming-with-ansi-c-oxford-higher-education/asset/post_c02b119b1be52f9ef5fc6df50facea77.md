
MIL initialization depends on the order of definition of the variables rather than their order of appearance in the MIL.

execute in the same order. It is even possible to provide function calls in the MIL, though it is not recommended because function call dependencies are not known precisely and hence may lead to serious errors.

## Initialization and assignment

The difference between initialization and assignment discussed in Section 5.12.1 also applies in this case.

Class object members can be initialized only using MIL. This is also true for constants and references. This means that when we use assignment, it is first defined and then assigned a value, which is wrong as these items are constants. Constants can only be given values at the time of initialization.

## Assignment always follows initialization

It has already been mentioned that the order of initialization depends on the order of definition of data members in the class, which may be different than the order of appearance and that the constructor body behaves in a different (rather normal) way. Let us see what is done in the following case.

```
TestOrder(unsigned Value)
:Third(Value /= 10),
Second(Value /= 10)
{
    Value /= 10
    First = Value;
}
```

The initialization of First has been moved in the constructor body. Now, Second is assigned first, then Third and finally First, that is, First will be 1, Second will be 123 and Third will be 12. This is because of the simple rule that all initializations should be carried out before the constructor body statements. This means that assignments will be carried out only after initializations take place.

## 5.13 DESTRUCTORS

When a variable is defined in C++, it continues to be in effect until its scope is over. If a variable is defined as a global variable, it remains in effect throughout the execution of the program. If a variable is defined as a local variable, say, in a function, it remains in effect until the function exits. If a variable is defined as follows:

```
for(int i=0; i<10; ++i)
{
    // statements
}
```

i is known only in the for loop. As soon as the for loop is over, i will cease to exist.

The compiler achieves this effect by creating a variable when it is defined and destroying it after its scope is over. The memory allocated at the time of creation is regained at the end and may be reused for some other purpose. This memory allocation is done on the stack. Dynamically created objects in C++ are an exception to this rule.

If customer is defined as given in the program, the memory obtained for ItemsInterested using new operator would not be regained after customer goes

out of scope. This is because the programmer and not the compiler has obtained that memory, and hence, it is the programmer’s job to release it back. In the given example, all objects of customer are a part of the main. The scope of the customer object is the main itself. Even if that memory (i.e., the new memory for ItemsInterested) is not returned, after the program execution is over the memory will be returned anyway. In this case, no harm is done if we do not deallocate the memory ourselves. If some of the customer objects were defined inside some function, the situation would be more serious. After claiming that memory, it will not be possible to return it even after coming back from that function. The memory allocated will be freed only after the execution of the program is over.

What should be done to get the allocated memory back immediately after the function call is over, that is, when the variable goes out of scope? The answer is to define destructors. As the name suggests, destructors are opposite to constructors. They come into effect when the object goes out of scope. Like constructors, they are automatically applied and calling them explicitly is also possible.

> Note The primary use of destructors is to free the memory dynamically allocated; however, they are also useful for providing terminating effects. If we would like to do something other than releasing memory when the object goes out of scope, such as reducing the value of a variable, say, by one, a destructor can be used.

## 5.13.1 Use of Destructors

Destructors are special functions that are used to execute automatically when the object of the class goes out of scope. They have the same name as of the class prefixed by “~”, for example, ~customer() is a destructor for class customer. The code written in the body of function ~customer() would be executed when the object of type customer goes out of scope. The destructor would also be called when delete is executed as shown in the following example.

```
Customer *pCust = new customer;
delete pCust; // the destructor is called at this place
```

In the following program, a destructor is defined for the point class. The point class now has a destructor, which displays the point that is going out of scope.

```
//PointDestructor.cpp
#include <iostream>
using namespace std;
class Point
{
private:
    float x, y;
public:
    Point(Point& OtherPoint)
    {
        x = OtherPoint.x;
        y = OtherPoint.y;
    }
    Point(float TempX = 0, float TempY = 0)
```

```
{
 x = TempX;
 y = TempY;
}
~Point()
{
cout << "Point at X = " << x << " Y = " << y << " Destroyed";
}
};
void main()
{
Point Point1(2,3);
Point Point2(4,5);
} // destructor is called here
Output
Point at X = 4 Y = 5 Destroyed
Point at X = 2 Y = 3 Destroyed
```

An interesting observation is that the destructor for the point defined later is executed before the point defined earlier. This is because when the objects are created, they are pushed on stack, which are destroyed by popping them, obviously in the reverse order.

Let us consider Program 5.8 to understand more about destructors. A destructor is provided for the customer class. It deletes the memory gained by new when the variable goes out of scope or when delete is called for customer object.

## PROGRAM 5.8 Using destructors

```
//Destructor1.cpp
#include <iostream>
#include <string>
using namespace std;
class Item
{
 int ItemNo; string ItemName;
public:
Item()
{
ItemNo = 0;
}
Item(int TempItemNo, string TempItemName)
{
ItemNo = TempItemNo;
ItemName = TempItemName;
}
void ShowDetails()
{
cout << "\n Item number is " << ItemNo;
cout << "\n Item name is " << ItemName;
}
};
```

```
class customer
{
    int CustNo;
    string CustName;
    string CustAddress;
    Item *ItemsInterested;
    int TotalItems;

    public:
        ~customer(); customer()
    {
        TotalItems = 0;
        ItemsInterested = 0; // assigning it to null
        cout << "Constructor is called";
    }

    void operator = (customer & CustRef)
    {
        CustNo = CustRef.CustNo;
        CustName = CustRef.CustName;
        CustAddress = CustRef.CustAddress;
        ItemsInterested = new Item[CustRef.TotalItems];
        // New memory for new object; this is the difference
        for(int i=0; i<CustRef.TotalItems; ++i)
        {
            ItemsInterested[i] = CustRef.ItemsInterested[i];
        }
        TotalItems = CustRef.TotalItems;
    }

    customer(int TempCustNo, string TempCustName, string TempCustAddress, Item *TempItemsInterested, int TempTotalItems)
    {
        CustNo = TempCustNo;
        CustName = TempCustName;
        CustAddress = TempCustAddress;
        ItemsInterested = new Item[TempTotalItems];
        for(int i=0; i<TempTotalItems; ++i)
        {
            ItemsInterested[i] = TempItemsInterested[i];
        }
        TotalItems = TempTotalItems;
        cout << "Parameterized constructor is called for " << CustName;
    }

    void ShowDetails()
    {
        cout << "\n Customer number is " << CustNo;
        cout << "\n Customer name is " << CustName;
        cout << "\n Customer address is " << CustAddress;
        cout << "\n" << CustName << " is interested in the following items:" << "\n";
        for(int i=0; i<TotalItems; i++)
        {
            ItemsInterested[i].ShowDetails();
        }
    }
};
// The following is the destructor
```
