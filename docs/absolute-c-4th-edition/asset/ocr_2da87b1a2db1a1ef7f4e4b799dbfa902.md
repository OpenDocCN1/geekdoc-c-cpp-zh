# 8.2 Friend Functions and Automatic Type Conversion

*Trust your friends.*

Common advice

Friend functions are nonmember functions that have all the privileges of member functions. Before we discuss friend functions in any detail, we discuss automatic type conversion via constructors, since that helps to explain one of the advantages of overloading operators (or any functions) as friend functions.

# CONSTRUCTORS FOR AUTOMATIC TYPE CONVERSION

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