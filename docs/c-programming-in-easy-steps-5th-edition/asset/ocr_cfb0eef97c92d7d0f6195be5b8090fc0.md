# Creating string variables

Unlike the **char**, **int**, **float**, **double**, and **bool** data types, there is no native “string” data type in C++ – but its **<string>** library class provides a **string** object that emulates a string data type. To make this available to a program, the library must be added with an **#include <string>** directive at the start of the program.

![](bbox=[0.118, 0.211, 0.197, 0.336])

Like the **<iostream>** class library, the **<string>** library is part of the **std** namespace that is used by the C++ standard library classes. This means that a string object can be referred to as **std::string**, or more simply as **string** when a **using namespace std;** directive is included at the start of the program.

Once the **<string>** library is made available, a **string** “variable” can be declared in the same way as other variables. The declaration may optionally initialize the variable using the **=** assignment operator, or it may be initialized later in the program.

Additionally, a **string** variable may be initialized by including a text string between parentheses after the variable name.

Text strings in C++ must always be enclosed within “ ” double quote characters – ‘ ’ single quotes are only used to surround character values of the **char** data type.

A C++ **string** variable is much easier to work with than the **char** arrays which C programmers must use, as it automatically resizes to accommodate the length of any text string. At a lower level, the text is still stored as a character array, but the **string** variable lets you ignore those details. Consequently, a character array can be assigned to a **string** variable using the **=** assignment operator.

It is important to remember that when numeric values are assigned to a **string** variable, they are no longer a numeric data type, so arithmetic cannot be performed on them. For example, attempting to add **string** values of “7” and “6” with the **+** addition operator produces the concatenated **string “76”**, not the numerical value of 13. In this case, the **+** operator recognizes that the context is not arithmetical, so adopts the guise of “concatenation operator” to unite the two strings. Similarly, the **+=** operator appends a **string** to another **string** and is useful to build long strings of text.

Several **string** values are built into a single long string in the example program described below.

![](bbox=[0.118, 0.738, 0.193, 0.783])

+   1. Start a new program by specifying the C++ library classes to include, and a namespace prefix to use

```
```cpp
#include <string>       // Include string support.
#include <iostream>
using namespace std;
```
```

+   2. Add a main function containing four **string** variable declarations and a final **return** statement

```
```cpp
int main()
```
```