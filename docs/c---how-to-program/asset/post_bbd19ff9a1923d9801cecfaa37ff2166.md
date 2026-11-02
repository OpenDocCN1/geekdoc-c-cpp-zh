
```cpp
friend std::ostream &operator<<( std::ostream &, const PhoneNumber & );
friend std::istream &operator>>( std::istream &, PhoneNumber & );
private:
std::string areaCode; // 3-digit area code
std::string exchange; // 3-digit exchange
std::string line; // 4-digit line
}; // end class PhoneNumber

#endif
```

Fig. 18.3 | PhoneNumber class with overloaded stream insertion and stream extraction operators as friend functions. (Part 2 of 2.)

```cpp
// Fig. 18.4: PhoneNumber.cpp
// Overloaded stream insertion and stream extraction operators
// for class PhoneNumber.
#include <iostream>
#include "PhoneNumber.h"
using namespace std;

// overloaded stream insertion operator; cannot be
// a member function if we would like to invoke it with
// cout << somePhoneNumber;
ostream &operator<<( ostream &output, const PhoneNumber &number )
{
    output << "(" << number.areaCode << ") ";
    output << number.exchange << "-" << number.line;
    return output; // enables cout << a << b << c;
} // end function operator<<

// overloaded stream extraction operator; cannot be
// a member function if we would like to invoke it with
// cin >> somePhoneNumber;
istream &operator>>( istream &input, PhoneNumber &number )
{
    input.ignore(); // skip (
    input >> setw(3) >> number.areaCode; // input area code
    input.ignore(2); // skip ) and space
    input >> setw(3) >> number.exchange; // input exchange
    input.ignore(); // skip dash (-)
    input >> setw(4) >> number.line; // input line
    return input; // enables cin >> a >> b >> c;
} // end function operator>>
```

Fig. 18.4 | Overloaded stream insertion and stream extraction operators for class PhoneNumber.

```cpp
// Fig. 18.5: fig18_05.cpp
// Demonstrating class PhoneNumber's overloaded stream insertion
// and stream extraction operators.
#include <iostream>
```

Fig. 18.5 | Overloaded stream insertion and stream extraction operators. (Part 1 of 2.)

```cpp
5 #include "PhoneNumber.h"
6 using namespace std;
7
8 int main()
9 {
10     PhoneNumber phone; // create object phone
11
12     cout << "Enter phone number in the form (123) 456-7890:" << endl;
13
14     // cin >> phone invokes operator>> by implicitly issuing
15     // the non-member function call operator>>( cin, phone )
16     cin >> phone;
17
18     cout << "The phone number entered was: ";
19
20     // cout << phone invokes operator<< by implicitly issuing
21     // the non-member function call operator<<( cout, phone )
22     cout << phone << endl;
23 } // end main
```

```text
Enter phone number in the form (123) 456-7890:
(800) 555-1212
The phone number entered was: (800) 555-1212
```

Fig. 18.5 | Overloaded stream insertion and stream extraction operators. (Part 2 of 2.)

## Overloading the Stream Extraction (>>) Operator

The stream extraction operator function operator>> (Fig. 18.4, lines 21–30) takes the istream reference input and the PhoneNumber reference number as arguments and returns an istream reference. Operator function operator>> inputs phone numbers of the form

```text
(800) 555-1212
```

into objects of class PhoneNumber. When the compiler sees the expression

```cpp
cin >> phone
```

in line 16 of Fig. 18.5, the compiler generates the non-member function call

```cpp
operator>>( cin, phone );
```

When this call executes, reference parameter input (Fig. 18.4, line 21) becomes an alias for cin and reference parameter number becomes an alias for phone. The operator function reads as strings the three parts of the telephone number into the areaCode (line 24), exchange (line 26) and line (line 28) members of the PhoneNumber object referenced by parameter number. Stream manipulator setw limits the number of characters read into each string. When used with cin and strings, setw limits the number of characters read to the number of characters specified by its argument (i.e., setw(3) allows three characters to be read). The parentheses, space and dash characters are skipped by calling istream member function ignore (Fig. 18.4, lines 23, 25 and 27), which discards the specified number of characters in the input stream (one character by default). Function operator>> returns istream reference input (i.e., cin). This enables input operations on PhoneNumber objects to be cascaded with input operations on other PhoneNumber objects or other data types. For example, a program can input two PhoneNumber objects in one statement as follows:

