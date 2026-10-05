
# 256 CHAPTER 6 Structures and Classes

## Member Function Definition
A member function is defined similar to any other function except that the Class_Name and the scope resolution operator, ::, are given in the function heading.

**SYNTAX**
```
Returned_Type Class_Name::Function_Name(Parameter_List)
{
  Function_Body_Statements
}
```
**EXAMPLE**
See Display 6.3. Note that the member variables (month and day) are not preceded by an object name and when they occur in a member function definition.

member variables in function definitions

Look at the definition of the member function DayOfYear::output given in Display 6.3. Notice that in the function definition of DayOfYear::output: we used the member names month and day by themselves without first getting the object and dot operator. That is not as strange as it may at first appear. At this point we are simply defining the member function output. This definition of output will apply to all objects of type DayOfYear, but at this point we do not know the names of the objects of type DayOfYear that we will use, so we cannot give them names. When the member function is called, as in

```
today.output();
```

all the member names in the function definition are specialized to the name of the calling object. So, the previous function call is equivalent to the following:

```cpp
switch (today.month)
{
  case 1:
    .
    .
}

cout << today.day;
```

# Classes 257

In the function definition for a member function, you can use the names of all members of that class (both the data members and the function members) without using the dot operator.

## The Dot Operator and the Scope Resolution Operator

Both the dot operator and the scope resolution operator are used with member names to specify what they are a member. For example, suppose you have declared a class DayOfYear and you declare an object today as follows:

```
DayOfYear today;
```

You use the dot operator to specify a member of the object today. For example, output is a member function for the class DayOfYear (defined in Display 6.3), and the following function call will output the data values stored in the object today:

```
today.output( );
```

You use the scope resolution operator, ::, to specify the class name when giving the function definition for a member function. For example, the heading of the function definition for the member function output would be as:

```
DayOfYear::output( )
```

Remember, the scope resolution operator, ::, is used with a class name, whereas the dot operator is used with an object of that class.

## A Class Is a Full-Fledged Type

A class is a type just like the int and double. You can have variables of a class type, you can have parameters of a class type, a function can return a value of a class type, and more generally, you can use a class type like any other type.

## Self-Test Exercises

- 9. Here we have redefined the class DayOfYear from Display 6.3 so that it now has one additional member function called input. Write an appropriate definition for the member function input.

```cpp
class DayOfYear
{
public:
    void input( );
    void output( );
    int month;
    int day;
```

(continued)

# 258 CHAPTER 6 Structures and Classes

## Self-Test Exercises (continued)

- 10. Given the following class definition, write an appropriate definition for the member function set.

```cpp
class Temperature {
  public:
    void set(double newDegrees, char newScale);
    //Sets the member variables to the values given as
    //arguments.
    double degrees;
    char scale; //F' for Fahrenheit or 'C' for Celsius.
};
```

- 11. Clearly distinguish between the meaning and use of the dot operator and the scope resolution operator, ::.

## Encapsulation

A data type, such as the type int, has specified values, such as 0, 1, -1, and 2 and so forth. You intend to think of the data type as having values, but the operations on these values are as important as the values. Without the operations, you could do nothing with the values. The operations for the type int consist of +, -, *, /, and a few other operations and predefined library functions. You should not think of a data type as simply a collection of values. A data type consists of a collection of values together with a set of basic operations defined on them. A data type is called abstract type (abbreviated ADT) if the programmers who use the type do not have access to the details of how the operations are implemented. The predefined types, such as int, are ADTs. You do not know how the operations such as + are implemented for the type int. Even if you knew, could not use this information in any C++ program. Classes, which are programmer-defined, should be hidden from, or at least to, any programmer who uses the class. The operations of a class are the (public) member functions of the class. A programmer who uses a class should not need to look at the definitions of the member functions. The member function declarations, and a few comments should be all the programmer needs in order to use the class.

A programmer uses a class also should not need to know how the data of the class is implemented. The implementation of the data should be hidden as the implementation of the member functions. In fact, it is close to distinguish between hiding the implementation of member functions and the implementation of the data. To a programmer, the class DayOfYear (Display 6.3) has dates as, numbers. The programmer should not know or care which is implemented as the int value 3, the quoted string "March", or some other. Defining a class so that the implementation of the member functions and the implementation of the data in objects are not known, or is at least irrelevant, to

# Classes 259

data types programmer who uses the class is known by a number of different terms. The most common terms used are information hiding, data abstraction, and encapsulation, each of which means the details of the implementation of a class are hidden from the programmer who uses the class. This principle is one of the main tenets of object-oriented programming. When discussing OOP, the term that is used most frequently is encapsulation. One of the ways to apply this principle of encapsulation to your class definitions is to make member variables private, which is what we discuss in the next section.

## Public and Private Members

Look back at the definition of the type DayOfYear in Class 6.3. In order to use that class, you need to know there are two member variables of type int that are named month and day. This violates the principle of encapsulation (information hiding) that we decided in the previous section. Class 6.4 is a rewritten version of the class DayOfYear that conforms to this encapsulation principle.

private member variable Notice the words private and public: in Class 6.4. All the items that follow the private: (in this case the member variables month and day) are said to be private, which means they cannot be referenced by name except within the definitions of the member functions of the class DayOfYear. For example, with the changed definition of the class DayOfYear, the two assignments and other code are no longer permitted in the main function of the program and are not permitted in any other function, except for member functions of the class DayOfYear:

```cpp
DayOfYear:
today.month = 12; //ILLEGAL
today.day = 25; //ILLEGAL
cout << today.month; //ILLEGAL
cout << today.day; //ILLEGAL
if (today.month == 1) //ILLEGAL
cout << "January";
```

Class 6.4 Class with Private Members (part 1 of 3)

```cpp
#include <iostream>
#include <cstdlib>
using namespace std;
class DayOfYear
{
public:
    void input();
    void output();
    void set(int newMonth, int newDay);
//Precondition: newMonth and newDay form a possible date.
    void set(int newMonth);
//Precondition: 1 <= newMonth <= 12
```

> This is an improved version of the class DayOfYear that we get in Display 6.3.
