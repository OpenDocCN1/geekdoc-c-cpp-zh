
## Display 8.2  **Overloading Operators as Members (part 2 of 2)**

```
42    if (sumAllCents < 0)
43    {
44        finalDollars = -finalDollars;
45        finalCents = -finalCents;
46    }

47    return Money(finalDollars, finalCents);
48 }

49 const Money Money::operator -(const Money& secondOperand) const
50 {
       // The rest of this definition is self-explanatory.
51 bool Money::operator ==(const Money& secondOperand) const
52 {
53     return ((dollars == secondOperand.dollars)
54             && (cents == secondOperand.cents));
55 }

56 const Money Money::operator -() const
57 {
58     return Money(-dollars, -cents);
59 }

60        <definitions of all other member functions are the same as in Display 8.1>
```

## Tip **A Class Has Access to All Its Objects**

When defining a member function or operator, you may access any private member variable (or function) of the calling object. However, you are allowed even more than that. You may access any private member variable (or private member function) of any object of the class being defined.

For example, consider the following few lines that begin the definition of the plus operator for the class Money in Display 8.2:

```
const Money Money::operator +(const Money& secondOperand) const
{
    int allCents1 = cents + dollars*100;
    int allCents2 = secondOperand.cents + secondOperand.dollars*100;
```

In this case, the plus operator is being defined as a member operator, so the variables cents and dollars, in the first line of the function body, are the member variables of the calling object (which happens to be the first operand). However, it is also legal to access by name the member variables of the object secondOperand, as in the following line:

```
int allCents2 = secondOperand.cents + secondOperand.dollars*100;
```

This is legal because secondOperand is an object of the class Money and this line is in the definition of a member operator for the class Money. Many novice programmers mistakenly think they only have direct access to the private members of the calling object and do not realize that they have direct access to all objects of the class being defined.

## Self-Test Exercises

- 5. Complete the definition of the member binary operator - in Display 8.2.

## Overloading Function Application ( )

The function call operator ( ) must be overloaded as a member function. It allows you to use an object of the class as if it were a function. If class AClass has overloaded the function application operator to have one argument of type int and anObject is an object of AClass, then anObject(42) invokes the overloaded function call operator ( ) with calling object anObject and argument 42. The type returned may be void or any other type.

The function call operator ( ) is unusual in that it allows any number of arguments. So, you can define several overloaded versions of the function call operator ( ).

## Pitfall: OVERLOADING &&, ||, AND THE COMMA OPERATOR

The predefined versions of && and || that work for the type bool use short-circuit evaluation. However, when overloaded these operators perform complete evaluation. This is so contrary to what most programmers expect that it inevitably causes problems. It is best to just not overload these two operators.

The comma operator also presents problems. In its normal use the comma operator guarantees left-to-right evaluations. When overloaded no such guarantee is given. The comma operator is another operator it is safest to avoid overloading.

## 8.2 Friend Functions and Automatic Type Conversion

*Trust your friends.*

Common advice

Friend functions are nonmember functions that have all the privileges of member functions. Before we discuss friend functions in any detail, we discuss automatic type conversion via constructors, since that helps to explain one of the advantages of overloading operators (or any functions) as friend functions.

### CONSTRUCTORS FOR AUTOMATIC TYPE CONVERSION

If your class definition contains the appropriate constructors, the system will perform certain type conversions automatically. For example, if your program contains the definition of the class Money either as given in Display 8.1 or as given in Display 8.2, you could use the following in your program:

```
Money baseAmount(100, 60), fullAmount;
fullAmount = baseAmount + 25;
fullAmount.output();
```

The output would be

$125.60

The code above may look simple and natural enough, but there is one subtle point. The 25 in the expression baseAmount + 25 is not of the appropriate type. In Display 8.1 we only overloaded the operator + so that it could be used with two values of type Money. We did not overload + so that it could be used with a value of type Money and an integer. The constant 25 can be considered to be of type int, but 25 cannot be used as a value of type Money unless the class definition somehow tells the system how to convert an integer to a value of type Money. The only way that the system knows that 25 means $25.00 is that we included a constructor that takes a single argument of type int. When the system sees the expression

```
baseAmount + 25
```

the constructor converts 25 to an object of type Money that represents $25.00. (The definition of the constructor is in Display 8.1.)

