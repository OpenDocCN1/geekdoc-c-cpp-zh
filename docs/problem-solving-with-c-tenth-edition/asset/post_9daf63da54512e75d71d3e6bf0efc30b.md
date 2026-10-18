
## DISPLAY 15.6 Implementation for the Derived Class HourlyEmployee (part 1 of 2)

```
1   //This is the file: hourlyemployee.cpp
2   //This is the implementation for the class HourlyEmployee.
3   //The interface for the class HourlyEmployee is in
4   //the header file hourlyemployee.h.
5   #include <string>
6   #include <iostream>
7   #include "hourlyemployee.h"
8   using namespace std;

9   namespace employeeessavitch
10  {

11      HourlyEmployee::HourlyEmployee( ) : Employee( ), wageRate(0), hours(0)
12      {
13          //deliberately empty
14      }

15      HourlyEmployee::HourlyEmployee(string theName, string theNumber,
16                                      double theWageRate, double theHours)
17      : Employee(theName, theNumber), wageRate(theWageRate), hours(theHours)
18      {
19          //deliberately empty
20      }

21      void HourlyEmployee::setRate(double newWageRate)
22      {
23          wageRate = newWageRate;
24      }

25      double HourlyEmployee::getRate( ) const
26      {
27          return wageRate;
28      }

29      void HourlyEmployee::setHours(double hoursWorked)
30      {
31          hours = hoursWorked;
32      }

33      double HourlyEmployee::getHours( ) const
34      {
35          return hours;
36      }
```

## Parent and Child Classes

When discussing derived classes, it is common to use terminology derived from family relationships. A base class is often called a parent class. A derived class is then called a child class. This makes the language of inheritance very smooth. For example, we can say that a child class inherits member variables and member functions from its parent class. This analogy is often carried one step further. A class that is a parent of a parent of a parent of another class (or some other number of “parent of” iterations) is often called an ancestor class. If class A is an ancestor of class B, then class B is often called a descendant of class A.

## Inherited Members

A derived class automatically has all the member variables and all the ordinary member functions of the base class. (As discussed later in this chapter, there are some specialized member functions, such as constructors, that are not automatically inherited.) These members from the base class are said to be inherited. These inherited member functions and inherited member variables are, with one exception, not mentioned in the definition of the derived class, but they are automatically members of the derived class. As explained in the text, you do mention an inherited member function in the definition of the derived class if you want to change the definition of the inherited member function.

Note that the class Employee has all the code that is common to the two classes HourlyEmployee and SalariedEmployee. This saves you the trouble of writing identical code two times, once for the class HourlyEmployee and once for the class SalariedEmployee. Inheritance allows you to reuse the code in the class Employee.

## Constructors in Derived Classes

A constructor in a base class is not inherited in the derived class, but you can invoke a constructor of the base class within the definition of a derived class constructor, and that is all you need or normally want. A constructor for a derived class uses a constructor from the base class in a special way. A constructor for the base class initializes all the data inherited from the base class. Thus, a constructor for a derived class begins with an invocation of a constructor for the base class.

There is a special syntax for invoking the base class constructor that is illustrated by the constructor definitions for the class HourlyEmployee given in Display 15.6. In what follows we have reproduced (with minor changes in the line breaks to make it fit the text column) one of the constructor definitions for the class HourlyEmployee taken from that display:

```
HourlyEmployee::HourlyEmployee(string theName,
    string theNumber, double theWageRate,
    double theHours)
    : Employee(theName, theNumber),
      wageRate(theWageRate), hours(theHours)
{
    //deliberately empty
}
```

The portion after the colon is the initialization section of the constructor definition for the constructor HourlyEmployee::HourlyEmployee. The part Employee(theName, theNumber) is an invocation of the two-argument constructor for the base class Employee. Note that the syntax for invoking the base class constructor is analogous to the syntax used to set member variables: The entry wageRate(theWageRate) sets the value of the member variable wageRate to theWageRate; the entry Employee(theName, theNumber) invokes the base class constructor Employee with the arguments theName and theNumber. Since all the work is done in the initialization section, the body of the constructor definition is empty.

Here we reproduce the other constructor for the class HourlyEmployee from Display 15.6:

```
HourlyEmployee::HourlyEmployee( ) : Employee( ), wageRate(0),
    hours(0)
{
    //deliberately empty
}
```

In this constructor definition the default (zero-argument) version of the base class constructor is called to initialize the inherited member variables. You should always include an invocation of one of the base class constructors in the initialization section of a derived class constructor.

If a constructor definition for a derived class does not include an invocation of a constructor for the base class, then the default (zero-argument) version of the base class constructor will be invoked automatically. So, the following definition of the default constructor for the class HourlyEmployee (with Employee( ) omitted) is equivalent to the version we just discussed:

```
HourlyEmployee::HourlyEmployee( ) : wageRate(0), hours(0)
{
//deliberately empty
}
```

## An Object of a Derived Class Has More Than One Type

In everyday experience an hourly employee is an employee. In C++ the same sort of thing holds. Since `HourlyEmployee` is a derived class of the class `Employee`, every object of the class `HourlyEmployee` can be used anywhere an object of the class `Employee` can be used. In particular, you can use an argument of type `HourlyEmployee` when a function requires an argument of type `Employee`. You can assign an object of the class `HourlyEmployee` to a variable of type `Employee`. (But be warned: You cannot assign a plain old `Employee` object to a variable of type `HourlyEmployee`.) Of course, the same remarks apply to any base class and its derived class. You can use an object of a derived class anywhere that an object of its base class is allowed.

More generally, an object of a class type can be used anywhere that an object of any of its ancestor classes can be used. If class `Child` is derived from class `Ancestor` and class `Grandchild` is derived from class `Child`, then an object of class `Grandchild` can be used anywhere an object of class `Child` can be used, and the object of class `Grandchild` can also be used anywhere that an object of class `Ancestor` can be used.

However, we prefer to always explicitly include a call to a base class constructor, even if it would be invoked automatically.

A derived class object has all the member variables of the base class. When a derived class constructor is called, these member variables need to be allocated memory and should be initialized. This allocation of memory for the inherited member variables must be done by a constructor for the base class, and the base class constructor is the most convenient place to initialize these inherited member variables. That is why you should always include a call to one of the base class constructors when you define a constructor for a derived class. If you do not include a call to a base class constructor (in the initialization section of the definition of a derived class constructor), then the default (zero-argument) constructor of the base class is called automatically. (If there is no default constructor for the base class, that is an error condition.)

The call to the base class constructor is the first action taken by a derived class constructor. Thus, if class B is derived from class A and class C is derived from class B, then when an object of the class C is created, first a constructor for the class A is called, then a constructor for B is called, and finally the remaining actions of the C constructor are taken.
