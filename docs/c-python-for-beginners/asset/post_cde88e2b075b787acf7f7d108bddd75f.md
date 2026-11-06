
## Data Types

Variables, as we've seen, store information that the programmer can then later call up, and manipulate if required. Variables are simply reserved memory locations that store the values the programmer assigns, depending on the data type used.

### THE VALUE OF DATA

There are many different data types available for the programmer in C++, such as an integer, floating point, Boolean, character and so on. It's widely accepted that there are seven basic data types, often called Primitive Built-In Types; however, you can create your own data types should the need ever arise within your code.

The seven basic data types are:

| TYPE | COMMAND |
|---|---|
| Integer | int |
| Floating Point | float |
| Character | char |
| Boolean | bool |
| Double Floating Point | double |
| Wide Character | wchar_t |
| No Value | void |

These basic types can also be extended using the following modifiers: Long, Short, Signed and Unsigned. Basically, this means the modifiers can expand the minimum and maximum range values for each data type. For example, the int data type has a default value range of -2147483648 to 2147483647, a fair value, you would agree.

Now, if you were to use one of the modifiers, the range alters:

- Unsigned int = 0 to 4294967295
- Signed int = -2147483648 to 2147483647
- Short int = -32768 to 32767
- Unsigned Short int = 0 to 65535
- Signed Short int = -32768 to 32767
- Long int = -2147483647 to 2147483647
- Signed Long int = -2147483647 to 2147483647
- Unsigned Long int = 0 to 4294967295

Naturally you can get away with using the basic type without the modifier, as there's plenty of range provided with each data type. However, it's considered good C++ programming practice to use the modifiers when possible.

There are issues when using the modifiers though. Double represents a double floating point value, which you can use for incredibly accurate numbers but those numbers are only accurate up to the fifteenth decimal place. There's also the problem when displaying such numbers in C++ using the cout function, in that cout by default only outputs the first five decimal places. You can combat that by adding a cout.precision() function and adding a value inside the brackets, but even then you're still limited by the accuracy of the double data type. For example, try this code:

```cpp
#include <iostream>
using namespace std;
double PI = 3.141592653589793238463;
int main()
{
    cout << PI;
}
```

![](img/840275566c862102888f27d8ae2ac921_69_0.png)

Build and run the code, and as you can see, the output is only 3.14159, representing cout's limitations in this example.

You can also alter the code including the aforementioned cout.precision function, for greater accuracy. Take precision all the way up to 22 decimal places, with the following code:

```cpp
#include <iostream>
using namespace std;
double PI = 3.141592653589793238463;
int main()
{
    cout.precision(22);
    cout << PI;
}
```

![](img/840275566c862102888f27d8ae2ac921_70_0.png)

This is mainly due to the conversion from binary in the compiler and that the IEEE 754 double precision standard occupies 64-bits of data, of which 52-bits are dedicated to the significand (the significant digits in a floating-point number) and roughly 3.5-bits are taken holding the values 0 to 9. If you divide 53 by 3.5, then you arrive at 15.142857 recurring, which is 15-digits of precision.

To be honest, if you’re creating code that needs to be accurate to more than fifteen decimal places, then you wouldn’t be using C++, you would use some scientific specific language with C++ as the connective tissue between the two languages.

You can create your own data types, using an alias-like system called typedef. For example:

![](img/840275566c862102888f27d8ae2ac921_70_1.png)

Again, build and run the code; as you can see from the command line window, the number represented by the variable PI is different to the number you’ve told C++ to use in the variable. The output reads the value of PI as 3.141592653589793115998, with the numbers going awry from the fifteenth decimal place.

![](img/840275566c862102888f27d8ae2ac921_70_2.png)

![](img/840275566c862102888f27d8ae2ac921_70_3.png)

```cpp
#include <iostream>
using namespace std;
typedef int metres;

int main()
{
    metres distance;
    distance = 15;
    cout << "distance in metres is: " << distance;
}
```

![](img/840275566c862102888f27d8ae2ac921_70_4.png)

