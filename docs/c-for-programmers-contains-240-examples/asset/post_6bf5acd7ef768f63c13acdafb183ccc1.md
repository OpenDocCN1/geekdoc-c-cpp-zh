
```
Time *timePtr = new Time( 12, 45, 0 );
```

initializes a newly created Time object to 12:45 PM and assigns the resulting pointer to timePtr.

As discussed earlier, the new operator can be used to allocate arrays dynamically. For example, a 10-element integer array can be allocated and assigned to gradesArray as follows:

```
int *gradesArray = new int[ 10 ];
```

which declares int pointer gradesArray and assigns it a pointer to the first element of a dynamically allocated 10-element array of ints. Recall that the size of an array created at compile time must be specified using a constant integral expression. However, the size of a dynamically allocated array can be specified using any non-negative integral expression that can be evaluated at execution time. Also note that, when allocating an array of objects dynamically, you cannot pass arguments to each object’s constructor. Instead, each object in the array is initialized by its default constructor. To delete the dynamically allocated array to which gradesArray points, use the statement

```
delete [] gradesArray;
```

The preceding statement deallocates the array to which gradesArray points. If the pointer in the preceding statement points to an array of objects, the statement first calls the destructor for every object in the array, then deallocates the memory. If the preceding statement did not include the square brackets ([]) and gradesArray pointed to an array of objects, the result is undefined. Some compilers call the destructor only for the first object in the array. Using delete on a null pointer (i.e., a pointer with the value 0) has no effect.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_451_0.png)

## Common Programming Error 10.9

> Using delete instead of delete [] for arrays of objects can lead to runtime logic errors. To ensure that every object in the array receives a destructor call, always delete memory allocated as an array with operator delete []. Similarly, always delete memory allocated as an individual element with operator delete; otherwise, the result of the operation is undefined.

## 10.7 static Class Members

There is an important exception to the rule that each object of a class has its own copy of all the data members of the class. In certain cases, only one copy of a variable should be shared by all objects of a class. A static data member is used for these and other reasons. Such a variable represents “class-wide” information (i.e., a property of the class shared by all instances, not a property of a specific object of the class). The declaration of a static member begins with keyword static. Recall that the versions of class GradeBook in Chapter 7 use static data members to store constants representing the number of grades that all GradeBook objects can hold.

Let us further motivate the need for static class-wide data with an example. Suppose that we have a video game with Martians and other space creatures. Each Martian tends to be brave and willing to attack other space creatures when the Martian is aware that there are at least five Martians present. If fewer than five are present, each Martian becomes cowardly. So each Martian needs to know the martianCount. We could endow each instance of class Martian with martianCount as a data member. If we do, every Martian will have a separate copy of the data member. Every time we create a new Martian, we’ll have to update the data member martianCount in all Martian objects. Doing this would require every Martian object to have, or have access to, handles to all other Martian objects in memory. This wastes space with the redundant copies and wastes time in updating the separate copies. Instead, we declare martianCount to be static. This makes martianCount class-wide data. Every Martian can access martianCount as if it were a data member of the Martian, but only one copy of the static variable martianCount is maintained by C++. This saves space. We save time by having the Martian constructor increment static variable martianCount and having the Martian destructor decrement martianCount. Because there is only one copy, we do not have to increment or decrement separate copies of martianCount for each Martian object.

### Performance Tip 10.3

> Use static data members to save storage when a single copy of the data for all objects of a class will suffice.

Although they may seem like global variables, a class’s static data members have class scope. Also, static members can be declared public, private or protected. A fundamental-type static data member is initialized by default to 0. If you want a different initial value, a static data member can be initialized once (and only once). A const static data member of int or enum type can be initialized in its declaration in the class definition. However, all other static data members must be defined at file scope (i.e., outside the body of the class definition) and can be initialized only in those definitions. Note that static data members of class types (i.e., static member objects) that have default constructors need not be initialized because their default constructors will be called.

A class’s private and protected static members are normally accessed through public member functions of the class or through friends of the class. (In Chapter 12, we’ll see that a class’s private and protected static members can also be accessed through protected member functions of the class.) A class’s static members exist even when no objects of that class exist. To access a public static class member when no objects of the class exist, simply prefix the class name and the binary scope resolution operator (::) to the name of the data member. For example, if our preceding variable martianCount is public, it can be accessed with the expression Martian::martianCount when there are no Martian objects. (Of course, using public data is discouraged.)

A class’s public static class members can also be accessed through any object of that class using the object’s name, the dot operator and the name of the member (e.g., myMartian.martianCount). To access a private or protected static class member when no objects of the class exist, provide a public static member function and call the function by prefixing its name with the class name and binary scope resolution operator. (As we’ll see in Chapter 12, a protected static member function can serve this purpose, too.) A static member function is a service of the class, not of a specific object of the class.

### Software Engineering Observation 10.11

> A class’s static data members and static member functions exist and can be used even if no objects of that class have been instantiated.

The program of Figs. 10.21–10.23 demonstrates a private static data member called count (Fig. 10.21, line 21) and a public static member function called getCount (Fig. 10.21, line 15). In Fig. 10.22, line 14 defines and initializes the data member count

```
#include <cstring> // strlen and strcpy prototypes
using std::strlen;
using std::strcpy;

#include "Employee.h" // Employee class definition

// define and initialize static data member at file scope
int Employee::count = 0; // cannot include keyword static

// define static member function that returns number of
// Employee objects instantiated (declared static in Employee.h)
int Employee::getCount()
{
    return count;
} // end static function getCount

// constructor dynamically allocates space for first and last name and
// uses strcpy to copy first and last names into the object
Employee::Employee( const char * const first, const char * const last )
{
    firstName = new char[ strlen( first ) + 1 ]; // create space
    strcpy( firstName, first ); // copy first into object

    lastName = new char[ strlen( last ) + 1 ]; // create space
    strcpy( lastName, last ); // copy last into object

    count++; // increment static count of employees

    cout << "Employee constructor for " << firstName
         << ' ' << lastName << " called." << endl;
} // end Employee constructor

// destructor deallocates dynamically allocated memory
Employee::~Employee()
{
    cout << "~Employee() called for " << firstName
         << ' ' << lastName << endl;

    delete [] firstName; // release memory
    delete [] lastName; // release memory

    count--; // decrement static count of employees
} // end ~Employee destructor

// return first name of employee
const char *Employee::getFirstName() const
{
    // const before return type prevents client from modifying
    // private data; client should copy returned string before
    // destructor deletes storage to prevent undefined pointer
    return firstName;
} // end function getFirstName
```
