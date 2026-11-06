
## Outline

- 11.1 Introduction
- 11.2 Fundamentals of Operator Overloading
- 11.3 Restrictions on Operator Overloading
- 11.4 Operator Functions as Class Members vs. Global Functions
- 11.5 Overloading Stream Insertion and Stream Extraction Operators
- 11.6 Overloading Unary Operators
- 11.7 Overloading Binary Operators
- 11.8 Dynamic Memory Management
- 11.9 Case Study: Array Class
- 11.10 Converting between Types
- 11.11 Building a String Class
- 11.12 Overloading ++ and --
- 11.13 Case Study: A Date Class
- 11.14 Standard Library Class string
- 11.15 explicit Constructors
- 11.16 Proxy Classes
- 11.17 Wrap-Up

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

## 11.1 Introduction

Chapters 9–10 introduced the basics of C++ classes. Services were obtained from objects by sending messages (in the form of member-function calls) to the objects. This function call notation is cumbersome for certain kinds of classes (such as mathematical classes). Also, many common manipulations are performed with operators (e.g., input and output). We can use C++'s rich set of built-in operators to specify common object manipulations. This chapter shows how to enable C++'s operators to work with objects—a process called operator overloading.

One example of an overloaded operator built into C++ is <<, which is used both as the stream insertion operator and as the bitwise left-shift operator (which is discussed in Chapter 21, Bits, Characters, Strings and structs). Similarly, >> is also overloaded; it's used both as the stream extraction operator and as the bitwise right-shift operator. Both of these operators are overloaded in the C++ Standard Library.

Although operator overloading sounds like an exotic capability, most programmers implicitly use overloaded operators. For example, the C++ language overloads the addition operator (+) and the subtraction operator (-). These operators perform differently, depending on their context in integer, floating-point and pointer arithmetic.

C++ enables you to overload most operators to be sensitive to the context in which they're used—the compiler generates the appropriate code based on the context (in particular, the types of the operands). Some operators are overloaded frequently, especially the assignment, relational and various arithmetic operators such as + and -. The jobs performed by overloaded operators can also be performed by explicit function calls, but operator notation is often clearer and more familiar to programmers.

We discuss when to, and when not to, use operator overloading. We create classes PhoneNumber, Array and Date to demonstrate how to overload operators, including the stream insertion, stream extraction, assignment, equality, relational, subscript, logical negation and increment operators. We demonstrate C++'s Standard Library class string, which provides many overloaded operators. In the exercises, we ask you to implement several classes with overloaded operators. The exercises also use classes Complex (for complex numbers) and HugeInt (for integers larger than a computer can represent with type long) to demonstrate overloaded arithmetic operators + and -, and ask you to enhance those

### Creating New Operators

It isn’t possible to create new operators; only existing operators can be overloaded. Unfortunately, this prevents you from using popular notations like the ** operator used in some other programming languages for exponentiation. [Note: You could overload an existing operator to perform exponentiation.]

![](img/023f159fdd47d944d48e08843cea732d_506_0.png)

> **Common Programming Error 11.2**
> 
> *Attempting to create new operators via operator overloading is a syntax error.*

### Operators for Fundamental Types

The meaning of how an operator works on objects of fundamental types cannot be changed by operator overloading. You cannot, for example, change the meaning of how + adds two integers. Operator overloading works only with objects of user-defined types or with a mixture of an object of a user-defined type and an object of a fundamental type.

![](img/023f159fdd47d944d48e08843cea732d_506_1.png)

> **Software Engineering Observation 11.2**
> 
> *At least one argument of an operator function must be an object or reference of a user-defined type. This prevents you from changing how operators work on fundamental types.*

![](img/023f159fdd47d944d48e08843cea732d_506_2.png)

> **Common Programming Error 11.3**
> 
> *Attempting to modify how an operator works with objects of fundamental types is a compilation error.*

### Related Operators

Overloading an assignment operator and an addition operator to allow statements like

```
object2 = object2 + object1;
```

does not imply that the += operator is also overloaded to allow statements such as

```
object2 += object1;
```

Such behavior can be achieved only by explicitly overloading operator += for that class.

![](img/023f159fdd47d944d48e08843cea732d_506_3.png)

> **Common Programming Error 11.4**
> 
> *Assuming that overloading an operator such as + overloads related operators such as += or that overloading == overloads a related operator like != can lead to errors. Operators can be overloaded only explicitly; there is no implicit overloading.*

## 11.4 Operator Functions as Class Members vs. Global Functions

Operator functions can be member functions or global functions; global functions are often made friends for performance reasons. Member functions use the this pointer implicitly to obtain one of their class object arguments (the left operand for binary operators). Arguments for both operands of a binary operator must be explicitly listed in a global function call.

### Operators That Must Be Overloaded as Member Functions

When overloading (), [], -> or any of the assignment operators, the operator overloading function must be declared as a class member. For the other operators, the operator overloading functions can be class members or standalone functions.

### Operators as Member Functions and Global Functions

Whether an operator function is implemented as a member function or as a global function, the operator is still used the same way in expressions. So which is best?

When an operator function is implemented as a member function, the leftmost (or only) operand must be an object (or a reference to an object) of the operator’s class. If the left operand must be an object of a different class or a fundamental type, this operator function must be implemented as a global function (as we’ll do in Section 11.5 when overloading << and >> as the stream insertion and stream extraction operators, respectively). A global operator function can be made a friend of a class if that function must access private or protected members of that class directly.

Operator member functions of a specific class are called (implicitly by the compiler) only when the left operand of a binary operator is specifically an object of that class, or when the single operand of a unary operator is an object of that class.

### Why Overloaded Stream Insertion and Stream Extraction Operators Are Overloaded as Global Functions

The overloaded stream insertion operator (<<) is used in an expression in which the left operand has type ostream &, as in cout << classObject. To use the operator in this manner where the right operand is an object of a user-defined class, it must be overloaded as a global function. To be a member function, operator << would have to be a member of the ostream class. This is not possible for user-defined classes, since we are not allowed to modify C++ Standard Library classes. Similarly, the overloaded stream extraction operator (>>) is used in an expression in which the left operand has type istream &, as in cin >> classObject, and the right operand is an object of a user-defined class, so it, too, must be a global function. Also, each of these overloaded operator functions may require access to the private data members of the class object being output or input, so these overloaded operator functions can be made friend functions of the class for performance reasons.

![](img/023f159fdd47d944d48e08843cea732d_507_0.png)

### Performance Tip 11.1

It’s possible to overload an operator as a global, non-friend function, but such a function requiring access to a class’s private or protected data would need to use set or get functions provided in that class’s public interface. The overhead of calling these functions could cause poor performance, so these functions can be inlined to improve performance.

### Commutative Operators

Another reason why one might choose a global function to overload an operator is to enable the operator to be commutative. For example, suppose we have an object, number, of type long int, and an object bigInteger1, of class HugeInteger (a class in which integers may be arbitrarily large rather than being limited by the machine word size of the underlying hardware; class HugeInteger is developed in the chapter exercises). The addition operator (+) produces a temporary HugeInteger object as the sum of a HugeInteger and a long int (as in the expression bigInteger1 + number), or as the sum of a long int and a HugeInteger (as in the expression number + bigInteger1). Thus, we require the addition
