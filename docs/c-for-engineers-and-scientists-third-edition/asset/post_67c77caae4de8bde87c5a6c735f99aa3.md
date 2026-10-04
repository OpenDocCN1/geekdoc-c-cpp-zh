
# Program 10.1

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

// class declaration section
class Date
{
private:
    int month;
    int day;
    int year;
public:
    Date(int = 7, int = 4, int = 2005); // constructor
    void setDate(int, int, int); // member function to copy a date
    void showDate(); // member function to display a date
};

// class implementation section
Date::setDate(int mm, int dd, int yyyy)
{
    month = mm;
    day = dd;
    year = yyyy;
}

void Date::showDate()
{
    cout << "The date is ";
    cout << setfill('0')
        << setw(2) << month << '/\'
        << setw(2) << day << '/\'
        << setw(2) << year % 100; // extract the last 2 year digits
    cout << endl;
}
```

## 562 Introduction to Classes

```cpp
int main()
{
    Date a, b, c(4,1,2000);    // declare 3 objects

    b.setDate(12,25,2006);      // assign values to b's data members
    a.showDate();                   // display object a's values
    b.showDate();                   // display object b's values
    c.showDate();                   // display object c's values

    return 0;
}
```

The declaration and implementation sections in the shaded area of Program 10.1 should look familiar. Notice, however, that this area declares the class; it doesn't create variables of this class type. This is true of all C++ types, including the built-in types, such as integers and doubles. Just as a variable of an integer type must be defined, variables of a user-declared class must also be defined. Variables defined to be of a user-declared class are referred to as **objects**.

Using this new syntax, the first statement in the Program 10.1 function defines three objects—named a, b, and c—to be of the class type. In C++, when a new object is defined, memory is allocated for the object, and its data members are initialized automatically by a call to the class constructor function. For example, the definition Date a, b, c(4,1,2000); in main(); When the object named a is defined, the constructor function Date() is called automatically. Because no parameters have been assigned to a, the default values of the constructor function are used, resulting in initialization:

- a.month = 7
- a.day = 4
- a.year = 2005

Notice the notation used here: an object name and an attribute name separated by a period. This is the standard syntax for referring to an object's attribute:

```
objectName.attributeName
```

The *objectName* is the name of a specific object, and *attributeName* is the name of a data member for the object's class. Therefore, the notation a.month = 7 indicates that a's data member has been set to the value 7. The notations a.day = 4 and a.year = 2005 indicate that a's day and year data members have been set to the values 4 and 2005.

In the same manner, when the object b is defined, the same default parameters are used, resulting in the initialization of b's data members as follows:

- b.month = 7
- b.day = 4
- b.year = 2005

## Chapter 10
### Abstract Data Types in C++ (Classes)

The object named c, however, is defined with the arguments 4, 1, and 2000. These arguments are passed to the constructor function when the object is defined, resulting in the initialization of c's data members:

```
c.month = 4
c.day = 1
c.year = 2000
```

The next statement in main(), b.setDate(12,25,2006), calls b's setDate() function, which assigns the values 12, 25, and 2006 to b's data members:

```
b.month = 12
b.day = 25
b.year = 2006
```

Notice the syntax for calling an object's method:

```
objectName.methodName(parameters)
```

The *objectName* is the name of a specific object, and *methodName* is the name of a function defined for the class. Because all class functions have been defined as public, a statement such as b.setDate(12,25,2006) is valid inside main(). Because all data members were specified as private, a statement such as b.month = 12 would be invalid inside main(). Therefore you are forced to rely on member functions to access data members.

The last three statements in main() call the showDate() function to operate on a, b, and c. The first call results in the display of a's data values, the second call in the display of b's data values, and the third call in the display of c's data values. Therefore, the output of Program 10.1 is:

```
The date is 07/04/05
The date is 12/25/06
The date is 04/01/00
```

Notice that a statement such as cout << is valid inside main() because cout doesn't know how to handle an object of class Date. Therefore the Date class is supplied with a function that can be used to access and display object's data.

## Terminology

As there is sometimes confusion about the classes, objects, and other object-oriented programming terminology, taking a moment to clarify and review the terminology is helpful.

### Interfaces, Implementations, and Information Hiding

The terms "interface" and "implementation" are used extensively in-object-oriented programming literature and can be equated to specific parts of a class's declaration and implementation sections.

An interface consists of a class's public declarations and any supporting comments. The implementation consists of both the class implementation section (containing private and public member definitions) and the class's data members, which are defined in the declaration section.

The implementation is the means of providing data hiding, which generally refers to the principle that how a class is constructed internally is irrelevant to programmers who want to use the class. The implementation can and should be hidden from all class users to ensure the class isn't altered or compromised in any way. All that a programmer needs to know to use a class correctly is provided by the interface.

A class is a programmer-defined data type from which objects can be created. Objects are created from classes; they have the same relationship to classes as variables to C++-in data types. For example, in the declaration:

```
int a;
```

a is said to be a variable, and in the Program 10.1 declaration:

```
Date a;
```

a is said to be an object. If it helps you to think of an object as a variable, do so. Objects are also referred to as instances of a class and the process of creating a new object is often referred as an instantiation of the object. Each time a new object is instantiated (created), a new set of data members belonging to the object is created. The values contained in these data members determine the object's state.

In this way, a class can be seen as a blueprint and each instance (object) of a class has its own set of values for the data members specified in the declaration section.

In addition to the data types allowed by a class, a class also defines behavior—that is, the operations to be performed on an object's data members. Users of the object need to know what these functions can do and how to activate them through function calls, but unless runtime or scope implications are relevant, they don't need to know how the operation is done. The actual implementation details of an object's operations are in the class implementation, which can (and should) be hidden from the user. Other names for the operations defined in a class implementation section are procedures, functions, and methods. These terms are used interchangeably throughout the remainder of the book.

> Note that only one set of class functions is created. These functions are shared between objects.

## Chapter 10
### Abstract Data Types in C++ (Classes)

## EXERCISES 10.1

- 1. (For Review) Define the following terms:
   a. Class
   b. Object
   c. Declaration section
   d. Implementation section
   e. Instance variable
   f. Member function
   g. Data member
   h. Constructor
   i. Class instance
   j. Services
   k. Methods
   l. Interface
   m. State
   n. Behavior

- 2. (For Thought) a. Instead of describing a rectangle's location by listing the position of two corner points, what other attributes could be?
   b. What other attributes, besides length and width, could be used to describe a rectangle to be drawn on a color monitor?
   c. Describe a set of attributes that could be used to define circles to be drawn on a black-and-white monitor.
   d. What attributes would you add to those selected in 2c if the circles are to be drawn on a color monitor?

- 3. (Practice) a. The attributes of a class represent how objects of the class appear to the outside world. The behavior represents how you think is the mechanism by which one object "triggers" the designated behavior in another object?
   b. If behavior in C++ is constructed by using an appropriate function, how do you think the behavior is activated in C++?

- 4. (Practice) Write a class declaration section for each of the following specifications. In each case, implement a prototype for a constructor and a member function named showdata() that can be used to display data member values.
   a. A class named Time that has integer data members named secs, mins, and hours
   b. A class named Complex that has double-precision data members named real and imaginary
   c. A class named Circle that has integer data members named xcenter and ycenter and a double-precision data member radius
   d. A class named System that has character data members named computer, printer, and screen, each capable of holding 30 characters (including the end-of-string NULL), and double-precision data members named compPrice, printPrice, and scrnPrice
