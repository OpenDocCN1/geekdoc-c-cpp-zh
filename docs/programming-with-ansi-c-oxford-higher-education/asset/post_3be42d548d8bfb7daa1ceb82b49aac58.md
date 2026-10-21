
```cpp
class Item
{
int ItemNo;
string ItemName;
public:
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
friend Item ModifyItem(customer & TempCust, int ItemNoToBeReplaced);
};
```

```cpp
class customer
{
int CustNo;
string CustName;
string CustAddress;
Item *ItemsInterested;
int TotalItems;
public:
customer()
{
TotalItems = 0;
ItemsInterested = 0; // assigning it to null
}
// The following is a copy constructor
customer(customer & CustRef)
{
CustNo = CustRef.CustNo;
CustName = CustRef.CustName;
CustAddress = CustRef.CustAddress;
ItemsInterested = new Item[CustRef.TotalItems]; /* New memory for new object. This is the difference. 
Compilers do not do this by default. */
for(int i=0; i<CustRef.TotalItems; ++i)
{
ItemsInterested[i] = CustRef.ItemsInterested[i];
}
TotalItems = CustRef.TotalItems;
}
customer(int TempCustNo, string TempCustName, string TempCustAddress,
Item *TempItemsInterested, int TempTotalItems)
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
}
void ShowDetails()
{
cout << "\n Customer number is " << CustNo;
cout << "\n Customer name is " << CustName;
cout << "\n Customer address is " << CustAddress;
cout << "\n" << CustName << "is interested in following items" << "\n";
for(int i=0; i<TotalItems; i++)
{
ItemsInterested[i].ShowDetails();
}
}
friend Item ModifyItem(customer & TempCust, int ItemNoToBeReplaced);
};
void main()
{
customer Steve;
Item ItemArray[]=
{
Item(3,"Sandwiches"), Item(4,"Paper Bags"),
Item(5,"Napkins"), Item(6,"Toys"), Item(10,"Biscuits"),
Item(9,"Pen"), Item(1,"Pencil"), Item(2,"Eraser"),
};
Steve = customer(2, "Steve Waugh", "Australia", ItemArray, 5);
customer Mark(Steve);
Steve.ShowDetails();
Mark.ShowDetails();
ModifyItem(Mark, 3);
Mark.ShowDetails();
Steve.ShowDetails();
// Without copy constructor, it would show the same result
}
/* The following function is using private variables of both the classes, so it is made friend of both */
Item ModifyItem(customer & TempCust, int ItemNoToBeReplaced)
{
for(int i=0; i<TempCust.TotalItems; ++i)
{
if(TempCust.ItemsInterested[i].ItemNo) == ItemNoToBeReplaced)
{
cout << "Enter new details for item to be replaced \n";
cout << "Enter item no. \n";
int TempItemNo;
cin >> TempItemNo;
cout << "Enter item name \n";
string TempItemName;
cin >> TempItemName;
TempCust.ItemsInterested[i].ItemNo=TempItemNo;
TempCust.ItemsInterested[i].ItemName=TempItemName;
}
```

# Changes in this Program

The following modifications were made to Program 5.6:

+   1. A new function ModifyItem() for modifying the details of items for customers is added. A customer reference is passed, so the changes made to it are reflected back in the customer data.
+   2. The function ModifyItem() needs to operate on private variables of both the classes, namely, Item and customer. Therefore, it is defined as a friend in both the classes. Such type of "bridge" friend function is sometimes very useful (though a careful designer can and should avoid such functions).
+   3. We need to know about class customer while discussing class Item and vice versa. (This is because both these classes contain friend definition, which contains both customer and Item.) It is not a problem for the class customer because the class Item is introduced before it and the compiler knows about the class Item while dealing with the class customer. However, this is not the case for the class Item. So, we need a forward reference to class customer. This is done initially when we write
+   
+       class customer;
+   
+   just before the definition of class Item.
+   4. We have now introduced a copy constructor. According to the definition, it has the reference to the customer as a single argument.

> Note When two classes refer to each other, the class defined earlier needs to have a forward reference for the class defined later.

# Case with no copy constructor

Let us see what would happen if the copy constructor is not available when ModifyItem(Mark, 3) is called.

