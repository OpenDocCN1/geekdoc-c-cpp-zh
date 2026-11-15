The output from this program is

```
value of ch: 3; value of i: 3
value of ch: 3; value of i: 51
```

# String Data

string
C-style strings
string objects

A literal string constant is a sequence of characters enclosed within double quotes, as in "sensor", "F18", or "Jane Doe". String variables can be represented as C-style strings using arrays of type char, or as string objects using the string class. Both representations will be discussed in detail in Chapter 7. In this section, we give a brief introduction to the string class.

The C++ compiler does not have a built-in data type named string, but a string class definition is provided in the standard C++ library file string. To use the string class, a program must include the following preprocessor directive:

```
#include<string>
```

The following program illustrates the use of the predefined C++ string class:

```
/*-------------------------------------------*/
/* Program chapter2_2                         */
/*                                           */
/* This program prints a greeting            */
/* using the string class.                   */
/*-------------------------------------------*/

#include <iostream>   // Required for cout
#include <string>     // Required for string
using namespace std;

int main()
{
    // Declare and initialize two string objects.
    string salutation("Hello"), name("Jane Doe");

    // Output greeting.
    cout << salutation << ' ' << name << '!' << endl;

    // Exit program.
    return(0);
}
```

The output from this program is

```
Hello Jane Doe!
```

A memory snapshot of program chapter2_2 is provided below.

```
string salutation("Hello"), name("Jane Doe");
string salutation   Hello
string name         Jane Doe
```