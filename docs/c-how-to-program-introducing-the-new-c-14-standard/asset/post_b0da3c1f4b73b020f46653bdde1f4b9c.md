
## Overloaded

Most of C++’s operators can be overloaded. **Figure 10.2** shows the operators that cannot be overloaded.¹

1. Although it’s possible to overload the address (`&`), comma (`,`), `&&` and `[]` operators, you should avoid doing so to avoid subtle errors. For insights on this, see CERT guideline DCL10-CPP.

**Fig. 10.2** Operators that cannot be overloaded.

| Operators that cannot be overloaded | | | |
|---|---|---|---|
| `.` | `.*` (pointer to member) | `::` | `?:` |

### 10.3.4 Rules and Restrictions on Operator Overloading

As you prepare to overload operators for your own classes, there are several rules and restrictions you should keep in mind:

- *An operator’s precedence cannot be changed by overloading.* Parentheses can be used to force the order of evaluation of overloaded operators in an expression.
- *An operator’s associativity cannot be changed by overloading*—if an operator normally associates from left to right, then so do all of its overloaded versions.
- *An operator’s “arity”* (that is, the number of operands an operator takes) *cannot be changed*—overloaded unary operators remain unary operators; overloaded binary operators remain binary operators. C++’s only ternary operator, `?:`, cannot be overloaded. Operators `&`, `*`, `+` and `-` all have both unary and binary versions that can be separately overloaded.
- *Only existing operators can be overloaded*—you cannot create new ones.
- You *cannot* overload operators to change how an operator works on fundamental-type values. For example, you cannot make the `+` operator subtract two `int`s. Operator overloading works only with *objects of user-defined types* or with a mixture of an object of a user-defined type and an object of a fundamental type.
- Related operators, like `+` and `+=`, must be overloaded separately.
- When overloading `()`, `[]`, `->` or any of the assignment operators, the operator overloading function *must* be declared as a class member. For all other overloadable operators, the operator overloading functions can be member functions or non-member functions.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1336_0.png)

### Software Engineering Observation 10.1

Overload operators for class types so they work as closely as possible to the way built-in operators work on fundamental types.

## 10.4 Overloading Binary Operators

A binary operator can be overloaded as a non-`static` member function with one parameter or as a non-member function with two parameters (one of those parameters must be either a class object or a reference to a class object). A non-member operator function often is declared as `friend` of a class for performance reasons.

### Binary Overloaded Operators as Member Functions

Consider using `<` to compare two objects of a `String` class that you define. When overloading binary operator `<` as a non-`static` member function, if `y` and `z` are `String`-class objects, then `y < z` is treated by the compiler as if `y.operator<(z)` had been written, invoking the `operator<` member function with one argument declared below:

```cpp
class String {
public:
  bool operator<(const String&) const;
  // ...
};
```

Overloaded operator functions for binary operators can be member functions *only when the left operand is an object of the class in which the function is a member.*

### Binary Overloaded Operators as Non-Member Functions

As a non-member function, binary operator `<` *must* take *two* arguments—*one* of which *must* be an object (or a reference to an object) of the class that the overloaded operator is associated with. If `y` and `z` are `String`-class objects or references to `String`-class objects, then `y < z` is treated as if the call `operator<(y, z)` had been written in the program, invoking function `operator<`, which is declared as follows:

```cpp
bool operator<(const String&, const String&);
```

## 10.5 Overloading the Binary Stream Insertion and Stream Extraction Operators

You can input and output fundamental-type data using the stream extraction operator `>>` and the stream insertion operator `<<`, respectively. The C++ class libraries overload these binary operators for each fundamental type, including pointers and `char *` strings. You can also overload these operators to perform input and output for your own types. The program of **Figs. 10.3–10.5** overloads these operators to input `PhoneNumber` objects in the format

```text
(555) 555-5555
```

and to output them in the format

```text
Area code: 555
Exchange: 555
Line: 5555
(555) 555-5555
```

The program assumes telephone numbers are input correctly.

