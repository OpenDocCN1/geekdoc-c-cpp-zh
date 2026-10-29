
## Display 8.5 Overloading `<<` and `>>`

```cpp
cout << yourAmount << " + " << myAmount
     << " equals " << ourAmount << endl;

Money diffAmount = yourAmount - myAmount;
cout << yourAmount << " - " << myAmount
     << " equals " << diffAmount << endl;

return 0;
}
```

Definitions of other member functions are as in Display 8.1. Definitions of other overloaded operators are as in Display 8.3.

```cpp
ostream& operator <<(ostream& outputStream, const Money& amount)
{
    int absDollars = abs(amount.dollars);
    int absCents = abs(amount.cents);
    if (amount.dollars < 0 || amount.cents < 0)
        //accounts for dollars == 0 or cents == 0
        outputStream << "$-";
    else
        outputStream << '$';

    outputStream << absDollars;

    if (absCents >= 10)
        outputStream << '.' << absCents;
    else
        outputStream << '.' << '0' << absCents;

    return outputStream;
}
```

```cpp
//Uses iostream and cstdlib:
istream& operator >>(istream& inputStream, Money& amount)
{
    char dollarSign;
    inputStream >> dollarSign; //hopefully
    if (dollarSign != '$')
    {
        cout << "No dollar sign in Money input.\n";
        exit(1);
    }

    double amountAsDouble;
    inputStream >> amountAsDouble;
    amount.dollars = amount.dollarsPart(amountAsDouble);
    amount.cents = amount.centsPart(amountAsDouble);
    return inputStream;
}
```

![](img/9505fd46e120aa9c1406715936ff6251_328_0.png)

Returns a reference

### SAMPLE DIALOGUE

```text
Enter an amount of money: $123.45
Your amount is $123.45
My amount is $10.09.
One of us is richer.
$123.45 + $10.09 equals $133.54
$123.45 - $10.09 equals $113.36
```

## Self-Test Exercises

- 9. In Display 8.5, the definition of the overloaded operator << contains lines like the following:

  `outputStream << "$-";`

  Isn't this circular? Aren't we defining << in terms of <<?

- 10. Why can't we overload << or >> as member operators?

- 11. Below is the definition for a class called Percent. Objects of type Percent represent percentages such as 10% or 99%. Give the definitions of the overloaded operators >> and << so that they can be used for input and output with objects of the class Percent. Assume that input always consists of an integer followed by the character '%', such as 25%. All percentages are whole numbers and are stored in the int member variable named value. You do not need to define the other overloaded operators and do not need to define the constructor. You only have to define the overloaded operators >> and <<.

```cpp
#include <iostream>
using namespace std;
class Percent
{
public:
    friend bool operator ==(const Percent& first,
        const Percent& second);
    friend bool operator <(const Percent& first,
        const Percent& second);
    Percent();
    friend istream& operator >>(istream& inputStream,
                         Percent& aPercent);
    friend ostream& operator <<(ostream& outputStream,
                         const Percent& aPercent);
    //There would normally also be other members and friends.
private:
    int value;
};
```

## OVERLOADING >> AND <<

The input and output operators >> and << can be overloaded just like any other operators. If you want the operators to behave as expected for cin, cout, and file I/O, then the value returned should be of type istream for input and ostream for output, and the value should be returned by reference.

### DECLARATIONS

```cpp
class Class_Name
{
        . . .
public:
        . . .
    friend istream& operator >>(istream& Parameter_1,
                                  Class_Name& Parameter_2);

    friend ostream& operator <<(ostream& Parameter_3,
                                  const Class_Name& Parameter_4);
        . . .
```

The operators do not need to be friends but cannot be members of the class being input or output.

### DEFINITIONS

```cpp
istream& operator >>(istream& Parameter_1,
                              Class_Name& Parameter_2)
{
        . . .
}
ostream& operator <<(ostream& Parameter_3,
    const Class_Name& Parameter_4)
{
    ...
}
```

If you have enough accessor and mutator functions, you can overload >> and << as nonfriend functions. However, it is natural and more efficient to define them as friends.

### What Mode of Returned Value to Use

A function can return a value of type T in four different ways:

- By plain old value, as in the function declaration T f();
- By constant value, as in the function declaration const T f();
- By reference, as in the function declaration T& f();
- By const reference, as in the function declaration const T& f();

There is not unanimous agreement on which to use when. So, do not expect too much consistency in usage. Even when an author or programmer has a clear policy, they seldom manage to follow it without exception. Still, some points are clear.

If you are returning a simple type, like int or char, there is no point in using a const when returning by value or by reference. So programmers typically do not use a const on the return type when it is a simple type. If you want the simple value returned to be allowed as an l-value, that is to be allowed on the left-hand side of an assignment statement, then return by reference; otherwise return the simple type by plain old value. Class types are not so simple. The rest of this discussion applies to returning an object of a class type.

The decision on whether or not to return by reference has to do with whether or not you want to be able to use the returned object as an l-value. If you want to return something that can be used as an l-value, that is, that can be used on the left-hand side of an assignment operator, you must return by reference and so must use an ampersand sign & on the returned type.

Returning a local variable (or other short lived object) by reference, with or without a const, can produce problems and should be avoided.

For class types, the two returned type specifications const T and const T& are very similar. They both mean that you cannot change the returned object by invoking some mutator function directly on the returned object, as in

```cpp
f().mutator();
```

The returned value can still be copied to another variable with an assignment operator and that other variable can have the mutator function applied to it. If you cannot decide between the const T& and const T, use const T (without the ampersand). A const T& is perhaps a bit more efficient than a const T.3 However, the difference is not typically that important and most programmers use const T rather than const T& as a returned type specification. As noted earlier, const T& can sometimes cause problems.

The following summary may be of help. T is assumed to be a class type. Copy constructors are not covered until Chapter 10, but we include details about them here for reference value. If you have not yet read Chapter 10, simply ignore all references to copy constructors.

If a public member function returns a private class member variable, it should always have a const on the returned type, as we explained in the pitfall section of this chapter entitled Returning Member Variables of a Class Type. (One exception to this rule is that programmers normally always return a value of type string by ordinary value, not by const value. This is presumably because the type string is thought of as a simple type like int and char, even though string is a class type.)

The following summary may be of help. T is assumed to be a class type.

- Simple returning by value, as in the function declaration T f();
  Cannot be used as an l-value, and the returned value can be changed directly as in f().mutator(). Calls the copy constructor.
- Returning by constant value, as in const T f();
  This case is the same as the previous case, but the returned value cannot be changed directly as in f().mutator().
- Returning by reference as in T& f();
  Can be used as an l-value, and the returned value can be changed directly as in f().mutator(). Does not call the copy constructor.
- Returning by constant reference, as in const T& f();
  Cannot be used as an l-value, and the returned value cannot be changed directly as in f().mutator(). Does not call the copy constructor.

## THE ASSIGNMENT OPERATOR

If you overload the assignment operator =, you must overload it as a member operator. If you do not overload the assignment operator =, then you automatically get an assignment operator for your class. This default assignment operator copies the values of member variables from one object of the class to the corresponding member variables of another object of the class. For simple classes, that is usually what you want. When we discuss pointers, this default assignment operator will not be what we want, and we will discuss overloading the assignment operator at that point.

3 This is because const T& does not call the copy constructor while const T does call the copy constructor. Copy constructors are discussed in Chapter 10.
