```
```cpp
using std::fixed;
using std::scientific;
using std::boolalpha;
}
```
```

Then a program could include this file and use the namespaces it needs:

```
```cpp
#include "mynames"
using namespace io;
```
```

# ## Use Smart Pointers

Each use of `new` should be paired with a use of `delete`. This can lead to problems if a function in which `new` is used terminates early via an exception being thrown. As discussed in Chapter 15, using an `auto_ptr` object to keep track of an object created by `new` automates the activation of `delete`. The C++11 additions `unique_ptr` and `shared_ptr` provide yet better alternatives.

# ## Use the *string* Class

The traditional C-style string suffers from not being a real type. You can store a string in a character array, and you can initialize a character array to a string. But you can't use the assignment operator to assign a string to a character array; instead, you must remember to use `strcpy()` or `strncpy()`. You can't use the relational operators to compare C-style strings; instead, you must remember to use `strcmp()`. (And if you forget and use, say, the `>` operator, you don't get a syntax error; instead, the program compares string addresses instead of string contents.)

The *string* class (see Chapter 16, “The *string* Class and the Standard Template Library,” and Appendix F, “The *string* Template Class”), on the other hand, lets you use objects to represent strings. Assignment operators, relational operators, and the addition operator (for concatenation) are all defined. Furthermore, the *string* class provides automatic memory management so that you normally don't have to worry about someone entering a string that either overruns an array or gets truncated before being stored.

The *string* class provides many convenience methods. For example, you can append one *string* object to another, but you can also append a C-style string or even a `char` value to a *string* object. For functions that require a C-style string argument, you can use the `c_str()` method to return a suitable pointer-to-char.

Not only does the *string* class provide a well-designed set of methods for handling string-related tasks, such as finding substrings, but it also features a design that is compatible with the Standard Template Library (STL) so that you can use STL algorithms with *string* objects.