
### Operators That Cannot Be Overloaded

Most of C++'s operators can be overloaded. Figure 18.2 shows the operators that cannot be overloaded.¹

| Operators that cannot be overloaded | | | |
|---|---|---|---|
| . | .* (pointer to member) | :: | ?: |

**Fig. 18.2** | Operators that cannot be overloaded.

1. Although it’s possible to overload the address (&), comma (,), && and || operators, you should avoid doing so to avoid subtle errors. For insights on this, see CERT guideline DCL10-CPP.

### Rules and Restrictions on Operator Overloading

As you prepare to overload operators for your own classes, there are several rules and restrictions you should keep in mind:

- The *precedence* of an operator *cannot* be changed by overloading. However, parentheses can be used to force the order of evaluation of overloaded operators in an expression.
- The *associativity* of an operator *cannot* be changed by overloading—if an operator normally associates from left to right, then so do all of its overloaded versions.
- You *cannot change the “arity” of an operator* (that is, the number of operands an operator takes)—overloaded unary operators remain unary operators; overloaded binary operators remain binary operators. Operators &, *, + and - all have both unary and binary versions; these unary and binary versions can be separately overloaded.
- You *cannot create new operators*; only existing operators can be overloaded.
- The meaning of how an operator works on values of fundamental types *cannot* be changed by operator overloading. For example, you cannot make the + operator subtract two ints. Operator overloading works only with *objects of user-defined types* or with a *mixture of an object of a user-defined type and an object of a fundamental type*.
- Related operators, like + and +=, *must* be overloaded separately.
- When overloading (), [], -> or any of the assignment operators, the operator overloading function *must* be declared as a class member. For all other overloadable operators, the operator overloading functions can be member functions or non-member functions.

> > **Software Engineering Observation 18.1**
> > *Overload operators for class types so they work as closely as possible to the way built-in operators work on fundamental types.*

## 18.4 Overloading Binary Operators

*A binary operator can be overloaded as a non-static member function with one parameter or as a non-member function with two parameters (one of those parameters must be either a class object or a reference to a class object).* A non-member operator function is often declared as friend of a class for performance reasons.

### Binary Overloaded Operators as Member Functions

Consider using `<` to compare two objects of a `String` class that you define. When overloading binary operator `<` as a non-static member function of a `String` class, if `y` and `z` are `String`-class objects, then `y < z` is treated as if `y.operator<(z)` had been written, invoking the `operator<` member function with one argument declared below:

```cpp
class String
{
public:
   bool operator<( const String & ) const;
   ...
}; // end class String
```

Overloaded operator functions for binary operators can be member functions *only when the left operand is an object of the class in which the function is a member*.

### Binary Overloaded Operators as Non-Member Functions

As a non-member function, binary operator `<` *must take two arguments—one of which must be an object* (or a reference to an object) of the class that the overloaded operator is associated with. If `y` and `z` are `String`-class objects or references to `String`-class objects, then `y < z` is treated as if the call `operator<(y, z)` had been written in the program, invoking function `operator<` which is declared as follows:

```cpp
bool operator<( const String &, const String & );
```

## 18.5 Overloading the Binary Stream Insertion and Stream Extraction Operators

You can input and output fundamental-type data using the stream extraction operator `>>` and the stream insertion operator `<<`. The C++ class libraries overload these binary operators for each fundamental type, including pointers and `char *` strings. You can also overload these operators to perform input and output for your own types. The program of Figs. 18.3–18.5 overloads these operators to input and output `PhoneNumber` objects in the format "(000) 000-0000." The program assumes telephone numbers are input correctly.

```cpp
// Fig. 18.3: PhoneNumber.h
// PhoneNumber class definition
#ifndef PHONENUMBER_H
#define PHONENUMBER_H

#include <iostream>
#include <string>

class PhoneNumber
{
```

**Fig. 18.3** | PhoneNumber class with overloaded stream insertion and stream extraction operators as friend functions. (Part 1 of 2.)

