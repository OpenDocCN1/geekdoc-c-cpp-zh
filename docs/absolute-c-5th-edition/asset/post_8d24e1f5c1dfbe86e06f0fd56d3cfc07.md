
# CHAPTER 8 Operator Overloading, Friends, and References

## Display 8.2 Overloading Operators as Members (part 2 of 2)

```cpp
private:
    int dollars; //A negative amount is represented as negative
    //dollars and
    int cents; //negative cents. Negative $4.50 is represented as
    //-4 and -50.

    int dollarsPart(double amount) const;
    int centsPart(double amount) const;
    int round(double number) const;

int main() {
    //If the main function is the same as in Display 8.1, then the screen dialogue
    // will be the same as shown in Display 8.1.

    const Money::operator+(const Money& operand) const {
        int allC1 = cents + dollars * 100;
        int allC2 = operand.cents + operand.dollars * 100;
        int sumAllCents = allC1 + allC2;
        int absAllCents = abs(sumAllCents);//Money can be negative.
        int finalDollars = absAllCents / 100;
        int finalCents = absAllCents % 100;
        if (sumAllCents < 0) {
            finalDollars = -finalDollars;
            finalCents = -finalCents;
        }
    }

const Money::operator-(const Money& operand) const {
    //The rest of this definition is Self-Test Exercise 5.
}

bool Money::operator=(const Money& operand) const {
    return ((dollars == operand.dollars)
        && (cents == operand.cents));
}

const Money::operator() const {
    return Money(-dollars, -cents);
}

    //Definitions of all other member functions are the same as in Display 8.1.
```

# TIP: A Class Has Access to All Its Objects

When defining a member function or operator, you may access any private member variable (or function) of the calling object. However, you are allowed even more than that. You may access any private member variable (private member function) of any object of the class being defined.
For example, consider the following few lines that begin in the definition of the plus operator for the class Money in Display 8.2:

```cpp
const Money::operator +(const Money& secondOperand) const {
    int allCents1 = cents + dollars*100;
    int allCents2 = secondOperand.cents + secondOperand.dollars
                               * 100;
}
```

In this case, the plus operator is being defined as a member operator, and the variables cents and dollars, in the first line of the function body, the member variables of the calling object (which happens to be the first operand). However, it is legal to access by name the member variables of the object secondOperand, as in the following line:

```cpp
int allCents2 = secondOperand.cents + secondOperand.dollars * 100;
```

This is because secondOperand is an object of the class Money and this line is in the definition of a member operator for the class Money. Many novice programmers mistakenly think they have direct access to the private members of the class object and do not realize that they have access to all objects of the class being defined.

# Self-Test Exercise

- 5. Complete the definition of the member binary operator in Display 8.2.

# Overloading Function Application ( )

The function call operator () must be overloaded as a member function. It allows you to use an object of the class as if it were function. If AClass has overloaded the function application to have one argument of type int anObject is an object of AClass, then anObject (42) invokes the overloaded function call operator () with calling object anObject and argument 42. The type returned may be void or any other type.

The function call operator () is unusual in that it allows any number of arguments. So, you can define several overloaded versions of the function call operator ().

## PITFALL: Overloading &&, ||, and the Comma Operator

The predefined versions of && and || work for the type bool short-circuit evaluation. However, when overloaded these operators perform complete evaluation. This is so contrary to most programmers expect that it inevitably causes problems. It is best to just not overload these two operators.

The comma operator also presents problems. In its normal use the comma operator guarantees left-to-right evaluations. When overloaded no such guarantee is given. The comma operator is another operator it is safest to avoid overloading.

# 8.2 Friend Functions and Automatic Type Conversion

Trust your friends.

Common advice

Friend functions are nonmember functions that have all the privileges of member functions. Before we discuss friend functions in any detail, we discuss automatic type conversion via constructors, since that helps to explain one of the advantages of overloading operators (or any functions) as friend functions.

# Constructors for Automatic Type Conversion

If your class definition contains the appropriate constructors, the system will perform certain type conversions automatically. For example, if your program contains the definition of the class Money either given in Display 8.1 or as given in Display 8.2, you could use the following in your program:

```cpp
Money baseAmount(100, 60), fullAmount;
fullAmount = baseAmount + 25;
fullAmount.output( );
```