This code when executed creates a new int data type called metres. Then, in the main code block, there’s a new variable called distance, which is an integer; so you’re basically telling the compiler that there’s another name for int. We assigned the value 15 to distance and displayed the output: distance in metres is 15.

It might sound a little confusing to begin with but the more you use C++ and create your own code, the easier it becomes.

## Strings

Strings are objects that represent and hold sequences of characters. For example, you could have a universal greeting in your code “Welcome” and assign that as a string to be called up whenever you like in the program.

### STRING THEORY

There are different ways in which you can create a string of characters, which historically are all carried over from the original C language, and are still supported by C++.

### STEP 1

To create a string you use the char function. Open a new C++ file and begin with the usual header:

```cpp
#include <iostream>
using namespace std;

int main()
{
}
```

![](img/840275566c862102888f27d8ae2ac921_71_0.png)

### STEP 2

It’s easy to confuse a string with an array. Here’s an array, which can be terminated with a null character:

```cpp
#include <iostream>
using namespace std;

int main()
{
    char greet[8] = {'W', 'e', 'l', 'c', 'o', 'm', 'e', '\0'};
    cout << greet << "\n";
}
```

![](img/840275566c862102888f27d8ae2ac921_71_1.png)

### STEP 3

Build and run the code, and ‘Welcome’ appears not a string. A string is a class, which defines objects that can be represented as a stream of characters and doesn’t need to be terminated like an array. The code can therefore be represented as:

```cpp
#include <iostream>
using namespace std;

int main()
{
    char greet[] = "Welcome";
    cout << greet << "\n";
}
```

![](img/840275566c862102888f27d8ae2ac921_71_2.png)

### STEP 4

In C++ there’s also a string function, which works in much the same way. Using the greeting code again, you can enter:

```cpp
#include <iostream>
using namespace std;

int main()
{
    string greet = "Welcome";
    cout << greet << "\n";
}
```

![](img/840275566c862102888f27d8ae2ac921_71_3.png)

### STEP 5

There are also many different operations that you can apply with the string function. For instance, to get the length of a string you can use:

```cpp
#include <iostream>
using namespace std;
int main()
{
    string greet = "Welcome";
    cout << "The length of the string is: ";
    cout << greet.size() << "\n";
}
```

![](img/840275566c862102888f27d8ae2ac921_72_0.png)

### STEP 6

You can see that we used greet.size() to output the length, the number of characters there are, of the contents of the string. Naturally, if you call your string something other than greet, then you need to change the command to reflect this. It's always stringname.operation. Build and run the code to see the results.

![](img/840275566c862102888f27d8ae2ac921_72_1.png)

### STEP 7

You can of course add strings together, or rather combine them to form longer strings:

```cpp
#include <iostream>
using namespace std;
int main()
{
    string greet1 = "Hello";
    string greet2 = ", world!";
    string greet3 = greet1 + greet2;
    cout << greet3 << "\n";
}
```

![](img/840275566c862102888f27d8ae2ac921_72_2.png)

### STEP 8

Just as you might expect, you can mix in an integer and store something to do with the string. In this example, we created int length, which stores the result of string.size() and outputs it to the user.

```cpp
#include <iostream>
using namespace std;
int main()
{
    int length;
    string greet1 = "Hello";
    string greet2 = ", world!";
    string greet3 = greet1 + greet2;
    length = greet3.size();
    cout << "The length of the combined strings is: " << length << "\n";
}
```

### STEP 9

Using the available operations that come with the string function, you can manipulate the contents of a string. For example, to remove characters from a string you could use:

```cpp
#include <iostream>
using namespace std;
int main()
{
    string str ("Here is a long sentence in a string.");
    cout << str << '\n';
    str.erase (10,5);
    cout << str << '\n';
    str.erase (str.begin()+8);
    cout << str << '\n';
    str.erase (str.begin()+9, str.end()-9);
    cout << str << '\n';
}
```

### STEP 10

It's worth spending some time playing around with the numbers, which are the character positions in the string. Occasionally, it can be hit and miss whether you get it right, so practice makes perfect. Take a look at the screenshot to see the result of the code.

![](img/840275566c862102888f27d8ae2ac921_72_3.png)