```cpp
11        friend std::ostream &operator<<( std::ostream &, const PhoneNumber & );
12        friend std::istream &operator>>( std::istream &, PhoneNumber & );
13    private:
14        std::string areaCode; // 3-digit area code
15        std::string exchange; // 3-digit exchange
16        std::string line; // 4-digit line
17    }; // end class PhoneNumber
18
19 #endif
```

**Fig. 18.3 |** PhoneNumber class with overloaded stream insertion and stream extraction operators as friend functions. (Part 2 of 2.)

```cpp
1 // Fig. 18.4: PhoneNumber.cpp
2 // Overloaded stream insertion and stream extraction operators
3 // for class PhoneNumber.
4 #include <iostream>
5 #include "PhoneNumber.h"
6 using namespace std;
7
8 // overloaded stream insertion operator; cannot be
9 // a member function if we would like to invoke it with
10 // cout << somePhoneNumber;
11 ostream &operator<<( ostream &output, const PhoneNumber &number )
12 {
13     output << "(" << number.areaCode << ") "
14         << number.exchange << "-" << number.line;
15     return output; // enables cout << a << b << c;
16 } // end function operator<<
17
18 // overloaded stream extraction operator; cannot be
19 // a member function if we would like to invoke it with
20 // cin >> somePhoneNumber;
21 istream &operator>>( istream &input, PhoneNumber &number )
22 {
23     input.ignore(); // skip (
24     input >> setw( 3 ) >> number.areaCode; // input area code
25     input.ignore( 2 ); // skip ) and space
26     input >> setw( 3 ) >> number.exchange; // input exchange
27     input.ignore(); // skip dash (-)
28     input >> setw( 4 ) >> number.line; // input line
29     return input; // enables cin >> a >> b >> c;
30 } // end function operator>>
```

**Fig. 18.4 |** Overloaded stream insertion and stream extraction operators for class PhoneNumber.

```cpp
1 // Fig. 18.5: fig18_05.cpp
2 // Demonstrating class PhoneNumber's overloaded stream insertion
3 // and stream extraction operators.
4 #include <iostream>
```

**Fig. 18.5 |** Overloaded stream insertion and stream extraction operators. (Part 1 of 2.)

```cpp
 5  #include "PhoneNumber.h"
 6  using namespace std;
 7
 8  int main()
 9  {
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
23  } // end main
```

```
Enter phone number in the form (123) 456-7890:
(800) 555-1212
The phone number entered was: (800) 555-1212
```

**Fig. 18.5** | Overloaded stream insertion and stream extraction operators. (Part 2 of 2.)

### Overloading the Stream Extraction (>>) Operator

The stream extraction operator function `operator>>` (Fig. 18.4, lines 21–30) takes the `istream` reference `input` and the `PhoneNumber` reference `number` as arguments and returns an `istream` reference. Operator function `operator>>` inputs phone numbers of the form

`(800) 555-1212`

into objects of class `PhoneNumber`. When the compiler sees the expression

`cin >> phone`

in line 16 of Fig. 18.5, the compiler generates the non-member function call

`operator>>( cin, phone );`

When this call executes, reference parameter `input` (Fig. 18.4, line 21) becomes an alias for `cin` and reference parameter `number` becomes an alias for `phone`. The operator function reads as strings the three parts of the telephone number into the `areaCode` (line 24), `exchange` (line 26) and `line` (line 28) members of the `PhoneNumber` object referenced by parameter `number`. Stream manipulator `setw` limits the number of characters read into each string. When used with `cin` and strings, `setw` restricts the number of characters read to the number of characters specified by its argument (i.e., `setw(3)` allows three characters to be read). The parentheses, space and dash characters are skipped by calling `istream` member function `ignore` (Fig. 18.4, lines 23, 25 and 27), which discards the specified number of characters in the input stream (one character by default). Function `operator>>` returns `istream` reference `input` (i.e., `cin`). This enables input operations on `PhoneNumber` objects