The output would be

```
$125.60
```

The previous code may look simple and natural enough, but there is one subtle point. The 25 (in the expression baseAmount + 25) is not of the appropriate type. In Display 8.1 we only overloaded the operator + so that it could be used with two values of Money. We did not overload + so that it could be used with a value of Money and an integer. The constant 25 can be considered to be of int, but 25 cannot be used as a value of Money unless the class definition somehow tells the system to convert an integer to a value of Money. The only way that system knows that 25 is that we included a constructor that takes a single argument of type int. When the system sees the expression

```cpp
baseAmount + 25
```

it first checks if the operator + has been overloaded for the combination of a value of Money and an integer. Since there is no such overloading, the system next looks to see if there is a constructor that takes a single argument that is an integer. If it finds a constructor that takes a single argument, it uses constructor to convert 25 to a value of Money. The one-argument constructor says that 25 should be converted to an object of Money that represents $25.00.

Note that this type conversion will not work unless there is a suitable constructor. If the class does not contain a constructor with one parameter of type int (or some other type, such as long or double), the expression

```cpp
baseAmount + 25
```

would produce an error. Automatic type conversions (produced by constructors) seem most common and compelling over numeric operators as + and -. However, these automatic conversions apply exactly the same way to arguments of ordinary functions, arguments of member functions, and arguments of overloaded operators.

# PITFALL: Member Operators and Automatic Type Conversion

![](img/f4b6fcd28ec32a6e3350e284d.png)

When you overload a binary operator as a member, the two arguments are no longer symmetric. One is a calling object, and the second "argument" is a true argument. This is not only aesthetic but also has a practical shortcoming. Any type conversion will apply only to the second argument. So, for example, as noted in the previous section, the following would be:

```cpp
Money baseAmount(100, 60), fullAmount;
fullAmount = baseAmount + 25;
```

```cpp
fullAmount = 25 + baseAmount;
```

because 25 cannot be a calling object. Conversion of int values to type Money works for arguments but not for calling objects.

## PITFALL: (continued)

On the other hand, if you overload + as a nonmember (as in Display 8.1), then the following is perfectly legal:

```cpp
fullAmount = 25 + baseAmount;
```

This is the biggest advantage of overloading an operator as a nonmember. Overloading an operator as a nonmember gives you automatic type conversion of all arguments. Overloading an operator as a member gives you the efficiency of bypassing accessor and mutator functions and directly accessing member variables. There is a way to overload an operator (and certain functions) that offers both of these advantages. It called overloading as a friend function and is our next topic.

# Friend Functions

If your class has a set of accessor and mutator functions, you can use the accessor and mutator functions to define nonmember overloaded operators (as in Display 8.2). However, although this may give you access to the member variables, it may not give you efficient access to them. Look again at the definition of the overloaded addition operator + in Display 8.1. Rather than just four member variables, it must incur the overhead of two invocations of getCounts and getDollars. This adds a bit of inefficiency and can also make the code harder to understand. The alternative of overloading as a member gets around this problem at the price of losing automatic type conversion of the first operator. Overloading + as a friend will allow you to directly access member variables and have automatic type conversion for all operations.

A friend function of a class is not a member function of the class, but it has access to the private members of that class (to both private member variables and member functions) just as a friend in the class definition. To make a function a friend function, you must name it as a friend in the class definition. For example, in Display 8.3 we have rewritten the definition of the class Money yet another time. We have overloaded the operators as friends. You may declare an operator or function as a friend of a class by listing the operator or function declaration in the definition of the class and placing the keyword friend in front of the operator or function declaration.

A friend will list the declaration of a member function, except that you would precede the declaration by the keyword friend, just as you would the declaration of a member function. However, a friend is not a member function; rather, it is an ordinary function with extraordinary access to the data members of the class. The friend is defined exactly like the ordinary function it is. In particular, the operator definitions shown in Display 8.3 do not include the qualifier Money:: in the function heading. Also, do not use the keyword friend in the function definition (only in the function declaration). The friend operators in Display 8.3 are invoked just like the nonfriend, nonmember operators in Display 8.1, and have automatic type conversion of all arguments just like the nonfriend, nonmember operators in Display 8.1.
