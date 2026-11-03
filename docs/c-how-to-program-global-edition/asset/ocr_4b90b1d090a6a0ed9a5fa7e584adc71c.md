*object or a reference to a class object).* A non-member operator function is often declared as friend of a class for performance reasons.

# ### Binary Overloaded Operators as Member Functions

Consider using `<` to compare two objects of a `String` class that you define. When overloading binary operator `<` as a non-static member function of a `String` class, if `y` and `z` are `String`-class objects, then `y < z` is treated as if `y.operator<(z)` had been written, invoking the `operator<` member function with one argument declared below:

```
```cpp
class String
{
public:
   bool operator<( const String & ) const;
   ...
}; // end class String
```
```

Overloaded operator functions for binary operators can be member functions *only when the left operand is an object of the class in which the function is a member*.

# ### Binary Overloaded Operators as Non-Member Functions

As a non-member function, binary operator `<` *must take two arguments—one of which must be an object* (or a reference to an object) of the class that the overloaded operator is associated with. If `y` and `z` are `String`-class objects or references to `String`-class objects, then `y < z` is treated as if the call `operator<(y, z)` had been written in the program, invoking function `operator<` which is declared as follows:

```
```cpp
bool operator<( const String &, const String & );
```
```

# ## 18.5 Overloading the Binary Stream Insertion and Stream Extraction Operators

You can input and output fundamental-type data using the stream extraction operator `>>` and the stream insertion operator `<<`. The C++ class libraries overload these binary operators for each fundamental type, including pointers and `char *` strings. You can also overload these operators to perform input and output for your own types. The program of Figs. 18.3–18.5 overloads these operators to input and output `PhoneNumber` objects in the format "(000) 000-0000." The program assumes telephone numbers are input correctly.

```
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
```

**Fig. 18.3** | PhoneNumber class with overloaded stream insertion and stream extraction operators as friend functions. (Part 1 of 2.)