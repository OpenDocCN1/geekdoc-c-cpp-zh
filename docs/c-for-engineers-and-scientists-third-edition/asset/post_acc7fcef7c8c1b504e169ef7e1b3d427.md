
# Chapter 9

## 505
The string Class

### string Class Functions

The string class provides a number of functions for declaring, creating, and initializing a string. In earlier versions of C++, the process of creating a new object is referred to as instantiating an object, which in this case means reinstating a string object, or creating a string, for. Table 9.2 lists the string class functions for creating and initializing an object. In class terminology, functions are formally referred to as methods, and the methods that perform the tasks of creating and initializing are called constructor methods, or constructors, for.

Table 9.2 string Class Constructors (Require the Header File string)

| Constructor | Description | Examples |
|---|---|---|
| string objectName = value | Creates and initializes a string object to a value that can be a string literal, a previously declared string object, or an expression containing string literals and string objects | string1 = "Good Morning"; string2 = str1; string3 = str1 + |
| objectName(stringValue) | Produces the same initialization as the preceding item | string1("Hot"); string1(str1 + "Dog") |
| objectName(str, n) | Creates and initializes a string object with a substring of string object starting at index n of str | string1(str2, 5) If str2 contains the string Good Morning, then str1 becomes the string Morning |
| objectName(str, n, p) | Creates and initializes a string object with a substring of string object starting at index n of str and containing p characters | string1(str2, 5, 2) If str2 contains the string Good Morning, then str1 becomes the string |
| objectName(n, char) | Creates and initializes a string object with n copies of char | string1(5,'*') This makes str1 = ***** |

## 506 Completing the Basics

**Table 9.2** string Class Constructors (Require the Header File string) (continued)

| Constructor | Description | Examples |
| --- | --- | --- |
| string objectName | Creates and initializes a string object to represent an empty character sequence (same as string objectName = ""; so length of the string is 0) | string message; |

Program 9.6 shows examples of each constructor the string class provides.

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_525_0.png)

# Program 9.6

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string str1; // an empty string
    string str2("Good Morning");
    string str3 = "Hot Dog";
    string str4(str3);
    string str5(str4, 4);
    string str6 = "linear";
    string str7(str6, 3, 3);

    cout << "str1 is: " << str1 << endl;
    cout << "str2 is: " << str2 << endl;
    cout << "str3 is: " << str3 << endl;
    cout << "str4 is: " << str4 << endl;
    cout << "str5 is: " << str5 << endl;
    cout << "str6 is: " << str6 << endl;
    cout << "str7 is: " << str7 << endl;

    return 0;
}
```

## Chapter 9 507

Here is the output created by Program 9.6:

```
str1 is:
str2 is: Good Morning
str3 is: Hot Dog
str4 is: Hot Dog
str5 is: Dog
str6 is: linear
str7 is: ear
```

Although this output is straightforward, str1 is an empty string consisting of no characters; because the first character in a string is designated as position 0, not 1, the character position of the D in the string Dog is position 4, which is shown in Figure 9.4.

| Character position: 0 | 1 | 2 | 3 | 4 | 5 | 6 |
|---|---|---|---|---|---|---|---|
| | H | o | t | | D | | g |

**Figure 9.4** The character positions of the string Dog

## String Input and Output

In addition to a string initialized with the constructors listed in Table 9.2, strings can be input from the keyboard and displayed on screen. Table 9.3 lists the basic functions and objects for input and output of string values.

## 9.3 string Class Input and Output

| C++ Object or Function | Description |
|---|---|
| cout | General-purpose screen output object |
| cin | General-purpose keyboard input object that stops reading input when white space is |
| getline(cin, strobj) | General-purpose keyboard input function that inputs all characters, stores them in the string strobj, and stops accepting characters when it receives a newline character \n |

In addition to the standard cout and cin you have been using throughout the book, the string uses getline() function for string input. For example, the expression getline(cin, message) accepts stores characters typed at the terminal continuously until the Enter is pressed. The Enter key generates a newline character, '\n', while getline() interprets the end-of-line input. All the characters encountered by getline(), except the newline character, are stored in the string message, as illustrated in Figure 9.5.

Program 9.7 shows using the getline() function and cout statement to input and output a string that's entered at the user's terminal. Although cout is used in Program 9.7 for string output, cin generally can't be used in place of getline() for string input because cin reads a set of characters until a blank space or newline character. Therefore, attempting to enter the characters This is a string by using the statement cin >> message; results in only the

## 508 Completing the Basics

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_527_0.png)

**Figure 9.5** Inputting a string with getline()

word This being assigned to message. Because a blank terminates a cin extraction operation, cin's usefulness for entering string data is restricted; therefore, getline() is used.

# Program 9.7

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string message;                // declare a string object

    cout << "Enter a string:\n";

    getline(cin, message);

    cout << "The string just entered is:\n"
    << message << endl;

    return 0;
}
```

The following is a sample run of Program 9.7:

Enter the string:
This is a test input of a string of characters.
The string just entered is:
This is a test input of a string of characters.

In its most general form, the getline() function has the syntax

getline(cin, strObj, terminatingChar)
where strObj is a variable name and terminatingChar is an optional constant, or variable, specifying the terminating character. For example, the expression getline(cin, message, "!!") accepts all characters entered at the keyboard, including a newline character, until an exclamation point is entered. The exclamation point isn't stored as part of the string.

## Chapter 9 509

If the optional argument, `terminatingChar`, is omitted when getline() is called, the default terminating character is the newline ('\n') character. Therefore, the statement `getline(cin, message, '\n')` can be used in place of the statement `getline(cin, message);`. Both these stop reading characters when the Enter key is pressed. In all the programs used from this point forward, input is terminated by pressing the Enter key. For this reason, the third argument passed to `getline()`, which is the terminating character, is omitted.

**Caution: The Phantom Character** Seemingly strange results can happen when the cin input stream object and getline() are used together to accept data or when cin is used by itself to accept characters. To see how this occur, take a look at Program 9.8, which uses cin to accept an integer entered at the keyboard. The integer is stored in the variable value, and a getline() function follows.

# Program 9.8

![](img/e2a849fc7bc04aa2e6669ad865e0c22b_528_0.png)

```cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
    int value;
    string message;

    cout << "Enter a number: ";
    cin >> value;
    cout << "The number entered is:\n"
         << value << endl;

    cout << "Enter text:\n";
    getline(cin, message);
    cout << "The text entered is:\n"
         << message << endl;
    cout << int(message.length()) << endl;

    return 0;
}
```

When Program 9.8 runs, the number entered in response to the prompt Enter a number: is stored in the variable value. At this point, everything seems to be working fine. Notice, however, that in entering a number, you enter the number and press the Enter key. On almost all computer systems, this entered data is stored in a temporary holding area called immediately after the characters are entered, as shown in Figure 9.6.
