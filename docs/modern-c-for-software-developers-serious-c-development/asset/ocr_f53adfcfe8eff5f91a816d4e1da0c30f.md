# Modern C++: Raw Strings (C++11)

# Raw Strings

C++11 lets us define raw strings. A raw string is a sequence of characters that is interpreted literally; it does not have any characters that are interpreted specially. For example, the character pair \n in a raw string will not be interpreted as a newline.

The general syntax for a raw string is: R"(...)"

A raw string starts with R"(\ and ends with \)". The raw string is inside the parentheses. ( ) are the delimiters for the raw string. It can contain line breaks as well as other special characters which will be interpreted literally.

We can specify special delimiters for a raw string to handle quotation marks inside the parentheses.

A delimiter is a user-defined sequence of up to 16 characters that immediately precedes the opening parenthesis of a raw string, and immediately after the closing parenthesis. The delimiter must not include quotation marks. A delimiter marks the start and end of a raw string.

For example, in the expression:

```
R"abc{Hello\()}abc"
```

the delimiter is abc and the string content Hello"( is inside the parentheses.

Here is a raw string example:

```
#include <iostream>
using namespace std;
```