Note that this type conversion will not work unless there is a suitable constructor. If the class Money did not contain a constructor with one parameter of type `int` (or of some other number type, such as `long` or `double`), then the expression

```
baseAmount + 25
```

would produce an error message.

These automatic type conversions (produced by constructors) seem most common and compelling with overloaded numeric operators such as + and -. However, these automatic conversions apply in exactly the same way to arguments of ordinary functions, arguments of member functions, and arguments of other overloaded operators.

### Pitfall: MEMBER OPERATORS AND AUTOMATIC TYPE CONVERSION

When you overload a binary operator as a member operator, the two arguments are no longer symmetric. One is a calling object, and only the second "argument" is a true argument. This is not only unaesthetic but also has a very practical shortcoming. Any automatic type conversion will only apply to the second argument. So, for example, as we noted in the previous subsection, the following would be legal:

```
Money baseAmount(100, 60), fullAmount;
fullAmount = baseAmount + 25;
```

This is because Money has a constructor with one argument of type int, and so the value 25 will be considered an int value that is automatically converted to a value of type Money.

However, if you overload + as a member operator (as in Display 8.2), then you cannot reverse the two arguments to +. The following is illegal:

```
fullAmount = 25 + baseAmount;
```

because 25 cannot be a calling object. Conversion of int values to type Money works for arguments but not for calling objects.

On the other hand, if you overload + as a nonmember (as in Display 8.1), then the following is perfectly legal:

```
fullAmount = 25 + baseAmount;
```

This is the biggest advantage of overloading an operator as a nonmember.

Overloading an operator as a nonmember gives you automatic type conversion of all arguments. Overloading an operator as a member gives you the efficiency of bypassing accessor and mutator functions and directly accessing member variables. There is a way to overload an operator (and certain functions) that offers both of these advantages. It is called overloading as a friend function and is our next topic.

### **FRIEND FUNCTIONS**

If your class has a full set of accessor and mutator functions, you can use the accessor and mutator functions to define nonmember overloaded operators (as in Display 8.1 as opposed to Display 8.2). However, although this may give you access to the private member variables, it may not give you efficient access to them. Look again at the definition of the overloaded addition operator + given in Display 8.1. Rather than just reading four member variables, it must incur the overhead of two invocations of getCents and two invocations of getDollars. This adds a bit of inefficiency and also can make the code harder to understand. The alternative of overloading + as a member gets around this problem at the price of losing automatic type conversion of the first operand. Overloading the + operator as a friend will allow us to both directly access member variables and have automatic type conversion for all operands.

A **friend function** of a class is not a member function of the class, but it has access to the private members of that class (both private member variables and private member functions) just as a member function does. To make a function a friend function, you must name it as a friend in the class definition. For example, in Display 8.3 we have rewritten the definition of the class Money yet another time. This time we have overloaded the operators as friends. You make an operator or function a friend of a class by listing the operator or function declaration in the definition of the class and placing the keyword `friend` in front of the operator or function declaration.

A friend operator or friend function has its declaration listed in the class definition, just as you would list the declaration of a member function, except that you precede the declaration by the keyword `friend`. However, a friend is *not* a member function; rather, it really is an ordinary function with extraordinary access to the data members of the class. The friend is defined exactly like the ordinary function it is. In particular, the operator definitions shown in Display 8.3 do not include the qualifier `Money::` in the function heading. Also, you do not use the keyword `friend` in the function definition (only in the function declaration). The friend operators in Display 8.3 are invoked just like the nonfriend, nonmember operators in Display 8.1, and they have automatic type conversion of all arguments just like the nonfriend, nonmember operators in Display 8.1.

The most common kinds of friend functions are overloaded operators. However, any kind of function can be made a friend function.

A function (or overloaded operator) can be a friend of more than one class. To make it a friend of multiple classes, just give the declaration of the friend function in each class for which you want it to be a friend.

Many experts consider friend functions (and operators) to be in some sense not "pure." They feel that in the true spirit of object-oriented programming all operators and functions should be member functions. On the other hand, overloading operators as friends provides the pragmatic advantage of automatic type conversion in all arguments, and since the operator declaration is inside the class definitions, it provides at least a bit more encapsulation than nonmember, nonfriend operators. We have shown you three ways to overload operators: as nonmember nonfriends, as members, and as friends. You can decide for yourself which technique you prefer.
