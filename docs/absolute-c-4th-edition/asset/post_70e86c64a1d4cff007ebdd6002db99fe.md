
```
int dollars1 = amount1.getDollars();
int dollars2 = amount2.getDollars();
int cents1 = amount1.getCents();
int cents2 = amount2.getCents();
return ((dollars1 < dollars2) ||
        ((dollars1 == dollars2) && (cents1 < cents2)));
}
```

3. When overloading an operator, at least one of the arguments to the operator must be of a class type. This prevents changing the behavior of + for integers.

4. If you omit the const at the beginning of the declaration and definition of the overloaded plus operator for the class Money, then the following is legal:

```
(m1 + m2) = m3;
```

If the definition of the class Money is as shown in Display 8.1, so that the plus operator returns by const value, then it is not legal.

## 5. const Money

```
Money::operator -(const Money& secondOperand) const
{
    int allCents1 = cents + dollars*100;
    int allCents2 = secondOperand.cents
                 + secondOperand.dollars*100;
    int diffAllCents = allCents1 - allCents2;
    int absAllCents = abs(diffAllCents);
    int finalDollars = absAllCents/100;
    int finalCents = absAllCents%100;
    if (diffAllCents < 0)
    {
        finalDollars = -finalDollars;
        finalCents = -finalCents;
    }
    return Money(finalDollars, finalCents);
}
```

6. A friend function and a member function are alike in that they both can use any member of the class (either public or private) in their function definition. However, a friend function is defined and used just like an ordinary function; the dot operator is not used when you call a friend function and no type qualifier is used when you define a friend function. A member function, on the other hand, is called using an object name and the dot operator. Also, a member function definition includes a type qualifier consisting of the class name and the scope resolution operator, ::.

```
//Uses stdlib:
const Money operator -(const Money& amount1,
                       const Money& amount2)
{
    int allCents1 = amount1.cents + amount1.dollars*100;
    int allCents2 = amount2.cents + amount2.dollars*100;
    int diffAllCents = allCents1 - allCents2;
    int absAllCents = abs(diffAllCents);

    int finalDollars = absAllCents/100;
    int finalCents = absAllCents%100;

    if (diffAllCents < 0)
    {
        finalDollars = -finalDollars;
        finalCents = -finalCents;
    }

    return Money(finalDollars, finalCents);
}
```

8. Add the following declaration and function definition:

```
friend bool operator <(const Money& amount1,
                       const Money& amount2);

bool operator <(const Money& amount1,
                const Money& amount2)
{
    return ((amount1.dollars < amount2.dollars) ||
            ((amount1.dollars == amount2.dollars) &&
             (amount1.cents < amount2.cents)));
}
```

9. To understand why it is not circular, you need to think about the basic message of over-loading: A single function or operator name can have two or more definitions. That means that two or more different operators (or functions) can share a single name. In the line

```cpp
outputStream << "$";
```

the operator << is the name of an operator defined in the library iostream to be used when the second argument is a quoted string. The operator named << that we define in Display 8.5 is a different operator that works when the second argument is of type Money.

10. If << and >> are to work as we want, then the first operand (first argument) must be cout or cin (or some file I/O stream). But if we want to overload the operators as members of, say, the class Money, then the first operand would have to be the calling object and so would have to be of type Money, and that is not what we want.

```
//Uses istream:
istream& operator >> (istream& inputStream,
                                Percent& aPercent)
{
    char percentSign;
    inputStream >> aPercent.value;
    inputStream >> percentSign; //Discards the % sign.
    return inputStream;
}

//Uses iostream:
ostream& operator <<(ostream& outputStream,
                                const Percent& aPercent)
{
    outputStream << aPercent.value << '%';
    return outputStream;
}
```

12. It is legal, but the meaning is not what you might want. (a++) increases the value of the member variables in a by one, but (a++)++ raises the value of the member variables in a++ by one, and a++ is a different object from a. (It is possible to define the increment operator so that (a++)++ will increase the value of the member variables by two but that requires use of the this pointer which is not discussed until Chapter 10.)

# PROGRAMMING PROJECTS

- 1. Modify the definition of the class Money shown in Display 8.5 so that the following are added:
  
  a. The operators <, <=, >, and >= have each been overloaded to apply to the type Money. *(Hint: See Self-Test Exercise 8.)*
  
  b. The following member function has been added to the class definition. (We show the function declaration as it should appear in the class definition. The definition of the function itself will include the qualifier `Money::`.)

```
const Money percent(int percentFigure) const;
//Returns a percentage of the money amount in the calling object.
//For example, if percentFigure is 10, then the value returned is
//10% of the amount of money represented by the calling object.
```

For example, if purse is an object of type Money whose value represents the amount $100.10, then the call

```
purse.percent(10);
```

returns 10% of $100.10; that is, it returns a value of type Money that represents the amount $10.01.

- 2. Define a class for rational numbers. A rational number is a number that can be represented as the quotient of two integers. For example, 1/2, 3/4, 6/4/2, and so forth are all rational numbers. (By 1/2 and so on we mean the everyday fraction, not the integer division this expression would produce in a C++ program.) Represent rational numbers as two values of type int, one for the numerator and one for the denominator. Call the class Rational. Include a constructor with two arguments that can be used to set the member variables of an object to any legitimate values. Also include a constructor that has only a single parameter of type int; call this single parameter wholeNumber and define the constructor so that the object will be initialized to the rational number wholeNumber/1. Include a default constructor that initializes an object to 0 (that is, to 0/1). Overload the input and output operators >> and <<. Numbers are to be input and output in the form 1/2, 15/32, 300/401, and so forth. Note that the numerator, the denominator, or both may contain a minus sign, so −1/2, 15/−32, and −300/−401 are also possible inputs. Overload all the following operators so that they correctly apply to the type Rational: ==, <, <=, >, >=, +, −, *, and /. Write a test program to test your class. Hints: Two rational numbers a/b and c/d are equal if a*d equals c*b. If b and d are positive rationals, a/b is less than c/d provided a*d is less than c*b. You should include a function to normalize the values stored so that, after normalization, the denominator is positive and the numerator and denominator are as small as possible. For example, after normalization 4/−8 would be represented the same as −1/2.

- 3. Define a class for complex numbers. A complex number is a number of the form
  
  *a + b*i*
  
  where for our purposes, *a* and *b* are numbers of type double, and *i* is a number that represents the quantity √−1. Represent a complex number as two values of type double. Name the member variables real and imaginary. (The variable for the number that is multiplied by *i* is the one called *imaginary*.) Call the class Complex. Include a constructor with two parameters of type double that can be used to set the member variables of an object to any values. Include a constructor that has only a single parameter of type double; call this parameter realPart and define the constructor so that the object will be initialized to realPart + 0*i. Include a default constructor that initializes an object to 0 (that is, to 0 + 0*i). Overload all the following operators so that they correctly apply to the type Complex: ==, +, −, *, >>, and <<. You should also write a test program to test your class. Hints: To add or subtract two complex numbers, add or subtract the two member variables of type double. The product of two complex numbers is given by the following formula:

\((a + b*i)*(c + d*i) == (a*c − b*d) + (a*d + b*c)*i\)

In the interface file, you should define a constant i as follows:

```
const Complex i(0, 1);
```

This defined constant i will be the same as the i discussed above.

- 4. (Cumulatively modify the example from Display 8.7 as follows.
