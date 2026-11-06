# Syntax 1.2　Output Statement

![](bbox=[0.284, 0.126, 0.924, 0.334])

Enclose text strings in quotation marks.

The statement

```
```cpp
cout << "Hello";
```
```

displays the string Hello. A string is a sequence of characters. You must enclose the contents of a string inside quotation marks so that the compiler knows you literally mean the text "Hello" and not a function with the same name.

Use + to add two numbers and * to multiply two numbers.

You can send more than one item to cout. Use a << before each one of them. For example,

```
```cpp
cout << "The answer is " << 6 * 7;
```
```

displays The answer is 42 (in C++, the * denotes multiplication).

Send endl to cout to end a line of displayed output.

The end symbol denotes an end of line marker. When this marker is sent to cout, the cursor is moved to the first column in the next screen row. If you don’t use an end of line marker, then the next displayed item will simply follow the current string on the same line. In this program we printed one item, but in general we will want to print multiple items, and it is a good habit to end all lines of output with an end of line marker.

End each statement with a semicolon.

Finally, note that each statement in C++ ends in a semicolon, just as every English sentence ends in a period.

![](bbox=[0.122, 0.689, 0.27, 0.777])

+   12. How do you modify the `hello.cpp` program to greet you instead?
+   13. What is wrong with this program?

```
```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << Goodbye, World! << endl;
    return 0;
}
```
```

+   14. What does the following sequence of statements print?

```
```cpp
cout << "Hello";
cout << "World";
```
```