```cpp
cin >> phone1 >> phone2;
```

First, the expression cin >> phone1 executes by making the non-member function call

```cpp
operator>>( cin, phone1 );
```

This call then returns a reference to cin as the value of cin >> phone1, so the remaining portion of the expression is interpreted simply as cin >> phone2. This executes by making the non-member function call

```cpp
operator>>( cin, phone2 );
```

### Good Programming Practice 18.1

Overloaded operators should mimic the functionality of their built-in counterparts—e.g., the + operator should perform addition, not subtraction. Avoid excessive or inconsistent use of operator overloading, as this can make a program cryptic and difficult to read.

## Overloading the Stream Insertion (<<) Operator

The stream insertion operator function (Fig. 18.4, lines 11–16) takes an ostream reference (output) and a const PhoneNumber reference (number) as arguments and returns an ostream reference. Function operator<< displays objects of type PhoneNumber. When the compiler sees the expression

```cpp
cout << phone
```

in line 22 of Fig. 18.5, the compiler generates the non-member function call

```cpp
operator<<( cout, phone );
```

Function operator<< displays the parts of the telephone number as strings, because they're stored as string objects.

## Overloaded Operators as Non-Member friend Functions

The functions operator>> and operator<< are declared in PhoneNumber as non-member, friend functions (Fig. 18.3, lines 11–12). They're non-member functions because the object of class PhoneNumber must be the operator's right operand. If these were to be PhoneNumber member functions, the following awkward statements would have to be used to output and input a PhoneNumber:

```cpp
phone << cout;
phone >> cin;
```

Such statements would be confusing to most C++ programmers, who are familiar with cout and cin appearing as the left operands of << and >>, respectively.

Overloaded operator functions for binary operators can be member functions only when the left operand is an object of the class in which the function is a member. Overloaded input and output operators are declared as friends if they need to access non-public class members directly or because the class may not offer appropriate get functions. Also, the PhoneNumber reference in function operator<<'s parameter list (Fig. 18.4, line 11) is const, because the PhoneNumber will simply be output, and the PhoneNumber reference in function operator>>'s parameter list (line 21) is non-const, because the PhoneNumber object must be modified to store the input telephone number in the object.

### Software Engineering Observation 18.2

> *New input/output capabilities for user-defined types are added to C++ without modifying standard input/output library classes. This is another example of C++'s extensibility.*

## Why Overloaded Stream Insertion and Stream Extraction Operators Are Overloaded as Non-Member Functions

The overloaded stream insertion operator (<<) is used in an expression in which the left operand has type ostream &, as in cout << classObject. To use the operator in this manner where the right operand is an object of a user-defined class, it must be overloaded as a non-member function. To be a member function, operator << would have to be a member of class ostream. This is not possible for user-defined classes, since we are not allowed to modify C++ Standard Library classes. Similarly, the overloaded stream extraction operator (>>) is used in an expression in which the left operand has the type istream &, as in cin >> classObject, and the right operand is an object of a user-defined class, so it, too, must be a non-member function. Also, each of these overloaded operator functions may require access to the private data members of the class object being output or input, so these overloaded operator functions can be made friend functions of the class for performance reasons.

## 18.6 Overloading Unary Operators

A unary operator for a class can be overloaded as a non-static member function with no arguments or as a non-member function with one argument that must be an object (or a reference to an object) of the class. Member functions that implement overloaded operators must be non-static so that they can access the non-static data in each object of the class.

### Unary Overloaded Operators as Member Functions

Consider overloading unary operator ! to test whether an object of your own String class is empty. Such a function would return a bool result. When a unary operator such as ! is overloaded as a member function with no arguments and the compiler sees the expression !s (in which s is an object of class String), the compiler generates the function call s.operator!( ). The operand s is the String object for which the String class member function operator! is being invoked. The function is declared as follows:

```cpp
class String
{
public:
    bool operator!() const;
    ...;
}; // end class String
```

### Unary Overloaded Operators as Non-Member Functions

A unary operator such as ! may be overloaded as a non-member function with one parameter. If s is a String class object (or a reference to a String class object), then !s is treated as if the call operator!(s) had been written, invoking the non-member operator! function that's declared as follows:

```cpp
bool operator!( const String & );
```
