
# Pitfall

## Same Object on Both Sides of the Assignment Operator

Whenever you overload an assignment operator, always make sure your definition works when the same object occurs on both sides of the assignment operator. In most cases, you will need to make this a special case with some code of its own. An example of this is given in the programming example “Partially Filled Array with Backup.”

## Self-Test Exercises

- 8. Suppose Child is a class derived from the class Parent and that the class Grandchild is a class derived from the class Child. This question is concerned with the constructors and destructors for the three classes Parent, Child, and Grandchild. When a constructor for the class Grandchild is invoked, what constructors are invoked and in what order? When the destructor for the class Grandchild is invoked, what destructors are invoked and in what order?
- 9. Is the following alternative definition of the default constructor for the class PFArrayDBak (Displays 14.10 and 14.11) legal? (The invocation of the constructor from the base class has been omitted.) Explain your answer.

```cpp
PFArrayDBak::PFArrayDBak() : usedB(0)
{
    b = new double[capacity];
}
```

## Example:

## Alternative Implementation of PFArrayDBak

At first glance it may seem that we needed to make the member variables of the base class PFArrayD protected in order to give the definitions of the member functions for the derived class PFArrayDBak. After all, many of the member functions manipulate the inherited member variables a, used, and capacity. The implementation we gave in Display 14.11 does indeed refer to a, used, and capacity by name, and so those particular definitions do depend on these member variables being protected in the base class (as opposed to private). However, we have enough accessor and mutator functions in the base class that with just a bit more thinking, we can rewrite the implementation of the derived class PFArrayDBak so that it works even if all the member variables in the base class PFArrayD are private (rather than protected).

Display 14.13 shows an alternate implementation for the class PFArrayDBak that works fine even if all the member variables in the base class are private instead of protected. The parts that differ from our previous implementation are shaded. Most changes are obvious, but there are a few points that merit notice.

Consider the member function backup. In our previous implementation (Display 14.1), we copied the array entries from a to b. Since a is now private, we cannot access it by name, but we have overloaded the array square brackets operator (`operator[]`) so that it applies to objects of type PFArrayD, and this operator is inherited in PFArrayDBak. We simply use `operator[]` with the calling object. The net effect is to copy from the array a to the array b, but we never mention the private array a by name. The code is as follows:

```
usedB = getNumberUsed( );
for (int i = 0; i < usedB; i++)
    b[i] = operator[](i);
```

Be sure to note the syntax for calling an operator of the class being defined. If superArray is an object of the class PFArrayDBak, then in the invocation superArray.backup( ), the notation `operator[](i)` means superArray[i].

We could have used the notation `operator[](i)` in our definition of the member function restore, but it is just as easy to empty the array a with the inherited member function empty—Array and then add the backed-up elements using addElement. This way, we also set the private member variable used in the process.

With this alternate implementation, the class PFArrayDBak is used just as it was with the previous implementation. In particular, the demonstration program in Display 14.12 works exactly the same for either implementation.

## A Class Has Access to Private Members of All Objects of the Class

Consider the following lines from the implementation of the overloaded assignment operator given in Display 14.13:

```
usedB = rightSide.usedB;
for (int i = 0; i < usedB; i++)
    b[i] = rightSide.b[i];
```

You might object that rightSide.usedB and rightSide.b[i] are illegal since usedB and b are private member variables of some object other than the calling object. Normally that objection would be correct. However, the object rightSide is of the same type as the class being defined, and so this is legal.

In the definition of a class, you can access private members of any object of the class, not just private members of the calling object.

## Display 14.13  Alternate Implementation of PFArrayDBak (part 1 of 2)

```
//This is the file pfarraydbak.cpp.
//This is the implementation of the class PFArrayDBak.
//The interface for the class PFArrayDBak is in the file pfarraydbak.h.
#include "pfarraydbak.h"
#include <iostream>
using std::cout;

PFArrayDBak::PFArrayDBak( ) : PFArrayD( ), usedB(0)
{
    b = new double[getCapacity( )];
}

PFArrayDBak::PFArrayDBak(int capacityValue) : PFArrayD(capacityValue), usedB(0)
{
    b = new double[getCapacity( )];
}

PFArrayDBak::PFArrayDBak(const PFArrayDBak& oldObject)
    : PFArrayD(oldObject), usedB(0)
{
    b = new double[getCapacity( )];
    usedB = oldObject.usedB;
    for (int i = 0; i < usedB; i++)
        b[i] = oldObject.b[i];
}

void PFArrayDBak::backup( )
{
    usedB = getNumberUsed( );
    for (int i = 0; i < usedB; i++)
        b[i] = operator[ ](i);
}

void PFArrayDBak::restore( )
{
    emptyArray( );
    for (int i = 0; i < usedB; i++)
        addElement(b[i]);
}

PFArrayDBak& PFArrayDBak::operator =(const PFArrayDBak& rightSide)
{
    PFArrayD::operator =(rightSide);
}
```

> This implementation works even if all the member variables in the base class are private (rather than protected).

> Invocation of the square brackets operator with the calling object

## Display 14.13  Alternate Implementation of PFArrayDBak (part 2 of 2)

```
39    if (getCapacity() != rightSide.getCapacity())
40    {
41        delete [] b;
42        b = new double[rightSide.getCapacity()];
43    }
44
45    usedB = rightSide.usedB;
46    for (int i = 0; i < usedB; i++)
47        b[i] = rightSide.b[i];

48    return *this;
49 }

50 PFArrayDBak::~PFArrayDBak( )
51 {
52    delete [] b;
53 }
```

## Tip  “Is A” VERSUS “Has A”

- “is a” relationship
- “has a” relationship

Early in this chapter we defined a derived class called HourlyEmployee using the class Employee as the base class. In such a case an object of the derived class HourlyEmployee is also of type Employee. Stated more simply, an HourlyEmployee is an Employee. This is an example of the “is a” relationship between classes. It is one way to make a more complex class from a simpler class.

Another way to make a more complex class from a simpler class is known as the “has a” relationship. For example, if you have a class that represents a date, then you might add a date of employment to the Employee class by adding a member variable of type Date to the Employee class. In this case we say an Employee “has a” Date. As another example, if we have an appropriately named class to simulate a jet engine and we are defining a class to simulate a passenger airplane, then we can give the PassengerAirPlane class one or more member variables of type JetEngine. In this case we say that a PassengerAirPlane “has a” JetEngine.

In most situations you can make your code work with either an “is a” relationship or a “has a” relationship. It seems silly (and it is silly) to make the PassengerAirPlane class a derived class of the JetEngine class, but it can be done and can be made to work (perhaps with difficulty). Fortunately, the best programming technique is to simply follow what sounds most natural in English. It makes more sense to say “A passenger airplane has a jet engine” than it does to say “A passenger airplane is a jet engine.” So, it makes better programming sense to have JetEngine as a member variable of a PassengerAirPlane class. It makes little sense to make the PassengerAirPlane class a derived class of the JetEngine class.
