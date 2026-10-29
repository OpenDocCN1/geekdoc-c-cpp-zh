
# REDEFINING AN INHERITED FUNCTION

A derived class inherits all the member functions (and member variables) that belong to the base class. However, if a derived class requires a different implementation for an inherited member function, the function may be redefined in the derived class. When a member function is redefined, you must list its declaration in the definition of the derived class, even though the declaration is the same as in the base class. If you do not wish to redefine a member function that is inherited from the base class, do not list it in the definition of the derived class.

## Display 16-7 Using Derived Classes (part 1 of 2)

```cpp
#include <iostream>
#include "hourlyemployee.h"
#include "salariedemployee.h"
using std::cout;
using std::endl;
using SavitchEmployees::HourlyEmployee;
using SavitchEmployees::SalariedEmployee;

int main()
{
    HourlyEmployee joe;

    joe.setName("Mighty Joe");
    joe.setSsn("123-45-6789");
    joe.setRate(20.50);
    joe.setHours(40);
    cout << "Check for " << joe.getName()
         << " for " << joe.getHours() << " hours.\n";
    joe.printCheck();
    cout << endl;

    SalariedEmployee boss("Mr. Big Shot", "987-65-4321", 10500.50);
    cout << "Check for " << boss.getName() << endl;
    boss.printCheck();

    return 0;
}
```

*The functions setName, setSsn, setRate, setHours, and getName are inherited unchanged from the class Employee. The function printCheck is redefined. The function getHours was added to the derived class HourlyEmployee.*

## Display 14.7 Using Derived Classes (part 2 of 2)

### SAMPLE DIALOGUE

```
Check for Mighty Joe for 40 hours.
------------------------------------------------
Pay to the order of Mighty Joe
The sum of 820 Dollars
------------------------------------------------
Check Stub: NOT NEGOTIABLE
Employee Number: 123-45-6789
Hourly Employee.
Hours worked: 40 Rate: 20.5 Pay: 820
------------------------------------------------
Check for Mr. Big Shot
------------------------------------------------
Pay to the order of Mr. Big Shot
The sum of 10500.5 Dollars
------------------------------------------------
Check Stub NOT NEGOTIABLE
Employee Number: 987-65-4321
Salaried Employee. Regular Pay: 10500.5
------------------------------------------------
```

# REDEFINING VERSUS OVERLOADING

Do not confuse redefining a function definition in a derived class with overloading a function name. When you redefine a function definition, the new function definition given in the derived class has the same number and types of parameters. When you overload a function, the function in the derived class has a different number of parameters or a parameter of a different type from the function in the base class, and the derived class has both functions. For example, suppose we added a function with the following function declaration to the definition of the class HourlyEmployee:

```
void setName(string firstName, string lastName);
```

The class HourlyEmployee would have this two-argument function setName and would also inherit the following one argument function setName:

```
void setName(string newName);
```

The class HourlyEmployee would have two functions named setName. This would be overloading the function name setName.

On the other hand, both the class Employee and the class HourlyEmployee define a function with the following function declaration:

```
void printCheck( );
```

In this case, the class HourlyEmployee has only one function named printCheck, but the definition of the function printCheck for the class HourlyEmployee is different from its definition for the class Employee. In this case, the function printCheck has been redefined.

If you get redefining and overloading confused, you do have one consolation: They are both legal. So, it is more important to learn how to use them than it is to learn to distinguish between them. Nonetheless, you should learn the difference between them.

# SIGNATURE

A function’s signature is the function’s name with the sequence of types in the parameter list, not including the const keyword and the ampersand, &. When you overload a function name, the two definitions of the function name must have different signatures using this definition of signature. (Some authorities include the const and/or ampersand as part of the signature, but we wanted a definition that works for explaining overloading.) A function that has the same name in a derived class as in the base class but has a different signature is overloaded, not redefined.

(As we noted in Chapter 4, some compilers will, in fact, allow you to overload on the basis of const versus no const, but you should not count on this. The C++ standard says it is not allowed.)

# ACCESS TO A REDEFINED BASE FUNCTION

Suppose you redefine a function so that it has a different definition in the derived class from what it had in the base class. The definition that was given in the base class is not completely lost to the derived class objects. However, if you want to invoke the version of the function given in the base class with an object in the derived class, you need some way to say “use the definition of this function as given in the base class (even though I am an object of the derived class).” The way you say this is to use the scope resolution operator with the name of the base class. An example should clarify the details.

Consider the base class Employee (Display 14.1) and the derived class HourlyEmployee (Display 14.3). The function printCheck( ) is defined in both classes. Now suppose you have an object of each class, as in the following:

```
Employee JaneE;
HourlyEmployee SallyH;
```

Then

```
JaneE.printCheck( );
```

uses the definition of printCheck given in the class Employee, and

```
SallyH.printCheck( );
```

uses the definition of printCheck given in the class HourlyEmployee.

But suppose you want to invoke the version of printCheck given in the definition of the base class Employee with the derived class object SallyH as the calling object for printCheck. You do that as follows:

```
SallyH.Employee::printCheck( );
```

Of course, you are unlikely to want to use the version of printCheck given in the particular class Employee, but with other classes and other functions, you may occasionally want to use a function definition from a base class with a derived class object. An example is given in Self-Test Exercise 6.

# FUNCTIONS THAT ARE NOT INHERITED

As a general rule, if Derived is a derived class with base class Base, then all "normal" functions in the class Base are usable inherited members of the class Derived. However, there are some special functions that are, for all practical purposes, not inherited. We have already seen that, as a practical matter, constructors are not inherited and that private member functions are not inherited. Destructors (discussed in Section 14.2) are also effectively not inherited.

The copy constructor is not inherited, but if you do not define a copy constructor in a derived class (or any class, for that matter), C++ will automatically generate a copy constructor for you. However, this default copy constructor simply copies the contents of member variables and does not work correctly for classes with pointers or dynamic data in their member variables. Thus, if your class member variables involve pointers, dynamic arrays, or other dynamic data, you should define a copy constructor for the class. This applies whether or not the class is a derived class.

The assignment operator = is also not inherited. If the base class Base defines the assignment operator, but the derived class Derived does not define the assignment operator, then the class Derived will have an assignment operator, but it will be the default assignment operator that C++ creates (when you do not define =); it will not have anything to do with the base class assignment operator defined in Base. Techniques for defining the assignment operator are discussed in the subsection "Assignment Operators and Copy Constructors in Derived Classes" of Section 14.2.

It is natural that constructors, destructors, and the assignment operator are not inherited. To correctly perform their tasks they need information that the base class does not possess; namely, they need to know about the new member variables introduced in the derived class.
