A function can be overloaded to take arguments of different types. An operator is really a function, so an operator can be overloaded. The way you overload an operator, such as +, is basically the same as the way you overload a function name. In this section we show you how to overload operators in C++.

# Overloading Operators

You can overload the operator + (and many other operators) so that it will accept arguments of a class type. The difference between overloading the + operator and defining the function add (given in Display 11.3) involves only a slight change in syntax. The definition of the overloaded operator + is basically the same as the definition of the function add. The only differences are that you use the name + instead of the name add and you precede the + with the keyword operator. In Display 11.5 we have rewritten the type Money to include the overloaded operator + and we have embedded the definition in a small demonstration program.

The class Money, as defined in Display 11.5, also overloads the == operator so that == can be used to compare two objects of type Money. If amount1 and amount2 are two objects of type Money, we want the expression

```
amount1 == amount2
```

to return the same value as the following Boolean expression:

```
amount1.allCents == amount2.allCents
```

As shown in Display 11.5, this is the value returned by the overloaded operator ==.

You can overload most, but not all, operators. The operator need not be a friend of a class, but you will often want it to be a friend. Check the box entitled “Rules on Overloading Operators” for some technical details on when and how you can overload an operator.

# Operator Overloading

A (binary) operator, such as +, -, /, %, and so forth, is simply a function that is called using a different syntax for listing its arguments. With an operator, the arguments are listed before and after the operator; with a function, the arguments are listed in parentheses after the function name. An operator definition is written similarly to a function definition, except that the operator definition includes the reserved word operator before the operator name. The predefined operators, such as + and so forth, can be overloaded by giving them a new definition for a class type.

An operator may be a friend of a class although this is not required. An example of overloading the + operator as a friend is given in Display 11.5.