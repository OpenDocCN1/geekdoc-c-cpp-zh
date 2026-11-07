
## 11.13 explicit Constructors

Any single-argument constructor—except a copy constructor—can be used by the compiler to perform an implicit conversion. The constructor's argument is converted to an object of the class in which the constructor is defined. The conversion is automatic and you need not use a cast operator. In some situations, implicit conversions are undesirable or error-prone. For example, our Array class in Fig. 11.10 defines a constructor that takes a single int argument. The intent of this constructor is to create an Array object containing the number of elements specified by the int argument. However, this constructor can be misused by the compiler to perform an implicit conversion.

![](img/bfd978e7e9b192bab46ec2a89e481263_518_0.png)

> **Common Programming Error 11.6**
>
> *Unfortunately, the compiler might use implicit conversions in cases that you do not expect, resulting in ambiguous expressions that generate compilation errors or result in execution-time logic errors.*

### Accidentally Using a Single-Argument Constructor as a Conversion Constructor

The program (Fig. 11.12) uses the Array class of Figs. 11.10–11.11 to demonstrate an improper implicit conversion.

```cpp
// Fig. 11.12: Fig11_12.cpp
// Driver for simple class Array.
#include <iostream>
#include "Array.h"
using namespace std;

void outputArray( const Array & ); // prototype

int main()
{
   Array integers1( 7 ); // 7-element array
   outputArray( integers1 ); // output Array integers1
   outputArray( 3 ); // convert 3 to an Array and output Array’s contents
} // end main

// print Array contents
void outputArray( const Array &arrayToOutput )
{
   cout << "The Array received has " << arrayToOutput.getSize()
        << " elements. The contents are:\n" << arrayToOutput << endl;
} // end outputArray
```

```text
The Array received has 7 elements. The contents are:
             0             0             0             0
             0             0             0

The Array received has 3 elements. The contents are:
             0             0             0
```

**Fig. 11.12** | Single-argument constructors and implicit conversions.

```cpp
void outputArray( const Array & ); // prototype

int main()
{
   Array integers1( 7 ); // 7-element array
   outputArray( integers1 ); // output Array integers1
   outputArray( 3 ); // convert 3 to an Array and output Array's contents
   outputArray( Array( 3 ) ); // explicit single-argument constructor call
} // end main

// print array contents
void outputArray( const Array &arrayToOutput )
{
   cout << "The Array received has " << arrayToOutput.getSize()
        << " elements. The contents are:\n" << arrayToOutput << endl;
} // end outputArray
```

```text
c:\cpphtp8_examples\ch11\fig11_13\fig11_13.cpp(13) : error C2664:
'outputArray' : cannot convert parameter 1 from 'int' to 'const Array &'
             cannot convert from 'int' to 'Array'
             Constructor for class 'Array' is declared 'explicit'
```

Fig. 11.13 | Demonstrating an explicit constructor. (Part 2 of 2)

## 11.14 Building a String Class

In Section 8.10, we introduced C-style, pointer-based string processing with character arrays. Our discussion of char * strings continues in Section 21.10. As part of our coverage of crafting valuable classes, we implement our own String class that encapsulates a dynamically allocated char * string and provides many capabilities that are similar to those we introduced in the Array class. To implement this class, we use several of the capabilities introduced in Sections 8.10 and 21.10. Because classes Array and String are so similar, we placed our String class's code and discussion online at www.deitel.com/books/cpphtp8/ under Downloads and Resources for Registered Users. The C++ standard library includes the similar, more robust class string, which we demonstrated in Section 11.12 and study in detail in Chapter 18. In this section, we discuss one key feature of our String class.

### Overloaded Function Call Operator

Overloading the function call operator `()` is powerful, because functions can take an arbitrary number of parameters. In our String class, we overload this operator to select a substring from a String. The operator's two integer parameters specify the start location and the length of the substring to be selected. If the start location is out of range or the substring length is negative, the operator simply returns an empty String. If the substring length is 0, then the substring is selected to the end of the String object. Suppose string1 is a String object containing the string "AEIOU". When the compiler encounters the expression `string1( 2, 2 )`, it generates the member-function call

```cpp
string1.operator()( 2, 2 )
```

which returns a String containing "IO".

## 11.15 Wrap-Up

In this chapter, you learned how to overload operators to work with class objects. We demonstrated standard C++ class string, which makes extensive use of overloaded operators to create a robust, reusable class that can replace C-style, pointer-based strings. Next, we discussed several restrictions that the C++ standard places on overloaded operators. We then presented a PhoneNumber class that overloaded operators << and >> to conveniently output and input phone numbers. You also saw a Date class that overloaded the prefix and postfix increment (++) operators and we showed a special syntax that's required to differentiate between the prefix and postfix versions of the increment (++) operator.

Next, we introduced the concept of dynamic memory management. You learned that you can create and destroy objects dynamically with the new and delete operators, respectively. Then, we presented a capstone Array class case study that used overloaded operators and other capabilities to solve various problems with pointer-based arrays. This case study helped you truly understand what classes and object technology are all about—crafting, using and reusing valuable classes. As part of this class, you saw overloaded stream insertion, stream extraction, assignment, equality, relational and subscript operators.

You learned reasons for implementing overloaded operators as member functions or as non-member functions. The chapter concluded with discussions of converting between types (including class types), problems with certain implicit conversions defined by single-argument constructors and how to prevent those problems by using explicit constructors.

In the next chapter, we continue our discussion of classes by introducing a form of software reuse called inheritance. We'll see that when classes share common attributes and behaviors, it's possible to define those attributes and behaviors in a common "base" class and "inherit" those capabilities into new class definitions, enabling you to create the new classes with a minimal amount of code.

## Summary

### Section 11.1.1 Introduction

- C++ enables you to overload most operators to be sensitive to the context in which they're used—the compiler generates the appropriate code based on the types of the operands.
- One example of an overloaded operator built into C++ is operator <<, which is used both as the stream insertion operator and as the bitwise left-shift operator. Similarly, >> is also overloaded; it's used both as the stream extraction operator and as the bitwise right-shift operator. Both of these operators are overloaded in the C++ Standard Library.
- C++ overloads + and - to perform differently, depending on their context in integer arithmetic, floating-point arithmetic and pointer arithmetic.
- The jobs performed by overloaded operators can also be performed by explicit function calls, but operator notation is often more natural.

### Section 11.1.2 Using the Overloaded Operators of Standard Library Class string

- Standard class string is defined in header <string> and belongs to namespace std.
- Class string provides many overloaded operators, including equality, relational, assignment, addition assignment (for concatenation) and subscript operators.
- Class string provides member function empty (p. 455), which returns true if the string is empty; otherwise, it returns false.
