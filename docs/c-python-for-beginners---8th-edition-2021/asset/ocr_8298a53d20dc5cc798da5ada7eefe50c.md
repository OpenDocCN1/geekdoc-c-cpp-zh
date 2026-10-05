# C++ Fundamentals

# Data Types

Variables, as we've seen, store information that the programmer can then call up, and manipulate if needed. Variables are simply reserved memory locations where the values the programmer assigns, depending on the data type used.

# THE VALUE OF DATA

There are many different data types available for the programmer in C++, such as integer, floating point, Boolean, character and so on. It's widely accepted that there are seven basic data types, often called Built-in Types; however, you can create your own data types as need arise within the code.
The seven basic data types are:

| TYPE | COMMAND |
|---|---|n| Integer | Integer |
| Floating Point | float |
| Character | char |
| Boolean | bool |
| Double Floating Point | double |
| Wide Character | char_t |
| No Value | void |

These basic types can also be extended using the following modifiers: Long, Short, and Signed. Basically this means they can expand the minimum and maximum range for each data type. For example, the int data type has a default range of -2147483648 to 2147483647, a fair value, you would agree.

Now, if you were to use one of the modifiers, the ranges alter:
ununsigned int = 0 to 4294967295
int = -2147483648 to 2147483647
short = -32768 to 32767
unsigned short = 0 to 65535
signed short = -32768 to 32767
int = -2147483648 to 2147483647
unsigned int = 0 to 4294967295

Naturally you can get away with using the basic type without the modifier, as there's plenty of range provided with each data type. However, it's good C++ programming practice to use the modifiers when needed.

There are issues when using the modifiers. Double represents a double-floating point, which you can use for

```
#include <iostream>
using namespace std;
double PI = 3.14159265358979323463;
int main() {
    cout << PI;
}
```

```
#include <iostream>
using namespace std;
double PI = 3.14159265358979323463;
int main() {
    cout << PI;
}
```

```
/* C:\Users\Documents\DataTypes.cpp */
Process returned (0) execution time: 0.054 s
Press any key to continue.
```

Build and run the code so you can see the output is 3.14159, representing double's limitations in precision.

You can also limit the code using the aforementioned cout.precision function, for greater accuracy. Precision all the way up to 22 decimal places, with the following code:

```
#include <iostream>
using namespace std;
double PI = 3.14159265358979323463;
int main() {
}
```