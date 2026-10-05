# TIP: A Class Has Access to All Its Objects

When defining a member function or operator, you may access any private member variable (or function) of the calling object. However, you are allowed even more than that. You may access any private member variable (private member function) of any object of the class being defined.
For example, consider the following few lines that begin in the definition of the plus operator for the class Money in Display 8.2:

```
const Money::operator +(const Money& secondOperand) const
    int allCents1 = cents + dollars*100;
    int allCents2 = secondOperand.cents + secondOperand.dollars
                               * 100
```

In this case, the plus operator is being defined as a member operator, and the variables cents and dollars, in the first line of the function body, the member variables of the calling object (which happens to be the first operand). However, it is legal to access by name the member variables of the object secondOperand, as in the following line:

```
int allCents2 = secondOperand.cents + secondOperand.dollars * 100;
```

This is because secondOperand is an object of the class Money and this line is in the definition of a member operator for the class Money. Many novice programmers mistakenly think they have direct access to the private members of the class object and do not realize that they have access to all objects of the class being defined.

# Self-Test Exercise

+   5. Complete the definition of the member binary operator in Display 8.2.

# Overloading Function Application ( )

The function call operator () must be overloaded as a member function. It allows you to use an object of the class as if it were function. If AClass has overloaded the function application to have one argument of type int anObject is an object of AClass, then anObject (42) invokes the overloaded function call operator () with calling object anObject and argument 42. The type returned may be void or any other type.

The function call operator () is unusual in that it allows any number of arguments. So, you can define several overloaded versions of the function call operator ().