```cpp
// Fig. 10.3: PhoneNumber.h
// PhoneNumber class definition
#ifndef PHONENUMBER_H
#define PHONENUMBER_H

#include <iostream>
#include <string>

class PhoneNumber {
    friend std::ostream& operator<<(std::ostream&, const PhoneNumber&);
    friend std::istream& operator>>(std::istream&, PhoneNumber&);
private:
    std::string areaCode; // 3-digit area code
    std::string exchange; // 3-digit exchange
    std::string line;     // 4-digit line
};

#endif
```

**Fig. 10.3** `PhoneNumber` class with overloaded stream insertion and stream extraction operators as `friend` functions.

```cpp
// Fig. 10.4: PhoneNumber.cpp
// Overloaded stream insertion and stream extraction operators
// for class PhoneNumber.
#include <iomanip>
#include "PhoneNumber.h"
using namespace std;

// overloaded stream insertion operator; cannot be a member function
// if we would like to invoke it with cout << somePhoneNumber;
ostream& operator<<(ostream& output, const PhoneNumber& number) {
   output << "Area code: " << number.areaCode << "\nExchange: "
      << number.exchange << "\nLine: " << number.line << "\n"
      << "(" << number.areaCode << ") " << number.exchange << "-"
      << number.line << "\n";
   return output; // enables cout << a << b << c;
}

// overloaded stream extraction operator; cannot be a member function
// if we would like to invoke it with cin >> somePhoneNumber;
istream& operator>>(istream& input, PhoneNumber& number) {
   input.ignore(); // skip (
   input >> setw(3) >> number.areaCode; // input area code
   input.ignore(2); // skip ) and space
   input >> setw(3) >> number.exchange; // input exchange
   input.ignore(); // skip dash (-)
   input >> setw(4) >> number.line; // input line
   return input; // enables cin >> a >> b >> c;
}
```

**Fig. 10.4** Overloaded stream insertion and stream extraction operators for class `PhoneNumber`.

```cpp
// Fig. 10.5: fig10_05.cpp
// Demonstrating class PhoneNumber's overloaded stream insertion
// and stream extraction operators.
#include <iostream>
#include "PhoneNumber.h"
using namespace std;

int main() {
    PhoneNumber phone; // create object phone

    cout << "Enter phone number in the form (555) 555-5555:" << endl;

    // cin >> phone invokes operator>> by implicitly issuing
    // the non-member function call operator>>(cin, phone)
    cin >> phone;

    cout << "\nThe phone number entered was:\n";

    // cout << phone invokes operator<< by implicitly issuing
    // the non-member function call operator<<(cout, phone)
    cout << phone << endl;
}
```

```text
Enter phone number in the form (555) 555-5555:
(800) 555-1212

The phone number entered was:
Area code: 800
Exchange: 555
Line: 1212
(800) 555-1212
```

**Fig. 10.5** Overloaded stream insertion and stream extraction operators.

### Overloading the Stream Extraction (>>) Operator

The stream extraction operator function `operator>>` (Fig. 10.4, lines 20–28) takes the `istream` reference `input` and the `PhoneNumber` reference `number` as arguments and returns an `istream` reference. The function inputs phone numbers of the form `(555) 555-5555` into objects of class `PhoneNumber`. When the compiler sees the expression

```cpp
cin >> phone
```

in line 15 of [Fig. 10.5](#), the compiler generates the *non-member function call*

```cpp
operator>>(cin, phone);
```

When this call executes, reference parameter `input` ([Fig. 10.4](#), line 20) becomes an alias for `cin` and reference parameter `number` becomes an alias for `phone`.

The operator function reads as `strings` the three parts of the telephone number into the `areaCode` (line 22), `exchange` (line 24) and `line` (line 26) data members of the `PhoneNumber` object referenced by parameter `number`—the function is a friend of the class, so it can access a `PhoneNumber`’s `private` members. Stream manipulator `setw` limits the number of characters read into each `string`. *When used with* `cin` *and* `strings`, `setw` *restricts the number of characters read to the number of characters specified by its argument* (i.e., `setw(3)`).
