
```cpp
return true;
else
    return false;
}
```

Because the built-in < operator already returns a type bool value, you can simplify the code further to this:

```cpp
bool operator<(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) < 0);
}
```

Similarly, you can code the other two comparison functions like this:

```cpp
bool operator>(const String &st1, const String &st2)
{
    return st2 < st1;
}
bool operator==(const String &st1, const String &st2)
{
    return (std::strcmp(st1.str, st2.str) == 0);
}
```

The first definition expresses the > operator in terms of the < operator and would be a good choice for an inline function.

Making the comparison functions friends facilitates comparisons between String objects and regular C strings. For example, suppose answer is a String object and that you have the following code:

```cpp
if ("love" == answer)
```

This gets translated to the following:

```cpp
if (operator==("love", answer))
```

The compiler then uses one of the constructors to convert the code, in effect, to this:

```cpp
if (operator==(String("love"), answer))
```

And this matches the prototype.

## Accessing Characters by Using Bracket Notation

With a standard C-style string, you can use brackets to access individual characters:

```cpp
char city[40] = "Amsterdam";
cout << city[0] << endl; // display the letter A
```

In C++ the two bracket symbols constitute a single operator, the bracket operator, and you can overload this operator by using a method called operator[](). Typically, a binary C++ operator (one with two operands) puts the operator between the two operands, as in 2 + 5. But the bracket operator places one operand in front of the first bracket and the other operand between the two brackets. Thus, in the expression `city[0]`, city is the first operand, `[]` is the operator, and 0 is the second operand.

Suppose that opera is a string object:

```cpp
String opera("The Magic Flute");
```

If you use the expression `opera[4]`, C++ looks for a method with this name and signature:

```cpp
String::operator[](int i)
```

If it finds a matching prototype, the compiler replaces the expression `opera[4]` with this function call:

```cpp
opera.operator[](4)
```

The opera object invokes the method, and the array subscript 4 becomes the function argument.

Here’s a simple implementation:

```cpp
char & String::operator[](int i)
{
    return str[i];
}
```

With this definition, the statement

```cpp
cout << opera[4];
```

becomes this:

```cpp
cout << opera.operator[](4);
```

The return value is `opera.str[4]`, or the character 'M'. So the public method gives access to private data.

Declaring the return type as type `char &` allows you to assign values to a particular element. For example, you can use the following:

```cpp
String means("might");
means[0] = 'r';
```

The second statement is converted to an overloaded operator function call:

```cpp
means.operator[](0) = 'r';
```

This assigns 'r' to the method’s return value. But the function returns a reference to `means.str[0]`, making the code equivalent to

```cpp
means.str[0] = 'r';
```

This last line of code violates private access, but because `operator[]()` is a class method, it is allowed to alter the array contents. The net effect of the code is that "might" becomes "right".

Suppose you have a constant object:

```cpp
const String answer("futile");
```

Then, if the only available definition for operator[]() is the one you've just seen, the following code is labeled an error:

```cpp
cout << answer[1];  // compile-time error
```

The reason is that answer is const, and the method doesn't promise not to alter data. (In fact, sometimes the method's job is to alter data, so it can't promise not to.)

However, C++ distinguishes between const and non-const function signatures when overloading, so you can provide a second version of operator[]() that is used just by const String objects:

```cpp
// for use with const String objects
const char & String::operator[](int i) const
{
    return str[i];
}
```

With the definitions, you have read/write access to regular String objects and read-only access to const String data:

```cpp
String text("Once upon a time");
const String answer("futile");
cout << text[1];      // ok, uses non-const version of operator[]()
cout << answer[1];    // ok, uses const version of operator[]()
cin >> text[1];       // ok, uses non-const version of operator[]()
cin >> answer[1];     // compile-time error
```

## Static Class Member Functions

It's possible to declare a member function as being static. (The keyword static should appear in the function declaration but not in the function definition if the latter is separate.) This has two important consequences.

First, a static member function doesn't have to be invoked by an object; in fact, it doesn't even get a this pointer to play with. If the static member function is declared in the public section, it can be invoked using the class name and the scope-resolution operator. For instance, you can give the String class a static member function called HowMany() with the following prototype/definition in the class declaration:

```cpp
static int HowMany() { return num_strings; }
```

It could be invoked like this:

```cpp
int count = String::HowMany();   // invoking a static member function
```

The second consequence is that because a static member function is not associated with a particular object, the only data members it can use are the static data members. For example, the `HowMany()` static method can access the `num_strings` static member, but not `str` or `len`.

Similarly, a static member function can be used to set a classwide flag that controls how some aspect of the class interface behaves. For example, it can control the formatting used by a method that displays class contents.

## Further Assignment Operator Overloading

Before looking at the new listings for the String class example, let’s consider another matter. Suppose you want to copy an ordinary string to a String object. For example, suppose you use `getline()` to read a string and you want to place it in a String object. The class methods already allow you to do the following:

```cpp
String name;
char temp[40];
cin.getline(temp, 40);
name = temp;  // use constructor to convert type
```

However, this might not be a satisfactory solution if you have to do it often. To see why, let’s review how the final statement works:

- 1. The program uses the `String(const char *)` constructor to construct a temporary String object containing a copy of the string stored in `temp`. Remember from Chapter 11, “Working with Classes,” that a constructor with a single argument serves as a conversion function.
- 2. In Listing 12.6, later in this chapter, the program uses the `String & String::operator=(const String &)` function to copy information from the temporary object to the name object.
- 3. The program calls the `~String()` destructor to delete the temporary object.

The simplest way to make the process more efficient is to overload the assignment operator so that it works directly with ordinary strings. This removes the extra steps of creating and destroying a temporary object. Here’s one possible implementation:

```cpp
String & String::operator=(const char * s)
{
    delete [] str;
    len = std::strlen(s);
    str = new char[len + 1];
    std::strcpy(str, s);
    return *this;
}
```

As usual, you must deallocate memory formerly managed by `str` and allocate enough memory for the new string.

Listing 12.4 shows the revised class declaration. In addition to the changes already mentioned, it defines the constant `CINLIM`, which is used in implementing `operator>>()`.

### Listing 12.4 **string1.h**

```cpp
// string1.h -- fixed and augmented string class definition

#ifndef STRING1_H
#define STRING1_H
#include <iostream>
using std::ostream;
using std::istream;

class String
{
private:
    char * str;             // pointer to string
    int len;                // length of string
    static int num_strings; // number of objects
    static const int CINLIM = 80; // cin input limit
public:
// constructors and other methods
    String(const char * s);       // constructor
    String();                     // default constructor
    String(const String &);       // copy constructor
    ~String();                   // destructor
    int length() const { return len; }
// overloaded operator methods
    String & operator=(const String &);
    String & operator=(const char *);
    char & operator[](int i);
    const char & operator[](int i) const;
// overloaded operator friends
    friend bool operator<(const String &st, const String &st2);
    friend bool operator>(const String &st, const String &st2);
    friend bool operator==(const String &st, const String &st2);
    friend ostream & operator<<(ostream & os, const String & st);
    friend istream & operator>>(istream & is, String & st);
// static function
    static int HowMany();
};
#endif
```

Listing 12.5 presents the revised method definitions.

### Listing 12.5 **string1.cpp**

```cpp
// string1.cpp -- String class methods
#include <cstring>              // string.h for some
#include "string1.h"            // includes <iostream>
```
