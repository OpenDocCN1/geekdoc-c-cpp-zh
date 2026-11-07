
## Syntax for Operator Functions

The result of an operation is a value. Therefore, the operator function is a value-returning function.

The syntax of the heading for an operator function is:

```
returnType operator operatorSymbol(formal parameter list)
```

In C++, `operator` is a reserved word.

Recall that the only built-in operations on classes are assignment (=) and member selection. To use other operators on class objects, they must be explicitly overloaded. Operator overloading provides the same concise expressions for user-defined data types as it does for built-in data types.

To overload an operator for a class:

- 1. Include the statement to declare the function prototype to overload the operator (that is, the operator function) in the definition of the class.
- 2. Write the definition of the operator function.

Certain rules must be followed when you include an operator function in a class definition. These rules are described in the section, "Operator Functions as Member Functions and Nonmember Functions" later in this chapter.

## Overloading an Operator: Some Restrictions

When overloading an operator, keep the following in mind:

- 1. You cannot change the precedence of an operator.
- 2. The associativity cannot be changed. (For example, the associativity of the arithmetic operator addition is from left to right, and it cannot be changed.)
- 3. Default parameters cannot be used with an overloaded operator.
- 4. You cannot change the number of parameters an operator takes.
- 5. You cannot create new operators. Only existing operators can be overloaded.
- 6. The operators that cannot be overloaded are:
    - `.` `.*` `::` `?:` `sizeof`
- 7. The meaning of how an operator works with built-in types, such as `int`, remains the same. That is, you cannot redefine how operators work with built-in data types.
- 8. Operators can be overloaded either for objects of the user-defined types, or for a combination of objects of the user-defined type and objects of the built-in type.

## EXAMPLE 13-1

In the beginning of this chapter, we remarked that if we can overload various operators for a class, then we can increase the flexibility of the class. Now that we know the syntax to overload an operator for a class and certain restrictions on operator overloading, in this example, we only illustrate how to overload the relational operator `==` for the class `clockType`. After discussing, in general, various concepts related to operator overloading, later in this chapter in the Programming Example clockType, we will show how to overload other operators, such as `>>`, `<<`, and `++` (pre-increment), for the class `clockType`.

The prototype of the function to overload the equality operator for the class `clockType` is:

```cpp
bool operator==(const clockType& otherClock) const;
```

Therefore, this statement must be included in the definition of the class `clockType`. Because in this example we are illustrating how to only overload the operator `==`, we do not include the functions to increment the time. So consider the following definition of the class `clockType`:

```cpp
class clockType
{
public:
    void setTime(int hours, int minutes, int seconds);
    void printTime() const;

    bool operator==(const clockType& otherClock) const;
        //Overload the operator ==

    clockType(int = 0, int = 0, int = 0);

private:
    int hr;
    int min;
    int sec;
};
```

Next we must write the definition of the function `operator==`, which is:

```cpp
bool clockType::operator==(const clockType& otherClock) const
{
    return (hr == otherClock.hr && min == otherClock.min
            && sec == otherClock.sec);
}
```

Notice that the body of the function `operator==` is the same as the body of the function `equalTime` given in Chapter 10. Also, the definitions of other functions of the class `clockType` are the same as given in Chapter 10.

The following program illustrates how to use the modified definition of the class clockType:

```cpp
#include <iostream>
#include "clockType.h"

using namespace std;

int main()
{
        clockType myClock(8, 23, 50);
        clockType yourClock(8, 23, 50);
        clockType tempClock(9, 16, 25);

        cout << "Line 6: myClock: ";
        myClock.printTime();
        cout << endl;

        cout << "Line 9: yourClock: ";
        yourClock.printTime();
        cout << endl;

        cout << "Line 12: tempClock: ";
        tempClock.printTime();
        cout << endl;

                //Compare myClock and yourClock
        if (myClock == yourClock) {
                cout << "Line 16: The time of myClock and "
                     << "yourClock are equal." << endl;
        }
        else
                cout << "Line 18: The time of myClock and "
                     << "yourClock are not equal." << endl;

                //Compare myClock and tempClock
        if (myClock == tempClock)
                cout << "Line 20: The time of myClock and "
                     << "tempClock are equal." << endl;
        else
                cout << "Line 22: The time of myClock and "
                     << "tempClock are not equal." << endl;

        return 0;
}//end main
```

### Sample Run:

```
Line 6: myClock: 08:23:50
Line 9: yourClock: 08:23:50
Line 12: tempClock: 09:16:25
Line 16: The time of myClock and yourClock are equal.
Line 22: The time of myClock and tempClock are not equal.
```

The sample run is easy to follow. However, note that the statement in Line 15 uses the operator `==` to compare the time of myClock and yourClock. Similarly, the statement in Line 19 uses the operator `==` to compare the time of myClock and tempClock. The output of statements in Lines 16 and 22 show that the operator `==` is successfully overloaded for the class `clockType`.

Before discussing operator overloading in general, in the next two sections we discuss two important concepts related to operator overloading.

### Pointer `this`

A member function of a class can (indirectly) access the member variables of a given object of that class. Sometimes, it is necessary for a member function to refer to the object as a whole, rather than the object's individual member variables. How do you refer to the object as a whole (that is, as a single unit) in the definition of the member function, especially when the object is not passed as a parameter? Every object of a class maintains a (hidden) pointer to itself, and the name of this pointer is `this`. In C++, `this` is a reserved word. The pointer `this` (in a member function) is available for you to use. When an object invokes a member function, the member function references the pointer `this` of the object. For example, suppose that `test` is a class and has a member function called `one`. Further suppose that the definition of one looks like the following:

```cpp
test test::one()
{
    .
    .
    .
    return *this;
}
```

If x and y are objects of type test, then the statement:

```cpp
y = x.one();
```

copies the value of object x into object y. That is, the member variables of x are copied into the corresponding member variables of y. When object x invokes function one, the pointer `this` in the definition of member function one refers to object x, so `this` means the address of x and `*this` means the contents of x. On the other hand, in the statement

```cpp
x = y.one();
```

the pointer `this` in the definition of member function one refers to object y, and so `this` means the address of y and `*this` means the contents of y. So the statement copies the contents of object y into object x.

The following example illustrates how the pointer `this` works.

## EXAMPLE 13-2

In Chapter 11, we defined the `class` rectangleType. We will add a function to this class to illustrate how the pointer `this` works. We do not give the complete definition of this class. We only show the function that uses the pointer `this` to return the whole object. The complete definition can be found at the Web site accompanying this book.

```cpp
class rectangleType
{
public:
    //The functions setDimension, getLength, getWidth, area,
    //perimeter, print, and the constructors are the same as before.

    rectangleType doubleDimensions();
    //Postcondition: length = 2 * length;
    //              width = 2 * width;

private:
    double length;
    double width;
};
```

Suppose that the definition of the member function `doubleDimensions` is:

```cpp
rectangleType rectangleType::doubleDimensions()
{
    length = 2 * length;
    width = 2 * width;

    return *this;
}
```

The function `doubleDimensions` doubles both the length and width of the object and uses the pointer `this` to return the value of the entire object.

Consider the following function main:

```cpp
//Chapter 13: this pointer illustration

#include <iostream>                              //Line 1
#include <iomanip>                               //Line 2
#include "rectangleType.h"                       //Line 3

using namespace std;                             //Line 4

int main()                                       //Line 5
{                                                //Line 6
    rectangleType oldYard(20.00, 10.00);         //Line 7
    rectangleType newYard;                       //Line 8

    cout << fixed << showpoint << setprecision(2); //Line 9
```