To understand this, let us try to recap what happens when we write customer Mark(Steve). The content of Steve is copied into Mark. (Assume that the copy constructor is not available at the moment, so it would follow default behaviour.) The pointer to ItemsInterested is also copied as it is. It should be remembered that the contents of ItemsInterested do not have a separate storage in this case. Both Steve and Mark share the same address in ItemsInterested, and hence, the same array items. So, when we modify Mark's details while calling ModifyItem, we are indirectly accessing the same set of items pointed to by the pointer in the Steve object. Thus, our change would change both objects, Mark and Steve. This undesirable behaviour can be eliminated using copy constructors.

![](img/0da15892b2796544fb447dc5727e9ab4_231_0.png)

# Solving the problem using copy constructors

Let us look at the copy constructor now. It takes a reference of the class as a single argument. Then, it copies each item, except the pointer, to ItemsInterested. It obtains memory using new. It gets the memory good enough for storing the same number of items as the reference and it stores the items there. It should be noted that the contents

of ItemsInterested are not shared in this case. We get a new array. So, if ItemsInterested of Mark is changed later, it would not have any effect on that of Steve.

The copy constructor, as shown here, is a must if an item contains a dynamic constructor, that is, when a constructor is defined using the new operator.

## 5.12 PRIVATE COPY CONSTRUCTORS

If the copy constructor is defined in a private section, the objects of the class cannot call it. In a way, it stops the operations of the form customer Mark(Steve) or customer Mark = Steve. If such statements are written when the copy constructor is private, the program will not be compiled. This is very useful when a class is designed and the object code is provided to the user for using it. It should be noted that if the definition of the copy constructor is omitted, C++ would provide a default copy constructor (may not synthesize the physical one) and the user cannot be stopped from writing erroneous statements such as mentioned earlier . In this case, the contents of the copy constructor body are not executed, and hence, the body is usually left empty:

```
customer(customer & dummy){};
// see the empty body
```

### 5.12.1 Member Initialization List

Memberwise initialization list or member initialization list (MIL) is the method for initialization of the members of a class using the constructor function. It provides an alternative for providing initializations outside the constructor body. Let us consider the following program to understand it.

```
//SimpleMemberInitializationList.cpp
#include <iostream>
using namespace std;
class Time
{
public:
    int Hours;
    int Minutes;
    int Seconds;
    void ShowTime()
    {
        cout << "Time is " << Hours << " hours : " << Minutes << " minutes : and "
             << Seconds << " seconds \n";
    }
Time(){}
/* The following is a constructor using MIL */
Time(int TempHours, int TempMinutes, int TempSeconds)
:Hours(TempHours),
Minutes(TempMinutes),
Seconds(TempSeconds)
{ } // The empty body 
/* Second constructor */
};
```

```
void main()
{
    Time Time1(12,15,15);
    /* Second constructor with MIL is used here */
    cout << "Time number 1 \n";
    Time1.ShowTime();
}
```

An MIL appears in between the header and the body, starting with a colon.

The initialization list has been used in the second constructor for the Time class to initialize the Time object. Earlier, the same was done using assignment statements in the constructor body. Let us compare the two methods syntactically. The earlier approach was as follows:

```
Time(int TempHours, int TempMinutes, int TempSeconds)
{
    Hours = TempHours;
    Minutes = TempMinutes;
    Seconds = TempSeconds;
}
```

The MIL approach is as follows:

```
Time(int TempHours, int TempMinutes, int TempSeconds)
:Hours(TempHours),
Minutes(TempMinutes),
Seconds(TempSeconds)
{ } // the empty body
```

Syntactically, the MIL appears in between the body of the constructor and the header. It starts with a colon (:) and has all the initializations separated by a comma. The initialization has the normal syntax of initialization, that is, Variable(value) for initializing a variable with a value. In the given example, both the approaches yield the same result.

# Need for Initialization List

However, it is not true that both these approaches always yield the same result. There are some cases where the use of the second approach is a must (or is better). The difference between assignment and initialization has already been elaborated in Section 5.11.1. The assignment statements in the function body invoke the assignment operator whereas the MIL invokes initialization. The following sub-sections discuss the advantages of using the MIL approach.

# Readability

When the MIL is used in a constructor function, it is separated from the rest of the code, and thus, the program becomes more readable. (There is an argument against this. Those who are new to C++ claim that the syntax of the MIL is a bit cryptic and one can easily misunderstand it for a function call.) MIL has not been used in the examples in this book, but its use is advisable while writing commercial programs.

# Efficiency

The MIL is more efficient in certain cases. Consider the following program.
