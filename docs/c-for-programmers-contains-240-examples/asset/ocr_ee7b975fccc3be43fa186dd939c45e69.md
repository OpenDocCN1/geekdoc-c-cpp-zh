We discuss when to, and when not to, use operator overloading. We implement user-defined classes PhoneNumber, Array, String and Date to demonstrate how to overload operators, including the stream insertion, stream extraction, assignment, equality, relational, subscript, logical negation, parentheses and increment operators. The chapter ends with an example of C++’s Standard Library class string, which provides many overloaded operators that are similar to our String class that we present earlier in the chapter.

# 11.2 Fundamentals of Operator Overloading

C++ programming is a type-sensitive and type-focused process. Programmers can use fundamental types and can define new types. The fundamental types can be used with C++’s rich collection of operators. Operators provide programmers with a concise notation for expressing manipulations of data of fundamental types.

Programmers can use operators with user-defined types as well. Although C++ does not allow new operators to be created, it does allow most existing operators to be overloaded so that, when these operators are used with objects, the operators have meaning appropriate to those objects. This is a powerful capability.

# Software Engineering Observation 11.1

> Operator overloading contributes to C++’s extensibility—one of the language’s most appealing attributes.

# Good Programming Practice 11.1

> Use operator overloading when it makes a program clearer than accomplishing the same operations with function calls.

# Good Programming Practice 11.2

> Overloaded operators should mimic the functionality of their built-in counterparts—for example, the + operator should be overloaded to perform addition, not subtraction. Avoid excessive or inconsistent use of operator overloading, as this can make a program cryptic and difficult to read.

An operator is overloaded by writing a non-static member function definition or global function definition as you normally would, except that the function name now becomes the keyword operator followed by the symbol for the operator being overloaded. For example, the function name operator+ would be used to overload the addition operator (+). When operators are overloaded as member functions, they must be non-static, because they must be called on an object of the class and operate on that object.

To use an operator on class objects, that operator must be overloaded—with three exceptions. The assignment operator (=) may be used with every class to perform memberwise assignment of the data members of the class—each data member is assigned from the “source” object to the “target” object of the assignment. We’ll soon see that such default memberwise assignment is dangerous for classes with pointer members; we’ll explicitly overload the assignment operator for such classes. The address (&) and comma (,) operators may also be used with objects of any class without overloading. The address operator returns the address of the object in memory. The comma operator evaluates the expression to its left, then the expression to its right. Both of these operators can also be overloaded.