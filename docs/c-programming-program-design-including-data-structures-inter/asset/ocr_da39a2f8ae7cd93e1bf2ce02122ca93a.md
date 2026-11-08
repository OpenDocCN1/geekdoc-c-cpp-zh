The stream function putback lets you put the last character extracted from the input stream by the get function back into the input stream. The stream function peek looks into the input stream and tells you what the next character is without removing it from the input stream. By using these functions, after determining that the next input is a number, you can read it as a number. You do not have to read the digits of the number as characters and then convert these characters to that number.

The syntax to use the function putback is:

```
```cpp
istreamVar.putback(ch);
```
```

Here, istreamVar is an input stream variable, such as cin, and ch is a char variable.

The peek function returns the next character from the input stream but does not remove the character from that stream. In other words, the function peek looks into the input stream and checks the identity of the next input character. Moreover, after checking the next input character in the input stream, it can store this character in a designated memory location without removing it from the input stream. That is, when you use the peek function, the next input character stays the same, even though you now know what it is.

The syntax to use the function peek is:

```
```cpp
ch = istreamVar.peek();
```
```

Here, istreamVar is an input stream variable, such as cin, and ch is a char variable.

Notice how the function peek is used. First, the function peek is used in an assignment statement. It is not a stand-alone statement like get, ignore, and putback. Second, the function peek has empty parentheses. Until you become comfortable with using a function and learn how to write one, pay close attention to how to use a predefined function.

The following example illustrates how to use the peek and putback functions.

# **EXAMPLE 3-7**

```
```cpp
//Functions peek and putback

#include <iostream>

using namespace std;

int main()
{
    char ch;

    cout << "Line 1: Enter a string: ";        //Line 1
    cin.get(ch);                               //Line 2
    cout << endl;                              //Line 3
```
```